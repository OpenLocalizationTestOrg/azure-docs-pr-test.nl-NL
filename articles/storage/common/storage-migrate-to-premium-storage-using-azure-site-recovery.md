---
title: aaaMigrating tooAzure Premium-opslag met Azure Site Recovery (niet-beheerde schijven) | Microsoft Docs
description: Migreer uw bestaande virtuele machines tooAzure Premium-opslag met Site Recovery (niet-beheerde schijven).
services: storage
documentationcenter: 
author: luywang
manager: kavithag
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: luywang
ms.openlocfilehash: 2c82fffaa38baeeb4a676748125bd85d6e0500f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-toopremium-storage-using-azure-site-recovery-unmanaged-disks"></a>Migreren tooPremium Storage met Azure Site Recovery (niet-beheerde schijven)

[Azure Premium-opslag](storage-premium-storage.md) biedt ondersteuning voor hoge prestaties, lage latentie schijven voor virtuele machines (VM's) die I/O-intensieve werkbelastingen worden uitgevoerd. Hallo-doel van deze handleiding is toohelp gebruikers hun VM-schijven migreert van een Standard-opslag account tooa Premium storage-account met behulp van [Azure Site Recovery](../../site-recovery/site-recovery-overview.md).

Site Recovery is een Azure-service die tooyour zakelijke continuïteit bijdraagt en noodherstelplan door te organiseren Hallo replicatie van fysieke on-premises servers en virtuele machines toohello cloud (Azure) of tooa secundair datacenter. Wanneer er storingen optreden op uw primaire locatie, schakelt u over toohello secundaire locatie tookeep toepassingen en workloads beschikbaar. U mislukken back tooyour primaire locatie wanneer deze toonormal bewerking weer. Site Recovery biedt testfailovers toosupport noodhersteloefeningen zonder productieomgevingen. U kunt failovers met minimaal gegevensverlies (afhankelijk van de replicatiefrequentie) bij onverwachte noodsituaties uitvoeren. In geval van Hallo tooPremium opslag migreert, kunt u Hallo [-Failover in Site Recovery](../../site-recovery/site-recovery-failover.md) in Azure Site Recovery toomigrate doel schijven tooa Premium storage-account.

Het is raadzaam migreren tooPremium opslag met behulp van Site Recovery omdat deze optie minimale downtime biedt en Hallo handmatig uitvoeren voorkomt van het kopiëren van schijven en het maken van nieuwe virtuele machines. Site Recovery wordt systematischer kopiëren van de schijven en nieuwe virtuele machines maken tijdens de failover. Site Recovery biedt ondersteuning voor verschillende soorten failovers met minimaal of er geen uitvaltijd. tooplan uw schatting van uitvaltijd en verlies van gegevens, Zie Hallo [soorten failovers](../../site-recovery/site-recovery-failover.md) tabel in Site Recovery. Als u [voorbereiden tooconnect tooAzure VM's na een failover](../../site-recovery/vmware-walkthrough-overview.md), moet u kunnen tooconnect toohello virtuele machine van Azure met RDP na een failover.

![][1]

## <a name="azure-site-recovery-components"></a>Azure Site Recovery-onderdelen

Dit zijn onderdelen van Site Recovery Hallo die relevant toothis migratiescenario.

* **Configuratieserver** is van een virtuele machine van Azure die coördineert de communicatie en processen voor replicatie en herstel van gegevens beheert. Op deze virtuele machine voert u een één setup tooinstall Hallo configuratie bestandsserver en een extra onderdeel, een processerver als replicatiegateway genoemd. Meer informatie over [server configuratievereisten](../../site-recovery/vmware-walkthrough-overview.md). Configuratieserver alleen moet toobe eenmaal is geconfigureerd en kan worden gebruikt voor alle migraties toohello dezelfde regio.

* **Processerver** replicatiegateway die replicatiegegevens van virtuele bronmachines ontvangt optimaliseert de Hallo-gegevens met caching, compressie en codering, en verzendt het tooa storage-account is. Ook omgaat met push-installatie van Hallo mobility service toosource VM's en automatische detectie van de virtuele bronmachines uitvoert. Hallo proces standaardserver is geïnstalleerd op de configuratieserver Hallo. U kunt aanvullende zelfstandige proces servers tooscale uw implementatie te implementeren. Meer informatie over [best practices voor processerverimplementatie](https://azure.microsoft.com/blog/best-practices-for-process-server-deployment-when-protecting-vmware-and-physical-workloads-with-azure-site-recovery/) en [implementatie extra processervers](../../site-recovery/site-recovery-plan-capacity-vmware.md#deploy-additional-process-servers). Processerver alleen moet toobe eenmaal is geconfigureerd en kan worden gebruikt voor alle migraties toohello dezelfde regio.

* **Mobility-service** is een onderdeel dat is geïmplementeerd op elke standard VM gewenste tooreplicate. Deze gegevens schrijfbewerkingen vastgelegd op Hallo standard VM en stuurt ze toohello processerver. Meer informatie over [gerepliceerde machine vereisten](../../site-recovery/vmware-walkthrough-overview.md).

Deze afbeelding ziet u hoe deze onderdelen samenwerken.

![][15]

> [!NOTE]
> Site Recovery biedt geen ondersteuning voor migratie van Hallo van schijven met opslagruimten.

Voor extra onderdelen voor andere scenario's, raadpleegt u te[scenarioarchitectuur](../../site-recovery/vmware-walkthrough-overview.md).

## <a name="azure-essentials"></a>Azure essentials

Deze zijn hello Azure-vereisten voor dit migratiescenario.

* Een Azure-abonnement
* Een Azure Premium storage-account toostore gerepliceerde gegevens
* Een Azure-netwerk (VNet) toowhich virtuele machines verbinding maken wanneer ze worden gemaakt bij een failover. Hello Azure VNet moet in dezelfde regio Hallo zoals Hallo een in welke Hallo Site Recovery wordt uitgevoerd
* Een standaard Azure storage-account in de logboeken van welke toostore replicatie. Dit kan zijn hetzelfde opslagaccount Hallo zoals Hallo VM schijven wordt gemigreerd

## <a name="prerequisites"></a>Vereisten

* Hallo relevante migratie scenario-onderdelen in de voorgaande sectie Hallo begrijpen
* De uitvaltijd plannen met leren over Hallo [-Failover in Site Recovery](../../site-recovery/site-recovery-failover.md)

## <a name="setup-and-migration-steps"></a>Stappen voor installatie en -migratie

U kunt Site Recovery toomigrate Azure IaaS VM's tussen regio's of binnen dezelfde regio. Hallo volgende instructies zijn aangepast voor dit migratiescenario vanuit Hallo artikel [VMware-machines repliceren of fysieke servers tooAzure](../../site-recovery/vmware-walkthrough-overview.md). Volg Hallo koppelingen voor gedetailleerde stappen in de aanvullende toohello instructies in dit artikel.

1. **Een Recovery Services-kluis maken**. Maken en beheren van Site Recovery-kluis via Hallo Hallo [Azure-portal](https://portal.azure.com). Klik op **nieuwe** > **Management** > **back-up** en **Site Recovery (OMS)**. U kunt ook klikken op **Bladeren** > **Recovery Services-kluis** > **toevoegen**. Virtuele machines worden gerepliceerd toohello regio die u in deze stap opgeeft. Voor doel van de migratie in Hallo Hallo dezelfde regio, selecteer Hallo regio waar uw bron-VM's en bron storage-accounts. 

2. Hallo volgende stappen kunt u **uw beveiligingsdoelstellingen kiezen**.

    2a. Open op de virtuele machine waar u tooinstall Hallo configuratieserver Hallo, Hallo [Azure-portal](https://portal.azure.com). Ga te**Recovery Services-kluizen** > **instellingen**. Onder **instellingen**, selecteer **siteherstel**. Onder **siteherstel**, selecteer **stap 1: infrastructuur voorbereiden**. Onder **infrastructuur voorbereiden**, selecteer **beveiligingsdoel**.

    ![][2]

    2b. Onder **beveiligingsdoel**, Hallo eerste vervolgkeuzelijst in, selecteer **tooAzure**. Selecteer in de tweede vervolgkeuzelijst lijst Hallo **niet gevirtualiseerde / andere**, en klik vervolgens op **OK**.

    ![][3]

3. Hallo volgende stappen kunt u **Hallo bronomgeving (configuratieserver) instellen**.

    3a. Hallo downloaden **Azure Site Recovery Unified Setup** en Hallo **kluisregistratiesleutel** door te gaan toohello **infrastructuur voorbereiden**  >  **Bron voorbereiden** > **Server toevoegen** blade. U moet Hallo kluis registratie sleutel toorun Hallo unified setup. Hallo-sleutel is geldig tot 5 dagen nadat u het genereren.

    ![][4]

    3b. Configuratieserver toevoegen in Hallo **Server toevoegen** blade.

    ![][5]

    3c. Voer Setup Unified tooinstall Hallo configuratieserver en de processerver van Hallo op Hallo VM die u als de configuratieserver hello. U kunt schermafbeeldingen Hallo doorlopen [hier](../../site-recovery/vmware-walkthrough-overview.md) toocomplete Hallo-installatie. U kunt schermafbeeldingen voor stappen die zijn opgegeven voor dit migratiescenario na toohello verwijzen.

    In **voordat u begint met**, selecteer **installeren Hallo configuratieserver en de processerver**.

    ![][6]

    3D. In **registratie**, bladeren en selecteer Hallo registratiesleutel u hebt gedownload van Hallo kluis.

    ![][7]

    3e. In **omgeving Details**Selecteer of u tooreplicate virtuele VMware-machines gaat. Voor dit migratiescenario kiezen **Nee**.

    ![][8]

    3F. Nadat het Hallo-installatie is voltooid, ziet u Hallo **Microsoft Azure Site Recovery-configuratieserver** venster. Gebruik Hallo **Accounts beheren** tabblad toocreate Hallo account met Site Recovery voor automatische detectie gebruiken kunt. (In Hallo scenario over het beveiligen van fysieke machines Hallo-account instellen niet relevant, maar u moet ten minste één account tooenable een Hallo stappen te volgen. In dit geval kunt u naam Hallo-account en wachtwoord als willekeurig.) Gebruik Hallo **kluis registratie** tabblad tooupload hello kluisreferentiebestand.

    ![][9]

4. **Hallo doelomgeving instellen**. Klik op **infrastructuur voorbereiden** > **doel**, en geef Hallo implementatiemodel gewenste toouse voor virtuele machines na een failover. U kunt kiezen **klassieke** of **Resource Manager**, afhankelijk van uw scenario.

    ![][10]

    Site Recovery controleert of u een of meer compatibele Azure-opslagaccounts en -netwerken hebt. Opmerking Als u een Premium storage-account voor gerepliceerde gegevens gebruikt, u tooset van een extra Standard-opslag account toostore replicatie moet Logboeken.

5. **Replicatie-instellingen instellen**. Volg [replicatie-instellingen instellen](../../site-recovery/vmware-walkthrough-overview.md) tooverify dat de configuratieserver is is gekoppeld aan Hallo replicatiebeleid dat u maakt.

6. **Capaciteitsplanning**. Gebruik Hallo [Capaciteitsplanner](../../site-recovery/site-recovery-capacity-planner.md) tooaccurately schatting netwerkbandbreedte, opslag en andere vereisten toomeet uw replicatie moet. Wanneer u bent klaar, selecteert u **Ja** in **hebt u capaciteitsplanning?**.

    ![][11]

7. Hallo volgende stappen kunt u **installeren van de mobility-service en -replicatie inschakelen**.

    7. U kunt ervoor kiezen te[push-installatie](../../site-recovery/vmware-walkthrough-overview.md) tooyour bronmachines of te[handmatig installeren van de mobility-service](../../site-recovery/site-recovery-vmware-to-azure-install-mob-svc.md) op uw virtuele bronmachines. U vindt Hallo vereiste van pushen installatie en het pad van de Hallo van handmatige installatieprogramma Hallo in Hallo koppeling. Als u een handmatige installatie uitvoert, moet u mogelijk een interne IP-adres toofind Hallo configuratieserver toouse.

    ![][12]

    Hallo failover VM heeft twee tijdelijke schijven: één van primaire virtuele machine en Hallo andere gemaakt tijdens het Hallo inrichten van virtuele machine in Hallo herstel regio Hallo. tooexclude hello tijdelijke schijf voordat de replicatie, installeer Hallo mobility-service voordat u replicatie inschakelt. toolearn meer informatie over hoe tooexclude tijdelijke schijf Hallo te verwijzen[schijven uitsluiten van replicatie](../../site-recovery/vmware-walkthrough-overview.md).

    7 ter. Schakel nu als volgt replicatie in:
      * Klik op **toepassing repliceren** > **bron**. Nadat u replicatie voor Hallo eerst hebt ingeschakeld, klik op + op Hallo kluis tooenable replicatie voor aanvullende machines repliceren.
      * In stap 1 voert instellen als uw processerver.
      * Geef in stap 2, Hallo na een failover-implementatiemodel, een toomigrate Premium storage-account voor een Standard-opslag account toosave logboeken en een virtueel netwerk toofail aan.
      * Voeg in stap 3, beveiligde virtuele machines met IP-adres (mogelijk moet u een interne IP-adres toofind ze).
      * In stap 4 Hallo eigenschappen te configureren door het Hallo-accounts die u eerder hebt ingesteld op de processerver Hallo selecteren.
      * Kies in stap 5 Hallo replicatiebeleid die u eerder hebt gemaakt, instellen van de replicatie-instellingen.
      Klik op **OK** en replicatie inschakelen.

    > [!NOTE]
    > Wanneer een Azure VM is de toewijzing ongedaan gemaakt en opnieuw hebt gestart, er is geen garantie dat u krijgt Hallo hetzelfde IP-adres. Als Hallo IP-adres van de server-proces configuratieserver Hallo of Hallo beveiligd wijziging van de Azure VM's, werken Hallo replicatie in dit scenario mogelijk niet correct.

    ![][13]

    Wanneer u uw Azure Storage-omgeving ontwerpt, wordt u aangeraden dat u afzonderlijke storage-accounts voor elke virtuele machine in een beschikbaarheidsset gebruiken. Het is raadzaam dat u de aanbevolen procedure in de opslaglaag Hallo Hallo te volgt[meerdere storage-accounts gebruiken voor elke beschikbaarheidsset](../../virtual-machines/windows/manage-availability.md). VM schijven toomultiple storage-accounts distribueren helpt tooimprove opslag beschikbaarheid en distribueert Hallo i/o over de infrastructuur van hello Azure-opslag. Als uw virtuele machines in een beschikbaarheidsset, in plaats van de schijven van alle virtuele machines repliceren naar één storage-account wordt ten zeerste aanbevolen meerdere keren voor meerdere virtuele machines migreren zodat Hallo virtuele machines in dezelfde Hallo beschikbaarheidsset één storage-account niet delen. Gebruik Hallo **replicatie inschakelen** blade tooset up opslagaccount voor elke virtuele machine, één voor één doel. U kunt een volgens tooyour moet na een failover-implementatiemodel. Als u Resource Manager (RM) als uw na een failover-implementatiemodel kiest, kunt u een VM RM tooan RM VM failover of kunt u een klassieke VM tooan RM VM failover.

8. **Een testfailover uitvoeren**. toocheck of de replicatie is voltooid, klikt u op het herstel van uw Site en klik vervolgens op **instellingen** > **gerepliceerde Items**. U ziet Hallo status en het percentage van het replicatieproces. Na de initiële replicatie is voltooid, voert Testfailover toovalidate uw replicatiestrategie voor. Voor gedetailleerde stappen van de testfailover Raadpleeg te[een testfailover uitvoeren in Site Recovery](../../site-recovery/vmware-walkthrough-overview.md). U kunt zien Hallo status van de testfailover in **instellingen** > **taken** > **YOUR_FAILOVER_PLAN_NAME**. Op de blade hello ziet u een uitsplitsing van Hallo stappen en geslaagde/mislukte resultaten. Als de testfailover Hallo mislukt, klikt u op Hallo stap toocheck Hallo foutbericht weergegeven. Zorg ervoor dat uw virtuele machines en replicatiestrategie voldoen aan Hallo vereisten voordat u een failover uitvoert. Lees [Testfailover tooAzure in Site Recovery](../../site-recovery/site-recovery-test-failover-to-azure.md) voor meer informatie en instructies van de testfailover.

9. **Een failover uitvoeren**. Nadat Hallo testfailover is voltooid, voer een failover-toomigrate uw schijven tooPremium opslag en repliceren Hallo VM-exemplaren. Volg Hallo gedetailleerde stappen in [een failover uitvoeren](../../site-recovery/site-recovery-failover.md#run-a-failover). Zorg ervoor dat u selecteert **virtuele machines afsluiten en het synchroniseren van de meest recente gegevens Hallo** toospecify dat Site Recovery moet tooshut omlaag Hallo beveiligde virtuele machines proberen en Hallo gegevens synchroniseren zodat hello meest recente versie van Hallo gegevens wordt failover. Als u deze optie niet selecteert of het Hallo-poging niet lukt worden Hallo failover van Hallo meest recente beschikbare herstelpunt voor Hallo VM. Site Recovery maakt een VM-exemplaar waarvan het type Hallo is gelijk aan of vergelijkbare tooa compatibel zijn met opslag VM voor Premium. U kunt Hallo prestaties en prijs van verschillende VM-exemplaren controleren door te gaan[prijzen van virtuele Machines in Windows](https://azure.microsoft.com/pricing/details/virtual-machines/windows/) of [prijzen van Linux virtuele Machines](https://azure.microsoft.com/pricing/details/virtual-machines/linux/).

## <a name="post-migration-steps"></a>Stappen na de migratie

1. **Configureren van de gerepliceerde virtuele machines toohello beschikbaarheidsset indien van toepassing**. Site Recovery biedt geen ondersteuning voor migratie VM's samen met de Hallo beschikbaarheidsset. Afhankelijk van Hallo-implementatie van de gerepliceerde virtuele machine, gaat u een van de volgende Hallo:
  * Voor een virtuele machine gemaakt met het klassieke implementatiemodel Hallo: Hallo VM toohello beschikbaarheidsset hello Azure-portal toevoegen. Voor gedetailleerde stappen gaat te[toevoegen van een bestaande beschikbaarheidsset voor de virtuele machine tooan](../../virtual-machines/windows/classic/configure-availability.md#addmachine).
  * Hallo Resource Manager-implementatiemodel: de configuratie van Hallo VM opslaan en vervolgens verwijderen en opnieuw maken Hallo virtuele machines in de beschikbaarheidsset Hallo. toodo hello script op voor het geval is, gebruiken [ingesteld Azure Resource Manager VM Beschikbaarheidsset](https://gallery.technet.microsoft.com/Set-Azure-Resource-Manager-f7509ec4). Controleer de Hallo beperking van dit script en uitvaltijd te plannen voordat het Hallo-script wordt uitgevoerd.

2. **Verwijderen van oude VM's en schijven**. Voordat u verwijdert deze, Controleer of Hallo Premium-schijven zijn consistent met de bron-schijven en nieuwe virtuele machines voeren dezelfde functie uitgevoerd als virtuele bronmachines Hallo HALLO hallo. Hallo implementatiemodel van Resource Manager (RM), verwijder Hallo VM en Hallo schijven verwijderen uit de bron-opslagaccounts in hello Azure-portal. In het klassieke implementatiemodel hello, kunt u Hallo VM en schijven in de klassieke portal Hallo of Azure-portal te verwijderen. Als er een probleem in welke Hallo schijf niet verwijderd ondanks dat u Hallo VM hebt verwijderd, raadpleegt u [fouten bij het verwijderen van VHD's oplossen](storage-resource-manager-cannot-delete-storage-account-container-vhd.md).

3. **Schone hello Azure Site Recovery-infrastructuur**. Wanneer u Site Recovery niet langer nodig hebt, kunt u de infrastructuur opschonen gerepliceerde items, Hallo configuratieserver en Hallo herstelbeleid verwijderd en wordt vervolgens hello Azure Site Recovery-kluis te verwijderen.

## <a name="troubleshooting"></a>Problemen oplossen

* [Controleren en problemen oplossen van beveiliging voor virtuele machines en fysieke servers](../../site-recovery/site-recovery-monitoring-and-troubleshooting.md)
* [Microsoft Azure Site Recovery-forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr)

## <a name="next-steps"></a>Volgende stappen

Zie Hallo resources voor specifieke scenario's voor het migreren van virtuele machines te volgen:

* [Azure virtuele Machines tussen Opslagaccounts migreren](https://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/)
* [Maken en uploaden van een Windows Server-VHD tooAzure.](../../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [Maakt en uploadt u een virtuele harde schijf met Hallo Linux-besturingssysteem](../../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Migreren van virtuele Machines van Amazon AWS tooMicrosoft Azure](http://channel9.msdn.com/Series/Migrating-Virtual-Machines-from-Amazon-AWS-to-Microsoft-Azure)

Zie ook Hallo resources toolearn meer informatie over Azure Storage en Azure Virtual Machines te volgen:

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
