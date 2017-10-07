---
title: aaaOperating systeemfunctionaliteit op Azure App Service
description: Meer informatie over Hallo OS functionaliteit beschikbaar tooweb apps, back-ends voor mobiele Apps en API apps in Azure App Service
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: 39d5514f-0139-453a-b52e-4a1c06d8d914
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/01/2016
ms.author: cephalin
ms.openlocfilehash: 695188c48102b10ece326fba8d50a5f55b03b003
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="operating-system-functionality-on-azure-app-service"></a>Besturingssysteem-functionaliteit op Azure App Service
In dit artikel wordt Hallo algemene basislijn besturingssysteem functionaliteit beschreven die beschikbaar tooall apps die worden uitgevoerd op [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714). Deze functionaliteit omvat bestand, netwerk, en toegang tot het register en logboeken met diagnostische gegevens en gebeurtenissen. 

<a id="tiers"></a>

## <a name="app-service-plan-tiers"></a>App Service plan lagen
App Service kan apps van de klant in een multitenant-hostomgeving uitgevoerd. Apps die worden geïmplementeerd in Hallo **vrije** en **gedeelde** lagen in werkprocessen worden uitgevoerd op gedeelde virtuele machines tijdens de apps die worden geïmplementeerd in Hallo **standaard** en  **Premium** lagen worden uitgevoerd op speciale specifiek voor Hallo-apps die zijn gekoppeld aan één klant horen.

Omdat App Service biedt ondersteuning voor een naadloze ervaring voor vergroten/verkleinen tussen verschillende lagen, Hallo beveiligingsconfiguratie afgedwongen voor App Service-apps blijft Hallo dezelfde. Dit zorgt ervoor dat apps niet plotseling zich anders gedragen, onverwachte manieren mislukt bij het App Service-abonnement van één laag tooanother verandert.

<a id="developmentframeworks"></a>

## <a name="development-frameworks"></a>Ontwikkelingsframeworks
App Service prijzen lagen besturingselement Hallo hoeveelheid rekenresources (CPU, schijfruimte, geheugen en netwerk uitgaande) beschikbaar tooapps. Hallo breedte van de framework-functionaliteit beschikbaar tooapps blijft echter Hallo die dezelfde ongeacht Hallo lagen schalen.

App Service ondersteunt een groot aantal ontwikkelingsframeworks, met inbegrip van ASP.NET, klassiek ASP, node.js, PHP en Python - die allemaal als-extensies in IIS uitvoeren. In de volgorde toosimplify en normaliseren beveiligingsconfiguratie, App Service-apps gewoonlijk uitgevoerd Hallo verschillende ontwikkelingsframeworks met de standaardinstellingen. Een aanpak tooconfiguring apps kunnen zijn toocustomize Hallo API oppervlak en functionaliteit voor elke afzonderlijke ontwikkelframework. App Service duurt in plaats daarvan een meer algemene benadering doordat een gemeenschappelijke basislijn van de functionaliteit van besturingssysteem ongeacht ontwikkelframework voor een app.

Hallo volgende secties geven een overzicht Hallo algemene soorten besturingssysteem functionaliteit beschikbaar tooApp Service-apps.

<a id="FileAccess"></a>

## <a name="file-access"></a>Toegang tot het bestand
Er bestaan verschillende schijven in App Service, waaronder lokale stations- en netwerkstations.

<a id="LocalDrives"></a>

### <a name="local-drives"></a>Lokale stations
De kern is App Service een service die wordt uitgevoerd op Hallo Azure PaaS (platform als een service)-infrastructuur. Als gevolg hiervan, Hallo lokale stations die zijn '' tooa virtuele machine gekoppelde worden hello hetzelfde station typen beschikbaar tooany-werkrol uitgevoerd in Azure. Dit omvat een systeemstation (hello station D:\), een toepassing station waarop Azure cspkg pakketbestanden uitsluitend door App Service (en niet-toegankelijke toocustomers) gebruikt en een 'gebruiker' station (Hallo station C:\), waarvan de grootte, afhankelijk van Hallo grootte varieert Hallo VM.

<a id="NetworkDrives"></a>

