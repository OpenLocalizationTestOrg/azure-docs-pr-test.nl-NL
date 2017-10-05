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
ms.openlocfilehash: 8a1650a65e7980f4a13fa4edc7918b0099bb5464
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
## <a name="configure-your-aspnet-web-app-with-the-applications-registration-information"></a><span data-ttu-id="9a965-103">Configureren van uw ASP.NET-Web-App met gegevens van de registratie van de toepassing</span><span class="sxs-lookup"><span data-stu-id="9a965-103">Configure your ASP.NET Web App with the application's registration information</span></span>

<span data-ttu-id="9a965-104">In deze stap maakt u configureren van uw project om SSL te gebruiken, en vervolgens de SSL-URL gebruiken voor het configureren van de registratie-informatie van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="9a965-104">In this step, you will configure your project to use SSL, and then use the SSL URL to configure your application’s registration information.</span></span> <span data-ttu-id="9a965-105">Hierna moeten de toepassing toevoegen ' registratiegegevens naar uw oplossing via *web.config*.</span><span class="sxs-lookup"><span data-stu-id="9a965-105">After this, add the application’ registration information to your solution via *web.config*.</span></span>

1.  <span data-ttu-id="9a965-106">Selecteer het project in Solution Explorer en bekijk de `Properties` venster (als er geen een venster met eigenschappen, druk op F4)</span><span class="sxs-lookup"><span data-stu-id="9a965-106">In Solution Explorer, select the project and look at the `Properties` window (if you don’t see a Properties window, press F4)</span></span>
2.  <span data-ttu-id="9a965-107">Wijziging `SSL Enabled` naar`True`</span><span class="sxs-lookup"><span data-stu-id="9a965-107">Change `SSL Enabled` to `True`</span></span>
3.  <span data-ttu-id="9a965-108">Kopieer de waarde van `SSL URL` hierboven en plak deze in de `Redirect URL` veld boven aan deze pagina en klik vervolgens op *Update*:</span><span class="sxs-lookup"><span data-stu-id="9a965-108">Copy the value from `SSL URL` above and paste it in the `Redirect URL` field on the top of this page, then click *Update*:</span></span><br/><br/><span data-ttu-id="9a965-109">![Projecteigenschappen](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)</span><span class="sxs-lookup"><span data-stu-id="9a965-109">![Project properties](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)</span></span><br />
4.  <span data-ttu-id="9a965-110">Voeg de volgende in `web.config` bestand in de hoofdmap van de map, onder sectie `configuration\appSettings`:</span><span class="sxs-lookup"><span data-stu-id="9a965-110">Add the following in `web.config` file located in root’s folder, under section `configuration\appSettings`:</span></span>

```xml
<add key="ClientId" value="[Enter the application Id here]" />
<add key="RedirectUri" value="[Enter the Redirect URL here]" />
<add key="Tenant" value="common" />
<add key="Authority" value="https://login.microsoftonline.com/{0}/v2.0" /> 
```
