---
uid: web-api/overview/advanced/dependency-injection
title: "ASP.NET Web API 2 中的依赖关系注入 |Microsoft 文档"
author: MikeWasson
description: "本教程演示如何将依赖关系注入到你的 ASP.NET Web API 控制器。 在教程的 Web API 2 Unity 应用程序块中使用的软件版本..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/20/2014
ms.topic: article
ms.assetid: e3d3e7ba-87f0-4032-bdd3-31f3c1aa9d9c
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/advanced/dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: b4cf39c59ed257b0014dbdbecef3eb7bc48f410d
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2017
---
<a name="dependency-injection-in-aspnet-web-api-2"></a><span data-ttu-id="bd3b3-104">ASP.NET Web API 2 中的依赖关系注入</span><span class="sxs-lookup"><span data-stu-id="bd3b3-104">Dependency Injection in ASP.NET Web API 2</span></span>
====================
<span data-ttu-id="bd3b3-105">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="bd3b3-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="bd3b3-106">下载已完成的项目</span><span class="sxs-lookup"><span data-stu-id="bd3b3-106">Download Completed Project</span></span>](http://code.msdn.microsoft.com/ASP-NET-Web-API-Tutorial-468ee148)

> <span data-ttu-id="bd3b3-107">本教程演示如何将依赖关系注入到你的 ASP.NET Web API 控制器。</span><span class="sxs-lookup"><span data-stu-id="bd3b3-107">This tutorial shows how to inject dependencies into your ASP.NET Web API controller.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="bd3b3-108">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="bd3b3-108">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="bd3b3-109">Web API 2</span><span class="sxs-lookup"><span data-stu-id="bd3b3-109">Web API 2</span></span>
> - [<span data-ttu-id="bd3b3-110">Unity 应用程序块</span><span class="sxs-lookup"><span data-stu-id="bd3b3-110">Unity Application Block</span></span>](https://www.nuget.org/packages/Unity/)
> - <span data-ttu-id="bd3b3-111">实体框架 6 （也适用版本 5）</span><span class="sxs-lookup"><span data-stu-id="bd3b3-111">Entity Framework 6 (version 5 also works)</span></span>


## <a name="what-is-dependency-injection"></a><span data-ttu-id="bd3b3-112">什么是依赖关系注入？</span><span class="sxs-lookup"><span data-stu-id="bd3b3-112">What is Dependency Injection?</span></span>

<span data-ttu-id="bd3b3-113">A*依赖*是另一个对象需要的任何对象。</span><span class="sxs-lookup"><span data-stu-id="bd3b3-113">A *dependency* is any object that another object requires.</span></span> <span data-ttu-id="bd3b3-114">例如，很容易定义[存储库](http://martinfowler.com/eaaCatalog/repository.html)用于处理数据访问。</span><span class="sxs-lookup"><span data-stu-id="bd3b3-114">For example, it's common to define a [repository](http://martinfowler.com/eaaCatalog/repository.html) that handles data access.</span></span> <span data-ttu-id="bd3b3-115">让我们举例说明了。</span><span class="sxs-lookup"><span data-stu-id="bd3b3-115">Let's illustrate with an example.</span></span> <span data-ttu-id="bd3b3-116">首先，我们将定义域模型：</span><span class="sxs-lookup"><span data-stu-id="bd3b3-116">First, we'll define a domain model:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample1.cs)]

<span data-ttu-id="bd3b3-117">此处是一个简单的存储库类，将项存储在数据库中，使用 Entity Framework。</span><span class="sxs-lookup"><span data-stu-id="bd3b3-117">Here is a simple repository class that stores items in a database, using Entity Framework.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample2.cs)]

<span data-ttu-id="bd3b3-118">现在让我们定义支持 GET 请求的一个 Web API 控制器`Product`实体。</span><span class="sxs-lookup"><span data-stu-id="bd3b3-118">Now let's define a Web API controller that supports GET requests for `Product` entities.</span></span> <span data-ttu-id="bd3b3-119">（我已经将出 POST 和为简单起见其他方法。）下面是第一次尝试：</span><span class="sxs-lookup"><span data-stu-id="bd3b3-119">(I'm leaving out POST and other methods for simplicity.) Here is a first attempt:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample3.cs)]

