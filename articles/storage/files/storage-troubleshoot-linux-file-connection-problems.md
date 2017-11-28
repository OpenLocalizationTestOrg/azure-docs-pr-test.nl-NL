---
title: problemen met aaaTroubleshoot Azure File storage in Linux | Microsoft Docs
description: Problemen met Azure File storage in Linux
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
ms.date: 07/11/2017
ms.author: genli
ms.openlocfilehash: 4bdc3c6ed2e48f245060a03632fca9bd14d33545
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-file-storage-problems-in-linux"></a><span data-ttu-id="19fd9-103">Problemen met Azure File storage in Linux</span><span class="sxs-lookup"><span data-stu-id="19fd9-103">Troubleshoot Azure File storage problems in Linux</span></span>

<span data-ttu-id="19fd9-104">Dit artikel worden veelvoorkomende problemen die gerelateerde tooMicrosoft Azure File storage zijn wanneer u verbinding vanaf een Linux-clients maakt.</span><span class="sxs-lookup"><span data-stu-id="19fd9-104">This article lists common problems that are related tooMicrosoft Azure File storage when you connect from Linux clients.</span></span> <span data-ttu-id="19fd9-105">Het bevat ook mogelijke oorzaken en oplossingen voor deze problemen.</span><span class="sxs-lookup"><span data-stu-id="19fd9-105">It also provides possible causes and resolutions for these problems.</span></span>

<a id="permissiondenied"></a>
## <a name="permission-denied-disk-quota-exceeded-when-you-try-tooopen-a-file"></a><span data-ttu-id="19fd9-106">"[toegang geweigerd] schijfquotum is overschreden" wanneer u probeert een bestand tooopen</span><span class="sxs-lookup"><span data-stu-id="19fd9-106">"[permission denied] Disk quota exceeded" when you try tooopen a file</span></span>

<span data-ttu-id="19fd9-107">U ontvangt een foutbericht weergegeven dat lijkt op de volgende Hallo in Linux:</span><span class="sxs-lookup"><span data-stu-id="19fd9-107">In Linux, you receive an error message that resembles hello following:</span></span>

<span data-ttu-id="19fd9-108">**<filename>[toegang geweigerd] Schijfquotum is overschreden**</span><span class="sxs-lookup"><span data-stu-id="19fd9-108">**<filename> [permission denied] Disk quota exceeded**</span></span>

### <a name="cause"></a><span data-ttu-id="19fd9-109">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="19fd9-109">Cause</span></span>

<span data-ttu-id="19fd9-110">Hallo bovenlimiet van gelijktijdige open ingangen die zijn toegestaan voor een bestand is bereikt.</span><span class="sxs-lookup"><span data-stu-id="19fd9-110">You have reached hello upper limit of concurrent open handles that are allowed for a file.</span></span>

### <a name="solution"></a><span data-ttu-id="19fd9-111">Oplossing</span><span class="sxs-lookup"><span data-stu-id="19fd9-111">Solution</span></span>

