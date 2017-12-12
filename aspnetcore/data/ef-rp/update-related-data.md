---
title: "与 EF 核心-razor 页更新相关的数据-7 个 8"
author: rick-anderson
description: "在本教程中你将更新的更新外键字段和导航属性的相关的数据。"
keywords: "ASP.NET 核心，实体框架核心，相关数据，联接"
ms.author: riande
manager: wpickett
ms.date: 11/15/2017
ms.topic: get-started-article
ms.technology: aspnet
ms.prod: asp.net-core
uid: data/ef-rp/update-related-data
ms.openlocfilehash: f07a33c19ba1be623fae14228f8fbc909d766816
ms.sourcegitcommit: 6e46abd65973dea796d364a514de9ec2e3e1c1ed
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/02/2017
---
# <a name="updating-related-data---ef-core-razor-pages-7-of-8"></a><span data-ttu-id="35b54-104">更新相关的数据的 EF 核心 Razor 页 (7 个 8)</span><span class="sxs-lookup"><span data-stu-id="35b54-104">Updating related data - EF Core Razor Pages (7 of 8)</span></span>

<span data-ttu-id="35b54-105">通过[Tom Dykstra](https://github.com/tdykstra)，和[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="35b54-105">By [Tom Dykstra](https://github.com/tdykstra), and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE[about the series](../../includes/RP-EF/intro.md)]

<span data-ttu-id="35b54-106">本教程演示了更新相关的数据。</span><span class="sxs-lookup"><span data-stu-id="35b54-106">This tutorial demonstrates updating related data.</span></span> <span data-ttu-id="35b54-107">如果你遇到无法解决的问题，请下载[对此阶段已完成应用程序](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots/cu-part7)。</span><span class="sxs-lookup"><span data-stu-id="35b54-107">If you run into problems you can't solve, download the [completed app for this stage](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots/cu-part7).</span></span>

<span data-ttu-id="35b54-108">下图显示了一些已完成的页。</span><span class="sxs-lookup"><span data-stu-id="35b54-108">The following illustrations shows some of the completed pages.</span></span>

<span data-ttu-id="35b54-109">![课程编辑页面](update-related-data/_static/course-edit.png)
![教师编辑页](update-related-data/_static/instructor-edit-courses.png)</span><span class="sxs-lookup"><span data-stu-id="35b54-109">![Course Edit page](update-related-data/_static/course-edit.png)
![Instructor Edit page](update-related-data/_static/instructor-edit-courses.png)</span></span>

<span data-ttu-id="35b54-110">检查并测试创建和编辑课程页面。</span><span class="sxs-lookup"><span data-stu-id="35b54-110">Examine and test the Create and Edit course pages.</span></span> <span data-ttu-id="35b54-111">创建新的课程。</span><span class="sxs-lookup"><span data-stu-id="35b54-111">Create a new course.</span></span> <span data-ttu-id="35b54-112">由其主键 （整数），而不是其名称选择部门。</span><span class="sxs-lookup"><span data-stu-id="35b54-112">The department is selected by its primary key (an integer), not its name.</span></span> <span data-ttu-id="35b54-113">编辑新的过程。</span><span class="sxs-lookup"><span data-stu-id="35b54-113">Edit the new course.</span></span> <span data-ttu-id="35b54-114">完成测试后，删除新的过程。</span><span class="sxs-lookup"><span data-stu-id="35b54-114">When you have finished testing, delete the new course.</span></span>

## <a name="create-a-base-class-to-share-common-code"></a><span data-ttu-id="35b54-115">创建一个基本的类，以共享通用代码</span><span class="sxs-lookup"><span data-stu-id="35b54-115">Create a base class to share common code</span></span>

<span data-ttu-id="35b54-116">课程/创建和课程/编辑页每个需要部门名称的列表。</span><span class="sxs-lookup"><span data-stu-id="35b54-116">The Courses/Create and Courses/Edit pages each need a list of department names.</span></span> <span data-ttu-id="35b54-117">创建*Pages/Courses/DepartmentNamePageModel.cshtml.cs*基类的创建和编辑页：</span><span class="sxs-lookup"><span data-stu-id="35b54-117">Create the *Pages/Courses/DepartmentNamePageModel.cshtml.cs* base class for the Create and Edit pages:</span></span>

[!code-csharp[Main](intro/samples/cu/Pages/Courses/DepartmentNamePageModel.cshtml.cs?highlight=9,11,20-21)]

<span data-ttu-id="35b54-118">前面的代码创建[此时](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.mvc.rendering.selectlist?view=aspnetcore-2.0)用于包含部门名称的列表。</span><span class="sxs-lookup"><span data-stu-id="35b54-118">The preceding code creates a [SelectList](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.mvc.rendering.selectlist?view=aspnetcore-2.0) to contain the list of department names.</span></span> <span data-ttu-id="35b54-119">如果`selectedDepartment`指定，在中选择该部门`SelectList`。</span><span class="sxs-lookup"><span data-stu-id="35b54-119">If `selectedDepartment` is specified, that department is selected in the `SelectList`.</span></span>

<span data-ttu-id="35b54-120">创建和编辑页模型类都派生自`DepartmentNamePageModel`。</span><span class="sxs-lookup"><span data-stu-id="35b54-120">The Create and Edit page model classes will derive from `DepartmentNamePageModel`.</span></span>

## <a name="customize-the-courses-pages"></a><span data-ttu-id="35b54-121">自定义课程页</span><span class="sxs-lookup"><span data-stu-id="35b54-121">Customize the Courses Pages</span></span>

<span data-ttu-id="35b54-122">创建新的课程实体时，它必须具有与现有部门的关系。</span><span class="sxs-lookup"><span data-stu-id="35b54-122">When a new course entity is created, it must have a relationship to an existing department.</span></span> <span data-ttu-id="35b54-123">若要创建某一课程时添加一个部门，创建和编辑的基类包含下拉列表选择部门。</span><span class="sxs-lookup"><span data-stu-id="35b54-123">To add a department while creating a course, the base class for Create and Edit contains a drop-down list for selecting the department.</span></span> <span data-ttu-id="35b54-124">下拉列表设置`Course.DepartmentID`外键 (FK) 属性。</span><span class="sxs-lookup"><span data-stu-id="35b54-124">The drop-down list sets the `Course.DepartmentID` foreign key (FK) property.</span></span> <span data-ttu-id="35b54-125">EF 核心使用`Course.DepartmentID`FK 加载`Department`导航属性。</span><span class="sxs-lookup"><span data-stu-id="35b54-125">EF Core uses the `Course.DepartmentID` FK to load the `Department` navigation property.</span></span>

![创建过程](update-related-data/_static/ddl.png)

<span data-ttu-id="35b54-127">替换为以下代码更新创建页模型：</span><span class="sxs-lookup"><span data-stu-id="35b54-127">Update the Create page model with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Pages/Courses/Create.cshtml.cs?highlight=7,18,32-)]

