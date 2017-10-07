---
title: aaaSet van een Linux RDMA cluster toorun MPI-toepassingen | Microsoft Docs
description: Een Linux-cluster van de grootte van H16r, H16mr, A8 of A9-VM's toouse hello Azure RDMA netwerk toorun MPI-apps maken
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 01834bad-c8e6-48a3-b066-7f1719047dd2
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/14/2017
ms.author: danlep
ms.openlocfilehash: 3199317a37b095e80718d6724954687d30aea3a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-linux-rdma-cluster-toorun-mpi-applications"></a><span data-ttu-id="3664c-103">Instellen van een Linux RDMA cluster toorun MPI-toepassingen</span><span class="sxs-lookup"><span data-stu-id="3664c-103">Set up a Linux RDMA cluster toorun MPI applications</span></span>
<span data-ttu-id="3664c-104">Meer informatie over hoe tooset van een Linux RDMA-cluster in Azure met [hoge prestaties compute-VM-grootten](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toorun parallelle Message Passing Interface (MPI)-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="3664c-104">Learn how tooset up a Linux RDMA cluster in Azure with [High performance compute VM sizes](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toorun parallel Message Passing Interface (MPI) applications.</span></span> <span data-ttu-id="3664c-105">Dit artikel bevat stappen tooprepare een Linux HPC installatiekopie toorun Intel MPI op een cluster.</span><span class="sxs-lookup"><span data-stu-id="3664c-105">This article provides steps tooprepare a Linux HPC image toorun Intel MPI on a cluster.</span></span> <span data-ttu-id="3664c-106">Nadat de voorbereiding, moet u een cluster van virtuele machines met behulp van deze installatiekopie en een van de Hallo RDMA-compatibele Azure VM-grootten (H16mr momenteel H16r A8 of A9) implementeert.</span><span class="sxs-lookup"><span data-stu-id="3664c-106">After preparation, you deploy a cluster of VMs using this image and one of hello RDMA-capable Azure VM sizes (currently H16r, H16mr, A8, or A9).</span></span> <span data-ttu-id="3664c-107">Hallo cluster toorun MPI-toepassingen die efficiënt via een lage latentie, een hoge gegevensdoorvoer netwerk op basis van remote direct memory access (RDMA)-technologie communiceren gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3664c-107">Use hello cluster toorun MPI applications that communicate efficiently over a low-latency, high-throughput network based on remote direct memory access (RDMA) technology.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3664c-108">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) en klassieke.</span><span class="sxs-lookup"><span data-stu-id="3664c-108">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span></span> <span data-ttu-id="3664c-109">In dit artikel wordt behandeld met het klassieke implementatiemodel Hallo.</span><span class="sxs-lookup"><span data-stu-id="3664c-109">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="3664c-110">Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3664c-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

## <a name="cluster-deployment-options"></a><span data-ttu-id="3664c-111">Cluster-implementatieopties</span><span class="sxs-lookup"><span data-stu-id="3664c-111">Cluster deployment options</span></span>
<span data-ttu-id="3664c-112">Hieronder vindt u methoden kunt u een cluster Linux RDMA toocreate met of zonder een Taakplanner.</span><span class="sxs-lookup"><span data-stu-id="3664c-112">Following are methods you can use toocreate a Linux RDMA cluster with or without a job scheduler.</span></span>

* <span data-ttu-id="3664c-113">**Azure CLI-scripts**: Zie verderop in dit artikel, gebruikt u Hallo [Azure-opdrachtregelinterface](../../../cli-install-nodejs.md) (CLI) tooscript Hallo implementatie van een cluster met RDMA-compatibele virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="3664c-113">**Azure CLI scripts**: As shown later in this article, use hello [Azure command-line interface](../../../cli-install-nodejs.md) (CLI) tooscript hello deployment of a cluster of RDMA-capable VMs.</span></span> <span data-ttu-id="3664c-114">Hallo CLI in Service Management-modus maakt Hallo clusterknooppunten opeenvolgend in het klassieke implementatiemodel hello, dus veel rekenknooppunten implementeren kan enkele minuten duren.</span><span class="sxs-lookup"><span data-stu-id="3664c-114">hello CLI in Service Management mode creates hello cluster nodes serially in hello classic deployment model, so deploying many compute nodes might take several minutes.</span></span> <span data-ttu-id="3664c-115">tooenable hello RDMA-netwerkverbinding wanneer u het klassieke implementatiemodel hello, Hallo virtuele machines implementeren in Hallo dezelfde cloudservice.</span><span class="sxs-lookup"><span data-stu-id="3664c-115">tooenable hello RDMA network connection when you use hello classic deployment model, deploy hello VMs in hello same cloud service.</span></span>
* <span data-ttu-id="3664c-116">**Azure Resource Manager-sjablonen**: U kunt ook Hallo Resource Manager deployment model toodeploy een cluster met RDMA-compatibele virtuele machines die toohello RDMA netwerk verbindt.</span><span class="sxs-lookup"><span data-stu-id="3664c-116">**Azure Resource Manager templates**: You can also use hello Resource Manager deployment model toodeploy a cluster of RDMA-capable VMs that connects toohello RDMA network.</span></span> <span data-ttu-id="3664c-117">U kunt [uw eigen sjabloon maken](../../../resource-group-authoring-templates.md), of Controleer Hallo [Azure-snelstartsjablonen](https://azure.microsoft.com/documentation/templates/) voor sjablonen die is bijgedragen door Microsoft of Hallo community toodeploy Hallo gewenste oplossing.</span><span class="sxs-lookup"><span data-stu-id="3664c-117">You can [create your own template](../../../resource-group-authoring-templates.md), or check hello [Azure quickstart templates](https://azure.microsoft.com/documentation/templates/) for templates contributed by Microsoft or hello community toodeploy hello solution you want.</span></span> <span data-ttu-id="3664c-118">Resource Manager-sjablonen kunnen bieden een snelle en betrouwbare manier toodeploy een Linux-cluster.</span><span class="sxs-lookup"><span data-stu-id="3664c-118">Resource Manager templates can provide a fast and reliable way toodeploy a Linux cluster.</span></span> <span data-ttu-id="3664c-119">tooenable hello RDMA-netwerkverbinding wanneer u Hallo Resource Manager-implementatiemodel implementeren Hallo VM's in Hallo dezelfde beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="3664c-119">tooenable hello RDMA network connection when you use hello Resource Manager deployment model, deploy hello VMs in hello same availability set.</span></span>
* <span data-ttu-id="3664c-120">**HPC Pack**: een Microsoft HPC Pack-cluster in Azure maken en toevoegen van RDMA-compatibele rekenknooppunten waarop een ondersteunde Linux distributie tooaccess hello RDMA-netwerk wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3664c-120">**HPC Pack**: Create a Microsoft HPC Pack cluster in Azure and add RDMA-capable compute nodes that run a supported Linux distribution tooaccess hello RDMA network.</span></span> <span data-ttu-id="3664c-121">Zie voor meer informatie [aan de slag met Linux-rekenknooppunten in een cluster HPC Pack Azure](hpcpack-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="3664c-121">For more information, see [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md).</span></span>

## <a name="sample-deployment-steps-in-hello-classic-model"></a><span data-ttu-id="3664c-122">Voorbeeld-implementatiestappen in het klassieke model Hallo</span><span class="sxs-lookup"><span data-stu-id="3664c-122">Sample deployment steps in hello classic model</span></span>
<span data-ttu-id="3664c-123">Hallo volgende stappen laten zien hoe toouse hello Azure CLI toodeploy een SUSE Linux Enterprise Server (SLES) 12 SP1 HPC VM van hello Azure Marketplace, aanpassen en een aangepaste installatiekopie van de virtuele machine maken.</span><span class="sxs-lookup"><span data-stu-id="3664c-123">hello following steps show how toouse hello Azure CLI toodeploy a SUSE Linux Enterprise Server (SLES) 12 SP1 HPC VM from hello Azure Marketplace, customize it, and create a custom VM image.</span></span> <span data-ttu-id="3664c-124">Vervolgens kunt u Hallo tooscript Hallo implementatie van de installatiekopie van een cluster van RDMA-compatibele virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="3664c-124">Then you can use hello image tooscript hello deployment of a cluster of RDMA-capable VMs.</span></span>

> [!TIP]
> <span data-ttu-id="3664c-125">Gebruik dezelfde stappen toodeploy die een cluster met RDMA-compatibele virtuele machines op basis van installatiekopieën op basis van CentOS HPC in hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="3664c-125">Use similar steps toodeploy a cluster of RDMA-capable VMs based on CentOS-based HPC images in hello Azure Marketplace.</span></span> <span data-ttu-id="3664c-126">Een aantal stappen verschillen, zoals aangegeven.</span><span class="sxs-lookup"><span data-stu-id="3664c-126">Some steps differ slightly, as noted.</span></span> 
>
>

### <a name="prerequisites"></a><span data-ttu-id="3664c-127">Vereisten</span><span class="sxs-lookup"><span data-stu-id="3664c-127">Prerequisites</span></span>
* <span data-ttu-id="3664c-128">**Clientcomputer**: U moet een Mac, Linux of Windows client computer toocommunicate met Azure.</span><span class="sxs-lookup"><span data-stu-id="3664c-128">**Client computer**: You need a Mac, Linux, or Windows client computer toocommunicate with Azure.</span></span> <span data-ttu-id="3664c-129">Deze stappen wordt ervan uitgegaan dat u een Linux-client.</span><span class="sxs-lookup"><span data-stu-id="3664c-129">These steps assume you are using a Linux client.</span></span>
* <span data-ttu-id="3664c-130">**Azure-abonnement**: als u geen een abonnement hebt, kunt u een [gratis account](https://azure.microsoft.com/free/) binnen een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="3664c-130">**Azure subscription**: If you don't have a subscription, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span> <span data-ttu-id="3664c-131">Voor grotere clusters kunt u een abonnement op gebruiksbasis of andere Aankoopopties.</span><span class="sxs-lookup"><span data-stu-id="3664c-131">For larger clusters, consider a pay-as-you-go subscription or other purchase options.</span></span>
* <span data-ttu-id="3664c-132">**Beschikbaarheid van de VM-grootte**: Hallo na instanties zijn RDMA-compatibele: H16r, H16mr A8 en A9.</span><span class="sxs-lookup"><span data-stu-id="3664c-132">**VM size availability**: hello following instance sizes are RDMA capable: H16r, H16mr, A8, and A9.</span></span> <span data-ttu-id="3664c-133">Controleer [producten die beschikbaar zijn in elke regio](https://azure.microsoft.com/regions/services/) voor beschikbaarheid in een Azure-regio's.</span><span class="sxs-lookup"><span data-stu-id="3664c-133">Check [Products available by region](https://azure.microsoft.com/regions/services/) for availability in Azure regions.</span></span>
* <span data-ttu-id="3664c-134">**Quotum voor kernen**: tooincrease Hallo quotum van kernen toodeploy een cluster van virtuele machines rekenintensieve moet u mogelijk.</span><span class="sxs-lookup"><span data-stu-id="3664c-134">**Cores quota**: You might need tooincrease hello quota of cores toodeploy a cluster of compute-intensive VMs.</span></span> <span data-ttu-id="3664c-135">Bijvoorbeeld, moet u ten minste 128 kernen als u wilt dat toodeploy 8 A9 VM's zoals in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="3664c-135">For example, you need at least 128 cores if you want toodeploy 8 A9 VMs as shown in this article.</span></span> <span data-ttu-id="3664c-136">Uw abonnement mogelijk ook het aantal kernen dat u in bepaalde VM grootte families implementeren kunt, met inbegrip van Hallo H-serie Hallo beperken.</span><span class="sxs-lookup"><span data-stu-id="3664c-136">Your subscription might also limit hello number of cores you can deploy in certain VM size families, including hello H-series.</span></span> <span data-ttu-id="3664c-137">toorequest een quotum verhogen, [opent u een ondersteuningsaanvraag online klant](../../../azure-supportability/how-to-create-azure-support-request.md) zonder kosten.</span><span class="sxs-lookup"><span data-stu-id="3664c-137">toorequest a quota increase, [open an online customer support request](../../../azure-supportability/how-to-create-azure-support-request.md) at no charge.</span></span>
* <span data-ttu-id="3664c-138">**Azure CLI**: [installeren](../../../cli-install-nodejs.md) hello Azure CLI en [tooyour Azure-abonnement verbinden](../../../xplat-cli-connect.md) van Hallo-clientcomputer.</span><span class="sxs-lookup"><span data-stu-id="3664c-138">**Azure CLI**: [Install](../../../cli-install-nodejs.md) hello Azure CLI and [connect tooyour Azure subscription](../../../xplat-cli-connect.md) from hello client computer.</span></span>

### <a name="provision-an-sles-12-sp1-hpc-vm"></a><span data-ttu-id="3664c-139">Een VM SLES 12 SP1 HPC inrichten</span><span class="sxs-lookup"><span data-stu-id="3664c-139">Provision an SLES 12 SP1 HPC VM</span></span>
<span data-ttu-id="3664c-140">Voer na het aanmelden tooAzure Hello Azure CLI, `azure config list` tooconfirm die Hallo uitvoer toont Service Management-modus.</span><span class="sxs-lookup"><span data-stu-id="3664c-140">After signing in tooAzure with hello Azure CLI, run `azure config list` tooconfirm that hello output shows Service Management mode.</span></span> <span data-ttu-id="3664c-141">Als dit niet het geval is, stelt u Hallo-modus met deze opdracht:</span><span class="sxs-lookup"><span data-stu-id="3664c-141">If it does not, set hello mode by running this command:</span></span>

    azure config mode asm


<span data-ttu-id="3664c-142">Hallo toolist na alle Hallo abonnementen zijn van bevoegde toouse typt u:</span><span class="sxs-lookup"><span data-stu-id="3664c-142">Type hello following toolist all hello subscriptions you are authorized toouse:</span></span>

    azure account list

<span data-ttu-id="3664c-143">de huidige actieve abonnement Hallo wordt geïdentificeerd met `Current` instellen te`true`.</span><span class="sxs-lookup"><span data-stu-id="3664c-143">hello current active subscription is identified with `Current` set too`true`.</span></span> <span data-ttu-id="3664c-144">Als dit abonnement niet Hallo u toouse toocreate Hallo cluster wilt toevoegen, Hallo juiste abonnements-ID als Hallo actief abonnement instellen:</span><span class="sxs-lookup"><span data-stu-id="3664c-144">If this subscription isn't hello one you want toouse toocreate hello cluster, set hello appropriate subscription ID as hello active subscription:</span></span>

    azure account set <subscription-Id>

<span data-ttu-id="3664c-145">toosee Hallo openbaar SLES 12 SP1 HPC-afbeeldingen in Azure, voert u een opdracht zoals hello te volgen, ervan uitgaande dat uw omgeving shell ondersteunt **grep**:</span><span class="sxs-lookup"><span data-stu-id="3664c-145">toosee hello publicly available SLES 12 SP1 HPC images in Azure, run a command like hello following, assuming your shell environment supports **grep**:</span></span>

    azure vm image list | grep "suse.*hpc"

<span data-ttu-id="3664c-146">Richt een RDMA-compatibele virtuele machine met een installatiekopie SLES 12 SP1 HPC door het uitvoeren van een opdracht zoals Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="3664c-146">Provision an RDMA-capable VM with a SLES 12 SP1 HPC image by running a command like hello following:</span></span>

    azure vm create -g <username> -p <password> -c <cloud-service-name> -l <location> -z A9 -n <vm-name> -e 22 b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-v20160824

<span data-ttu-id="3664c-147">Waar:</span><span class="sxs-lookup"><span data-stu-id="3664c-147">Where:</span></span>

* <span data-ttu-id="3664c-148">Hallo grootte (A9 in dit voorbeeld) is een van de VM-grootten Hallo RDMA-functionaliteit.</span><span class="sxs-lookup"><span data-stu-id="3664c-148">hello size (A9 in this example) is one of hello RDMA-capable VM sizes.</span></span>
* <span data-ttu-id="3664c-149">Hallo externe SSH-poortnummer (22 in dit voorbeeld Hallo SSH standaard is) is een geldig poortnummer.</span><span class="sxs-lookup"><span data-stu-id="3664c-149">hello external SSH port number (22 in this example, which is hello SSH default) is any valid port number.</span></span> <span data-ttu-id="3664c-150">Hallo interne SSH-poortnummer is too22 ingesteld.</span><span class="sxs-lookup"><span data-stu-id="3664c-150">hello internal SSH port number is set too22.</span></span>
* <span data-ttu-id="3664c-151">Een nieuwe cloudservice wordt gemaakt in hello Azure-regio op Hallo locatie opgegeven.</span><span class="sxs-lookup"><span data-stu-id="3664c-151">A new cloud service is created in hello Azure region specified by hello location.</span></span> <span data-ttu-id="3664c-152">Geef een locatie in welke Hallo VM grootte die u kiest beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="3664c-152">Specify a location in which hello VM size you choose is available.</span></span>
* <span data-ttu-id="3664c-153">Voor ondersteuning van prioriteit SUSE (die extra kosten in rekening worden gebracht), de naam van de installatiekopie Hallo SLES 12 SP1 momenteel kan bestaan uit een van deze twee opties:</span><span class="sxs-lookup"><span data-stu-id="3664c-153">For SUSE priority support (which incurs additional charges), hello SLES 12 SP1 image name currently can be one of these two options:</span></span> 

 `b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-v20160824`

  `b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-priority-v20160824`


### <a name="customize-hello-vm"></a><span data-ttu-id="3664c-154">Hallo VM aanpassen</span><span class="sxs-lookup"><span data-stu-id="3664c-154">Customize hello VM</span></span>
<span data-ttu-id="3664c-155">Nadat Hallo VM is ingericht, wordt SSH toohello VM via Hallo van het externe IP-adres van de virtuele machine (of DNS-naam) en Hallo externe poortnummer dat u hebt geconfigureerd en deze aanpassen.</span><span class="sxs-lookup"><span data-stu-id="3664c-155">After hello VM finishes provisioning, SSH toohello VM by using hello VM's external IP address (or DNS name) and hello external port number you configured, and then customize it.</span></span> <span data-ttu-id="3664c-156">Zie voor meer informatie verbinding [hoe toolog op tooa virtuele machine met Linux](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3664c-156">For connection details, see [How toolog on tooa virtual machine running Linux](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="3664c-157">Opdrachten uitvoeren als Hallo-gebruiker die u hebt geconfigureerd op Hallo VM, tenzij de toegang tot de hoofdmap is vereist toocomplete een stap.</span><span class="sxs-lookup"><span data-stu-id="3664c-157">Perform commands as hello user you configured on hello VM, unless root access is required toocomplete a step.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3664c-158">Microsoft Azure biedt geen toegang tot de hoofdmap tooLinux virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="3664c-158">Microsoft Azure does not provide root access tooLinux VMs.</span></span> <span data-ttu-id="3664c-159">beheerderstoegang toogain wanneer verbonden als een gebruiker toohello VM, het uitvoeren van opdrachten via `sudo`.</span><span class="sxs-lookup"><span data-stu-id="3664c-159">toogain administrative access when connected as a user toohello VM, run commands by using `sudo`.</span></span>
>
>

* <span data-ttu-id="3664c-160">**Updates**: Installeer updates met behulp van zypper.</span><span class="sxs-lookup"><span data-stu-id="3664c-160">**Updates**: Install updates by using zypper.</span></span> <span data-ttu-id="3664c-161">U kunt ook tooinstall NFS-hulpprogramma's.</span><span class="sxs-lookup"><span data-stu-id="3664c-161">You might also want tooinstall NFS utilities.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="3664c-162">U wordt aangeraden dat u kernel-updates, wat leiden problemen Hello Linux RDMA stuurprogramma's tot kunnen niet toe te passen in een VM SLES 12 SP1 HPC.</span><span class="sxs-lookup"><span data-stu-id="3664c-162">In a SLES 12 SP1 HPC VM, we recommend that you don't apply kernel updates, which can cause issues with hello Linux RDMA drivers.</span></span>
  >
  >
* <span data-ttu-id="3664c-163">**Intel MPI**: Hallo-installatie van Intel MPI op Hallo SLES 12 SP1 HPC VM voltooid door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="3664c-163">**Intel MPI**: Complete hello installation of Intel MPI on hello SLES 12 SP1 HPC VM by running hello following command:</span></span>

        sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
* <span data-ttu-id="3664c-164">**Vergrendelen van geheugen**: voor MPI-codes toolock Hallo geheugen beschikbaar voor RDMA, toevoegen of wijzigen van de volgende instellingen in Hallo /etc/security/limits.conf bestand Hallo.</span><span class="sxs-lookup"><span data-stu-id="3664c-164">**Lock memory**: For MPI codes toolock hello memory available for RDMA, add or change hello following settings in hello /etc/security/limits.conf file.</span></span> <span data-ttu-id="3664c-165">U moet dit bestand hoofdmap toegang tooedit.</span><span class="sxs-lookup"><span data-stu-id="3664c-165">You need root access tooedit this file.</span></span>

    ```
    <User or group name> hard    memlock <memory required for your application in KB>

    <User or group name> soft    memlock <memory required for your application in KB>
    ```

  > [!NOTE]
  > <span data-ttu-id="3664c-166">U kunt ook memlock toounlimited instellen voor testdoeleinden.</span><span class="sxs-lookup"><span data-stu-id="3664c-166">For testing purposes, you can also set memlock toounlimited.</span></span> <span data-ttu-id="3664c-167">Bijvoorbeeld: `<User or group name>    hard    memlock unlimited`.</span><span class="sxs-lookup"><span data-stu-id="3664c-167">For example: `<User or group name>    hard    memlock unlimited`.</span></span> <span data-ttu-id="3664c-168">Zie voor meer informatie [aanbevolen bekende methoden voor instelling vergrendeld geheugengrootte](https://software.intel.com/en-us/blogs/2014/12/16/best-known-methods-for-setting-locked-memory-size).</span><span class="sxs-lookup"><span data-stu-id="3664c-168">For more information, see [Best known methods for setting locked memory size](https://software.intel.com/en-us/blogs/2014/12/16/best-known-methods-for-setting-locked-memory-size).</span></span>
  >
  >
* <span data-ttu-id="3664c-169">**SSH-sleutels voor virtuele machines SLES**: genereren SSH-sleutels tooestablish vertrouwensrelatie voor uw gebruikersaccount tussen Hallo rekenknooppunten in Hallo SLES cluster bij het uitvoeren van MPI-taken.</span><span class="sxs-lookup"><span data-stu-id="3664c-169">**SSH keys for SLES VMs**: Generate SSH keys tooestablish trust for your user account among hello compute nodes in hello SLES cluster when running MPI jobs.</span></span> <span data-ttu-id="3664c-170">Als u een VM op basis van CentOS HPC hebt geïmplementeerd, niet volgt u deze stap.</span><span class="sxs-lookup"><span data-stu-id="3664c-170">If you deployed a CentOS-based HPC VM, don't follow this step.</span></span> <span data-ttu-id="3664c-171">Zie de instructies verderop in dit artikel tooset up passwordless SSH-vertrouwensrelatie tussen de clusterknooppunten Hallo na het Hallo-installatiekopie en Hallo-cluster implementeren.</span><span class="sxs-lookup"><span data-stu-id="3664c-171">See instructions later in this article tooset up passwordless SSH trust among hello cluster nodes after you capture hello image and deploy hello cluster.</span></span>

    <span data-ttu-id="3664c-172">toocreate SSH-sleutels, Hallo volgende opdracht uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="3664c-172">toocreate SSH keys, run hello following command.</span></span> <span data-ttu-id="3664c-173">Wanneer u wordt gevraagd om invoer, selecteert u **Enter** toogenerate Hallo sleutels in de standaardlocatie Hallo zonder een wachtwoord wordt ingesteld.</span><span class="sxs-lookup"><span data-stu-id="3664c-173">When you are prompted for input, select **Enter** toogenerate hello keys in hello default location without setting a password.</span></span>

        ssh-keygen

    <span data-ttu-id="3664c-174">Toevoegen van Hallo openbare sleutel toohello authorized_keys voor bekende openbare sleutels.</span><span class="sxs-lookup"><span data-stu-id="3664c-174">Append hello public key toohello authorized_keys file for known public keys.</span></span>

        cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys

    <span data-ttu-id="3664c-175">In Hallo ~/.ssh directory bewerken of Hallo-configuratiebestand te maken.</span><span class="sxs-lookup"><span data-stu-id="3664c-175">In hello ~/.ssh directory, edit or create hello config file.</span></span> <span data-ttu-id="3664c-176">Hallo IP-adresbereik van het particuliere netwerk Hallo bieden dat u van plan toouse in Azure (10.32.0.0/16 in dit voorbeeld bent):</span><span class="sxs-lookup"><span data-stu-id="3664c-176">Provide hello IP address range of hello private network that you plan toouse in Azure (10.32.0.0/16 in this example):</span></span>

        host 10.32.0.*
        StrictHostKeyChecking no

    <span data-ttu-id="3664c-177">U kunt ook als volgt Hallo particulier netwerk-IP-adres van elke virtuele machine in het cluster weergeven:</span><span class="sxs-lookup"><span data-stu-id="3664c-177">Alternatively, list hello private network IP address of each VM in your cluster as follows:</span></span>

    ```
    host 10.32.0.1
     StrictHostKeyChecking no
    host 10.32.0.2
     StrictHostKeyChecking no
    host 10.32.0.3
     StrictHostKeyChecking no
    ```

  > [!NOTE]
  > <span data-ttu-id="3664c-178">Configureren van `StrictHostKeyChecking no` een beveiligingsrisico met zich mee kunt maken wanneer er een specifiek IP-adres of -bereik is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="3664c-178">Configuring `StrictHostKeyChecking no` can create a potential security risk when a specific IP address or range is not specified.</span></span>
  >
  >
* <span data-ttu-id="3664c-179">**Toepassingen**: installeert u alle toepassingen die u nodig hebt of andere aanpassingen uitvoeren voordat u Hallo installatiekopie vastleggen.</span><span class="sxs-lookup"><span data-stu-id="3664c-179">**Applications**: Install any applications you need or perform other customizations before you capture hello image.</span></span>

### <a name="capture-hello-image"></a><span data-ttu-id="3664c-180">Hallo installatiekopie vastleggen</span><span class="sxs-lookup"><span data-stu-id="3664c-180">Capture hello image</span></span>
<span data-ttu-id="3664c-181">toocapture hello afbeelding, Hallo volgende opdracht op Hallo Linux-VM voor het eerst uitvoert.</span><span class="sxs-lookup"><span data-stu-id="3664c-181">toocapture hello image, first run hello following command on hello Linux VM.</span></span> <span data-ttu-id="3664c-182">Met deze opdracht Hallo VM deprovisions maar behoudt gebruikersaccounts en SSH-sleutels die u hebt ingesteld.</span><span class="sxs-lookup"><span data-stu-id="3664c-182">This command deprovisions hello VM but maintains user accounts and SSH keys that you set up.</span></span>

```
sudo waagent -deprovision
```

<span data-ttu-id="3664c-183">Uitvoeren vanaf de clientcomputer hello Azure CLI-opdrachten toocapture Hallo installatiekopie te volgen.</span><span class="sxs-lookup"><span data-stu-id="3664c-183">From your client computer, run hello following Azure CLI commands toocapture hello image.</span></span> <span data-ttu-id="3664c-184">Zie voor meer informatie [hoe toocapture klassieke virtuele Linux-machine als afbeelding](capture-image.md).</span><span class="sxs-lookup"><span data-stu-id="3664c-184">For more information, see [How toocapture a classic Linux virtual machine as an image](capture-image.md).</span></span>  

```
azure vm shutdown <vm-name>

azure vm capture -t <vm-name> <image-name>

```

<span data-ttu-id="3664c-185">Nadat u deze opdrachten uitgevoerd, Hallo VM-installatiekopie wordt vastgelegd voor het gebruik en Hallo VM is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="3664c-185">After you run these commands, hello VM image is captured for your use and hello VM is deleted.</span></span> <span data-ttu-id="3664c-186">Nu hebt u uw aangepaste installatiekopie gereed toodeploy een cluster.</span><span class="sxs-lookup"><span data-stu-id="3664c-186">Now you have your custom image ready toodeploy a cluster.</span></span>

### <a name="deploy-a-cluster-with-hello-image"></a><span data-ttu-id="3664c-187">Een installatiekopie van het Hallo-cluster implementeren</span><span class="sxs-lookup"><span data-stu-id="3664c-187">Deploy a cluster with hello image</span></span>
<span data-ttu-id="3664c-188">Hallo Bash-script met de juiste waarden voor uw omgeving te volgen wijzigen en uitvoeren vanaf de clientcomputer.</span><span class="sxs-lookup"><span data-stu-id="3664c-188">Modify hello following Bash script with appropriate values for your environment and run it from your client computer.</span></span> <span data-ttu-id="3664c-189">Omdat Azure Hallo VMs opeenvolgend in het klassieke implementatiemodel Hallo implementeert, duurt het enkele minuten toodeploy Hallo acht A9-VM's in dit script wordt voorgesteld.</span><span class="sxs-lookup"><span data-stu-id="3664c-189">Because Azure deploys hello VMs serially in hello classic deployment model, it takes a few minutes toodeploy hello eight A9 VMs suggested in this script.</span></span>

```
#!/bin/bash -x
# Script toocreate a compute cluster without a scheduler in a VNet in Azure
# Create a custom private network in Azure
# Replace 10.32.0.0 with your virtual network address space
# Replace <network-name> with your network identifier
# Replace "West US" with an Azure region where hello VM size is available
# See Azure Pricing pages for prices and availability of compute-intensive VMs

azure network vnet create -l "West US" -e 10.32.0.0 -i 16 <network-name>

# Create a cloud service. All hello compute-intensive instances need toobe in hello same cloud service for Linux RDMA toowork across InfiniBand.
# Note: hello current maximum number of VMs in a cloud service is 50. If you need tooprovision more than 50 VMs in hello same cloud service in your cluster, contact Azure Support.

azure service create <cloud-service-name> --location "West US" –s <subscription-ID>

# Define a prefix naming scheme for compute nodes, e.g., cluster11, cluster12, etc.

vmname=cluster

# Define a prefix for external port numbers. If you want tooturn off external ports and use only internal ports toocommunicate between compute nodes via port 22, don’t use this option. Since port numbers up too10000 are reserved, use numbers after 10000. Leave external port on for rank 0 and head node.

portnumber=101

# In this cluster there will be 8 size A9 nodes, named cluster11 toocluster18. Specify your captured image in <image-name>. Specify hello username and password you used when creating hello SSH keys.

for (( i=11; i<19; i++ )); do
        azure vm create -g <username> -p <password> -c <cloud-service-name> -z A9 -n $vmname$i -e $portnumber$i -w <network-name> -b Subnet-1 <image-name>
done

# Save this script with a name like makecluster.sh and run it in your shell environment tooprovision your cluster
```

## <a name="considerations-for-a-centos-hpc-cluster"></a><span data-ttu-id="3664c-190">Overwegingen voor een CentOS HPC-cluster</span><span class="sxs-lookup"><span data-stu-id="3664c-190">Considerations for a CentOS HPC cluster</span></span>
<span data-ttu-id="3664c-191">Als u tooset van een op basis van een van de Hallo op basis van CentOS HPC-afbeeldingen in hello Azure Marketplace in plaats van SLES 12 voor HPC-cluster wilt, stappen Hallo Algemeen in de voorgaande sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="3664c-191">If you want tooset up a cluster based on one of hello CentOS-based HPC images in hello Azure Marketplace instead of SLES 12 for HPC, follow hello general steps in hello preceding section.</span></span> <span data-ttu-id="3664c-192">Houd er rekening mee Hallo verschillen volgen wanneer u inricht en Hallo VM configureert:</span><span class="sxs-lookup"><span data-stu-id="3664c-192">Note hello following differences when you provision and configure hello VM:</span></span>

- <span data-ttu-id="3664c-193">Intel MPI is al geïnstalleerd op een virtuele machine vanaf een installatiekopie van een HPC op basis van CentOS wordt ingericht.</span><span class="sxs-lookup"><span data-stu-id="3664c-193">Intel MPI is already installed on a VM provisioned from a CentOS-based HPC image.</span></span>
- <span data-ttu-id="3664c-194">Vergrendeling geheugeninstellingen zijn al toegevoegd in Hallo van de virtuele machine /etc/security/limits.conf-bestand.</span><span class="sxs-lookup"><span data-stu-id="3664c-194">Lock memory settings are already added in hello VM's /etc/security/limits.conf file.</span></span>
- <span data-ttu-id="3664c-195">Genereren geen SSH-sleutels op Hallo VM die u inricht voor vastleggen.</span><span class="sxs-lookup"><span data-stu-id="3664c-195">Do not generate SSH keys on hello VM you provision for capture.</span></span> <span data-ttu-id="3664c-196">In plaats daarvan wordt aangeraden verificatie op basis van een gebruiker instellen nadat u Hallo-cluster implementeren.</span><span class="sxs-lookup"><span data-stu-id="3664c-196">Instead, we recommend setting up user-based authentication after you deploy hello cluster.</span></span> <span data-ttu-id="3664c-197">Zie Hallo volgende sectie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="3664c-197">For more information, see hello following section.</span></span>  

### <a name="set-up-passwordless-ssh-trust-on-hello-cluster"></a><span data-ttu-id="3664c-198">Passwordless SSH vertrouwen op Hallo cluster instellen</span><span class="sxs-lookup"><span data-stu-id="3664c-198">Set up passwordless SSH trust on hello cluster</span></span>
<span data-ttu-id="3664c-199">Op een op basis van CentOS HPC-cluster, er zijn twee methoden voor het instellen van een vertrouwensrelatie tussen de rekenknooppunten Hallo: verificatie op basis van de host en verificatie op basis van gebruiker.</span><span class="sxs-lookup"><span data-stu-id="3664c-199">On a CentOS-based HPC cluster, there are two methods for establishing trust between hello compute nodes: host-based authentication and user-based authentication.</span></span> <span data-ttu-id="3664c-200">Verificatie op basis van een host bevindt zich buiten het bereik van dit artikel hello en in het algemeen moet worden uitgevoerd via een script extensie tijdens de implementatie.</span><span class="sxs-lookup"><span data-stu-id="3664c-200">Host-based authentication is outside of hello scope of this article and generally must be done through an extension script during deployment.</span></span> <span data-ttu-id="3664c-201">Verificatie op basis van een gebruiker is handig voor het instellen van een vertrouwensrelatie na de implementatie en vereist Hallo genereren en delen van SSH-sleutels tussen Hallo rekenknooppunten in Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="3664c-201">User-based authentication is convenient for establishing trust after deployment and requires hello generation and sharing of SSH keys among hello compute nodes in hello cluster.</span></span> <span data-ttu-id="3664c-202">Deze methode staat bekend als passwordless SSH-aanmelding en is vereist bij het uitvoeren van MPI-taken.</span><span class="sxs-lookup"><span data-stu-id="3664c-202">This method is commonly known as passwordless SSH login and is required when running MPI jobs.</span></span>

<span data-ttu-id="3664c-203">Een voorbeeld van een script bijgedragen Hallo community is beschikbaar op [GitHub](https://github.com/tanewill/utils/blob/master/user_authentication.sh) tooenable eenvoudig gebruikersverificatie op een op basis van CentOS HPC-cluster.</span><span class="sxs-lookup"><span data-stu-id="3664c-203">A sample script contributed from hello community is available on [GitHub](https://github.com/tanewill/utils/blob/master/user_authentication.sh) tooenable easy user authentication on a CentOS-based HPC cluster.</span></span> <span data-ttu-id="3664c-204">Download en gebruik dit script met behulp van Hallo stappen te volgen.</span><span class="sxs-lookup"><span data-stu-id="3664c-204">Download and use this script by using hello following steps.</span></span> <span data-ttu-id="3664c-205">U kunt ook dit script wijzigen of een andere methode tooestablish passwordless SSH-verificatie tussen de clusterknooppunten compute hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3664c-205">You can also modify this script or use any other method tooestablish passwordless SSH authentication between hello cluster compute nodes.</span></span>

    wget https://raw.githubusercontent.com/tanewill/utils/master/ user_authentication.sh

<span data-ttu-id="3664c-206">toorun hello script, moet u tooknow Hallo voorvoegsel voor uw subnet IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="3664c-206">toorun hello script, you need tooknow hello prefix for your subnet IP addresses.</span></span> <span data-ttu-id="3664c-207">Hallo voorvoegsel ophalen door het uitvoeren van de volgende opdracht op een van de clusterknooppunten Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="3664c-207">Get hello prefix by running hello following command on one of hello cluster nodes.</span></span> <span data-ttu-id="3664c-208">De uitvoer ziet er ongeveer als 10.1.3.5 en Hallo-voorvoegsel is Hallo/m 10.1.3 gedeelte.</span><span class="sxs-lookup"><span data-stu-id="3664c-208">Your output should look something like 10.1.3.5, and hello prefix is hello 10.1.3 portion.</span></span>

    ifconfig eth0 | grep -w inet | awk '{print $2}'

<span data-ttu-id="3664c-209">Voer nu Hallo script met drie parameters: algemene gebruikersnaam op Hallo Hallo rekenknooppunten, Hallo gemeenschappelijk wachtwoord voor die gebruiker op Hallo van rekenknooppunten en Hallo subnetvoorvoegsel die is geretourneerd van de vorige opdracht Hallo.</span><span class="sxs-lookup"><span data-stu-id="3664c-209">Now run hello script using three parameters: hello common user name on hello compute nodes, hello common password for that user on hello compute nodes, and hello subnet prefix that was returned from hello previous command.</span></span>

    ./user_authentication.sh <myusername> <mypassword> 10.1.3

<span data-ttu-id="3664c-210">Dit script Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="3664c-210">This script does hello following:</span></span>

* <span data-ttu-id="3664c-211">Maakt een map op Hallo hostknooppunt met SSH, de naam die is vereist voor passwordless aanmelding.</span><span class="sxs-lookup"><span data-stu-id="3664c-211">Creates a directory on hello host node named .ssh, which is required for passwordless login.</span></span>
* <span data-ttu-id="3664c-212">Maakt een configuratiebestand in Hallo SSH directory zodat passwordless aanmelding tooallow aanmelding vanaf elk knooppunt in het Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="3664c-212">Creates a configuration file in hello .ssh directory that instructs passwordless login tooallow login from any node in hello cluster.</span></span>
* <span data-ttu-id="3664c-213">Bestanden met Hallo node names en knooppunt IP-adressen voor alle Hallo knooppunten in Hallo-cluster maakt.</span><span class="sxs-lookup"><span data-stu-id="3664c-213">Creates files containing hello node names and node IP addresses for all hello nodes in hello cluster.</span></span> <span data-ttu-id="3664c-214">Deze bestanden blijven nadat het Hallo-script wordt uitgevoerd voor naslagdoeleinden.</span><span class="sxs-lookup"><span data-stu-id="3664c-214">These files are left after hello script is run for later reference.</span></span>
* <span data-ttu-id="3664c-215">Maakt een persoonlijke en openbare sleutelpaar voor elk clusterknooppunt (inclusief Hallo hostknooppunt) en vermeldingen in Hallo authorized_keys bestand maakt.</span><span class="sxs-lookup"><span data-stu-id="3664c-215">Creates a private and public key pair for each cluster node (including hello host node) and creates entries in hello authorized_keys file.</span></span>

> [!WARNING]
> <span data-ttu-id="3664c-216">Dit script uitvoert, kan een beveiligingsrisico met zich mee maken.</span><span class="sxs-lookup"><span data-stu-id="3664c-216">Running this script can create a potential security risk.</span></span> <span data-ttu-id="3664c-217">Zorg ervoor dat Hallo openbare sleutelinformatie in ~/.ssh niet is gedistribueerd.</span><span class="sxs-lookup"><span data-stu-id="3664c-217">Ensure that hello public key information in ~/.ssh is not distributed.</span></span>
>
>

## <a name="configure-intel-mpi"></a><span data-ttu-id="3664c-218">Intel MPI configureren</span><span class="sxs-lookup"><span data-stu-id="3664c-218">Configure Intel MPI</span></span>
<span data-ttu-id="3664c-219">toorun MPI-toepassingen op Azure Linux RDMA, moet u tooconfigure bepaalde omgeving variabelen specifieke tooIntel MPI.</span><span class="sxs-lookup"><span data-stu-id="3664c-219">toorun MPI applications on Azure Linux RDMA, you need tooconfigure certain environment variables specific tooIntel MPI.</span></span> <span data-ttu-id="3664c-220">Hier volgt een voorbeeld Bash script tooconfigure Hallo variabelen nodig toorun een toepassing.</span><span class="sxs-lookup"><span data-stu-id="3664c-220">Here is a sample Bash script tooconfigure hello variables needed toorun an application.</span></span> <span data-ttu-id="3664c-221">Hallo pad toompivars.sh Wijzig zo nodig voor de installatie van Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="3664c-221">Change hello path toompivars.sh as needed for your installation of Intel MPI.</span></span>

```
#!/bin/bash -x

# For a SLES 12 SP1 HPC cluster

source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh

# For a CentOS-based HPC cluster

# source /opt/intel/impi/5.1.3.181/bin64/mpivars.sh

export I_MPI_FABRICS=shm:dapl

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB
# Setting hello variable tooshm:dapl gives best performance for some applications
# If your application doesn’t take advantage of shared memory and MPI together, then set only dapl

export I_MPI_DAPL_PROVIDER=ofa-v2-ib0

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB

export I_MPI_DYNAMIC_CONNECTION=0

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB

# Command line toorun hello job

mpirun -n <number-of-cores> -ppn <core-per-node> -hostfile <hostfilename>  /path <path toohello application exe> <arguments specific toohello application>

#end
```

<span data-ttu-id="3664c-222">Hallo-indeling van het hostbestand Hallo is als volgt.</span><span class="sxs-lookup"><span data-stu-id="3664c-222">hello format of hello host file is as follows.</span></span> <span data-ttu-id="3664c-223">Een regel voor elk knooppunt in het cluster toevoegen.</span><span class="sxs-lookup"><span data-stu-id="3664c-223">Add one line for each node in your cluster.</span></span> <span data-ttu-id="3664c-224">Geef de privé IP-adressen van het virtuele netwerk Hallo eerder hebt gedefinieerd, niet de DNS-namen.</span><span class="sxs-lookup"><span data-stu-id="3664c-224">Specify private IP addresses from hello virtual network defined earlier, not DNS names.</span></span> <span data-ttu-id="3664c-225">Hallo-bestand bevat bijvoorbeeld voor twee hosts met IP-adressen 10.32.0.1 en 10.32.0.2 Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="3664c-225">For example, for two hosts with IP addresses 10.32.0.1 and 10.32.0.2, hello file contains hello following:</span></span>

```
10.32.0.1:16
10.32.0.2:16
```

## <a name="run-mpi-on-a-basic-two-node-cluster"></a><span data-ttu-id="3664c-226">MPI worden uitgevoerd op een basic cluster met twee knooppunten</span><span class="sxs-lookup"><span data-stu-id="3664c-226">Run MPI on a basic two-node cluster</span></span>
<span data-ttu-id="3664c-227">Als u dit nog niet hebt gedaan, eerst Hallo omgeving instellen voor Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="3664c-227">If you haven't already done so, first set up hello environment for Intel MPI.</span></span>

```
# For a SLES 12 SP1 HPC cluster

source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh

# For a CentOS-based HPC cluster

# source /opt/intel/impi/5.1.3.181/bin64/mpivars.sh
```

### <a name="run-an-mpi-command"></a><span data-ttu-id="3664c-228">Voer een MPI-opdracht</span><span class="sxs-lookup"><span data-stu-id="3664c-228">Run an MPI command</span></span>
<span data-ttu-id="3664c-229">Een MPI-opdracht uitvoeren op een van de Hallo compute knooppunten tooshow die MPI juist is geïnstalleerd en kan communiceren tussen ten minste twee rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="3664c-229">Run an MPI command on one of hello compute nodes tooshow that MPI is installed properly and can communicate between at least two compute nodes.</span></span> <span data-ttu-id="3664c-230">Hallo volgende **mpirun** opdracht wordt uitgevoerd Hallo **hostnaam** opdracht op twee knooppunten.</span><span class="sxs-lookup"><span data-stu-id="3664c-230">hello following **mpirun** command runs hello **hostname** command on two nodes.</span></span>

```
mpirun -ppn 1 -n 2 -hosts <host1>,<host2> -env I_MPI_FABRICS=shm:dapl -env I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -env I_MPI_DYNAMIC_CONNECTION=0 hostname
```
<span data-ttu-id="3664c-231">De uitvoer moet lijst Hallo-namen van alle Hallo knooppunten die u hebt doorgegeven als invoer voor `-hosts`.</span><span class="sxs-lookup"><span data-stu-id="3664c-231">Your output should list hello names of all hello nodes that you passed as input for `-hosts`.</span></span> <span data-ttu-id="3664c-232">Bijvoorbeeld, een **mpirun** opdracht met twee knooppunten retourneert Hallo volgende uitvoer:</span><span class="sxs-lookup"><span data-stu-id="3664c-232">For example, an **mpirun** command with two nodes returns output like hello following:</span></span>

```
cluster11
cluster12
```

### <a name="run-an-mpi-benchmark"></a><span data-ttu-id="3664c-233">Voer een benchmark MPI</span><span class="sxs-lookup"><span data-stu-id="3664c-233">Run an MPI benchmark</span></span>
<span data-ttu-id="3664c-234">Hallo volgende Intel MPI-opdracht wordt uitgevoerd een pingpong benchmark tooverify Hallo configuratie en verbinding toohello RDMA clusternetwerk.</span><span class="sxs-lookup"><span data-stu-id="3664c-234">hello following Intel MPI command runs a pingpong benchmark tooverify hello cluster configuration and connection toohello RDMA network.</span></span>

```
mpirun -hosts <host1>,<host2> -ppn 1 -n 2 -env I_MPI_FABRICS=dapl -env I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -env I_MPI_DYNAMIC_CONNECTION=0 IMB-MPI1 pingpong
```

<span data-ttu-id="3664c-235">Op een werkende-cluster met twee knooppunten ziet u uitvoer zoals Hallo volgende.</span><span class="sxs-lookup"><span data-stu-id="3664c-235">On a working cluster with two nodes, you should see output like hello following.</span></span> <span data-ttu-id="3664c-236">Verwacht op Hallo RDMA Azure-netwerk, latentie op of onder 3 microseconden voor berichtgrootten up too512 bytes.</span><span class="sxs-lookup"><span data-stu-id="3664c-236">On hello Azure RDMA network, expect latency at or below 3 microseconds for message sizes up too512 bytes.</span></span>

```
#------------------------------------------------------------
#    Intel (R) MPI Benchmarks 4.0 Update 1, MPI-1 part
#------------------------------------------------------------
# Date                  : Fri Jul 17 23:16:46 2015
# Machine               : x86_64
# System                : Linux
# Release               : 3.12.39-44-default
# Version               : #5 SMP Thu Jun 25 22:45:24 UTC 2015
# MPI Version           : 3.0
# MPI Thread Environment:
# New default behavior from Version 3.2 on:
# hello number of iterations per message size is cut down
# dynamically when a certain run time (per message size sample)
# is expected toobe exceeded. Time limit is defined by variable
# "SECS_PER_SAMPLE" (=> IMB_settings.h)
# or through hello flag => -time

# Calling sequence was:
# /opt/intel/impi_latest/bin64/IMB-MPI1 pingpong
# Minimum message length in bytes:   0
# Maximum message length in bytes:   4194304
#
# MPI_Datatype                   :   MPI_BYTE
# MPI_Datatype for reductions    :   MPI_FLOAT
# MPI_Op                         :   MPI_SUM
#
#
# List of Benchmarks toorun:
# PingPong
#---------------------------------------------------
# Benchmarking PingPong
# #processes = 2
#---------------------------------------------------
       #bytes #repetitions      t[usec]   Mbytes/sec
            0         1000         2.23         0.00
            1         1000         2.26         0.42
            2         1000         2.26         0.85
            4         1000         2.26         1.69
            8         1000         2.26         3.38
           16         1000         2.36         6.45
           32         1000         2.57        11.89
           64         1000         2.36        25.81
          128         1000         2.64        46.19
          256         1000         2.73        89.30
          512         1000         3.09       157.99
         1024         1000         3.60       271.53
         2048         1000         4.46       437.57
         4096         1000         6.11       639.23
         8192         1000         7.49      1043.47
        16384         1000         9.76      1600.76
        32768         1000        14.98      2085.77
        65536          640        25.99      2405.08
       131072          320        50.68      2466.64
       262144          160        80.62      3101.01
       524288           80       145.86      3427.91
      1048576           40       279.06      3583.42
      2097152           20       543.37      3680.71
      4194304           10      1082.94      3693.63

# All processes entering MPI_Finalize

```



## <a name="next-steps"></a><span data-ttu-id="3664c-237">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3664c-237">Next steps</span></span>
* <span data-ttu-id="3664c-238">Implementeren en uw Linux MPI-toepassingen uitvoeren op uw Linux-cluster.</span><span class="sxs-lookup"><span data-stu-id="3664c-238">Deploy and run your Linux MPI applications on your Linux cluster.</span></span>
* <span data-ttu-id="3664c-239">Zie Hallo [Intel MPI-bibliotheek documentatie](https://software.intel.com/en-us/articles/intel-mpi-library-documentation/) voor hulp bij het Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="3664c-239">See hello [Intel MPI Library documentation](https://software.intel.com/en-us/articles/intel-mpi-library-documentation/) for guidance on Intel MPI.</span></span>
* <span data-ttu-id="3664c-240">Probeer een [snelstartsjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/intel-lustre-clients-on-centos) toocreate een Intel Lustre met behulp van een installatiekopie op basis van CentOS HPC-cluster.</span><span class="sxs-lookup"><span data-stu-id="3664c-240">Try a [quickstart template](https://github.com/Azure/azure-quickstart-templates/tree/master/intel-lustre-clients-on-centos) toocreate an Intel Lustre cluster by using a CentOS-based HPC image.</span></span> <span data-ttu-id="3664c-241">Zie voor meer informatie [Intel Cloud Edition implementeren voor Lustre in Microsoft Azure](https://blogs.msdn.microsoft.com/arsen/2015/10/29/deploying-intel-cloud-edition-for-lustre-on-microsoft-azure/).</span><span class="sxs-lookup"><span data-stu-id="3664c-241">For details, see [Deploying Intel Cloud Edition for Lustre on Microsoft Azure](https://blogs.msdn.microsoft.com/arsen/2015/10/29/deploying-intel-cloud-edition-for-lustre-on-microsoft-azure/).</span></span>
