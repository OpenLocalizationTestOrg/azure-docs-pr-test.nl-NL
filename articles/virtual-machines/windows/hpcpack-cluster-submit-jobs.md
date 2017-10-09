---
title: aaaSubmit taken tooan HPC Pack-cluster in Azure | Microsoft Docs
description: Meer informatie over hoe tooset van een lokale computer toosubmit taken tooan HPC Pack cluster in Azure
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management,hpc-pack
ms.assetid: 78f6833c-4aa6-4b3e-be71-97201abb4721
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 10/14/2016
ms.author: danlep
ms.openlocfilehash: 2918cf633917d8730487152e6a5ddb863eb8bb5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="submit-hpc-jobs-from-an-on-premises-computer-tooan-hpc-pack-cluster-deployed-in-azure"></a><span data-ttu-id="d80a7-103">Verzenden van HPC-taken van een lokale computer tooan HPC Pack cluster geïmplementeerd in Azure</span><span class="sxs-lookup"><span data-stu-id="d80a7-103">Submit HPC jobs from an on-premises computer tooan HPC Pack cluster deployed in Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="d80a7-104">Configureren van een lokale client computer toosubmit taken tooa [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) cluster in Azure.</span><span class="sxs-lookup"><span data-stu-id="d80a7-104">Configure an on-premises client computer toosubmit jobs tooa [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) cluster in Azure.</span></span> <span data-ttu-id="d80a7-105">Dit artikel laat zien hoe tooset op een lokale computer client toosubmit taak tools via HTTPS toohello cluster in Azure.</span><span class="sxs-lookup"><span data-stu-id="d80a7-105">This article shows you how tooset up a local computer with client tools toosubmit job over HTTPS toohello cluster in Azure.</span></span> <span data-ttu-id="d80a7-106">Op deze manier kunnen verschillende cluster gebruikers taken tooa cloud-gebaseerde HPC Pack cluster kunnen worden verzonden, maar zonder toohello hoofdknooppunt VM rechtstreeks verbinding maken of openen van een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="d80a7-106">In this way, several cluster users can submit jobs tooa cloud-based HPC Pack cluster, but without connecting directly toohello head node VM or accessing an Azure subscription.</span></span>

![Verzenden van een taak tooa-cluster in Azure][jobsubmit]

## <a name="prerequisites"></a><span data-ttu-id="d80a7-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="d80a7-108">Prerequisites</span></span>
* <span data-ttu-id="d80a7-109">**HPC Pack hoofdknooppunt geïmplementeerd in een Azure VM** -het is raadzaam dat u hulpprogramma's, zoals een [snelstartsjabloon met de Azure](https://azure.microsoft.com/documentation/templates/) of een [Azure PowerShell-script](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) toodeploy Hallo hoofdknooppunt en cluster.</span><span class="sxs-lookup"><span data-stu-id="d80a7-109">**HPC Pack head node deployed in an Azure VM** - We recommend that you use automated tools such as an [Azure quickstart template](https://azure.microsoft.com/documentation/templates/) or an [Azure PowerShell script](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) toodeploy hello head node and cluster.</span></span> <span data-ttu-id="d80a7-110">U moet Hallo DNS-naam van het hoofdknooppunt Hallo en Hallo referenties van een Clusterbeheerder Hallo stappen in dit artikel uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="d80a7-110">You need hello DNS name of hello head node and hello credentials of a cluster administrator to complete hello steps in this article.</span></span>
* <span data-ttu-id="d80a7-111">**Clientcomputer** -moet u een Windows- of Windows Server-clientcomputer die HPC Pack client-hulpprogramma's kan worden uitgevoerd (Zie [systeemvereisten](https://technet.microsoft.com/library/dn535781.aspx)).</span><span class="sxs-lookup"><span data-stu-id="d80a7-111">**Client computer** - You need a Windows or Windows Server client computer that can run HPC Pack client utilities (see [system requirements](https://technet.microsoft.com/library/dn535781.aspx)).</span></span> <span data-ttu-id="d80a7-112">Als u alleen toouse Hallo HPC Pack web-portal of REST-API toosubmit taken wilt, kunt u elke clientcomputer van uw keuze.</span><span class="sxs-lookup"><span data-stu-id="d80a7-112">If you only want toouse hello HPC Pack web portal or REST API toosubmit jobs, you can use any client computer of your choice.</span></span>
* <span data-ttu-id="d80a7-113">**HPC Pack installatiemedia** -tooinstall Hallo HPC Pack client utilities, gratis Hallo-installatiepakket voor de nieuwste versie van HPC Pack (HPC Pack 2012 R2) is beschikbaar via de [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024).</span><span class="sxs-lookup"><span data-stu-id="d80a7-113">**HPC Pack installation media** - tooinstall hello HPC Pack client utilities, hello free installation package for the latest version of HPC Pack (HPC Pack 2012 R2) is available from the [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024).</span></span> <span data-ttu-id="d80a7-114">Zorg ervoor dat u Hallo downloaden dezelfde versie van HPC Pack die is geïnstalleerd op Hallo hoofdknooppunt VM.</span><span class="sxs-lookup"><span data-stu-id="d80a7-114">Make sure that you download hello same version of HPC Pack that is installed on hello head node VM.</span></span>

