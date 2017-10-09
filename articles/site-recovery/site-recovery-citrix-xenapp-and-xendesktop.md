---
title: een Citrix XenDesktop en XenApp implementatie van meerdere lagen met Azure Site Recovery aaaReplicate | Microsoft Docs
description: Dit artikel wordt beschreven hoe tooprotect en herstel Citrix XenDesktop en XenApp implementaties met Azure Site Recovery.
services: site-recovery
documentationcenter: 
author: ponatara
manager: abhemraj
editor: 
ms.assetid: 9126f5e8-e9ed-4c31-b6b4-bf969c12c184
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: ponatara
ms.openlocfilehash: c4ea9f95f91c585cdcf9d776b02c0967f4c16ab0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-a-multi-tier-citrix-xenapp-and-xendesktop-deployment-using-azure-site-recovery"></a>Een Citrix XenApp en XenDesktop implementatie van meerdere lagen met Azure Site Recovery repliceren

## <a name="overview"></a>Overzicht

Citrix XenDesktop is een bureaublad-virtualisatie-oplossing die bureaubladen en toepassingen als ondemand service tooany gebruiker met een willekeurige plaats levert. Met de FlexCast levering technologie kunt XenDesktop snel en veilig leveren toepassingen en bureaubladen toousers.
Vandaag de dag biedt Citrix XenApp geen elke ramp herstelfuncties.

Een goede noodhersteloplossing moet modellering van herstelplannen rond Hallo hierboven architecturen voor complexe toepassingen bevatten en ook Hallo mogelijkheid tooadd aangepast stappen toohandle Toepassingstoewijzingen tussen verschillende lagen daarom bieden een één klik ervoor oplossing maken in geval van een noodgeval voorloopspaties tooa Hallo RTO verlagen.

Dit document bevat een stapsgewijze instructies voor het bouwen van een noodherstel voor uw on-premises Citrix XenApp implementaties op Hyper-V- en VMware vSphere-platforms. Dit document beschrijft ook hoe tooperform een testfailover (drill disaster recovery) en niet-geplande failover tooAzure met herstelplannen, Hallo ondersteunde configuraties en vereisten.


## <a name="prerequisites"></a>Vereisten

Voordat u begint, zorg er dan voor dat u begrijpt Hallo volgende:

1. [Een virtuele machine tooAzure repliceren](site-recovery-vmware-to-azure.md)
1. Hoe te[ontwerpen van een netwerk herstel](site-recovery-network-design.md)
1. [Tijdens het doorzoeken van een failover-test tooAzure](site-recovery-test-failover-to-azure.md)
1. [Tijdens het doorzoeken van een failover-tooAzure](site-recovery-failover.md)
1. Hoe te[repliceren van een domeincontroller](site-recovery-active-directory.md)
1. Hoe te[SQL-Server repliceren](site-recovery-sql.md)

## <a name="deployment-patterns"></a>Implementaties

Een farm Citrix XenApp en XenDesktop heeft doorgaans Hallo implementatie patroon volgen:

**Patroon van de implementatie**

Citrix XenApp en XenDesktop implementatie met AD DNS-server, SQL databaseserver server, Citrix levering Controller, winkel, XenApp Master (VDA), Citrix XenApp licentieserver

![Implementatie-patroon 1](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-deployment.png)


## <a name="site-recovery-support"></a>Site Recovery-ondersteuning

Citrix-implementaties op virtuele VMware-machines worden beheerd door vSphere 6.0-System Center VMM 2012 R2 zijn gebruikte toosetup DR voor Hallo doel van dit artikel.

### <a name="source-and-target"></a>Bron en doel

**Scenario** | **de secundaire site tooa** | **tooAzure**
--- | --- | ---
**Hyper-V** | Niet binnen het bereik | Ja
**VMware** | Niet binnen het bereik | Ja
**Fysieke server** | Niet binnen het bereik | Ja

### <a name="versions"></a>Versies
Klanten kunnen XenApp onderdelen implementeren als virtuele Machines waarop Hyper-V- of VMware of fysieke Servers. Azure Site Recovery kunt beveiligen beide tooAzure fysieke en virtuele-implementaties.
Aangezien XenApp 7,7 of hoger wordt ondersteund in Azure, alleen implementaties met deze versies failover mogelijk tooAzure voor herstel na noodgevallen of migratie.

### <a name="things-tookeep-in-mind"></a>Dingen tookeep rekening

1. Beveiliging en herstel van lokale implementaties met behulp van Server-besturingssysteem machines toodeliver XenApp gepubliceerde apps en XenApp gepubliceerd bureaubladen wordt ondersteund.

