---
title: Een Azure-bestandsshare koppelen en de share openen in Windows | Microsoft Docs
description: Een Azure-bestandsshare koppelen en de share openen in Windows.
services: storage
documentationcenter: na
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: e911e787cd1e29b2bbeaa648869c50245f2dd9ba
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/29/2017
---
# <a name="mount-an-azure-file-share-and-access-the-share-in-windows"></a><span data-ttu-id="58cf4-103">Een Azure-bestandsshare koppelen en de share openen in Windows</span><span class="sxs-lookup"><span data-stu-id="58cf4-103">Mount an Azure File share and access the share in Windows</span></span>
<span data-ttu-id="58cf4-104">[Azure File Storage](storage-dotnet-how-to-use-files.md) is het eenvoudig te gebruiken cloudbestandssysteem van Microsoft.</span><span class="sxs-lookup"><span data-stu-id="58cf4-104">[Azure File storage](storage-dotnet-how-to-use-files.md) is Microsoft's easy to use cloud file system.</span></span> <span data-ttu-id="58cf4-105">Azure-bestandsshares kunnen worden gekoppeld in Windows en Windows Server.</span><span class="sxs-lookup"><span data-stu-id="58cf4-105">Azure File shares can be mounted in Windows and Windows Server.</span></span> <span data-ttu-id="58cf4-106">In dit artikel ziet u drie verschillende manieren om een Azure-bestandsshare in Windows te koppelen: met de File Explorer-gebruikersinterface, via PowerShell en via de opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="58cf4-106">This article shows three different ways to mount an Azure File share on Windows: with the File Explorer UI, via PowerShell, and via the Command Prompt.</span></span> 

<span data-ttu-id="58cf4-107">Als u een Azure-bestandsshare wilt koppelen buiten de Azure-regio waarin deze wordt gehost, bijvoorbeeld on-premises of in een andere Azure-regio, moet het besturingssysteem ondersteuning bieden voor SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="58cf4-107">In order to mount an Azure File share outside of the Azure region it is hosted in, such as on-premises or in a different Azure region, the OS must support SMB 3.0.</span></span> 

<span data-ttu-id="58cf4-108">Afhankelijk van de versie van het besturingssysteem kan een Azure-bestandsshare on-premises op een Windows-machine worden gekoppeld of op een virtuele Azure-machine.</span><span class="sxs-lookup"><span data-stu-id="58cf4-108">Azure File share can be mounted on Windows machine either on-premises or in Azure VM depending on OS version.</span></span> <span data-ttu-id="58cf4-109">In de onderstaande tabel ziet u de mogelijkheden:</span><span class="sxs-lookup"><span data-stu-id="58cf4-109">Below table illustrates the</span></span> 