### <a name="network-drives-aka-unc-shares"></a>Netwerkstations (aka UNC shares)
Een van de Hallo unieke aspecten van App-Service waarmee app-implementatie en het onderhoud duidelijk is dat alle gebruikersinhoud is opgeslagen op een reeks UNC-shares. Dit model maps zeer mooi toohello algemene patroon van inhoudopslag die wordt gebruikt door lokale webhosting-omgevingen met meerdere servers met gelijke taakverdeling. 

In App Service, er zijn van een UNC-shares in elke Datacenter wordt gemaakt. Een percentage van Hallo gebruikersinhoud voor alle klanten in elk Datacenter toegewezen tooeach UNC-share. Alle inhoud van het Hallo-bestand voor één klant-abonnement is bovendien altijd geplaatst op Hallo dezelfde UNC-share. 

Let op: vanwege toohow cloudservices werkt, Hallo specifieke virtuele machine die verantwoordelijk is voor het hosten van een UNC-share verandert gedurende een bepaalde periode. Het kan worden gegarandeerd dat UNC-shares gekoppeld door andere virtuele machines als ze omhoog en omlaag tijdens Hallo normale bewerkingen van de cloud gebracht worden. Apps moet daarom nooit vastgelegde veronderstellingen dat informatie van het Hallo-machine via een UNC-pad stabiel gedurende een bepaalde periode blijft. In plaats daarvan moeten ze Hallo handige gebruiken *faux* absoluut pad **D:\home\site** die voorziet in App Service. Deze faux absoluut pad biedt een methode draagbare, app en gebruiker-networkdirect voor tooone eigen app verwijzen. Met behulp van **D:\home\site**, een gedeelde bestanden kan overdragen vanuit app tooapp zonder tooconfigure een nieuwe absoluut pad voor elke overdracht.

<a id="TypesOfFileAccess"></a>

### <a name="types-of-file-access-granted-tooan-app"></a>Typen bestandstoegang verleend tooan app
Elke klant-abonnement heeft een gereserveerde mapstructuur op een specifieke UNC-share binnen een datacenter. Een klant meerdere apps die zijn gemaakt binnen een specifieke datacentrum kan hebben, zodat alle Hallo-mappen die behoren tooa één klant-abonnement worden gemaakt op Hallo dezelfde UNC-share. Hallo share omvat mogelijk mappen zoals die voor inhoud, fout en diagnostische logboeken en eerdere versies van het Hallo-app gemaakt door het besturingselement. Zoals verwacht, is een klant app mappen zijn beschikbaar voor lees- en schrijftoegang tijdens runtime door de toepassingscode Hallo-app.

Op Hallo lokale stations aangesloten toohello virtuele machine die een app uitvoert, App Service een deel van de ruimte op station C:\ voor tijdelijke lokale opslag van de app-specifiek Hallo zijn gereserveerd. Hoewel een app volledige lezen/schrijven toegang tooits eigen tijdelijke lokale opslag, dat de opslag beoogde toobe rechtstreeks gebruikt door de toepassingscode Hallo echt niet heeft. Hallo bedoeling is in plaats daarvan tooprovide tijdelijke bestandsopslag voor IIS en web-App-frameworks. App Service wordt ook beperkt Hallo hoeveelheid tijdelijke lokale opslag beschikbaar tooeach app tooprevent afzonderlijke apps buitensporige hoeveelheden lokale bestandsopslag verbruikt.

Twee voorbeelden van hoe App Service gebruikt voor lokale tijdelijke zijn Hallo-map voor tijdelijke bestanden voor ASP.NET en Hallo directory voor IIS gecomprimeerde bestanden. Hallo 'Temporary ASP.NET Files' directory Hallo ASP.NET-compilatie-systeem gebruikt als een tijdelijke compilatie cachelocatie. Hallo 'IIS tijdelijke gecomprimeerde bestanden' directory toostore gecomprimeerd antwoorduitvoer wordt gebruikt door IIS. Beide typen van bestand gebruik (evenals anderen) worden toegewezen in App Service tooper app tijdelijke lokale opslag. Deze opnieuw toe te wijzen, zorgt u ervoor dat de functionaliteit blijft zoals verwacht.

