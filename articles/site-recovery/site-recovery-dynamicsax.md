---
title: Een meerlaagse Dynamics AX-implementatie met behulp van Azure Site Recovery repliceren | Microsoft Docs
description: Dit artikel wordt beschreven hoe repliceren en Dynamics AX met Azure Site Recovery beveiligen
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
ms.openlocfilehash: 03127c8f4841b67436c4819628319705af0b2cd5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="replicate-a-multi-tier-dynamics-ax-application-using-azure-site-recovery"></a>Een toepassing met meerdere lagen Dynamics AX met Azure Site Recovery repliceren

## <a name="overview"></a>Overzicht


Microsoft Dynamics AX is een van de meest populaire ERP-oplossing tussen ondernemingen gestandaardiseerde proces verschillende locaties, beheren van resources en de naleving te vereenvoudigen. Considering de toepassing essentieel voor een organisatie bedrijf is is het belangrijk dat u moet u ervoor zorgen dat als elke ramp toepassing kan worden uitgevoerd en in de minimale tijd.

Vandaag de dag biedt Microsoft Dynamics AX geen een out-of-the-box-noodherstel herstelfuncties. Microsoft Dynamics AX bestaat uit veel serveronderdelen, zoals AOS-Server, Active Directory (AD), SQL Database-Server, SharePoint Server, Reporting Server, enzovoort. Voor het beheren van de sitedatabase is herstellen van elk van deze onderdelen handmatig niet alleen dure, maar ook gevoelig voor fouten.

Dit artikel wordt uitgelegd in detail over hoe u een noodherstel voor uw Dynamics AX-toepassing met maken kunt [Azure Site Recovery](site-recovery-overview.md). Het omvat tevens geplande en ongeplande/testen failovers met één klik herstelplan, ondersteunde configuraties en vereisten.
Azure Site Recovery op basis van noodherstel is volledig getest, gecertificeerd en aanbevolen door Microsoft Dynamics AX.



## <a name="prerequisites"></a>Vereisten

Herstel na noodgevallen voor Dynamics AX-toepassing met Azure Site Recovery implementeert, moet de volgende vereisten is voltooid.

• Een on-premises Dynamics AX-implementatie is ingesteld

• Azure Site Recovery Services-kluis is gemaakt in Microsoft Azure-abonnement

• Als Azure uw site recovery de Azure virtuele Machine Readiness Assessment hulpprogramma uitvoeren op virtuele machines om ervoor te zorgen dat ze compatibel met Azure VM's en Azure Site Recovery-Services zijn


## <a name="site-recovery-support"></a>Site Recovery-ondersteuning

In dit artikel maakt, omwille van de werden virtuele VMware-machines met Dynamics AX 2012R3 op Windows Server 2012 R2 Enterprise gebruikt. Als replicatie van site recovery networkdirect van toepassing is, worden de aanbevelingen die in de volgende scenario's evenals verwacht.

### <a name="source-and-target"></a>Bron en doel

**Scenario** | **Een secundaire site** | **Naar Azure**
--- | --- | ---
**Hyper-V** | Ja | Ja
**VMware** | Ja | Ja
**Fysieke server** | Ja | Ja

## <a name="enable-dr-of-dynamics-ax-application-using-azure-site-recovery"></a>DR van Dynamics AX-toepassing met Azure Site Recovery inschakelen
### <a name="protect-your-dynamics-ax-application"></a>Uw toepassing Dynamics AX beveiligen
Elk onderdeel van de Dynamics AX moet worden beveiligd, zodat de replicatie van de volledige toepassing en het herstel. Deze sectie worden behandeld:

**1. Bescherming van Active Directory**

**2. Beveiliging van SQL-laag**

**3. Beveiliging van de App en Web lagen**

**4. Netwerkconfiguratie**

**5. Plan voor herstel**

### <a name="1-setup-ad-and-dns-replication"></a>1. Setup AD- en DNS-replicatie

