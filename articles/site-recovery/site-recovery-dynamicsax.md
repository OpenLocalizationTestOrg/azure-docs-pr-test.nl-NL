---
title: een meerlaagse Dynamics AX-implementatie met behulp van Azure Site Recovery aaaReplicate | Microsoft Docs
description: Dit artikel wordt beschreven hoe tooreplicate en Dynamics AX met Azure Site Recovery beveiligen
services: site-recovery
documentationcenter: 
author: asgang
manager: rochakm
editor: 
ms.assetid: 9126f5e8-e9ed-4c31-b6b4-bf969c12c184
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/24/2017
ms.author: asgang
ms.openlocfilehash: b974315ec50ab2ec43846b3d3f95c7de88b72fc3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-a-multi-tier-dynamics-ax-application-using-azure-site-recovery"></a>Een toepassing met meerdere lagen Dynamics AX met Azure Site Recovery repliceren

## <a name="overview"></a>Overzicht


Microsoft Dynamics AX is een van de meest populaire ERP-oplossing Hallo tussen ondernemingen toostandardized proces verschillende locaties, beheren van resources en de naleving te vereenvoudigen. Considering toepassing hello kritieke tooan bedrijfsorganisatie is is erg belangrijk toobe ervoor dat als elke ramp toepassing actief en werkend in de minimale tijd moet.

Vandaag de dag biedt Microsoft Dynamics AX geen een out-of-the-box-noodherstel herstelfuncties. Microsoft Dynamics AX bestaat uit veel serveronderdelen, zoals AOS-Server, Active Directory (AD), SQL Database-Server, SharePoint Server, Reporting Server enzovoort toomanage Hallo herstel na noodgevallen van elk van deze onderdelen handmatig is niet alleen dure maar ook gevoelig voor fouten.

Dit artikel wordt uitgelegd in detail over hoe u een noodherstel voor uw Dynamics AX-toepassing met maken kunt [Azure Site Recovery](site-recovery-overview.md). Het omvat tevens geplande en ongeplande/testen failovers met één klik herstelplan, ondersteunde configuraties en vereisten.
Azure Site Recovery op basis van noodherstel is volledig getest, gecertificeerd en aanbevolen door Microsoft Dynamics AX.



## <a name="prerequisites"></a>Vereisten

Hallo vereisten voltooid na implementatie van herstel na noodgevallen voor Dynamics AX-toepassing met Azure Site Recovery worden vereist.

• Een on-premises Dynamics AX-implementatie is ingesteld

• Azure Site Recovery Services-kluis is gemaakt in Microsoft Azure-abonnement

• Als uw site recovery is Azure hello Azure virtuele Machine Readiness Assessment hulpprogramma uitvoeren op virtuele machines tooensure dat ze compatibel zijn met de Azure VM's en Azure Site Recovery Services


## <a name="site-recovery-support"></a>Site Recovery-ondersteuning

Voor Hallo doel van het maken van dit artikel, werden virtuele VMware-machines met Dynamics AX 2012R3 op Windows Server 2012 R2 Enterprise gebruikt. Als de replicatie van site recovery networkdirect van toepassing is, voorziet in Hallo aanbevelingen zijn hier verwachte toohold op de volgende scenario's ook.

### <a name="source-and-target"></a>Bron en doel

**Scenario** | **de secundaire site tooa** | **tooAzure**
--- | --- | ---
**Hyper-V** | Ja | Ja
**VMware** | Ja | Ja
**Fysieke server** | Ja | Ja

## <a name="enable-dr-of-dynamics-ax-application-using-azure-site-recovery"></a>DR van Dynamics AX-toepassing met Azure Site Recovery inschakelen
### <a name="protect-your-dynamics-ax-application"></a>Uw toepassing Dynamics AX beveiligen
Elk onderdeel van Hallo Dynamics AX behoeften toobe beveiligd tooenable Hallo volledige toepassing replicatie en herstel. Deze sectie worden behandeld:

**1. Bescherming van Active Directory**

**2. Beveiliging van SQL-laag**

**3. Beveiliging van de App en Web lagen**

**4. Netwerkconfiguratie**

**5. Plan voor herstel**

### <a name="1-setup-ad-and-dns-replication"></a>1. Setup AD- en DNS-replicatie