<span data-ttu-id="35b54-128">前面的代码：</span><span class="sxs-lookup"><span data-stu-id="35b54-128">The preceding code:</span></span>

* <span data-ttu-id="35b54-129">派生自 `DepartmentNamePageModel`。</span><span class="sxs-lookup"><span data-stu-id="35b54-129">Derives from `DepartmentNamePageModel`.</span></span>
* <span data-ttu-id="35b54-130">使用`TryUpdateModelAsync`以防止[过多发布](xref:data/ef-rp/crud#overposting)。</span><span class="sxs-lookup"><span data-stu-id="35b54-130">Uses `TryUpdateModelAsync` to prevent [overposting](xref:data/ef-rp/crud#overposting).</span></span>
* <span data-ttu-id="35b54-131">替换`ViewData["DepartmentID"]`与`DepartmentNameSL`（从基类）。</span><span class="sxs-lookup"><span data-stu-id="35b54-131">Replaces `ViewData["DepartmentID"]` with `DepartmentNameSL` (from the base class).</span></span>

<span data-ttu-id="35b54-132">`ViewData["DepartmentID"]`替换为使用强类型化`DepartmentNameSL`。</span><span class="sxs-lookup"><span data-stu-id="35b54-132">`ViewData["DepartmentID"]` is replaced with the strongly typed `DepartmentNameSL`.</span></span> <span data-ttu-id="35b54-133">强类型化的模型被优先于弱化类型使用。</span><span class="sxs-lookup"><span data-stu-id="35b54-133">Strongly typed models are preferred over weakly typed.</span></span> <span data-ttu-id="35b54-134">有关详细信息，请参阅[弱类型化数据 （ViewData 和 ViewBag）](xref:mvc/views/overview#VD_VB)。</span><span class="sxs-lookup"><span data-stu-id="35b54-134">For more information, see [Weakly typed data (ViewData and ViewBag)](xref:mvc/views/overview#VD_VB).</span></span>

### <a name="update-the-courses-create-page"></a><span data-ttu-id="35b54-135">更新课程创建页</span><span class="sxs-lookup"><span data-stu-id="35b54-135">Update the Courses Create page</span></span>

<span data-ttu-id="35b54-136">更新*Pages/Courses/Create.cshtml*替换为以下标记：</span><span class="sxs-lookup"><span data-stu-id="35b54-136">Update *Pages/Courses/Create.cshtml* with the following markup:</span></span>

[!code-cshtml[Main](intro/samples/cu/Pages/Courses/Create.cshtml?highlight=29-34)]

<span data-ttu-id="35b54-137">前面的标记进行以下更改：</span><span class="sxs-lookup"><span data-stu-id="35b54-137">The preceding markup makes the following changes:</span></span>

* <span data-ttu-id="35b54-138">更改从标题**DepartmentID**到**部门**。</span><span class="sxs-lookup"><span data-stu-id="35b54-138">Changes the caption from **DepartmentID** to **Department**.</span></span>
* <span data-ttu-id="35b54-139">替换`"ViewBag.DepartmentID"`与`DepartmentNameSL`（从基类）。</span><span class="sxs-lookup"><span data-stu-id="35b54-139">Replaces `"ViewBag.DepartmentID"` with `DepartmentNameSL` (from the base class).</span></span>
* <span data-ttu-id="35b54-140">将添加"选择部门"选项。</span><span class="sxs-lookup"><span data-stu-id="35b54-140">Adds the "Select Department" option.</span></span> <span data-ttu-id="35b54-141">此更改而不是第一个部门呈现"选择部门"。</span><span class="sxs-lookup"><span data-stu-id="35b54-141">This change renders "Select Department" rather than the first department.</span></span>
* <span data-ttu-id="35b54-142">如果未选择部门，请添加一条验证消息。</span><span class="sxs-lookup"><span data-stu-id="35b54-142">Adds a validation message when the department is not selected.</span></span>

<span data-ttu-id="35b54-143">使用 Razor 页[选择标记帮助器](xref:mvc/views/working-with-forms#the-select-tag-helper):</span><span class="sxs-lookup"><span data-stu-id="35b54-143">The Razor Page uses the [Select Tag Helper](xref:mvc/views/working-with-forms#the-select-tag-helper):</span></span>

[!code-cshtml[Main](intro/samples/cu/Pages/Courses/Create.cshtml?range=28-35&highlight=3-6)]

<span data-ttu-id="35b54-144">创建页进行测试。</span><span class="sxs-lookup"><span data-stu-id="35b54-144">Test the Create page.</span></span> <span data-ttu-id="35b54-145">创建页显示部门名称，而不是部门 id。</span><span class="sxs-lookup"><span data-stu-id="35b54-145">The Create page displays the department name rather than the department ID.</span></span>

### <a name="update-the-courses-edit-page"></a><span data-ttu-id="35b54-146">更新课程编辑页。</span><span class="sxs-lookup"><span data-stu-id="35b54-146">Update the Courses Edit page.</span></span>

<span data-ttu-id="35b54-147">更新编辑页模型替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="35b54-147">Update the edit page model with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Pages/Courses/Edit.cshtml.cs?highlight=8,28,35,36,40,47-)]

<span data-ttu-id="35b54-148">在类似于那些在创建页模型中所做更改。</span><span class="sxs-lookup"><span data-stu-id="35b54-148">The changes are similar to those made in the Create page model.</span></span> <span data-ttu-id="35b54-149">在前面的代码中，`PopulateDepartmentsDropDownList`部门 ID，其中选择下拉列表中指定的部门的传递。</span><span class="sxs-lookup"><span data-stu-id="35b54-149">In the preceding code, `PopulateDepartmentsDropDownList` passes in the department ID, which select the department specified in the drop-down list.</span></span>

<span data-ttu-id="35b54-150">更新*Pages/Courses/Edit.cshtml*替换为以下标记：</span><span class="sxs-lookup"><span data-stu-id="35b54-150">Update *Pages/Courses/Edit.cshtml* with the following markup:</span></span>

[!code-cshtml[Main](intro/samples/cu/Pages/Courses/Edit.cshtml?highlight=17-20,32-35)]

<span data-ttu-id="35b54-151">前面的标记进行以下更改：</span><span class="sxs-lookup"><span data-stu-id="35b54-151">The preceding markup makes the following changes:</span></span>

* <span data-ttu-id="35b54-152">显示过程 id。</span><span class="sxs-lookup"><span data-stu-id="35b54-152">Displays the course ID.</span></span> <span data-ttu-id="35b54-153">通常在实体的主密钥 (PK) 不会显示。</span><span class="sxs-lookup"><span data-stu-id="35b54-153">Generally the Primary Key (PK) of an entity is not displayed.</span></span> <span data-ttu-id="35b54-154">Pk 将向用户通常毫无意义。</span><span class="sxs-lookup"><span data-stu-id="35b54-154">PKs are usually meaningless to users.</span></span> <span data-ttu-id="35b54-155">在这种情况下，在 PK 是过程数。</span><span class="sxs-lookup"><span data-stu-id="35b54-155">In this case, the PK is the course number.</span></span>
* <span data-ttu-id="35b54-156">更改从标题**DepartmentID**到**部门**。</span><span class="sxs-lookup"><span data-stu-id="35b54-156">Changes the caption from **DepartmentID** to **Department**.</span></span>
* <span data-ttu-id="35b54-157">替换`"ViewBag.DepartmentID"`与`DepartmentNameSL`（从基类）。</span><span class="sxs-lookup"><span data-stu-id="35b54-157">Replaces `"ViewBag.DepartmentID"` with `DepartmentNameSL` (from the base class).</span></span>
* <span data-ttu-id="35b54-158">将添加"选择部门"选项。</span><span class="sxs-lookup"><span data-stu-id="35b54-158">Adds the "Select Department" option.</span></span> <span data-ttu-id="35b54-159">此更改而不是第一个部门呈现"选择部门"。</span><span class="sxs-lookup"><span data-stu-id="35b54-159">This change renders "Select Department" rather than the first department.</span></span>
* <span data-ttu-id="35b54-160">如果未选择部门，请添加一条验证消息。</span><span class="sxs-lookup"><span data-stu-id="35b54-160">Adds a validation message when the department is not selected.</span></span>

<span data-ttu-id="35b54-161">页包含隐藏的字段 (`<input type="hidden">`) 过程数。</span><span class="sxs-lookup"><span data-stu-id="35b54-161">The page contains a hidden field (`<input type="hidden">`) for the course number.</span></span> <span data-ttu-id="35b54-162">添加`<label>`标记帮助器与`asp-for="Course.CourseID"`不消除隐藏字段的需要。</span><span class="sxs-lookup"><span data-stu-id="35b54-162">Adding a `<label>` tag helper with `asp-for="Course.CourseID"` doesn't eliminate the need for the hidden field.</span></span> <span data-ttu-id="35b54-163">`<input type="hidden">`需要的课程编号，以包括在已发布数据中，当用户单击**保存**。</span><span class="sxs-lookup"><span data-stu-id="35b54-163">`<input type="hidden">` is required for the course number to be included in the posted data when the user clicks **Save**.</span></span>

<span data-ttu-id="35b54-164">测试更新的代码。</span><span class="sxs-lookup"><span data-stu-id="35b54-164">Test the updated code.</span></span> <span data-ttu-id="35b54-165">创建、 编辑和删除过程。</span><span class="sxs-lookup"><span data-stu-id="35b54-165">Create, edit, and delete a course.</span></span>

## <a name="add-asnotracking-to-the-details-and-delete-page-models"></a><span data-ttu-id="35b54-166">将 AsNoTracking 添加到详细信息和删除页模型</span><span class="sxs-lookup"><span data-stu-id="35b54-166">Add AsNoTracking to the Details and Delete page models</span></span>

<span data-ttu-id="35b54-167">[AsNoTracking](https://docs.microsoft.com/dotnet/api/microsoft.entityframeworkcore.entityframeworkqueryableextensions.asnotracking?view=efcore-2.0#Microsoft_EntityFrameworkCore_EntityFrameworkQueryableExtensions_AsNoTracking__1_System_Linq_IQueryable___0__)跟踪不需要时可以提高性能。</span><span class="sxs-lookup"><span data-stu-id="35b54-167">[AsNoTracking](https://docs.microsoft.com/dotnet/api/microsoft.entityframeworkcore.entityframeworkqueryableextensions.asnotracking?view=efcore-2.0#Microsoft_EntityFrameworkCore_EntityFrameworkQueryableExtensions_AsNoTracking__1_System_Linq_IQueryable___0__) can improve performance when tracking is not required.</span></span> <span data-ttu-id="35b54-168">添加`AsNoTracking`到删除和详细信息页模型。</span><span class="sxs-lookup"><span data-stu-id="35b54-168">Add `AsNoTracking` to the Delete and Details page model.</span></span> <span data-ttu-id="35b54-169">下面的代码演示更新的删除页模型：</span><span class="sxs-lookup"><span data-stu-id="35b54-169">The following code shows the updated Delete page model:</span></span>

[!code-csharp[Main](intro/samples/cu/Pages/Courses/Delete.cshtml.cs?name=snippet&highlight=21,23,40,41)]

<span data-ttu-id="35b54-170">更新`OnGetAsync`中的方法*Pages/Courses/Details.cshtml.cs*文件：</span><span class="sxs-lookup"><span data-stu-id="35b54-170">Update the `OnGetAsync` method in the *Pages/Courses/Details.cshtml.cs* file:</span></span>

[!code-csharp[Main](intro/samples/cu/Pages/Courses/Details.cshtml.cs?name=snippet)]

### <a name="modify-the-delete-and-details-pages"></a><span data-ttu-id="35b54-171">修改删除和详细信息页</span><span class="sxs-lookup"><span data-stu-id="35b54-171">Modify the Delete and Details pages</span></span>

<span data-ttu-id="35b54-172">使用以下标记更新删除 Razor 页：</span><span class="sxs-lookup"><span data-stu-id="35b54-172">Update the Delete Razor page with the following markup:</span></span>

[!code-cshtml[Main](intro/samples/cu/Pages/Courses/Delete.cshtml?highlight=15-20)]

<span data-ttu-id="35b54-173">到详细信息页中进行相同的更改。</span><span class="sxs-lookup"><span data-stu-id="35b54-173">Make the same changes to the Details page.</span></span>

### <a name="test-the-course-pages"></a><span data-ttu-id="35b54-174">测试过程页面</span><span class="sxs-lookup"><span data-stu-id="35b54-174">Test the Course pages</span></span>

<span data-ttu-id="35b54-175">测试创建、 编辑，详细信息，和删除。</span><span class="sxs-lookup"><span data-stu-id="35b54-175">Test create, edit, details, and delete.</span></span>

## <a name="update-the-instructor-pages"></a><span data-ttu-id="35b54-176">更新教师页</span><span class="sxs-lookup"><span data-stu-id="35b54-176">Update the instructor pages</span></span>

<span data-ttu-id="35b54-177">下列各节更新教师页。</span><span class="sxs-lookup"><span data-stu-id="35b54-177">The following sections update the instructor pages.</span></span>

### <a name="add-office-location"></a><span data-ttu-id="35b54-178">添加 office 位置</span><span class="sxs-lookup"><span data-stu-id="35b54-178">Add office location</span></span>

<span data-ttu-id="35b54-179">在编辑教师记录时，你可能想要更新教师的办公室分配。</span><span class="sxs-lookup"><span data-stu-id="35b54-179">When editing an instructor record, you may want to update the instructor's office assignment.</span></span> <span data-ttu-id="35b54-180">`Instructor`实体具有对零或一一个关系`OfficeAssignment`实体。</span><span class="sxs-lookup"><span data-stu-id="35b54-180">The `Instructor` entity has a one-to-zero-or-one relationship with the `OfficeAssignment` entity.</span></span> <span data-ttu-id="35b54-181">教师代码必须处理：</span><span class="sxs-lookup"><span data-stu-id="35b54-181">The instructor code must handle:</span></span>

* <span data-ttu-id="35b54-182">如果用户清除 office 分配，删除`OfficeAssignment`实体。</span><span class="sxs-lookup"><span data-stu-id="35b54-182">If the user clears the office assignment, delete the `OfficeAssignment` entity.</span></span>
* <span data-ttu-id="35b54-183">如果用户输入一个办公室分配，且为空，创建一个新`OfficeAssignment`实体。</span><span class="sxs-lookup"><span data-stu-id="35b54-183">If the user enters an office assignment and it was empty, create a new `OfficeAssignment` entity.</span></span>
* <span data-ttu-id="35b54-184">如果用户更改 office 分配，更新`OfficeAssignment`实体。</span><span class="sxs-lookup"><span data-stu-id="35b54-184">If the user changes the office assignment, update the `OfficeAssignment` entity.</span></span>

<span data-ttu-id="35b54-185">替换为以下代码更新教师编辑页模型：</span><span class="sxs-lookup"><span data-stu-id="35b54-185">Update the instructors Edit page model with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Pages/Instructors/Edit1.cshtml.cs?name=snippet&highlight=20-23,32,39-)]