<span data-ttu-id="bd3b3-120">请注意，取决于控制器类`ProductRepository`，我们会让创建控制器和`ProductRepository`实例。</span><span class="sxs-lookup"><span data-stu-id="bd3b3-120">Notice that the controller class depends on `ProductRepository`, and we are letting the controller create the `ProductRepository` instance.</span></span> <span data-ttu-id="bd3b3-121">但是，它的原因是为硬编码的依赖关系，这种方式，是个好主意。</span><span class="sxs-lookup"><span data-stu-id="bd3b3-121">However, it's a bad idea to hard code the dependency in this way, for several reasons.</span></span>

- <span data-ttu-id="bd3b3-122">如果你想要替换`ProductRepository`使用不同的实现，你还需要修改控制器类。</span><span class="sxs-lookup"><span data-stu-id="bd3b3-122">If you want to replace `ProductRepository` with a different implementation, you also need to modify the controller class.</span></span>
- <span data-ttu-id="bd3b3-123">如果`ProductRepository`具有依赖关系，你必须配置这些控制器中。</span><span class="sxs-lookup"><span data-stu-id="bd3b3-123">If the `ProductRepository` has dependencies, you must configure these inside the controller.</span></span> <span data-ttu-id="bd3b3-124">对于具有多个控制器的大型项目，你的配置代码变得分散在你的项目。</span><span class="sxs-lookup"><span data-stu-id="bd3b3-124">For a large project with multiple controllers, your configuration code becomes scattered across your project.</span></span>
- <span data-ttu-id="bd3b3-125">很难进行单元测试，因为控制器是硬编码来查询数据库。</span><span class="sxs-lookup"><span data-stu-id="bd3b3-125">It is hard to unit test, because the controller is hard-coded to query the database.</span></span> <span data-ttu-id="bd3b3-126">对于单元测试，则应使用一个模型或存根 （stub） 存储库，这是不可能与当前设计。</span><span class="sxs-lookup"><span data-stu-id="bd3b3-126">For a unit test, you should use a mock or stub repository, which is not possible with the currect design.</span></span>

<span data-ttu-id="bd3b3-127">我们可以解决这些问题的*将注入*插入控制器的存储库。</span><span class="sxs-lookup"><span data-stu-id="bd3b3-127">We can address these problems by *injecting* the repository into the controller.</span></span> <span data-ttu-id="bd3b3-128">首先，重构`ProductRepository`到接口的类：</span><span class="sxs-lookup"><span data-stu-id="bd3b3-128">First, refactor the `ProductRepository` class into an interface:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample4.cs)]

<span data-ttu-id="bd3b3-129">然后提供`IProductRepository`作为构造函数参数：</span><span class="sxs-lookup"><span data-stu-id="bd3b3-129">Then provide the `IProductRepository` as a constructor parameter:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample5.cs)]

<span data-ttu-id="bd3b3-130">此示例使用[构造函数注入](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection)。</span><span class="sxs-lookup"><span data-stu-id="bd3b3-130">This example uses [constructor injection](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection).</span></span> <span data-ttu-id="bd3b3-131">你还可以使用*setter 注入*，则将通过 setter 方法或属性的依赖关系的设置。</span><span class="sxs-lookup"><span data-stu-id="bd3b3-131">You can also use *setter injection*, where you set the dependency through a setter method or property.</span></span>

<span data-ttu-id="bd3b3-132">但现在没有问题，因为你的应用程序不直接创建控制器。</span><span class="sxs-lookup"><span data-stu-id="bd3b3-132">But now there is a problem, because your application doesn't create the controller directly.</span></span> <span data-ttu-id="bd3b3-133">Web API 可创建控制器，当它将路由请求，并且 Web API 不知道任何有关`IProductRepository`。</span><span class="sxs-lookup"><span data-stu-id="bd3b3-133">Web API creates the controller when it routes the request, and Web API doesn't know anything about `IProductRepository`.</span></span> <span data-ttu-id="bd3b3-134">这是 Web API 依赖项解析程序传入的位置。</span><span class="sxs-lookup"><span data-stu-id="bd3b3-134">This is where the Web API dependency resolver comes in.</span></span>

