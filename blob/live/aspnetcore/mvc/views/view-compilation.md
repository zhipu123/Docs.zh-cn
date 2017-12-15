---
title: "Razor 视图编译和预编译"
author: rick-anderson
description: "参考文档，以解释如何启用 MVC Razor 视图编译和 ASP.NET Core 应用程序中的预编译。"
keywords: "ASP.NET 核心，Razor 视图编译、 Razor 预编译、 Razor 预编译"
ms.author: riande
manager: wpickett
ms.date: 12/13/2017
ms.topic: article
ms.assetid: ab4705b7-1638-1638-bc97-ea7f292fe92a
ms.technology: aspnet
ms.prod: asp.net-core
uid: mvc/views/view-compilation
ms.openlocfilehash: 6839892c104673af0fd0fd074d368f3f42259d76
ms.sourcegitcommit: 198fb0488e961048bfa376cf58cb853ef1d1cb91
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2017
---
# <a name="razor-view-compilation-and-precompilation-in-aspnet-core"></a><span data-ttu-id="4fb68-104">Razor 视图编译和 ASP.NET Core 中的预编译</span><span class="sxs-lookup"><span data-stu-id="4fb68-104">Razor view compilation and precompilation in ASP.NET Core</span></span>

<span data-ttu-id="4fb68-105">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="4fb68-105">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="4fb68-106">调用视图时，则 razor 视图是在运行时编译。</span><span class="sxs-lookup"><span data-stu-id="4fb68-106">Razor views are compiled at runtime when the view is invoked.</span></span> <span data-ttu-id="4fb68-107">ASP.NET 核心 1.1.0 和更高版本可以根据需要编译 Razor 视图以及如何将它们部署与应用&mdash;称为预编译的过程。</span><span class="sxs-lookup"><span data-stu-id="4fb68-107">ASP.NET Core 1.1.0 and higher can optionally compile Razor views and deploy them with the app&mdash;a process known as precompilation.</span></span> <span data-ttu-id="4fb68-108">默认情况下，ASP.NET Core 2.x 项目模板启用预编译。</span><span class="sxs-lookup"><span data-stu-id="4fb68-108">The ASP.NET Core 2.x project templates enable precompilation by default.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4fb68-109">在执行时，razor 视图预编译是当前不可用[独立的部署 (SCD)](/dotnet/core/deploying/#self-contained-deployments-scd) ASP.NET 核心 2.0 中。</span><span class="sxs-lookup"><span data-stu-id="4fb68-109">Razor view precompilation is currently unavailable when performing a [self-contained deployment (SCD)](/dotnet/core/deploying/#self-contained-deployments-scd) in ASP.NET Core 2.0.</span></span> <span data-ttu-id="4fb68-110">2.1 版本时，此功能将被用于 Scd。</span><span class="sxs-lookup"><span data-stu-id="4fb68-110">The feature will be available for SCDs when 2.1 releases.</span></span> <span data-ttu-id="4fb68-111">有关详细信息，请参阅[视图编译失败适用于 Windows 上的 Linux 跨编译时](https://github.com/aspnet/MvcPrecompilation/issues/102)。</span><span class="sxs-lookup"><span data-stu-id="4fb68-111">For more information, see [View compilation fails when cross-compiling for Linux on Windows](https://github.com/aspnet/MvcPrecompilation/issues/102).</span></span>

<span data-ttu-id="4fb68-112">预编译的注意事项：</span><span class="sxs-lookup"><span data-stu-id="4fb68-112">Precompilation considerations:</span></span>

* <span data-ttu-id="4fb68-113">预编译视图生成较小的已发布的捆绑和更快的启动时间。</span><span class="sxs-lookup"><span data-stu-id="4fb68-113">Precompiling views results in a smaller published bundle and faster startup time.</span></span>
* <span data-ttu-id="4fb68-114">预编译视图后，无法编辑 Razor 文件。</span><span class="sxs-lookup"><span data-stu-id="4fb68-114">You can't edit Razor files after you precompile views.</span></span> <span data-ttu-id="4fb68-115">编辑的视图将不会出现在已发布的捆绑包。</span><span class="sxs-lookup"><span data-stu-id="4fb68-115">The edited views won't be present in the published bundle.</span></span> 

