---
title: een AWS-VM's van Windows-tooAzure aaaMove | Microsoft Docs
description: Verplaatsen van een Amazon Web Services (AWS) EC2 Windows exemplaar tooAzure virtuele Machines met Azure PowerShell.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: cynthn
ms.openlocfilehash: f912c28d3ffe585162c3add715a1318ac3cd4643
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-a-windows-vm-from-amazon-web-services-aws-tooazure-using-powershell"></a><span data-ttu-id="258bb-103">Een Windows VM verplaatsen van Amazon Web Services (AWS) tooAzure met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="258bb-103">Move a Windows VM from Amazon Web Services (AWS) tooAzure using PowerShell</span></span>

<span data-ttu-id="258bb-104">Als u virtuele machines voor het hosten van uw workloads in Azure, kunt u een bestaand exemplaar van de virtuele machine met Amazon Web Services (AWS) EC2 Windows exporteren vervolgens Hallo virtuele harde schijf (VHD) tooAzure uploaden.</span><span class="sxs-lookup"><span data-stu-id="258bb-104">If you are evaluating Azure virtual machines for hosting your workloads, you can export an existing Amazon Web Services (AWS) EC2 Windows VM instance then upload hello virtual hard disk (VHD) tooAzure.</span></span> <span data-ttu-id="258bb-105">Eenmaal Hallo die VHD is geüpload, kunt u een nieuwe virtuele machine in Azure uit Hallo VHD.</span><span class="sxs-lookup"><span data-stu-id="258bb-105">Once hello VHD is uploaded, you can create a new VM in Azure from hello VHD.</span></span> 