| <span data-ttu-id="58cf4-110">Windows-versie</span><span class="sxs-lookup"><span data-stu-id="58cf4-110">Windows Version</span></span>        | <span data-ttu-id="58cf4-111">SMB-versie</span><span class="sxs-lookup"><span data-stu-id="58cf4-111">SMB Version</span></span> |<span data-ttu-id="58cf4-112">Koppelbaar op Azure-VM</span><span class="sxs-lookup"><span data-stu-id="58cf4-112">Mountable On Azure VM</span></span>|<span data-ttu-id="58cf4-113">Koppelbaar on-premises</span><span class="sxs-lookup"><span data-stu-id="58cf4-113">Mountable On-Premise</span></span>|
|------------------------|-------------|---------------------|---------------------|
| <span data-ttu-id="58cf4-114">Windows 7</span><span class="sxs-lookup"><span data-stu-id="58cf4-114">Windows 7</span></span>              | <span data-ttu-id="58cf4-115">SMB 2.1</span><span class="sxs-lookup"><span data-stu-id="58cf4-115">SMB 2.1</span></span>     | <span data-ttu-id="58cf4-116">Ja</span><span class="sxs-lookup"><span data-stu-id="58cf4-116">Yes</span></span>                 | <span data-ttu-id="58cf4-117">Nee</span><span class="sxs-lookup"><span data-stu-id="58cf4-117">No</span></span>                  |
| <span data-ttu-id="58cf4-118">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="58cf4-118">Windows Server 2008 R2</span></span> | <span data-ttu-id="58cf4-119">SMB 2.1</span><span class="sxs-lookup"><span data-stu-id="58cf4-119">SMB 2.1</span></span>     | <span data-ttu-id="58cf4-120">Ja</span><span class="sxs-lookup"><span data-stu-id="58cf4-120">Yes</span></span>                 | <span data-ttu-id="58cf4-121">Nee</span><span class="sxs-lookup"><span data-stu-id="58cf4-121">No</span></span>                  |
| <span data-ttu-id="58cf4-122">Windows 8</span><span class="sxs-lookup"><span data-stu-id="58cf4-122">Windows 8</span></span>              | <span data-ttu-id="58cf4-123">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="58cf4-123">SMB 3.0</span></span>     | <span data-ttu-id="58cf4-124">Ja</span><span class="sxs-lookup"><span data-stu-id="58cf4-124">Yes</span></span>                 | <span data-ttu-id="58cf4-125">Ja</span><span class="sxs-lookup"><span data-stu-id="58cf4-125">Yes</span></span>                 |
| <span data-ttu-id="58cf4-126">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="58cf4-126">Windows Server 2012</span></span>    | <span data-ttu-id="58cf4-127">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="58cf4-127">SMB 3.0</span></span>     | <span data-ttu-id="58cf4-128">Ja</span><span class="sxs-lookup"><span data-stu-id="58cf4-128">Yes</span></span>                 | <span data-ttu-id="58cf4-129">Ja</span><span class="sxs-lookup"><span data-stu-id="58cf4-129">Yes</span></span>                 |
| <span data-ttu-id="58cf4-130">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="58cf4-130">Windows Server 2012 R2</span></span> | <span data-ttu-id="58cf4-131">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="58cf4-131">SMB 3.0</span></span>     | <span data-ttu-id="58cf4-132">Ja</span><span class="sxs-lookup"><span data-stu-id="58cf4-132">Yes</span></span>                 | <span data-ttu-id="58cf4-133">Ja</span><span class="sxs-lookup"><span data-stu-id="58cf4-133">Yes</span></span>                 |
| <span data-ttu-id="58cf4-134">Windows 10</span><span class="sxs-lookup"><span data-stu-id="58cf4-134">Windows 10</span></span>             | <span data-ttu-id="58cf4-135">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="58cf4-135">SMB 3.0</span></span>     | <span data-ttu-id="58cf4-136">Ja</span><span class="sxs-lookup"><span data-stu-id="58cf4-136">Yes</span></span>                 | <span data-ttu-id="58cf4-137">Ja</span><span class="sxs-lookup"><span data-stu-id="58cf4-137">Yes</span></span>                 |

> [!Note]  
> <span data-ttu-id="58cf4-138">We raden altijd aan de meest recente KB voor uw versie van Windows te nemen.</span><span class="sxs-lookup"><span data-stu-id="58cf4-138">We always recommend taking the most recent KB for your version of Windows.</span></span>

## <a name="aprerequisites-for-mounting-azure-file-share-with-windows"></a><span data-ttu-id="58cf4-139"></a>Vereisten voor het koppelen van een Azure-bestandsshare met Windows</span><span class="sxs-lookup"><span data-stu-id="58cf4-139"></a>Prerequisites for Mounting Azure File Share with Windows</span></span> 
* <span data-ttu-id="58cf4-140">**Naam van het opslagaccount**: voor het koppelen van een Azure-bestandsshare hebt u de naam van het opslagaccount nodig.</span><span class="sxs-lookup"><span data-stu-id="58cf4-140">**Storage Account Name**: To mount an Azure File share, you will need the name of the storage account.</span></span>

* <span data-ttu-id="58cf4-141">**Sleutel van het opslagaccount**: voor het koppelen van een Azure-bestandsshare hebt u de primaire (of secundaire) opslagsleutel nodig.</span><span class="sxs-lookup"><span data-stu-id="58cf4-141">**Storage Account Key**: To mount an Azure File share, you will need the primary (or secondary) storage key.</span></span> <span data-ttu-id="58cf4-142">SAS-sleutels worden momenteel niet ondersteund voor koppelen.</span><span class="sxs-lookup"><span data-stu-id="58cf4-142">SAS keys are not currently supported for mounting.</span></span>

* <span data-ttu-id="58cf4-143">**Zorg ervoor dat poort 445 is geopend**: Azure File Storage maakt gebruik van het SMB-protocol.</span><span class="sxs-lookup"><span data-stu-id="58cf4-143">**Ensure port 445 is open**: Azure File storage uses SMB protocol.</span></span> <span data-ttu-id="58cf4-144">SMB communiceert via TCP-poort 445 - controleer of de TCP-poort 445 van de clientcomputer niet door uw firewall wordt geblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="58cf4-144">SMB communicates over TCP port 445 - check to see if your firewall is not blocking TCP ports 445 from client machine.</span></span>