<span data-ttu-id="4fb68-116">部署预编译的视图：</span><span class="sxs-lookup"><span data-stu-id="4fb68-116">To deploy precompiled views:</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="4fb68-117">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="4fb68-117">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="4fb68-118">如果你的项目以.NET Framework 为目标，包括对的包引用[Microsoft.AspNetCore.Mvc.Razor.ViewCompilation](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.Razor.ViewCompilation/):</span><span class="sxs-lookup"><span data-stu-id="4fb68-118">If your project targets .NET Framework, include a package reference to [Microsoft.AspNetCore.Mvc.Razor.ViewCompilation](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.Razor.ViewCompilation/):</span></span>

```xml
<PackageReference Include="Microsoft.AspNetCore.Mvc.Razor.ViewCompilation" Version="2.0.0" PrivateAssets="All" />
```

<span data-ttu-id="4fb68-119">如果你的项目面向.NET 核心，不不需要进行任何更改。</span><span class="sxs-lookup"><span data-stu-id="4fb68-119">If your project targets .NET Core, no changes are necessary.</span></span>

<span data-ttu-id="4fb68-120">ASP.NET 核心 2.x 项目模板隐式设置`MvcRazorCompileOnPublish`到`true`默认情况下，这意味着此节点可以安全地删除从*.csproj*文件。</span><span class="sxs-lookup"><span data-stu-id="4fb68-120">The ASP.NET Core 2.x project templates implicitly set `MvcRazorCompileOnPublish` to `true` by default, which means this node can be safely removed from the *.csproj* file.</span></span> <span data-ttu-id="4fb68-121">如果想要为显式，没有设置任何影响`MvcRazorCompileOnPublish`属性`true`。</span><span class="sxs-lookup"><span data-stu-id="4fb68-121">If you prefer to be explicit, there's no harm in setting the `MvcRazorCompileOnPublish` property to `true`.</span></span> <span data-ttu-id="4fb68-122">以下*.csproj*示例重点介绍了此设置：</span><span class="sxs-lookup"><span data-stu-id="4fb68-122">The following *.csproj* sample highlights this setting:</span></span>

[!code-xml[Main](view-compilation\sample\MvcRazorCompileOnPublish2.csproj?highlight=5)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="4fb68-123">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="4fb68-123">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="4fb68-124">设置`MvcRazorCompileOnPublish`到`true`，并包含对的包引用`Microsoft.AspNetCore.Mvc.Razor.ViewCompilation`。</span><span class="sxs-lookup"><span data-stu-id="4fb68-124">Set `MvcRazorCompileOnPublish` to `true`, and include a package reference to `Microsoft.AspNetCore.Mvc.Razor.ViewCompilation`.</span></span> <span data-ttu-id="4fb68-125">以下*.csproj*示例重点介绍了这些设置：</span><span class="sxs-lookup"><span data-stu-id="4fb68-125">The following *.csproj* sample highlights these settings:</span></span>

[!code-xml[Main](view-compilation\sample\MvcRazorCompileOnPublish.csproj?highlight=5,12)]

---

<span data-ttu-id="4fb68-126">准备适用于的应用[framework 相关部署](/dotnet/core/deploying/#framework-dependent-deployments-fdd)通过执行如下所示在项目根目录命令：</span><span class="sxs-lookup"><span data-stu-id="4fb68-126">Prepare the app for a [framework-dependent deployment](/dotnet/core/deploying/#framework-dependent-deployments-fdd) by executing a command such as the following at the project root:</span></span>

```console
dotnet publish -c Release
```

<span data-ttu-id="4fb68-127">A *< 文件 > 的内容。PrecompiledViews.dll*如果预编译成功，则会生成包含已编译的 Razor 视图中，文件。</span><span class="sxs-lookup"><span data-stu-id="4fb68-127">A *<project_name>.PrecompiledViews.dll* file, containing the compiled Razor views, is produced when precompilation succeeds.</span></span> <span data-ttu-id="4fb68-128">例如，下面的屏幕截图描绘的内容*Index.cshtml*内*WebApplication1.PrecompiledViews.dll*:</span><span class="sxs-lookup"><span data-stu-id="4fb68-128">For example, the screenshot below depicts the contents of *Index.cshtml* inside of *WebApplication1.PrecompiledViews.dll*:</span></span>

![DLL 中的 razor 视图](view-compilation/_static/razor-views-in-dll.png)