## <a name="step-1-install-and-configure-hello-web-components-on-hello-head-node"></a><span data-ttu-id="d80a7-115">Stap 1: Installeren en configureren van Hallo webonderdelen op Hallo hoofdknooppunt</span><span class="sxs-lookup"><span data-stu-id="d80a7-115">Step 1: Install and configure hello web components on hello head node</span></span>
<span data-ttu-id="d80a7-116">tooenable een REST-interface toosubmit taken toohello cluster via HTTPS, zorg ervoor dat Hallo HPC Pack webonderdelen zijn geconfigureerd op Hallo HPC Pack hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="d80a7-116">tooenable a REST interface toosubmit jobs toohello cluster over HTTPS, ensure that hello HPC Pack web components are configured on hello HPC Pack head node.</span></span> <span data-ttu-id="d80a7-117">Als ze niet zijn geïnstalleerd, moet u eerst Hallo webonderdelen installeren door het Hallo HpcWebComponents.msi-installatiebestand uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="d80a7-117">If they aren't already installed, first install hello web components by running hello HpcWebComponents.msi installation file.</span></span> <span data-ttu-id="d80a7-118">Configureer vervolgens Hallo onderdelen Hallo HPC PowerShell-script uit te voeren **Set HPCWebComponents.ps1**.</span><span class="sxs-lookup"><span data-stu-id="d80a7-118">Then, configure hello components by running hello HPC PowerShell script **Set-HPCWebComponents.ps1**.</span></span>

