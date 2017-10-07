---
title: vergelijking van App Service, virtuele Machines, Service Fabric en Cloud Services aaaAzure | Microsoft Docs
description: Meer informatie over hoe toochoose tussen Azure App Service, virtuele Machines, Service Fabric en Cloud-Services voor het hosten van webtoepassingen.
services: app-service\web, virtual-machines, cloud-services
documentationcenter: 
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: 7d346a23-532a-42a9-98a8-23b7286d32a8
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: overview
ms.date: 07/07/2016
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 7577332ed049df66178c7b2cd5c440a7f93a7865
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-virtual-machines-service-fabric-and-cloud-services-comparison"></a>Vergelijking van Azure App Service, virtuele Machines, Service Fabric en Cloud-Services
## <a name="overview"></a>Overzicht
Azure biedt verschillende manieren toohost websites: [Azure App Service][Azure App Service], [virtuele Machines][Virtual Machines], [Service Fabric ] [ Service Fabric], en [Cloudservices][Cloud Services]. In dit artikel helpt u begrijpen Hallo-opties en de juiste keuze Hallo voor uw webtoepassing.

Azure App Service is de beste keuze Hallo voor de meeste web-apps. Implementatie en beheer zijn geïntegreerd in Hallo-platform, sites snel toohandle intensief verkeer belastingen kunnen schalen en Hallo ingebouwde load balancing en verkeer manager bieden hoge beschikbaarheid. U kunt verplaatsen bestaande sites tooAzure App Service eenvoudig met een [online Migratiehulpmiddel](https://www.migratetoazure.net/), gebruiken een open source-app van Hallo galerie met toepassingen of maak een nieuwe site met behulp van Hallo framework en hulpprogramma's van uw keuze. Hallo [WebJobs] [ WebJobs] functie kunt u eenvoudig tooadd achtergrond taak verwerking tooyour App Service-web-app.

Service Fabric is een goede keuze als u een nieuwe app maken of een bestaande app opnieuw in te schrijven toouse een microservice-architectuur. Apps die worden uitgevoerd op een gedeelde groep machines, kunnen begin klein en toomassive schaal met honderden of duizenden computers naar behoefte groeien. Stateful services maken het gemakkelijk tooconsistently en veilig opslaan van app-status en automatisch beheerd met Service Fabric service partitioneren, schaalbaarheid en beschikbaarheid voor u.  Service Fabric ondersteunt ook WebAPI met Open Web Interface voor .NET (OWIN) en ASP.NET Core.  Vergeleken tooApp Service Fabric-Service biedt ook meer controle over of directe toegang tot de onderliggende infrastructuur Hallo. U kunt externe in uw servers of server starten van de taken configureren. Cloud-Services is vergelijkbaar tooService Fabric in de mate van controle en eenvoudig te gebruiken, maar is nu een verouderde service en Service Fabric wordt aanbevolen voor het ontwikkelen van nieuwe.

Als u een bestaande toepassing waarvoor toorun aanzienlijke wijzigingen in App Service- of Service Fabric hebt, kunt u virtuele Machines in de volgorde toosimplify toohello cloud migreren. Echter correct configureren, beveiligen en beheren van virtuele machines veel meer tijd nodig en IT-expertise vergeleken tooAzure App Service en Service Fabric. Als u Azure Virtual Machines overweegt, moet u rekening account Hallo doorlopend onderhoud moeite toopatch bijwerken en beheren van uw VM-omgeving. Virtuele Machines in Azure is Infrastructure-as-a-Service (IaaS), terwijl de App Service en Service Fabric-Platform-as-a-Service (Paas) zijn. 

## <a name="features"></a>Vergelijking van functies
Hallo volgende tabel vergelijkt Hallo-mogelijkheden van App Service, Cloud Services, virtuele Machines en Service Fabric toohelp u Hallo beste keuze. Zie voor actuele informatie over Hallo SLA voor elke optie [Azure Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).

| Functie | App Service (web-apps) | Cloud-Services (webrollen) | Virtuele machines | Service Fabric | Opmerkingen |
| --- | --- | --- | --- | --- | --- |
| Handomdraai implementatie |X | | |X |Implementeren van een toepassing of een toepassing update tooa Cloudservice of het maken van een virtuele machine, duurt het enkele minuten ten minste; een toepassing tooa web-app implementeren duurt seconden. |
| Opschalen toolarger machines zonder opnieuw distribueren |X | | |X | |
| Web server-exemplaren delen inhoud en configuratie, wat betekent dat u niet hebt tooredeploy of opnieuw configureren terwijl u schaalt. |X | | |X | |
| Meerdere implementatieomgevingen (productie en in fasering) |X |X | |X |Service Fabric, kunt u toohave omgevingen met meerdere voor uw toepassingen of toodeploy verschillende versies van uw app naast elkaar. |
| Automatische OS updatebeheer |X |X | | |Automatische updates voor het besturingssysteem zijn gepland voor een toekomstige Service Fabric-release. |
| Naadloze platform overschakelen (gemakkelijk verplaatsen tussen de 32-bits en 64-bits) |X |X | | | |
| Code implementeren in GIT, FTP |X | |X | | |
| Code implementeren met Web Deploy |X | |X | |Cloudservices ondersteunt Hallo gebruik van Web Deploy toodeploy updates tooindividual rolinstanties. Echter, u deze niet gebruiken voor de initiële implementatie van een rol, en als u Web Deploy voor een update hebt toodeploy afzonderlijk tooeach exemplaar van een rol. Meerdere exemplaren zijn vereist in de volgorde tooqualify voor Hallo Cloud Service SLA voor productieomgevingen. |
| Ondersteuning voor WebMatrix |X | |X | | |
| Toegang tooservices zoals Service Bus-, opslag-, SQL-Database |X |X |X |X | |
| Host-web- of web services-laag van een architectuur met meerdere lagen |X |X |X |X | |
| Middelste laag van de host van een architectuur met meerdere lagen |X |X |X |X |App Service-web-apps kunnen eenvoudig host een REST-API als middelste laag en Hallo [WebJobs](http://go.microsoft.com/fwlink/?linkid=390226) functie achtergrondtaken verwerking kan hosten. U kunt WebJobs uitvoeren in een speciale website tooachieve onafhankelijke schaalbaarheid voor Hallo laag. Hallo preview [API-apps](../app-service-api/app-service-api-apps-why-best-platform.md) functie biedt nog meer functies voor het hosten van de REST-services. |
| Geïntegreerde MySQL as a service-ondersteuning |X |X |X | |MySQL-as-a-service kunnen worden geïntegreerd in cloud-Services via de offerings van ClearDB, maar niet als onderdeel van de werkstroom van hello Azure-Portal. |
| Ondersteuning voor ASP.NET, klassiek ASP, Node.js, PHP, Python |X |X |X |X |Service Fabric ondersteunt het Hallo maken van een web-front-met [ASP.NET 5](../service-fabric/service-fabric-add-a-web-frontend.md) of kunt u elk type toepassing (Node.js, Java, enzovoort) implementeren als een [Gast uitvoerbaar bestand](../service-fabric/service-fabric-deploy-existing-app.md). |
| Scale-out toomultiple exemplaren zonder opnieuw distribueren |X |X |X |X |Virtuele Machines uitbreiden toomultiple exemplaren, maar Hallo services die worden uitgevoerd op deze toohandle dit scale-out moeten worden geschreven. U hebt tooconfigure een load balancer tooroute aanvragen over Hallo-machines en maak een Affiniteitsgroep tooprevent gelijktijdige opnieuw opstarten van alle exemplaren vanwege toomaintenance- of hardwarestoringen. |
| Ondersteuning voor SSL |X |X |X |X |Voor App Service WebApps, wordt SSL voor aangepaste domeinnamen alleen ondersteund voor Basic en Standard-modus. Zie voor meer informatie over het gebruik van SSL met web-apps [configureren van een SSL-certificaat voor een Azure-Website](app-service-web-tutorial-custom-ssl.md). |
| Visual Studio-integratie |X |X |X |X | |
| Foutopsporing op afstand |X |X |X | | |
| Code implementeren in TFS |X |X |X |X | |
| Netwerkisolatie met [Azure Virtual Network](/azure/virtual-network/) |X |X |X |X |Zie ook [Azure Websites virtuele netwerkintegratie](https://azure.microsoft.com/blog/2014/09/15/azure-websites-virtual-network-integration/) |
| Ondersteuning voor [met Azure Traffic Manager](/azure/traffic-manager/) |X |X |X |X | |
| Geïntegreerde Eindpuntcontrole |X |X |X | | |
| Toegang tot extern bureaublad-tooservers | |X |X |X | |
| Een aangepaste MSI installeren | |X |X |X |Service Fabric, kunt u toohost elk uitvoerbaar bestand opslaan als een [Gast uitvoerbaar bestand](../service-fabric/service-fabric-deploy-existing-app.md) of u kunt een app installeren op Hallo van virtuele machines. |
| Mogelijkheid toodefine/uitvoeren opstarten taken | |X |X |X | |
| Kan tooETW gebeurtenissen luisteren | |X |X |X | |

## <a name="scenarios"></a>Scenario's en aanbevelingen
Hier volgen enkele algemene scenario's van de toepassing uit met aanbevelingen toowhich Azure-web-hosting optie mogelijk meest geschikt is voor elk.

* [Ik heb nodig een webfront-end met achtergrondverwerking en database back-end toorun zakelijke toepassingen zijn geïntegreerd met lokale activa.](#onprem)
* [Ik moet een betrouwbare manier toohost mijn zakelijke website die wordt geschaald well en aanbiedingen globale bereiken.](#corp)
* [Ik heb een IIS6-toepassing op Windows Server 2003 wordt uitgevoerd.](#iis6)
* [Ik ben eigenaar van een klein bedrijf en ik mijn site een goedkope manier toohost nodig, maar met toekomstige groei in gedachten.](#smallbusiness)
* [Ik ben een web- of grafisch ontwerper en ik toodesign wilt en websites voor mijn klant opbouwen.](#designer)
* [Ik ben mijn toepassing met meerdere lagen met een web-front-toohello Cloud migreert.](#multitier)
* [Mijn toepassing afhankelijk is zeer aangepaste Windows of Linux-omgevingen en I wilt toomove het toohello cloud.](#custom)
* [Mijn site maakt gebruik van open-sourcesoftware en wil toohost in Azure.](#oss)
* [Ik heb een line-of-business-toepassing die tooconnect toohello bedrijfsnetwerk moet.](#lob)
* [Ik wil toohost een REST-API of web-service voor mobiele clients.](#mobile)

### <a id="onprem"></a>Ik heb nodig een webfront-end met achtergrondverwerking en database back-end toorun zakelijke toepassingen zijn geïntegreerd met lokale activa.
Azure App Service is een uitstekende oplossing voor complexe business-toepassingen. U kunt ontwikkelen van apps die automatisch schalen op een load balanced platform, zijn beveiligd met Active Directory en verbinding maken met tooyour lokale bronnen. Er wordt het beheer van apps die via een hoogwaardige portal en API's eenvoudig, en kunt u toogain inzicht in hoe klanten ze worden gebruikt met hulpprogramma's voor app-inzicht. Hallo [Webjobs] [ Webjobs] functie kunt u achtergrondprocessen uitvoeren en taken als onderdeel van uw weblaag bij hybride verbindingen en VNET-functies kunnen u eenvoudig tooconnect back tooon lokale bronnen. Azure App Service biedt drie 9 SLA voor web-apps en kunt u:

* Uw toepassingen betrouwbaar uitvoeren op een zelfherstellende, automatisch patchen cloudplatform.
* Schalen automatisch via een wereldwijd netwerk van datacenters.
* Back-up en herstel voor herstel na noodgevallen.
* ISO, SOC2 en PCI compatibel zijn.
* Integratie met Active Directory

### <a id="corp"></a>Ik moet een betrouwbare manier toohost mijn zakelijke website die wordt geschaald well en aanbiedingen globale bereiken.
Azure App Service is een uitstekende oplossing voor het hosten van zakelijke websites. Deze web-apps tooscale kan snel en eenvoudig toomeet vraag over een wereldwijd netwerk van datacenters. Lokale reach fouttolerantie en intelligente verkeer management biedt. Alle op een platform waarmee hoogwaardige beheerhulpprogramma's, zodat u toogain inzicht in de sitestatus en siteverkeer snel en eenvoudig. Azure App Service biedt drie 9 SLA voor web-apps en kunt u:

* Uw websites betrouwbaar uitvoeren op een zelfherstellende, automatisch patchen cloudplatform.
* Schalen automatisch via een wereldwijd netwerk van datacenters.
* Back-up en herstel voor herstel na noodgevallen.
* Beheren van Logboeken en verkeer met geïntegreerde hulpmiddelen.
* ISO, SOC2 en PCI compatibel zijn.
* Integratie met Active Directory

### <a id="iis6"></a>Ik heb een IIS6-toepassing op Windows Server 2003 wordt uitgevoerd.
Azure App Service kunt u eenvoudig tooavoid Hallo infrastructuurkosten in verband met het migreren van oudere IIS6-toepassingen. Microsoft heeft gemaakt [eenvoudig toouse-hulpprogramma's voor migratie en gedetailleerde migratie-richtlijnen](https://www.movemetowebsites.net/) die u toocheck compatibiliteit inschakelen en eventuele wijzigingen die nodig hebt aangebracht toobe identificeren. Integratie met Visual Studio, TFS en algemene CMS's maakt het eenvoudig toodeploy IIS6 toepassingen rechtstreeks toohello cloud. Zodra geïmplementeerd, biedt hello Azure Portal krachtige beheerprogramma's waarmee u tooscale toomanage kosten en omhoog in toomeet vraag indien nodig. U kunt met het hulpprogramma voor migratie van Hallo:

* Migreer uw cloud oudere Windows Server 2003 web application toohello snel en eenvoudig.
* Tooleave kiezen voor de gekoppelde SQL database lokale-toocreate een hybride-toepassing.
* De SQL-database, samen met de oudere toepassing verplaatst automatisch.

### <a id="smallbusiness"></a>Ik ben eigenaar van een klein bedrijf en ik mijn site een goedkope manier toohost nodig, maar met toekomstige groei in gedachten.
Azure App Service is een uitstekende oplossing voor dit scenario, omdat u kunt gratis gebruiken en vervolgens meer mogelijkheden toevoegen wanneer u deze nodig. Elke gratis web-app wordt geleverd met een domein dat is verstrekt door Azure (*your_company*. azurewebsites.net), en Hallo-platform omvat geïntegreerde hulpprogramma's voor implementatie en beheer, evenals een toepassingsgalerie waarmee u eenvoudig tooget gestart. Er zijn veel andere services en schalingsopties Hallo site tooevolve met verbeterde gebruikersvraag toestaan. U kunt met Azure App Service:

* Beginnen met de gratis laag Hallo en schaal omhoog indien nodig.
* Gebruik Hallo-Toepassingsgalerie tooquickly populaire webtoepassingen, zoals WordPress instellen.
* Extra Azure-services en functies tooyour toepassing toevoegen naar behoefte.
* Beveilig uw web-app met HTTPS.

### <a id="designer"></a>Ik ben een web- of grafisch ontwerper en ik toodesign wilt en websites bouwen voor mijn klant
Biedt ondersteuning voor Git en FTP-implementatie en nauwe integratie met hulpprogramma's en services, zoals Visual Studio en SQL-Database biedt voor webontwikkelaars- en ontwerpers Azure App Service kan eenvoudig worden geïntegreerd met tal van frameworks en hulpprogramma's. Met App Service kunt u:

* Gebruik de opdrachtregelprogramma's voor [geautomatiseerde taken][scripting].
* Werken met populaire talen zoals [.Net][dotnet], [PHP][PHP], [Node.js] [ nodejs], en [Python][Python].
* Selecteer de drie verschillende schalen niveaus voor het schalen van toovery hoge capaciteit.
* Integreren met andere Azure-services, zoals [SQL-Database][sqldatabase], [Service Bus] [ servicebus] en [opslag] [ Storage], of de offerings van Hallo partner [Azure Store][azurestore], zoals MySQL en MongoDB.
* Geïntegreerd met hulpprogramma's, zoals Visual Studio, Git WebMatrix, WebDeploy, TFS en FTP.

### <a id="multitier"></a>Ik ben mijn toepassing met meerdere lagen met een web-front-toohello Cloud migreren
Als u een toepassing met meerdere lagen, zoals een webserver die verbinding tooa database maakt, is Azure App Service een goede optie die nauwe integratie met Azure SQL Database biedt. En u kunt Hallo webtaken functie gebruiken voor het uitvoeren van back-end-processen.

Service Fabric kiezen voor een of meer van uw lagen als u meer controle over Hallo server-omgeving, zoals Hallo mogelijkheid tooremote in de server of server starten van de taken configureren.

Virtuele Machines kiezen voor een of meer van uw lagen als u wilt dat toouse uw eigen computerinstallatiekopie of server-software of services die u op de Service Fabric configureren kunt uitvoeren.

### <a id="custom"></a>Mijn toepassing afhankelijk is zeer aangepaste Windows of Linux-omgevingen en I wilt toomove het toohello cloud.
Als uw toepassing complexe installatie vereist of de configuratie van virtuele Machines van de besturingssysteem-software en Hallo waarschijnlijk de beste oplossing Hallo is. Met virtuele Machines, kunt u het volgende doen:

* Hallo virtuele Machine galerie toostart gebruiken met een besturingssysteem, zoals Windows of Linux, en vervolgens aanpassen voor uw toepassingsvereisten.
* Maken en uploaden van een aangepaste installatiekopie van een bestaande lokale server toorun op een virtuele machine in Azure.

### <a id="oss"></a>Mijn site maakt gebruik van open-sourcesoftware en wil toohost in Azure
Als uw open-source framework wordt ondersteund op App Service, Hallo talen en frameworks die nodig is voor uw toepassing automatisch voor u geconfigureerd. App Service kunt u:

* Gebruik veel populaire open source talen, zoals [.NET][dotnet], [PHP][PHP], [Node.js] [ nodejs], en [Python][Python].
* WordPress, Drupal, Umbraco, DNN en vele andere webtoepassingen van derden instellen.
* Migreren van een bestaande toepassing of maak een nieuwe van Hallo-Toepassingsgalerie.

Als uw open-source framework wordt niet ondersteund op App Service, kunt u uitvoeren op een van de Hallo andere Azure-web hosting-opties. Met virtuele Machines u software installeren en configureren Hallo op Hallo machine-installatiekopie, die Windows worden kan of Linux-.

### <a id="lob"></a>Ik heb een line-of-business-toepassing die tooconnect toohello bedrijfsnetwerk moet
Als u wilt dat toocreate een line-of-business-toepassing, is uw website mogelijk directe toegang tooservices of gegevens in het bedrijfsnetwerk Hallo. Dit is mogelijk op App Service, Service Fabric en virtuele Machines met Hallo [Azure Virtual Network service](/azure/virtual-network/). Op App Service kunt u Hallo [VNET-integratiefunctie](https://azure.microsoft.com/blog/2014/09/15/azure-websites-virtual-network-integration/), waardoor uw Azure-toepassingen toorun alsof ze in uw bedrijfsnetwerk.

### <a id="mobile"></a>Ik wil toohost een REST-API of web-service voor mobiele clients
HTTP-gebaseerde web-services kunnen u toosupport tal van clients, waaronder mobiele clients. Frameworks zoals ASP.NET Web API integreren met Visual Studio toomake eenvoudiger toocreate en REST-services gebruiken.  Deze services beschikbaar worden gesteld van een webeindpunt, dus is het mogelijk toouse een web-hosting techniek op Azure toosupport dit scenario. App Service is echter een uitstekende keuze is voor het hosten van de REST-API's. Met App Service kunt u:

* Snel maken een [mobiele app](../app-service-mobile/app-service-mobile-value-prop.md) of [API-app](../app-service-api/app-service-api-apps-why-best-platform.md) toohost Hallo HTTP-webservice in een Azure globaal gedistribueerde datacenters.
* Migreren van bestaande services of nieuwe maken.
* SLA voor beschikbaarheid met één exemplaar bereiken of toomultiple toegewezen machines uitbreiden.
* Gebruik Hallo gepubliceerd site tooprovide REST-API's tooany HTTP-clients, waaronder mobiele clients.

> [!NOTE]
> Als u wilt dat tooget voordat u zich aanmeldt voor een account met Azure App Service is gestart, gaat u verder te<a href="https://trywebsites.azurewebsites.net/">https://trywebsites.azurewebsites.net</a>, waar u kunt direct een tijdelijke en eenvoudige app maken in Azure App Service gratis. Geen creditcard nodig en bent nergens toe verplicht.
> 
> 

## <a id="nextsteps"></a>De volgende stappen
Zie voor meer informatie over opties voor webhosting Hallo drie [Introducing Azure](../fundamentals-introduction-to-azure.md).

gestart met opties voor uw toepassing hello gekozen tooget Zie Hallo resources te volgen:

* [Azure App Service](/azure/app-service/)
* [Azure Cloud Services](/azure/cloud-services/)
* [Virtuele Machines in Azure](/azure/virtual-machines/)
* [Service Fabric](/azure/service-fabric/)

<!-- URL List -->

[Azure App Service]: /azure/app-service/
[Cloud Services]: /azure/cloud-services/
[Virtual Machines]: /azure/virtual-machines/
[Service Fabric]: /azure/service-fabric/
[ClearDB]: http://www.cleardb.com/
[WebJobs]: http://go.microsoft.com/fwlink/?linkid=390226&clcid=0x409
[Configuring an SSL certificate for an Azure Website]: app-service-web-tutorial-custom-ssl.md
[azurestore]: https://azuremarketplace.microsoft.com/en-us/marketplace/apps
[scripting]: https://azure.microsoft.com/documentation/scripts/?services=web-sites
[dotnet]: https://azure.microsoft.com/develop/net/
[nodejs]: https://azure.microsoft.com/develop/nodejs/
[PHP]: https://azure.microsoft.com/develop/php/
[Python]: https://azure.microsoft.com/develop/python/
[servicebus]: /azure/service-bus/
[sqldatabase]: /azure/sql-database/
[Storage]: /azure/storage/

<!-- IMG List -->

[ChoicesDiagram]: ./media/choose-web-site-cloud-service-vm/Websites_CloudServices_VMs_3.png