## <a name="the-web-api-dependency-resolver"></a><span data-ttu-id="bd3b3-135">Web API 依赖项解析程序</span><span class="sxs-lookup"><span data-stu-id="bd3b3-135">The Web API Dependency Resolver</span></span>

<span data-ttu-id="bd3b3-136">Web API 定义**IDependencyResolver**用于解析的依赖关系接口。</span><span class="sxs-lookup"><span data-stu-id="bd3b3-136">Web API defines the **IDependencyResolver** interface for resolving dependencies.</span></span> <span data-ttu-id="bd3b3-137">下面是接口的定义：</span><span class="sxs-lookup"><span data-stu-id="bd3b3-137">Here is the definition of the interface:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample6.cs)]

<span data-ttu-id="bd3b3-138">**IDependencyScope**接口有两种方法：</span><span class="sxs-lookup"><span data-stu-id="bd3b3-138">The **IDependencyScope** interface has two methods:</span></span>

- <span data-ttu-id="bd3b3-139">**GetService**创建类型的一个实例。</span><span class="sxs-lookup"><span data-stu-id="bd3b3-139">**GetService** creates one instance of a type.</span></span>
- <span data-ttu-id="bd3b3-140">**GetServices**创建指定类型的对象的集合。</span><span class="sxs-lookup"><span data-stu-id="bd3b3-140">**GetServices** creates a collection of objects of a specified type.</span></span>

<span data-ttu-id="bd3b3-141">**IDependencyResolver**方法继承**IDependencyScope**并添加**如何**方法。</span><span class="sxs-lookup"><span data-stu-id="bd3b3-141">The **IDependencyResolver** method inherits **IDependencyScope** and adds the **BeginScope** method.</span></span> <span data-ttu-id="bd3b3-142">我将在本教程后面讨论的作用域。</span><span class="sxs-lookup"><span data-stu-id="bd3b3-142">I'll talk about scopes later in this tutorial.</span></span>

<span data-ttu-id="bd3b3-143">当 Web API 创建的控制器实例时，首先调用**IDependencyResolver.GetService**，并传入控制器类型。</span><span class="sxs-lookup"><span data-stu-id="bd3b3-143">When Web API creates a controller instance, it first calls **IDependencyResolver.GetService**, passing in the controller type.</span></span> <span data-ttu-id="bd3b3-144">此扩展性挂钩，可用于创建控制器上，解决任何依赖关系。</span><span class="sxs-lookup"><span data-stu-id="bd3b3-144">You can use this extensibility hook to create the controller, resolving any dependencies.</span></span> <span data-ttu-id="bd3b3-145">如果**GetService** ，则返回 null，Web API 控制器类上的无参数构造函数的如下所示。</span><span class="sxs-lookup"><span data-stu-id="bd3b3-145">If **GetService** returns null, Web API looks for a parameterless constructor on the controller class.</span></span>

## <a name="dependency-resolution-with-the-unity-container"></a><span data-ttu-id="bd3b3-146">依赖项解析与 Unity 容器</span><span class="sxs-lookup"><span data-stu-id="bd3b3-146">Dependency Resolution with the Unity Container</span></span>

<span data-ttu-id="bd3b3-147">尽管你可以编写的完整**IDependencyResolver**从零开始，该接口的实现真正旨在作为 Web API 和现有 IoC 容器之间的桥。</span><span class="sxs-lookup"><span data-stu-id="bd3b3-147">Although you could write a complete **IDependencyResolver** implementation from scratch, the interface is really designed to act as bridge between Web API and existing IoC containers.</span></span>

