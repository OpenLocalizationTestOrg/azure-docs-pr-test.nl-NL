---
title: aaaWhat werkbelastingen kunnen u met Azure Site Recovery beveiligen?
description: "Azure Site Recovery beveiligt uw workloads en toepassingen door een coördinatie Hallo replicatie, failovers en herstel van on-premises virtuele machines en fysieke servers tooAzure of tooa secundaire on-premises site"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: cfreeman
editor: 
ms.assetid: 4953948f-26c0-4699-8fe7-59d3bfc1d3da
ms.service: site-recovery
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/08/2017
ms.author: raynew
ms.openlocfilehash: cab2e1ce3c2b7b2c5f899d957219f5c12eb5965c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="what-workloads-can-you-protect-with-azure-site-recovery"></a>Welke workloads kunt u met Azure Site Recovery beveiligen?
Dit artikel wordt beschreven werkbelastingen en toepassingen die u Hello Azure Site Recovery-service repliceren kunt.

Eventuele opmerkingen of vragen plaatsen onderin Hallo van dit artikel of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="overview"></a>Overzicht
Organisaties moeten een zakelijke continuïteit en disaster recovery (BCDR) strategie tookeep workloads en gegevens veilig en beschikbaar tijdens geplande en ongeplande uitval, en tooregular werkomstandigheden zo snel mogelijk te herstellen.

Site Recovery is een Azure-service die tooyour BCDR-strategie bijdraagt. Met Site Recovery kunt implementeren u toepassingsgevoelige replicatie toohello cloud of tooa secundaire site. Hiermee wordt aangegeven of uw apps zijn Windows of op basis van Linux, uitgevoerd op fysieke servers, VMware- of Hyper-V, u kunt Site Recovery tooorchestrate replicatie gebruiken disaster recovery tests uitvoeren en uitvoeren van failovers en failbacks.

Site Recovery kan worden geïntegreerd met diverse Microsoft-toepassingen, waaronder SharePoint, Exchange, Dynamics, SQL Server en Active Directory. Microsoft werkt ook nauw samen met toonaangevende leveranciers zoals Oracle, SAP, IBM en Red Hat. U kunt replicatie-oplossingen per app aanpassen.

## <a name="why-use-site-recovery-for-application-replication"></a>Waarom u Site Recovery moet gebruiken voor het repliceren van toepassingen
Site Recovery draagt bij tooapplication beveiliging en herstel als volgt:

* Toepassingsonafhankelijk, met replicatie voor alle workloads die worden uitgevoerd op een ondersteunde machine.
* Bijna-synchrone replicatie met RPO's van 30 seconden toomeet Hallo behoeften van de meest kritieke zakelijke apps.
* Toepassingsconsistente momentopnamen voor toepassingen met één of meer lagen.
* Integratie met SQL Server AlwaysOn en samenwerking met replicatietechnologieën die op toepassingsniveau actief zijn, waaronder AD-replicatie, SQL AlwaysOn, Exchange Database-beschikbaarheidsgroepen (DAG’s) en Oracle Data Guard.
* Flexibele herstelplannen waarmee u toorecover een volledige-toepassing met een enkele klik stapelen en tooinclude externe scripts en handmatige acties opnemen in het Hallo-plan.
* Geavanceerd netwerkbeheer in Site Recovery en Azure toosimplify configureren netwerkvereisten voor apps, inclusief Hallo mogelijkheid tooreserve IP-adressen-taakverdeling en de integratie met Azure Traffic Manager voor laag RTO netwerk dit.
* Een uitgebreide Automation-bibliotheek met toepassingsspecifieke scripts die klaar zijn voor gebruik, en kunnen worden gedownload en geïntegreerd met herstelplannen.

## <a name="workload-summary"></a>Workloadoverzicht
Met Site Recovery kan elke app die wordt uitgevoerd op een ondersteunde machine, worden gerepliceerd. Bovendien wordt er samengewerkt met product teams toocarry uit aanvullende toepassingsspecifieke tests.

