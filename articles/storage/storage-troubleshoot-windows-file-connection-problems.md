---
title: problemen met aaaTroubleshoot Azure File storage in Windows | Microsoft Docs
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
ms.openlocfilehash: ba0315d1add76a27fec93a9aee3aa99ccb7fa164
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-file-storage-problems-in-windows"></a><span data-ttu-id="f7ce6-103">Problemen met Azure File storage in Windows</span><span class="sxs-lookup"><span data-stu-id="f7ce6-103">Troubleshoot Azure File storage problems in Windows</span></span>

<span data-ttu-id="f7ce6-104">Dit artikel worden veelvoorkomende problemen die gerelateerde tooMicrosoft Azure File storage zijn wanneer u verbinding vanaf een Windows-clients maakt.</span><span class="sxs-lookup"><span data-stu-id="f7ce6-104">This article lists common problems that are related tooMicrosoft Azure File storage when you connect from Windows clients.</span></span> <span data-ttu-id="f7ce6-105">Het bevat ook mogelijke oorzaken en oplossingen voor deze problemen.</span><span class="sxs-lookup"><span data-stu-id="f7ce6-105">It also provides possible causes and resolutions for these problems.</span></span> <span data-ttu-id="f7ce6-106">Bovendien toohello probleemoplossing stappen in dit artikel, kunt u ook [AzFileDiagnostics](https://gallery.technet.microsoft.com/Troubleshooting-tool-for-a9fa1fe5) om ervoor te zorgen dat Hallo Windows clientomgeving juist vereisten heeft.</span><span class="sxs-lookup"><span data-stu-id="f7ce6-106">In addition toohello troubleshooting steps in this article, you can also use [AzFileDiagnostics](https://gallery.technet.microsoft.com/Troubleshooting-tool-for-a9fa1fe5) to ensure that hello Windows client environment has correct prerequisites.</span></span> <span data-ttu-id="f7ce6-107">AzFileDiagnostics automatiseert detectie van de meeste Hallo symptomen die in dit artikel worden vermeld en helpt bij het instellen van uw omgeving tooget optimale prestaties.</span><span class="sxs-lookup"><span data-stu-id="f7ce6-107">AzFileDiagnostics automates detection of most of hello symptoms mentioned in this article and helps set up your environment tooget optimal performance.</span></span> <span data-ttu-id="f7ce6-108">U kunt deze informatie ook vinden in Hallo [Azure-bestandsshares probleemoplosser](https://support.microsoft.com/help/4022301/troubleshooter-for-azure-files-shares) stappen tooassist en waarmee u problemen verbinden/toewijzing/koppelen Azure bestandsshares.</span><span class="sxs-lookup"><span data-stu-id="f7ce6-108">You can also find this information in hello [Azure Files shares Troubleshooter](https://support.microsoft.com/help/4022301/troubleshooter-for-azure-files-shares) that provides steps tooassist you with problems connecting/mapping/mounting Azure Files shares.</span></span>


<a id="error53-67-87"></a>
## <a name="error-53-error-67-or-error-87-when-you-mount-or-unmount-an-azure-file-share"></a><span data-ttu-id="f7ce6-109">Fout 53, fout 67 of fout 87 wanneer u koppelen of ontkoppelen van een Azure-bestandsshare</span><span class="sxs-lookup"><span data-stu-id="f7ce6-109">Error 53, Error 67, or Error 87 when you mount or unmount an Azure file share</span></span>

<span data-ttu-id="f7ce6-110">Wanneer u een bestandsshare van on-premises of vanuit een ander datacenter toomount, verschijnt er Hallo volgende fouten:</span><span class="sxs-lookup"><span data-stu-id="f7ce6-110">When you try toomount a file share from on-premises or from a different datacenter, you might receive hello following errors:</span></span>

- <span data-ttu-id="f7ce6-111">Systeemfout 53 is opgetreden.</span><span class="sxs-lookup"><span data-stu-id="f7ce6-111">System error 53 has occurred.</span></span> <span data-ttu-id="f7ce6-112">Hallo netwerkpad is niet gevonden.</span><span class="sxs-lookup"><span data-stu-id="f7ce6-112">hello network path was not found.</span></span>
- <span data-ttu-id="f7ce6-113">Systeemfout 67 is opgetreden.</span><span class="sxs-lookup"><span data-stu-id="f7ce6-113">System error 67 has occurred.</span></span> <span data-ttu-id="f7ce6-114">Hallo-netwerknaam kan niet worden gevonden.</span><span class="sxs-lookup"><span data-stu-id="f7ce6-114">hello network name cannot be found.</span></span>
- <span data-ttu-id="f7ce6-115">Systeemfout 87 is opgetreden.</span><span class="sxs-lookup"><span data-stu-id="f7ce6-115">System error 87 has occurred.</span></span> <span data-ttu-id="f7ce6-116">Hallo-parameter is onjuist.</span><span class="sxs-lookup"><span data-stu-id="f7ce6-116">hello parameter is incorrect.</span></span>

### <a name="cause-1-unencrypted-communication-channel"></a><span data-ttu-id="f7ce6-117">Oorzaak 1: De niet-versleutelde communicatiekanaal</span><span class="sxs-lookup"><span data-stu-id="f7ce6-117">Cause 1: Unencrypted communication channel</span></span>

<span data-ttu-id="f7ce6-118">Uit veiligheidsoverwegingen Hallo verbindingen tooAzure bestandsshares worden geblokkeerd als Hallo communicatiekanaal is niet versleuteld en Hallo verbinding wordt niet geprobeerd uit hetzelfde datacenter waar hello Azure-bestandsshares zich bevinden.</span><span class="sxs-lookup"><span data-stu-id="f7ce6-118">For security reasons, connections tooAzure file shares are blocked if hello communication channel isn’t encrypted and if hello connection attempt isn't made from hello same datacenter where hello Azure file shares reside.</span></span> <span data-ttu-id="f7ce6-119">Alleen als van de gebruiker Hallo clientbesturingssysteem SMB-versleuteling ondersteunt wordt de communicatie kanaalversleuteling geleverd.</span><span class="sxs-lookup"><span data-stu-id="f7ce6-119">Communication channel encryption is provided only if hello user’s client OS supports SMB encryption.</span></span>

<span data-ttu-id="f7ce6-120">Windows 8, Windows Server 2012 en latere versies van elk systeem te onderhandelen over aanvragen met SMB 3.0, die ondersteuning biedt voor versleuteling.</span><span class="sxs-lookup"><span data-stu-id="f7ce6-120">Windows 8, Windows Server 2012, and later versions of each system negotiate requests that include SMB 3.0, which supports encryption.</span></span>

### <a name="solution-for-cause-1"></a><span data-ttu-id="f7ce6-121">Oplossing voor oorzaak 1</span><span class="sxs-lookup"><span data-stu-id="f7ce6-121">Solution for cause 1</span></span>

<span data-ttu-id="f7ce6-122">Verbinding maken vanaf een client die een van de volgende Hallo biedt:</span><span class="sxs-lookup"><span data-stu-id="f7ce6-122">Connect from a client that does one of hello following:</span></span>

- <span data-ttu-id="f7ce6-123">Hallo voldoet aan de vereisten van Windows 8 en Windows Server 2012 of hoger</span><span class="sxs-lookup"><span data-stu-id="f7ce6-123">Meets hello requirements of Windows 8 and Windows Server 2012 or later versions</span></span>
- <span data-ttu-id="f7ce6-124">Verbinding van een virtuele machine in Hallo dezelfde datacenter zoals Azure storage-account dat wordt gebruikt voor het Azure-bestandsshare Hallo Hallo</span><span class="sxs-lookup"><span data-stu-id="f7ce6-124">Connects from a virtual machine in hello same datacenter as hello Azure storage account that is used for hello Azure file share</span></span>

### <a name="cause-2-port-445-is-blocked"></a><span data-ttu-id="f7ce6-125">2 oorzaak: Poort 445 is geblokkeerd</span><span class="sxs-lookup"><span data-stu-id="f7ce6-125">Cause 2: Port 445 is blocked</span></span>

<span data-ttu-id="f7ce6-126">Systeemfout 53 of Systeemfout 67 kan zich voordoen als de poort 445 uitgaande communicatie tooan Azure File storage datacenter wordt geblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="f7ce6-126">System error 53 or system error 67 can occur if port 445 outbound communication tooan Azure File storage datacenter is blocked.</span></span> <span data-ttu-id="f7ce6-127">toosee hello samenvatting van internetproviders die toestaan of weigeren van toegang via poort 445, gaat u te[TechNet](http://social.technet.microsoft.com/wiki/contents/articles/32346.azure-summary-of-isps-that-allow-disallow-access-from-port-445.aspx).</span><span class="sxs-lookup"><span data-stu-id="f7ce6-127">toosee hello summary of ISPs that allow or disallow access from port 445, go too[TechNet](http://social.technet.microsoft.com/wiki/contents/articles/32346.azure-summary-of-isps-that-allow-disallow-access-from-port-445.aspx).</span></span>

<span data-ttu-id="f7ce6-128">toounderstand of dit de reden Hallo achter 'Systeemfout 53' het Hallo-bericht is, kunt u Portqry tooquery hello TCP:445 eindpunt.</span><span class="sxs-lookup"><span data-stu-id="f7ce6-128">toounderstand whether this is hello reason behind hello "System error 53" message, you can use Portqry tooquery hello TCP:445 endpoint.</span></span> <span data-ttu-id="f7ce6-129">Als Hallo TCP:445 eindpunt wordt weergegeven als gefilterd, is Hallo TCP-poort geblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="f7ce6-129">If hello TCP:445 endpoint is displayed as filtered, hello TCP port is blocked.</span></span> <span data-ttu-id="f7ce6-130">Hier volgt een voorbeeldquery:</span><span class="sxs-lookup"><span data-stu-id="f7ce6-130">Here is an example query:</span></span>

  `g:\DataDump\Tools\Portqry>PortQry.exe -n [storage account name].file.core.windows.net -p TCP -e 445`

<span data-ttu-id="f7ce6-131">Als TCP-poort 445 wordt geblokkeerd door een regel langs Hallo netwerkpad, ziet u Hallo volgende uitvoer:</span><span class="sxs-lookup"><span data-stu-id="f7ce6-131">If TCP port 445 is blocked by a rule along hello network path, you will see hello following output:</span></span>

  `TCP port 445 (microsoft-ds service): FILTERED`

<span data-ttu-id="f7ce6-132">Voor meer informatie over het toouse Portqry, Zie [beschrijving van Hallo Portqry.exe opdrachtregelprogramma](https://support.microsoft.com/help/310099).</span><span class="sxs-lookup"><span data-stu-id="f7ce6-132">For more information about how toouse Portqry, see [Description of hello Portqry.exe command-line utility](https://support.microsoft.com/help/310099).</span></span>

### <a name="solution-for-cause-2"></a><span data-ttu-id="f7ce6-133">Oplossing voor oorzaak 2</span><span class="sxs-lookup"><span data-stu-id="f7ce6-133">Solution for cause 2</span></span>

<span data-ttu-id="f7ce6-134">Werken met uw IT-afdeling tooopen poort 445 uitgaand te[Azure IP-bereiken](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="f7ce6-134">Work with your IT department tooopen port 445 outbound too[Azure IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>

### <a name="cause-3-ntlmv1-is-enabled"></a><span data-ttu-id="f7ce6-135">3 oorzaak: NTLMv1 is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="f7ce6-135">Cause 3: NTLMv1 is enabled</span></span>

<span data-ttu-id="f7ce6-136">Systeemfout 53 of systeemfout 87 kan optreden als NTLMv1-communicatie is ingeschakeld op Hallo-client.</span><span class="sxs-lookup"><span data-stu-id="f7ce6-136">System error 53 or system error 87 can occur if NTLMv1 communication is enabled on hello client.</span></span> <span data-ttu-id="f7ce6-137">Azure File storage ondersteunt alleen NTLMv2-authenticatie.</span><span class="sxs-lookup"><span data-stu-id="f7ce6-137">Azure File storage supports only NTLMv2 authentication.</span></span> <span data-ttu-id="f7ce6-138">NTLMv1 ingeschakeld met maakt een minder veilige client.</span><span class="sxs-lookup"><span data-stu-id="f7ce6-138">Having NTLMv1 enabled creates a less-secure client.</span></span> <span data-ttu-id="f7ce6-139">Daarom is communicatie geblokkeerd voor Azure File storage.</span><span class="sxs-lookup"><span data-stu-id="f7ce6-139">Therefore, communication is blocked for Azure File storage.</span></span> 

<span data-ttu-id="f7ce6-140">toodetermine of dit Hallo oorzaak van Hallo fout, Controleer of dat Hallo volgende subsleutel in het register is ingesteld tooa waarde van 3:</span><span class="sxs-lookup"><span data-stu-id="f7ce6-140">toodetermine whether this is hello cause of hello error, verify that hello following registry subkey is set tooa value of 3:</span></span>

<span data-ttu-id="f7ce6-141">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa > LmCompatibilityLevel**</span><span class="sxs-lookup"><span data-stu-id="f7ce6-141">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa > LmCompatibilityLevel**</span></span>

<span data-ttu-id="f7ce6-142">Zie voor meer informatie, Hallo [LmCompatibilityLevel](https://technet.microsoft.com/library/cc960646.aspx) onderwerp op TechNet.</span><span class="sxs-lookup"><span data-stu-id="f7ce6-142">For more information, see hello [LmCompatibilityLevel](https://technet.microsoft.com/library/cc960646.aspx) topic on TechNet.</span></span>

### <a name="solution-for-cause-3"></a><span data-ttu-id="f7ce6-143">Oplossing voor oorzaak 3</span><span class="sxs-lookup"><span data-stu-id="f7ce6-143">Solution for cause 3</span></span>

<span data-ttu-id="f7ce6-144">Hallo terugkeren **LmCompatibilityLevel** toohello standaardwaarde 3 in de volgende registersubsleutel Hallo waarde:</span><span class="sxs-lookup"><span data-stu-id="f7ce6-144">Revert hello **LmCompatibilityLevel** value toohello default value of 3 in hello following registry subkey:</span></span>

  <span data-ttu-id="f7ce6-145">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa**</span><span class="sxs-lookup"><span data-stu-id="f7ce6-145">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa**</span></span>

<a id="error1816"></a>
## <a name="error-1816-not-enough-quota-is-available-tooprocess-this-command-when-you-copy-tooan-azure-file-share"></a><span data-ttu-id="f7ce6-146">Fout 1816 ' Onvoldoende quota beschikbaar tooprocess met deze opdracht is ' wanneer u Azure-bestandsshare tooan kopiëren</span><span class="sxs-lookup"><span data-stu-id="f7ce6-146">Error 1816 “Not enough quota is available tooprocess this command” when you copy tooan Azure file share</span></span>

### <a name="cause"></a><span data-ttu-id="f7ce6-147">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="f7ce6-147">Cause</span></span>

<span data-ttu-id="f7ce6-148">Fout 1816 treedt op wanneer u bereiken Hallo bovenlimiet van gelijktijdige open ingangen die zijn toegestaan voor een bestand op Hallo computer waar Hallo-bestandsshare is wordt gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="f7ce6-148">Error 1816 happens when you reach hello upper limit of concurrent open handles that are allowed for a file on hello computer where hello file share is being mounted.</span></span>

### <a name="solution"></a><span data-ttu-id="f7ce6-149">Oplossing</span><span class="sxs-lookup"><span data-stu-id="f7ce6-149">Solution</span></span>

<span data-ttu-id="f7ce6-150">Aantal gelijktijdige open ingangen Hallo verminderen door te sluiten van een aantal ingangen en probeer het vervolgens opnieuw.</span><span class="sxs-lookup"><span data-stu-id="f7ce6-150">Reduce hello number of concurrent open handles by closing some handles, and then retry.</span></span> <span data-ttu-id="f7ce6-151">Zie voor meer informatie [controlelijst voor prestaties en schaalbaarheid van Microsoft Azure Storage](storage-performance-checklist.md).</span><span class="sxs-lookup"><span data-stu-id="f7ce6-151">For more information, see [Microsoft Azure Storage performance and scalability checklist](storage-performance-checklist.md).</span></span>

<a id="slowfilecopying"></a>
## <a name="slow-file-copying-tooand-from-azure-file-storage-in-windows"></a><span data-ttu-id="f7ce6-152">Trage bestand tooand kopiëren van Azure File storage in Windows</span><span class="sxs-lookup"><span data-stu-id="f7ce6-152">Slow file copying tooand from Azure File storage in Windows</span></span>

<span data-ttu-id="f7ce6-153">U kunt trage prestaties tegenkomen wanneer u tootransfer bestanden toohello Azure File-service probeert.</span><span class="sxs-lookup"><span data-stu-id="f7ce6-153">You might see slow performance when you try tootransfer files toohello Azure File service.</span></span>

- <span data-ttu-id="f7ce6-154">Als u een specifieke i/o-grootte minimumvereiste hebt, raden wij 1 MB te gebruiken, zoals Hallo i/o-grootte voor optimale prestaties.</span><span class="sxs-lookup"><span data-stu-id="f7ce6-154">If you don’t have a specific minimum I/O size requirement, we recommend that you use 1 MB as hello I/O size for optimal performance.</span></span>
-   <span data-ttu-id="f7ce6-155">Als u weet Hallo uiteindelijke omvang van een bestand dat u met uitbreiden schrijft en uw software geen compatibiliteitsproblemen wanneer hello unwritten tail op Hallo-bestand bevat nullen, vervolgens set Hallo bestandsgrootte van tevoren in plaats van elke schrijfbewerking waardoor het terugschrijven van een uitbreiden.</span><span class="sxs-lookup"><span data-stu-id="f7ce6-155">If you know hello final size of a file that you are extending with writes, and your software doesn’t have compatibility problems when hello unwritten tail on hello file contains zeros, then set hello file size in advance instead of making every write an extending write.</span></span>
-   <span data-ttu-id="f7ce6-156">Hallo rechts copy-methode gebruiken:</span><span class="sxs-lookup"><span data-stu-id="f7ce6-156">Use hello right copy method:</span></span>
    -   <span data-ttu-id="f7ce6-157">Gebruik [AzCopy](storage-use-azcopy.md#file-copy) de overdracht tussen twee bestandsshares.</span><span class="sxs-lookup"><span data-stu-id="f7ce6-157">Use [AzCopy](storage-use-azcopy.md#file-copy) for any transfer between two file shares.</span></span>
    -   <span data-ttu-id="f7ce6-158">Gebruik [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) tussen bestandsshares op een on-premises computer.</span><span class="sxs-lookup"><span data-stu-id="f7ce6-158">Use [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) between file shares on an on-premises computer.</span></span>

### <a name="considerations-for-windows-81-or-windows-server-2012-r2"></a><span data-ttu-id="f7ce6-159">Overwegingen voor Windows 8.1 of Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="f7ce6-159">Considerations for Windows 8.1 or Windows Server 2012 R2</span></span>

<span data-ttu-id="f7ce6-160">Voor clients met Windows 8.1 of Windows Server 2012 R2, zorg ervoor dat Hallo [KB3114025](https://support.microsoft.com/help/3114025) hotfix is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="f7ce6-160">For clients that are running Windows 8.1 or Windows Server 2012 R2, make sure that hello [KB3114025](https://support.microsoft.com/help/3114025) hotfix is installed.</span></span> <span data-ttu-id="f7ce6-161">Deze hotfix verbetert de prestaties van create Hallo en ingangen sluit.</span><span class="sxs-lookup"><span data-stu-id="f7ce6-161">This hotfix improves hello performance of create and close handles.</span></span>

<span data-ttu-id="f7ce6-162">Hallo script toocheck te volgen of Hallo hotfix is geïnstalleerd, kunt u uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="f7ce6-162">You can run hello following script toocheck whether hello hotfix has been installed:</span></span>

`reg query HKLM\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters\Policies`

<span data-ttu-id="f7ce6-163">Als hotfix is geïnstalleerd, hello volgende uitvoer weergegeven:</span><span class="sxs-lookup"><span data-stu-id="f7ce6-163">If hotfix is installed, hello following output is displayed:</span></span>

`HKEY_Local_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters\Policies {96c345ef-3cac-477b-8fcd-bea1a564241c} REG_DWORD 0x1`

> [!Note]
> <span data-ttu-id="f7ce6-164">Windows Server 2012 R2-afbeeldingen in Azure Marketplace hebben hotfix KB3114025 standaard geïnstalleerd, vanaf December 2015.</span><span class="sxs-lookup"><span data-stu-id="f7ce6-164">Windows Server 2012 R2 images in Azure Marketplace have hotfix KB3114025 installed by default, starting in December 2015.</span></span>

<a id="shareismissing"></a>
## <a name="no-folder-with-a-drive-letter-in-my-computer"></a><span data-ttu-id="f7ce6-165">Er is geen map met een stationsletter in **Mijn Computer**</span><span class="sxs-lookup"><span data-stu-id="f7ce6-165">No folder with a drive letter in **My Computer**</span></span>

<span data-ttu-id="f7ce6-166">Als u een Azure-bestandsshare als een beheerder met behulp van net gebruik toewijst, Hallo share toobe weergegeven ontbreekt.</span><span class="sxs-lookup"><span data-stu-id="f7ce6-166">If you map an Azure file share as an administrator by using net use, hello share appears toobe missing.</span></span>

### <a name="cause"></a><span data-ttu-id="f7ce6-167">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="f7ce6-167">Cause</span></span>

<span data-ttu-id="f7ce6-168">Windows Verkenner wordt niet uitgevoerd als beheerder.</span><span class="sxs-lookup"><span data-stu-id="f7ce6-168">By default, Windows File Explorer does not run as an administrator.</span></span> <span data-ttu-id="f7ce6-169">Als u net gebruik van een administratieve opdrachtprompt uitvoert, wordt het Hallo-netwerkstation toewijzen als beheerder.</span><span class="sxs-lookup"><span data-stu-id="f7ce6-169">If you run net use from an administrative command prompt, you map hello network drive as an administrator.</span></span> <span data-ttu-id="f7ce6-170">Omdat netwerkstations gebruikersgerichte zijn, wordt Hallo-gebruikersaccount dat is aangemeld Hallo stations niet weergegeven als ze worden gekoppeld onder een ander gebruikersaccount.</span><span class="sxs-lookup"><span data-stu-id="f7ce6-170">Because mapped drives are user-centric, hello user account that is logged in does not display hello drives if they are mounted under a different user account.</span></span>

### <a name="solution"></a><span data-ttu-id="f7ce6-171">Oplossing</span><span class="sxs-lookup"><span data-stu-id="f7ce6-171">Solution</span></span>
<span data-ttu-id="f7ce6-172">Hallo-share koppelen vanuit een opdrachtregel niet-beheerders.</span><span class="sxs-lookup"><span data-stu-id="f7ce6-172">Mount hello share from a non-administrator command line.</span></span> <span data-ttu-id="f7ce6-173">U kunt ook kunt u [dit TechNet-onderwerp](https://technet.microsoft.com/library/ee844140.aspx) tooconfigure hello **EnableLinkedConnections** registerwaarde.</span><span class="sxs-lookup"><span data-stu-id="f7ce6-173">Alternatively, you can follow [this TechNet topic](https://technet.microsoft.com/library/ee844140.aspx) tooconfigure hello **EnableLinkedConnections** registry value.</span></span>

<a id="netuse"></a>
## <a name="net-use-command-fails-if-hello-storage-account-contains-a-forward-slash"></a><span data-ttu-id="f7ce6-174">Opdracht net use mislukt als Hallo-opslagaccount een slash bevat</span><span class="sxs-lookup"><span data-stu-id="f7ce6-174">Net use command fails if hello storage account contains a forward slash</span></span>

### <a name="cause"></a><span data-ttu-id="f7ce6-175">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="f7ce6-175">Cause</span></span>

<span data-ttu-id="f7ce6-176">de opdracht net use Hello wordt een slash (/) geïnterpreteerd als een opdrachtregeloptie.</span><span class="sxs-lookup"><span data-stu-id="f7ce6-176">hello net use command interprets a forward slash (/) as a command-line option.</span></span> <span data-ttu-id="f7ce6-177">Als de naam van uw gebruikersaccount wordt gestart met een slash, mislukt de stationstoewijzing Hallo.</span><span class="sxs-lookup"><span data-stu-id="f7ce6-177">If your user account name starts with a forward slash, hello drive mapping fails.</span></span>

### <a name="solution"></a><span data-ttu-id="f7ce6-178">Oplossing</span><span class="sxs-lookup"><span data-stu-id="f7ce6-178">Solution</span></span>

<span data-ttu-id="f7ce6-179">U kunt gebruiken Hallo toowork rond Hallo probleem stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f7ce6-179">You can use either of hello following steps toowork around hello problem:</span></span>

- <span data-ttu-id="f7ce6-180">Hallo volgende PowerShell-opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="f7ce6-180">Run hello following PowerShell command:</span></span>

  `New-SmbMapping -LocalPath y: -RemotePath \\server\share -UserName accountName -Password "password can contain / and \ etc" `

  <span data-ttu-id="f7ce6-181">Vanuit een batchbestand kunt u Hallo-opdracht uitvoeren op deze manier:</span><span class="sxs-lookup"><span data-stu-id="f7ce6-181">From a batch file, you can run hello command this way:</span></span>

  `Echo new-smbMapping ... | powershell -command –`

- <span data-ttu-id="f7ce6-182">Dubbele aanhalingstekens rond Hallo sleutel toowork om dit probleem--geplaatst tenzij de schuine streep Hallo Hallo eerste teken.</span><span class="sxs-lookup"><span data-stu-id="f7ce6-182">Put double quotation marks around hello key toowork around this problem--unless hello forward slash is hello first character.</span></span> <span data-ttu-id="f7ce6-183">Als het, Hallo interactieve modus gebruiken en voer uw wachtwoord afzonderlijk of opnieuw genereren van uw sleutels tooget een sleutel die niet met een slash begint.</span><span class="sxs-lookup"><span data-stu-id="f7ce6-183">If it is, either use hello interactive mode and enter your password separately or regenerate your keys tooget a key that doesn't start with a forward slash.</span></span>

<a id="cannotaccess"></a>
## <a name="application-or-service-cannot-access-a-mounted-azure-file-storage-drive"></a><span data-ttu-id="f7ce6-184">Toepassing of service heeft geen toegang tot een gekoppelde Azure File storage-station</span><span class="sxs-lookup"><span data-stu-id="f7ce6-184">Application or service cannot access a mounted Azure File storage drive</span></span>

### <a name="cause"></a><span data-ttu-id="f7ce6-185">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="f7ce6-185">Cause</span></span>

<span data-ttu-id="f7ce6-186">Schijven zijn per gebruiker gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="f7ce6-186">Drives are mounted per user.</span></span> <span data-ttu-id="f7ce6-187">Als uw toepassing of service wordt uitgevoerd onder een ander gebruikersaccount dan Hallo die gekoppeld station hello, ziet Hallo toepassing hello station niet.</span><span class="sxs-lookup"><span data-stu-id="f7ce6-187">If your application or service is running under a different user account than hello one that mounted hello drive, hello application will not see hello drive.</span></span>

### <a name="solution"></a><span data-ttu-id="f7ce6-188">Oplossing</span><span class="sxs-lookup"><span data-stu-id="f7ce6-188">Solution</span></span>

<span data-ttu-id="f7ce6-189">Gebruik een van de volgende oplossingen Hallo:</span><span class="sxs-lookup"><span data-stu-id="f7ce6-189">Use one of hello following solutions:</span></span>

-   <span data-ttu-id="f7ce6-190">Hallo-station koppelen vanuit Hallo hetzelfde gebruikersaccount dat de toepassing hello bevat.</span><span class="sxs-lookup"><span data-stu-id="f7ce6-190">Mount hello drive from hello same user account that contains hello application.</span></span> <span data-ttu-id="f7ce6-191">U kunt een hulpprogramma zoals PsExec gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f7ce6-191">You can use a tool such as PsExec.</span></span>
- <span data-ttu-id="f7ce6-192">Hallo opslagaccountnaam en de sleutel in Hallo gebruiker naam en het wachtwoord parameters van de opdracht net use Hallo doorgeven.</span><span class="sxs-lookup"><span data-stu-id="f7ce6-192">Pass hello storage account name and key in hello user name and password parameters of hello net use command.</span></span>

<span data-ttu-id="f7ce6-193">Nadat u deze instructies opvolgt, Hallo volgende foutbericht wordt weergegeven tijdens het uitvoeren van net gebruiken voor Hallo system/Netwerkservice-account kan worden weergegeven: 'Systeemfout 1312 is opgetreden.</span><span class="sxs-lookup"><span data-stu-id="f7ce6-193">After you follow these instructions, you might receive hello following error message when you run net use for hello system/network service account: "System error 1312 has occurred.</span></span> <span data-ttu-id="f7ce6-194">De sessie van een opgegeven gebruiker bestaat niet.</span><span class="sxs-lookup"><span data-stu-id="f7ce6-194">A specified logon session does not exist.</span></span> <span data-ttu-id="f7ce6-195">Het is mogelijk al beëindigd."</span><span class="sxs-lookup"><span data-stu-id="f7ce6-195">It may already have been terminated."</span></span> <span data-ttu-id="f7ce6-196">Als dit het geval is, zorg ervoor dat Hallo-gebruikersnaam die wordt doorgegeven toonet gebruik domeingegevens bevat (bijvoorbeeld: ' [opslagaccountnaam]. file.core.windows .net ').</span><span class="sxs-lookup"><span data-stu-id="f7ce6-196">If this occurs, make sure that hello username that is passed toonet use includes domain information (for example: "[storage account name].file.core.windows.net").</span></span>

<a id="doesnotsupportencryption"></a>
## <a name="error-you-are-copying-a-file-tooa-destination-that-does-not-support-encryption"></a><span data-ttu-id="f7ce6-197">'U kopieert een bestand tooa doel geen versleuteling ondersteunt' fout</span><span class="sxs-lookup"><span data-stu-id="f7ce6-197">Error "You are copying a file tooa destination that does not support encryption"</span></span>

<span data-ttu-id="f7ce6-198">Als een bestand wordt gekopieerd via Hallo netwerk, is Hallo-bestand op Hallo broncomputer verzonden als leesbare tekst en opnieuw versleuteld op Hallo bestemming te ontsleutelen.</span><span class="sxs-lookup"><span data-stu-id="f7ce6-198">When a file is copied over hello network, hello file is decrypted on hello source computer, transmitted in plaintext, and re-encrypted at hello destination.</span></span> <span data-ttu-id="f7ce6-199">Echter, ziet u mogelijk Hallo volgende fout wanneer u een versleuteld bestand toocopy probeert: "Kopieert u Hallo tooa bestemming die geen ondersteuning biedt voor versleuteling."</span><span class="sxs-lookup"><span data-stu-id="f7ce6-199">However, you might see hello following error when you're trying toocopy an encrypted file: "You are copying hello file tooa destination that does not support encryption."</span></span>

### <a name="cause"></a><span data-ttu-id="f7ce6-200">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="f7ce6-200">Cause</span></span>
<span data-ttu-id="f7ce6-201">Dit probleem kan optreden als u van Encrypting File System (EFS gebruikmaakt).</span><span class="sxs-lookup"><span data-stu-id="f7ce6-201">This problem can occur if you are using Encrypting File System (EFS).</span></span> <span data-ttu-id="f7ce6-202">BitLocker-versleuteling-bestanden kunnen worden gekopieerd tooAzure File storage.</span><span class="sxs-lookup"><span data-stu-id="f7ce6-202">BitLocker-encrypted files can be copied tooAzure File storage.</span></span> <span data-ttu-id="f7ce6-203">Azure File storage biedt echter geen ondersteuning voor NTFS EFS.</span><span class="sxs-lookup"><span data-stu-id="f7ce6-203">However, Azure File storage does not support NTFS EFS.</span></span>

### <a name="workaround"></a><span data-ttu-id="f7ce6-204">Tijdelijke oplossing</span><span class="sxs-lookup"><span data-stu-id="f7ce6-204">Workaround</span></span>
<span data-ttu-id="f7ce6-205">een bestand via Hallo netwerk toocopy, u moet eerst worden gedecodeerd.</span><span class="sxs-lookup"><span data-stu-id="f7ce6-205">toocopy a file over hello network, you must first decrypt it.</span></span> <span data-ttu-id="f7ce6-206">Een van de volgende methoden hello gebruiken:</span><span class="sxs-lookup"><span data-stu-id="f7ce6-206">Use one of hello following methods:</span></span>

- <span data-ttu-id="f7ce6-207">Gebruik Hallo **kopiëren /d** opdracht.</span><span class="sxs-lookup"><span data-stu-id="f7ce6-207">Use hello **copy /d** command.</span></span> <span data-ttu-id="f7ce6-208">Kunt u Hallo versleuteld opgeslagen als de ontsleutelde bestanden op de bestemming Hallo toobe bestanden.</span><span class="sxs-lookup"><span data-stu-id="f7ce6-208">It allows hello encrypted files toobe saved as decrypted files at hello destination.</span></span>
- <span data-ttu-id="f7ce6-209">Stel Hallo volgende registersleutel:</span><span class="sxs-lookup"><span data-stu-id="f7ce6-209">Set hello following registry key:</span></span>
  - <span data-ttu-id="f7ce6-210">Pad = HKLM\Software\Policies\Microsoft\Windows\System</span><span class="sxs-lookup"><span data-stu-id="f7ce6-210">Path = HKLM\Software\Policies\Microsoft\Windows\System</span></span>
  - <span data-ttu-id="f7ce6-211">Waarde type DWORD =</span><span class="sxs-lookup"><span data-stu-id="f7ce6-211">Value type = DWORD</span></span>
  - <span data-ttu-id="f7ce6-212">Naam CopyFileAllowDecryptedRemoteDestination =</span><span class="sxs-lookup"><span data-stu-id="f7ce6-212">Name = CopyFileAllowDecryptedRemoteDestination</span></span>
  - <span data-ttu-id="f7ce6-213">Waarde = 1</span><span class="sxs-lookup"><span data-stu-id="f7ce6-213">Value = 1</span></span>

<span data-ttu-id="f7ce6-214">Let die instelling Hallo-registersleutel is van invloed op alle kopieerbewerkingen die zijn aangebracht toonetwork shares.</span><span class="sxs-lookup"><span data-stu-id="f7ce6-214">Be aware that setting hello registry key affects all copy operations that are made toonetwork shares.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="f7ce6-215">Hulp nodig?</span><span class="sxs-lookup"><span data-stu-id="f7ce6-215">Need help?</span></span> <span data-ttu-id="f7ce6-216">Neem contact op met ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="f7ce6-216">Contact support.</span></span>
<span data-ttu-id="f7ce6-217">Als u nog hulp nodig hebt, [contact op met ondersteuning](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget snel uw probleem is opgelost.</span><span class="sxs-lookup"><span data-stu-id="f7ce6-217">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your problem resolved quickly.</span></span>
