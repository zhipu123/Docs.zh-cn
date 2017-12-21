---
title: ".NET 的开放 Web 接口 (OWIN)"
author: ardalis
description: "发现如何 ASP.NET Core 支持打开的 Web 接口的.NET (OWIN)，这允许 web 应用程序从 web 服务器分离。"
keywords: "ASP.NET 核心，为使.NET，OWIN 打开 Web 接口"
ms.author: riande
manager: wpickett
ms.date: 10/14/2016
ms.topic: article
ms.assetid: 70c4e6bc-a773-4039-96ec-6fe557c9369d
ms.technology: aspnet
ms.prod: asp.net-core
uid: fundamentals/owin
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e2ee970a1c9cd05ebee76b92c3e2c7c6c6cc6ef8
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2017
---
# <a name="introduction-to-open-web-interface-for-net-owin"></a>.NET Web 开放标准接口(OWIN)简介

通过[Steve Smith](https://ardalis.com/)和[Rick Anderson](https://twitter.com/RickAndMSFT)


ASP.NET Core 支持 .NET 的开放 Web 接口 (OWIN)。 OWIN 允许 Web 应用从 Web 服务器分离。 它定义的中间件来用于在管道中使用，以处理请求和响应关联的标准方法。 ASP.NET Core 应用程序和中间件可以与基于 OWIN 的应用程序、 服务器和中间件互操作。

OWIN 提供了允许与不同的对象模型一起使用的两个框架解除层。 `Microsoft.AspNetCore.Owin`包提供了两个适配器实现：
- 从 OWIN 到 ASP.NET Core 
- 从 ASP.NET Core 到 OWIN 

这样 ASP.NET Core 应用就可以托管在基于 OWIN 的服务器/主机，另外又可以在 ASP.NET Core 上运行其他 OWIN 兼容的组件。

注意： 使用这些适配器附带有一定的性能开销。 如果仅仅使用了 ASP.NET Core的应用程序不应使用 Owin 的包或适配器。

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/owin/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）

## <a name="running-owin-middleware-in-the-aspnet-pipeline"></a>在 ASP.NET 管道中运行 OWIN 中间件

ASP.NET Core 对于 OWIN 的支持包含在`Microsoft.AspNetCore.Owin`包中。 你可以通过安装此包导入你的项目的中来获取 OWIN 支持。

OWIN middleware conforms to the OWIN specification, which requires a Func<IDictionary<string, object>, Task> interface, and specific keys be set (such as owin.ResponseBody). The following simple OWIN middleware displays "Hello World":


OWIN 中间件遵循[OWIN 规范](http://owin.org/spec/spec/owin-1.0.0.html)，他实现了`Func<IDictionary<string, object>, Task>`接口并通过特定的键值对操作环境变量 (如`owin.ResponseBody`)。 以下简单的 OWIN 中间件将显示"Hello World":

```csharp
public Task OwinHello(IDictionary<string, object> environment)
{
    string responseText = "Hello World via OWIN";
    byte[] responseBytes = Encoding.UTF8.GetBytes(responseText);

    // OWIN Environment Keys: http://owin.org/spec/spec/owin-1.0.0.html
    var responseStream = (Stream)environment["owin.ResponseBody"];
    var responseHeaders = (IDictionary<string, string[]>)environment["owin.ResponseHeaders"];

    responseHeaders["Content-Length"] = new string[] { responseBytes.Length.ToString(CultureInfo.InvariantCulture) };
    responseHeaders["Content-Type"] = new string[] { "text/plain" };

    return responseStream.WriteAsync(responseBytes, 0, responseBytes.Length);
}
```

示例代码 遵循 OWIN 标准返回`Task`并接受`IDictionary<string, object>`作为参数 。

下面的代码演示如何将 `OwinHello`（上面所述） 中间件添加到 ASP.NET 的管道中,只需要使用 `UseOwin`扩展方法。

```csharp
public void Configure(IApplicationBuilder app)
{
    app.UseOwin(pipeline =>
    {
        pipeline(next => OwinHello);
    });
}
```

你可以使用通过OWIN 管道配置更多的操作。

> [!NOTE]
> 必须在首次向响应流写入之前修改响应标头。

> [!NOTE]
> 不建议多次调用`UseOwin`,因为这样可能会引发性能问题。最好的方式是将OWIN Pipeline系统的组合在一起。

```csharp
app.UseOwin(pipeline =>
{
    pipeline(next =>
    {
        // do something before
        return OwinHello;
        // do something after
    });
});
```

<a name="hosting-on-owin"></a>

## <a name="using-aspnet-hosting-on-an-owin-based-server"></a>在基于 OWIN 的服务器上 使用 ASP.NET 

基于 OWIN 的服务器可以承载 ASP.NET 应用程序。 [Nowin](https://github.com/Bobris/Nowin)就是基于 OWIN 的服务器中的一个实现。 在本文示例中，我们创建了一个项目，这个项引用了 Nowin 并使用它创建了一个可以运行　ASP.NET Core　的　`IServer` 。

[!code-csharp[Main](owin/sample/src/NowinSample/Program.cs?highlight=15)]

Start is responsible for configuring and starting the server, which in this case is done through a series of fluent API calls that set addresses parsed from the IServerAddressesFeature. Note that the fluent configuration of the _builder variable specifies that requests will be handled by the appFunc defined earlier in the method. This Func is called on each request to process incoming requests.

We'll also add an IWebHostBuilder extension to make it easy to add and configure the Nowin server.
`IServer`作为接口，需要`Features`属性和`Start`方法。

`Start`负责配置和启动服务器．通过一连串的fluent API调用, 我们设置Server的地址,这些地址是从 IServerAddressesFeature 那里解析出来的。 请注意的 fluent 配置`_builder`变量指定了所有的请求会被方法里指定的`appFunc`响应。 每个请求以处理传入的请求都会被这个`Func`处理。

我们还将添加`IWebHostBuilder`扩展，以便可以方便地添加和配置 Nowin 服务器。

```csharp
using System;
using Microsoft.AspNetCore.Hosting.Server;
using Microsoft.Extensions.DependencyInjection;
using Nowin;
using NowinSample;

namespace Microsoft.AspNetCore.Hosting
{
    public static class NowinWebHostBuilderExtensions
    {
        public static IWebHostBuilder UseNowin(this IWebHostBuilder builder)
        {
            return builder.ConfigureServices(services =>
            {
                services.AddSingleton<IServer, NowinServer>();
            });
        }

        public static IWebHostBuilder UseNowin(this IWebHostBuilder builder, Action<ServerBuilder> configure)
        {
            builder.ConfigureServices(services =>
            {
                services.Configure(configure);
            });
            return builder.UseNowin();
        }
    }
}
```

与此就地，所有，具有需要运行 ASP.NET 应用程序使用此自定义服务器调用扩展*Program.cs*:

```csharp

using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Threading.Tasks;
using Microsoft.AspNetCore.Hosting;

namespace NowinSample
{
    public class Program
    {
        public static void Main(string[] args)
        {
            var host = new WebHostBuilder()
                .UseNowin()
                .UseContentRoot(Directory.GetCurrentDirectory())
                .UseIISIntegration()
                .UseStartup<Startup>()
                .Build();

            host.Run();
        }
    }
}

```

了解有关 ASP.NET[服务器](servers/index.md)。

## <a name="run-aspnet-core-on-an-owin-based-server-and-use-its-websockets-support"></a>基于 OWIN 的服务器上运行 ASP.NET 核心，并使用其 Websocket 支持

如何基于 OWIN 的服务器的功能的另一个示例可以利用 ASP.NET 核心是对等 Websocket 功能的访问。 在前面的示例使用的.NET OWIN web 服务器具有用于 Web 套接字内置的这可以利用 ASP.NET Core 应用程序支持。 下面的示例演示一个简单的 web 应用，支持 Web 套接字回显 Websocket 通过向服务器发送的所有内容。

```csharp
public class Startup
{
    public void Configure(IApplicationBuilder app)
    {
        app.Use(async (context, next) =>
        {
            if (context.WebSockets.IsWebSocketRequest)
            {
                WebSocket webSocket = await context.WebSockets.AcceptWebSocketAsync();
                await EchoWebSocket(webSocket);
            }
            else
            {
                await next();
            }
        });

        app.Run(context =>
        {
            return context.Response.WriteAsync("Hello World");
        });
    }

    private async Task EchoWebSocket(WebSocket webSocket)
    {
        byte[] buffer = new byte[1024];
        WebSocketReceiveResult received = await webSocket.ReceiveAsync(
            new ArraySegment<byte>(buffer), CancellationToken.None);

        while (!webSocket.CloseStatus.HasValue)
        {
            // Echo anything we receive
            await webSocket.SendAsync(new ArraySegment<byte>(buffer, 0, received.Count), 
                received.MessageType, received.EndOfMessage, CancellationToken.None);

            received = await webSocket.ReceiveAsync(new ArraySegment<byte>(buffer), 
                CancellationToken.None);
        }

        await webSocket.CloseAsync(webSocket.CloseStatus.Value, 
            webSocket.CloseStatusDescription, CancellationToken.None);
    }
}
```

这[示例](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/owin/sample)使用相同配置`NowinServer`与之前的唯一的区别是在应用程序中的配置方式其`Configure`方法。 测试使用[简单 websocket 客户端](https://chrome.google.com/webstore/detail/simple-websocket-client/pfdhoblngboilpfeibdedpjgfnlcodoo?hl=en)演示应用程序：

![Web 套接字测试客户端](owin/_static/websocket-test.png)

## <a name="owin-environment"></a>OWIN 环境

你可以构造 OWIN 环境使用`HttpContext`。

```csharp

   var environment = new OwinEnvironment(HttpContext);
   var features = new OwinFeatureCollection(environment);
   ```

## <a name="owin-keys"></a>OWIN 键

取决于 OWIN`IDictionary<string,object>`对象进行通信信息的整个 HTTP 请求/响应交换。 ASP.NET 核心实现下面列出的密钥。 请参阅[主规范、 扩展](http://owin.org/#spec)，和[OWIN 键指导原则和常见的键](http://owin.org/spec/spec/CommonKeys.html)。

### <a name="request-data-owin-v100"></a>请求的数据 (OWIN v1.0.0)

| 键               | 值 （类型） | 描述 |
| ----------------- | ------------ | ----------- |
| owin。RequestScheme | `String` |  |
| owin。RequestMethod  | `String` | |    
| owin。RequestPathBase  | `String` | |    
| owin。RequestPath | `String` | |     
| owin。RequestQueryString  | `String` | |    
| owin。RequestProtocol  | `String` | |    
| owin。RequestHeaders | `IDictionary<string,string[]>`  | |
| owin。RequestBody | `Stream`  | |

### <a name="request-data-owin-v110"></a>请求的数据 (OWIN v1.1.0)

| 键               | 值 （类型） | 描述 |
| ----------------- | ------------ | ----------- |
| owin。请求 Id | `String` | Optional |

### <a name="response-data-owin-v100"></a>响应数据 (OWIN v1.0.0)

| 键               | 值 （类型） | 描述 |
| ----------------- | ------------ | ----------- |
| owin。ResponseStatusCode | `int` | Optional |
| owin。ResponseReasonPhrase | `String` | Optional |
| owin。ResponseHeaders | `IDictionary<string,string[]>`  | |
| owin。ResponseBody | `Stream`  | |


### <a name="other-data-owin-v100"></a>其他数据 (OWIN v1.0.0)

| 键               | 值 （类型） | 描述 |
| ----------------- | ------------ | ----------- |
| owin。CallCancelled | `CancellationToken` |  |
| owin。版本  | `String` | |   


### <a name="common-keys"></a>常见的键

| 键               | 值 （类型） | 描述 |
| ----------------- | ------------ | ----------- |
| ssl。ClientCertificate | `X509Certificate` |  |
| ssl。LoadClientCertAsync  | `Func<Task>` | |    
| 服务器。RemoteIpAddress  | `String` | |    
| 服务器。端口远程端口 | `String` | |     
| 服务器。LocalIpAddress  | `String` | |    
| 服务器。LocalPort  | `String` | |    
| 服务器。IsLocal  | `bool` | |    
| 服务器。OnSendingHeaders  | `Action<Action<object>,object>` | |


### <a name="sendfiles-v030"></a>SendFiles v0.3.0

| 键               | 值 （类型） | 描述 |
| ----------------- | ------------ | ----------- |
| sendfile。SendAsync | 请参阅[委托签名](http://owin.org/spec/extensions/owin-SendFile-Extension-v0.3.0.htm) | 每个请求 |


### <a name="opaque-v030"></a>不透明 v0.3.0

| 键               | 值 （类型） | 描述 |
| ----------------- | ------------ | ----------- |
| 不透明。版本 | `String` |  |
| 不透明。升级 | `OpaqueUpgrade` | 请参阅[委托签名](http://owin.org/spec/extensions/owin-SendFile-Extension-v0.3.0.htm) |
| 不透明。流 | `Stream` |  |
| 不透明。CallCancelled | `CancellationToken` |  |


### <a name="websocket-v030"></a>WebSocket v0.3.0

| 键               | 值 （类型） | 描述 |
| ----------------- | ------------ | ----------- |
| websocket。版本 | `String` |  |
| websocket。接受 | `WebSocketAccept` | 请参阅[委托签名](http://owin.org/spec/extensions/owin-SendFile-Extension-v0.3.0.htm) |
| websocket。AcceptAlt |  | 非规范 |
| websocket。子协议 | `String` | 请参阅[RFC6455 4.2.2](https://tools.ietf.org/html/rfc6455#section-4.2.2)步骤 5.5 |
| websocket。SendAsync | `WebSocketSendAsync` | 请参阅[委托签名](http://owin.org/spec/extensions/owin-SendFile-Extension-v0.3.0.htm)  |
| websocket。ReceiveAsync | `WebSocketReceiveAsync` | 请参阅[委托签名](http://owin.org/spec/extensions/owin-SendFile-Extension-v0.3.0.htm)  |
| websocket。CloseAsync | `WebSocketCloseAsync` | 请参阅[委托签名](http://owin.org/spec/extensions/owin-SendFile-Extension-v0.3.0.htm)  |
| websocket。CallCancelled | `CancellationToken` |  |
| websocket。ClientCloseStatus | `int` | Optional |
| websocket。ClientCloseDescription | `String` | Optional |


## <a name="additional-resources"></a>其他资源

* [中间件](middleware.md)

* [服务器](servers/index.md)
