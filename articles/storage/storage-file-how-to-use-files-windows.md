---
title: een Azure-bestandsshare aaaMount en toegang Hallo delen in Windows | Microsoft Docs
description: Koppel een bestandsshare in Azure en -toegang Hallo share in Windows.
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
ms.openlocfilehash: 15ac468d9d7b8e0a195b024926ed4dd9790360d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="mount-an-azure-file-share-and-access-hello-share-in-windows"></a><span data-ttu-id="21d86-103">Koppelen van een Azure-bestandsshare en -toegang Hallo share in Windows</span><span class="sxs-lookup"><span data-stu-id="21d86-103">Mount an Azure File share and access hello share in Windows</span></span>
<span data-ttu-id="21d86-104">[Azure File storage](storage-dotnet-how-to-use-files.md) is van Microsoft easy toouse cloud-bestandssysteem.</span><span class="sxs-lookup"><span data-stu-id="21d86-104">[Azure File storage](storage-dotnet-how-to-use-files.md) is Microsoft's easy toouse cloud file system.</span></span> <span data-ttu-id="21d86-105">Azure-bestandsshares kunnen worden gekoppeld in Windows en Windows Server.</span><span class="sxs-lookup"><span data-stu-id="21d86-105">Azure File shares can be mounted in Windows and Windows Server.</span></span> <span data-ttu-id="21d86-106">In dit artikel bevat drie verschillende manieren toomount een Azure-bestandsshare op Windows: Hello bestand Explorer-gebruikersinterface via PowerShell en via Hallo opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="21d86-106">This article shows three different ways toomount an Azure File share on Windows: with hello File Explorer UI, via PowerShell, and via hello Command Prompt.</span></span> 

<span data-ttu-id="21d86-107">In de volgorde toomount een Azure-bestand delen buiten hello Azure-regio deze wordt gehost in, bijvoorbeeld on-premises of in een andere Azure-regio, moet de Hallo OS SMB 3.0 ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="21d86-107">In order toomount an Azure File share outside of hello Azure region it is hosted in, such as on-premises or in a different Azure region, hello OS must support SMB 3.0.</span></span> 

<span data-ttu-id="21d86-108">Afhankelijk van de versie van het besturingssysteem kan een Azure-bestandsshare on-premises op een Windows-machine worden gekoppeld of op een virtuele Azure-machine.</span><span class="sxs-lookup"><span data-stu-id="21d86-108">Azure File share can be mounted on Windows machine either on-premises or in Azure VM depending on OS version.</span></span> <span data-ttu-id="21d86-109">Onderstaande tabel ziet u Hallo</span><span class="sxs-lookup"><span data-stu-id="21d86-109">Below table illustrates hello</span></span> 