| **Workload** | **Hyper-V-machines tooa secundaire site repliceren** | **Hyper-V-machines tooAzure repliceren** | **Virtuele VMware-machines tooa secundaire site repliceren** | **Virtuele VMware-machines tooAzure repliceren** |
| --- | --- | --- | --- | --- |
| Active Directory, DNS |J |J |J |J |
| Web-apps (IIS, SQL) |J |J |J |J |
| System Center Operations Manager |J |J |J |J |
| SharePoint |J |J |J |J |
| SAP<br/><br/>SAP-site tooAzure voor niet-cluster repliceren |J (door Microsoft getest) |J (door Microsoft getest) |J (door Microsoft getest) |J (door Microsoft getest) |
| Exchange (niet-DAG) |J |J |J |J |
| Extern bureaublad/VDI |J |J |J |N.v.t. |
| Linux (besturingssysteem en apps) |J (door Microsoft getest) |J (door Microsoft getest) |J (door Microsoft getest) |J (door Microsoft getest) |
| Dynamics AX |J |J |J |J |
| Dynamics CRM |J |Binnenkort beschikbaar |J |Binnenkort beschikbaar |
| Oracle |J (door Microsoft getest) |J (door Microsoft getest) |J (door Microsoft getest) |J (door Microsoft getest) |
| Windows-bestandsserver |J |J |J |J |
| Citrix XenApp en XenDesktop |N.v.t. |J |N.v.t. |J |

## <a name="replicate-active-directory-and-dns"></a>Active Directory en DNS repliceren
Een Active Directory en DNS-infrastructuur zijn essentieel toomost zakelijke apps. Tijdens herstel na noodgevallen, moet u tooprotect nodig hebt en deze infrastructuuronderdelen herstellen voordat u uw workloads en apps herstelt.

U kunt Site Recovery toocreate een herstelplan volledig geautomatiseerd noodherstel gebruiken voor Active Directory en DNS. Bijvoorbeeld als u toofail via SharePoint en SAP van een primaire tooa secundaire site wilt, kunt u een herstelplan dat eerst via Active Directory niet instellen en vervolgens een extra app-specifiek herstelplan toofail via Hallo andere apps die afhankelijk zijn van de actieve De map.

[Meer informatie](site-recovery-active-directory.md) over het beveiligen van Active Directory en DNS.

## <a name="protect-sql-server"></a>SQL Server beveiligen
SQL Server biedt een Data Services-basis voor Data Services voor vele zakelijke apps in een on-premises datacenter.  Site Recovery kan worden gebruikt in combinatie met SQL Server HA-/ DR-technologieën, tooprotect meerdere lagen zakelijke apps die gebruikmaken van SQL Server. Site Recovery biedt:

* Een eenvoudige en voordelige oplossing voor herstel na noodgevallen voor SQL Server. Meerdere versies en edities van SQL Server zelfstandige servers en clusters, tooAzure of tooa secundaire site repliceren.  
* Integratie met SQL AlwaysOn-beschikbaarheidsgroepen, toomanage failovers en failbacks met Azure Site Recovery-herstelplannen.
* End-to-end herstelplannen voor Hallo alle lagen in een toepassing, met inbegrip van Hallo SQL Server-databases.
* Het schalen van SQL Server voor tijdelijk grote workloads met Site Recovery door ze door te sturen naar grotere virtuele IaaS-machines in Azure.
* Eenvoudig testen van SQL Server-noodherstel. U kunt testfailovers uitvoeren tooanalyze gegevens en nalevingscontroles, uit te voeren zonder enige impact op uw productieomgeving.

[Meer informatie](site-recovery-sql.md) over het beveiligen van SQL Server.

## <a name="protect-sharepoint"></a>SharePoint beveiligen
Met Azure Site Recovery kunnen SharePoint-implementaties als volgt worden beveiligd:

* Elimineert Hallo nodig en kosten van de bijbehorende infrastructuur voor een farm stand-by voor herstel na noodgevallen. Gebruik Site Recovery tooreplicate een volledige farm (Web, app- en databaselagen) tooAzure of tooa secundaire site.
* Site Recovery vereenvoudigt het beheer en de implementatie van toepassingen. Updates die worden geïmplementeerd toohello primaire site worden automatisch gerepliceerd en zijn dus na failover en herstel van een farm in een secundaire site beschikbaar. Ook wordt verlaagd Hallo management complexiteit en kosten in verband met een stand-by-farm up-to-date te houden.
* Site Recovery vereenvoudigt het ontwikkelen en testen van SharePoint-toepassingen, omdat er een op de productieomgeving lijkende replica-omgeving wordt gemaakt, die naar wens kan worden gebruikt voor testen en foutopsporing.
* Vereenvoudigt overgang toohello cloud met behulp van Site Recovery toomigrate SharePoint implementaties tooAzure.

