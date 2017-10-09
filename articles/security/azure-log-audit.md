---
title: aaaAzure logboekregistratie en controle | Microsoft Docs
description: Meer informatie over hoe u logboekregistratie gegevens toogain uitgebreide statistieken over uw toepassing kunt gebruiken.
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: TomSh
ms.openlocfilehash: d0e817b071962ad9bef6250267092b5f9282bc7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-logging-and-auditing"></a>Azure logboekregistratie en controle
## <a name="introduction"></a>Inleiding
### <a name="overview"></a>Overzicht
tooassist huidige potentiële Azure klanten en meer informatie over en met behulp van verschillende betrekking hebben op beveiliging mogelijkheden beschikbaar zijn in Hallo en omringende hello Azure-Platform, Microsoft heeft ontwikkeld die een reeks whitepapers, overzichten van de beveiliging, aanbevolen procedures en controlelijsten. bereik van de onderwerpen in termen van breedte en diepte Hallo en regelmatig worden bijgewerkt. Dit document is onderdeel van de reeks zoals samengevat in Hallo abstracte sectie volgen.
### <a name="azure-platform"></a>Azure-Platform
Azure is een open en flexibele cloud service-platform dat ondersteuning Hallo breedste selectie van besturingssystemen biedt, programmeertalen, frameworks, hulpprogramma's, databases, en apparaten.

U kunt bijvoorbeeld:
-   Linux-containers worden uitgevoerd met Docker-integratie.

-   Met JavaScript, Python, .NET, PHP, Java en Node.js-apps bouwen

-   Build back-ends voor iOS, Android en Windows apparaten.

Hallo van dezelfde technologieën miljoenen van ontwikkelaars en IT-professionals al zijn afhankelijk van en vertrouwen wordt ondersteund door Azure openbare cloud-services.

Wanneer u bouwen op of IT-middelen migreren naar een cloudprovider, u zijn afhankelijk van die organisatie mogelijkheden tooprotect uw toepassingen en gegevens met services en Hallo besturingselementen Hallo bieden ze toomanage Hallo beveiliging van uw cloud-gebaseerde activa.

Azure infrastructuur is speciaal ontworpen van Hallo faciliteit tooapplications voor het hosten van miljoenen klanten tegelijkertijd en biedt een betrouwbare basis waarop bedrijven hun beveiliging behoeften kunnen. Bovendien Azure biedt u een breed scala aan configureerbare beveiliging opties en Hallo mogelijkheid toocontrol ze zodat u beveiliging toomeet Hallo unieke vereisten van uw implementaties kunt aanpassen. Dit document wordt helpt u aan deze vereisten voldoet.

### <a name="abstract"></a>Abstracte
Controle en logboekregistratie van gebeurtenissen die betrekking hebben op beveiliging en gerelateerde waarschuwingen, zijn belangrijke onderdelen van een effectieve strategie voor gegevensbescherming. Beveiligingslogboeken en rapporten bieden u een elektronisch record van verdachte activiteiten en helpen u de patronen die geprobeerde of geslaagde externe binnendringen van Hallo netwerk, evenals de interne aanvallen aangeven mogelijk detecteren. U kunt gebruiken controle toomonitor gebruikersactiviteit document naleving van regelgeving, voert u forensische analyse en meer. Waarschuwingen bevatten een onmiddellijke melding wanneer beveiligingsgebeurtenissen plaatsvinden.

Microsoft Azure-services en producten bieden u configureerbare beveiligingscontrole en logboekregistratie opties toohelp u hiaten in uw beveiligingsbeleid en de mechanismen en los deze toohelp onderbrekingen te voorkomen dat schendingen. Microsoft-services bieden een deel (en in sommige gevallen alle) na opties Hallo: gecentraliseerde bewaking, logboekregistratie en analyse systemen tooprovide continue zichtbaarheid; tijdige waarschuwingen; en rapporten toohelp die u Hallo grote hoeveelheid gegevens die worden gegenereerd door apparaten en services beheren.

Microsoft Azure-logboekgegevens kan geëxporteerde tooSecurity Incident en Event Management SIEM ()-systemen voor analyse en kan worden geïntegreerd met controle oplossingen van derden.

Dit technisch document bevat een inleiding voor het genereren, te verzamelen en analyseren van beveiligingslogboeken van services die worden gehost op Azure en kunt u beveiliging voor inzicht in uw Azure-implementaties. Hallo-bereik van dit technisch document is beperkt tooapplications en gebouwd en geïmplementeerd in Azure-services.

> [!Note]
> Bepaalde aanbevelingen in dit document kunnen leiden tot hogere-, netwerk- of compute-Resourcegebruik en de kosten van uw licentie of abonnement te verhogen.

## <a name="types-of-logs-in-azure"></a>Verschillende typen logboeken in Azure
Cloud-toepassingen zijn complexe met veel bewegende onderdelen. Logboeken kunt u gegevens tooensure die uw toepassing up blijft en wordt uitgevoerd in een foutloze toestand bevindt. Ook kunt u toostave potentiële problemen uitgeschakeld of het oplossen van het verleden zijn. Bovendien kunt u logboekregistratie gegevens toogain uitgebreide statistieken over uw toepassing. Deze kennis kan u helpen de prestaties van toepassingen tooimprove of onderhoud of acties die anders worden handmatige interventie moeten automatiseren.

Azure produceert uitgebreide logboekregistratie in voor elke Azure-service. Deze logboeken worden gecategoriseerd door deze belangrijkste typen:
-   **Besturingselement/management-logboeken** geven inzicht in hello Azure Resource Manager maken, bijwerken en DELETE-bewerkingen. [Azure activiteitenlogboeken](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs) is een voorbeeld van dit type van het logboek.

-   **Gegevens vlak logboeken** geven inzicht in deze gebeurtenis treedt op als onderdeel van het gebruik van een Azure-resource Hallo Hallo-gebeurtenissen. Voorbeelden van dit type van het logboek zijn Windows-gebeurtenis systeem, beveiliging, Hallo en toepassingslogboeken op een virtuele machine en Hallo [diagnostische logboeken](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs) geconfigureerd via de Azure-Monitor


-   **Verwerkte gebeurtenissen** geven informatie over geanalyseerde gebeurtenissen /-waarschuwingen die zijn verwerkt namens jou. Voorbeelden van dit type zijn [Azure Security Center Alerts](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts) waar [Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-intro) heeft verwerkt en uw abonnement geanalyseerd en biedt beknopte beveiligingswaarschuwingen

Hallo volgende tabel belangrijkste lijsttype logboeken beschikbaar in Azure.