Active Directory is vereist op de site DR voor Dynamics AX-toepassing naar de functie. Er zijn twee aanbevolen keuzes op basis van de complexiteit van de klant on-premises omgeving.

**Optie 1**

Als de klant heeft een klein aantal toepassingen en één domeincontroller voor de gehele on-premises site en zal worden failover van de hele site samen, en vervolgens wordt u ASR-replicatie aangeraden naar de DC-machine repliceren naar secundaire site (van toepassing op zowel Site naar Site als Site naar Azure).

**Optie 2**

Als de klant heeft een groot aantal toepassingen en een Active Directory-forest wordt uitgevoerd en wordt failover-paar toepassingen op een tijdstip, wordt aangeraden een extra domeincontroller op de DR-site instellen (secundaire site of in Azure).

Raadpleeg [aanvullende handleiding op het beschikbaar maken van een domeincontroller op DR-site](site-recovery-active-directory.md). Voor de rest van dit document wordt ervan uitgegaan dat een domeincontroller beschikbaar is op DR-site.

### <a name="2-setup-sql-server-replication"></a>2. Setup van SQL Server-replicatie
Raadpleeg de handleiding voor gedetailleerde richtlijnen voor technische op de aanbevolen optie voor het beveiligen van [SQL laag](site-recovery-sql.md).

### <a name="3-enable-protection-for-dynamics-ax-client-and-aos-vms"></a>3. Schakel de beveiliging voor de Dynamics AX-client- en AOS-virtuele machines
Voer een relevante Azure Site Recovery-configuratie op basis van het feit of de virtuele machines op zijn geïmplementeerd [Hyper-V](site-recovery-hyper-v-site-to-azure.md) of op [VMware](site-recovery-vmware-to-azure.md).

> [!TIP]
> Is 15 minuten Crash consistent frequentie aanbevolen als u wilt configureren.
>

De hieronder momentopname toont u de beveiligingsstatus van Dynamics onderdeel VM's in beveiligingsscenario VMware-site naar Azure.
![Beveiligde items](./media/site-recovery-dynamics-ax/protecteditems.png)

### <a name="4-configure-networking"></a>4. Netwerken configureren
Configureer VM berekenen en -instellingen

Voor de AX-client en de virtuele machines AOS-netwerkinstellingen configureren in Azure Site Recovery zodat de VM-netwerken ophalen gekoppeld aan het juiste DR-netwerk na een failover. Zorg ervoor dat het netwerk DR voor deze lagen routeerbaar zijn naar de SQL-laag.

U kunt de virtuele machine selecteren in de gerepliceerde items voor het configureren van de netwerkinstellingen, zoals wordt weergegeven in de onderstaande momentopname.

* Selecteer de juiste beschikbaarheid voor AOS-servers.

* Als u met behulp van een statische IP-adres en geeft u het IP-adres dat u wilt dat de virtuele machine moet worden uitgevoerd de **IP-adres doel** veld ![netwerkinstellingen](./media/site-recovery-dynamics-ax/vmpropertiesaos1.png)



### <a name="5-creating-a-recovery-plan"></a>5. Een herstelplan maken

U kunt een herstelplan maken in Azure Site Recovery voor de failover te automatiseren. App-laag en weblaag toevoegen in het herstelplan. In verschillende groepen zo gerangschikt dat het front-afsluiten voordat de app-laag.

1)  Selecteer de Azure Site Recovery-kluis in uw abonnement en klik op de tegel 'Herstelplannen'.

2)  Klik op ' + herstel plannen en geef een naam op.

3)  Selecteer de 'Source' en 'Target'. Het doel mag Azure of een secundaire site. Als u Azure kiest, moet u het implementatiemodel

![Herstelplan maken](./media/site-recovery-dynamics-ax/recoveryplancreation1.png)

4)  Selecteer de AOS en de client virtuele machines aan het herstelplan en klik ✓.
![Herstelplan maken](./media/site-recovery-dynamics-ax/selectvms.png)


![Plan voor herstel](./media/site-recovery-dynamics-ax/recoveryplan.png)

