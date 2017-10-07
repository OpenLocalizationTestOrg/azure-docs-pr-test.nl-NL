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
ms.openlocfilehash: badc47e131290a56a507592f944a0fc7093260a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
## <a name="configure-your-aspnet-web-app-with-hello-applications-registration-information"></a>Configureren van uw ASP.NET-Web-App met de registratie-informatie van de toepassing hello

In deze stap maakt u uw project toouse SSL configureren, en vervolgens de registratiegegevens van uw toepassing gebruiken Hallo SSL URL tooconfigure. Hierna Hallo-toepassing toevoegen ' registratie informatie tooyour oplossing via *web.config*.

1.  Selecteer Hallo-project in Solution Explorer en bekijkt hello `Properties` venster (als er geen een venster met eigenschappen, druk op F4)
2.  Wijziging `SSL Enabled` te`True`
3.  Hallo-waarde van kopiëren `SSL URL` hierboven en plak deze in Hallo `Redirect URL` veld op Hallo boven aan deze pagina en klik vervolgens op *Update*:<br/><br/>![Projecteigenschappen](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)<br />
4.  Voeg de volgende Hallo in `web.config` bestand in de hoofdmap van de map, onder sectie `configuration\appSettings`:

```xml
<add key="ClientId" value="[Enter hello application Id here]" />
<add key="RedirectUri" value="[Enter hello Redirect URL here]" />
<add key="Tenant" value="common" />
<add key="Authority" value="https://login.microsoftonline.com/{0}/v2.0" /> 
```
