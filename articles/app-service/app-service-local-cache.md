---
title: overzicht van de lokale App Service-Cache aaaAzure | Microsoft Docs
description: Dit artikel wordt beschreven hoe tooenable, aanpassen en query status van de lokale Cache in Azure App Service-functie Hallo Hallo
services: app-service
documentationcenter: app-service
author: SyntaxC4
manager: yochayk
editor: 
tags: optional
keywords: 
ms.assetid: e34d405e-c5d4-46ad-9b26-2a1eda86ce80
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/04/2016
ms.author: cfowler
ms.openlocfilehash: 220331ac7e15352a434d63266701071024d868c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-local-cache-overview"></a>Overzicht van Azure App Service lokale Cache
Azure-web-app-inhoud is opgeslagen op Azure Storage en omhoog in een duurzame manier als share met de inhoud is opgehaald. Dit ontwerp is bedoeld toowork met tal van apps en Hallo volgende kenmerken heeft:  

* Hallo-inhoud wordt gedeeld over meerdere exemplaren van de virtuele machine (VM) van Hallo web-app.
* Hallo inhoud duurzaam en kan worden gewijzigd door het uitvoeren van web-apps.
* Logboekbestanden en diagnostische gegevensbestanden zijn beschikbaar onder Hallo dezelfde gedeelde map met inhoud.
* Publiceren van nieuwe inhoud rechtstreeks updates Hallo map met inhoud. U kunt onmiddellijk weergave Hallo dezelfde inhoud via Hallo SCM-website en Hallo actieve WebApp (doorgaans bij sommige technologieën zoals ASP.NET een web-app herstart initiëren wijzigingen tooget Hallo meest recente inhoud van sommige bestanden).

Bij veel WebApps gebruik maken van een of meer van deze functies, zijn sommige web-apps hoeft alleen maar een hoge prestaties, alleen-lezen store voor inhoud die ze vanuit met hoge beschikbaarheid uitvoeren kunnen. Deze apps kunnen profiteren van een VM-exemplaar van een specifieke lokale cache.

Hallo lokale Cache in Azure App Service-functie biedt een webweergave van de rol van uw inhoud. Deze inhoud is een cache voor write-maar-negeren inhoud van de opslag die asynchroon wordt gemaakt bij het opstarten van de site. Wanneer Hallo cache klaar is, is Hallo site geschakelde toorun tegen Hallo in de cache opgeslagen inhoud. Web-apps die worden uitgevoerd op de lokale Cache hebben Hallo volgende voordelen:

* Ze zijn gebaseerd toolatencies die zich voordoen wanneer ze toegang krijgen inhoud op Azure Storage tot.
* Ze zijn gebaseerd toohello geplande upgrades of ongeplande downtime en eventuele andere storingen met Azure Storage die plaatsvinden op servers die de inhoudsshare Hallo dienen.
* Ze hebben minder app opnieuw wordt opgestart vanwege toostorage share wijzigingen.

## <a name="how-local-cache-changes-hello-behavior-of-app-service"></a>Hoe Hallo gedrag van App Service wordt gewijzigd in lokale Cache
* Hallo lokale cache is een kopie van Hallo KCC/site en /siteextensions mappen van Hallo web-app. Het is gemaakt op Hallo lokale VM-exemplaar op web-app starten. Hallo grootte van de lokale cache Hallo per web-app is beperkt too300 MB door standaard, maar u kunt de up too2 GB.
* Hallo lokale cache is alleen-lezen. Echter worden eventuele wijzigingen verwijderd wanneer de web-app Hallo virtuele machines verplaatst of opnieuw wordt opgestart. U moet lokale Cache niet gebruiken voor apps die bedrijfskritieke gegevens opslaan op Hallo inhoudsarchief.
* Web-apps kunnen blijven toowrite-logboekbestanden en diagnostische gegevens net zo uit als op dit moment. Logboekbestanden en gegevens, maar worden lokaal opgeslagen op Hallo VM. Vervolgens worden ze gekopieerd via periodiek toohello gedeelde store voor inhoud. Hallo kopiëren toohello shared content store is een gunstigste moeite--write-back-maakt mogelijk verloren gegaan vanwege tooa plotselinge vastlopen van een VM-exemplaar.
* Er is een wijziging in de mapstructuur Hallo Hallo logboekbestanden en-mappen van de gegevens voor web-apps die gebruikmaken van de lokale Cache. Er zijn nu submappen Hallo logboekbestanden en de gegevens opslagmap die Hallo naamgevingspatroon van 'unieke id' + tijdstempel volgen. Elk van de submappen Hallo komt overeen met tooa VM-instantie waar Hallo web-app wordt uitgevoerd of is uitgevoerd.  
* Gedeeld inhoudsarchief toohello publiceren Publishing wijzigingen toohello web-app via een van de publicatie mechanismen Hallo. Dit is standaard omdat we willen Hallo inhoud toobe duurzame gepubliceerd. toorefresh hello lokale cache van Hallo web-app, moet deze toobe opnieuw gestart. Dit een uitzonderlijk groot stap lijkt? toomake hello lifecycle naadloze, Zie Hallo verderop in dit artikel.
* De lokale cache toohello verwijst D:\Home. D:\Local blijven toohello tijdelijke VM specifieke opslag te wijzen.
* Hallo inhoud standaardweergave van Hallo SCM site blijft toobe die Hallo gedeeld inhoudsarchief.

