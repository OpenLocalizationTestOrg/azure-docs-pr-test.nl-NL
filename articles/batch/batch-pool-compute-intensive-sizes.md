---
title: aaaUse rekenintensieve Azure VM's met Batch | Microsoft Docs
description: Hoe tootake profiteren van de RDMA-compatibele of GPU ingeschakeld VM in Azure Batch-pools groottes
services: batch
documentationcenter: 
author: dlepow
manager: timlt
editor: 
ms.assetid: 
ms.service: batch
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: danlep
ms.openlocfilehash: 6a462a5f2a44ddcec8bf4e5c200d444cac8fafe6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-rdma-capable-or-gpu-enabled-instances-in-batch-pools"></a>Gebruik van RDMA-compatibele of GPU ingeschakeld exemplaren in Batch-pools

toorun bepaalde taken Batch kunt u profiteren van Azure VM-formaten ontworpen voor grootschalige berekeningen tootake. Bijvoorbeeld: toorun meerdere exemplaren [MPI belastingen](batch-mpi.md), kunt u A8, A9, of H-serie-groottes met een netwerk interface voor Remote Direct Memory Access (RDMA). Deze formaten verbinding tooan InfiniBand-netwerk voor de communicatie tussen knooppunten, die MPI-toepassingen kan versnellen. Of voor CUDA toepassingen, kunt u N-serie grootten die NVIDIA Tesla afbeeldingen verwerken kaarten GPU (unit) bevatten.

Dit artikel bevat richtlijnen en voorbeelden toouse aantal gespecialiseerde grootten in Batch-pools van Azure. Zie voor technische specificaties en achtergrond:

* Hoge prestaties compute-VM-grootten ([Linux](../virtual-machines/linux/sizes-hpc.md), [Windows](../virtual-machines/windows/sizes-hpc.md)) 

* VM-grootten GPU-functionaliteit ([Linux](../virtual-machines/linux/sizes-gpu.md), [Windows](../virtual-machines/windows/sizes-gpu.md)) 


## <a name="subscription-and-account-limits"></a>Abonnement en limieten