<span data-ttu-id="35b54-186">前面的代码：</span><span class="sxs-lookup"><span data-stu-id="35b54-186">The preceding code:</span></span>

- <span data-ttu-id="35b54-187">获取当前`Instructor`中使用的预先加载的数据库实体`OfficeAssignment`导航属性。</span><span class="sxs-lookup"><span data-stu-id="35b54-187">Gets the current `Instructor` entity from the database using eager loading for the `OfficeAssignment` navigation property.</span></span>
- <span data-ttu-id="35b54-188">更新检索`Instructor`模型联编程序中的值的实体。</span><span class="sxs-lookup"><span data-stu-id="35b54-188">Updates the retrieved `Instructor` entity with values from the model binder.</span></span> <span data-ttu-id="35b54-189">`TryUpdateModel`阻止[过多发布](xref:data/ef-rp/crud#overposting)。</span><span class="sxs-lookup"><span data-stu-id="35b54-189">`TryUpdateModel` prevents [overposting](xref:data/ef-rp/crud#overposting).</span></span>
- <span data-ttu-id="35b54-190">如果 office 位置为空，设置`Instructor.OfficeAssignment`为 null。</span><span class="sxs-lookup"><span data-stu-id="35b54-190">If the office location is blank, sets `Instructor.OfficeAssignment` to null.</span></span> <span data-ttu-id="35b54-191">当`Instructor.OfficeAssignment`是 null 中的相关的行`OfficeAssignment`删除表。</span><span class="sxs-lookup"><span data-stu-id="35b54-191">When `Instructor.OfficeAssignment` is null, the related row in the `OfficeAssignment` table is deleted.</span></span>

### <a name="update-the-instructor-edit-page"></a><span data-ttu-id="35b54-192">更新教师编辑页</span><span class="sxs-lookup"><span data-stu-id="35b54-192">Update the instructor Edit page</span></span>

<span data-ttu-id="35b54-193">更新*Pages/Instructors/Edit.cshtml*与办公地点：</span><span class="sxs-lookup"><span data-stu-id="35b54-193">Update *Pages/Instructors/Edit.cshtml* with the office location:</span></span>

[!code-cshtml[Main](intro/samples/cu/Pages/Instructors/Edit1.cshtml?highlight=29-33)]

<span data-ttu-id="35b54-194">验证可以更改教师办公地点。</span><span class="sxs-lookup"><span data-stu-id="35b54-194">Verify you can change an instructors office location.</span></span>

## <a name="add-course-assignments-to-the-instructor-edit-page"></a><span data-ttu-id="35b54-195">将课程作业添加到教师编辑页</span><span class="sxs-lookup"><span data-stu-id="35b54-195">Add Course assignments to the instructor Edit page</span></span>

<span data-ttu-id="35b54-196">教师可能讲解任意数量的课程。</span><span class="sxs-lookup"><span data-stu-id="35b54-196">Instructors may teach any number of courses.</span></span> <span data-ttu-id="35b54-197">在本部分中，你将添加能够更改课程作业。</span><span class="sxs-lookup"><span data-stu-id="35b54-197">In this section, you add the ability to change course assignments.</span></span> <span data-ttu-id="35b54-198">下图显示更新的教师编辑页：</span><span class="sxs-lookup"><span data-stu-id="35b54-198">The following image shows the updated instructor Edit page:</span></span>

![课程教师编辑页](update-related-data/_static/instructor-edit-courses.png)

<span data-ttu-id="35b54-200">`Course`和`Instructor`具有多对多关系。</span><span class="sxs-lookup"><span data-stu-id="35b54-200">`Course` and `Instructor` has a many-to-many relationship.</span></span> <span data-ttu-id="35b54-201">若要添加和删除关系，你可以添加和删除实体从`CourseAssignments`加入实体集。</span><span class="sxs-lookup"><span data-stu-id="35b54-201">To add and remove relationships, you add and remove entities from the `CourseAssignments` join entity set.</span></span>

<span data-ttu-id="35b54-202">复选框启用对一个教师分配给的课程的更改。</span><span class="sxs-lookup"><span data-stu-id="35b54-202">Check boxes enable changes to courses an instructor is assigned to.</span></span> <span data-ttu-id="35b54-203">在数据库中每个课程显示一个复选框。</span><span class="sxs-lookup"><span data-stu-id="35b54-203">A check box is displayed for every course in the database.</span></span> <span data-ttu-id="35b54-204">检查教师分配给的课程。</span><span class="sxs-lookup"><span data-stu-id="35b54-204">Courses that the instructor is assigned to are checked.</span></span> <span data-ttu-id="35b54-205">用户可以选择或清除复选框来更改过程分配。</span><span class="sxs-lookup"><span data-stu-id="35b54-205">The user can select or clear check boxes to change course assignments.</span></span> <span data-ttu-id="35b54-206">如果课程数大得多：</span><span class="sxs-lookup"><span data-stu-id="35b54-206">If the number of courses were much greater:</span></span>

* <span data-ttu-id="35b54-207">你可能需要使用不同的用户界面以显示课程。</span><span class="sxs-lookup"><span data-stu-id="35b54-207">You'd probably use a different user interface to display the courses.</span></span>
* <span data-ttu-id="35b54-208">操作创建或删除关系的联接实体的方法不会更改。</span><span class="sxs-lookup"><span data-stu-id="35b54-208">The method of manipulating a join entity to create or delete relationships would not change.</span></span>

### <a name="add-classes-to-support-create-and-edit-instructor-pages"></a><span data-ttu-id="35b54-209">添加类以支持创建和编辑教师页面</span><span class="sxs-lookup"><span data-stu-id="35b54-209">Add classes to support Create and Edit instructor pages</span></span>

<span data-ttu-id="35b54-210">创建*SchoolViewModels/AssignedCourseData.cs*替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="35b54-210">Create *SchoolViewModels/AssignedCourseData.cs* with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/SchoolViewModels/AssignedCourseData.cs)]