| Logboek categorie | Logboektype | Sleutelgebruik | Integratie |
| ------------ | -------- | ------ | ----------- |
|[Activiteitenlogboeken](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs)|Besturingselement vlak gebeurtenissen op Azure Resource Manager-resources| Bieden inzicht in Hallo-bewerkingen die zijn uitgevoerd op resources in uw abonnement.|   Rest-API & [Azure Monitor](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs)|
|[Azure diagnostische logboeken](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)|regelmatig gegevens over Hallo werking van Azure Resource Manager-resources in abonnement| Inzicht bieden in bewerkingen dat de bron zelf uitgevoerd| Azure Monitor [stroom](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)|
|[AAD-rapportage](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-reporting-azure-portal)|Logboeken en rapporten|Gebruiker aanmelden activiteiten & systeem activiteit informatie over gebruikers- en groepsbeheer|[Graph API](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-graph-api-quickstart)|
|[Virtuele Machine & Cloudservices](https://docs.microsoft.com/en-us/azure/cloud-services/cloud-services-dotnet-diagnostics-storage)|Windows-gebeurtenislogboek & Linux Syslog|  Vastleggen van systeemgegevens van het en logboekregistratie op Hallo virtuele machines en die gegevens overgebracht naar een opslagaccount van uw keuze.| Met behulp van Windows [af](https://docs.microsoft.com/en-us/azure/azure-diagnostics) (Windows Azure Diagnostics opslag)- en Linux in Azure monitor|
|[Storage Analytics](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/storage-analytics)|Logboekregistratie voor opslag en metrische gegevens voor een opslagaccount biedt|Biedt inzicht in de trace-aanvragen trends in gebruik analyseren en onderzoeken van problemen met uw opslagaccount.|  REST-API of Hallo [clientbibliotheek](https://msdn.microsoft.com/en-us/library/azure/mt347887.aspx)|
|[NSG (Netwerkbeveiligingsgroep) stroom-Logboeken](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-nsg-flow-logging-overview)|JSON-indeling en ziet u per regel op basis van een binnenkomende en uitgaande stromen|Informatie weergeven over inkomende en uitgaande IP-verkeer via een Netwerkbeveiligingsgroep|[Netwerk-Watcher](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-monitoring-overview)|
|[Toepassing inzicht](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-overview)|Logboeken, uitzonderingen en aangepaste diagnostische gegevens|  Application Performance (APM)-service voor webontwikkelaars op meerdere platforms.| REST-API [Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-azure-and-power-bi/)|
|Gegevens verwerken / beveiligingswaarschuwing| Azure Security Center-waarschuwing, OMS-waarschuwing| Informatie over beveiliging en waarschuwingen.|   REST-API's, JSON|

### <a name="activity-log"></a>Activiteitenlogboek
Hallo [Azure Activity Log](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs), biedt inzicht in het Hallo-bewerkingen die zijn uitgevoerd op resources in uw abonnement. Hallo activiteitenlogboek heette vroeger 'Controlelogboeken' of 'Operationele Logs', omdat deze rapporten [besturingselement vlak gebeurtenissen](https://driftboatdave.com/2016/10/13/azure-auditing-options-for-your-custom-reporting-needs/) voor uw abonnementen. Hallo activiteitenlogboek gebruikt, u kunt bepalen Hallo ' wat, wie, en wanneer ' voor een (PUT, POST, verwijderen schrijfbewerkingen) die zijn gemaakt op Hallo van resources in uw abonnement. U kunt ook Hallo status Hallo-werking en andere relevante eigenschappen begrijpen. Hallo activiteitenlogboek omvat geen leesbewerkingen (GET).

VERWIJDEREN van de PUT, POST, verwijst hier tooall Hallo-schrijfbewerkingen activiteitenlogboek op Hallo bronnen bevat. Bijvoorbeeld, kunt u Hallo activiteit logboeken toofind een fout bij het oplossen van of toomonitor hoe een gebruiker in uw organisatie een resource gewijzigd.

![Activiteitenlogboek](./media/azure-log-audit/azure-log-audit-fig1.png)


U kunt gebeurtenissen ophalen uit uw activiteitenlogboek hello Azure-portal met [CLI](https://docs.microsoft.com/azure/storage/storage-azure-cli), PowerShell-cmdlets en [REST-API van Azure-Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-rest-api-walkthrough). Activiteitenlogboeken hebben Gegevensretentieperiode 19 dagen.

Integratiescenario 's
-   [Maak een e-mailadres of webhook waarschuwing die uit een Activity Log-gebeurtenis wordt geactiveerd.](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-auditlog-to-webhook-email)

-   [Deze tooan Event Hub stream](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-stream-activity-logs-event-hubs) voor opname door een service van derden of aangepaste analytics-oplossing zoals Power BI.

-   Analyseren in Power BI met Hallo [Power BI-inhoudspakket.](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs/)

-   [Sla het tooa Storage-Account voor archivering of handmatig inspectie.](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-archive-activity-log) Hallo bewaartijd (in dagen) met behulp van logboek-profielen, kunt u opgeven.

-   Opvragen en weergeven in hello Azure-portal.

-   Deze query's uitvoeren via PowerShell-Cmdlet, CLI of REST-API.

-   Hallo activiteitenlogboek met logboek profielen te exporteren[Meld Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview).

Kunt u een opslagaccount of [event hub naamruimte](https://docs.microsoft.com/azure/event-hubs/event-hubs-resource-manager-namespace-event-hub-enable-archive) die zich niet in hetzelfde abonnement Hallo als één importeerbereik logboek Hallo. Hallo-gebruiker die Hallo instelling configureert moet beschikken over relevante Hallo [RBAC](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure) toegang tot tooboth abonnementen
### <a name="azure-diagnostic-logs"></a>Azure diagnostische logboeken
Azure logboeken met diagnostische gegevens worden gegenereerd door een resource die uitgebreide, regelmatig gegevens over Hallo-bewerking van de bron. Hallo-inhoud van deze logboeken varieert per resourcetype (bijvoorbeeld [Windows-gebeurtenislogboeken system](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-windows-events)één categorie van diagnostische logboeken zijn voor virtuele machines en [blob, table en queue logboeken](https://docs.microsoft.com/azure/storage/storage-monitor-storage-account) categorieën van diagnostische logboeken zijn voor de storage-accounts) en verschillen van Hallo activiteitenlogboek die biedt inzicht in het Hallo-bewerkingen die zijn uitgevoerd op resources in uw abonnement.

![Azure diagnostische logboeken](./media/azure-log-audit/azure-log-audit-fig2.png)

Azure Diagnostics-logboeken bieden verschillende configuratieopties die, Azure portal, met behulp van PowerShell-opdrachtregelinterface (CLI) en REST-API.

**Integratiescenario 's**
-   Deze tooa opslaan [Opslagaccount](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-archive-diagnostic-logs) voor inspectie controle of handmatig. U kunt Hallo bewaartijd (in dagen) met behulp van de diagnostische instellingen Hallo opgeven.

-   [Stream ze tooEvent Hubs](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs) voor opname door een service van derden of aangepaste analytics-oplossing zoals [Power BI.](https://powerbi.microsoft.com/documentation/powerbi-azure-and-power-bi/)

-   Analyseer ze met [OMS-logboekanalyse.](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview)

**Services, ondersteund schema voor diagnostische logboeken en ondersteunde logboek categorieën per resourcetype**


| Service | Schema & Docs | Resourcetype | Category |
| ------- | ------------- | ------------- | -------- |
|Load balancer| [Log analytics voor Azure Load Balancer (Preview)](https://docs.microsoft.com/en-us/azure/load-balancer/load-balancer-monitor-log)|Microsoft.Network/loadBalancers|  LoadBalancerAlertEvent|
|||Microsoft.Network/loadBalancers| LoadBalancerProbeHealthStatus
|Netwerkbeveiligingsgroepen|[Logboekanalyses voor netwerkbeveiligingsgroepen (NSG's)](https://docs.microsoft.com/en-us/azure/virtual-network/virtual-network-nsg-manage-log)|Microsoft.Network/networksecuritygroups|NetworkSecurityGroupEvent|
|||Microsoft.Network/networksecuritygroups|NetworkSecurityGroupRuleCounter|
|Toepassingsgateways|[Logboekregistratie van diagnostische gegevens voor de toepassingsgateway](https://docs.microsoft.com/en-us/azure/application-gateway/application-gateway-diagnostics)|Microsoft.Network/applicationGateways|ApplicationGatewayAccessLog|
|||Microsoft.Network/applicationGateways|ApplicationGatewayPerformanceLog|
|||Microsoft.Network/applicationGateways|ApplicationGatewayFirewallLog|
|Key Vault|[Logboekregistratie van Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-logging)|Microsoft.KeyVault/vaults|AuditEvent|
|Azure Search|[Inschakelen en gebruiken van Search Traffic Analytics](https://docs.microsoft.com/en-us/azure/search/search-traffic-analytics)|Microsoft.Search/searchServices|OperationLogs|
|Data Lake Store|[Toegang tot diagnoselogboeken voor Azure Data Lake Store](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-diagnostic-logs)|Microsoft.DataLakeStore/accounts|Controleren|
|Data Lake Analytics|[Diagnostische logboeken openen voor Azure Data Lake Analytics](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-diagnostic-logs)|Microsoft.DataLakeAnalytics/accounts|Controleren|
|||Microsoft.DataLakeAnalytics/accounts|Aanvragen|
|||Microsoft.DataLakeStore/accounts|Aanvragen|
|Logic Apps|[Aangepast Logic Apps B2B-volgschema](https://docs.microsoft.com/en-us/azure/logic-apps/logic-apps-track-integration-account-custom-tracking-schema)|Microsoft.Logic/workflows|WorkflowRuntime|
|||Microsoft.Logic/integrationAccounts|IntegrationAccountTrackingEvents|
|Azure Batch|[Diagnostische logboekregistratie van Azure Batch](https://docs.microsoft.com/en-us/azure/batch/batch-diagnostics)|Microsoft.Batch/batchAccounts|ServiceLog|
|Azure Automation|[Log analytics voor Azure Automation](https://docs.microsoft.com/en-us/azure/automation/automation-manage-send-joblogs-log-analytics)|Microsoft.Automation/automationAccounts|JobLogs|
|||Microsoft.Automation/automationAccounts|JobStreams|
|Event Hubs|[Diagnostische logboeken van Azure Event Hubs](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-diagnostic-logs)|Microsoft.EventHub/namespaces|ArchiveLogs|
|||Microsoft.EventHub/namespaces|OperationalLogs|
|Stream Analytics|[Diagnostische logboeken van taak](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-job-diagnostic-logs)|Microsoft.StreamAnalytics/streamingjobs|Uitvoering|
|||Microsoft.StreamAnalytics/streamingjobs|Ontwerpen|
|Service Bus|[Diagnostische logboeken van Azure Service Bus](https://docs.microsoft.com/en-us/azure/service-bus-messaging/service-bus-diagnostic-logs)|Microsoft.ServiceBus/namespaces|OperationalLogs|

### <a name="azure-active-directory-reporting"></a>Azure Active Directory-rapportage
Azure Active Directory (Azure AD) bevat beveiligings-, activiteits- en controlerapporten voor uw directory. Hallo [Azure Active Directory-controlerapport](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-guide) helpt klanten tooidentify bevoegde acties die is opgetreden in Azure Active Directory. Bevoegdheden omvatten wijzigingen van de uitbreiding van bevoegdheden (bijvoorbeeld het maken of opnieuw instellen van wachtwoorden), het wijzigen van beleidsconfiguraties (bijvoorbeeld wachtwoordbeleid) of wijzigingen toodirectory configuratie (bijvoorbeeld wijzigingen toodomain federation instellingen).

Hallo-rapporten geven Hallo controlerecord voor gebeurtenisnaam hello, Hallo actor die Hallo actie, Hallo doelbron beïnvloed door wijziging van de Hallo en Hallo datum en tijd (in UTC) heeft uitgevoerd. Klanten kunnen tooretrieve Hallo lijst van de controlegebeurtenissen voor Azure Active Directory via Hallo zijn [Azure-portal](https://portal.azure.com/), zoals beschreven in [uw logboeken Audit](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-azure-portal). Hier volgt een lijst met opgenomen Hallo-rapporten:

| Beveiligingsrapporten | Activiteitsrapporten | Controlerapporten |
| :--------------- | :--------------- | :------------ |
|Aanmeldingen van onbekende bronnen| Toepassingsgebruik: samenvatting| Directorycontrolerapport|
|Aanmeldingen na meerdere mislukte pogingen|  Toepassingsgebruik: gedetailleerd||
|Aanmeldingen vanuit meerdere locaties|    Toepassingsdashboard||
|Aanmeldingen van IP-adressen met verdachte activiteit|   Fouten bij het inrichten van een account||
|Onregelmatige aanmeldingsactiviteiten|    Afzonderlijke gebruikersapparaten||
|Aanmeldingen vanaf mogelijk geïnfecteerde apparaten|   Afzonderlijke gebruikersactiviteiten||
|Gebruikers met afwijkende aanmeldingsactiviteiten| Rapport met groepsactiviteiten||
||Rapport voor de registratie van opnieuw ingestelde wachtwoorden||
||Activiteit voor wachtwoord opnieuw instellen|||

Hallo-gegevens van deze rapporten kunnen nuttig tooyour toepassingen, zoals de SIEM-systemen, controle en hulpprogramma's voor bedrijfsinformatie worden. Hello Azure AD rapportage-API's bieden toegang op programmeerniveau toohello gegevens via een set op basis van REST-API's. U kunt deze aanroepen [API's](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-api-getting-started) van verschillende programmeertalen en hulpprogramma's.

Gebeurtenissen in hello Azure AD-controlerapport worden bewaard gedurende 180 dagen.

> [!Note]
> Zie voor meer informatie over de bewaarperiode op rapporten [bewaarbeleid voor Azure Active Directory rapport.](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-retention)

Voor klanten die de bij het opslaan van de controlegebeurtenissen voor langere bewaartermijn, hello rapportage-API kan worden gebruikt tooregularly pull [controlegebeurtenissen](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-audit-events) in een afzonderlijke gegevensarchief.

### <a name="virtual-machine-logs-using-azure-diagnostics"></a>Virtuele Machine logboeken met behulp van Azure Diagnostics
[Azure Diagnostics](https://docs.microsoft.com/azure/azure-diagnostics) Hallo mogelijkheid binnen Azure waarmee Hallo verzamelen van diagnostische gegevens op een geïmplementeerde toepassing is. U kunt Hallo-extensie voor diagnostische gegevens uit verschillende bronnen. Op dit moment ondersteund zijn [Azure Cloud Service-Web- en werkrollen](https://docs.microsoft.com/azure/cloud-services/cloud-services-choose-me),

![Virtuele Machine logboeken met behulp van Azure Diagnostics](./media/azure-log-audit/azure-log-audit-fig3.png)

[Virtuele Machines in Azure](https://azure.microsoft.com/documentation/learning-paths/virtual-machines/) met Microsoft Windows en [Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-overview).

U diagnostische Azure kunt inschakelen op een virtuele machine met volgende:

-   Met Visual Studio, Zie [Gebruik Visual Studio tootrace Azure Virtual Machines](https://docs.microsoft.com/azure/vs-azure-tools-debug-cloud-services-virtual-machines)

-   [Instellen van Azure Diagnostics op een Azure virtuele Machine op afstand](https://docs.microsoft.com/azure/virtual-machines-dotnet-diagnostics)

-   [Gebruik PowerShell tooset van diagnostische gegevens op Azure Virtual Machines](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-ps-extensions-diagnostics?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

-   [Een Windows virtuele machine met de controle en diagnostische gegevens met Azure Resource Manager-sjabloon maken](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-extensions-diagnostics-template?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="storage-analytics"></a>Storage Analytics
[Azure Storage Analytics](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics) voert logboekregistratie en voorziet in metrische gegevens voor een opslagaccount. U kunt deze gegevensaanvragen tootrace gebruiken, trends in gebruik analyseren en vaststellen van problemen met uw opslagaccount. Logboekregistratie van Storage Analytics is beschikbaar voor Hallo [services Blob, wachtrijen en tabellen.](https://docs.microsoft.com/azure/storage/storage-introduction) Storage Analytics registreert gedetailleerde informatie over geslaagde en mislukte aanvragen tooa storage-service.

Deze informatie kan worden gebruikt toomonitor afzonderlijke aanvragen en toodiagnose problemen met de storage-service. Aanvragen worden geregistreerd op basis van best-effort. Logboekvermeldingen worden alleen gemaakt als er ten opzichte van de service-eindpunt Hallo aanvragen zijn. Als u een opslagaccount heeft een activiteit in de Blob-eindpunt maar niet in de tabel of een wachtrij-eindpunten alleen logboeken die betrekking hebben wordt bijvoorbeeld toohello Blob-service gemaakt.

toouse Storage Analytics, moet u deze inschakelen voor elke service wilt u afzonderlijk toomonitor. U kunt ze inschakelen in Hallo [Azure-portal](https://portal.azure.com/); voor meer informatie Zie [bewaken van een opslagaccount in hello Azure-portal.](https://docs.microsoft.com/azure/storage/storage-monitor-storage-account) U kunt ook Opslaganalyse programmatisch via Hallo REST-API of clientbibliotheek Hallo inschakelen. Hallo-Service-eigenschappen instellen bewerking tooenable Storage Analytics afzonderlijk gebruiken voor elke service.

Hallo wordt geaggregeerde gegevens opgeslagen in een bekende blob (voor logboekregistratie) en in een bekende tabellen (voor metrische gegevens) waartoe toegang kunnen worden verkregen met behulp van Hallo Blob-service en service API's van de tabel.

Storage Analytics heeft een limiet van 20 TB op Hallo en de hoeveelheid opgeslagen gegevens die onafhankelijk is van de totale Hallo-limiet voor uw opslagaccount. Alle logboeken worden opgeslagen in [blok-blobs](https://docs.microsoft.com/azure/storage/storage-analytics) in een container met de naam $logs, die automatisch worden gemaakt wanneer Opslaganalyse is ingeschakeld voor een opslagaccount.

> [!Note]
> Zie voor meer informatie over facturering en bewaarbeleid voor gegevens [Storage Analytics en facturering.](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-and-billing)
>
> [!Note]
> Zie voor meer informatie over opslagaccountlimieten [Azure Storage Scalability and Performance Targets.](https://docs.microsoft.com/azure/storage/storage-scalability-targets)

Hallo volgende typen geverifieerde en anonieme aanvragen worden geregistreerd.



| Geverifieerd  | Anonieme|
| :------------- | :-------------|
| Geslaagde aanvragen | Geslaagde aanvragen |
|Mislukte aanvragen, met inbegrip van de time-outperiode, beperking, netwerk, autorisatie en andere fouten | -Aanvragen via een Shared Access Signature (SAS), met inbegrip van mislukte en geslaagde aanvragen |
| -Aanvragen via een Shared Access Signature (SAS), met inbegrip van mislukte en geslaagde aanvragen |Time-out fouten voor zowel client als server |
|   Aanvragen tooanalytics gegevens |    GET-aanvragen is mislukt met foutcode 304 (niet gewijzigd) |
| Aanvragen door Storage Analytics zelf, zoals logboekbestanden worden gemaakt of verwijderd, worden niet geregistreerd. Een volledige lijst met Hallo geregistreerd gegevens wordt beschreven in Hallo [Storage Analytics geregistreerde bewerkingen en statusberichten](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-logged-operations-and-status-messages) en [Storage Analytics logboekindeling](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-log-format) onderwerpen. | Alle andere mislukte anonieme aanvragen worden niet geregistreerd. Een volledige lijst met Hallo geregistreerd gegevens wordt beschreven in Hallo [Storage Analytics geregistreerde bewerkingen en statusberichten](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-logged-operations-and-status-messages) en [Storage Analytics logboekindeling](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-log-format). |

### <a name="azure-networking-logs"></a>Azure VPN-Logboeken
Netwerk logboekregistratie en controle in Azure is uitgebreid en bevat informatie over twee hoofdcategorieën:

-   [Netwerk-Watcher](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview#network-watcher) -Scenario's gebaseerde netwerkbewaking wordt geleverd bij Hallo-functies in netwerk-Watcher. Deze service omvat pakketopname, volgende hop, IP-stroom controleren, groep beveiligingsweergave, NSG stroom Logboeken. Scenario niveau bewaking biedt een end-tooend-weergave van netwerkbronnen in contrast tooindividual resource netwerkbewaking.

-   [Broncontrole](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview#network-resource-level-monitoring) -niveau Broncontrole bestaat uit vier onderdelen, diagnostische logboeken, metrische gegevens, het oplossen van problemen en resourcestatus. Al deze functies zijn gebouwd op niveau van de bron van de Hallo.

![Azure VPN-Logboeken](./media/azure-log-audit/azure-log-audit-fig4.png)

Netwerk-Watcher is een regionale service waarmee u toomonitor en onderzoeken van voorwaarden op een netwerk scenario niveau in, en naar Azure. Netwerkcontrole en visualisatie hulpprogramma's beschikbaar met de netwerk-Watcher kunnen u begrijpen, diagnoses stellen en krijgen insights tooyour netwerk in Azure.

**Logboekregistratie NSG Flow** -logboeken van de stroom voor Netwerkbeveiligingsgroepen kunt u toocapture gerelateerde tootraffic logboeken die worden toegestaan of geweigerd door Hallo beveiligingsregels voor verbindingen in groep Hallo. Deze stroom logboeken zijn geschreven in JSON-indeling en weergeven van uitgaande en inkomende stromen per regel op basis van een Hallo NIC Hallo stroom is van toepassing op 5-tuple informatie over het Hallo-stroom (bron/het doel-IP, bron/het doel-poort, het Protocol) en als hello verkeer is toegestaan of geweigerd.

### <a name="network-security-group-flow-logging"></a>Netwerkbeveiligingsgroep stroom logboekregistratie

[Netwerkbeveiligingsgroep stroom logboeken](https://docs.microsoft.com/azure/network-watcher/network-watcher-nsg-flow-logging-overview) zijn een functie van netwerk-Watcher waarmee u tooview informatie over inkomende en uitgaande IP-verkeer via een Netwerkbeveiligingsgroep. Deze stroom logboeken zijn geschreven in JSON-indeling en weergeven van uitgaande en inkomende stromen per regel op basis van een Hallo NIC Hallo stroom is van toepassing op 5-tuple informatie over het Hallo-stroom (bron/het doel-IP, bron/het doel-poort, het Protocol) en als hello verkeer is toegestaan of geweigerd.

Terwijl de stroom registreert Netwerkbeveiligingsgroepen doel, worden ze niet weergegeven Hallo dezelfde als Hallo andere logboeken. Stroom logboeken worden opgeslagen alleen binnen een opslagaccount.

Hallo dezelfde bewaarbeleidsregels weergegeven op andere logboeken tooflow logboeken toegepast. Logboeken hebben een bewaarbeleid van 1 dag too365 dagen kan worden ingesteld. Als een bewaarbeleid niet is ingesteld, worden altijd Hallo logboeken gehandhaafd.

**Diagnostische logboeken**

Periodieke en eigen initiatief gebeurtenissen zijn gemaakt door netwerkbronnen en vastgelegd in de storage-accounts, tooan Event Hub of Log Analytics verzonden. Deze logboeken bieden inzicht in het Hallo-status van een resource. Deze logboeken kunnen worden weergegeven in de hulpprogramma's, zoals Power BI en Log Analytics. hoe diagnostische logboeken tooview, gaat u naar toolearn [logboekanalyse.](https://docs.microsoft.com/azure/log-analytics/log-analytics-azure-networking-analytics)

![Diagnostische logboeken](./media/azure-log-audit/azure-log-audit-fig5.png)

Diagnostische logboeken beschikbaar zijn voor [Load Balancer](https://docs.microsoft.com/azure/load-balancer/load-balancer-monitor-log), [Netwerkbeveiligingsgroepen](https://docs.microsoft.com/azure/virtual-network/virtual-network-nsg-manage-log), Routes, en [Application Gateway.](https://docs.microsoft.com/azure/application-gateway/application-gateway-diagnostics)

Netwerk-Watcher biedt dat een diagnostische logboeken weergeven. Deze weergave bevat alle netwerkresources die ondersteuning bieden voor diagnostische gegevens vastleggen. U kunt in deze weergave inschakelen en uitschakelen van netwerkresources snel en gemakkelijk.


In de mogelijkheden voor toevoeging toopreceding logboekregistratie heeft netwerk-Watcher momenteel Hallo volgende mogelijkheden:
- [Topologie](https://docs.microsoft.com/azure/network-watcher/network-watcher-topology-overview) -voorziet in een netwerk niveau weergave tonen Hallo verschillende verbindingskabels en koppelingen tussen netwerkbronnen in een resourcegroep.

- [Variabele pakketopname](https://docs.microsoft.com/azure/network-watcher/network-watcher-packet-capture-overview) -pakketgegevens naar en vanuit een virtuele machine worden vastgelegd. Geavanceerde filteropties en verfijnd besturingselementen zoals kunnen tooset wordt bieden tijd en grootte beperkingen versatility.hello pakketgegevens kunnen worden opgeslagen in een blob-opslag of op de lokale schijf Hallo in de CAP-indeling.

-   [IP-stroom controleert of](https://docs.microsoft.com/azure/network-watcher/network-watcher-ip-flow-verify-overview) -controleert of een pakket wordt toegestaan of geweigerd op basis van stroom informatie 5-tuple pakket parameters (doel-IP, bron-IP, doelpoort, bronpoort en Protocol). Als hello-pakket is geweigerd door een beveiligingsgroep, wordt hello regel en -groep die geweigerd hello-pakket geretourneerd.

-   [Volgende hop](https://docs.microsoft.com/azure/network-watcher/network-watcher-next-hop-overview) -Hallo volgende hop voor pakketten worden gerouteerd in hello Azure Network-Fabric, zodat u toodiagnose een verkeerd geconfigureerde gebruiker gedefinieerde routes bepaalt.

-   [Groep beveiligingsweergave](https://docs.microsoft.com/azure/network-watcher/network-watcher-security-group-view-overview) -Hallo effectieve en toegepaste beveiligingsregels voor verbindingen die worden toegepast op een virtuele machine opgehaald.

-   [Virtuele netwerkgateway en verbinding probleemoplossing](https://docs.microsoft.com/azure/network-watcher/network-watcher-troubleshoot-manage-rest) -Hallo mogelijkheid tootroubleshoot biedt virtuele netwerkgateways en verbindingen.

-   [Netwerk-abonnementen](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview#network-subscription-limits) -kunt u gebruik van netwerkbronnen tooview tegen limieten.

### <a name="application-insight"></a>Toepassing inzicht

[Application Insights](https://docs.microsoft.com/azure/application-insights/app-insights-overview) is een uitbreidbaar Management APM (Application Performance)-service voor webontwikkelaars op meerdere platforms. Gebruik deze toomonitor uw live-webtoepassing. Is het automatisch detecteren afwijkingen. Dit omvat krachtige analytics extra toohelp onderzoeken van problemen en toounderstand met uw app daadwerkelijk wat gebruikers doen.

 Het ontworpen toohelp u continu prestaties en bruikbaarheid verbeteren.

 De Tool werkt voor apps gehost op een groot aantal verschillende platforms, waaronder .NET, Node.js en J2EE, lokaal of in de cloud Hallo. Het kan worden geïntegreerd met uw devOps-proces en verbinding punten toovarious ontwikkelingsprogramma's heeft.

![Toepassing inzicht](./media/azure-log-audit/azure-log-audit-fig6.png)

Application Insights is gericht op Hallo ontwikkelingsteam, toohelp u begrijpen hoe uw app wordt uitgevoerd en hoe deze wordt gebruikt. Met deze service kunt u het volgende controleren:

-   **Aantal aanvragen, reactietijden en foutpercentages** - ga na welke pagina's het populairst zijn op welke tijdstippen van de dag en waar uw gebruikers zich bevinden. Ontdek welke pagina's het beste presteren. Als uw reactietijden en foutpercentages omhoog gaan wanneer er meer aanvragen binnenkomen, hebt u mogelijk te weinig resources.

-   **Aantal afhankelijkheidsrelaties, reactietijden en foutpercentages** - controleer of externe services zorgen voor vertraging.

-   **Uitzonderingen** - analyseren Hallo geaggregeerd statistieken, of Kies specifieke exemplaren en inzoomen Hallo stacktracering en verwante aanvragen. Zowel server- als browseruitzonderingen worden gerapporteerd.

-   **Paginaweergaven en de prestaties bij het laden van pagina’s** - deze gegevens worden gerapporteerd door de browsers van uw gebruikers.

-   **AJAX-aanroepen** van webpagina's - ga na wat het aantal aanroepen, de reactietijden en de foutpercentages zijn.

-   **Aantal gebruikers en sessies**.

-   **Prestatiemeteritems** van uw Windows- of Linux-servers, zoals die voor CPU-, geheugen- en netwerkgebruik.

-   **Diagnostische gegevens van hosts** van Docker of Azure.

-   **Diagnostische traceerlogboeken** van uw app - met behulp hiervan kunt u de samenhang vaststellen tussen traceergebeurtenissen en aanvragen.

-   **Aangepaste gebeurtenissen en metrische gegevens** dat u uzelf in Hallo client of server code, tootrack zakelijke gebeurtenissen schrijven zoals artikelen verkocht of games gewonnen.

**Lijst met integratiescenario's en -beschrijving:**

| Integratiescenario 's | Beschrijving |
| --------------------- | :---------- |
|[De toepassingstoewijzing vast](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-app-map)|Hallo-onderdelen van uw app, met de belangrijkste metrische gegevens en waarschuwingen.||
|[Diagnostische gegevens doorzoeken bijvoorbeeld gegevens](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-diagnostic-search)| U kunt zoeken naar gebeurtenissen, zoals aanvragen, uitzonderingen, afhankelijkheidsaanroepen, logboektraceringen en paginaweergaven en deze gegevens ook filteren.||
|[Metrics Explorer voor geaggregeerde gegevens](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-metrics-explorer)|Verken, filter en segmenteer cumulatieve gegevens, zoals aantallen aanvragen, fouten en uitzonderingen, reactietijden en paginalaadtijden.||
|[Dashboards](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-dashboards#dashboards)|Combineer gegevens van meerdere resources tot een mash-up en deel deze met anderen. Dit is ideaal voor toepassingen met meerdere onderdelen en continue weergegeven in de Hallo team ruimte.||
|[Metrische gegevens livestream](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-live-stream)|Wanneer u een nieuwe build implementeert, bekijk deze indicatoren toomake voor prestaties near-realtime controleren of alles werkt zoals verwacht.||
|[Analytische gegevens](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics)|Beantwoord moeilijke vragen over de prestaties en het gebruik van uw app met behulp van deze krachtige querytaal.||
|[Automatische en handmatige waarschuwingen](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-alerts)|Automatische waarschuwingen aan te passen van tooyour app normale patronen van Telemetrie en trigger wanneer er iets buiten Hallo gebruikelijke patroon. U kunt ook waarschuwingen instellen voor bepaalde niveaus van aangepaste functies of standaardfuncties voor het verzamelen van metrische gegevens.||
|[Visual Studio](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-visual-studio)|Zie prestatiegegevens op Hallo-code. Ga toocode van stack-traces.||
|[Power BI](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-export-power-bi)|Integreer metrische gegevens over het gebruik van de toepassing met andere business intelligence.||
|[REST API](https://dev.applicationinsights.io/)|Schrijf code toorun query's via uw metrische gegevens en de onbewerkte gegevens.||
|[Continue export](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-export-telemetry)|Het exporteren van de onbewerkte gegevens toostorage bulksgewijs wanneer het wordt geleverd.||

### <a name="azure-security-center-alerts"></a>Azure Security Center-waarschuwingen
[Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-intro) automatisch verzamelt, analyseert, en kan worden geïntegreerd logboekgegevens van uw Azure-resources, het Hallo-netwerk en de verbonden partneroplossingen, zoals een firewall en endpoint protection-oplossingen, toodetect Werkelijke dreigingen en beperken Fout-positieven. Een lijst met beveiligingswaarschuwingen in Security Center wordt weergegeven, samen met de Hallo informatie die u nodig tooquickly onderzoeken Hallo probleem en aanbevelingen voor hoe tooremediate een aanval.

Detectie van dreigingen Security Center werkt door het automatisch verzamelen van gegevens van de beveiliging van uw Azure-resources, het Hallo-netwerk en de verbonden partneroplossingen. Deze informatie kunt vaak correleren van gegevens uit meerdere bronnen, tooidentify bedreigingen wordt geanalyseerd. Beveiligingswaarschuwingen worden samen met aanbevelingen voor hoe tooremediate threat Hallo prioriteit in Security Center.

![Azure Security Center](./media/azure-log-audit/azure-log-audit-fig7.png)

Security Center maakt gebruik van geavanceerde beveiligingsanalyses die veel verder gaan dan op handtekeningen gebaseerde benaderingen. Doorbraken in grote hoeveelheden gegevens en [machine learning](https://azure.microsoft.com/blog/machine-learning-in-azure-security-center/) technologieën zijn toegepaste tooevaluate gebeurtenissen op Hallo gehele cloud-infrastructuurresources – bedreigingen die onmogelijk tooidentify handmatige benaderingen en het voorspellen van Hallo detecteren evolutie van aanvallen. Deze beveiligingsanalyses omvatten:

-   **Geïntegreerd dreigingen:** lijkt voor bekende ongewenste actoren door toe te passen wereldwijde dreigingen van Microsoft-producten en services, Microsoft Digital Crimes Unit (DCU), Hallo Hallo Microsoft Security Response Center (MSRC) en externe -feeds.

-   **Gedragsanalyse:** bekende patronen toodiscover schadelijke gedrag van toepassing is.

-   **Afwijkingsdetectie:** maakt gebruik van statistische profilering toobuild historische basislijn. Deze waarschuwing op afwijkingen van vastgestelde basislijnen die potentiële aanvalsvector tooa voldoen.


Veel beveiligingsbewerkingen en respons op incidenten teams afhankelijk van een oplossing Security Information en Event Management (SIEM) als Hallo startpunt voor gesorteerd en beveiligingswaarschuwingen onderzoeken. Klanten kunnen met Azure-logboekanalyse-integratie synchroniseren Security Center-waarschuwingen en beveiligingsgebeurtenissen voor virtuele machine, die zijn verzameld door Azure Diagnostics- en Azure controlelogboeken met hun logboekanalyse of SIEM-oplossing in bijna realtime.


## <a name="log-analytics"></a>Log Analytics

Log Analytics is een service in [Operations Management Suite (OMS)](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) die helpt u bij het verzamelen en analyseren van gegevens die zijn gegenereerd voor resources in uw cloud en on-premises omgevingen. Dit biedt u realtime-inzichten verkrijgen met geïntegreerde zoekfunctie en aangepaste dashboards tooreadily miljoenen records analyseren voor alle werkbelastingen en servers, ongeacht de fysieke locatie.

![Log Analytics](./media/azure-log-audit/azure-log-audit-fig8.png)

Hallo is center logboekanalyse Hallo OMS-opslagplaats, die wordt gehost in hello Azure-cloud. Gegevens worden verzameld in Hallo opslagplaats van verbonden bronnen door configureren gegevensbronnen en toe te voegen oplossingen tooyour abonnement. Gegevensbronnen en oplossingen maakt elk verschillende recordtypen die hun eigen set eigenschappen, maar nog steeds in query's toohello opslagplaats samen kunnen worden geanalyseerd. Hiermee kunt u toouse Hallo dezelfde toowork in hulpprogramma's en -methoden met verschillende soorten gegevens verzameld door verschillende bronnen.

Verbonden bronnen zijn Hallo computers en andere bronnen die gegevens verzameld door logboekanalyse genereren. Het kan hierbij gaan agents zijn geïnstalleerd op [Windows](https://docs.microsoft.com/azure/log-analytics/log-analytics-windows-agents) en [Linux](https://docs.microsoft.com/azure/log-analytics/log-analytics-linux-agents) computers die rechtstreeks verbinding te maken of agents in [een verbonden beheergroep van System Center Operations Manager.](https://docs.microsoft.com/azure/log-analytics/log-analytics-om-agents) Log Analytics kunnen ook worden verzameld van [Azure-opslag.](https://docs.microsoft.com/azure/log-analytics/log-analytics-azure-storage)

[Gegevensbronnen](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources) Hallo verschillende soorten gegevens verzameld van elke bron verbonden zijn. Dit omvat gebeurtenissen en [prestatiegegevens](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-performance-counters) van [Windows](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-windows-events) en Linux-agents in toevoeging toosources zoals [IIS-logboeken](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-iis-logs), en [aangepaste tekstlogboeken.](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-custom-logs) U configureren elke gegevensbron dat u wilt dat toocollect en Hallo configuratie automatisch geleverde tooeach verbonden gegevensbron is.

Er zijn vier verschillende manieren van [verzamelen van Logboeken en metrische gegevens voor Azure-services:](https://docs.microsoft.com/azure/log-analytics/log-analytics-azure-storage)
1.  Azure diagnostics direct tooLog Analytics (diagnostische gegevens in de volgende tabel Hallo)

2.  Azure diagnostics tooAzure opslag tooLog Analytics (opslag in de volgende tabel Hallo)

3.  Connectors voor Azure-services (Connectors in de volgende tabel Hallo)

4.  Scripts toocollect en vervolgens postgegevens in logboekanalyse (lege cellen in de volgende tabel Hallo en voor services die niet worden weergegeven)

| Service | Resourcetype | Logboeken | Metrische gegevens | Oplossing |
| :------ | :------------ | :--- | :------ | :------- |
|Toepassingsgateways|  Microsoft.Network/<br>applicationGateways|  Diagnostiek|Diagnostiek|    [Azure-toepassing](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-networking-analytics#azure-application-gateway-analytics-solution-in-log-analytics) [Analytics Gateway](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-networking-analytics#azure-application-gateway-analytics-solution-in-log-analytics)|
|Application insights||     Connector|  Connector|  [Application Insights](https://blogs.technet.microsoft.com/msoms/2016/09/26/application-insights-connector-in-oms/) [Connector (evaluatie)](https://blogs.technet.microsoft.com/msoms/2016/09/26/application-insights-connector-in-oms/)|
|Automation-accounts|   Microsoft.Automation/<br>AutomationAccounts|    Diagnostiek||       [Meer informatie](https://docs.microsoft.com/en-us/azure/automation/automation-manage-send-joblogs-log-analytics)|
|Batch-accounts|    Microsoft.Batch/<br>batchAccounts|  Diagnostiek|    Diagnostiek||
|Klassieke cloudservices||       Storage||       [Meer informatie](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-storage-iis-table)|
|Cognitive Services|    Microsoft.CognitiveServices/<br>accounts|       Diagnostiek|||
|Data Lake analytics|   Microsoft.DataLakeAnalytics/<br>accounts|   Diagnostiek|||
|Data Lake store|   Microsoft.DataLakeStore/<br>accounts|   Diagnostiek|||
|Event Hub-naamruimte|   Microsoft.EventHub/<br>Naamruimten|  Diagnostiek|    Diagnostiek||
|IoT-Hubs|  Microsoft.Devices/<br>IotHubs||     Diagnostiek||
|Key Vault| Microsoft.KeyVault/<br>Kluizen|  Diagnostiek  || [KeyVault Analytics](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-key-vault)|
|Taakverdelers|    Microsoft.Network/<br>loadBalancers|    Diagnostiek|||
|Logic Apps|    Microsoft.Logic/<br>Werkstromen|  Diagnostiek|    Diagnostiek||
||Microsoft.Logic/<br>integrationAccounts||||
|Netwerkbeveiligingsgroepen|   Microsoft.Network/<br>networksecuritygroups|Diagnostiek||   [Netwerkbeveiligingsgroep Azure Analytics](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-networking-analytics#azure-network-security-group-analytics-solution-in-log-analytics)|
|Recovery kluizen|   Microsoft.RecoveryServices/<br>Kluizen|||[Azure Recovery Services-Analytics (Preview)](https://github.com/krnese/AzureDeploy/blob/master/OMS/MSOMS/Solutions/recoveryservices/)|
|Services zoeken|   Microsoft.Search/<br>searchServices|    Diagnostiek|    Diagnostiek||
|Service Bus-naamruimte| Microsoft.ServiceBus/<br>Naamruimten|    Diagnostiek|Diagnostiek|    [Service Bus Analytics (Preview)](https://github.com/Azure/azure-quickstart-templates/tree/master/oms-servicebus-solution)|
|Service Fabric||       Storage||    [Service Fabric Analytics (Preview)](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-service-fabric)|
|SQL (v12)| Microsoft.Sql/<br>servers /<br>databases||       Diagnostiek||
||Microsoft.Sql/<br>servers /<br>elasticPools||||
|Storage|||         Script| [Azure Storage Analytics (Preview)](https://github.com/Azure/azure-quickstart-templates/tree/master/oms-azure-storage-analytics-solution)|
|Virtuele machines|  Microsoft.Compute/<br>Virtuele machines|  Toestelnummer|  Toestelnummer||
||||Diagnostiek||
|Virtuele Machines-schaalsets|   Microsoft.Compute/<br>Virtuele machines    ||Diagnostiek||
||Microsoft.Compute/<br>virtualMachineScaleSets /<br>Virtuele machines||||
|Webserver-farms|Microsoft.Web/<br>serverfarms||   Diagnostiek
|Web Sites| Microsoft.Web/<br>sites ||      Diagnostiek|    [Meer informatie](https://github.com/Azure/azure-quickstart-templates/tree/master/101-webappazure-oms-monitoring)|
||Microsoft.Web/<br>sites /<br>sleuven|||||


## <a name="log-integration-with-on-premises-siem-systems"></a>Logboek-integratie met on-premises SIEM-systemen
[Integratie van Azure-logboekanalyse](https://www.microsoft.com/download/details.aspx?id=53324) kunt u de onbewerkte logboeken toointegrate van uw Azure-resources op tooyour on-premises **Security Information en Event Management SIEM ()-systemen**.

![Logboek-integratie](./media/azure-log-audit/azure-log-audit-fig9.png)

Integratie van Azure-logboekanalyse verzamelt diagnostische Azure-gegevens van uw Windows (af) virtuele machines, activiteitenlogboeken Azure, Azure Security Center-waarschuwingen en Azure Resource Provider registreert. Deze integratie biedt een uniforme dashboard voor alle activa, lokaal of in Hallo cloud, zodat aggregeren, correleren, analyseren en voor beveiligingsgebeurtenissen waarschuwen.



Azure-logboekanalyse-integratie ondersteunt momenteel integratie van Azure activiteitenlogboeken, Windows-gebeurtenislogboek van Windows virtuele machine in uw Azure-abonnement, de auditlogboeken van Azure Security Center waarschuwingen, Azure diagnostische logboeken en Azure Active Directory.

| Logboektype | Log analytics ondersteuning van JSON (Splunk, ArcSight, Qradar) |
| :------- | :-------------------------------------------------------- |
|AAD-auditlogboeken|    Ja|
|Activiteitenlogboeken| Ja|
|ASC waarschuwingen |Ja|
|Diagnostische logboeken (resource Logboeken)|  Ja|
|VM-Logboeken|   Ja via doorgestuurde gebeurtenissen en niet via JSON|


Hallo volgende tabel beschrijft Hallo logboek categorie en details van SIEM-integratie.

[Aan de slag met Azure-logboekanalyse integratie](https://docs.microsoft.com/azure/security/security-azure-log-integration-get-started) - zelfstudie leert u de installatie van de integratie van Azure-logboekanalyse en integratie van Logboeken vanuit Azure af opslag activiteitenlogboeken Azure, Azure Security Center-waarschuwingen en Azure Active Directory controlelogboeken.

Integratiescenario 's

-   [Partner configuratiestappen](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/) – dit blogbericht leest u hoe tooconfigure Azure integratie toowork Meld met partneroplossingen Splunk, HP ArcSight en IBM QRadar.

-   [Azure-logboekanalyse integratie Veelgestelde vragen (FAQ)](https://docs.microsoft.com/azure/security/security-azure-log-integration-faq) -deze Veelgestelde vragen over de antwoorden op vragen over Azure-logboekanalyse-integratie.

-   [Waarschuwingen met Azure Security Center integreren Meld integratie](https://docs.microsoft.com/azure/security-center/security-center-integrating-alerts-with-log-integration) : dit document leest u hoe toosync Security Center waarschuwingen, samen met de virtuele machine beveiligingsgebeurtenissen die zijn verzameld door Azure Diagnostics- en Azure controlelogboeken met uw logboekanalyse of SIEM-oplossing.

## <a name="next-steps"></a>Volgende stappen

- [Controle en logboekregistratie](https://www.microsoft.com/trustcenter/security/auditingandlogging)

Gegevens beveiligen door het onderhouden van de zichtbaarheid en snel tootimely beveiligingswaarschuwingen reageren

- [Opties voor logboekregistratie en Audit Collection Services-logboek in Azure](https://azure.microsoft.com/resources/videos/security-logging-and-audit-log-collection/)

Welke instellingen moet u ervoor dat uw Azure-exemplaren verzamelt tooenforce-toomake Hallo correct zijn beveiligd en de auditlogboeken.

- [Controle-instellingen voor een siteverzameling configureren](https://support.office.com/article/Configure-audit-settings-for-a-site-collection-A9920C97-38C0-44F2-8BCB-4CF1E2AE22D2?ui=&rs=&ad=US)

Als beheerder van een site een Hallo geschiedenis van acties die door een bepaalde gebruiker kunt ophalen en Hallo geschiedenis van acties die worden uitgevoerd tijdens een bepaald datumbereik kan ook worden opgehaald. 

- [Zoeken Hallo auditlogboek in Office 365-beveiliging Hallo & Compliancecentrum](https://support.office.com/article/Search-the-audit-log-in-the-Office-365-Security-Compliance-Center-0d4d0f35-390b-4518-800e-0c7ec95e946c?ui=&rs=&ad=US)

Een kunt Hallo Office 365-beveiliging & Compliancecentrum toosearch Hallo unified audit log tooview gebruiker en activiteit van de beheerder in uw organisatie Office 365 gebruiken.


