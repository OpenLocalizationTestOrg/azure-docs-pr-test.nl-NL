---
title: Beveiligen van een Web-API-back-end met Azure Active Directory en API Management | Microsoft Docs
description: Informatie over het beveiligen van een Web-API-back-end met Azure Active Directory en API Management.
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
ms.openlocfilehash: 0dfb4102904c2e972e6617fd3851fb1c50147357
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-protect-a-web-api-backend-with-azure-active-directory-and-api-management"></a><span data-ttu-id="c10d5-103">Het beveiligen van een Web-API-back-end met Azure Active Directory en API Management</span><span class="sxs-lookup"><span data-stu-id="c10d5-103">How to protect a Web API backend with Azure Active Directory and API Management</span></span>
<span data-ttu-id="c10d5-104">De volgende video ziet u hoe het bouwen van een Web-API-back-end en beveiligen met behulp van OAuth 2.0-protocol met Azure Active Directory en API Management.</span><span class="sxs-lookup"><span data-stu-id="c10d5-104">The following video shows how to build a Web API backend and protect it using OAuth 2.0 protocol with Azure Active Directory and API Management.</span></span>  <span data-ttu-id="c10d5-105">Dit artikel bevat een overzicht en aanvullende informatie voor de stappen in de video.</span><span class="sxs-lookup"><span data-stu-id="c10d5-105">This article provides an overview and additional information for the steps in the video.</span></span> <span data-ttu-id="c10d5-106">Deze 24 minuut video ziet u hoe aan:</span><span class="sxs-lookup"><span data-stu-id="c10d5-106">This 24 minute video shows you how to:</span></span>

* <span data-ttu-id="c10d5-107">Een Web-API-back-end bouwen en beveilig deze met AAD - begint bij 1:30</span><span class="sxs-lookup"><span data-stu-id="c10d5-107">Build a Web API backend and secure it with AAD - starting at 1:30</span></span>
* <span data-ttu-id="c10d5-108">De API in API Management - 7:10 vanaf importeren</span><span class="sxs-lookup"><span data-stu-id="c10d5-108">Import the API into API Management - starting at 7:10</span></span>
* <span data-ttu-id="c10d5-109">De portal voor ontwikkelaars voor het aanroepen van de API - vanaf 9:09 configureren</span><span class="sxs-lookup"><span data-stu-id="c10d5-109">Configure the Developer portal to call the API - starting at 9:09</span></span>
* <span data-ttu-id="c10d5-110">Configureer een bureaubladtoepassing het API - vanaf 18:08 aan te roepen</span><span class="sxs-lookup"><span data-stu-id="c10d5-110">Configure a desktop application to call the API - starting at 18:08</span></span>
* <span data-ttu-id="c10d5-111">Configureer een beleid voor de validatie van JWT vooraf om aanvragen te verifiëren - 20:47 vanaf</span><span class="sxs-lookup"><span data-stu-id="c10d5-111">Configure a JWT validation policy to pre-authorize requests - starting at 20:47</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Protecting-Web-API-Backend-with-Azure-Active-Directory-and-API-Management/player]
> 
> 

## <a name="create-an-azure-ad-directory"></a><span data-ttu-id="c10d5-112">Een Azure AD-directory maken</span><span class="sxs-lookup"><span data-stu-id="c10d5-112">Create an Azure AD directory</span></span>
<span data-ttu-id="c10d5-113">Voor het beveiligen van uw Web-API ondersteund met Azure Active Directory moet u eerst hebben een AAD-tenant.</span><span class="sxs-lookup"><span data-stu-id="c10d5-113">To secure your Web API backed using Azure Active Directory you must first have a an AAD tenant.</span></span> <span data-ttu-id="c10d5-114">In deze video met de naam van een tenant **APIMDemo** wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c10d5-114">In this video a tenant named **APIMDemo** is used.</span></span> <span data-ttu-id="c10d5-115">Voor het maken van een AAD-tenant, aanmelding bij de [klassieke Azure-Portal](https://manage.windowsazure.com) en klik op **nieuw**->**App Services**->**Active Directory**  -> **Directory**->**aangepast maken**.</span><span class="sxs-lookup"><span data-stu-id="c10d5-115">To create an AAD tenant, sign-in to the [Azure Classic Portal](https://manage.windowsazure.com) and click **New**->**App Services**->**Active Directory**->**Directory**->**Custom Create**.</span></span> 

![Azure Active Directory][api-management-create-aad-menu]

<span data-ttu-id="c10d5-117">In dit voorbeeld van een map met de naam **APIMDemo** wordt gemaakt met een standaarddomein met de naam **DemoAPIM.onmicrosoft.com**.</span><span class="sxs-lookup"><span data-stu-id="c10d5-117">In this example a directory named **APIMDemo** is created with a default domain named **DemoAPIM.onmicrosoft.com**.</span></span> <span data-ttu-id="c10d5-118">Deze map wordt gebruikt in de video.</span><span class="sxs-lookup"><span data-stu-id="c10d5-118">This directory is used throughout the video.</span></span>

![Azure Active Directory][api-management-create-aad]

## <a name="create-a-web-api-service-secured-by-azure-active-directory"></a><span data-ttu-id="c10d5-120">Een Web-API-service worden beveiligd door Azure Active Directory maken</span><span class="sxs-lookup"><span data-stu-id="c10d5-120">Create a Web API service secured by Azure Active Directory</span></span>
<span data-ttu-id="c10d5-121">In deze stap wordt een Web-API-back-end gemaakt met behulp van Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="c10d5-121">In this step, a Web API backend is created using Visual Studio 2013.</span></span> <span data-ttu-id="c10d5-122">In deze stap van de video begint bij 1:30.</span><span class="sxs-lookup"><span data-stu-id="c10d5-122">This step of the video starts at 1:30.</span></span> <span data-ttu-id="c10d5-123">Voor het maken van back-end-Web API-project in Visual Studio klikt u op **bestand**->**nieuw**->**Project**, en kies **ASP.NET-webtoepassing Toepassing** van de **Web** lijst met sjablonen.</span><span class="sxs-lookup"><span data-stu-id="c10d5-123">To create Web API backend project in Visual Studio click **File**->**New**->**Project**, and choose **ASP.NET Web Application** from the **Web** templates list.</span></span> <span data-ttu-id="c10d5-124">In deze video van het project de naam **APIMAADDemo**.</span><span class="sxs-lookup"><span data-stu-id="c10d5-124">In this video the project is named **APIMAADDemo**.</span></span> <span data-ttu-id="c10d5-125">Klik op **OK** om het project te maken.</span><span class="sxs-lookup"><span data-stu-id="c10d5-125">Click **OK** to create the project.</span></span> 

