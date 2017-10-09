---
title: aaaAzure AD v2 ASP.NET Web Server aan de slag - Config | Microsoft Docs
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
ms.openlocfilehash: e666be4622ad30aaa1e12e49ae56bbe1e129b2a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
## <a name="create-an-application-express"></a><span data-ttu-id="9671a-103">Maken van een toepassing (snelle)</span><span class="sxs-lookup"><span data-stu-id="9671a-103">Create an application (Express)</span></span>
<span data-ttu-id="9671a-104">Nu u uw toepassing in Hallo tooregister moet *Portal voor registratie van Microsoft-toepassing*:</span><span class="sxs-lookup"><span data-stu-id="9671a-104">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="9671a-105">Registreren van uw toepassing via Hallo [Portal voor registratie van Microsoft-toepassing](https://apps.dev.microsoft.com/portal/register-app?appType=serverSideWebApp&appTech=aspNetWebAppOwin&step=configure)</span><span class="sxs-lookup"><span data-stu-id="9671a-105">Register your application via hello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=serverSideWebApp&appTech=aspNetWebAppOwin&step=configure)</span></span>
2.  <span data-ttu-id="9671a-106">Voer een naam voor uw toepassing en uw e-mailadres</span><span class="sxs-lookup"><span data-stu-id="9671a-106">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="9671a-107">Zorg ervoor dat de optie Hallo voor begeleide Setup is ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="9671a-107">Make sure hello option for Guided Setup is checked</span></span>
4.  <span data-ttu-id="9671a-108">Ga als volgt Hallo instructies tooadd een Omleidings-URL tooyour-toepassing</span><span class="sxs-lookup"><span data-stu-id="9671a-108">Follow hello instructions tooadd a Redirect URL tooyour application</span></span>

## <a name="add-your-application-registration-information-tooyour-solution-advanced"></a><span data-ttu-id="9671a-109">Toevoegen van uw toepassing registratie informatie tooyour oplossing (Geavanceerd)</span><span class="sxs-lookup"><span data-stu-id="9671a-109">Add your application registration information tooyour solution (Advanced)</span></span>
<span data-ttu-id="9671a-110">Nu u uw toepassing in Hallo tooregister moet *Portal voor registratie van Microsoft-toepassing*:</span><span class="sxs-lookup"><span data-stu-id="9671a-110">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="9671a-111">Ga toohello [Portal voor registratie van Microsoft-toepassing](https://apps.dev.microsoft.com/portal/register-app) tooregister een toepassing</span><span class="sxs-lookup"><span data-stu-id="9671a-111">Go toohello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app) tooregister an application</span></span>
2. <span data-ttu-id="9671a-112">Voer een naam voor uw toepassing en uw e-mailadres</span><span class="sxs-lookup"><span data-stu-id="9671a-112">Enter a name for your application and your email</span></span> 
3.  <span data-ttu-id="9671a-113">Zorg ervoor dat de optie Hallo voor begeleide Setup is uitgeschakeld</span><span class="sxs-lookup"><span data-stu-id="9671a-113">Make sure hello option for Guided Setup is unchecked</span></span>
4.  <span data-ttu-id="9671a-114">Klik op `Add Platform`, selecteer vervolgens`Web`</span><span class="sxs-lookup"><span data-stu-id="9671a-114">Click `Add Platform`, then select `Web`</span></span>
5.  <span data-ttu-id="9671a-115">Ga terug tooVisual Studio, selecteer Hallo-project in Solution Explorer en bekijkt hello eigenschappenvenster (als er geen een venster met eigenschappen, druk op F4)</span><span class="sxs-lookup"><span data-stu-id="9671a-115">Go back tooVisual Studio and, in Solution Explorer, select hello project and look at hello Properties window (if you don’t see a Properties window, press F4)</span></span>
6.  <span data-ttu-id="9671a-116">SSL ingeschakeld te wijzigen`True`</span><span class="sxs-lookup"><span data-stu-id="9671a-116">Change SSL Enabled too`True`</span></span>
7.  <span data-ttu-id="9671a-117">Hallo SSL URL kopiëren en toevoegen van deze URL toohello lijst van de omleidings-URL's in de lijst Hallo Registratieportal van de omleidings-URL's:</span><span class="sxs-lookup"><span data-stu-id="9671a-117">Copy hello SSL URL and add this URL toohello list of Redirect URLs in hello Registration Portal’s list of Redirect URLs:</span></span><br/><br/>![Projecteigenschappen](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)<br />
8.  <span data-ttu-id="9671a-119">Voeg de volgende Hallo in `web.config` zich in de hoofdmap Hallo onder sectie Hallo `configuration\appSettings`:</span><span class="sxs-lookup"><span data-stu-id="9671a-119">Add hello following in `web.config` located in hello root folder under hello section `configuration\appSettings`:</span></span>

```xml
<add key="ClientId" value="Enter_the_Application_Id_here" />
<add key="redirectUri" value="Enter_the_Redirect_URL_here" />
<add key="Tenant" value="common" />
<add key="Authority" value="https://login.microsoftonline.com/{0}/v2.0" /> 
```
<!-- Workaround for Docs conversion bug -->
<ol start="9">
<li>
<span data-ttu-id="9671a-120">Vervang `ClientId` Hello toepassings-Id die u zojuist hebt geregistreerd</span><span class="sxs-lookup"><span data-stu-id="9671a-120">Replace `ClientId` with hello Application Id you just registered</span></span>
</li>
<li>
<span data-ttu-id="9671a-121">Vervang `redirectUri` Hello SSL-URL van uw project</span><span class="sxs-lookup"><span data-stu-id="9671a-121">Replace `redirectUri` with hello SSL URL of your project</span></span>
</li>
</ol>
<!-- End Docs -->