| <span data-ttu-id="21d86-110">Windows-versie</span><span class="sxs-lookup"><span data-stu-id="21d86-110">Windows Version</span></span>        | <span data-ttu-id="21d86-111">SMB-versie</span><span class="sxs-lookup"><span data-stu-id="21d86-111">SMB Version</span></span> |<span data-ttu-id="21d86-112">Koppelbaar op Azure-VM</span><span class="sxs-lookup"><span data-stu-id="21d86-112">Mountable On Azure VM</span></span>|<span data-ttu-id="21d86-113">Koppelbaar on-premises</span><span class="sxs-lookup"><span data-stu-id="21d86-113">Mountable On-Premise</span></span>|
|------------------------|-------------|---------------------|---------------------|
| <span data-ttu-id="21d86-114">Windows 7</span><span class="sxs-lookup"><span data-stu-id="21d86-114">Windows 7</span></span>              | <span data-ttu-id="21d86-115">SMB 2.1</span><span class="sxs-lookup"><span data-stu-id="21d86-115">SMB 2.1</span></span>     | <span data-ttu-id="21d86-116">Ja</span><span class="sxs-lookup"><span data-stu-id="21d86-116">Yes</span></span>                 | <span data-ttu-id="21d86-117">Nee</span><span class="sxs-lookup"><span data-stu-id="21d86-117">No</span></span>                  |
| <span data-ttu-id="21d86-118">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="21d86-118">Windows Server 2008 R2</span></span> | <span data-ttu-id="21d86-119">SMB 2.1</span><span class="sxs-lookup"><span data-stu-id="21d86-119">SMB 2.1</span></span>     | <span data-ttu-id="21d86-120">Ja</span><span class="sxs-lookup"><span data-stu-id="21d86-120">Yes</span></span>                 | <span data-ttu-id="21d86-121">Nee</span><span class="sxs-lookup"><span data-stu-id="21d86-121">No</span></span>                  |
| <span data-ttu-id="21d86-122">Windows 8</span><span class="sxs-lookup"><span data-stu-id="21d86-122">Windows 8</span></span>              | <span data-ttu-id="21d86-123">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="21d86-123">SMB 3.0</span></span>     | <span data-ttu-id="21d86-124">Ja</span><span class="sxs-lookup"><span data-stu-id="21d86-124">Yes</span></span>                 | <span data-ttu-id="21d86-125">Ja</span><span class="sxs-lookup"><span data-stu-id="21d86-125">Yes</span></span>                 |
| <span data-ttu-id="21d86-126">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="21d86-126">Windows Server 2012</span></span>    | <span data-ttu-id="21d86-127">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="21d86-127">SMB 3.0</span></span>     | <span data-ttu-id="21d86-128">Ja</span><span class="sxs-lookup"><span data-stu-id="21d86-128">Yes</span></span>                 | <span data-ttu-id="21d86-129">Ja</span><span class="sxs-lookup"><span data-stu-id="21d86-129">Yes</span></span>                 |
| <span data-ttu-id="21d86-130">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="21d86-130">Windows Server 2012 R2</span></span> | <span data-ttu-id="21d86-131">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="21d86-131">SMB 3.0</span></span>     | <span data-ttu-id="21d86-132">Ja</span><span class="sxs-lookup"><span data-stu-id="21d86-132">Yes</span></span>                 | <span data-ttu-id="21d86-133">Ja</span><span class="sxs-lookup"><span data-stu-id="21d86-133">Yes</span></span>                 |
| <span data-ttu-id="21d86-134">Windows 10</span><span class="sxs-lookup"><span data-stu-id="21d86-134">Windows 10</span></span>             | <span data-ttu-id="21d86-135">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="21d86-135">SMB 3.0</span></span>     | <span data-ttu-id="21d86-136">Ja</span><span class="sxs-lookup"><span data-stu-id="21d86-136">Yes</span></span>                 | <span data-ttu-id="21d86-137">Ja</span><span class="sxs-lookup"><span data-stu-id="21d86-137">Yes</span></span>                 |

> [!Note]  
> <span data-ttu-id="21d86-138">Aangeraden altijd nemen meest recente KB voor uw versie van Windows hello.</span><span class="sxs-lookup"><span data-stu-id="21d86-138">We always recommend taking hello most recent KB for your version of Windows.</span></span>

## <a name="aprerequisites-for-mounting-azure-file-share-with-windows"></a><span data-ttu-id="21d86-139"></a>Vereisten voor het koppelen van een Azure-bestandsshare met Windows</span><span class="sxs-lookup"><span data-stu-id="21d86-139"></a>Prerequisites for Mounting Azure File Share with Windows</span></span> 
* <span data-ttu-id="21d86-140">**Naam van het opslagaccount**: toomount een Azure-bestand delen, kunt u moet Hallo naam van het opslagaccount Hallo.</span><span class="sxs-lookup"><span data-stu-id="21d86-140">**Storage Account Name**: toomount an Azure File share, you will need hello name of hello storage account.</span></span>

* <span data-ttu-id="21d86-141">**Opslagaccountsleutel**: toomount een Azure-bestand delen, kunt u moet Hallo primaire (of secundaire)-opslagsleutel.</span><span class="sxs-lookup"><span data-stu-id="21d86-141">**Storage Account Key**: toomount an Azure File share, you will need hello primary (or secondary) storage key.</span></span> <span data-ttu-id="21d86-142">SAS-sleutels worden momenteel niet ondersteund voor koppelen.</span><span class="sxs-lookup"><span data-stu-id="21d86-142">SAS keys are not currently supported for mounting.</span></span>

* <span data-ttu-id="21d86-143">**Zorg ervoor dat poort 445 is geopend**: Azure File Storage maakt gebruik van het SMB-protocol.</span><span class="sxs-lookup"><span data-stu-id="21d86-143">**Ensure port 445 is open**: Azure File storage uses SMB protocol.</span></span> <span data-ttu-id="21d86-144">Controleer de toosee SMB communiceert via TCP-poort 445 - als TCP-poort 445 van client-computer niet door uw firewall wordt geblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="21d86-144">SMB communicates over TCP port 445 - check toosee if your firewall is not blocking TCP ports 445 from client machine.</span></span>