[Meer informatie](site-recovery-sharepoint.md) over het beveiligen van SharePoint.

## <a name="protect-dynamics-ax"></a>Dynamics AX beveiligen
Met Azure Site Recovery kunt u op de volgende manier uw Dynamics AX ERP-oplossing beveiligen:

* Replicatie van uw volledige Dynamics AX-omgeving (Web- en AOS-lagen, databaselagen, SharePoint) organiseren tooAzure, of tooa secundaire site.
* Vereenvoudigen de migratie van Dynamics AX-implementaties toohello cloud (Azure).
* Site Recovery vereenvoudigt de ontwikkeling en het testen van Dynamics AX-toepassingen door een op de productieomgeving lijkende replica-omgeving te bieden, zodat u naar wens kunt testen en fouten kunt opsporen.

[Meer informatie](site-recovery-dynamicsax.md) over het beveiligen van Dynamic AX.

## <a name="protect-rds"></a>Extern bureaublad-services beveiligen
Extern bureaublad-Services (RDS) kunnen virtuele desktopinfrastructuur (VDI), op sessies gebaseerde bureaubladen en toepassingen, zodat gebruikers toowork overal. Met Azure Site Recovery kunt u het volgende doen:

* Beheerd of onbeheerd gegroepeerde virtuele bureaubladen tooa secundaire site, en externe toepassingen en sessies tooa secundaire site of Azure repliceren.
* Dit is wat u kunt repliceren:

| **RDS** | **Hyper-V-machines tooa secundaire site repliceren** | **Hyper-V-machines tooAzure repliceren** | **Virtuele VMware-machines tooa secundaire site repliceren** | **Virtuele VMware-machines tooAzure repliceren** | **Fysieke servers tooa secundaire site repliceren** | **TooAzure fysieke servers repliceren** |
| --- | --- | --- | --- | --- | --- | --- |
| **Gepoold virtueel bureaublad (onbeheerd)** |Ja |Nee |Ja |Nee |Ja |Nee |
| **Gepoold virtueel bureaublad (beheerd en zonder UDP)** |Ja |Nee |Ja |Nee |Ja |Nee |
| **Externe toepassingen en bureaubladsessies (zonder UDP)** |Ja |Ja |Ja |Ja |Ja |Ja |

