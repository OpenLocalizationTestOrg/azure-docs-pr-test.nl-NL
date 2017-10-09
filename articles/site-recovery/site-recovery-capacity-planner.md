---
title: capaciteit van de aaaEstimate replicatie in Azure | Microsoft Docs
description: De capaciteit van dit artikel tooestimate gebruiken bij het repliceren met Azure Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 0a1cd8eb-a8f7-4228-ab84-9449e0b2887b
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: nisoneji
ms.openlocfilehash: 54d10e50dd4fc1b875273c7fc0f38f0e85dadddc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="plan-capacity-for-protecting-virtual-machines-and-physical-servers-in-azure-site-recovery"></a>Plannen van capaciteit voor het beveiligen van virtuele machines en fysieke servers in de Azure Site Recovery

Hello Azure Site Recovery Capacity Planner hulpprogramma kunt u toofigure uit uw capaciteitsvereisten bij het repliceren van Hyper-V-machines, virtuele VMware-machines en fysieke servers met Windows of Linux, met Azure Site Recovery.

Hallo Site Recovery Capacity Planner tooanalyze gebruiken uw bronomgeving en werkbelastingen, schat u bandbreedte behoeften en serverbronnen die u nodig hebt voor de bronlocatie Hallo en Hallo resources (virtuele machines en opslag, enzovoort), die u nodig hebt in Hallo-doel locatie.

U kunt Hallo hulpprogramma uitvoeren in een aantal modi:

* **Snelle planning**: Hallo hulpprogramma uitvoeren in deze modus tooget netwerk- en projecties op basis van een gemiddelde aantal virtuele machines, schijven, opslag en wijzigingssnelheid.
* **Gedetailleerde planning**: Hallo hulpprogramma uitvoeren in deze modus en Geef details op van elke werkbelasting op het niveau van de virtuele machine. VM-compatibiliteit analyseren en netwerk- en projecties ophalen.

## <a name="before-you-start"></a>Voordat u begint