Active Directory is vereist op Hallo DR-site voor toofunction van Dynamics AX-toepassing. Er zijn twee aanbevolen keuzes op basis van de complexiteit Hallo van van de klant Hallo on-premises omgeving.

**Optie 1**

Als klant Hallo heeft een klein aantal toepassingen en één domeincontroller voor de gehele on-premises site en wordt samen gedurende de gehele site Hallo mislukken wordt aangeraden ASR-replicatie tooreplicate Hallo DC machine toosecondary site ( van toepassing voor zowel tooSite Site als Site tooAzure).

**Optie 2**

Als klant Hallo heeft een groot aantal toepassingen en een Active Directory-forest wordt uitgevoerd en wordt failover-paar toepassingen op een tijdstip, wordt aangeraden een extra domeincontroller op Hallo DR-site instellen (secundaire site of in Azure).

Raadpleeg het te[aanvullende handleiding op het beschikbaar maken van een domeincontroller op DR-site](site-recovery-active-directory.md). Voor de rest van dit document wordt ervan uitgegaan dat een domeincontroller beschikbaar is op DR-site.

### <a name="2-setup-sql-server-replication"></a>2. Setup van SQL Server-replicatie
Raadpleeg de handleiding toocompanion voor gedetailleerde technische richtlijnen voor aanbevolen optie voor het beveiligen van Hallo [SQL laag](site-recovery-sql.md).

### <a name="3-enable-protection-for-dynamics-ax-client-and-aos-vms"></a>3. Schakel de beveiliging voor de Dynamics AX-client- en AOS-virtuele machines
Voer een relevante Azure Site Recovery-configuratie op basis van of Hallo virtuele machines zijn geïmplementeerd op [Hyper-V](site-recovery-hyper-v-site-to-azure.md) of op [VMware](site-recovery-vmware-to-azure.md).

> [!TIP]
> Aanbevolen Crash consistent frequentie tooconfigure is 15 minuten.
>

Hallo onder momentopname bevat Hallo beveiligingsstatus van Dynamics onderdeel VM's in 'VMware site tooAzure' beveiligingsscenario.
![Beveiligde items](./media/site-recovery-dynamics-ax/protecteditems.png)

### <a name="4-configure-networking"></a>4. Netwerken configureren
Configureer VM berekenen en -instellingen

Voor Hallo AX-client- en AOS-VMs netwerkinstellingen configureren in Azure Site Recovery zodat Hallo VM-netwerken beschikken over gekoppelde toohello rechts DR netwerk na een failover. Zorg ervoor dat Hallo DR-netwerk voor deze lagen routeerbaar toohello SQL laag is.

U kunt selecteren Hallo VM in Hallo gerepliceerd items tooconfigure Hallo netwerkinstellingen, zoals weergegeven in de onderstaande Hallo-momentopname.

* Voor de juiste beschikbaarheidsset Hallo AOS-servers selecteren

* Als u met behulp van een statische IP-adres opgeven Hallo IP die u wilt dat virtuele machine tootake in Hallo Hallo **IP-adres doel** veld ![netwerkinstellingen](./media/site-recovery-dynamics-ax/vmpropertiesaos1.png)



### <a name="5-creating-a-recovery-plan"></a>5. Een herstelplan maken

U kunt een herstelplan maken in Azure Site Recovery tooautomate Hallo failover-proces. App-laag en weblaag in Hallo herstelplan toevoegen. Bestellen in verschillende groepen zodat die Hallo front-afsluiten voordat de app-laag.

1)  Selecteer hello Azure Site Recovery-kluis in uw abonnement en klik op de tegel 'Herstelplannen'.

2)  Klik op ' + herstel plannen en geef een naam op.

3)  Selecteer Hallo 'Source' en 'Target'. Hallo doel mag Azure of een secundaire site. Als u Azure kiest, moet u Hallo-implementatiemodel

![Herstelplan maken](./media/site-recovery-dynamics-ax/recoveryplancreation1.png)

4)  Hallo AOS en client VMs toohello herstelplan selecteren en klik op ✓.
![Herstelplan maken](./media/site-recovery-dynamics-ax/selectvms.png)


![Plan voor herstel](./media/site-recovery-dynamics-ax/recoveryplan.png)