<span data-ttu-id="35b54-211">`AssignedCourseData`类包含数据以创建一个教师通过分配课程对应的复选框。</span><span class="sxs-lookup"><span data-stu-id="35b54-211">The `AssignedCourseData` class contains data to create the check boxes for assigned courses by an instructor.</span></span>

<span data-ttu-id="35b54-212">创建*Pages/Instructors/InstructorCoursesPageModel.cshtml.cs*基类：</span><span class="sxs-lookup"><span data-stu-id="35b54-212">Create the *Pages/Instructors/InstructorCoursesPageModel.cshtml.cs* base class:</span></span>

[!code-csharp[Main](intro/samples/cu/Pages/Instructors/InstructorCoursesPageModel.cshtml.cs)]

<span data-ttu-id="35b54-213">`InstructorCoursesPageModel`是将用于编辑和创建页模型的基类。</span><span class="sxs-lookup"><span data-stu-id="35b54-213">The `InstructorCoursesPageModel` is the base class you will use for the Edit and Create page models.</span></span> <span data-ttu-id="35b54-214">`PopulateAssignedCourseData`读取所有`Course`实体来填充`AssignedCourseDataList`。</span><span class="sxs-lookup"><span data-stu-id="35b54-214">`PopulateAssignedCourseData` reads all `Course` entities to populate `AssignedCourseDataList`.</span></span> <span data-ttu-id="35b54-215">对于每个课程中，该代码将设置`CourseID`，标题，并决定是否教师分配给过程。</span><span class="sxs-lookup"><span data-stu-id="35b54-215">For each course, the code sets the `CourseID`, title, and whether or not the instructor is assigned to the course.</span></span> <span data-ttu-id="35b54-216">A [HashSet](https://docs.microsoft.com/dotnet/api/system.collections.generic.hashset-1)用于创建高效的查找。</span><span class="sxs-lookup"><span data-stu-id="35b54-216">A [HashSet](https://docs.microsoft.com/dotnet/api/system.collections.generic.hashset-1) is used to create efficient lookups.</span></span>

### <a name="instructors-edit-page-model"></a><span data-ttu-id="35b54-217">教师编辑页模型</span><span class="sxs-lookup"><span data-stu-id="35b54-217">Instructors Edit page model</span></span>

<span data-ttu-id="35b54-218">替换为以下代码更新教师编辑页模型：</span><span class="sxs-lookup"><span data-stu-id="35b54-218">Update the instructor Edit page model with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Pages/Instructors/Edit.cshtml.cs?name=snippet&highlight=1,20-24,30,34,41-)]