<span data-ttu-id="d80a7-119">Zie voor gedetailleerde procedures [installeren Hallo Microsoft HPC Pack webcomponenten](http://technet.microsoft.com/library/hh314627.aspx).</span><span class="sxs-lookup"><span data-stu-id="d80a7-119">For detailed procedures, see [Install hello Microsoft HPC Pack Web Components](http://technet.microsoft.com/library/hh314627.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="d80a7-120">Bepaalde Azure-snelstartsjablonen voor HPC Pack installeren en configureren van webonderdelen Hallo automatisch.</span><span class="sxs-lookup"><span data-stu-id="d80a7-120">Certain Azure quickstart templates for HPC Pack install and configure hello web components automatically.</span></span> <span data-ttu-id="d80a7-121">Als u Hallo [HPC Pack IaaS-implementatiescript](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) toocreate Hallo cluster, u kunt eventueel installeren en configureren van webonderdelen Hallo als onderdeel van Hallo-implementatie.</span><span class="sxs-lookup"><span data-stu-id="d80a7-121">If you use hello [HPC Pack IaaS deployment script](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) toocreate hello cluster, you can optionally install and configure hello web components as part of hello deployment.</span></span>
> 
> 

<span data-ttu-id="d80a7-122">**tooinstall hello webonderdelen**</span><span class="sxs-lookup"><span data-stu-id="d80a7-122">**tooinstall hello web components**</span></span>

1. <span data-ttu-id="d80a7-123">Verbinding toohello hoofdknooppunt VM via Hallo referenties van de Clusterbeheerder van een.</span><span class="sxs-lookup"><span data-stu-id="d80a7-123">Connect toohello head node VM by using hello credentials of a cluster administrator.</span></span>
2. <span data-ttu-id="d80a7-124">Uitvoeren van Hallo HPC Pack Setup, map, HpcWebComponents.msi op Hallo hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="d80a7-124">From hello HPC Pack Setup folder, run HpcWebComponents.msi on hello head node.</span></span>
3. <span data-ttu-id="d80a7-125">Volg de stappen Hallo in Hallo wizard tooinstall Hallo-webonderdelen</span><span class="sxs-lookup"><span data-stu-id="d80a7-125">Follow hello steps in hello wizard tooinstall hello web components</span></span>

<span data-ttu-id="d80a7-126">**tooconfigure hello webonderdelen**</span><span class="sxs-lookup"><span data-stu-id="d80a7-126">**tooconfigure hello web components**</span></span>

1. <span data-ttu-id="d80a7-127">Start op het hoofdknooppunt Hallo HPC PowerShell als beheerder.</span><span class="sxs-lookup"><span data-stu-id="d80a7-127">On hello head node, start HPC PowerShell as an administrator.</span></span>
2. <span data-ttu-id="d80a7-128">toochange directory toohello locatie van het Hallo-configuratiescript, type Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="d80a7-128">toochange directory toohello location of hello configuration script, type hello following command:</span></span>
   
    ```powershell
    cd $env:CCP_HOME\bin
    ```
3. <span data-ttu-id="d80a7-129">tooconfigure Hallo REST-interface en start Hallo HPC-webservice, type Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="d80a7-129">tooconfigure hello REST interface and start hello HPC Web Service, type hello following command:</span></span>
   
    ```powershell
    .\Set-HPCWebComponents.ps1 –Service REST –enable
    ```
4. <span data-ttu-id="d80a7-130">Wanneer na vragen aan gebruiker tooselect een certificaat kiezen Hallo certificaat die overeenkomt met openbare DNS-naam van het hoofdknooppunt Hallo toohello.</span><span class="sxs-lookup"><span data-stu-id="d80a7-130">When prompted tooselect a certificate, choose hello certificate that corresponds toohello public DNS name of hello head node.</span></span> <span data-ttu-id="d80a7-131">Bijvoorbeeld, als het implementeren van hoofdknooppunt Hallo VM die gebruikmaakt van Hallo klassieke implementatiemodel, Hallo certificaatnaam ziet als CN eruit =&lt;*HeadNodeDnsName*&gt;. cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="d80a7-131">For example, if you deploy hello head node VM using hello classic deployment model, hello certificate name looks like CN=&lt;*HeadNodeDnsName*&gt;.cloudapp.net.</span></span> <span data-ttu-id="d80a7-132">Als u Hallo Resource Manager-implementatiemodel, Hallo certificaatnaam ziet eruit als CN =&lt;*HeadNodeDnsName*&gt;.&lt; *regio*&gt;. cloudapp.azure.com.</span><span class="sxs-lookup"><span data-stu-id="d80a7-132">If you use hello Resource Manager deployment model, hello certificate name looks like CN=&lt;*HeadNodeDnsName*&gt;.&lt;*region*&gt;.cloudapp.azure.com.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="d80a7-133">U selecteert dit certificaat later wanneer u taken toohello hoofdknooppunt uit een on-premises computer indienen.</span><span class="sxs-lookup"><span data-stu-id="d80a7-133">You select this certificate later when you submit jobs toohello head node from an on-premises computer.</span></span> <span data-ttu-id="d80a7-134">Geen selecteren of een certificaat dat overeenkomt met de computernaam toohello van hoofdknooppunt in Active Directory-domein Hallo Hallo configureren (bijvoorbeeld CN =*MyHPCHeadNode.HpcAzure.local*).</span><span class="sxs-lookup"><span data-stu-id="d80a7-134">Don't select or configure a certificate that corresponds toohello computer name of hello head node in hello Active Directory domain (for example, CN=*MyHPCHeadNode.HpcAzure.local*).</span></span>
   > 
   > 
5. <span data-ttu-id="d80a7-135">Hallo webportal tooconfigure taak te verzenden, type Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="d80a7-135">tooconfigure hello web portal for job submission, type hello following command:</span></span>
   
    ```powershell
    .\Set-HPCWebComponents.ps1 –Service Portal -enable
    ```
6. <span data-ttu-id="d80a7-136">Nadat het Hallo-script is voltooid, stoppen en opnieuw opstarten Hallo HPC Job Scheduler-Service door Hallo volgende opdrachten te typen:</span><span class="sxs-lookup"><span data-stu-id="d80a7-136">After hello script completes, stop and restart hello HPC Job Scheduler Service by typing hello following commands:</span></span>
   
    ```powershell
    net stop hpcscheduler
    net start hpcscheduler
    ```

## <a name="step-2-install-hello-hpc-pack-client-utilities-on-an-on-premises-computer"></a><span data-ttu-id="d80a7-137">Stap 2: Hallo HPC Pack client hulpprogramma's installeren op een on-premises computer</span><span class="sxs-lookup"><span data-stu-id="d80a7-137">Step 2: Install hello HPC Pack client utilities on an on-premises computer</span></span>
<span data-ttu-id="d80a7-138">Als u tooinstall Hallo HPC Pack client hulpprogramma's op uw computer wilt, de HPC Pack setup-bestanden (volledige installatie) downloaden van Hallo [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024).</span><span class="sxs-lookup"><span data-stu-id="d80a7-138">If you want tooinstall hello HPC Pack client utilities on your computer, download the HPC Pack setup files (full installation) from hello [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024).</span></span> <span data-ttu-id="d80a7-139">Wanneer u Hallo installatie begint, selecteer de installatieoptie Hallo voor Hallo **HPC Pack client utilities**.</span><span class="sxs-lookup"><span data-stu-id="d80a7-139">When you begin hello installation, choose hello setup option for hello **HPC Pack client utilities**.</span></span>

<span data-ttu-id="d80a7-140">toouse hello HPC Pack clienthulpprogramma's toosubmit taken toohello hoofdknooppunt VM, u ook een certificaat van het hoofdknooppunt Hallo tooexport nodig hebt en op Hallo-clientcomputer installeren.</span><span class="sxs-lookup"><span data-stu-id="d80a7-140">toouse hello HPC Pack client tools toosubmit jobs toohello head node VM, you also need tooexport a certificate from hello head node and install it on hello client computer.</span></span> <span data-ttu-id="d80a7-141">Hallo-certificaat moet. CER-indeling.</span><span class="sxs-lookup"><span data-stu-id="d80a7-141">hello certificate must be in .CER format.</span></span>

<span data-ttu-id="d80a7-142">**tooexport hello certificaat van het hoofdknooppunt Hallo**</span><span class="sxs-lookup"><span data-stu-id="d80a7-142">**tooexport hello certificate from hello head node**</span></span>

1. <span data-ttu-id="d80a7-143">Toevoegen op het hoofdknooppunt hello, Hallo certificaten module tooa Microsoft Management Console voor Hallo lokale computeraccount.</span><span class="sxs-lookup"><span data-stu-id="d80a7-143">On hello head node, add hello Certificates snap-in tooa Microsoft Management Console for hello Local Computer account.</span></span> <span data-ttu-id="d80a7-144">Zie voor stappen tooadd Hallo-module [toevoegen Hallo module Certificaten tooan MMC](https://technet.microsoft.com/library/cc754431.aspx).</span><span class="sxs-lookup"><span data-stu-id="d80a7-144">For steps tooadd hello snap-in, see [Add hello Certificates Snap-in tooan MMC](https://technet.microsoft.com/library/cc754431.aspx).</span></span>
2. <span data-ttu-id="d80a7-145">Vouw in de consolestructuur Hallo **certificaten-lokale Computer** > **persoonlijke**, en klik vervolgens op **certificaten**.</span><span class="sxs-lookup"><span data-stu-id="d80a7-145">In hello console tree, expand **Certificates – Local Computer** > **Personal**, and then click **Certificates**.</span></span>
3. <span data-ttu-id="d80a7-146">Hallo-certificaat dat u hebt geconfigureerd voor Hallo HPC Pack webonderdelen in vinden [stap 1: installeren en configureren van Hallo webonderdelen op Hallo hoofdknooppunt](#step-1:-install-and-configure-the-web-components-on-the-head-node) (bijvoorbeeld CN =&lt;*HeadNodeDnsName* &gt;. cloudapp.net).</span><span class="sxs-lookup"><span data-stu-id="d80a7-146">Locate hello certificate that you configured for hello HPC Pack web components in [Step 1: Install and configure hello web components on hello head node](#step-1:-install-and-configure-the-web-components-on-the-head-node) (for example, CN=&lt;*HeadNodeDnsName*&gt;.cloudapp.net).</span></span>
4. <span data-ttu-id="d80a7-147">Met de rechtermuisknop op het Hallo-certificaat en klik op **alle taken** > **exporteren**.</span><span class="sxs-lookup"><span data-stu-id="d80a7-147">Right-click hello certificate, and click **All Tasks** > **Export**.</span></span>
5. <span data-ttu-id="d80a7-148">Klik in de Wizard Certificaat exporteren hello, **volgende**, en zorg ervoor dat **Nee, Hallo persoonlijke sleutel niet exporteren** is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="d80a7-148">In hello Certificate Export Wizard, click **Next**, and ensure that **No, do not export hello private key** is selected.</span></span>
6. <span data-ttu-id="d80a7-149">Volg Hallo resterende stappen van de wizard tooexport Hallo-certificaat in DER Hallo encoded binary X.509 (. De indeling van de CER).</span><span class="sxs-lookup"><span data-stu-id="d80a7-149">Follow hello remaining steps of hello wizard tooexport hello certificate in DER encoded binary X.509 (.CER) format.</span></span>

<span data-ttu-id="d80a7-150">**tooimport hello certificaat op de clientcomputer Hallo**</span><span class="sxs-lookup"><span data-stu-id="d80a7-150">**tooimport hello certificate on hello client computer**</span></span>

1. <span data-ttu-id="d80a7-151">Hallo-certificaat dat u hebt geëxporteerd uit Hallo hoofdknooppunt tooa map op de clientcomputer Hallo kopiëren.</span><span class="sxs-lookup"><span data-stu-id="d80a7-151">Copy hello certificate that you exported from hello head node tooa folder on hello client computer.</span></span>
2. <span data-ttu-id="d80a7-152">Klik op de clientcomputer Hallo certmgr.msc worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d80a7-152">On hello client computer, run certmgr.msc.</span></span>
3. <span data-ttu-id="d80a7-153">Vouw in de certificaatbeheerder **certificaten-huidige gebruiker** > **Trusted Root Certification Authorities**, met de rechtermuisknop op **certificaten**, en vervolgens Klik op **alle taken** > **importeren**.</span><span class="sxs-lookup"><span data-stu-id="d80a7-153">In Certificate Manager, expand **Certificates – Current user** > **Trusted Root Certification Authorities**, right-click **Certificates**, and then click **All Tasks** > **Import**.</span></span>
4. <span data-ttu-id="d80a7-154">Klik in de Wizard Certificaat importeren hello, **volgende** en volg Hallo stappen tooimport Hallo certificaat dat u hebt geëxporteerd uit Hallo hoofdknooppunt toohello Trusted Root Certification Authorities opslaan.</span><span class="sxs-lookup"><span data-stu-id="d80a7-154">In hello Certificate Import Wizard, click **Next** and follow hello steps tooimport hello certificate that you exported from hello head node toohello Trusted Root Certification Authorities store.</span></span>

> [!TIP]
> <span data-ttu-id="d80a7-155">U ziet een beveiligingswaarschuwing, omdat het Hallo-certificeringsinstantie op Hallo hoofdknooppunt wordt niet herkend door Hallo-clientcomputer.</span><span class="sxs-lookup"><span data-stu-id="d80a7-155">You might see a security warning, because hello certification authority on hello head node isn't recognized by hello client computer.</span></span> <span data-ttu-id="d80a7-156">Voor testdoeleinden kunt u deze waarschuwing en voltooid Hallo certificaat importeren te negeren.</span><span class="sxs-lookup"><span data-stu-id="d80a7-156">For testing purposes, you can ignore this warning and complete hello certificate import.</span></span>
> 
> 

## <a name="step-3-run-test-jobs-on-hello-cluster"></a><span data-ttu-id="d80a7-157">Stap 3: Voer testtaken op Hallo-cluster</span><span class="sxs-lookup"><span data-stu-id="d80a7-157">Step 3: Run test jobs on hello cluster</span></span>
<span data-ttu-id="d80a7-158">uw configuratie, probeer actieve taken op Hallo-cluster in Azure van Hallo tooverify lokale computer.</span><span class="sxs-lookup"><span data-stu-id="d80a7-158">tooverify your configuration, try running jobs on hello cluster in Azure from hello on-premises computer.</span></span> <span data-ttu-id="d80a7-159">U kunt bijvoorbeeld HPC Pack GUI-hulpprogramma's of de opdrachtregelopdrachten toosubmit taken toohello cluster gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d80a7-159">For example, you can use HPC Pack GUI tools or command-line commands toosubmit jobs toohello cluster.</span></span> <span data-ttu-id="d80a7-160">U kunt ook de taken van een web gebaseerde portal toosubmit gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d80a7-160">You can also use a web-based portal toosubmit jobs.</span></span>

<span data-ttu-id="d80a7-161">**toorun taak verzending van opdrachten op de clientcomputer Hallo**</span><span class="sxs-lookup"><span data-stu-id="d80a7-161">**toorun job submission commands on hello client computer**</span></span>

1. <span data-ttu-id="d80a7-162">Start een opdrachtprompt op een clientcomputer waarop Hallo HPC Pack client hulpprogramma's zijn geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="d80a7-162">On a client computer where hello HPC Pack client utilities are installed, start a Command Prompt.</span></span>
2. <span data-ttu-id="d80a7-163">Typ een voorbeeld van een opdracht.</span><span class="sxs-lookup"><span data-stu-id="d80a7-163">Type a sample command.</span></span> <span data-ttu-id="d80a7-164">Bijvoorbeeld toolist alle taken op het Hallo-cluster, typt u een opdracht vergelijkbare tooone te volgen, afhankelijk van de volledige DNS-naam van het hoofdknooppunt Hallo HALLO hallo:</span><span class="sxs-lookup"><span data-stu-id="d80a7-164">For example, toolist all jobs on hello cluster, type a command similar tooone of hello following, depending on hello full DNS name of hello head node:</span></span>
   
    ```command
    job list /scheduler:https://<HeadNodeDnsName>.cloudapp.net /all
    ```
   
    <span data-ttu-id="d80a7-165">of</span><span class="sxs-lookup"><span data-stu-id="d80a7-165">or</span></span>
   
    ```command
    job list /scheduler:https://<HeadNodeDnsName>.<region>.cloudapp.azure.com /all
    ```
   
   > [!TIP]
   > <span data-ttu-id="d80a7-166">Hallo volledige DNS-naam van hoofdknooppunt hello, niet Hallo IP-adres in Hallo scheduler URL gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d80a7-166">Use hello full DNS name of hello head node, not hello IP address, in hello scheduler URL.</span></span> <span data-ttu-id="d80a7-167">Als u Hallo IP-adres opgeeft, een fout lijkt te ' Hallo-servercertificaat tooeither moet een geldige keten van een vertrouwensrelatie of toobe geplaatst in het vertrouwde basisarchief Hallo. "</span><span class="sxs-lookup"><span data-stu-id="d80a7-167">If you specify hello IP address, an error appears similar too"hello server certificate needs tooeither have a valid chain of trust or toobe placed in hello trusted root store."</span></span>
   > 
   > 
3. <span data-ttu-id="d80a7-168">Wanneer u wordt gevraagd, typt u Hallo-gebruikersnaam (in de vorm Hallo &lt;DomainName&gt;\\&lt;gebruikersnaam&gt;) en het wachtwoord van HPC-Clusterbeheer hello of een ander cluster-gebruiker die u hebt geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="d80a7-168">When prompted, type hello user name (in hello form &lt;DomainName&gt;\\&lt;UserName&gt;) and password of hello HPC cluster administrator or another cluster user that you configured.</span></span> <span data-ttu-id="d80a7-169">U kunt toostore Hallo referenties lokaal voor meer taakbewerkingen uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="d80a7-169">You can choose toostore hello credentials locally for more job operations.</span></span>
   
    <span data-ttu-id="d80a7-170">Een lijst met taken wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d80a7-170">A list of jobs appears.</span></span>

<span data-ttu-id="d80a7-171">**toouse HPC Job Manager op de clientcomputer Hallo**</span><span class="sxs-lookup"><span data-stu-id="d80a7-171">**toouse HPC Job Manager on hello client computer**</span></span>

1. <span data-ttu-id="d80a7-172">Als u niet eerder domeinreferenties voor een cluster gebruiker opslaat bij het indienen van een taak, kunt u Hallo-referenties in Aanmeldingsgegevensbeheer toevoegen.</span><span class="sxs-lookup"><span data-stu-id="d80a7-172">If you didn't previously store domain credentials for a cluster user when submitting a job, you can add hello credentials in Credential Manager.</span></span>
   
    <span data-ttu-id="d80a7-173">a.</span><span class="sxs-lookup"><span data-stu-id="d80a7-173">a.</span></span> <span data-ttu-id="d80a7-174">Start Referentiebeheer in het Configuratiescherm op Hallo-clientcomputer.</span><span class="sxs-lookup"><span data-stu-id="d80a7-174">In Control Panel on hello client computer, start Credential Manager.</span></span>
   
    <span data-ttu-id="d80a7-175">b.</span><span class="sxs-lookup"><span data-stu-id="d80a7-175">b.</span></span> <span data-ttu-id="d80a7-176">Klik op **Windows-referenties** > **toevoegen van een algemene referentie**.</span><span class="sxs-lookup"><span data-stu-id="d80a7-176">Click **Windows Credentials** > **Add a generic credential**.</span></span>
   
    <span data-ttu-id="d80a7-177">c.</span><span class="sxs-lookup"><span data-stu-id="d80a7-177">c.</span></span> <span data-ttu-id="d80a7-178">Hallo internetadres opgeven (bijvoorbeeld https://&lt;HeadNodeDnsName&gt;.cloudapp.net/HpcScheduler of https://&lt;HeadNodeDnsName&gt;.&lt; regio&gt;.cloudapp.azure.com/HpcScheduler), en de gebruikersnaam hello (&lt;DomainName&gt;\\&lt;gebruikersnaam&gt;) en het wachtwoord van de Clusterbeheerder hello of een ander cluster-gebruiker die u hebt geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="d80a7-178">Specify hello Internet address (for example, https://&lt;HeadNodeDnsName&gt;.cloudapp.net/HpcScheduler or https://&lt;HeadNodeDnsName&gt;.&lt;region&gt;.cloudapp.azure.com/HpcScheduler), and hello user name (&lt;DomainName&gt;\\&lt;UserName&gt;) and password of hello cluster administrator or another cluster user that you configured.</span></span>
2. <span data-ttu-id="d80a7-179">Start op de clientcomputer Hallo HPC Job Manager.</span><span class="sxs-lookup"><span data-stu-id="d80a7-179">On hello client computer, start HPC Job Manager.</span></span>
3. <span data-ttu-id="d80a7-180">In Hallo **hoofdknooppunt selecteren** dialoogvenster, type Hallo URL toohello hoofdknooppunt in Azure (bijvoorbeeld https://&lt;HeadNodeDnsName&gt;. cloudapp.net of https://&lt;HeadNodeDnsName&gt;. &lt;regio&gt;. cloudapp.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d80a7-180">In hello **Select Head Node** dialog box, type hello URL toohello head node in Azure (for example, https://&lt;HeadNodeDnsName&gt;.cloudapp.net or https://&lt;HeadNodeDnsName&gt;.&lt;region&gt;.cloudapp.azure.com).</span></span>
   
    <span data-ttu-id="d80a7-181">HPC Job Manager wordt geopend en ziet u een lijst met taken op Hallo hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="d80a7-181">HPC Job Manager opens and shows a list of jobs on hello head node.</span></span>

<span data-ttu-id="d80a7-182">**Hallo-webportal toouse uitgevoerd op het hoofdknooppunt Hallo**</span><span class="sxs-lookup"><span data-stu-id="d80a7-182">**toouse hello web portal running on hello head node**</span></span>

1. <span data-ttu-id="d80a7-183">Start een webbrowser op Hallo-clientcomputer en voer een van de volgende adressen, afhankelijk van de volledige DNS-naam van het hoofdknooppunt Hallo HALLO hallo:</span><span class="sxs-lookup"><span data-stu-id="d80a7-183">Start a web browser on hello client computer, and enter one of hello following addresses, depending on hello full DNS name of hello head node:</span></span>
   
    ```
    https://<HeadNodeDnsName>.cloudapp.net/HpcPortal
    ```
   
    <span data-ttu-id="d80a7-184">of</span><span class="sxs-lookup"><span data-stu-id="d80a7-184">or</span></span>
   
    ```
    https://<HeadNodeDnsName>.<region>.cloudapp.azure.com/HpcPortal
    ```
2. <span data-ttu-id="d80a7-185">Typ de domeinreferenties Hallo van Hallo HPC-Clusterbeheer in Hallo beveiliging in het dialoogvenster dat wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d80a7-185">In hello security dialog box that appears, type hello domain credentials of hello HPC cluster administrator.</span></span> <span data-ttu-id="d80a7-186">(U kunt ook andere cluster gebruikers toevoegen in verschillende rollen.</span><span class="sxs-lookup"><span data-stu-id="d80a7-186">(You can also add other cluster users in different roles.</span></span> <span data-ttu-id="d80a7-187">Zie [het beheren van gebruikers van de Cluster](https://technet.microsoft.com/library/ff919335.aspx).)</span><span class="sxs-lookup"><span data-stu-id="d80a7-187">See [Managing Cluster Users](https://technet.microsoft.com/library/ff919335.aspx).)</span></span>
   
    <span data-ttu-id="d80a7-188">Hallo-webportal wordt geopend toohello taak lijstweergave.</span><span class="sxs-lookup"><span data-stu-id="d80a7-188">hello web portal opens toohello job list view.</span></span>
3. <span data-ttu-id="d80a7-189">toosubmit een voorbeeld-taak die Hallo tekenreeks "Hallo wereld" uit Hallo-cluster retourneert, klik op **nieuwe taak** in de linkernavigatiebalk Hallo.</span><span class="sxs-lookup"><span data-stu-id="d80a7-189">toosubmit a sample job that returns hello string “Hello World” from hello cluster, click **New job** in hello left-hand navigation.</span></span>
4. <span data-ttu-id="d80a7-190">Op Hallo **nieuwe taak** pagina onder **van verzending van pagina's**, klikt u op **HelloWorld**.</span><span class="sxs-lookup"><span data-stu-id="d80a7-190">On hello **New Job** page, under **From submission pages**, click **HelloWorld**.</span></span> <span data-ttu-id="d80a7-191">Hallo taak verzendpagina wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d80a7-191">hello job submission page appears.</span></span>
5. <span data-ttu-id="d80a7-192">Klik op **indienen**.</span><span class="sxs-lookup"><span data-stu-id="d80a7-192">Click **Submit**.</span></span> <span data-ttu-id="d80a7-193">Als u wordt gevraagd, bieden de domeinreferenties Hallo van Hallo HPC-Clusterbeheer.</span><span class="sxs-lookup"><span data-stu-id="d80a7-193">If prompted, provide hello domain credentials of hello HPC cluster administrator.</span></span> <span data-ttu-id="d80a7-194">Hallo-taak wordt verzonden en Hallo taak-ID wordt weergegeven op Hallo **mijn taken** pagina.</span><span class="sxs-lookup"><span data-stu-id="d80a7-194">hello job is submitted, and hello job ID appears on hello **My Jobs** page.</span></span>
6. <span data-ttu-id="d80a7-195">tooview hello resultaten van het Hallo-taak die u hebt ingediend, klikt u op Hallo taak-ID en klik vervolgens op **taken weergeven** tooview Hallo opdrachtuitvoer (onder **uitvoer**).</span><span class="sxs-lookup"><span data-stu-id="d80a7-195">tooview hello results of hello job that you submitted, click hello job ID, and then click **View Tasks** tooview hello command output (under **Output**).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d80a7-196">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d80a7-196">Next steps</span></span>
* <span data-ttu-id="d80a7-197">U kunt ook taken toohello Azure cluster Hello verzenden [HPC Pack REST-API](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).</span><span class="sxs-lookup"><span data-stu-id="d80a7-197">You can also submit jobs toohello Azure cluster with hello [HPC Pack REST API](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).</span></span>
* <span data-ttu-id="d80a7-198">Als u toosubmit cluster taken van een Linux-client wilt, Zie Hallo Python voorbeeld in Hallo [HPC Pack 2012 R2 SDK en voorbeeldcode](https://www.microsoft.com/download/details.aspx?id=41633).</span><span class="sxs-lookup"><span data-stu-id="d80a7-198">If you want toosubmit cluster jobs from a Linux client, see hello Python sample in hello [HPC Pack 2012 R2 SDK and Sample Code](https://www.microsoft.com/download/details.aspx?id=41633).</span></span>

<!--Image references-->
[jobsubmit]: ./media/virtual-machines-windows-hpcpack-cluster-submit-jobs/jobsubmit.png