![Visual Studio][api-management-new-web-app]

<span data-ttu-id="c10d5-127">Klik op **Web API** van de **selecteert u een lijst met sjablonen** een Web-API-project maken.</span><span class="sxs-lookup"><span data-stu-id="c10d5-127">Click **Web API** from the **Select a template list** to create a Web API project.</span></span> <span data-ttu-id="c10d5-128">Klik op Azure Directory-verificatie configureren **verificatie wijzigen**.</span><span class="sxs-lookup"><span data-stu-id="c10d5-128">To configure Azure Directory Authentication click **Change Authentication**.</span></span>

![Nieuw project][api-management-new-project]

<span data-ttu-id="c10d5-130">Klik op **Organisatieaccounts**, en geef de **domein** van uw AAD-tenant.</span><span class="sxs-lookup"><span data-stu-id="c10d5-130">Click **Organizational Accounts**, and specify the **Domain** of your AAD tenant.</span></span> <span data-ttu-id="c10d5-131">In dit voorbeeld voor het domein is **DemoAPIM.onmicrosoft.com**.</span><span class="sxs-lookup"><span data-stu-id="c10d5-131">In this example the domain is **DemoAPIM.onmicrosoft.com**.</span></span> <span data-ttu-id="c10d5-132">Het domein van uw directory kan worden verkregen van de **domeinen** tabblad van uw directory.</span><span class="sxs-lookup"><span data-stu-id="c10d5-132">The domain of your directory can be obtained from the **Domains** tab of your directory.</span></span>

![Domeinen][api-management-aad-domains]

<span data-ttu-id="c10d5-134">Configureer de gewenste instellingen in de **verificatie wijzigen** dialoogvenster en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="c10d5-134">Configure the desired settings in the **Change Authentication** dialog box and click **OK**.</span></span>

![Verificatie wijzigen][api-management-change-authentication]

<span data-ttu-id="c10d5-136">Wanneer u klikt op **OK** Visual Studio probeert te registreren van uw toepassing bij uw Azure AD-directory en wordt u mogelijk gevraagd zich aanmelden door Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c10d5-136">When you click **OK** Visual Studio will attempt to register your application with your Azure AD directory and you may be prompted to sign in by Visual Studio.</span></span> <span data-ttu-id="c10d5-137">Meld u aan met een Administrator-account voor uw directory.</span><span class="sxs-lookup"><span data-stu-id="c10d5-137">Sign in using an administrative account for your directory.</span></span>

![Aanmelden bij Visual Studio][api-management-sign-in-vidual-studio]

<span data-ttu-id="c10d5-139">Voor het configureren van dit project als een Azure-Web-API Schakel het selectievakje voor **Host in de cloud** en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="c10d5-139">To configure this project as an Azure Web API check the box for **Host in the cloud** and then click **OK**.</span></span>

![Nieuw project][api-management-new-project-cloud]

<span data-ttu-id="c10d5-141">U wordt mogelijk gevraagd om aan te melden bij Azure en vervolgens kunt u de Web-App configureren.</span><span class="sxs-lookup"><span data-stu-id="c10d5-141">You may be prompted to sign in to Azure, and then you can configure the Web App.</span></span>

![Configureren][api-management-configure-web-app]

<span data-ttu-id="c10d5-143">In dit voorbeeld is een nieuwe **App Service-abonnement** met de naam **APIMAADDemo** is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="c10d5-143">In this example a new **App Service plan** named **APIMAADDemo** is specified.</span></span>

<span data-ttu-id="c10d5-144">Klik op **OK** voor het configureren van de Web-App en het project maken.</span><span class="sxs-lookup"><span data-stu-id="c10d5-144">Click **OK** to configure the Web App and create the project.</span></span>

## <a name="add-the-code-to-the-web-api-project"></a><span data-ttu-id="c10d5-145">Voeg de code toe aan de Web-API-project</span><span class="sxs-lookup"><span data-stu-id="c10d5-145">Add the code to the Web API project</span></span>
<span data-ttu-id="c10d5-146">De code van de volgende stap in de video wordt toegevoegd aan de Web-API-project.</span><span class="sxs-lookup"><span data-stu-id="c10d5-146">The next step in the video adds the code to the Web API project.</span></span> <span data-ttu-id="c10d5-147">Deze stap 4:35 wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="c10d5-147">This step starts at 4:35.</span></span>

<span data-ttu-id="c10d5-148">De Web-API in dit voorbeeld implementeert een basisrekenmachine-service met behulp van een model en een domeincontroller.</span><span class="sxs-lookup"><span data-stu-id="c10d5-148">The Web API in this example implements a basic calculator service using a model and a controller.</span></span> <span data-ttu-id="c10d5-149">Als u wilt toevoegen in het model voor de service, met de rechtermuisknop op **modellen** in **Solution Explorer** en kies **toevoegen**, **klasse**.</span><span class="sxs-lookup"><span data-stu-id="c10d5-149">To add the model for the service, right-click **Models** in **Solution Explorer** and choose **Add**, **Class**.</span></span> <span data-ttu-id="c10d5-150">Naam van de klasse `CalcInput` en klik op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="c10d5-150">Name the class `CalcInput` and click **Add**.</span></span>

<span data-ttu-id="c10d5-151">Voeg de volgende `using` instructie boven aan de `CalcInput.cs` bestand.</span><span class="sxs-lookup"><span data-stu-id="c10d5-151">Add the following `using` statement to the top of the `CalcInput.cs` file.</span></span>

```c#
using Newtonsoft.Json;
```

<span data-ttu-id="c10d5-152">De gegenereerde klasse vervangen door de volgende code.</span><span class="sxs-lookup"><span data-stu-id="c10d5-152">Replace the generated class with the following code.</span></span>

```c#
public class CalcInput
{
    [JsonProperty(PropertyName = "a")]
    public int a;

    [JsonProperty(PropertyName = "b")]
    public int b;
}
```

