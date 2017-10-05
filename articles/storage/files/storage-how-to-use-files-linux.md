---
title: Azure File storage gebruiken met Linux | Microsoft Docs
description: Informatie over het koppelen van een Azure-bestandsshare via SMB op Linux.
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
ms.openlocfilehash: d8987082c559a374b8d19fd69e20cf5e81cb25ef
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-file-storage-with-linux"></a><span data-ttu-id="8cc96-103">Azure File storage gebruiken met Linux</span><span class="sxs-lookup"><span data-stu-id="8cc96-103">Use Azure File storage with Linux</span></span>
<span data-ttu-id="8cc96-104">[Azure File Storage](../storage-dotnet-how-to-use-files.md) is het eenvoudig te gebruiken cloudbestandssysteem van Microsoft.</span><span class="sxs-lookup"><span data-stu-id="8cc96-104">[Azure File storage](../storage-dotnet-how-to-use-files.md) is Microsoft's easy to use cloud file system.</span></span> <span data-ttu-id="8cc96-105">Azure-bestandsshares kunnen worden gekoppeld in Linux-distributies met behulp van de [cifs utils pakket](https://wiki.samba.org/index.php/LinuxCIFS_utils) van de [Samba project](https://www.samba.org/).</span><span class="sxs-lookup"><span data-stu-id="8cc96-105">Azure File shares can be mounted in Linux distributions using the [cifs-utils package](https://wiki.samba.org/index.php/LinuxCIFS_utils) from the [Samba project](https://www.samba.org/).</span></span> <span data-ttu-id="8cc96-106">In dit artikel ziet u twee manieren om een Azure-bestandsshare te koppelen: op aanvraag met de `mount` opdracht en op opstarten door het maken van een vermelding in `/etc/fstab`.</span><span class="sxs-lookup"><span data-stu-id="8cc96-106">This article shows two ways to mount an Azure File share: on-demand with the `mount` command and on-boot by creating an entry in `/etc/fstab`.</span></span>

> [!NOTE]  
> <span data-ttu-id="8cc96-107">Om te koppelen van een Azure-bestandsshare buiten de Azure moet regio die deze wordt gehost in, bijvoorbeeld on-premises of in een andere Azure regio, het besturingssysteem ondersteuning voor de versleutelingsfunctionaliteit van SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="8cc96-107">In order to mount an Azure File share outside of the Azure region it is hosted in, such as on-premises or in a different Azure region, the OS must support the encryption functionality of SMB 3.0.</span></span> <span data-ttu-id="8cc96-108">Coderingsfunctie voor SMB 3.0 voor Linux is geïntroduceerd in 4.11 kernel.</span><span class="sxs-lookup"><span data-stu-id="8cc96-108">Encryption feature for SMB 3.0 for Linux was introduced in 4.11 kernel.</span></span> <span data-ttu-id="8cc96-109">Deze functie kunt koppelen van de bestandsshare in Azure vanaf on-premises of andere Azure-regio.</span><span class="sxs-lookup"><span data-stu-id="8cc96-109">This feature enables mounting of Azure File share from on-premises or a different Azure region.</span></span> <span data-ttu-id="8cc96-110">Op het moment van publicatie is deze functionaliteit backported Ubuntu van 16.04 en hoger.</span><span class="sxs-lookup"><span data-stu-id="8cc96-110">At the time of publishing, this functionality has been backported to Ubuntu from 16.04 and above.</span></span>