## <a name="mount-hello-azure-file-share-with-file-explorer"></a><span data-ttu-id="21d86-145">Hello Azure-bestandsshare met Verkenner koppelen</span><span class="sxs-lookup"><span data-stu-id="21d86-145">Mount hello Azure File share with File Explorer</span></span>
> [!Note]  
> <span data-ttu-id="21d86-146">Let op Hallo van instructies te volgen op Windows 10 worden weergegeven en kunnen enigszins verschillen op oudere versies.</span><span class="sxs-lookup"><span data-stu-id="21d86-146">Note that hello following instructions are shown on Windows 10 and may differ slightly on older releases.</span></span> 

1. <span data-ttu-id="21d86-147">**Open de Verkenner**: dit kan worden gedaan door het openen van Hallo Menu Start of door op de snelkoppeling Win + E.</span><span class="sxs-lookup"><span data-stu-id="21d86-147">**Open File Explorer**: This can be done by opening from hello Start Menu, or by pressing Win+E shortcut.</span></span>

2. <span data-ttu-id="21d86-148">**Navigeer toohello 'Deze PC' item aan de linkerkant Hallo van Hallo-venster. Hiermee wijzigt u Hallo menu's beschikbaar zijn in het Hallo-lint. Selecteer onder menu Computer Hallo 'Stations toewijzen netwerk'**.</span><span class="sxs-lookup"><span data-stu-id="21d86-148">**Navigate toohello "This PC" item on hello left-hand side of hello window. This will change hello menus available in hello ribbon. Under hello Computer menu, select "Map Network Drive"**.</span></span>
    
    ![Een schermopname van de vervolgkeuzelijst Hallo 'Netwerkverbinding maken'](media/storage-file-how-to-use-files-windows/1_MountOnWindows10.png)