<span data-ttu-id="35b54-219">前面的代码处理 office 分配更改。</span><span class="sxs-lookup"><span data-stu-id="35b54-219">The preceding code handles office assignment changes.</span></span>

<span data-ttu-id="35b54-220">更新教师 Razor 视图：</span><span class="sxs-lookup"><span data-stu-id="35b54-220">Update the instructor Razor View:</span></span>

[!code-cshtml[Main](intro/samples/cu/Pages/Instructors/Edit.cshtml?highlight=34-59)]

<a id="notepad"></a>
> [!NOTE]
> <span data-ttu-id="35b54-221">当你将代码粘贴到 Visual Studio 时，分行符都转换将中断代码的方式。</span><span class="sxs-lookup"><span data-stu-id="35b54-221">When you paste the code in Visual Studio, line breaks are changed in a way that breaks the code.</span></span> <span data-ttu-id="35b54-222">按 Ctrl + Z 一次撤消的自动格式设置。</span><span class="sxs-lookup"><span data-stu-id="35b54-222">Press Ctrl+Z one time to undo the automatic formatting.</span></span> <span data-ttu-id="35b54-223">Ctrl + Z，以便它们看起来像你在此处看到修复分行符。</span><span class="sxs-lookup"><span data-stu-id="35b54-223">Ctrl+Z fixes the line breaks so that they look like what you see here.</span></span> <span data-ttu-id="35b54-224">缩进不一定是完美的但`@</tr><tr>`， `@:<td>`， `@:</td>`，和`@:</tr>`行都必须在单独的行所示。</span><span class="sxs-lookup"><span data-stu-id="35b54-224">The indentation doesn't have to be perfect, but the `@</tr><tr>`, `@:<td>`, `@:</td>`, and `@:</tr>` lines must each be on a single line as shown.</span></span> <span data-ttu-id="35b54-225">与所选的新代码块，按 tab 键三次到了新代码与现有代码的行。</span><span class="sxs-lookup"><span data-stu-id="35b54-225">With the block of new code selected, press Tab three times to line up the new code with the existing code.</span></span> <span data-ttu-id="35b54-226">对投票或查看此 bug 的状态[与此链接](https://developercommunity.visualstudio.com/content/problem/147795/razor-editor-malforms-pasted-markup-and-creates-in.html)。</span><span class="sxs-lookup"><span data-stu-id="35b54-226">Vote on or review the status of this bug [with this link](https://developercommunity.visualstudio.com/content/problem/147795/razor-editor-malforms-pasted-markup-and-creates-in.html).</span></span>