2. Beveiliging en herstel van on-premises implementaties met bureaublad OS machines toodeliver VDI Desktop voor client virtuele bureaubladen, met inbegrip van Windows 10, wordt niet ondersteund. Dit is omdat ASR Hallo herstel van machines met bureaublad OS'es niet ondersteunt.  Bovendien sommige client virtueel bureaublad aroma's (bv. Windows 7) zijn nog niet ondersteund voor licentieverlening in Azure. [Meer informatie](https://azure.microsoft.com/pricing/licensing-faq/) over licentieverlening voor clientbureaubladen en serverdesktops in Azure.

3.  Azure Site Recovery kan niet repliceren en de bestaande lokale MCS of PV's klonen beveiligen.
U moet deze met Azure RM inrichten vanuit levering domeincontroller klonen toorecreate.

4. NetScaler kan niet worden beveiligd met Azure Site Recovery zoals NetScaler is gebaseerd op FreeBSD en Azure Site Recovery biedt geen ondersteuning voor beveiliging van het besturingssysteem FreeBSD. U zou toodeploy nodig hebt en een nieuw toestel NetScaler van Azure-marktplaats na failover tooAzure configureren.


## <a name="replicating-virtual-machines"></a>Repliceren van virtuele machines

Hallo volgende onderdelen van Hallo Citrix XenApp implementatie moet toobe beveiligd tooenable replicatie en herstel.

* Beveiliging van AD DNS-server
* Beveiliging van SQL database-server
* Beveiliging van Citrix levering Controller
* Beveiliging van server winkel.
* Beveiliging van XenApp Master (VDA)
* Beveiliging van de licentieserver Citrix XenApp


**AD DNS-server-replicatie**

Raadpleeg het te[beveiligen van Active Directory en DNS met Azure Site Recovery](site-recovery-active-directory.md) op richtlijnen voor het repliceren van en het configureren van een domeincontroller in Azure.

**SQL Server databasereplicatie**

Raadpleeg het te[SQL-Server beveiligen met SQL Server-noodherstel en Azure Site Recovery](site-recovery-sql.md) voor gedetailleerde technische richtlijnen voor Hallo aanbevolen opties voor het beveiligen van SQL-servers.

Ga als volgt [in deze richtlijnen](site-recovery-vmware-to-azure.md) toostart repliceren Hallo andere tooAzure van onderdeel virtuele machines.

![Beveiliging van XenApp onderdelen](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-enablereplication.png)

**Reken- en netwerkinstellingen**

Nadat Hallo-machines zijn beveiligd (status wordt weergegeven als 'Beveiligde' onder gerepliceerde Items), Compute Hallo en netwerkinstellingen moeten toobe geconfigureerd.
In de berekening en netwerk > Compute-eigenschappen, kunt u de naam en doel van de grootte van virtuele machine van Azure Hallo opgeven.
Hallo naam toocomply met Azure-vereisten wijzigen als u wilt. U kunt ook bekijken en informatie over het doelnetwerk hello, subnet en IP-adres dat wordt toegewezen toohello virtuele Azure-machine toevoegen.

Let op Hallo volgende:

* U kunt IP-adres van Hallo doel instellen. Als u een adres niet opgeeft, wordt Hallo failover machine DHCP gebruikt. Als u een adres dat is niet beschikbaar bij een failover, werkt Hallo failover niet. Hallo hetzelfde IP-adres van doel kan worden gebruikt voor een testfailover als Hallo adres in het testfailovernetwerk Hallo beschikbaar is.

* Voor Hallo AD en DNS-server, bewaren Hallo on-premises adres-kunt die u dezelfde adres Hallo opgeven als Hallo DNS-server voor hello Azure Virtual network.

Hallo aantal netwerkadapters wordt bepaald door Hallo-grootte die u voor Hallo doel-virtuele machine, als volgt opgeeft:

*   Als het aantal netwerkadapters op de bronmachine Hallo Hallo kleiner dan of gelijk aantal adapters toohello toegestaan voor de doelgrootte machine Hallo vervolgens Hallo doel hetzelfde aantal adapters als bron Hallo Hallo.
*   Als het aantal adapters voor de virtuele bronmachine Hallo HALLO hallo maximum overschrijden voor Hallo doelgrootte, wordt maximaal Hallo doel wordt gebruikt.
* Als een bronmachine twee netwerkadapters heeft en de grootte van Hallo doelmachine vier ondersteunt, wordt Hallo doelmachine twee adapters hebben. Als Hallo-bronmachine twee adapters heeft, maar hello ondersteunde doelgrootte biedt alleen ondersteuning voor een hebben Hallo doelmachine slechts één adapter.
*   Als Hallo virtuele machine meerdere netwerkadapters heeft worden deze allemaal verbonden toohello hetzelfde netwerk.
*   Als Hallo virtuele machine meerdere netwerkadapters heeft, wordt hello eerste is weergegeven in de lijst hello vervolgens Hallo standaard-netwerkadapter in hello Azure virtuele machine.


## <a name="creating-a-recovery-plan"></a>Een herstelplan maken

Nadat de replicatie is ingeschakeld voor Hallo XenApp onderdeel VM's, is de volgende stap Hallo toocreate een herstelplan.
Een herstelplan groepen samen virtuele machines met vergelijkbare vereisten voor failover en herstel.  

**Stappen toocreate een herstelplan**

1. Hallo XenApp onderdeel virtual machines toevoegen in Hallo herstelplan.
2. Klik op de herstelplannen -> + herstelplan. Geef een intuïtieve naam voor het herstelplan Hallo.
3. Voor virtuele VMware-machines: bron selecteren als processerver VMware, doel als Microsoft Azure en implementatiemodel als Resource Manager en klik op items selecteren.
4. Voor Hyper-V virtuele machines: bron selecteren als VMM-server, zoals Microsoft Azure en als Resource Manager-implementatiemodel zijn gericht en klik op items selecteren en selecteer Hallo XenApp implementatie virtuele machines.

### <a name="adding-virtual-machines-toofailover-groups"></a>Toevoegen van virtuele machines toofailover groepen

Plannen voor herstel kunnen worden aangepast tooadd failover groepen voor starten van de specifieke volgorde, scripts of handmatige acties. Hallo na groepen moet toobe toegevoegde toohello herstelplan.

1. Failover Group1: AD DNS
2. Failover-Group2: SQL Server-VM's
2. Failover groep3: VDA Master installatiekopie VM
3. Failover Group4: De levering van Controller en de winkel server VMs


### <a name="adding-scripts-toohello-recovery-plan"></a>Het herstelplan toohello toe te voegen scripts

Scripts kunnen worden uitgevoerd vóór of na een bepaalde groep in een plan voor herstel. Handmatige acties kunnen worden ook worden opgenomen en tijdens de failover is uitgevoerd.

de aangepaste herstelplan Hallo ziet er Hallo hieronder:

1. Failover Group1: AD DNS
2. Failover-Group2: SQL Server-VM's
3. Failover groep3: VDA Master installatiekopie VM

   >[!NOTE]     
   >Stap 4, 6 en 7 met handmatige of script acties zijn van toepassing tooonly een lokale XenApp >-omgeving met MCS/PV's catalogussen.

4. De actie handmatig of script groep 3: afsluiten master VDA VM Hallo Master VDA VM na een failover uitgevoerd tooAzure zich in een actieve status. toocreate nieuwe MCS catalogussen met behulp van Azure ARM die als host fungeert, Hallo master VDA VM is vereist toobe in gestopt (de toegewezen) staat. Afsluiten hello VM van Azure Portal.

5. Failover Group4: De levering van Controller en de winkel server VMs
6. Groep3 handmatig of script actie 1:

    ***Azure RM hostverbinding toevoegen***

    Azure ARM hostverbinding maken in levering Controller machine tooprovision nieuwe MCS catalogussen in Azure. Hallo stappen zoals wordt beschreven in dit [artikel](https://www.citrix.com/blogs/2016/07/21/connecting-to-azure-resource-manager-in-xenapp-xendesktop/).

7. Groep3 handmatig of script actie 2:

    ***MCS-catalogussen in Azure opnieuw maken***

    Hallo bestaande MCS of PV's klonen op Hallo primaire site worden niet gerepliceerd tooAzure. U moet deze met behulp van Hallo klonen gerepliceerd master VDA en Azure ARM-inrichting van levering controller toorecreate. Hallo stappen zoals wordt beschreven in dit [artikel](https://www.citrix.com/blogs/2016/09/12/using-xenapp-xendesktop-in-azure-resource-manager/) toocreate MCS catalogus maken in Azure.

![Plan voor herstel voor XenApp onderdelen](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-recoveryplan.png)


   >[!NOTE]
   >U kunt scripts op de [locatie](https://github.com/Azure/azure-quickstart-templates/blob/>master/asr-automation-recovery/scripts) tooupdate hello, DNS-Hello nieuwe IP-adressen van Hallo failover > virtuele machines of tooattach een load balancer op Hallo failover virtuele machine, indien nodig.


## <a name="doing-a-test-failover"></a>Een testfailover uitvoeren

Ga als volgt [in deze richtlijnen](site-recovery-test-failover-to-azure.md) toodo een testfailover.

![Plan voor herstel](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-tfo.png)


## <a name="doing-a-failover"></a>U een failover uitvoert

Ga als volgt [in deze richtlijnen](site-recovery-failover.md) bij het uitvoeren van een failover.

## <a name="next-steps"></a>Volgende stappen

U kunt [meer](https://aka.ms/citrix-xenapp-xendesktop-with-asr) over Citrix XenApp en XenDesktop implementaties in deze white paper repliceren. Bekijkt hello richtlijnen te[andere toepassingen repliceren](site-recovery-workload.md) met Site Recovery.