## <a name="prerequisities-for-mounting-an-azure-file-share-with-linux-and-the-cifs-utils-package"></a><span data-ttu-id="8cc96-111">Prerequisities voor het koppelen van een Azure-bestand delen met Linux en het pakket cifs-utils</span><span class="sxs-lookup"><span data-stu-id="8cc96-111">Prerequisities for mounting an Azure File share with Linux and the cifs-utils package</span></span>
* <span data-ttu-id="8cc96-112">**Kies een Linux-distributie waarvoor het cifs-utils-pakket geïnstalleerd**: Microsoft raadt u aan de volgende Linux-distributies in de afbeelding voor Azure-galerie:</span><span class="sxs-lookup"><span data-stu-id="8cc96-112">**Pick a Linux distribution that can have the cifs-utils package installed**: Microsoft recommends the following Linux distributions in the Azure image gallery:</span></span>

    * <span data-ttu-id="8cc96-113">Ubuntu Server 14.04 +</span><span class="sxs-lookup"><span data-stu-id="8cc96-113">Ubuntu Server 14.04+</span></span>
    * <span data-ttu-id="8cc96-114">RHEL 7 +</span><span class="sxs-lookup"><span data-stu-id="8cc96-114">RHEL 7+</span></span>
    * <span data-ttu-id="8cc96-115">CentOS 7 +</span><span class="sxs-lookup"><span data-stu-id="8cc96-115">CentOS 7+</span></span>
    * <span data-ttu-id="8cc96-116">Debian 8</span><span class="sxs-lookup"><span data-stu-id="8cc96-116">Debian 8</span></span>
    * <span data-ttu-id="8cc96-117">openSUSE 13.2 +</span><span class="sxs-lookup"><span data-stu-id="8cc96-117">openSUSE 13.2+</span></span>
    * <span data-ttu-id="8cc96-118">SUSE Linux Enterprise Server 12</span><span class="sxs-lookup"><span data-stu-id="8cc96-118">SUSE Linux Enterprise Server 12</span></span>