## <a name="mount-the-azure-file-share-with-file-explorer"></a><span data-ttu-id="58cf4-145">De Azure-bestandsshare koppelen met de Verkenner</span><span class="sxs-lookup"><span data-stu-id="58cf4-145">Mount the Azure File share with File Explorer</span></span>
> [!Note]  
> <span data-ttu-id="58cf4-146">Houd er rekening mee dat de volgende instructies worden weergegeven in Windows 10 en enigszins kunnen verschillen in oudere versies.</span><span class="sxs-lookup"><span data-stu-id="58cf4-146">Note that the following instructions are shown on Windows 10 and may differ slightly on older releases.</span></span> 

1. <span data-ttu-id="58cf4-147">**Open de Verkenner**: dit kan worden gedaan door deze te openen vanuit het menu Start of door op de snelkoppeling Win + E te drukken.</span><span class="sxs-lookup"><span data-stu-id="58cf4-147">**Open File Explorer**: This can be done by opening from the Start Menu, or by pressing Win+E shortcut.</span></span>

2. <span data-ttu-id="58cf4-148">**Ga naar het item 'Deze pc' aan de linkerkant van het venster. Hiermee wijzigt u de menu's die beschikbaar zijn in het lint. Selecteer in het menu Computer 'Netwerkverbinding maken'**.</span><span class="sxs-lookup"><span data-stu-id="58cf4-148">**Navigate to the "This PC" item on the left-hand side of the window. This will change the menus available in the ribbon. Under the Computer menu, select "Map Network Drive"**.</span></span>
    
    ![Een schermafbeelding van de vervolgkeuzelijst 'Netwerkverbinding maken'](media/storage-file-how-to-use-files-windows/1_MountOnWindows10.png)

