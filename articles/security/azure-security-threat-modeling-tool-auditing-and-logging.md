---
title: aaaAuditing en logboekregistratie - Microsoft Threat Modeling Tool - Azure | Microsoft Docs
description: oplossingen voor bedreigingen die worden weergegeven in Hallo Threat Modeling hulpprogramma
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: f28988833eba251b6ceb8bbd47cde37e871af609
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-auditing-and-logging--mitigations"></a>Beveiliging Frame: Controle en logboekregistratie | Oplossingen 
| Product/Service | Artikel |
| --------------- | ------- |
| **Dynamics CRM**    | <ul><li>[Gevoelige entiteiten in uw oplossing voor het identificeren en te implementeren controle van wijzigingen](#sensitive-entities)</li></ul> |
| **Webtoepassing** | <ul><li>[Zorg ervoor dat voor controle en logboekregistratie wordt afgedwongen op Hallo-toepassing](#auditing)</li><li>[Zorg ervoor dat logrotatie en scheiding aanwezig zijn](#log-rotation)</li><li>[Zorg ervoor dat de toepassing hello registreert niet gevoelige gebruikersgegevens](#log-sensitive-data)</li><li>[Zorg ervoor dat u controle- en logboekbestanden beperkte toegang hebben](#log-restricted-access)</li><li>[Zorg ervoor dat de gebruiker Management gebeurtenissen worden geregistreerd](#user-management)</li><li>[Zorg ervoor dat de systeem Hallo ingebouwde beveiliging tegen misbruik](#inbuilt-defenses)</li><li>[Logboekregistratie van diagnostische gegevens van web-apps in Azure App Service](#diagnostics-logging)</li></ul> |
| **Database** | <ul><li>[Zorg ervoor dat de controle van de aanmelding is ingeschakeld op SQL Server](#identify-sensitive-entities)</li><li>[Detectie van dreigingen in Azure SQL inschakelen](#threat-detection)</li></ul> |
| **Azure Storage** | <ul><li>[Gebruik Azure Storage Analytics tooaudit toegang van Azure Storage](#analytics)</li></ul> |
| **WCF** | <ul><li>[Voldoende logboekregistratie implementeren](#sufficient-logging)</li><li>[Afhandeling van voldoende Audit fout implementeren](#audit-failure-handling)</li></ul> |
| **Web-API** | <ul><li>[Zorg ervoor dat de controle en logboekregistratie wordt afgedwongen voor Web-API](#logging-web-api)</li></ul> |
| **Veld IoT Gateway** | <ul><li>[Zorg ervoor dat de juiste voor controle en logboekregistratie wordt afgedwongen voor Veldgateway](#logging-field-gateway)</li></ul> |
| **IoT-Cloudgateway** | <ul><li>[Zorg ervoor dat de juiste voor controle en logboekregistratie wordt afgedwongen voor Cloudgateway](#logging-cloud-gateway)</li></ul> |

## <a id="sensitive-entities"></a>Gevoelige entiteiten in uw oplossing voor het identificeren en te implementeren controle van wijzigingen

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Dynamics CRM | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen**                   | Entiteiten in uw oplossing met gevoelige gegevens identificeren en te implementeren op deze entiteiten en velden controle van wijzigingen |

## <a id="auditing"></a>Zorg ervoor dat voor controle en logboekregistratie wordt afgedwongen op Hallo-toepassing

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen**                   | Inschakelen van controle en logboekregistratie voor alle onderdelen. Controlelogboeken moeten gebruikerscontext vastleggen. Alle belangrijke gebeurtenissen identificeren en deze gebeurtenissen. Centrale logboekregistratie implementeren |

## <a id="log-rotation"></a>Zorg ervoor dat logrotatie en scheiding aanwezig zijn

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen**                   | <p>Logrotatie is een geautomatiseerd proces gebruikt in Systeembeheer waarin datum logboekbestanden worden gearchiveerd. Servers die vaak grote toepassingen uitvoeren Meld elke aanvraag: Hallo gezicht van zware Logboeken, logrotatie is een manier toolimit Hallo totale grootte van Hallo logboeken terwijl u nog steeds analyse van recente gebeurtenissen. </p><p>Logboek scheiding in feite betekent dat u toostore uw logboekbestanden op een andere partitie als waar uw OS/toepassing wordt uitgevoerd op in de volgorde tooavert Denial of service aanvallen of Hallo downgraden van de prestaties van uw toepassing</p>|

## <a id="log-sensitive-data"></a>Zorg ervoor dat de toepassing hello registreert niet gevoelige gebruikersgegevens

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen**                   | <p>U kunt geen gevoelige gegevens dat een gebruiker tooyour site verzendt zich niet aanmelden controleren Controleer of opzettelijk logboekregistratie, evenals bijwerkingen veroorzaakt door problemen van ontwerp. Voorbeelden van gevoelige gegevens omvatten:</p><ul><li>De referenties van gebruiker</li><li>Sociaal-fiscaal nummer of andere identiteitsgegevens</li><li>Creditcardnummers of andere financiële gegevens</li><li>Statusgegevens</li><li>Persoonlijke sleutels of andere gegevens die gebruikt toodecrypt versleutelde gegevens worden kan</li><li>Informatie van systemen of toepassingen die kan worden gebruikt toomore aanvallen effectief Hallo-toepassing</li></ul>|

## <a id="log-restricted-access"></a>Zorg ervoor dat u controle- en logboekbestanden beperkte toegang hebben

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen**                   | <p>Controleer tooensure toegang rechten toolog bestanden op de juiste wijze zijn ingesteld. Toepassing accounts moeten alleen-schrijven toegang en operators en ondersteuningspersoneel alleen-lezen toegang moeten hebben, indien nodig.</p><p>Administrators-accounts zijn alleen Hallo-accounts die volledige toegang moeten hebben. Controleer dat Windows ACL voor logboek bestanden tooensure ze zijn correct beperkt:</p><ul><li>Accounts van de toepassing moeten alleen-schrijven toegang hebben</li><li>Operators en iemand van ondersteuning moeten alleen-lezen toegang hebben indien nodig</li><li>Beheerders zijn Hallo alleen accounts volledige toegang hebben</li></ul>|

## <a id="user-management"></a>Zorg ervoor dat de gebruiker Management gebeurtenissen worden geregistreerd

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen**                   | <p>Zorg dat de toepassing hello bewaakt gebeurtenissen voor het beheer van gebruikers zoals geslaagde en mislukte aanmeldingen, wachtwoorden opnieuw instellen, wijzigen van wachtwoorden, accountvergrendeling, gebruikersregistratie. Hierdoor helpt toodetect en toopotentially verdacht gedrag reageren. Deze kan gegevens ook toogather operations; bijvoorbeeld: tootrack wie toegang heeft tot de toepassing hello</p>|

## <a id="inbuilt-defenses"></a>Zorg ervoor dat de systeem Hallo ingebouwde beveiliging tegen misbruik

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen**                   | <p>Besturingselementen moeten aanwezig zijn die beveiligingsuitzondering in geval van een toepassing misbruik genereert. Bijvoorbeeld, als validatie voor invoer geïmplementeerd is en een hacker probeert tooinject schadelijke code die komt niet overeen met reguliere expressie hello, een beveiligingsuitzondering kan worden gegenereerd die een aanduiden system misbruik kan zijn</p><p>Bijvoorbeeld: u wordt aangeraden toohave beveiligingsuitzonderingen vastgelegd en acties die worden uitgevoerd voor Hallo problemen te volgen:</p><ul><li>Validatie voor invoer</li><li>CSRF schendingen</li><li>Beveiligingsaanvallen (bovengrens voor het aantal aanvragen per gebruiker per resource)</li><li>Bestand uploaden schendingen</li><ul>|

## <a id="diagnostics-logging"></a>Logboekregistratie van diagnostische gegevens van web-apps in Azure App Service

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | EnvironmentType - Azure |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | <p>Azure biedt ingebouwde diagnostics tooassist met foutopsporing van een App Service-web-app. Dit geldt ook tooAPI apps en mobiele apps. App Service-web-apps bieden diagnostische functionaliteit voor logboekinformatie van zowel Hallo-webserver en Hallo-webtoepassing.</p><p>Deze zijn logisch verdeeld in de web server diagnostics en application diagnostics</p>|

## <a id="identify-sensitive-entities"></a>Zorg ervoor dat de controle van de aanmelding is ingeschakeld op SQL Server

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Database | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [Aanmelding controle configureren](https://msdn.microsoft.com/library/ms175850.aspx) |
| **Stappen** | <p>Server aanmelding Databasecontrole moet zijn ingeschakeld toodetect/Bevestig het wachtwoord raden aanvallen. Het is belangrijk toocapture mislukte aanmeldingspogingen. Vastleggen van beide geslaagde en mislukte aanmeldingspogingen biedt een extra voordeel tijdens forensische onderzoeken</p>|

## <a id="threat-detection"></a>Detectie van dreigingen in Azure SQL inschakelen

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Database | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | SQL Azure |
| **Kenmerken**              | SQL-versie - V12 |
| **Verwijzingen**              | [Aan de slag met detectie van dreigingen van SQL Database](https://azure.microsoft.com/documentation/articles/sql-database-threat-detection-get-started/)|
| **Stappen** |<p>Detectie van dreigingen detecteert afwijkende databaseactiviteiten die wijzen op mogelijke bedreigingen toohello database met. Het biedt een nieuwe laag van beveiliging, waarbij kan klanten toodetect en hierop reageren toopotential bedreigingen wanneer deze zich voordoen doordat beveiligingswaarschuwingen op vreemde activiteiten worden gedetecteerd.</p><p>Gebruikers kunnen verkennen Hallo verdachte gebeurtenissen met Azure SQL Database Auditing toodetermine als ze het gevolg zijn van een tooaccess poging schenden of misbruik van gegevens in Hallo-database.</p><p>Detectie van dreigingen maakt het eenvoudig tooaddress potentiële bedreigingen toohello database zonder Hallo nodig toobe een expert beveiliging of systemen bewaking van de geavanceerde beveiliging beheren</p>|

## <a id="analytics"></a>Gebruik Azure Storage Analytics tooaudit toegang van Azure Storage

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Azure Storage | 
| **SDL-fase**               | Implementatie |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t. |
| **Verwijzingen**              | [Met behulp van Storage Analytics toomonitor autorisatie type](https://azure.microsoft.com/documentation/articles/storage-security-guide/#storage-analytics) |
| **Stappen** | <p>Voor elke storage-account kan een Azure Storage Analytics tooperform logboekregistratie inschakelen en metrische gegevens opslaan. Hallo storage analytics logboeken bieden belangrijke informatie zoals de verificatiemethode die door iemand wordt gebruikt wanneer ze toegang hebben tot opslag.</p><p>Dit is heel nuttig als u toegang toostorage nauw zijn beveiligen. Bijvoorbeeld in Blob Storage kunt u alle Hallo containers tooprivate instellen en implementeren van Hallo gebruik van een SAS-service in uw toepassingen. U kunt vervolgens controleren Hallo Logboeken regelmatig toosee als uw blobs worden geopend met behulp van Hallo toegangscodes voor opslag, dit kunnen duiden op een schending van beveiliging, of als Hallo blobs openbaar zijn, maar ze mag niet.</p>|

## <a id="sufficient-logging"></a>Voldoende logboekregistratie implementeren

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | WCF | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | .NET framework |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Voeg Koninkrijk](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Stappen** | <p>Hallo gebrek aan een juiste audittrail na een beveiligingsincident kunt forensische inspanningen belemmeren. Windows Communication Foundation (WCF) biedt Hallo mogelijkheid toolog geslaagd en/of mislukte verificatiepogingen.</p><p>Logboekregistratie van mislukte verificatiepogingen kan beheerders van mogelijke aanvallen met brute kracht waarschuwing. Op deze manier kunt vastleggen van gebeurtenissen voor geslaagde verificatie bieden een handig audittrail bij een legitieme account is geknoeid. Inschakelen van WCF-service-onderdeel voor controle van beveiliging |

### <a name="example"></a>Voorbeeld
Hallo Hier volgt een voorbeeldconfiguratie met de controle is ingeschakeld
```
<system.serviceModel>
    <behaviors>
        <serviceBehaviors>
            <behavior name=""NewBehavior"">
                <serviceSecurityAudit auditLogLocation=""Default""
                suppressAuditFailure=""false"" 
                serviceAuthorizationAuditLevel=""SuccessAndFailure""
                messageAuthenticationAuditLevel=""SuccessAndFailure"" />
                ...
            </behavior>
        </servicebehaviors>
    </behaviors>
</system.serviceModel>
```

## <a id="audit-failure-handling"></a>Afhandeling van voldoende Audit fout implementeren

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | WCF | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | .NET framework |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Voeg Koninkrijk](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Stappen** | <p>Ontwikkelde oplossing is geconfigureerd niet toogenerate een uitzondering toowrite tooan controlelogboek is mislukt. Als WCF is geconfigureerd niet toothrow een uitzondering opgeleverd bij dit niet kan toowrite tooan controlelogboek, Hallo programma wordt niet gewaarschuwd voor Hallo mislukt en de controle van kritieke beveiligingsgebeurtenissen mogelijk niet plaatsvinden.</p>|

### <a name="example"></a>Voorbeeld
Hallo `<behavior/>` element van Hallo WCF-configuratiebestand onderstaande Hiermee geeft u WCF toonot toepassing hello waarschuwen als WCF toowrite tooan controlelogboek is mislukt.
````
<behaviors>
    <serviceBehaviors>
        <behavior name="NewBehavior">
            <serviceSecurityAudit auditLogLocation="Application"
            suppressAuditFailure="true"
            serviceAuthorizationAuditLevel="Success"
            messageAuthenticationAuditLevel="Success" />
        </behavior>
    </serviceBehaviors>
</behaviors>
````
Configureer WCF toonotify Hallo programma wanneer u het controlelogboek voor niet kan toowrite tooan is. Hallo programma heeft een alternatieve notification-schema in place tooalert Hallo organisatie audittrails niet wordt behouden. 

## <a id="logging-web-api"></a>Zorg ervoor dat de controle en logboekregistratie wordt afgedwongen voor Web-API

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Web-API | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | Inschakelen van controle en logboekregistratie op Web-API's. Controlelogboeken moeten gebruikerscontext vastleggen. Alle belangrijke gebeurtenissen identificeren en deze gebeurtenissen. Centrale logboekregistratie implementeren |

## <a id="logging-field-gateway"></a>Zorg ervoor dat de juiste voor controle en logboekregistratie wordt afgedwongen voor Veldgateway

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Veld IoT Gateway | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | <p>Als meerdere apparaten verbinding tooa Veldgateway, zorg ervoor dat verbindingspogingen en verificatiestatus (slagen of mislukken) voor afzonderlijke apparaten zijn geregistreerd en beheerd op Hallo Veldgateway.</p><p>Ook in gevallen waar Veldgateway is het bijhouden van Hallo IoT Hub-referenties voor afzonderlijke apparaten, zorg ervoor dat de controle wordt uitgevoerd wanneer deze referenties worden opgehaald. Ontwikkel een proces tooperiodically uploaden Hallo logboeken tooAzure IoT Hub/opslag voor het bewaren van de lange termijn.</p> |

## <a id="logging-cloud-gateway"></a>Zorg ervoor dat de juiste voor controle en logboekregistratie wordt afgedwongen voor Cloudgateway

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | IoT-Cloudgateway | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [Inleiding tooIoT Hub bewerkingen controleren](https://azure.microsoft.com/documentation/articles/iot-hub-operations-monitoring/) |
| **Stappen** | <p>Ontwerpen voor het verzamelen en opslaan van controlegegevens die zijn verzameld via IoT Hub Operations Monitoring. Hallo na controle categorieën inschakelen:</p><ul><li>Bewerkingen voor apparaat-id</li><li>Apparaat-naar-cloud-communicatie</li><li>Cloud-naar-apparaat communicatie</li><li>Verbindingen</li><li>Uploaden van bestanden</li></ul>|
