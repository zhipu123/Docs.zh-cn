---
uid: signalr/overview/testing-and-debugging/troubleshooting
title: "SignalR 疑难解答 |Microsoft 文档"
author: pfletcher
description: "本文介绍开发 SignalR 应用程序的常见问题。"
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/10/2014
ms.topic: article
ms.assetid: 4b559e6c-4fb0-4a04-9812-45cf08ae5779
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/testing-and-debugging/troubleshooting
msc.type: authoredcontent
ms.openlocfilehash: d7a1dcc04baaa5ab27aecf95936d943f5a9b3f0c
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2017
---
<a name="signalr-troubleshooting"></a><span data-ttu-id="656a5-103">SignalR 故障排除</span><span class="sxs-lookup"><span data-stu-id="656a5-103">SignalR Troubleshooting</span></span>
====================
<span data-ttu-id="656a5-104">通过[Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="656a5-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

> <span data-ttu-id="656a5-105">本文档将介绍使用 SignalR 的常见故障排除问题。</span><span class="sxs-lookup"><span data-stu-id="656a5-105">This document describes common troubleshooting issues with SignalR.</span></span>
> 
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="656a5-106">本主题中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="656a5-106">Software versions used in this topic</span></span>
> 
> 
> - [<span data-ttu-id="656a5-107">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="656a5-107">Visual Studio 2013</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - <span data-ttu-id="656a5-108">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="656a5-108">.NET 4.5</span></span>
> - <span data-ttu-id="656a5-109">SignalR 版本 2</span><span class="sxs-lookup"><span data-stu-id="656a5-109">SignalR version 2</span></span>
>   
> 
> 
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="656a5-110">本主题的早期版本</span><span class="sxs-lookup"><span data-stu-id="656a5-110">Previous versions of this topic</span></span>
> 
> <span data-ttu-id="656a5-111">有关 SignalR 的早期版本的信息，请参阅[SignalR 较旧版本](../older-versions/index.md)。</span><span class="sxs-lookup"><span data-stu-id="656a5-111">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="656a5-112">问题和意见</span><span class="sxs-lookup"><span data-stu-id="656a5-112">Questions and comments</span></span>
> 
> <span data-ttu-id="656a5-113">请留下反馈上如何喜欢本教程的方式，我们可以提高在页面底部的注释中。</span><span class="sxs-lookup"><span data-stu-id="656a5-113">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="656a5-114">如果你有与本教程不直接相关的问题，你可以发布到[ASP.NET SignalR 论坛](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。</span><span class="sxs-lookup"><span data-stu-id="656a5-114">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>


<span data-ttu-id="656a5-115">本文档包含以下各节。</span><span class="sxs-lookup"><span data-stu-id="656a5-115">This document contains the following sections.</span></span>

- [<span data-ttu-id="656a5-116">以无提示方式调用客户端和服务器之间的方法，则会失败</span><span class="sxs-lookup"><span data-stu-id="656a5-116">Calling methods between the client and server silently fails</span></span>](#connection)
- [<span data-ttu-id="656a5-117">配置 IIS websocket ping/pong 来检测死的客户端</span><span class="sxs-lookup"><span data-stu-id="656a5-117">Configuring IIS websockets to ping/pong to detect a dead client</span></span>](#pong)
- [<span data-ttu-id="656a5-118">其他连接问题</span><span class="sxs-lookup"><span data-stu-id="656a5-118">Other connection issues</span></span>](#other)
- [<span data-ttu-id="656a5-119">编译和服务器端错误</span><span class="sxs-lookup"><span data-stu-id="656a5-119">Compilation and server-side errors</span></span>](#server)
- [<span data-ttu-id="656a5-120">Visual Studio 问题</span><span class="sxs-lookup"><span data-stu-id="656a5-120">Visual Studio issues</span></span>](#vs)
- [<span data-ttu-id="656a5-121">Internet 信息服务的问题</span><span class="sxs-lookup"><span data-stu-id="656a5-121">Internet Information Services issues</span></span>](#iis)
- [<span data-ttu-id="656a5-122">Microsoft Azure 问题</span><span class="sxs-lookup"><span data-stu-id="656a5-122">Microsoft Azure issues</span></span>](#azure)

<a id="connection"></a>

## <a name="calling-methods-between-the-client-and-server-silently-fails"></a><span data-ttu-id="656a5-123">以无提示方式调用客户端和服务器之间的方法，则会失败</span><span class="sxs-lookup"><span data-stu-id="656a5-123">Calling methods between the client and server silently fails</span></span>

<span data-ttu-id="656a5-124">本部分介绍方法调用失败没有有意义的错误消息的客户端和服务器之间可能的原因。</span><span class="sxs-lookup"><span data-stu-id="656a5-124">This section describes possible causes for a method call between client and server to fail without a meaningful error message.</span></span> <span data-ttu-id="656a5-125">在 SignalR 应用程序中，服务器已没有有关该客户端实现; 的方法的信息当服务器调用时的客户端方法，方法名称和参数数据发送到客户端，并仅当它存在于指定的服务器的格式时，才执行此方法。</span><span class="sxs-lookup"><span data-stu-id="656a5-125">In a SignalR application, the server has no information about the methods that the client implements; when the server invokes a client method, the method name and parameter data are sent to the client, and the method is executed only if it exists in the format that the server specified.</span></span> <span data-ttu-id="656a5-126">如果没有匹配的方法是在上找到客户端，会执行任何操作，并且在服务器上不会引发任何错误消息。</span><span class="sxs-lookup"><span data-stu-id="656a5-126">If no matching method is found on the client, nothing happens, and no error message is raised on the server.</span></span>

<span data-ttu-id="656a5-127">要进一步调查不调用客户端方法，可以打开之前调用的中心查看哪些调用 start 方法都来自服务器的日志记录。</span><span class="sxs-lookup"><span data-stu-id="656a5-127">To further investigate client methods not getting called, you can turn on logging before the calling the start method on the hub to see what calls are coming from the server.</span></span> <span data-ttu-id="656a5-128">若要启用日志记录中的 JavaScript 应用程序，请参阅[如何启用客户端日志记录 （JavaScript 客户端版本）](../guide-to-the-api/hubs-api-guide-javascript-client.md#logging)。</span><span class="sxs-lookup"><span data-stu-id="656a5-128">To enable logging in a JavaScript application, see [How to enable client-side logging (JavaScript client version)](../guide-to-the-api/hubs-api-guide-javascript-client.md#logging).</span></span> <span data-ttu-id="656a5-129">若要启用日志记录在.NET 客户端应用程序，请参阅[如何启用客户端日志记录 （.NET 客户端版本）](../guide-to-the-api/hubs-api-guide-net-client.md#logging)。</span><span class="sxs-lookup"><span data-stu-id="656a5-129">To enable logging in a .NET client application, see [How to enable client-side logging (.NET Client version)](../guide-to-the-api/hubs-api-guide-net-client.md#logging).</span></span>

### <a name="misspelled-method-incorrect-method-signature-or-incorrect-hub-name"></a><span data-ttu-id="656a5-130">拼写错误的方法、 不正确的方法签名或不正确的中心名称</span><span class="sxs-lookup"><span data-stu-id="656a5-130">Misspelled method, incorrect method signature, or incorrect hub name</span></span>

<span data-ttu-id="656a5-131">如果名称或调用方法的签名与客户端上适当的方法不完全匹配，则调用将失败。</span><span class="sxs-lookup"><span data-stu-id="656a5-131">If the name or signature of a called method does not exactly match an appropriate method on the client, the call will fail.</span></span> <span data-ttu-id="656a5-132">验证由服务器调用的方法名称匹配的客户端上的方法的名称。</span><span class="sxs-lookup"><span data-stu-id="656a5-132">Verify that the method name called by the server matches the name of the method on the client.</span></span> <span data-ttu-id="656a5-133">此外，SignalR 创建中心代理使用混合使用大小写的方法，以根据在 JavaScript 中，因此调用的方法，`SendMessage`在服务器上将调用`sendMessage`客户端代理中。</span><span class="sxs-lookup"><span data-stu-id="656a5-133">Also, SignalR creates the hub proxy using camel-cased methods, as is appropriate in JavaScript, so a method called `SendMessage` on the server would be called `sendMessage` in the client proxy.</span></span> <span data-ttu-id="656a5-134">如果你使用`HubName`属性在服务器端代码中，验证是否使用的名称与用来在客户端上创建中心的名称匹配。</span><span class="sxs-lookup"><span data-stu-id="656a5-134">If you use the `HubName` attribute in your server-side code, verify that the name used matches the name used to create the hub on the client.</span></span> <span data-ttu-id="656a5-135">如果不使用`HubName`属性中，验证是否 camel 大小写形式，如而不是 ChatHub chatHub JavaScript 客户端在中心的名称。</span><span class="sxs-lookup"><span data-stu-id="656a5-135">If you do not use the `HubName` attribute, verify that the name of the hub in a JavaScript client is camel-cased, such as chatHub instead of ChatHub.</span></span>

### <a name="duplicate-method-name-on-client"></a><span data-ttu-id="656a5-136">客户端上的重复的方法名称</span><span class="sxs-lookup"><span data-stu-id="656a5-136">Duplicate method name on client</span></span>

<span data-ttu-id="656a5-137">请确认不有重复的方法仅大小写上不同的客户端上。</span><span class="sxs-lookup"><span data-stu-id="656a5-137">Verify that you do not have a duplicate method on the client that differs only by case.</span></span> <span data-ttu-id="656a5-138">如果客户端应用程序调用的方法`sendMessage`，请验证是否未还调用的方法`SendMessage`以及。</span><span class="sxs-lookup"><span data-stu-id="656a5-138">If your client application has a method called `sendMessage`, verify that there isn't also a method called `SendMessage` as well.</span></span>

### <a name="missing-json-parser-on-the-client"></a><span data-ttu-id="656a5-139">客户端上缺少 JSON 分析器</span><span class="sxs-lookup"><span data-stu-id="656a5-139">Missing JSON parser on the client</span></span>

<span data-ttu-id="656a5-140">SignalR 需要 JSON 分析器存在才可序列化的服务器和客户端之间的调用。</span><span class="sxs-lookup"><span data-stu-id="656a5-140">SignalR requires a JSON parser to be present to serialize calls between the server and the client.</span></span> <span data-ttu-id="656a5-141">如果你的客户端没有内置的 JSON 分析器 （如 Internet Explorer 7)，你将需要包含一个应用程序中。</span><span class="sxs-lookup"><span data-stu-id="656a5-141">If your client doesn't have a built-in JSON parser (such as Internet Explorer 7), you'll need to include one in your application.</span></span> <span data-ttu-id="656a5-142">你可以下载 JSON 分析器[此处](http://nuget.org/packages/json2)。</span><span class="sxs-lookup"><span data-stu-id="656a5-142">You can download the JSON parser [here](http://nuget.org/packages/json2).</span></span>

### <a name="mixing-hub-and-persistentconnection-syntax"></a><span data-ttu-id="656a5-143">混合使用中心 PersistentConnection 语法</span><span class="sxs-lookup"><span data-stu-id="656a5-143">Mixing Hub and PersistentConnection syntax</span></span>

<span data-ttu-id="656a5-144">SignalR 使用两个通信模型： 中心和 PersistentConnections。</span><span class="sxs-lookup"><span data-stu-id="656a5-144">SignalR uses two communication models: Hubs and PersistentConnections.</span></span> <span data-ttu-id="656a5-145">调用这些两个通信模型的语法是在客户端代码不同。</span><span class="sxs-lookup"><span data-stu-id="656a5-145">The syntax for calling these two communication models is different in the client code.</span></span> <span data-ttu-id="656a5-146">如果你已在服务器代码中添加一个中心，请验证所有客户端代码使用正确的中心语法。</span><span class="sxs-lookup"><span data-stu-id="656a5-146">If you have added a hub in your server code, verify that all of your client code uses the proper hub syntax.</span></span>

<span data-ttu-id="656a5-147">**在 JavaScript 客户端中创建 PersistentConnection 的 JavaScript 客户端代码**</span><span class="sxs-lookup"><span data-stu-id="656a5-147">**JavaScript client code that creates a PersistentConnection in a JavaScript client**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample1.js)]

<span data-ttu-id="656a5-148">**在 Javascript 客户端中创建一个中心代理的 JavaScript 客户端代码**</span><span class="sxs-lookup"><span data-stu-id="656a5-148">**JavaScript client code that creates a Hub Proxy in a Javascript client**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample2.js)]

<span data-ttu-id="656a5-149">**C# 服务器代码映射到 PersistentConnection 的路由**</span><span class="sxs-lookup"><span data-stu-id="656a5-149">**C# server code that maps a route to a PersistentConnection**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample3.cs)]

<span data-ttu-id="656a5-150">**将路由映射到一个中心，或多个中心上，如果你有多个应用程序的 C# 服务器代码**</span><span class="sxs-lookup"><span data-stu-id="656a5-150">**C# server code that maps a route to a Hub, or to mulitple hubs if you have multiple applications**</span></span>

[!code-css[Main](troubleshooting/samples/sample4.css)]

### <a name="connection-started-before-subscriptions-are-added"></a><span data-ttu-id="656a5-151">在添加订阅之前启动的连接</span><span class="sxs-lookup"><span data-stu-id="656a5-151">Connection started before subscriptions are added</span></span>

<span data-ttu-id="656a5-152">如果可以从服务器调用的方法添加到代理之前启动中心的连接，则将不接收消息。</span><span class="sxs-lookup"><span data-stu-id="656a5-152">If the Hub's connection is started before methods that can be called from the server are added to the proxy, messages will not be received.</span></span> <span data-ttu-id="656a5-153">下面的 JavaScript 代码将不会正确启动中心：</span><span class="sxs-lookup"><span data-stu-id="656a5-153">The following JavaScript code will not start the hub properly:</span></span>

<span data-ttu-id="656a5-154">**将不允许将接收的中心消息的不正确 JavaScript 客户端代码**</span><span class="sxs-lookup"><span data-stu-id="656a5-154">**Incorrect JavaScript client code that will not allow Hubs messages to be received**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample5.js)]

<span data-ttu-id="656a5-155">相反，请在调用开始之前添加方法订阅：</span><span class="sxs-lookup"><span data-stu-id="656a5-155">Instead, add the method subscriptions before calling Start:</span></span>

<span data-ttu-id="656a5-156">**正确将订阅添加到一个中心的 JavaScript 客户端代码**</span><span class="sxs-lookup"><span data-stu-id="656a5-156">**JavaScript client code that correctly adds subscriptions to a hub**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample6.js)]

### <a name="missing-method-name-on-the-hub-proxy"></a><span data-ttu-id="656a5-157">在中心代理服务器上缺少方法名称</span><span class="sxs-lookup"><span data-stu-id="656a5-157">Missing method name on the hub proxy</span></span>

<span data-ttu-id="656a5-158">验证服务器上定义的方法向订阅客户端上。</span><span class="sxs-lookup"><span data-stu-id="656a5-158">Verify that the method defined on the server is subscribed to on the client.</span></span> <span data-ttu-id="656a5-159">即使服务器定义的方法，则它必须仍将添加到客户端代理。</span><span class="sxs-lookup"><span data-stu-id="656a5-159">Even though the server defines the method, it must still be added to the client proxy.</span></span> <span data-ttu-id="656a5-160">方法可以通过以下方式添加到客户端代理 (请注意，该方法添加到`client`的中心，而不中心直接成员):</span><span class="sxs-lookup"><span data-stu-id="656a5-160">Methods can be added to the client proxy in the following ways (Note that the method is added to the `client` member of the hub, not the hub directly):</span></span>

<span data-ttu-id="656a5-161">**将方法添加到中心代理的 JavaScript 客户端代码**</span><span class="sxs-lookup"><span data-stu-id="656a5-161">**JavaScript client code that adds methods to a hub proxy**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample7.js)]

### <a name="hub-or-hub-methods-not-declared-as-public"></a><span data-ttu-id="656a5-162">中心或未声明为公共的中心方法</span><span class="sxs-lookup"><span data-stu-id="656a5-162">Hub or hub methods not declared as Public</span></span>

<span data-ttu-id="656a5-163">若要在客户端上可见，中心实现和方法必须声明为`public`。</span><span class="sxs-lookup"><span data-stu-id="656a5-163">To be visible on the client, the hub implementation and methods must be declared as `public`.</span></span>

### <a name="accessing-hub-from-a-different-application"></a><span data-ttu-id="656a5-164">从不同的应用程序访问中心</span><span class="sxs-lookup"><span data-stu-id="656a5-164">Accessing hub from a different application</span></span>

<span data-ttu-id="656a5-165">仅可以通过实现 SignalR 客户端应用程序访问 SignalR 集线器。</span><span class="sxs-lookup"><span data-stu-id="656a5-165">SignalR Hubs can only be accessed through applications that implement SignalR clients.</span></span> <span data-ttu-id="656a5-166">SignalR 无法进行交互操作，与其他通信库 （如 SOAP 或 WCF web 服务。）如果没有可用于你的目标平台的无 SignalR 客户端，你不能直接访问服务器的终结点。</span><span class="sxs-lookup"><span data-stu-id="656a5-166">SignalR cannot interoperate with other communication libraries (like SOAP or WCF web services.) If there is no SignalR client available for your target platform, you cannot access the server's endpoint directly.</span></span>

### <a name="manually-serializing-data"></a><span data-ttu-id="656a5-167">手动序列化数据</span><span class="sxs-lookup"><span data-stu-id="656a5-167">Manually serializing data</span></span>

<span data-ttu-id="656a5-168">SignalR 将自动使用 JSON 序列化你的方法参数-这无需自行执行此操作。</span><span class="sxs-lookup"><span data-stu-id="656a5-168">SignalR will automatically use JSON to serialize your method parameters- there's no need to do it yourself.</span></span>

### <a name="remote-hub-method-not-executed-on-client-in-ondisconnected-function"></a><span data-ttu-id="656a5-169">没有对 OnDisconnected 函数中的客户端执行的远程中心方法</span><span class="sxs-lookup"><span data-stu-id="656a5-169">Remote Hub method not executed on client in OnDisconnected function</span></span>

<span data-ttu-id="656a5-170">此行为是有意安排的。</span><span class="sxs-lookup"><span data-stu-id="656a5-170">This behavior is by design.</span></span> <span data-ttu-id="656a5-171">当`OnDisconnected`是调用，已进入中心`Disconnected`状态，不允许进一步中心方法调用。</span><span class="sxs-lookup"><span data-stu-id="656a5-171">When `OnDisconnected` is called, the hub has already entered the `Disconnected` state, which does not allow further hub methods to be called.</span></span>

<span data-ttu-id="656a5-172">**正确 OnDisconnected 事件中执行代码的 C# 服务器代码**</span><span class="sxs-lookup"><span data-stu-id="656a5-172">**C# server code that correctly executes code in the OnDisconnected event**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample8.cs)]

### <a name="ondisconnect-not-firing-at-consistent-times"></a><span data-ttu-id="656a5-173">以一致的时间不引发 OnDisconnect</span><span class="sxs-lookup"><span data-stu-id="656a5-173">OnDisconnect not firing at consistent times</span></span>

<span data-ttu-id="656a5-174">此行为是有意安排的。</span><span class="sxs-lookup"><span data-stu-id="656a5-174">This behavior is by design.</span></span> <span data-ttu-id="656a5-175">当用户尝试通过导航离开 SignalR 连接处于活动的页时，SignalR 客户端然后将进行通知服务器将停止客户端连接的最大努力尝试。</span><span class="sxs-lookup"><span data-stu-id="656a5-175">When a user attempts to navigate away from a page with an active SignalR connection, the SignalR client will then make a best-effort attempt to notify the server that the client connection will be stopped.</span></span> <span data-ttu-id="656a5-176">如果 SignalR 客户端的最大努力尝试无法到达服务器，服务器将停止后可配置连接`DisconnectTimeout`更高版本，在这段时间`OnDisconnected`事件将激发。</span><span class="sxs-lookup"><span data-stu-id="656a5-176">If the SignalR client's best-effort attempt fails to reach the server, the server will dispose of the connection after a configurable `DisconnectTimeout` later, at which time the `OnDisconnected` event will fire.</span></span> <span data-ttu-id="656a5-177">如果 SignalR 客户端的最大努力尝试不成功，`OnDisconnected`将立即触发事件。</span><span class="sxs-lookup"><span data-stu-id="656a5-177">If the SignalR client's best-effort attempt is successful, the `OnDisconnected` event will fire immediately.</span></span>

<span data-ttu-id="656a5-178">有关设置信息`DisconnectTimeout`设置，请参阅[处理连接生存期事件： DisconnectTimeout](../guide-to-the-api/handling-connection-lifetime-events.md#disconnecttimeout)。</span><span class="sxs-lookup"><span data-stu-id="656a5-178">For information on setting the `DisconnectTimeout` setting, see [Handling connection lifetime events: DisconnectTimeout](../guide-to-the-api/handling-connection-lifetime-events.md#disconnecttimeout).</span></span>

### <a name="connection-limit-reached"></a><span data-ttu-id="656a5-179">已达到连接限制</span><span class="sxs-lookup"><span data-stu-id="656a5-179">Connection limit reached</span></span>

<span data-ttu-id="656a5-180">当使用 IIS 的完整版本，如 Windows 7 客户端操作系统上，受 10 连接限制。</span><span class="sxs-lookup"><span data-stu-id="656a5-180">When using the full version of IIS on a client operating system like Windows 7, a 10-connection limit is imposed.</span></span> <span data-ttu-id="656a5-181">在使用客户端操作系统，改用 IIS Express 以避免此限制。</span><span class="sxs-lookup"><span data-stu-id="656a5-181">When using a client OS, use IIS Express instead to avoid this limit.</span></span>

### <a name="cross-domain-connection-not-set-up-properly"></a><span data-ttu-id="656a5-182">跨域连接未正确设置</span><span class="sxs-lookup"><span data-stu-id="656a5-182">Cross-domain connection not set up properly</span></span>

<span data-ttu-id="656a5-183">如果跨域连接 （连接为其的 SignalR URL 不是为宿主的页位于同一域中） 未正确设置，连接可能会失败并且不显示错误消息。</span><span class="sxs-lookup"><span data-stu-id="656a5-183">If a cross-domain connection (a connection for which the SignalR URL is not in the same domain as the hosting page) is not set up correctly, the connection may fail without an error message.</span></span> <span data-ttu-id="656a5-184">有关如何启用跨域通信的信息，请参阅[如何建立的跨域连接](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)。</span><span class="sxs-lookup"><span data-stu-id="656a5-184">For information on how to enable cross-domain communication, see [How to establish a cross-domain connection](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span></span>

### <a name="connection-using-ntlm-active-directory-not-working-in-net-client"></a><span data-ttu-id="656a5-185">连接使用 NTLM (Active Directory) 不在.NET 客户端中工作</span><span class="sxs-lookup"><span data-stu-id="656a5-185">Connection using NTLM (Active Directory) not working in .NET client</span></span>

<span data-ttu-id="656a5-186">如果连接未正确配置，在.NET 客户端应用程序中使用域安全的连接可能会失败。</span><span class="sxs-lookup"><span data-stu-id="656a5-186">A connection in a .NET client application that uses Domain security may fail if the connection is not configured properly.</span></span> <span data-ttu-id="656a5-187">若要在域环境中使用 SignalR，请将所需的连接属性，如下所示设置：</span><span class="sxs-lookup"><span data-stu-id="656a5-187">To use SignalR in a domain environment, set the requisite connection property as follows:</span></span>

<span data-ttu-id="656a5-188">**实现连接凭据的 C# 客户端代码**</span><span class="sxs-lookup"><span data-stu-id="656a5-188">**C# client code that implements connection credentials**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample9.cs)]

<a id="pong"></a>

## <a name="configuring-iis-websockets-to-pingpong-to-detect-a-dead-client"></a><span data-ttu-id="656a5-189">配置 IIS websocket ping/pong 来检测死的客户端</span><span class="sxs-lookup"><span data-stu-id="656a5-189">Configuring IIS websockets to ping/pong to detect a dead client</span></span>

<span data-ttu-id="656a5-190">SignalR 服务器不知道，是否客户端是否已死以及它们依赖于从基础 websocket 连接失败的通知，即 OnClose 回调。</span><span class="sxs-lookup"><span data-stu-id="656a5-190">SignalR servers don't know if the client is dead or not and they rely on notification from the underlying websocket for connection failures, that is, the OnClose callback.</span></span> <span data-ttu-id="656a5-191">此问题的一种解决方案是配置 IIS websocket ping/pong 为你执行操作。</span><span class="sxs-lookup"><span data-stu-id="656a5-191">One solution to this problem is to configure IIS websockets to do the ping/pong for you.</span></span> <span data-ttu-id="656a5-192">这可确保，如果它在意外中断，你的连接将关闭。</span><span class="sxs-lookup"><span data-stu-id="656a5-192">This ensures that your connection will close if it breaks unexpectedly.</span></span> <span data-ttu-id="656a5-193">有关详细信息请参阅[此 stackoverflow 文章](http://stackoverflow.com/questions/19502755/websocket-clients-state-not-changing-on-network-loss)。</span><span class="sxs-lookup"><span data-stu-id="656a5-193">For more information see [this stackoverflow post](http://stackoverflow.com/questions/19502755/websocket-clients-state-not-changing-on-network-loss).</span></span>

<a id="other"></a>

## <a name="other-connection-issues"></a><span data-ttu-id="656a5-194">其他连接问题</span><span class="sxs-lookup"><span data-stu-id="656a5-194">Other connection issues</span></span>

<span data-ttu-id="656a5-195">本部分介绍的原因和解决方案的具体的症状或在连接过程中发生的错误消息。</span><span class="sxs-lookup"><span data-stu-id="656a5-195">This section describes the causes and solutions for specific symptoms or error messages that occur during a connection.</span></span>

### <a name="start-must-be-called-before-data-can-be-sent-error"></a><span data-ttu-id="656a5-196">"可以发送数据之前，必须调用 start"错误</span><span class="sxs-lookup"><span data-stu-id="656a5-196">"Start must be called before data can be sent" error</span></span>

<span data-ttu-id="656a5-197">如果代码引用 SignalR 对象启动连接之前，通常出现此错误。</span><span class="sxs-lookup"><span data-stu-id="656a5-197">This error is commonly seen if code references SignalR objects before the connection is started.</span></span> <span data-ttu-id="656a5-198">处理程序和 like 绑定，将在服务器上定义的调用方法必须添加连接完成后。</span><span class="sxs-lookup"><span data-stu-id="656a5-198">The wireup for handlers and the like that will call methods defined on the server must be added after the connection completes.</span></span> <span data-ttu-id="656a5-199">请注意，调用`Start`是异步的因此，代码调用可能在它之前执行后完成。</span><span class="sxs-lookup"><span data-stu-id="656a5-199">Note that the call to `Start` is asynchronous, so code after the call may be executed before it completes.</span></span> <span data-ttu-id="656a5-200">连接完全启动后添加处理程序的最佳方法是将其放到作为参数传递到的启动方法的回调函数：</span><span class="sxs-lookup"><span data-stu-id="656a5-200">The best way to add handlers after a connection starts completely is to put them into a callback function that is passed as a parameter to the start method:</span></span>

<span data-ttu-id="656a5-201">**正确添加引用 SignalR 对象的事件处理程序的 JavaScript 客户端代码**</span><span class="sxs-lookup"><span data-stu-id="656a5-201">**JavaScript client code that correctly adds event handlers that reference SignalR objects**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample10.js?highlight=1)]

<span data-ttu-id="656a5-202">如果连接会在仍然引用 SignalR 对象时停止，则也将出现此错误。</span><span class="sxs-lookup"><span data-stu-id="656a5-202">This error will also be seen if a connection stops while SignalR objects are still being referenced.</span></span>

### <a name="301-moved-permanently-or-302-moved-temporarily-error"></a><span data-ttu-id="656a5-203">"永久移动 301"或者"暂时移动 302"错误</span><span class="sxs-lookup"><span data-stu-id="656a5-203">"301 Moved Permanently" or "302 Moved Temporarily" error</span></span>

<span data-ttu-id="656a5-204">如果项目包含一个名为 SignalR 会干扰自动创建代理文件夹，则可能出现此错误。</span><span class="sxs-lookup"><span data-stu-id="656a5-204">This error may be seen if the project contains a folder called SignalR, which will interfere with the automatically-created proxy.</span></span> <span data-ttu-id="656a5-205">若要避免此错误，不要使用一个名为文件夹`SignalR`你的应用程序，或关闭的启用自动代理生成。</span><span class="sxs-lookup"><span data-stu-id="656a5-205">To avoid this error, do not use a folder called `SignalR` in your application, or turn automatic proxy generation off.</span></span> <span data-ttu-id="656a5-206">请参阅[生成代理和它为您完成](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)有关详细信息。</span><span class="sxs-lookup"><span data-stu-id="656a5-206">See [The Generated Proxy and what it does for you](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy) for more details.</span></span>

### <a name="403-forbidden-error-in-net-or-silverlight-client"></a><span data-ttu-id="656a5-207">在.NET 或 Silverlight 客户端中的"403 禁止访问"错误</span><span class="sxs-lookup"><span data-stu-id="656a5-207">"403 Forbidden" error in .NET or Silverlight client</span></span>

<span data-ttu-id="656a5-208">在跨域通信未正确启用跨域环境中可能出现此错误。</span><span class="sxs-lookup"><span data-stu-id="656a5-208">This error may occur in cross-domain environments where cross-domain communication is not properly enabled.</span></span> <span data-ttu-id="656a5-209">有关如何启用跨域通信的信息，请参阅[如何建立的跨域连接](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)。</span><span class="sxs-lookup"><span data-stu-id="656a5-209">For information on how to enable cross-domain communication, see [How to establish a cross-domain connection](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span></span> <span data-ttu-id="656a5-210">若要建立在 Silverlight 客户端的跨域连接，请参阅[来自 Silverlight 客户端的跨域连接](../guide-to-the-api/hubs-api-guide-net-client.md#slcrossdomain)。</span><span class="sxs-lookup"><span data-stu-id="656a5-210">To establish a cross-domain connection in a Silverlight client, see [Cross-domain connections from Silverlight clients](../guide-to-the-api/hubs-api-guide-net-client.md#slcrossdomain).</span></span>

### <a name="404-not-found-error"></a><span data-ttu-id="656a5-211">"404 未找到"错误</span><span class="sxs-lookup"><span data-stu-id="656a5-211">"404 Not Found" error</span></span>

<span data-ttu-id="656a5-212">有几个原因，此问题。</span><span class="sxs-lookup"><span data-stu-id="656a5-212">There are several causes for this issue.</span></span> <span data-ttu-id="656a5-213">验证所有以下操作：</span><span class="sxs-lookup"><span data-stu-id="656a5-213">Verify all of the following:</span></span>

- <span data-ttu-id="656a5-214">**中心代理地址引用的格式不正确：**如果对生成的中心代理地址的引用的格式不正确，则通常会出现此错误。</span><span class="sxs-lookup"><span data-stu-id="656a5-214">**Hub proxy address reference not formatted correctly:** This error is commonly seen if the reference to the generated hub proxy address is not formatted correctly.</span></span> <span data-ttu-id="656a5-215">验证对中心地址的引用可以正确地完成。</span><span class="sxs-lookup"><span data-stu-id="656a5-215">Verify that the reference to the hub address is made properly.</span></span> <span data-ttu-id="656a5-216">请参阅[如何引用动态生成的代理](../guide-to-the-api/hubs-api-guide-javascript-client.md#dynamicproxy)有关详细信息。</span><span class="sxs-lookup"><span data-stu-id="656a5-216">See [How to reference the dynamically generated proxy](../guide-to-the-api/hubs-api-guide-javascript-client.md#dynamicproxy) for details.</span></span>
- <span data-ttu-id="656a5-217">**将路由添加到应用程序，然后添加中心路由：**如果你的应用程序使用的其他路由，验证是否添加的第一个路由是对调用`MapSignalR`。</span><span class="sxs-lookup"><span data-stu-id="656a5-217">**Adding routes to application before adding the hub route:** If your application uses other routes, verify that the first route added is the call to `MapSignalR`.</span></span>
- <span data-ttu-id="656a5-218">**适用于无扩展名的 Url 中使用 IIS 7 或不带更新 7.5:**使用 IIS 7 或 7.5 需要更新无扩展名的 url，以便服务器可以提供对中心定义访问`/signalr/hubs`。</span><span class="sxs-lookup"><span data-stu-id="656a5-218">**Using IIS 7 or 7.5 without the update for extensionless URLs:** Using IIS 7 or 7.5 requires an update for extensionless URLs so that the server can provide access to the hub definitions at `/signalr/hubs`.</span></span> <span data-ttu-id="656a5-219">找不到更新[此处](https://support.microsoft.com/kb/980368/en-us)。</span><span class="sxs-lookup"><span data-stu-id="656a5-219">The update can be found [here](https://support.microsoft.com/kb/980368/en-us).</span></span>
- <span data-ttu-id="656a5-220">**IIS 缓存过期或已损坏：**若要验证缓存内容不是过期，可清除缓存的 PowerShell 窗口中输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="656a5-220">**IIS cache out of date or corrupt:** To verify that the cache contents are not out of date, enter the following command in a PowerShell window to clear the cache:</span></span>

    [!code-powershell[Main](troubleshooting/samples/sample11.ps1)]

### <a name="500-internal-server-error"></a><span data-ttu-id="656a5-221">"500 内部服务器错误"</span><span class="sxs-lookup"><span data-stu-id="656a5-221">"500 Internal Server Error"</span></span>

<span data-ttu-id="656a5-222">这是一个非常一般性错误，可能有多种原因。</span><span class="sxs-lookup"><span data-stu-id="656a5-222">This is a very generic error that could have a wide variety of causes.</span></span> <span data-ttu-id="656a5-223">错误的详细信息应出现在服务器的事件日志，或可以通过调试服务器发现。</span><span class="sxs-lookup"><span data-stu-id="656a5-223">The details of the error should appear in the server's event log, or can be found through debugging the server.</span></span> <span data-ttu-id="656a5-224">通过打开服务器上的详细错误都可以获得更多详细的错误信息。</span><span class="sxs-lookup"><span data-stu-id="656a5-224">More detailed error information may be obtained by turning on detailed errors on the server.</span></span> <span data-ttu-id="656a5-225">有关详细信息，请参阅[如何处理中心类中的错误](../guide-to-the-api/hubs-api-guide-server.md#handleErrors)。</span><span class="sxs-lookup"><span data-stu-id="656a5-225">For more information, see [How to handle errors in the Hub class](../guide-to-the-api/hubs-api-guide-server.md#handleErrors).</span></span>

<span data-ttu-id="656a5-226">如果防火墙或代理配置不正确，导致请求标头重写，通常还出现此错误。</span><span class="sxs-lookup"><span data-stu-id="656a5-226">This error is also commonly seen if a firewall or proxy is not configured properly, causing the request headers to be rewritten.</span></span> <span data-ttu-id="656a5-227">解决方案是确保在防火墙或代理上启用了端口 80。</span><span class="sxs-lookup"><span data-stu-id="656a5-227">The solution is to make sure that port 80 is enabled on the firewall or proxy.</span></span>

### <a name="unexpected-response-code-500"></a><span data-ttu-id="656a5-228">"意外的响应代码： 500"</span><span class="sxs-lookup"><span data-stu-id="656a5-228">"Unexpected response code: 500"</span></span>

<span data-ttu-id="656a5-229">如果在应用程序中使用的.NET framework 的版本与在 Web.Config 中指定的版本不匹配，则可能出现此错误。该解决方案旨在验证应用程序设置和 Web.Config 文件中使用了.NET 4.5。</span><span class="sxs-lookup"><span data-stu-id="656a5-229">This error may occur if the version of .NET framework used in the application does not match the version specified in Web.Config. The solution is to verify that .NET 4.5 is used in both the application settings and the Web.Config file.</span></span>

### <a name="typeerror-lthubtypegt-is-undefined-error"></a><span data-ttu-id="656a5-230">"TypeError: &lt;hubType&gt;是不确定的"错误</span><span class="sxs-lookup"><span data-stu-id="656a5-230">"TypeError: &lt;hubType&gt; is undefined" error</span></span>

<span data-ttu-id="656a5-231">如果导致此错误，将调用`MapSignalR`不会正确进行。</span><span class="sxs-lookup"><span data-stu-id="656a5-231">This error will result if the call to `MapSignalR` is not made properly.</span></span> <span data-ttu-id="656a5-232">请参阅[如何注册 SignalR 中间件和配置 SignalR 选项](../guide-to-the-api/hubs-api-guide-server.md#route)有关详细信息。</span><span class="sxs-lookup"><span data-stu-id="656a5-232">See [How to register SignalR Middleware and configure SignalR options](../guide-to-the-api/hubs-api-guide-server.md#route) for more information.</span></span>

### <a name="jsonserializationexception-was-unhandled-by-user-code"></a><span data-ttu-id="656a5-233">用户代码未处理 JsonSerializationException</span><span class="sxs-lookup"><span data-stu-id="656a5-233">JsonSerializationException was unhandled by user code</span></span>

<span data-ttu-id="656a5-234">验证发送到你的方法的参数不包括非可序列化类型 （如文件句柄或数据库连接）。</span><span class="sxs-lookup"><span data-stu-id="656a5-234">Verify that the parameters you send to your methods do not include non-serializable types (like file handles or database connections).</span></span> <span data-ttu-id="656a5-235">如果你需要在你不想要将发送到客户端 （不管是进行安全，或者序列化的原因），使用服务器端对象上使用成员`JSONIgnore`属性。</span><span class="sxs-lookup"><span data-stu-id="656a5-235">If you need to use members on a server-side object that you don't want to be sent to the client (either for security or for reasons of serialization), use the `JSONIgnore` attribute.</span></span>

### <a name="protocol-error-unknown-transport-error"></a><span data-ttu-id="656a5-236">"协议错误： 未知的传输"错误</span><span class="sxs-lookup"><span data-stu-id="656a5-236">"Protocol error: Unknown transport" error</span></span>

<span data-ttu-id="656a5-237">如果客户端不支持使用 SignalR 的传输，则可能出现此错误。</span><span class="sxs-lookup"><span data-stu-id="656a5-237">This error may occur if the client does not support the transports that SignalR uses.</span></span> <span data-ttu-id="656a5-238">请参阅[传输和回退](../getting-started/introduction-to-signalr.md#transports)有关可与 SignalR 在其的浏览器的信息。</span><span class="sxs-lookup"><span data-stu-id="656a5-238">See [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports) for information on which browsers can be used with SignalR.</span></span>

### <a name="javascript-hub-proxy-generation-has-been-disabled"></a><span data-ttu-id="656a5-239">"JavaScript Hub 代理生成已禁用。"</span><span class="sxs-lookup"><span data-stu-id="656a5-239">"JavaScript Hub proxy generation has been disabled."</span></span>

<span data-ttu-id="656a5-240">如果将发生此错误`DisableJavaScriptProxies`时还包括对在动态生成的代理的引用设置`signalr/hubs`。</span><span class="sxs-lookup"><span data-stu-id="656a5-240">This error will occur if `DisableJavaScriptProxies` is set while also including a reference to the dynamically generated proxy at `signalr/hubs`.</span></span> <span data-ttu-id="656a5-241">有关手动创建代理的详细信息，请参阅[生成的代理和它为您完成](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)。</span><span class="sxs-lookup"><span data-stu-id="656a5-241">For more information on creating the proxy manually, see [The generated proxy and what it does for you](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy).</span></span>

### <a name="the-connection-id-is-in-the-incorrect-format-or-the-user-identity-cannot-change-during-an-active-signalr-connection-error"></a><span data-ttu-id="656a5-242">"连接 ID 格式不正确"或"SignalR 连接处于活动状态期间无法更改用户标识"错误</span><span class="sxs-lookup"><span data-stu-id="656a5-242">"The connection ID is in the incorrect format" or "The user identity cannot change during an active SignalR connection" error</span></span>

<span data-ttu-id="656a5-243">如果正在使用身份验证，并且客户端已注销，在停止连接之前，可能出现此错误。</span><span class="sxs-lookup"><span data-stu-id="656a5-243">This error may be seen if authentication is being used, and the client is logged out before the connection is stopped.</span></span> <span data-ttu-id="656a5-244">该解决方案旨在停止之前注销客户端的 SignalR 连接。</span><span class="sxs-lookup"><span data-stu-id="656a5-244">The solution is to stop the SignalR connection before logging the client out.</span></span>

### <a name="uncaught-error-signalr-jquery-not-found-please-ensure-jquery-is-referenced-before-the-signalrjs-file-error"></a><span data-ttu-id="656a5-245">"未捕获的错误： SignalR: jQuery 找不到。</span><span class="sxs-lookup"><span data-stu-id="656a5-245">"Uncaught Error: SignalR: jQuery not found.</span></span> <span data-ttu-id="656a5-246">请确保 jQuery 引用然后 SignalR.js 文件"错误</span><span class="sxs-lookup"><span data-stu-id="656a5-246">Please ensure jQuery is referenced before the SignalR.js file" error</span></span>

<span data-ttu-id="656a5-247">SignalR JavaScript 客户端需要 jQuery 运行。</span><span class="sxs-lookup"><span data-stu-id="656a5-247">The SignalR JavaScript client requires jQuery to run.</span></span> <span data-ttu-id="656a5-248">验证你对 jQuery 引用正确，使用的路径有效，以及对 jQuery 的引用是之前对 SignalR 的引用。</span><span class="sxs-lookup"><span data-stu-id="656a5-248">Verify that your reference to jQuery is correct, that the path used is valid, and that the reference to jQuery is before the reference to SignalR.</span></span>

### <a name="uncaught-typeerror-cannot-read-property-ltpropertygt-of-undefined-error"></a><span data-ttu-id="656a5-249">"未捕获的 TypeError： 无法读取属性&lt;属性&gt;的未定义"错误</span><span class="sxs-lookup"><span data-stu-id="656a5-249">"Uncaught TypeError: Cannot read property '&lt;property&gt;' of undefined" error</span></span>

<span data-ttu-id="656a5-250">不具有 jQuery 或引用正确的中心代理导致此错误。</span><span class="sxs-lookup"><span data-stu-id="656a5-250">This error results from not having jQuery or the hubs proxy referenced properly.</span></span> <span data-ttu-id="656a5-251">验证正确，使用的路径有效，以及对 jQuery 的引用是对中心代理引用之前 jQuery 和中心代理你参考。</span><span class="sxs-lookup"><span data-stu-id="656a5-251">Verify that your reference to jQuery and the hubs proxy is correct, that the path used is valid, and that the reference to jQuery is before the reference to the hubs proxy.</span></span> <span data-ttu-id="656a5-252">对中心代理的默认引用应如下所示：</span><span class="sxs-lookup"><span data-stu-id="656a5-252">The default reference to the hubs proxy should look like the following:</span></span>

<span data-ttu-id="656a5-253">**HTML 客户端代码与正确引用中心代理**</span><span class="sxs-lookup"><span data-stu-id="656a5-253">**HTML client-side code that correctly references the Hubs proxy**</span></span>

[!code-html[Main](troubleshooting/samples/sample12.html)]

### <a name="runtimebinderexception-was-unhandled-by-user-code-error"></a><span data-ttu-id="656a5-254">"由用户代码未处理 RuntimeBinderException"错误</span><span class="sxs-lookup"><span data-stu-id="656a5-254">"RuntimeBinderException was unhandled by user code" error</span></span>

<span data-ttu-id="656a5-255">可能会发生此错误时的不正确的重载`Hub.On`使用。</span><span class="sxs-lookup"><span data-stu-id="656a5-255">This error may occur when the incorrect overload of `Hub.On` is used.</span></span> <span data-ttu-id="656a5-256">如果该方法具有返回值，则必须作为泛型类型参数指定返回类型：</span><span class="sxs-lookup"><span data-stu-id="656a5-256">If the method has a return value, the return type must be specified as a generic type parameter:</span></span>

<span data-ttu-id="656a5-257">**（无需生成的代理） 客户端上定义的方法**</span><span class="sxs-lookup"><span data-stu-id="656a5-257">**Method defined on the client (without generated proxy)**</span></span>

[!code-html[Main](troubleshooting/samples/sample13.html?highlight=1)]

### <a name="connection-id-is-inconsistent-or-connection-breaks-between-page-loads"></a><span data-ttu-id="656a5-258">连接 ID 不一致或连接中断之间页面加载</span><span class="sxs-lookup"><span data-stu-id="656a5-258">Connection ID is inconsistent or connection breaks between page loads</span></span>

<span data-ttu-id="656a5-259">此行为是有意安排的。</span><span class="sxs-lookup"><span data-stu-id="656a5-259">This behavior is by design.</span></span> <span data-ttu-id="656a5-260">由于中心对象中的页对象承载，中心被销毁时刷新该页面。</span><span class="sxs-lookup"><span data-stu-id="656a5-260">Since the hub object is hosted in the page object, the hub is destroyed when the page refreshes.</span></span> <span data-ttu-id="656a5-261">多页应用程序需要维护用户与连接 Id 之间的关联，从而使它们将页面加载之间保持一致。</span><span class="sxs-lookup"><span data-stu-id="656a5-261">A multi-page application needs to maintain the association between users and connection IDs so that they will be consistent between page loads.</span></span> <span data-ttu-id="656a5-262">可以在服务器上存储的连接 Id`ConcurrentDictionary`对象或数据库。</span><span class="sxs-lookup"><span data-stu-id="656a5-262">The connection IDs can be stored on the server in either a `ConcurrentDictionary` object or a database.</span></span>

### <a name="value-cannot-be-null-error"></a><span data-ttu-id="656a5-263">"值不能为 null"错误</span><span class="sxs-lookup"><span data-stu-id="656a5-263">"Value cannot be null" error</span></span>

<span data-ttu-id="656a5-264">当前不支持带有可选参数的服务器端方法;如果省略可选参数，该方法将失败。</span><span class="sxs-lookup"><span data-stu-id="656a5-264">Server-side methods with optional parameters are not currently supported; if the optional parameter is omitted, the method will fail.</span></span> <span data-ttu-id="656a5-265">有关详细信息，请参阅[可选参数](https://github.com/SignalR/SignalR/issues/324)。</span><span class="sxs-lookup"><span data-stu-id="656a5-265">For more information, see [Optional Parameters](https://github.com/SignalR/SignalR/issues/324).</span></span>

### <a name="firefox-cant-establish-a-connection-to-the-server-at-ltaddressgt-error-in-firebug"></a><span data-ttu-id="656a5-266">"Firefox 无法建立到上的服务器的连接&lt;地址&gt;"Firebug 时出错</span><span class="sxs-lookup"><span data-stu-id="656a5-266">"Firefox can't establish a connection to the server at &lt;address&gt;" error in Firebug</span></span>

<span data-ttu-id="656a5-267">如果协商的 WebSocket 传输会失败，改为使用另一个传输，可以在 Firebug 看到此错误消息。</span><span class="sxs-lookup"><span data-stu-id="656a5-267">This error message can be seen in Firebug if negotiation of the WebSocket transport fails and another transport is used instead.</span></span> <span data-ttu-id="656a5-268">此行为是有意安排的。</span><span class="sxs-lookup"><span data-stu-id="656a5-268">This behavior is by design.</span></span>

### <a name="the-remote-certificate-is-invalid-according-to-the-validation-procedure-error-in-net-client-application"></a><span data-ttu-id="656a5-269">在.NET 客户端应用程序中的"远程证书无效的验证过程根据"错误</span><span class="sxs-lookup"><span data-stu-id="656a5-269">"The remote certificate is invalid according to the validation procedure" error in .NET client application</span></span>

<span data-ttu-id="656a5-270">如果你的服务器需要自定义客户端证书，则可以将 x509 证书添加到连接之前发出的请求。</span><span class="sxs-lookup"><span data-stu-id="656a5-270">If your server requires custom client certificates, then you can add an x509certificate to the connection before the request is made.</span></span> <span data-ttu-id="656a5-271">将证书添加到连接使用`Connection.AddClientCertificate`。</span><span class="sxs-lookup"><span data-stu-id="656a5-271">Add the certificate to the connection using `Connection.AddClientCertificate`.</span></span>

### <a name="connection-drops-after-authentication-times-out"></a><span data-ttu-id="656a5-272">连接中断后身份验证超时</span><span class="sxs-lookup"><span data-stu-id="656a5-272">Connection drops after authentication times out</span></span>

<span data-ttu-id="656a5-273">此行为是有意安排的。</span><span class="sxs-lookup"><span data-stu-id="656a5-273">This behavior is by design.</span></span> <span data-ttu-id="656a5-274">连接处于活动状态; 时，不能修改身份验证凭据若要刷新的凭据，必须停止并重新启动连接。</span><span class="sxs-lookup"><span data-stu-id="656a5-274">Authentication credentials cannot be modified while a connection is active; to refresh credentials, the connection must be stopped and restarted.</span></span>

### <a name="onconnected-gets-called-twice-when-using-jquery-mobile"></a><span data-ttu-id="656a5-275">OnConnected 获取调用两次时使用 jQuery Mobile</span><span class="sxs-lookup"><span data-stu-id="656a5-275">OnConnected gets called twice when using jQuery Mobile</span></span>

<span data-ttu-id="656a5-276">jQuery Mobile`initializePage`函数强制重新执行，每个页中的脚本从而创建第二个连接。</span><span class="sxs-lookup"><span data-stu-id="656a5-276">jQuery Mobile's `initializePage` function forces the scripts in each page to be re-executed, thus creating a second connection.</span></span> <span data-ttu-id="656a5-277">此问题的解决方法包括：</span><span class="sxs-lookup"><span data-stu-id="656a5-277">Solutions for this issue include:</span></span>

- <span data-ttu-id="656a5-278">包括对 jQuery Mobile JavaScript 文件之前的引用。</span><span class="sxs-lookup"><span data-stu-id="656a5-278">Include the reference to jQuery Mobile before your JavaScript file.</span></span>
- <span data-ttu-id="656a5-279">禁用`initializePage`函数通过设置`$.mobile.autoInitializePage = false`。</span><span class="sxs-lookup"><span data-stu-id="656a5-279">Disable the `initializePage` function by setting `$.mobile.autoInitializePage = false`.</span></span>
- <span data-ttu-id="656a5-280">等待页后，可以完成初始化之前启动连接。</span><span class="sxs-lookup"><span data-stu-id="656a5-280">Wait for the page to finish initializing before starting the connection.</span></span>

### <a name="messages-are-delayed-in-silverlight-applications-using-server-sent-events"></a><span data-ttu-id="656a5-281">消息被延迟 Silverlight 应用程序使用服务器发送的事件中</span><span class="sxs-lookup"><span data-stu-id="656a5-281">Messages are delayed in Silverlight applications using Server Sent Events</span></span>

<span data-ttu-id="656a5-282">使用服务器上 Silverlight 发送事件时，消息被延迟。</span><span class="sxs-lookup"><span data-stu-id="656a5-282">Messages are delayed when using server sent events on Silverlight.</span></span> <span data-ttu-id="656a5-283">若要强制长轮询以改为使用，请在启动连接时使用以下：</span><span class="sxs-lookup"><span data-stu-id="656a5-283">To force long polling to be used instead, use the following when starting the connection:</span></span>

[!code-css[Main](troubleshooting/samples/sample14.css)]

### <a name="permission-denied-using-forever-frame-protocol"></a><span data-ttu-id="656a5-284">"权限被拒绝"使用永久框架协议</span><span class="sxs-lookup"><span data-stu-id="656a5-284">"Permission Denied" using Forever Frame protocol</span></span>

<span data-ttu-id="656a5-285">这是一个已知的问题，所述[此处](https://github.com/SignalR/SignalR/issues/1963)。</span><span class="sxs-lookup"><span data-stu-id="656a5-285">This is a known issue, described [here](https://github.com/SignalR/SignalR/issues/1963).</span></span> <span data-ttu-id="656a5-286">此故障现象，可能会看到使用最新的 JQuery 库;解决方法是降级到 JQuery 1.8.2 应用程序。</span><span class="sxs-lookup"><span data-stu-id="656a5-286">This symptom may be seen using the latest JQuery library; the workaround is to downgrade your application to JQuery 1.8.2.</span></span>

### <a name="invalidoperationexception-not-a-valid-web-socket-request"></a><span data-ttu-id="656a5-287">"InvalidOperationException： 不是有效的 web 套接字请求。</span><span class="sxs-lookup"><span data-stu-id="656a5-287">"InvalidOperationException: Not a valid web socket request.</span></span>

<span data-ttu-id="656a5-288">如果使用 WebSocket 协议，但网络代理修改请求标头，则可能出现此错误。</span><span class="sxs-lookup"><span data-stu-id="656a5-288">This error may occur if the WebSocket protocol is used, but the network proxy is modifying the request headers.</span></span> <span data-ttu-id="656a5-289">解决方案是配置代理服务器以允许在端口 80 上的 WebSocket。</span><span class="sxs-lookup"><span data-stu-id="656a5-289">The solution is to configure the proxy to allow WebSocket on port 80.</span></span>

### <a name="exception-ltmethod-namegt-method-could-not-be-resolved-when-client-calls-method-on-server"></a><span data-ttu-id="656a5-290">"异常：&lt;方法名称&gt;方法无法解析"客户端时在服务器上调用方法</span><span class="sxs-lookup"><span data-stu-id="656a5-290">"Exception: &lt;method name&gt; method could not be resolved" when client calls method on server</span></span>

<span data-ttu-id="656a5-291">使用不能发现在 JSON 负载，如数组中的数据类型，则可能会导致此错误。</span><span class="sxs-lookup"><span data-stu-id="656a5-291">This error can result from using data types that cannot be discovered in a JSON payload, such as Array.</span></span> <span data-ttu-id="656a5-292">解决方法是使用 JSON，如 IList 通过可发现的数据类型。</span><span class="sxs-lookup"><span data-stu-id="656a5-292">The workaround is to use a data type that is discoverable by JSON, such as IList.</span></span> <span data-ttu-id="656a5-293">有关详细信息，请参阅[.NET 客户端无法调用具有数组参数的中心方法](https://github.com/SignalR/SignalR/issues/2672)。</span><span class="sxs-lookup"><span data-stu-id="656a5-293">For more information, see [.NET Client unable to call hub methods with array parameters](https://github.com/SignalR/SignalR/issues/2672).</span></span>

<a id="server"></a>

## <a name="compilation-and-server-side-errors"></a><span data-ttu-id="656a5-294">编译和服务器端错误</span><span class="sxs-lookup"><span data-stu-id="656a5-294">Compilation and server-side errors</span></span>

 <span data-ttu-id="656a5-295">以下部分包含对编译器和服务器端运行时错误可能的解决方案。</span><span class="sxs-lookup"><span data-stu-id="656a5-295">The following section contains possible solutions to compiler and server-side runtime errors.</span></span> 

### <a name="reference-to-hub-instance-is-null"></a><span data-ttu-id="656a5-296">对中心实例引用为 null</span><span class="sxs-lookup"><span data-stu-id="656a5-296">Reference to Hub instance is null</span></span>

<span data-ttu-id="656a5-297">由于系统会为每个连接创建的 hub 实例，你无法创建实例的中心在代码中自己。</span><span class="sxs-lookup"><span data-stu-id="656a5-297">Since a hub instance is created for each connection, you can't create an instance of a hub in your code yourself.</span></span> <span data-ttu-id="656a5-298">若要在一个中心从外部集线器本身上调用方法，请参阅[如何调用方法的客户端和管理从中心类外部的组](../guide-to-the-api/hubs-api-guide-server.md#callfromoutsidehub)有关如何获取对中心上下文的引用。</span><span class="sxs-lookup"><span data-stu-id="656a5-298">To call methods on a hub from outside the hub itself, see [How to call client methods and manage groups from outside the Hub class](../guide-to-the-api/hubs-api-guide-server.md#callfromoutsidehub) for how to obtain a reference to the hub context.</span></span>

### <a name="httpcontextcurrentsession-is-null"></a><span data-ttu-id="656a5-299">HTTPContext.Current.Session 为 null</span><span class="sxs-lookup"><span data-stu-id="656a5-299">HTTPContext.Current.Session is null</span></span>

<span data-ttu-id="656a5-300">此行为是有意安排的。</span><span class="sxs-lookup"><span data-stu-id="656a5-300">This behavior is by design.</span></span> <span data-ttu-id="656a5-301">SignalR 不支持 ASP.NET 会话状态，因为启用会话状态将会破坏双工消息传递。</span><span class="sxs-lookup"><span data-stu-id="656a5-301">SignalR does not support the ASP.NET session state, since enabling the session state would break duplex messaging.</span></span>

### <a name="no-suitable-method-to-override"></a><span data-ttu-id="656a5-302">没有合适的方法重写</span><span class="sxs-lookup"><span data-stu-id="656a5-302">No suitable method to override</span></span>

<span data-ttu-id="656a5-303">如果你使用的较旧的文档或博客中的代码，你可能会看到此错误。</span><span class="sxs-lookup"><span data-stu-id="656a5-303">You may see this error if you are using code from older documentation or blogs.</span></span> <span data-ttu-id="656a5-304">验证未引用的已更改或已弃用的方法名称 (如`OnConnectedAsync`)。</span><span class="sxs-lookup"><span data-stu-id="656a5-304">Verify that you are not referencing names of methods that have been changed or deprecated (like `OnConnectedAsync`).</span></span>

### <a name="hostcontextextensionswebsocketserverurl-is-null"></a><span data-ttu-id="656a5-305">HostContextExtensions.WebSocketServerUrl 为 null</span><span class="sxs-lookup"><span data-stu-id="656a5-305">HostContextExtensions.WebSocketServerUrl is null</span></span>

<span data-ttu-id="656a5-306">此行为是有意安排的。</span><span class="sxs-lookup"><span data-stu-id="656a5-306">This behavior is by design.</span></span> <span data-ttu-id="656a5-307">此成员已弃用，不应使用。</span><span class="sxs-lookup"><span data-stu-id="656a5-307">This member is deprecated and should not be used.</span></span>

### <a name="a-route-named-signalrhubs-is-already-in-the-route-collection-error"></a><span data-ttu-id="656a5-308">"名为 signalr.hubs 的路由集合中已路由"错误</span><span class="sxs-lookup"><span data-stu-id="656a5-308">"A route named 'signalr.hubs' is already in the route collection" error</span></span>

<span data-ttu-id="656a5-309">将出现此错误，如果`MapSignalR`两次由你的应用程序调用。</span><span class="sxs-lookup"><span data-stu-id="656a5-309">This error will be seen if `MapSignalR` is called twice by your application.</span></span> <span data-ttu-id="656a5-310">一些示例应用程序调用`MapSignalR`直接在 Startup 类; 其他人在中进行调用的包装类。</span><span class="sxs-lookup"><span data-stu-id="656a5-310">Some example applications call `MapSignalR` directly in the Startup class; others make the call in a wrapper class.</span></span> <span data-ttu-id="656a5-311">确保你的应用程序不会不两。</span><span class="sxs-lookup"><span data-stu-id="656a5-311">Ensure that your application does not do both.</span></span>

### <a name="websocket-is-not-used"></a><span data-ttu-id="656a5-312">未使用 WebSocket</span><span class="sxs-lookup"><span data-stu-id="656a5-312">WebSocket is not used</span></span>

<span data-ttu-id="656a5-313">如果已验证你的服务器和客户端满足 WebSocket 的要求 (列入[支持的平台](../getting-started/supported-platforms.md)文档)，你将需要在你的服务器上启用 WebSocket。</span><span class="sxs-lookup"><span data-stu-id="656a5-313">If you have verified that your server and clients meet the requirements for WebSocket (listed in the [Supported Platforms](../getting-started/supported-platforms.md) document), you will need to enable WebSocket on your server.</span></span> <span data-ttu-id="656a5-314">找不到为执行此操作的说明[此处](https://www.iis.net/learn/get-started/whats-new-in-iis-8/iis-80-websocket-protocol-support)。</span><span class="sxs-lookup"><span data-stu-id="656a5-314">Instructions for doing this can be found [here](https://www.iis.net/learn/get-started/whats-new-in-iis-8/iis-80-websocket-protocol-support).</span></span>

### <a name="connection-is-undefined"></a><span data-ttu-id="656a5-315">$.connection 未定义</span><span class="sxs-lookup"><span data-stu-id="656a5-315">$.connection is undefined</span></span>

<span data-ttu-id="656a5-316">此错误表示，在页面上的脚本加载不正确，或者是中心代理不可访问或正在访问的不正确。</span><span class="sxs-lookup"><span data-stu-id="656a5-316">This error indicates that either the scripts on a page are not being loaded properly, or the hub proxy is not reachable or is being accessed incorrectly.</span></span> <span data-ttu-id="656a5-317">验证在你页面上的脚本引用对应于在项目中，加载的脚本和 /signalr/hubs 可以访问在浏览器中，如果服务器运行。</span><span class="sxs-lookup"><span data-stu-id="656a5-317">Verify that the script references on your page correspond to the scripts loaded in your project, and that /signalr/hubs can be accessed in a browser when the server is running.</span></span>

### <a name="one-or-more-types-required-to-compile-a-dynamic-expression-cannot-be-found"></a><span data-ttu-id="656a5-318">找不到需要编译动态表达式的一个或多个类型</span><span class="sxs-lookup"><span data-stu-id="656a5-318">One or more types required to compile a dynamic expression cannot be found</span></span>

<span data-ttu-id="656a5-319">此错误指示`Microsoft.CSharp`库是缺失。</span><span class="sxs-lookup"><span data-stu-id="656a5-319">This error indicates that the `Microsoft.CSharp` library is missing.</span></span> <span data-ttu-id="656a5-320">添加在**程序集的&gt;Framework**选项卡。</span><span class="sxs-lookup"><span data-stu-id="656a5-320">Add it in the **Assemblies-&gt;Framework** tab.</span></span>

### <a name="caller-state-cannot-be-accessed-from-clientscaller-in-visual-basic-or-in-a-strongly-typed-hub-conversion-from-type-taskof-object-to-type-string-is-not-valid-error"></a><span data-ttu-id="656a5-321">不能从 Clients.Caller 在 Visual Basic 中或在强类型化的中心; 访问调用方状态"从类型任务 （的对象） 到类型 'String' 的转换无效"错误</span><span class="sxs-lookup"><span data-stu-id="656a5-321">Caller state cannot be accessed from Clients.Caller in Visual Basic or in a strongly typed hub; "Conversion from type 'Task(Of Object)' to type 'String' is not valid" error</span></span>

<span data-ttu-id="656a5-322">若要访问调用方状态在 Visual Basic 中或在强类型化的中心，使用`Clients.CallerState`属性 （在 SignalR 2.1 中引入） 而不是`Clients.Caller`。</span><span class="sxs-lookup"><span data-stu-id="656a5-322">To access caller state in Visual Basic or in a strongly typed hub, use the `Clients.CallerState` property (introduced in SignalR 2.1) instead of `Clients.Caller`.</span></span>

<a id="vs"></a>

## <a name="visual-studio-issues"></a><span data-ttu-id="656a5-323">Visual Studio 问题</span><span class="sxs-lookup"><span data-stu-id="656a5-323">Visual Studio issues</span></span>

<span data-ttu-id="656a5-324">本部分介绍在 Visual Studio 中遇到问题。</span><span class="sxs-lookup"><span data-stu-id="656a5-324">This section describes issues encountered in Visual Studio.</span></span>

### <a name="script-documents-node-does-not-appear-in-solution-explorer"></a><span data-ttu-id="656a5-325">在解决方案资源管理器中不显示脚本文档节点</span><span class="sxs-lookup"><span data-stu-id="656a5-325">Script Documents node does not appear in Solution Explorer</span></span>

<span data-ttu-id="656a5-326">一些我们的教程在调试时将你定向到解决方案资源管理器中的"脚本文档"节点。</span><span class="sxs-lookup"><span data-stu-id="656a5-326">Some of our tutorials direct you to the "Script Documents" node in Solution Explorer while debugging.</span></span> <span data-ttu-id="656a5-327">此节点由 JavaScript 调试器中，并且将只会显示调试 Internet Explorer; 中的浏览器客户端时如果使用 Chrome 或 Firefox，将不会出现该节点。</span><span class="sxs-lookup"><span data-stu-id="656a5-327">This node is produced by the JavaScript debugger, and will only appear while debugging browser clients in Internet Explorer; the node will not appear if Chrome or Firefox are used.</span></span> <span data-ttu-id="656a5-328">如果正在运行另一个客户端调试器，例如 Silverlight 调试器 JavaScript 调试器也将不运行。</span><span class="sxs-lookup"><span data-stu-id="656a5-328">The JavaScript debugger will also not run if another client debugger is running, such as the Silverlight debugger.</span></span>

### <a name="signalr-does-not-work-on-visual-studio-2008-or-earlier"></a><span data-ttu-id="656a5-329">Visual Studio 2008 或更低版本 SignalR 不起作用</span><span class="sxs-lookup"><span data-stu-id="656a5-329">SignalR does not work on Visual Studio 2008 or earlier</span></span>

<span data-ttu-id="656a5-330">此行为是有意安排的。</span><span class="sxs-lookup"><span data-stu-id="656a5-330">This behavior is by design.</span></span> <span data-ttu-id="656a5-331">SignalR 需要.NET Framework 4 或更高版本;这需要 Visual Studio 2010 或更高版本的情况下开发 SignalR 应用程序。</span><span class="sxs-lookup"><span data-stu-id="656a5-331">SignalR requires .NET Framework 4 or later; this requires that SignalR applications be developed in Visual Studio 2010 or later.</span></span> <span data-ttu-id="656a5-332">SignalR 的服务器组件需要.NET Framework 4.5。</span><span class="sxs-lookup"><span data-stu-id="656a5-332">The server component of SignalR requires .NET Framework 4.5.</span></span>

<a id="iis"></a>

## <a name="iis-issues"></a><span data-ttu-id="656a5-333">IIS 问题</span><span class="sxs-lookup"><span data-stu-id="656a5-333">IIS issues</span></span>

<span data-ttu-id="656a5-334">本部分包含使用 Internet 信息服务的问题。</span><span class="sxs-lookup"><span data-stu-id="656a5-334">This section contains issues with Internet Information Services.</span></span>

### <a name="signalr-works-on-visual-studio-development-server-but-not-in-iis"></a><span data-ttu-id="656a5-335">在 Visual Studio 开发服务器上，但不是在 IIS 中的 SignalR 工作原理</span><span class="sxs-lookup"><span data-stu-id="656a5-335">SignalR works on Visual Studio development server, but not in IIS</span></span>

<span data-ttu-id="656a5-336">SignalR 支持在 IIS 7.0 和 7.5，但必须添加无扩展名的 Url 的支持。</span><span class="sxs-lookup"><span data-stu-id="656a5-336">SignalR is supported on IIS 7.0 and 7.5, but support for extensionless URLs must be added.</span></span> <span data-ttu-id="656a5-337">若要添加支持无扩展名的 Url，请参阅[https://support.microsoft.com/kb/980368](https://support.microsoft.com/kb/980368)</span><span class="sxs-lookup"><span data-stu-id="656a5-337">To add support for extensionless URLs, see [https://support.microsoft.com/kb/980368](https://support.microsoft.com/kb/980368)</span></span>

<span data-ttu-id="656a5-338">SignalR 需要 ASP.NET （ASP.NET 未安装 IIS 默认情况下） 在服务器上安装。</span><span class="sxs-lookup"><span data-stu-id="656a5-338">SignalR requires ASP.NET to be installed on the server (ASP.NET is not installed on IIS by default).</span></span> <span data-ttu-id="656a5-339">若要安装 ASP.NET，请参阅[ASP.NET 下载](https://www.asp.net/downloads)。</span><span class="sxs-lookup"><span data-stu-id="656a5-339">To install ASP.NET, see [ASP.NET Downloads](https://www.asp.net/downloads).</span></span>

<a id="azure"></a>

## <a name="microsoft-azure-issues"></a><span data-ttu-id="656a5-340">Microsoft Azure 问题</span><span class="sxs-lookup"><span data-stu-id="656a5-340">Microsoft Azure issues</span></span>

<span data-ttu-id="656a5-341">本部分包含与 Microsoft Azure 的问题。</span><span class="sxs-lookup"><span data-stu-id="656a5-341">This section contains issues with Microsoft Azure.</span></span>

### <a name="fileloadexception-when-hosting-signalr-in-an-azure-worker-role"></a><span data-ttu-id="656a5-342">FileLoadException 托管在 Azure 辅助角色中的 SignalR 时</span><span class="sxs-lookup"><span data-stu-id="656a5-342">FileLoadException when hosting SignalR in an Azure Worker Role</span></span>

<span data-ttu-id="656a5-343">承载在 Azure 辅助角色中的 SignalR 在异常中可能会导致"无法加载文件或程序集 Microsoft.Owin，Version = 2.0.0.0"。</span><span class="sxs-lookup"><span data-stu-id="656a5-343">Hosting SignalR in an Azure Worker Role might result in the exception "Could not load file or assembly 'Microsoft.Owin, Version=2.0.0.0".</span></span> <span data-ttu-id="656a5-344">这是使用 NuGet; 一个已知的问题绑定重定向不会自动添加在 Azure 辅助角色项目中。</span><span class="sxs-lookup"><span data-stu-id="656a5-344">This is a known issue with NuGet; Binding redirects are not added automatically in Azure Worker Role projects.</span></span> <span data-ttu-id="656a5-345">若要解决此问题，您可以手动添加绑定重定向。</span><span class="sxs-lookup"><span data-stu-id="656a5-345">To fix this, you can add the binding redirects manually.</span></span> <span data-ttu-id="656a5-346">添加以下行`app.config`辅助角色项目文件。</span><span class="sxs-lookup"><span data-stu-id="656a5-346">Add the following lines to the `app.config` file for your Worker Role project.</span></span>

[!code-xml[Main](troubleshooting/samples/sample15.xml)]

### <a name="messages-are-not-received-through-the-azure-backplane-after-altering-topic-names"></a><span data-ttu-id="656a5-347">收到的消息通过 Azure 底板后更改主题名称</span><span class="sxs-lookup"><span data-stu-id="656a5-347">Messages are not received through the Azure backplane after altering topic names</span></span>

<span data-ttu-id="656a5-348">使用 Azure 底板的主题是在内部; 进行维护不应将它们用户可配置。</span><span class="sxs-lookup"><span data-stu-id="656a5-348">The topics used by the Azure backplane are maintained internally; they are not intended to be user-configurable.</span></span>