3. <span data-ttu-id="58cf4-150">**Kopieer het UNC-pad van het deelvenster 'Verbinding maken' in Azure Portal**: een gedetailleerde beschrijving van het zoeken van deze informatie vindt u [hier](storage-file-how-to-use-files-portal.md#connect-to-file-share).</span><span class="sxs-lookup"><span data-stu-id="58cf4-150">**Copy the UNC path from the "Connect" pane in the Azure portal**: A detailed description of how to find this information can be found [here](storage-file-how-to-use-files-portal.md#connect-to-file-share).</span></span>

    ![Het UNC-pad in het deelvenster Verbinding maken van Azure File Storage](media/storage-file-how-to-use-files-windows/portal_netuse_connect.png)

4. <span data-ttu-id="58cf4-152">**Selecteer de stationsletter en voer het UNC-pad in.**</span><span class="sxs-lookup"><span data-stu-id="58cf4-152">**Select the Drive letter and enter the UNC path.**</span></span> 
    
    ![Een schermafbeelding van het dialoogvenster 'Netwerkverbinding maken'](media/storage-file-how-to-use-files-windows/2_MountOnWindows10.png)

5. <span data-ttu-id="58cf4-154">**Gebruik de opslagaccountnaam voorafgegaan door `Azure\` als de gebruikersnaam en een toegangssleutel als het wachtwoord.**</span><span class="sxs-lookup"><span data-stu-id="58cf4-154">**Use the Storage Account Name prepended with `Azure\` as the username and a Storage Account Key as the password.**</span></span>
    
    ![Een schermafbeelding van het dialoogvenster voor netwerkreferenties](media/storage-file-how-to-use-files-windows/3_MountOnWindows10.png)

6. <span data-ttu-id="58cf4-156">**Gebruik de Azure-bestandsshare naar wens**.</span><span class="sxs-lookup"><span data-stu-id="58cf4-156">**Use Azure File share as desired**.</span></span>
    
    ![De Azure-bestandsshare is nu gekoppeld](media/storage-file-how-to-use-files-windows/4_MountOnWindows10.png)

7. <span data-ttu-id="58cf4-158">**Wanneer u klaar bent om de Azure-bestandsshare te ontkoppelen (of de verbinding te verbreken), kunt u dit doen door met de rechtermuisknop in de Verkenner op de vermelding voor de share onder 'Netwerklocaties' te klikken en 'Verbinding verbreken' te selecteren**.</span><span class="sxs-lookup"><span data-stu-id="58cf4-158">**When you are ready to dismount (or disconnect) the Azure File share, you can do so by right clicking on the entry for the share under the "Network locations" in File Explorer and selecting "Disconnect"**.</span></span>

## <a name="mount-the-azure-file-share-with-powershell"></a><span data-ttu-id="58cf4-159">De Azure-bestandsshare koppelen met PowerShell</span><span class="sxs-lookup"><span data-stu-id="58cf4-159">Mount the Azure File share with PowerShell</span></span>
1. <span data-ttu-id="58cf4-160">**Gebruik de volgende opdracht om de Azure-bestandsshare te koppelen**: vervang `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` door de juiste informatie.</span><span class="sxs-lookup"><span data-stu-id="58cf4-160">**Use the following command to mount the Azure File share**: Remember to replace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` with the proper information.</span></span>

    ```PowerShell
    $acctKey = ConvertTo-SecureString -String "<storage-account-key>" -AsPlainText -Force
    $credential = New-Object System.Management.Automation.PSCredential -ArgumentList "Azure\<storage-account-name>", $acctKey
    New-PSDrive -Name <desired-drive-letter> -PSProvider FileSystem -Root "\\<storage-account-name>.file.core.windows.net\<share-name>" -Credential $credential
    ```

2. <span data-ttu-id="58cf4-161">**Gebruik de Azure-bestandsshare naar wens**.</span><span class="sxs-lookup"><span data-stu-id="58cf4-161">**Use the Azure File share as desired**.</span></span>

3. <span data-ttu-id="58cf4-162">**Wanneer u klaar bent, ontkoppelt u de Azure-bestandsshare met de volgende opdracht**.</span><span class="sxs-lookup"><span data-stu-id="58cf4-162">**When you are finished, dismount the Azure File share using the following command**.</span></span>

    ```PowerShell
    Remove-PSDrive -Name <desired-drive-letter>
    ```

> [!Note]  
> <span data-ttu-id="58cf4-163">U kunt de parameter `-Persist` in `New-PSDrive` gebruiken om de Azure-bestandsshare zichtbaar maken voor de rest van het besturingssysteem als deze is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="58cf4-163">You may use the `-Persist` parameter on `New-PSDrive` to make the Azure File share visible to the rest of the OS while mounted.</span></span>

## <a name="mount-the-azure-file-share-with-command-prompt"></a><span data-ttu-id="58cf4-164">De Azure-bestandsshare koppelen met de opdrachtprompt</span><span class="sxs-lookup"><span data-stu-id="58cf4-164">Mount the Azure File share with Command Prompt</span></span>
1. <span data-ttu-id="58cf4-165">**Gebruik de volgende opdracht om de Azure-bestandsshare te koppelen**: vervang `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` door de juiste informatie.</span><span class="sxs-lookup"><span data-stu-id="58cf4-165">**Use the following command to mount the Azure File share**: Remember to replace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` with the proper information.</span></span>

    ```
    net use <desired-drive-letter>: \\<storage-account-name>.file.core.windows.net\<share-name> <storage-account-key> /user:Azure\<storage-account-name>
    ```

2. <span data-ttu-id="58cf4-166">**Gebruik de Azure-bestandsshare naar wens**.</span><span class="sxs-lookup"><span data-stu-id="58cf4-166">**Use the Azure File share as desired**.</span></span>

3. <span data-ttu-id="58cf4-167">**Wanneer u klaar bent, ontkoppelt u de Azure-bestandsshare met de volgende opdracht**.</span><span class="sxs-lookup"><span data-stu-id="58cf4-167">**When you are finished, dismount the Azure File share using the following command**.</span></span>

    ```
    net use <desired-drive-letter>: /delete
    ```

> [!Note]  
> <span data-ttu-id="58cf4-168">U kunt de Azure-bestandsshare configureren om automatisch opnieuw verbinding te maken bij opnieuw opstarten door de Windows-referenties persistent te maken.</span><span class="sxs-lookup"><span data-stu-id="58cf4-168">You can configure the Azure File share to automatically reconnect on reboot by persisting the credentials in Windows.</span></span> <span data-ttu-id="58cf4-169">Met de volgende opdracht worden de referenties persistent gemaakt:</span><span class="sxs-lookup"><span data-stu-id="58cf4-169">The following command will persist the credentials:</span></span>
>   ```
>   cmdkey /add:<storage-account-name>.file.core.windows.net /user:AZURE\<storage-account-name> /pass:<storage-account-key>
>   ```

## <a name="next-steps"></a><span data-ttu-id="58cf4-170">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="58cf4-170">Next steps</span></span>
<span data-ttu-id="58cf4-171">Raadpleeg de volgende koppelingen voor meer informatie over Azure File Storage.</span><span class="sxs-lookup"><span data-stu-id="58cf4-171">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="58cf4-172">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="58cf4-172">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="58cf4-173">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="58cf4-173">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)

### <a name="conceptual-articles-and-videos"></a><span data-ttu-id="58cf4-174">Conceptuele artikelen en video's</span><span class="sxs-lookup"><span data-stu-id="58cf4-174">Conceptual articles and videos</span></span>
* [<span data-ttu-id="58cf4-175">Azure File Storage: een naadloos SMB-bestandssysteem voor Windows en Linux</span><span class="sxs-lookup"><span data-stu-id="58cf4-175">Azure File storage: a frictionless cloud SMB file system for Windows and Linux</span></span>](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
* [<span data-ttu-id="58cf4-176">Azure File Storage gebruiken met Linux</span><span class="sxs-lookup"><span data-stu-id="58cf4-176">How to use Azure File storage with Linux</span></span>](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-azure-file-storage"></a><span data-ttu-id="58cf4-177">Hulpprogramma-ondersteuning voor Azure File Storage</span><span class="sxs-lookup"><span data-stu-id="58cf4-177">Tooling support for Azure File storage</span></span>
* [<span data-ttu-id="58cf4-178">Azure PowerShell gebruiken met Azure Storage</span><span class="sxs-lookup"><span data-stu-id="58cf4-178">Using Azure PowerShell with Azure Storage</span></span>](storage-powershell-guide-full.md)
* [<span data-ttu-id="58cf4-179">AzCopy gebruiken met Microsoft Azure Storage</span><span class="sxs-lookup"><span data-stu-id="58cf4-179">How to use AzCopy with Microsoft Azure Storage</span></span>](storage-use-azcopy.md)
* [<span data-ttu-id="58cf4-180">De Azure CLI gebruiken met Azure Storage</span><span class="sxs-lookup"><span data-stu-id="58cf4-180">Using the Azure CLI with Azure Storage</span></span>](storage-azure-cli.md#create-and-manage-file-shares)
* [<span data-ttu-id="58cf4-181">Problemen met betrekking tot Azure File Storage oplossen</span><span class="sxs-lookup"><span data-stu-id="58cf4-181">Troubleshooting Azure File storage problems</span></span>](https://docs.microsoft.com/azure/storage/storage-troubleshoot-file-connection-problems)

### <a name="blog-posts"></a><span data-ttu-id="58cf4-182">Blogberichten</span><span class="sxs-lookup"><span data-stu-id="58cf4-182">Blog posts</span></span>
* [<span data-ttu-id="58cf4-183">Azure File storage is now generally available (Azure File Storage is nu algemeen beschikbaar)</span><span class="sxs-lookup"><span data-stu-id="58cf4-183">Azure File storage is now generally available</span></span>](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [<span data-ttu-id="58cf4-184">Inside Azure File Storage (Een kijkje achter de schermen van Azure File Storage)</span><span class="sxs-lookup"><span data-stu-id="58cf4-184">Inside Azure File storage</span></span>](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [<span data-ttu-id="58cf4-185">Introducing Microsoft Azure File Service (Introductie van Microsoft Azure File-service)</span><span class="sxs-lookup"><span data-stu-id="58cf4-185">Introducing Microsoft Azure File Service</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [<span data-ttu-id="58cf4-186">Gegevens migreren naar Azure File Storage</span><span class="sxs-lookup"><span data-stu-id="58cf4-186">Migrating data to Azure File </span></span>](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)

### <a name="reference"></a><span data-ttu-id="58cf4-187">Naslaginformatie</span><span class="sxs-lookup"><span data-stu-id="58cf4-187">Reference</span></span>
* [<span data-ttu-id="58cf4-188">Naslaginformatie over de Storage-clientbibliotheek voor .NET</span><span class="sxs-lookup"><span data-stu-id="58cf4-188">Storage Client Library for .NET reference</span></span>](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [<span data-ttu-id="58cf4-189">Naslaginformatie over REST API voor bestandsservices</span><span class="sxs-lookup"><span data-stu-id="58cf4-189">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)