<span data-ttu-id="35b54-227">前面的代码创建一个 HTML 表，包含三列。</span><span class="sxs-lookup"><span data-stu-id="35b54-227">The preceding code creates an HTML table that has three columns.</span></span> <span data-ttu-id="35b54-228">每列均具有一个复选框和包含课程编号及标题的标题。</span><span class="sxs-lookup"><span data-stu-id="35b54-228">Each column has a check box and a caption containing the course number and title.</span></span> <span data-ttu-id="35b54-229">所有对应的复选框具有相同的名称 ("selectedCourses")。</span><span class="sxs-lookup"><span data-stu-id="35b54-229">The check boxes all have the same name ("selectedCourses").</span></span> <span data-ttu-id="35b54-230">使用相同的名称会通知模型联编程序来将它们视为一个组。</span><span class="sxs-lookup"><span data-stu-id="35b54-230">Using the same name informs the model binder to treat them as a group.</span></span> <span data-ttu-id="35b54-231">每个复选框的值属性设置为`CourseID`。</span><span class="sxs-lookup"><span data-stu-id="35b54-231">The value attribute of each check box is set to `CourseID`.</span></span> <span data-ttu-id="35b54-232">模型联编程序当发页面时，将传递一个数组，其中包含`CourseID`仅复选框选择的值。</span><span class="sxs-lookup"><span data-stu-id="35b54-232">When the page is posted, the model binder passes an array that consists of the `CourseID` values for only the check boxes that are selected.</span></span>