1. Gegevens verzamelen over uw omgeving, inclusief virtuele machines, schijven per virtuele machine, opslag per schijf.
2. De snelheid van uw dagelijkse wijzigen (verloop) voor gerepliceerde gegevens identificeren. toodo dit:

   * Als u Hyper-V-machines repliceert, downloadt u Hallo [Hyper-V-hulpprogramma voor capaciteitsplanning](https://www.microsoft.com/download/details.aspx?id=39057) tooget Hallo wijzigingssnelheid. [Meer informatie](site-recovery-capacity-planning-for-hyper-v-replication.md) over dit hulpprogramma. U wordt aangeraden dat u gemiddelden dit hulpprogramma via een week toocapture uitvoeren.
   * Als u virtuele VMware-machines repliceert, gebruikt u Hallo [Azure Site Recovery implementatie Planner](./site-recovery-deployment-planner.md) toofigure uit Hallo verloop snelheid.
   * Als u fysieke servers repliceert, moet u tooestimate handmatig.

## <a name="run-hello-quick-planner"></a>Hallo snelle Planner uitvoeren
1. Download en open Hallo [Azure Site Recovery Capacity Planner](http://aka.ms/asr-capacity-planner-excel) hulpprogramma. U moet toorun macro's, dus selecteer tooenable bewerken en inschakelen wanneer u wordt gevraagd.
2. In **Selecteer een type planner** Selecteer **snelle Planner** van Hallo keuzelijst met invoervak.

   ![Aan de slag](./media/site-recovery-capacity-planner/getting-started.png)
3. In Hallo **Capacity Planner** werkblad, Geef informatie op Hallo vereist. U moet alle Hallo velden omcirkeld in rood in onderstaande schermafbeelding voor Hallo invullen.

   * In **selecteert u uw scenario**, kies **Hyper-V tooAzure** of **VMware of fysieke tooAzure**.
   * In **gemiddelde dagelijkse gegevens snelheid (%) wijzigen**, plaatsen in Hallo informatie u verzamelen met behulp van Hallo [Hyper-V-hulpprogramma voor capaciteitsplanning](site-recovery-capacity-planning-for-hyper-v-replication.md) of Hallo [Azure Site Recovery implementatie Planner](./site-recovery-deployment-planner.md).  
   * **Compressie** toocompression aangeboden bij het repliceren van VMware-machines of fysieke servers tooAzure is alleen van toepassing. We verwachten 30% of meer, maar u kunt de instelling Hallo zo nodig wijzigen. U kunt een toestel van derden zoals Riverbed gebruiken voor het repliceren van Hyper-V-machines tooAzure compressie.
   * In **bewaren invoer**, opgeven hoe lang de replica's moeten worden bewaard. Als u VMware of fysieke servers repliceert, invoerwaarde Hallo in dagen. Als u Hyper-V repliceert, geeft u Hallo tijd in uren.
   * In **aantal uren in waarop de initiële replicatie voor virtuele machines Hallo batch moet worden voltooid** en **aantal virtuele machines per batch van de initiële replicatie**, invoer van instellingen die worden gebruikt vereisten voor toocompute initiële replicatie.  Wanneer Site Recovery wordt geïmplementeerd, moet Hallo die initiële volledige gegevensset worden geüpload.

   ![Invoer](./media/site-recovery-capacity-planner/inputs.png)
4. Nadat u waarden voor de bronomgeving Hallo Hallo hebt geplaatst, bevat de uitvoer weergegeven:

   * **Bandbreedte vereist is voor replicatie van verschillen** (MB/sec). Netwerkbandbreedte voor replicatie van verschillen wordt berekend op Hallo gemiddelde dagelijkse gegevenswijzigingssnelheid.
   * **Bandbreedte die is vereist voor de initiële replicatie** (MB/sec). Netwerkbandbreedte voor de initiële replicatie wordt berekend op Hallo initiële replicatie waarden die u in plaatsen.
   * **Opslag vereist (in GB's)** Hallo totale Azure-opslag vereist is.
   * **Totaal aantal IOPS op standaard storage-accounts** wordt berekend op basis van de grootte van 8 kB IOPS op Hallo totale standaard storage-accounts.  Voor Hallo snelle Planner, wordt Hallo nummer berekend op basis van alle Hallo bron VMs schijven en dagelijks gegevenswijzigingssnelheid. Hallo voor gedetailleerde Planner, Hallo nummer is berekend op basis van totaal aantal virtuele machines die toegewezen toostandard Azure VM's zijn en gegevens wijzigen op deze virtuele machines.
   * **Aantal accounts standaardopslag** biedt totaal aantal standaardopslag accounts nodig tooprotect Hallo Hallo VM's. Een standard-opslagaccount kan bevatten up too20000 IOP's over alle Hallo VM's in een standard-opslag en maximaal 500 IOP's per schijf wordt ondersteund.
   * **Het aantal blob-schijven die zijn vereist** biedt Hallo aantal schijven dat wordt gemaakt op Azure-opslag.
   * **Aantal premium storage-accounts vereist** biedt totaal aantal premium storage-accounts nodig tooprotect Hallo Hallo VM's. Een bron-VM met een hoge IOPS (groter dan 20000) moet een premium storage-account. Een premium storage-account kan up too80000 IOP's bevatten.
   * **Totaal aantal IOPS op premium-opslag** wordt berekend op basis van de grootte van 256 kB IOPS op Hallo totale premium storage-accounts.  Voor Hallo snelle Planner, wordt Hallo nummer berekend op basis van alle Hallo bron VMs schijven en dagelijks gegevenswijzigingssnelheid. Hallo voor gedetailleerde Planner, Hallo nummer is berekend op basis van Hallo kunt u het totale aantal virtuele machines die toegewezen toopremium virtuele machine van Azure (Active Directory en GS-serie zijn) en Hallo gegevens wijzigen tarief op deze virtuele machines.
   * **Aantal vereiste configuratieservers** geeft aan hoeveel configuratieservers vereist voor de implementatie van Hallo.
   * **Aantal vereiste aanvullende processen servers** geeft aan of extra processervers vereist zijn, in aanvulling toohello processerver die wordt uitgevoerd op de configuratieserver Hallo standaard.
   * **Extra opslagruimte op de bron Hallo 100%** toont of extra opslagruimte op de bronlocatie Hallo vereist is.

   ![Uitvoer](./media/site-recovery-capacity-planner/output.png)

## <a name="run-hello-detailed-planner"></a>Voer Hallo gedetailleerde Planner

1. Download en open Hallo [Azure Site Recovery Capacity Planner](http://aka.ms/asr-capacity-planner-excel) hulpprogramma. U moet toorun macro's, dus selecteer tooenable bewerken en inschakelen wanneer u wordt gevraagd.
2. In **Selecteer een type planner**, selecteer **gedetailleerde Planner** van Hallo keuzelijst met invoervak.

   ![Aan de slag](./media/site-recovery-capacity-planner/getting-started-2.png)
3. In Hallo **werkbelasting kwalificatie** werkblad, Geef informatie op Hallo vereist. U moet alle Hallo gemarkeerd velden invullen.

   * In **Processor-cores**, Hallo totaal aantal kernen op een bronserver opgeven.
   * In **toewijzing van geheugen in MB**, Hallo RAM grootte van een bronserver opgeven.
   * Hallo **nummer van de NIC's**, Hallo aantal netwerkadapters op een bronserver opgeven.
   * In **totale opslag (in GB)**, totale grootte van de VM-opslag Hallo Hallo opgeven. Bijvoorbeeld, als de bronserver Hallo 3 schijven met 500 GB, is grootte van de totale opslagruimte 1500 GB.
   * In **aantal gekoppelde schijven**, Hallo kunt u het totale aantal schijven van een bronserver opgeven.
   * In **schijf gebruik van capaciteit**, Hallo Gemiddeld gebruik opgeven.
   * In **dagelijks snelheid (%) wijzigen**, geef Hallo dagelijkse gegevens frequentie van een bronserver wijzigen.
   * In **toewijzing Azure grootte**, hello Azure VM-grootte die u wilt dat toomap invoeren. Als u niet toodo dit handmatig wilt, klikt u op **Compute IaaS VM's**. Als u een handmatige instelling invoer en klik vervolgens op Compute IaaS VM's, kan Hallo handmatige instelling worden overschreven omdat de Hallo compute proces identificeert automatisch de beste overeenkomst Hallo op Azure VM-grootte.

   ![Kwalificatie werkbelasting](./media/site-recovery-capacity-planner/workload-qualification.png)
4. Als u op **Compute IaaS VM's** Hier ziet u hoe het werkt:

   * Hallo verplichte invoer valideert.
   * IOPS berekend en wordt voorgesteld Hallo beste Azure VM aize overeenkomst voor elke virtuele machines die in aanmerking komen voor replicatie tooAzure. Als een correcte grootte van virtuele machine van Azure kan worden gedetecteerd met dat een fout is uitgegeven. Bijvoorbeeld, als de Hallo aantal schijven gekoppeld 65, een fout gegenereerd omdat Hallo hoogste Azure VM 64 is.
   * Stelt een opslagaccount die kan worden gebruikt voor een virtuele machine in Azure.
   * Hallo totale aantal standaard storage-accounts en premium-opslagaccounts die zijn vereist voor de werkbelasting van Hallo berekent. Schuif naar beneden tooview hello Azure opslagtype en Hallo storage-account die kan worden gebruikt voor een bronserver.
   * Is voltooid en sorteert deze rest Hallo van Hallo tabel op basis van het vereiste opslagtype (standard of premium) voor een virtuele machine en het aantal gekoppelde schijven Hallo toegewezen. Voor alle virtuele machines die voldoen aan vereisten voor Azure hello, Hallo kolom **Is VM gekwalificeerd?** toont **Ja**. Als een virtuele machine kan niet worden back-up tooAzure, wordt er een fout weergegeven.

Kolommen AA tooAE worden uitgevoerd en informatie te verstrekken voor elke virtuele machine.

![Kwalificatie werkbelasting](./media/site-recovery-capacity-planner/workload-qualification-2.png)

### <a name="example"></a>Voorbeeld
Als u bijvoorbeeld voor zes VM's met Hallo waarden uit de tabel hello, Hallo hulpprogramma berekend en hello Azure VM relevantie en hello Azure opslagvereisten moet worden toegewezen.

![Kwalificatie werkbelasting](./media/site-recovery-capacity-planner/workload-qualification-3.png)

* Let op Hallo volgende in Hallo voorbeeld van uitvoer:

  * de eerste kolom Hallo is een kolom validatie voor Hallo virtuele machines, schijven en verloop.
  * Twee standaard storage-accounts en een premium-opslagaccount nodig zijn voor vijf virtuele machines.
  * VM3 niet in aanmerking voor beveiliging, omdat een of meer schijven meer dan 1 TB zijn.
  * VM1 en VM2 kunt Hallo eerste standard-opslagaccount gebruiken
  * VM4 kunt hello tweede standard-opslagaccount gebruiken.
  * VM5 en VM6 een premium-opslagaccount nodig en kunnen beide één account gebruiken.

    > [!NOTE]
    > IOPS op standard en premium storage worden berekend op Hallo VM-niveau en niet op het niveau van de schijf. Een standaard virtuele machine kan verwerken van too500 IOP's per schijf. Als IOPS aan voor een schijf groter dan 500 zijn, moet u premium-opslag. Echter, als IOPS aan voor een schijf meer dan 500 zijn, maar IOPS voor Hallo totale VM-schijven binnen Hallo zijn ondersteunen standaard Azure VM limieten (VM-grootte, het aantal schijven, het aantal adapters, CPU, geheugen), vervolgens Hallo planner hervat een standaard virtuele machine en niet Hallo DS of GS reeksen. U moet toomanually update Hallo toewijzing Azure grootte cel met de juiste DS- of GS-serie VM.


Nadat alle Hallo-details gemaakt zijn, klikt u op **verzenden gegevens toohello planner hulpprogramma** tooopen hello **Capacity Planner** werkbelastingen zijn gemarkeerd, tooshow of ze in aanmerking komen voor beveiliging zijn of niet.

### <a name="submit-data-in-hello-capacity-planner"></a>Verzenden van gegevens in Hallo Capacity Planner
1. Wanneer u Hallo opent **Capacity Planner** werkblad dit ingevuld op basis van Hallo-instellingen die u hebt opgegeven. word 'Werkbelasting' wordt weergegeven in Hallo Hallo **Infra invoer bron** cel, tooshow die invoer Hallo Hallo is **werkbelasting kwalificatie** werkblad.
2. Als u toomake wijzigingen wilt, moet u toomodify hello **werkbelasting kwalificatie** werkblad en klik op **verzenden gegevens toohello planner hulpprogramma** opnieuw.  

   ![Capaciteit Planner](./media/site-recovery-capacity-planner/capacity-planner.png)
