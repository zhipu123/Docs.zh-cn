---
title: "通过在 ASP.NET Core LoggerMessage 的高性能日志记录"
author: guardrex
description: "了解如何使用 LoggerMessage 功能来创建可缓存于高性能日志记录方案需要较少的对象分配比记录器扩展方法的委托。"
ms.author: riande
manager: wpickett
ms.date: 11/03/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: fundamentals/logging/loggermessage
ms.openlocfilehash: defba75c6c9ea13d24af4cd8515d82d9e7cf9853
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2017
---
# <a name="high-performance-logging-with-loggermessage-in-aspnet-core"></a><span data-ttu-id="4d82c-103">通过在 ASP.NET Core LoggerMessage 的高性能日志记录</span><span class="sxs-lookup"><span data-stu-id="4d82c-103">High-performance logging with LoggerMessage in ASP.NET Core</span></span>

<span data-ttu-id="4d82c-104">作者：[Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="4d82c-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="4d82c-105">[LoggerMessage](/dotnet/api/microsoft.extensions.logging.loggermessage)功能创建一个可缓存委托需要较少的对象分配，并减少计算开销比[记录器扩展方法](/dotnet/api/Microsoft.Extensions.Logging.LoggerExtensions)，如`LogInformation`， `LogDebug`，和`LogError`.</span><span class="sxs-lookup"><span data-stu-id="4d82c-105">[LoggerMessage](/dotnet/api/microsoft.extensions.logging.loggermessage) features create cacheable delegates that require fewer object allocations and reduced computational overhead than [logger extension methods](/dotnet/api/Microsoft.Extensions.Logging.LoggerExtensions), such as `LogInformation`, `LogDebug`, and `LogError`.</span></span> <span data-ttu-id="4d82c-106">对于高性能日志记录方案，使用`LoggerMessage`模式。</span><span class="sxs-lookup"><span data-stu-id="4d82c-106">For high-performance logging scenarios, use the `LoggerMessage` pattern.</span></span>

<span data-ttu-id="4d82c-107">`LoggerMessage`提供了相对记录器扩展方法的以下性能优势：</span><span class="sxs-lookup"><span data-stu-id="4d82c-107">`LoggerMessage` provides the following performance advantages over Logger extension methods:</span></span>

* <span data-ttu-id="4d82c-108">记录器扩展方法要求使用"装箱"（转换） 的值类型，如`int`，到`object`。</span><span class="sxs-lookup"><span data-stu-id="4d82c-108">Logger extension methods require "boxing" (converting) value types, such as `int`, into `object`.</span></span> <span data-ttu-id="4d82c-109">`LoggerMessage`模式通过使用静态来避免装箱`Action`字段和具有强类型参数的扩展方法。</span><span class="sxs-lookup"><span data-stu-id="4d82c-109">The `LoggerMessage` pattern avoids boxing by using static `Action` fields and extension methods with strongly-typed parameters.</span></span>
* <span data-ttu-id="4d82c-110">记录器扩展方法必须分析每次写入日志消息的消息模板 （命名的格式字符串）。</span><span class="sxs-lookup"><span data-stu-id="4d82c-110">Logger extension methods must parse the message template (named format string) every time a log message is written.</span></span> <span data-ttu-id="4d82c-111">`LoggerMessage`只需一次分析模板时定义该消息。</span><span class="sxs-lookup"><span data-stu-id="4d82c-111">`LoggerMessage` only requires parsing a template once when the message is defined.</span></span>

<span data-ttu-id="4d82c-112">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/logging/loggermessage/sample/)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="4d82c-112">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/logging/loggermessage/sample/) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

