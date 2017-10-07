---
title: aaaAzure AD v2 JS SPA begeleide Setup - configureren (ARP) | Microsoft Docs
description: Hoe een API waarvoor toegangstokens door Azure Active Directory v2-eindpunt (ARP) kunnen aanroepen in JavaScript SPA-toepassingen
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
ms.openlocfilehash: 157f4e342cd684294e24da6ee1fad8a7c2fc266a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
## <a name="add-hello-applications-registration-information-tooyour-app"></a>Toevoegen van de toepassing hello registratie informatie tooyour App

In deze stap maakt u moet tooconfigure Hallo Omleidings-URL van de registratiegegevens van de toepassing en voeg vervolgens Hallo toepassings-Id tooyour JavaScript SPA-toepassing.

### <a name="configure-redirect-url"></a>Omleidings-URL configureren

Hallo configureren `Redirect URL` veld hierboven met Hallo-URL voor uw pagina index.html op basis van uw webserver en klik vervolgens op *Update*.


> #### <a name="visual-studio-instructions-for-obtaining-redirect-url"></a>Visual Studio-instructies voor het verkrijgen van de omleidings-URL
> tooobtain uw Omleidings-URL, volg de instructies van de Hallo is hieronder:
> 1.    In *Solution Explorer*, selecteer Hallo-project en bekijkt hello `Properties` venster (als u een venster met eigenschappen niet ziet, drukt u op `F4`)
> 2.    Hallo-waarde van kopiëren `URL` toohello Klembord:<br/> ![Projecteigenschappen](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)<br />
> 3.    Plak Hallo-waarde als een `Redirect URL` op Hallo boven aan deze pagina, klik vervolgens op`Update`

<p/>

> #### <a name="setting-redirect-url-for-python"></a>Instelling Omleidings-URL voor Python
> Voor Python, kunt u de poort van de webserver Hallo via de opdrachtregel instellen. Deze Begeleide installatie Hallo poort 8080 gebruikt ter referentie, maar kunt u gratis toouse een willekeurige poort beschikbaar. In elk geval Volg onderstaande tooset van een Omleidings-URL in inschrijvingsgegevens Hallo-toepassing hello instructies:<br/>
> Stel `http://localhost:8080/` als een `Redirect URL` op Hallo boven aan deze pagina, of gebruik `http://localhost:[port]/` als u een aangepaste TCP-poort (waar *[poort]* Hallo aangepaste TCP-poortnummer is), en klik op 'Bijwerken'

### <a name="configure-your-javascript-spa-application"></a>Uw toepassing JavaScript SPA configureren

1.  Maak een bestand met de naam `msalconfig.js` met registratiegegevens Hallo-toepassing. Als u Visual Studio, selecteer Hallo-project (project basismap), klik met de rechtermuisknop en selecteer: `Add`  >  `New Item`  >  `JavaScript File`. Geef deze de naam`msalconfig.js`
2.  Hallo na code tooyour toevoegen `msalconfig.js` bestand:

```javascript
var msalconfig = {
    clientID: "[Enter hello application Id here]",
    redirectUri: location.origin
};
``` 
