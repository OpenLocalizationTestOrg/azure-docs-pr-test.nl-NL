---
title: Problemen met Windows virtuele machine activering in Azure | Microsoft Docs
description: Biedt de stappen voor probleemoplossing voor het oplossen van problemen met Windows virtuele machine activation in Azure
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
ms.openlocfilehash: 77ef396e0bf75fab56bda2e76516b481d018c5b9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-azure-windows-virtual-machine-activation-problems"></a><span data-ttu-id="5bf42-103">Windows Azure virtuele machine activation problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="5bf42-103">Troubleshoot Azure Windows virtual machine activation problems</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="5bf42-104">Als u problemen hebt bij het activeren van Windows Azure virtuele machine (VM) die van een aangepaste installatiekopie wordt gemaakt, kunt u de informatie in dit document op te lossen.</span><span class="sxs-lookup"><span data-stu-id="5bf42-104">If you have trouble when activating Azure Windows virtual machine (VM) that is created from a custom image, you can use the information provided in this document to troubleshoot the issue.</span></span> 

## <a name="symptom"></a><span data-ttu-id="5bf42-105">Symptoom</span><span class="sxs-lookup"><span data-stu-id="5bf42-105">Symptom</span></span>

<span data-ttu-id="5bf42-106">Wanneer u probeert te activeren van een Windows Azure VM, u een foutbericht ontvangt bericht lijkt op het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="5bf42-106">When you try to activate an Azure Windows VM, you receive an error message resembles the following sample:</span></span>

<span data-ttu-id="5bf42-107">**Fout: 0xC004F074 die de LicensingService Software gerapporteerd dat de computer niet kan worden geactiveerd. Er is geen ManagementService KMS (Key) kan worden bereikt. Raadpleeg het logboek voor toepassingsgebeurtenissen voor meer informatie.**</span><span class="sxs-lookup"><span data-stu-id="5bf42-107">**Error: 0xC004F074 The Software LicensingService reported that the computer could not be activated. No Key ManagementService (KMS) could be contacted. Please see the Application Event Log for additional information.**</span></span>

## <a name="cause"></a><span data-ttu-id="5bf42-108">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="5bf42-108">Cause</span></span>
<span data-ttu-id="5bf42-109">In het algemeen optreden activeringsproblemen Azure VM als de virtuele machine van Windows is niet geconfigureerd met behulp van de desbetreffende Installatiecode voor KMS-client of de virtuele machine van Windows een probleem met de Azure-KMS-service (kms.core.windows.net, poort 1668 is).</span><span class="sxs-lookup"><span data-stu-id="5bf42-109">Generally, Azure VM activation issues occur if the Windows VM is not configured by using the appropriate KMS client setup key, or the Windows VM has a connectivity problem to the Azure KMS service (kms.core.windows.net, port 1668).</span></span> 

## <a name="solution"></a><span data-ttu-id="5bf42-110">Oplossing</span><span class="sxs-lookup"><span data-stu-id="5bf42-110">Solution</span></span>

