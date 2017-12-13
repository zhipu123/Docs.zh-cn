---
title: "将文件上传至 ASP.NET Core 中的 Razor 页面"
author: guardrex
description: "了解如何将文件上传至 Razor 页面。"
keywords: "ASP.NET Core, Razor, Razor 页, IFormFile, 文件上传, fileupload"
ms.author: riande
manager: wpickett
ms.date: 09/12/2017
ms.topic: get-started-article
ms.technology: aspnet
ms.prod: aspnet-core
uid: tutorials/razor-pages/uploading-files
ms.openlocfilehash: 3b54bf0b40c396c8c141966219f65231fb362ca4
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2017
---
# <a name="uploading-files-to-a-razor-page-in-aspnet-core"></a><span data-ttu-id="96139-104">将文件上传至 ASP.NET Core 中的 Razor 页面</span><span class="sxs-lookup"><span data-stu-id="96139-104">Uploading files to a Razor Page in ASP.NET Core</span></span>

<span data-ttu-id="96139-105">作者：[Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="96139-105">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="96139-106">本部分演示使用 Razor 页面上传文件。</span><span class="sxs-lookup"><span data-stu-id="96139-106">In this section, uploading files with a Razor Page is demonstrated.</span></span>

<span data-ttu-id="96139-107">本教程中的 [Razor 页面 Movie 示例应用](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie)使用简单的模型绑定上传文件，非常适合上传小型文件。</span><span class="sxs-lookup"><span data-stu-id="96139-107">The [Razor Pages Movie sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie) in this tutorial uses simple model binding to upload files, which works well for uploading small files.</span></span> <span data-ttu-id="96139-108">有关流式传输大文件的信息，请参阅[通过流式传输上传大文件](xref:mvc/models/file-uploads#uploading-large-files-with-streaming)。</span><span class="sxs-lookup"><span data-stu-id="96139-108">For information on streaming large files, see [Uploading large files with streaming](xref:mvc/models/file-uploads#uploading-large-files-with-streaming).</span></span>

<span data-ttu-id="96139-109">执行以下步骤，可向示例应用添加电影计划文件上传功能。</span><span class="sxs-lookup"><span data-stu-id="96139-109">In the steps below, you add a movie schedule file upload feature to the sample app.</span></span> <span data-ttu-id="96139-110">每个电影计划由一个 `Schedule` 类表示。</span><span class="sxs-lookup"><span data-stu-id="96139-110">A movie schedule is represented by a `Schedule` class.</span></span> <span data-ttu-id="96139-111">该类包括两个版本的计划。</span><span class="sxs-lookup"><span data-stu-id="96139-111">The class includes two versions of the schedule.</span></span> <span data-ttu-id="96139-112">其中一个版本 (`PublicSchedule`) 提供给客户。</span><span class="sxs-lookup"><span data-stu-id="96139-112">One version is provided to customers, `PublicSchedule`.</span></span> <span data-ttu-id="96139-113">另一个版本 (`PrivateSchedule`) 用于公司员工。</span><span class="sxs-lookup"><span data-stu-id="96139-113">The other version is used for company employees, `PrivateSchedule`.</span></span> <span data-ttu-id="96139-114">每个版本作为单独的文件进行上传。</span><span class="sxs-lookup"><span data-stu-id="96139-114">Each version is uploaded as a separate file.</span></span> <span data-ttu-id="96139-115">本教程演示如何通过单个 POST 将两个文件上传至服务器。</span><span class="sxs-lookup"><span data-stu-id="96139-115">The tutorial demonstrates how to perform two file uploads from a page with a single POST to the server.</span></span>

## <a name="add-a-fileupload-class"></a><span data-ttu-id="96139-116">添加 FileUpload 类</span><span class="sxs-lookup"><span data-stu-id="96139-116">Add a FileUpload class</span></span>

<span data-ttu-id="96139-117">下面，创建 Razor 页以处理一对文件上载。</span><span class="sxs-lookup"><span data-stu-id="96139-117">Below, you create a Razor page to handle a pair of file uploads.</span></span> <span data-ttu-id="96139-118">添加 `FileUpload` 类（此类与页面绑定以获取计划数据）。</span><span class="sxs-lookup"><span data-stu-id="96139-118">Add a `FileUpload` class, which is bound to the page to obtain the schedule data.</span></span> <span data-ttu-id="96139-119">右键单击“Models”文件夹。</span><span class="sxs-lookup"><span data-stu-id="96139-119">Right click the *Models* folder.</span></span> <span data-ttu-id="96139-120">选择“添加” > “类”。</span><span class="sxs-lookup"><span data-stu-id="96139-120">Select **Add** > **Class**.</span></span> <span data-ttu-id="96139-121">将类命名为“FileUpload”，并添加以下属性：</span><span class="sxs-lookup"><span data-stu-id="96139-121">Name the class **FileUpload** and add the following properties:</span></span>

[!code-csharp[Main](razor-pages-start/sample/RazorPagesMovie/Models/FileUpload.cs)]

<span data-ttu-id="96139-122">此类有一个属性对应计划标题，另各有一个属性对应计划的两个版本。</span><span class="sxs-lookup"><span data-stu-id="96139-122">The class has a property for the schedule's title and a property for each of the two versions of the schedule.</span></span> <span data-ttu-id="96139-123">3 个属性皆为必需属性，标题长度必须为 3-60 个字符。</span><span class="sxs-lookup"><span data-stu-id="96139-123">All three properties are required, and the title must be 3-60 characters long.</span></span>

## <a name="add-a-helper-method-to-upload-files"></a><span data-ttu-id="96139-124">添加用于上传文件的 helper 方法</span><span class="sxs-lookup"><span data-stu-id="96139-124">Add a helper method to upload files</span></span>

<span data-ttu-id="96139-125">为避免处理未上传计划文件时出现代码重复，请首先上传一个静态 helper 方法。</span><span class="sxs-lookup"><span data-stu-id="96139-125">To avoid code duplication for processing uploaded schedule files, add a static helper method first.</span></span> <span data-ttu-id="96139-126">在此应用中创建一个“Utilities”文件夹，然后在“FileHelpers.cs”文件中添加以下内容。</span><span class="sxs-lookup"><span data-stu-id="96139-126">Create a *Utilities* folder in the app and add a *FileHelpers.cs* file with the following content.</span></span> <span data-ttu-id="96139-127">helper 方法 `ProcessFormFile` 接受 [IFormFile](/dotnet/api/microsoft.aspnetcore.http.iformfile) 和 [ModelStateDictionary](/api/microsoft.aspnetcore.mvc.modelbinding.modelstatedictionary)，并返回包含文件大小和内容的字符串。</span><span class="sxs-lookup"><span data-stu-id="96139-127">The helper method, `ProcessFormFile`, takes an [IFormFile](/dotnet/api/microsoft.aspnetcore.http.iformfile) and [ModelStateDictionary](/api/microsoft.aspnetcore.mvc.modelbinding.modelstatedictionary) and returns a string containing the file's size and content.</span></span> <span data-ttu-id="96139-128">检查内容类型和长度。</span><span class="sxs-lookup"><span data-stu-id="96139-128">The content type and length are checked.</span></span> <span data-ttu-id="96139-129">如果文件未通过验证检查，将向 `ModelState` 添加一个错误。</span><span class="sxs-lookup"><span data-stu-id="96139-129">If the file doesn't pass a validation check, an error is added to the `ModelState`.</span></span>

[!code-csharp[Main](razor-pages-start/sample/RazorPagesMovie/Utilities/FileHelpers.cs)]

## <a name="add-the-schedule-class"></a><span data-ttu-id="96139-130">添加 Schedule 类</span><span class="sxs-lookup"><span data-stu-id="96139-130">Add the Schedule class</span></span>

<span data-ttu-id="96139-131">右键单击“Models”文件夹。</span><span class="sxs-lookup"><span data-stu-id="96139-131">Right click the *Models* folder.</span></span> <span data-ttu-id="96139-132">选择“添加” > “类”。</span><span class="sxs-lookup"><span data-stu-id="96139-132">Select **Add** > **Class**.</span></span> <span data-ttu-id="96139-133">将类命名为“Schedule”，并添加以下属性：</span><span class="sxs-lookup"><span data-stu-id="96139-133">Name the class **Schedule** and add the following properties:</span></span>

[!code-csharp[Main](razor-pages-start/sample/RazorPagesMovie/Models/Schedule.cs)]

<span data-ttu-id="96139-134">此类使用 `Display` 和 `DisplayFormat` 特性，呈现计划数据时，这些特性会生成友好型的标题和格式。</span><span class="sxs-lookup"><span data-stu-id="96139-134">The class uses `Display` and `DisplayFormat` attributes, which produce friendly titles and formatting when the schedule data is rendered.</span></span>

## <a name="update-the-moviecontext"></a><span data-ttu-id="96139-135">更新 MovieContext</span><span class="sxs-lookup"><span data-stu-id="96139-135">Update the MovieContext</span></span>

<span data-ttu-id="96139-136">在 `MovieContext` (*Models/MovieContext.cs*) 中为计划指定 `DbSet`：</span><span class="sxs-lookup"><span data-stu-id="96139-136">Specify a `DbSet` in the `MovieContext` (*Models/MovieContext.cs*) for the schedules:</span></span>

[!code-csharp[Main](razor-pages-start/sample/RazorPagesMovie/Models/MovieContext.cs?highlight=13)]

## <a name="add-the-schedule-table-to-the-database"></a><span data-ttu-id="96139-137">将 Schedule 表添加到数据库</span><span class="sxs-lookup"><span data-stu-id="96139-137">Add the Schedule table to the database</span></span>

<span data-ttu-id="96139-138">打开包管理器控制台 (PMC)：“工具” > “NuGet 包管理器” > “包管理器控制台”。</span><span class="sxs-lookup"><span data-stu-id="96139-138">Open the Package Manger Console (PMC): **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>

![PMC 菜单](../first-mvc-app/adding-model/_static/pmc.png)

<span data-ttu-id="96139-140">在 PMC 中执行以下命令。</span><span class="sxs-lookup"><span data-stu-id="96139-140">In the PMC, execute the following commands.</span></span> <span data-ttu-id="96139-141">这些命令将向数据库添加 `Schedule` 表：</span><span class="sxs-lookup"><span data-stu-id="96139-141">These commands add a `Schedule` table to the database:</span></span>

```powershell
Add-Migration AddScheduleTable
Update-Database
```

## <a name="add-a-file-upload-razor-page"></a><span data-ttu-id="96139-142">添加文件上传 Razor 页面</span><span class="sxs-lookup"><span data-stu-id="96139-142">Add a file upload Razor Page</span></span>

<span data-ttu-id="96139-143">在“Pages”文件夹中创建“Schedules”文件夹。</span><span class="sxs-lookup"><span data-stu-id="96139-143">In the *Pages* folder, create a *Schedules* folder.</span></span> <span data-ttu-id="96139-144">在“Schedules”文件夹中，创建名为“Index.cshtml”的页面，用于上传具有如下内容的计划：</span><span class="sxs-lookup"><span data-stu-id="96139-144">In the *Schedules* folder, create a page named *Index.cshtml* for uploading a schedule with the following content:</span></span>

[!code-cshtml[Main](razor-pages-start/sample/RazorPagesMovie/Pages/Schedules/Index.cshtml)]

<span data-ttu-id="96139-145">每个窗体组包含一个 \<label>，它显示每个类属性的名称。</span><span class="sxs-lookup"><span data-stu-id="96139-145">Each form group includes a **\<label>** that displays the name of each class property.</span></span> <span data-ttu-id="96139-146">`FileUpload` 模型中的 `Display` 特性提供这些标签的显示值。</span><span class="sxs-lookup"><span data-stu-id="96139-146">The `Display` attributes in the `FileUpload` model provide the display values for the labels.</span></span> <span data-ttu-id="96139-147">例如，`UploadPublicSchedule` 特性的显示名称通过 `[Display(Name="Public Schedule")]` 进行设置，因此呈现窗体时会在此标签中显示“Public Schedule”。</span><span class="sxs-lookup"><span data-stu-id="96139-147">For example, the `UploadPublicSchedule` property's display name is set with `[Display(Name="Public Schedule")]` and thus displays "Public Schedule" in the label when the form renders.</span></span>

<span data-ttu-id="96139-148">每个窗体组包含一个验证 \<span>。</span><span class="sxs-lookup"><span data-stu-id="96139-148">Each form group includes a validation **\<span>**.</span></span> <span data-ttu-id="96139-149">如果用户输入未能满足 `FileUpload` 类中设置的属性特性，或者任何 `ProcessFormFile` 方法文件检查失败，则模型验证会失败。</span><span class="sxs-lookup"><span data-stu-id="96139-149">If the user's input fails to meet the property attributes set in the `FileUpload` class or if any of the `ProcessFormFile` method file validation checks fail, the model fails to validate.</span></span> <span data-ttu-id="96139-150">模型验证失败时，会向用户呈现有用的验证消息。</span><span class="sxs-lookup"><span data-stu-id="96139-150">When model validation fails, a helpful validation message is rendered to the user.</span></span> <span data-ttu-id="96139-151">例如，`Title` 属性带有 `[Required]` 和 `[StringLength(60, MinimumLength = 3)]` 注释。</span><span class="sxs-lookup"><span data-stu-id="96139-151">For example, the `Title` property is annotated with `[Required]` and `[StringLength(60, MinimumLength = 3)]`.</span></span> <span data-ttu-id="96139-152">用户若未提供标题，会接收到一条指示需要提供值的消息。</span><span class="sxs-lookup"><span data-stu-id="96139-152">If the user fails to supply a title, they receive a message indicating that a value is required.</span></span> <span data-ttu-id="96139-153">如果用户输入的值少于 3 个字符或多于 60 个字符，则会接收到一条指示值长度不正确的消息。</span><span class="sxs-lookup"><span data-stu-id="96139-153">If the user enters a value less than three characters or more than sixty characters, they receive a message indicating that the value has an incorrect length.</span></span> <span data-ttu-id="96139-154">如果提供不含内容的文件，则会显示一条指示文件为空的消息。</span><span class="sxs-lookup"><span data-stu-id="96139-154">If a file is provided that has no content, a message appears indicating that the file is empty.</span></span>

## <a name="add-the-code-behind-file"></a><span data-ttu-id="96139-155">添加代码隐藏文件</span><span class="sxs-lookup"><span data-stu-id="96139-155">Add the code-behind file</span></span>

<span data-ttu-id="96139-156">将代码隐藏文件 (Index.cshtml.cs) 添加到“Schedules”文件夹：</span><span class="sxs-lookup"><span data-stu-id="96139-156">Add the code-behind file (*Index.cshtml.cs*) to the *Schedules* folder:</span></span>

[!code-csharp[Main](razor-pages-start/sample/RazorPagesMovie/Pages/Schedules/Index.cshtml.cs)]

<span data-ttu-id="96139-157">页面模型（Index.cshtml.cs 中的 `IndexModel`）绑定 `FileUpload` 类：</span><span class="sxs-lookup"><span data-stu-id="96139-157">The page model (`IndexModel` in *Index.cshtml.cs*) binds the `FileUpload` class:</span></span>

[!code-csharp[Main](razor-pages-start/snapshot_sample/RazorPagesMovie/Pages/Schedules/Index.cshtml.cs?name=snippet1)]

<span data-ttu-id="96139-158">此模型还使用计划列表 (`IList<Schedule>`) 在页面上显示数据库中存储的计划：</span><span class="sxs-lookup"><span data-stu-id="96139-158">The model also uses a list of the schedules (`IList<Schedule>`) to display the schedules stored in the database on the page:</span></span>

[!code-csharp[Main](razor-pages-start/snapshot_sample/RazorPagesMovie/Pages/Schedules/Index.cshtml.cs?name=snippet2)]

<span data-ttu-id="96139-159">页面加载 `OnGetAsync` 时，会从数据库填充 `Schedules`，用于生成已加载计划的 HTML 表：</span><span class="sxs-lookup"><span data-stu-id="96139-159">When the page loads with `OnGetAsync`, `Schedules` is populated from the database and used to generate an HTML table of loaded schedules:</span></span>

[!code-csharp[Main](razor-pages-start/snapshot_sample/RazorPagesMovie/Pages/Schedules/Index.cshtml.cs?name=snippet3)]

<span data-ttu-id="96139-160">将窗体发布到服务器时，会检查 `ModelState`。</span><span class="sxs-lookup"><span data-stu-id="96139-160">When the form is posted to the server, the `ModelState` is checked.</span></span> <span data-ttu-id="96139-161">如果无效，会重新生成 `Schedule`，且页面会呈现一个或多个验证消息，陈述页面验证失败的原因。</span><span class="sxs-lookup"><span data-stu-id="96139-161">If invalid, `Schedule` is rebuilt, and the page renders with one or more validation messages stating why page validation failed.</span></span> <span data-ttu-id="96139-162">如果有效，`FileUpload` 属性将用于“OnPostAsync”中，以完成两个计划版本的文件上传，并创建一个用于存储数据的新 `Schedule` 对象。</span><span class="sxs-lookup"><span data-stu-id="96139-162">If valid, the `FileUpload` properties are used in *OnPostAsync* to complete the file upload for the two versions of the schedule and to create a new `Schedule` object to store the data.</span></span> <span data-ttu-id="96139-163">然后会将此计划保存到数据库：</span><span class="sxs-lookup"><span data-stu-id="96139-163">The schedule is then saved to the database:</span></span>

[!code-csharp[Main](razor-pages-start/snapshot_sample/RazorPagesMovie/Pages/Schedules/Index.cshtml.cs?name=snippet4)]

## <a name="link-the-file-upload-razor-page"></a><span data-ttu-id="96139-164">链接文件上传 Razor 页面</span><span class="sxs-lookup"><span data-stu-id="96139-164">Link the file upload Razor Page</span></span>

<span data-ttu-id="96139-165">打开“_Layout.cshtml”，然后向导航栏添加一个链接以访问文件上传页面：</span><span class="sxs-lookup"><span data-stu-id="96139-165">Open *_Layout.cshtml* and add a link to the navigation bar to reach the file upload page:</span></span>

[!code-cshtml[Main](razor-pages-start/sample/RazorPagesMovie/Pages/_Layout.cshtml?range=31-38&highlight=4)]

## <a name="add-a-page-to-confirm-schedule-deletion"></a><span data-ttu-id="96139-166">添加计划删除确认页面</span><span class="sxs-lookup"><span data-stu-id="96139-166">Add a page to confirm schedule deletion</span></span>

<span data-ttu-id="96139-167">用户单击删除计划时，应为其提供取消此操作的机会。</span><span class="sxs-lookup"><span data-stu-id="96139-167">When the user clicks to delete a schedule, you want them to have a chance to cancel the operation.</span></span> <span data-ttu-id="96139-168">向“Schedules”文件夹添加删除确认页面 (Delete.cshtml)：</span><span class="sxs-lookup"><span data-stu-id="96139-168">Add a delete confirmation page (*Delete.cshtml*) to the *Schedules* folder:</span></span>

[!code-cshtml[Main](razor-pages-start/sample/RazorPagesMovie/Pages/Schedules/Delete.cshtml)]

<span data-ttu-id="96139-169">代码隐藏文件 (Delete.cshtml.cs) 在请求的路由数据中加载由 `id` 标识的单个计划。</span><span class="sxs-lookup"><span data-stu-id="96139-169">The code-behind file (*Delete.cshtml.cs*) loads a single schedule identified by `id` in the request's route data.</span></span> <span data-ttu-id="96139-170">将“Delete.cshtml.cs”文件添加到“Schedules”文件夹：</span><span class="sxs-lookup"><span data-stu-id="96139-170">Add the *Delete.cshtml.cs* file to the *Schedules* folder:</span></span>

[!code-csharp[Main](razor-pages-start/sample/RazorPagesMovie/Pages/Schedules/Delete.cshtml.cs)]

<span data-ttu-id="96139-171">`OnPostAsync` 方法按 `id` 处理计划删除：</span><span class="sxs-lookup"><span data-stu-id="96139-171">The `OnPostAsync` method handles deleting the schedule by its `id`:</span></span>

[!code-csharp[Main](razor-pages-start/snapshot_sample/RazorPagesMovie/Pages/Schedules/Delete.cshtml.cs?name=snippet1&highlight=8,12-13)]

<span data-ttu-id="96139-172">成功删除计划后，`RedirectToPage` 将返回到计划的“Index.cshtml”页面。</span><span class="sxs-lookup"><span data-stu-id="96139-172">After successfully deleting the schedule, the `RedirectToPage` sends the user back to the schedules *Index.cshtml* page.</span></span>

## <a name="the-working-schedules-razor-page"></a><span data-ttu-id="96139-173">有效的 Schedules Razor 页面</span><span class="sxs-lookup"><span data-stu-id="96139-173">The working Schedules Razor Page</span></span>

<span data-ttu-id="96139-174">页面加载时，计划标题、公用计划和专用计划的标签和输入将呈现提交按钮：</span><span class="sxs-lookup"><span data-stu-id="96139-174">When the page loads, labels and inputs for schedule title, public schedule, and private schedule are rendered with a submit button:</span></span>

![按初始加载所示计划 Razor 页面，其中不含验证错误和空字段](uploading-files/_static/browser1.png)

<span data-ttu-id="96139-176">在不填充任何字段的情况下选择“上传”按钮会违反此模型上的 `[Required]` 特性。</span><span class="sxs-lookup"><span data-stu-id="96139-176">Selecting the **Upload** button without populating any of the fields violates the `[Required]` attributes on the model.</span></span> <span data-ttu-id="96139-177">`ModelState` 无效。</span><span class="sxs-lookup"><span data-stu-id="96139-177">The `ModelState` is invalid.</span></span> <span data-ttu-id="96139-178">会向用户显示验证错误消息：</span><span class="sxs-lookup"><span data-stu-id="96139-178">The validation error messages are displayed to the user:</span></span>

![验证错误消息显示在每个输入控件旁边](uploading-files/_static/browser2.png)

<span data-ttu-id="96139-180">在“标题”字段中键入两个字母。</span><span class="sxs-lookup"><span data-stu-id="96139-180">Type two letters into the **Title** field.</span></span> <span data-ttu-id="96139-181">验证消息改为指示标题长度必须介于 3-60 个字符之间：</span><span class="sxs-lookup"><span data-stu-id="96139-181">The validation message changes to indicate that the title must be between 3-60 characters:</span></span>

![标题验证消息已更改](uploading-files/_static/browser3.png)

<span data-ttu-id="96139-183">上传一个或多个计划时，“已加载计划”部分会显示已加载计划：</span><span class="sxs-lookup"><span data-stu-id="96139-183">When one or more schedules are uploaded, the **Loaded Schedules** section renders the loaded schedules:</span></span>

![已加载计划表，显示每个计划的标题、UTC 格式的上传日期、公用版本文件大小和专用版本文件大小](uploading-files/_static/browser4.png)

<span data-ttu-id="96139-185">用户可单击该表中的“删除”链接以访问删除确认视图，并在其中选择确认或取消删除操作。</span><span class="sxs-lookup"><span data-stu-id="96139-185">The user can click the **Delete** link from there to reach the delete confirmation view, where they have an opportunity to confirm or cancel the delete operation.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="96139-186">疑难解答</span><span class="sxs-lookup"><span data-stu-id="96139-186">Troubleshooting</span></span>

<span data-ttu-id="96139-187">有关上传 `IFormFile` 的疑难解答信息，请参阅 [ASP.NET Core 中的文件上传：疑难解答](xref:mvc/models/file-uploads#troubleshooting)。</span><span class="sxs-lookup"><span data-stu-id="96139-187">For troubleshooting information with `IFormFile` uploading, see the [File uploads in ASP.NET Core: Troubleshooting](xref:mvc/models/file-uploads#troubleshooting).</span></span>

<span data-ttu-id="96139-188">感谢读完这篇 Razor 页面简介。</span><span class="sxs-lookup"><span data-stu-id="96139-188">Thanks for completing this introduction to Razor Pages.</span></span> <span data-ttu-id="96139-189">我们期待你的意见。</span><span class="sxs-lookup"><span data-stu-id="96139-189">We appreciate any comments you leave.</span></span> <span data-ttu-id="96139-190">完成本教程后，大力推荐了解 [MVC 和 EF Core 入门](xref:data/ef-mvc/intro)。</span><span class="sxs-lookup"><span data-stu-id="96139-190">[Getting started with MVC and EF Core](xref:data/ef-mvc/intro) is an excellent follow up to this tutorial.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="96139-191">其他资源</span><span class="sxs-lookup"><span data-stu-id="96139-191">Additional resources</span></span>

* [<span data-ttu-id="96139-192">ASP.NET Core 中的文件上传</span><span class="sxs-lookup"><span data-stu-id="96139-192">File uploads in ASP.NET Core</span></span>](xref:mvc/models/file-uploads)
* [<span data-ttu-id="96139-193">IFormFile</span><span class="sxs-lookup"><span data-stu-id="96139-193">IFormFile</span></span>](/dotnet/api/microsoft.aspnetcore.http.iformfile)

>[!div class="step-by-step"]
[<span data-ttu-id="96139-194">上一篇：验证</span><span class="sxs-lookup"><span data-stu-id="96139-194">Previous: Validation</span></span>](xref:tutorials/razor-pages/validation)