<span data-ttu-id="bd3b3-148">IoC 容器是一个软件组件，负责管理依赖关系。</span><span class="sxs-lookup"><span data-stu-id="bd3b3-148">An IoC container is a software component that is responsible for managing dependencies.</span></span> <span data-ttu-id="bd3b3-149">你向容器中，注册类型，然后使用容器以创建对象。</span><span class="sxs-lookup"><span data-stu-id="bd3b3-149">You register types with the container, and then use the container to create objects.</span></span> <span data-ttu-id="bd3b3-150">容器自动计算出的依赖关系。</span><span class="sxs-lookup"><span data-stu-id="bd3b3-150">The container automatically figures out the dependency relations.</span></span> <span data-ttu-id="bd3b3-151">多个 IoC 容器还可用于控制对象生存期和作用域等事务。</span><span class="sxs-lookup"><span data-stu-id="bd3b3-151">Many IoC containers also allow you to control things like object lifetime and scope.</span></span>

> [!NOTE]
> <span data-ttu-id="bd3b3-152">"IoC"代表"反向的控件"，它是常规的模式其中一个框架，调入应用程序代码。</span><span class="sxs-lookup"><span data-stu-id="bd3b3-152">"IoC" stands for "inversion of control", which is a general pattern where a framework calls into application code.</span></span> <span data-ttu-id="bd3b3-153">IoC 容器构造对象，其中"反转"常用控制流。</span><span class="sxs-lookup"><span data-stu-id="bd3b3-153">An IoC container constructs your objects for you, which "inverts" the usual flow of control.</span></span>


<span data-ttu-id="bd3b3-154">对于本教程中，我们将使用[Unity](https://msdn.microsoft.com/en-us/library/ff647202.aspx)从 Microsoft 模式&amp;做法。</span><span class="sxs-lookup"><span data-stu-id="bd3b3-154">For this tutorial, we'll use [Unity](https://msdn.microsoft.com/en-us/library/ff647202.aspx) from Microsoft Patterns &amp; Practices.</span></span> <span data-ttu-id="bd3b3-155">(其他常用库包括[城堡 Windsor](http://www.castleproject.org/)， [Spring.Net](http://www.springframework.net/)， [Autofac](https://code.google.com/p/autofac/)， [Ninject](http://www.ninject.org/)，和[StructureMap](http://docs.structuremap.net/).)NuGet 包管理器可用于安装 Unity。</span><span class="sxs-lookup"><span data-stu-id="bd3b3-155">(Other popular libraries include [Castle Windsor](http://www.castleproject.org/), [Spring.Net](http://www.springframework.net/), [Autofac](https://code.google.com/p/autofac/), [Ninject](http://www.ninject.org/), and [StructureMap](http://docs.structuremap.net/).) You can use NuGet Package Manager to install Unity.</span></span> <span data-ttu-id="bd3b3-156">从**工具**菜单在 Visual Studio 中，选择**库程序包管理器**，然后选择**程序包管理器控制台**。</span><span class="sxs-lookup"><span data-stu-id="bd3b3-156">From the **Tools** menu in Visual Studio, select **Library Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="bd3b3-157">在 Package Manager Console 窗口中，键入以下命令：</span><span class="sxs-lookup"><span data-stu-id="bd3b3-157">In the Package Manager Console window, type the following command:</span></span>

[!code-console[Main](dependency-injection/samples/sample7.cmd)]

<span data-ttu-id="bd3b3-158">下面是实现**IDependencyResolver**包装 Unity 容器。</span><span class="sxs-lookup"><span data-stu-id="bd3b3-158">Here is an implementation of **IDependencyResolver** that wraps a Unity container.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample8.cs)]

> [!NOTE]
> <span data-ttu-id="bd3b3-159">如果**GetService**方法不能解析类型，它应返回**null**。</span><span class="sxs-lookup"><span data-stu-id="bd3b3-159">If the **GetService** method cannot resolve a type, it should return **null**.</span></span> <span data-ttu-id="bd3b3-160">如果**GetServices**方法不能解析类型，则它应返回一个空集合对象。</span><span class="sxs-lookup"><span data-stu-id="bd3b3-160">If the **GetServices** method cannot resolve a type, it should return an empty collection object.</span></span> <span data-ttu-id="bd3b3-161">不引发异常的未知类型。</span><span class="sxs-lookup"><span data-stu-id="bd3b3-161">Don't throw exceptions for unknown types.</span></span>