3. <span data-ttu-id="21d86-150">**Kopiëren Hallo UNC-pad vanuit Hallo 'Connect' deelvenster in hello Azure-portal**: een gedetailleerde beschrijving van hoe toofind deze informatie vindt u [hier](storage-file-how-to-use-files-portal.md#connect-to-file-share).</span><span class="sxs-lookup"><span data-stu-id="21d86-150">**Copy hello UNC path from hello "Connect" pane in hello Azure portal**: A detailed description of how toofind this information can be found [here](storage-file-how-to-use-files-portal.md#connect-to-file-share).</span></span>

    ![Hallo UNC-pad in hello Azure File storage Connect deelvenster](media/storage-file-how-to-use-files-windows/portal_netuse_connect.png)

4. <span data-ttu-id="21d86-152">**Selecteer Hallo stationsletter en Voer Hallo UNC-pad.**</span><span class="sxs-lookup"><span data-stu-id="21d86-152">**Select hello Drive letter and enter hello UNC path.**</span></span> 
    
    ![Een schermopname van dialoogvenster voor Hallo 'Stations toewijzen netwerk'](media/storage-file-how-to-use-files-windows/2_MountOnWindows10.png)

5. <span data-ttu-id="21d86-154">**Gebruik Hallo Opslagaccountnaam voorafgegaan door `Azure\` als Hallo gebruikersnaam en de sleutel van een Opslagaccount als Hallo wachtwoord.**</span><span class="sxs-lookup"><span data-stu-id="21d86-154">**Use hello Storage Account Name prepended with `Azure\` as hello username and a Storage Account Key as hello password.**</span></span>
    
    ![Een schermopname van dialoogvenster voor gebruikersreferenties Hallo-netwerk](media/storage-file-how-to-use-files-windows/3_MountOnWindows10.png)

6. <span data-ttu-id="21d86-156">**Gebruik de Azure-bestandsshare naar wens**.</span><span class="sxs-lookup"><span data-stu-id="21d86-156">**Use Azure File share as desired**.</span></span>
    
    ![De Azure-bestandsshare is nu gekoppeld](media/storage-file-how-to-use-files-windows/4_MountOnWindows10.png)

7. <span data-ttu-id="21d86-158">**Wanneer u klaar toodismount (of Verbreek de verbinding met) hello Azure-bestandsshare, kunt u doen door met de rechtermuisknop te klikken op Hallo-vermelding voor de share Hallo onder Hallo 'netwerklocaties' in Windows Verkenner en 'Verbinding verbreken'**.</span><span class="sxs-lookup"><span data-stu-id="21d86-158">**When you are ready toodismount (or disconnect) hello Azure File share, you can do so by right clicking on hello entry for hello share under hello "Network locations" in File Explorer and selecting "Disconnect"**.</span></span>

## <a name="mount-hello-azure-file-share-with-powershell"></a><span data-ttu-id="21d86-159">Hello Azure-bestandsshare met PowerShell koppelen</span><span class="sxs-lookup"><span data-stu-id="21d86-159">Mount hello Azure File share with PowerShell</span></span>
1. <span data-ttu-id="21d86-160">**Gebruik Hallo volgende opdracht toomount hello Azure-bestandsshare**: onthouden tooreplace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` met de juiste informatie Hallo.</span><span class="sxs-lookup"><span data-stu-id="21d86-160">**Use hello following command toomount hello Azure File share**: Remember tooreplace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` with hello proper information.</span></span>

    ```PowerShell
    $acctKey = ConvertTo-SecureString -String "<storage-account-key>" -AsPlainText -Force
    $credential = New-Object System.Management.Automation.PSCredential -ArgumentList "Azure\<storage-account-name>", $acctKey
    New-PSDrive -Name <desired-drive-letter> -PSProvider FileSystem -Root "\\<storage-account-name>.file.core.windows.net\<share-name>" -Credential $credential
    ```

2. <span data-ttu-id="21d86-161">**Gebruik hello Azure-bestandsshare naar wens**.</span><span class="sxs-lookup"><span data-stu-id="21d86-161">**Use hello Azure File share as desired**.</span></span>

3. <span data-ttu-id="21d86-162">**Wanneer u klaar bent, ontkoppelen Hallo bestandsshare in Azure met behulp van de volgende opdracht Hallo**.</span><span class="sxs-lookup"><span data-stu-id="21d86-162">**When you are finished, dismount hello Azure File share using hello following command**.</span></span>

    ```PowerShell
    Remove-PSDrive -Name <desired-drive-letter>
    ```

> [!Note]  
> <span data-ttu-id="21d86-163">U kunt op Hallo `-Persist` parameter op `New-PSDrive` toomake hello Azure File share zichtbaar toohello rest Hallo OS terwijl gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="21d86-163">You may use hello `-Persist` parameter on `New-PSDrive` toomake hello Azure File share visible toohello rest of hello OS while mounted.</span></span>

## <a name="mount-hello-azure-file-share-with-command-prompt"></a><span data-ttu-id="21d86-164">Hello Azure-bestandsshare bij de opdrachtprompt koppelen</span><span class="sxs-lookup"><span data-stu-id="21d86-164">Mount hello Azure File share with Command Prompt</span></span>
1. <span data-ttu-id="21d86-165">**Gebruik Hallo volgende opdracht toomount hello Azure-bestandsshare**: onthouden tooreplace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` met de juiste informatie Hallo.</span><span class="sxs-lookup"><span data-stu-id="21d86-165">**Use hello following command toomount hello Azure File share**: Remember tooreplace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` with hello proper information.</span></span>

    ```
    net use <desired-drive-letter>: \\<storage-account-name>.file.core.windows.net\<share-name> <storage-account-key> /user:Azure\<storage-account-name>
    ```

2. <span data-ttu-id="21d86-166">**Gebruik hello Azure-bestandsshare naar wens**.</span><span class="sxs-lookup"><span data-stu-id="21d86-166">**Use hello Azure File share as desired**.</span></span>

3. <span data-ttu-id="21d86-167">**Wanneer u klaar bent, ontkoppelen Hallo bestandsshare in Azure met behulp van de volgende opdracht Hallo**.</span><span class="sxs-lookup"><span data-stu-id="21d86-167">**When you are finished, dismount hello Azure File share using hello following command**.</span></span>

    ```
    net use <desired-drive-letter>: /delete
    ```

> [!Note]  
> <span data-ttu-id="21d86-168">U kunt hello Azure File share tooautomatically opnieuw configureren op opnieuw opstarten persisting Hallo-referenties in Windows.</span><span class="sxs-lookup"><span data-stu-id="21d86-168">You can configure hello Azure File share tooautomatically reconnect on reboot by persisting hello credentials in Windows.</span></span> <span data-ttu-id="21d86-169">Hallo na de opdracht bewaard Hallo referenties:</span><span class="sxs-lookup"><span data-stu-id="21d86-169">hello following command will persist hello credentials:</span></span>
>   ```
>   cmdkey /add:<storage-account-name>.file.core.windows.net /user:AZURE\<storage-account-name> /pass:<storage-account-key>
>   ```

## <a name="next-steps"></a><span data-ttu-id="21d86-170">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="21d86-170">Next steps</span></span>
<span data-ttu-id="21d86-171">Raadpleeg de volgende koppelingen voor meer informatie over Azure File Storage.</span><span class="sxs-lookup"><span data-stu-id="21d86-171">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="21d86-172">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="21d86-172">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="21d86-173">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="21d86-173">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)

### <a name="conceptual-articles-and-videos"></a><span data-ttu-id="21d86-174">Conceptuele artikelen en video's</span><span class="sxs-lookup"><span data-stu-id="21d86-174">Conceptual articles and videos</span></span>
* [<span data-ttu-id="21d86-175">Azure File Storage: een naadloos SMB-bestandssysteem voor Windows en Linux</span><span class="sxs-lookup"><span data-stu-id="21d86-175">Azure File storage: a frictionless cloud SMB file system for Windows and Linux</span></span>](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
* [<span data-ttu-id="21d86-176">Hoe toouse Azure File storage met Linux</span><span class="sxs-lookup"><span data-stu-id="21d86-176">How toouse Azure File storage with Linux</span></span>](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-azure-file-storage"></a><span data-ttu-id="21d86-177">Hulpprogramma-ondersteuning voor Azure File Storage</span><span class="sxs-lookup"><span data-stu-id="21d86-177">Tooling support for Azure File storage</span></span>
* [<span data-ttu-id="21d86-178">Azure PowerShell gebruiken met Azure Storage</span><span class="sxs-lookup"><span data-stu-id="21d86-178">Using Azure PowerShell with Azure Storage</span></span>](storage-powershell-guide-full.md)
* [<span data-ttu-id="21d86-179">Hoe toouse AzCopy met Microsoft Azure Storage</span><span class="sxs-lookup"><span data-stu-id="21d86-179">How toouse AzCopy with Microsoft Azure Storage</span></span>](storage-use-azcopy.md)
* [<span data-ttu-id="21d86-180">Hello Azure CLI gebruiken met Azure Storage</span><span class="sxs-lookup"><span data-stu-id="21d86-180">Using hello Azure CLI with Azure Storage</span></span>](storage-azure-cli.md#create-and-manage-file-shares)
* [<span data-ttu-id="21d86-181">Problemen met betrekking tot Azure File Storage oplossen</span><span class="sxs-lookup"><span data-stu-id="21d86-181">Troubleshooting Azure File storage problems</span></span>](https://docs.microsoft.com/azure/storage/storage-troubleshoot-file-connection-problems)

### <a name="blog-posts"></a><span data-ttu-id="21d86-182">Blogberichten</span><span class="sxs-lookup"><span data-stu-id="21d86-182">Blog posts</span></span>
* [<span data-ttu-id="21d86-183">Azure File storage is now generally available (Azure File Storage is nu algemeen beschikbaar)</span><span class="sxs-lookup"><span data-stu-id="21d86-183">Azure File storage is now generally available</span></span>](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [<span data-ttu-id="21d86-184">Inside Azure File Storage (Een kijkje achter de schermen van Azure File Storage)</span><span class="sxs-lookup"><span data-stu-id="21d86-184">Inside Azure File storage</span></span>](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [<span data-ttu-id="21d86-185">Introducing Microsoft Azure File Service (Introductie van Microsoft Azure File-service)</span><span class="sxs-lookup"><span data-stu-id="21d86-185">Introducing Microsoft Azure File Service</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [<span data-ttu-id="21d86-186">Migreren gegevens tooAzure bestand</span><span class="sxs-lookup"><span data-stu-id="21d86-186">Migrating data tooAzure File </span></span>](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)

### <a name="reference"></a><span data-ttu-id="21d86-187">Naslaginformatie</span><span class="sxs-lookup"><span data-stu-id="21d86-187">Reference</span></span>
* [<span data-ttu-id="21d86-188">Naslaginformatie over de Storage-clientbibliotheek voor .NET</span><span class="sxs-lookup"><span data-stu-id="21d86-188">Storage Client Library for .NET reference</span></span>](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [<span data-ttu-id="21d86-189">Naslaginformatie over REST API voor bestandsservices</span><span class="sxs-lookup"><span data-stu-id="21d86-189">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)
