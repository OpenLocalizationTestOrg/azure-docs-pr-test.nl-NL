---
title: aanbevolen procedures voor aaaAzure operationele beveiliging | Microsoft Docs
description: Dit artikel bevat een set met aanbevolen procedures voor operationele Azure-beveiliging.
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
ms.date: 08/04/2017
ms.author: tomsh
ms.openlocfilehash: b3b17ef20fb3545b1c268ac0d7ce692e07c8da00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-operational-security-best-practices"></a>Aanbevolen procedures voor Azure operationele beveiliging
Azure bedrijfsbeveiliging verwijst toohello services, besturingselementen en functies beschikbaar toousers voor het beveiligen van hun gegevens, toepassingen en andere elementen in Microsoft Azure. Azure operationele beveiliging is gebaseerd op een framework dat Hallo kennis die is opgedaan met verschillende mogelijkheden die de unieke tooMicrosoft, met inbegrip van Microsoft Security Development Lifecycle (SDL), Microsoft Security Response Center Hallo Hallo zijn opgenomen programma en grondige kennis van Hallo cybersecurity threat Liggend.

In dit artikel bespreken we een verzameling aanbevolen beveiligingsprocedures voor Azure-database. Deze aanbevolen procedures zijn afgeleid van onze ervaring met beveiliging van de Azure-database en Hallo ervaringen van klanten, zoals zelf.

Voor elke beste kunnen worden uitgelegd:
-   Welke beste Hallo
-   Waarom u wilt dat tooenable die best practices
-   Wat zijn Hallo resultaat als u niet tooenable Hallo aanbevolen
- Hoe meer u tooenable Hallo best practices

In dit artikel Azure operationele Best Practices voor beveiliging is gebaseerd op een advies consensus en mogelijkheden van Azure-platform en functiesets, als deze bestaan in Hallo tijd die in dit artikel is geschreven. Adviezen en technologieën op den duur veranderen en dit artikel worden de wijzigingen op een tooreflect regelmatig wordt bijgewerkt.

Azure operationeel aanbevolen beveiligingsprocedures besproken in dit artikel zijn onder andere:

-   Bewaken, beheren en cloudinfrastructuur beveiligen
-   Identiteiten beheren en implementeren van eenmalige aanmelding (SSO)
-   Trace-aanvragen, trends in gebruik analyseren en problemen identificeren
-   Bewaking van services met een oplossing voor gecentraliseerde controle
-   Detecteren, voorkomen van en reageren toothreats
-   End-to-end scenario's gebaseerde netwerkbewaking
-   Veilig implementeren met de beproefde DevOps-hulpprogramma 's

## <a name="monitor-manage-and-protect-cloud-infrastructure"></a>Bewaken, beheren en cloudinfrastructuur beveiligen
IT Operations is verantwoordelijk voor het beheren van datacenter-infrastructuur, toepassingen en gegevens, inclusief Hallo stabiliteit en beveiliging van deze systemen. Security insights krijgen over de vaak complexe IT-omgevingen verhogen vereist echter organisaties toocobble samen gegevens uit meerdere systemen voor beveiliging en beheer.

[Microsoft Operations Management Suite (OMS)](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) van Microsoft cloud-gebaseerde IT beheeroplossing waarmee u beheren kunt en beveiligen van uw on-premises en cloud-infrastructuur.

