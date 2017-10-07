---
title: aaaConfigure web-apps in Azure App Service
description: Hoe tooconfigure een web-app in Azure App Services
services: app-service\web
documentationcenter: 
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9af8a367-7d39-4399-9941-b80cbc5f39a0
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 8697ab6f21cfeb470e11f0d82c68692d43142fc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-web-apps-in-azure-app-service"></a>Web-apps configureren in Azure App Service
Dit onderwerp wordt uitgelegd hoe een app met tooconfigure Hallo [Azure Portal].

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="application-settings"></a>Toepassingsinstellingen
1. In Hallo [Azure Portal]Open Hallo blade voor Hallo web-app.
2. Klik op **alle instellingen**.
3. Klik op **toepassingsinstellingen**.

![Toepassingsinstellingen][configure01]

Hallo **toepassingsinstellingen** blade bevat instellingen die zijn gegroepeerd onder verschillende categorieën.

### <a name="general-settings"></a>Algemene instellingen
**Framework-versies**. Deze opties instellen als uw app gebruikmaakt van een deze frameworks: 

* **.NET framework**: Set Hallo .NET framework-versie. 
* **PHP**: Set Hallo PHP-versie of **OFF** toodisable PHP. 
* **Java**: Selecteer Hallo Java-versie of **OFF** toodisable Java. Gebruik Hallo **webcontainer** optie toochoose tussen versies voor Tomcat en Jetty.
* **Python**: Selecteer Hallo Python-versie, of **OFF** toodisable Python.

Omwille van de technische Java inschakelen voor uw app wordt uitgeschakeld Hallo-opties voor .NET, PHP en Python.

<a name="platform"></a>
**Platform**. Hiermee selecteert u of uw web-app wordt uitgevoerd in een 32-bits of 64-bits-omgeving. Hallo 64-bits omgeving vereist Basic- of Standard-modus. Gratis en gedeelde modi altijd uitgevoerd in een 32-bits-omgeving.

**Web-Sockets**. Stel **ON** tooenable hello WebSocket-protocol; bijvoorbeeld, als uw web-app gebruikt [ASP.NET SignalR] of [socket.io].

<a name="alwayson"></a>
**AlwaysOn**. Standaard worden web-apps uit het geheugen verwijderd als ze een bepaalde tijd inactief zijn. Hiermee Hallo-systeem te besparen. In de modus voor Basic- of Standard, schakelt u **altijd op** tookeep Hallo app geladen alle Hallo tijd. Als uw app doorlopende webtaken wordt uitgevoerd of wordt uitgevoerd WebJobs geactiveerd met behulp van een expressie CRON, moet u inschakelen **altijd op**, of Hallo webtaken mogelijk niet betrouwbaar worden uitgevoerd.

**Beheerde Pipeline-versie**. Sets Hallo IIS [pipeline-modus]. Laat dit tooIntegrated (standaard Hallo) hebt ingesteld, tenzij u hebt een oudere app waarvoor een oudere versie van IIS is vereist.

**Automatisch wisselen**. Als u automatisch wisselen voor een implementatiesleuf inschakelt, wordt App Service automatisch Hallo web-app wisselen naar de productie wanneer u een update toothat sleuf pushen. Zie voor meer informatie [toostaging sleuven voor web-apps in Azure App Service implementeren](web-sites-staged-publishing.md).

### <a name="debugging"></a>Foutopsporing
**Foutopsporing op afstand**. Hiermee schakelt u foutopsporing op afstand. Wanneer dit is ingeschakeld, kunt u externe foutopsporingsprogramma Hallo in Visual Studio tooconnect direct tooyour web-app. Foutopsporing op afstand blijft ingeschakeld voor 48 uur. 

### <a name="app-settings"></a>App-instellingen
Deze sectie bevat de naam/waarde-paren die u web-app wordt geladen op start. 

* Voor .NET-toepassingen, deze instellingen zijn opgenomen in de configuratie van uw .NET `AppSettings` tijdens runtime, overschrijven bestaande instellingen. 
* PHP, Python, Java en knooppunt toepassingen hebben toegang tot deze instellingen als omgevingsvariabelen tijdens runtime. Twee omgevingsvariabelen zijn gemaakt voor elke app-instelling. een met Hallo door Hallo app instelling invoer en een andere met het voorvoegsel APPSETTING_ opgegeven. Beide Hallo bevatten dezelfde waarde.