U kunt plannen voor Dynamics AX-toepassing hello herstel aanpassen door verschillende stappen toe te voegen zoals hieronder wordt beschreven. Hallo hierboven momentopname toont Hallo voltooid herstelplan na het toevoegen van alle Hallo stappen.

*Stappen:*

*1. SQL Server failover stappen*

Raadpleeg te[DR van SQL Server-oplossing](site-recovery-sql.md) aanvullende handleiding voor meer informatie over specifieke tooSQL van de herstelserver stappen.

*2. Failover-groep 1: Een failover Hallo AOS-virtuele machines*

Zorg ervoor dat Hallo herstelpunt geselecteerd zo dicht mogelijk toohello database PIT maar niet verder gaan is.

*3. Script: Toevoegen load balancer (alleen E-A)* voegt een script toe (via Azure automation) na AOS VM groep tooadd een load balancer tooit voordoet. U kunt een script toodo Gebruik deze taak. Raadpleeg artikel [hoe tooadd load balancer voor DR-toepassing met meerdere lagen](https://azure.microsoft.com/blog/cloud-migration-and-disaster-recovery-of-load-balanced-multi-tier-applications-using-azure-site-recovery/)

*4. Failover-groep 2: Een failover Hallo AX-client virtuele machines.*
Hallo weblaag virtuele machines als onderdeel van het herstelplan Hallo een failover.


### <a name="doing-a-test-failover"></a>Een testfailover uitvoeren

Raadpleeg too'AD DR Solution ' en de aanvullende handleidingen DR van SQL Server-oplossing voor specifieke tooAD overwegingen en SQL server respectievelijk tijdens de Testfailover.

1.  Ga tooAzure portal en selecteer de Site Recovery-kluis.
2.  Klik op Hallo herstelplan is gemaakt voor Dynamics AX.
3.  Klik op 'Testfailover'.
4.  Selecteer Hallo virtueel netwerk toostart Hallo test failover-proces.
5.  Wanneer secundaire Hallo-omgeving is, kunt u uw validaties kunt uitvoeren.
6.  Zodra Hallo validaties voltooid zijn, kunt u 'Validaties voltooid' en de testfailoveromgeving hello wordt gereinigd.

Ga als volgt [in deze richtlijnen](site-recovery-test-failover-to-azure.md) toodo een testfailover.

### <a name="doing-a-failover"></a>U een failover uitvoert

1.  Ga tooAzure portal en selecteer de Site Recovery-kluis.
2.  Klik op Hallo herstelplan is gemaakt voor Dynamics AX.
3.  Klik op 'Failover' en 'Failover' selecteren.
4.  Hallo-doelnetwerk selecteren en op ✓ toostart Hallo failover-proces.

Ga als volgt [in deze richtlijnen](site-recovery-failover.md) bij het uitvoeren van een failover.

### <a name="perform-a-failback"></a>Een Failback uitvoeren

Raadpleeg too'SQL Server DR-oplossing is aanvullende handleiding voor overwegingen met betrekking tot specifieke tooSQL server tijdens de Failback.

1.  Ga tooAzure portal en selecteer de Site Recovery-kluis.
2.  Klik op Hallo herstelplan is gemaakt voor Dynamics AX.
3.  Klik op 'Failover' en selecteer failover.
4.  Klik op 'Wijziging richting'.
5.  Hallo juiste opties selecteren - synchronisatie van gegevens en opties voor het maken van VM
6.  Klik op ✓ toostart Hallo 'Failback' proces.


Ga als volgt [in deze richtlijnen](site-recovery-failback-azure-to-vmware.md) bij het uitvoeren van een failback.

##<a name="summary"></a>Samenvatting
Met Azure Site Recovery kunt u een herstelplan volledig geautomatiseerd noodherstel voor uw Dynamics AX-toepassing maken. U kunt het Hallo failover initiëren binnen enkele seconden vanaf elke locatie in Hallo-gebeurtenis van een onderbreking van de en krijgt u de toepassing hello up-to-date en worden uitgevoerd in minuten.

## <a name="next-steps"></a>Volgende stappen
Lees [welke workloads kan ik beveiligen?](site-recovery-workload.md) toolearn meer over het beveiligen van enterprise-werkbelastingen met Azure Site Recovery.
