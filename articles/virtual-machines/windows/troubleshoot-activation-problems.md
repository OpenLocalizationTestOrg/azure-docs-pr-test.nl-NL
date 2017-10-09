---
title: aaaTroubleshoot Windows virtuele machine activeringsproblemen in Azure | Microsoft Docs
description: Hallo bevat stappen voor het oplossen van problemen met Windows virtuele machine activation in Azure oplossen
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: genlin
manager: willchen
editor: 
tags: top-support-issue, azure-resource-manager
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 4ebdac66166e80dcd68cd9e2931b30a29ac01eef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-windows-virtual-machine-activation-problems"></a><span data-ttu-id="1da95-103">Windows Azure virtuele machine activation problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="1da95-103">Troubleshoot Azure Windows virtual machine activation problems</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="1da95-104">Als u problemen hebt bij het activeren van Windows Azure virtuele machine (VM) die van een aangepaste installatiekopie wordt gemaakt, kunt u Hallo informatie in dit document tootroubleshoot Hallo probleem.</span><span class="sxs-lookup"><span data-stu-id="1da95-104">If you have trouble when activating Azure Windows virtual machine (VM) that is created from a custom image, you can use hello information provided in this document tootroubleshoot hello issue.</span></span> 

## <a name="symptom"></a><span data-ttu-id="1da95-105">Symptoom</span><span class="sxs-lookup"><span data-stu-id="1da95-105">Symptom</span></span>

<span data-ttu-id="1da95-106">Wanneer u een Windows Azure VM tooactivate, u een foutbericht ontvangt bericht lijkt op Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="1da95-106">When you try tooactivate an Azure Windows VM, you receive an error message resembles hello following sample:</span></span>

<span data-ttu-id="1da95-107">**Fout: 0xC004F074 Hallo Software LicensingService gerapporteerd dat die Hallo-computer kan niet worden geactiveerd. Er is geen ManagementService KMS (Key) kan worden bereikt. Zie Hallo toepassingslogboek voor meer informatie.**</span><span class="sxs-lookup"><span data-stu-id="1da95-107">**Error: 0xC004F074 hello Software LicensingService reported that hello computer could not be activated. No Key ManagementService (KMS) could be contacted. Please see hello Application Event Log for additional information.**</span></span>

## <a name="cause"></a><span data-ttu-id="1da95-108">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="1da95-108">Cause</span></span>
<span data-ttu-id="1da95-109">In het algemeen optreden activeringsproblemen van de virtuele machine van Azure als virtuele machine van Windows hello niet is geconfigureerd met juiste Installatiecode voor KMS-client met behulp van Hallo of Hallo Windows VM heeft een connectiviteit probleem toohello Azure KMS-service (kms.core.windows.net, poort 1668).</span><span class="sxs-lookup"><span data-stu-id="1da95-109">Generally, Azure VM activation issues occur if hello Windows VM is not configured by using hello appropriate KMS client setup key, or hello Windows VM has a connectivity problem toohello Azure KMS service (kms.core.windows.net, port 1668).</span></span> 

## <a name="solution"></a><span data-ttu-id="1da95-110">Oplossing</span><span class="sxs-lookup"><span data-stu-id="1da95-110">Solution</span></span>

