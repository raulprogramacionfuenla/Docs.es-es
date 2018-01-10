---
uid: signalr/overview/security/hub-authorization
title: "Autenticación y autorización para los concentradores SignalR | Documentos de Microsoft"
author: pfletcher
description: "En este tema se describe cómo restringir qué usuarios o roles pueden tener acceso a métodos de concentrador. Versiones de software usan en este tema ha de Visual Studio 2013 .NET 4.5 SignalR..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/05/2015
ms.topic: article
ms.assetid: a610c796-c131-473c-baef-2e6c568cb2a2
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/security/hub-authorization
msc.type: authoredcontent
ms.openlocfilehash: f1538c933ff9e8e680d70ce1e63d24b189be47e5
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/10/2017
---
<a name="authentication-and-authorization-for-signalr-hubs"></a><span data-ttu-id="70847-104">Autenticación y autorización para los concentradores de SignalR</span><span class="sxs-lookup"><span data-stu-id="70847-104">Authentication and Authorization for SignalR Hubs</span></span>
====================
<span data-ttu-id="70847-105">por [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="70847-105">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="70847-106">En este tema se describe cómo restringir qué usuarios o roles pueden tener acceso a métodos de concentrador.</span><span class="sxs-lookup"><span data-stu-id="70847-106">This topic describes how to restrict which users or roles can access hub methods.</span></span> 
> 
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="70847-107">Versiones de software que se usa en este tema</span><span class="sxs-lookup"><span data-stu-id="70847-107">Software versions used in this topic</span></span>
> 
> 
> - [<span data-ttu-id="70847-108">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="70847-108">Visual Studio 2013</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - <span data-ttu-id="70847-109">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="70847-109">.NET 4.5</span></span>
> - <span data-ttu-id="70847-110">SignalR versión 2</span><span class="sxs-lookup"><span data-stu-id="70847-110">SignalR version 2</span></span>
>   
> 
> 
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="70847-111">Versiones anteriores de este tema</span><span class="sxs-lookup"><span data-stu-id="70847-111">Previous versions of this topic</span></span>
> 
> <span data-ttu-id="70847-112">Para obtener información acerca de las versiones anteriores de SignalR, consulte [versiones anteriores de SignalR](../older-versions/index.md).</span><span class="sxs-lookup"><span data-stu-id="70847-112">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="70847-113">Preguntas y comentarios</span><span class="sxs-lookup"><span data-stu-id="70847-113">Questions and comments</span></span>
> 
> <span data-ttu-id="70847-114">Vota sobre cómo le gustó este tutorial y lo que podemos mejorar en los comentarios en la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="70847-114">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="70847-115">Si tiene preguntas que no están directamente relacionados con el tutorial, puede publicar para la [foro de ASP.NET SignalR](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) o [StackOverflow.com](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="70847-115">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>


## <a name="overview"></a><span data-ttu-id="70847-116">Información general</span><span class="sxs-lookup"><span data-stu-id="70847-116">Overview</span></span>

<span data-ttu-id="70847-117">Este tema contiene las siguientes secciones:</span><span class="sxs-lookup"><span data-stu-id="70847-117">This topic contains the following sections:</span></span>

- [<span data-ttu-id="70847-118">Autorizar el atributo</span><span class="sxs-lookup"><span data-stu-id="70847-118">Authorize attribute</span></span>](#authorizeattribute)
- [<span data-ttu-id="70847-119">Requerir autenticación para todos los centros</span><span class="sxs-lookup"><span data-stu-id="70847-119">Require authentication for all hubs</span></span>](#requireauth)
- [<span data-ttu-id="70847-120">Autorización personalizada</span><span class="sxs-lookup"><span data-stu-id="70847-120">Customized authorization</span></span>](#custom)
- [<span data-ttu-id="70847-121">Pasar información de autenticación a los clientes</span><span class="sxs-lookup"><span data-stu-id="70847-121">Pass authentication information to clients</span></span>](#passauth)
- [<span data-ttu-id="70847-122">Opciones de autenticación para los clientes de .NET</span><span class="sxs-lookup"><span data-stu-id="70847-122">Authentication options for .NET clients</span></span>](#authoptions)

    - [<span data-ttu-id="70847-123">Cookie de autenticación de formularios</span><span class="sxs-lookup"><span data-stu-id="70847-123">Cookie with Forms Authentication</span></span>](#cookie)
    - [<span data-ttu-id="70847-124">Autenticación de Windows</span><span class="sxs-lookup"><span data-stu-id="70847-124">Windows Authentication</span></span>](#windows)
    - [<span data-ttu-id="70847-125">Encabezado de conexión</span><span class="sxs-lookup"><span data-stu-id="70847-125">Connection header</span></span>](#header)
    - [<span data-ttu-id="70847-126">Certificado</span><span class="sxs-lookup"><span data-stu-id="70847-126">Certificate</span></span>](#certificate)

<a id="authorizeattribute"></a>

## <a name="authorize-attribute"></a><span data-ttu-id="70847-127">Autorizar el atributo</span><span class="sxs-lookup"><span data-stu-id="70847-127">Authorize attribute</span></span>

<span data-ttu-id="70847-128">SignalR proporciona el [Authorize](https://msdn.microsoft.com/en-us/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx) atributo para especificar qué usuarios o roles tienen acceso a un concentrador o un método.</span><span class="sxs-lookup"><span data-stu-id="70847-128">SignalR provides the [Authorize](https://msdn.microsoft.com/en-us/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx) attribute to specify which users or roles have access to a hub or method.</span></span> <span data-ttu-id="70847-129">Este atributo se encuentra en la `Microsoft.AspNet.SignalR` espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="70847-129">This attribute is located in the `Microsoft.AspNet.SignalR` namespace.</span></span> <span data-ttu-id="70847-130">Aplicar el `Authorize` atributo a un concentrador o determinados métodos en un concentrador.</span><span class="sxs-lookup"><span data-stu-id="70847-130">You apply the `Authorize` attribute to either a hub or particular methods in a hub.</span></span> <span data-ttu-id="70847-131">Al aplicar el `Authorize` atributo a una clase de base de datos central, el requisito de autorización especificado se aplica a todos los métodos en el concentrador.</span><span class="sxs-lookup"><span data-stu-id="70847-131">When you apply the `Authorize` attribute to a hub class, the specified authorization requirement is applied to all of the methods in the hub.</span></span> <span data-ttu-id="70847-132">En este tema se proporciona ejemplos de los distintos tipos de requisitos de autorización que se pueden aplicar.</span><span class="sxs-lookup"><span data-stu-id="70847-132">This topic provides examples of the different types of authorization requirements that you can apply.</span></span> <span data-ttu-id="70847-133">Sin el `Authorize` atributo conectada cliente puede tener acceso a cualquier método público en el concentrador.</span><span class="sxs-lookup"><span data-stu-id="70847-133">Without the `Authorize` attribute, a connected client can access any public method on the hub.</span></span>

<span data-ttu-id="70847-134">Si ha definido un rol denominado "Admin" en la aplicación web, puede especificar que sólo los usuarios con ese rol pueden tener acceso a un concentrador con el código siguiente.</span><span class="sxs-lookup"><span data-stu-id="70847-134">If you have defined a role named "Admin" in your web application, you could specify that only users in that role can access a hub with the following code.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample1.cs)]

<span data-ttu-id="70847-135">O bien, puede especificar que un concentrador contiene un método que está disponible para todos los usuarios y un segundo método solo está disponible para los usuarios autenticados, tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="70847-135">Or, you can specify that a hub contains one method that is available to all users, and a second method that is only available to authenticated users, as shown below.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample2.cs)]

<span data-ttu-id="70847-136">Los siguientes ejemplos referentes a los escenarios de autorización diferentes:</span><span class="sxs-lookup"><span data-stu-id="70847-136">The following examples address different authorization scenarios:</span></span>

- <span data-ttu-id="70847-137">`[Authorize]`: solo los usuarios autenticados</span><span class="sxs-lookup"><span data-stu-id="70847-137">`[Authorize]` – only authenticated users</span></span>
- <span data-ttu-id="70847-138">`[Authorize(Roles = "Admin,Manager")]`: solo autenticados los usuarios de los roles especificados</span><span class="sxs-lookup"><span data-stu-id="70847-138">`[Authorize(Roles = "Admin,Manager")]` – only authenticated users in the specified roles</span></span>
- <span data-ttu-id="70847-139">`[Authorize(Users = "user1,user2")]`: solo autenticados los usuarios con los nombres de usuario especificado</span><span class="sxs-lookup"><span data-stu-id="70847-139">`[Authorize(Users = "user1,user2")]` – only authenticated users with the specified user names</span></span>
- <span data-ttu-id="70847-140">`[Authorize(RequireOutgoing=false)]`: solo los usuarios autenticados pueden invocar el concentrador, pero las llamadas desde el servidor a los clientes no están limitadas por la autorización, como por ejemplo, cuando solo ciertos usuarios pueden enviar un mensaje, pero todas las demás pueden recibir el mensaje.</span><span class="sxs-lookup"><span data-stu-id="70847-140">`[Authorize(RequireOutgoing=false)]` – only authenticated users can invoke the hub, but calls from the server back to clients are not limited by authorization, such as, when only certain users can send a message but all others can receive the message.</span></span> <span data-ttu-id="70847-141">La propiedad RequireOutgoing solo puede aplicarse al concentrador completo, no en los métodos de usuarios en el concentrador.</span><span class="sxs-lookup"><span data-stu-id="70847-141">The RequireOutgoing property can only be applied to the entire hub, not on individuals methods within the hub.</span></span> <span data-ttu-id="70847-142">Cuando RequireOutgoing no está establecido en false, solo los usuarios que cumplan los requisitos de autorización se llaman desde el servidor.</span><span class="sxs-lookup"><span data-stu-id="70847-142">When RequireOutgoing is not set to false, only users that meet the authorization requirement are called from the server.</span></span>

<a id="requireauth"></a>

## <a name="require-authentication-for-all-hubs"></a><span data-ttu-id="70847-143">Requerir autenticación para todos los centros</span><span class="sxs-lookup"><span data-stu-id="70847-143">Require authentication for all hubs</span></span>

<span data-ttu-id="70847-144">Puede requerir la autenticación para todos los concentradores y métodos de concentrador en la aplicación mediante una llamada a la [RequireAuthentication](https://msdn.microsoft.com/en-us/library/microsoft.aspnet.signalr.hubpipelineextensions.requireauthentication(v=vs.111).aspx) método cuando se inicia la aplicación.</span><span class="sxs-lookup"><span data-stu-id="70847-144">You can require authentication for all hubs and hub methods in your application by calling the [RequireAuthentication](https://msdn.microsoft.com/en-us/library/microsoft.aspnet.signalr.hubpipelineextensions.requireauthentication(v=vs.111).aspx) method when the application starts.</span></span> <span data-ttu-id="70847-145">Puede utilizar este método cuando tiene varios concentradores y desea aplicar un requisito de autenticación para todas ellas.</span><span class="sxs-lookup"><span data-stu-id="70847-145">You might use this method when you have multiple hubs and want to enforce an authentication requirement for all of them.</span></span> <span data-ttu-id="70847-146">Con este método, no puede especificar los requisitos de autorización saliente, usuario o rol de.</span><span class="sxs-lookup"><span data-stu-id="70847-146">With this method, you cannot specify requirements for role, user, or outgoing authorization.</span></span> <span data-ttu-id="70847-147">Solo se puede especificar que está restringido a los usuarios autenticados acceso a los métodos de concentrador.</span><span class="sxs-lookup"><span data-stu-id="70847-147">You can only specify that access to the hub methods is restricted to authenticated users.</span></span> <span data-ttu-id="70847-148">Sin embargo, todavía puede aplicar el atributo Authorize a concentradores o métodos para especificar requisitos adicionales.</span><span class="sxs-lookup"><span data-stu-id="70847-148">However, you can still apply the Authorize attribute to hubs or methods to specify additional requirements.</span></span> <span data-ttu-id="70847-149">Cualquier requisito que especifique en un atributo se agrega al requisito de autenticación básico.</span><span class="sxs-lookup"><span data-stu-id="70847-149">Any requirement you specify in an attribute is added to the basic requirement of authentication.</span></span>

<span data-ttu-id="70847-150">En el ejemplo siguiente se muestra un archivo de inicio que restringe todos los métodos de concentrador a los usuarios autenticados.</span><span class="sxs-lookup"><span data-stu-id="70847-150">The following example shows a Startup file which restricts all hub methods to authenticated users.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample3.cs)]

<span data-ttu-id="70847-151">Si se llama a la `RequireAuthentication()` método se ha procesado una solicitud de SignalR, SignalR producirá un `InvalidOperationException` excepción.</span><span class="sxs-lookup"><span data-stu-id="70847-151">If you call the `RequireAuthentication()` method after a SignalR request has been processed, SignalR will throw a `InvalidOperationException` exception.</span></span> <span data-ttu-id="70847-152">SignalR produce esta excepción porque no se puede agregar un módulo a la HubPipeline después de que se ha invocado la canalización.</span><span class="sxs-lookup"><span data-stu-id="70847-152">SignalR throws this exception because you cannot add a module to the HubPipeline after the pipeline has been invoked.</span></span> <span data-ttu-id="70847-153">El ejemplo anterior muestra que realiza la llamada la `RequireAuthentication` método en el `Configuration` método que se ejecuta una vez antes de tratar la primera solicitud.</span><span class="sxs-lookup"><span data-stu-id="70847-153">The previous example shows calling the `RequireAuthentication` method in the `Configuration` method which is executed one time prior to handling the first request.</span></span>

<a id="custom"></a>

## <a name="customized-authorization"></a><span data-ttu-id="70847-154">Autorización personalizada</span><span class="sxs-lookup"><span data-stu-id="70847-154">Customized authorization</span></span>

<span data-ttu-id="70847-155">Si necesita personalizar cómo se determina la autorización, puede crear una clase que deriva de `AuthorizeAttribute` e invalide el [UserAuthorized](https://msdn.microsoft.com/en-us/library/microsoft.aspnet.signalr.authorizeattribute.userauthorized(v=vs.111).aspx) método.</span><span class="sxs-lookup"><span data-stu-id="70847-155">If you need to customize how authorization is determined, you can create a class that derives from `AuthorizeAttribute` and override the [UserAuthorized](https://msdn.microsoft.com/en-us/library/microsoft.aspnet.signalr.authorizeattribute.userauthorized(v=vs.111).aspx) method.</span></span> <span data-ttu-id="70847-156">SignalR para cada solicitud, invoca este método para determinar si el usuario está autorizado para completar la solicitud.</span><span class="sxs-lookup"><span data-stu-id="70847-156">For each request, SignalR invokes this method to determine whether the user is authorized to complete the request.</span></span> <span data-ttu-id="70847-157">En el método invalidado, proporcione la lógica necesaria para su escenario de autorización.</span><span class="sxs-lookup"><span data-stu-id="70847-157">In the overridden method, you provide the necessary logic for your authorization scenario.</span></span> <span data-ttu-id="70847-158">En el ejemplo siguiente se muestra cómo aplicar la autorización a través de la identidad basada en notificaciones.</span><span class="sxs-lookup"><span data-stu-id="70847-158">The following example shows how to enforce authorization through claims-based identity.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample4.cs)]

<a id="passauth"></a>

## <a name="pass-authentication-information-to-clients"></a><span data-ttu-id="70847-159">Pasar información de autenticación a los clientes</span><span class="sxs-lookup"><span data-stu-id="70847-159">Pass authentication information to clients</span></span>

<span data-ttu-id="70847-160">Debe usar la información de autenticación en el código que se ejecuta en el cliente.</span><span class="sxs-lookup"><span data-stu-id="70847-160">You may need to use authentication information in the code that runs on the client.</span></span> <span data-ttu-id="70847-161">Pasar la información necesaria al llamar a los métodos en el cliente.</span><span class="sxs-lookup"><span data-stu-id="70847-161">You pass the required information when calling the methods on the client.</span></span> <span data-ttu-id="70847-162">Por ejemplo, un método de aplicación de chat podría pasar como parámetro el nombre de usuario de la persona que publica un mensaje, tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="70847-162">For example, a chat application method could pass as a parameter the user name of the person posting a message, as shown below.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample5.cs)]

<span data-ttu-id="70847-163">O bien, puede crear un objeto para representar la información de autenticación y pasar ese objeto como un parámetro, tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="70847-163">Or, you can create an object to represent the authentication information and pass that object as a parameter, as shown below.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample6.cs)]

<span data-ttu-id="70847-164">No debe pasar nunca Id. de conexión de un cliente a otros clientes, cuando un usuario malintencionado podría utilizarlo para imitar una solicitud de ese cliente.</span><span class="sxs-lookup"><span data-stu-id="70847-164">You should never pass one client's connection id to other clients, as a malicious user could use it to mimic a request from that client.</span></span>

<a id="authoptions"></a>

## <a name="authentication-options-for-net-clients"></a><span data-ttu-id="70847-165">Opciones de autenticación para los clientes de .NET</span><span class="sxs-lookup"><span data-stu-id="70847-165">Authentication options for .NET clients</span></span>

<span data-ttu-id="70847-166">Si tiene un cliente. NET, como una aplicación de consola que interactúa con un concentrador que está limitado a los usuarios autenticados, puede pasar las credenciales de autenticación en una cookie, el encabezado de conexión o un certificado.</span><span class="sxs-lookup"><span data-stu-id="70847-166">When you have a .NET client, such as a console app, which interacts with a hub that is limited to authenticated users, you can pass the authentication credentials in a cookie, the connection header, or a certificate.</span></span> <span data-ttu-id="70847-167">Los ejemplos de esta sección muestran cómo utilizar los distintos métodos para autenticar a un usuario.</span><span class="sxs-lookup"><span data-stu-id="70847-167">The examples in this section show how to use those different methods for authenticating a user.</span></span> <span data-ttu-id="70847-168">No son totalmente funcionales aplicaciones SignalR.</span><span class="sxs-lookup"><span data-stu-id="70847-168">They are not fully-functional SignalR apps.</span></span> <span data-ttu-id="70847-169">Para obtener más información acerca de los clientes de .NET con SignalR, consulte [Guía de la API de concentradores - cliente .NET](../guide-to-the-api/hubs-api-guide-net-client.md).</span><span class="sxs-lookup"><span data-stu-id="70847-169">For more information about .NET clients with SignalR, see [Hubs API Guide - .NET Client](../guide-to-the-api/hubs-api-guide-net-client.md).</span></span>

<a id="cookie"></a>

### <a name="cookie"></a><span data-ttu-id="70847-170">Cookie</span><span class="sxs-lookup"><span data-stu-id="70847-170">Cookie</span></span>

<span data-ttu-id="70847-171">Cuando el cliente .NET interactúa con un concentrador que utiliza la autenticación de formularios de ASP.NET, debe establecer manualmente la cookie de autenticación en la conexión.</span><span class="sxs-lookup"><span data-stu-id="70847-171">When your .NET client interacts with a hub that uses ASP.NET Forms Authentication, you will need to manually set the authentication cookie on the connection.</span></span> <span data-ttu-id="70847-172">Agregue la cookie a la `CookieContainer` propiedad en el [HubConnection](https://msdn.microsoft.com/en-us/library/microsoft.aspnet.signalr.client.hubs.hubconnection(v=vs.111).aspx) objeto.</span><span class="sxs-lookup"><span data-stu-id="70847-172">You add the cookie to the `CookieContainer` property on the [HubConnection](https://msdn.microsoft.com/en-us/library/microsoft.aspnet.signalr.client.hubs.hubconnection(v=vs.111).aspx) object.</span></span> <span data-ttu-id="70847-173">En el ejemplo siguiente se muestra una aplicación de consola que recupera una cookie de autenticación desde una página web y agrega dicha cookie para la conexión.</span><span class="sxs-lookup"><span data-stu-id="70847-173">The following example shows a console app that retrieves an authentication cookie from a web page and adds that cookie to the connection.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample7.cs)]

<span data-ttu-id="70847-174">La aplicación de consola envía las credenciales para **www.contoso.com/RemoteLogin** que podría hacer referencia a una página vacía que contiene el siguiente archivo de código subyacente.</span><span class="sxs-lookup"><span data-stu-id="70847-174">The console app posts the credentials to **www.contoso.com/RemoteLogin** which could refer to an empty page that contains the following code-behind file.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample8.cs)]

<a id="windows"></a>

### <a name="windows-authentication"></a><span data-ttu-id="70847-175">Autenticación de Windows</span><span class="sxs-lookup"><span data-stu-id="70847-175">Windows authentication</span></span>

<span data-ttu-id="70847-176">Al utilizar la autenticación de Windows, puede pasar las credenciales del usuario actual mediante el [DefaultCredentials](https://msdn.microsoft.com/en-us/library/system.net.credentialcache.defaultcredentials.aspx) propiedad.</span><span class="sxs-lookup"><span data-stu-id="70847-176">When using Windows authentication, you can pass the current user's credentials by using the [DefaultCredentials](https://msdn.microsoft.com/en-us/library/system.net.credentialcache.defaultcredentials.aspx) property.</span></span> <span data-ttu-id="70847-177">Establezca las credenciales para la conexión con el valor de la DefaultCredentials.</span><span class="sxs-lookup"><span data-stu-id="70847-177">You set the credentials for the connection to the value of the DefaultCredentials.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample9.cs?highlight=6)]

<a id="header"></a>

### <a name="connection-header"></a><span data-ttu-id="70847-178">Encabezado de conexión</span><span class="sxs-lookup"><span data-stu-id="70847-178">Connection header</span></span>

<span data-ttu-id="70847-179">Si la aplicación no utiliza cookies, puede pasar información de usuario en el encabezado de conexión.</span><span class="sxs-lookup"><span data-stu-id="70847-179">If your application is not using cookies, you can pass user information in the connection header.</span></span> <span data-ttu-id="70847-180">Por ejemplo, puede pasar un token en el encabezado de conexión.</span><span class="sxs-lookup"><span data-stu-id="70847-180">For example, you can pass a token in the connection header.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample10.cs?highlight=6)]

<span data-ttu-id="70847-181">A continuación, en el concentrador, debe comprobar el token del usuario.</span><span class="sxs-lookup"><span data-stu-id="70847-181">Then, in the hub, you would verify the user's token.</span></span>

<a id="certificate"></a>

### <a name="certificate"></a><span data-ttu-id="70847-182">Certificado</span><span class="sxs-lookup"><span data-stu-id="70847-182">Certificate</span></span>

<span data-ttu-id="70847-183">Puede pasar un certificado de cliente para comprobar que el usuario.</span><span class="sxs-lookup"><span data-stu-id="70847-183">You can pass a client certificate to verify the user.</span></span> <span data-ttu-id="70847-184">Agregar el certificado al crear la conexión.</span><span class="sxs-lookup"><span data-stu-id="70847-184">You add the certificate when creating the connection.</span></span> <span data-ttu-id="70847-185">En el ejemplo siguiente se muestra solamente cómo agregar un certificado de cliente para la conexión; no se muestra la aplicación de consola completa.</span><span class="sxs-lookup"><span data-stu-id="70847-185">The following example shows only how to add a client certificate to the connection; it does not show the full console app.</span></span> <span data-ttu-id="70847-186">Usa el [X509Certificate](https://msdn.microsoft.com/en-us/library/system.security.cryptography.x509certificates.x509certificate.aspx) clase que proporciona varias formas de crear el certificado.</span><span class="sxs-lookup"><span data-stu-id="70847-186">It uses the [X509Certificate](https://msdn.microsoft.com/en-us/library/system.security.cryptography.x509certificates.x509certificate.aspx) class which provides several different ways to create the certificate.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample11.cs?highlight=6)]