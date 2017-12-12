---
uid: web-pages/overview/ui-layouts-and-themes/twitter-helper
title: "Twitter 与 ASP.NET Web 页的帮助器 |Microsoft 文档"
author: tfitzmac
description: "此主题和应用程序演示如何将 Twitter 的帮助器添加到您的 WebMatrix 3 项目。 它包含的 Twitter 帮助器代码，并演示如何调用帮助器..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/07/2014
ms.topic: article
ms.assetid: c1a1244e-b9c8-42e6-a00b-8456a4ec027c
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/twitter-helper
msc.type: authoredcontent
ms.openlocfilehash: 07d9c4d485c42b78a42c54c9740af5f67cb44763
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2017
---
<a name="twitter-helper-with-aspnet-web-pages"></a><span data-ttu-id="37750-104">Twitter 与 ASP.NET Web 页的帮助器</span><span class="sxs-lookup"><span data-stu-id="37750-104">Twitter Helper with ASP.NET Web Pages</span></span>
====================
<span data-ttu-id="37750-105">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="37750-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="37750-106">此主题和应用程序演示如何将 Twitter 的帮助器添加到您的 WebMatrix 3 项目。</span><span class="sxs-lookup"><span data-stu-id="37750-106">This topic and application show how to add a Twitter Helper to your WebMatrix 3 project.</span></span> <span data-ttu-id="37750-107">它包含的 Twitter 帮助器代码，并演示如何调用的帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="37750-107">It contains the Twitter Helper code and shows how to call the helper methods.</span></span>
> 
> <span data-ttu-id="37750-108">这段代码用于 Twitter.cshtml 文件由开发**天平移**的 Microsoft。</span><span class="sxs-lookup"><span data-stu-id="37750-108">This code for the Twitter.cshtml file was developed by **Tian Pan** of Microsoft.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="37750-109">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="37750-109">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="37750-110">ASP.NET 网页 (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="37750-110">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="37750-111">本教程还适用于 ASP.NET Web Pages 2。</span><span class="sxs-lookup"><span data-stu-id="37750-111">This tutorial also works with ASP.NET Web Pages 2.</span></span>


## <a name="introduction"></a><span data-ttu-id="37750-112">介绍</span><span class="sxs-lookup"><span data-stu-id="37750-112">Introduction</span></span>

<span data-ttu-id="37750-113">本主题演示如何将 Twitter 的帮助器添加到你的应用程序并使用 Razor 语法来调用的帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="37750-113">This topic demonstrates how to add a Twitter Helper to your application and use Razor syntax to call the helper methods.</span></span> <span data-ttu-id="37750-114">Twitter 帮助器，可以轻松合并 Twitter 按钮和你的应用程序中的小组件。</span><span class="sxs-lookup"><span data-stu-id="37750-114">The Twitter Helper makes it easy to incorporate Twitter buttons and widgets in your application.</span></span> <span data-ttu-id="37750-115">若要使用 Twitter 小组件，如用户的时间线或哈希标记的搜索结果必须先创建[Twitter 上的小组件](https://twitter.com/settings/widgets)。</span><span class="sxs-lookup"><span data-stu-id="37750-115">To use a Twitter widget, such as a user's timeline or the search results for a hashtag, you must first create the [widget on Twitter](https://twitter.com/settings/widgets).</span></span> <span data-ttu-id="37750-116">在创建后你小组件，您将收到一个小组件 id。调用显示小组件的帮助器方法时，你将作为参数传递此小组件 id。</span><span class="sxs-lookup"><span data-stu-id="37750-116">After creating your widget, you will receive a widget id. You pass this widget id as a parameter when calling the helper methods that show widget.</span></span>

<span data-ttu-id="37750-117">本主题是版本 1.1 的 Twitter API 编写的。</span><span class="sxs-lookup"><span data-stu-id="37750-117">This topic was written for version 1.1 of the Twitter API.</span></span> <span data-ttu-id="37750-118">通过直接将 Twitter 帮助程序代码添加到你的项目，你可以更新的帮助器代码，如果 Twitter API 更改。</span><span class="sxs-lookup"><span data-stu-id="37750-118">By directly adding the Twitter Helper code to your project, you can update the helper code if the Twitter API changes.</span></span>

<span data-ttu-id="37750-119">有关安装 WebMatrix 的信息，请参阅[简介 ASP.NET 网页 2-入门](../getting-started/introducing-aspnet-web-pages-2/getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="37750-119">For information about installing WebMatrix, see [Introducing ASP.NET Web Pages 2 - Getting Started](../getting-started/introducing-aspnet-web-pages-2/getting-started.md).</span></span>

## <a name="add-twitter-helper-to-your-project"></a><span data-ttu-id="37750-120">将 Twitter 帮助器添加到你的项目</span><span class="sxs-lookup"><span data-stu-id="37750-120">Add Twitter Helper to your project</span></span>

<span data-ttu-id="37750-121">若要添加 Twitter 帮助程序，首先，添加名为的文件夹**应用\_代码**到你的项目。</span><span class="sxs-lookup"><span data-stu-id="37750-121">To add the Twitter Helper, first, add a folder named **App\_Code** to your project.</span></span> <span data-ttu-id="37750-122">然后，创建名为的文件**Twitter.cshtml**。</span><span class="sxs-lookup"><span data-stu-id="37750-122">Then, create a file named **Twitter.cshtml**.</span></span>

![App_Code 文件夹](twitter-helper/_static/image1.png)

<span data-ttu-id="37750-124">Twitter.cshtml 中的默认代码替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="37750-124">Replace the default code in Twitter.cshtml with the following code.</span></span>

[!code-cshtml[Main](twitter-helper/samples/sample1.cshtml)]

## <a name="call-twitter-methods-from-your-web-pages"></a><span data-ttu-id="37750-125">从 web 页面调用 Twitter 方法</span><span class="sxs-lookup"><span data-stu-id="37750-125">Call Twitter methods from your web pages</span></span>

<span data-ttu-id="37750-126">下面的示例演示如何在你的项目中使用从页的 Twitter 帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="37750-126">The following example shows how to use the Twitter Helper methods from a page in your project.</span></span> <span data-ttu-id="37750-127">在你的项目，你将想要将参数值替换为与你的需求相关的值。</span><span class="sxs-lookup"><span data-stu-id="37750-127">In your project, you will want to replace the parameter values with values that are relevant to your needs.</span></span> <span data-ttu-id="37750-128">你可以使用提供的小组件 id 来浏览方法的工作方式，但你将想要生成你自己的小组件为你的项目。</span><span class="sxs-lookup"><span data-stu-id="37750-128">You can use the provided widget ids to explore how the methods work, but you will want to generate your own widgets for your project.</span></span>

<span data-ttu-id="37750-129">不是所有下面所示的参数都是必需的。</span><span class="sxs-lookup"><span data-stu-id="37750-129">Not all of the parameters shown below are required.</span></span> <span data-ttu-id="37750-130">可选的参数用于自定义按钮或小组件的显示方式。</span><span class="sxs-lookup"><span data-stu-id="37750-130">The optional parameters are used to customize how the button or widget is displayed.</span></span> <span data-ttu-id="37750-131">例如，请按照按钮仅要求用户名称遵循，但该示例演示如何包含数量的追随者的用户，以及如何指定按钮和语言的大小。</span><span class="sxs-lookup"><span data-stu-id="37750-131">For example, the Follow Button only requires the user name to follow, but the example shows how to include the number of followers, and how specify the size of the button and the language.</span></span>

[!code-html[Main](twitter-helper/samples/sample2.html)]

## <a name="see-the-results"></a><span data-ttu-id="37750-132">查看结果</span><span class="sxs-lookup"><span data-stu-id="37750-132">See the results</span></span>

<span data-ttu-id="37750-133">上面的代码生成以下按钮和小组件。</span><span class="sxs-lookup"><span data-stu-id="37750-133">The above code produces the following buttons and widgets.</span></span> <span data-ttu-id="37750-134">这些按钮和小组件是功能完整的不屏幕快照。</span><span class="sxs-lookup"><span data-stu-id="37750-134">These buttons and widgets are fully-functional, not screenshots.</span></span> <span data-ttu-id="37750-135">请按照按钮将显示西班牙语，因为语言参数设置为**es**。</span><span class="sxs-lookup"><span data-stu-id="37750-135">The Follow Button is displayed in Spanish because the language parameter was set to **es**.</span></span>

### <a name="follow-button"></a><span data-ttu-id="37750-136">请按照按钮</span><span class="sxs-lookup"><span data-stu-id="37750-136">Follow Button</span></span>

<span data-ttu-id="37750-137">[请按照@aspnet)](https://twitter.com/aspnet)<script>！ 函数 （d、 s、 id） {var js，fjs = d.getElementsByTagName(s) [0]，p = /^http:/.test(d.location)？http: https;如果 (！ d.getElementById(id)) {js = d.createElement(s); js.id = id; js.src = p +: / / platform.twitter.com/widgets.js 的; fjs.parentNode.insertBefore （js，fjs）;}}（文档、 脚本、 twitter wjs）;</script></span><span class="sxs-lookup"><span data-stu-id="37750-137">[Follow @aspnet)](https://twitter.com/aspnet)<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + '://platform.twitter.com/widgets.js'; fjs.parentNode.insertBefore(js, fjs); } }(document, 'script', 'twitter-wjs');</script></span></span>

### <a name="tweet-button"></a><span data-ttu-id="37750-138">推文按钮</span><span class="sxs-lookup"><span data-stu-id="37750-138">Tweet Button</span></span>

<span data-ttu-id="37750-139">[推文](https://twitter.com/share)<script>！ 函数 （d、 s、 id） {var js，fjs = d.getElementsByTagName(s) [0]，p = /^http:/.test(d.location)？http: https;如果 (！ d.getElementById(id)) {js = d.createElement(s); js.id = id; js.src = p +: / / platform.twitter.com/widgets.js 的; fjs.parentNode.insertBefore （js，fjs）;}}（文档、 脚本、 twitter wjs）;</script></span><span class="sxs-lookup"><span data-stu-id="37750-139">[Tweet](https://twitter.com/share)<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + '://platform.twitter.com/widgets.js'; fjs.parentNode.insertBefore(js, fjs); } }(document, 'script', 'twitter-wjs');</script></span></span>

### <a name="user-timeline-profile"></a><span data-ttu-id="37750-140">用户时间线 （配置文件）</span><span class="sxs-lookup"><span data-stu-id="37750-140">User Timeline (Profile)</span></span>

<span data-ttu-id="37750-141">[通过推文@aspnet ](https://twitter.com/aspnet) <script>！ 函数 （d、 s、 id） {var js，fjs = d.getElementsByTagName(s) [0]，p = /^http:/.test(d.location)？http: https;如果 (！ d.getElementById(id)) {js = d.createElement(s); js.id = id; js.src = p +": / / platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore （js，fjs）;}}（文档、"脚本"、"twitter wjs"）;</script></span><span class="sxs-lookup"><span data-stu-id="37750-141">[Tweets by @aspnet](https://twitter.com/aspnet)<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script></span></span>

### <a name="favorites"></a><span data-ttu-id="37750-142">收藏夹</span><span class="sxs-lookup"><span data-stu-id="37750-142">Favorites</span></span>

<span data-ttu-id="37750-143">[收藏夹的推文通过@Microsoft ](https://twitter.com/Microsoft/favorites) <script>！ 函数 （d、 s、 id） {var js，fjs = d.getElementsByTagName(s) [0]，p = /^http:/.test(d.location)？http: https;如果 (！ d.getElementById(id)) {js = d.createElement(s); js.id = id; js.src = p +": / / platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore （js，fjs）;}}（文档、"脚本"、"twitter wjs"）;</script></span><span class="sxs-lookup"><span data-stu-id="37750-143">[Favorite Tweets by @Microsoft](https://twitter.com/Microsoft/favorites)<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script></span></span>

### <a name="list"></a><span data-ttu-id="37750-144">列表</span><span class="sxs-lookup"><span data-stu-id="37750-144">List</span></span>

<span data-ttu-id="37750-145">[从推文@Microsoft/MS\_使用者\_带区](https://twitter.com/microsoft/ms-consumer-brands/)<script>！ 函数 （d、 s、 id） {var js，fjs = d.getElementsByTagName(s) [0]，p = /^http:/.test(d.location)？http: https;如果 (！ d.getElementById(id)) {js = d.createElement(s); js.id = id; js.src = p +": / / platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore （js，fjs）;}}（文档、"脚本"、"twitter wjs"）;</script></span><span class="sxs-lookup"><span data-stu-id="37750-145">[Tweets from @Microsoft/MS\_Consumer\_Bands](https://twitter.com/microsoft/ms-consumer-brands/)<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script></span></span>

### <a name="search"></a><span data-ttu-id="37750-146">搜索</span><span class="sxs-lookup"><span data-stu-id="37750-146">Search</span></span>

<span data-ttu-id="37750-147">[有关推文&quot;#asp.net&quot;](https://twitter.com/search?q=%23asp.net)<script>！ 函数 （d、 s、 id） {var js，fjs = d.getElementsByTagName(s) [0]，p = /^http:/.test(d.location)？http: https;如果 (！ d.getElementById(id)) {js = d.createElement(s); js.id = id; js.src = p +": / / platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore （js，fjs）;}}（文档、"脚本"、"twitter wjs"）;</script></span><span class="sxs-lookup"><span data-stu-id="37750-147">[Tweets about &quot;#asp.net&quot;](https://twitter.com/search?q=%23asp.net)<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script></span></span>
