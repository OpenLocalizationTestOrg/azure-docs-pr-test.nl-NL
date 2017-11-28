---
title: MySQL-prestaties op Linux aaaOptimize | Microsoft Docs
description: Meer informatie over hoe toooptimize MySQL uitgevoerd op Azure een virtuele machine (VM) waarop Linux wordt uitgevoerd.
services: virtual-machines-linux
documentationcenter: 
author: NingKuang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 0c1c7fc5-a528-4d84-b65d-2df225f2233f
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: ningk
ms.openlocfilehash: 9e6458723233721e06f30b9de33635d403eefcba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-mysql-performance-on-azure-linux-vms"></a><span data-ttu-id="25724-103">MySQL-optimaliseren op Azure Linux VM 's</span><span class="sxs-lookup"><span data-stu-id="25724-103">Optimize MySQL Performance on Azure Linux VMs</span></span>
<span data-ttu-id="25724-104">Er zijn talloze factoren die van invloed op prestaties MySQL in Azure, zowel in de selectie van de virtuele hardware en softwareconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="25724-104">There are many factors that affect MySQL performance on Azure, both in virtual hardware selection and software configuration.</span></span> <span data-ttu-id="25724-105">Dit artikel is gericht op optimaliseren prestaties door middel van opslag-, systeem- en databaseconfiguraties.</span><span class="sxs-lookup"><span data-stu-id="25724-105">This article focuses on optimizing performance through storage, system, and database configurations.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="25724-106">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) en klassieke.</span><span class="sxs-lookup"><span data-stu-id="25724-106">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span></span> <span data-ttu-id="25724-107">In dit artikel wordt behandeld met het klassieke implementatiemodel Hallo.</span><span class="sxs-lookup"><span data-stu-id="25724-107">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="25724-108">Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="25724-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="25724-109">Zie voor meer informatie over Linux-VM-optimalisatie met Resource Manager-model Hallo [optimaliseren van uw Linux-VM op Azure](../optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="25724-109">For information about Linux VM optimizations with hello Resource Manager model, see [Optimize your Linux VM on Azure](../optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="utilize-raid-on-an-azure-virtual-machine"></a><span data-ttu-id="25724-110">Gebruikmaken van RAID op een virtuele machine van Azure</span><span class="sxs-lookup"><span data-stu-id="25724-110">Utilize RAID on an Azure virtual machine</span></span>
<span data-ttu-id="25724-111">Opslag is Hallo van groot belang dat betrekking heeft op de prestaties van de database in cloudomgevingen.</span><span class="sxs-lookup"><span data-stu-id="25724-111">Storage is hello key factor that affects database performance in cloud environments.</span></span> <span data-ttu-id="25724-112">Enkele schijf vergeleken tooa RAID kan sneller toegang via Gelijktijdigheidsfout bieden.</span><span class="sxs-lookup"><span data-stu-id="25724-112">Compared tooa single disk, RAID can provide faster access via concurrency.</span></span> <span data-ttu-id="25724-113">Zie voor meer informatie [standaard RAID-niveaus](http://en.wikipedia.org/wiki/Standard_RAID_levels).</span><span class="sxs-lookup"><span data-stu-id="25724-113">For more information, see [Standard RAID levels](http://en.wikipedia.org/wiki/Standard_RAID_levels).</span></span>   

<span data-ttu-id="25724-114">-I/o-schijfdoorvoer en i/o-reactietijd in Azure kunnen worden verbeterd via RAID.</span><span class="sxs-lookup"><span data-stu-id="25724-114">Disk I/O throughput and I/O response time in Azure can be improved through RAID.</span></span> <span data-ttu-id="25724-115">Onze tests lab ziet u dat-i/o-schijfdoorvoer kan worden verdubbeld en i/o-reactietijd kan worden verkleind door helft gemiddeld wanneer verdubbeld Hallo aantal RAID-schijven (van toofour twee, vier tooeight, enzovoort).</span><span class="sxs-lookup"><span data-stu-id="25724-115">Our lab tests show that disk I/O throughput can be doubled and I/O response time can be reduced by half on average when hello number of RAID disks is doubled (from two toofour, four tooeight, etc.).</span></span> <span data-ttu-id="25724-116">Zie [bijlage A](#AppendixA) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="25724-116">See [Appendix A](#AppendixA) for details.</span></span>  

<span data-ttu-id="25724-117">Bovendien toodisk i/o, MySQL prestaties worden verbeterd als u Hallo RAID-niveau verhogen.</span><span class="sxs-lookup"><span data-stu-id="25724-117">In addition toodisk I/O, MySQL performance improves when you increase hello RAID level.</span></span>  <span data-ttu-id="25724-118">Zie [bijlage B](#AppendixB) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="25724-118">See [Appendix B](#AppendixB) for details.</span></span>  

<span data-ttu-id="25724-119">U kunt ook tooconsider Hallo chunkgrootte.</span><span class="sxs-lookup"><span data-stu-id="25724-119">You might also want tooconsider hello chunk size.</span></span> <span data-ttu-id="25724-120">In het algemeen als u een grotere chunkgrootte hebt, krijgt u lagere overhead, met name voor grote schrijfbewerkingen.</span><span class="sxs-lookup"><span data-stu-id="25724-120">In general, when you have a larger chunk size, you get lower overhead, especially for large writes.</span></span> <span data-ttu-id="25724-121">Wanneer de chunkgrootte hello te groot is, kan deze extra overhead die voorkomen dat u profiteert van RAID toevoegen.</span><span class="sxs-lookup"><span data-stu-id="25724-121">However, when hello chunk size is too large, it might add additional overhead that prevents you from taking advantage of RAID.</span></span> <span data-ttu-id="25724-122">de huidige standaardgrootte Hallo is 512 KB bewezen wordt toobe optimaal is voor de meest algemene productieomgevingen.</span><span class="sxs-lookup"><span data-stu-id="25724-122">hello current default size is 512 KB, which is proven toobe optimal for most general production environments.</span></span> <span data-ttu-id="25724-123">Zie [bijlage C](#AppendixC) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="25724-123">See [Appendix C](#AppendixC) for details.</span></span>   

<span data-ttu-id="25724-124">Er gelden beperkingen op hoeveel schijven die u voor andere virtuele machine-typen kunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="25724-124">There are limits on how many disks you can add for different virtual machine types.</span></span> <span data-ttu-id="25724-125">Deze limieten zijn aangegeven in [grootten voor virtuele machine en cloud-service voor Azure](http://msdn.microsoft.com/library/azure/dn197896.aspx).</span><span class="sxs-lookup"><span data-stu-id="25724-125">These limits are detailed in [Virtual machine and cloud service sizes for Azure](http://msdn.microsoft.com/library/azure/dn197896.aspx).</span></span> <span data-ttu-id="25724-126">U moet vier bijgesloten gegevens schijven toofollow Hallo RAID voorbeeld in dit artikel, hoewel u tooset van RAID met minder schijven kunt kiezen.</span><span class="sxs-lookup"><span data-stu-id="25724-126">You will need four attached data disks toofollow hello RAID example in this article, although you can choose tooset up RAID with fewer disks.</span></span>  

<span data-ttu-id="25724-127">In dit artikel wordt ervan uitgegaan dat u al een virtuele Linux-machine hebt gemaakt en hebben MYSQL geïnstalleerd en geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="25724-127">This article assumes you have already created a Linux virtual machine and have MYSQL installed and configured.</span></span> <span data-ttu-id="25724-128">Zie voor meer informatie over aan de slag, hoe tooinstall MySQL in Azure.</span><span class="sxs-lookup"><span data-stu-id="25724-128">For more information on getting started, see How tooinstall MySQL on Azure.</span></span>  

### <a name="set-up-raid-on-azure"></a><span data-ttu-id="25724-129">Instellen van RAID op Azure</span><span class="sxs-lookup"><span data-stu-id="25724-129">Set up RAID on Azure</span></span>
<span data-ttu-id="25724-130">Hallo volgende stappen laten zien hoe toocreate RAID op Azure met behulp van hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="25724-130">hello following steps show how toocreate RAID on Azure by using hello Azure portal.</span></span> <span data-ttu-id="25724-131">U kunt ook RAID instellen met behulp van Windows PowerShell-scripts.</span><span class="sxs-lookup"><span data-stu-id="25724-131">You can also set up RAID by using Windows PowerShell scripts.</span></span>
<span data-ttu-id="25724-132">In dit voorbeeld configureert we RAID 0 met vier schijven.</span><span class="sxs-lookup"><span data-stu-id="25724-132">In this example, we will configure RAID 0 with four disks.</span></span>  

#### <a name="add-a-data-disk-tooyour-virtual-machine"></a><span data-ttu-id="25724-133">Een data schijf tooyour virtuele machine toevoegen</span><span class="sxs-lookup"><span data-stu-id="25724-133">Add a data disk tooyour virtual machine</span></span>
<span data-ttu-id="25724-134">In hello Azure-portal, gaat u toohello dashboard en selecteer Hallo virtuele machine toowhich gewenste tooadd een gegevensschijf.</span><span class="sxs-lookup"><span data-stu-id="25724-134">In hello Azure portal, go toohello dashboard and select hello virtual machine toowhich you want tooadd a data disk.</span></span> <span data-ttu-id="25724-135">In dit voorbeeld is Hallo virtuele machine mysqlnode1.</span><span class="sxs-lookup"><span data-stu-id="25724-135">In this example, hello virtual machine is mysqlnode1.</span></span>  

<!--![Virtual machines][1]-->

<span data-ttu-id="25724-136">Klik op **schijven** en klik vervolgens op **nieuwe koppelen**.</span><span class="sxs-lookup"><span data-stu-id="25724-136">Click **Disks** and then click **Attach New**.</span></span>

![Virtuele machines toevoegen schijf](media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-Disks-option.png)

<span data-ttu-id="25724-138">Maak een nieuwe schijf van 500 GB.</span><span class="sxs-lookup"><span data-stu-id="25724-138">Create a new 500 GB disk.</span></span> <span data-ttu-id="25724-139">Zorg ervoor dat **Host Cache voorkeur** te is ingesteld,**geen**.</span><span class="sxs-lookup"><span data-stu-id="25724-139">Make sure that **Host Cache Preference** is set too**None**.</span></span>  <span data-ttu-id="25724-140">Wanneer u klaar bent, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="25724-140">When you're finished, click **OK**.</span></span>

![Lege schijf koppelen](media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-attach-empty-disk.png)


<span data-ttu-id="25724-142">Hiermee wordt een lege schijf in uw virtuele machine toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="25724-142">This adds one empty disk into your virtual machine.</span></span> <span data-ttu-id="25724-143">Herhaal deze stap drie keer zodat er vier gegevensschijven voor RAID.</span><span class="sxs-lookup"><span data-stu-id="25724-143">Repeat this step three more times so that you have four data disks for RAID.</span></span>  

<span data-ttu-id="25724-144">U kunt zien Hallo toegevoegd stations in Hallo virtuele machine door te kijken Hallo kernel berichtenlogboek.</span><span class="sxs-lookup"><span data-stu-id="25724-144">You can see hello added drives in hello virtual machine by looking at hello kernel message log.</span></span> <span data-ttu-id="25724-145">Bijvoorbeeld: toosee op Ubuntu, gebruik Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="25724-145">For example, toosee this on Ubuntu, use hello following command:</span></span>  

    sudo grep SCSI /var/log/dmesg

#### <a name="create-raid-with-hello-additional-disks"></a><span data-ttu-id="25724-146">RAID Hello extra schijven maken</span><span class="sxs-lookup"><span data-stu-id="25724-146">Create RAID with hello additional disks</span></span>
<span data-ttu-id="25724-147">Hallo volgende stappen wordt beschreven hoe te[configureren van software-RAID op Linux](../configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="25724-147">hello following steps describe how too[configure software RAID on Linux](../configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

> [!NOTE]
> <span data-ttu-id="25724-148">Als u van Hallo XFS bestandssysteem gebruikmaakt, uitvoeren Hallo stappen te volgen nadat u RAID hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="25724-148">If you are using hello XFS file system, execute hello following steps after you have created RAID.</span></span>
>
>

<span data-ttu-id="25724-149">tooinstall XFS op Debian, Ubuntu of Linux-munt gebruik Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="25724-149">tooinstall XFS on Debian, Ubuntu, or Linux Mint, use hello following command:</span></span>  

    apt-get -y install xfsprogs  

<span data-ttu-id="25724-150">tooinstall XFS op Fedora, CentOS of RHEL, gebruik Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="25724-150">tooinstall XFS on Fedora, CentOS, or RHEL, use hello following command:</span></span>  

    yum -y install xfsprogs  xfsdump


#### <a name="set-up-a-new-storage-path"></a><span data-ttu-id="25724-151">Een nieuw opslagpad instellen</span><span class="sxs-lookup"><span data-stu-id="25724-151">Set up a new storage path</span></span>
<span data-ttu-id="25724-152">Gebruik Hallo opdracht tooset van een nieuw opslagpad te volgen:</span><span class="sxs-lookup"><span data-stu-id="25724-152">Use hello following command tooset up a new storage path:</span></span>  

    root@mysqlnode1:~# mkdir -p /RAID0/mysql

#### <a name="copy-hello-original-data-toohello-new-storage-path"></a><span data-ttu-id="25724-153">Hallo oorspronkelijke toohello nieuwe opslag gegevenspad kopiëren</span><span class="sxs-lookup"><span data-stu-id="25724-153">Copy hello original data toohello new storage path</span></span>
<span data-ttu-id="25724-154">Hallo opdracht toocopy toohello nieuwe opslag gegevenspad volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="25724-154">Use hello following command toocopy data toohello new storage path:</span></span>  

    root@mysqlnode1:~# cp -rp /var/lib/mysql/* /RAID0/mysql/

#### <a name="modify-permissions-so-mysql-can-access-read-and-write-hello-data-disk"></a><span data-ttu-id="25724-155">(Lezen en schrijven) zodat MySQL toegang heeft tot wijzigingsmachtiging Hallo gegevensschijf</span><span class="sxs-lookup"><span data-stu-id="25724-155">Modify permissions so MySQL can access (read and write) hello data disk</span></span>
<span data-ttu-id="25724-156">Hallo volgende opdracht toomodify machtigingen gebruiken:</span><span class="sxs-lookup"><span data-stu-id="25724-156">Use hello following command toomodify permissions:</span></span>  

    root@mysqlnode1:~# chown -R mysql.mysql /RAID0/mysql && chmod -R 755 /RAID0/mysql


## <a name="adjust-hello-disk-io-scheduling-algorithm"></a><span data-ttu-id="25724-157">Hallo schijf-i/o algoritme planning aanpassen</span><span class="sxs-lookup"><span data-stu-id="25724-157">Adjust hello disk I/O scheduling algorithm</span></span>
<span data-ttu-id="25724-158">Linux implementeert vier typen i/o algoritmen plannen:</span><span class="sxs-lookup"><span data-stu-id="25724-158">Linux implements four types of I/O scheduling algorithms:</span></span>  

* <span data-ttu-id="25724-159">Nooperation-algoritme (Er is geen bewerking)</span><span class="sxs-lookup"><span data-stu-id="25724-159">NOOP algorithm (No Operation)</span></span>
* <span data-ttu-id="25724-160">Deadline-algoritme (Deadline)</span><span class="sxs-lookup"><span data-stu-id="25724-160">Deadline algorithm (Deadline)</span></span>
* <span data-ttu-id="25724-161">Volledig evenredige Queuing-algoritme (CFQ)</span><span class="sxs-lookup"><span data-stu-id="25724-161">Completely fair queuing algorithm (CFQ)</span></span>
* <span data-ttu-id="25724-162">Periode budget-algoritme (Anticipatory)</span><span class="sxs-lookup"><span data-stu-id="25724-162">Budget period algorithm (Anticipatory)</span></span>  

<span data-ttu-id="25724-163">U kunt verschillende i/o-planners onder verschillende scenario's toooptimize prestaties selecteren.</span><span class="sxs-lookup"><span data-stu-id="25724-163">You can select different I/O schedulers under different scenarios toooptimize performance.</span></span> <span data-ttu-id="25724-164">In een omgeving met volledig willekeurige toegang is er een belangrijk verschil tussen Hallo CFQ en Deadline algoritmen voor prestaties.</span><span class="sxs-lookup"><span data-stu-id="25724-164">In a completely random access environment, there is not a significant difference between hello CFQ and Deadline algorithms for performance.</span></span> <span data-ttu-id="25724-165">Het is raadzaam dat u Hallo MySQL-database omgeving tooDeadline voor stabiliteit ingesteld.</span><span class="sxs-lookup"><span data-stu-id="25724-165">We recommend that you set hello MySQL database environment tooDeadline for stability.</span></span> <span data-ttu-id="25724-166">Als er een groot aantal opeenvolgende i/o, mogelijk CFQ schijf-i/o-prestaties verminderen.</span><span class="sxs-lookup"><span data-stu-id="25724-166">If there is a lot of sequential I/O, CFQ might reduce disk I/O performance.</span></span>   

<span data-ttu-id="25724-167">Voor de SSD- en andere apparatuur bereiken Nooperation of Deadline betere prestaties dan Hallo standaard scheduler.</span><span class="sxs-lookup"><span data-stu-id="25724-167">For SSD and other equipment, NOOP or Deadline can achieve better performance than hello default scheduler.</span></span>   

<span data-ttu-id="25724-168">Eerdere toohello kernel 2.5, Hallo standaard i/o planning algoritme is een Deadline.</span><span class="sxs-lookup"><span data-stu-id="25724-168">Prior toohello kernel 2.5, hello default I/O scheduling algorithm is Deadline.</span></span> <span data-ttu-id="25724-169">Beginnen met Hallo kernel 2.6.18, werd CFQ Hallo i/o-planning standaardalgoritme.</span><span class="sxs-lookup"><span data-stu-id="25724-169">Starting with hello kernel 2.6.18, CFQ became hello default I/O scheduling algorithm.</span></span>  <span data-ttu-id="25724-170">U kunt deze instelling tijdens het opstarten van de kernel opgeven of deze instelling dynamisch te wijzigen wanneer Hallo-systeem wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="25724-170">You can specify this setting at kernel boot time or dynamically modify this setting when hello system is running.</span></span>  

<span data-ttu-id="25724-171">Hallo volgende voorbeeld laat zien hoe Hallo scheduler toohello Nooperation standaardalgoritme in Hallo Debian distributie familie toocheck en set.</span><span class="sxs-lookup"><span data-stu-id="25724-171">hello following example demonstrates how toocheck and set hello default scheduler toohello NOOP algorithm in hello Debian distribution family.</span></span>  

### <a name="view-hello-current-io-scheduler"></a><span data-ttu-id="25724-172">Weergave Hallo huidige i/o-planner</span><span class="sxs-lookup"><span data-stu-id="25724-172">View hello current I/O scheduler</span></span>
<span data-ttu-id="25724-173">tooview hello scheduler Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="25724-173">tooview hello scheduler run hello following command:</span></span>  

    root@mysqlnode1:~# cat /sys/block/sda/queue/scheduler

<span data-ttu-id="25724-174">Ziet u uitvoer, waarmee wordt aangegeven van de huidige Taakplanner hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="25724-174">You will see following output, which indicates hello current scheduler:</span></span>  

    noop [deadline] cfq


### <a name="change-hello-current-device-devsda-of-hello-io-scheduling-algorithm"></a><span data-ttu-id="25724-175">Wijzigen in een huidige Hallo-apparaat (/ dev/sda) van planning Hallo i/o-algoritme</span><span class="sxs-lookup"><span data-stu-id="25724-175">Change hello current device (/dev/sda) of hello I/O scheduling algorithm</span></span>
<span data-ttu-id="25724-176">Voer Hallo opdrachten toochange Hallo huidige apparaat te volgen:</span><span class="sxs-lookup"><span data-stu-id="25724-176">Run hello following commands toochange hello current device:</span></span>  

    azureuser@mysqlnode1:~$ sudo su -
    root@mysqlnode1:~# echo "noop" >/sys/block/sda/queue/scheduler
    root@mysqlnode1:~# sed -i 's/GRUB_CMDLINE_LINUX=""/GRUB_CMDLINE_LINUX_DEFAULT="quiet splash elevator=noop"/g' /etc/default/grub
    root@mysqlnode1:~# update-grub

> [!NOTE]
> <span data-ttu-id="25724-177">Instellen van dit voor /dev/sda zichzelf is niet handig.</span><span class="sxs-lookup"><span data-stu-id="25724-177">Setting this for /dev/sda alone is not useful.</span></span> <span data-ttu-id="25724-178">Deze moet worden ingesteld op alle gegevensschijven waar Hallo-database zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="25724-178">It must be set on all data disks where hello database resides.</span></span>  
>
>

<span data-ttu-id="25724-179">U ziet Hallo volgende uitvoer, die aangeeft dat grub.cfg met succes is opnieuw opgebouwd en die standaard Hallo scheduler is bijgewerkte tooNOOP:</span><span class="sxs-lookup"><span data-stu-id="25724-179">You should see hello following output, indicating that grub.cfg has been rebuilt successfully and that hello default scheduler has been updated tooNOOP:</span></span>  

    Generating grub configuration file ...
    Found linux image: /boot/vmlinuz-3.13.0-34-generic
    Found initrd image: /boot/initrd.img-3.13.0-34-generic
    Found linux image: /boot/vmlinuz-3.13.0-32-generic
    Found initrd image: /boot/initrd.img-3.13.0-32-generic
    Found memtest86+ image: /memtest86+.elf
    Found memtest86+ image: /memtest86+.bin
    done

<span data-ttu-id="25724-180">Voor Hallo Red Hat distributie familie, moet u alleen Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="25724-180">For hello Red Hat distribution family, you need only hello following command:</span></span>

    echo 'echo noop >/sys/block/sda/queue/scheduler' >> /etc/rc.local

## <a name="configure-system-file-operations-settings"></a><span data-ttu-id="25724-181">Bewerkingen van de systeeminstellingen-bestand configureren</span><span class="sxs-lookup"><span data-stu-id="25724-181">Configure system file operations settings</span></span>
<span data-ttu-id="25724-182">Een aanbevolen procedure is toodisable hello *atime* functie voor logboekregistratie op Hallo-bestandssysteem.</span><span class="sxs-lookup"><span data-stu-id="25724-182">One best practice is toodisable hello *atime* logging feature on hello file system.</span></span> <span data-ttu-id="25724-183">Atime is hello bestandstijd van laatste.</span><span class="sxs-lookup"><span data-stu-id="25724-183">Atime is hello last file access time.</span></span> <span data-ttu-id="25724-184">Wanneer een bestand wordt geopend, Hallo Hallo system bestandsrecords tijdstempel in Hallo logboek.</span><span class="sxs-lookup"><span data-stu-id="25724-184">Whenever a file is accessed, hello file system records hello timestamp in hello log.</span></span> <span data-ttu-id="25724-185">Deze informatie wordt echter zelden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="25724-185">However, this information is rarely used.</span></span> <span data-ttu-id="25724-186">U kunt deze uitschakelen als u niet nodig hebt, waarmee algehele schijftijd toegang wordt beperkt.</span><span class="sxs-lookup"><span data-stu-id="25724-186">You can disable it if you don't need it, which will reduce overall disk access time.</span></span>  

<span data-ttu-id="25724-187">toodisable atime aan te melden, u moet toomodify Hallo bestand system configuratie bestand /etc/ bevinden fstab en Hallo toevoegen **noatime** optie.</span><span class="sxs-lookup"><span data-stu-id="25724-187">toodisable atime logging, you need toomodify hello file system configuration file /etc/ fstab and add hello **noatime** option.</span></span>  

<span data-ttu-id="25724-188">Bijvoorbeeld, bewerk Hallo vim /etc/fstab bestand, toe te voegen Hallo noatime, zoals wordt weergegeven in Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="25724-188">For example, edit hello vim /etc/fstab file, adding hello noatime as shown in hello following sample:</span></span>  

    # CLOUD_IMG: This file was created/modified by hello Cloud Image build process
    UUID=3cc98c06-d649-432d-81df-6dcd2a584d41       /        ext4   defaults,discard        0 0
    #Add hello “noatime” option below toodisable atime logging
    UUID="431b1e78-8226-43ec-9460-514a9adf060e"     /RAID0   xfs   defaults,nobootwait, noatime 0 0
    /dev/sdb1       /mnt    auto    defaults,nobootwait,comment=cloudconfig 0       2

<span data-ttu-id="25724-189">Vervolgens opnieuw koppelen Hallo bestandssysteem Hello volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="25724-189">Then, remount hello file system with hello following command:</span></span>  

    mount -o remount /RAID0

<span data-ttu-id="25724-190">Test Hallo gewijzigd resultaat.</span><span class="sxs-lookup"><span data-stu-id="25724-190">Test hello modified result.</span></span> <span data-ttu-id="25724-191">Wanneer u het testbestand Hallo wijzigt, wordt Hallo tijd niet bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="25724-191">When you modify hello test file, hello access time is not updated.</span></span> <span data-ttu-id="25724-192">Hallo volgen voorbeelden kunt u zien welke Hallo code ziet er vóór en na wijziging.</span><span class="sxs-lookup"><span data-stu-id="25724-192">hello following examples show what hello code looks like before and after modification.</span></span>

<span data-ttu-id="25724-193">Voor:</span><span class="sxs-lookup"><span data-stu-id="25724-193">Before:</span></span>        

![Code voordat toegang werd gewijzigd][5]

<span data-ttu-id="25724-195">Na:</span><span class="sxs-lookup"><span data-stu-id="25724-195">After:</span></span>

![Code na wijziging toegang][6]

## <a name="increase-hello-maximum-number-of-system-handles-for-high-concurrency"></a><span data-ttu-id="25724-197">Maximum aantal ingangen voor hoge gelijktijdigheid system Hallo vergroten</span><span class="sxs-lookup"><span data-stu-id="25724-197">Increase hello maximum number of system handles for high concurrency</span></span>
<span data-ttu-id="25724-198">MySQL is een database hoge gelijktijdigheid van taken.</span><span class="sxs-lookup"><span data-stu-id="25724-198">MySQL is a high concurrency database.</span></span> <span data-ttu-id="25724-199">Hallo standaardaantal gelijktijdige ingangen is 1024 voor Linux, die niet altijd voldoende.</span><span class="sxs-lookup"><span data-stu-id="25724-199">hello default number of concurrent handles is 1024 for Linux, which is not always sufficient.</span></span> <span data-ttu-id="25724-200">Volgende stappen tooincrease Hallo maximum aantal gelijktijdige ingangen van Hallo system toosupport hoge gelijktijdigheid van MySQL hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="25724-200">Use hello following steps tooincrease hello maximum concurrent handles of hello system toosupport high concurrency of MySQL.</span></span>

### <a name="modify-hello-limitsconf-file"></a><span data-ttu-id="25724-201">Hallo limits.conf bestand wijzigen</span><span class="sxs-lookup"><span data-stu-id="25724-201">Modify hello limits.conf file</span></span>
<span data-ttu-id="25724-202">tooincrease hello maximum aantal gelijktijdige ingangen toegestaan, Hallo volgende vier regels in Hallo /etc/security/limits.conf bestand toevoegen.</span><span class="sxs-lookup"><span data-stu-id="25724-202">tooincrease hello maximum allowed concurrent handles, add hello following four lines in hello /etc/security/limits.conf file.</span></span> <span data-ttu-id="25724-203">Houd er rekening mee dat 65536 Hallo maximumaantal die Hallo-systeem kan ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="25724-203">Note that 65536 is hello maximum number that hello system can support.</span></span>   

    * <span data-ttu-id="25724-204">voorlopig nofile 65536</span><span class="sxs-lookup"><span data-stu-id="25724-204">soft nofile 65536</span></span>
    * <span data-ttu-id="25724-205">vaste nofile 65536</span><span class="sxs-lookup"><span data-stu-id="25724-205">hard nofile 65536</span></span>
    * <span data-ttu-id="25724-206">voorlopig nproc 65536</span><span class="sxs-lookup"><span data-stu-id="25724-206">soft nproc 65536</span></span>
    * <span data-ttu-id="25724-207">vaste nproc 65536</span><span class="sxs-lookup"><span data-stu-id="25724-207">hard nproc 65536</span></span>

### <a name="update-hello-system-for-hello-new-limits"></a><span data-ttu-id="25724-208">Hallo-systeem voor nieuwe Hallo-beperkingen bijwerken</span><span class="sxs-lookup"><span data-stu-id="25724-208">Update hello system for hello new limits</span></span>
<span data-ttu-id="25724-209">tooupdate hello systeem, Hallo volgende opdrachten uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="25724-209">tooupdate hello system, run hello following commands:</span></span>  

    ulimit -SHn 65536
    ulimit -SHu 65536

### <a name="ensure-that-hello-limits-are-updated-at-boot-time"></a><span data-ttu-id="25724-210">Zorg ervoor dat de Hallo limieten tijdens het opstarten zijn bijgewerkt</span><span class="sxs-lookup"><span data-stu-id="25724-210">Ensure that hello limits are updated at boot time</span></span>
<span data-ttu-id="25724-211">Starten van de opdrachten in Hallo /etc/rc.local bestand volgen zodat deze van tijdens het opstarten kracht wordt Hallo geplaatst.</span><span class="sxs-lookup"><span data-stu-id="25724-211">Put hello following startup commands in hello /etc/rc.local file so it will take effect at boot time.</span></span>  

    echo “ulimit -SHn 65536” >>/etc/rc.local
    echo “ulimit -SHu 65536” >>/etc/rc.local

## <a name="mysql-database-optimization"></a><span data-ttu-id="25724-212">Optimalisatie van MySQL-database</span><span class="sxs-lookup"><span data-stu-id="25724-212">MySQL database optimization</span></span>
<span data-ttu-id="25724-213">tooconfigure MySQL in Azure, kunt u dezelfde prestaties afstemmen strategie u op een on-premises machine gebruiken Hallo.</span><span class="sxs-lookup"><span data-stu-id="25724-213">tooconfigure MySQL on Azure, you can use hello same performance-tuning strategy you use on an on-premises machine.</span></span>  

<span data-ttu-id="25724-214">Hallo belangrijkste i/o-optimalisatie regels zijn:</span><span class="sxs-lookup"><span data-stu-id="25724-214">hello main I/O optimization rules are:</span></span>   

* <span data-ttu-id="25724-215">Hallo-cachegrootte verhogen.</span><span class="sxs-lookup"><span data-stu-id="25724-215">Increase hello cache size.</span></span>
* <span data-ttu-id="25724-216">I/o-reactietijd verminderen.</span><span class="sxs-lookup"><span data-stu-id="25724-216">Reduce I/O response time.</span></span>  

<span data-ttu-id="25724-217">toooptimize MySQL-serverinstellingen, kunt u Hallo my.cnf bestand Hallo standaardconfiguratiebestand voor server en clientcomputers bijwerken.</span><span class="sxs-lookup"><span data-stu-id="25724-217">toooptimize MySQL server settings, you can update hello my.cnf file, which is hello default configuration file for both server and client computers.</span></span>  

<span data-ttu-id="25724-218">Hallo zijn volgende configuratie-items Hallo belangrijkste factoren die van invloed op prestaties MySQL:</span><span class="sxs-lookup"><span data-stu-id="25724-218">hello following configuration items are hello main factors that affect MySQL performance:</span></span>  

* <span data-ttu-id="25724-219">**innodb_buffer_pool_size**: Hallo buffergroep buffer opgeslagen gegevens en Hallo index bevat.</span><span class="sxs-lookup"><span data-stu-id="25724-219">**innodb_buffer_pool_size**: hello buffer pool contains buffered data and hello index.</span></span> <span data-ttu-id="25724-220">Dit wordt meestal ingesteld too70 procent van het fysieke geheugen.</span><span class="sxs-lookup"><span data-stu-id="25724-220">This is usually set too70 percent of physical memory.</span></span>
* <span data-ttu-id="25724-221">**innodb_log_file_size**: dit Hallo opnieuw logboekgrootte is.</span><span class="sxs-lookup"><span data-stu-id="25724-221">**innodb_log_file_size**: This is hello redo log size.</span></span> <span data-ttu-id="25724-222">U opnieuw logboeken tooensure dat schrijfbewerkingen snelle, betrouwbare en hersteld na een crash zijn.</span><span class="sxs-lookup"><span data-stu-id="25724-222">You use redo logs tooensure that write operations are fast, reliable, and recoverable after a crash.</span></span> <span data-ttu-id="25724-223">Deze wordt too512 MB, zodat u voldoende ruimte voor het registreren van schrijfbewerkingen ingesteld.</span><span class="sxs-lookup"><span data-stu-id="25724-223">This is set too512 MB, which will give you plenty of space for logging write operations.</span></span>
* <span data-ttu-id="25724-224">**max_connections**: soms toepassingen niet sluiten verbindingen goed.</span><span class="sxs-lookup"><span data-stu-id="25724-224">**max_connections**: Sometimes applications do not close connections properly.</span></span> <span data-ttu-id="25724-225">Een hogere waarde geeft Hallo server meer tijd toorecycle inactief sinds verbindingen.</span><span class="sxs-lookup"><span data-stu-id="25724-225">A larger value will give hello server more time toorecycle idled connections.</span></span> <span data-ttu-id="25724-226">Hallo kunt u het maximum aantal verbindingen is 10.000, maar Hallo aanbevolen maximaal 5.000 is.</span><span class="sxs-lookup"><span data-stu-id="25724-226">hello maximum number of connections is 10,000, but hello recommended maximum is 5,000.</span></span>
* <span data-ttu-id="25724-227">**Innodb_file_per_table**: deze instelling Hiermee schakelt u of de mogelijkheid Hallo van InnoDB toostore tabellen in afzonderlijke bestanden.</span><span class="sxs-lookup"><span data-stu-id="25724-227">**Innodb_file_per_table**: This setting enables or disables hello ability of InnoDB toostore tables in separate files.</span></span> <span data-ttu-id="25724-228">Schakel Hallo optie tooensure dat verschillende geavanceerde beheerbewerkingen efficiënt kunnen worden toegepast.</span><span class="sxs-lookup"><span data-stu-id="25724-228">Turn on hello option tooensure that several advanced administration operations can be applied efficiently.</span></span> <span data-ttu-id="25724-229">Uit oogpunt van prestaties kan het versnellen Hallo tabel ruimte verzending en Hallo opgeruimd management prestaties te optimaliseren.</span><span class="sxs-lookup"><span data-stu-id="25724-229">From a performance point of view, it can speed up hello table space transmission and optimize hello debris management performance.</span></span> <span data-ttu-id="25724-230">Hallo aanbevolen instelling voor deze optie is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="25724-230">hello recommended setting for this option is ON.</span></span></br></br>
<span data-ttu-id="25724-231">Hallo standaardinstelling is ingeschakeld, van MySQL 5.6, dus er is geen actie vereist.</span><span class="sxs-lookup"><span data-stu-id="25724-231">From MySQL 5.6, hello default setting is ON, so no action is required.</span></span> <span data-ttu-id="25724-232">Voor eerdere versies is de standaardinstelling Hallo uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="25724-232">For earlier versions, hello default setting is OFF.</span></span> <span data-ttu-id="25724-233">Hallo-instelling moet worden gewijzigd voordat gegevens worden geladen, omdat alleen de zojuist gemaakte tabellen worden getroffen.</span><span class="sxs-lookup"><span data-stu-id="25724-233">hello setting should be changed before data is loaded, because only newly created tables are affected.</span></span>
* <span data-ttu-id="25724-234">**innodb_flush_log_at_trx_commit**: Hallo standaardwaarde is 1, hello bereik too0 stelt ~ 2.</span><span class="sxs-lookup"><span data-stu-id="25724-234">**innodb_flush_log_at_trx_commit**: hello default value is 1, with hello scope set too0~2.</span></span> <span data-ttu-id="25724-235">Hallo-standaardwaarde is de meest geschikte optie Hallo zelfstandig MySQL-database.</span><span class="sxs-lookup"><span data-stu-id="25724-235">hello default value is hello most suitable option for standalone MySQL DB.</span></span> <span data-ttu-id="25724-236">Hallo-instelling van 2 schakelt Hallo meeste gegevensintegriteit en geschikt is voor het model in de MySQL-Cluster.</span><span class="sxs-lookup"><span data-stu-id="25724-236">hello setting of 2 enables hello most data integrity and is suitable for Master in MySQL Cluster.</span></span> <span data-ttu-id="25724-237">Hallo-instelling van 0 kan verlies van gegevens die invloed kan zijn op de betrouwbaarheid (in sommige gevallen met betere prestaties) en is geschikt voor Slave in MySQL-Cluster.</span><span class="sxs-lookup"><span data-stu-id="25724-237">hello setting of 0 allows data loss, which can affect reliability (in some cases with better performance), and is suitable for Slave in MySQL Cluster.</span></span>
* <span data-ttu-id="25724-238">**Innodb_log_buffer_size**: Hallo logboekbuffer kan transacties toorun zonder tooflush Hallo logboek toodisk voordat Hallo transacties doorvoeren.</span><span class="sxs-lookup"><span data-stu-id="25724-238">**Innodb_log_buffer_size**: hello log buffer allows transactions toorun without having tooflush hello log toodisk before hello transactions commit.</span></span> <span data-ttu-id="25724-239">Als er grote binaire object of tekstveld, Hallo cache snel worden gebruikt en regelmatig schijf-i/o wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="25724-239">However, if there is large binary object or text field, hello cache will be consumed quickly and frequent disk I/O will be triggered.</span></span> <span data-ttu-id="25724-240">Het is beter Hallo buffergrootte verhogen als Innodb_log_waits status variabele niet is 0.</span><span class="sxs-lookup"><span data-stu-id="25724-240">It is better increase hello buffer size if Innodb_log_waits state variable is not 0.</span></span>
* <span data-ttu-id="25724-241">**query_cache_size**: de beste optie Hallo is toodisable op Hallo begin.</span><span class="sxs-lookup"><span data-stu-id="25724-241">**query_cache_size**: hello best option is toodisable it from hello outset.</span></span> <span data-ttu-id="25724-242">Query_cache_size too0 (dit is de standaardinstelling Hallo in MySQL 5.6) en andere toospeed methoden om query's gebruikt.</span><span class="sxs-lookup"><span data-stu-id="25724-242">Set query_cache_size too0 (this is hello default setting in MySQL 5.6) and use other methods toospeed up queries.</span></span>  

<span data-ttu-id="25724-243">Zie [bijlage D](#AppendixD) voor een vergelijking van de prestaties voor en na Hallo optimalisatie.</span><span class="sxs-lookup"><span data-stu-id="25724-243">See [Appendix D](#AppendixD) for a comparison of performance before and after hello optimization.</span></span>

## <a name="turn-on-hello-mysql-slow-query-log-for-analyzing-hello-performance-bottleneck"></a><span data-ttu-id="25724-244">Hallo MySQL trage querylogboek voor het analyseren van het prestatieknelpunt Hallo inschakelen</span><span class="sxs-lookup"><span data-stu-id="25724-244">Turn on hello MySQL slow query log for analyzing hello performance bottleneck</span></span>
<span data-ttu-id="25724-245">Hallo MySQL trage querylogboek kunt u trage Hallo-query's voor MySQL identificeren.</span><span class="sxs-lookup"><span data-stu-id="25724-245">hello MySQL slow query log can help you identify hello slow queries for MySQL.</span></span> <span data-ttu-id="25724-246">Nadat de Hallo MySQL trage query-logboek is ingeschakeld, kunt u MySQL hulpmiddelen zoals **mysqldumpslow** tooidentify hello prestatieknelpunt.</span><span class="sxs-lookup"><span data-stu-id="25724-246">After enabling hello MySQL slow query log, you can use MySQL tools like **mysqldumpslow** tooidentify hello performance bottleneck.</span></span>  

<span data-ttu-id="25724-247">Standaard, is dit niet ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="25724-247">By default, this is not enabled.</span></span> <span data-ttu-id="25724-248">Hallo trage querylogboek inschakelen mogelijk enkele CPU-resources in beslag nemen.</span><span class="sxs-lookup"><span data-stu-id="25724-248">Turning on hello slow query log might consume some CPU resources.</span></span> <span data-ttu-id="25724-249">Het is raadzaam dat u dit tijdelijk inschakelt voor het oplossen van knelpunten.</span><span class="sxs-lookup"><span data-stu-id="25724-249">We recommend that you enable this temporarily for troubleshooting performance bottlenecks.</span></span> <span data-ttu-id="25724-250">tooturn op Hallo trage querylogboek:</span><span class="sxs-lookup"><span data-stu-id="25724-250">tooturn on hello slow query log:</span></span>

1. <span data-ttu-id="25724-251">Hallo my.cnf bestand wijzigen door Hallo na toohello regels toe te voegen:</span><span class="sxs-lookup"><span data-stu-id="25724-251">Modify hello my.cnf file by adding hello following lines toohello end:</span></span>

        long_query_time = 2
        slow_query_log = 1
        slow_query_log_file = /RAID0/mysql/mysql-slow.log

2. <span data-ttu-id="25724-252">Hallo MySQL-server opnieuw opstarten.</span><span class="sxs-lookup"><span data-stu-id="25724-252">Restart hello MySQL server.</span></span>

        service  mysql  restart

3. <span data-ttu-id="25724-253">Controleer of instelling Hallo effect duurt via Hallo **weergeven** opdracht.</span><span class="sxs-lookup"><span data-stu-id="25724-253">Check whether hello setting is taking effect by using hello **show** command.</span></span>

![Trage query log ON][7]   

![Resultaten van trage-query-logboek][8]

<span data-ttu-id="25724-256">In dit voorbeeld ziet u dat deze functie van de query wordt vertraagd Hallo is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="25724-256">In this example, you can see that hello slow query feature has been turned on.</span></span> <span data-ttu-id="25724-257">Vervolgens kunt u Hallo **mysqldumpslow** hulpprogramma toodetermine prestatieknelpunten en optimaliseren, zoals het toevoegen van indexen.</span><span class="sxs-lookup"><span data-stu-id="25724-257">You can then use hello **mysqldumpslow** tool toodetermine performance bottlenecks and optimize performance, such as adding indexes.</span></span>

## <a name="appendices"></a><span data-ttu-id="25724-258">Bijlagen</span><span class="sxs-lookup"><span data-stu-id="25724-258">Appendices</span></span>
<span data-ttu-id="25724-259">Hallo hieronder vindt u voorbeeld test prestatiegegevens in een testomgeving gerichte geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="25724-259">hello following are sample performance test data produced in a targeted lab environment.</span></span> <span data-ttu-id="25724-260">Ze bieden algemene achtergrond op Hallo prestaties gegevens trend met verschillende prestaties afstemmen benaderingen.</span><span class="sxs-lookup"><span data-stu-id="25724-260">They provide general background on hello performance data trend with different performance tuning approaches.</span></span> <span data-ttu-id="25724-261">Hallo resultaten kunnen variëren en onder verschillende versies van omgeving of product.</span><span class="sxs-lookup"><span data-stu-id="25724-261">hello results might vary under different environment or product versions.</span></span>

### <span data-ttu-id="25724-262"><a name="AppendixA"></a>Bijlage A</span><span class="sxs-lookup"><span data-stu-id="25724-262"><a name="AppendixA"></a>Appendix A</span></span>  
<span data-ttu-id="25724-263">**Prestaties (IOPS) van de schijf met verschillende RAID-niveaus**</span><span class="sxs-lookup"><span data-stu-id="25724-263">**Disk performance (IOPS) with different RAID levels**</span></span>

![Schijf IOP's met verschillende RAID-niveaus][9]

<span data-ttu-id="25724-265">**Test-opdrachten**</span><span class="sxs-lookup"><span data-stu-id="25724-265">**Test commands**</span></span>  

    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=5G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite

> [!NOTE]
> <span data-ttu-id="25724-266">Hallo werkbelasting van deze test maakt gebruik van 64 threads, probeert tooreach Hallo bovengrens van RAID.</span><span class="sxs-lookup"><span data-stu-id="25724-266">hello workload of this test uses 64 threads, trying tooreach hello upper limit of RAID.</span></span>
>
>

### <span data-ttu-id="25724-267"><a name="AppendixB"></a>Bijlage B</span><span class="sxs-lookup"><span data-stu-id="25724-267"><a name="AppendixB"></a>Appendix B</span></span>  
<span data-ttu-id="25724-268">**Vergelijking van MySQL-prestaties (doorvoer) met verschillende RAID-niveaus** </span><span class="sxs-lookup"><span data-stu-id="25724-268">**MySQL performance (throughput) comparison with different RAID levels** </span></span>  
<span data-ttu-id="25724-269">(XFS bestandssysteem)</span><span class="sxs-lookup"><span data-stu-id="25724-269">(XFS file system)</span></span>

![Vergelijking van MySQL-prestaties met verschillende RAID-niveaus][10]  
![Vergelijking van MySQL-prestaties met verschillende RAID-niveaus][11]

<span data-ttu-id="25724-272">**Test-opdrachten**</span><span class="sxs-lookup"><span data-stu-id="25724-272">**Test commands**</span></span>

    mysqlslap -p0ps.123 --concurrency=2 --iterations=1 --number-int-cols=10 --number-char-cols=10 -a --auto-generate-sql-guid-primary --number-of-queries=10000 --auto-generate-sql-load-type=write –engine=innodb

<span data-ttu-id="25724-273">**Vergelijking van MySQL-prestaties (OLTP) met verschillende RAID-niveaus**</span><span class="sxs-lookup"><span data-stu-id="25724-273">**MySQL performance (OLTP) comparison with different RAID levels**</span></span>  
<span data-ttu-id="25724-274">![Vergelijking van MySQL-prestaties (OLTP) met verschillende RAID-niveaus][12]</span><span class="sxs-lookup"><span data-stu-id="25724-274">![MySQL performance (OLTP) comparison with different RAID levels][12]</span></span>

<span data-ttu-id="25724-275">**Test-opdrachten**</span><span class="sxs-lookup"><span data-stu-id="25724-275">**Test commands**</span></span>

    time sysbench --test=oltp --db-driver=mysql --mysql-user=root --mysql-password=0ps.123  --mysql-table-engine=innodb --mysql-host=127.0.0.1 --mysql-port=3306 --mysql-socket=/var/run/mysqld/mysqld.sock --mysql-db=test --oltp-table-size=1000000 prepare

### <span data-ttu-id="25724-276"><a name="AppendixC"></a>Bijlage C</span><span class="sxs-lookup"><span data-stu-id="25724-276"><a name="AppendixC"></a>Appendix C</span></span>   
<span data-ttu-id="25724-277">**Vergelijking van de schijf prestaties (IOPS) voor verschillende chunk grootten**</span><span class="sxs-lookup"><span data-stu-id="25724-277">**Disk performance (IOPS) comparison for different chunk sizes**</span></span>  
<span data-ttu-id="25724-278">(XFS bestandssysteem)</span><span class="sxs-lookup"><span data-stu-id="25724-278">(XFS file system)</span></span>

![][13]

<span data-ttu-id="25724-279">**Test-opdrachten**</span><span class="sxs-lookup"><span data-stu-id="25724-279">**Test commands**</span></span>  

    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=30G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite
    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=1G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite  

<span data-ttu-id="25724-280">Hallo bestandsgrootten waarmee deze test zijn respectievelijk 30 GB en 1 GB, met RAID 0 (4 schijven) XFS bestandssysteem.</span><span class="sxs-lookup"><span data-stu-id="25724-280">hello file sizes used for this testing are 30 GB and 1 GB, respectively, with RAID 0 (4 disks) XFS file system.</span></span>

### <span data-ttu-id="25724-281"><a name="AppendixD"></a>Bijlage D</span><span class="sxs-lookup"><span data-stu-id="25724-281"><a name="AppendixD"></a>Appendix D</span></span>  
<span data-ttu-id="25724-282">**Vergelijking van MySQL prestaties (doorvoer) voor en na optimalisatie**</span><span class="sxs-lookup"><span data-stu-id="25724-282">**MySQL performance (throughput) comparison before and after optimization**</span></span>  
<span data-ttu-id="25724-283">(XFS File System)</span><span class="sxs-lookup"><span data-stu-id="25724-283">(XFS File System)</span></span>

![Vergelijking van MySQL prestaties (doorvoer) voor en na optimalisatie][14]

<span data-ttu-id="25724-285">**Test-opdrachten**</span><span class="sxs-lookup"><span data-stu-id="25724-285">**Test commands**</span></span>

    mysqlslap -p0ps.123 --concurrency=2 --iterations=1 --number-int-cols=10 --number-char-cols=10 -a --auto-generate-sql-guid-primary --number-of-queries=10000 --auto-generate-sql-load-type=write –engine=innodb,misam

<span data-ttu-id="25724-286">**Hallo-configuratie-instelling voor standaard- en optimalisatie is als volgt:**</span><span class="sxs-lookup"><span data-stu-id="25724-286">**hello configuration setting for default and optimization is as follows:**</span></span>

| <span data-ttu-id="25724-287">Parameters</span><span class="sxs-lookup"><span data-stu-id="25724-287">Parameters</span></span> | <span data-ttu-id="25724-288">Standaard</span><span class="sxs-lookup"><span data-stu-id="25724-288">Default</span></span> | <span data-ttu-id="25724-289">Optimalisatie</span><span class="sxs-lookup"><span data-stu-id="25724-289">Optimization</span></span> |
| --- | --- | --- |
| <span data-ttu-id="25724-290">**innodb_buffer_pool_size**</span><span class="sxs-lookup"><span data-stu-id="25724-290">**innodb_buffer_pool_size**</span></span> |<span data-ttu-id="25724-291">Geen</span><span class="sxs-lookup"><span data-stu-id="25724-291">None</span></span> |<span data-ttu-id="25724-292">7 GB</span><span class="sxs-lookup"><span data-stu-id="25724-292">7 GB</span></span> |
| <span data-ttu-id="25724-293">**innodb_log_file_size**</span><span class="sxs-lookup"><span data-stu-id="25724-293">**innodb_log_file_size**</span></span> |<span data-ttu-id="25724-294">5 MB</span><span class="sxs-lookup"><span data-stu-id="25724-294">5 MB</span></span> |<span data-ttu-id="25724-295">512 MB</span><span class="sxs-lookup"><span data-stu-id="25724-295">512 MB</span></span> |
| <span data-ttu-id="25724-296">**max_connections**</span><span class="sxs-lookup"><span data-stu-id="25724-296">**max_connections**</span></span> |<span data-ttu-id="25724-297">100</span><span class="sxs-lookup"><span data-stu-id="25724-297">100</span></span> |<span data-ttu-id="25724-298">5000</span><span class="sxs-lookup"><span data-stu-id="25724-298">5000</span></span> |
| <span data-ttu-id="25724-299">**innodb_file_per_table**</span><span class="sxs-lookup"><span data-stu-id="25724-299">**innodb_file_per_table**</span></span> |<span data-ttu-id="25724-300">0</span><span class="sxs-lookup"><span data-stu-id="25724-300">0</span></span> |<span data-ttu-id="25724-301">1</span><span class="sxs-lookup"><span data-stu-id="25724-301">1</span></span> |
| <span data-ttu-id="25724-302">**innodb_flush_log_at_trx_commit**</span><span class="sxs-lookup"><span data-stu-id="25724-302">**innodb_flush_log_at_trx_commit**</span></span> |<span data-ttu-id="25724-303">1</span><span class="sxs-lookup"><span data-stu-id="25724-303">1</span></span> |<span data-ttu-id="25724-304">2</span><span class="sxs-lookup"><span data-stu-id="25724-304">2</span></span> |
| <span data-ttu-id="25724-305">**innodb_log_buffer_size**</span><span class="sxs-lookup"><span data-stu-id="25724-305">**innodb_log_buffer_size**</span></span> |<span data-ttu-id="25724-306">8 MB</span><span class="sxs-lookup"><span data-stu-id="25724-306">8 MB</span></span> |<span data-ttu-id="25724-307">128 MB</span><span class="sxs-lookup"><span data-stu-id="25724-307">128 MB</span></span> |
| <span data-ttu-id="25724-308">**query_cache_size**</span><span class="sxs-lookup"><span data-stu-id="25724-308">**query_cache_size**</span></span> |<span data-ttu-id="25724-309">16 MB</span><span class="sxs-lookup"><span data-stu-id="25724-309">16 MB</span></span> |<span data-ttu-id="25724-310">0</span><span class="sxs-lookup"><span data-stu-id="25724-310">0</span></span> |

<span data-ttu-id="25724-311">Voor meer gedetailleerde [optimalisatie configuratieparameters](http://dev.mysql.com/doc/refman/5.6/en/innodb-configuration.html), Raadpleeg toohello [MySQL officiële instructies](http://dev.mysql.com/doc/refman/5.6/en/innodb-parameters.html#sysvar_innodb_flush_method).</span><span class="sxs-lookup"><span data-stu-id="25724-311">For more detailed [optimization configuration parameters](http://dev.mysql.com/doc/refman/5.6/en/innodb-configuration.html), refer toohello [MySQL official instructions](http://dev.mysql.com/doc/refman/5.6/en/innodb-parameters.html#sysvar_innodb_flush_method).</span></span>  

  <span data-ttu-id="25724-312">**Testomgeving**</span><span class="sxs-lookup"><span data-stu-id="25724-312">**Test environment**</span></span>  

| <span data-ttu-id="25724-313">Hardware</span><span class="sxs-lookup"><span data-stu-id="25724-313">Hardware</span></span> | <span data-ttu-id="25724-314">Details</span><span class="sxs-lookup"><span data-stu-id="25724-314">Details</span></span> |
| --- | --- |
| <span data-ttu-id="25724-315">CPU</span><span class="sxs-lookup"><span data-stu-id="25724-315">CPU</span></span> |<span data-ttu-id="25724-316">AMD Opteron (TM) Processor 4171 hij / 4 kernen</span><span class="sxs-lookup"><span data-stu-id="25724-316">AMD Opteron(tm) Processor 4171 HE/4 cores</span></span> |
| <span data-ttu-id="25724-317">Geheugen</span><span class="sxs-lookup"><span data-stu-id="25724-317">Memory</span></span> |<span data-ttu-id="25724-318">14 GB</span><span class="sxs-lookup"><span data-stu-id="25724-318">14 GB</span></span> |
| <span data-ttu-id="25724-319">Schijf</span><span class="sxs-lookup"><span data-stu-id="25724-319">Disk</span></span> |<span data-ttu-id="25724-320">10 GB/schijf</span><span class="sxs-lookup"><span data-stu-id="25724-320">10 GB/disk</span></span> |
| <span data-ttu-id="25724-321">OS</span><span class="sxs-lookup"><span data-stu-id="25724-321">OS</span></span> |<span data-ttu-id="25724-322">Ubuntu 14.04.1 TNS</span><span class="sxs-lookup"><span data-stu-id="25724-322">Ubuntu 14.04.1 LTS</span></span> |

[1]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-01.png
[2]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-02.png
[3]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-03.png
[4]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-04.png
[5]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-05.png
[6]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-06.png
[7]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-07.png
[8]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-08.png
[9]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-09.png
[10]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-10.png
[11]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-11.png
[12]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-12.png
[13]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-13.png
[14]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-14.png

