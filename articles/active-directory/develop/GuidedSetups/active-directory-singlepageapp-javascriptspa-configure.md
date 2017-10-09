---
title: aaaAzure AD v2 JS SPA begeleide Setup - configureren | Microsoft Docs
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
ms.openlocfilehash: 1b93298d4bd4e17dd261dbb75502a122c30aac97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
## <a name="register-your-application"></a>Uw toepassing registreren

Er zijn meerdere manieren toocreate een toepassing, selecteer een van beide:

### <a name="option-1-register-your-application-express-mode"></a>Optie 1: De toepassing (Express-modus) registreren
Nu u uw toepassing in Hallo tooregister moet *Portal voor registratie van Microsoft-toepassing*:

1.  Registreren van uw toepassing via Hallo [Portal voor registratie van Microsoft-toepassing](https://apps.dev.microsoft.com/portal/register-app?appType=singlePageApp&appTech=javascriptSpa&step=configure)
2.  Voer een naam voor uw toepassing en uw e-mailadres
3.  Zorg ervoor Hallo-optie voor *Begeleide instelprocedure* is ingeschakeld
4.  Ga als volgt Hallo instructies tooobtain Hallo toepassings-ID en plak deze in uw code

### <a name="option-2-register-your-application-advanced-mode"></a>Optie 2: De toepassing (geavanceerde modus) registreren

1. Ga toohello [Portal voor registratie van Microsoft-toepassing](https://apps.dev.microsoft.com/portal/register-app) tooregister een toepassing
2. Voer een naam voor uw toepassing en uw e-mailadres 
3. Zorg ervoor Hallo-optie voor *Begeleide instelprocedure* is uitgeschakeld
4.  Klik op `Add Platform`, selecteer vervolgens`Web`
5. Hallo toevoegen `Redirect URL` die overeenkomen met de URL van de van toohello toepassing is op basis van uw webserver. Zie Hallo secties voor instructies over het tooset / verkrijgen Hallo Omleidings-URL in Visual Studio en Python.
6. Klik op *opslaan*

> #### <a name="visual-studio-instructions-for-obtaining-redirect-url"></a>Visual Studio-instructies voor het verkrijgen van de omleidings-URL
> Ga als volgt Hallo instructies tooobtain Omleidings-URL:
> 1.    In *Solution Explorer*, selecteer Hallo-project en bekijkt hello `Properties` venster (als u een venster met eigenschappen niet ziet, drukt u op `F4`)
> 2.    Hallo-waarde van kopiëren `URL` toohello Klembord:<br/> ![Projecteigenschappen](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)<br />
> 3.    Overschakelen back toohello *toepassing Registratieportal* en plak Hallo-waarde als een `Redirect URL` en klik op 'Opslaan'

<p/>

> #### <a name="setting-redirect-url-for-python"></a>Instelling Omleidings-URL voor Python
> Voor Python, kunt u de poort van de webserver Hallo via de opdrachtregel instellen. Deze Begeleide installatie Hallo poort 8080 gebruikt ter referentie, maar kunt u gratis toouse een willekeurige poort beschikbaar. In elk geval Volg onderstaande tooset van een Omleidings-URL in inschrijvingsgegevens Hallo-toepassing hello instructies:<br/>
> - Overschakelen back toohello *Portal voor registratie van toepassing* en stel `http://localhost:8080/` als een `Redirect URL`, of gebruik `http://localhost:[port]/` als u een aangepaste TCP-poort (waarbij *[poort]* Hallo aangepaste TCP-poort getal) en klik op 'Opslaan'


#### <a name="configure-your-javascript-spa"></a>Uw JavaScript SPA configureren

1.  Maak een bestand met de naam `msalconfig.js` met registratiegegevens Hallo-toepassing. Als u Visual Studio, selecteer Hallo-project (project basismap), klik met de rechtermuisknop en selecteer: `Add`  >  `New Item`  >  `JavaScript File`. Geef deze de naam`msalconfig.js`
2.  Hallo na code tooyour toevoegen `msalconfig.js` bestand:

```javascript
var msalconfig = {
    clientID: "Enter_the_Application_Id_here",
    redirectUri: location.origin
};
```
<ol start="3">
<li>
Vervang <code>Enter_the_Application_Id_here</code> Hello toepassings-Id die u zojuist hebt geregistreerd
</li>
</ol>