* **Quota's** -een of meer Azure-quota, beperkt dat mogelijk Hallo getal of het type van knooppunten kunt u de Batch-pool tooa toevoegen. U bent waarschijnlijker toobe beperkt wanneer u RDMA-functionaliteit, GPU is ingeschakeld, of andere multicore VM-groottes. Afhankelijk van het type Hallo van Batch-account die u hebt gemaakt, kunnen de Hallo quota toohello account zelf of tooyour abonnement toepassen.

    * Als u uw Batch-account hebt gemaakt in Hallo **Batch-service** configuratie, u beperkt door Hallo [toegewezen kernen quotum per Batch-account](batch-quota-limit.md#resource-quotas). Standaard is dit quotum 20 kernen. Een afzonderlijke quotum van toepassing is te[prioriteit Laag VMs](batch-low-pri-vms.md), als u deze gebruikt. 

    * Als u Hallo-account hebt gemaakt in Hallo **gebruikerabonnement** configureren van uw abonnement beperkt het aantal kernen per regio VM Hallo. Zie [Azure-abonnement en Servicelimieten, quota's en beperkingen](../azure-subscription-service-limits.md). Uw abonnement geldt ook een regionale quotum toocertain VM-grootten, met inbegrip van HPC en GPU-exemplaren. In Hallo-Gebruikersconfiguratie abonnement gelden geen extra quota toohello Batch-account. 

  Mogelijk moet u tooincrease quota's voor een of meer wanneer u een speciale VM-grootte in Batch. toorequest een verhoging van het quotum, open een [online klant ondersteuningsaanvraag](../azure-supportability/how-to-create-azure-support-request.md) zonder kosten.

* **Beschikbaarheid in regio's** - rekenintensieve VM's mogelijk niet beschikbaar in Hallo regio's waar u uw Batch-accounts maken. toocheck dat een grootte is beschikbaar, Zie [producten die beschikbaar zijn in elke regio](https://azure.microsoft.com/regions/services/).


## <a name="dependencies"></a>Afhankelijkheden

Hallo RDMA en GPU-mogelijkheden van rekenintensieve grootten worden alleen ondersteund in bepaalde besturingssystemen. Afhankelijk van uw besturingssysteem mogelijk u moet tooinstall of extra stuurprogramma of andere software configureren. Hallo volgende tabellen geven een overzicht van deze afhankelijkheden. Zie gekoppelde artikelen voor meer informatie. Zie voor opties tooconfigure Batch-pools verderop in dit artikel.


### <a name="linux-pools---virtual-machine-configuration"></a>Groepen van Linux - Virtuele-machineconfiguratie

| Grootte | Mogelijkheid | Besturingssystemen | Vereiste software | Instellingen voor toepassingen |
| -------- | -------- | ----- |  -------- | ----- |
| [H16r, H16mr, A8, A9](../virtual-machines/linux/sizes-hpc.md#rdma-capable-instances) | RDMA | SUSE Linux Enterprise Server 12 HPC of<br/>Op basis van centOS HPC<br/>(Azure Marketplace) | Intel MPI 5 | Communicatie tussen knooppunten inschakelen, uitschakelen van de uitvoering van gelijktijdige taken |
| [NC reeks *](../virtual-machines/linux/n-series-driver-setup.md#install-cuda-drivers-for-nc-vms) | NVIDIA Tesla R80 GPU | Ubuntu 16.04 TNS.<br/>Red Hat Enterprise Linux 7.3, of<br/>7.3 op basis van CentOS<br/>(Azure Marketplace) | NVIDIA CUDA Toolkit 8.0 stuurprogramma 's | N.v.t. | 
| [NV reeks](../virtual-machines/linux/n-series-driver-setup.md#install-grid-drivers-for-nv-vms) | NVIDIA Tesla M60 GPU | Ubuntu 16.04 LTS<br/>Red Hat Enterprise Linux 7.3<br/>7.3 op basis van CentOS<br/>(Azure Marketplace) | NVIDIA RASTER 4.3 stuurprogramma 's | N.v.t. |

* RDMA-connectiviteit op NC24r VM's wordt op 7.3 HPC met Intel MPI op basis van CentOS ondersteund.



### <a name="windows-pools---virtual-machine-configuration"></a>Windows-groepen - configuratie van virtuele machine

| Grootte | Mogelijkheid | Besturingssystemen | Vereiste software | Instellingen voor toepassingen |
| -------- | ------ | -------- | -------- | ----- |
| [H16r, H16mr, A8, A9](../virtual-machines/windows/sizes-hpc.md#rdma-capable-instances) | RDMA | Windows Server 2012 R2 of<br/>WindowsServer 2012 (Azure Marketplace) | Microsoft MPI 2012 R2 of hoger, of<br/> Intel MPI 5<br/><br/>HpcVMDrivers Azure VM-extensie | Communicatie tussen knooppunten inschakelen, uitschakelen van de uitvoering van gelijktijdige taken |
| [NC reeks *](../virtual-machines/windows/n-series-driver-setup.md) | NVIDIA Tesla R80 GPU | WindowsServer 2016 of <br/>Windows Server 2012 R2 (Azure Marketplace) | NVIDIA Tesla stuurprogramma's of CUDA Toolkit 8.0 's| N.v.t. | 
| [NV reeks](../virtual-machines/windows/n-series-driver-setup.md) | NVIDIA Tesla M60 GPU | WindowsServer 2016 of<br/>Windows Server 2012 R2 (Azure Marketplace) | NVIDIA RASTER 4.3 stuurprogramma 's | N.v.t. |

* RDMA-connectiviteit op NC24r VM's wordt ondersteund op Windows Server 2012 R2 met de extensie HpcVMDrivers en Microsoft MPI of Intel MPI.

### <a name="windows-pools---cloud-services-configuration"></a>Windows-groepen - configuratie voor Cloud-services

> [!NOTE]
> N-serie grootten worden niet ondersteund in de Batch-pools met Hallo cloud services-configuratie.
>

| Grootte | Mogelijkheid | Besturingssystemen | Vereiste software | Instellingen voor toepassingen |
| -------- | ------- | -------- | -------- | ----- |
| [H16r, H16mr, A8, A9](../virtual-machines/windows/sizes-hpc.md#rdma-capable-instances) | RDMA | Windows Server 2012 R2<br/>WindowsServer 2012 of<br/>Windows Server 2008 R2 (Gast OS-familie) | Microsoft MPI 2012 R2 of hoger, of<br/>Intel MPI 5<br/><br/>HpcVMDrivers Azure VM-extensie | Communicatie tussen knooppunten, inschakelen<br/> uitvoering van gelijktijdige taken uitschakelen |





## <a name="pool-configuration-options"></a>Groep configuratie-opties

tooconfigure een gespecialiseerde VM-grootte voor uw Batch-pool, Hallo Batch-API's en hulpprogramma's bieden verschillende opties tooinstall vereist software of stuurprogramma's, waaronder:

* [Begintaak](batch-api-basics.md#start-task) -een installatiepakket voor uploaden als een resource bestand tooan Azure storage-account in Hallo dezelfde regio bevinden als Hallo Batch-account. Maken een starten vanaf de opdrachtregel tooinstall Hallo bronbestand achtergrond wanneer Hallo van toepassingen wordt gestart. Zie voor meer informatie, Hallo [REST API-documentatie](/rest/api/batchservice/add-a-pool-to-an-account#bk_starttask).

  > [!NOTE] 
  > Hallo begintaak moet worden uitgevoerd met verhoogde bevoegdheden (admin) machtigingen en het voor een correcte werking moet wachten.
  >

* [Toepassingspakket](batch-application-packages.md) - een installatie van het gecomprimeerde pakket tooyour Batch-account toevoegen en configureren van een pakket-verwijzing in Hallo van toepassingen. Deze instelling wordt geüpload en Hallo-pakket op alle knooppunten in de groep hello wordt uitgepakt. Als Hallo-pakket een installatieprogramma is, maakt u een app Hallo van start taak opdrachtregel toosilently installeren op alle knooppunten van de groep van toepassingen. Eventueel hello-pakketten installeren wanneer een taak geplande toorun op een knooppunt is.

* [Afbeelding van aangepaste toepassingen](batch-api-basics.md#pool) - maken van een aangepaste Windows of Linux-VM-installatiekopie met stuurprogramma's, software of andere instellingen die vereist zijn voor Hallo VM-grootte. Als u uw Batch-account hebt gemaakt in de Gebruikersconfiguratie abonnement hello, geef de aangepaste installatiekopie Hallo voor uw Batch-pool. (Aangepaste installatiekopieën worden niet ondersteund in de configuratie van de service Batch Hallo-accounts.) Aangepaste installatiekopieën kunnen alleen worden gebruikt met toepassingen die in de configuratie van de virtuele machine Hallo.

  > [!IMPORTANT]
  > U niet in Batch-pools momenteel een aangepaste installatiekopie gemaakt met beheerde schijven of met Premium-opslag gebruiken.
  >



* [Batch-scheepswerf](https://github.com/Azure/batch-shipyard) configureert Hallo GPU en RDMA toowork automatisch transparant met beperkte workloads in Azure Batch. Batch scheepswerf wordt volledig aangedreven met configuratiebestanden. Er zijn veel voorbeeld recept configuraties beschikbaar waarmee GPU en RDMA werkbelastingen zoals Hallo [CNTK GPU recept](https://github.com/Azure/batch-shipyard/tree/master/recipes/CNTK-GPU-OpenMPI) die configureert vooraf GPU-stuurprogramma's op virtuele machines N-reeks en cognitieve Toolkit voor Microsoft-software als een Docker-installatiekopie wordt geladen.


## <a name="example-microsoft-mpi-on-an-a8-vm-pool"></a>Voorbeeld: Microsoft MPI op een groep A8-VM

toorun Windows MPI-toepassingen op een pool van Azure A8 knooppunten, moet u tooinstall ondersteunde MPI-implementatie. Hier vindt u voorbeeld stappen tooinstall [Microsoft MPI](https://msdn.microsoft.com/library/bb524831(v=vs.85).aspx) op een Windows-groep met behulp van een Batch-toepassingspakket.

1. Hallo downloaden [installatiepakket](http://go.microsoft.com/FWLink/p/?LinkID=389556) (MSMpiSetup.exe) voor de meest recente versie van Microsoft MPI Hallo.
2. Maak een zip-bestand van het Hallo-pakket.
3. Hallo pakket tooyour Batch-account uploaden. Zie voor stappen Hallo [toepassingspakketten](batch-application-packages.md) richtlijnen. Geef een toepassings-id zoals *MSMPI*, en een versie zoals *8.1*. 
4. Maak een groep met Hallo Batch-API's of Azure-portal in Hallo cloud services-configuratie met Hallo gewenst aantal knooppunten en de schaal. Hallo volgende tabel toont voorbeeld instellingen tooset up MPI in met behulp van een begintaak zonder toezicht:

| Instelling | Waarde |
| ---- | ----- | 
| **Type installatiekopie** | Cloudservices |
| **OS-familie** | Windows Server 2012 R2 (OS-familie 4) |
| **De grootte van knooppunt** | A8-standaard |
| **De communicatie tussen knooppunten is ingeschakeld** | True |
| **Maximum aantal taken per knooppunt** | 1 |
| **Verwijzingen naar Application-pakket** | MSMPI |
| **Begintaak ingeschakeld** | True<br>**Vanaf de opdrachtregel** - `"cmd /c %AZ_BATCH_APP_PACKAGE_MSMPI#8.1%\\MSMpiSetup.exe -unattend -force"`<br/>**Gebruikersidentiteit** -Pool autouser, admin<br/>**Wacht tot succes** : True

## <a name="example-nvidia-tesla-drivers-on-nc-vm-pool"></a>Voorbeeld: NVIDIA Tesla stuurprogramma's op de NC-VM-groep

toorun CUDA toepassingen op een pool van Linux NC-knooppunten, moet u tooinstall CUDA Toolkit 8.0 op Hallo knooppunten. Hallo Toolkit Hallo nodig NVIDIA Tesla GPU-stuurprogramma's geïnstalleerd. Hier volgt een voorbeeld stappen toodeploy een aangepaste installatiekopie Ubuntu 16.04 TNS Hallo GPU-stuurprogramma's:

1. Implementeer een Azure-NC6 VM Ubuntu 16.04 TNS uitgevoerd. Bijvoorbeeld Hallo VM maken in Hallo ons Zuid-centraal regio. Zorg ervoor dat u Hallo VM met de standard-opslag maakt en *zonder* schijven die worden beheerd.
2. Ga als volgt Hallo stappen tooconnect toohello VM en [CUDA stuurprogramma's installeren](../virtual-machines/linux/n-series-driver-setup.md#install-cuda-drivers-for-nc-vms).
3. Inrichting ervan ongedaan Hallo Linux-agent en vervolgens vastleggen Linux VM-installatiekopie hello Azure CLI 1.0-opdrachten gebruiken. Zie voor stappen [vastleggen van een virtuele Linux-machine uitgevoerd op Azure](../virtual-machines/linux/capture-image-nodejs.md). Noteer Hallo installatiekopie URI.
  > [!IMPORTANT]
  > Gebruik geen Azure CLI 2.0 opdrachten toocapture Hallo afbeelding voor Azure Batch. Hallo 2.0 CLI-opdrachten vastleggen op dit moment alleen virtuele machines die zijn gemaakt met behulp van beheerde schijven.
  >
4. Een Batch-account maken met Hallo abonnement Gebruikersconfiguratie in een regio die ondersteuning biedt voor NC virtuele machines.
5. Hallo Batch-API's of Azure-portal, met een pool maken met de aangepaste installatiekopie Hallo en Hello gewenst aantal knooppunten en de schaal. Hallo volgende tabel ziet u voorbeelden van groepsinstellingen voor de installatiekopie van het Hallo:

| Instelling | Waarde |
| ---- | ---- |
| **Type installatiekopie** | Aangepaste installatiekopie |
| **Aangepaste installatiekopie** | Afbeelding URI van Hallo formulier`https://yourstorageaccountdisks.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd` |
| **Knooppunt agent SKU** | batch.node.Ubuntu 16.04 |
| **De grootte van knooppunt** | Standard NC6 |



## <a name="next-steps"></a>Volgende stappen

* toorun MPI-taken op een Azure Batch-toepassingen, Zie Hallo [Windows](batch-mpi.md) of [Linux](https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/) voorbeelden.

* Zie voor voorbeelden van GPU werkbelastingen op Batch Hallo [Batch scheepswerf](https://github.com/Azure/batch-shipyard/) recepten.