<span data-ttu-id="c10d5-153">Met de rechtermuisknop op **domeincontrollers** in **Solution Explorer** en kies **toevoegen**->**Controller**.</span><span class="sxs-lookup"><span data-stu-id="c10d5-153">Right-click **Controllers** in **Solution Explorer** and choose **Add**->**Controller**.</span></span> <span data-ttu-id="c10d5-154">Kies **Web API 2-Controller - leeg** en klik op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="c10d5-154">Choose **Web API 2 Controller - Empty** and click **Add**.</span></span> <span data-ttu-id="c10d5-155">Type **CalcController** naam voor de Controller en klik op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="c10d5-155">Type **CalcController** for the Controller name and click **Add**.</span></span>

![Controller toevoegen][api-management-add-controller]

<span data-ttu-id="c10d5-157">Voeg de volgende `using` instructie boven aan de `CalcController.cs` bestand.</span><span class="sxs-lookup"><span data-stu-id="c10d5-157">Add the following `using` statement to the top of the `CalcController.cs` file.</span></span>

```c#
using System.IO;
using System.Web;
using APIMAADDemo.Models;
```

<span data-ttu-id="c10d5-158">De gegenereerde controllerklasse vervangen door de volgende code.</span><span class="sxs-lookup"><span data-stu-id="c10d5-158">Replace the generated controller class with the following code.</span></span> <span data-ttu-id="c10d5-159">Deze code implementeert de `Add`, `Subtract`, `Multiply`, en `Divide` bewerkingen van de basisrekenmachine-API.</span><span class="sxs-lookup"><span data-stu-id="c10d5-159">This code implements the `Add`, `Subtract`, `Multiply`, and `Divide` operations of the Basic Calculator API.</span></span>

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

<span data-ttu-id="c10d5-160">Druk op **F6** te controleren of de oplossing.</span><span class="sxs-lookup"><span data-stu-id="c10d5-160">Press **F6** to build and verify the solution.</span></span>

## <a name="publish-the-project-to-azure"></a><span data-ttu-id="c10d5-161">Het project naar Azure publiceren</span><span class="sxs-lookup"><span data-stu-id="c10d5-161">Publish the project to Azure</span></span>
<span data-ttu-id="c10d5-162">In deze stap van de Visual Studio is project gepubliceerd naar Azure.</span><span class="sxs-lookup"><span data-stu-id="c10d5-162">In this step the Visual Studio project is published to Azure.</span></span> <span data-ttu-id="c10d5-163">In deze stap van de video begint bij 5:45.</span><span class="sxs-lookup"><span data-stu-id="c10d5-163">This step of the video starts at 5:45.</span></span>

<span data-ttu-id="c10d5-164">Voor het publiceren van het project naar Azure, met de rechtermuisknop op de **APIMAADDemo** in Visual Studio-project en kies **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="c10d5-164">To publish the project to Azure, right-click the **APIMAADDemo** project in Visual Studio and choose **Publish**.</span></span> <span data-ttu-id="c10d5-165">Behoud de standaardinstellingen de **webpublicatie** dialoogvenster en klik op **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="c10d5-165">Keep the default settings in the **Publish Web** dialog box and click **Publish**.</span></span>

![Web publiceren][api-management-web-publish]

## <a name="grant-permissions-to-the-azure-ad-backend-service-application"></a><span data-ttu-id="c10d5-167">Machtigingen toekennen voor de servicetoepassing voor back-end van Azure AD</span><span class="sxs-lookup"><span data-stu-id="c10d5-167">Grant permissions to the Azure AD backend service application</span></span>
<span data-ttu-id="c10d5-168">Een nieuwe aanvraag om de back-endservice wordt gemaakt in uw Azure AD-directory als onderdeel van het configureren en publiceren van uw Web-API-project.</span><span class="sxs-lookup"><span data-stu-id="c10d5-168">A new application for the backend service is created in your Azure AD directory as part of the configuring and publishing process of your Web API project.</span></span> <span data-ttu-id="c10d5-169">In deze stap van de video, beginnend bij 6:13 worden machtigingen verleend aan de Web-API-back-end.</span><span class="sxs-lookup"><span data-stu-id="c10d5-169">In this step of the video, starting at 6:13, permissions are granted to the Web API backend.</span></span>

![Toepassing][api-management-aad-backend-app]

<span data-ttu-id="c10d5-171">Klik op de naam van de toepassing om de vereiste machtigingen te configureren.</span><span class="sxs-lookup"><span data-stu-id="c10d5-171">Click the name of the application to configure the required permissions.</span></span> <span data-ttu-id="c10d5-172">Navigeer naar de **configureren** tabblad en schuif omlaag naar de **machtigingen voor andere toepassingen** sectie.</span><span class="sxs-lookup"><span data-stu-id="c10d5-172">Navigate to the **Configure** tab and scroll down to the **permissions to other applications** section.</span></span> <span data-ttu-id="c10d5-173">Klik op de **Toepassingsmachtigingen** -omlaag naast **Windows** **Azure Active Directory**, schakel het selectievakje voor **mapgegevens lezen** , en klik op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="c10d5-173">Click the **Application Permissions** drop-down beside **Windows** **Azure Active Directory**, check the box for **Read directory data**, and click **Save**.</span></span>

![Machtigingen toevoegen][api-management-aad-add-permissions]

> [!NOTE]
> <span data-ttu-id="c10d5-175">Als **Windows** **Azure Active Directory** wordt niet vermeld in de machtigingen voor andere toepassingen, klikt u op **toepassing toevoegen** en toe te voegen in de lijst.</span><span class="sxs-lookup"><span data-stu-id="c10d5-175">If **Windows** **Azure Active Directory** is not listed under permissions to other applications, click **Add application** and add it from the list.</span></span>
> 
> 

<span data-ttu-id="c10d5-176">Noteer de **App Id URI** voor gebruik in een latere stap wanneer een Azure AD-toepassing is geconfigureerd voor de API Management-portal voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="c10d5-176">Make a note of the **App Id URI** for use in a subsequent step when an Azure AD application is configured for the API Management developer portal.</span></span>

![App Id URI][api-management-aad-sso-uri]