<span data-ttu-id="4d82c-113">示例应用演示`LoggerMessage`功能跟踪系统的基本引号。</span><span class="sxs-lookup"><span data-stu-id="4d82c-113">The sample app demonstrates `LoggerMessage` features with a basic quote tracking system.</span></span> <span data-ttu-id="4d82c-114">应用程序添加和删除使用内存中数据库的引号。</span><span class="sxs-lookup"><span data-stu-id="4d82c-114">The app adds and deletes quotes using an in-memory database.</span></span> <span data-ttu-id="4d82c-115">这些操作出现时，使用生成日志消息`LoggerMessage`模式。</span><span class="sxs-lookup"><span data-stu-id="4d82c-115">As these operations occur, log messages are generated using the `LoggerMessage` pattern.</span></span>

## <a name="loggermessagedefine"></a><span data-ttu-id="4d82c-116">LoggerMessage.Define</span><span class="sxs-lookup"><span data-stu-id="4d82c-116">LoggerMessage.Define</span></span>

<span data-ttu-id="4d82c-117">[定义 （LogLevel，EventId，字符串）](/dotnet/api/microsoft.extensions.logging.loggermessage.define)创建`Action`日志记录消息的委托。</span><span class="sxs-lookup"><span data-stu-id="4d82c-117">[Define(LogLevel, EventId, String)](/dotnet/api/microsoft.extensions.logging.loggermessage.define) creates an `Action` delegate for logging a message.</span></span> <span data-ttu-id="4d82c-118">`Define`重载允许将最多六个类型参数传递给命名的格式字符串 （模板）。</span><span class="sxs-lookup"><span data-stu-id="4d82c-118">`Define` overloads permit passing up to six type parameters to a named format string (template).</span></span>

## <a name="loggermessagedefinescope"></a><span data-ttu-id="4d82c-119">LoggerMessage.DefineScope</span><span class="sxs-lookup"><span data-stu-id="4d82c-119">LoggerMessage.DefineScope</span></span>