<span data-ttu-id="19fd9-112">Het aantal gelijktijdige open ingangen Hallo verminderen door te sluiten van een aantal ingangen en probeer Hallo opnieuw.</span><span class="sxs-lookup"><span data-stu-id="19fd9-112">Reduce hello number of concurrent open handles by closing some handles, and then retry hello operation.</span></span> <span data-ttu-id="19fd9-113">Zie voor meer informatie [controlelijst voor prestaties en schaalbaarheid van Microsoft Azure Storage](../common/storage-performance-checklist.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="19fd9-113">For more information, see [Microsoft Azure Storage performance and scalability checklist](../common/storage-performance-checklist.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span></span>

<a id="slowfilecopying"></a>
## <a name="slow-file-copying-tooand-from-azure-file-storage-in-linux"></a><span data-ttu-id="19fd9-114">Trage bestand tooand kopiëren van Azure File storage in Linux</span><span class="sxs-lookup"><span data-stu-id="19fd9-114">Slow file copying tooand from Azure File storage in Linux</span></span>

-   <span data-ttu-id="19fd9-115">Als u een specifieke i/o-grootte minimumvereiste hebt, raden wij 1 MB te gebruiken, zoals Hallo i/o-grootte voor optimale prestaties.</span><span class="sxs-lookup"><span data-stu-id="19fd9-115">If you don’t have a specific minimum I/O size requirement, we recommend that you use 1 MB as hello I/O size for optimal performance.</span></span>
-   <span data-ttu-id="19fd9-116">Als u weet dat de uiteindelijke omvang Hallo van een bestand dat u met behulp van schrijfbewerkingen uitbreidt en de software niet compatibiliteitsproblemen ervaren wanneer een unwritten tail op Hallo bestand nullen bevat, klikt u vervolgens de bestandsgrootte Hallo van tevoren in plaats van het maken van een uitbreiding van elke schrijfbewerking instellen schrijven.</span><span class="sxs-lookup"><span data-stu-id="19fd9-116">If you know hello final size of a file that you are extending by using writes, and your software doesn’t experience compatibility problems when an unwritten tail on hello file contains zeros, then set hello file size in advance instead of making every write an extending write.</span></span>
-   <span data-ttu-id="19fd9-117">Hallo rechts copy-methode gebruiken:</span><span class="sxs-lookup"><span data-stu-id="19fd9-117">Use hello right copy method:</span></span>
    -   <span data-ttu-id="19fd9-118">Gebruik [AzCopy](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#file-copy) de overdracht tussen twee bestandsshares.</span><span class="sxs-lookup"><span data-stu-id="19fd9-118">Use [AzCopy](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#file-copy) for any transfer between two file shares.</span></span>
    -   <span data-ttu-id="19fd9-119">Gebruik [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) tussen bestandsshares op een on-premises computer.</span><span class="sxs-lookup"><span data-stu-id="19fd9-119">Use [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) between file shares on an on-premises computer.</span></span>

<a id="error112"></a>
## <a name="mount-error112-host-is-down-because-of-a-reconnection-time-out"></a><span data-ttu-id="19fd9-120">' Error(112) koppelen: Host is niet beschikbaar ' vanwege een time-out van de nieuwe verbindingen</span><span class="sxs-lookup"><span data-stu-id="19fd9-120">"Mount error(112): Host is down" because of a reconnection time-out</span></span>

<span data-ttu-id="19fd9-121">Een '112' mount-fout treedt op Hallo Linux-client als Hallo client gedurende een lange periode niet actief is geweest.</span><span class="sxs-lookup"><span data-stu-id="19fd9-121">A "112" mount error occurs on hello Linux client when hello client has been idle for a long time.</span></span> <span data-ttu-id="19fd9-122">Na de uitgebreide niet-actieve tijd, Hallo-client de verbinding verbreekt en Hallo verbinding een time-out optreedt.</span><span class="sxs-lookup"><span data-stu-id="19fd9-122">After extended idle time, hello client disconnects and hello connection times out.</span></span>  

### <a name="cause"></a><span data-ttu-id="19fd9-123">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="19fd9-123">Cause</span></span>

<span data-ttu-id="19fd9-124">Hallo-verbinding tot stand kan worden gedurende de volgende redenen Hallo:</span><span class="sxs-lookup"><span data-stu-id="19fd9-124">hello connection can be idle for hello following reasons:</span></span>

-   <span data-ttu-id="19fd9-125">Communicatie netwerkfouten die voorkomen dat het herstellen van een TCP-verbinding toohello server wanneer de standaardoptie mount 'soft' hello wordt gebruikt</span><span class="sxs-lookup"><span data-stu-id="19fd9-125">Network communication failures that prevent re-establishing a TCP connection toohello server when hello default “soft” mount option is used</span></span>
-   <span data-ttu-id="19fd9-126">Recente opnieuw verbinden met oplossingen die niet aanwezig in oudere kernels zijn</span><span class="sxs-lookup"><span data-stu-id="19fd9-126">Recent reconnection fixes that are not present in older kernels</span></span>

### <a name="solution"></a><span data-ttu-id="19fd9-127">Oplossing</span><span class="sxs-lookup"><span data-stu-id="19fd9-127">Solution</span></span>

<span data-ttu-id="19fd9-128">Dit probleem opnieuw verbinding te maken in Linux-kernel Hallo is nu opgelost als onderdeel van de volgende wijzigingen Hallo:</span><span class="sxs-lookup"><span data-stu-id="19fd9-128">This reconnection problem in hello Linux kernel is now fixed as part of hello following changes:</span></span>

- [<span data-ttu-id="19fd9-129">FIX verbinding toonot smb3-sessie uit te stellen verbinding lang nadat socket opnieuw verbinding maken</span><span class="sxs-lookup"><span data-stu-id="19fd9-129">Fix reconnect toonot defer smb3 session reconnect long after socket reconnect</span></span>](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/fs/cifs?id=4fcd1813e6404dd4420c7d12fb483f9320f0bf93)
-   [<span data-ttu-id="19fd9-130">Echo-service aanroepen onmiddellijk nadat de socket opnieuw verbinding maken</span><span class="sxs-lookup"><span data-stu-id="19fd9-130">Call echo service immediately after socket reconnect</span></span>](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=b8c600120fc87d53642476f48c8055b38d6e14c7)
-   [<span data-ttu-id="19fd9-131">CIFS: Een geheugenbeschadiging van de mogelijke tijdens reconnect oplossen</span><span class="sxs-lookup"><span data-stu-id="19fd9-131">CIFS: Fix a possible memory corruption during reconnect</span></span>](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=53e0e11efe9289535b060a51d4cf37c25e0d0f2b)
-   [<span data-ttu-id="19fd9-132">CIFS: Los een mogelijke dubbele vergrendeling van mutex tijdens reconnect (voor kernel v4.9 en hoger)</span><span class="sxs-lookup"><span data-stu-id="19fd9-132">CIFS: Fix a possible double locking of mutex during reconnect (for kernel v4.9 and later)</span></span>](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=96a988ffeb90dba33a71c3826086fe67c897a183)

<span data-ttu-id="19fd9-133">Deze wijzigingen kunnen echter niet worden overgezet nog tooall Hallo Linux-distributies.</span><span class="sxs-lookup"><span data-stu-id="19fd9-133">However, these changes might not be ported yet tooall hello Linux distributions.</span></span> <span data-ttu-id="19fd9-134">Deze oplossing en andere correcties voor nieuwe verbindingen zijn aangebracht in Hallo populaire Linux kernels te volgen: 4.4.40 4.8.16 en 4.9.1.</span><span class="sxs-lookup"><span data-stu-id="19fd9-134">This fix and other reconnection fixes are made in hello following popular Linux kernels: 4.4.40, 4.8.16, and 4.9.1.</span></span> <span data-ttu-id="19fd9-135">U kunt deze oplossing ophalen door het upgraden van tooone van deze aanbevolen kernel-versies.</span><span class="sxs-lookup"><span data-stu-id="19fd9-135">You can get this fix by upgrading tooone of these recommended kernel versions.</span></span>

### <a name="workaround"></a><span data-ttu-id="19fd9-136">Tijdelijke oplossing</span><span class="sxs-lookup"><span data-stu-id="19fd9-136">Workaround</span></span>

<span data-ttu-id="19fd9-137">U kunt dit probleem omzeilen door te geven van een harde koppeling.</span><span class="sxs-lookup"><span data-stu-id="19fd9-137">You can work around this problem by specifying a hard mount.</span></span> <span data-ttu-id="19fd9-138">Hallo client toowait wordt gedwongen totdat een verbinding tot stand is gebracht of totdat deze expliciet wordt onderbroken en gebruikte tooprevent fouten vanwege netwerk time-outs kan worden.</span><span class="sxs-lookup"><span data-stu-id="19fd9-138">This forces hello client toowait until a connection is established or until it’s explicitly interrupted and can be used tooprevent errors because of network time-outs.</span></span> <span data-ttu-id="19fd9-139">Deze tijdelijke oplossing kan echter de onbepaalde wachttijd veroorzaken.</span><span class="sxs-lookup"><span data-stu-id="19fd9-139">However, this workaround might cause indefinite waits.</span></span> <span data-ttu-id="19fd9-140">Voorbereide toostop verbindingen zoals die nodig zijn.</span><span class="sxs-lookup"><span data-stu-id="19fd9-140">Be prepared toostop connections as necessary.</span></span>

<span data-ttu-id="19fd9-141">Als u de meest recente kernel-versies toohello niet bijwerken, kunt u dit probleem omzeilen door een bestand in hello Azure-bestandsshare die u tooevery 30 seconden schrijft of minder.</span><span class="sxs-lookup"><span data-stu-id="19fd9-141">If you cannot upgrade toohello latest kernel versions, you can work around this problem by keeping a file in hello Azure file share that you write tooevery 30 seconds or less.</span></span> <span data-ttu-id="19fd9-142">Dit moet een schrijfbewerking zoals herschrijven Hallo op gemaakt of gewijzigd datum Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="19fd9-142">This must be a write operation, such as rewriting hello created or modified date on hello file.</span></span> <span data-ttu-id="19fd9-143">Anders krijgt u mogelijk de resultaten in het cachegeheugen en uw bewerking mogelijk opnieuw verbinden met Hallo niet activeren.</span><span class="sxs-lookup"><span data-stu-id="19fd9-143">Otherwise, you might get cached results, and your operation might not trigger hello reconnection.</span></span>

<a id="error115"></a>
## <a name="mount-error115-operation-now-in-progress-when-you-mount-azure-file-storage-by-using-smb-30"></a><span data-ttu-id="19fd9-144">' Error(115) koppelen: Bezig met bewerking ' bij het koppelen van Azure File storage met behulp van SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="19fd9-144">"Mount error(115): Operation now in progress" when you mount Azure File storage by using SMB 3.0</span></span>

### <a name="cause"></a><span data-ttu-id="19fd9-145">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="19fd9-145">Cause</span></span>

<span data-ttu-id="19fd9-146">Sommige Linux-distributies nog ondersteunen geen versleutelingsfuncties in SMB 3.0 en gebruikers mogelijk foutbericht '115' als ze toomount Azure File storage proberen met behulp van SMB 3.0 vanwege een ontbrekend onderdeel.</span><span class="sxs-lookup"><span data-stu-id="19fd9-146">Some Linux distributions do not yet support encryption features in SMB 3.0 and users might receive a "115" error message if they try toomount Azure File storage by using SMB 3.0 because of a missing feature.</span></span>

### <a name="solution"></a><span data-ttu-id="19fd9-147">Oplossing</span><span class="sxs-lookup"><span data-stu-id="19fd9-147">Solution</span></span>

<span data-ttu-id="19fd9-148">Coderingsfunctie voor SMB 3.0 voor Linux is geïntroduceerd in 4.11 kernel.</span><span class="sxs-lookup"><span data-stu-id="19fd9-148">Encryption feature for SMB 3.0 for Linux was introduced in 4.11 kernel.</span></span> <span data-ttu-id="19fd9-149">Deze functie kunt koppelen van de bestandsshare in Azure vanaf on-premises of andere Azure-regio.</span><span class="sxs-lookup"><span data-stu-id="19fd9-149">This feature enables mounting of Azure File share from on-premises or a different Azure region.</span></span> <span data-ttu-id="19fd9-150">Op Hallo moment van publicatie is deze functionaliteit backported tooUbuntu 17.04 en Ubuntu 16,10.</span><span class="sxs-lookup"><span data-stu-id="19fd9-150">At hello time of publishing, this functionality has been backported tooUbuntu 17.04 and Ubuntu 16.10.</span></span> <span data-ttu-id="19fd9-151">Als uw Linux SMB-client geen ondersteuning biedt voor versleuteling, koppelt u Azure File storage met behulp van SMB 2.1 van een Azure Linux VM die zich in hetzelfde datacenter Hallo zoals Hallo File storage-account.</span><span class="sxs-lookup"><span data-stu-id="19fd9-151">If your Linux SMB client does not support encryption, mount Azure File storage by using SMB 2.1 from an Azure Linux VM that's in hello same datacenter as hello File storage account.</span></span>

<a id="slowperformance"></a>
## <a name="slow-performance-on-an-azure-file-share-mounted-on-a-linux-vm"></a><span data-ttu-id="19fd9-152">Langzame prestaties van een Azure-bestandsshare die is gekoppeld aan een Linux-VM</span><span class="sxs-lookup"><span data-stu-id="19fd9-152">Slow performance on an Azure file share mounted on a Linux VM</span></span>

### <a name="cause"></a><span data-ttu-id="19fd9-153">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="19fd9-153">Cause</span></span>

<span data-ttu-id="19fd9-154">Een mogelijke oorzaak van vertragingen bij het opslaan in cache is uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="19fd9-154">One possible cause of slow performance is disabled caching.</span></span>

### <a name="solution"></a><span data-ttu-id="19fd9-155">Oplossing</span><span class="sxs-lookup"><span data-stu-id="19fd9-155">Solution</span></span>

<span data-ttu-id="19fd9-156">toocheck of opslaan in cache is uitgeschakeld, zoekt u naar Hallo **cache =** vermelding.</span><span class="sxs-lookup"><span data-stu-id="19fd9-156">toocheck whether caching is disabled, look for hello **cache=** entry.</span></span> 

<span data-ttu-id="19fd9-157">**Cache = geen** geeft aan dat opslaan in cache is uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="19fd9-157">**Cache=none** indicates that caching is disabled.</span></span>  <span data-ttu-id="19fd9-158">Koppelen Hallo share met Hallo standaard koppelpunt opdracht of door expliciet toe te voegen Hallo **cache = strikte** optie toohello koppelpunt opdracht tooensure die standaard in het cachegeheugen of 'strict' cache-modus is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="19fd9-158">Remount hello share by using hello default mount command or by explicitly adding hello **cache=strict** option toohello mount command tooensure that default caching or "strict" caching mode is enabled.</span></span>

<span data-ttu-id="19fd9-159">In sommige gevallen Hallo **serverino** mount-optie kan leiden tot Hallo **ls** opdracht toorun stat tegen elke directory-vermelding.</span><span class="sxs-lookup"><span data-stu-id="19fd9-159">In some scenarios, hello **serverino** mount option can cause hello **ls** command toorun stat against every directory entry.</span></span> <span data-ttu-id="19fd9-160">Dit gedrag leidt tot verminderde prestaties wanneer u een grote directory aangeboden.</span><span class="sxs-lookup"><span data-stu-id="19fd9-160">This behavior results in performance degradation when you're listing a big directory.</span></span> <span data-ttu-id="19fd9-161">U kunt opties voor het koppelen van Hallo controleren uw **/etc/fstab** post:</span><span class="sxs-lookup"><span data-stu-id="19fd9-161">You can check hello mount options in your **/etc/fstab** entry:</span></span>

`//azureuser.file.core.windows.net/cifs /cifs cifs vers=3.0,serverino,username=xxx,password=xxx,dir_mode=0777,file_mode=0777`

<span data-ttu-id="19fd9-162">U kunt ook controleren of de juiste opties hello worden gebruikt door Hallo uitgevoerd **sudo koppelen | grep cifs** opdracht en de uitvoer, zoals de volgende voorbeelduitvoer hello te controleren:</span><span class="sxs-lookup"><span data-stu-id="19fd9-162">You can also check whether hello correct options are being used by running hello  **sudo mount | grep cifs** command and checking its output, such as hello following example output:</span></span>

`//mabiccacifs.file.core.windows.net/cifs on /cifs type cifs (rw,relatime,vers=3.0,sec=ntlmssp,cache=strict,username=xxx,domain=X,uid=0,noforceuid,gid=0,noforcegid,addr=192.168.10.1,file_mode=0777, dir_mode=0777,persistenthandles,nounix,serverino,mapposix,rsize=1048576,wsize=1048576,actimeo=1)`

<span data-ttu-id="19fd9-163">Als hello **cache = strikte** of **serverino** optie is niet aanwezig zijn, ontkoppelen en opnieuw koppelen van Azure File storage door Hallo koppelpunt opdracht vanaf Hallo [documentatie](../storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="19fd9-163">If hello **cache=strict** or **serverino** option is not present, unmount and mount Azure File storage again by running hello mount command from hello [documentation](../storage-how-to-use-files-linux.md).</span></span> <span data-ttu-id="19fd9-164">Vervolgens controleren die Hallo **/etc/fstab** vermelding heeft Hallo juiste opties.</span><span class="sxs-lookup"><span data-stu-id="19fd9-164">Then, recheck that hello **/etc/fstab** entry has hello correct options.</span></span>

<a id="timestampslost"></a>
## <a name="time-stamps-were-lost-in-copying-files-from-windows-toolinux"></a><span data-ttu-id="19fd9-165">Tijdstempels verloren zijn gegaan bij het kopiëren van bestanden van Windows tooLinux</span><span class="sxs-lookup"><span data-stu-id="19fd9-165">Time stamps were lost in copying files from Windows tooLinux</span></span>

<span data-ttu-id="19fd9-166">Op Linux/Unix-platforms Hallo **cp -p** opdracht mislukt als de 1 en 2 bestand eigendom zijn van andere gebruikers.</span><span class="sxs-lookup"><span data-stu-id="19fd9-166">On Linux/Unix platforms, hello **cp -p** command fails if file 1 and file 2 are owned by different users.</span></span>

### <a name="cause"></a><span data-ttu-id="19fd9-167">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="19fd9-167">Cause</span></span>

<span data-ttu-id="19fd9-168">Hallo vlag force **f** in COPYFILE resulteert in het uitvoeren van **cp -p -f** op Unix.</span><span class="sxs-lookup"><span data-stu-id="19fd9-168">hello force flag **f** in COPYFILE results in executing **cp -p -f** on Unix.</span></span> <span data-ttu-id="19fd9-169">Deze opdracht mislukt ook toopreserve Hallo tijdstempel van Hallo-bestand dat u niet de eigenaar.</span><span class="sxs-lookup"><span data-stu-id="19fd9-169">This command also fails toopreserve hello time stamp of hello file that you don't own.</span></span>

### <a name="workaround"></a><span data-ttu-id="19fd9-170">Tijdelijke oplossing</span><span class="sxs-lookup"><span data-stu-id="19fd9-170">Workaround</span></span>

<span data-ttu-id="19fd9-171">Hallo storage accountgebruiker voor het kopiëren van bestanden hello gebruiken:</span><span class="sxs-lookup"><span data-stu-id="19fd9-171">Use hello storage account user for copying hello files:</span></span>

- `Useadd : [storage account name]`
- `Passwd [storage account name]`
- `Su [storage account name]`
- `Cp -p filename.txt /share`

## <a name="need-help-contact-support"></a><span data-ttu-id="19fd9-172">Hulp nodig?</span><span class="sxs-lookup"><span data-stu-id="19fd9-172">Need help?</span></span> <span data-ttu-id="19fd9-173">Neem contact op met ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="19fd9-173">Contact support.</span></span>

<span data-ttu-id="19fd9-174">Als u nog hulp nodig hebt, [contact op met ondersteuning](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget snel uw probleem is opgelost.</span><span class="sxs-lookup"><span data-stu-id="19fd9-174">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your problem resolved quickly.</span></span>