>[!NOTE]
><span data-ttu-id="5bf42-111">Als u een site-naar-site-VPN en geforceerde tunneling, Zie [gebruik Azure aangepaste routes om in te schakelen van KMS-activering met geforceerde tunneling](http://blogs.msdn.com/b/mast/archive/2015/05/20/use-azure-custom-routes-to-enable-kms-activation-with-forced-tunneling.aspx).</span><span class="sxs-lookup"><span data-stu-id="5bf42-111">If you are using a site-to-site VPN and forced tunneling, see [Use Azure custom routes to enable KMS activation with forced tunneling](http://blogs.msdn.com/b/mast/archive/2015/05/20/use-azure-custom-routes-to-enable-kms-activation-with-forced-tunneling.aspx).</span></span> 
>
><span data-ttu-id="5bf42-112">Als u ExpressRoute gebruikt en u hebt een standaardroute gepubliceerd, Zie [Azure VM mislukken om te activeren via ExpressRoute](http://blogs.msdn.com/b/mast/archive/2015/12/01/azure-vm-may-fail-to-activate-over-expressroute.aspx).</span><span class="sxs-lookup"><span data-stu-id="5bf42-112">If you are using ExpressRoute and you have a default route published, see [Azure VM may fail to activate over ExpressRoute](http://blogs.msdn.com/b/mast/archive/2015/12/01/azure-vm-may-fail-to-activate-over-expressroute.aspx).</span></span>

### <a name="step-1-configure-the-appropriate-kms-client-setup-key-for-windows-server-2016-and-windows-server-2012-r2"></a><span data-ttu-id="5bf42-113">Stap 1 de desbetreffende Installatiecode voor KMS-client configureren (voor Windows Server 2016 en Windows Server 2012 R2)</span><span class="sxs-lookup"><span data-stu-id="5bf42-113">Step 1 Configure the appropriate KMS client setup key (for Windows Server 2016 and Windows Server 2012 R2)</span></span>

<span data-ttu-id="5bf42-114">Voor de virtuele machine die wordt gemaakt van een aangepaste installatiekopie van Windows Server 2016 of Windows Server 2012 R2, moet u de desbetreffende Installatiecode voor KMS-client configureren voor de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="5bf42-114">For the VM that is created from a custom image of Windows Server 2016 or Windows Server 2012 R2, you must configure the appropriate KMS client setup key for the VM.</span></span>

<span data-ttu-id="5bf42-115">Deze stap is niet van toepassing op Windows 2012 of Windows 2008 R2.</span><span class="sxs-lookup"><span data-stu-id="5bf42-115">This step does not apply to Windows 2012 or Windows 2008 R2.</span></span> <span data-ttu-id="5bf42-116">De functie activering automatisering van virtuele Machine (AVMA), waardoor wordt alleen ondersteund door Windows Server 2016 en Windows Server 2012 R2 wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="5bf42-116">It uses the Automation Virtual Machine Activation (AVMA) feature, which is supported only by Windows Server 2016 and Windows Server 2012 R2.</span></span>

1. <span data-ttu-id="5bf42-117">Voer **slmgr.vbs/dlv** bij een opdrachtprompt met verhoogde bevoegdheden.</span><span class="sxs-lookup"><span data-stu-id="5bf42-117">Run **slmgr.vbs /dlv** at an elevated command prompt.</span></span> <span data-ttu-id="5bf42-118">Controleer de waarde van de beschrijving in de uitvoer en Ga na of deze is gemaakt vanuit retail (RETAIL kanaal) of (VOLUME_KMSCLIENT) volume license-media:</span><span class="sxs-lookup"><span data-stu-id="5bf42-118">Check the Description value in the output, and then determine whether it was created from retail (RETAIL channel) or volume (VOLUME_KMSCLIENT) license media:</span></span>
  
    ```
    cscript c:\windows\system32\slmgr.vbs /dlv
    ```

2. <span data-ttu-id="5bf42-119">Als **slmgr.vbs/dlv** detailhandel, voer de volgende opdrachten om in te stellen toont de [Installatiecode voor KMS-client](https://technet.microsoft.com/library/jj612867%28v=ws.11%29.aspx?f=255&MSPPError=-2147217396) voor de versie van Windows Server wordt gebruikt en gedwongen proberen opnieuw te activeren:</span><span class="sxs-lookup"><span data-stu-id="5bf42-119">If **slmgr.vbs /dlv** shows RETAIL channel, run the following commands to set the [KMS client setup key](https://technet.microsoft.com/library/jj612867%28v=ws.11%29.aspx?f=255&MSPPError=-2147217396) for the version of Windows Server being used, and force it to retry activation:</span></span> 

    ```
    cscript c:\windows\system32\slmgr.vbs /ipk <KMS client setup key>

    cscript c:\windows\system32\slmgr.vbs /ato
     ```

    <span data-ttu-id="5bf42-120">Bijvoorbeeld: voor Windows Server 2016 Datacenter, moet u de volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="5bf42-120">For example, for Windows Server 2016 Datacenter, you would run the following command:</span></span>

    ```
    cscript c:\windows\system32\slmgr.vbs /ipk CB7KF-BWN84-R7R2Y-793K2-8XDDG
    ```

### <a name="step-2-verify-the-connectivity-between-the-vm-and-azure-kms-service"></a><span data-ttu-id="5bf42-121">Stap 2 de connectiviteit tussen de virtuele machine en Azure KMS-service controleren</span><span class="sxs-lookup"><span data-stu-id="5bf42-121">Step 2 Verify the connectivity between the VM and Azure KMS service</span></span>

1. <span data-ttu-id="5bf42-122">Downloaden en uitpakken van de [psping om](http:/technet.microsoft.com/en-us/sysinternals/jj729731.aspx) hulpprogramma naar een lokale map in de virtuele machine die niet worden geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="5bf42-122">Download and extract the [Psping](http:/technet.microsoft.com/en-us/sysinternals/jj729731.aspx) tool to a local folder in the VM that does not activate.</span></span> 

2. <span data-ttu-id="5bf42-123">Ga naar Start, zoeken op Windows PowerShell, met de rechtermuisknop op Windows PowerShell en selecteer als administrator uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="5bf42-123">Go to Start, search on Windows PowerShell, right-click Windows PowerShell, and then select Run as administrator.</span></span>

3. <span data-ttu-id="5bf42-124">Zorg ervoor dat de virtuele machine is geconfigureerd voor gebruik van de juiste Azure KMS-server.</span><span class="sxs-lookup"><span data-stu-id="5bf42-124">Make sure that the VM is configured to use the correct Azure KMS server.</span></span> <span data-ttu-id="5bf42-125">Voer hiertoe de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="5bf42-125">To do this, run the following command:</span></span>
  
    ```
    iex “$env:windir\system32\cscript.exe $env:windir\system32\slmgr.vbs /skms
    kms.core.windows.net:1688
    ```
    <span data-ttu-id="5bf42-126">De opdracht moet worden geretourneerd: naam van de Key Management Service-machine ingesteld op kms.core.windows.net:1688 is.</span><span class="sxs-lookup"><span data-stu-id="5bf42-126">The command should return: Key Management Service machine name set to kms.core.windows.net:1688 successfully.</span></span>

4. <span data-ttu-id="5bf42-127">Controleer of met behulp van psping om dat er een verbinding met de KMS-server.</span><span class="sxs-lookup"><span data-stu-id="5bf42-127">Verify by using Psping that you have connectivity to the KMS server.</span></span> <span data-ttu-id="5bf42-128">Ga naar de map waar u het downloaden van de Pstools.zip uitgepakt en voer het volgende:</span><span class="sxs-lookup"><span data-stu-id="5bf42-128">Switch to the folder where you extracted the Pstools.zip download, and then run the following:</span></span>
  
    ```
    \psping.exe kms.core.windows.net:1688
    ```
  
  <span data-ttu-id="5bf42-129">Zorg ervoor dat u ziet in de uitvoer van de laatste seconde coderegel: verzonden = 4, ontvangen = 4, verloren = 0 (0% verlies).</span><span class="sxs-lookup"><span data-stu-id="5bf42-129">In the second-to-last line of the output, make sure that you see: Sent = 4, Received = 4, Lost = 0 (0% loss).</span></span>

  <span data-ttu-id="5bf42-130">Als verloren is groter dan 0 (nul), is de virtuele machine heeft geen verbinding met de KMS-server.</span><span class="sxs-lookup"><span data-stu-id="5bf42-130">If Lost is greater than 0 (zero), the VM does not have connectivity to the KMS server.</span></span> <span data-ttu-id="5bf42-131">In deze situatie is als de virtuele machine zich in een virtueel netwerk en heeft een aangepaste DNS-server opgegeven, moet u ervoor zorgen dat DNS-server kunnen omzetten kms.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="5bf42-131">In this situation, if the VM is in a virtual network and has a custom DNS server specified, you must make sure that DNS server is able to resolve kms.core.windows.net.</span></span> <span data-ttu-id="5bf42-132">Of wijzig de DNS-server in een kms.core.windows.net is opgelost.</span><span class="sxs-lookup"><span data-stu-id="5bf42-132">Or, change the DNS server to one that does resolve kms.core.windows.net.</span></span>

  <span data-ttu-id="5bf42-133">U ziet dat als u alle DNS-servers uit een virtueel netwerk verwijderen, virtuele machines van Azure interne DNS-service gebruiken.</span><span class="sxs-lookup"><span data-stu-id="5bf42-133">Notice that if you remove all DNS servers from a virtual network, VMs use Azure’s internal DNS service.</span></span> <span data-ttu-id="5bf42-134">Deze service kunt kms.core.windows.net oplossen.</span><span class="sxs-lookup"><span data-stu-id="5bf42-134">This service can resolve kms.core.windows.net.</span></span>
  
<span data-ttu-id="5bf42-135">Controleer ook of de Gast-firewall is niet geconfigureerd op een wijze waarbij activation pogingen blokkeren.</span><span class="sxs-lookup"><span data-stu-id="5bf42-135">Also verify that the guest firewall has not been configured in a manner that would block activation attempts.</span></span>

5. <span data-ttu-id="5bf42-136">Nadat u geslaagde verbinding met kms.core.windows.net verifieert, voer de volgende opdracht op die Windows PowerShell-prompt met verhoogde bevoegdheden.</span><span class="sxs-lookup"><span data-stu-id="5bf42-136">After you verify successful connectivity to kms.core.windows.net, run the following command at that elevated Windows PowerShell prompt.</span></span> <span data-ttu-id="5bf42-137">Met deze opdracht wordt activering geprobeerd meerdere keren.</span><span class="sxs-lookup"><span data-stu-id="5bf42-137">This command tries activation multiple times.</span></span>

    ```
    1..12 | % { iex “$env:windir\system32\cscript.exe $env:windir\system32\slmgr.vbs /ato” ; start-sleep 5 }
    ```

<span data-ttu-id="5bf42-138">Een geslaagde activering wordt informatie de volgende strekking weergegeven:</span><span class="sxs-lookup"><span data-stu-id="5bf42-138">A successful activation returns information that resembles the following:</span></span>

<span data-ttu-id="5bf42-139">**Windows(R), ServerDatacenter edition (12345678-1234-1234-1234-12345678) activeren... Product is geactiveerd.**</span><span class="sxs-lookup"><span data-stu-id="5bf42-139">**Activating Windows(R), ServerDatacenter edition (12345678-1234-1234-1234-12345678) … Product activated successfully.**</span></span>

## <a name="faq"></a><span data-ttu-id="5bf42-140">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="5bf42-140">FAQ</span></span> 

### <a name="i-created-the-windows-server-2016-from-azure-marketplace-do-i-need-to-configure-kms-key-for-activating-the-windows-server-2016"></a><span data-ttu-id="5bf42-141">Ik heb de Windows Server 2016 gemaakt uit Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="5bf42-141">I created the Windows Server 2016 from Azure Marketplace.</span></span> <span data-ttu-id="5bf42-142">Heb ik nodig voor het configureren van de KMS-code voor het activeren van de Windows Server 2016?</span><span class="sxs-lookup"><span data-stu-id="5bf42-142">Do I need to configure KMS key for activating the Windows Server 2016?</span></span> 
 
<span data-ttu-id="5bf42-143">Nee.</span><span class="sxs-lookup"><span data-stu-id="5bf42-143">No.</span></span> <span data-ttu-id="5bf42-144">De afbeelding in Azure Marketplace heeft de juiste KMS clientinstallatiecode al is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="5bf42-144">The image in Azure Marketplace has the appropriate KMS client setup key already configured.</span></span> 

### <a name="does-windows-activation-work-the-same-way-regardless-if-the-vm-is-using-azure-hybrid-use-benefit-hub-or-not"></a><span data-ttu-id="5bf42-145">Windows-activering werkt hetzelfde ongeacht als de virtuele machine van Azure hybride gebruik voordeel (HUB) of niet gebruikmaakt?</span><span class="sxs-lookup"><span data-stu-id="5bf42-145">Does Windows activation work the same way regardless if the VM is using Azure Hybrid Use Benefit (HUB) or not?</span></span> 
 
<span data-ttu-id="5bf42-146">Ja.</span><span class="sxs-lookup"><span data-stu-id="5bf42-146">Yes.</span></span> 
 
### <a name="what-happens-if-windows-activation-period-expires"></a><span data-ttu-id="5bf42-147">Wat gebeurt er als Windows-activering is verlopen?</span><span class="sxs-lookup"><span data-stu-id="5bf42-147">What happens if Windows activation period expires?</span></span> 
 
<span data-ttu-id="5bf42-148">Wanneer de respijtperiode is verlopen en Windows is nog niet geactiveerd, wordt Windows Server 2008 R2 en latere versies van Windows extra meldingen over het activeren van weergeven.</span><span class="sxs-lookup"><span data-stu-id="5bf42-148">When the grace period has expired and Windows is still not activated, Windows Server 2008 R2 and later versions of Windows will show additional notifications about activating.</span></span> <span data-ttu-id="5bf42-149">De bureaubladachtergrond blijft zwart en Windows Update wordt geïnstalleerd, beveiliging en alleen essentiële updates, maar niet optionele updates.</span><span class="sxs-lookup"><span data-stu-id="5bf42-149">The desktop wallpaper remains black, and Windows Update will install security and critical updates only, but not optional updates.</span></span> <span data-ttu-id="5bf42-150">Zie de sectie meldingen aan de onderkant van de [licentieverlening voorwaarden](http://technet.microsoft.com/en-us/library/ff793403.aspx) pagina.</span><span class="sxs-lookup"><span data-stu-id="5bf42-150">See  the Notifications section at the bottom of the [Licensing Conditions](http://technet.microsoft.com/en-us/library/ff793403.aspx) page.</span></span>   

## <a name="need-help-contact-support"></a><span data-ttu-id="5bf42-151">Hulp nodig?</span><span class="sxs-lookup"><span data-stu-id="5bf42-151">Need help?</span></span> <span data-ttu-id="5bf42-152">Neem contact op met ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="5bf42-152">Contact support.</span></span>
<span data-ttu-id="5bf42-153">Als u nog hulp nodig hebt, [contact op met ondersteuning](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) ophalen van uw probleem snel worden opgelost.</span><span class="sxs-lookup"><span data-stu-id="5bf42-153">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span></span>