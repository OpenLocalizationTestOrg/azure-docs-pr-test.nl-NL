---
title: aaaCreate en het uploaden van een FreeBSD VM image | Microsoft Docs
description: Informatie over toocreate en het uploaden van een virtuele harde schijf (VHD) die Hallo FreeBSD besturingssysteem toocreate Azure een virtuele machine bevat
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1ef30f32-61c1-4ba8-9542-801d7b18e9bf
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/08/2017
ms.author: kyliel
ms.openlocfilehash: f3bd155e496f1a2713d36bb66ea9824ed4c210ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-upload-a-freebsd-vhd-tooazure"></a><span data-ttu-id="e9ad5-103">Maken en een tooAzure FreeBSD VHD uploaden</span><span class="sxs-lookup"><span data-stu-id="e9ad5-103">Create and upload a FreeBSD VHD tooAzure</span></span>
<span data-ttu-id="e9ad5-104">Dit artikel laat zien hoe Hallo besturingssysteem FreeBSD toocreate en het uploaden van een virtuele harde schijf (VHD) die bevat.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-104">This article shows you how toocreate and upload a virtual hard disk (VHD) that contains hello FreeBSD operating system.</span></span> <span data-ttu-id="e9ad5-105">Nadat u deze uploaden, kunt u deze kunt gebruiken als uw eigen toocreate installatiekopie van een virtuele machine (VM) in Azure.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-105">After you upload it, you can use it as your own image toocreate a virtual machine (VM) in Azure.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="e9ad5-106">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="e9ad5-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="e9ad5-107">In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-107">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="e9ad5-108">Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="e9ad5-109">Zie voor meer informatie over het uploaden van een VHD met Resource Manager-model Hallo [hier](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e9ad5-109">For information about uploading a VHD using hello Resource Manager model, see [here](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e9ad5-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="e9ad5-110">Prerequisites</span></span>
<span data-ttu-id="e9ad5-111">In dit artikel wordt ervan uitgegaan dat u hebt Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="e9ad5-111">This article assumes that you have hello following items:</span></span>

* <span data-ttu-id="e9ad5-112">**Een Azure-abonnement**--als u geen account hebt, kunt u een in een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-112">**An Azure subscription**--If you don't have an account, you can create one in just a couple of minutes.</span></span> <span data-ttu-id="e9ad5-113">Als u een MSDN-abonnement hebt, raadpleegt u [maandelijkse Azure-tegoed voor Visual Studio-abonnees](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span><span class="sxs-lookup"><span data-stu-id="e9ad5-113">If you have an MSDN subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span> <span data-ttu-id="e9ad5-114">Anders wordt informatie over hoe te[maken van een gratis proefaccount](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e9ad5-114">Otherwise, learn how too[create a free trial account](https://azure.microsoft.com/pricing/free-trial/).</span></span>  
* <span data-ttu-id="e9ad5-115">**Azure PowerShell-hulpprogramma's**--hello Azure PowerShell-module moet worden geïnstalleerd en geconfigureerd toouse uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-115">**Azure PowerShell tools**--hello Azure PowerShell module must be installed and configured toouse your Azure subscription.</span></span> <span data-ttu-id="e9ad5-116">toodownload Hallo-module, Zie [Azure downloadt](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="e9ad5-116">toodownload hello module, see [Azure downloads](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="e9ad5-117">Een zelfstudie waarin wordt beschreven hoe tooinstall en configureer Hallo-module is hier beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-117">A tutorial that describes how tooinstall and configure hello module is available here.</span></span> <span data-ttu-id="e9ad5-118">Gebruik Hallo [Azure downloadt](https://azure.microsoft.com/downloads/) cmdlet tooupload Hallo VHD.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-118">Use hello [Azure Downloads](https://azure.microsoft.com/downloads/) cmdlet tooupload hello VHD.</span></span>
* <span data-ttu-id="e9ad5-119">**FreeBSD-besturingssysteem is geïnstalleerd in een .vhd-bestand**--er is een ondersteund besturingssysteem voor FreeBSD moet tooa virtuele hardeschijf geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-119">**FreeBSD operating system installed in a .vhd file**--A supported   FreeBSD operating system must be installed tooa virtual hard disk.</span></span> <span data-ttu-id="e9ad5-120">Meerdere hulpprogramma's bestaan toocreate VHD-bestanden.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-120">Multiple tools exist toocreate .vhd files.</span></span> <span data-ttu-id="e9ad5-121">U kunt bijvoorbeeld een oplossing voor netwerkvirtualisatie gebruiken zoals Hyper-V toocreate Hallo .vhd-bestand en Hallo-besturingssysteem installeren.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-121">For example, you can use a virtualization solution such as Hyper-V toocreate hello .vhd file and install hello operating system.</span></span> <span data-ttu-id="e9ad5-122">Voor instructies over hoe tooinstall en het gebruik van Hyper-V, Zie [Hyper-V installeren en een virtuele machine maken](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="e9ad5-122">For instructions about how tooinstall and use Hyper-V, see [Install Hyper-V and create a virtual machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="e9ad5-123">Hallo nieuwere VHDX-indeling wordt niet ondersteund in Azure.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-123">hello newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="e9ad5-124">U kunt converteren Hallo tooVHD schijfindeling met behulp van Hyper-V-beheer of cmdlet Hallo [convert-vhd](https://technet.microsoft.com/library/hh848454.aspx).</span><span class="sxs-lookup"><span data-stu-id="e9ad5-124">You can convert hello disk tooVHD format by using Hyper-V Manager or hello cmdlet [convert-vhd](https://technet.microsoft.com/library/hh848454.aspx).</span></span> <span data-ttu-id="e9ad5-125">Er is bovendien een [zelfstudie in MSDN over het toouse FreeBSD met Hyper-V](http://blogs.msdn.com/b/kylie/archive/2014/12/25/running-freebsd-on-hyper-v.aspx).</span><span class="sxs-lookup"><span data-stu-id="e9ad5-125">In addition, there is a [tutorial on MSDN about how toouse FreeBSD with Hyper-V](http://blogs.msdn.com/b/kylie/archive/2014/12/25/running-freebsd-on-hyper-v.aspx).</span></span>
>
>

<span data-ttu-id="e9ad5-126">Deze taak omvat Hallo vijf stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e9ad5-126">This task includes hello following five steps:</span></span>

## <a name="step-1-prepare-hello-image-for-upload"></a><span data-ttu-id="e9ad5-127">Stap 1: Voorbereiden Hallo installatiekopie uploaden</span><span class="sxs-lookup"><span data-stu-id="e9ad5-127">Step 1: Prepare hello image for upload</span></span>
<span data-ttu-id="e9ad5-128">Voer op Hallo virtuele machine waar u Hallo FreeBSD besturingssysteem hebt geïnstalleerd, Hallo procedures te volgen:</span><span class="sxs-lookup"><span data-stu-id="e9ad5-128">On hello virtual machine where you installed hello FreeBSD operating system, complete hello following procedures:</span></span>

1. <span data-ttu-id="e9ad5-129">Schakel DHCP in.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-129">Enable DHCP.</span></span>

        # echo 'ifconfig_hn0="SYNCDHCP"' >> /etc/rc.conf
        # service netif restart
2. <span data-ttu-id="e9ad5-130">SSH inschakelen.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-130">Enable SSH.</span></span>

    <span data-ttu-id="e9ad5-131">Zorg ervoor dat Hallo SSH-server is geïnstalleerd en geconfigureerd toostart tijdens het opstarten.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-131">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span> <span data-ttu-id="e9ad5-132">Dit is standaard ingeschakeld na de installatie van FreeBSD schijf.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-132">By default it is enabled after installation from FreeBSD disc.</span></span> 
3. <span data-ttu-id="e9ad5-133">Instellen van een seriële console.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-133">Set up a serial console.</span></span>

        # echo 'console="comconsole vidconsole"' >> /boot/loader.conf
        # echo 'comconsole_speed="115200"' >> /boot/loader.conf
4. <span data-ttu-id="e9ad5-134">Sudo installeren.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-134">Install sudo.</span></span>

    <span data-ttu-id="e9ad5-135">Hallo root-account is uitgeschakeld in Azure.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-135">hello root account is disabled in Azure.</span></span> <span data-ttu-id="e9ad5-136">Dit betekent dat u tooutilize sudo uit een onbevoegde gebruiker toorun-opdrachten met verhoogde bevoegdheden nodig.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-136">This means you need tooutilize sudo from an unprivileged user toorun commands with elevated privileges.</span></span>

        # pkg install sudo
   
5. <span data-ttu-id="e9ad5-137">Vereisten voor Azure-Agent.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-137">Prerequisites for Azure Agent.</span></span>

        # pkg install python27  
        # pkg install Py27-setuptools  
        # ln -s /usr/local/bin/python2.7 /usr/bin/python   
        # pkg install git
6. <span data-ttu-id="e9ad5-138">Azure-Agent installeren.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-138">Install Azure Agent.</span></span>

    <span data-ttu-id="e9ad5-139">Hallo meest recente versie van hello Azure-Agent altijd vindt u op [github](https://github.com/Azure/WALinuxAgent/releases).</span><span class="sxs-lookup"><span data-stu-id="e9ad5-139">hello latest release of hello Azure Agent can always be found on [github](https://github.com/Azure/WALinuxAgent/releases).</span></span> <span data-ttu-id="e9ad5-140">Hallo versie 2.0.10 + officieel ondersteunt FreeBSD 10 & 10.1 en Hallo versie 2.1.4 + (inclusief 2.2.x) officieel ondersteunt FreeBSD 10.2 en latere versies.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-140">hello version 2.0.10 + officially supports FreeBSD 10 & 10.1, and hello version 2.1.4 + (including 2.2.x) officially supports FreeBSD 10.2 and later releases.</span></span>

        # git clone https://github.com/Azure/WALinuxAgent.git  
        # cd WALinuxAgent  
        # git tag  
        …
        WALinuxAgent-2.0.16
        …
        v2.1.4
        v2.1.4.rc0
        v2.1.4.rc1

    <span data-ttu-id="e9ad5-141">Gebruik voor 2.0, gaan we 2.0.16 als een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="e9ad5-141">For 2.0, let's use 2.0.16 as an example:</span></span>

        # git checkout WALinuxAgent-2.0.16
        # python setup.py install  
        # ln -sf /usr/local/sbin/waagent /usr/sbin/waagent  

    <span data-ttu-id="e9ad5-142">2.1, gaan we gebruik 2.1.4 als voor een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="e9ad5-142">For 2.1, let's use 2.1.4 as an example:</span></span>

        # git checkout v2.1.4
        # python setup.py install  
        # ln -sf /usr/local/sbin/waagent /usr/sbin/waagent  
        # ln -sf /usr/local/sbin/waagent2.0 /usr/sbin/waagent2.0

   > [!IMPORTANT]
   > <span data-ttu-id="e9ad5-143">Nadat u Azure-Agent hebt geïnstalleerd, is het een goed idee tooverify dat deze wordt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="e9ad5-143">After you install Azure Agent, it's a good idea tooverify that it's running:</span></span>
   >
   >

        # waagent -version
        WALinuxAgent-2.1.4 running on freebsd 10.3
        Python: 2.7.11
        # ps auxw | grep waagent
        root   639   0.0  0.5 104620 17520 u0- I    05:17    0:00.20 python /usr/local/sbin/waagent -daemon (python2.7)
        # cat /var/log/waagent.log
7. <span data-ttu-id="e9ad5-144">Inrichting ervan ongedaan Hallo-systeem.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-144">Deprovision hello system.</span></span>

    <span data-ttu-id="e9ad5-145">Identiteitsgegevens Hallo system tooclean deze en maak deze geschikt is voor reprovisioning.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-145">Deprovision hello system tooclean it and make it suitable for reprovisioning.</span></span> <span data-ttu-id="e9ad5-146">Hallo volgende opdracht ook verwijderd Hallo laatste ingerichte gebruiker serviceaccount en Hallo die zijn gekoppeld:</span><span class="sxs-lookup"><span data-stu-id="e9ad5-146">hello following command also deletes hello last provisioned user account and hello associated data:</span></span>

        # echo "y" |  /usr/local/sbin/waagent -deprovision+user  
        # echo  'waagent_enable="YES"' >> /etc/rc.conf

    <span data-ttu-id="e9ad5-147">U kunt nu uw virtuele machine afsluiten.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-147">Now you can shut down your VM.</span></span>

## <a name="step-2-create-a-storage-account-in-azure"></a><span data-ttu-id="e9ad5-148">Stap 2: Een opslagaccount maken in Azure</span><span class="sxs-lookup"><span data-stu-id="e9ad5-148">Step 2: Create a storage account in Azure</span></span>
<span data-ttu-id="e9ad5-149">U moet een opslagaccount in Azure tooupload een .vhd-bestand, zodat deze gebruikt toocreate een virtuele machine worden kan.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-149">You need a storage account in Azure tooupload a .vhd file so it can be used toocreate a virtual machine.</span></span> <span data-ttu-id="e9ad5-150">U kunt hello Azure classic portal toocreate storage-account gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-150">You can use hello Azure classic portal toocreate a storage account.</span></span>

1. <span data-ttu-id="e9ad5-151">Meld u aan toohello [klassieke Azure-portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="e9ad5-151">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="e9ad5-152">Selecteer op de opdrachtbalk Hallo **nieuw**.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-152">On hello command bar, select **New**.</span></span>
3. <span data-ttu-id="e9ad5-153">Selecteer **gegevensservices** > **opslag** > **snelle invoer**.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-153">Select **Data Services** > **Storage** > **Quick Create**.</span></span>

    ![Snel een opslagaccount maken](./media/freebsd-create-upload-vhd/Storage-quick-create.png)
4. <span data-ttu-id="e9ad5-155">Vul de velden Hallo als volgt in:</span><span class="sxs-lookup"><span data-stu-id="e9ad5-155">Fill out hello fields as follows:</span></span>

   * <span data-ttu-id="e9ad5-156">In Hallo **URL** veld, typt u een subdomein naam toouse in Hallo storage account-URL.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-156">In hello **URL** field, type a subdomain name toouse in hello storage account URL.</span></span> <span data-ttu-id="e9ad5-157">Hallo-vermelding kan van 3 tot 24 cijfers en kleine letters bevatten.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-157">hello entry can contain from 3-24 numbers and lowercase letters.</span></span> <span data-ttu-id="e9ad5-158">Deze naam wordt Hallo hostnaam binnen Hallo-URL die is gebruikt tooaddress Azure Blob storage, Azure Queue storage of Azure Table storage-resources voor Hallo-abonnement.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-158">This name becomes hello host name within hello URL that is used tooaddress Azure Blob storage, Azure Queue storage, or Azure Table storage resources for hello subscription.</span></span>
   * <span data-ttu-id="e9ad5-159">In Hallo **locatie/Affiniteitsgroep** vervolgkeuzelijst, kies Hallo **locatie of affiniteitsgroep** voor Hallo storage-account.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-159">In hello **Location/Affinity Group** drop-down menu, choose hello **location or affinity group** for hello storage account.</span></span> <span data-ttu-id="e9ad5-160">Een affiniteitsgroep kunt u uw cloud-services en opslag in Hallo plaatst hetzelfde Datacenter.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-160">An affinity group lets you put your cloud services and storage in hello same data center.</span></span>
   * <span data-ttu-id="e9ad5-161">In Hallo **replicatie** veld, besluiten of toouse **geografisch redundante** replicatie voor het Hallo-opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-161">In hello **Replication** field, decide whether toouse **Geo-Redundant** replication for hello storage account.</span></span> <span data-ttu-id="e9ad5-162">Geo-replicatie is standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-162">Geo-replication is turned on by default.</span></span> <span data-ttu-id="e9ad5-163">Deze optie uw gegevens tooa secundaire locatie, er zijn geen kosten tooyou repliceert, zodat uw opslag wordt overgenomen toothat locatie als een storing optreedt op Hallo primaire locatie.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-163">This option replicates your data tooa secondary location, at no cost tooyou, so that your storage fails over toothat location if a major failure occurs at hello primary location.</span></span> <span data-ttu-id="e9ad5-164">Hallo secundaire locatie wordt automatisch toegewezen en kan niet worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-164">hello secondary location is assigned automatically and can't be changed.</span></span> <span data-ttu-id="e9ad5-165">Als u meer controle over het Hallo-locatie van de cloud-gebaseerde opslag vervaldatum toolegal vereisten of organisatie beleid nodig hebt, kunt u geo-replicatie kunt uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-165">If you need more control over hello location of your cloud-based storage due toolegal requirements or organizational policy, you can turn off geo-replication.</span></span> <span data-ttu-id="e9ad5-166">Echter wel rekening dat als u later geo-replicatie inschakelt, wordt u gefactureerd eenmalig kosten tooreplicate van gegevensoverdracht uw bestaande gegevens toohello secundaire locatie.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-166">However, be aware that if you later turn on geo-replication, you will be charged a one-time data transfer fee tooreplicate your existing data toohello secondary location.</span></span> <span data-ttu-id="e9ad5-167">Storage-services zonder geo-replicatie worden aangeboden met korting.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-167">Storage services without geo-replication are offered at a discount.</span></span> <span data-ttu-id="e9ad5-168">Meer informatie over het beheren van geo-replicatie van opslagaccounts vindt u hier: [Azure Storage-replicatie](../../../storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="e9ad5-168">More details about managing geo-replication of storage accounts can be found here: [Azure Storage replication](../../../storage/common/storage-redundancy.md).</span></span>

     ![Voer de details van opslag](./media/freebsd-create-upload-vhd/Storage-create-account.png)
5. <span data-ttu-id="e9ad5-170">Selecteer **Storage-Account maken**.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-170">Select **Create Storage Account**.</span></span> <span data-ttu-id="e9ad5-171">Hallo account wordt nu weergegeven onder **opslag**.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-171">hello account now appears under **storage**.</span></span>

    ![Storage-account is gemaakt](./media/freebsd-create-upload-vhd/Storagenewaccount.png)
6. <span data-ttu-id="e9ad5-173">Maak vervolgens een container voor uw geüploade VHD-bestanden.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-173">Next, create a container for your uploaded .vhd files.</span></span> <span data-ttu-id="e9ad5-174">Selecteer de opslagaccountnaam hello, en selecteer vervolgens **Containers**.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-174">Select hello storage account name, and then select **Containers**.</span></span>

    ![Details van de Storage-account](./media/freebsd-create-upload-vhd/storageaccount_detail.png)
7. <span data-ttu-id="e9ad5-176">Selecteer **maken van een Container**.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-176">Select **Create a Container**.</span></span>

    ![Details van de Storage-account](./media/freebsd-create-upload-vhd/storageaccount_container.png)
8. <span data-ttu-id="e9ad5-178">In Hallo **naam** veld, typ een naam voor de container.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-178">In hello **Name** field, type a name for your container.</span></span> <span data-ttu-id="e9ad5-179">Klik op Hallo **toegang** vervolgkeuzelijst, selecteer welk type toegangsbeleid dat u wilt.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-179">Then, in hello **Access** drop-down menu, select what type of access policy you want.</span></span>

    ![Containernaam](./media/freebsd-create-upload-vhd/storageaccount_containervalues.png)

   > [!NOTE]
   > <span data-ttu-id="e9ad5-181">Standaard Hallo container privé is en alleen toegankelijk zijn voor de accounteigenaar Hallo.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-181">By default, hello container is private and can only be accessed by hello account owner.</span></span> <span data-ttu-id="e9ad5-182">tooallow openbare leestoegang toohello blobs in de container hello, maar niet de eigenschappen van toohello-container en metagegevens gebruiken Hallo **openbare Blob** optie.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-182">tooallow public read access toohello blobs in hello container, but not toohello container properties and metadata, use hello **Public Blob** option.</span></span> <span data-ttu-id="e9ad5-183">tooallow volledige openbare leestoegang voor hello container en blobs, Hallo **openbare Container** optie.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-183">tooallow full public read access for hello container and blobs, use hello **Public Container** option.</span></span>
   >
   >

## <a name="step-3-prepare-hello-connection-tooazure"></a><span data-ttu-id="e9ad5-184">Stap 3: Hallo verbinding tooAzure voorbereiden</span><span class="sxs-lookup"><span data-stu-id="e9ad5-184">Step 3: Prepare hello connection tooAzure</span></span>
<span data-ttu-id="e9ad5-185">Voordat u een .vhd-bestand uploadt kunt, moet u tooestablish een beveiligde verbinding tussen uw computer en uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-185">Before you can upload a .vhd file, you need tooestablish a secure connection between your computer and your Azure subscription.</span></span> <span data-ttu-id="e9ad5-186">U kunt gebruiken hello Azure Active Directory (Azure AD)-methode of Hallo certificaat methode toodo deze.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-186">You can use hello Azure Active Directory (Azure AD) method or hello certificate method toodo it.</span></span>

### <a name="use-hello-azure-ad-method-tooupload-a-vhd-file"></a><span data-ttu-id="e9ad5-187">Hello Azure AD-methode tooupload een .vhd-bestand gebruiken</span><span class="sxs-lookup"><span data-stu-id="e9ad5-187">Use hello Azure AD method tooupload a .vhd file</span></span>
1. <span data-ttu-id="e9ad5-188">Open hello Azure PowerShell-console.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-188">Open hello Azure PowerShell console.</span></span>
2. <span data-ttu-id="e9ad5-189">Type Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="e9ad5-189">Type hello following command:</span></span>  
    `Add-AzureAccount`

    <span data-ttu-id="e9ad5-190">Deze opdracht opent een aanmeldingspagina-venster waar u zich met uw werk- of schoolaccount aanmelden kunt.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-190">This command opens a sign-in window where you can sign in with your work or school account.</span></span>

    ![PowerShell-venster](./media/freebsd-create-upload-vhd/add_azureaccount.png)
3. <span data-ttu-id="e9ad5-192">Azure worden geverifieerd en Hallo referentie-informatie wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-192">Azure authenticates and saves hello credential information.</span></span> <span data-ttu-id="e9ad5-193">Vervolgens wordt Hallo-venster gesloten.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-193">Then it closes hello window.</span></span>

### <a name="use-hello-certificate-method-tooupload-a-vhd-file"></a><span data-ttu-id="e9ad5-194">Hallo certificaat methode tooupload een .vhd-bestand gebruiken</span><span class="sxs-lookup"><span data-stu-id="e9ad5-194">Use hello certificate method tooupload a .vhd file</span></span>
1. <span data-ttu-id="e9ad5-195">Open hello Azure PowerShell-console.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-195">Open hello Azure PowerShell console.</span></span>
2. <span data-ttu-id="e9ad5-196">Type: `Get-AzurePublishSettingsFile`.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-196">Type:  `Get-AzurePublishSettingsFile`.</span></span>
3. <span data-ttu-id="e9ad5-197">Een browservenster wordt geopend en vraagt u toodownload hello .publishsettings-bestand.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-197">A browser window opens and prompts you toodownload hello .publishsettings file.</span></span> <span data-ttu-id="e9ad5-198">Dit bestand bevat informatie en een certificaat voor uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-198">This file contains information and a certificate for your Azure subscription.</span></span>

    ![Browser-downloadpagina](./media/freebsd-create-upload-vhd/Browser_download_GetPublishSettingsFile.png)
4. <span data-ttu-id="e9ad5-200">Hallo .publishsettings-bestand opslaan.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-200">Save hello .publishsettings file.</span></span>
5. <span data-ttu-id="e9ad5-201">Type: `Import-AzurePublishSettingsFile <PathToFile>`, waarbij `<PathToFile>` Hallo volledig pad toohello .publishsettings-bestand is.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-201">Type:  `Import-AzurePublishSettingsFile <PathToFile>`, where `<PathToFile>` is hello full path toohello .publishsettings file.</span></span>

   <span data-ttu-id="e9ad5-202">Zie voor meer informatie [aan de slag met Azure-cmdlets](http://msdn.microsoft.com/library/windowsazure/jj554332.aspx).</span><span class="sxs-lookup"><span data-stu-id="e9ad5-202">For more information, see [Get started with Azure cmdlets](http://msdn.microsoft.com/library/windowsazure/jj554332.aspx).</span></span>

   <span data-ttu-id="e9ad5-203">Zie voor meer informatie over het installeren en configureren van PowerShell [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e9ad5-203">For more information about installing and configuring PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="step-4-upload-hello-vhd-file"></a><span data-ttu-id="e9ad5-204">Stap 4: Hallo .vhd-bestand uploaden</span><span class="sxs-lookup"><span data-stu-id="e9ad5-204">Step 4: Upload hello .vhd file</span></span>
<span data-ttu-id="e9ad5-205">Wanneer u Hallo .vhd-bestand uploadt, kunt u deze overal opnemen in de Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-205">When you upload hello .vhd file, you can place it anywhere within your Blob storage.</span></span> <span data-ttu-id="e9ad5-206">Hieronder volgen enkele termen die u bij het Hallo-bestand te uploaden:</span><span class="sxs-lookup"><span data-stu-id="e9ad5-206">Following are some terms you will use when you upload hello file:</span></span>

* <span data-ttu-id="e9ad5-207">**BlobStorageURL** Hallo-URL voor Hallo storage-account die u in stap 2 hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-207">**BlobStorageURL** is hello URL for hello storage account that you created in Step 2.</span></span>
* <span data-ttu-id="e9ad5-208">**YourImagesFolder** Hallo-container in Blob-opslag is waar u toostore uw afbeeldingen.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-208">**YourImagesFolder** is hello container within Blob storage where you want toostore your images.</span></span>
* <span data-ttu-id="e9ad5-209">**VHDName** Hallo-label die wordt weergegeven in hello Azure classic portal tooidentify Hallo virtuele harde schijf.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-209">**VHDName** is hello label that appears in hello Azure classic portal tooidentify hello virtual hard disk.</span></span>
* <span data-ttu-id="e9ad5-210">**PathToVHDFile** Hallo volledig pad en naam van Hallo .vhd-bestand.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-210">**PathToVHDFile** is hello full path and name of hello .vhd file.</span></span>

<span data-ttu-id="e9ad5-211">U hebt gebruikt in de vorige stap Hallo hello Azure PowerShell-venster, typ:</span><span class="sxs-lookup"><span data-stu-id="e9ad5-211">From hello Azure PowerShell window you used in hello previous step, type:</span></span>

        Add-AzureVhd -Destination "<BlobStorageURL>/<YourImagesFolder>/<VHDName>.vhd" -LocalFilePath <PathToVHDFile>

## <a name="step-5-create-a-vm-with-hello-uploaded-vhd-file"></a><span data-ttu-id="e9ad5-212">Stap 5: Een virtuele machine maken met de Hallo geüploade .vhd-bestand</span><span class="sxs-lookup"><span data-stu-id="e9ad5-212">Step 5: Create a VM with hello uploaded .vhd file</span></span>
<span data-ttu-id="e9ad5-213">Nadat u Hallo .vhd-bestand uploadt, kunt u deze toevoegen als een lijst met afbeeldingen toohello van aangepaste installatiekopieën die zijn gekoppeld aan uw abonnement en een virtuele machine maken met deze aangepaste installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-213">After you upload hello .vhd file, you can add it as an image toohello list of custom images that are associated with your subscription and create a virtual machine with this custom image.</span></span>

1. <span data-ttu-id="e9ad5-214">U hebt gebruikt in de vorige stap Hallo hello Azure PowerShell-venster, typ:</span><span class="sxs-lookup"><span data-stu-id="e9ad5-214">From hello Azure PowerShell window you used in hello previous step, type:</span></span>

        Add-AzureVMImage -ImageName <Your Image's Name> -MediaLocation <location of hello VHD> -OS <Type of hello OS on hello VHD>

   > [!NOTE]
   > <span data-ttu-id="e9ad5-215">Linux gebruiken als Hallo BS-type.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-215">Use Linux as hello OS type.</span></span> <span data-ttu-id="e9ad5-216">de huidige Azure PowerShell-versie Hallo accepteert alleen 'Linux' of 'Windows' als parameter.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-216">hello current Azure PowerShell version accepts only “Linux” or “Windows” as a parameter.</span></span>
   >
   >
2. <span data-ttu-id="e9ad5-217">Nadat u de vorige stappen hello, Hallo nieuwe installatiekopie wordt weergegeven wanneer u ervoor Hallo kiest **installatiekopieën** tabblad op Hallo klassieke Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-217">After you complete hello previous steps, hello new image is listed when you choose hello **Images** tab on hello Azure classic portal.</span></span>  

    ![Een afbeelding kiezen](./media/freebsd-create-upload-vhd/addfreebsdimage.png)
3. <span data-ttu-id="e9ad5-219">Een virtuele machine maken vanuit Hallo-galerie.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-219">Create a virtual machine from hello gallery.</span></span> <span data-ttu-id="e9ad5-220">Deze nieuwe installatiekopie is nu beschikbaar onder **Mijn afbeeldingen**.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-220">This new image is now available under **My Images**.</span></span>
4. <span data-ttu-id="e9ad5-221">Hallo nieuwe installatiekopie selecteren.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-221">Select hello new image.</span></span> <span data-ttu-id="e9ad5-222">Ga vervolgens door Hallo prompts tooset van een hostnaam, een wachtwoord, een SSH-sleutel, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-222">Next, go through hello prompts tooset up a host name, password, SSH key, and so on.</span></span>

    ![Aangepaste installatiekopie](./media/freebsd-create-upload-vhd/createfreebsdimageinazure.png)
5. <span data-ttu-id="e9ad5-224">Nadat u het Hallo-inrichting hebt voltooid, ziet u uw FreeBSD VM worden uitgevoerd in Azure.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-224">After you complete hello provisioning, you'll see your FreeBSD VM running in Azure.</span></span>

    ![Afbeelding van FreeBSD in azure](./media/freebsd-create-upload-vhd/freebsdimageinazure.png)
