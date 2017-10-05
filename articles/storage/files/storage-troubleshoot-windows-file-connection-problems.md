---
title: Problemen met Azure File storage in Windows | Microsoft Docs
description: Problemen met Azure File storage in Windows
services: storage
documentationcenter: 
author: genlin
manager: willchen
editor: na
tags: storage
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: genli
ms.openlocfilehash: daaf7d0589f5e2d82b43dad879bffd23370a2c81
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshoot-azure-file-storage-problems-in-windows"></a><span data-ttu-id="02be0-103">Problemen met Azure File storage in Windows</span><span class="sxs-lookup"><span data-stu-id="02be0-103">Troubleshoot Azure File storage problems in Windows</span></span>

<span data-ttu-id="02be0-104">Dit artikel worden veelvoorkomende problemen die betrekking op Microsoft Azure File storage hebben wanneer u verbinding vanaf een Windows-clients maakt.</span><span class="sxs-lookup"><span data-stu-id="02be0-104">This article lists common problems that are related to Microsoft Azure File storage when you connect from Windows clients.</span></span> <span data-ttu-id="02be0-105">Het bevat ook mogelijke oorzaken en oplossingen voor deze problemen.</span><span class="sxs-lookup"><span data-stu-id="02be0-105">It also provides possible causes and resolutions for these problems.</span></span> <span data-ttu-id="02be0-106">Naast de stappen voor probleemoplossing in dit artikel kunt u ook gebruiken [AzFileDiagnostics](https://gallery.technet.microsoft.com/Troubleshooting-tool-for-a9fa1fe5) om ervoor te zorgen dat de Windows client-omgeving juist vereisten.</span><span class="sxs-lookup"><span data-stu-id="02be0-106">In addition to the troubleshooting steps in this article, you can also use [AzFileDiagnostics](https://gallery.technet.microsoft.com/Troubleshooting-tool-for-a9fa1fe5) to ensure that the Windows client environment has correct prerequisites.</span></span> <span data-ttu-id="02be0-107">AzFileDiagnostics automatiseert detectie van de meeste van de problemen die worden vermeld in dit artikel en helpt bij het instellen van uw omgeving om optimale prestaties te behalen.</span><span class="sxs-lookup"><span data-stu-id="02be0-107">AzFileDiagnostics automates detection of most of the symptoms mentioned in this article and helps set up your environment to get optimal performance.</span></span> <span data-ttu-id="02be0-108">U kunt ook deze informatie vinden in de [Azure-bestandsshares probleemoplosser](https://support.microsoft.com/help/4022301/troubleshooter-for-azure-files-shares) die bevat stappen om u te helpen problemen verbinden/toewijzing/koppelen Azure-bestandsshares.</span><span class="sxs-lookup"><span data-stu-id="02be0-108">You can also find this information in the [Azure Files shares Troubleshooter](https://support.microsoft.com/help/4022301/troubleshooter-for-azure-files-shares) that provides steps to assist you with problems connecting/mapping/mounting Azure Files shares.</span></span>


<a id="error53-67-87"></a>
## <a name="error-53-error-67-or-error-87-when-you-mount-or-unmount-an-azure-file-share"></a><span data-ttu-id="02be0-109">Fout 53, fout 67 of fout 87 wanneer u koppelen of ontkoppelen van een Azure-bestandsshare</span><span class="sxs-lookup"><span data-stu-id="02be0-109">Error 53, Error 67, or Error 87 when you mount or unmount an Azure file share</span></span>

<span data-ttu-id="02be0-110">Wanneer u een bestandsshare te koppelen van on-premises of vanuit een ander datacenter, kan de volgende fouten worden weergegeven:</span><span class="sxs-lookup"><span data-stu-id="02be0-110">When you try to mount a file share from on-premises or from a different datacenter, you might receive the following errors:</span></span>

- <span data-ttu-id="02be0-111">Systeemfout 53 is opgetreden.</span><span class="sxs-lookup"><span data-stu-id="02be0-111">System error 53 has occurred.</span></span> <span data-ttu-id="02be0-112">Het netwerkpad is niet gevonden.</span><span class="sxs-lookup"><span data-stu-id="02be0-112">The network path was not found.</span></span>
- <span data-ttu-id="02be0-113">Systeemfout 67 is opgetreden.</span><span class="sxs-lookup"><span data-stu-id="02be0-113">System error 67 has occurred.</span></span> <span data-ttu-id="02be0-114">Naam van het netwerk kan niet worden gevonden.</span><span class="sxs-lookup"><span data-stu-id="02be0-114">The network name cannot be found.</span></span>
- <span data-ttu-id="02be0-115">Systeemfout 87 is opgetreden.</span><span class="sxs-lookup"><span data-stu-id="02be0-115">System error 87 has occurred.</span></span> <span data-ttu-id="02be0-116">De parameter is onjuist.</span><span class="sxs-lookup"><span data-stu-id="02be0-116">The parameter is incorrect.</span></span>

### <a name="cause-1-unencrypted-communication-channel"></a><span data-ttu-id="02be0-117">Oorzaak 1: De niet-versleutelde communicatiekanaal</span><span class="sxs-lookup"><span data-stu-id="02be0-117">Cause 1: Unencrypted communication channel</span></span>

<span data-ttu-id="02be0-118">Verbindingen met de Azure-bestandsshares worden uit veiligheidsoverwegingen geblokkeerd als het communicatiekanaal is niet versleuteld en als de verbinding is niet geprobeerd uit hetzelfde datacenter waarin de Azure-bestandsshares zich bevinden.</span><span class="sxs-lookup"><span data-stu-id="02be0-118">For security reasons, connections to Azure file shares are blocked if the communication channel isn’t encrypted and if the connection attempt isn't made from the same datacenter where the Azure file shares reside.</span></span> <span data-ttu-id="02be0-119">Alleen als de gebruiker clientbesturingssysteem SMB-versleuteling ondersteunt wordt de communicatie kanaalversleuteling geleverd.</span><span class="sxs-lookup"><span data-stu-id="02be0-119">Communication channel encryption is provided only if the user’s client OS supports SMB encryption.</span></span>

<span data-ttu-id="02be0-120">Windows 8, Windows Server 2012 en latere versies van elk systeem te onderhandelen over aanvragen met SMB 3.0, die ondersteuning biedt voor versleuteling.</span><span class="sxs-lookup"><span data-stu-id="02be0-120">Windows 8, Windows Server 2012, and later versions of each system negotiate requests that include SMB 3.0, which supports encryption.</span></span>

### <a name="solution-for-cause-1"></a><span data-ttu-id="02be0-121">Oplossing voor oorzaak 1</span><span class="sxs-lookup"><span data-stu-id="02be0-121">Solution for cause 1</span></span>

<span data-ttu-id="02be0-122">Verbinding maken vanaf een client die een van de volgende biedt:</span><span class="sxs-lookup"><span data-stu-id="02be0-122">Connect from a client that does one of the following:</span></span>

- <span data-ttu-id="02be0-123">Voldoet aan de vereisten van Windows 8 en Windows Server 2012 of hoger</span><span class="sxs-lookup"><span data-stu-id="02be0-123">Meets the requirements of Windows 8 and Windows Server 2012 or later versions</span></span>
- <span data-ttu-id="02be0-124">Verbinding maakt vanaf een virtuele machine in hetzelfde datacenter als de Azure storage-account dat wordt gebruikt voor de Azure-bestandsshare</span><span class="sxs-lookup"><span data-stu-id="02be0-124">Connects from a virtual machine in the same datacenter as the Azure storage account that is used for the Azure file share</span></span>

### <a name="cause-2-port-445-is-blocked"></a><span data-ttu-id="02be0-125">2 oorzaak: Poort 445 is geblokkeerd</span><span class="sxs-lookup"><span data-stu-id="02be0-125">Cause 2: Port 445 is blocked</span></span>

<span data-ttu-id="02be0-126">Systeemfout 53 of Systeemfout 67 kan zich voordoen als de poort 445 uitgaande communicatie naar een datacenter van Azure File storage is geblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="02be0-126">System error 53 or system error 67 can occur if port 445 outbound communication to an Azure File storage datacenter is blocked.</span></span> <span data-ttu-id="02be0-127">De samenvatting van internetproviders die toestaan of weigeren van toegang via poort 445, Ga naar [TechNet](http://social.technet.microsoft.com/wiki/contents/articles/32346.azure-summary-of-isps-that-allow-disallow-access-from-port-445.aspx).</span><span class="sxs-lookup"><span data-stu-id="02be0-127">To see the summary of ISPs that allow or disallow access from port 445, go to [TechNet](http://social.technet.microsoft.com/wiki/contents/articles/32346.azure-summary-of-isps-that-allow-disallow-access-from-port-445.aspx).</span></span>

<span data-ttu-id="02be0-128">Om te begrijpen of dit de reden achter het bericht 'Systeemfout 53' is, kunt u Portqry query uitvoeren op het eindpunt TCP:445.</span><span class="sxs-lookup"><span data-stu-id="02be0-128">To understand whether this is the reason behind the "System error 53" message, you can use Portqry to query the TCP:445 endpoint.</span></span> <span data-ttu-id="02be0-129">Als het eindpunt TCP:445 wordt weergegeven als gefilterd, is de TCP-poort geblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="02be0-129">If the TCP:445 endpoint is displayed as filtered, the TCP port is blocked.</span></span> <span data-ttu-id="02be0-130">Hier volgt een voorbeeldquery:</span><span class="sxs-lookup"><span data-stu-id="02be0-130">Here is an example query:</span></span>

  `g:\DataDump\Tools\Portqry>PortQry.exe -n [storage account name].file.core.windows.net -p TCP -e 445`

<span data-ttu-id="02be0-131">Als TCP-poort 445 wordt geblokkeerd door een regel op het netwerkpad, ziet u de volgende uitvoer:</span><span class="sxs-lookup"><span data-stu-id="02be0-131">If TCP port 445 is blocked by a rule along the network path, you will see the following output:</span></span>

  `TCP port 445 (microsoft-ds service): FILTERED`

<span data-ttu-id="02be0-132">Zie voor meer informatie over het gebruik van Portqry [beschrijving van het opdrachtregelprogramma Portqry.exe](https://support.microsoft.com/help/310099).</span><span class="sxs-lookup"><span data-stu-id="02be0-132">For more information about how to use Portqry, see [Description of the Portqry.exe command-line utility](https://support.microsoft.com/help/310099).</span></span>

### <a name="solution-for-cause-2"></a><span data-ttu-id="02be0-133">Oplossing voor oorzaak 2</span><span class="sxs-lookup"><span data-stu-id="02be0-133">Solution for cause 2</span></span>

<span data-ttu-id="02be0-134">Werken met uw IT-afdeling open poort 445 uitgaand naar [Azure IP-bereiken](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="02be0-134">Work with your IT department to open port 445 outbound to [Azure IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>

### <a name="cause-3-ntlmv1-is-enabled"></a><span data-ttu-id="02be0-135">3 oorzaak: NTLMv1 is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="02be0-135">Cause 3: NTLMv1 is enabled</span></span>

<span data-ttu-id="02be0-136">Systeemfout 53 of systeemfout 87 kan optreden als NTLMv1-communicatie is ingeschakeld op de client.</span><span class="sxs-lookup"><span data-stu-id="02be0-136">System error 53 or system error 87 can occur if NTLMv1 communication is enabled on the client.</span></span> <span data-ttu-id="02be0-137">Azure File storage ondersteunt alleen NTLMv2-authenticatie.</span><span class="sxs-lookup"><span data-stu-id="02be0-137">Azure File storage supports only NTLMv2 authentication.</span></span> <span data-ttu-id="02be0-138">NTLMv1 ingeschakeld met maakt een minder veilige client.</span><span class="sxs-lookup"><span data-stu-id="02be0-138">Having NTLMv1 enabled creates a less-secure client.</span></span> <span data-ttu-id="02be0-139">Daarom is communicatie geblokkeerd voor Azure File storage.</span><span class="sxs-lookup"><span data-stu-id="02be0-139">Therefore, communication is blocked for Azure File storage.</span></span> 

<span data-ttu-id="02be0-140">Om te bepalen of dit de oorzaak van de fout is, moet u controleren of de volgende registersubsleutel is ingesteld op een waarde van 3:</span><span class="sxs-lookup"><span data-stu-id="02be0-140">To determine whether this is the cause of the error, verify that the following registry subkey is set to a value of 3:</span></span>

<span data-ttu-id="02be0-141">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa > LmCompatibilityLevel**</span><span class="sxs-lookup"><span data-stu-id="02be0-141">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa > LmCompatibilityLevel**</span></span>

<span data-ttu-id="02be0-142">Zie voor meer informatie de [LmCompatibilityLevel](https://technet.microsoft.com/library/cc960646.aspx) onderwerp op TechNet.</span><span class="sxs-lookup"><span data-stu-id="02be0-142">For more information, see the [LmCompatibilityLevel](https://technet.microsoft.com/library/cc960646.aspx) topic on TechNet.</span></span>

### <a name="solution-for-cause-3"></a><span data-ttu-id="02be0-143">Oplossing voor oorzaak 3</span><span class="sxs-lookup"><span data-stu-id="02be0-143">Solution for cause 3</span></span>

<span data-ttu-id="02be0-144">Herstellen de **LmCompatibilityLevel** waarde op de standaardwaarde van 3 in de volgende registersubsleutel:</span><span class="sxs-lookup"><span data-stu-id="02be0-144">Revert the **LmCompatibilityLevel** value to the default value of 3 in the following registry subkey:</span></span>

  <span data-ttu-id="02be0-145">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa**</span><span class="sxs-lookup"><span data-stu-id="02be0-145">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa**</span></span>

<a id="error1816"></a>
## <a name="error-1816-not-enough-quota-is-available-to-process-this-command-when-you-copy-to-an-azure-file-share"></a><span data-ttu-id="02be0-146">Fout 1816 'Onvoldoende quota is beschikbaar om deze opdracht te verwerken' als u kopieert naar een Azure-bestandsshare</span><span class="sxs-lookup"><span data-stu-id="02be0-146">Error 1816 “Not enough quota is available to process this command” when you copy to an Azure file share</span></span>

### <a name="cause"></a><span data-ttu-id="02be0-147">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="02be0-147">Cause</span></span>

<span data-ttu-id="02be0-148">Fout 1816 treedt op wanneer het bereiken van de bovengrens van gelijktijdige open ingangen die zijn toegestaan voor een bestand op de computer waar de bestandsshare is wordt gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="02be0-148">Error 1816 happens when you reach the upper limit of concurrent open handles that are allowed for a file on the computer where the file share is being mounted.</span></span>

### <a name="solution"></a><span data-ttu-id="02be0-149">Oplossing</span><span class="sxs-lookup"><span data-stu-id="02be0-149">Solution</span></span>

<span data-ttu-id="02be0-150">Verminder het aantal gelijktijdige open ingangen door te sluiten van een aantal ingangen en probeer het vervolgens opnieuw.</span><span class="sxs-lookup"><span data-stu-id="02be0-150">Reduce the number of concurrent open handles by closing some handles, and then retry.</span></span> <span data-ttu-id="02be0-151">Zie voor meer informatie [controlelijst voor prestaties en schaalbaarheid van Microsoft Azure Storage](../common/storage-performance-checklist.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="02be0-151">For more information, see [Microsoft Azure Storage performance and scalability checklist](../common/storage-performance-checklist.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span></span>

<a id="slowfilecopying"></a>
## <a name="slow-file-copying-to-and-from-azure-file-storage-in-windows"></a><span data-ttu-id="02be0-152">Trage bestand kopiëren van en naar Azure File storage in Windows</span><span class="sxs-lookup"><span data-stu-id="02be0-152">Slow file copying to and from Azure File storage in Windows</span></span>

<span data-ttu-id="02be0-153">U ziet trage prestaties wanneer u bestanden overbrengen naar de Azure File-service.</span><span class="sxs-lookup"><span data-stu-id="02be0-153">You might see slow performance when you try to transfer files to the Azure File service.</span></span>

- <span data-ttu-id="02be0-154">Als u een specifieke i/o-grootte minimumvereiste hebt, raden wij aan 1 MB te gebruiken als de i/o-grootte voor optimale prestaties.</span><span class="sxs-lookup"><span data-stu-id="02be0-154">If you don’t have a specific minimum I/O size requirement, we recommend that you use 1 MB as the I/O size for optimal performance.</span></span>
-   <span data-ttu-id="02be0-155">Als u weet dat de uiteindelijke omvang van een bestand dat u met schrijfbewerkingen uitbreidt en de software geen compatibiliteitsproblemen wanneer de unwritten staart op het bestand nullen bevat, stelt u de bestandsgrootte van tevoren in plaats van elke schrijfbewerking waardoor het terugschrijven van een uitbreiden.</span><span class="sxs-lookup"><span data-stu-id="02be0-155">If you know the final size of a file that you are extending with writes, and your software doesn’t have compatibility problems when the unwritten tail on the file contains zeros, then set the file size in advance instead of making every write an extending write.</span></span>
-   <span data-ttu-id="02be0-156">Gebruik de juiste copy-methode:</span><span class="sxs-lookup"><span data-stu-id="02be0-156">Use the right copy method:</span></span>
    -   <span data-ttu-id="02be0-157">Gebruik [AzCopy](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#file-copy) de overdracht tussen twee bestandsshares.</span><span class="sxs-lookup"><span data-stu-id="02be0-157">Use [AzCopy](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#file-copy) for any transfer between two file shares.</span></span>
    -   <span data-ttu-id="02be0-158">Gebruik [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) tussen bestandsshares op een on-premises computer.</span><span class="sxs-lookup"><span data-stu-id="02be0-158">Use [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) between file shares on an on-premises computer.</span></span>

### <a name="considerations-for-windows-81-or-windows-server-2012-r2"></a><span data-ttu-id="02be0-159">Overwegingen voor Windows 8.1 of Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="02be0-159">Considerations for Windows 8.1 or Windows Server 2012 R2</span></span>

<span data-ttu-id="02be0-160">Voor clients met Windows 8.1 of Windows Server 2012 R2, zorg ervoor dat de [KB3114025](https://support.microsoft.com/help/3114025) hotfix is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="02be0-160">For clients that are running Windows 8.1 or Windows Server 2012 R2, make sure that the [KB3114025](https://support.microsoft.com/help/3114025) hotfix is installed.</span></span> <span data-ttu-id="02be0-161">Deze hotfix verbetert de prestaties van maken en sluit verwerkt.</span><span class="sxs-lookup"><span data-stu-id="02be0-161">This hotfix improves the performance of create and close handles.</span></span>

<span data-ttu-id="02be0-162">U kunt uitvoeren in het volgende script om te controleren of de hotfix is geïnstalleerd:</span><span class="sxs-lookup"><span data-stu-id="02be0-162">You can run the following script to check whether the hotfix has been installed:</span></span>

`reg query HKLM\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters\Policies`

<span data-ttu-id="02be0-163">Als de hotfix is geïnstalleerd, wordt de volgende uitvoer weergegeven:</span><span class="sxs-lookup"><span data-stu-id="02be0-163">If hotfix is installed, the following output is displayed:</span></span>

`HKEY_Local_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters\Policies {96c345ef-3cac-477b-8fcd-bea1a564241c} REG_DWORD 0x1`

> [!Note]
> <span data-ttu-id="02be0-164">Windows Server 2012 R2-afbeeldingen in Azure Marketplace hebben hotfix KB3114025 standaard geïnstalleerd, vanaf December 2015.</span><span class="sxs-lookup"><span data-stu-id="02be0-164">Windows Server 2012 R2 images in Azure Marketplace have hotfix KB3114025 installed by default, starting in December 2015.</span></span>

<a id="shareismissing"></a>
## <a name="no-folder-with-a-drive-letter-in-my-computer"></a><span data-ttu-id="02be0-165">Er is geen map met een stationsletter in **Mijn Computer**</span><span class="sxs-lookup"><span data-stu-id="02be0-165">No folder with a drive letter in **My Computer**</span></span>

<span data-ttu-id="02be0-166">Als u een Azure-bestandsshare als een beheerder met behulp van net gebruik toewijst, wordt de share lijkt te ontbreken.</span><span class="sxs-lookup"><span data-stu-id="02be0-166">If you map an Azure file share as an administrator by using net use, the share appears to be missing.</span></span>

### <a name="cause"></a><span data-ttu-id="02be0-167">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="02be0-167">Cause</span></span>

<span data-ttu-id="02be0-168">Windows Verkenner wordt niet uitgevoerd als beheerder.</span><span class="sxs-lookup"><span data-stu-id="02be0-168">By default, Windows File Explorer does not run as an administrator.</span></span> <span data-ttu-id="02be0-169">Als u net gebruik van een administratieve opdrachtprompt uitvoert, kunt u het netwerkstation toewijzen als beheerder.</span><span class="sxs-lookup"><span data-stu-id="02be0-169">If you run net use from an administrative command prompt, you map the network drive as an administrator.</span></span> <span data-ttu-id="02be0-170">Omdat netwerkstations gebruikersgerichte zijn, wordt het gebruikersaccount dat is vastgelegd in de stations niet weergegeven als ze worden gekoppeld onder een ander gebruikersaccount.</span><span class="sxs-lookup"><span data-stu-id="02be0-170">Because mapped drives are user-centric, the user account that is logged in does not display the drives if they are mounted under a different user account.</span></span>

### <a name="solution"></a><span data-ttu-id="02be0-171">Oplossing</span><span class="sxs-lookup"><span data-stu-id="02be0-171">Solution</span></span>
<span data-ttu-id="02be0-172">De bestandsshare koppelen vanuit een opdrachtregel niet-beheerders.</span><span class="sxs-lookup"><span data-stu-id="02be0-172">Mount the share from a non-administrator command line.</span></span> <span data-ttu-id="02be0-173">U kunt ook kunt u [dit TechNet-onderwerp](https://technet.microsoft.com/library/ee844140.aspx) voor het configureren van de **EnableLinkedConnections** registerwaarde.</span><span class="sxs-lookup"><span data-stu-id="02be0-173">Alternatively, you can follow [this TechNet topic](https://technet.microsoft.com/library/ee844140.aspx) to configure the **EnableLinkedConnections** registry value.</span></span>

<a id="netuse"></a>
## <a name="net-use-command-fails-if-the-storage-account-contains-a-forward-slash"></a><span data-ttu-id="02be0-174">Opdracht net use mislukt als het opslagaccount een slash bevat</span><span class="sxs-lookup"><span data-stu-id="02be0-174">Net use command fails if the storage account contains a forward slash</span></span>

### <a name="cause"></a><span data-ttu-id="02be0-175">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="02be0-175">Cause</span></span>

<span data-ttu-id="02be0-176">Een slash (/) de opdracht net use geïnterpreteerd als een opdrachtregeloptie.</span><span class="sxs-lookup"><span data-stu-id="02be0-176">The net use command interprets a forward slash (/) as a command-line option.</span></span> <span data-ttu-id="02be0-177">Als de naam van uw gebruikersaccount wordt gestart met een slash, wordt de stationstoewijzing mislukt.</span><span class="sxs-lookup"><span data-stu-id="02be0-177">If your user account name starts with a forward slash, the drive mapping fails.</span></span>

### <a name="solution"></a><span data-ttu-id="02be0-178">Oplossing</span><span class="sxs-lookup"><span data-stu-id="02be0-178">Solution</span></span>

<span data-ttu-id="02be0-179">U kunt een van de volgende stappen gebruiken om het probleem te omzeilen:</span><span class="sxs-lookup"><span data-stu-id="02be0-179">You can use either of the following steps to work around the problem:</span></span>

- <span data-ttu-id="02be0-180">Voer de volgende PowerShell-opdracht:</span><span class="sxs-lookup"><span data-stu-id="02be0-180">Run the following PowerShell command:</span></span>

  `New-SmbMapping -LocalPath y: -RemotePath \\server\share -UserName accountName -Password "password can contain / and \ etc" `

  <span data-ttu-id="02be0-181">Vanuit een batch-bestand, kunt u de opdracht uitvoeren op deze manier:</span><span class="sxs-lookup"><span data-stu-id="02be0-181">From a batch file, you can run the command this way:</span></span>

  `Echo new-smbMapping ... | powershell -command –`

- <span data-ttu-id="02be0-182">Dubbele aanhalingstekens rond de sleutel voor dit probleem--omzeilen geplaatst tenzij de slash is het eerste onjuiste teken.</span><span class="sxs-lookup"><span data-stu-id="02be0-182">Put double quotation marks around the key to work around this problem--unless the forward slash is the first character.</span></span> <span data-ttu-id="02be0-183">Als het, de interactieve modus gebruiken en voer uw wachtwoord afzonderlijk of opnieuw genereren van uw sleutels als u een sleutel die niet met een slash begint.</span><span class="sxs-lookup"><span data-stu-id="02be0-183">If it is, either use the interactive mode and enter your password separately or regenerate your keys to get a key that doesn't start with a forward slash.</span></span>

<a id="cannotaccess"></a>
## <a name="application-or-service-cannot-access-a-mounted-azure-file-storage-drive"></a><span data-ttu-id="02be0-184">Toepassing of service heeft geen toegang tot een gekoppelde Azure File storage-station</span><span class="sxs-lookup"><span data-stu-id="02be0-184">Application or service cannot access a mounted Azure File storage drive</span></span>

### <a name="cause"></a><span data-ttu-id="02be0-185">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="02be0-185">Cause</span></span>

<span data-ttu-id="02be0-186">Schijven zijn per gebruiker gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="02be0-186">Drives are mounted per user.</span></span> <span data-ttu-id="02be0-187">Als uw toepassing of service wordt uitgevoerd onder een ander gebruikersaccount dan het station gekoppeld, wordt het station niet weergegeven in de toepassing.</span><span class="sxs-lookup"><span data-stu-id="02be0-187">If your application or service is running under a different user account than the one that mounted the drive, the application will not see the drive.</span></span>

### <a name="solution"></a><span data-ttu-id="02be0-188">Oplossing</span><span class="sxs-lookup"><span data-stu-id="02be0-188">Solution</span></span>

<span data-ttu-id="02be0-189">Gebruik een van de volgende oplossingen:</span><span class="sxs-lookup"><span data-stu-id="02be0-189">Use one of the following solutions:</span></span>

-   <span data-ttu-id="02be0-190">Het station koppelen vanuit dezelfde gebruikersaccount dat de toepassing bevat.</span><span class="sxs-lookup"><span data-stu-id="02be0-190">Mount the drive from the same user account that contains the application.</span></span> <span data-ttu-id="02be0-191">U kunt een hulpprogramma zoals PsExec gebruiken.</span><span class="sxs-lookup"><span data-stu-id="02be0-191">You can use a tool such as PsExec.</span></span>
- <span data-ttu-id="02be0-192">Geeft de naam van het opslagaccount en de sleutel in de gebruikersnaam en wachtwoordparameters van het net gebruik de opdracht.</span><span class="sxs-lookup"><span data-stu-id="02be0-192">Pass the storage account name and key in the user name and password parameters of the net use command.</span></span>

<span data-ttu-id="02be0-193">Nadat u deze instructies opvolgt, verschijnt er het volgende foutbericht weergegeven wanneer u net gebruiken voor het serviceaccount/in het netwerk uitvoert: 'Systeemfout 1312 is opgetreden.</span><span class="sxs-lookup"><span data-stu-id="02be0-193">After you follow these instructions, you might receive the following error message when you run net use for the system/network service account: "System error 1312 has occurred.</span></span> <span data-ttu-id="02be0-194">De sessie van een opgegeven gebruiker bestaat niet.</span><span class="sxs-lookup"><span data-stu-id="02be0-194">A specified logon session does not exist.</span></span> <span data-ttu-id="02be0-195">Het is mogelijk al beëindigd."</span><span class="sxs-lookup"><span data-stu-id="02be0-195">It may already have been terminated."</span></span> <span data-ttu-id="02be0-196">Als dit het geval is, zorg ervoor dat de gebruikersnaam die wordt doorgegeven aan net gebruik domeingegevens bevat (bijvoorbeeld: ' [opslagaccountnaam]. file.core.windows .net ').</span><span class="sxs-lookup"><span data-stu-id="02be0-196">If this occurs, make sure that the username that is passed to net use includes domain information (for example: "[storage account name].file.core.windows.net").</span></span>

<a id="doesnotsupportencryption"></a>
## <a name="error-you-are-copying-a-file-to-a-destination-that-does-not-support-encryption"></a><span data-ttu-id="02be0-197">'U kopieert een bestand op een doel geen versleuteling ondersteunt' fout</span><span class="sxs-lookup"><span data-stu-id="02be0-197">Error "You are copying a file to a destination that does not support encryption"</span></span>

<span data-ttu-id="02be0-198">Als een bestand wordt gekopieerd via het netwerk, wordt het bestand op de broncomputer is ontsleuteld, verzonden als leesbare tekst en opnieuw versleuteld op de bestemming.</span><span class="sxs-lookup"><span data-stu-id="02be0-198">When a file is copied over the network, the file is decrypted on the source computer, transmitted in plaintext, and re-encrypted at the destination.</span></span> <span data-ttu-id="02be0-199">Echter kunt u de volgende fout tegenkomen wanneer u probeert een versleuteld bestand kopiëren: "Kopieert u het bestand naar een bestemming die geen ondersteuning biedt voor versleuteling."</span><span class="sxs-lookup"><span data-stu-id="02be0-199">However, you might see the following error when you're trying to copy an encrypted file: "You are copying the file to a destination that does not support encryption."</span></span>

### <a name="cause"></a><span data-ttu-id="02be0-200">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="02be0-200">Cause</span></span>
<span data-ttu-id="02be0-201">Dit probleem kan optreden als u van Encrypting File System (EFS gebruikmaakt).</span><span class="sxs-lookup"><span data-stu-id="02be0-201">This problem can occur if you are using Encrypting File System (EFS).</span></span> <span data-ttu-id="02be0-202">BitLocker-versleutelde bestanden kunnen worden gekopieerd naar Azure File storage.</span><span class="sxs-lookup"><span data-stu-id="02be0-202">BitLocker-encrypted files can be copied to Azure File storage.</span></span> <span data-ttu-id="02be0-203">Azure File storage biedt echter geen ondersteuning voor NTFS EFS.</span><span class="sxs-lookup"><span data-stu-id="02be0-203">However, Azure File storage does not support NTFS EFS.</span></span>

### <a name="workaround"></a><span data-ttu-id="02be0-204">Tijdelijke oplossing</span><span class="sxs-lookup"><span data-stu-id="02be0-204">Workaround</span></span>
<span data-ttu-id="02be0-205">Als u wilt een bestand via het netwerk kopieert, moet u het eerst ontsleutelen.</span><span class="sxs-lookup"><span data-stu-id="02be0-205">To copy a file over the network, you must first decrypt it.</span></span> <span data-ttu-id="02be0-206">Gebruik een van de volgende methoden:</span><span class="sxs-lookup"><span data-stu-id="02be0-206">Use one of the following methods:</span></span>

- <span data-ttu-id="02be0-207">Gebruik de **kopiëren /d** opdracht.</span><span class="sxs-lookup"><span data-stu-id="02be0-207">Use the **copy /d** command.</span></span> <span data-ttu-id="02be0-208">Hierdoor kan de versleutelde bestanden worden opgeslagen als de ontsleutelde bestanden op de bestemming.</span><span class="sxs-lookup"><span data-stu-id="02be0-208">It allows the encrypted files to be saved as decrypted files at the destination.</span></span>
- <span data-ttu-id="02be0-209">Stel de volgende registersleutel:</span><span class="sxs-lookup"><span data-stu-id="02be0-209">Set the following registry key:</span></span>
  - <span data-ttu-id="02be0-210">Pad = HKLM\Software\Policies\Microsoft\Windows\System</span><span class="sxs-lookup"><span data-stu-id="02be0-210">Path = HKLM\Software\Policies\Microsoft\Windows\System</span></span>
  - <span data-ttu-id="02be0-211">Waarde type DWORD =</span><span class="sxs-lookup"><span data-stu-id="02be0-211">Value type = DWORD</span></span>
  - <span data-ttu-id="02be0-212">Naam CopyFileAllowDecryptedRemoteDestination =</span><span class="sxs-lookup"><span data-stu-id="02be0-212">Name = CopyFileAllowDecryptedRemoteDestination</span></span>
  - <span data-ttu-id="02be0-213">Waarde = 1</span><span class="sxs-lookup"><span data-stu-id="02be0-213">Value = 1</span></span>

<span data-ttu-id="02be0-214">Let erop dat voor het instellen van de registersleutel is van invloed op alle kopieerbewerkingen die zijn aangebracht aan netwerkshares.</span><span class="sxs-lookup"><span data-stu-id="02be0-214">Be aware that setting the registry key affects all copy operations that are made to network shares.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="02be0-215">Hulp nodig?</span><span class="sxs-lookup"><span data-stu-id="02be0-215">Need help?</span></span> <span data-ttu-id="02be0-216">Neem contact op met ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="02be0-216">Contact support.</span></span>
<span data-ttu-id="02be0-217">Als u nog hulp nodig hebt, [contact op met ondersteuning](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) ophalen van uw probleem snel worden opgelost.</span><span class="sxs-lookup"><span data-stu-id="02be0-217">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your problem resolved quickly.</span></span>