<span data-ttu-id="35b54-233">当最初呈现复选框时，分配给教师课程签入属性。</span><span class="sxs-lookup"><span data-stu-id="35b54-233">When the check boxes are initially rendered, courses assigned to the instructor have checked attributes.</span></span>

<span data-ttu-id="35b54-234">运行应用和测试更新的教师编辑页。</span><span class="sxs-lookup"><span data-stu-id="35b54-234">Run the app and test the updated instructors Edit page.</span></span> <span data-ttu-id="35b54-235">更改某些过程分配。</span><span class="sxs-lookup"><span data-stu-id="35b54-235">Change some course assignments.</span></span> <span data-ttu-id="35b54-236">所做的更改会反映在索引页面。</span><span class="sxs-lookup"><span data-stu-id="35b54-236">The changes are reflected on the Index page.</span></span>

<span data-ttu-id="35b54-237">注意： 采取此处编辑教师课程数据的做法适用于没有有限的数量的课程。</span><span class="sxs-lookup"><span data-stu-id="35b54-237">Note: The approach taken here to edit instructor course data works well when there is a limited number of courses.</span></span> <span data-ttu-id="35b54-238">对于要大得多的集合，不同的 UI 和其他更新方法为更可用且更高效。</span><span class="sxs-lookup"><span data-stu-id="35b54-238">For collections that are much larger, a different UI and a different updating method would be more useable and efficient.</span></span>