* <span data-ttu-id="8cc96-119"><a id="install-cifs-utils"></a>**Het pakket cifs-utils is geïnstalleerd**: de cifs-utils kan worden geïnstalleerd met behulp van de package manager op de Linux-distributie van uw keuze.</span><span class="sxs-lookup"><span data-stu-id="8cc96-119"><a id="install-cifs-utils"></a>**The cifs-utils package is installed**: The cifs-utils can be installed using the package manager on the Linux distribution of your choice.</span></span> 

    <span data-ttu-id="8cc96-120">Op **Ubuntu** en **op basis van Debian** distributies, gebruiken de `apt-get` Pakketbeheer:</span><span class="sxs-lookup"><span data-stu-id="8cc96-120">On **Ubuntu** and **Debian-based** distributions, use the `apt-get` package manager:</span></span>

    ```
    sudo apt-get update
    sudo apt-get install cifs-utils
    ```

    <span data-ttu-id="8cc96-121">Op **RHEL** en **CentOS**, gebruiken de `yum` Pakketbeheer:</span><span class="sxs-lookup"><span data-stu-id="8cc96-121">On **RHEL** and **CentOS**, use the `yum` package manager:</span></span>

    ```
    sudo yum install samba-client samba-common cifs-utils
    ```

    <span data-ttu-id="8cc96-122">Op **openSUSE**, gebruiken de `zypper` Pakketbeheer:</span><span class="sxs-lookup"><span data-stu-id="8cc96-122">On **openSUSE**, use the `zypper` package manager:</span></span>

    ```
    sudo zypper install samba*
    ```

    <span data-ttu-id="8cc96-123">Gebruik de juiste package manager op andere distributies of [compileren van bron](https://wiki.samba.org/index.php/LinuxCIFS_utils#Download).</span><span class="sxs-lookup"><span data-stu-id="8cc96-123">On other distributions, use the appropriate package manager or [compile from source](https://wiki.samba.org/index.php/LinuxCIFS_utils#Download).</span></span>

* <span data-ttu-id="8cc96-124">**Bepalen van de map/bestand machtigingen van de gekoppelde share**: In de volgende voorbeelden gebruiken we 0777, om te geven lezen, schrijven en uitvoeren van machtigingen voor alle gebruikers.</span><span class="sxs-lookup"><span data-stu-id="8cc96-124">**Decide on the directory/file permissions of the mounted share**: In the examples below, we use 0777, to give read, write, and execute permissions to all users.</span></span> <span data-ttu-id="8cc96-125">U kunt het vervangen door andere [type chmod machtigingen](https://en.wikipedia.org/wiki/Chmod) naar wens.</span><span class="sxs-lookup"><span data-stu-id="8cc96-125">You can replace it with other [chmod permissions](https://en.wikipedia.org/wiki/Chmod) as desired.</span></span> 

* <span data-ttu-id="8cc96-126">**Naam van het opslagaccount**: voor het koppelen van een Azure-bestandsshare hebt u de naam van het opslagaccount nodig.</span><span class="sxs-lookup"><span data-stu-id="8cc96-126">**Storage Account Name**: To mount an Azure File share, you will need the name of the storage account.</span></span>

* <span data-ttu-id="8cc96-127">**Sleutel van het opslagaccount**: voor het koppelen van een Azure-bestandsshare hebt u de primaire (of secundaire) opslagsleutel nodig.</span><span class="sxs-lookup"><span data-stu-id="8cc96-127">**Storage Account Key**: To mount an Azure File share, you will need the primary (or secondary) storage key.</span></span> <span data-ttu-id="8cc96-128">SAS-sleutels worden momenteel niet ondersteund voor koppelen.</span><span class="sxs-lookup"><span data-stu-id="8cc96-128">SAS keys are not currently supported for mounting.</span></span>

* <span data-ttu-id="8cc96-129">**Zorg ervoor dat poort 445 is geopend**: SMB communiceert via TCP-poort 445 - controleren om te zien als uw firewall niet wordt geblokkeerd door TCP-poorten 445 van client-computer.</span><span class="sxs-lookup"><span data-stu-id="8cc96-129">**Ensure port 445 is open**: SMB communicates over TCP port 445 - check to see if your firewall is not blocking TCP ports 445 from client machine.</span></span>

## <a name="mount-the-azure-file-share-on-demand-with-mount"></a><span data-ttu-id="8cc96-130">De Azure File share op aanvraag met koppelen`mount`</span><span class="sxs-lookup"><span data-stu-id="8cc96-130">Mount the Azure File share on-demand with `mount`</span></span>
1. <span data-ttu-id="8cc96-131">**[Installeer het pakket cifs-utils voor uw Linux-distributie](#install-cifs-utils)**.</span><span class="sxs-lookup"><span data-stu-id="8cc96-131">**[Install the cifs-utils package for your Linux distribution](#install-cifs-utils)**.</span></span>

2. <span data-ttu-id="8cc96-132">**Maak een map voor het koppelpunt**: u kunt hiervoor een willekeurige plaats in het bestandssysteem.</span><span class="sxs-lookup"><span data-stu-id="8cc96-132">**Create a folder for the mount point**: This can be done anywhere on the file system.</span></span>

    ```
    mkdir mymountpoint
    ```

3. <span data-ttu-id="8cc96-133">**Gebruik de koppelopdracht om de Azure-bestandsshare koppelen**: Vervang `<storage-account-name>`, `<share-name>`, en `<storage-account-key>` met de juiste informatie.</span><span class="sxs-lookup"><span data-stu-id="8cc96-133">**Use the mount command to mount the Azure File share**: Remember to replace `<storage-account-name>`, `<share-name>`, and `<storage-account-key>` with the proper information.</span></span>

    ```
    sudo mount -t cifs //<storage-account-name>.file.core.windows.net/<share-name> ./mymountpoint -o vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino
    ```

> [!Note]  
> <span data-ttu-id="8cc96-134">Wanneer u klaar bent met de Azure-bestandsshare, mag u `sudo umount ./mymountpoint` ontkoppelen van de share.</span><span class="sxs-lookup"><span data-stu-id="8cc96-134">When you are done using the Azure File share, you may use `sudo umount ./mymountpoint` to unmount the share.</span></span>

## <a name="create-a-persistent-mount-point-for-the-azure-file-share-with-etcfstab"></a><span data-ttu-id="8cc96-135">Maken van een permanente koppelpunt voor de Azure-bestandsshare met`/etc/fstab`</span><span class="sxs-lookup"><span data-stu-id="8cc96-135">Create a persistent mount point for the Azure File share with `/etc/fstab`</span></span>
1. <span data-ttu-id="8cc96-136">**[Installeer het pakket cifs-utils voor uw Linux-distributie](#install-cifs-utils)**.</span><span class="sxs-lookup"><span data-stu-id="8cc96-136">**[Install the cifs-utils package for your Linux distribution](#install-cifs-utils)**.</span></span>

2. <span data-ttu-id="8cc96-137">**Maak een map voor het koppelpunt**: dit is mogelijk een willekeurige plaats in het bestandssysteem, maar u moet Noteer het absolute pad van de map.</span><span class="sxs-lookup"><span data-stu-id="8cc96-137">**Create a folder for the mount point**: This can be done anywhere on the file system, but you need to note the absolute path of the folder.</span></span> <span data-ttu-id="8cc96-138">Het volgende voorbeeld maakt een map onder de hoofdmap.</span><span class="sxs-lookup"><span data-stu-id="8cc96-138">The following example creates a folder under root.</span></span>

    ```
    sudo mkdir /mymountpoint
    ```

3. <span data-ttu-id="8cc96-139">**Gebruik de volgende opdracht toe te voegen van de volgende regel om `/etc/fstab`** : Vervang `<storage-account-name>`, `<share-name>`, en `<storage-account-key>` met de juiste informatie.</span><span class="sxs-lookup"><span data-stu-id="8cc96-139">**Use the following command to append the following line to `/etc/fstab`**: Remember to replace `<storage-account-name>`, `<share-name>`, and `<storage-account-key>` with the proper information.</span></span>

    ```
    sudo bash -c 'echo "//<storage-account-name>.file.core.windows.net/<share-name> /mymountpoint cifs vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino" >> /etc/fstab'
    ```

> [!Note]  
> <span data-ttu-id="8cc96-140">U kunt `sudo mount -a` koppelen van de Azure-bestandsshare na het bewerken van `/etc/fstab` in plaats van opnieuw opstarten.</span><span class="sxs-lookup"><span data-stu-id="8cc96-140">You can use `sudo mount -a` to mount the Azure File share after editing `/etc/fstab` instead of rebooting.</span></span>

## <a name="feedback"></a><span data-ttu-id="8cc96-141">Feedback</span><span class="sxs-lookup"><span data-stu-id="8cc96-141">Feedback</span></span>
<span data-ttu-id="8cc96-142">Linux-gebruikers, die we willen graag van u!</span><span class="sxs-lookup"><span data-stu-id="8cc96-142">Linux users, we want to hear from you!</span></span>

<span data-ttu-id="8cc96-143">De Azure-bestandsopslag voor Linux gebruikersgroep biedt een forum voor u feedback kunt delen terwijl u evalueren en een bestandsopslag op Linux vast.</span><span class="sxs-lookup"><span data-stu-id="8cc96-143">The Azure File storage for Linux users' group provides a forum for you to share feedback as you evaluate and adopt File storage on Linux.</span></span> <span data-ttu-id="8cc96-144">E-mailadres [Azure File storage Linux gebruikers](mailto:azurefileslinuxusers@microsoft.com) lid worden van de gebruikersgroep.</span><span class="sxs-lookup"><span data-stu-id="8cc96-144">Email [Azure File storage Linux Users](mailto:azurefileslinuxusers@microsoft.com) to join the users' group.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8cc96-145">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8cc96-145">Next steps</span></span>
<span data-ttu-id="8cc96-146">Raadpleeg de volgende koppelingen voor meer informatie over Azure File Storage.</span><span class="sxs-lookup"><span data-stu-id="8cc96-146">See these links for more information about Azure File storage.</span></span>
* [<span data-ttu-id="8cc96-147">Naslaginformatie over REST API voor bestandsservices</span><span class="sxs-lookup"><span data-stu-id="8cc96-147">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)
* [<span data-ttu-id="8cc96-148">AzCopy gebruiken met Microsoft Azure storage</span><span class="sxs-lookup"><span data-stu-id="8cc96-148">How to use AzCopy with Microsoft Azure storage</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)
* [<span data-ttu-id="8cc96-149">De Azure CLI gebruiken met Azure storage</span><span class="sxs-lookup"><span data-stu-id="8cc96-149">Using the Azure CLI with Azure storage</span></span>](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#create-and-manage-file-shares)
* [<span data-ttu-id="8cc96-150">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="8cc96-150">FAQ</span></span>](../storage-files-faq.md)
* [<span data-ttu-id="8cc96-151">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="8cc96-151">Troubleshooting</span></span>](storage-troubleshoot-linux-file-connection-problems.md)
