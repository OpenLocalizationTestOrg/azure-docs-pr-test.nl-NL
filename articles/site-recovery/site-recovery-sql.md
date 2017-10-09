---
title: toepassingen met SQL Server en Azure Site Recovery aaaReplicate | Microsoft Docs
description: Dit artikel wordt beschreven hoe tooreplicate SQL Server met behulp van Azure Site Recovery voor de mogelijkheden van SQL Server-noodherstel.
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: 9126f5e8-e9ed-4c31-b6b4-bf969c12c184
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: pratshar
ms.openlocfilehash: 99755f2cd2f7e924071f1e230ac4a0bda88f0a39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="protect-sql-server-using-sql-server-disaster-recovery-and-azure-site-recovery"></a>SQL Server met behulp van SQL Server-noodherstel en Azure Site Recovery beveiligen

Dit artikel wordt beschreven hoe tooprotect Hallo SQL Server back-end van een toepassing met een combinatie van SQL Server zakelijke continuïteit en disaster recovery (BCDR)-technologieën, en [Azure Site Recovery](site-recovery-overview.md).

Voordat u begint, zorg er dan voor dat u begrijpt dat SQL Server disaster recovery mogelijkheden, zoals Failoverclustering, altijd op beschikbaarheidsgroepen databasespiegeling en back-upfunctie voor logboekbestanden.


## <a name="sql-server-deployments"></a>Implementaties van SQL Server

Veel werkbelastingen SQL Server gebruiken als basis en kunnen worden geïntegreerd met apps, zoals SharePoint, Dynamics en SAP, tooimplement dataservices.  SQL Server kan worden geïmplementeerd in een aantal verschillende manieren:

* **Zelfstandige SQL Server**: SQL Server en alle databases worden gehost op een enkele computer (fysiek of een virtuele). Wanneer u een gevirtualiseerde, worden host clustering wordt gebruikt voor lokale beschikbaarheid. Hoge beschikbaarheid gastniveau wordt niet geïmplementeerd.
* **SQL Server Failover Clustering-exemplaren (altijd op FCI)**: twee of meer knooppunten met SQL Server-exemplaar gestart met gedeelde schijven zijn geconfigureerd in een Windows-failovercluster. Als een knooppunt niet actief is, kan Hallo cluster failover SQL Server tooanother exemplaar. Dit is gewoonlijk gebruikte tooimplement hoge beschikbaarheid op een primaire site. Deze implementatie biedt geen bescherming tegen storingen of storing in Hallo gedeelde opslaglaag. Een gedeelde schijf kan worden geïmplementeerd met behulp van iSCSI, Fibre channel of gedeelde vhdx.
* **SQL AlwaysOn-beschikbaarheidsgroepen**: twee of meer knooppunten zijn ingesteld op shared nothing-cluster, met SQL Server-databases die zijn geconfigureerd in een beschikbaarheidsgroep met synchrone replicatie en automatische failover.

 In dit artikel maakt gebruik van Hallo systeemeigen SQL disaster recovery technologieën voor het herstellen van databases tooa externe site te volgen:

* SQL AlwaysOn-beschikbaarheidsgroepen tooprovide voor herstel na noodgevallen voor SQL Server 2012 of 2014 Enterprise-edities.
* SQL database mirroring in de modus hoge beveiliging voor SQL Server Standard edition (alle versies), of voor SQL Server 2008 R2.

## <a name="site-recovery-support"></a>Site Recovery-ondersteuning

### <a name="supported-scenarios"></a>Ondersteunde scenario 's
Site Recovery kan SQL Server beveiligen, zoals samengevat in de tabel Hallo.

**Scenario** | **de secundaire site tooa** | **tooAzure**
--- | --- | ---
**Hyper-V** | Ja | Ja
**VMware** | Ja | Ja
**Fysieke server** | Ja | Ja

### <a name="supported-sql-server-versions"></a>Ondersteunde versies van SQL Server
Deze SQL Server-versies worden ondersteund voor Hallo ondersteund scenario's:

* SQL Server 2016 Enterprise en Standard
* SQL Server 2014 Enterprise en Standard
* SQL Server 2012 Enterprise en Standard
* SQL Server 2008 R2 Enterprise en Standard

### <a name="supported-sql-server-integration"></a>Ondersteunde SQL Server-integratie

Site Recovery kan worden geïntegreerd met systeemeigen SQL Server BCDR-technologieën samengevat in de tabel hello, tooprovide een noodherstel.