### <a name="update-the-instructors-create-page"></a><span data-ttu-id="35b54-239">更新教师创建页</span><span class="sxs-lookup"><span data-stu-id="35b54-239">Update the instructors Create page</span></span>

<span data-ttu-id="35b54-240">替换为以下代码更新教师创建页模型：</span><span class="sxs-lookup"><span data-stu-id="35b54-240">Update the instructor Create page model with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Pages/Instructors/Create.cshtml.cs)]

<span data-ttu-id="35b54-241">前面的代码将类似于*Pages/Instructors/Edit.cshtml.cs*代码。</span><span class="sxs-lookup"><span data-stu-id="35b54-241">The preceding code is similar to the *Pages/Instructors/Edit.cshtml.cs* code.</span></span>

<span data-ttu-id="35b54-242">使用以下标记更新教师创建 Razor 页：</span><span class="sxs-lookup"><span data-stu-id="35b54-242">Update the instructor Create Razor page with the following markup:</span></span>

[!code-cshtml[Main](intro/samples/cu/Pages/Instructors/Create.cshtml?highlight=32-62)]

<span data-ttu-id="35b54-243">教师创建页进行测试。</span><span class="sxs-lookup"><span data-stu-id="35b54-243">Test the instructor Create page.</span></span>

## <a name="update-the-delete-page"></a><span data-ttu-id="35b54-244">更新删除页</span><span class="sxs-lookup"><span data-stu-id="35b54-244">Update the Delete page</span></span>

<span data-ttu-id="35b54-245">替换为以下代码更新删除页模型：</span><span class="sxs-lookup"><span data-stu-id="35b54-245">Update the Delete page model with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Pages/Instructors/Delete.cshtml.cs?highlight=5,40-)]

<span data-ttu-id="35b54-246">前面的代码进行以下更改：</span><span class="sxs-lookup"><span data-stu-id="35b54-246">The preceding code makes the following changes:</span></span>

* <span data-ttu-id="35b54-247">使用预先加载的`CourseAssignments`导航属性。</span><span class="sxs-lookup"><span data-stu-id="35b54-247">Uses eager loading for the `CourseAssignments` navigation property.</span></span> <span data-ttu-id="35b54-248">`CourseAssignments`必须包含或删除教师时不删除它们。</span><span class="sxs-lookup"><span data-stu-id="35b54-248">`CourseAssignments` must be included or they aren't deleted when the instructor is deleted.</span></span> <span data-ttu-id="35b54-249">若要避免无需阅读这些条款，配置数据库中的级联删除。</span><span class="sxs-lookup"><span data-stu-id="35b54-249">To avoid needing to read them, configure cascade delete in the database.</span></span>

* <span data-ttu-id="35b54-250">如果要删除教师被指定为任何部门的管理员，移除这些部门教师分配。</span><span class="sxs-lookup"><span data-stu-id="35b54-250">If the instructor to be deleted is assigned as administrator of any departments, removes the instructor assignment from those departments.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="35b54-251">[上一页](xref:data/ef-rp/read-related-data)
[下一页](xref:data/ef-rp/concurrency)</span><span class="sxs-lookup"><span data-stu-id="35b54-251">[Previous](xref:data/ef-rp/read-related-data)
[Next](xref:data/ef-rp/concurrency)</span></span>