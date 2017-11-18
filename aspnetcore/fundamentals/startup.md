---
title: "ASP.NET Core 中的应用程序启动"
author: ardalis
description: "发现服务和应用程序的请求管道 Startup 类在 ASP.NET 核心中的配置的方式。"
keywords: "ASP.NET Core，启动时，Configure 方法，ConfigureServices 方法"
ms.author: tdykstra
manager: wpickett
ms.date: 02/29/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: fundamentals/startup
ms.openlocfilehash: bba0eafe3917fa850b3a07df8df6448409f4062d
ms.sourcegitcommit: 732cd2684246e49e796836596643a8d37e20c46d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2017
---
# <a name="application-startup-in-aspnet-core"></a>ASP.NET Core 中的应用程序启动

作者：[Steve Smith](https://ardalis.com/)和[Tom Dykstra](https://github.com/tdykstra/)

`Startup`类配置服务和应用程序的请求管道。

## <a name="the-startup-class"></a>Startup 类

ASP.NET Core 应用需要`Startup`类，按照约定，该类命名为`Startup`。 你可以在`Main`程序的[WebHostBuilderExtensions](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.hosting.webhostbuilderextensions) 中的 [ `UseStartup<TStartup>` ](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.hosting.webhostbuilderextensions#Microsoft_AspNetCore_Hosting_WebHostBuilderExtensions_UseStartup__1_Microsoft_AspNetCore_Hosting_IWebHostBuilder_)方法中指定启动类名。 请参阅[Hosting](xref:fundamentals/hosting)以详细了解在`Startup`之前运行的`WebHostBuilder`。

你可以为不同的环境定义单独`Startup`类，在运行时将选择合适的一个类。 如果在[WebHost 配置](https://docs.microsoft.com/aspnet/core/fundamentals/hosting?tabs=aspnetcore2x#configuring-a-host)或选项中指定了`startupAssembly`，宿主将加载该startup程序集并搜索`Startup`或`Startup[Environment]`类型。 名称后缀匹配当前运行环境的类将具有优先级，因此，如果应用运行在*Development*环境，并同时包含`Startup`和`StartupDevelopment`类，则使用`StartupDevelopment`类。 请参阅`StartupLoader`中的[FindStartupType](https://github.com/aspnet/Hosting/blob/rel/1.1.0/src/Microsoft.AspNetCore.Hosting/Internal/StartupLoader.cs)和[使用多个环境](environments.md#startup-conventions)。

或者，你可以定义不变的`Startup`类，将调用`UseStartup<TStartup>`而不考虑环境。 这是推荐的方法。

`Startup`类构造函数可以接受通过[依赖注入](xref:fundamentals/dependency-injection)提供的依赖项。 常见方法是使用`IHostingEnvironment`设置[configuration](xref:fundamentals/configuration)源。

`Startup`类必须包含一个`Configure`方法，并且可以根据需要包含`ConfigureServices`方法，这两种方法都在应用程序启动时调用。 此类还可包含[这些方法特定于环境的版本](xref:fundamentals/environments#startup-conventions)。 如果存在`ConfigureServices`, 则它在`Configure`之前调用。

了解有关[处理应用程序启动期间的异常](xref:fundamentals/error-handling#startup-exception-handling)。

## <a name="the-configureservices-method"></a>ConfigureServices 方法

[ConfigureServices](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.hosting.startupbase#Microsoft_AspNetCore_Hosting_StartupBase_ConfigureServices_Microsoft_Extensions_DependencyInjection_IServiceCollection_)方法是可选的; 但如果使用，则 Web 主机将在`Configure`方法之前调用它。 Web 主机可以在`Startup`方法被调用之前配置某些服务 (请参阅[hosting](xref:fundamentals/hosting))。 按照约定，[配置选项](xref:fundamentals/configuration)在此方法中设置。

对于需要大量设置的特性，可以使用[IServiceCollection](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.dependencyinjection.iservicecollection)的`Add[Service]`扩展方法。 此来自默认网站模板配置的示例，对应用程序进行配置，以将服务用于Entity Framework, Identity, 和 MVC:

[!code-csharp[Main](../common/samples/WebApplication1/Startup.cs?highlight=4,7,11&start=40&end=55)]

通过[依赖注入](xref:fundamentals/dependency-injection)将服务添加到服务容器，使它们在应用程序中可用。

## <a name="services-available-in-startup"></a>在Startup中可用的服务

ASP.NET Core 依赖注入在应用程序启动期间提供服务。 你可以通过在`Startup`类的构造函数或其`Configure`方法中传递适当的接口参数来请求这些服务 。`ConfigureServices`方法仅采用`IServiceCollection`参数 （但此集合中可以获取任何已注册的服务，因此不需要其他参数）。

以下是一些通常由`Startup`方法请求的服务：

* 构造函数中： `IHostingEnvironment`，`ILogger<Startup>`
* 在`ConfigureServices`:`IServiceCollection`
* 在`Configure`: `IApplicationBuilder`， `IHostingEnvironment`，`ILoggerFactory`

`Startup`类构造函数或其`Configure`方法可能请求任何通过``WebHostBuilder````ConfigureServices``方法添加的服务。 使用`WebHostBuilder`在`Startup`方法提供任何你需要的服务。

## <a name="the-configure-method"></a>Configure 方法

`Configure`方法用于指定 ASP.NET 应用程序将如何响应 HTTP 请求。 通过向一个由依赖注入提供的`IApplicationBuilder`实例添加[中间件](middleware.md)组件，来配置请求管道。

在以下来自默认网站模板的示例中，使用了多个扩展方法来配置管道，用于支持[浏览器链接](http://vswebessentials.com/features/browserlink)，错误页、 静态文件、 ASP.NET MVC 和 Identity。

[!code-csharp[Main](../common/samples/WebApplication1/Startup.cs?highlight=8,9,10,14,17,19,21&start=58&end=84)]

每个`Use`扩展方法都向请求管道组件添加一个[中间件](xref:fundamentals/middleware)。 例如，`UseMvc`扩展方法将向请求管道添加[路由](routing.md)中间件，并配置[MVC](xref:mvc/overview)作为默认处理程序。

有关如何使用`IApplicationBuilder`，请参阅[中间件](xref:fundamentals/middleware)。

其他服务，如`IHostingEnvironment`和`ILoggerFactory`还可以在方法签名中指定，在这种情况下这些服务如果可用，将被[注入](dependency-injection.md)。 

## <a name="additional-resources"></a>其他资源

* [使用多个环境](xref:fundamentals/environments)
* [中间件](xref:fundamentals/middleware)
* [日志记录](xref:fundamentals/logging)
* [配置](xref:fundamentals/configuration)