**Functie** | **Details** | **SQL Server** |
--- | --- | ---
**AlwaysOn-beschikbaarheidsgroep** | Meerdere exemplaren van de zelfstandige versie van SQL Server worden uitgevoerd in een failovercluster met meerdere knooppunten.<br/><br/>Databases kunnen worden gegroepeerd in failover-groepen die kunnen worden gekopieerd (gespiegeld) voor SQL Server-exemplaren zodat er is geen gedeelde opslag nodig is.<br/><br/>Biedt herstel na noodgevallen tussen een primaire site en een of meer secundaire sites. Twee knooppunten kunnen worden ingesteld in een gedeelde niets cluster met SQL Server-databases die zijn geconfigureerd in een beschikbaarheidsgroep met synchrone replicatie en automatische failover. | SQL Server 2014 & 2012 Enterprise edition
**Failover clustering (altijd op FCI)** | SQL Server maakt gebruik van Windows failover clustering voor hoge beschikbaarheid van de lokale SQL Server-werkbelastingen.<br/><br/>Knooppunten met exemplaren van SQL Server met gedeelde schijven zijn geconfigureerd in een failovercluster. Als u een exemplaar is niet actief failover cluster Hallo toodifferent een.<br/><br/>Hallo-cluster biedt geen bescherming tegen storingen of storingen in gedeelde opslag. Hallo gedeelde schijf kan worden geïmplementeerd met iSCSI, Fibre channel, of gedeelde vhdx-bestanden. | SQL Server Enterprise-edities<br/><br/>SQL Server Standard edition (alleen beperkt tootwo knooppunten)
**Databasespiegeling (modus hoge beveiliging)** | Een individuele database tooa één secundaire kopie beveiligt. Beschikbaar in beide hoge beveiliging (synchrone) en hoge prestaties (asynchrone) replicatie modi. Geen vereist een failover-cluster. | SQL Server 2008 R2<br/><br/>SQL Server Enterprise alle edities
**Zelfstandige SQL Server** | Hallo SQL Server en database gehost op één server (fysiek of virtueel). Host clustering wordt gebruikt voor hoge beschikbaarheid als Hallo server virtueel is. Er is geen gastniveau met hoge beschikbaarheid. | Enterprise of Standard edition

## <a name="deployment-recommendations"></a>Aanbevelingen voor de implementatie

Deze tabel bevat een overzicht van onze aanbevelingen voor het SQL Server BCDR-technologieën te integreren met Site Recovery.

| **Versie** | **Editie** | **Implementatie** | **On-premises tooon-premises** | **On-premises tooAzure** |
| --- | --- | --- | --- | --- |
| SQL Server 2014 of 2012 |Enterprise |Failover clusterexemplaar |Altijd op beschikbaarheidsgroepen |Altijd op beschikbaarheidsgroepen |
|| Enterprise |AlwaysOn-beschikbaarheidsgroepen voor hoge beschikbaarheid |Altijd op beschikbaarheidsgroepen |Altijd op beschikbaarheidsgroepen | |
|| Standard |Failover cluster instance (FCI) |Replicatie van site Recovery met lokale mirror |Replicatie van site Recovery met lokale mirror | |
|| Enterprise of Standard |Zelfstandig |Replicatie van site Recovery |Replicatie van site Recovery | |
| SQL Server 2008 R2 of 2008 |Enterprise of Standard |Failover cluster instance (FCI) |Replicatie van site Recovery met lokale mirror |Replicatie van site Recovery met lokale mirror |
|| Enterprise of Standard |Zelfstandig |Replicatie van site Recovery |Replicatie van site Recovery | |
| SQL Server (alle versies) |Enterprise of Standard |Failover cluster instance - DTC-toepassing |Replicatie van site Recovery |Niet ondersteund |

## <a name="deployment-prerequisites"></a>Vereisten voor implementatie

