---
title: een Web-API-back-end met Azure Active Directory en API Management aaaProtect | Microsoft Docs
description: Meer informatie over hoe tooprotect een Web-API-back-end met Azure Active Directory en API Management.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: f856ff03-64a1-4548-9ec4-c0ec4cc1600f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: f4b323034354aa09579c643bade47257fbf1e5c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooprotect-a-web-api-backend-with-azure-active-directory-and-api-management"></a><span data-ttu-id="15da7-103">Hoe tooprotect een Web-API-back-end met Azure Active Directory en API Management</span><span class="sxs-lookup"><span data-stu-id="15da7-103">How tooprotect a Web API backend with Azure Active Directory and API Management</span></span>
<span data-ttu-id="15da7-104">Hallo volgende video toont hoe toobuild een Web-API-back-end en beveiligen met behulp van OAuth 2.0-protocol met Azure Active Directory en API Management.</span><span class="sxs-lookup"><span data-stu-id="15da7-104">hello following video shows how toobuild a Web API backend and protect it using OAuth 2.0 protocol with Azure Active Directory and API Management.</span></span>  <span data-ttu-id="15da7-105">In dit artikel biedt een overzicht en aanvullende informatie voor Hallo stappen in Hallo video.</span><span class="sxs-lookup"><span data-stu-id="15da7-105">This article provides an overview and additional information for hello steps in hello video.</span></span> <span data-ttu-id="15da7-106">Deze 24 minuut video ziet u hoe aan:</span><span class="sxs-lookup"><span data-stu-id="15da7-106">This 24 minute video shows you how to:</span></span>

* <span data-ttu-id="15da7-107">Een Web-API-back-end bouwen en beveilig deze met AAD - begint bij 1:30</span><span class="sxs-lookup"><span data-stu-id="15da7-107">Build a Web API backend and secure it with AAD - starting at 1:30</span></span>
* <span data-ttu-id="15da7-108">Hallo-API in API Management - 7:10 vanaf importeren</span><span class="sxs-lookup"><span data-stu-id="15da7-108">Import hello API into API Management - starting at 7:10</span></span>
* <span data-ttu-id="15da7-109">Hallo Developer portal toocall Hallo API - vanaf 9:09 configureren</span><span class="sxs-lookup"><span data-stu-id="15da7-109">Configure hello Developer portal toocall hello API - starting at 9:09</span></span>
* <span data-ttu-id="15da7-110">Een bureaubladtoepassing toocall Hallo API - vanaf 18:08 configureren</span><span class="sxs-lookup"><span data-stu-id="15da7-110">Configure a desktop application toocall hello API - starting at 18:08</span></span>
* <span data-ttu-id="15da7-111">Configureren van een JWT validatie beleid toopre-aanvragen - vanaf 20:47 autoriseren</span><span class="sxs-lookup"><span data-stu-id="15da7-111">Configure a JWT validation policy toopre-authorize requests - starting at 20:47</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Protecting-Web-API-Backend-with-Azure-Active-Directory-and-API-Management/player]
> 
> 