### <a name="connection-strings"></a>Verbindingsreeksen
Tekenreeksen voor databaseverbindingen voor de gekoppelde resources. 

Voor .NET-toepassingen, deze verbindingsreeksen zijn opgenomen in de configuratie van uw .NET `connectionStrings` instellingen tijdens runtime, overschrijven bestaande vermeldingen waarbij Hallo sleutel gelijk is aan Hallo gekoppelde databasenaam. 

Deze instellingen zijn beschikbaar als omgevingsvariabelen tijdens runtime, voorafgegaan door het verbindingstype Hallo voor PHP, Python, knooppunt en Java-toepassingen. Hallo omgeving variabele voorvoegsels zijn als volgt: 

* SQL Server:`SQLCONNSTR_`
* MySQL:`MYSQLCONNSTR_`
* SQL-Database:`SQLAZURECONNSTR_`
* Aangepaste:`CUSTOMCONNSTR_`

Bijvoorbeeld, als u een MySql-verbindingsreeks zijn met de naam `connectionstring1`, deze zou worden geopend via de omgevingsvariabele Hallo `MYSQLCONNSTR_connectionString1`.

### <a name="default-documents"></a>Standaarddocumenten
Hallo standaarddocument is Hallo webpagina die wordt weergegeven op Hallo basis-URL voor een website.  Hallo eerste overeenkomende bestand in Hallo lijst wordt gebruikt. 

Modules dat route op basis van de URL in plaats voor statische inhoud, in welk geval er is geen standaarddocument zo mogelijk gebruik van web-apps.    

### <a name="handler-mappings"></a>Handlertoewijzingen
Gebruik dit gebied tooadd aangepast script processors toohandle aanvragen voor specifieke bestandsextensies. 

* **Extensie**. Hallo bestand extensie toobe verwerkt zoals *.php of handler.fcgi. 
* **Pad van de Processor script**. Hallo absolute pad van Hallo ScriptProcessor. Aanvragen toofiles die overeenkomen met de bestandsextensie Hallo worden door Hallo ScriptProcessor verwerkt. Hallo-pad gebruiken `D:\home\site\wwwroot` toorefer tooyour app-hoofdmap.
* **Extra argumenten**. Optionele opdrachtregelargumenten voor Hallo ScriptProcessor 

### <a name="virtual-applications-and-directories"></a>Virtuele toepassingen en mappen
tooconfigure virtuele toepassingen en mappen, geef alle virtuele mappen en de bijbehorende fysieke pad relatief toohello website hoofdmap. U kunt eventueel Hallo selecteren **toepassing** selectievakje toomark een virtuele map als een toepassing.

## <a name="enabling-diagnostic-logs"></a>Logboeken met diagnostische gegevens inschakelen
Diagnostische logboeken tooenable:

1. Klik op Hallo blade voor uw web-app **alle instellingen**.
2. Klik op **diagnostische logboeken**. 

Opties voor het schrijven van diagnostische logboeken vanuit een webtoepassing die ondersteuning biedt voor logboekregistratie: 

* **Toepassingslogboeken**. Schrijft toepassingslogboeken toohello-bestandssysteem. Logboekregistratie duurt gedurende een periode van 12 uur. 

**Niveau**. Wanneer toepassingslogboeken is ingeschakeld, geeft deze optie Hallo en de hoeveelheid gegevens die zijn opgenomen (fout, waarschuwing, informatie of uitgebreid).

**Logboekregistratie van webserver**. Logboeken worden opgeslagen in Hallo W3C extended logboekindeling. 

**Gedetailleerde foutberichten**. Bespaart foutberichten gedetailleerde htm-bestanden. Hallo-bestanden worden opgeslagen onder /LogFiles/DetailedErrors. 

**Tracering van mislukte aanvragen**. Logboeken is aanvragen tooXML bestanden mislukt. Hallo-bestanden worden opgeslagen onder/logboekbestanden/W3SVC*xxx*, waarbij xxx een unieke id. Deze map bevat een XSL-bestand en een of meer XML-bestanden. Zorg ervoor dat toodownload Hallo XSL-bestand omdat deze functionaliteit biedt voor het formatteren en inhoud van XML-bestanden Hallo Hallo filteren.