<span data-ttu-id="4d82c-120">[DefineScope(String)](/dotnet/api/microsoft.extensions.logging.loggermessage.definescope)创建`Func`定义的委托[日志范围](xref:fundamentals/logging/index#log-scopes)。</span><span class="sxs-lookup"><span data-stu-id="4d82c-120">[DefineScope(String)](/dotnet/api/microsoft.extensions.logging.loggermessage.definescope) creates a `Func` delegate for defining a [log scope](xref:fundamentals/logging/index#log-scopes).</span></span> <span data-ttu-id="4d82c-121">`DefineScope`重载允许将最多三个类型参数传递给命名的格式字符串 （模板）。</span><span class="sxs-lookup"><span data-stu-id="4d82c-121">`DefineScope` overloads permit passing up to three type parameters to a named format string (template).</span></span>

## <a name="message-template-named-format-string"></a><span data-ttu-id="4d82c-122">消息模板 （名为格式字符串）</span><span class="sxs-lookup"><span data-stu-id="4d82c-122">Message template (named format string)</span></span>

<span data-ttu-id="4d82c-123">到提供的字符串`Define`和`DefineScope`方法是一个模板，而不相比内, 插的字符串。</span><span class="sxs-lookup"><span data-stu-id="4d82c-123">The string provided to the `Define` and `DefineScope` methods is a template and not an interpolated string.</span></span> <span data-ttu-id="4d82c-124">占位符将填充的类型指定的顺序。</span><span class="sxs-lookup"><span data-stu-id="4d82c-124">Placeholders are filled in the order that the types are specified.</span></span> <span data-ttu-id="4d82c-125">在模板中的占位符名称应为在模板具说明性且更一致。</span><span class="sxs-lookup"><span data-stu-id="4d82c-125">Placeholder names in the template should be descriptive and consistent across templates.</span></span> <span data-ttu-id="4d82c-126">用作结构化的日志数据中的属性名称。</span><span class="sxs-lookup"><span data-stu-id="4d82c-126">They serve as property names within structured log data.</span></span> <span data-ttu-id="4d82c-127">我们建议[Pascal 大小写](/dotnet/standard/design-guidelines/capitalization-conventions)的占位符名称。</span><span class="sxs-lookup"><span data-stu-id="4d82c-127">We recommend [Pascal casing](/dotnet/standard/design-guidelines/capitalization-conventions) for placeholder names.</span></span> <span data-ttu-id="4d82c-128">例如， `{Count}`， `{FirstName}`。</span><span class="sxs-lookup"><span data-stu-id="4d82c-128">For example, `{Count}`, `{FirstName}`.</span></span>

## <a name="implementing-loggermessagedefine"></a><span data-ttu-id="4d82c-129">实现 LoggerMessage.Define</span><span class="sxs-lookup"><span data-stu-id="4d82c-129">Implementing LoggerMessage.Define</span></span>

<span data-ttu-id="4d82c-130">每条日志消息是`Action`中创建的某个静态字段保存`LoggerMessage.Define`。</span><span class="sxs-lookup"><span data-stu-id="4d82c-130">Each log message is an `Action` held in a static field created by `LoggerMessage.Define`.</span></span> <span data-ttu-id="4d82c-131">例如，示例应用程序创建一个字段，以描述索引页 GET 请求的日志消息 (*Internal/LoggerExtensions.cs*):</span><span class="sxs-lookup"><span data-stu-id="4d82c-131">For example, the sample app creates a field to describe a log message for a GET request for the Index page (*Internal/LoggerExtensions.cs*):</span></span>

[!code-csharp[Main](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet1)]

<span data-ttu-id="4d82c-132">有关`Action`，指定：</span><span class="sxs-lookup"><span data-stu-id="4d82c-132">For the `Action`, specify:</span></span>

* <span data-ttu-id="4d82c-133">日志级别。</span><span class="sxs-lookup"><span data-stu-id="4d82c-133">The log level.</span></span>
* <span data-ttu-id="4d82c-134">唯一的事件标识符 ([EventId](/dotnet/api/microsoft.extensions.logging.eventid)) 替换为静态的扩展方法的名称。</span><span class="sxs-lookup"><span data-stu-id="4d82c-134">A unique event identifier ([EventId](/dotnet/api/microsoft.extensions.logging.eventid)) with the name of the static extension method.</span></span>
* <span data-ttu-id="4d82c-135">消息模板 （名为格式字符串）。</span><span class="sxs-lookup"><span data-stu-id="4d82c-135">The message template (named format string).</span></span> 

<span data-ttu-id="4d82c-136">示例应用程序集的索引页的请求:</span><span class="sxs-lookup"><span data-stu-id="4d82c-136">A request for the Index page of the sample app sets the:</span></span>

* <span data-ttu-id="4d82c-137">日志级别设置为`Information`。</span><span class="sxs-lookup"><span data-stu-id="4d82c-137">Log level to `Information`.</span></span>
* <span data-ttu-id="4d82c-138">事件 id`1`同名的`IndexPageRequested`方法。</span><span class="sxs-lookup"><span data-stu-id="4d82c-138">Event id to `1` with the name of the `IndexPageRequested` method.</span></span>
* <span data-ttu-id="4d82c-139">消息模板 （名为格式字符串） 为字符串。</span><span class="sxs-lookup"><span data-stu-id="4d82c-139">Message template (named format string) to a string.</span></span>

[!code-csharp[Main](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet5)]

<span data-ttu-id="4d82c-140">提供使用事件 id 来丰富日志记录时，结构化日志记录存储区可能使用的事件名称。</span><span class="sxs-lookup"><span data-stu-id="4d82c-140">Structured logging stores may use the event name when it's supplied with the event id to enrich logging.</span></span> <span data-ttu-id="4d82c-141">例如， [Serilog](https://github.com/serilog/serilog-extensions-logging)使用事件名称。</span><span class="sxs-lookup"><span data-stu-id="4d82c-141">For example, [Serilog](https://github.com/serilog/serilog-extensions-logging) uses the event name.</span></span>

<span data-ttu-id="4d82c-142">`Action`通过强类型扩展方法调用。</span><span class="sxs-lookup"><span data-stu-id="4d82c-142">The `Action` is invoked through a strongly-typed extension method.</span></span> <span data-ttu-id="4d82c-143">`IndexPageRequested`方法的示例应用中记录为索引页 GET 请求消息：</span><span class="sxs-lookup"><span data-stu-id="4d82c-143">The `IndexPageRequested` method logs a message for an Index page GET request in the sample app:</span></span>

[!code-csharp[Main](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet9)]

<span data-ttu-id="4d82c-144">`IndexPageRequested`在中记录器上调用`OnGetAsync`中的方法*Pages/Index.cshtml.cs*:</span><span class="sxs-lookup"><span data-stu-id="4d82c-144">`IndexPageRequested` is called on the logger in the `OnGetAsync` method in *Pages/Index.cshtml.cs*:</span></span>

[!code-csharp[Main](loggermessage/sample/Pages/Index.cshtml.cs?name=snippet2&highlight=3)]

<span data-ttu-id="4d82c-145">检查应用程序的控制台输出：</span><span class="sxs-lookup"><span data-stu-id="4d82c-145">Inspect the app's console output:</span></span>

```console
info: LoggerMessageSample.Pages.IndexModel[1]
      => RequestId:0HL90M6E7PHK4:00000001 RequestPath:/ => /Index
      GET request for Index page
```

<span data-ttu-id="4d82c-146">若要将参数传递给一条日志消息，请创建静态字段时定义最多六个类型。</span><span class="sxs-lookup"><span data-stu-id="4d82c-146">To pass parameters to a log message, define up to six types when creating the static field.</span></span> <span data-ttu-id="4d82c-147">当通过定义添加引号示例应用程序日志，string`string`键入`Action`字段：</span><span class="sxs-lookup"><span data-stu-id="4d82c-147">The sample app logs a string when adding a quote by defining a `string` type for the `Action` field:</span></span>

[!code-csharp[Main](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet2)]

<span data-ttu-id="4d82c-148">该委托的日志消息模板提供的类型从接收其占位符值。</span><span class="sxs-lookup"><span data-stu-id="4d82c-148">The delegate's log message template receives its placeholder values from the types provided.</span></span> <span data-ttu-id="4d82c-149">示例应用程序定义委托的添加引号参数所在的引号`string`:</span><span class="sxs-lookup"><span data-stu-id="4d82c-149">The sample app defines a delegate for adding a quote where the quote parameter is a `string`:</span></span>

[!code-csharp[Main](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet6)]

<span data-ttu-id="4d82c-150">用于添加引号、 静态的扩展方法`QuoteAdded`、 接收报价自变量值并将其传递给`Action`委托：</span><span class="sxs-lookup"><span data-stu-id="4d82c-150">The static extension method for adding a quote, `QuoteAdded`, receives the quote argument value and passes it to the `Action` delegate:</span></span>

[!code-csharp[Main](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet10)]

<span data-ttu-id="4d82c-151">索引页的代码隐藏文件中 (*Pages/Index.cshtml.cs*)，`QuoteAdded`调用来记录消息：</span><span class="sxs-lookup"><span data-stu-id="4d82c-151">In the Index page's code-behind file (*Pages/Index.cshtml.cs*), `QuoteAdded` is called to log the message:</span></span>

[!code-csharp[Main](loggermessage/sample/Pages/Index.cshtml.cs?name=snippet3&highlight=6)]

<span data-ttu-id="4d82c-152">检查应用程序的控制台输出：</span><span class="sxs-lookup"><span data-stu-id="4d82c-152">Inspect the app's console output:</span></span>

```console
info: LoggerMessageSample.Pages.IndexModel[2]
      => RequestId:0HL90M6E7PHK5:0000000A RequestPath:/ => /Index
      Quote added (Quote = 'You can avoid reality, but you cannot avoid the consequences of avoiding reality. - Ayn Rand')
```

<span data-ttu-id="4d82c-153">本示例应用程序实现`try` &ndash; `catch`引号删除模式。</span><span class="sxs-lookup"><span data-stu-id="4d82c-153">The sample app implements a `try`&ndash;`catch` pattern for quote deletion.</span></span> <span data-ttu-id="4d82c-154">一条信息性消息只记录成功的删除操作。</span><span class="sxs-lookup"><span data-stu-id="4d82c-154">An informational message is logged for a successful delete operation.</span></span> <span data-ttu-id="4d82c-155">引发异常时，将删除操作的记录一条错误消息。</span><span class="sxs-lookup"><span data-stu-id="4d82c-155">An error message is logged for a delete operation when an exception is thrown.</span></span> <span data-ttu-id="4d82c-156">日志消息的不成功，则删除操作包括异常堆栈跟踪 (*Internal/LoggerExtensions.cs*):</span><span class="sxs-lookup"><span data-stu-id="4d82c-156">The log message for the unsuccessful delete operation includes the exception stack trace (*Internal/LoggerExtensions.cs*):</span></span>

[!code-csharp[Main](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet3)]

[!code-csharp[Main](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet7)]

<span data-ttu-id="4d82c-157">请注意如何将异常传递给该委托`QuoteDeleteFailed`:</span><span class="sxs-lookup"><span data-stu-id="4d82c-157">Note how the exception is passed to the delegate in `QuoteDeleteFailed`:</span></span>

[!code-csharp[Main](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet11)]

<span data-ttu-id="4d82c-158">索引页代码隐藏文件中，成功引号删除调用`QuoteDeleted`记录器方法。</span><span class="sxs-lookup"><span data-stu-id="4d82c-158">In the Index page code-behind, a successful quote deletion calls the `QuoteDeleted` method on the logger.</span></span> <span data-ttu-id="4d82c-159">当为删除，找不到有引号`ArgumentNullException`引发。</span><span class="sxs-lookup"><span data-stu-id="4d82c-159">When a quote isn't found for deletion, an `ArgumentNullException` is thrown.</span></span> <span data-ttu-id="4d82c-160">通过捕获异常`try` &ndash; `catch`语句，并通过调用记录`QuoteDeleteFailed`方法中记录器`catch`块 (*Pages/Index.cshtml.cs*):</span><span class="sxs-lookup"><span data-stu-id="4d82c-160">The exception is trapped by the `try`&ndash;`catch` statement and logged by calling the `QuoteDeleteFailed` method on the logger in the `catch` block (*Pages/Index.cshtml.cs*):</span></span>

[!code-csharp[Main](loggermessage/sample/Pages/Index.cshtml.cs?name=snippet5&highlight=14,18)]

<span data-ttu-id="4d82c-161">在成功删除引号，检查应用程序的控制台输出：</span><span class="sxs-lookup"><span data-stu-id="4d82c-161">When a quote is successfully deleted, inspect the app's console output:</span></span>

```console
info: LoggerMessageSample.Pages.IndexModel[4]
      => RequestId:0HL90M6E7PHK5:00000016 RequestPath:/ => /Index
      Quote deleted (Quote = 'You can avoid reality, but you cannot avoid the consequences of avoiding reality. - Ayn Rand' Id = 1)
```

<span data-ttu-id="4d82c-162">当引号删除失败时，检查应用程序的控制台输出。</span><span class="sxs-lookup"><span data-stu-id="4d82c-162">When quote deletion fails, inspect the app's console output.</span></span> <span data-ttu-id="4d82c-163">请注意，日志消息中包含的异常：</span><span class="sxs-lookup"><span data-stu-id="4d82c-163">Note that the exception is included in the log message:</span></span>

```console
fail: LoggerMessageSample.Pages.IndexModel[5]
      => RequestId:0HL90M6E7PHK5:00000010 RequestPath:/ => /Index
      Quote delete failed (Id = 999)
System.ArgumentNullException: Value cannot be null.
Parameter name: entity
   at Microsoft.EntityFrameworkCore.Utilities.Check.NotNull[T](T value, String parameterName)
   at Microsoft.EntityFrameworkCore.DbContext.Remove[TEntity](TEntity entity)
   at Microsoft.EntityFrameworkCore.Internal.InternalDbSet`1.Remove(TEntity entity)
   at LoggerMessageSample.Pages.IndexModel.<OnPostDeleteQuoteAsync>d__14.MoveNext() in 
      <PATH>\sample\Pages\Index.cshtml.cs:line 87
```

## <a name="implementing-loggermessagedefinescope"></a><span data-ttu-id="4d82c-164">实现 LoggerMessage.DefineScope</span><span class="sxs-lookup"><span data-stu-id="4d82c-164">Implementing LoggerMessage.DefineScope</span></span>

<span data-ttu-id="4d82c-165">定义[日志范围](xref:fundamentals/logging/index#log-scopes)要应用于使用的日志消息的一系列[DefineScope(String)](/dotnet/api/microsoft.extensions.logging.loggermessage.definescope)方法。</span><span class="sxs-lookup"><span data-stu-id="4d82c-165">Define a [log scope](xref:fundamentals/logging/index#log-scopes) to apply to a series of log messages using the [DefineScope(String)](/dotnet/api/microsoft.extensions.logging.loggermessage.definescope) method.</span></span>

<span data-ttu-id="4d82c-166">示例应用程序具有**全部清除**删除所有数据库中引号的按钮。</span><span class="sxs-lookup"><span data-stu-id="4d82c-166">The sample app has a **Clear All** button for deleting all of the quotes in the database.</span></span> <span data-ttu-id="4d82c-167">删除其中一个会删除引号一次。</span><span class="sxs-lookup"><span data-stu-id="4d82c-167">The quotes are deleted by removing them one at a time.</span></span> <span data-ttu-id="4d82c-168">删除引号，每次`QuoteDeleted`对记录器调用方法。</span><span class="sxs-lookup"><span data-stu-id="4d82c-168">Each time a quote is deleted, the `QuoteDeleted` method is called on the logger.</span></span> <span data-ttu-id="4d82c-169">日志范围添加到这些日志消息。</span><span class="sxs-lookup"><span data-stu-id="4d82c-169">A log scope is added to these log messages.</span></span>

<span data-ttu-id="4d82c-170">启用`IncludeScopes`控制台记录器选项中：</span><span class="sxs-lookup"><span data-stu-id="4d82c-170">Enable `IncludeScopes` in the console logger options:</span></span>

[!code-csharp[Main](loggermessage/sample/Program.cs?name=snippet1&highlight=22)]

<span data-ttu-id="4d82c-171">设置`IncludeScopes`ASP.NET 核心 2.0 应用程序中需要来启用日志作用域。</span><span class="sxs-lookup"><span data-stu-id="4d82c-171">Setting `IncludeScopes` is required in ASP.NET Core 2.0 apps to enable log scopes.</span></span> <span data-ttu-id="4d82c-172">设置`IncludeScopes`通过*appsettings*配置文件是已计划 ASP.NET 核心 2.1 版本的功能。</span><span class="sxs-lookup"><span data-stu-id="4d82c-172">Setting `IncludeScopes` via *appsettings* configuration files is a feature that's planned for the ASP.NET Core 2.1 release.</span></span>

<span data-ttu-id="4d82c-173">示例应用程序清除其他提供程序，并添加筛选器以减少日志记录输出。</span><span class="sxs-lookup"><span data-stu-id="4d82c-173">The sample app clears other providers and adds filters to reduce the logging output.</span></span> <span data-ttu-id="4d82c-174">这使得更轻松地查看演示的示例的日志消息`LoggerMessage`功能。</span><span class="sxs-lookup"><span data-stu-id="4d82c-174">This makes it easier to see the sample's log messages that demonstrate `LoggerMessage` features.</span></span>

<span data-ttu-id="4d82c-175">若要创建的日志作用域，添加一个字段以保存`Func`委托的范围。</span><span class="sxs-lookup"><span data-stu-id="4d82c-175">To create a log scope, add a field to hold a `Func` delegate for the scope.</span></span> <span data-ttu-id="4d82c-176">示例应用程序创建一个名为字段`_allQuotesDeletedScope`(*Internal/LoggerExtensions.cs*):</span><span class="sxs-lookup"><span data-stu-id="4d82c-176">The sample app creates a field called `_allQuotesDeletedScope` (*Internal/LoggerExtensions.cs*):</span></span>

[!code-csharp[Main](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet4)]

<span data-ttu-id="4d82c-177">使用`DefineScope`来创建委托。</span><span class="sxs-lookup"><span data-stu-id="4d82c-177">Use `DefineScope` to create the delegate.</span></span> <span data-ttu-id="4d82c-178">最多三种类型可以被指定用于作为模板自变量时调用委托。</span><span class="sxs-lookup"><span data-stu-id="4d82c-178">Up to three types can be specified for use as template arguments when the delegate is invoked.</span></span> <span data-ttu-id="4d82c-179">示例应用使用一个包含已删除引号数的消息模板 (`int`类型):</span><span class="sxs-lookup"><span data-stu-id="4d82c-179">The sample app uses a message template that includes the number of deleted quotes (an `int` type):</span></span>

[!code-csharp[Main](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet8)]

<span data-ttu-id="4d82c-180">提供日志消息的静态扩展方法。</span><span class="sxs-lookup"><span data-stu-id="4d82c-180">Provide a static extension method for the log message.</span></span> <span data-ttu-id="4d82c-181">消息模板中包括任何类型参数对于显示的命名属性。</span><span class="sxs-lookup"><span data-stu-id="4d82c-181">Include any type parameters for named properties that appear in the message template.</span></span> <span data-ttu-id="4d82c-182">示例应用程序采用`count`的引号，若要删除并返回`_allQuotesDeletedScope`:</span><span class="sxs-lookup"><span data-stu-id="4d82c-182">The sample app takes in a `count` of quotes to delete and returns `_allQuotesDeletedScope`:</span></span>

[!code-csharp[Main](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet12)]

<span data-ttu-id="4d82c-183">调用中的日志记录扩展作用域包装`using`块：</span><span class="sxs-lookup"><span data-stu-id="4d82c-183">The scope wraps the logging extension calls in a `using` block:</span></span>

[!code-csharp[Main](loggermessage/sample/Pages/Index.cshtml.cs?name=snippet4&highlight=5-6,14)]

<span data-ttu-id="4d82c-184">检查应用程序的控制台输出中的日志消息。</span><span class="sxs-lookup"><span data-stu-id="4d82c-184">Inspect the log messages in the app's console output.</span></span> <span data-ttu-id="4d82c-185">下面的结果显示删除包含的日志范围消息使用的三个引号：</span><span class="sxs-lookup"><span data-stu-id="4d82c-185">The following result shows three quotes deleted with the log scope message included:</span></span>

```console
info: LoggerMessageSample.Pages.IndexModel[4]
      => RequestId:0HL90M6E7PHK5:0000002E RequestPath:/ => /Index => All quotes deleted (Count = 3)
      Quote deleted (Quote = 'Quote 1' Id = 2)
info: LoggerMessageSample.Pages.IndexModel[4]
      => RequestId:0HL90M6E7PHK5:0000002E RequestPath:/ => /Index => All quotes deleted (Count = 3)
      Quote deleted (Quote = 'Quote 2' Id = 3)
info: LoggerMessageSample.Pages.IndexModel[4]
      => RequestId:0HL90M6E7PHK5:0000002E RequestPath:/ => /Index => All quotes deleted (Count = 3)
      Quote deleted (Quote = 'Quote 3' Id = 4)
```

## <a name="see-also"></a><span data-ttu-id="4d82c-186">请参阅</span><span class="sxs-lookup"><span data-stu-id="4d82c-186">See also</span></span>

* [<span data-ttu-id="4d82c-187">日志记录</span><span class="sxs-lookup"><span data-stu-id="4d82c-187">Logging</span></span>](xref:fundamentals/logging/index)
