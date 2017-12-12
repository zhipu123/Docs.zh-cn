---
uid: web-forms/videos/how-do-i/how-do-i-cache-an-aspnet-page-based-upon-information-in-the-http-header
title: "[如何:] ASP.NET 页基于 HTTP 标头中的信息的缓存 |Microsoft 文档"
author: rick-anderson
description: "在此视频 Chris Pels 演示如何在基于页面的 HTTP 标头中的信息 ASP.NET 输出缓存中保留一个页面。 首先，潜在 HTTP hea..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/26/2009
ms.topic: article
ms.assetid: 0f8df1bd-080a-4eeb-980c-c2fbb05d30c2
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-cache-an-aspnet-page-based-upon-information-in-the-http-header
msc.type: video
ms.openlocfilehash: fcb4b5e3b60bbcf3a0e5a95ff294bf41c7553a9d
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2017
---
<a name="how-do-i--cache-an-aspnet-page-based-upon-information-in-the-http-header"></a><span data-ttu-id="7174b-104">[如何:] 缓存 ASP.NET 页基于 HTTP 标头中的信息</span><span class="sxs-lookup"><span data-stu-id="7174b-104">[How Do I:]  Cache an ASP.NET Page Based Upon Information in the HTTP Header</span></span>
====================
<span data-ttu-id="7174b-105">通过[Chris Pels](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="7174b-105">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="7174b-106">在此视频 Chris Pels 演示如何在基于页面的 HTTP 标头中的信息 ASP.NET 输出缓存中保留一个页面。</span><span class="sxs-lookup"><span data-stu-id="7174b-106">In this video Chris Pels shows how to keep a page in the ASP.NET output cache based upon information in the page's HTTP header.</span></span> <span data-ttu-id="7174b-107">首先，评审潜在的 HTTP 标头值。</span><span class="sxs-lookup"><span data-stu-id="7174b-107">First, the potential HTTP header values are reviewed.</span></span> <span data-ttu-id="7174b-108">然后，创建了一个示例页，并随后将 OutputCache 指令用于 VaryByHeader 属性，其中包含一个值为"接受的语言"，一个 HTTP 标头，以控制缓存基于用户的浏览器的语言。</span><span class="sxs-lookup"><span data-stu-id="7174b-108">Then, a sample page is created and then the OutputCache directive is used with the VaryByHeader attribute which contains a value "accept-language", an HTTP header, to control caching based upon the language of the user's browser.</span></span> <span data-ttu-id="7174b-109">在 IE 设置为英语中，然后在 FireFox 设置为使用法语的查看示例页。</span><span class="sxs-lookup"><span data-stu-id="7174b-109">The sample page is viewed in IE which is set to English and then in FireFox which is set to use French.</span></span> <span data-ttu-id="7174b-110">最后，将讨论将缓存定义移到 CacheProfile web.config 文件中的选项。</span><span class="sxs-lookup"><span data-stu-id="7174b-110">Finally, the option to move the cache definition to a CacheProfile in the web.config file is discussed.</span></span>

[<span data-ttu-id="7174b-111">&#9654;观看视频 （12 分钟）</span><span class="sxs-lookup"><span data-stu-id="7174b-111">&#9654; Watch video (12 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-cache-an-aspnet-page-based-upon-information-in-the-http-header)