[Meer informatie](https://gallery.technet.microsoft.com/Remote-Desktop-DR-Solution-bdf6ddcb) over het beveiligen van RDS.

## <a name="protect-exchange"></a>Exchange beveiligen
Met Site Recovery wordt Exchange als volgt beveiligd:

* Voor kleine Exchange-implementaties, zoals een enkele of zelfstandige servers, Site Recovery worden gerepliceerd en failover tooAzure of tooa secundaire site.
* Bij grotere implementaties kan Site Recovery worden geïntegreerd met Exchange DAG’s.
* Exchange dag's zijn Hallo aanbevolen oplossing voor herstel van Exchange na noodgevallen in een onderneming.  Site Recovery-herstelplannen kunnen dag, failover tussen sites tooorchestrate DAG's bevatten.

[Meer informatie](https://gallery.technet.microsoft.com/Exchange-DR-Solution-using-11a7dcb6) over het beveiligen van Exchange.

## <a name="protect-sap"></a>SAP beveiligen
Site Recovery tooprotect uw SAP-implementatie als volgt gebruiken:

* Schakel de beveiliging van toepassingen voor SAP NetWeaver en NetWeaver productie uitvoeren van de on-premises onderdelen tooAzure repliceren.
* Schakel de beveiliging van toepassingen voor SAP NetWeaver en NetWeaver productie met Azure, met het repliceren van onderdelen tooanother Azure-datacenter.
* Vereenvoudig de cloudmigratie, met behulp van Site Recovery toomigrate uw tooAzure SAP-implementatie.
* Vereenvoudig SAP-projectupgrades, tests en het maken van prototypen door een on-demand een productiekloon te maken voor het testen van SAP-toepassingen.

[Meer informatie](site-recovery-sap.md) over het beveiligen van SAP.

## <a name="protect-iis"></a>IIS beveiligen
Site Recovery tooprotect uw IIS-implementatie als volgt gebruiken:

Azure Site Recovery biedt herstel na noodgevallen door te repliceren van de belangrijkste componenten Hallo in uw omgeving tooa koude externe site of een openbare cloud, zoals Microsoft Azure. Aangezien Hallo virtuele machine met het Hallo-webserver en Hallo-database, worden gerepliceerde toohello herstelsite, is er geen vereiste toobackup-configuratiebestanden of certificaten afzonderlijk. Hallo Toepassingstoewijzingen en bindingen die afhankelijk zijn van omgevingsvariabelen die gewijzigd na failover zijn kan worden bijgewerkt via scripts die zijn geïntegreerd in Hallo na noodgevallen herstelplannen. Virtuele Machines komen op Hallo herstelsite alleen in het Hallo-gebeurtenis van een failover. Niet alleen dit Azure Site Recovery ook helpt u Hallo end tooend failover doordat u de volgende mogelijkheden Hallo indelen:

-   Hallo verschillende lagen sequentiëren Hallo afsluiten en opstarten van virtuele machines in.
-   Toevoegen van scripts tooallow bijwerken van de afhankelijkheden voor toepassingen en bindingen op Hallo virtuele machines nadat ze zijn begonnen. Hallo scripts kunnen ook worden gebruikt tooupdate Hallo DNS-server toopoint toohello herstel-site.
-   Toewijzen van IP-adressen toovirtual machines pre-failover via het toewijzen van de primaire en herstelsites netwerken Hallo en daarom scripts die toobe bijgewerkt na failover niet hoeven te gebruiken.
-   De mogelijkheid voor een failover met één Klik voor meerdere webtoepassingen op Hallo webservers, dus elimineren Hallo bereik verwarring in Hallo gebeurtenis van een noodgeval.
-   Mogelijkheid tootest Hallo herstelplannen in een geïsoleerde omgeving voor DR oefeningen.

[Meer informatie](https://aka.ms/asr-iis) over het beveiligen van IIS-webfarm.

## <a name="protect-citrix-xenapp-and-xendesktop"></a>Citrix XenApp en XenDesktop beveiligen
Site Recovery tooprotect uw implementaties Citrix XenApp en XenDesktop als volgt gebruiken:

* Inschakelen van de beveiliging van Hallo Citrix XenApp en XenDesktop-implementatie, door te repliceren van de implementatie van de verschillende lagen inclusief (AD DNS-server, SQL databaseserver server, Citrix levering Controller, winkel, XenApp Master (VDA), Citrix XenApp licentieserver) tooAzure.
* Cloudmigratie van met behulp van Site Recovery toomigrate uw implementatie Citrix XenApp en XenDesktop tooAzure vereenvoudigen.
* Vereenvoudig Citrix XenApp-/XenDesktop-tests door een op de productieomgeving lijkende replica-omgeving op aanvraag te maken voor tests en foutopsporing.
* Deze oplossing is alleen van toepassing op virtuele bureaubladen en virtuele niet-clientbureaubladen in een Windows Server-besturingssysteem. Dit komt omdat voor virtuele clientbureaubladen licentieverlening nog niet wordt ondersteund in Azure.
[Meer informatie](https://azure.microsoft.com/pricing/licensing-faq/) over licentieverlening voor clientbureaubladen en serverdesktops in Azure.

[Meer informatie](site-recovery-citrix-xenapp-and-xendesktop.md) over het beveiligen van Citrix XenApp- en XenDesktop-implementaties. U kunt ook Hallo verwijzen [technisch document van Citrix](https://aka.ms/citrix-xenapp-xendesktop-with-asr) met gedetailleerde informatie over dezelfde Hallo.

## <a name="next-steps"></a>Volgende stappen
[Vereisten controleren](site-recovery-prereq.md)