>[!NOTE]
><span data-ttu-id="1da95-111">Als u een site-naar-site-VPN en geforceerde tunneling, Zie [gebruik Azure aangepaste routes tooenable KMS-activering met geforceerde tunneling](http://blogs.msdn.com/b/mast/archive/2015/05/20/use-azure-custom-routes-to-enable-kms-activation-with-forced-tunneling.aspx).</span><span class="sxs-lookup"><span data-stu-id="1da95-111">If you are using a site-to-site VPN and forced tunneling, see [Use Azure custom routes tooenable KMS activation with forced tunneling](http://blogs.msdn.com/b/mast/archive/2015/05/20/use-azure-custom-routes-to-enable-kms-activation-with-forced-tunneling.aspx).</span></span> 
>
><span data-ttu-id="1da95-112">Als u ExpressRoute gebruikt en u hebt een standaardroute gepubliceerd, Zie [Azure VM mislukken tooactivate via ExpressRoute](http://blogs.msdn.com/b/mast/archive/2015/12/01/azure-vm-may-fail-to-activate-over-expressroute.aspx).</span><span class="sxs-lookup"><span data-stu-id="1da95-112">If you are using ExpressRoute and you have a default route published, see [Azure VM may fail tooactivate over ExpressRoute](http://blogs.msdn.com/b/mast/archive/2015/12/01/azure-vm-may-fail-to-activate-over-expressroute.aspx).</span></span>

### <a name="step-1-configure-hello-appropriate-kms-client-setup-key-for-windows-server-2016-and-windows-server-2012-r2"></a><span data-ttu-id="1da95-113">Stap 1 configureren Hallo juiste KMS-clientinstallatiecode (voor Windows Server 2016 en Windows Server 2012 R2)</span><span class="sxs-lookup"><span data-stu-id="1da95-113">Step 1 Configure hello appropriate KMS client setup key (for Windows Server 2016 and Windows Server 2012 R2)</span></span>

<span data-ttu-id="1da95-114">Hallo virtuele machine die wordt gemaakt van een aangepaste installatiekopie van Windows Server 2016 of Windows Server 2012 R2, moet u Hallo juiste KMS-clientinstallatiecode voor Hallo VM configureren.</span><span class="sxs-lookup"><span data-stu-id="1da95-114">For hello VM that is created from a custom image of Windows Server 2016 or Windows Server 2012 R2, you must configure hello appropriate KMS client setup key for hello VM.</span></span>

<span data-ttu-id="1da95-115">Deze stap is niet van toepassing tooWindows 2012 of Windows 2008 R2.</span><span class="sxs-lookup"><span data-stu-id="1da95-115">This step does not apply tooWindows 2012 or Windows 2008 R2.</span></span> <span data-ttu-id="1da95-116">Hallo activering automatisering van virtuele Machine (AVMA) functie, wordt alleen ondersteund door Windows Server 2016 en Windows Server 2012 R2 wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="1da95-116">It uses hello Automation Virtual Machine Activation (AVMA) feature, which is supported only by Windows Server 2016 and Windows Server 2012 R2.</span></span>

1. <span data-ttu-id="1da95-117">Voer **slmgr.vbs/dlv** bij een opdrachtprompt met verhoogde bevoegdheden.</span><span class="sxs-lookup"><span data-stu-id="1da95-117">Run **slmgr.vbs /dlv** at an elevated command prompt.</span></span> <span data-ttu-id="1da95-118">Hallo beschrijvingswaarde in Hallo uitvoer controleren en Ga na of deze is gemaakt vanuit retail (RETAIL kanaal) of (VOLUME_KMSCLIENT) volume license-media:</span><span class="sxs-lookup"><span data-stu-id="1da95-118">Check hello Description value in hello output, and then determine whether it was created from retail (RETAIL channel) or volume (VOLUME_KMSCLIENT) license media:</span></span>
  
    ```
    cscript c:\windows\system32\slmgr.vbs /dlv
    ```

2. <span data-ttu-id="1da95-119">Als **slmgr.vbs/dlv** detailhandel, uitvoeren van opdrachten tooset Hallo na Hallo toont [Installatiecode voor KMS-client](https://technet.microsoft.com/library/jj612867%28v=ws.11%29.aspx?f=255&MSPPError=-2147217396) voor Hallo-versie van Windows Server wordt gebruikt en gedwongen tooretry activering:</span><span class="sxs-lookup"><span data-stu-id="1da95-119">If **slmgr.vbs /dlv** shows RETAIL channel, run hello following commands tooset hello [KMS client setup key](https://technet.microsoft.com/library/jj612867%28v=ws.11%29.aspx?f=255&MSPPError=-2147217396) for hello version of Windows Server being used, and force it tooretry activation:</span></span> 

    ```
    cscript c:\windows\system32\slmgr.vbs /ipk <KMS client setup key>

    cscript c:\windows\system32\slmgr.vbs /ato
     ```

    <span data-ttu-id="1da95-120">Bijvoorbeeld: voor Windows Server 2016 Datacenter, moet u Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="1da95-120">For example, for Windows Server 2016 Datacenter, you would run hello following command:</span></span>

    ```
    cscript c:\windows\system32\slmgr.vbs /ipk CB7KF-BWN84-R7R2Y-793K2-8XDDG
    ```

### <a name="step-2-verify-hello-connectivity-between-hello-vm-and-azure-kms-service"></a><span data-ttu-id="1da95-121">Stap 2 Controleer Hallo de verbinding tussen Hallo VM en Azure KMS-service</span><span class="sxs-lookup"><span data-stu-id="1da95-121">Step 2 Verify hello connectivity between hello VM and Azure KMS service</span></span>

1. <span data-ttu-id="1da95-122">Downloaden en uitpakken van Hallo [psping om](http:/technet.microsoft.com/en-us/sysinternals/jj729731.aspx) hulpprogramma tooa lokale map in Hallo virtuele machine die niet worden geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="1da95-122">Download and extract hello [Psping](http:/technet.microsoft.com/en-us/sysinternals/jj729731.aspx) tool tooa local folder in hello VM that does not activate.</span></span> 

2. <span data-ttu-id="1da95-123">Ga tooStart, zoeken op Windows PowerShell, met de rechtermuisknop op Windows PowerShell en selecteer als administrator uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="1da95-123">Go tooStart, search on Windows PowerShell, right-click Windows PowerShell, and then select Run as administrator.</span></span>

3. <span data-ttu-id="1da95-124">Zorg ervoor dat de VM bevindt zich Hallo toouse Hallo juiste Azure KMS-server geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="1da95-124">Make sure that hello VM is configured toouse hello correct Azure KMS server.</span></span> <span data-ttu-id="1da95-125">toodo dit de volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="1da95-125">toodo this, run the following command:</span></span>
  
    ```
    iex “$env:windir\system32\cscript.exe $env:windir\system32\slmgr.vbs /skms
    kms.core.windows.net:1688
    ```
    <span data-ttu-id="1da95-126">Hallo-opdracht moet worden geretourneerd: Key Management Service-computernaam tookms.core.windows.net:1688 is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="1da95-126">hello command should return: Key Management Service machine name set tookms.core.windows.net:1688 successfully.</span></span>

4. <span data-ttu-id="1da95-127">Controleer of met behulp van psping om dat er verbinding toohello KMS-server.</span><span class="sxs-lookup"><span data-stu-id="1da95-127">Verify by using Psping that you have connectivity toohello KMS server.</span></span> <span data-ttu-id="1da95-128">Toohello map waar u Hallo Pstools.zip downloaden uitgepakt switch en voer vervolgens de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="1da95-128">Switch toohello folder where you extracted hello Pstools.zip download, and then run hello following:</span></span>
  
    ```
    \psping.exe kms.core.windows.net:1688
    ```
  
  <span data-ttu-id="1da95-129">Zorg ervoor dat u ziet in Hallo seconde laatste regel van het Hallo-uitvoer wordt: verzonden = 4, ontvangen = 4, verloren = 0 (0% verlies).</span><span class="sxs-lookup"><span data-stu-id="1da95-129">In hello second-to-last line of hello output, make sure that you see: Sent = 4, Received = 4, Lost = 0 (0% loss).</span></span>

  <span data-ttu-id="1da95-130">Als verloren is groter dan 0 (nul), is Hallo VM heeft geen connectiviteit toohello KMS-server.</span><span class="sxs-lookup"><span data-stu-id="1da95-130">If Lost is greater than 0 (zero), hello VM does not have connectivity toohello KMS server.</span></span> <span data-ttu-id="1da95-131">In deze situatie is als hello VM bevindt zich in een virtueel netwerk en heeft een aangepaste DNS-server opgegeven, moet u ervoor zorgen dat DNS-server kunnen tooresolve kms.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="1da95-131">In this situation, if hello VM is in a virtual network and has a custom DNS server specified, you must make sure that DNS server is able tooresolve kms.core.windows.net.</span></span> <span data-ttu-id="1da95-132">Of wijzigen van Hallo DNS-server tooone die kms.core.windows.net is opgelost.</span><span class="sxs-lookup"><span data-stu-id="1da95-132">Or, change hello DNS server tooone that does resolve kms.core.windows.net.</span></span>

  <span data-ttu-id="1da95-133">U ziet dat als u alle DNS-servers uit een virtueel netwerk verwijderen, virtuele machines van Azure interne DNS-service gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1da95-133">Notice that if you remove all DNS servers from a virtual network, VMs use Azure’s internal DNS service.</span></span> <span data-ttu-id="1da95-134">Deze service kunt kms.core.windows.net oplossen.</span><span class="sxs-lookup"><span data-stu-id="1da95-134">This service can resolve kms.core.windows.net.</span></span>
  
<span data-ttu-id="1da95-135">Controleer ook dat of Hallo Gast de firewall is niet geconfigureerd op een wijze waarbij activation pogingen blokkeren.</span><span class="sxs-lookup"><span data-stu-id="1da95-135">Also verify that hello guest firewall has not been configured in a manner that would block activation attempts.</span></span>

5. <span data-ttu-id="1da95-136">Nadat u tookms.core.windows.net van geslaagde verbinding verifieert, Hallo volgen die opdrachtprompt van Windows PowerShell-opdracht worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="1da95-136">After you verify successful connectivity tookms.core.windows.net, run hello following command at that elevated Windows PowerShell prompt.</span></span> <span data-ttu-id="1da95-137">Met deze opdracht wordt activering geprobeerd meerdere keren.</span><span class="sxs-lookup"><span data-stu-id="1da95-137">This command tries activation multiple times.</span></span>

    ```
    1..12 | % { iex “$env:windir\system32\cscript.exe $env:windir\system32\slmgr.vbs /ato” ; start-sleep 5 }
    ```

<span data-ttu-id="1da95-138">Een geslaagde activering wordt informatie Hallo volgende strekking weergegeven:</span><span class="sxs-lookup"><span data-stu-id="1da95-138">A successful activation returns information that resembles hello following:</span></span>

<span data-ttu-id="1da95-139">**Windows(R), ServerDatacenter edition (12345678-1234-1234-1234-12345678) activeren... Product is geactiveerd.**</span><span class="sxs-lookup"><span data-stu-id="1da95-139">**Activating Windows(R), ServerDatacenter edition (12345678-1234-1234-1234-12345678) … Product activated successfully.**</span></span>

## <a name="faq"></a><span data-ttu-id="1da95-140">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="1da95-140">FAQ</span></span> 

### <a name="i-created-hello-windows-server-2016-from-azure-marketplace-do-i-need-tooconfigure-kms-key-for-activating-hello-windows-server-2016"></a><span data-ttu-id="1da95-141">Ik heb gemaakt Hallo Windows Server 2016 uit Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="1da95-141">I created hello Windows Server 2016 from Azure Marketplace.</span></span> <span data-ttu-id="1da95-142">Moet ik tooconfigure KMS-code voor het activeren van Windows Server 2016 Hallo?</span><span class="sxs-lookup"><span data-stu-id="1da95-142">Do I need tooconfigure KMS key for activating hello Windows Server 2016?</span></span> 
 
<span data-ttu-id="1da95-143">Nee.</span><span class="sxs-lookup"><span data-stu-id="1da95-143">No.</span></span> <span data-ttu-id="1da95-144">Hallo-installatiekopie in Azure Marketplace heeft Hallo juiste KMS-clientinstallatiecode al is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="1da95-144">hello image in Azure Marketplace has hello appropriate KMS client setup key already configured.</span></span> 

### <a name="does-windows-activation-work-hello-same-way-regardless-if-hello-vm-is-using-azure-hybrid-use-benefit-hub-or-not"></a><span data-ttu-id="1da95-145">Windows activation werk Hallo dezelfde manier ongeacht als Hallo VM van Azure hybride gebruik voordeel (HUB) of niet gebruikmaakt?</span><span class="sxs-lookup"><span data-stu-id="1da95-145">Does Windows activation work hello same way regardless if hello VM is using Azure Hybrid Use Benefit (HUB) or not?</span></span> 
 
<span data-ttu-id="1da95-146">Ja.</span><span class="sxs-lookup"><span data-stu-id="1da95-146">Yes.</span></span> 
 
### <a name="what-happens-if-windows-activation-period-expires"></a><span data-ttu-id="1da95-147">Wat gebeurt er als Windows-activering is verlopen?</span><span class="sxs-lookup"><span data-stu-id="1da95-147">What happens if Windows activation period expires?</span></span> 
 
<span data-ttu-id="1da95-148">Wanneer Hallo respijtperiode verlopen en Windows is nog niet geactiveerd, wordt Windows Server 2008 R2 en latere versies van Windows extra meldingen over het activeren van weergeven.</span><span class="sxs-lookup"><span data-stu-id="1da95-148">When hello grace period has expired and Windows is still not activated, Windows Server 2008 R2 and later versions of Windows will show additional notifications about activating.</span></span> <span data-ttu-id="1da95-149">Hallo bureaubladachtergrond blijft zwart en Windows Update wordt geïnstalleerd, beveiliging en alleen essentiële updates, maar niet optionele updates.</span><span class="sxs-lookup"><span data-stu-id="1da95-149">hello desktop wallpaper remains black, and Windows Update will install security and critical updates only, but not optional updates.</span></span> <span data-ttu-id="1da95-150">Zie Hallo meldingen sectie onderin Hallo Hallo [licentieverlening voorwaarden](http://technet.microsoft.com/en-us/library/ff793403.aspx) pagina.</span><span class="sxs-lookup"><span data-stu-id="1da95-150">See  hello Notifications section at hello bottom of hello [Licensing Conditions](http://technet.microsoft.com/en-us/library/ff793403.aspx) page.</span></span>   

## <a name="need-help-contact-support"></a><span data-ttu-id="1da95-151">Hulp nodig?</span><span class="sxs-lookup"><span data-stu-id="1da95-151">Need help?</span></span> <span data-ttu-id="1da95-152">Neem contact op met ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="1da95-152">Contact support.</span></span>
<span data-ttu-id="1da95-153">Als u nog hulp nodig hebt, [contact op met ondersteuning](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget uw probleem snel worden opgelost.</span><span class="sxs-lookup"><span data-stu-id="1da95-153">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your issue resolved quickly.</span></span>
