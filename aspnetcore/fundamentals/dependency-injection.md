---
title: "在 ASP.NET Core 中的依赖关系注入"
author: ardalis
description: "了解 ASP.NET Core 如何实现依赖关系注入和如何使用它。"
keywords: "ASP.NET Core，依赖注入、 DI"
ms.author: riande
manager: wpickett
ms.date: 10/14/2016
ms.topic: article
ms.assetid: fccd69be-7ad1-47fb-b203-b3633b6b9a9b
ms.technology: aspnet
ms.prod: asp.net-core
uid: fundamentals/dependency-injection
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a3a6f755d8825d4bd31cad4e459750c549709c6d
ms.sourcegitcommit: 8f4d4fad1ca27adf9e396f5c205c9875a3963664
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/13/2017
---
# <a name="introduction-to-dependency-injection-in-aspnet-core"></a>在 ASP.NET Core中的依赖关系注入简介

<a name="fundamentals-dependency-injection"></a>

作者：[Steve Smith](https://ardalis.com/)和[Scott Addie](https://scottaddie.com)

ASP.NET Core旨在从根本上设计为支持并利用依赖注入。 ASP.NET Core应用程序可以通过注入到Startup类中的方法的方式利用内置框架服务，也可以将应用程序服务配置为注入。 由 ASP.NET Core 提供的默认服务容器提供了一个最小功能集合，并不计划替换其他容器。

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/dependency-injection/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）

## <a name="what-is-dependency-injection"></a>什么是依赖注入？

依赖注入 (DI) 是一种技术，有助于实现对象与其协作者或依赖项之间的松散耦合。与其直接实例化协作者或使用静态引用，类以某种方式向类提供一个对象，以便执行其操作。大多数情况下，类将通过其构造函数声明它们的依赖关系，从而允许它们遵循[显式依赖关系原则](http://deviq.com/explicit-dependencies-principle/)。 此方法被称为"构造函数注入"。

在遵循DI原则来设计类时，由于它们与其协作者没有直接的，硬编码的依赖关系，所以它们之间的耦合更为松散。 这遵循[依赖倒置原则](http://deviq.com/dependency-inversion-principle/)，其中指出*"高级模块不应依赖于低级模块; 同时两者都应依赖于抽象"。* 类请求在该类被构造时提供给它们的抽象(通常是`接口`)，而不是引用特定的实现。将依赖关系提取到接口中并将这些接口的实现作为参数提供也是[策略设计模式](http://deviq.com/strategy-design-pattern/)的一个例子。

当系统被设计为使用 DI 时，许多类通过其构造函数 （或属性）来请求它们的依赖关系，所以有一个专门用来创建这些类以及它们相关的依赖关系的类是很有帮助的。 这些类统称为*容器*，或更具体地说，[控制反转 (IoC)](http://deviq.com/inversion-of-control/)容器或依赖注入 (DI) 容器。 一个容器本质上是一个工厂，它负责提供从中请求的类型的实例。 如果一个给定的类型已声明它具有依赖关系，并且容器已经被配置为提供依赖类型，那么它将创建依赖关系并将其作为创建请求实例的一部分。通过这种方式，可以为类提供复杂的依赖关系图，而无需任何硬编码对象构造函数。 除了使用依赖创建对象之外，容器通常还可以管理应用程序中的对象生命周期。

ASP.NET Core包含一个简单的内置容器 (表示为`IServiceProvider`接口)，默认情况下，支持构造函数注入，ASP.NET 可通过 DI 提供某些服务。 ASP。NET 的容器将它管理的类型作为*服务*。 本文其余部分中，*服务*将引用由 ASP.NET Core IoC 容器管理的类型。 您可以在应用程序的`Startup`类中的`ConfigureServices`方法中配置内置容器的服务。

> [!NOTE]
> Martin Fowler 写了另外的一篇关于[控制反转容器和依赖注入模式](https://www.martinfowler.com/articles/injection.html)的文章。 Microsoft 模式和实践也对[依赖关系注入](https://msdn.microsoft.com/library/hh323705.aspx)具有很好的描述。

> [!NOTE]
> 本文介绍了依赖注入，因为它适用于所有 ASP.NET 应用程序。 MVC 控制器中的依赖注入包含在[依赖注入和控制器](../mvc/controllers/dependency-injection.md)中。

### <a name="constructor-injection-behavior"></a>构造函数注入行为

构造函数注入要求*public*的构造函数。 否则，你的应用程序会抛出`InvalidOperationException`异常:

> 找不到适合类型 YourType 的构造函数。 请确保该类型是具体的，并为公共构造函数的所有参数注册服务。


构造函数注入要求只存在一个适用的构造函数。 构造函数支持重载，但其参数可以全部通过依赖注入来实现的重载只能存在一个。如果存在多个，您的应用程序将抛出一个`InvalidOperationException`异常:

> 已在类型 YourType 中找到多个接受所有给定的参数类型的构造函数。 应该只有一个适用的构造函数。

构造函数可以接受依赖注入没有提供的参数，但这些参数必须支持默认值。 例如: 

```csharp
// throws InvalidOperationException: Unable to resolve service for type 'System.String'...
public CharactersController(ICharacterRepository characterRepository, string title)
{
    _characterRepository = characterRepository;
    _title = title;
}

// runs without error
public CharactersController(ICharacterRepository characterRepository, string title = "Characters")
{
    _characterRepository = characterRepository;
    _title = title;
}
```

## <a name="using-framework-provided-services"></a>使用框架提供的服务

`Startup`类中的`ConfigureServices`方法负责定义应用程序将使用的服务，包括Entity Framework Core和 ASP.NET Core MVC 这样的平台特性。 最初，提供给`ConfigureServices`的`IServiceCollection`定义了以下服务 (具体取决于[配置主机的方式](xref:fundamentals/hosting)):

| 服务类型 | 生存期 |
| ----- | ------- |
| [Microsoft.AspNetCore.Hosting.IHostingEnvironment](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.hosting.ihostingenvironment) | 单例 |
| [Microsoft.Extensions.Logging.ILoggerFactory](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.iloggerfactory) | 单例 |
| [Microsoft.Extensions.Logging.ILogger&lt;T&gt;](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.ilogger) | 单例 |
| [Microsoft.AspNetCore.Hosting.Builder.IApplicationBuilderFactory](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.hosting.builder.iapplicationbuilderfactory) | 瞬时 |
| [Microsoft.AspNetCore.Http.IHttpContextFactory](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.http.ihttpcontextfactory) | 瞬时 |
| [Microsoft.Extensions.Options.IOptions&lt;T&gt;](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.options.ioptions-1) | 单例 |
| [System.Diagnostics.DiagnosticSource](https://docs.microsoft.com/dotnet/core/api/system.diagnostics.diagnosticsource) | 单例 |
| [System.Diagnostics.DiagnosticListener](https://docs.microsoft.com/dotnet/core/api/system.diagnostics.diagnosticlistener) | 单例 |
| [Microsoft.AspNetCore.Hosting.IStartupFilter](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.hosting.istartupfilter) | 瞬时 |
| [Microsoft.Extensions.ObjectPool.ObjectPoolProvider](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.objectpool.objectpoolprovider) | 单例 |
| [Microsoft.Extensions.Options.IConfigureOptions&lt;T&gt;](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.options.iconfigureoptions-1) | 瞬时 |
| [Microsoft.AspNetCore.Hosting.Server.IServer](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.hosting.server.iserver) | 单例 |
| [Microsoft.AspNetCore.Hosting.IStartup](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.hosting.istartup) | 单例 |
| [Microsoft.AspNetCore.Hosting.IApplicationLifetime](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.hosting.iapplicationlifetime) | 单例 |

下面是如何使用若干扩展方法如`AddDbContext`， `AddIdentity`，和`AddMvc`将附加服务添加到容器的示例。

[!code-csharp[Main](../common/samples/WebApplication1/Startup.cs?highlight=5-6,8-10,12&range=39-56)]

ASP.NET提供的功能和中间件，如 MVC，遵循使用单个*AddServiceName*扩展方法的约定来注册该功能所需的所有服务。

>[!TIP]
> 你可以通过参数列表在`Startup`方法中请求某些框架提供的服务-请参阅[应用程序启动](startup.md)以获取更多详细信息。

## <a name="registering-your-own-services"></a>注册你自己的服务

您可以按如下方式注册自己的应用程序服务。 第一个泛型类型表示将从容器请求的类型 （通常是一个接口）。 第二个泛型类型表示将由容器实例化并用于满足此类请求的具体类型。

[!code-csharp[Main](../common/samples/WebApplication1/Startup.cs?range=53-54)]

> [!NOTE]
> 每个`services.Add<ServiceName>`扩展方法添加 （并可能配置） 服务。 例如，`services.AddMvc()`添加 MVC 需要的服务。 建议您遵循此约定，将扩展方法放置在`Microsoft.Extensions.DependencyInjection`命名空间中，以封装服务注册的组。

`AddTransient`方法用于将抽象类型映射到为每个需要它的对象分别实例化的具体服务。 这称为服务的*生命周期*，其他生命周期选项如下所述。 为您注册的每个服务选择适当的生命周期非常重要。 是否应该向每个请求它的类提供一个新的服务实例？是否在整个给定的Web请求中使用一个实例？或是否应该在应用程序生命周期内使用单例？

在本文示例中，有一个显示Character名称的简单控制器，名为`CharactersController`。 其`Index`方法会显示存储在应用程序中的当前character列表，如果不存在，则使用少量Character初始化该集合。请注意，尽管此应用程序为其持久化使用Entity Framework Core和`ApplicationDbContext`，但在控制器中没有任何明显的表现。 相反，特定的数据访问机制已经被抽象为一个接口，即`ICharacterRepository`，它遵循[仓储模式](http://deviq.com/repository-pattern/)。通过构造函数请求`ICharacterRepository`实例，并将其分配给私有字段，然后根据需要使用它访问characters。

[!code-csharp[Main](../fundamentals/dependency-injection/sample/DependencyInjectionSample/Controllers/CharactersController.cs?highlight=3,5,6,7,8,14,21-27&range=8-36)]

`ICharacterRepository`定义了控制器需要使用`Character`实例的两种方法。

[!code-csharp[Main](../fundamentals/dependency-injection/sample/DependencyInjectionSample/Interfaces/ICharacterRepository.cs?highlight=8,9)]

此接口又由一个具体类型实现，即`CharacterRepository`，其在运行时使用。

> [!NOTE]
> DI与`CharacterRepository`类一起使用的方式是一个通用模型，您可以为所有应用程序服务遵循此模型，而不仅仅在“仓储库”或数据访问类中。

[!code-csharp[Main](../fundamentals/dependency-injection/sample/DependencyInjectionSample/Models/CharacterRepository.cs?highlight=9,11,12,13,14)]

请注意，`CharacterRepository`在其构造函数中请求一个`ApplicationDbContext`。 依赖注入以这种链式方式被使用并不罕见，每个被请求的依赖依次请求它自己的依赖。 容器将负责解决图中所有的依赖关系，并返回完全解析后的服务。

> [!NOTE]
> 创建请求的对象，和它需要的所有对象，以及这些需要的所有对象，有时被称为*对象图*。 同样，必须被解析的集合依赖关系通常被称为*依赖关系树*或*依赖项关系图*。

在这种情况下，`ICharacterRepository`和`ApplicationDbContext`必须在`Startup`类的`ConfigureServices`中的服务容器中注册。 `ApplicationDbContext`通过调用扩展方法`AddDbContext<T>`进行配置。 下面的代码演示了`CharacterRepository`类型的注册。

[!code-csharp[Main](dependency-injection/sample/DependencyInjectionSample/Startup.cs?highlight=3-5,11&range=16-32)]

应使用`Scoped`生命周期将Entity Framework上下文添加到服务容器中。如果您使用上面所示的帮助方法，则会自动执行此操作。使用Entity Framework的仓储库应使用相同的生命周期。

>[!WARNING]
> 需要注意的主要危险是从单例解析一个`Scoped`服务。 在此类情况下，当处理后续请求时，服务可能会处于不正确的状态。

具有依赖的服务应将其注册到容器中。 如果服务的构造函数需要一个基元，例如`string`，这可以通过使用[选项模式和配置](configuration.md)来注入。

## <a name="service-lifetimes-and-registration-options"></a>服务生命周期和注册选项

可以使用以下的生命周期配置 ASP.NET 服务：

**瞬时（Transient）**

每次请求时都会创建瞬时生命周期服务。 这种生命周期适合轻量级、 无状态的服务。

**作用域（Scoped）**

每个请求创建一次作用域生命周期服务。

**单例（Singleton）**

单例生命周期服务在第一次被请求时创建(或者当指定一个实例时`ConfigureServices`正在运行的情况下)，然后每个后续请求将使用同一实例。 如果您的应用程序需要单例行为，建议允许服务容器管理服务的生命周期，而不是自己实现单例设计模式并在类中管理对象的生命周期。

服务可以使用多种方式注册到容器中。我们已经看到了如何通过指定要使用的具体类型来注册一个给定类型的服务实现。 此外，可以指定一个工厂，然后将其用于按需创建实例。 第三种方法是直接指定要使用的类型的实例，在这种情况下，容器将永远不会尝试创建实例（也不会释放实例）。

为了演示这些生命周期和注册选项之间的差异，请考虑一个简单的接口，将一个或多个任务表示为具有唯一标识符`OperationId`的*operation*。 根据我们配置此服务生命周期的方式，容器将向请求的类提供相同或不同的实例。为了明确正在请求哪个生命周期，我们将为每个生命周期选项创建一个类型：

[!code-csharp[Main](../fundamentals/dependency-injection/sample/DependencyInjectionSample/Interfaces/IOperation.cs?highlight=5-8)]

我们实现使用一个类`Operation`来实现这些接口，它在构造函数中接受一个`Guid`，如果没有提供，则使用一个新的`Guid`。

接下来，在`ConfigureServices`中，根据其命名的生命周期，将每个类型添加到容器中：

[!code-csharp[Main](dependency-injection/sample/DependencyInjectionSample/Startup.cs?range=26-32)]

请注意，`IOperationSingletonInstance`服务正在使用一个具有已知ID为`Guid.Empty`的特定实例，因此使用此类型时ID将会被清除（其Guid将全部为零）。我们已注册了依赖于每个其他`Operation`类型的`OperationService`，因此对每个operation类型来说，该服务是否获得了作为控制器的同一实例，或一个新的实例，是很清楚的。 所有此服务的作用将其依赖项作为属性公开，以便它们可以显示在视图中。

[!code-csharp[Main](dependency-injection/sample/DependencyInjectionSample/Services/OperationService.cs)]

为了演示单独的对应用程序的请求之内和之间的对象生命周期，该示例包含一个`OperationsController`，它请求每种`IOperation`类型以及一个`OperationService`。`Index`操作将显示所有控制器和服务的`OperationId`值。

[!code-csharp[Main](dependency-injection/sample/DependencyInjectionSample/Controllers/OperationsController.cs)]

现在对该控制器操作发起了两个单独的请求：

![在 Microsoft Edge 中运行的依赖注入示例 web 应用程序操作视图，显示第一次请求时的瞬时、 作用域、单例，和实例控制器和操作服务的操作 ID 值 (GUID)。](dependency-injection/_static/lifetimes_request1.png)

![第二个请求时操作视图显示的操作 ID 值。](dependency-injection/_static/lifetimes_request2.png)

观察哪个`OperationId`值会在一个请求之内和不同请求之间变化。

* *瞬时*对象始终是不同的; 为每个控制器和每个服务提供一个新实例。

* *作用域*对象在一个请求中是相同的，但在不同请求中是不同的。

* *单例*对象对每个对象和每个请求都是相同的 (不管`ConfigureServices`是否提供了一个实例)

## <a name="request-services"></a>请求服务

来自`HttpContext`的ASP.NET请求中可用的服务通过`RequestServices`集合公开。

![HttpContext 请求服务智能感知上下文对话框，指出请求服务获取或设置 IServiceProvider，其提供对请求的服务容器的访问。](dependency-injection/_static/request-services.png)

请求服务表示您配置和请求的服务，其作为应用程序的一部分。 当您的对象指定的依赖关系时，`RequestServices`（而不`ApplicationServices`）中的类型将满足这些要求。

通常情况下，不应直接使用这些属性，而应该通过类的构造函数来请求所需类的类型，并让框架注入这些依赖关系。 这将生成更易于测试的类 (请参阅[测试](../testing/index.md)) 并更松散耦合。

> [!NOTE]
> 优先请求依赖作为构造函数的参数来访问`RequestServices`集合。

## <a name="designing-your-services-for-dependency-injection"></a>为依赖注入设计您的服务

您应设计你的服务以使用依赖注入来获取其协作者。 这意味着避免使用有状态的静态方法调用 (这会导致称为[静态粘贴](http://deviq.com/static-cling/)的代码坏味道) 和您的服务中的依赖类的直接实例化。在选择是实例化一个类型还是通过依赖注入来请求它时，可能会帮助你记住这个短语：[新增即粘附](https://ardalis.com/new-is-glue)。遵循[面向对象设计的SOLID原则](http://deviq.com/solid/)，您的类将自然倾向于小型、 良好分解，和容易测试。

如果您发现您的类往往具有太多的依赖注入怎么办？ 这通常表明您的类正试图做更多的事情，而且可能违反了 SRP-[单一责任原则](http://deviq.com/single-responsibility-principle/)。 看看是否可以通过将某些职责移动到一个新类来重构类。 请记住，您的`Controller`类应关注用户界面问题，因此业务规则和数据访问实现细节应保存在适用于这些[分离关注](http://deviq.com/separation-of-concerns/)的类中。

具体就数据访问而言，可以将`DbContext`注入到你的控制器 (假设你已向`ConfigureServices`中的服务容器中添加了 EF )。 一些开发人员更愿意使用数据库的仓储接口而不是直接注入`DbContext`。 使用接口将数据访问逻辑封装在一个地方，可以最大程度减少数据库更改时需要更改的地方数量。

### <a name="disposing-of-services"></a>释放服务

容器将为它创建的`IDisposable`类型调用`Dispose`。但是，如果您自己将一个实例添加到容器，它将不会被销毁。

示例:

```csharp
// Services implement IDisposable:
public class Service1 : IDisposable {}
public class Service2 : IDisposable {}
public class Service3 : IDisposable {}

public void ConfigureServices(IServiceCollection services)
{
    // container will create the instance(s) of these types and will dispose them
    services.AddScoped<Service1>();
    services.AddSingleton<Service2>();

    // container did not create instance so it will NOT dispose it
    services.AddSingleton<Service3>(new Service3());
    services.AddSingleton(new Service3());
}
```

> [!NOTE]
> 在 1.0 版中，容器将对*所有*`IDisposable`对象调用 dispose，包括那些未创建的对象。

## <a name="replacing-the-default-services-container"></a>替换默认服务容器

内置的服务容器旨在提供框架和在其上生成的大多数消费者应用程序的基本需求。 但是，开发人员可以使用自己喜欢的容器替换内置容器。 `ConfigureServices`方法通常返回`void`，但是，如果更改其签名以返回`IServiceProvider`，则可以配置和返回不同的容器。 有许多可用于.NET 的 IOC 容器。 在此示例中，使用[Autofac](https://autofac.org/)包。

首先，安装适当的容器程序包：

* `Autofac`
* `Autofac.Extensions.DependencyInjection`

接下来，在`ConfigureServices`中配置容器并返回`IServiceProvider`:

```csharp
public IServiceProvider ConfigureServices(IServiceCollection services)
{
    services.AddMvc();
    // Add other framework services

    // Add Autofac
    var containerBuilder = new ContainerBuilder();
    containerBuilder.RegisterModule<DefaultModule>();
    containerBuilder.Populate(services);
    var container = containerBuilder.Build();
    return new AutofacServiceProvider(container);
}
```

> [!NOTE]
> 在使用第三方 DI 容器时，必须更改`ConfigureServices`，以便它返回`IServiceProvider`而不是`void`。

最后，在`DefaultModule`中正常配置Autofac:

```csharp
public class DefaultModule : Module
{
    protected override void Load(ContainerBuilder builder)
    {
        builder.RegisterType<CharacterRepository>().As<ICharacterRepository>();
    }
}
```

在运行时，将使用 Autofac 来解析类型，并注入依赖。 [了解有关使用 Autofac 和 ASP.NET Core的更多信息](http://docs.autofac.org/en/latest/integration/aspnetcore.html)。

### <a name="thread-safety"></a>线程安全

单例服务需要是线程安全的。 如果单例服务依赖于一个瞬时服务，那么瞬时服务可能也需要是线程安全的，具体取决于单例使用它的方式。

## <a name="recommendations"></a>建议

在使用依赖关系注入，请记住以下建议：

* DI 适用于具有复杂的依赖关系的对象。 控制器、 服务、 适配器和仓储都是可能添加到 DI 中的对象示例。

* 避免在 DI 中直接存储数据和配置。 例如，用户的购物车通常不应添加到服务容器中。 配置应使用[选项模型](configuration.md#options-config-objects)。 同样，避免仅存在允许访问某些其他对象的"数据持有者"对象。如果可能的话，最好通过 DI 请求所需的实际项目。

* 避免静态访问服务。

* 避免应用程序代码中的服务定位。

* 避免对`HttpContext`的静态访问。

> [!NOTE]
> 像所有的建议一样，您可能会遇到忽略其中一个的情况。 我们发现罕见的例外情况 - 大多数是框架本身非常特殊的情况。。

请记住，依赖注入是静态/全局对象访问模式的*替代*方法。如果将其与静态对象访问混合使用，则无法实现DI的优点。

## <a name="additional-resources"></a>其他资源

* [应用程序启动](startup.md)

* [测试](../testing/index.md)

* [在 ASP.NET Core中使用依赖关系注入编写干净代码 (MSDN) ](https://msdn.microsoft.com/magazine/mt703433.aspx)

* [容器管理应用程序设计，序：容器属于何处？](https://blogs.msdn.microsoft.com/nblumhardt/2008/12/26/container-managed-application-design-prelude-where-does-the-container-belong/)

* [显式依赖原则](http://deviq.com/explicit-dependencies-principle/)

* [控制反转容器和依赖关系注入模式](https://www.martinfowler.com/articles/injection.html)(Fowler)
