---
title: Migreren naar Azure Premium-opslag met Azure Site Recovery | Microsoft Docs
description: Uw bestaande virtuele machines migreren naar Azure Premium-opslag met Site Recovery. Premium-opslag biedt ondersteuning voor schijven voor hoge prestaties, lage latentie voor I/O-intensieve werkbelastingen die worden uitgevoerd op Azure Virtual Machines.
services: storage
cloud: Azure
documentationcenter: na
author: luywang
manager: kavithag
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/06/2017
ms.author: luywang
ms.openlocfilehash: cc364bdae49068a50ec86c537c3b878670b8b8b7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="migrating-to-premium-storage-using-azure-site-recovery"></a>Migreren naar Premium Storage met Azure Site Recovery

[Azure Premium-opslag](storage-premium-storage.md) biedt ondersteuning voor hoge prestaties, lage latentie schijven voor virtuele machines (VM's) die I/O-intensieve werkbelastingen worden uitgevoerd. Het doel van deze handleiding is om gebruikers hun VM-schijven van de account van een Standard-opslag migreren naar een Premium storage-account met behulp van [Azure Site Recovery](../site-recovery/site-recovery-overview.md).

Site Recovery is een Azure-service die aan uw strategie voor zakelijke continuïteit en noodherstel bijdraagt door de replicatie van fysieke on-premises servers en virtuele machines in de cloud (Azure) of naar een secundair datacenter te organiseren. Wanneer er storingen optreden op uw primaire locatie, schakelt u over naar de secundaire locatie om toepassingen en workloads beschikbaar te houden. U failback naar uw primaire locatie wanneer deze weer normaal functioneren. Site Recovery biedt testfailovers ter ondersteuning van noodhersteloefeningen zonder productieomgevingen. U kunt failovers met minimaal gegevensverlies (afhankelijk van de replicatiefrequentie) bij onverwachte noodsituaties uitvoeren. In het scenario van de migratie naar de Premium-opslag, kunt u de [-Failover in Site Recovery](../site-recovery/site-recovery-failover.md) in Azure Site Recovery doel schijven migreren naar een Premium storage-account.

Het is raadzaam om de migratie naar de Premium-opslag met behulp van Site Recovery omdat deze optie minimale downtime biedt en de handmatige uitvoering van het kopiëren van schijven en het maken van nieuwe virtuele machines voorkomt. Site Recovery wordt systematischer kopiëren van de schijven en nieuwe virtuele machines maken tijdens de failover. Site Recovery biedt ondersteuning voor verschillende soorten failovers met minimaal of er geen uitvaltijd. Voor het plannen van uw uitvaltijd en verlies van gegevens schatten, Zie de [soorten failovers](../site-recovery/site-recovery-failover.md) tabel in Site Recovery. Als u [voorbereiden verbinding maken met virtuele Azure-machines na een failover](../site-recovery/site-recovery-vmware-to-azure.md), moet u kunnen verbinding maken met de Azure-VM met RDP na een failover.

![][1]

## <a name="azure-site-recovery-components"></a>Azure Site Recovery-onderdelen

Dit zijn de Site Recovery-onderdelen die relevant voor dit migratiescenario zijn.

* **Configuratieserver** is van een virtuele machine van Azure die coördineert de communicatie en processen voor replicatie en herstel van gegevens beheert. Op deze virtuele machine voert u een één installatiebestand voor het installeren van de configuratieserver en een extra onderdeel, een processerver als replicatiegateway genoemd. Meer informatie over [server configuratievereisten](../site-recovery/site-recovery-vmware-to-azure.md). Configuratieserver alleen moet eenmaal worden geconfigureerd en kan worden gebruikt voor alle migraties om dezelfde regio.

* **Processerver** replicatiegateway die replicatiegegevens van virtuele bronmachines ontvangt optimaliseert de gegevens met caching, compressie en codering en verzendt het naar een opslagaccount is. Ook push-installatie van de mobility-service naar de virtuele bronmachines worden verwerkt en wordt automatische detectie van de virtuele bronmachines uitgevoerd. De processerver standaard is geïnstalleerd op de configuratieserver. U kunt aanvullende zelfstandige processervers om te schalen van uw implementatie kunt implementeren. Meer informatie over [best practices voor processerverimplementatie](https://azure.microsoft.com/blog/best-practices-for-process-server-deployment-when-protecting-vmware-and-physical-workloads-with-azure-site-recovery/) en [implementatie extra processervers](../site-recovery/site-recovery-plan-capacity-vmware.md#deploy-additional-process-servers). Processerver alleen moet eenmaal worden geconfigureerd en kan worden gebruikt voor alle migraties om dezelfde regio.

* **Mobility-service** is een onderdeel dat is geïmplementeerd op elke standard VM die u wilt repliceren. Deze gegevens schrijfbewerkingen op de standaard virtuele machine vastgelegd en stuurt deze door naar de processerver. Meer informatie over [gerepliceerde machine vereisten](../site-recovery/site-recovery-vmware-to-azure.md).

Deze afbeelding ziet u hoe deze onderdelen samenwerken.

![][15]

> [!NOTE]
> Site Recovery biedt geen ondersteuning voor de migratie van schijven met opslagruimten.

Raadpleeg voor aanvullende onderdelen voor andere scenario's [scenarioarchitectuur](../site-recovery/site-recovery-vmware-to-azure.md).

## <a name="azure-essentials"></a>Azure essentials

Dit zijn de Azure-vereisten voor dit migratiescenario.

* Een Azure-abonnement
* Een Azure Premium storage-account voor het opslaan van gerepliceerde gegevens
* Een Azure-netwerk (VNet) waarmee virtuele machines verbinding maken wanneer ze worden gemaakt bij een failover. Het Azure VNet moet zich in dezelfde regio bevinden als die waarin de Site Recovery wordt uitgevoerd
* Een standaard Azure storage-account waarin replicatielogboeken worden opgeslagen. Dit is hetzelfde opslagaccount als de schijven van de virtuele machine wordt gemigreerd

## <a name="prerequisites"></a>Vereisten

* Inzicht in de relevante migratie scenario-onderdelen in de vorige sectie
* De uitvaltijd plannen door informatie over de [-Failover in Site Recovery](../site-recovery/site-recovery-failover.md)

## <a name="setup-and-migration-steps"></a>Stappen voor installatie en -migratie

U kunt Site Recovery kunt gebruiken voor het migreren van Azure IaaS VM's tussen regio's of binnen dezelfde regio. De volgende instructies zijn aangepast voor dit migratiescenario van het artikel [VMware-machines repliceren of fysieke servers naar Azure](../site-recovery/site-recovery-vmware-to-azure.md). Volg de koppelingen voor gedetailleerde stappen voor het extra de instructies in dit artikel.

1. **Een Recovery Services-kluis maken**. Maken en beheren van de Site Recovery-kluis via de [Azure-portal](https://portal.azure.com). Klik op **nieuwe** > **Management** > **back-up** en **Site Recovery (OMS)**. U kunt ook klikken op **Bladeren** > **Recovery Services-kluis** > **toevoegen**. Virtuele machines worden gerepliceerd naar de regio die u in deze stap opgeeft. Selecteer de regio waar uw Bronmachines en bron storage-accounts zijn omwille van de migratie in dezelfde regio. Houd er rekening mee dat de migratie naar Premium storage-accounts wordt alleen ondersteund in de [Azure-portal](https://portal.azure.com), niet de [klassieke portal](https://manage.windowsazure.com).

2. De volgende stappen kunt u **uw beveiligingsdoelstellingen kiezen**.

    2a. Open op de virtuele machine waarop u wilt installeren van de configuratieserver, de [Azure-portal](https://portal.azure.com). Ga naar **Recovery Services-kluizen** > **instellingen**. Onder **instellingen**, selecteer **siteherstel**. Onder **siteherstel**, selecteer **stap 1: infrastructuur voorbereiden**. Onder **infrastructuur voorbereiden**, selecteer **beveiligingsdoel**.

    ![][2]

    2b. Onder **beveiligingsdoel**, selecteer in de vervolgkeuzelijst eerste **naar Azure**. Selecteer in de vervolgkeuzelijst tweede **niet gevirtualiseerde / andere**, en klik vervolgens op **OK**.

    ![][3]

3. De volgende stappen kunt u **instellen van de bronomgeving (configuratieserver)**.

    3a. Download de **Azure Site Recovery Unified Setup** en de **kluisregistratiesleutel** door te gaan naar de **infrastructuur voorbereiden**  >   **Bron voorbereiden** > **Server toevoegen** blade. U moet de kluisregistratiesleutel de uniforme setup uit te voeren. De sleutel blijft vijf dagen na het genereren ervan geldig.

    ![][4]

    3b. Toevoegen van de configuratieserver in de **Server toevoegen** blade.

    ![][5]

    3c. Op de virtuele machine die u als de configuratieserver, Unified Setup uitvoeren om te installeren van de configuratieserver en de processerver. U kunt de schermafbeeldingen doorlopen [hier](../site-recovery/site-recovery-vmware-to-azure.md) om de installatie te voltooien. U kunt verwijzen naar de volgende schermafbeeldingen voor stappen die zijn opgegeven voor dit migratiescenario.

    Selecteer bij **Voordat u begint** de optie **De configuratieserver en processerver installeren**.

    ![][6]

    3D. In **registratie**, bladeren en selecteer de registratiesleutel die u hebt gedownload van de kluis.

    ![][7]

    3e. Selecteer bij **Details van de omgeving** of u virtuele VMware-machines wilt repliceren. Voor dit migratiescenario kiezen **Nee**.

    ![][8]

    3F. Nadat de installatie voltooid is, ziet u de **Microsoft Azure Site Recovery-configuratieserver** venster. Gebruik de **Accounts beheren** tabblad account wilt maken die Site Recovery kunt gebruiken voor automatische detectie. (In het scenario over het beveiligen van fysieke machines, instellen van het account niet relevant, maar u moet ten minste één account om in te schakelen op een van de volgende stappen uit. In dit geval kunt u naam-account en wachtwoord als willekeurig.) Gebruik de **kluis registratie** tabblad voor het uploaden van het kluisreferentiebestand.

    ![][9]

4. **De doelomgeving instellen**. Klik op **infrastructuur voorbereiden** > **doel**, en geef het implementatiemodel dat u wilt gebruiken voor virtuele machines na een failover. U kunt kiezen **klassieke** of **Resource Manager**, afhankelijk van uw scenario.

    ![][10]

    Site Recovery controleert of u een of meer compatibele Azure-opslagaccounts en -netwerken hebt. Houd er rekening mee dat als u een Premium storage-account voor gerepliceerde gegevens gebruikt, u moet een extra Standard-opslagaccount instellen voor replicatielogboeken worden opgeslagen.

5. **Replicatie-instellingen instellen**. Volg [replicatie-instellingen instellen](../site-recovery/site-recovery-vmware-to-azure.md) om te controleren of uw configuratieserver is gekoppeld aan het replicatiebeleid dat u maakt.

6. **Capaciteitsplanning**. Gebruik de [Capaciteitsplanner](../site-recovery/site-recovery-capacity-planner.md) moet netwerkbandbreedte, opslag en andere vereisten om te voldoen aan uw replicatie nauwkeurig te schatten. Wanneer u bent klaar, selecteert u **Ja** in **hebt u capaciteitsplanning?**.

    ![][11]

7. De volgende stappen kunt u **installeren van de mobility-service en -replicatie inschakelen**.

    7. U kunt [push-installatie](../site-recovery/site-recovery-vmware-to-azure.md) aan uw Bronmachines of aan [handmatig installeren van de mobility-service](../site-recovery/site-recovery-vmware-to-azure-install-mob-svc.md) op uw virtuele bronmachines. U vindt de vereiste van de installatie en het pad van het installatieprogramma voor het handmatig pushen in de koppeling. Als u een handmatige installatie uitvoert, moet u mogelijk een interne IP-adres gebruiken om te bepalen van de configuratieserver.

    ![][12]

    De failover-VM heeft twee tijdelijke schijven: één van de primaire virtuele machine en de andere gemaakt tijdens het inrichten van virtuele machine in de regio van het herstel. Als u wilt uitsluiten van de tijdelijke schijf voordat de replicatie, installeert u de mobility-service voordat u replicatie inschakelt. Raadpleeg voor meer informatie over het uitsluiten van de tijdelijke schijf [schijven uitsluiten van replicatie](../site-recovery/site-recovery-vmware-to-azure.md).

    7 ter. Schakel nu als volgt replicatie in:
      * Klik op **toepassing repliceren** > **bron**. Nadat u replicatie voor het eerst hebt ingeschakeld, klik op + repliceren in de kluis aanvullende machines replicatie in te schakelen.
      * In stap 1 voert instellen als uw processerver.
      * Geef het implementatiemodel na een failover, een Premium storage-account om te migreren naar, een standaard opslagaccount logboeken en een virtueel netwerk niet opslaan in stap 2.
      * In stap 3 toevoegen beveiligde virtuele machines op IP-adres (mogelijk moet u een interne IP-adres te zoeken).
      * In stap 4, door de eigenschappen te configureren met behulp van de accounts die u eerder hebt ingesteld op de processerver.
      * Kies in stap 5, het replicatiebeleid dat u eerder hebt gemaakt, instellen van de replicatie-instellingen.
      Klik op **OK** en replicatie inschakelen.

    > [!NOTE]
    > Wanneer een Azure VM is de toewijzing ongedaan gemaakt en opnieuw hebt gestart, is er geen garantie dat hetzelfde IP-adres worden opgehaald. Als het IP-adres van de server-proces configuratieserver of de beveiligde virtuele machines van Azure wijzigt, werkt de replicatie in dit scenario mogelijk niet correct.

    ![][13]

    Wanneer u uw Azure Storage-omgeving ontwerpt, wordt u aangeraden dat u afzonderlijke storage-accounts voor elke virtuele machine in een beschikbaarheidsset gebruiken. We raden u aan de aanbevolen procedure in de opslaglaag te [meerdere storage-accounts gebruiken voor elke beschikbaarheidsset](../virtual-machines/windows/manage-availability.md). Distributie van VM-schijven naar meerdere accounts voor opslag voor het verbeteren van de beschikbaarheid van opslag en verdeelt de i/o over de Azure-opslag-infrastructuur. Als uw virtuele machines in een beschikbaarheidsset, in plaats van de schijven van alle virtuele machines repliceren naar één storage-account, sterk aangeraden meerdere keren voor meerdere virtuele machines migreren zodat de virtuele machines in dezelfde beschikbaarheidsset één storage-account niet delen. Gebruik de **replicatie inschakelen** blade een doelopslagaccount instellen voor elke virtuele machine, één voor één. U kunt een implementatiemodel na een failover volgens uw behoeften. Als u Resource Manager (RM) als uw na een failover-implementatiemodel kiest, kunt u een RM-VM naar een RM-virtuele machine failover of u kunt een klassieke virtuele machine naar een RM-virtuele machine failover.

8. **Een testfailover uitvoeren**. Als u wilt controleren of de replicatie voltooid is, klikt u op het herstel van uw Site en klik vervolgens op **instellingen** > **gerepliceerde Items**. U ziet de status en het percentage van het replicatieproces. Na de initiële replicatie is voltooid, Testfailover voor het valideren van uw replicatiestrategie voor uitvoeren. Raadpleeg voor gedetailleerde stappen van de testfailover [een testfailover uitvoeren in Site Recovery](../site-recovery/site-recovery-vmware-to-azure.md). U ziet de status van de testfailover in **instellingen** > **taken** > **YOUR_FAILOVER_PLAN_NAME**. Op de blade ziet u een overzicht van de stappen en de resultaten van de geslaagde/mislukte. Als de testfailover is mislukt tijdens elke stap, klikt u op de stap voor het controleren van het foutbericht. Zorg ervoor dat uw virtuele machines en replicatiestrategie voldoen aan de vereisten voordat u een failover uitvoert. Lees [Testfailover naar Azure in Site Recovery](../site-recovery/site-recovery-test-failover-to-azure.md) voor meer informatie en instructies van de testfailover.

9. **Een failover uitvoeren**. Nadat de test is failover voltooid, wordt een failover voor het migreren van uw schijven naar Premium-opslag en repliceren van de VM-instanties worden uitgevoerd. Volg de gedetailleerde stappen in [een failover uitvoeren](../site-recovery/site-recovery-failover.md#run-a-failover). Zorg ervoor dat u selecteert **virtuele machines afsluiten en de meest recente gegevens synchroniseren** om op te geven dat de Site Recovery proberen moet de beveiligde virtuele machines afsluiten en de gegevens te synchroniseren, zodat de meest recente versie van de gegevens failover. Als u deze optie niet selecteert of de poging niet lukt worden de failover van de meest recente beschikbare herstelpunt voor de virtuele machine. Site Recovery maakt een VM-exemplaar waarvan het type hetzelfde als of vergelijkbare voor een virtuele machine voor Premium-compatibel zijn met opslag is. U kunt de prestaties en de prijs van verschillende VM-instanties controleren door te gaan naar [prijzen van virtuele Machines in Windows](https://azure.microsoft.com/pricing/details/virtual-machines/windows/) of [prijzen van Linux virtuele Machines](https://azure.microsoft.com/pricing/details/virtual-machines/linux/).

## <a name="post-migration-steps"></a>Stappen na de migratie

1. **Configureren van de gerepliceerde virtuele machines voor de beschikbaarheidsset, indien van toepassing**. Site Recovery biedt geen ondersteuning voor migratie VM's samen met de beschikbaarheidsset. Afhankelijk van de implementatie van de gerepliceerde virtuele machine, gaat u een van de volgende:
  * Voor een virtuele machine gemaakt met behulp van het klassieke implementatiemodel: de virtuele machine toevoegen aan de beschikbaarheidsset voor de Azure-portal. Ga voor gedetailleerde stappen naar [een bestaande virtuele machine toevoegen aan een beschikbaarheidsset](../virtual-machines/windows/classic/configure-availability.md#addmachine).
  * Voor het Resource Manager-implementatiemodel: opslaan van uw configuratie van de virtuele machine en vervolgens verwijderen en opnieuw maken van de virtuele machines in de beschikbaarheidsset. Om dit te doen, gebruikt u het script op [ingesteld Azure Resource Manager VM Beschikbaarheidsset](https://gallery.technet.microsoft.com/Set-Azure-Resource-Manager-f7509ec4). Controleer de beperking van dit script en uitvaltijd plannen voordat het script wordt uitgevoerd.

2. **Verwijderen van oude VM's en schijven**. Voordat u verwijdert deze, Controleer of de Premium-schijven zijn consistent met de bron-schijven en de nieuwe virtuele machines uit te voeren dezelfde functie uit als de bron-VM's. In het implementatiemodel van Resource Manager (RM) Verwijder de virtuele machine en de schijven verwijderen uit uw gegevensbron storage-accounts in de Azure portal. In het klassieke implementatiemodel, kunt u de virtuele machine en de schijven in de klassieke portal of Azure-portal te verwijderen. Als er een probleem waarbij de schijf niet verwijderd ondanks dat u de virtuele machine hebt verwijderd, raadpleegt u [fouten bij het verwijderen van VHD's oplossen](storage-resource-manager-cannot-delete-storage-account-container-vhd.md).

3. **Opschonen van de Azure Site Recovery-infrastructuur**. Wanneer u Site Recovery niet langer nodig hebt, kunt u de infrastructuur opschonen gerepliceerde items, de configuratieserver en het herstelbeleid verwijderd en wordt vervolgens de Azure Site Recovery-kluis te verwijderen.

## <a name="troubleshooting"></a>Problemen oplossen

* [Controleren en problemen oplossen van beveiliging voor virtuele machines en fysieke servers](../site-recovery/site-recovery-monitoring-and-troubleshooting.md)
* [Microsoft Azure Site Recovery-forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr)

## <a name="next-steps"></a>Volgende stappen

Zie de volgende bronnen voor specifieke scenario's voor het migreren van virtuele machines:

* [Azure virtuele Machines tussen Opslagaccounts migreren](https://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/)
* [Maken en een Windows Server-VHD uploaden naar Azure.](../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [Maakt en uploadt u een virtuele harde schijf met het Linux-besturingssysteem](../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Migreren van virtuele Machines van Amazon AWS naar Microsoft Azure](http://channel9.msdn.com/Series/Migrating-Virtual-Machines-from-Amazon-AWS-to-Microsoft-Azure)

Zie ook de volgende bronnen voor meer informatie over Azure Storage en Azure Virtual Machines:

* [Azure Storage](https://azure.microsoft.com/documentation/services/storage/)
* [Virtuele Machines in Azure](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [Premium Storage: opslag met hoge prestaties voor de werkbelasting van virtuele Azure-machines](storage-premium-storage.md)

[1]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-1.png
[2]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-2.png
[3]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-3.png
[4]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-4.png
[5]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-5.png
[6]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-6.PNG
[7]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-7.PNG
[8]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-8.PNG
[9]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-9.PNG
[10]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-10.png
[11]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-11.PNG
[12]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-12.PNG
[13]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-13.png
[14]:../site-recovery/media/site-recovery-vmware-to-azure/v2a-architecture-henry.png
[15]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-14.png
