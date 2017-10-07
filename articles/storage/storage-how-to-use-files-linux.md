---
title: Azure File storage met Linux aaaUse | Microsoft Docs
description: Meer informatie over hoe toomount een Azure-bestand delen via SMB op Linux.
services: storage
documentationcenter: na
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 6edc37ce-698f-4d50-8fc1-591ad456175d
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/8/2017
ms.author: renash
ms.openlocfilehash: ed6ba9b98f121d6629d858320ca3760384303ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-file-storage-with-linux"></a><span data-ttu-id="876e3-103">Azure File storage gebruiken met Linux</span><span class="sxs-lookup"><span data-stu-id="876e3-103">Use Azure File storage with Linux</span></span>
<span data-ttu-id="876e3-104">[Azure File storage](storage-dotnet-how-to-use-files.md) is van Microsoft easy toouse cloud-bestandssysteem.</span><span class="sxs-lookup"><span data-stu-id="876e3-104">[Azure File storage](storage-dotnet-how-to-use-files.md) is Microsoft's easy toouse cloud file system.</span></span> <span data-ttu-id="876e3-105">Azure-bestandsshares kunnen worden gekoppeld in Linux-distributies met Hallo [cifs utils pakket](https://wiki.samba.org/index.php/LinuxCIFS_utils) van Hallo [Samba project](https://www.samba.org/).</span><span class="sxs-lookup"><span data-stu-id="876e3-105">Azure File shares can be mounted in Linux distributions using hello [cifs-utils package](https://wiki.samba.org/index.php/LinuxCIFS_utils) from hello [Samba project](https://www.samba.org/).</span></span> <span data-ttu-id="876e3-106">In dit artikel ziet u twee manieren toomount een Azure-bestandsshare: op aanvraag Hello `mount` opdracht en op opstarten door het maken van een vermelding in `/etc/fstab`.</span><span class="sxs-lookup"><span data-stu-id="876e3-106">This article shows two ways toomount an Azure File share: on-demand with hello `mount` command and on-boot by creating an entry in `/etc/fstab`.</span></span>

> [!NOTE]  
> <span data-ttu-id="876e3-107">In volgorde toomount een Azure-bestandsshare buiten hello moet Azure-regio die deze wordt gehost in, bijvoorbeeld on-premises of in een andere Azure-regio Hallo OS ondersteunen Hallo versleuteling van SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="876e3-107">In order toomount an Azure File share outside of hello Azure region it is hosted in, such as on-premises or in a different Azure region, hello OS must support hello encryption functionality of SMB 3.0.</span></span> <span data-ttu-id="876e3-108">Coderingsfunctie voor SMB 3.0 voor Linux is geïntroduceerd in 4.11 kernel.</span><span class="sxs-lookup"><span data-stu-id="876e3-108">Encryption feature for SMB 3.0 for Linux was introduced in 4.11 kernel.</span></span> <span data-ttu-id="876e3-109">Deze functie kunt koppelen van de bestandsshare in Azure vanaf on-premises of andere Azure-regio.</span><span class="sxs-lookup"><span data-stu-id="876e3-109">This feature enables mounting of Azure File share from on-premises or a different Azure region.</span></span> <span data-ttu-id="876e3-110">Deze functionaliteit is op Hallo moment van publicatie, backported tooUbuntu van 16.04 en hoger.</span><span class="sxs-lookup"><span data-stu-id="876e3-110">At hello time of publishing, this functionality has been backported tooUbuntu from 16.04 and above.</span></span>