[OMS beveiligings- en Audit oplossing](https://docs.microsoft.com/azure/operations-management-suite/oms-security-monitoring-resources) kunnen IT-tooactively bewaken alle resources die kunnen helpen minimaliseren Hallo impact van beveiligingsincidenten. OMS beveiligings- en Audit hebben security-domeinen die kunnen worden gebruikt voor het bewaken van de resources.

Lees voor meer informatie over OMS Hallo-artikel [Operations Management Suite](https://technet.microsoft.com/library/mt484091.aspx).

toohelp u detecteren, voorkomen van en reageren toothreats, [Operations Management Suite (OMS) beveiligings- en Audit oplossing](https://docs.microsoft.com/azure/operations-management-suite/oms-security-getting-started) verzamelt en verwerkt gegevens over uw resources, waaronder:

-   Beveiligingslogboek
-   ETW-gebeurtenissen (Event Tracing for Windows)
-   Controlegebeurtenissen AppLocker
-   Windows Firewall-logboek
-   Advanced Threat Analytics-gebeurtenissen
-   Resultaten van de evaluatie van de basislijn
-   Resultaten van de antimalware-evaluatie
-   Resultaten van de evaluatie van updates/patching
-   Syslog-stromen die expliciet zijn ingeschakeld op het Hallo-agent


## <a name="manage-identity-and-implement-single-sign-on"></a>Identiteiten beheren en implementeren van eenmalige aanmelding
[Azure Active Directory (Azure AD)](https://docs.microsoft.com/azure/active-directory/active-directory-whatis) is Microsoft van meerdere tenants in de cloud-map en identity management-service.

[Azure AD](https://azure.microsoft.com/services/active-directory/) bevat ook een volledige reeks [identiteitsbeheer](https://docs.microsoft.com/azure/security/security-identity-management-overview) mogelijkheden, waaronder [multi-factorauthenticatie](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication), apparaatregistratie, selfservice voor wachtwoordherstel management, self-service groepsbeheer, bevoegd accountmanagement, op rollen gebaseerde toegangsbeheer, toepassingsgebruik bewaking, uitgebreide controle en beveiligingsbewaking en waarschuwingen.

Hallo na mogelijkheden kunt cloud-gebaseerde toepassingen, IT-processen te stroomlijnen, kosten knippen en ervoor te zorgen dat de doelstellingen van de naleving wordt voldaan:

-   Beheer van identiteits- en toegangsbeheer voor Hallo cloud
-   Vereenvoudigen van de gebruiker toegang tooany cloud-app
-   Vertrouwelijke gegevens en toepassingen beveiligen
-   Self-service voor uw werknemers mogelijk maken
-   Integreren met Azure Active Directory

### <a name="identity-and-access-management-for-hello-cloud"></a>Beheer van identiteits- en toegangsbeheer voor Hallo cloud
Azure Active Directory (Azure AD) is een uitgebreide [identiteits- en toegangsbeheer management-cloudoplossing](https://www.microsoft.com/cloud-platform/identity-management), hebt u een set krachtige mogelijkheden toomanage gebruikers en groepen. Het helpt beveiligde toegang tot tooon-premises en cloudtoepassingen, met inbegrip van Microsoft web-services zoals Office 365 en veel niet-Microsoft-software als een dienst (SaaS)-toepassingen.
meer hoe tooenable identiteitsbeveiliging in Azure AD zien toolearn [inschakelen van Azure Active Directory: Identity Protection](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection-enable).

### <a name="simplify-user-access-tooany-cloud-app"></a>Vereenvoudigen van de gebruiker toegang tooany cloud-app
[Eenmalige aanmelding inschakelen](https://docs.microsoft.com/azure/active-directory/active-directory-sso-integrate-saas-apps) toosimplify gebruiker toegang toothousands van cloud-toepassingen van Windows, Mac, Android en iOS-apparaten. Gebruikers kunnen toepassingen starten vanuit een persoonlijke webtoegang Configuratiescherm of mobiele app met zijn bedrijfsreferenties. Gebruik hello Azure AD-toepassingsproxy module toogo afgezien van SaaS-toepassingen en publiceren van lokale toepassingen tooprovide zeer veilige externe webtoegang en eenmalige aanmelding.

### <a name="protect-sensitive-data-and-applications"></a>Vertrouwelijke gegevens en toepassingen beveiligen
Schakel [Azure multi-factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication) tooprevent onbevoegde toegang tot tooon-premises en cloudtoepassingen door te geven van een extra verificatieniveau. Bescherm uw bedrijf met beveiligingsbewaking, meldingen en rapporten op basis van Machine Learning die inconsistente toegangspatronen identificeren om zo potentiële bedreigingen te helpen voorkomen.

### <a name="enable-self-service-for-your-employees"></a>Self-service voor uw werknemers mogelijk maken
Delegeren belangrijke taken tooyour werknemers, zoals het opnieuw instellen van wachtwoorden en groepen maken en beheren. [Wijziging van de selfservice voor wachtwoordherstel inschakelen](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-update-your-own-password)resetten en Self-service groepsbeheer met Azure AD.

### <a name="integrate-with-azure-active-directory"></a>Integreren met Azure Active Directory
Uitbreiden [Active Directory](https://docs.microsoft.com/azure/active-directory/develop/active-directory-how-to-integrate) en andere on-premises mappen tooAzure AD tooenable eenmalige aanmelding voor alle cloud-gebaseerde toepassingen. Gebruikerskenmerken kunnen worden automatisch gesynchroniseerd tooyour clouddirectory van alle soorten on-premises adreslijsten.

meer informatie over de integratie van Azure Active Directory toolearn en hoe tooenable, lees Hallo-artikel [uw on-premises adreslijsten integreren met Azure Active Directory](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect).

## <a name="trace-requests-analyze-usage-trends-and-diagnose-issues"></a>Trace-aanvragen, trends in gebruik analyseren en problemen identificeren
[Azure Storage Analytics](https://docs.microsoft.com/azure/storage/storage-analytics) voert logboekregistratie en voorziet in metrische gegevens voor een opslagaccount. U kunt deze gegevensaanvragen tootrace gebruiken, trends in gebruik analyseren en vaststellen van problemen met uw opslagaccount.

Metrische gegevens Storage Analytics zijn standaard ingeschakeld voor nieuwe storage-accounts. U kunt logboekregistratie inschakelen en configureren van de metrische gegevens en logboekregistratie in hello Azure-portal; Zie voor meer informatie [een opslagaccount in hello Azure-portal bewaken](https://docs.microsoft.com/azure/storage/storage-monitor-storage-account). U kunt ook Opslaganalyse programmatisch via Hallo REST-API of clientbibliotheek Hallo inschakelen. Hallo-Service-eigenschappen instellen bewerking tooenable Storage Analytics afzonderlijk gebruiken voor elke service.

Voor een gedetailleerde richtlijnen voor het gebruik van Storage Analytics en andere hulpprogramma's voor tooidentify, diagnose, en problemen met Azure Storage, Zie [Monitor, vaststellen en oplossen van Microsoft Azure Storage](https://docs.microsoft.com/azure/storage/storage-monitoring-diagnosing-troubleshooting).

meer informatie over de integratie van Azure Active Directory toolearn en hoe de tooenable bij het lezen Hallo artikel [inschakelen en configureren van opslag Analytics](https://docs.microsoft.com/rest/api/storageservices/Enabling-and-Configuring-Storage-Analytics?redirectedfrom=MSDN).

## <a name="monitoring-services"></a>Bewaking van services
Cloud-toepassingen zijn complexe met veel bewegende onderdelen. Monitoring biedt gegevens tooensure die uw toepassing up blijft en wordt uitgevoerd in een foutloze toestand bevindt. Ook kunt u toostave potentiële problemen uitgeschakeld of het oplossen van het verleden zijn. Bovendien kunt u bewaking gegevens toogain uitgebreide statistieken over uw toepassing. Deze kennis kan u helpen de prestaties van toepassingen tooimprove of onderhoud of acties die anders worden handmatige interventie moeten automatiseren.

### <a name="monitor-azure-resources"></a>Azure-resources bewaken
[Monitor voor Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-get-started) hello platformservice en één bron biedt voor het bewaken van de Azure-resources is. Met Azure-Monitor kunt u visualiseren, query, routeren, archiveren en Neem maatregelen op Hallo metrische gegevens en de logboeken die afkomstig zijn van bronnen in Azure. U kunt werken met deze gegevens met behulp van Hallo Monitor portalblade, [Monitor PowerShell-Cmdlets](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-powershell-samples), [platformoverschrijdende CLI](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-cli-samples), of [Monitor REST-API's van Azure](https://msdn.microsoft.com/library/dn931943.aspx).

### <a name="enable-autoscale-with-azure-monitor"></a>Automatisch schalen met monitor voor Azure inschakelen
Schakel [Azure Monitor automatisch schalen](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-autoscale-get-started) geldt alleen toovirtual machineschaalsets (VMSS), cloudservices, app-serviceabonnementen en app service-omgevingen.

### <a name="manage-roles-permissions-and-security"></a>Rollen beheren machtigingen en beveiliging
Veel teams moeten toostrictly [reguleren toegang toomonitoring](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-roles-permissions-security) gegevens en instellingen. Bijvoorbeeld, als er teamleden die werken alleen op de bewaking (ondersteuningsmedewerkers, devops engineers) of als u een provider van beheerde services gebruikt, u ze toegang tot bewakingsgegevens kunt tijdens het beperken van hun mogelijkheid toocreate tooonly toogrant, wijzigen, of resources verwijderen.

Dit toont hoe tooquickly toepassen van een ingebouwde bewaking RBAC-rol tooa gebruiker in Azure of uw eigen aangepaste rol voor een gebruiker aan wie beperkte machtigingen voor controle moet bouwen. Beveiligingsoverwegingen voor uw Azure-Monitor-gerelateerde resources vervolgens besproken en hoe u toegang tot toohello gegevens kunt beperken bevatten.

## <a name="prevent-detect-and-respond-toothreats"></a>Detecteren, voorkomen van en reageren toothreats
Detectie van dreigingen Security Center werkt door het automatisch verzamelen van gegevens van de beveiliging van de Azure-resources, het Hallo-netwerk en verbonden partneroplossingen. Deze analyseert deze gegevens vaak correleren van gegevens uit meerdere bronnen, tooidentify bedreigingen. Beveiligingswaarschuwingen worden samen met aanbevelingen voor hoe tooremediate threat Hallo prioriteit in Security Center.

-   [Een beveiligingsbeleid configureren](https://docs.microsoft.com/azure/security-center/security-center-policies) voor uw Azure-abonnement.
-   Gebruik Hallo [aanbevelingen in Security Center](https://docs.microsoft.com/azure/security-center/security-center-recommendations) toohelp beveiligen van uw Azure-resources.
-   Bekijken en beheren van uw huidige [beveiligingswaarschuwingen](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts).

[Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-intro) helpt u te voorkomen, detecteren, en toothreats reageren met een verhoogde zichtbaarheid van en controle over Hallo beveiliging van uw Azure-resources. Het biedt geïntegreerde beveiligingsbewaking en beleidsbeheer voor uw Azure-abonnementen, helpt bedreigingen te detecteren die anders onopgemerkt zouden blijven, en werkt met een uitgebreid ecosysteem van beveiligingsoplossingen.

Security Center biedt eenvoudig te gebruiken en effectieve bedreiging mogelijkheden voor preventie, detectie en reactie die zijn ingebouwd in tooAzure. De belangrijkste mogelijkheden zijn:

-   Beveiligingsstatus van de cloud begrijpen
-   Neem de controle over cloudbeveiliging
-   Eenvoudig geïntegreerde cloudbeveiligingsoplossingen implementeren
-   Snel bedreigingen detecteren en erop reageren

### <a name="understand-cloud-security-state"></a>Beveiligingsstatus van de cloud begrijpen
Gebruik Azure Security Center tooget een centrale weergave van Hallo beveiligingsstatus van alle Azure-resources. In één oogopslag controleren of Hallo geschikte beveiligingscontroles voorhanden geïnstalleerd zijn en correct geconfigureerd en snel identificeren alle resources die aandacht vereisen.

### <a name="take-control-of-cloud-security"></a>Neem de controle over cloudbeveiliging
Definieer [beveiligingsbeleid](https://docs.microsoft.com/azure/security-center/security-center-policies) voor uw Azure-abonnementen tooyour bedrijf volgens de cloud security behoeften, speciaal afgestemd toohello type toepassingen of vertrouwelijkheid van gegevens Hallo in elk abonnement. Aanbevelingen beleid op basis van beschikbare resources tooguide resource eigenaars per proces van de implementatie van de vereiste besturingselementen hello gebruiken: Hallo verschillende cloud security duren.

### <a name="easily-deploy-integrated-cloud-security-solutions"></a>Eenvoudig geïntegreerde cloudbeveiligingsoplossingen implementeren
[Inschakelen van beveiligingsoplossingen](https://docs.microsoft.com/azure/security-center/security-center-partner-integration) van Microsoft en haar partners, met inbegrip van toonaangevende firewalls en anti-malware. Gebruik gestroomlijnd inrichting toodeploy beveiligingsoplossingen: zelfs netwerken wijzigingen voor u zijn geconfigureerd. De beveiligingsgebeurtenissen van partneroplossingen worden automatisch verzameld voor analyse en waarschuwingsdoeleinden.

### <a name="detect-threats-and-respond-fast"></a>Snel bedreigingen detecteren en erop reageren
Blijf actuele en toekomstige cloudbedreigingen voor met een geïntegreerde, op analyses gebaseerde aanpak. Door een combinatie van Microsoft globale [dreiging intelligence](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities) en expertise met inzichten in cloud beveiligingsgebeurtenissen in uw Azure-implementaties, Security Center helpt u vroeg werkelijke bedreigingen detecteren en fout-positieven te verminderen. Beveiligingswaarschuwingen cloud bieden u inzicht in Hallo aanval campagne, met inbegrip van gerelateerde gebeurtenissen en betrokken resources en stellen manieren tooremediate uitgeeft en snel herstellen.

## <a name="end-to-end-scenario-based-network-monitoring"></a>End-to-end scenario's gebaseerde netwerkbewaking
Een end-to-end-netwerk in Azure opbouwen klanten door te organiseren en samenstellen van verschillende afzonderlijke netwerkbronnen zoals VNet, ExpressRoute, Application Gateway, Load balancers en meer. Bewaking is beschikbaar op elke Hallo netwerkbronnen.

[Netwerk-Watcher](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview) is een regionale service waarmee u toomonitor en onderzoeken van de voorwaarden op een netwerk scenario niveau in naar en van Azure. Netwerkcontrole en visualisatie hulpprogramma's beschikbaar met de netwerk-Watcher kunnen u begrijpen, diagnoses stellen en krijgen insights tooyour netwerk in Azure.

### <a name="automate-remote-network-monitoring-with-packet-capture"></a>Externe netwerkbewaking automatiseren met packetopname
Controle en diagnose van netwerkproblemen zonder tooyour (virtuele machines) met behulp van netwerk-Watcher aanmelden. Trigger [pakketopname](https://docs.microsoft.com/azure/network-watcher/network-watcher-alert-triggered-packet-capture) door waarschuwingen instellen en toegang tooreal-time-prestatiegegevens op pakketniveau Hallo krijgen. Wanneer er een probleem wordt vastgesteld, kunt u dat uitgebreid onderzoeken voor een gedetailleerde diagnose.

### <a name="gain-insight-into-your-network-traffic-using-flow-logs"></a>Inzicht in uw netwerkverkeer met stroomlogboeken
Maken van een beter begrip van uw netwerkverkeer patroon met [Netwerkbeveiligingsgroep stroom logboeken](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-nsg-flow-logging-overview). Informatie die door de stroom logboeken helpt u gegevens op naleving controleren en bewaken van uw netwerk beveiligingsprofiel verzamelen.

### <a name="diagnose-vpn-connectivity-issues"></a>VPN-verbindingsproblemen vaststellen
Netwerk-Watcher biedt u de mogelijkheid te Hallo[vaststellen van de meest voorkomende problemen met VPN-Gateway en verbindingen](https://docs.microsoft.com/azure/network-watcher/network-watcher-diagnose-on-premises-connectivity). Zodat u niet alleen tooidentify Hallo probleem, maar ook toouse gedetailleerde Hallo logboeken gemaakte toohelp verder onderzoek.

meer informatie over hoe toolearn tooconfigure netwerk-watcher en hoe tooenable, lees Hallo-artikel [configureren van netwerk-watcher](https://docs.microsoft.com/azure/network-watcher/network-watcher-create).

## <a name="secure-deployment-using-proven-devops-tools"></a>Veilig implementeren met de beproefde DevOps-hulpprogramma 's
Dit zijn enkele Hallo lijst van Azure DevOps procedures in deze ruimte Microsoft Cloud, waardoor de bedrijven en teams productief en efficiënt.

-   **Infrastructuur als de Code (IaC):** infrastructuur als de Code is een verzameling technieken en procedures waarmee IT-professionals verwijderen Hallo last Hallo dag tooday build en het beheer van modulaire infrastructuur gekoppeld. Deze kunnen IT-professionals toobuild en hun moderne serveromgeving op een manier die lijkt op hoe Softwareontwikkelaars bouwen en onderhouden van toepassingscode beheren. Voor Azure, hebben we [Azure Resource Manager]( https://azure.microsoft.com/documentation/articles/resource-group-authoring-templates/) kunt u tooprovision uw toepassingen met behulp van een declaratief sjabloon. U kunt in één enkele sjabloon meerdere services plus de bijbehorende afhankelijkheden implementeren. U hello gebruiken dezelfde sjabloon toorepeatedly uw toepassing tijdens elke fase van de levenscyclus van de toepassing hello implementeren.
-   **Continue integratie en implementatie:** kunt u uw Visual Studio Online teamprojecten te configureren[automatisch bouwen en implementeren](https://www.visualstudio.com/docs/build/overview) tooAzure web-apps of cloudservices. VSO hello binaire bestanden wordt hierna moet u een build tooAzure na elke inchecken code automatisch wordt geïmplementeerd. Hallo pakket buildproces hier beschreven is gelijkwaardig toohello pakketopdracht in Visual Studio en Hallo publishing stappen zijn equivalent toohello publiceren opdracht in Visual Studio.
-   **Releasebeheer:** Visual Studio [Release Management](https://msdn.microsoft.com/library/vs/alm/release/overview) is een uitstekende oplossing voor implementatie van meerdere fasen automatiseren en beheren van Hallo release proces. Maak beheerde continue implementatie pijplijnen toorelease snel, eenvoudig en vaak. Met de Release Management we onze release-proces veel kunt automatiseren en we kunnen beschikken over vooraf gedefinieerde werkstromen voor goedkeuring. On-premises en toohello implementeren cloud, uitbreiden en aanpassen zoals vereist.
-   **Bewaking van App-prestaties:** problemen detecteren, oplossen van problemen en breng voortdurend verbeteringen aan uw toepassingen. Analyseer snel problemen in uw live-toepassing. Krijg inzicht in wat gebruikers met uw toepassing doen. Configuratie is eenvoudig kwestie van JS code en een webconfig-vermelding toe te voegen en u binnen enkele minuten in de portal met details van alle Hallo Hallo resultaten te zien. [App insights](https://azure.microsoft.com/documentation/articles/app-insights-start-monitoring-app-health-usage/) helpt bedrijven voor een snellere detectie van problemen en herstel.
-   **Laden getest & automatisch schalen:** We vindt prestatieproblemen in onze app tooimprove implementatie kwaliteit en toomake ervoor dat de app is altijd up-to-date of beschikbaar toocater toohello zakelijke behoeften. Zorg ervoor dat uw app voor uw volgende starten of marketing campagne verkeer kan verwerken. Cloud-gebaseerde uitgevoerd [tests laden](https://www.visualstudio.com/docs/test/performance-testing/getting-started/getting-started-with-performance-testing) in bijna geen tijd met Visual Studio Online.

## <a name="next-steps"></a>Volgende stappen
- Meer informatie over [Azure bedrijfsbeveiliging](https://docs.microsoft.com/azure/security/azure-operational-security).
- meer tooLearn [Operations Management Suite | Beveiliging en naleving](https://www.microsoft.com/cloud-platform/security-and-compliance).
- [Aan de slag met beveiliging van Operations Management Suite-oplossing van de Audit en](https://docs.microsoft.com/azure/operations-management-suite/oms-security-getting-started).