## <a name="import-the-web-api-into-api-management"></a><span data-ttu-id="c10d5-178">De Web-API importeren in API Management</span><span class="sxs-lookup"><span data-stu-id="c10d5-178">Import the Web API into API Management</span></span>
<span data-ttu-id="c10d5-179">API's worden geconfigureerd in de API-publicatieportal, die wordt geopend via de Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="c10d5-179">APIs are configured from the API publisher portal, which is accessed through the Azure Portal.</span></span> <span data-ttu-id="c10d5-180">Als u wilt openen, klikt u op **publicatieportal** van de werkbalk van uw API Management-service.</span><span class="sxs-lookup"><span data-stu-id="c10d5-180">To reach it, click **Publisher portal** from the toolbar of your API Management service.</span></span> <span data-ttu-id="c10d5-181">Als u nog geen exemplaar van API Management-service hebt gemaakt, raadpleegt u [API Management service-exemplaar maken] [ Create an API Management service instance] in de [uw eerste API beheren] [ Manage your first API] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="c10d5-181">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Manage your first API][Manage your first API] tutorial.</span></span>

![Publicatieportal][api-management-management-console]

<span data-ttu-id="c10d5-183">Bewerkingen kunnen worden [toegevoegd aan de API's handmatig](api-management-howto-add-operations.md), of ze kunnen worden geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="c10d5-183">Operations can be [added to APIs manually](api-management-howto-add-operations.md), or they can be imported.</span></span> <span data-ttu-id="c10d5-184">In deze video worden bewerkingen in Swagger-indeling vanaf 6:40 geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="c10d5-184">In this video, operations are imported in Swagger format starting at 6:40.</span></span>

<span data-ttu-id="c10d5-185">Maak een bestand met de naam `calcapi.json` met de volgende inhoud en sla deze op uw computer.</span><span class="sxs-lookup"><span data-stu-id="c10d5-185">Create a file named `calcapi.json` with following contents and save it to your computer.</span></span> <span data-ttu-id="c10d5-186">Zorg ervoor dat de `host` punten kenmerk back-end van uw Web-API.</span><span class="sxs-lookup"><span data-stu-id="c10d5-186">Ensure that the `host` attribute points to your Web API backend.</span></span> <span data-ttu-id="c10d5-187">In dit voorbeeld `"host": "apimaaddemo.azurewebsites.net"` wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c10d5-187">In this example `"host": "apimaaddemo.azurewebsites.net"` is used.</span></span>

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

<span data-ttu-id="c10d5-188">Klik voor het importeren van de rekenmachine-API op **API's** in het menu **API Management** aan de linkerkant en klik vervolgens op **API importeren**.</span><span class="sxs-lookup"><span data-stu-id="c10d5-188">To import the calculator API, click **APIs** from the **API Management** menu on the left, and then click **Import API**.</span></span>

![Knop API importeren][api-management-import-api]

<span data-ttu-id="c10d5-190">Voer de volgende stappen uit voor het configureren van de Rekenmachine-API.</span><span class="sxs-lookup"><span data-stu-id="c10d5-190">Perform the following steps to configure the calculator API.</span></span>

1. <span data-ttu-id="c10d5-191">Klik op **uit bestand**, blader naar de `calculator.json` bestand dat u hebt opgeslagen en op de **Swagger** keuzerondje.</span><span class="sxs-lookup"><span data-stu-id="c10d5-191">Click **From file**, browse to the `calculator.json` file you saved, and click the **Swagger** radio button.</span></span>
2. <span data-ttu-id="c10d5-192">Type **calc** in de **achtervoegsel URL Web-API** textbox.</span><span class="sxs-lookup"><span data-stu-id="c10d5-192">Type **calc** into the **Web API URL suffix** textbox.</span></span>
3. <span data-ttu-id="c10d5-193">Klik in het vak **Producten (optioneel)** en kies **Starter**.</span><span class="sxs-lookup"><span data-stu-id="c10d5-193">Click in the **Products (optional)** box and choose **Starter**.</span></span>
4. <span data-ttu-id="c10d5-194">Klik op **Opslaan** om de API te importeren.</span><span class="sxs-lookup"><span data-stu-id="c10d5-194">Click **Save** to import the API.</span></span>

![Nieuwe API toevoegen][api-management-import-new-api]

<span data-ttu-id="c10d5-196">Zodra de API is geïmporteerd, wordt de overzichtspagina voor de API weergegeven in de publicatieportal.</span><span class="sxs-lookup"><span data-stu-id="c10d5-196">Once the API is imported, the summary page for the API is displayed in the publisher portal.</span></span>

## <a name="call-the-api-unsuccessfully-from-the-developer-portal"></a><span data-ttu-id="c10d5-197">De API succes aanroepen vanuit de portal voor ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="c10d5-197">Call the API unsuccessfully from the developer portal</span></span>
<span data-ttu-id="c10d5-198">Op dit moment de API is geïmporteerd in API Management, maar kan nog worden aangeroepen met succes vanuit de ontwikkelaarsportal omdat de back-endservice is beveiligd met Azure AD-verificatie.</span><span class="sxs-lookup"><span data-stu-id="c10d5-198">At this point, the API has been imported into API Management, but cannot yet be called successfully from the developer portal because the backend service is protected with Azure AD authentication.</span></span> <span data-ttu-id="c10d5-199">Dit wordt geïllustreerd in de video vanaf 7:40 met behulp van de volgende stappen uit.</span><span class="sxs-lookup"><span data-stu-id="c10d5-199">This is demonstrated in the video starting at 7:40 using the following steps.</span></span>

<span data-ttu-id="c10d5-200">Klik op **ontwikkelaarsportal** uit de rechts bovenaan kant van de publicatieportal.</span><span class="sxs-lookup"><span data-stu-id="c10d5-200">Click **Developer portal** from the top-right side of the publisher portal.</span></span>

![ontwikkelaarsportal][api-management-developer-portal-menu]

<span data-ttu-id="c10d5-202">Klik op **API's** en klik op de **Rekenmachine** API.</span><span class="sxs-lookup"><span data-stu-id="c10d5-202">Click **APIs** and click the **Calculator** API.</span></span>

![ontwikkelaarsportal][api-management-dev-portal-apis]

<span data-ttu-id="c10d5-204">Klik op **Try it**.</span><span class="sxs-lookup"><span data-stu-id="c10d5-204">Click **Try it**.</span></span>

![Probeer het nu][api-management-dev-portal-try-it]

<span data-ttu-id="c10d5-206">Klik op **verzenden** en noteer de antwoordstatus van **401 niet geautoriseerd**.</span><span class="sxs-lookup"><span data-stu-id="c10d5-206">Click **Send** and note the response status of **401 Unauthorized**.</span></span>

![Verzenden][api-management-dev-portal-send-401]

<span data-ttu-id="c10d5-208">De aanvraag is niet geautoriseerd, omdat de back-end API is beveiligd door Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c10d5-208">The request is unauthorized because the backend API is protected by Azure Active Directory.</span></span> <span data-ttu-id="c10d5-209">Voordat het is de API aanroept de ontwikkelaar moet de portal worden geconfigureerd voor het autoriseren van ontwikkelaars met behulp van OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="c10d5-209">Before successfully calling the API the developer portal must be configured to authorize developers using OAuth 2.0.</span></span> <span data-ttu-id="c10d5-210">Dit proces wordt beschreven in de volgende secties.</span><span class="sxs-lookup"><span data-stu-id="c10d5-210">This process is described in the following sections.</span></span>

## <a name="register-the-developer-portal-as-an-aad-application"></a><span data-ttu-id="c10d5-211">De portal voor ontwikkelaars registreren als een AAD-toepassing</span><span class="sxs-lookup"><span data-stu-id="c10d5-211">Register the developer portal as an AAD application</span></span>
<span data-ttu-id="c10d5-212">De eerste stap bij het configureren van de portal voor ontwikkelaars om te verifiëren met behulp van OAuth 2.0 ontwikkelaars is de portal voor ontwikkelaars registreren als een AAD-toepassing.</span><span class="sxs-lookup"><span data-stu-id="c10d5-212">The first step in configuring the developer portal to authorize developers using OAuth 2.0 is to register the developer portal as an AAD application.</span></span> <span data-ttu-id="c10d5-213">Dit wordt geïllustreerd 8:27 in de video wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="c10d5-213">This is demonstrated starting at 8:27 in the video.</span></span>

<span data-ttu-id="c10d5-214">Navigeer naar de Azure AD-tenant van de eerste stap in deze video in dit voorbeeld **APIMDemo** en navigeer naar de **toepassingen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="c10d5-214">Navigate to the Azure AD tenant from the first step of this video, in this example **APIMDemo** and navigate to the **Applications** tab.</span></span>

![nieuwe toepassing][api-management-aad-new-application-devportal]

<span data-ttu-id="c10d5-216">Klik op de **toevoegen** klikken om een nieuwe Azure Active Directory-toepassing maken en kies **mijn organisatie ontwikkelt toepassing toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="c10d5-216">Click the **Add** button to create a new Azure Active Directory application, and choose **Add an application my organization is developing**.</span></span>

![nieuwe toepassing][api-management-new-aad-application-menu]

<span data-ttu-id="c10d5-218">Kies **Web-toepassing en/of Web-API**, voer een naam in en klik op de pijl Volgende.</span><span class="sxs-lookup"><span data-stu-id="c10d5-218">Choose **Web application and/or Web API**, enter a name, and click the next arrow.</span></span> <span data-ttu-id="c10d5-219">In dit voorbeeld **APIMDeveloperPortal** wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c10d5-219">In this example **APIMDeveloperPortal** is used.</span></span>

![nieuwe toepassing][api-management-aad-new-application-devportal-1]

<span data-ttu-id="c10d5-221">Voor **aanmeldings-URL** Voer de URL van uw API Management-service en toevoeg- `/signin`.</span><span class="sxs-lookup"><span data-stu-id="c10d5-221">For **Sign-on URL** enter the URL of your API Management service and append `/signin`.</span></span> <span data-ttu-id="c10d5-222">In dit voorbeeld `https://contoso5.portal.azure-api.net/signin` wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c10d5-222">In this example `https://contoso5.portal.azure-api.net/signin` is used.</span></span>

<span data-ttu-id="c10d5-223">Voor **App-Id-URL** Voer de URL van uw API Management-service en het toevoegen van enkele unieke tekens.</span><span class="sxs-lookup"><span data-stu-id="c10d5-223">For **App Id URL** enter the URL of your API Management service and append some unique characters.</span></span> <span data-ttu-id="c10d5-224">Deze mag gewenste tekens lang zijn en in dit voorbeeld `https://contoso5.portal.azure-api.net/dp` wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c10d5-224">These can be any desired characters and in this example `https://contoso5.portal.azure-api.net/dp` is used.</span></span> <span data-ttu-id="c10d5-225">Wanneer de gewenste **App-eigenschappen** zijn geconfigureerd, klikt u op het vinkje om de toepassing te maken.</span><span class="sxs-lookup"><span data-stu-id="c10d5-225">When the  desired **App properties** are configured, click the check mark to create the application.</span></span>

![nieuwe toepassing][api-management-aad-new-application-devportal-2]

## <a name="configure-an-api-management-oauth-20-authorization-server"></a><span data-ttu-id="c10d5-227">Een API Management OAuth 2.0-autorisatie-server configureren</span><span class="sxs-lookup"><span data-stu-id="c10d5-227">Configure an API Management OAuth 2.0 authorization server</span></span>
<span data-ttu-id="c10d5-228">De volgende stap is het configureren van een OAuth 2.0-autorisatie-server in API Management.</span><span class="sxs-lookup"><span data-stu-id="c10d5-228">The next step is to configure an OAuth 2.0 authorization server in API Management.</span></span> <span data-ttu-id="c10d5-229">Deze stap wordt geïllustreerd in de video op 9:43 wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="c10d5-229">This step is demonstrated in the video starting at 9:43.</span></span>

<span data-ttu-id="c10d5-230">Klik op **beveiliging** in het menu API Management aan de linkerkant, klikt u op **OAuth 2.0**, en klik vervolgens op **toevoegen autorisatie** server.</span><span class="sxs-lookup"><span data-stu-id="c10d5-230">Click **Security** from the API Management menu on the left, click **OAuth 2.0**, and then click **Add authorization** server.</span></span>

![Autorisatie-server toevoegen][api-management-add-authorization-server]

<span data-ttu-id="c10d5-232">Voer een naam en een optionele beschrijving in de **naam** en **beschrijving** velden.</span><span class="sxs-lookup"><span data-stu-id="c10d5-232">Enter a name and an optional description in the **Name** and **Description** fields.</span></span> <span data-ttu-id="c10d5-233">Deze velden worden gebruikt voor de server van de autorisatie OAuth 2.0 binnen het exemplaar van API Management-service identificeren.</span><span class="sxs-lookup"><span data-stu-id="c10d5-233">These fields are used to identify the OAuth 2.0 authorization server within the API Management service instance.</span></span> <span data-ttu-id="c10d5-234">In dit voorbeeld **autorisatie server demo** wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c10d5-234">In this example **Authorization server demo** is used.</span></span> <span data-ttu-id="c10d5-235">Later wanneer u een OAuth 2.0-server moet worden gebruikt voor verificatie voor een API opgeeft, selecteert u deze naam.</span><span class="sxs-lookup"><span data-stu-id="c10d5-235">Later when you specify an OAuth 2.0 server to be used for authentication for an API, you will select this name.</span></span>

<span data-ttu-id="c10d5-236">Voor de **Client de registratie van URL** Voer een aanduidingswaarde van de tijdelijke zoals `http://localhost`.</span><span class="sxs-lookup"><span data-stu-id="c10d5-236">For the **Client registration page URL** enter a placeholder value such as `http://localhost`.</span></span>  <span data-ttu-id="c10d5-237">De **Client de registratie van URL** verwijst naar de pagina die gebruikers gebruiken kunnen voor het maken en hun eigen accounts configureren voor OAuth 2.0-providers die ondersteuning bieden voor gebruikersbeheer van accounts.</span><span class="sxs-lookup"><span data-stu-id="c10d5-237">The **Client registration page URL** points to the page that users can use to create and configure their own accounts for OAuth 2.0 providers that support user management of accounts.</span></span> <span data-ttu-id="c10d5-238">In dit voorbeeld gebruikers niet maken en hun eigen accounts configureren zodat een tijdelijke aanduiding wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c10d5-238">In this example users do not create and configure their own accounts so a placeholder is used.</span></span>

![Autorisatie-server toevoegen][api-management-add-authorization-server-1]

<span data-ttu-id="c10d5-240">Geef vervolgens **autorisatie eindpunt-URL** en **Token eindpunt-URL**.</span><span class="sxs-lookup"><span data-stu-id="c10d5-240">Next, specify **Authorization endpoint URL** and **Token endpoint URL**.</span></span>

![Autorisatie-server][api-management-add-authorization-server-1a]

<span data-ttu-id="c10d5-242">Deze waarden kunnen worden opgehaald uit de **App eindpunten** pagina van de AAD-toepassing die u hebt gemaakt voor de portal voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="c10d5-242">These values can be retrieved from the **App Endpoints** page of the AAD application you created for the developer portal.</span></span> <span data-ttu-id="c10d5-243">Voor toegang tot de eindpunten, navigeer naar de **configureren** tabblad voor de AAD-toepassing en klik op **eindpunten weergeven**.</span><span class="sxs-lookup"><span data-stu-id="c10d5-243">To access the endpoints navigate to the **Configure** tab for the AAD application and click **View endpoints**.</span></span>

![Toepassing][api-management-aad-devportal-application]

![Eindpunten weergeven][api-management-aad-view-endpoints]

<span data-ttu-id="c10d5-246">Kopieer de **OAuth 2.0-eindpunt voor autorisatie** en plak deze in de **autorisatie eindpunt-URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="c10d5-246">Copy the **OAuth 2.0 authorization endpoint** and paste it into the **Authorization endpoint URL** textbox.</span></span>

![Autorisatie-server toevoegen][api-management-add-authorization-server-2]

<span data-ttu-id="c10d5-248">Kopieer de **OAuth 2.0-tokeneindpunt** en plak deze in de **Token eindpunt-URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="c10d5-248">Copy the **OAuth 2.0 token endpoint** and paste it into the **Token endpoint URL** textbox.</span></span>

![Autorisatie-server toevoegen][api-management-add-authorization-server-2a]

<span data-ttu-id="c10d5-250">Naast plakken in het token eindpunt toevoegen een extra inhoudparameter met de naam **resource** en voor het gebruik van de waarde de **App Id URI** van de AAD-toepassing voor de back endservice die is gemaakt wanneer de Visual Studio-project is gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="c10d5-250">In addition to pasting in the token endpoint, add an additional body parameter named **resource** and for the value use the **App Id URI** from the AAD application for the backend service that was created when the Visual Studio project was published.</span></span>

![App Id URI][api-management-aad-sso-uri]

<span data-ttu-id="c10d5-252">Geef vervolgens de referenties van de client.</span><span class="sxs-lookup"><span data-stu-id="c10d5-252">Next, specify the client credentials.</span></span> <span data-ttu-id="c10d5-253">Dit zijn de referenties voor de resource die u wilt openen, in dit geval de portal voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="c10d5-253">These are the credentials for the resource you want to access, in this case the developer portal.</span></span>

![Clientreferenties][api-management-client-credentials]

<span data-ttu-id="c10d5-255">Ophalen van de **Client-Id**, gaat u naar de **configureren** tabblad van de AAD-toepassing voor het portal voor ontwikkelaars en kopieer de **Client-Id**.</span><span class="sxs-lookup"><span data-stu-id="c10d5-255">To get the **Client Id**, navigate to the **Configure** tab of the AAD application for the developer portal and copy the **Client Id**.</span></span>

<span data-ttu-id="c10d5-256">Ophalen van de **Clientgeheim** klikt u op de **Selecteer duur** omlaag in de **sleutels** sectie en geeft u een interval.</span><span class="sxs-lookup"><span data-stu-id="c10d5-256">To get the **Client Secret** click the **Select duration** drop-down in the **Keys** section and specify an interval.</span></span> <span data-ttu-id="c10d5-257">In dit voorbeeld wordt 1 jaar gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c10d5-257">In this example 1 year is used.</span></span>

![Client-ID][api-management-aad-client-id]

<span data-ttu-id="c10d5-259">Klik op **opslaan** de configuratie op te slaan en de sleutel wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c10d5-259">Click **Save** to save the configuration and display the key.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="c10d5-260">Noteer deze sleutel.</span><span class="sxs-lookup"><span data-stu-id="c10d5-260">Make a note of this key.</span></span> <span data-ttu-id="c10d5-261">Wanneer u het venster Azure Active Directory-configuratie hebt gesloten, wordt de sleutel kan niet opnieuw weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c10d5-261">Once you close the Azure Active Directory configuration window, the key cannot be displayed again.</span></span>
> 
> 

<span data-ttu-id="c10d5-262">De sleutel naar het Klembord kopiëren, gaat u terug naar de publicatieportal, plak de sleutel in de **Clientgeheim** tekstvak en klik op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="c10d5-262">Copy the key to the clipboard, switch back to the publisher portal, paste the key into the **Client Secret** textbox, and click **Save**.</span></span>

![Autorisatie-server toevoegen][api-management-add-authorization-server-3]

<span data-ttu-id="c10d5-264">Direct na de referenties van de client is een code machtiging grant.</span><span class="sxs-lookup"><span data-stu-id="c10d5-264">Immediately following the client credentials is an authorization code grant.</span></span> <span data-ttu-id="c10d5-265">Kopieer deze autorisatiecode en keert u terug naar uw Azure AD portal developer-toepassing-pagina configureren en plak de machtiging grant in de **antwoord-URL** veld en klikt u op **opslaan** opnieuw.</span><span class="sxs-lookup"><span data-stu-id="c10d5-265">Copy this authorization code and switch back to your Azure AD developer portal application configure page, and paste the authorization grant into the **Reply URL** field, and click **Save** again.</span></span>

![Antwoord-URL][api-management-aad-reply-url]

<span data-ttu-id="c10d5-267">De volgende stap is om de machtigingen voor de portal voor ontwikkelaars AAD-toepassing te configureren.</span><span class="sxs-lookup"><span data-stu-id="c10d5-267">The next step is to configure the permissions for the developer portal AAD application.</span></span> <span data-ttu-id="c10d5-268">Klik op **Toepassingsmachtigingen** en schakel het selectievakje voor **mapgegevens lezen**.</span><span class="sxs-lookup"><span data-stu-id="c10d5-268">Click **Application Permissions** and check the box for **Read directory data**.</span></span> <span data-ttu-id="c10d5-269">Klik op **opslaan** deze wijziging opslaat, en klik vervolgens op **toepassing toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="c10d5-269">Click **Save** to save this change, and then click **Add application**.</span></span>

![Machtigingen toevoegen][api-management-add-devportal-permissions]

<span data-ttu-id="c10d5-271">Klik op het zoekpictogram type **APIM** selecteren in de start met het selectievakje **APIMAADDemo**, en klik op het vinkje om op te slaan.</span><span class="sxs-lookup"><span data-stu-id="c10d5-271">Click the search icon, type **APIM** into the Starting with box, select **APIMAADDemo**, and click the check mark to save.</span></span>

![Machtigingen toevoegen][api-management-aad-add-app-permissions]

<span data-ttu-id="c10d5-273">Klik op **gedelegeerde machtigingen** voor **APIMAADDemo** en schakel het selectievakje voor **toegang APIMAADDemo**, en klik op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="c10d5-273">Click **Delegated Permissions** for **APIMAADDemo** and check the box for **Access APIMAADDemo**, and click **Save**.</span></span> <span data-ttu-id="c10d5-274">Hierdoor kan de ontwikkelaar van de bedrijfsportal-App voor toegang tot de back-endservice.</span><span class="sxs-lookup"><span data-stu-id="c10d5-274">This allows the developer portal application to access the backend service.</span></span>

![Machtigingen toevoegen][api-management-aad-add-delegated-permissions]

## <a name="enable-oauth-20-user-authorization-for-the-calculator-api"></a><span data-ttu-id="c10d5-276">Inschakelen van OAuth 2.0-gebruikersautorisatie voor de basisrekenmachine-API</span><span class="sxs-lookup"><span data-stu-id="c10d5-276">Enable OAuth 2.0 user authorization for the Calculator API</span></span>
<span data-ttu-id="c10d5-277">Nu dat het OAuth 2.0-server is geconfigureerd, kunt u deze kunt opgeven in de beveiligingsinstellingen voor uw API.</span><span class="sxs-lookup"><span data-stu-id="c10d5-277">Now that the OAuth 2.0 server is configured, you can specify it in the security settings for your API.</span></span> <span data-ttu-id="c10d5-278">Deze stap wordt geïllustreerd in de video vanaf 14:30.</span><span class="sxs-lookup"><span data-stu-id="c10d5-278">This step is demonstrated in the video starting at 14:30.</span></span>

<span data-ttu-id="c10d5-279">Klik op **API's** in het menu aan de linkerkant en klik op **Rekenmachine** weergeven en configureren van de instellingen ervan.</span><span class="sxs-lookup"><span data-stu-id="c10d5-279">Click **APIs** in the left menu, and click  **Calculator** to view and configure its settings.</span></span>

![Rekenmachine-API][api-management-calc-api]

<span data-ttu-id="c10d5-281">Navigeer naar de **beveiliging** tabblad controle de **OAuth 2.0** selectievakje, selecteer de gewenste autorisatie-server in de **autorisatie server** vervolgkeuzelijst en klik op  **Sla**.</span><span class="sxs-lookup"><span data-stu-id="c10d5-281">Navigate to the **Security** tab, check the **OAuth 2.0** checkbox, select the desired authorization server from the **Authorization server** drop-down, and click **Save**.</span></span>

![Rekenmachine-API][api-management-enable-aad-calculator]

## <a name="successfully-call-the-calculator-api-from-the-developer-portal"></a><span data-ttu-id="c10d5-283">Is de basisrekenmachine-API aanroepen vanuit de portal voor ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="c10d5-283">Successfully call the Calculator API from the developer portal</span></span>
<span data-ttu-id="c10d5-284">Nu dat het OAuth 2.0-autorisatie is geconfigureerd op de API, kunnen bewerkingen met succes worden aangeroepen vanuit het developer center.</span><span class="sxs-lookup"><span data-stu-id="c10d5-284">Now that the OAuth 2.0 authorization is configured on the API, its operations can be successfully called from the developer center.</span></span> <span data-ttu-id="c10d5-285">Deze stap wordt geïllustreerd in de video om 15:00 uur wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="c10d5-285">THis step is demonstrated in the video starting at 15:00.</span></span>

<span data-ttu-id="c10d5-286">Ga terug naar de **twee gehele getallen toevoegen** bewerking van de Rekenmachine-service in de portal voor ontwikkelaars en klik op **Try it**.</span><span class="sxs-lookup"><span data-stu-id="c10d5-286">Navigate back to the **Add two integers** operation of the calculator service in the developer portal and click **Try it**.</span></span> <span data-ttu-id="c10d5-287">Let op het nieuwe item in de **autorisatie** sectie overeenkomt met de autorisatie-server die u zojuist hebt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="c10d5-287">Note the new item in the **Authorization** section corresponding to the authorization server you just added.</span></span>

![Rekenmachine-API][api-management-calc-authorization-server]

<span data-ttu-id="c10d5-289">Selecteer **autorisatiecode** uit de vervolgkeuzelijst van de autorisatie en voer de referenties van de account moet worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c10d5-289">Select **Authorization code** from the authorization drop-down list and enter the credentials of the account to use.</span></span> <span data-ttu-id="c10d5-290">Als u bent al aangemeld bij het account dat u niet gevraagd.</span><span class="sxs-lookup"><span data-stu-id="c10d5-290">If you are already signed in with the account you may not be prompted.</span></span>

![Rekenmachine-API][api-management-devportal-authorization-code]

<span data-ttu-id="c10d5-292">Klik op **verzenden** en noteer de **antwoordstatus** van **200 OK** en de resultaten van de bewerking in de antwoordinhoud.</span><span class="sxs-lookup"><span data-stu-id="c10d5-292">Click **Send** and note the **Response status** of **200 OK** and the results of the operation in the response content.</span></span>

![Rekenmachine-API][api-management-devportal-response]

## <a name="configure-a-desktop-application-to-call-the-api"></a><span data-ttu-id="c10d5-294">Configureer een bureaubladtoepassing de API aan te roepen</span><span class="sxs-lookup"><span data-stu-id="c10d5-294">Configure a desktop application to call the API</span></span>
<span data-ttu-id="c10d5-295">De volgende procedure in de video begint bij 16:30 en configureert u een eenvoudige bureaubladtoepassing de API aan te roepen.</span><span class="sxs-lookup"><span data-stu-id="c10d5-295">The next procedure in the video starts at 16:30 and configures a simple desktop application to call the API.</span></span> <span data-ttu-id="c10d5-296">De eerste stap is het registreren van de bureaubladtoepassing in Azure AD en toegang geven tot de map en de back-endservice.</span><span class="sxs-lookup"><span data-stu-id="c10d5-296">The first step is to register the desktop application in Azure AD and give it access to the directory and to the backend service.</span></span> <span data-ttu-id="c10d5-297">18:25 is er een demonstratie van de bureaubladtoepassing een bewerking op de Rekenmachine-API aanroepen.</span><span class="sxs-lookup"><span data-stu-id="c10d5-297">At 18:25 there is a demonstration of the desktop application calling an operation on the calculator API.</span></span>

## <a name="configure-a-jwt-validation-policy-to-pre-authorize-requests"></a><span data-ttu-id="c10d5-298">Configureer een beleid voor de validatie van JWT vooraf om aanvragen te verifiëren</span><span class="sxs-lookup"><span data-stu-id="c10d5-298">Configure a JWT validation policy to pre-authorize requests</span></span>
<span data-ttu-id="c10d5-299">De laatste procedure in de video begint bij 20:48 en leest u hoe u de [JWT valideren](https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#ValidateJWT) beleid voor het autoriseren vooraf aanvragen door het valideren van de toegangstokens voor elke inkomende aanvraag.</span><span class="sxs-lookup"><span data-stu-id="c10d5-299">The final procedure in the video starts at 20:48 and shows you how to use the [Validate JWT](https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#ValidateJWT) policy to pre-authorize requests by validating the access tokens of each incoming request.</span></span> <span data-ttu-id="c10d5-300">Als de aanvraag is niet gevalideerd door het valideren van JWT-beleid, wordt de aanvraag wordt geblokkeerd door de API Management en niet wordt doorgestuurd naar de back-end.</span><span class="sxs-lookup"><span data-stu-id="c10d5-300">If the request is not validated by the Validate JWT policy, the request is blocked by API Management and is not passed along to the backend.</span></span>

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

<span data-ttu-id="c10d5-301">Zie voor een andere demonstratie van configureren en gebruiken van dit beleid [Cloud hebben betrekking op aflevering 177: meer API Management-functies](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) en vooruit tot 13:50.</span><span class="sxs-lookup"><span data-stu-id="c10d5-301">For another demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 13:50.</span></span> <span data-ttu-id="c10d5-302">Snel doorsturen naar 15:00 voor een overzicht van het beleid dat is geconfigureerd in de beleidseditor en vervolgens naar 18:50 voor een demonstratie van een bewerking aanroepen vanuit de ontwikkelaarsportal zowel met als zonder de vereiste verificatietoken.</span><span class="sxs-lookup"><span data-stu-id="c10d5-302">Fast forward to 15:00 to see the policies configured in the policy editor and then to 18:50 for a demonstration of calling an operation from the developer portal both with and without the required authorization token.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c10d5-303">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c10d5-303">Next steps</span></span>
* <span data-ttu-id="c10d5-304">Bekijk meer [video's](https://azure.microsoft.com/documentation/videos/index/?services=api-management) over API Management.</span><span class="sxs-lookup"><span data-stu-id="c10d5-304">Check out more [videos](https://azure.microsoft.com/documentation/videos/index/?services=api-management) about API Management.</span></span>
* <span data-ttu-id="c10d5-305">Zie voor andere manieren voor het beveiligen van uw back-endservice [wederzijdse certificaatverificatie](api-management-howto-mutual-certificates.md).</span><span class="sxs-lookup"><span data-stu-id="c10d5-305">For other ways to secure your backend service, see [Mutual Certificate authentication](api-management-howto-mutual-certificates.md).</span></span>

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