## <a name="prerequisities-for-mounting-an-azure-file-share-with-linux-and-hello-cifs-utils-package"></a><span data-ttu-id="876e3-111">Prerequisities voor het koppelen van een Azure-bestandsshare met Linux en Hallo cifs-utils-pakket</span><span class="sxs-lookup"><span data-stu-id="876e3-111">Prerequisities for mounting an Azure File share with Linux and hello cifs-utils package</span></span>
* <span data-ttu-id="876e3-112">**Kies een Linux-distributie waarvoor Hallo cifs utils pakket is geïnstalleerd kan**: Microsoft raadt Hallo Linux-distributies in de afbeelding voor Azure-galerie hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="876e3-112">**Pick a Linux distribution that can have hello cifs-utils package installed**: Microsoft recommends hello following Linux distributions in hello Azure image gallery:</span></span>

    * <span data-ttu-id="876e3-113">Ubuntu Server 14.04 +</span><span class="sxs-lookup"><span data-stu-id="876e3-113">Ubuntu Server 14.04+</span></span>
    * <span data-ttu-id="876e3-114">RHEL 7 +</span><span class="sxs-lookup"><span data-stu-id="876e3-114">RHEL 7+</span></span>
    * <span data-ttu-id="876e3-115">CentOS 7 +</span><span class="sxs-lookup"><span data-stu-id="876e3-115">CentOS 7+</span></span>
    * <span data-ttu-id="876e3-116">Debian 8</span><span class="sxs-lookup"><span data-stu-id="876e3-116">Debian 8</span></span>
    * <span data-ttu-id="876e3-117">openSUSE 13.2 +</span><span class="sxs-lookup"><span data-stu-id="876e3-117">openSUSE 13.2+</span></span>
    * <span data-ttu-id="876e3-118">SUSE Linux Enterprise Server 12</span><span class="sxs-lookup"><span data-stu-id="876e3-118">SUSE Linux Enterprise Server 12</span></span>