<span data-ttu-id="258bb-106">In dit onderwerp bevat informatie over het verplaatsen van één VM van AWS tooAzure.</span><span class="sxs-lookup"><span data-stu-id="258bb-106">This topic covers moving a single VM from AWS tooAzure.</span></span> <span data-ttu-id="258bb-107">Als u toomove virtuele machines van AWS tooAzure op grote schaal wilt, Zie [migreren van virtuele machines in Amazon Web Services (AWS) tooAzure met Azure Site Recovery](../../site-recovery/site-recovery-migrate-aws-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="258bb-107">If you want toomove VMs from AWS tooAzure at scale, see [Migrate virtual machines in Amazon Web Services (AWS) tooAzure with Azure Site Recovery](../../site-recovery/site-recovery-migrate-aws-to-azure.md).</span></span>

## <a name="prepare-hello-vm"></a><span data-ttu-id="258bb-108">Hallo VM voorbereiden</span><span class="sxs-lookup"><span data-stu-id="258bb-108">Prepare hello VM</span></span> 
 
<span data-ttu-id="258bb-109">U kunt algemene en gespecialiseerde VHD's tooAzure uploaden.</span><span class="sxs-lookup"><span data-stu-id="258bb-109">You can upload both generalized and specialized VHDs tooAzure.</span></span> <span data-ttu-id="258bb-110">Elk type vereist dat u Hallo VM voorbereiden voordat u exporteert van AWS.</span><span class="sxs-lookup"><span data-stu-id="258bb-110">Each type requires that you prepare hello VM before exporting from AWS.</span></span> 

- <span data-ttu-id="258bb-111">**VHD gegeneraliseerd** -een gegeneraliseerde VHD heeft al uw persoonlijke accountgegevens verwijderd met behulp van Sysprep.</span><span class="sxs-lookup"><span data-stu-id="258bb-111">**Generalized VHD** - a generalized VHD has had all of your personal account information removed using Sysprep.</span></span> <span data-ttu-id="258bb-112">Als u van plan toouse Hallo VHD als een installatiekopie toocreate bent nieuwe virtuele machines van moet:</span><span class="sxs-lookup"><span data-stu-id="258bb-112">If you intend toouse hello VHD as an image toocreate new VMs from, you should:</span></span> 
 
    * <span data-ttu-id="258bb-113">[Voorbereiden van een Windows VM](prepare-for-upload-vhd-image.md).</span><span class="sxs-lookup"><span data-stu-id="258bb-113">[Prepare a Windows VM](prepare-for-upload-vhd-image.md).</span></span>  
    * <span data-ttu-id="258bb-114">Generalize Hallo virtuele machine met behulp van Sysprep.</span><span class="sxs-lookup"><span data-stu-id="258bb-114">Generalize hello virtual machine using Sysprep.</span></span>  

 
- <span data-ttu-id="258bb-115">**VHD gespecialiseerde** -een gespecialiseerde VHD onderhoudt Hallo gebruikersaccounts, toepassingen en andere statusgegevens van uw oorspronkelijke VM.</span><span class="sxs-lookup"><span data-stu-id="258bb-115">**Specialized VHD** - a specialized VHD maintains hello user accounts, applications and other state data from your original VM.</span></span> <span data-ttu-id="258bb-116">Als u van plan toouse bent Hallo VHD-toocreate is een nieuwe virtuele machine, Controleer Hallo stappen zijn voltooid.</span><span class="sxs-lookup"><span data-stu-id="258bb-116">If you intend toouse hello VHD as-is toocreate a new VM, ensure hello following steps are completed.</span></span>  
    * <span data-ttu-id="258bb-117">[Voorbereiden van een Windows-VHD tooupload tooAzure](prepare-for-upload-vhd-image.md).</span><span class="sxs-lookup"><span data-stu-id="258bb-117">[Prepare a Windows VHD tooupload tooAzure](prepare-for-upload-vhd-image.md).</span></span> <span data-ttu-id="258bb-118">**Geen** generalize Hallo van virtuele machine met behulp van Sysprep.</span><span class="sxs-lookup"><span data-stu-id="258bb-118">**Do not** generalize hello VM using Sysprep.</span></span> 
    * <span data-ttu-id="258bb-119">Verwijder eventuele Gast virtualisatie-hulpprogramma's en de agents die zijn geïnstalleerd op Hallo VM (dat wil zeggen VMware tools).</span><span class="sxs-lookup"><span data-stu-id="258bb-119">Remove any guest virtualization tools and agents that are installed on hello VM (i.e. VMware tools).</span></span> 
    * <span data-ttu-id="258bb-120">Zorg ervoor dat Hallo VM geconfigureerde toopull is het IP-adres en DNS-instellingen via DHCP.</span><span class="sxs-lookup"><span data-stu-id="258bb-120">Ensure hello VM is configured toopull its IP address and DNS settings via DHCP.</span></span> <span data-ttu-id="258bb-121">Dit zorgt ervoor dat Hallo-server verkrijgt IP-adres binnen Hallo VNet wanneer deze opgestart wordt.</span><span class="sxs-lookup"><span data-stu-id="258bb-121">This ensures that hello server obtains an IP address within hello VNet when it starts up.</span></span>  


## <a name="export-and-download-hello-vhd"></a><span data-ttu-id="258bb-122">Exporteren en Hallo VHD downloaden</span><span class="sxs-lookup"><span data-stu-id="258bb-122">Export and download hello VHD</span></span> 

<span data-ttu-id="258bb-123">Hallo EC2 exemplaar tooa VHD in een Amazon S3-bucket exporteren.</span><span class="sxs-lookup"><span data-stu-id="258bb-123">Export hello EC2 instance tooa VHD in an Amazon S3 bucket.</span></span> <span data-ttu-id="258bb-124">Volg de stappen Hallo in Hallo Amazon-documentatie-onderwerp [exporteren van een exemplaar als een virtuele machine met behulp van virtuele machine importeren/exporteren](http://docs.aws.amazon.com/vm-import/latest/userguide/vmexport.html) en Voer Hallo [-exemplaar-export-taak maken](http://docs.aws.amazon.com/cli/latest/reference/ec2/create-instance-export-task.html) opdracht tooexport Hallo EC2 exemplaar tooa VHD-bestand.</span><span class="sxs-lookup"><span data-stu-id="258bb-124">Follow hello steps described in hello Amazon documentation topic [Exporting an Instance as a VM Using VM Import/Export](http://docs.aws.amazon.com/vm-import/latest/userguide/vmexport.html) and run hello [create-instance-export-task](http://docs.aws.amazon.com/cli/latest/reference/ec2/create-instance-export-task.html) command tooexport hello EC2 instance tooa VHD file.</span></span> 

<span data-ttu-id="258bb-125">Hallo wordt geëxporteerde VHD-bestand opgeslagen in Hallo Amazon S3-bucket die u opgeeft.</span><span class="sxs-lookup"><span data-stu-id="258bb-125">hello exported VHD file is saved in hello Amazon S3 bucket you specify.</span></span> <span data-ttu-id="258bb-126">Hallo basic syntaxis voor exporteren Hallo VHD lager is dan, vervangt Hallo tijdelijke aanduiding voor tekst in <brackets> met uw gegevens.</span><span class="sxs-lookup"><span data-stu-id="258bb-126">hello basic syntax for exporting hello VHD is below, just replace hello placeholder text in <brackets> with your information.</span></span>

```
aws ec2 create-instance-export-task --instance-id <instanceID> --target-environment Microsoft \
  --export-to-s3-task DiskImageFormat=VHD,ContainerFormat=ova,S3Bucket=<bucket>,S3Prefix=<prefix>
```

<span data-ttu-id="258bb-127">Eenmaal Hallo VHD geëxporteerd werden, volg de instructies Hallo in [hoe kan ik een Object downloaden van een S3-Bucket?](http://docs.aws.amazon.com/AmazonS3/latest/user-guide/download-objects.html) toodownload Hallo VHD-bestand van Hallo S3-bucket.</span><span class="sxs-lookup"><span data-stu-id="258bb-127">Once hello VHD has been exported, follow hello instructions in [How Do I Download an Object from an S3 Bucket?](http://docs.aws.amazon.com/AmazonS3/latest/user-guide/download-objects.html) toodownload hello VHD file from hello S3 bucket.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="258bb-128">AWS brengt gegevensoverdracht kosten voor het downloaden van Hallo VHD.</span><span class="sxs-lookup"><span data-stu-id="258bb-128">AWS charges data transfer fees for downloading hello VHD.</span></span> <span data-ttu-id="258bb-129">Zie [Amazon S3 prijzen](https://aws.amazon.com/s3/pricing/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="258bb-129">See [Amazon S3 Pricing](https://aws.amazon.com/s3/pricing/) for more information.</span></span>


## <a name="next-steps"></a><span data-ttu-id="258bb-130">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="258bb-130">Next steps</span></span>

<span data-ttu-id="258bb-131">U kunt nu Hallo VHD tooAzure uploaden en maken van een nieuwe virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="258bb-131">Now you can upload hello VHD tooAzure and create a new VM.</span></span> 

- <span data-ttu-id="258bb-132">Als u Sysprep uitgevoerd op de bron te**generalize** deze voordat u exporteert, Zie [een gegeneraliseerde VHD uploaden en toocreate een nieuwe virtuele machines in Azure gebruiken](upload-generalized-managed.md)</span><span class="sxs-lookup"><span data-stu-id="258bb-132">If you ran Sysprep on your source too**generalize** it before exporting, see [Upload a generalized VHD and use it toocreate a new VMs in Azure](upload-generalized-managed.md)</span></span>
- <span data-ttu-id="258bb-133">Als u niet Sysprep hebt uitgevoerd voordat u exporteert, hello VHD wordt beschouwd als **gespecialiseerde**, Zie [een gespecialiseerde VHD tooAzure uploaden en een nieuwe virtuele machine maken](create-vm-specialized.md)</span><span class="sxs-lookup"><span data-stu-id="258bb-133">If you did not run Sysprep before exporting, hello VHD is considered **specialized**, see [Upload a specialized VHD tooAzure and create a new VM](create-vm-specialized.md)</span></span>

 