## <a name="create-an-azure-ad-directory"></a><span data-ttu-id="15da7-112">Een Azure AD-directory maken</span><span class="sxs-lookup"><span data-stu-id="15da7-112">Create an Azure AD directory</span></span>
<span data-ttu-id="15da7-113">toosecure uw Web-API-back met Azure Active Directory moet u eerst hebben een AAD-tenant.</span><span class="sxs-lookup"><span data-stu-id="15da7-113">toosecure your Web API backed using Azure Active Directory you must first have a an AAD tenant.</span></span> <span data-ttu-id="15da7-114">In deze video met de naam van een tenant **APIMDemo** wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="15da7-114">In this video a tenant named **APIMDemo** is used.</span></span> <span data-ttu-id="15da7-115">toocreate een AAD-tenant aanmelden toohello [klassieke Azure-Portal](https://manage.windowsazure.com) en klik op **nieuw**->**App Services**->**Active Directory**->**Directory**->**aangepast maken**.</span><span class="sxs-lookup"><span data-stu-id="15da7-115">toocreate an AAD tenant, sign-in toohello [Azure Classic Portal](https://manage.windowsazure.com) and click **New**->**App Services**->**Active Directory**->**Directory**->**Custom Create**.</span></span> 

![Azure Active Directory][api-management-create-aad-menu]

<span data-ttu-id="15da7-117">In dit voorbeeld van een map met de naam **APIMDemo** wordt gemaakt met een standaarddomein met de naam **DemoAPIM.onmicrosoft.com**. Deze map wordt gebruikt in de gehele Hallo video.</span><span class="sxs-lookup"><span data-stu-id="15da7-117">In this example a directory named **APIMDemo** is created with a default domain named **DemoAPIM.onmicrosoft.com**. This directory is used throughout hello video.</span></span>

![Azure Active Directory][api-management-create-aad]

## <a name="create-a-web-api-service-secured-by-azure-active-directory"></a><span data-ttu-id="15da7-119">Een Web-API-service worden beveiligd door Azure Active Directory maken</span><span class="sxs-lookup"><span data-stu-id="15da7-119">Create a Web API service secured by Azure Active Directory</span></span>
<span data-ttu-id="15da7-120">In deze stap wordt een Web-API-back-end gemaakt met behulp van Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="15da7-120">In this step, a Web API backend is created using Visual Studio 2013.</span></span> <span data-ttu-id="15da7-121">In deze stap van de video Hallo begint bij 1:30.</span><span class="sxs-lookup"><span data-stu-id="15da7-121">This step of hello video starts at 1:30.</span></span> <span data-ttu-id="15da7-122">toocreate Web API-back-end-project in Visual Studio klikt u op **bestand**->**nieuw**->**Project**, en kies **ASP.NET-webtoepassing Toepassing** van Hallo **Web** lijst met sjablonen.</span><span class="sxs-lookup"><span data-stu-id="15da7-122">toocreate Web API backend project in Visual Studio click **File**->**New**->**Project**, and choose **ASP.NET Web Application** from hello **Web** templates list.</span></span> <span data-ttu-id="15da7-123">In deze video Hallo project de naam **APIMAADDemo**.</span><span class="sxs-lookup"><span data-stu-id="15da7-123">In this video hello project is named **APIMAADDemo**.</span></span> <span data-ttu-id="15da7-124">Klik op **OK** toocreate Hallo project.</span><span class="sxs-lookup"><span data-stu-id="15da7-124">Click **OK** toocreate hello project.</span></span> 

![Visual Studio][api-management-new-web-app]

<span data-ttu-id="15da7-126">Klik op **Web API** van Hallo **selecteert u een lijst met sjablonen** toocreate een Web API-project.</span><span class="sxs-lookup"><span data-stu-id="15da7-126">Click **Web API** from hello **Select a template list** toocreate a Web API project.</span></span> <span data-ttu-id="15da7-127">Azure Directory Authentication tooconfigure klikt u op **verificatie wijzigen**.</span><span class="sxs-lookup"><span data-stu-id="15da7-127">tooconfigure Azure Directory Authentication click **Change Authentication**.</span></span>

![Nieuw project][api-management-new-project]

<span data-ttu-id="15da7-129">Klik op **Organisatieaccounts**, en geef Hallo **domein** van uw AAD-tenant.</span><span class="sxs-lookup"><span data-stu-id="15da7-129">Click **Organizational Accounts**, and specify hello **Domain** of your AAD tenant.</span></span> <span data-ttu-id="15da7-130">In dit voorbeeld Hallo domein is **DemoAPIM.onmicrosoft.com**. Hallo domein van uw directory kan worden verkregen van Hallo **domeinen** tabblad van uw directory.</span><span class="sxs-lookup"><span data-stu-id="15da7-130">In this example hello domain is **DemoAPIM.onmicrosoft.com**. hello domain of your directory can be obtained from hello **Domains** tab of your directory.</span></span>

![Domeinen][api-management-aad-domains]

<span data-ttu-id="15da7-132">Hallo gewenst instellingen configureren in Hallo **verificatie wijzigen** dialoogvenster en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="15da7-132">Configure hello desired settings in hello **Change Authentication** dialog box and click **OK**.</span></span>

![Verificatie wijzigen][api-management-change-authentication]

<span data-ttu-id="15da7-134">Wanneer u klikt op **OK** Visual Studio probeert tooregister uw toepassing met uw Azure AD-directory en hebt u mogelijk na vragen aan gebruiker toosign in door Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="15da7-134">When you click **OK** Visual Studio will attempt tooregister your application with your Azure AD directory and you may be prompted toosign in by Visual Studio.</span></span> <span data-ttu-id="15da7-135">Meld u aan met een Administrator-account voor uw directory.</span><span class="sxs-lookup"><span data-stu-id="15da7-135">Sign in using an administrative account for your directory.</span></span>

![Meld u aan tooVisual Studio][api-management-sign-in-vidual-studio]

<span data-ttu-id="15da7-137">tooconfigure dit project als een Azure-Web-API selectievakje Hallo vak voor **hosten in de cloud Hallo** en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="15da7-137">tooconfigure this project as an Azure Web API check hello box for **Host in hello cloud** and then click **OK**.</span></span>

![Nieuw project][api-management-new-project-cloud]

<span data-ttu-id="15da7-139">Hebt u mogelijk na vragen aan gebruiker toosign in tooAzure en vervolgens kunt u Hallo Web-App configureren.</span><span class="sxs-lookup"><span data-stu-id="15da7-139">You may be prompted toosign in tooAzure, and then you can configure hello Web App.</span></span>

![Configureren][api-management-configure-web-app]

<span data-ttu-id="15da7-141">In dit voorbeeld is een nieuwe **App Service-abonnement** met de naam **APIMAADDemo** is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="15da7-141">In this example a new **App Service plan** named **APIMAADDemo** is specified.</span></span>

<span data-ttu-id="15da7-142">Klik op **OK** tooconfigure Hallo Web-App en Hallo-project maken.</span><span class="sxs-lookup"><span data-stu-id="15da7-142">Click **OK** tooconfigure hello Web App and create hello project.</span></span>

## <a name="add-hello-code-toohello-web-api-project"></a><span data-ttu-id="15da7-143">Hallo code toohello Web API-project toevoegen</span><span class="sxs-lookup"><span data-stu-id="15da7-143">Add hello code toohello Web API project</span></span>
<span data-ttu-id="15da7-144">de volgende stap Hallo in Hallo video wordt toegevoegd Hallo code toohello Web API-project.</span><span class="sxs-lookup"><span data-stu-id="15da7-144">hello next step in hello video adds hello code toohello Web API project.</span></span> <span data-ttu-id="15da7-145">Deze stap 4:35 wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="15da7-145">This step starts at 4:35.</span></span>

<span data-ttu-id="15da7-146">Hallo-Web-API in dit voorbeeld implementeert een basisrekenmachine-service met behulp van een model en een domeincontroller.</span><span class="sxs-lookup"><span data-stu-id="15da7-146">hello Web API in this example implements a basic calculator service using a model and a controller.</span></span> <span data-ttu-id="15da7-147">tooadd hello model voor Hallo-service met de rechtermuisknop op **modellen** in **Solution Explorer** en kies **toevoegen**, **klasse**.</span><span class="sxs-lookup"><span data-stu-id="15da7-147">tooadd hello model for hello service, right-click **Models** in **Solution Explorer** and choose **Add**, **Class**.</span></span> <span data-ttu-id="15da7-148">Naam Hallo klasse `CalcInput` en klik op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="15da7-148">Name hello class `CalcInput` and click **Add**.</span></span>

<span data-ttu-id="15da7-149">Voeg de volgende Hallo `using` instructie toohello bovenaan Hallo `CalcInput.cs` bestand.</span><span class="sxs-lookup"><span data-stu-id="15da7-149">Add hello following `using` statement toohello top of hello `CalcInput.cs` file.</span></span>

```c#
using Newtonsoft.Json;
```

<span data-ttu-id="15da7-150">Hallo gegenereerd klasse vervangen door Hallo code te volgen.</span><span class="sxs-lookup"><span data-stu-id="15da7-150">Replace hello generated class with hello following code.</span></span>

```c#
public class CalcInput
{
    [JsonProperty(PropertyName = "a")]
    public int a;

    [JsonProperty(PropertyName = "b")]
    public int b;
}
```

<span data-ttu-id="15da7-151">Met de rechtermuisknop op **domeincontrollers** in **Solution Explorer** en kies **toevoegen**->**Controller**.</span><span class="sxs-lookup"><span data-stu-id="15da7-151">Right-click **Controllers** in **Solution Explorer** and choose **Add**->**Controller**.</span></span> <span data-ttu-id="15da7-152">Kies **Web API 2-Controller - leeg** en klik op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="15da7-152">Choose **Web API 2 Controller - Empty** and click **Add**.</span></span> <span data-ttu-id="15da7-153">Type **CalcController** voor Hallo Controller naam en klik op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="15da7-153">Type **CalcController** for hello Controller name and click **Add**.</span></span>

![Controller toevoegen][api-management-add-controller]

<span data-ttu-id="15da7-155">Voeg de volgende Hallo `using` instructie toohello bovenaan Hallo `CalcController.cs` bestand.</span><span class="sxs-lookup"><span data-stu-id="15da7-155">Add hello following `using` statement toohello top of hello `CalcController.cs` file.</span></span>

```c#
using System.IO;
using System.Web;
using APIMAADDemo.Models;
```

<span data-ttu-id="15da7-156">Hallo gegenereerd controllerklasse vervangen door Hallo code te volgen.</span><span class="sxs-lookup"><span data-stu-id="15da7-156">Replace hello generated controller class with hello following code.</span></span> <span data-ttu-id="15da7-157">Deze code implementeert Hallo `Add`, `Subtract`, `Multiply`, en `Divide` operations Hallo basisrekenmachine-API.</span><span class="sxs-lookup"><span data-stu-id="15da7-157">This code implements hello `Add`, `Subtract`, `Multiply`, and `Divide` operations of hello Basic Calculator API.</span></span>

```c#
[Authorize]
public class CalcController : ApiController
{
    [Route("api/add")]
    [HttpGet]
    public HttpResponseMessage GetSum([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a + b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }

    [Route("api/sub")]
    [HttpGet]
    public HttpResponseMessage GetDiff([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a - b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }

    [Route("api/mul")]
    [HttpGet]
    public HttpResponseMessage GetProduct([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a * b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }

    [Route("api/div")]
    [HttpGet]
    public HttpResponseMessage GetDiv([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a / b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }
}
```

<span data-ttu-id="15da7-158">Druk op **F6** toobuild en controleer of Hallo-oplossing.</span><span class="sxs-lookup"><span data-stu-id="15da7-158">Press **F6** toobuild and verify hello solution.</span></span>

## <a name="publish-hello-project-tooazure"></a><span data-ttu-id="15da7-159">Hallo project tooAzure publiceren</span><span class="sxs-lookup"><span data-stu-id="15da7-159">Publish hello project tooAzure</span></span>
<span data-ttu-id="15da7-160">In deze stap Hallo Visual Studio is-project gepubliceerde tooAzure.</span><span class="sxs-lookup"><span data-stu-id="15da7-160">In this step hello Visual Studio project is published tooAzure.</span></span> <span data-ttu-id="15da7-161">In deze stap van de video Hallo begint bij 5:45.</span><span class="sxs-lookup"><span data-stu-id="15da7-161">This step of hello video starts at 5:45.</span></span>

<span data-ttu-id="15da7-162">toopublish Hallo project tooAzure, met de rechtermuisknop op Hallo **APIMAADDemo** in Visual Studio-project en kies **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="15da7-162">toopublish hello project tooAzure, right-click hello **APIMAADDemo** project in Visual Studio and choose **Publish**.</span></span> <span data-ttu-id="15da7-163">Hallo-standaardinstellingen behouden in Hallo **webpublicatie** dialoogvenster en klik op **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="15da7-163">Keep hello default settings in hello **Publish Web** dialog box and click **Publish**.</span></span>

![Web publiceren][api-management-web-publish]

## <a name="grant-permissions-toohello-azure-ad-backend-service-application"></a><span data-ttu-id="15da7-165">Machtigingen toekennen toohello Azure AD-back-end-servicetoepassing</span><span class="sxs-lookup"><span data-stu-id="15da7-165">Grant permissions toohello Azure AD backend service application</span></span>
<span data-ttu-id="15da7-166">Een nieuwe aanvraag om de back-endservice hello wordt gemaakt in uw Azure AD-directory als onderdeel van het Hallo configureren en publicatieproces van uw Web-API-project.</span><span class="sxs-lookup"><span data-stu-id="15da7-166">A new application for hello backend service is created in your Azure AD directory as part of hello configuring and publishing process of your Web API project.</span></span> <span data-ttu-id="15da7-167">In deze stap van de video hello, worden beginnend bij 6:13 machtigingen verleend toohello Web API-back-end.</span><span class="sxs-lookup"><span data-stu-id="15da7-167">In this step of hello video, starting at 6:13, permissions are granted toohello Web API backend.</span></span>

![Toepassing][api-management-aad-backend-app]

<span data-ttu-id="15da7-169">Klik op de naam Hallo Hallo toepassing tooconfigure Hallo vereist machtigingen.</span><span class="sxs-lookup"><span data-stu-id="15da7-169">Click hello name of hello application tooconfigure hello required permissions.</span></span> <span data-ttu-id="15da7-170">Navigeer toohello **configureren** tabblad en schuif omlaag toohello **machtigingen tooother toepassingen** sectie.</span><span class="sxs-lookup"><span data-stu-id="15da7-170">Navigate toohello **Configure** tab and scroll down toohello **permissions tooother applications** section.</span></span> <span data-ttu-id="15da7-171">Klik op Hallo **Toepassingsmachtigingen** -omlaag naast **Windows** **Azure Active Directory**, Hallo selectievakje voor **mapgegevenslezen**, en klik op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="15da7-171">Click hello **Application Permissions** drop-down beside **Windows** **Azure Active Directory**, check hello box for **Read directory data**, and click **Save**.</span></span>

![Machtigingen toevoegen][api-management-aad-add-permissions]

> [!NOTE]
> <span data-ttu-id="15da7-173">Als **Windows** **Azure Active Directory** is niet wordt vermeld onder machtigingen tooother toepassingen, klikt u op **toepassing toevoegen** en toe te voegen in de lijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="15da7-173">If **Windows** **Azure Active Directory** is not listed under permissions tooother applications, click **Add application** and add it from hello list.</span></span>
> 
> 

<span data-ttu-id="15da7-174">Maak een notitie van Hallo **App Id URI** voor gebruik in een latere stap wanneer een Azure AD-toepassing is geconfigureerd voor Hallo API Management-portal voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="15da7-174">Make a note of hello **App Id URI** for use in a subsequent step when an Azure AD application is configured for hello API Management developer portal.</span></span>

![App Id URI][api-management-aad-sso-uri]

## <a name="import-hello-web-api-into-api-management"></a><span data-ttu-id="15da7-176">Hallo-Web-API importeren in API Management</span><span class="sxs-lookup"><span data-stu-id="15da7-176">Import hello Web API into API Management</span></span>
<span data-ttu-id="15da7-177">API's zijn geconfigureerd met Hallo API-publicatieportal, die wordt geopend via hello Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="15da7-177">APIs are configured from hello API publisher portal, which is accessed through hello Azure Portal.</span></span> <span data-ttu-id="15da7-178">tooreach, klikt u op **publicatieportal** van Hallo werkbalk van uw API Management-service.</span><span class="sxs-lookup"><span data-stu-id="15da7-178">tooreach it, click **Publisher portal** from hello toolbar of your API Management service.</span></span> <span data-ttu-id="15da7-179">Als u nog geen exemplaar van API Management-service hebt gemaakt, raadpleegt u [API Management service-exemplaar maken] [ Create an API Management service instance] in Hallo [uw eerste API beheren] [ Manage your first API] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="15da7-179">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Manage your first API][Manage your first API] tutorial.</span></span>

![Publicatieportal][api-management-management-console]

<span data-ttu-id="15da7-181">Bewerkingen kunnen worden [tooAPIs handmatig toegevoegd](api-management-howto-add-operations.md), of ze kunnen worden geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="15da7-181">Operations can be [added tooAPIs manually](api-management-howto-add-operations.md), or they can be imported.</span></span> <span data-ttu-id="15da7-182">In deze video worden bewerkingen in Swagger-indeling vanaf 6:40 geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="15da7-182">In this video, operations are imported in Swagger format starting at 6:40.</span></span>

<span data-ttu-id="15da7-183">Maak een bestand met de naam `calcapi.json` met de volgende inhoud en sla het tooyour computer.</span><span class="sxs-lookup"><span data-stu-id="15da7-183">Create a file named `calcapi.json` with following contents and save it tooyour computer.</span></span> <span data-ttu-id="15da7-184">Zorg ervoor dat Hallo `host` kenmerk verwijst tooyour Web API-back-end.</span><span class="sxs-lookup"><span data-stu-id="15da7-184">Ensure that hello `host` attribute points tooyour Web API backend.</span></span> <span data-ttu-id="15da7-185">In dit voorbeeld `"host": "apimaaddemo.azurewebsites.net"` wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="15da7-185">In this example `"host": "apimaaddemo.azurewebsites.net"` is used.</span></span>

```json
{
  "swagger": "2.0",
  "info": {
    "title": "Calculator",
    "description": "Arithmetics over HTTP!",
    "version": "1.0"
  },
  "host": "apimaaddemo.azurewebsites.net",
  "basePath": "/api",
  "schemes": [
    "http"
  ],
  "paths": {
    "/add?a={a}&b={b}": {
      "get": {
        "description": "Responds with a sum of two numbers.",
        "operationId": "Add two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>51</code>.",
            "required": true,
            "type": "string",
            "default": "51",
            "enum": [
              "51"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>49</code>.",
            "required": true,
            "type": "string",
            "default": "49",
            "enum": [
              "49"
            ]
          }
        ],
        "responses": { }
      }
    },
    "/sub?a={a}&b={b}": {
      "get": {
        "description": "Responds with a difference between two numbers.",
        "operationId": "Subtract two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>100</code>.",
            "required": true,
            "type": "string",
            "default": "100",
            "enum": [
              "100"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>50</code>.",
            "required": true,
            "type": "string",
            "default": "50",
            "enum": [
              "50"
            ]
          }
        ],
        "responses": { }
      }
    },
    "/div?a={a}&b={b}": {
      "get": {
        "description": "Responds with a quotient of two numbers.",
        "operationId": "Divide two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>100</code>.",
            "required": true,
            "type": "string",
            "default": "100",
            "enum": [
              "100"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>20</code>.",
            "required": true,
            "type": "string",
            "default": "20",
            "enum": [
              "20"
            ]
          }
        ],
        "responses": { }
      }
    },
    "/mul?a={a}&b={b}": {
      "get": {
        "description": "Responds with a product of two numbers.",
        "operationId": "Multiply two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>20</code>.",
            "required": true,
            "type": "string",
            "default": "20",
            "enum": [
              "20"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>5</code>.",
            "required": true,
            "type": "string",
            "default": "5",
            "enum": [
              "5"
            ]
          }
        ],
        "responses": { }
      }
    }
  }
}
```

<span data-ttu-id="15da7-186">tooimport hello Rekenmachine-API, klikt u op **API's** van Hallo **API Management** menu op Hallo links en klik vervolgens op **Import API**.</span><span class="sxs-lookup"><span data-stu-id="15da7-186">tooimport hello calculator API, click **APIs** from hello **API Management** menu on hello left, and then click **Import API**.</span></span>

![Knop API importeren][api-management-import-api]

<span data-ttu-id="15da7-188">Volgende stappen tooconfigure hello basisrekenmachine-API Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="15da7-188">Perform hello following steps tooconfigure hello calculator API.</span></span>

1. <span data-ttu-id="15da7-189">Klik op **uit bestand**, bladeren toohello `calculator.json` bestand dat u opgeslagen en klik op Hallo **Swagger** keuzerondje.</span><span class="sxs-lookup"><span data-stu-id="15da7-189">Click **From file**, browse toohello `calculator.json` file you saved, and click hello **Swagger** radio button.</span></span>
2. <span data-ttu-id="15da7-190">Type **calc** in Hallo **achtervoegsel URL Web-API** textbox.</span><span class="sxs-lookup"><span data-stu-id="15da7-190">Type **calc** into hello **Web API URL suffix** textbox.</span></span>
3. <span data-ttu-id="15da7-191">Klik in het Hallo **producten (optioneel)** vak en kies **Starter**.</span><span class="sxs-lookup"><span data-stu-id="15da7-191">Click in hello **Products (optional)** box and choose **Starter**.</span></span>
4. <span data-ttu-id="15da7-192">Klik op **opslaan** tooimport Hallo API.</span><span class="sxs-lookup"><span data-stu-id="15da7-192">Click **Save** tooimport hello API.</span></span>

![Nieuwe API toevoegen][api-management-import-new-api]

<span data-ttu-id="15da7-194">Zodra het Hallo-API is geïmporteerd, wordt hello overzichtspagina voor Hallo API weergegeven in de publicatieportal Hallo.</span><span class="sxs-lookup"><span data-stu-id="15da7-194">Once hello API is imported, hello summary page for hello API is displayed in hello publisher portal.</span></span>

## <a name="call-hello-api-unsuccessfully-from-hello-developer-portal"></a><span data-ttu-id="15da7-195">Succes Hallo-API aanroepen vanuit de ontwikkelaarsportal Hallo</span><span class="sxs-lookup"><span data-stu-id="15da7-195">Call hello API unsuccessfully from hello developer portal</span></span>
<span data-ttu-id="15da7-196">Op dit moment Hallo API is geïmporteerd in API Management, maar kan nog worden aangeroepen met succes vanuit de ontwikkelaarsportal Hallo omdat Hallo back-endservice is beveiligd met Azure AD-verificatie.</span><span class="sxs-lookup"><span data-stu-id="15da7-196">At this point, hello API has been imported into API Management, but cannot yet be called successfully from hello developer portal because hello backend service is protected with Azure AD authentication.</span></span> <span data-ttu-id="15da7-197">Dit wordt geïllustreerd in Hallo video vanaf 7:40 met Hallo stappen te volgen.</span><span class="sxs-lookup"><span data-stu-id="15da7-197">This is demonstrated in hello video starting at 7:40 using hello following steps.</span></span>

<span data-ttu-id="15da7-198">Klik op **ontwikkelaarsportal** van Hallo rechtsboven kant van de publicatieportal Hallo.</span><span class="sxs-lookup"><span data-stu-id="15da7-198">Click **Developer portal** from hello top-right side of hello publisher portal.</span></span>

![ontwikkelaarsportal][api-management-developer-portal-menu]

<span data-ttu-id="15da7-200">Klik op **API's** en klik op Hallo **Rekenmachine** API.</span><span class="sxs-lookup"><span data-stu-id="15da7-200">Click **APIs** and click hello **Calculator** API.</span></span>

![ontwikkelaarsportal][api-management-dev-portal-apis]

<span data-ttu-id="15da7-202">Klik op **Try it**.</span><span class="sxs-lookup"><span data-stu-id="15da7-202">Click **Try it**.</span></span>

![Probeer het nu][api-management-dev-portal-try-it]

<span data-ttu-id="15da7-204">Klik op **verzenden** en noteer de antwoordstatus Hallo van **401 niet geautoriseerd**.</span><span class="sxs-lookup"><span data-stu-id="15da7-204">Click **Send** and note hello response status of **401 Unauthorized**.</span></span>

![Verzenden][api-management-dev-portal-send-401]

<span data-ttu-id="15da7-206">Hallo-aanvraag is niet geautoriseerd omdat Hallo-end-API is beveiligd door Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="15da7-206">hello request is unauthorized because hello backend API is protected by Azure Active Directory.</span></span> <span data-ttu-id="15da7-207">Hallo-portal voor ontwikkelaars moet geconfigureerde tooauthorize ontwikkelaars met behulp van OAuth 2.0, voordat het Hallo-API op correcte wijze aanroept.</span><span class="sxs-lookup"><span data-stu-id="15da7-207">Before successfully calling hello API hello developer portal must be configured tooauthorize developers using OAuth 2.0.</span></span> <span data-ttu-id="15da7-208">Dit proces wordt beschreven in Hallo uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="15da7-208">This process is described in hello following sections.</span></span>

## <a name="register-hello-developer-portal-as-an-aad-application"></a><span data-ttu-id="15da7-209">Hallo-portal voor ontwikkelaars registreren als een AAD-toepassing</span><span class="sxs-lookup"><span data-stu-id="15da7-209">Register hello developer portal as an AAD application</span></span>
<span data-ttu-id="15da7-210">eerste stap bij het configureren van Hallo developer portal tooauthorize ontwikkelaars met behulp van OAuth 2.0 Hallo is tooregister Hallo developer-portal als een AAD-toepassing.</span><span class="sxs-lookup"><span data-stu-id="15da7-210">hello first step in configuring hello developer portal tooauthorize developers using OAuth 2.0 is tooregister hello developer portal as an AAD application.</span></span> <span data-ttu-id="15da7-211">Dit wordt geïllustreerd vanaf 8:27 in Hallo video.</span><span class="sxs-lookup"><span data-stu-id="15da7-211">This is demonstrated starting at 8:27 in hello video.</span></span>

<span data-ttu-id="15da7-212">Navigeer toohello Azure AD-tenant van de eerste stap Hallo van deze video in dit voorbeeld **APIMDemo** en navigeer toohello **toepassingen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="15da7-212">Navigate toohello Azure AD tenant from hello first step of this video, in this example **APIMDemo** and navigate toohello **Applications** tab.</span></span>

![nieuwe toepassing][api-management-aad-new-application-devportal]

<span data-ttu-id="15da7-214">Klik op Hallo **toevoegen** knop toocreate een nieuwe Azure Active Directory-toepassing, en kies **mijn organisatie ontwikkelt toepassing toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="15da7-214">Click hello **Add** button toocreate a new Azure Active Directory application, and choose **Add an application my organization is developing**.</span></span>

![nieuwe toepassing][api-management-new-aad-application-menu]

<span data-ttu-id="15da7-216">Kies **Web-toepassing en/of Web-API**, voer een naam in en klik op volgende pijl Hallo.</span><span class="sxs-lookup"><span data-stu-id="15da7-216">Choose **Web application and/or Web API**, enter a name, and click hello next arrow.</span></span> <span data-ttu-id="15da7-217">In dit voorbeeld **APIMDeveloperPortal** wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="15da7-217">In this example **APIMDeveloperPortal** is used.</span></span>

![nieuwe toepassing][api-management-aad-new-application-devportal-1]

<span data-ttu-id="15da7-219">Voor **aanmeldings-URL** Voer Hallo-URL van uw API Management-service en toevoeg- `/signin`.</span><span class="sxs-lookup"><span data-stu-id="15da7-219">For **Sign-on URL** enter hello URL of your API Management service and append `/signin`.</span></span> <span data-ttu-id="15da7-220">In dit voorbeeld `https://contoso5.portal.azure-api.net/signin` wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="15da7-220">In this example `https://contoso5.portal.azure-api.net/signin` is used.</span></span>

<span data-ttu-id="15da7-221">Voor **App-Id-URL** Voer Hallo-URL van uw API Management-service en het toevoegen van enkele unieke tekens.</span><span class="sxs-lookup"><span data-stu-id="15da7-221">For **App Id URL** enter hello URL of your API Management service and append some unique characters.</span></span> <span data-ttu-id="15da7-222">Deze mag gewenste tekens lang zijn en in dit voorbeeld `https://contoso5.portal.azure-api.net/dp` wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="15da7-222">These can be any desired characters and in this example `https://contoso5.portal.azure-api.net/dp` is used.</span></span> <span data-ttu-id="15da7-223">Wanneer Hallo gewenst **App-eigenschappen** zijn geconfigureerd, klikt u op Hallo vinkje toocreate Hallo toepassing.</span><span class="sxs-lookup"><span data-stu-id="15da7-223">When hello  desired **App properties** are configured, click hello check mark toocreate hello application.</span></span>

![nieuwe toepassing][api-management-aad-new-application-devportal-2]

## <a name="configure-an-api-management-oauth-20-authorization-server"></a><span data-ttu-id="15da7-225">Een API Management OAuth 2.0-autorisatie-server configureren</span><span class="sxs-lookup"><span data-stu-id="15da7-225">Configure an API Management OAuth 2.0 authorization server</span></span>
<span data-ttu-id="15da7-226">de volgende stap Hallo is tooconfigure een OAuth 2.0-autorisatie-server in API Management.</span><span class="sxs-lookup"><span data-stu-id="15da7-226">hello next step is tooconfigure an OAuth 2.0 authorization server in API Management.</span></span> <span data-ttu-id="15da7-227">Deze stap wordt geïllustreerd in de video vanaf 9:43 Hallo.</span><span class="sxs-lookup"><span data-stu-id="15da7-227">This step is demonstrated in hello video starting at 9:43.</span></span>

<span data-ttu-id="15da7-228">Klik op **beveiliging** in aan de linkerkant Hallo Hallo API Management-menu, klikt u op **OAuth 2.0**, en klik vervolgens op **toevoegen autorisatie** server.</span><span class="sxs-lookup"><span data-stu-id="15da7-228">Click **Security** from hello API Management menu on hello left, click **OAuth 2.0**, and then click **Add authorization** server.</span></span>

![Autorisatie-server toevoegen][api-management-add-authorization-server]

<span data-ttu-id="15da7-230">Voer een naam en een optionele beschrijving in Hallo **naam** en **beschrijving** velden.</span><span class="sxs-lookup"><span data-stu-id="15da7-230">Enter a name and an optional description in hello **Name** and **Description** fields.</span></span> <span data-ttu-id="15da7-231">Deze velden zijn gebruikte tooidentify Hallo OAuth 2.0 autorisatie server binnen Hallo API Management service-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="15da7-231">These fields are used tooidentify hello OAuth 2.0 authorization server within hello API Management service instance.</span></span> <span data-ttu-id="15da7-232">In dit voorbeeld **autorisatie server demo** wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="15da7-232">In this example **Authorization server demo** is used.</span></span> <span data-ttu-id="15da7-233">Later wanneer u een OAuth 2.0-server toobe voor verificatie voor een API gebruikt opgeeft, selecteert u deze naam.</span><span class="sxs-lookup"><span data-stu-id="15da7-233">Later when you specify an OAuth 2.0 server toobe used for authentication for an API, you will select this name.</span></span>

<span data-ttu-id="15da7-234">Voor Hallo **Client de registratie van URL** Voer een aanduidingswaarde van de tijdelijke zoals `http://localhost`.</span><span class="sxs-lookup"><span data-stu-id="15da7-234">For hello **Client registration page URL** enter a placeholder value such as `http://localhost`.</span></span>  <span data-ttu-id="15da7-235">Hallo **Client de registratie van URL** punten toohello pagina die door gebruikers kunnen toocreate gebruiken en hun eigen accounts configureren voor OAuth 2.0-providers die ondersteuning bieden voor gebruikersbeheer van accounts.</span><span class="sxs-lookup"><span data-stu-id="15da7-235">hello **Client registration page URL** points toohello page that users can use toocreate and configure their own accounts for OAuth 2.0 providers that support user management of accounts.</span></span> <span data-ttu-id="15da7-236">In dit voorbeeld gebruikers niet maken en hun eigen accounts configureren zodat een tijdelijke aanduiding wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="15da7-236">In this example users do not create and configure their own accounts so a placeholder is used.</span></span>

![Autorisatie-server toevoegen][api-management-add-authorization-server-1]

<span data-ttu-id="15da7-238">Geef vervolgens **autorisatie eindpunt-URL** en **Token eindpunt-URL**.</span><span class="sxs-lookup"><span data-stu-id="15da7-238">Next, specify **Authorization endpoint URL** and **Token endpoint URL**.</span></span>

![Autorisatie-server][api-management-add-authorization-server-1a]

<span data-ttu-id="15da7-240">Deze waarden kunnen worden opgehaald uit Hallo **App eindpunten** pagina Hallo AAD-toepassing die u hebt gemaakt voor het Hallo-portal voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="15da7-240">These values can be retrieved from hello **App Endpoints** page of hello AAD application you created for hello developer portal.</span></span> <span data-ttu-id="15da7-241">tooaccess hello eindpunten Navigeer toohello **configureren** voor AAD-toepassing hello tabblad en klik op **eindpunten weergeven**.</span><span class="sxs-lookup"><span data-stu-id="15da7-241">tooaccess hello endpoints navigate toohello **Configure** tab for hello AAD application and click **View endpoints**.</span></span>

![Toepassing][api-management-aad-devportal-application]

![Eindpunten weergeven][api-management-aad-view-endpoints]

<span data-ttu-id="15da7-244">Kopiëren Hallo **OAuth 2.0-eindpunt voor autorisatie** en plak deze in Hallo **autorisatie eindpunt-URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="15da7-244">Copy hello **OAuth 2.0 authorization endpoint** and paste it into hello **Authorization endpoint URL** textbox.</span></span>

![Autorisatie-server toevoegen][api-management-add-authorization-server-2]

<span data-ttu-id="15da7-246">Kopiëren Hallo **OAuth 2.0-tokeneindpunt** en plak deze in Hallo **Token eindpunt-URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="15da7-246">Copy hello **OAuth 2.0 token endpoint** and paste it into hello **Token endpoint URL** textbox.</span></span>

![Autorisatie-server toevoegen][api-management-add-authorization-server-2a]

<span data-ttu-id="15da7-248">Bovendien toopasting in token Hallo-eindpunt toevoegen voor een extra inhoudparameter met de naam **resource** en gebruiken voor Hallo waarde Hallo **App Id URI** van Hallo AAD-toepassing voor Hallo back-endservice die was gemaakt tijdens het Hallo Visual Studio-project is gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="15da7-248">In addition toopasting in hello token endpoint, add an additional body parameter named **resource** and for hello value use hello **App Id URI** from hello AAD application for hello backend service that was created when hello Visual Studio project was published.</span></span>

![App Id URI][api-management-aad-sso-uri]

<span data-ttu-id="15da7-250">Geef vervolgens referenties Hallo-client.</span><span class="sxs-lookup"><span data-stu-id="15da7-250">Next, specify hello client credentials.</span></span> <span data-ttu-id="15da7-251">Dit zijn Hallo referenties voor Hallo-bron die u wilt dat tooaccess, in dit geval Hallo-portal voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="15da7-251">These are hello credentials for hello resource you want tooaccess, in this case hello developer portal.</span></span>

![Clientreferenties][api-management-client-credentials]

<span data-ttu-id="15da7-253">Hallo tooget **Client-Id**, navigeer toohello **configureren** tabblad Hallo AAD-toepassing voor Hallo developer-portal en kopieer Hallo **Client-Id**.</span><span class="sxs-lookup"><span data-stu-id="15da7-253">tooget hello **Client Id**, navigate toohello **Configure** tab of hello AAD application for hello developer portal and copy hello **Client Id**.</span></span>

<span data-ttu-id="15da7-254">Hallo tooget **Clientgeheim** klikt u op Hallo **Selecteer duur** vervolgkeuzelijst in Hallo **sleutels** sectie en geeft u een interval.</span><span class="sxs-lookup"><span data-stu-id="15da7-254">tooget hello **Client Secret** click hello **Select duration** drop-down in hello **Keys** section and specify an interval.</span></span> <span data-ttu-id="15da7-255">In dit voorbeeld wordt 1 jaar gebruikt.</span><span class="sxs-lookup"><span data-stu-id="15da7-255">In this example 1 year is used.</span></span>

![Client-ID][api-management-aad-client-id]

<span data-ttu-id="15da7-257">Klik op **opslaan** toosave Hallo configuratie- en Hallo sleutel.</span><span class="sxs-lookup"><span data-stu-id="15da7-257">Click **Save** toosave hello configuration and display hello key.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="15da7-258">Noteer deze sleutel.</span><span class="sxs-lookup"><span data-stu-id="15da7-258">Make a note of this key.</span></span> <span data-ttu-id="15da7-259">Wanneer u een venster hello Azure Active Directory-configuratie hebt gesloten, kan niet opnieuw Hallo sleutel weergegeven.</span><span class="sxs-lookup"><span data-stu-id="15da7-259">Once you close hello Azure Active Directory configuration window, hello key cannot be displayed again.</span></span>
> 
> 

<span data-ttu-id="15da7-260">Kopiëren Hallo sleutel toohello Klembord, switch back toohello publicatieportal, plak Hallo sleutel Hallo **Clientgeheim** tekstvak en klik op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="15da7-260">Copy hello key toohello clipboard, switch back toohello publisher portal, paste hello key into hello **Client Secret** textbox, and click **Save**.</span></span>

![Autorisatie-server toevoegen][api-management-add-authorization-server-3]

<span data-ttu-id="15da7-262">Direct na de clientreferenties Hallo is een code machtiging grant.</span><span class="sxs-lookup"><span data-stu-id="15da7-262">Immediately following hello client credentials is an authorization code grant.</span></span> <span data-ttu-id="15da7-263">Deze autorisatiecode kopiëren en switch back tooyour developer-portal Azure AD-toepassing pagina configureren en plak Hallo authorization grant in Hallo **antwoord-URL** veld en klikt u op **opslaan** opnieuw.</span><span class="sxs-lookup"><span data-stu-id="15da7-263">Copy this authorization code and switch back tooyour Azure AD developer portal application configure page, and paste hello authorization grant into hello **Reply URL** field, and click **Save** again.</span></span>

![Antwoord-URL][api-management-aad-reply-url]

<span data-ttu-id="15da7-265">de volgende stap Hallo is tooconfigure Hallo machtigingen voor Hallo-portal voor ontwikkelaars AAD-toepassing.</span><span class="sxs-lookup"><span data-stu-id="15da7-265">hello next step is tooconfigure hello permissions for hello developer portal AAD application.</span></span> <span data-ttu-id="15da7-266">Klik op **Toepassingsmachtigingen** en het selectievakje in voor Hallo **mapgegevens lezen**.</span><span class="sxs-lookup"><span data-stu-id="15da7-266">Click **Application Permissions** and check hello box for **Read directory data**.</span></span> <span data-ttu-id="15da7-267">Klik op **opslaan** toosave dit wijzigen en klik vervolgens op **toepassing toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="15da7-267">Click **Save** toosave this change, and then click **Add application**.</span></span>

![Machtigingen toevoegen][api-management-add-devportal-permissions]

<span data-ttu-id="15da7-269">Klik op het zoekpictogram hello, type **APIM** in Hallo beginnen met het selectievakje, selecteer **APIMAADDemo**, en klik op Hallo vinkje toosave.</span><span class="sxs-lookup"><span data-stu-id="15da7-269">Click hello search icon, type **APIM** into hello Starting with box, select **APIMAADDemo**, and click hello check mark toosave.</span></span>

![Machtigingen toevoegen][api-management-aad-add-app-permissions]

<span data-ttu-id="15da7-271">Klik op **gedelegeerde machtigingen** voor **APIMAADDemo** en het selectievakje in voor Hallo **toegang APIMAADDemo**, en klik op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="15da7-271">Click **Delegated Permissions** for **APIMAADDemo** and check hello box for **Access APIMAADDemo**, and click **Save**.</span></span> <span data-ttu-id="15da7-272">Dit kan Hallo ontwikkelaar portaltoepassing tooaccess Hallo back-endservice.</span><span class="sxs-lookup"><span data-stu-id="15da7-272">This allows hello developer portal application tooaccess hello backend service.</span></span>

![Machtigingen toevoegen][api-management-aad-add-delegated-permissions]

## <a name="enable-oauth-20-user-authorization-for-hello-calculator-api"></a><span data-ttu-id="15da7-274">Inschakelen van OAuth 2.0-gebruikersautorisatie voor Hallo basisrekenmachine-API</span><span class="sxs-lookup"><span data-stu-id="15da7-274">Enable OAuth 2.0 user authorization for hello Calculator API</span></span>
<span data-ttu-id="15da7-275">Nu dat hello OAuth 2.0-server is geconfigureerd, kunt u deze kunt opgeven in de beveiligingsinstellingen Hallo voor uw API.</span><span class="sxs-lookup"><span data-stu-id="15da7-275">Now that hello OAuth 2.0 server is configured, you can specify it in hello security settings for your API.</span></span> <span data-ttu-id="15da7-276">Deze stap wordt geïllustreerd in Hallo video vanaf 14:30.</span><span class="sxs-lookup"><span data-stu-id="15da7-276">This step is demonstrated in hello video starting at 14:30.</span></span>

<span data-ttu-id="15da7-277">Klik op **API's** in Hallo menu aan de linkerkant en klik op **Rekenmachine** tooview en configureer de instellingen.</span><span class="sxs-lookup"><span data-stu-id="15da7-277">Click **APIs** in hello left menu, and click  **Calculator** tooview and configure its settings.</span></span>

![Rekenmachine-API][api-management-calc-api]

<span data-ttu-id="15da7-279">Navigeer toohello **beveiliging** tabblad, controleert u Hallo **OAuth 2.0** selectievakje, selecteer Hallo gewenste autorisatie server uit Hallo **autorisatie server** vervolgkeuzelijst en klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="15da7-279">Navigate toohello **Security** tab, check hello **OAuth 2.0** checkbox, select hello desired authorization server from hello **Authorization server** drop-down, and click **Save**.</span></span>

![Rekenmachine-API][api-management-enable-aad-calculator]

## <a name="successfully-call-hello-calculator-api-from-hello-developer-portal"></a><span data-ttu-id="15da7-281">Alleen Hallo basisrekenmachine-API aanroepen vanuit de ontwikkelaarsportal Hallo</span><span class="sxs-lookup"><span data-stu-id="15da7-281">Successfully call hello Calculator API from hello developer portal</span></span>
<span data-ttu-id="15da7-282">Nu dat Hallo OAuth 2.0-autorisatie op Hallo API is geconfigureerd, kunnen bewerkingen met succes worden aangeroepen vanuit Hallo developer center.</span><span class="sxs-lookup"><span data-stu-id="15da7-282">Now that hello OAuth 2.0 authorization is configured on hello API, its operations can be successfully called from hello developer center.</span></span> <span data-ttu-id="15da7-283">Deze stap wordt geïllustreerd in Hallo video om 15:00 uur wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="15da7-283">THis step is demonstrated in hello video starting at 15:00.</span></span>

<span data-ttu-id="15da7-284">Navigeer terug toohello **twee gehele getallen toevoegen** bewerking van Hallo Rekenmachine service in Hallo developer-portal en klik op **Try it**.</span><span class="sxs-lookup"><span data-stu-id="15da7-284">Navigate back toohello **Add two integers** operation of hello calculator service in hello developer portal and click **Try it**.</span></span> <span data-ttu-id="15da7-285">Opmerking Hallo nieuw item in Hallo **autorisatie** sectie bijbehorende toohello autorisatie server u zojuist hebt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="15da7-285">Note hello new item in hello **Authorization** section corresponding toohello authorization server you just added.</span></span>

![Rekenmachine-API][api-management-calc-authorization-server]

<span data-ttu-id="15da7-287">Selecteer **autorisatiecode** van Hallo autorisatie vervolgkeuzelijst en voer de referenties op Hallo van Hallo account toouse.</span><span class="sxs-lookup"><span data-stu-id="15da7-287">Select **Authorization code** from hello authorization drop-down list and enter hello credentials of hello account toouse.</span></span> <span data-ttu-id="15da7-288">Als u al bent aangemeld bij Hallo-account is u mogelijk niet gevraagd.</span><span class="sxs-lookup"><span data-stu-id="15da7-288">If you are already signed in with hello account you may not be prompted.</span></span>

![Rekenmachine-API][api-management-devportal-authorization-code]

<span data-ttu-id="15da7-290">Klik op **verzenden** en Opmerking Hallo **antwoordstatus** van **200 OK** en Hallo resultaten van antwoordinhoud Hallo Hallo-bewerking.</span><span class="sxs-lookup"><span data-stu-id="15da7-290">Click **Send** and note hello **Response status** of **200 OK** and hello results of hello operation in hello response content.</span></span>

![Rekenmachine-API][api-management-devportal-response]

## <a name="configure-a-desktop-application-toocall-hello-api"></a><span data-ttu-id="15da7-292">Een bureaubladtoepassing toocall Hallo API configureren</span><span class="sxs-lookup"><span data-stu-id="15da7-292">Configure a desktop application toocall hello API</span></span>
<span data-ttu-id="15da7-293">de volgende procedure Hallo in Hallo video begint bij 16:30 en configureert u een eenvoudige bureaubladtoepassing toocall Hallo API.</span><span class="sxs-lookup"><span data-stu-id="15da7-293">hello next procedure in hello video starts at 16:30 and configures a simple desktop application toocall hello API.</span></span> <span data-ttu-id="15da7-294">de eerste stap Hallo is tooregister Hallo bureaubladtoepassing in Azure AD en geef deze toegang toohello directory en toohello back-endservice.</span><span class="sxs-lookup"><span data-stu-id="15da7-294">hello first step is tooregister hello desktop application in Azure AD and give it access toohello directory and toohello backend service.</span></span> <span data-ttu-id="15da7-295">18:25 is er een demonstratie van Hallo bureaubladtoepassing een bewerking op Hallo Rekenmachine-API aanroepen.</span><span class="sxs-lookup"><span data-stu-id="15da7-295">At 18:25 there is a demonstration of hello desktop application calling an operation on hello calculator API.</span></span>

## <a name="configure-a-jwt-validation-policy-toopre-authorize-requests"></a><span data-ttu-id="15da7-296">Configureren van een JWT validatie beleid toopre-aanvragen toestaan</span><span class="sxs-lookup"><span data-stu-id="15da7-296">Configure a JWT validation policy toopre-authorize requests</span></span>
<span data-ttu-id="15da7-297">Hallo laatste procedure in Hallo video begint bij 20:48 en laat u zien hoe toouse hello [JWT valideren](https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#ValidateJWT) beleid toopre-aanvragen door het Hallo-toegangstokens voor elke inkomende aanvraag valideren autoriseren.</span><span class="sxs-lookup"><span data-stu-id="15da7-297">hello final procedure in hello video starts at 20:48 and shows you how toouse hello [Validate JWT](https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#ValidateJWT) policy toopre-authorize requests by validating hello access tokens of each incoming request.</span></span> <span data-ttu-id="15da7-298">Hallo-aanvraag is niet gevalideerd door Hallo valideren JWT-beleid, Hallo-aanvraag wordt geblokkeerd door de API Management als back-end voor toohello niet wordt doorgestuurd.</span><span class="sxs-lookup"><span data-stu-id="15da7-298">If hello request is not validated by hello Validate JWT policy, hello request is blocked by API Management and is not passed along toohello backend.</span></span>

```xml
<validate-jwt header-name="Authorization" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Access token is missing or invalid.">
    <openid-config url="https://login.microsoftonline.com/DemoAPIM.onmicrosoft.com/.well-known/openid-configuration" />
    <required-claims>
        <claim name="aud">
            <value>https://DemoAPIM.NOTonmicrosoft.com/APIMAADDemo</value>
        </claim>
    </required-claims>
</validate-jwt>
```

<span data-ttu-id="15da7-299">Zie voor een andere demonstratie van configureren en gebruiken van dit beleid [Cloud hebben betrekking op aflevering 177: meer API Management-functies](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) en too13:50 vooruit.</span><span class="sxs-lookup"><span data-stu-id="15da7-299">For another demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too13:50.</span></span> <span data-ttu-id="15da7-300">Snel toosee Hallo beleid dat is geconfigureerd in de beleidseditor Hallo doorsturen too15:00 en vervolgens too18:50 voor een demonstratie van een bewerking aanroepen vanuit de ontwikkelaarsportal Hallo zowel met als zonder Hallo verificatietoken vereist.</span><span class="sxs-lookup"><span data-stu-id="15da7-300">Fast forward too15:00 toosee hello policies configured in hello policy editor and then too18:50 for a demonstration of calling an operation from hello developer portal both with and without hello required authorization token.</span></span>

## <a name="next-steps"></a><span data-ttu-id="15da7-301">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="15da7-301">Next steps</span></span>
* <span data-ttu-id="15da7-302">Bekijk meer [video's](https://azure.microsoft.com/documentation/videos/index/?services=api-management) over API Management.</span><span class="sxs-lookup"><span data-stu-id="15da7-302">Check out more [videos](https://azure.microsoft.com/documentation/videos/index/?services=api-management) about API Management.</span></span>
* <span data-ttu-id="15da7-303">Voor andere manieren toosecure uw back-endservice Zie [wederzijdse certificaatverificatie](api-management-howto-mutual-certificates.md).</span><span class="sxs-lookup"><span data-stu-id="15da7-303">For other ways toosecure your backend service, see [Mutual Certificate authentication](api-management-howto-mutual-certificates.md).</span></span>

[api-management-management-console]: ./media/api-management-howto-protect-backend-with-aad/api-management-management-console.png

[api-management-import-api]: ./media/api-management-howto-protect-backend-with-aad/api-management-import-api.png
[api-management-import-new-api]: ./media/api-management-howto-protect-backend-with-aad/api-management-import-new-api.png
[api-management-create-aad-menu]: ./media/api-management-howto-protect-backend-with-aad/api-management-create-aad-menu.png
[api-management-create-aad]: ./media/api-management-howto-protect-backend-with-aad/api-management-create-aad.png
[api-management-new-web-app]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-web-app.png
[api-management-new-project]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-project.png
[api-management-new-project-cloud]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-project-cloud.png
[api-management-change-authentication]: ./media/api-management-howto-protect-backend-with-aad/api-management-change-authentication.png
[api-management-sign-in-vidual-studio]: ./media/api-management-howto-protect-backend-with-aad/api-management-sign-in-vidual-studio.png
[api-management-configure-web-app]: ./media/api-management-howto-protect-backend-with-aad/api-management-configure-web-app.png
[api-management-aad-domains]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-domains.png
[api-management-add-controller]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-controller.png
[api-management-web-publish]: ./media/api-management-howto-protect-backend-with-aad/api-management-web-publish.png
[api-management-aad-backend-app]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-backend-app.png
[api-management-aad-add-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-add-permissions.png
[api-management-developer-portal-menu]: ./media/api-management-howto-protect-backend-with-aad/api-management-developer-portal-menu.png
[api-management-dev-portal-apis]: ./media/api-management-howto-protect-backend-with-aad/api-management-dev-portal-apis.png
[api-management-dev-portal-try-it]: ./media/api-management-howto-protect-backend-with-aad/api-management-dev-portal-try-it.png
[api-management-dev-portal-send-401]: ./media/api-management-howto-protect-backend-with-aad/api-management-dev-portal-send-401.png
[api-management-aad-new-application-devportal]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-new-application-devportal.png
[api-management-aad-new-application-devportal-1]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-new-application-devportal-1.png
[api-management-aad-new-application-devportal-2]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-new-application-devportal-2.png
[api-management-aad-devportal-application]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-devportal-application.png
[api-management-add-authorization-server]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server.png
[api-management-aad-sso-uri]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-sso-uri.png
[api-management-aad-view-endpoints]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-view-endpoints.png
[api-management-aad-client-id]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-client-id.png
[api-management-add-authorization-server-1]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-1.png
[api-management-add-authorization-server-2]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-2.png
[api-management-add-authorization-server-2a]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-2a.png
[api-management-add-authorization-server-3]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-3.png
[api-management-aad-reply-url]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-reply-url.png
[api-management-add-devportal-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-devportal-permissions.png
[api-management-aad-add-app-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-add-app-permissions.png
[api-management-aad-add-delegated-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-add-delegated-permissions.png
[api-management-calc-api]: ./media/api-management-howto-protect-backend-with-aad/api-management-calc-api.png
[api-management-enable-aad-calculator]: ./media/api-management-howto-protect-backend-with-aad/api-management-enable-aad-calculator.png
[api-management-devportal-authorization-code]: ./media/api-management-howto-protect-backend-with-aad/api-management-devportal-authorization-code.png
[api-management-devportal-response]: ./media/api-management-howto-protect-backend-with-aad/api-management-devportal-response.png
[api-management-calc-authorization-server]: ./media/api-management-howto-protect-backend-with-aad/api-management-calc-authorization-server.png
[api-management-add-authorization-server-1a]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-1a.png
[api-management-client-credentials]: ./media/api-management-howto-protect-backend-with-aad/api-management-client-credentials.png
[api-management-new-aad-application-menu]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-aad-application-menu.png

[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Manage your first API]: api-management-get-started.md