## <a name="configuring-the-dependency-resolver"></a><span data-ttu-id="bd3b3-162">配置依赖项解析程序</span><span class="sxs-lookup"><span data-stu-id="bd3b3-162">Configuring the Dependency Resolver</span></span>

<span data-ttu-id="bd3b3-163">设置依赖项解析程序上**DependencyResolver**的全局属性**HttpConfiguration**对象。</span><span class="sxs-lookup"><span data-stu-id="bd3b3-163">Set the dependency resolver on the **DependencyResolver** property of the global **HttpConfiguration** object.</span></span>

<span data-ttu-id="bd3b3-164">下面的代码注册`IProductRepository`与 Unity 之间的接口，然后创建`UnityResolver`。</span><span class="sxs-lookup"><span data-stu-id="bd3b3-164">The following code registers the `IProductRepository` interface with Unity and then creates a `UnityResolver`.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample9.cs)]

## <a name="dependency-scope-and-controller-lifetime"></a><span data-ttu-id="bd3b3-165">依赖项作用域和控制器生存期</span><span class="sxs-lookup"><span data-stu-id="bd3b3-165">Dependency Scope and Controller Lifetime</span></span>

<span data-ttu-id="bd3b3-166">每个请求创建控制器。</span><span class="sxs-lookup"><span data-stu-id="bd3b3-166">Controllers are created per request.</span></span> <span data-ttu-id="bd3b3-167">若要管理对象生存期**IDependencyResolver**使用的概念*作用域*。</span><span class="sxs-lookup"><span data-stu-id="bd3b3-167">To manage object lifetimes, **IDependencyResolver** uses the concept of a *scope*.</span></span>

<span data-ttu-id="bd3b3-168">依赖项解析程序附加到**HttpConfiguration**对象具有全局作用域。</span><span class="sxs-lookup"><span data-stu-id="bd3b3-168">The dependency resolver attached to the **HttpConfiguration** object has global scope.</span></span> <span data-ttu-id="bd3b3-169">当 Web API 可创建控制器时，它将调用**如何**。</span><span class="sxs-lookup"><span data-stu-id="bd3b3-169">When Web API creates a controller, it calls **BeginScope**.</span></span> <span data-ttu-id="bd3b3-170">此方法返回**IDependencyScope**表示子范围。</span><span class="sxs-lookup"><span data-stu-id="bd3b3-170">This method returns an **IDependencyScope** that represents a child scope.</span></span>

<span data-ttu-id="bd3b3-171">然后 web API 调用**GetService**在子范围，可创建控制器上。</span><span class="sxs-lookup"><span data-stu-id="bd3b3-171">Web API then calls **GetService** on the child scope to create the controller.</span></span> <span data-ttu-id="bd3b3-172">完成请求时，Web API 调用**释放**在子作用域上。</span><span class="sxs-lookup"><span data-stu-id="bd3b3-172">When request is complete, Web API calls **Dispose** on the child scope.</span></span> <span data-ttu-id="bd3b3-173">使用**释放**方法来释放控制器的依赖关系。</span><span class="sxs-lookup"><span data-stu-id="bd3b3-173">Use the **Dispose** method to dispose of the controller's dependencies.</span></span>

<span data-ttu-id="bd3b3-174">如何实现**如何**取决于 IoC 容器。</span><span class="sxs-lookup"><span data-stu-id="bd3b3-174">How you implement **BeginScope** depends on the IoC container.</span></span> <span data-ttu-id="bd3b3-175">For Unity，作用域对应于子容器：</span><span class="sxs-lookup"><span data-stu-id="bd3b3-175">For Unity, scope corresponds to a child container:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample10.cs)]

<span data-ttu-id="bd3b3-176">大多数 IoC 容器具有类似的等效项。</span><span class="sxs-lookup"><span data-stu-id="bd3b3-176">Most IoC containers have similar equivalents.</span></span>
