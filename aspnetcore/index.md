---
title: "ASP.NET Core 简介"
author: rick-anderson
description: "提供 ASP.NET Core 简介。"
keywords: ASP.NET Core
ms.author: riande
manager: wpickett
ms.date: 09/03/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: index
ms.openlocfilehash: a075c63fddb9e28a1da37d4ef6647808a0dcb583
ms.sourcegitcommit: 8f42ab93402c1b8044815e1e48d0bb84c81f8b59
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/29/2017
---
# <a name="introduction-to-aspnet-core"></a><span data-ttu-id="8775a-104">ASP.NET Core 简介</span><span class="sxs-lookup"><span data-stu-id="8775a-104">Introduction to ASP.NET Core</span></span>

<span data-ttu-id="8775a-105">作者：[Daniel Roth](https://github.com/danroth27)[Rick Anderson](https://twitter.com/RickAndMSFT) 和 [Shaun Luttin](https://twitter.com/dicshaunary)</span><span class="sxs-lookup"><span data-stu-id="8775a-105">By [Daniel Roth](https://github.com/danroth27), [Rick Anderson](https://twitter.com/RickAndMSFT), and [Shaun Luttin](https://twitter.com/dicshaunary)</span></span>

<span data-ttu-id="8775a-106">ASP.NET Core 是一个跨平台的高性能[开源](https://github.com/aspnet/home)框架，用于生成基于云且连接 Internet 的新式应用程序。</span><span class="sxs-lookup"><span data-stu-id="8775a-106">ASP.NET Core is a cross-platform, high-performance, [open-source](https://github.com/aspnet/home) framework for building modern, cloud-based, Internet-connected applications.</span></span> <span data-ttu-id="8775a-107">使用 ASP.NET Core，可以：</span><span class="sxs-lookup"><span data-stu-id="8775a-107">With ASP.NET Core, you can:</span></span>

* <span data-ttu-id="8775a-108">生成 Web 应用和服务、[IoT](https://www.microsoft.com/en-us/internet-of-things/) 应用和移动后端。</span><span class="sxs-lookup"><span data-stu-id="8775a-108">Build web apps and services, [IoT](https://www.microsoft.com/en-us/internet-of-things/) apps, and mobile backends.</span></span>
* <span data-ttu-id="8775a-109">在 Windows、macOS 和 Linux 上使用喜爱的开发工具。</span><span class="sxs-lookup"><span data-stu-id="8775a-109">Use your favorite development tools on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="8775a-110">部署到云或本地</span><span class="sxs-lookup"><span data-stu-id="8775a-110">Deploy to the cloud or on-premises</span></span>
* <span data-ttu-id="8775a-111">在 [.NET Core 或 .NET Framework](https://docs.microsoft.com/dotnet/articles/standard/choosing-core-framework-server) 上运行。</span><span class="sxs-lookup"><span data-stu-id="8775a-111">Run on [.NET Core or .NET Framework](https://docs.microsoft.com/dotnet/articles/standard/choosing-core-framework-server).</span></span>

## <a name="why-use-aspnet-core"></a><span data-ttu-id="8775a-112">为何使用 ASP.NET Core？</span><span class="sxs-lookup"><span data-stu-id="8775a-112">Why use ASP.NET Core?</span></span>

<span data-ttu-id="8775a-113">数百万开发人员在使用（并继续使用）ASP.NET 来创建 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="8775a-113">Millions of developers have used (and continue to use) ASP.NET to create web apps.</span></span> <span data-ttu-id="8775a-114">ASP.NET Core 是重新设计的 ASP.NET，对体系结构进行了更改，提供更精简的模块化框架。</span><span class="sxs-lookup"><span data-stu-id="8775a-114">ASP.NET Core is a redesign of ASP.NET, with architectural changes that result in a leaner and modular framework.</span></span>

<span data-ttu-id="8775a-115">ASP.NET Core 具有如下优点：</span><span class="sxs-lookup"><span data-stu-id="8775a-115">ASP.NET Core provides the following benefits:</span></span>

* <span data-ttu-id="8775a-116">生成 Web UI 和 Web API 的统一场景。</span><span class="sxs-lookup"><span data-stu-id="8775a-116">A unified story for building web UI and web APIs.</span></span>
* <span data-ttu-id="8775a-117">[新式客户端框架](xref:client-side/index)与开发工作流的集成。</span><span class="sxs-lookup"><span data-stu-id="8775a-117">Integration of [modern client-side frameworks](xref:client-side/index) and development workflows.</span></span>
* <span data-ttu-id="8775a-118">基于环境的云就绪[配置系统](xref:fundamentals/configuration/index)。</span><span class="sxs-lookup"><span data-stu-id="8775a-118">A cloud-ready, environment-based [configuration system](xref:fundamentals/configuration/index).</span></span>
* <span data-ttu-id="8775a-119">内置[依赖项注入](xref:fundamentals/dependency-injection)。</span><span class="sxs-lookup"><span data-stu-id="8775a-119">Built-in [dependency injection](xref:fundamentals/dependency-injection).</span></span>
* <span data-ttu-id="8775a-120">轻型高性能模块化 HTTP 请求管道。</span><span class="sxs-lookup"><span data-stu-id="8775a-120">A lightweight, high-performance, and modular HTTP request pipeline.</span></span>
* <span data-ttu-id="8775a-121">能够在 IIS 上进行托管或在自己的进程中进行自托管。</span><span class="sxs-lookup"><span data-stu-id="8775a-121">Ability to host on IIS or self-host in your own process.</span></span>
* <span data-ttu-id="8775a-122">可以在 [.NET Core](https://docs.microsoft.com/dotnet/articles/standard/choosing-core-framework-server) 上运行，支持真正的并行应用版本控制。</span><span class="sxs-lookup"><span data-stu-id="8775a-122">Can run on [.NET Core](https://docs.microsoft.com/dotnet/articles/standard/choosing-core-framework-server), which supports true side-by-side app versioning.</span></span>
* <span data-ttu-id="8775a-123">简化新式 Web 开发的工具。</span><span class="sxs-lookup"><span data-stu-id="8775a-123">Tooling that simplifies modern web development.</span></span>
* <span data-ttu-id="8775a-124">能够在 Windows、macOS 和 Linux 进行生成和运行。</span><span class="sxs-lookup"><span data-stu-id="8775a-124">Ability to build and run on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="8775a-125">开源和关注社区。</span><span class="sxs-lookup"><span data-stu-id="8775a-125">Open-source and community-focused.</span></span>

<span data-ttu-id="8775a-126">ASP.NET Core 完全作为 [NuGet](https://www.nuget.org/) 包的一部分提供。</span><span class="sxs-lookup"><span data-stu-id="8775a-126">ASP.NET Core ships entirely as [NuGet](https://www.nuget.org/) packages.</span></span> <span data-ttu-id="8775a-127">这可优化应用，使其只包含需要的 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="8775a-127">This allows you to optimize your app to include just the NuGet packages you need.</span></span> <span data-ttu-id="8775a-128">较小的应用图面区域的优势包括：提升安全性、减少维护和提高性能。</span><span class="sxs-lookup"><span data-stu-id="8775a-128">The benefits of a smaller app surface area include tighter security, reduced servicing, and improved performance.</span></span>

## <a name="build-web-apis-and-web-ui-using-aspnet-core-mvc"></a><span data-ttu-id="8775a-129">使用 ASP.NET Core MVC 生成 Web API 和 Web UI</span><span class="sxs-lookup"><span data-stu-id="8775a-129">Build web APIs and web UI using ASP.NET Core MVC</span></span>

<span data-ttu-id="8775a-130">ASP.NET Core MVC 提供帮助生成 [Web API](xref:tutorials/index#building-web-apis) 和 [Web 应用](xref:tutorials/index#building-web-applications)的功能：</span><span class="sxs-lookup"><span data-stu-id="8775a-130">ASP.NET Core MVC provides features that help you build [web APIs](xref:tutorials/index#building-web-apis) and [web apps](xref:tutorials/index#building-web-applications):</span></span>

* <span data-ttu-id="8775a-131">[Model-View-Controller (MVC) 模式](xref:mvc/overview) 使 Web API 和 Web 应用[可测试](testing/index.md)。</span><span class="sxs-lookup"><span data-stu-id="8775a-131">The [Model-View-Controller (MVC) pattern](xref:mvc/overview) helps make your web APIs and web apps [testable](testing/index.md).</span></span>
* <span data-ttu-id="8775a-132">[Razor 页面](xref:mvc/razor-pages/index)（2.0 中的新增功能）是基于页面的编程模式，它使 Web UI 的生成更加简单高效。</span><span class="sxs-lookup"><span data-stu-id="8775a-132">[Razor Pages](xref:mvc/razor-pages/index) (new in 2.0) is a page-based programming model that makes building web UI easier and more productive.</span></span>
* <span data-ttu-id="8775a-133">[Razor 语法](xref:mvc/views/razor)为 [Razor 页面](xref:mvc/razor-pages/index)和 [MVC 视图](xref:mvc/views/overview)提供高效的语言。</span><span class="sxs-lookup"><span data-stu-id="8775a-133">[Razor syntax](xref:mvc/views/razor) provides a productive language for [Razor Pages](xref:mvc/razor-pages/index) and [MVC Views](xref:mvc/views/overview).</span></span>
* <span data-ttu-id="8775a-134">[标记帮助程序](xref:mvc/views/tag-helpers/intro)使服务器端代码可以在 Razor 文件中参与创建和呈现 HTML 元素。</span><span class="sxs-lookup"><span data-stu-id="8775a-134">[Tag Helpers](xref:mvc/views/tag-helpers/intro) enable server-side code to participate in creating and rendering HTML elements in Razor files.</span></span>
* <span data-ttu-id="8775a-135">内置的[多数据格式和内容协商](mvc/models/formatting.md)支持使 Web API 可访问多种客户端，包括浏览器和移动设备。</span><span class="sxs-lookup"><span data-stu-id="8775a-135">Built-in support for [multiple data formats and content negotiation](mvc/models/formatting.md) lets your web APIs reach a broad range of clients, including browsers and mobile devices.</span></span>
* <span data-ttu-id="8775a-136">[模型绑定](xref:mvc/models/model-binding)自动将数据从 HTTP 请求映射到操作方法参数。</span><span class="sxs-lookup"><span data-stu-id="8775a-136">[Model Binding](xref:mvc/models/model-binding) automatically maps data from HTTP requests to action method parameters.</span></span>
* <span data-ttu-id="8775a-137">[模型验证](xref:mvc/models/validation)自动执行客户端和服务器端验证。</span><span class="sxs-lookup"><span data-stu-id="8775a-137">[Model Validation](xref:mvc/models/validation) automatically performs client and server-side validation.</span></span>

## <a name="client-side-development"></a><span data-ttu-id="8775a-138">客户端开发</span><span class="sxs-lookup"><span data-stu-id="8775a-138">Client-side development</span></span>

<span data-ttu-id="8775a-139">ASP.NET Core 经过精心设计，可与多种客户端框架无缝集成，包括 [AngularJS](xref:client-side/angular)、[KnockoutJS](xref:client-side/knockout) 和 [Bootstrap](xref:client-side/bootstrap)。</span><span class="sxs-lookup"><span data-stu-id="8775a-139">ASP.NET Core is designed to integrate seamlessly with a variety of client-side frameworks, including [AngularJS](xref:client-side/angular), [KnockoutJS](xref:client-side/knockout), and [Bootstrap](xref:client-side/bootstrap).</span></span> <span data-ttu-id="8775a-140">有关详细信息，请参阅[客户端开发](client-side/index.md)。</span><span class="sxs-lookup"><span data-stu-id="8775a-140">See [Client-side development](client-side/index.md) for more details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8775a-141">后续步骤</span><span class="sxs-lookup"><span data-stu-id="8775a-141">Next steps</span></span>

<span data-ttu-id="8775a-142">有关更多信息，请参见以下资源：</span><span class="sxs-lookup"><span data-stu-id="8775a-142">For more information, see the following resources:</span></span>

* [<span data-ttu-id="8775a-143">ASP.NET Core 教程</span><span class="sxs-lookup"><span data-stu-id="8775a-143">ASP.NET Core tutorials</span></span>](xref:tutorials/index)
* [<span data-ttu-id="8775a-144">ASP.NET Core 基础知识</span><span class="sxs-lookup"><span data-stu-id="8775a-144">ASP.NET Core fundamentals</span></span>](xref:fundamentals/index)
* <span data-ttu-id="8775a-145">[每周的 ASP.NET Community Standup](https://live.asp.net/) 介绍团队的进度和计划，包括新的博客和第三方软件。</span><span class="sxs-lookup"><span data-stu-id="8775a-145">[The weekly ASP.NET community standup](https://live.asp.net/) covers the team's progress and plans and features new blogs and third-party software.</span></span>