* Een lokale SQL Server-implementatie, met een ondersteunde versie van SQL Server. Normaal gesproken moet u ook Active Directory voor uw SQL-server.
* Hallo-vereisten voor het scenario dat u wilt toodeploy Hallo. Meer informatie over de ondersteuningsvereisten voor voor [replicatie tooAzure](site-recovery-support-matrix-to-azure.md) en [lokale](site-recovery-support-matrix.md), en [implementatievereisten](site-recovery-prereq.md).
* tooset een herstel in Azure, Voer Hallo [Azure virtuele Machine Readiness Assessment](http://www.microsoft.com/download/details.aspx?id=40898) hulpprogramma op uw virtuele machines van het SQL Server toomake dat ze compatibel zijn met de Azure Site Recovery bent.

## <a name="set-up-active-directory"></a>Active Directory instellen

Active Directory op Hallo herstel van secundaire site voor SQL Server-toorun correct ingesteld.

* **Kleine onderneming**— met een klein aantal toepassingen en één domeincontroller voor Hallo on-premises-site, als u wilt dat toofail gedurende de hele site hello, raden wij aan u Site Recovery replicatie tooreplicate Hallo-domeincontroller gebruiken secundair datacenter toohello of tooAzure.
* **Gemiddeld toolarge enterprise**— als u een groot aantal toepassingen, een Active Directory-forest hebt en u toofail toepassing of een werkbelasting wilt, raden wij aan instellen van een extra domeincontroller in Hallo secundair datacenter of in Azure. Als u altijd op beschikbaarheid groepen toorecover tooa externe site gebruikt, raden wij dat u een andere extra domeincontroller op de secundaire site Hallo of in Azure, toouse voor SQL Server-exemplaar Hallo hersteld instellen.

Hallo-instructies in dit artikel wordt ervan uitgegaan dat een domeincontroller beschikbaar op de secundaire locatie Hallo is. [Lees meer](site-recovery-active-directory.md) over het beveiligen van Active Directory met Site Recovery.


## <a name="integrate-with-sql-server-always-on-for-replication-tooazure"></a>Integreren met SQL Server Always On replicatie tooAzure

Dit is wat u moet toodo:

1. Importeer de scripts in uw Azure Automation-account. Dit document bevat Hallo scripts toofailover SQL-beschikbaarheidsgroep in een [Resource Manager virtuele machine](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/asr-automation-recovery/scripts/ASR-SQL-FailoverAG.ps1) en een [klassieke virtuele machine](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/asr-automation-recovery/scripts/ASR-SQL-FailoverAGClassic.ps1).

    [![TooAzure implementeren](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)


1. ASR-SQL-FailoverAG als een pre-actie van eerste groep Hallo Hallo herstelplan toevoegen.

1. Volg instructies beschikbaar in Hallo script toocreate het Hallo-naam van een automation-variabele tooprovide Hallo Hallo availability groups.

### <a name="steps-toodo-a-test-failover"></a>Stappen toodo een testfailover

Systeemeigen SQL Always On biedt geen ondersteuning voor de testfailover. Daarom raden we aan Hallo volgende:

1. Instellen van [Azure Backup](../backup/backup-azure-vms.md) op Hallo virtuele machine die als host fungeert voor Hallo beschikbaarheidsgroepreplica's in Azure.

1. Voordat de activering van de testfailover van het herstelplan Hallo Hallo virtuele machine van Hallo back-up is gemaakt in de vorige stap hello te herstellen.

    ![Azure back-up terugzetten ](./media/site-recovery-sql/restore-from-backup.png)

1. [Een quorum forceren](https://docs.microsoft.com/sql/sql-server/failover-clusters/windows/force-a-wsfc-cluster-to-start-without-a-quorum#PowerShellProcedure) in Hallo virtuele machine is hersteld op basis van de back-up.

1. IP van Hallo listener tooan IP-adres beschikbaar in het testfailovernetwerk Hallo bijwerken.

    ![Bijwerken van de Listener IP](./media/site-recovery-sql/update-listener-ip.png)

1. Listener online brengen.

    ![Listener Online brengen](./media/site-recovery-sql/bring-listener-online.png)

1. Maak een load balancer met één IP-adres die zijn gemaakt onder frontend IP-adresgroep bijbehorende tooeach beschikbaarheidsgroep-listener en met Hallo SQL virtuele machine in de back-endpool Hallo toegevoegd.

     ![Load Balancer - Frontend IP-adresgroep maken ](./media/site-recovery-sql/create-load-balancer1.png)

    ![Load Balancer - back-endpool maken ](./media/site-recovery-sql/create-load-balancer2.png)

1. Een testfailover van het herstelplan Hallo doen.

### <a name="steps-toodo-a-failover"></a>Stappen toodo een failover

Nadat u hebt Hallo script toegevoegd in het herstelplan Hallo en gevalideerde Hallo herstelplan als volgt een failovertest uitvoert, kunt u de failover van herstelplan Hallo kunt doen.


## <a name="integrate-with-sql-server-always-on-for-replication-tooa-secondary-on-premises-site"></a>Integratie met SQL Server Always On voor replicatie tooa secundaire on-premises site

Als Hallo SQL Server-beschikbaarheidsgroepen gebruikt voor hoge beschikbaarheid (of een FCI), wordt u aangeraden beschikbaarheidsgroepen op Hallo herstelsite ook. Houd er rekening mee dat dit van toepassing is tooapps die geen van gedistribueerde transacties gebruikmaken.

1. [Databases configureren](https://msdn.microsoft.com/library/hh213078.aspx) in beschikbaarheidsgroepen.
1. Maak een virtueel netwerk op Hallo secundaire site.
1. Een site-naar-site VPN-verbinding tussen Hallo virtueel netwerk en de primaire site Hallo instellen.
1. Maak een virtuele machine op de herstelsite hello en SQL Server installeren op deze.
1. Hallo bestaande Always On availability groepen toohello uitbreiden nieuwe virtuele machine voor SQL Server. Dit exemplaar van SQL Server configureren als een kopie van de asynchrone replica.
1. Een beschikbaarheidsgroep-listener te maken of bijwerken van Hallo bestaande listener tooinclude Hallo asynchrone replica virtuele machine.
1. Zorg ervoor dat die toepassing hello farm met behulp van Hallo-listener is ingesteld. Als deze ingesteld met behulp van de naam van de databaseserver hello is, bijwerken toouse Hallo listener, dus u tooreconfigure hoeft deze na een failover Hallo.

Voor toepassingen die gebruikmaken van gedistribueerde transacties, raden wij aan u Site Recovery met implementeert [VMware of fysieke server site-naar-site-replicatie](site-recovery-vmware-to-vmware.md).

### <a name="recovery-plan-considerations"></a>Overwegingen voor het plannen van herstel
1. In dit voorbeeld script toohello VMM-bibliotheek op Hallo primaire en secundaire sites toevoegen.

        Param(
        [string]$SQLAvailabilityGroupPath
        )
        import-module sqlps
        Switch-SqlAvailabilityGroup -Path $SQLAvailabilityGroupPath -AllowDataLoss -force

1. Wanneer u een herstelplan voor Hallo-toepassing maakt, een vooraf actie tooGroup 1 systeemscript stap toevoegen, die wordt aangeroepen Hallo script toofail via beschikbaarheidsgroepen.

## <a name="protect-a-standalone-sql-server"></a>Een zelfstandige SQL-Server beveiligen

In dit scenario is het raadzaam dat u Site Recovery replicatie tooprotect Hallo SQL Server-computer. de exacte stappen Hallo is afhankelijk van of SQL Server is een virtuele machine of een fysieke server, en of u wilt dat tooreplicate tooAzure of een secundaire on-premises site. Meer informatie over [Site herstelscenario's](site-recovery-overview.md).

## <a name="protect-a-sql-server-cluster-standard-editionwindows-server-2008-r2"></a>Beveiligen van een SQL Server-cluster (standard edition/Windows Server 2008 R2)

Voor een cluster met SQL Server Standard edition of SQL Server 2008 R2, wordt u aangeraden dat u Site Recovery replicatie tooprotect SQL Server gebruiken.

### <a name="on-premises-tooon-premises"></a>Lokale tooon-premises

* Als het Hallo-app maakt gebruik van gedistribueerde transacties is het raadzaam u implementeert [Site Recovery met SAN-replicatie](site-recovery-vmm-san.md) voor een Hyper-V-omgeving of [VMware of fysieke server tooVMware](site-recovery-vmware-to-vmware.md) voor een VMware-omgeving.
* Gebruik voor niet-DTC-toepassingen, Hallo hierboven benadering toorecover Hallo cluster als een zelfstandige server, dankzij het gebruik van een lokale hoge beveiliging DB mirror.

### <a name="on-premises-tooazure"></a>Lokale tooAzure

Site Recovery biedt niet de Gast clusterondersteuning bij het repliceren van tooAzure. SQL Server bieden niet ook een goedkope noodherstel voor Standard-editie. In dit scenario wordt aangeraden de Hallo lokale SQL Server-cluster tooa zelfstandige SQL Server beveiligen en herstellen in Azure.

1. Configureer een extra zelfstandige SQL Server-exemplaar op Hallo on-premises-site.
1. Hallo exemplaar tooserve configureren als mirror voor Hallo-databases wilt tooprotect. Configureer in de modus hoge beveiliging spiegelen.
1. Site Recovery op Hallo lokale site configureren voor ([Hyper-V](site-recovery-hyper-v-site-to-azure.md) of [VMware-virtuele machines/fysieke servers)](site-recovery-vmware-to-azure-classic.md).
1. Site Recovery replicatie tooreplicate Hallo nieuwe SQL Server-exemplaar tooAzure gebruiken. Omdat het een hoge beveiliging mirror-kopie, deze worden vervolgens gesynchroniseerd met de primaire cluster hello, maar moeten gerepliceerde tooAzure met behulp van replicatie van Site Recovery.


![Standard-cluster](./media/site-recovery-sql/standalone-cluster-local.png)

### <a name="failback-considerations"></a>Overwegingen voor failback

Failback na een niet-geplande failover is voor SQL Server Standard clusters vereist een SQL server-back-up en herstel uit Hallo mirror exemplaar toohello oorspronkelijke cluster met reestablishment van Hallo mirror.

## <a name="next-steps"></a>Volgende stappen
[Meer informatie](site-recovery-components.md) over de architectuur van Site Recovery.
