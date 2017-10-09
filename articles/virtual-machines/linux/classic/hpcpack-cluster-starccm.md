---
title: aaaRun STER-CCM + met HPC Pack op de virtuele Linux-machines | Microsoft Docs
description: Een Microsoft HPC Pack cluster in Azure implementeren en uitvoeren van een STER-taak CCM + op meerdere Linux-rekenknooppunten via een netwerk RDMA.
services: virtual-machines-linux
documentationcenter: 
author: xpillons
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: 75523406-d268-4623-ac3e-811c7b74de4b
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 09/13/2016
ms.author: xpillons
ms.openlocfilehash: 8265013cb295f53d6d4354ab2f100ef20d9f4c8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="run-star-ccm-with-microsoft-hpc-pack-on-a-linux-rdma-cluster-in-azure"></a><span data-ttu-id="b2634-103">Uitvoeren van de STER-CCM + met Microsoft HPC Pack op een Linux RDMA-cluster in Azure</span><span class="sxs-lookup"><span data-stu-id="b2634-103">Run STAR-CCM+ with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>
<span data-ttu-id="b2634-104">Dit artikel laat zien hoe een Microsoft HPC Pack toodeploy cluster op Azure en voer een [CD adapco STER-CCM +](http://www.cd-adapco.com/products/star-ccm%C2%AE) taak op meerdere Linux-rekenknooppunten die met elkaar door middel van InfiniBand verbonden zijn.</span><span class="sxs-lookup"><span data-stu-id="b2634-104">This article shows you how toodeploy a Microsoft HPC Pack cluster on Azure and run a [CD-adapco STAR-CCM+](http://www.cd-adapco.com/products/star-ccm%C2%AE) job on multiple Linux compute nodes that are interconnected with InfiniBand.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="b2634-105">Microsoft HPC Pack biedt functies toorun tal van grootschalige HPC en parallelle toepassingen, waaronder MPI-toepassingen op clusters van Microsoft Azure virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="b2634-105">Microsoft HPC Pack provides features toorun a variety of large-scale HPC and parallel applications, including MPI applications, on clusters of Microsoft Azure virtual machines.</span></span> <span data-ttu-id="b2634-106">HPC Pack ondersteunt ook waarop Linux HPC-toepassingen op Linux-rekenknooppunt virtuele machines die zijn geïmplementeerd in een cluster HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="b2634-106">HPC Pack also supports running Linux HPC applications on Linux compute-node VMs that are deployed in an HPC Pack cluster.</span></span> <span data-ttu-id="b2634-107">Zie voor een inleiding toousing Linux-rekenknooppunten met HPC Pack, [aan de slag met Linux-rekenknooppunten in een cluster HPC Pack Azure](hpcpack-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="b2634-107">For an introduction toousing Linux compute nodes with HPC Pack, see [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md).</span></span>

## <a name="set-up-an-hpc-pack-cluster"></a><span data-ttu-id="b2634-108">Een cluster HPC Pack instellen</span><span class="sxs-lookup"><span data-stu-id="b2634-108">Set up an HPC Pack cluster</span></span>
<span data-ttu-id="b2634-109">Hallo HPC Pack IaaS implementatiescripts downloaden van Hallo [Downloadcentrum](https://www.microsoft.com/en-us/download/details.aspx?id=44949) en pak ze lokaal.</span><span class="sxs-lookup"><span data-stu-id="b2634-109">Download hello HPC Pack IaaS deployment scripts from hello [Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=44949) and extract them locally.</span></span>

<span data-ttu-id="b2634-110">Azure PowerShell is een vereiste.</span><span class="sxs-lookup"><span data-stu-id="b2634-110">Azure PowerShell is a prerequisite.</span></span> <span data-ttu-id="b2634-111">PowerShell is niet geconfigureerd op uw lokale computer, lees dan Hallo artikel [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b2634-111">If PowerShell is not configured on your local machine, please read hello article [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="b2634-112">Op moment van schrijven van dit Hallo zijn Hallo Linux installatiekopieën van hello Azure Marketplace (met daarin Hallo InfiniBand-stuurprogramma's voor Azure) voor SLES 12, CentOS 6.5 en CentOS 7.1.</span><span class="sxs-lookup"><span data-stu-id="b2634-112">At hello time of this writing, hello Linux images from hello Azure Marketplace (which contains hello InfiniBand drivers for Azure) are for SLES 12, CentOS 6.5, and CentOS 7.1.</span></span> <span data-ttu-id="b2634-113">In dit artikel is gebaseerd op Hallo gebruik van SLES 12.</span><span class="sxs-lookup"><span data-stu-id="b2634-113">This article is based on hello usage of SLES 12.</span></span> <span data-ttu-id="b2634-114">naam van de tooretrieve Hallo van alle Linux-installatiekopieën die ondersteuning bieden voor HPC in Hallo Marketplace, kunt u Hallo volgende PowerShell-opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="b2634-114">tooretrieve hello name of all Linux images that support HPC in hello Marketplace, you can run hello following PowerShell command:</span></span>

```
    get-azurevmimage | ?{$_.ImageName.Contains("hpc") -and $_.OS -eq "Linux" }
```

<span data-ttu-id="b2634-115">Hallo-uitvoer geeft een lijst van Hallo locatie waarin deze installatiekopieën beschikbaar zijn en Hallo installatiekopie met de naam (**ImageName**) toobe in implementatiesjabloon hello later gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b2634-115">hello output lists hello location in which these images are available and hello image name (**ImageName**) toobe used in hello deployment template later.</span></span>

<span data-ttu-id="b2634-116">Voordat u Hallo cluster implementeert, hebt u toobuild een sjabloonbestand HPC Pack-implementatie.</span><span class="sxs-lookup"><span data-stu-id="b2634-116">Before you deploy hello cluster, you have toobuild an HPC Pack deployment template file.</span></span> <span data-ttu-id="b2634-117">Omdat we een klein cluster ontwikkelt je, wordt de Hallo hoofdknooppunt Hallo-domeincontroller en de host een lokale SQL-database.</span><span class="sxs-lookup"><span data-stu-id="b2634-117">Because we're targeting a small cluster, hello head node will be hello domain controller and host a local SQL database.</span></span>

<span data-ttu-id="b2634-118">Hallo volgende sjabloon een hoofdknooppunt implementeren, maakt u een XML-bestand met de naam **MyCluster.xml**, en vervang de waarden Hallo van **SubscriptionId**, **StorageAccount**,  **Locatie**, **VMName**, en **ServiceName** met jouw e-mailadres.</span><span class="sxs-lookup"><span data-stu-id="b2634-118">hello following template will deploy such a head node, create an XML file named **MyCluster.xml**, and replace hello values of **SubscriptionId**, **StorageAccount**, **Location**, **VMName**, and **ServiceName** with yours.</span></span>

    <?xml version="1.0" encoding="utf-8" ?>
    <IaaSClusterConfig>
      <Subscription>
        <SubscriptionId>99999999-9999-9999-9999-999999999999</SubscriptionId>
        <StorageAccount>mystorageaccount</StorageAccount>
      </Subscription>
      <Location>North Europe</Location>
      <VNet>
        <VNetName>hpcvnetne</VNetName>
        <SubnetName>subnet-hpc</SubnetName>
      </VNet>
      <Domain>
        <DCOption>HeadNodeAsDC</DCOption>
        <DomainFQDN>hpc.local</DomainFQDN>
      </Domain>
      <Database>
        <DBOption>LocalDB</DBOption>
      </Database>
      <HeadNode>
        <VMName>myhpchn</VMName>
        <ServiceName>myhpchn</ServiceName>
        <VMSize>Standard_D4</VMSize>
      </HeadNode>
      <LinuxComputeNodes>
        <VMNamePattern>lnxcn-%0001%</VMNamePattern>
        <ServiceNamePattern>mylnxcn%01%</ServiceNamePattern>
        <MaxNodeCountPerService>20</MaxNodeCountPerService>
        <StorageAccountNamePattern>mylnxstorage%01%</StorageAccountNamePattern>
        <VMSize>A9</VMSize>
        <NodeCount>0</NodeCount>
        <ImageName>b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-hpc-v20150708</ImageName>
      </LinuxComputeNodes>
    </IaaSClusterConfig>

<span data-ttu-id="b2634-119">Start Hallo-hoofdknooppunt maken door het Hallo PowerShell-opdracht uitvoeren in een opdrachtprompt met verhoogde bevoegdheid:</span><span class="sxs-lookup"><span data-stu-id="b2634-119">Start hello head-node creation by running hello PowerShell command in an elevated command prompt:</span></span>

```
    .\New-HPCIaaSCluster.ps1 -ConfigFile MyCluster.xml
```

<span data-ttu-id="b2634-120">Na 20 minuten too30 Hallo hoofdknooppunt moet gereed.</span><span class="sxs-lookup"><span data-stu-id="b2634-120">After 20 too30 minutes, hello head node should be ready.</span></span> <span data-ttu-id="b2634-121">U kunt tooit verbinden van hello Azure-portal door te klikken op Hallo **Connect** pictogram van Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="b2634-121">You can connect tooit from hello Azure portal by clicking hello **Connect** icon of hello virtual machine.</span></span>

<span data-ttu-id="b2634-122">U hebt mogelijk uiteindelijk toofix Hallo DNS-doorstuurserver.</span><span class="sxs-lookup"><span data-stu-id="b2634-122">You might eventually have toofix hello DNS forwarder.</span></span> <span data-ttu-id="b2634-123">toodo starten, DNS-beheer.</span><span class="sxs-lookup"><span data-stu-id="b2634-123">toodo so, start DNS Manager.</span></span>

1. <span data-ttu-id="b2634-124">Klik met de rechtermuisknop Hallo-servernaam in DNS-beheer, selecteer **eigenschappen**, en klik vervolgens op Hallo **doorstuurservers** tabblad.</span><span class="sxs-lookup"><span data-stu-id="b2634-124">Right-click hello server name in DNS Manager, select **Properties**, and then click hello **Forwarders** tab.</span></span>
2. <span data-ttu-id="b2634-125">Klik op Hallo **bewerken** knop tooremove doorstuurservers en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="b2634-125">Click hello **Edit** button tooremove any forwarders, and then click **OK**.</span></span>
3. <span data-ttu-id="b2634-126">Zorg ervoor dat Hallo **root-hints gebruiken als er geen doorstuurservers beschikbaar** selectievakje is ingeschakeld en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="b2634-126">Make sure that hello **Use root hints if no forwarders are available** check box is selected, and then click **OK**.</span></span>

## <a name="set-up-linux-compute-nodes"></a><span data-ttu-id="b2634-127">Linux-rekenknooppunten instellen</span><span class="sxs-lookup"><span data-stu-id="b2634-127">Set up Linux compute nodes</span></span>
<span data-ttu-id="b2634-128">U Hallo Linux-rekenknooppunten implementeren met behulp van Hallo dezelfde sjabloon voor de implementatie die u hebt gebruikt toocreate Hallo hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="b2634-128">You deploy hello Linux compute nodes by using hello same deployment template that you used toocreate hello head node.</span></span>

<span data-ttu-id="b2634-129">Hallo-bestand kopiëren **MyCluster.xml** vanuit uw lokale machine toohello hoofdknooppunt en update Hallo **NodeCount** tag met het aantal knooppunten dat u wilt dat toodeploy hello (< = 20).</span><span class="sxs-lookup"><span data-stu-id="b2634-129">Copy hello file **MyCluster.xml** from your local machine toohello head node, and update hello **NodeCount** tag with hello number of nodes that you want toodeploy (<=20).</span></span> <span data-ttu-id="b2634-130">Worden zorgvuldige toohave voldoende beschikbare kernen in uw Azure quotum omdat elk exemplaar A9 16 kernen in uw abonnement verbruikt.</span><span class="sxs-lookup"><span data-stu-id="b2634-130">Be careful toohave enough available cores in your Azure quota, because each A9 instance will consume 16 cores in your subscription.</span></span> <span data-ttu-id="b2634-131">U kunt A8-exemplaren (8 kernen) gebruiken in plaats van A9 als u toouse meer virtuele machines in Hallo wilt hetzelfde budget.</span><span class="sxs-lookup"><span data-stu-id="b2634-131">You can use A8 instances (8 cores) instead of A9 if you want toouse more VMs in hello same budget.</span></span>

<span data-ttu-id="b2634-132">Kopieer op Hallo hoofdknooppunt, Hallo HPC Pack IaaS implementatiescripts.</span><span class="sxs-lookup"><span data-stu-id="b2634-132">On hello head node, copy hello HPC Pack IaaS deployment scripts.</span></span>

<span data-ttu-id="b2634-133">Voer Hallo volgende Azure PowerShell-opdrachten in een opdrachtprompt met verhoogde bevoegdheid:</span><span class="sxs-lookup"><span data-stu-id="b2634-133">Run hello following Azure PowerShell commands in an elevated command prompt:</span></span>

1. <span data-ttu-id="b2634-134">Voer **Add-AzureAccount** tooconnect tooyour Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="b2634-134">Run **Add-AzureAccount** tooconnect tooyour Azure subscription.</span></span>
2. <span data-ttu-id="b2634-135">Als u meerdere abonnementen hebt, voert u **Get-AzureSubscription** toolist ze.</span><span class="sxs-lookup"><span data-stu-id="b2634-135">If you have multiple subscriptions, run **Get-AzureSubscription** toolist them.</span></span>
3. <span data-ttu-id="b2634-136">Een standaardabonnement ingesteld door Hallo **Select-AzureSubscription - SubscriptionName-xxxx-standaard** opdracht.</span><span class="sxs-lookup"><span data-stu-id="b2634-136">Set a default subscription by running hello **Select-AzureSubscription -SubscriptionName xxxx -Default** command.</span></span>
4. <span data-ttu-id="b2634-137">Voer **.\New-HPCIaaSCluster.ps1 - ConfigFile MyCluster.xml** toostart Linux-rekenknooppunten implementeren.</span><span class="sxs-lookup"><span data-stu-id="b2634-137">Run **.\New-HPCIaaSCluster.ps1 -ConfigFile MyCluster.xml** toostart deploying Linux compute nodes.</span></span>
   
   ![Hoofdknooppunt implementatie in actie][hndeploy]

<span data-ttu-id="b2634-139">Open het hulpprogramma voor Hallo HPC Pack Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="b2634-139">Open hello HPC Pack Cluster Manager tool.</span></span> <span data-ttu-id="b2634-140">Linux-rekenknooppunten wordt regelmatig na enkele minuten weergegeven in de lijst met clusterknooppunten compute.</span><span class="sxs-lookup"><span data-stu-id="b2634-140">After few minutes, Linux compute nodes will regularly appear in list of cluster compute nodes.</span></span> <span data-ttu-id="b2634-141">Met de klassieke implementatiemodus Hallo worden opeenvolgend IaaS VM's gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b2634-141">With hello classic deployment mode, IaaS VMs are created sequentially.</span></span> <span data-ttu-id="b2634-142">Dus als het aantal knooppunten Hallo belangrijk is, alle geïmplementeerd ophalen kan duren voordat een aanzienlijke hoeveelheid tijd.</span><span class="sxs-lookup"><span data-stu-id="b2634-142">So if hello number of nodes is important, getting them all deployed can take a significant amount of time.</span></span>

![Linux-knooppunten in HPC Pack Cluster Manager][clustermanager]

<span data-ttu-id="b2634-144">Nu dat alle knooppunten actief in het Hallo-cluster zijn, zijn er extra infrastructuur instellingen toomake.</span><span class="sxs-lookup"><span data-stu-id="b2634-144">Now that all nodes are up and running in hello cluster, there are additional infrastructure settings toomake.</span></span>

## <a name="set-up-an-azure-file-share-for-windows-and-linux-nodes"></a><span data-ttu-id="b2634-145">Instellen van een bestandsshare in Azure voor Windows en Linux-knooppunten</span><span class="sxs-lookup"><span data-stu-id="b2634-145">Set up an Azure File share for Windows and Linux nodes</span></span>
<span data-ttu-id="b2634-146">U kunt hello Azure File service toostore scripts, toepassingspakketten en gegevensbestanden worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="b2634-146">You can use hello Azure File service toostore scripts, application packages, and data files.</span></span> <span data-ttu-id="b2634-147">Azure-bestand biedt mogelijkheden voor CIFS boven op Azure Blob-opslag als een permanente opslag.</span><span class="sxs-lookup"><span data-stu-id="b2634-147">Azure File provides CIFS capabilities on top of Azure Blob storage as a persistent store.</span></span> <span data-ttu-id="b2634-148">Let erop dat dit geen Hallo meest schaalbare oplossing is, maar het Hallo eenvoudigste één is en geen toegewezen virtuele machines vereist.</span><span class="sxs-lookup"><span data-stu-id="b2634-148">Be aware that this is not hello most scalable solution, but it is hello simplest one and doesn’t require dedicated VMs.</span></span>

<span data-ttu-id="b2634-149">Een Azure-bestandsshare maken door het Hallo-instructies in Hallo artikel [aan de slag met Azure File storage in Windows](../../../storage/files/storage-dotnet-how-to-use-files.md).</span><span class="sxs-lookup"><span data-stu-id="b2634-149">Create an Azure File share by following hello instructions in hello article [Get started with Azure File storage on Windows](../../../storage/files/storage-dotnet-how-to-use-files.md).</span></span>

<span data-ttu-id="b2634-150">Hallo-naam van uw opslagaccount als **saname**, Hallo bestandssharenaam als **sharename**, en de opslagaccountsleutel Hallo als **sakey**.</span><span class="sxs-lookup"><span data-stu-id="b2634-150">Keep hello name of your storage account as **saname**, hello file share name as **sharename**, and hello storage account key as **sakey**.</span></span>

### <a name="mount-hello-azure-file-share-on-hello-head-node"></a><span data-ttu-id="b2634-151">Hallo Azure-bestandsshare op het hoofdknooppunt Hallo koppelen</span><span class="sxs-lookup"><span data-stu-id="b2634-151">Mount hello Azure File share on hello head node</span></span>
<span data-ttu-id="b2634-152">Open een opdrachtprompt met verhoogde bevoegdheid en Voer Hallo opdracht toostore Hallo referenties in Hallo lokale machine kluis te volgen:</span><span class="sxs-lookup"><span data-stu-id="b2634-152">Open an elevated command prompt and run hello following command toostore hello credentials in hello local machine vault:</span></span>

```
    cmdkey /add:<saname>.file.core.windows.net /user:<saname> /pass:<sakey>
```

<span data-ttu-id="b2634-153">Vervolgens toomount Hallo bestandsshare in Azure, worden uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="b2634-153">Then, toomount hello Azure File share, run:</span></span>

```
    net use Z: \\<saname>.file.core.windows.net\<sharename> /persistent:yes
```

### <a name="mount-hello-azure-file-share-on-linux-compute-nodes"></a><span data-ttu-id="b2634-154">Hello Azure-bestandsshare op Linux-rekenknooppunten koppelen</span><span class="sxs-lookup"><span data-stu-id="b2634-154">Mount hello Azure File share on Linux compute nodes</span></span>
<span data-ttu-id="b2634-155">Een nuttig hulpmiddel dat wordt geleverd met HPC Pack is Hallo clusrun hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="b2634-155">One useful tool that comes with HPC Pack is hello clusrun tool.</span></span> <span data-ttu-id="b2634-156">U kunt dit opdrachtregelprogramma toorun Hallo dezelfde opdracht tegelijkertijd gebruiken in een set van rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="b2634-156">You can use this command-line tool toorun hello same command simultaneously on a set of compute nodes.</span></span> <span data-ttu-id="b2634-157">In ons geval het toomount hello Azure-bestandsshare wordt gebruikt en blijven behouden deze toosurvive opnieuw wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="b2634-157">In our case, it's used toomount hello Azure File share and persist it toosurvive reboots.</span></span>
<span data-ttu-id="b2634-158">In een opdrachtprompt met verhoogde bevoegdheid op Hallo hoofdknooppunt Hallo volgende opdrachten worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b2634-158">In an elevated command prompt on hello head node, run hello following commands.</span></span>

<span data-ttu-id="b2634-159">toocreate hello Koppelmap:</span><span class="sxs-lookup"><span data-stu-id="b2634-159">toocreate hello mount directory:</span></span>

```
    clusrun /nodegroup:LinuxNodes mkdir -p /hpcdata
```

<span data-ttu-id="b2634-160">toomount hello Azure-bestandsshare:</span><span class="sxs-lookup"><span data-stu-id="b2634-160">toomount hello Azure File share:</span></span>

```
    clusrun /nodegroup:LinuxNodes mount -t cifs //<saname>.file.core.windows.net/<sharename> /hpcdata -o vers=2.1,username=<saname>,password='<sakey>',dir_mode=0777,file_mode=0777
```

<span data-ttu-id="b2634-161">toopersist hello mount-share:</span><span class="sxs-lookup"><span data-stu-id="b2634-161">toopersist hello mount share:</span></span>

```
    clusrun /nodegroup:LinuxNodes "echo //<saname>.file.core.windows.net/<sharename> /hpcdata cifs vers=2.1,username=<saname>,password='<sakey>',dir_mode=0777,file_mode=0777 >> /etc/fstab"
```

## <a name="install-star-ccm"></a><span data-ttu-id="b2634-162">Installeren van de STER-CCM +</span><span class="sxs-lookup"><span data-stu-id="b2634-162">Install STAR-CCM+</span></span>
<span data-ttu-id="b2634-163">Azure VM-instanties A8 en A9 bieden ondersteuning voor InfiniBand en RDMA-mogelijkheden.</span><span class="sxs-lookup"><span data-stu-id="b2634-163">Azure VM instances A8 and A9 provide InfiniBand support and RDMA capabilities.</span></span> <span data-ttu-id="b2634-164">Hallo kernel-stuurprogramma's waarmee deze mogelijkheden zijn beschikbaar voor Windows Server 2012 R2, SUSE 12, CentOS 6.5 en CentOS 7.1 afbeeldingen in hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="b2634-164">hello kernel drivers that enable those capabilities are available for Windows Server 2012 R2, SUSE 12, CentOS 6.5, and CentOS 7.1 images in hello Azure Marketplace.</span></span> <span data-ttu-id="b2634-165">Microsoft MPI en Intel MPI (versie 5.x) zijn Hallo twee MPI-bibliotheken die ondersteuning bieden voor de stuurprogramma's in Azure.</span><span class="sxs-lookup"><span data-stu-id="b2634-165">Microsoft MPI and Intel MPI (release 5.x) are hello two MPI libraries that support those drivers in Azure.</span></span>

<span data-ttu-id="b2634-166">CD adapco STER-CCM + 11.x vrijgeven en later wordt meegeleverd met Intel MPI-versie 5.x, dus InfiniBand-ondersteuning voor Azure opgenomen is.</span><span class="sxs-lookup"><span data-stu-id="b2634-166">CD-adapco STAR-CCM+ release 11.x and later is bundled with Intel MPI version 5.x, so InfiniBand support for Azure is included.</span></span>

<span data-ttu-id="b2634-167">Hallo Linux64 ophalen STER-CCM + pakket van Hallo [CD adapco portal](https://steve.cd-adapco.com).</span><span class="sxs-lookup"><span data-stu-id="b2634-167">Get hello Linux64 STAR-CCM+ package from hello [CD-adapco portal](https://steve.cd-adapco.com).</span></span> <span data-ttu-id="b2634-168">In ons geval hebben we versie 11.02.010 in gemengde precisie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b2634-168">In our case, we used version 11.02.010 in mixed precision.</span></span>

<span data-ttu-id="b2634-169">Hoofdknooppunt Hallo in Hallo van **/hpcdata** Azure File delen, maakt u een shell-script met de naam **setupstarccm.sh** Hello inhoud te volgen.</span><span class="sxs-lookup"><span data-stu-id="b2634-169">On hello head node, in hello **/hpcdata** Azure File share, create a shell script named **setupstarccm.sh** with hello following content.</span></span> <span data-ttu-id="b2634-170">Dit script wordt uitgevoerd op elke compute knooppunt tooset up STER-CCM + lokaal.</span><span class="sxs-lookup"><span data-stu-id="b2634-170">This script will be run on each compute node tooset up STAR-CCM+ locally.</span></span>

#### <a name="sample-setupstarcmsh-script"></a><span data-ttu-id="b2634-171">Voorbeeldscript setupstarcm.sh</span><span class="sxs-lookup"><span data-stu-id="b2634-171">Sample setupstarcm.sh script</span></span>
```
    #!/bin/bash
    # setupstarcm.sh tooset up STAR-CCM+ locally

    # Create hello CD-adapco main directory
    mkdir -p /opt/CD-adapco

    # Copy hello STAR-CCM package from hello file share toohello local directory
    cp /hpcdata/StarCCM/STAR-CCM+11.02.010_01_linux-x86_64.tar.gz /opt/CD-adapco/

    # Extract hello package
    tar -xzf /opt/CD-adapco/STAR-CCM+11.02.010_01_linux-x86_64.tar.gz -C /opt/CD-adapco/

    # Start a silent installation of STAR-CCM without hello FLEXlm component
    /opt/CD-adapco/starccm+_11.02.010/STAR-CCM+11.02.010_01_linux-x86_64-2.5_gnu4.8.bin -i silent -DCOMPUTE_NODE=true -DNODOC=true -DINSTALLFLEX=false

    # Update memory limits
    echo "*               hard    memlock         unlimited" >> /etc/security/limits.conf
    echo "*               soft    memlock         unlimited" >> /etc/security/limits.conf
```
<span data-ttu-id="b2634-172">Nu tooset up STER-CCM + op alle uw Linux rekenknooppunten, open een opdrachtprompt met verhoogde bevoegdheid en Voer Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="b2634-172">Now, tooset up STAR-CCM+ on all your Linux compute nodes, open an elevated command prompt and run hello following command:</span></span>

```
    clusrun /nodegroup:LinuxNodes bash /hpcdata/setupstarccm.sh
```

<span data-ttu-id="b2634-173">Tijdens het Hallo-opdracht wordt uitgevoerd, kunt u Hallo CPU-gebruik controleren met behulp van heatmap Hallo van Clusterbeheer.</span><span class="sxs-lookup"><span data-stu-id="b2634-173">While hello command is running, you can monitor hello CPU usage by using hello heat map of Cluster Manager.</span></span> <span data-ttu-id="b2634-174">Na enkele minuten alle knooppunten moeten correct zijn ingesteld.</span><span class="sxs-lookup"><span data-stu-id="b2634-174">After few minutes, all nodes should be correctly set up.</span></span>

## <a name="run-star-ccm-jobs"></a><span data-ttu-id="b2634-175">Uitvoeren van de STER-CCM + taken</span><span class="sxs-lookup"><span data-stu-id="b2634-175">Run STAR-CCM+ jobs</span></span>
<span data-ttu-id="b2634-176">HPC Pack wordt gebruikt voor de taak scheduler-mogelijkheden in volgorde toorun STER-CCM + taken.</span><span class="sxs-lookup"><span data-stu-id="b2634-176">HPC Pack is used for its job scheduler capabilities in order toorun STAR-CCM+ jobs.</span></span> <span data-ttu-id="b2634-177">toodo dus moeten we ondersteuning van een paar scripts die zijn gebruikt toostart Hallo taak en STER worden uitgevoerd Hallo-CCM +.</span><span class="sxs-lookup"><span data-stu-id="b2634-177">toodo so, we need hello support of a few scripts that are used toostart hello job and run STAR-CCM+.</span></span> <span data-ttu-id="b2634-178">Hallo invoergegevens wordt opgeslagen op het Azure-bestandsshare Hallo eerste voor eenvoud.</span><span class="sxs-lookup"><span data-stu-id="b2634-178">hello input data is kept on hello Azure File share first for simplicity.</span></span>

<span data-ttu-id="b2634-179">Hallo volgende PowerShell-script is gebruikte tooqueue een STER-CCM + taak.</span><span class="sxs-lookup"><span data-stu-id="b2634-179">hello following PowerShell script is used tooqueue a STAR-CCM+ job.</span></span> <span data-ttu-id="b2634-180">Het duurt drie argumenten:</span><span class="sxs-lookup"><span data-stu-id="b2634-180">It takes three arguments:</span></span>

* <span data-ttu-id="b2634-181">Hallo modelnaam</span><span class="sxs-lookup"><span data-stu-id="b2634-181">hello model name</span></span>
* <span data-ttu-id="b2634-182">het aantal knooppunten toobe gebruikt Hallo</span><span class="sxs-lookup"><span data-stu-id="b2634-182">hello number of nodes toobe used</span></span>
* <span data-ttu-id="b2634-183">Hallo aantal kernen op elk knooppunt toobe gebruikt</span><span class="sxs-lookup"><span data-stu-id="b2634-183">hello number of cores on each node toobe used</span></span>

<span data-ttu-id="b2634-184">Omdat STER-CCM + kunt vullen Hallo geheugenbandbreedte, het doorgaans beter toouse minder cores per rekenknooppunten en nieuwe knooppunten toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="b2634-184">Because STAR-CCM+ can fill hello memory bandwidth, it's usually better toouse fewer cores per compute nodes and add new nodes.</span></span> <span data-ttu-id="b2634-185">Hallo exacte aantal kernen per knooppunt, is afhankelijk van Hallo processorfamilie en Hallo tussen geheugenonderdelen snelheid.</span><span class="sxs-lookup"><span data-stu-id="b2634-185">hello exact number of cores per node will depend on hello processor family and hello interconnect speed.</span></span>

<span data-ttu-id="b2634-186">Hallo knooppunten exclusief voor Hallo taak worden toegewezen en kunnen niet worden gedeeld met andere taken.</span><span class="sxs-lookup"><span data-stu-id="b2634-186">hello nodes are allocated exclusively for hello job and can’t be shared with other jobs.</span></span> <span data-ttu-id="b2634-187">Hallo-taak is niet rechtstreeks als een MPI-taak gestart.</span><span class="sxs-lookup"><span data-stu-id="b2634-187">hello job is not started as an MPI job directly.</span></span> <span data-ttu-id="b2634-188">Hallo **runstarccm.sh** shellscript Hallo MPI launcher wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="b2634-188">hello **runstarccm.sh** shell script will start hello MPI launcher.</span></span>

<span data-ttu-id="b2634-189">Hallo invoercode model en Hallo **runstarccm.sh** script worden opgeslagen in Hallo **/hpcdata** -share die eerder is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="b2634-189">hello input model and hello **runstarccm.sh** script are stored in hello **/hpcdata** share that was previously mounted.</span></span>

<span data-ttu-id="b2634-190">Logboekbestanden worden benoemd met Hallo taak-ID en worden opgeslagen in Hallo **/hpcdata share**, samen met de Hallo STER-CCM + uitvoerbestanden.</span><span class="sxs-lookup"><span data-stu-id="b2634-190">Log files are named with hello job ID and are stored in hello **/hpcdata share**, along with hello STAR-CCM+ output files.</span></span>

#### <a name="sample-submitstarccmjobps1-script"></a><span data-ttu-id="b2634-191">Voorbeeldscript SubmitStarccmJob.ps1</span><span class="sxs-lookup"><span data-stu-id="b2634-191">Sample SubmitStarccmJob.ps1 script</span></span>
```
    Add-PSSnapin Microsoft.HPC -ErrorAction silentlycontinue
    $scheduler="headnodename"
    $modelName=$args[0]
    $nbCoresPerNode=$args[2]
    $nbNodes=$args[1]

    #---------------------------------------------------------------------------------------------------------
    # Create a new job; this will give us hello job ID that's used tooidentify hello name of hello uploaded package in Azure
    #
    $job = New-HpcJob -Name "$modelName $nbNodes $nbCoresPerNode" -Scheduler $scheduler -NumNodes $nbNodes -NodeGroups "LinuxNodes" -FailOnTaskFailure $true -Exclusive $true
    $jobId = [String]$job.Id

    #---------------------------------------------------------------------------------------------------------
    # Submit hello job     
    $workdir =  "/hpcdata"
    $execName = "$nbCoresPerNode runner.java $modelName.sim"

    $job | Add-HpcTask -Scheduler $scheduler -Name "Compute" -stdout "$jobId.log" -stderr "$jobId.err" -Rerunnable $false -NumNodes $nbNodes -Command "runstarccm.sh $execName" -WorkDir "$workdir"


    Submit-HpcJob -Job $job -Scheduler $scheduler
```
<span data-ttu-id="b2634-192">Vervang **runner.java** met uw voorkeur STER-CCM + Java model linksboven en logboekregistratie-code.</span><span class="sxs-lookup"><span data-stu-id="b2634-192">Replace **runner.java** with your preferred STAR-CCM+ Java model launcher and logging code.</span></span>

#### <a name="sample-runstarccmsh-script"></a><span data-ttu-id="b2634-193">Voorbeeldscript runstarccm.sh</span><span class="sxs-lookup"><span data-stu-id="b2634-193">Sample runstarccm.sh script</span></span>
```
    #!/bin/bash
    echo "start"
    # hello path of this script
    SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
    echo ${SCRIPT_PATH}
    # Set hello mpirun runtime environment
    export CDLMD_LICENSE_FILE=1999@flex.cd-adapco.com

    # mpirun command
    STARCCM=/opt/CD-adapco/STAR-CCM+11.02.010/star/bin/starccm+

    # Get node information from ENVs
    NODESCORES=(${CCP_NODES_CORES})
    COUNT=${#NODESCORES[@]}
    NBCORESPERNODE=$1

    # Create hello hostfile file
    NODELIST_PATH=${SCRIPT_PATH}/hostfile_$$
    echo ${NODELIST_PATH}

    # Get every node name and write into hello hostfile file
    I=1
    NBNODES=0
    while [ ${I} -lt ${COUNT} ]
    do
        echo "${NODESCORES[${I}]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
        let "NBNODES=${NBNODES}+1"
    done
    let "NBCORES=${NBNODES}*${NBCORESPERNODE}"

    # Run STAR-CCM with hello hostfile argument
    #  
    ${STARCCM} -np ${NBCORES} -machinefile ${NODELIST_PATH} \
        -power -podkey "<yourkey>" -rsh ssh \
        -mpi intel -fabric UDAPL -cpubind bandwidth,v \
        -mppflags "-ppn $NBCORESPERNODE -genv I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -genv I_MPI_DAPL_UD=0 -genv I_MPI_DYNAMIC_CONNECTION=0" \
        -batch $2 $3
    RTNSTS=$?
    rm -f ${NODELIST_PATH}

    exit ${RTNSTS}
```

<span data-ttu-id="b2634-194">In onze test hebben we een token Power-On-Demand-licentie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b2634-194">In our test, we used a Power-On-Demand license token.</span></span> <span data-ttu-id="b2634-195">Voor dit token, hebt u tooset hello **$CDLMD_LICENSE_FILE** omgevingsvariabele te **1999@flex.cd-adapco.com**  en Hallo-sleutel in Hallo **- podkey** optie van Hallo-opdrachtregel .</span><span class="sxs-lookup"><span data-stu-id="b2634-195">For that token, you have tooset hello **$CDLMD_LICENSE_FILE** environment variable too**1999@flex.cd-adapco.com** and hello key in hello **-podkey** option of hello command line.</span></span>

<span data-ttu-id="b2634-196">Na enkele initialisatie Hallo script extraheert--uit Hallo **$CCP_NODES_CORES** omgevingsvariabelen die HPC Pack ingesteld--Hallo lijst met knooppunten toobuild maakt gebruik van een hostfile die Hallo MPI starten.</span><span class="sxs-lookup"><span data-stu-id="b2634-196">After some initialization, hello script extracts--from hello **$CCP_NODES_CORES** environment variables that HPC Pack set--hello list of nodes toobuild a hostfile that hello MPI launcher uses.</span></span> <span data-ttu-id="b2634-197">Deze hostfile bevat Hallo lijst met namen van de compute nodes die worden gebruikt voor de taak hello, één naam per regel.</span><span class="sxs-lookup"><span data-stu-id="b2634-197">This hostfile will contain hello list of compute node names that are used for hello job, one name per line.</span></span>

<span data-ttu-id="b2634-198">Hallo-indeling van **$CCP_NODES_CORES** volgt dit patroon:</span><span class="sxs-lookup"><span data-stu-id="b2634-198">hello format of **$CCP_NODES_CORES** follows this pattern:</span></span>

```
<Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>...`
```

<span data-ttu-id="b2634-199">Waar:</span><span class="sxs-lookup"><span data-stu-id="b2634-199">Where:</span></span>

* <span data-ttu-id="b2634-200">`<Number of nodes>`is het aantal knooppunten toegewezen toothis taak Hallo.</span><span class="sxs-lookup"><span data-stu-id="b2634-200">`<Number of nodes>` is hello number of nodes allocated toothis job.</span></span>
* <span data-ttu-id="b2634-201">`<Name of node_n_...>`Hallo-naam van elk knooppunt toothis taak toegewezen is.</span><span class="sxs-lookup"><span data-stu-id="b2634-201">`<Name of node_n_...>` is hello name of each node allocated toothis job.</span></span>
* <span data-ttu-id="b2634-202">`<Cores of node_n_...>`is het aantal kernen op Hallo-knooppunt toegewezen toothis taak Hallo.</span><span class="sxs-lookup"><span data-stu-id="b2634-202">`<Cores of node_n_...>` is hello number of cores on hello node allocated toothis job.</span></span>

<span data-ttu-id="b2634-203">het aantal kernen Hallo (**$NBCORES**) is ook het aantal knooppunten berekend op basis van hello (**$NBNODES**) en het aantal kernen per knooppunt hello (opgegeven als parameter **$NBCORESPERNODE**).</span><span class="sxs-lookup"><span data-stu-id="b2634-203">hello number of cores (**$NBCORES**) is also calculated based on hello number of nodes (**$NBNODES**) and hello number of cores per node (provided as parameter **$NBCORESPERNODE**).</span></span>

<span data-ttu-id="b2634-204">Hallo MPI-opties, Hallo waarden die worden gebruikt met Intel MPI in Azure zijn:</span><span class="sxs-lookup"><span data-stu-id="b2634-204">For hello MPI options, hello ones that are used with Intel MPI on Azure are:</span></span>

* <span data-ttu-id="b2634-205">`-mpi intel`toospecify Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="b2634-205">`-mpi intel` toospecify Intel MPI.</span></span>
* <span data-ttu-id="b2634-206">`-fabric UDAPL`toouse Azure InfiniBand termen.</span><span class="sxs-lookup"><span data-stu-id="b2634-206">`-fabric UDAPL` toouse Azure InfiniBand verbs.</span></span>
* <span data-ttu-id="b2634-207">`-cpubind bandwidth,v`toooptimize bandbreedte voor MPI met STER-CCM +.</span><span class="sxs-lookup"><span data-stu-id="b2634-207">`-cpubind bandwidth,v` toooptimize bandwidth for MPI with STAR-CCM+.</span></span>
* <span data-ttu-id="b2634-208">`-mppflags "-ppn $NBCORESPERNODE -genv I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -genv I_MPI_DAPL_UD=0 -genv I_MPI_DYNAMIC_CONNECTION=0"`toomake Intel MPI werken met Azure InfiniBand en tooset Hallo het vereiste aantal kernen per knooppunt.</span><span class="sxs-lookup"><span data-stu-id="b2634-208">`-mppflags "-ppn $NBCORESPERNODE -genv I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -genv I_MPI_DAPL_UD=0 -genv I_MPI_DYNAMIC_CONNECTION=0"` toomake Intel MPI work with Azure InfiniBand, and tooset hello required number of cores per node.</span></span>
* <span data-ttu-id="b2634-209">`-batch`toostart STER-CCM + in batchmodus met geen gebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="b2634-209">`-batch` toostart STAR-CCM+ in batch mode with no UI.</span></span>

<span data-ttu-id="b2634-210">Ten slotte toostart een taak, zorg dat uw knooppunten actief zijn en online in de Cluster-beheer zijn.</span><span class="sxs-lookup"><span data-stu-id="b2634-210">Finally, toostart a job, make sure that your nodes are up and running and are online in Cluster Manager.</span></span> <span data-ttu-id="b2634-211">Vanuit een PowerShell-opdrachtprompt voert u dit:</span><span class="sxs-lookup"><span data-stu-id="b2634-211">Then from a PowerShell command prompt, run this:</span></span>

```
    .\ SubmitStarccmJob.ps1 <model> <nbNodes> <nbCoresPerNode>
```

## <a name="stop-nodes"></a><span data-ttu-id="b2634-212">Knooppunten stoppen</span><span class="sxs-lookup"><span data-stu-id="b2634-212">Stop nodes</span></span>
<span data-ttu-id="b2634-213">Later in nadat u met de tests uitgevoerd bent klaar, kunt u gebruiken Hallo HPC Pack PowerShell-opdrachten toostop te volgen en start knooppunten:</span><span class="sxs-lookup"><span data-stu-id="b2634-213">Later on, after you're done with your tests, you can use hello following HPC Pack PowerShell commands toostop and start nodes:</span></span>

```
    Stop-HPCIaaSNode.ps1 -Name <prefix>-00*
    Start-HPCIaaSNode.ps1 -Name <prefix>-00*
```

## <a name="next-steps"></a><span data-ttu-id="b2634-214">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b2634-214">Next steps</span></span>
<span data-ttu-id="b2634-215">Probeer andere werkbelastingen Linux wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b2634-215">Try running other Linux workloads.</span></span> <span data-ttu-id="b2634-216">Bijvoorbeeld, Zie:</span><span class="sxs-lookup"><span data-stu-id="b2634-216">For example, see:</span></span>

* [<span data-ttu-id="b2634-217">Voer NAMD met Microsoft HPC Pack op Linux-rekenknooppunten in Azure</span><span class="sxs-lookup"><span data-stu-id="b2634-217">Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](hpcpack-cluster-namd.md)
* [<span data-ttu-id="b2634-218">OpenFOAM met Microsoft HPC Pack uitvoeren op een Linux RDMA-cluster in Azure</span><span class="sxs-lookup"><span data-stu-id="b2634-218">Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>](hpcpack-cluster-openfoam.md)

<!--Image references-->
[hndeploy]:media/hpcpack-cluster-starccm/hndeploy.png
[clustermanager]:media/hpcpack-cluster-starccm/ClusterManager.png
