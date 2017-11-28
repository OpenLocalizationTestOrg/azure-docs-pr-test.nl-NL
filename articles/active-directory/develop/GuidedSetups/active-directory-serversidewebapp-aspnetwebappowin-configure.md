---
title: Azure AD v2 ASP.NET Web Server aan de slag - Config | Microsoft Docs
description: Implementeren van Microsoft-aanmeldingspagina op een ASP.NET-oplossing met een traditioneel browser gebaseerde webtoepassing met behulp van standaard OpenID Connect
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 0c627802ccfba230dcde2dafffee26cb1c895791
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
## <a name="create-an-application-express"></a><span data-ttu-id="9f4d4-103">Maken van een toepassing (snelle)</span><span class="sxs-lookup"><span data-stu-id="9f4d4-103">Create an application (Express)</span></span>
<span data-ttu-id="9f4d4-104">Nu gaat u naar het registreren van uw toepassing in de *Portal voor registratie van Microsoft-toepassing*:</span><span class="sxs-lookup"><span data-stu-id="9f4d4-104">Now you need to register your application in the *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="9f4d4-105">Registreren van uw toepassingen via de [Portal voor registratie van Microsoft-toepassing](https://apps.dev.microsoft.com/portal/register-app?appType=serverSideWebApp&appTech=aspNetWebAppOwin&step=configure)</span><span class="sxs-lookup"><span data-stu-id="9f4d4-105">Register your application via the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=serverSideWebApp&appTech=aspNetWebAppOwin&step=configure)</span></span>
2.  <span data-ttu-id="9f4d4-106">Voer een naam voor uw toepassing en uw e-mailadres</span><span class="sxs-lookup"><span data-stu-id="9f4d4-106">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="9f4d4-107">Zorg ervoor dat de optie voor begeleide Setup is ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="9f4d4-107">Make sure the option for Guided Setup is checked</span></span>
4.  <span data-ttu-id="9f4d4-108">Volg de instructies voor het toevoegen van een Omleidings-URL voor uw toepassing</span><span class="sxs-lookup"><span data-stu-id="9f4d4-108">Follow the instructions to add a Redirect URL to your application</span></span>

## <a name="add-your-application-registration-information-to-your-solution-advanced"></a><span data-ttu-id="9f4d4-109">De registratiegegevens van uw toepassing toevoegen aan uw oplossing (Geavanceerd)</span><span class="sxs-lookup"><span data-stu-id="9f4d4-109">Add your application registration information to your solution (Advanced)</span></span>
<span data-ttu-id="9f4d4-110">Nu gaat u naar het registreren van uw toepassing in de *Portal voor registratie van Microsoft-toepassing*:</span><span class="sxs-lookup"><span data-stu-id="9f4d4-110">Now you need to register your application in the *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="9f4d4-111">Ga naar de [Portal voor registratie van Microsoft-toepassing](https://apps.dev.microsoft.com/portal/register-app) een toepassing registreren</span><span class="sxs-lookup"><span data-stu-id="9f4d4-111">Go to the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app) to register an application</span></span>
2. <span data-ttu-id="9f4d4-112">Voer een naam voor uw toepassing en uw e-mailadres</span><span class="sxs-lookup"><span data-stu-id="9f4d4-112">Enter a name for your application and your email</span></span> 
3.  <span data-ttu-id="9f4d4-113">Zorg ervoor dat de optie voor begeleide Setup is uitgeschakeld</span><span class="sxs-lookup"><span data-stu-id="9f4d4-113">Make sure the option for Guided Setup is unchecked</span></span>
4.  <span data-ttu-id="9f4d4-114">Klik op `Add Platform`, selecteer vervolgens`Web`</span><span class="sxs-lookup"><span data-stu-id="9f4d4-114">Click `Add Platform`, then select `Web`</span></span>
5.  <span data-ttu-id="9f4d4-115">Ga terug naar Visual Studio en klik in Solution Explorer, selecteert u het project en kijk in het venster Eigenschappen (als er geen een venster met eigenschappen, druk op F4)</span><span class="sxs-lookup"><span data-stu-id="9f4d4-115">Go back to Visual Studio and, in Solution Explorer, select the project and look at the Properties window (if you don’t see a Properties window, press F4)</span></span>
6.  <span data-ttu-id="9f4d4-116">SSL ingeschakeld om te wijzigen`True`</span><span class="sxs-lookup"><span data-stu-id="9f4d4-116">Change SSL Enabled to `True`</span></span>
7.  <span data-ttu-id="9f4d4-117">De SSL-URL kopiëren en deze URL toevoegen aan de lijst van de omleidings-URL's in de lijst van de Portal van de registratie van de omleidings-URL's:</span><span class="sxs-lookup"><span data-stu-id="9f4d4-117">Copy the SSL URL and add this URL to the list of Redirect URLs in the Registration Portal’s list of Redirect URLs:</span></span><br/><br/>![Projecteigenschappen](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)<br />
8.  <span data-ttu-id="9f4d4-119">Voeg de volgende in `web.config` zich in de hoofdmap in de sectie `configuration\appSettings`:</span><span class="sxs-lookup"><span data-stu-id="9f4d4-119">Add the following in `web.config` located in the root folder under the section `configuration\appSettings`:</span></span>

```xml
<add key="ClientId" value="Enter_the_Application_Id_here" />
<add key="redirectUri" value="Enter_the_Redirect_URL_here" />
<add key="Tenant" value="common" />
<add key="Authority" value="https://login.microsoftonline.com/{0}/v2.0" /> 
```
<!-- Workaround for Docs conversion bug -->
<ol start="9">
<li>
<span data-ttu-id="9f4d4-120">Vervang `ClientId` met de toepassings-Id die u zojuist hebt geregistreerd</span><span class="sxs-lookup"><span data-stu-id="9f4d4-120">Replace `ClientId` with the Application Id you just registered</span></span>
</li>
<li>
<span data-ttu-id="9f4d4-121">Vervang `redirectUri` met de SSL-URL van uw project</span><span class="sxs-lookup"><span data-stu-id="9f4d4-121">Replace `redirectUri` with the SSL URL of your project</span></span>
</li>
</ol>
<!-- End Docs -->
