---
title: overzicht van de operationele beveiliging aaaAzure | Microsoft Docs
description: Dit artikel bevat een overzicht van hello Azure operationele beveiliging.
services: security
documentationcenter: na
author: unifycloud
manager: swadhwa
editor: tomsh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: tomsh
ms.openlocfilehash: b91c7889660b32e4933c305007692bd6e1ded05f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-operational-security-overview"></a>Overzicht van Azure operationele beveiliging
Azure bedrijfsbeveiliging verwijst toohello services, besturingselementen en functies beschikbaar toousers voor het beveiligen van hun gegevens, toepassingen en andere elementen in Microsoft Azure. [Azure bedrijfsbeveiliging](https://docs.microsoft.com/azure/security/azure-operational-security) is een framework waarin Hallo kennis die is opgedaan met tal van mogelijkheden die unieke tooMicrosoft zijn, met inbegrip van Microsoft Security Development Lifecycle (SDL), Microsoft Security Hallo Hallo Response Center-programma en grondige kennis van Hallo cyberbeveiliging security threat Liggend.

In dit artikel operationele beveiligingsoverzicht van Azure is gericht op Hallo gebieden te volgen:

- Azure Operations Management Suite
-   Azure Security Center
-   Azure Monitor
-   Azure-netwerk-watcher
-   Azure Storage analytics
-   Azure Active directory

## <a name="azure-operations-management-suite"></a>Azure Operations Management Suite
IT Operations is verantwoordelijk voor het beheren van datacenter-infrastructuur, toepassingen en gegevens, inclusief Hallo stabiliteit en beveiliging van deze systemen. Security insights krijgen over de vaak complexe IT-omgevingen verhogen vereist echter organisaties toocobble samen gegevens uit meerdere systemen voor beveiliging en beheer.

[Microsoft Operations Management Suite (OMS)](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) van Microsoft cloud-gebaseerde IT beheeroplossing waarmee u beheren kunt en beveiligen van uw on-premises en cloud-infrastructuur.

OMS is een beheeroplossing cloud-gebaseerde IT met veel aanbiedingen, zoals de automatisering van IT, beveiliging en naleving, Log Analytics en back-up en herstel. Als zodanig is een perfecte hulp toomanage en uw IT-infrastructuur beveiligen: on-premises en in Hallo cloud.

Hallo kernfunctionaliteit van OMS wordt verstrekt door een set services die worden uitgevoerd in Azure. Elke service biedt een specifieke beheerfunctie en u kunt verschillende scenario's voor services tooachieve combineren. Dit omvat:

-   Log Analytics
-   Automatisering
-   Back-up maken
-   Site Recovery

### <a name="log-analytics"></a>Log Analytics
[Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics) biedt bewakingsservices voor OMS door in een centrale opslagplaats gegevens te verzamelen van beheerde resources. Deze gegevens kan bevatten gebeurtenissen, prestatiegegevens of aangepaste worden geleverd via Hallo API. Zodra verzameld, zijn Hallo gegevens beschikbaar voor waarschuwingen, analyse en exporteren. Deze methode kunt u tooconsolidate gegevens uit diverse bronnen, zodat u gegevens van uw Azure-services met uw bestaande on-premises omgeving combineren kunt. Ook duidelijk scheidt u Hallo verzamelen van gegevens van de Hallo van Hallo actie op die van die gegevens, zodat alle acties beschikbaar tooall soorten gegevens zijn.

### <a name="automation"></a>Automatisering
Microsoft [Azure Automation](https://docs.microsoft.com/azure/automation/automation-intro) biedt een manier voor gebruikers tooautomate Hallo handmatige, langlopende, foutgevoelige en regelmatig herhaalde taken die vaak worden uitgevoerd in een cloud en enterprise-omgeving. Dit bespaart tijd en verhoogt de betrouwbaarheid van regelmatige beheertaken Hallo en deze worden zelfs gepland toobe automatisch uitgevoerd met regelmatige tussenpozen. U kunt processen automatiseren met behulp van runbooks of configuratiebeheer automatiseren met behulp van Desired State Configuration.

### <a name="backup"></a>Back-up
[Azure Backup](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup) Hallo op basis van Azure Service u kunt tooback gebruikt (of beveiligen) en het herstellen van uw gegevens in Hallo Microsoft cloud. Met Azure Backup vervangt u uw bestaande on-premises of off-site back-upoplossing door een betrouwbare, veilige en kostenbesparende cloudoplossing. Azure Backup biedt meerdere onderdelen die u downloadt en implementeert op de desbetreffende computer hello, server of in de cloud Hallo. Hallo-onderdeel of agent, die u implementeert, is afhankelijk van wat u wilt tooprotect. Alle Azure Backup-onderdelen (ongeacht of u gegevens die lokaal beveiligen wilt of in de cloud Hallo) kunnen worden gebruikt tooback up gegevens tooa Recovery Services-kluis in Azure. Zie Hallo [Azure Backup-onderdelen tabel](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup#which-azure-backup-components-should-i-use).

### <a name="site-recovery"></a>Siteherstel
[Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery) biedt bedrijfscontinuïteit door te organiseren replicatie van de lokale virtuele en fysieke machines tooAzure of tooa secundaire site. Als uw primaire site niet beschikbaar is, schakelt u over de secundaire locatie toohello zodat gebruikers kunnen werken blijven en mislukken wanneer systemen tooworking order retourneren. intelligente en effectieve bedreigingsdetectie.

## <a name="azure-active-directory"></a>Azure Active Directory
[Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-enable-sso-scenario) is uitgebreide identiteit als een Service (IDaaS) van Microsoft die:

-   Hiermee kunt u IAM als een cloudservice
-   Voorziet in centraal toegangsbeleid beheer, eenmalige aanmelding (SSO) en rapportage
-   Ondersteunt de geïntegreerde access management voor [duizenden toepassingen](https://azure.microsoft.com/marketplace/active-directory/) in Hallo-toepassingsgalerie, met inbegrip van Salesforce, Google Apps, Box, Concur en meer.

Azure AD bevat ook een volledige reeks [mogelijkheden voor identiteitsbeheer](https://docs.microsoft.com/azure/security/security-identity-management-overview#security-monitoring-alerts-and-machine-learning-based-reports) inclusief [multi-factorauthenticatie](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication), [apparaatregistratie]( https://docs.microsoft.com/azure/active-directory/active-directory-device-registration-overview), [ Selfservice voor wachtwoordherstel management](https://azure.microsoft.com/resources/videos/self-service-password-reset-azure-ad/), [selfservicegroepsbeheer](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-update-your-own-password), [bevoorrecht accountbeheer](https://docs.microsoft.com/azure/active-directory/active-directory-privileged-identity-management-configure), [op rollen gebaseerde toegangsbeheer](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is), [gebruik toepassingsbewaking](https://docs.microsoft.com/azure/active-directory/connect-health/active-directory-aadconnect-health), [uitgebreide controle](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs), en [beveiligingsbewaking en waarschuwingen](https://docs.microsoft.com/azure/operations-management-suite/oms-security-responding-alerts).

Met Azure Active Directory, alle toepassingen u publiceren voor uw partners en klanten (werk of consumer) Hallo hebben dezelfde mogelijkheden voor identiteits- en toegangsbeheer. Dit kunt u toosignificantly uw operationele kosten te verlagen.

## <a name="azure-security-center"></a>Azure Security Center
[Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-get-started) helpt u te voorkomen, detecteren, en toothreats reageren met een verhoogde zichtbaarheid van en controle over Hallo beveiliging van uw Azure-resources. Het biedt geïntegreerde beveiligingsbewaking en beleidsbeheer voor uw abonnementen, helpt bedreigingen te detecteren die anders onopgemerkt zouden blijven, en werkt met een uitgebreid ecosysteem van beveiligingsoplossingen.

[Security Center](https://docs.microsoft.com/azure/security-center/security-center-linux-virtual-machine) helpt u gegevens van de virtuele machine in Azure beveiligt door te geven inzicht in de beveiligingsinstellingen van uw virtuele machine en bewaking voor bedreigingen. Security Center kan uw virtuele machines controleren op:

-   Besturingssysteem (OS) beveiligingsinstellingen Hello aanbevolen configuratieregels
-   Updates voor systeembeveiliging en essentiële updates die ontbreken
-   Aanbevelingen voor eindpuntbeveiliging
-   Validatie voor schijfversleuteling
-   Aanvallen op het netwerk

Maakt gebruik van Azure Security Center [op rollen gebaseerde toegangsbeheer (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure), waarmee u [ingebouwde rollen](https://docs.microsoft.com/azure/active-directory/role-based-access-built-in-roles) die kunnen worden toegewezen toousers, groepen en services in Azure.

Security Center beoordeelt Hallo-configuratie van uw resources tooidentify beveiligingsproblemen en beveiligingsproblemen. In Security Center, ziet u alleen informatie gerelateerd tooa resource wanneer u Hallo rol van eigenaar, bijdrager of lezer Hallo abonnement of resourcegroep beheergroep die deel uitmaakt van een resource te worden toegewezen.

>[!Note]
>Zie [machtigingen in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-permissions) toolearn meer over de functies en de toegestane acties in Security Center.

Security Center gebruikt Hallo Microsoft Monitoring Agent – dit Hallo dezelfde agent wordt gebruikt door Hallo Operations Management Suite en Log Analytics-service is. Gegevens die worden verzameld van deze agent wordt opgeslagen in een bestaande logboekanalyse [werkruimte](https://docs.microsoft.com/azure/log-analytics/log-analytics-manage-access) die zijn gekoppeld aan uw Azure-abonnement of een nieuwe workspace(s), waarbij rekening wordt gehouden account Hallo geolocatie Hallo VM.

## <a name="azure-monitor"></a>Azure Monitor
Prestatieproblemen in uw cloud-app kunnen invloed hebben op uw bedrijf. Degradations kan met meerdere onderdelen onderling verbonden en releases vaak gebeuren op elk gewenst moment. En als u een app ontwikkelt, uw gebruikers problemen die u hebt niet vinden in het testen van meestal te detecteren. U moet weten over deze problemen direct en hulpprogramma's voor het opsporen en oplossen van problemen Hallo hebben.

[Monitor voor Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-azure-monitor) is basic hulpprogramma voor het bewaken van services die worden uitgevoerd op Azure. Dit biedt u niveau van de infrastructuur gegevens over de doorvoer van een service en de omgeving rondom Hallo Hallo. Als u uw apps in Azure beheert, moet u bepalen of tooscale omhoog of omlaag bronnen, Azure Monitor u krijgt dan wat u toostart.

Bovendien kunt u bewaking gegevens toogain uitgebreide statistieken over uw toepassing. Deze kennis kan u helpen de prestaties van toepassingen tooimprove of onderhoud of acties die anders worden handmatige interventie moeten automatiseren. Het bevat:

-   Azure Activity Log
-   Azure diagnostische logboeken
-   Metrische gegevens
-   Azure Diagnostics

### <a name="azure-activity-log"></a>Azure Activity Log
Het is een logboek biedt inzicht in het Hallo-bewerkingen die zijn uitgevoerd op resources in uw abonnement. Hallo [activiteitenlogboek](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs) heette vroeger 'Controlelogboeken' of 'Operationele Logs', omdat het besturingselement vlak gebeurtenissen voor uw abonnementen rapporten.

### <a name="azure-diagnostic-logs"></a>Azure diagnostische logboeken
[Azure diagnostische logboeken](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs) worden gegenereerd door een resource en leveren rijke, regelmatig gegevens over Hallo-bewerking van de bron. Hallo-inhoud van deze logboeken varieert per resourcetype.

Bijvoorbeeld Windows-gebeurtenislogboeken system zijn één categorie van diagnostische logboeken voor virtuele machines en blob, table en queue logboeken zijn categorieën van diagnostische logboeken voor opslagaccounts.

Diagnostische logboeken verschillen van Hallo [activiteitenlogboek (voorheen bekend als het auditlogboek of operationeel logboek)](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs). Hallo activiteitenlogboek verschaft inzicht in het Hallo-bewerkingen die zijn uitgevoerd op resources in uw abonnement. Diagnostische logboeken bieden inzicht in bewerkingen dat de bron zelf uitgevoerd.

### <a name="metrics"></a>Metrische gegevens
Monitor voor Azure kunt u tooconsume telemetrie toogain inzicht in prestaties Hallo en status van uw workloads in Azure. Hallo belangrijkste type Azure telemetriegegevens is Hallo metrische gegevens (ook wel prestatiemeteritems) die door de meeste Azure-resources. Monitor voor Azure biedt verschillende manieren tooconfigure en verbruikt [metrische gegevens](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-metrics) voor bewaking en probleemoplossing.

### <a name="azure-diagnostics"></a>Azure Diagnostics
Het is Hallo-functionaliteit in Azure waarmee Hallo verzamelen van diagnostische gegevens op een geïmplementeerde toepassing. U kunt Hallo-extensie voor diagnostische gegevens uit diverse verschillende bronnen. Op dit moment ondersteund zijn [Azure Cloud Service-Web- en werkrollen](https://docs.microsoft.com/azure/vs-azure-tools-configure-roles-for-cloud-service), [Azure Virtual Machines](https://docs.microsoft.com/azure/vs-azure-tools-configure-roles-for-cloud-service) met Microsoft Windows, en [Service Fabric](https://docs.microsoft.com/azure/monitoring-and-diagnostics/azure-diagnostics).


## <a name="network-watcher"></a>Network Watcher
Een end-to-end-netwerk in Azure opbouwen klanten door te organiseren en samenstellen van verschillende afzonderlijke netwerkbronnen zoals VNet, ExpressRoute, Application Gateway, Load balancers en meer. Bewaking is beschikbaar op elke Hallo netwerkbronnen.

Hallo-endnetwerk tooend kunt complexe configuraties en interacties tussen resources, het maken van complexe scenario's die bewaking op basis van een scenario via netwerk-Watcher nodig hebben.

[Netwerk-Watcher](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview) wordt vereenvoudigt bewaking en het onderzoeken van uw Azure-netwerk. Diagnose- en visualisatie hulpprogramma's beschikbaar met de netwerk-Watcher inschakelen u tootake externe pakket worden vastgelegd op een virtuele Machine van Azure, verkrijg inzicht in het netwerkverkeer met stroom logboeken en onderzoeken van VPN-Gateway en verbindingen.

Netwerk-Watcher heeft momenteel Hallo volgende mogelijkheden:

- [Topologie](https://docs.microsoft.com/azure/network-watcher/network-watcher-topology-overview) -voorziet in een netwerk niveau weergave tonen Hallo verschillende verbindingskabels en koppelingen tussen netwerkbronnen in een resourcegroep.
-   [Variabele pakketopname](https://docs.microsoft.com/azure/network-watcher/network-watcher-packet-capture-overview) -pakketgegevens naar en vanuit een virtuele machine worden vastgelegd. Geavanceerde opties en verfijnd besturingselementen zoals kunnen tooset tijd wordt voor het filteren en beperkingen van de bestandsgrootte veelzijdigheid bieden. Hallo pakketgegevens kunnen worden opgeslagen in een blob-opslag of op Hallo lokale schijf in de CAP-indeling.
-   [IP-stromen controleren](https://docs.microsoft.com/azure/network-watcher/network-watcher-ip-flow-verify-overview) -controleert of een pakket wordt toegestaan of geweigerd op basis van stroom informatie 5-tuple pakket parameters (doel-IP, bron-IP, doelpoort, bronpoort en Protocol). Als hello-pakket is geweigerd door een beveiligingsgroep, wordt hello regel en -groep die geweigerd hello-pakket geretourneerd.
-   [Volgende hop](https://docs.microsoft.com/azure/network-watcher/network-watcher-next-hop-overview) -Hallo volgende hop voor pakketten worden gerouteerd in hello Azure Network-Fabric, zodat u toodiagnose een verkeerd geconfigureerde gebruiker gedefinieerde routes bepaalt.
-   [Groep beveiligingsweergave](https://docs.microsoft.com/azure/network-watcher/network-watcher-security-group-view-overview) -Hallo effectieve en toegepaste beveiligingsregels voor verbindingen die worden toegepast op een virtuele machine opgehaald.
-   [Logboekregistratie NSG Flow](https://docs.microsoft.com/azure/network-watcher/network-watcher-nsg-flow-logging-overview) -logboeken van de stroom voor Netwerkbeveiligingsgroepen kunt u toocapture gerelateerde tootraffic logboeken die worden toegestaan of geweigerd door Hallo beveiligingsregels voor verbindingen in groep Hallo. Hallo-stroom wordt gedefinieerd door de gegevens van een 5-tuple: bron-IP, doel-IP, bronpoort, doelpoort en -Protocol.
-   [Virtuele netwerkgateway en verbinding probleemoplossing](https://docs.microsoft.com/azure/network-watcher/network-watcher-troubleshoot-manage-rest) -Hallo mogelijkheid tootroubleshoot biedt virtuele netwerkgateways en verbindingen.
-   [Netwerk-abonnementen](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview) -kunt u gebruik van netwerkbronnen tooview tegen limieten.
-   [Configureren van diagnostische gegevens logboek](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview) : biedt een enkel deelvenster tooenable of diagnostische logboeken voor netwerkbronnen in een resourcegroep uitschakelen.

hoe meer tooconfigure netwerk-watcher ziet, toolearn [configureren van netwerk-watcher](https://docs.microsoft.com/azure/network-watcher/network-watcher-create).

## <a name="developer-operations-devops"></a>Developer-bewerkingen (DevOps)
Eerdere tooDevOps toepassingsontwikkeling, teams zijn verantwoordelijk voor het verzamelen van zakelijke vereisten voor een softwareprogramma en schrijven van code. Een afzonderlijk QA-team test vervolgens Hallo programma in een geïsoleerde ontwikkelingsomgeving als vereisten is voldaan en releases Hallo code voor bewerkingen toodeploy. Hallo-implementatieteam meer gefragmenteerd zijn in siloed groepen zoals netwerk- en database. Telkens wanneer een softwareprogramma 'gegenereerd via Hallo wanden' tooan onafhankelijke team knelpunten wordt toegevoegd.

[DevOps](https://www.visualstudio.com/learn/what-is-devops/) kunt teams toodeliver veiliger, hogere kwaliteit oplossingen sneller en goedkoper. Klanten verwachten een dynamische en betrouwbare ervaring wanneer software en -services worden verbruikt.  Software-updates snel teams moeten herhalen meten Hallo gevolgen van het Hallo-updates en snel reageren met nieuwe ontwikkeling iteraties tooaddress problemen of meer waarde bieden.  Cloud platformen, zoals Microsoft Azure hebt verwijderd van de traditionele knelpunten en geholpen commoditize infrastructuur. Software presteert minder in elk bedrijf als belangrijkste onderscheid en factor in bedrijfsresultaten Hallo. Geen organisatie, developer of IT-worker kunt of Hallo DevOps verkeer moet worden voorkomen.

Professionals in volwassen DevOps vast aantal Hallo procedures te volgen. Deze procedures [personen omvatten](https://www.visualstudio.com/learn/what-is-devops-culture/) tooform strategieën op basis van Hallo bedrijfsscenario's.  Tooling kan worden geautomatiseerd Hallo verschillende procedures:

-   [Flexibele planning en projectbeheer](https://www.visualstudio.com/learn/what-is-agile/) technieken zijn gebruikte tooplan en werk in sprints isoleren, team capaciteit beheren en kunnen teams snel aan te passen toochanging zakelijke behoeften.
-   [Versiebeheer, meestal met Git](https://www.visualstudio.com/learn/what-is-git/), kunnen zich ergens in hello world tooshare bron teams en integreren met software development tools tooautomate Hallo release pipeline.
-   [Continue integratie](https://www.visualstudio.com/learn/what-is-continuous-integration/) stations Hallo lopende samenvoegen en het testen van code, die toofinding defecte producten vroeg leidt.  Andere voordelen zijn minder tijd verspild op bestrijden samenvoegen problemen en snelle feedback voor ontwikkelteams.
-   [Continue levering](https://www.visualstudio.com/learn/what-is-continuous-delivery/) van softwareoplossingen tooproduction- en testomgevingen waarmee organisaties kunnen snel fouten corrigeren en reageren tooever wijzigen zakelijke vereisten.
-   [Bewaking](https://www.visualstudio.com/learn/what-is-monitoring/) van actieve toepassingen, waaronder productieomgevingen voor toepassingsstatus als klant gebruik help organisaties formulier evenals met een hypothese en snel valideren of strategieën bewijzen.  Uitgebreide gegevens worden vastgelegd en opgeslagen in verschillende indelingen voor logboekregistratie.
-   [Infrastructuur als de Code (IaC)](https://www.visualstudio.com/learn/what-is-infrastructure-as-code/) is een procedure waarmee Hallo automation en validatie van het maken en teardown van netwerken en virtuele machines toohelp met het leveren van beveiligde, stabiele toepassing hosting-platforms.
-   [Microservices](https://www.visualstudio.com/learn/what-are-microservices/) architectuur is overgenomen tooisolate zakelijke gebruiksvoorbeelden in kleine herbruikbare services.  Deze architectuur kunt u schaalbaarheid en efficiëntie.

## <a name="next-steps"></a>Volgende stappen
toolearn meer informatie over OMS beveiligings- en Audit-oplossing, Zie Hallo artikelen te volgen:

- [Operations Management Suite | Beveiliging en naleving](https://www.microsoft.com/cloud-platform/security-and-compliance).
- [Controle- en reageert tooSecurity waarschuwingen in de beveiliging van Operations Management Suite en Audit oplossing](https://docs.microsoft.com/en-us/azure/operations-management-suite/oms-security-responding-alerts).
- [Bewaking van Resources in de beveiliging van Operations Management Suite en Audit oplossing](https://docs.microsoft.com/en-us/azure/operations-management-suite/oms-security-monitoring-resources).