tooview Hallo-logboekbestanden, moet u referenties van de FTP-, als volgt:

1. Klik op Hallo blade voor uw web-app **alle instellingen**.
2. Klik op **implementatiereferenties**.
3. Voer een gebruikersnaam en wachtwoord.
4. Klik op **Opslaan**.

![Implementatiereferenties instellen][configure03]

Hallo volledige FTP-gebruikersnaam is 'app\username' waar *app* Hallo-naam van uw web-app. Hallo gebruikersnaam wordt vermeld in Hallo blade web-app onder **Essentials**.  

![FTP-implementatiereferenties][configure02]

## <a name="other-configuration-tasks"></a>Andere configuratietaken
### <a name="ssl"></a>SSL
U kunt SSL-certificaten voor een aangepast domein uploaden in de basis- of Standard-modus. Zie voor meer informatie [HTTPS inschakelen voor een web-app]. 

Klik op tooview uw geüploade certificaten **alle instellingen** > **aangepaste domeinen en SSL**.

### <a name="domain-names"></a>Domeinnamen
Aangepaste domeinnamen voor uw web-app toevoegen. Zie voor meer informatie [configureren voor een web-app in Azure App Service een aangepaste domeinnaam].

Klik op tooview uw domeinnamen **alle instellingen** > **aangepaste domeinen en SSL**.

### <a name="deployments"></a>Implementaties
* Doorlopende implementatie instellen. Zie [toodeploy Git met behulp van Web-Apps in Azure App Service](web-sites-deploy.md).
* Implementatiesites. Zie [tooStaging omgevingen voor Web-Apps in Azure App Service implementeren].

Klik op tooview uw implementatiesites **alle instellingen** > **implementatiesites**.

### <a name="monitoring"></a>Bewaking
In de modus voor Basic- of Standard, kunt u Hallo beschikbaarheid van HTTP of HTTPS-eindpunten, testen van toothree geografisch verspreide vestigingen. Een bewakingstest mislukt als Hallo HTTP-antwoordcode een fout (4xx of 5xx is) of antwoord Hallo langer dan 30 seconden duurt. Een eindpunt wordt aangemerkt als beschikbaar als de bewakingstests Hallo van alle slagen Hallo opgegeven locaties. 

Zie voor meer informatie [hoe: website-eindpunt Monitorstatus].

> [!NOTE]
> Als u wilt dat tooget de slag met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen], waar u direct een tijdelijke en eenvoudige web-app kunt maken in App Service. U hebt geen creditcard nodig en u doet geen toezeggingen.
> 
> 

## <a name="next-steps"></a>Volgende stappen
* [Een aangepaste domeinnaam configureren in Azure App Service]
* [HTTPS inschakelen voor een app in Azure App Service]
* [Een web-app schalen in Azure App Service]
* [Bewaking van de basisprincipes voor Web-Apps in Azure App Service]

<!-- URL List -->

[ASP.NET SignalR]: http://www.asp.net/signalr
[Azure Portal]: https://portal.azure.com/
[Een aangepaste domeinnaam configureren in Azure App Service]: ./app-service-web-tutorial-custom-domain.md
[tooStaging omgevingen voor Web-Apps in Azure App Service implementeren]: ./web-sites-staged-publishing.md
[HTTPS inschakelen voor een app in Azure App Service]: ./app-service-web-tutorial-custom-ssl.md
[hoe: website-eindpunt Monitorstatus]: http://go.microsoft.com/fwLink/?LinkID=279906
[Bewaking van de basisprincipes voor Web-Apps in Azure App Service]: ./web-sites-monitor.md
[pipeline-modus]: http://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture#Application
[Een web-app schalen in Azure App Service]: ./web-sites-scale.md
[socket.io]: ./web-sites-nodejs-chat-app-socketio.md
[App Service uitproberen]: https://azure.microsoft.com/try/app-service/

<!-- IMG List -->

[configure01]: ./media/web-sites-configure/configure01.png
[configure02]: ./media/web-sites-configure/configure02.png
[configure03]: ./media/web-sites-configure/configure03.png