* <span data-ttu-id="876e3-119"><a id="install-cifs-utils"></a>**Hallo cifs utils pakket is geïnstalleerd**: Hallo cifs-utils kan worden geïnstalleerd met behulp van Pakketbeheer Hallo op Hallo Linux-distributie van uw keuze.</span><span class="sxs-lookup"><span data-stu-id="876e3-119"><a id="install-cifs-utils"></a>**hello cifs-utils package is installed**: hello cifs-utils can be installed using hello package manager on hello Linux distribution of your choice.</span></span> 

    <span data-ttu-id="876e3-120">Op **Ubuntu** en **op basis van Debian** distributies, gebruik Hallo `apt-get` Pakketbeheer:</span><span class="sxs-lookup"><span data-stu-id="876e3-120">On **Ubuntu** and **Debian-based** distributions, use hello `apt-get` package manager:</span></span>

    ```
    sudo apt-get update
    sudo apt-get install cifs-utils
    ```

    <span data-ttu-id="876e3-121">Op **RHEL** en **CentOS**, gebruik Hallo `yum` Pakketbeheer:</span><span class="sxs-lookup"><span data-stu-id="876e3-121">On **RHEL** and **CentOS**, use hello `yum` package manager:</span></span>

    ```
    sudo yum install samba-client samba-common cifs-utils
    ```

    <span data-ttu-id="876e3-122">Op **openSUSE**, gebruik Hallo `zypper` Pakketbeheer:</span><span class="sxs-lookup"><span data-stu-id="876e3-122">On **openSUSE**, use hello `zypper` package manager:</span></span>

    ```
    sudo zypper install samba*
    ```

    <span data-ttu-id="876e3-123">Op andere distributies Hallo juiste package manager gebruiken of [compileren van bron](https://wiki.samba.org/index.php/LinuxCIFS_utils#Download).</span><span class="sxs-lookup"><span data-stu-id="876e3-123">On other distributions, use hello appropriate package manager or [compile from source](https://wiki.samba.org/index.php/LinuxCIFS_utils#Download).</span></span>

* <span data-ttu-id="876e3-124">**Besluit op Hallo van map/bestand machtigingen van de gekoppelde share Hallo**: In de onderstaande Hallo voorbeelden, gebruiken we 0777, toogive lezen, schrijven en uitvoeren van machtigingen tooall gebruikers.</span><span class="sxs-lookup"><span data-stu-id="876e3-124">**Decide on hello directory/file permissions of hello mounted share**: In hello examples below, we use 0777, toogive read, write, and execute permissions tooall users.</span></span> <span data-ttu-id="876e3-125">U kunt het vervangen door andere [type chmod machtigingen](https://en.wikipedia.org/wiki/Chmod) naar wens.</span><span class="sxs-lookup"><span data-stu-id="876e3-125">You can replace it with other [chmod permissions](https://en.wikipedia.org/wiki/Chmod) as desired.</span></span> 

* <span data-ttu-id="876e3-126">**Naam van het opslagaccount**: toomount een Azure-bestand delen, kunt u moet Hallo naam van het opslagaccount Hallo.</span><span class="sxs-lookup"><span data-stu-id="876e3-126">**Storage Account Name**: toomount an Azure File share, you will need hello name of hello storage account.</span></span>

* <span data-ttu-id="876e3-127">**Opslagaccountsleutel**: toomount een Azure-bestand delen, kunt u moet Hallo primaire (of secundaire)-opslagsleutel.</span><span class="sxs-lookup"><span data-stu-id="876e3-127">**Storage Account Key**: toomount an Azure File share, you will need hello primary (or secondary) storage key.</span></span> <span data-ttu-id="876e3-128">SAS-sleutels worden momenteel niet ondersteund voor koppelen.</span><span class="sxs-lookup"><span data-stu-id="876e3-128">SAS keys are not currently supported for mounting.</span></span>

* <span data-ttu-id="876e3-129">**Zorg ervoor dat poort 445 is geopend**: SMB communiceert via TCP-poort 445 - controleren toosee als uw firewall niet wordt geblokkeerd door TCP-poorten 445 van client-computer.</span><span class="sxs-lookup"><span data-stu-id="876e3-129">**Ensure port 445 is open**: SMB communicates over TCP port 445 - check toosee if your firewall is not blocking TCP ports 445 from client machine.</span></span>

## <a name="mount-hello-azure-file-share-on-demand-with-mount"></a><span data-ttu-id="876e3-130">Hello Azure-op-verzoek met de bestandsshare koppelen`mount`</span><span class="sxs-lookup"><span data-stu-id="876e3-130">Mount hello Azure File share on-demand with `mount`</span></span>
1. <span data-ttu-id="876e3-131">**[Hallo cifs utils pakket voor uw Linux-distributie](#install-cifs-utils)**.</span><span class="sxs-lookup"><span data-stu-id="876e3-131">**[Install hello cifs-utils package for your Linux distribution](#install-cifs-utils)**.</span></span>

2. <span data-ttu-id="876e3-132">**Maak een map voor het koppelpunt Hallo**: dit kan overal worden gedaan op Hallo-bestandssysteem.</span><span class="sxs-lookup"><span data-stu-id="876e3-132">**Create a folder for hello mount point**: This can be done anywhere on hello file system.</span></span>

    ```
    mkdir mymountpoint
    ```

3. <span data-ttu-id="876e3-133">**Gebruik Hallo koppelpunt opdracht toomount hello Azure File share**: onthouden tooreplace `<storage-account-name>`, `<share-name>`, en `<storage-account-key>` met de juiste informatie Hallo.</span><span class="sxs-lookup"><span data-stu-id="876e3-133">**Use hello mount command toomount hello Azure File share**: Remember tooreplace `<storage-account-name>`, `<share-name>`, and `<storage-account-key>` with hello proper information.</span></span>

    ```
    sudo mount -t cifs //<storage-account-name>.file.core.windows.net/<share-name> ./mymountpoint -o vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino
    ```

> [!Note]  
> <span data-ttu-id="876e3-134">Wanneer u klaar bent met behulp van Azure-bestandsshare Hallo, u kunt gebruiken `sudo umount ./mymountpoint` toounmount Hallo share.</span><span class="sxs-lookup"><span data-stu-id="876e3-134">When you are done using hello Azure File share, you may use `sudo umount ./mymountpoint` toounmount hello share.</span></span>

## <a name="create-a-persistent-mount-point-for-hello-azure-file-share-with-etcfstab"></a><span data-ttu-id="876e3-135">Maken van een permanente koppelpunt voor hello Azure-bestandsshare met`/etc/fstab`</span><span class="sxs-lookup"><span data-stu-id="876e3-135">Create a persistent mount point for hello Azure File share with `/etc/fstab`</span></span>
1. <span data-ttu-id="876e3-136">**[Hallo cifs utils pakket voor uw Linux-distributie](#install-cifs-utils)**.</span><span class="sxs-lookup"><span data-stu-id="876e3-136">**[Install hello cifs-utils package for your Linux distribution](#install-cifs-utils)**.</span></span>

2. <span data-ttu-id="876e3-137">**Maak een map voor het koppelpunt Hallo**: dit kan overal worden gedaan op Hallo bestandssysteem, maar u moet toonote Hallo absolute pad van Hallo-map.</span><span class="sxs-lookup"><span data-stu-id="876e3-137">**Create a folder for hello mount point**: This can be done anywhere on hello file system, but you need toonote hello absolute path of hello folder.</span></span> <span data-ttu-id="876e3-138">Hallo volgende voorbeeld maakt een map onder de hoofdmap.</span><span class="sxs-lookup"><span data-stu-id="876e3-138">hello following example creates a folder under root.</span></span>

    ```
    sudo mkdir /mymountpoint
    ```

3. <span data-ttu-id="876e3-139">**Gebruik Hallo volgende opdracht tooappend Hallo volgt regel te`/etc/fstab`**: onthouden tooreplace `<storage-account-name>`, `<share-name>`, en `<storage-account-key>` met de juiste informatie Hallo.</span><span class="sxs-lookup"><span data-stu-id="876e3-139">**Use hello following command tooappend hello following line too`/etc/fstab`**: Remember tooreplace `<storage-account-name>`, `<share-name>`, and `<storage-account-key>` with hello proper information.</span></span>

    ```
    sudo bash -c 'echo "//<storage-account-name>.file.core.windows.net/<share-name> /mymountpoint cifs vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino" >> /etc/fstab'
    ```

> [!Note]  
> <span data-ttu-id="876e3-140">U kunt `sudo mount -a` toomount Hallo bestandsshare in Azure na het bewerken van `/etc/fstab` in plaats van opnieuw opstarten.</span><span class="sxs-lookup"><span data-stu-id="876e3-140">You can use `sudo mount -a` toomount hello Azure File share after editing `/etc/fstab` instead of rebooting.</span></span>

## <a name="feedback"></a><span data-ttu-id="876e3-141">Feedback</span><span class="sxs-lookup"><span data-stu-id="876e3-141">Feedback</span></span>
<span data-ttu-id="876e3-142">Linux-gebruikers, willen we toohear van u!</span><span class="sxs-lookup"><span data-stu-id="876e3-142">Linux users, we want toohear from you!</span></span>

<span data-ttu-id="876e3-143">Hello Azure File storage voor Linux gebruikersgroep biedt een forum voor u tooshare feedback terwijl u evalueren en een bestandsopslag op Linux vast.</span><span class="sxs-lookup"><span data-stu-id="876e3-143">hello Azure File storage for Linux users' group provides a forum for you tooshare feedback as you evaluate and adopt File storage on Linux.</span></span> <span data-ttu-id="876e3-144">E-mailadres [Azure File storage Linux gebruikers](mailto:azurefileslinuxusers@microsoft.com) toojoin Hallo gebruikersgroep.</span><span class="sxs-lookup"><span data-stu-id="876e3-144">Email [Azure File storage Linux Users](mailto:azurefileslinuxusers@microsoft.com) toojoin hello users' group.</span></span>

## <a name="next-steps"></a><span data-ttu-id="876e3-145">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="876e3-145">Next steps</span></span>
<span data-ttu-id="876e3-146">Raadpleeg de volgende koppelingen voor meer informatie over Azure File Storage.</span><span class="sxs-lookup"><span data-stu-id="876e3-146">See these links for more information about Azure File storage.</span></span>
* [<span data-ttu-id="876e3-147">Naslaginformatie over REST API voor bestandsservices</span><span class="sxs-lookup"><span data-stu-id="876e3-147">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)
* [<span data-ttu-id="876e3-148">Azure PowerShell gebruiken met Azure storage</span><span class="sxs-lookup"><span data-stu-id="876e3-148">Using Azure PowerShell with Azure storage</span></span>](storage-powershell-guide-full.md)
* [<span data-ttu-id="876e3-149">Hoe toouse AzCopy met Microsoft Azure storage</span><span class="sxs-lookup"><span data-stu-id="876e3-149">How toouse AzCopy with Microsoft Azure storage</span></span>](storage-use-azcopy.md)
* [<span data-ttu-id="876e3-150">Hello Azure CLI gebruiken met Azure storage</span><span class="sxs-lookup"><span data-stu-id="876e3-150">Using hello Azure CLI with Azure storage</span></span>](storage-azure-cli.md#create-and-manage-file-shares)
* [<span data-ttu-id="876e3-151">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="876e3-151">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="876e3-152">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="876e3-152">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)
