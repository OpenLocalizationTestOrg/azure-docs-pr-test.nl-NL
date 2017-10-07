---
title: Ongeldige gateway aaaFix 502, 503 service niet beschikbaar fouten | Microsoft Docs
description: Problemen oplossen met 502 Slechte gateway en 503 service niet beschikbaar fouten in uw web-app in Azure App Service wordt gehost.
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: top-support-issue
keywords: 502 Slechte gateway 503 service niet beschikbaar, 503-fout, fout 502
ms.assetid: 51cd331a-a3fa-438f-90ef-385e755e50d5
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2016
ms.author: cephalin
ms.openlocfilehash: d9d8dcddaac930967a2e8d2bfd8cad09e6824c17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-http-errors-of-502-bad-gateway-and-503-service-unavailable-in-your-azure-web-apps"></a>HTTP-fouten van '502 Slechte gateway' en '503 service niet beschikbaar' in uw Azure-web-apps
'502 Slechte gateway' en '503 service niet beschikbaar' zijn veelvoorkomende fouten in uw web-app gehost in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714). In dit artikel helpt u bij deze fouten oplossen.

Als u meer hulp op elk gewenst moment in dit artikel nodig hebt, kunt u raadplegen hello Azure deskundigen op [hello Azure MSDN en forums Stack Overflow Hallo](https://azure.microsoft.com/support/forums/). U kunt ook kunt u ook een incident voor ondersteuning van Azure bestand. Ga toohello [ondersteuning van Azure site](https://azure.microsoft.com/support/options/) en klik op **Get Support**.

## <a name="symptom"></a>Symptoom
Wanneer u de web-app toohello bladert, wordt een HTTP '502 Slechte Gateway' fout of een HTTP-fout '503 Service niet beschikbaar'.

## <a name="cause"></a>Oorzaak
Dit probleem wordt vaak veroorzaakt door problemen met toepassingen niveau, zoals:

* aanvragen duurt lang
* toepassing met hoge geheugen/CPU
* de toepassing is gecrasht vanwege tooan uitzondering.

## <a name="troubleshooting-steps-toosolve-502-bad-gateway-and-503-service-unavailable-errors"></a>Het oplossen van stappen toosolve '502 Slechte gateway' en '503 service niet beschikbaar'-fouten
Het oplossen van problemen kan worden onderverdeeld in drie verschillende taken in opeenvolgende volgorde:

1. [Bekijken en controleren van gedrag van toepassingen](#observe)
2. [Gegevens verzamelen](#collect)
3. [Hallo probleem verhelpen](#mitigate)

[App Service Web Apps](/services/app-service/web/) biedt verschillende opties bij elke stap.

<a name="observe" />

### <a name="1-observe-and-monitor-application-behavior"></a>1. Bekijken en controleren van gedrag van toepassingen
#### <a name="track-service-health"></a>Servicestatus bijhouden
Microsoft Azure publicizes telkens wanneer er een service wordt onderbroken of de prestaties nadelig beïnvloeden is. U kunt Hallo status van Hallo service bijhouden op Hallo [Azure Portal](https://portal.azure.com/). Zie voor meer informatie [bijhouden servicestatus](../monitoring-and-diagnostics/insights-service-health.md).

#### <a name="monitor-your-web-app"></a>Uw web-app bewaken
Deze optie kunt u toofind uit als uw toepassing problemen ondervindt. Klik in de blade van uw web-app op Hallo **aanvragen en fouten** tegel. Hallo **metriek** blade ziet u alle Hallo metrische gegevens u kunt toevoegen.

Aantal Hallo metrische gegevens die u toomonitor voor uw web-app wilt mogelijk

* Gemiddelde geheugen werkset
* Gemiddelde reactietijd
* CPU-tijd
* Geheugen-werkset
* Aanvragen

![Monitor voor web-app voor het oplossen van HTTP-fouten van 502 Slechte gateway en 503 service niet beschikbaar](./media/app-service-web-troubleshoot-HTTP-502-503/1-monitor-metrics.png)

Zie voor meer informatie:

* [Web-Apps bewaken in Azure App Service](web-sites-monitor.md)
* [Waarschuwingen ontvangen](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)

<a name="collect" />

### <a name="2-collect-data"></a>2. Gegevens verzamelen
#### <a name="use-hello-azure-app-service-support-portal"></a>Hello Azure App Service-ondersteuning Portal gebruiken
Web Apps biedt Hallo mogelijkheid tootroubleshoot problemen gerelateerde tooyour web-app door te kijken HTTP Logboeken, gebeurtenislogboeken proces dumpbestanden en meer. U toegang hebt tot deze informatie met onze portal ondersteuning op **http://&lt;uw app-naam >.scm.azurewebsites.net/Support**

Hallo-portal voor ondersteuning van Azure App Service biedt drie afzonderlijke tabbladen toosupport Hallo drie stappen van een algemeen scenario voor het oplossen van problemen:

1. Huidige gedrag observeren
2. Door het verzamelen van diagnostische gegevens en Hallo ingebouwde analyzers analyseren
3. Beperken

Als het probleem Hallo nu zich voordoet, klikt u op **analyseren** > **Diagnostics** > **onderzoeken nu** toocreate een diagnostische sessie voor u verzamelt die HTTP zich aanmeldt, Logboeken, geheugen dumpbestanden, PHP-foutenlogboek en PHP-proces rapport.

Zodra het Hallo-gegevens worden verzameld, wordt ook een analyse uitgevoerd op Hallo gegevens en bieden u een HTML-rapport.

Als u wilt dat toodownload Hallo gegevens, standaard, zou dit worden opgeslagen in Hallo D:\home\data\DaaS map.

Zie voor meer informatie over de ondersteuning van Azure App Service-portal Hallo [nieuwe Updates tooSupport Site-uitbreiding voor Azure Websites](https://azure.microsoft.com/blog/new-updates-to-support-site-extension-for-azure-websites).

#### <a name="use-hello-kudu-debug-console"></a>Hallo Kudu-Console voor foutopsporing gebruiken
Web-Apps wordt geleverd met een Foutopsporingsconsole die u gebruiken kunt voor foutopsporing, verkennen, het uploaden van bestanden, evenals de JSON-eindpunten voor het ophalen van informatie over uw omgeving. Dit wordt genoemd, Hallo *Kudu-Console* of Hallo *SCM Dashboard* voor uw web-app.

U kunt toegang krijgen tot dit dashboard toohello koppeling gaat **https://&lt;uw app-naam >.scm.azurewebsites.net/**.

Enkele van de Kudu verschaft Hallo zaken zijn:

* omgevingsinstellingen voor uw toepassing
* logboekstream
* diagnostische dump
* fouten opsporen console waarin u Powershell-cmdlets en basic DOS-opdrachten kunt uitvoeren.

Een andere handige functie van Kudu is dat, als uw toepassing die eerste kans uitzonderingen, kunt u Kudu en Hallo SysInternals-hulpprogramma Procdump toocreate geheugendumps. Deze geheugendumps momentopnamen van het Hallo-proces en vaak kunt u meer gecompliceerde problemen oplossen met uw web-app.

Zie voor meer informatie over functies die beschikbaar zijn in Kudu [Azure Websites on line hulpmiddelen die u moet weten over](https://azure.microsoft.com/blog/windows-azure-websites-online-tools-you-should-know-about/).

<a name="mitigate" />

### <a name="3-mitigate-hello-issue"></a>3. Hallo probleem verhelpen
#### <a name="scale-hello-web-app"></a>Schaal Hallo web-app
In Azure App Service kunt voor betere prestaties en doorvoer, u aanpassen Hallo schaal waarmee u uw toepassing uitvoert. Schalen van een web-app omvat twee gerelateerde acties: uw App Service plan tooa hogere prijscategorie en bepaalde instellingen configureren nadat u hebt gekozen toohello hoger prijscategorie te wijzigen.

Zie voor meer informatie over het schalen [schalen van een web-app in Azure App Service](web-sites-scale.md).

U kunt bovendien kiezen toorun uw toepassing op meer dan één exemplaar. Dit niet alleen biedt u meer mogelijkheden voor verwerking, maar biedt u eveneens bepaalde hoeveelheid fouttolerantie. Als hello proces uitgeschakeld op één exemplaar wordt, blijven hello andere exemplaar nog steeds voldoen aan aanvragen.

U kunt Hallo toobe handmatig of automatisch schalen instellen.

#### <a name="use-autoheal"></a>Gebruik AutoHeal
AutoHeal wordt gerecycled werkproces Hallo voor uw app op basis van de instellingen die u kiest (zoals wijzigingen in de configuratie, aanvragen, op basis van geheugen limieten of Hallo tijd nodig tooexecute een aanvraag). Meestal Hallo is recyclen Hallo proces Hallo snelste manier toorecover van een probleem. Hoewel u altijd opnieuw Hallo web-app uit rechtstreeks in Azure Portal hello opstarten kunt, wordt AutoHeal het automatisch voor u doen. Toodo hoeft u sommige triggers in Hallo root web.config voor uw web-app toevoegen. Opmerking dat deze instellingen zijn werk gaat in Hallo dezelfde manier zelfs als uw toepassing niet een .net een is.

Zie voor meer informatie [Azure websites automatisch herstel](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites/).

#### <a name="restart-hello-web-app"></a>Hallo-web-app starten
Dit is vaak het eenvoudigste manier toorecover Hallo eenmalige problemen. Op Hallo [Azure Portal](https://portal.azure.com/), op de blade van uw web-app en u hebt Hallo opties toostop of opnieuw opstarten van uw app.

 ![opnieuw opstarten app toosolve HTTP-fouten van 502 Slechte gateway en 503 service niet beschikbaar](./media/app-service-web-troubleshoot-HTTP-502-503/2-restart.png)

U kunt ook uw web-app met Azure Powershell beheren. Zie [Azure PowerShell gebruiken met Azure Resource Manager](../powershell-azure-resource-manager.md) voor meer informatie.