## <a name="enable-local-cache-in-app-service"></a>Lokale Cache in App Service inschakelen
U configureren lokale Cache met behulp van een combinatie van gereserveerde app-instellingen. U kunt deze app-instellingen configureren met behulp van de volgende methoden Hallo:

* [Azure Portal](#Configure-Local-Cache-Portal)
* [Azure Resource Manager](#Configure-Local-Cache-ARM)

### <a name="configure-local-cache-by-using-hello-azure-portal"></a>Lokale Cache configureren met behulp van hello Azure-portal
<a name="Configure-Local-Cache-Portal"></a>

U kunt lokale Cache inschakelen op basis van de per-web-app met behulp van deze appinstelling:`WEBSITE_LOCAL_CACHE_OPTION` = `Always`  

![Azure portal-app-instellingen: lokale Cache](media/app-service-local-cache/app-service-local-cache-configure-portal.png)

### <a name="configure-local-cache-by-using-azure-resource-manager"></a>Lokale Cache configureren met behulp van Azure Resource Manager
<a name="Configure-Local-Cache-ARM"></a>

```

...

{
    "apiVersion": "2015-08-01",
    "type": "config",
    "name": "appsettings",
    "dependsOn": [
        "[resourceId('Microsoft.Web/sites/', variables('siteName'))]"
    ],

"properties": {
        "WEBSITE_LOCAL_CACHE_OPTION": "Always",
        "WEBSITE_LOCAL_CACHE_SIZEINMB": "300"
    }
}

...
```

## <a name="change-hello-size-setting-in-local-cache"></a>Hallo grootte instelling wijzigen in lokale Cache
De grootte van de lokale cache Hallo is standaard **300 MB**. Dit omvat Hallo KCC/site en /siteextensions-mappen die zijn gekopieerd van Hallo content store, evenals alle mappen logboeken en gegevens lokaal gemaakt. tooincrease dit beperken, Hallo app-instelling gebruiken `WEBSITE_LOCAL_CACHE_SIZEINMB`. U kunt Hallo tekengrootte up te maken van**2 GB** (2000 MB) per web-app.

## <a name="best-practices-for-using-app-service-local-cache"></a>Aanbevolen procedures voor het gebruik van lokale App Service-Cache
Het is raadzaam dat u de lokale Cache in combinatie met Hallo gebruiken [Faseringsomgevingen](../app-service-web/web-sites-staged-publishing.md) functie.

* Hallo toevoegen *een tijdelijke* app-instelling `WEBSITE_LOCAL_CACHE_OPTION` met Hallo waarde `Always` tooyour **productie** sleuf. Als u `WEBSITE_LOCAL_CACHE_SIZEINMB`, ook toevoegen als een instelling voor een tijdelijke tooyour-productiesite.
* Maak een **fasering** sleuf en tooyour Staging-sleuf publiceren. Hallo staging-sleuf toouse lokale Cache tooenable de levensduur van een naadloze build-implementeren-test voor fasering als u Hallo voordelen van de lokale Cache voor de productiesite Hallo krijgt doorgaans niet wordt ingesteld.
* Test uw site op basis van de Staging-site.  
* Wanneer u klaar bent, geven een [wisselen](../app-service-web/web-sites-staged-publishing.md#Swap) sleuven tussen uw fasering en productie.  
* Instellingen voor een tijdelijke bevatten naam en een tijdelijke tooa sleuf. Wanneer Hallo Staging-sleuf opgehaald gewisseld naar de productie, wordt deze dus Hallo lokale Cache app-instellingen overnemen. Hallo verwisseld zojuist productie sleuf wordt uitgevoerd op basis van de lokale cache Hallo na een paar minuten en wordt opgewarmd als onderdeel van sleuf opwarmtijd na wisselen. Wanneer Hallo sleuf wisselen voltooid is, wordt dus de productiesite uitgevoerd tegen Hallo lokale cache.

## <a name="frequently-asked-questions-faq"></a>Veelgestelde vragen
### <a name="how-can-i-tell-if-local-cache-applies-toomy-web-app"></a>Hoe kan ik zien of lokale Cache toomy web-app van toepassing is?
Als uw web-app een krachtige, betrouwbare inhoudsarchief moet geen Hallo inhoudsarchief toowrite kritieke gegevens tijdens runtime gebruikt en minder dan 2 GB in de totale grootte is, is Hallo antwoord 'Ja'! tooget hello totale grootte van de mappen KCC/site en /siteextensions, kunt u site-uitbreiding Hallo "Azure Web Apps gebruik van de schijf".  

### <a name="how-can-i-tell-if-my-site-has-switched-toousing-local-cache"></a>Hoe kan ik zien als Mijn site toousing lokale Cache is ingeschakeld?
Als u de lokale cachefunctie Hallo met Faseringsomgevingen, wisselen Hallo kan pas worden voltooid lokale Cache is opgewarmd. toocheck als uw site wordt uitgevoerd op basis van de lokale Cache, kunt u Hallo worker proces omgevingsvariabele controleren `WEBSITE_LOCALCACHE_READY`. Hallo-instructies gebruiken op Hallo [worker proces omgevingsvariabele](https://github.com/projectkudu/kudu/wiki/Process-Threads-list-and-minidump-gcdump-diagsession#process-environment-variable) pagina tooaccess Hallo worker proces omgevingsvariabele op meerdere exemplaren.  

### <a name="i-just-published-new-changes-but-my-web-app-does-not-seem-toohave-them-why"></a>Ik alleen nieuwe wijzigingen hebt gepubliceerd, maar mijn web-app niet lijkt toohave ze. Hoe komt dat?
Als uw web-app gebruikmaakt van lokale Cache, moet u toorestart uw site tooget Hallo meest recente wijzigingen. Niet wilt dat toopublish wijzigingen tooa productiesite? Zie Hallo sleuf opties in Hallo vorige best practices sectie.

### <a name="where-are-my-logs"></a>Waar bevinden zich mijn Logboeken?
Met de lokale Cache zien uw logboeken en gegevensmappen er iets anders. Echter hello structuur van uw blijft submappen Hallo dezelfde, maar, Hallo submappen zijn surfen onder een submap met de Hallo 'unieke id van VM-' + tijdstempel.

### <a name="i-have-local-cache-enabled-but-my-web-app-still-gets-restarted-why-is-that-i-thought-local-cache-helped-with-frequent-app-restarts"></a>Ik heb lokale Cache ingeschakeld, maar nog steeds mijn web-app wordt gestart. Waarom is dat? Ik beschouwd in dat lokale Cache heeft geholpen frequente app opnieuw wordt opgestart.
Lokale Cache voorkomen dat opslag-gerelateerde web-app opnieuw wordt opgestart. Uw web-app kan echter nog steeds opnieuw wordt opgestart ondergaan tijdens geplande infrastructuur upgrades Hallo VM. Hallo moet algehele app opnieuw wordt opgestart die met de lokale Cache ingeschakeld optreden minder.

### <a name="does-local-cache-exclude-any-directories-from-being-copied-toohello-faster-local-drive"></a>Lokale Cache komt uitsluiten alle mappen worden gekopieerd toohello sneller lokale schijf?
Als onderdeel van Hallo stap die Hallo opslag inhoud kopieert worden een map met de naam opslagplaats uitgesloten. Dit helpt met scenario's waar de inhoud van uw site een resourcebeheerbibliotheek die niet nodig in bewerking van de dag tooday van Hallo web-app zijn kan bevatten. 
