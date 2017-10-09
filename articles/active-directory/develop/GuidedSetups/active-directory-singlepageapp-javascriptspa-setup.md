---
title: aaaAzure AD v2 JS SPA begeleide installatie - instellingen | Microsoft Docs
description: Hoe een API waarvoor toegangstokens door Azure Active Directory-v2-eindpunt kunnen aanroepen in JavaScript SPA-toepassingen
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/01/2017
ms.author: andret
ms.openlocfilehash: 19e15c6c8db8bea2975f30e7505af79ccad17e02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
## <a name="setting-up-your-web-server-or-project"></a>Instellen van uw webserver of -project

> Voorkeur toodownload deze voorbeeldproject maken in plaats daarvan? 
> - [Hallo Visual Studio-project downloaden](https://github.com/Azure-Samples/active-directory-javascript-graphapi-v2/archive/VisualStudio.zip)
>
> of
> - [Hallo projectbestanden downloaden](https://github.com/Azure-Samples/active-directory-javascript-graphapi-v2/archive/core.zip) voor een lokale webserver, zoals Python
>
> En ga vervolgens verder toohello [configuratiestap](#create-an-application-express) tooconfigure Hallo codevoorbeeld voordat deze wordt uitgevoerd.

## <a name="prerequisites"></a>Vereisten
Een lokale webserver zoals [Python http.server](https://www.python.org/downloads/), [HTTP-server](https://www.npmjs.com/package/http-server/), [.NET Core](https://www.microsoft.com/net/core), of IIS Express integratie met [Visual Studio 2017](https://www.visualstudio.com/downloads/) vereiste toorun is deze Begeleide installatie. 

Instructies in deze handleiding zijn gebaseerd op zowel Python en Visual Studio 2017, maar kunnen u gratis toouse andere ontwikkelomgeving of de webserver.

## <a name="create-your-project"></a>Uw project maken 

> ### <a name="option-1-visual-studio"></a>Optie 1: Visual Studio 
> Als u met behulp van Visual Studio en een nieuw project maakt, voert u de Hallo stappen hieronder toocreate een nieuwe Visual Studio-oplossing:
> 1.    In Visual Studio:`File` > `New` > `Project`
> 2.    Onder `Visual C#\Web`, selecteer`ASP.NET Web Application (.NET Framework)`
> 3.    Naam van uw toepassing en klik op *OK*
> 4.    Onder `New ASP.NET Web Application`, selecteer`Empty`

<p/><!-- -->

> ### <a name="option-2-python-other-web-servers"></a>Optie 2: Python / andere webservers
> Zorg ervoor dat u hebt geïnstalleerd [Python](https://www.python.org/downloads/), volg op Hallo van de volgende stappen:
> - Maak een map toohost uw toepassing.


## <a name="create-your-single-page-applications-ui"></a>De gebruikersinterface van uw toepassing één pagina maken
1.  Maak een *index.html* -bestand voor de SPA JavaScript. Als u Visual Studio, selecteer Hallo-project (project basismap), klik met de rechtermuisknop en selecteer: `Add`  >  `New Item`  >  `HTML page` en noem deze index.html
2.  Hallo tooyour codetabel volgende toevoegen:
```html
<!DOCTYPE html>
<html>
<head>
    <!-- bootstrap reference used for styling hello page -->
    <link href="//maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css" rel="stylesheet">
    <title>JavaScript SPA Guided Setup</title>
</head>
<body style="margin: 40px">
    <button id="callGraphButton" type="button" class="btn btn-primary" onclick="callGraphApi()">Call Microsoft Graph API</button>
    <div id="errorMessage" class="text-danger"></div>
    <div class="hidden">
        <h3>Graph API Call Response</h3>
        <pre class="well" id="graphResponse"></pre>
    </div>
    <div class="hidden">
        <h3>Access Token</h3>
        <pre class="well" id="accessToken"></pre>
    </div>
    <div class="hidden">
        <h3>ID Token Claims</h3>
        <pre class="well" id="userInfo"></pre>
    </div>
    <button id="signOutButton" type="button" class="btn btn-primary hidden" onclick="signOut()">Sign out</button>

    <!-- This app uses cdn tooreference msal.js (recommended). 
         You can also download it from: https://github.com/AzureAD/microsoft-authentication-library-for-js -->
    <script src="https://secure.aadcdn.microsoftonline-p.com/lib/0.1.1/js/msal.min.js"></script>

    <!-- hello 'bluebird' and 'fetch' references below are required if you need toorun this application on Internet Explorer -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/bluebird/3.3.4/bluebird.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/fetch/2.0.3/fetch.min.js"></script>

    <script type="text/javascript" src="msalconfig.js"></script>
    <script type="text/javascript" src="app.js"></script>
</body>
</html>
````