U kunt het herstelplan voor Dynamics AX-toepassing aanpassen door verschillende stappen toe te voegen zoals hieronder wordt beschreven. De momentopname van de bovenstaande ziet u het volledige herstelplan na het toevoegen van alle stappen.

*Stappen:*

*1. SQL Server failover stappen*

Raadpleeg [DR van SQL Server-oplossing](site-recovery-sql.md) aanvullende handleiding voor meer informatie over specifieke herstelstappen voor het SQL server.

*2. Failover-groep 1: Een failover de AOS-virtuele machines*

Zorg ervoor dat het geselecteerde herstelpunt zo dicht mogelijk bij de database PIT maar niet verder gaan is.

*3. Script: Toevoegen load balancer (alleen E-A)* toevoegen aan een load balancer toevoegen wordt een script (via Azure automation) na AOS VM-groep. Een script kunt u deze taak. Raadpleeg artikel [load balancer voor de toepassing met meerdere lagen DR toevoegen](https://azure.microsoft.com/blog/cloud-migration-and-disaster-recovery-of-load-balanced-multi-tier-applications-using-azure-site-recovery/)

*4. Failover-groep 2: Een failover de virtuele machines van de AX-client.*
Failover van de weblaag virtuele machines als onderdeel van het herstelplan.


### <a name="doing-a-test-failover"></a>Een testfailover uitvoeren

Raadpleeg de AD-DR-oplossing en de SQL Server-DR-oplossing aanvullende handleidingen voor specifieke aandachtspunten met AD en SQL server respectievelijk tijdens de Testfailover.

1.  Ga naar de Azure-portal en selecteer de Site Recovery-kluis.
2.  Klik op het herstelplan gemaakt voor Dynamics AX.
3.  Klik op 'Testfailover'.
4.  Selecteer het virtuele netwerk om de test failover-proces te starten.
5.  Als de secundaire-omgeving is, kunt u uw validaties kunt uitvoeren.
6.  Zodra de validaties voltooid zijn, kunt u 'Validaties voltooid' en de testfailoveromgeving wordt gereinigd.

Ga als volgt [in deze richtlijnen](site-recovery-test-failover-to-azure.md) een testfailover uitvoeren.

### <a name="doing-a-failover"></a>U een failover uitvoert

1.  Ga naar de Azure-portal en selecteer de Site Recovery-kluis.
2.  Klik op het herstelplan gemaakt voor Dynamics AX.
3.  Klik op 'Failover' en 'Failover' selecteren.
4.  Selecteer het doelnetwerk en klik op ✓ om de failoverproces te starten.

Ga als volgt [in deze richtlijnen](site-recovery-failover.md) bij het uitvoeren van een failover.

### <a name="perform-a-failback"></a>Een Failback uitvoeren

Raadpleeg de SQL Server-DR-oplossing aanvullende handleiding voor overwegingen met betrekking tot specifieke met SQL server tijdens de Failback.

1.  Ga naar de Azure-portal en selecteer de Site Recovery-kluis.
2.  Klik op het herstelplan gemaakt voor Dynamics AX.
3.  Klik op 'Failover' en selecteer failover.
4.  Klik op 'Wijziging richting'.
5.  Selecteer de gewenste opties - synchronisatie van gegevens en opties voor het maken van VM
6.  Klik op ✓ om het te starten 'Failback'.


Ga als volgt [in deze richtlijnen](site-recovery-failback-azure-to-vmware.md) bij het uitvoeren van een failback.

##<a name="summary"></a>Samenvatting
Met Azure Site Recovery kunt u een herstelplan volledig geautomatiseerd noodherstel voor uw Dynamics AX-toepassing maken. U kunt de failover start binnen enkele seconden vanaf elke locatie in het geval van een onderbreking en ophalen van de toepassing binnen de minuten.

## <a name="next-steps"></a>Volgende stappen
Lees [welke workloads kan ik beveiligen?](site-recovery-workload.md) voor meer informatie over het beveiligen van enterprise-werkbelastingen met Azure Site Recovery.
