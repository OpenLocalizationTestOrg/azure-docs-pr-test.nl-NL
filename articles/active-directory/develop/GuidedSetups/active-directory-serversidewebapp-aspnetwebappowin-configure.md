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
## <a name="create-an-application-express"></a>Maken van een toepassing (snelle)
Nu u uw toepassing in Hallo tooregister moet *Portal voor registratie van Microsoft-toepassing*:
1. Registreren van uw toepassing via Hallo [Portal voor registratie van Microsoft-toepassing](https://apps.dev.microsoft.com/portal/register-app?appType=serverSideWebApp&appTech=aspNetWebAppOwin&step=configure)
2.  Voer een naam voor uw toepassing en uw e-mailadres
3.  Zorg ervoor dat de optie Hallo voor begeleide Setup is ingeschakeld
4.  Ga als volgt Hallo instructies tooadd een Omleidings-URL tooyour-toepassing

## <a name="add-your-application-registration-information-tooyour-solution-advanced"></a>Toevoegen van uw toepassing registratie informatie tooyour oplossing (Geavanceerd)
Nu u uw toepassing in Hallo tooregister moet *Portal voor registratie van Microsoft-toepassing*:
1. Ga toohello [Portal voor registratie van Microsoft-toepassing](https://apps.dev.microsoft.com/portal/register-app) tooregister een toepassing
2. Voer een naam voor uw toepassing en uw e-mailadres 
3.  Zorg ervoor dat de optie Hallo voor begeleide Setup is uitgeschakeld
4.  Klik op `Add Platform`, selecteer vervolgens`Web`
5.  Ga terug tooVisual Studio, selecteer Hallo-project in Solution Explorer en bekijkt hello eigenschappenvenster (als er geen een venster met eigenschappen, druk op F4)
6.  SSL ingeschakeld te wijzigen`True`
7.  Hallo SSL URL kopiëren en toevoegen van deze URL toohello lijst van de omleidings-URL's in de lijst Hallo Registratieportal van de omleidings-URL's:<br/><br/>![Projecteigenschappen](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)<br />
8.  Voeg de volgende Hallo in `web.config` zich in de hoofdmap Hallo onder sectie Hallo `configuration\appSettings`:

```xml
<add key="ClientId" value="Enter_the_Application_Id_here" />
<add key="redirectUri" value="Enter_the_Redirect_URL_here" />
<add key="Tenant" value="common" />
<add key="Authority" value="https://login.microsoftonline.com/{0}/v2.0" /> 
```
<!-- Workaround for Docs conversion bug -->
<ol start="9">
<li>
Vervang `ClientId` Hello toepassings-Id die u zojuist hebt geregistreerd
</li>
<li>
Vervang `redirectUri` Hello SSL-URL van uw project
</li>
</ol>
<!-- End Docs -->