Elke app in App Service wordt uitgevoerd als een willekeurig uniek beperkte bevoegdheden werkprocesidentiteit genoemd Hallo 'toepassingsgroepidentiteit', verder hier beschreven: [http://www.iis.net/learn/manage/configuring-security/application-pool-identities ](http://www.iis.net/learn/manage/configuring-security/application-pool-identities). Toepassingscode gebruikt deze identiteit voor basic alleen-lezen toegang toohello-systeemstation (hello D:\ station). Dit betekent dat toepassingscode kan algemene mapstructuren weergeven en lezen algemene bestanden op het systeemstation. Hoewel dit mogelijk toobe een enigszins algemeen niveau van toegang wordt weergegeven, Hallo dezelfde mappen en bestanden toegankelijk zijn wanneer het inrichten van een werkrol in een Azure gehoste service en Hallo station inhoud lezen. 

<a name="multipleinstances"></a>

### <a name="file-access-across-multiple-instances"></a>Toegang tot het bestand voor meerdere exemplaren
Hallo basismap bevat een app-inhoud en toepassingscode tooit kan schrijven. Als een app wordt uitgevoerd op meerdere exemplaren, Hallo basismap wordt gedeeld door alle exemplaren, zodat alle exemplaren Hallo zien dezelfde directory. Dus als een app wordt opgeslagen geüploade bestanden toohello basismap, zijn die bestanden bijvoorbeeld onmiddellijk beschikbaar tooall exemplaren. 

<a id="NetworkAccess"></a>

## <a name="network-access"></a>Toegang tot het netwerk
Toepassingscode kan TCP/IP gebruiken en op basis van UDP-protocollen toomake uitgaande verbindingen tooInternet toegankelijk eindpunten die externe services beschikbaar netwerk. Apps kunnen deze dezelfde protocollen tooconnect tooservices binnen Azure & #151, bijvoorbeeld door het opstellen van HTTPS-verbindingen tooSQL Database gebruiken.

Er is ook een beperkte capaciteit voor apps tooestablish één lokale loopback-verbinding en een app luisteren op die lokale loopback-socket. Deze functie bestaat voornamelijk tooenable-apps die op de lokale loopback-sockets als onderdeel van hun functionaliteit luisteren. Houd er rekening mee dat elke app een 'persoonlijke' loopback-verbinding ziet. App "A" kan niet luisteren tooa lokale loopback socket tot stand gebracht door app "B".

Named pipes worden ook ondersteund als een mechanisme voor communicatie tussen processen (IPC) tussen verschillende processen die gezamenlijk een app worden uitgevoerd. Bijvoorbeeld IIS FastCGI-module voor Hallo is afhankelijk van named pipes toocoordinate Hallo afzonderlijke processen die PHP-pagina's worden uitgevoerd.

<a id="Code"></a>

## <a name="code-execution-processes-and-memory"></a>De uitvoering van code, processen en geheugen
Zoals eerder opgemerkt, apps worden uitgevoerd binnen werkprocessen met beperkte bevoegdheden met een willekeurige toepassingsgroepidentiteit. Toepassingscode heeft toegang tot toohello-geheugenruimte die is gekoppeld aan het werkproces hello, evenals de onderliggende processen die mogelijk worden geïnitieerd door de CGI-processen of andere toepassingen. Maar één app heeft geen toegang tot Hallo geheugen of gegevens van een andere app, zelfs als deze zich op dezelfde virtuele machine Hallo.

Apps kunnen scripts of pagina's die zijn geschreven met ondersteunde web ontwikkelingsframeworks worden uitgevoerd. App Service configureren niet alle web framework instellingen toomore beperkt modi. Bijvoorbeeld: ASP.NET apps die worden uitgevoerd op App Service uitvoeren in 'volledige' vertrouwen als vertrouwensmodus tegengestelde tooa meer beperkt. Web-frameworks, met inbegrip van zowel klassieke ASP- en ASP.NET, kunnen aanroepen COM-onderdelen in-process (maar niet out-of-process COM-onderdelen) zoals ADO (ActiveX Data Objects), die standaard op Hallo van Windows-besturingssysteem zijn geregistreerd.

Apps kunnen starten en willekeurige code uitvoeren. Het is toegestaan voor een app toodo zaken zoals een opdrachtshell kan worden gemaakt of een PowerShell-script uitvoeren. Echter, hoewel arbitraire code en processen kunnen worden gestart vanuit een app, de uitvoerbare programma's en scripts zijn nog steeds beperkt toohello bevoegdheden verleend toohello bovenliggende groep van toepassingen. Bijvoorbeeld, een app kunt kan worden gemaakt een uitvoerbaar bestand dat u een uitgaande HTTP-aanroep maakt, maar deze kan niet dezelfde uitvoerbare toounbind Hallo IP-adres van een virtuele machine van de NIC proberen Een uitgaande netwerk oproep toolow bevoegdheden code is toegestaan, maar tooreconfigure netwerkinstellingen op een virtuele machine probeert beheerdersbevoegdheden vereist.

<a id="Diagnostics"></a>

## <a name="diagnostics-logs-and-events"></a>Logboeken met diagnostische gegevens en gebeurtenissen
Informatie in het foutenlogboek is een andere set gegevens dat sommige apps tooaccess proberen. Hallo typen logboek informatie beschikbaar toocode uitgevoerd in App Service bevat diagnostische en meld u informatie die wordt gegenereerd door een app die ook eenvoudig toegankelijk toohello app. 

W3C-HTTP-logboeken die zijn gegenereerd door een actieve app zijn bijvoorbeeld beschikbaar op een logboekmap in Hallo netwerk delen locatie gemaakt voor Hallo app of beschikbaar in de blob-opslag als een klant heeft ingesteld toostorage W3C-logboekregistratie. de laatste optie Hallo kan grote hoeveelheden logboeken toobe verzameld zonder risico Hallo Hallo bestand opslaglimieten die zijn gekoppeld aan een netwerkshare overschrijden.

In een vergelijkbare vein realtime diagnostische gegevens van .NET-toepassingen kan ook worden geregistreerd met Hallo .NET tracering en diagnostische gegevens infrastructuur, met opties toowrite Hallo trace informatie tooeither Hallo van app-netwerkshare, of u kunt ook tooa blob-opslag locatie.

Gebieden van diagnostische logboekregistratie en tracering die niet beschikbaar tooapps zijn Windows ETW-gebeurtenissen en algemene Windows-gebeurtenislogboeken (bijvoorbeeld systeem, toepassing en beveiliging gebeurtenislogboeken). Omdat informatie voor ETW-tracering mogelijk bekeken worden kan worden machine hele (met Hallo rechts ACL's), lees- en schrijftoegang tooETW gebeurtenissen geblokkeerd. Ontwikkelaars wellicht opgevallen dat die API-aanroepen tooread en write ETW-gebeurtenissen en algemene Windows-gebeurtenislogboeken weergegeven toowork, maar dat is omdat App Service is 'faking' hello aanroepen zodat deze toosucceed worden weergegeven. In werkelijkheid bevat toepassingscode Hallo geen toegang tot toothis gebeurtenisgegevens.

<a id="RegistryAccess"></a>

## <a name="registry-access"></a>Toegang tot het register
Apps hebben alleen-lezentoegang toomuch (hoewel niet alle) van register Hallo van Hallo virtuele machine ze worden uitgevoerd. Dit betekent de registersleutels waarmee alleen-lezentoegang toohello lokale groep gebruikers toegankelijk zijn voor apps uit te voeren in de praktijk. Is een gebied van Hallo-register wordt momenteel niet ondersteund voor lees- of schrijftoegang Hallo HKEY\_huidige\_gebruikerscomponent.

Toegang voor schrijven toohello register wordt geblokkeerd, met inbegrip van de registersleutels van toegang tooany per gebruiker. Vanuit het perspectief van de app hello, van schrijftoegang toohello register moet nooit worden aangehaald in hello Azure-omgeving omdat apps kunnen (en) ophalen gemigreerd in verschillende virtuele machines. Hallo alleen permanente beschrijfbare opslag die kan worden afhankelijk is van door een app is Hallo per app inhoudsmap structuur is opgeslagen op Hallo-App Service-UNC-shares. 

## <a name="more-information"></a>Meer informatie

[Azure-Web-App sandbox](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox) -Hallo meeste actuele informatie over de uitvoeringsomgeving Hallo van App Service. Deze pagina wordt beheerd rechtstreeks door Hallo ontwikkelteam App Service.

> [!NOTE]
> Als u wilt dat tooget de slag met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen](https://azure.microsoft.com/try/app-service/), waar u direct een tijdelijke en eenvoudige web-app kunt maken in App Service. U hebt geen creditcard nodig en u doet geen toezeggingen.
> 
> 


