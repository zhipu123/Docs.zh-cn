---
uid: mvc/overview/older-versions-1/views/passing-data-to-view-master-pages-cs
title: "将数据传递到视图母版页 (C#) |Microsoft 文档"
author: microsoft
description: "本教程旨在说明如何为视图的母版页，从控制器传递数据。 我们检查用于将数据传递到视图 m 的两种策略..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/16/2008
ms.topic: article
ms.assetid: 5fee879b-8bde-42a9-a434-60ba6b1cf747
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/views/passing-data-to-view-master-pages-cs
msc.type: authoredcontent
ms.openlocfilehash: b8bc8ce0690d2e45877be75011d8883facbc74a7
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2017
---
<a name="passing-data-to-view-master-pages-c"></a><span data-ttu-id="f9bef-104">将数据传递给视图母版页 (C#)</span><span class="sxs-lookup"><span data-stu-id="f9bef-104">Passing Data to View Master Pages (C#)</span></span>
====================
<span data-ttu-id="f9bef-105">通过[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="f9bef-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="f9bef-106">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="f9bef-106">Download PDF</span></span>](http://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_13_CS.pdf)

> <span data-ttu-id="f9bef-107">本教程旨在说明如何为视图的母版页，从控制器传递数据。</span><span class="sxs-lookup"><span data-stu-id="f9bef-107">The goal of this tutorial is to explain how you can pass data from a controller to a view master page.</span></span> <span data-ttu-id="f9bef-108">我们检查用于将数据传递到视图的母版页的两种策略。</span><span class="sxs-lookup"><span data-stu-id="f9bef-108">We examine two strategies for passing data to a view master page.</span></span> <span data-ttu-id="f9bef-109">首先，我们讨论的简单解决方案，它会导致难以维护应用程序。</span><span class="sxs-lookup"><span data-stu-id="f9bef-109">First, we discuss an easy solution that results in an application that is difficult to maintain.</span></span> <span data-ttu-id="f9bef-110">接下来，我们检查需要稍有更多的初始工作，但在更容易维护的应用程序中的结果的更好的解决方案。</span><span class="sxs-lookup"><span data-stu-id="f9bef-110">Next, we examine a much better solution that requires a little more initial work but results in a much more maintainable application.</span></span>


## <a name="passing-data-to-view-master-pages"></a><span data-ttu-id="f9bef-111">将数据传递给视图母版页</span><span class="sxs-lookup"><span data-stu-id="f9bef-111">Passing Data to View Master Pages</span></span>

<span data-ttu-id="f9bef-112">本教程旨在说明如何为视图的母版页，从控制器传递数据。</span><span class="sxs-lookup"><span data-stu-id="f9bef-112">The goal of this tutorial is to explain how you can pass data from a controller to a view master page.</span></span> <span data-ttu-id="f9bef-113">我们检查用于将数据传递到视图的母版页的两种策略。</span><span class="sxs-lookup"><span data-stu-id="f9bef-113">We examine two strategies for passing data to a view master page.</span></span> <span data-ttu-id="f9bef-114">首先，我们讨论的简单解决方案，它会导致难以维护应用程序。</span><span class="sxs-lookup"><span data-stu-id="f9bef-114">First, we discuss an easy solution that results in an application that is difficult to maintain.</span></span> <span data-ttu-id="f9bef-115">接下来，我们检查需要稍有更多的初始工作，但在更容易维护的应用程序中的结果的更好的解决方案。</span><span class="sxs-lookup"><span data-stu-id="f9bef-115">Next, we examine a much better solution that requires a little more initial work but results in a much more maintainable application.</span></span>

### <a name="the-problem"></a><span data-ttu-id="f9bef-116">问题</span><span class="sxs-lookup"><span data-stu-id="f9bef-116">The Problem</span></span>

<span data-ttu-id="f9bef-117">假设你正在构建电影数据库应用程序，并且你想要在你的应用程序中每页上显示电影类别列表中的 （请参见图 1）。</span><span class="sxs-lookup"><span data-stu-id="f9bef-117">Imagine that you are building a movie database application and you want to display the list of movie categories on every page in your application (see Figure 1).</span></span> <span data-ttu-id="f9bef-118">此外，假设的电影类别列表存储在数据库表。</span><span class="sxs-lookup"><span data-stu-id="f9bef-118">Imagine, furthermore, that the list of movie categories is stored in a database table.</span></span> <span data-ttu-id="f9bef-119">在这种情况下，它会有一定意义从数据库检索类别并呈现电影类别视图的母版页中的列表。</span><span class="sxs-lookup"><span data-stu-id="f9bef-119">In that case, it would make sense to retrieve the categories from the database and render the list of movie categories within a view master page.</span></span>


<span data-ttu-id="f9bef-120">[![在视图的母版页中显示电影类别](passing-data-to-view-master-pages-cs/_static/image2.png)](passing-data-to-view-master-pages-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="f9bef-120">[![Displaying movie categories in a view master page](passing-data-to-view-master-pages-cs/_static/image2.png)](passing-data-to-view-master-pages-cs/_static/image1.png)</span></span>

<span data-ttu-id="f9bef-121">**图 01**： 电影类别显示在视图的母版页 ([单击以查看实际尺寸的图像](passing-data-to-view-master-pages-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="f9bef-121">**Figure 01**: Displaying movie categories in a view master page ([Click to view full-size image](passing-data-to-view-master-pages-cs/_static/image3.png))</span></span>


<span data-ttu-id="f9bef-122">下面是问题。</span><span class="sxs-lookup"><span data-stu-id="f9bef-122">Here's the problem.</span></span> <span data-ttu-id="f9bef-123">如何检索在母版页中的电影类别列表中？</span><span class="sxs-lookup"><span data-stu-id="f9bef-123">How do you retrieve the list of movie categories in the master page?</span></span> <span data-ttu-id="f9bef-124">它很容易在母版页中直接调用的模型类的方法。</span><span class="sxs-lookup"><span data-stu-id="f9bef-124">It is tempting to call methods of your model classes in the master page directly.</span></span> <span data-ttu-id="f9bef-125">换而言之，它很容易包括用于从母版页中的数据库权限检索数据的代码。</span><span class="sxs-lookup"><span data-stu-id="f9bef-125">In other words, it is tempting to include the code for retrieving the data from the database right in your master page.</span></span> <span data-ttu-id="f9bef-126">但是，绕过你的 MVC 控制器来访问数据库将违反是构建一个 MVC 应用程序的主要优点之一完全分离关注点。</span><span class="sxs-lookup"><span data-stu-id="f9bef-126">However, bypassing your MVC controllers to access the database would violate the clean separation of concerns that is one of the primary benefits of building an MVC application.</span></span>

<span data-ttu-id="f9bef-127">在 MVC 应用程序，你希望 MVC 视图和 MVC 模型均由你的 MVC 控制器之间的所有交互。</span><span class="sxs-lookup"><span data-stu-id="f9bef-127">In an MVC application, you want all interaction between your MVC views and your MVC model to be handled by your MVC controllers.</span></span> <span data-ttu-id="f9bef-128">这种问题将会导致更易于维护、 自适应，和可测试的应用程序。</span><span class="sxs-lookup"><span data-stu-id="f9bef-128">This separation of concerns results in a more maintainable, adaptable, and testable application.</span></span>

<span data-ttu-id="f9bef-129">在 MVC 应用程序，传递到 – 包括视图的母版页 – 视图的所有数据应通过的控制器操作都传递到视图。</span><span class="sxs-lookup"><span data-stu-id="f9bef-129">In an MVC application, all data passed to a view – including a view master page – should be passed to a view by a controller action.</span></span> <span data-ttu-id="f9bef-130">此外，数据应传递通过利用查看数据。</span><span class="sxs-lookup"><span data-stu-id="f9bef-130">Furthermore, the data should be passed by taking advantage of view data.</span></span> <span data-ttu-id="f9bef-131">在本教程的其余部分中，我将检查两种方法可以将视图数据传递到视图的母版页。</span><span class="sxs-lookup"><span data-stu-id="f9bef-131">In the remainder of this tutorial, I examine two methods of passing view data to a view master page.</span></span>

### <a name="the-simple-solution"></a><span data-ttu-id="f9bef-132">简单的解决方案</span><span class="sxs-lookup"><span data-stu-id="f9bef-132">The Simple Solution</span></span>

<span data-ttu-id="f9bef-133">让我们开始使用将从控制器的视图数据传递到视图的母版页的简单解决方案。</span><span class="sxs-lookup"><span data-stu-id="f9bef-133">Let's start with the simplest solution to passing view data from a controller to a view master page.</span></span> <span data-ttu-id="f9bef-134">最简单的解决方案是在每个控制器操作中传递主控页查看数据。</span><span class="sxs-lookup"><span data-stu-id="f9bef-134">The simplest solution is to pass the view data for the master page in each and every controller action.</span></span>

<span data-ttu-id="f9bef-135">请考虑列出 1 中的控制器。</span><span class="sxs-lookup"><span data-stu-id="f9bef-135">Consider the controller in Listing 1.</span></span> <span data-ttu-id="f9bef-136">它公开两个操作名为`Index()`和`Details()`。</span><span class="sxs-lookup"><span data-stu-id="f9bef-136">It exposes two actions named `Index()` and `Details()`.</span></span> <span data-ttu-id="f9bef-137">`Index()`操作方法会返回每个电影的电影数据库表中。</span><span class="sxs-lookup"><span data-stu-id="f9bef-137">The `Index()` action method returns every movie in the Movies database table.</span></span> <span data-ttu-id="f9bef-138">`Details()`操作方法会返回特定电影类别中每个影片。</span><span class="sxs-lookup"><span data-stu-id="f9bef-138">The `Details()` action method returns every movie in a particular movie category.</span></span>

<span data-ttu-id="f9bef-139">**列表 1 –`Controllers\HomeController.cs`**</span><span class="sxs-lookup"><span data-stu-id="f9bef-139">**Listing 1 – `Controllers\HomeController.cs`**</span></span>

[!code-csharp[Main](passing-data-to-view-master-pages-cs/samples/sample1.cs)]

<span data-ttu-id="f9bef-140">请注意，index （） 和 Details() 操作添加两项以查看数据。</span><span class="sxs-lookup"><span data-stu-id="f9bef-140">Notice that both the Index() and the Details() actions add two items to view data.</span></span> <span data-ttu-id="f9bef-141">Index （） 操作将添加两个密钥： 类别和影片。</span><span class="sxs-lookup"><span data-stu-id="f9bef-141">The Index() action adds two keys: categories and movies.</span></span> <span data-ttu-id="f9bef-142">类别键表示的电影类别显示视图的母版页的列表。</span><span class="sxs-lookup"><span data-stu-id="f9bef-142">The categories key represents the list of movie categories displayed by the view master page.</span></span> <span data-ttu-id="f9bef-143">电影键表示索引视图页中显示的影片的列表。</span><span class="sxs-lookup"><span data-stu-id="f9bef-143">The movies key represents the list of movies displayed by the Index view page.</span></span>

<span data-ttu-id="f9bef-144">Details() 操作还将添加名为类别和影片的两个密钥。</span><span class="sxs-lookup"><span data-stu-id="f9bef-144">The Details() action also adds two keys named categories and movies.</span></span> <span data-ttu-id="f9bef-145">类别键，同样，表示显示视图的母版页的电影类别的列表。</span><span class="sxs-lookup"><span data-stu-id="f9bef-145">The categories key, once again, represents the list of movie categories displayed by the view master page.</span></span> <span data-ttu-id="f9bef-146">电影键表示的详细信息视图页显示的特定类别中的影片列表 （请参见图 2）。</span><span class="sxs-lookup"><span data-stu-id="f9bef-146">The movies key represents the list of movies in a particular category displayed by the Details view page (see Figure 2).</span></span>


<span data-ttu-id="f9bef-147">[![详细信息视图](passing-data-to-view-master-pages-cs/_static/image5.png)](passing-data-to-view-master-pages-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="f9bef-147">[![The Details view](passing-data-to-view-master-pages-cs/_static/image5.png)](passing-data-to-view-master-pages-cs/_static/image4.png)</span></span>

<span data-ttu-id="f9bef-148">**图 02**: 的详细信息视图 ([单击以查看实际尺寸的图像](passing-data-to-view-master-pages-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="f9bef-148">**Figure 02**: The Details view ([Click to view full-size image](passing-data-to-view-master-pages-cs/_static/image6.png))</span></span>


<span data-ttu-id="f9bef-149">索引视图包含在清单 2。</span><span class="sxs-lookup"><span data-stu-id="f9bef-149">The Index view is contained in Listing 2.</span></span> <span data-ttu-id="f9bef-150">它只需循环访问由中查看数据的电影项表示的影片列表。</span><span class="sxs-lookup"><span data-stu-id="f9bef-150">It simply iterates through the list of movies represented by the movies item in view data.</span></span>

<span data-ttu-id="f9bef-151">**列出 2 –`Views\Home\Index.aspx`**</span><span class="sxs-lookup"><span data-stu-id="f9bef-151">**Listing 2 – `Views\Home\Index.aspx`**</span></span>

[!code-aspx[Main](passing-data-to-view-master-pages-cs/samples/sample2.aspx)]

<span data-ttu-id="f9bef-152">视图的母版页包含在清单 3。</span><span class="sxs-lookup"><span data-stu-id="f9bef-152">The view master page is contained in Listing 3.</span></span> <span data-ttu-id="f9bef-153">视图的母版页循环，并呈现所有影片类别由类别项表示从查看数据。</span><span class="sxs-lookup"><span data-stu-id="f9bef-153">The view master page iterates and renders all of the movie categories represented by the categories item from view data.</span></span>

<span data-ttu-id="f9bef-154">**列出 3 –`Views\Shared\Site.master`**</span><span class="sxs-lookup"><span data-stu-id="f9bef-154">**Listing 3 – `Views\Shared\Site.master`**</span></span>

[!code-aspx[Main](passing-data-to-view-master-pages-cs/samples/sample3.aspx)]

<span data-ttu-id="f9bef-155">通过查看数据情况下，所有数据都传递给视图和视图的母版页。</span><span class="sxs-lookup"><span data-stu-id="f9bef-155">All data is passed to the view and the view master page through view data.</span></span> <span data-ttu-id="f9bef-156">这是将数据传递给母版页的正确方法。</span><span class="sxs-lookup"><span data-stu-id="f9bef-156">That is the correct way to pass data to the master page.</span></span>

<span data-ttu-id="f9bef-157">因此，这是为什么使用此解决方案？</span><span class="sxs-lookup"><span data-stu-id="f9bef-157">So, what's wrong with this solution?</span></span> <span data-ttu-id="f9bef-158">问题是该解决方案违反了模拟 （不重复自己） 原则。</span><span class="sxs-lookup"><span data-stu-id="f9bef-158">The problem is that this solution violates the DRY (Don't Repeat Yourself) principle.</span></span> <span data-ttu-id="f9bef-159">每个控制器操作必须添加非常相同电影类别以查看数据的列表。</span><span class="sxs-lookup"><span data-stu-id="f9bef-159">Each and every controller action must add the very same list of movie categories to view data.</span></span> <span data-ttu-id="f9bef-160">在你的应用程序中有重复的代码使你的应用程序更难维护、 改编，和修改。</span><span class="sxs-lookup"><span data-stu-id="f9bef-160">Having duplicate code in your application makes your application much more difficult to maintain, adapt, and modify.</span></span>

### <a name="the-good-solution"></a><span data-ttu-id="f9bef-161">很好的解决方案</span><span class="sxs-lookup"><span data-stu-id="f9bef-161">The Good Solution</span></span>

<span data-ttu-id="f9bef-162">在此部分中，我们将检查到将数据从控制器操作传递到视图的母版页的替代，并更好地，解决方案。</span><span class="sxs-lookup"><span data-stu-id="f9bef-162">In this section, we examine an alternative, and better, solution to passing data from a controller action to a view master page.</span></span> <span data-ttu-id="f9bef-163">而不是在每个控制器操作中添加母版页的电影类别，我们将添加影片类别到查看数据一次。</span><span class="sxs-lookup"><span data-stu-id="f9bef-163">Instead of adding the movie categories for the master page in each and every controller action, we add the movie categories to the view data only once.</span></span> <span data-ttu-id="f9bef-164">应用程序控制器中添加了使用的视图的母版页的所有视图数据。</span><span class="sxs-lookup"><span data-stu-id="f9bef-164">All view data used by the view master page is added in an Application controller.</span></span>

<span data-ttu-id="f9bef-165">ApplicationController 类包含在清单 4。</span><span class="sxs-lookup"><span data-stu-id="f9bef-165">The ApplicationController class is contained in Listing 4.</span></span>

<span data-ttu-id="f9bef-166">**列出 4 –`Controllers\ApplicationController.cs`**</span><span class="sxs-lookup"><span data-stu-id="f9bef-166">**Listing 4 – `Controllers\ApplicationController.cs`**</span></span>

[!code-csharp[Main](passing-data-to-view-master-pages-cs/samples/sample4.cs)]

<span data-ttu-id="f9bef-167">有三个您应注意到了清单 4 中的应用程序控制器的操作。</span><span class="sxs-lookup"><span data-stu-id="f9bef-167">There are three things that you should notice about the Application controller in Listing 4.</span></span> <span data-ttu-id="f9bef-168">首先，请注意此类从 System.Web.Mvc.Controller 基类继承。</span><span class="sxs-lookup"><span data-stu-id="f9bef-168">First, notice that the class inherits from the base System.Web.Mvc.Controller class.</span></span> <span data-ttu-id="f9bef-169">应用程序控制器是一个控制器类。</span><span class="sxs-lookup"><span data-stu-id="f9bef-169">The Application controller is a controller class.</span></span>

<span data-ttu-id="f9bef-170">其次，请注意应用程序控制器类是一个抽象类。</span><span class="sxs-lookup"><span data-stu-id="f9bef-170">Second, notice that the Application controller class is an abstract class.</span></span> <span data-ttu-id="f9bef-171">一个抽象类是具体的类必须实现的类。</span><span class="sxs-lookup"><span data-stu-id="f9bef-171">An abstract class is a class that must be implemented by a concrete class.</span></span> <span data-ttu-id="f9bef-172">因为应用程序控制器是一个抽象类，你不能调用的类中直接定义任何方法。</span><span class="sxs-lookup"><span data-stu-id="f9bef-172">Because the Application controller is an abstract class, you cannot not invoke any methods defined in the class directly.</span></span> <span data-ttu-id="f9bef-173">如果你尝试直接调用应用程序类，然后你将获得找不到资源的错误消息。</span><span class="sxs-lookup"><span data-stu-id="f9bef-173">If you attempt to invoke the Application class directly then you'll get a Resource Cannot Be Found error message.</span></span>

<span data-ttu-id="f9bef-174">第三个，请注意，应用程序控制器包含将影片类别以查看数据的列表添加一个构造函数。</span><span class="sxs-lookup"><span data-stu-id="f9bef-174">Third, notice that the Application controller contains a constructor that adds the list of movie categories to view data.</span></span> <span data-ttu-id="f9bef-175">每个控制器类都继承自应用程序控制器将自动调用应用程序控制器构造函数。</span><span class="sxs-lookup"><span data-stu-id="f9bef-175">Every controller class that inherits from the Application controller calls the Application controller's constructor automatically.</span></span> <span data-ttu-id="f9bef-176">每当从应用程序控制器继承任何控制器上调用任何操作，电影类别是自动包含在视图的数据。</span><span class="sxs-lookup"><span data-stu-id="f9bef-176">Whenever you call any action on any controller that inherits from the Application controller, the movie categories is included in the view data automatically.</span></span>

<span data-ttu-id="f9bef-177">从应用程序控制器继承中列出 5 的电影控制器。</span><span class="sxs-lookup"><span data-stu-id="f9bef-177">The Movies controller in Listing 5 inherits from the Application controller.</span></span>

<span data-ttu-id="f9bef-178">**列出 5-`Controllers\MoviesController.cs`**</span><span class="sxs-lookup"><span data-stu-id="f9bef-178">**Listing 5 – `Controllers\MoviesController.cs`**</span></span>

[!code-csharp[Main](passing-data-to-view-master-pages-cs/samples/sample5.cs)]

<span data-ttu-id="f9bef-179">电影控制器上，就像在上一节中讨论的主页控制器公开名为的两个操作方法`Index()`和`Details()`。</span><span class="sxs-lookup"><span data-stu-id="f9bef-179">The Movies controller, just like the Home controller discussed in the previous section, exposes two action methods named `Index()` and `Details()`.</span></span> <span data-ttu-id="f9bef-180">请注意，电影类别显示视图的母版页由该列表不是添加到视图中的数据`Index()`或`Details()`方法。</span><span class="sxs-lookup"><span data-stu-id="f9bef-180">Notice that the list of movie categories displayed by the view master page is not added to view data in either the `Index()` or `Details()` method.</span></span> <span data-ttu-id="f9bef-181">由于从应用程序控制器继承电影控制器，则将添加电影类别列表中的自动查看数据。</span><span class="sxs-lookup"><span data-stu-id="f9bef-181">Because the Movies controller inherits from the Application controller, the list of movie categories is added to view data automatically.</span></span>

<span data-ttu-id="f9bef-182">请注意将视图的母版页的视图数据添加到此解决方案不违反干 （不重复自己） 原则。</span><span class="sxs-lookup"><span data-stu-id="f9bef-182">Notice that this solution to adding view data for a view master page does not violate the DRY (Don't Repeat Yourself) principle.</span></span> <span data-ttu-id="f9bef-183">将添加影片类别来查看数据列表中的代码包含仅在一个位置： 应用程序控制器的构造函数。</span><span class="sxs-lookup"><span data-stu-id="f9bef-183">The code for adding the list of movie categories to view data is contained in only one location: the constructor for the Application controller.</span></span>

### <a name="summary"></a><span data-ttu-id="f9bef-184">摘要</span><span class="sxs-lookup"><span data-stu-id="f9bef-184">Summary</span></span>

<span data-ttu-id="f9bef-185">在本教程中，我们讨论了两种方法来将从控制器的视图数据传递到视图的母版页。</span><span class="sxs-lookup"><span data-stu-id="f9bef-185">In this tutorial, we discussed two approaches to passing view data from a controller to a view master page.</span></span> <span data-ttu-id="f9bef-186">首先，我们探讨了一个简单，但难以维护方法。</span><span class="sxs-lookup"><span data-stu-id="f9bef-186">First, we examined a simple, but difficult to maintain approach.</span></span> <span data-ttu-id="f9bef-187">在第一个部分中，我们讨论了如何添加查看的视图的母版页数据中每个每个控制器操作应用程序中。</span><span class="sxs-lookup"><span data-stu-id="f9bef-187">In the first section, we discussed how you can add view data for a view master page in each every controller action in your application.</span></span> <span data-ttu-id="f9bef-188">我们的结论，这是错误的方法，因为它违反了模拟 （不重复自己） 原则。</span><span class="sxs-lookup"><span data-stu-id="f9bef-188">We concluded that this was a bad approach because it violates the DRY (Don't Repeat Yourself) principle.</span></span>

<span data-ttu-id="f9bef-189">接下来，我们探讨了用于添加数据视图的母版页需查看数据的多较好策略。</span><span class="sxs-lookup"><span data-stu-id="f9bef-189">Next, we examined a much better strategy for adding data required by a view master page to view data.</span></span> <span data-ttu-id="f9bef-190">而不是在每个控制器操作中添加的视图数据，我们添加了视图数据一次在应用程序控制器内。</span><span class="sxs-lookup"><span data-stu-id="f9bef-190">Instead of adding the view data in each and every controller action, we added the view data only once within an Application controller.</span></span> <span data-ttu-id="f9bef-191">这样一来，你就可以将数据传递到视图母版页中的 ASP.NET MVC 应用程序时避免重复代码。</span><span class="sxs-lookup"><span data-stu-id="f9bef-191">That way, you can avoid duplicate code when passing data to a view master page in an ASP.NET MVC application.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="f9bef-192">[上一页](creating-page-layouts-with-view-master-pages-cs.md)
[下一页](asp-net-mvc-views-overview-vb.md)</span><span class="sxs-lookup"><span data-stu-id="f9bef-192">[Previous](creating-page-layouts-with-view-master-pages-cs.md)
[Next](asp-net-mvc-views-overview-vb.md)</span></span>
