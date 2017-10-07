---
title: aaaReplicate Hyper-V-machines met PowerShell en Azure Resource Manager | Microsoft Docs
description: Hallo replicatie van Hyper-V-machines tooAzure automatiseren met behulp van PowerShell en Azure Resource Manager van Azure Site Recovery.
services: site-recovery
documentationcenter: 
author: bsiva
manager: abhiag
editor: 
ms.assetid: 05e0d76e-c3f5-4845-8052-094019b6d102
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/31/2017
ms.author: bsiva
ms.openlocfilehash: 4fb15ce2e9ad54f1dd6f54ff769eb912aa4b0272
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-between-on-premises-hyper-v-virtual-machines-and-azure-by-using-powershell-and-azure-resource-manager"></a><span data-ttu-id="151c7-103">On-premises Hyper-V virtuele machines en Azure repliceren met behulp van PowerShell en Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="151c7-103">Replicate between on-premises Hyper-V virtual machines and Azure by using PowerShell and Azure Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="151c7-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="151c7-104">Azure Portal</span></span>](site-recovery-hyper-v-site-to-azure.md)
> * [<span data-ttu-id="151c7-105">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="151c7-105">PowerShell - Resource Manager</span></span>](site-recovery-deploy-with-powershell-resource-manager.md)
> * [<span data-ttu-id="151c7-106">Klassieke portal</span><span class="sxs-lookup"><span data-stu-id="151c7-106">Classic Portal</span></span>](site-recovery-hyper-v-site-to-azure-classic.md)
>
>

## <a name="overview"></a><span data-ttu-id="151c7-107">Overzicht</span><span class="sxs-lookup"><span data-stu-id="151c7-107">Overview</span></span>
<span data-ttu-id="151c7-108">Azure Site Recovery draagt bij aan tooyour zakelijke continuïteit en noodherstel strategie door replicatie, failovers en herstel van virtuele machines in een aantal implementatiescenario's te organiseren.</span><span class="sxs-lookup"><span data-stu-id="151c7-108">Azure Site Recovery contributes tooyour business continuity and disaster recovery strategy by orchestrating replication, failover, and recovery of virtual machines in a number of deployment scenarios.</span></span> <span data-ttu-id="151c7-109">Zie voor een volledige lijst van implementatiescenario's voor Hallo [Azure Site Recovery-overzicht](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="151c7-109">For a full list of deployment scenarios, see hello [Azure Site Recovery overview](site-recovery-overview.md).</span></span>

<span data-ttu-id="151c7-110">Azure PowerShell is een module die cmdlets toomanage Azure via Windows PowerShell biedt.</span><span class="sxs-lookup"><span data-stu-id="151c7-110">Azure PowerShell is a module that provides cmdlets toomanage Azure through Windows PowerShell.</span></span> <span data-ttu-id="151c7-111">Samenwerking met twee typen modules: Hallo module profiel Azure of hello Azure Resource Manager-module.</span><span class="sxs-lookup"><span data-stu-id="151c7-111">It can work with two types of modules: hello Azure Profile module, or hello Azure Resource Manager module.</span></span>

<span data-ttu-id="151c7-112">Site Recovery PowerShell-cmdlets beschikbaar met Azure PowerShell voor Azure Resource Manager helpen u bij het beveiligen en herstellen van uw servers in Azure.</span><span class="sxs-lookup"><span data-stu-id="151c7-112">Site Recovery PowerShell cmdlets, available with Azure PowerShell for Azure Resource Manager, help you protect and recover your servers in Azure.</span></span>

<span data-ttu-id="151c7-113">Dit artikel wordt beschreven hoe Windows PowerShell, samen met Azure Resource Manager, toodeploy siteherstel tooconfigure toouse en server protection tooAzure stroomlijnen.</span><span class="sxs-lookup"><span data-stu-id="151c7-113">This article describes how toouse Windows PowerShell, together with Azure Resource Manager, toodeploy Site Recovery tooconfigure and orchestrate server protection tooAzure.</span></span> <span data-ttu-id="151c7-114">Hallo-voorbeeld gebruikt in dit artikel ziet u hoe tooprotect, failover en virtuele machines op een Hyper-V-host-tooAzure herstellen met behulp van Azure PowerShell met Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="151c7-114">hello example used in this article shows you how tooprotect, fail over, and recover virtual machines on a Hyper-V host tooAzure, by using Azure PowerShell with Azure Resource Manager.</span></span>

> [!NOTE]
> <span data-ttu-id="151c7-115">Hallo Site Recovery PowerShell-cmdlets op dit moment kunt u tooconfigure hello te volgen: één tooanother voor Virtual Machine Manager-site, een tooAzure Virtual Machine Manager-site en een tooAzure Hyper-V-site.</span><span class="sxs-lookup"><span data-stu-id="151c7-115">hello Site Recovery PowerShell cmdlets currently allow you tooconfigure hello following: one Virtual Machine Manager site tooanother, a Virtual Machine Manager site tooAzure, and a Hyper-V site tooAzure.</span></span>
>
>

<span data-ttu-id="151c7-116">U hoeft niet toobe een PowerShell-deskundige toouse in dit artikel, maar hoeft u toounderstand Hallo basisconcepten, zoals modules, cmdlets en sessies.</span><span class="sxs-lookup"><span data-stu-id="151c7-116">You don't need toobe a PowerShell expert toouse this article, but you do need toounderstand hello basic concepts, such as modules, cmdlets, and sessions.</span></span> <span data-ttu-id="151c7-117">Zie [Aan de slag met Windows PowerShell](http://technet.microsoft.com/library/hh857337.aspx) voor meer informatie over Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="151c7-117">For more information about Windows PowerShell, see [Getting Started with Windows PowerShell](http://technet.microsoft.com/library/hh857337.aspx).</span></span>

<span data-ttu-id="151c7-118">U kunt ook meer informatie over [Azure PowerShell gebruiken met Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="151c7-118">You can also read more about [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

> [!NOTE]
> <span data-ttu-id="151c7-119">Microsoft-partners die deel van Hallo Cloud Solution Provider (CSP) programma uitmaken kunnen configureren en beheren van de beveiliging van hun klanten servers tootheir klanten respectieve CSP abonnementen (tenant-abonnementen).</span><span class="sxs-lookup"><span data-stu-id="151c7-119">Microsoft partners that are part of hello Cloud Solution Provider (CSP) program can configure and manage protection of their customers' servers tootheir customers' respective CSP subscriptions (tenant subscriptions).</span></span>
>
>

## <a name="before-you-start"></a><span data-ttu-id="151c7-120">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="151c7-120">Before you start</span></span>
<span data-ttu-id="151c7-121">Zorg ervoor dat u deze vereisten hebt voldaan:</span><span class="sxs-lookup"><span data-stu-id="151c7-121">Make sure you have these prerequisites in place:</span></span>

* <span data-ttu-id="151c7-122">Een [Microsoft Azure](https://azure.microsoft.com/) account.</span><span class="sxs-lookup"><span data-stu-id="151c7-122">A [Microsoft Azure](https://azure.microsoft.com/) account.</span></span> <span data-ttu-id="151c7-123">U kunt beginnen met een [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="151c7-123">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="151c7-124">U kunt bovendien lezen over [prijzen van Azure Site Recovery Manager](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="151c7-124">In addition, you can read about [Azure Site Recovery Manager pricing](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
* <span data-ttu-id="151c7-125">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="151c7-125">Azure PowerShell 1.0.</span></span> <span data-ttu-id="151c7-126">Voor informatie over deze release en hoe tooinstall, Zie [Azure PowerShell 1.0.](https://azure.microsoft.com/)</span><span class="sxs-lookup"><span data-stu-id="151c7-126">For information about this release and how tooinstall it, see [Azure PowerShell 1.0.](https://azure.microsoft.com/)</span></span>
* <span data-ttu-id="151c7-127">Hallo [AzureRM.SiteRecovery](https://www.powershellgallery.com/packages/AzureRM.SiteRecovery/) en [AzureRM.RecoveryServices](https://www.powershellgallery.com/packages/AzureRM.RecoveryServices/) modules.</span><span class="sxs-lookup"><span data-stu-id="151c7-127">hello [AzureRM.SiteRecovery](https://www.powershellgallery.com/packages/AzureRM.SiteRecovery/) and [AzureRM.RecoveryServices](https://www.powershellgallery.com/packages/AzureRM.RecoveryServices/) modules.</span></span> <span data-ttu-id="151c7-128">Kunt u de nieuwste versies Hallo van deze modules krijgen via Hallo [PowerShell gallery](https://www.powershellgallery.com/)</span><span class="sxs-lookup"><span data-stu-id="151c7-128">You can get hello latest versions of these modules from hello [PowerShell gallery](https://www.powershellgallery.com/)</span></span>

<span data-ttu-id="151c7-129">Dit artikel wordt beschreven hoe toouse Azure Powershell met Azure Resource Manager tooconfigure en beveiliging van uw servers beheren.</span><span class="sxs-lookup"><span data-stu-id="151c7-129">This article illustrates how toouse Azure Powershell with Azure Resource Manager tooconfigure and manage protection of your servers.</span></span> <span data-ttu-id="151c7-130">Hallo-voorbeeld gebruikt in dit artikel ziet u hoe een virtuele machine worden uitgevoerd op een Hyper-V-host tooAzure tooprotect.</span><span class="sxs-lookup"><span data-stu-id="151c7-130">hello example used in this article shows you how tooprotect a virtual machine, running on a Hyper-V host, tooAzure.</span></span> <span data-ttu-id="151c7-131">Hallo volgende vereisten zijn specifiek toothis voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="151c7-131">hello following prerequisites are specific toothis example.</span></span> <span data-ttu-id="151c7-132">Verschillende scenario's voor Site Recovery, Raadpleeg voor een uitgebreidere set vereisten voor Hallo toohello documentatie die betrekking hebben toothat scenario.</span><span class="sxs-lookup"><span data-stu-id="151c7-132">For a more comprehensive set of requirements for hello various Site Recovery scenarios, refer toohello documentation pertaining toothat scenario.</span></span>

* <span data-ttu-id="151c7-133">Een Hyper-V-host waarop Windows Server 2012 R2 of Microsoft Hyper-V Server 2012 R2 met een of meer virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="151c7-133">A Hyper-V host running Windows Server 2012 R2 or Microsoft Hyper-V Server 2012 R2 containing one or more virtual machines.</span></span>
* <span data-ttu-id="151c7-134">Hyper-V-servers verbonden toohello Internet, rechtstreeks of via een proxy.</span><span class="sxs-lookup"><span data-stu-id="151c7-134">Hyper-V servers connected toohello Internet, either directly or through a proxy.</span></span>
* <span data-ttu-id="151c7-135">Hallo moet virtuele machines die u wilt dat tooprotect voldoen aan [vereisten voor virtuele Machine](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="151c7-135">hello virtual machines you want tooprotect should conform with [Virtual Machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

## <a name="step-1-sign-in-tooyour-azure-account"></a><span data-ttu-id="151c7-136">Stap 1: Registreren in tooyour Azure-account</span><span class="sxs-lookup"><span data-stu-id="151c7-136">Step 1: Sign in tooyour Azure account</span></span>
1. <span data-ttu-id="151c7-137">Open een PowerShell-console en voer deze opdracht toosign in tooyour Azure-account.</span><span class="sxs-lookup"><span data-stu-id="151c7-137">Open a PowerShell console and run this command toosign in tooyour Azure account.</span></span> <span data-ttu-id="151c7-138">Hallo-cmdlet wordt een webpagina waarop u om referenties voor uw account vraagt.</span><span class="sxs-lookup"><span data-stu-id="151c7-138">hello cmdlet brings up a web page that will prompt you for your account credentials.</span></span>

        Login-AzureRmAccount

    <span data-ttu-id="151c7-139">U kunt u ook referenties van uw account kan opnemen als een parameter toohello `Login-AzureRmAccount` cmdlet, met behulp van Hallo `-Credential` parameter.</span><span class="sxs-lookup"><span data-stu-id="151c7-139">Alternately, you could also include your account credentials as a parameter toohello `Login-AzureRmAccount` cmdlet, by using hello `-Credential` parameter.</span></span>

    <span data-ttu-id="151c7-140">Als u CSP partner werken namens een tenant, opgeven Hallo klant als een tenant met de naam van de primaire domeincontroller tenantID of tenant.</span><span class="sxs-lookup"><span data-stu-id="151c7-140">If you are CSP partner working on behalf of a tenant, specify hello customer as a tenant, by using their tenantID or tenant primary domain name.</span></span>

        Login-AzureRmAccount -Tenant "fabrikam.com"
2. <span data-ttu-id="151c7-141">Een account kan meerdere abonnementen hebben, dus moet u Hallo abonnement u toouse met Hallo-account wilt koppelen.</span><span class="sxs-lookup"><span data-stu-id="151c7-141">An account can have several subscriptions, so you should associate hello subscription you want toouse with hello account.</span></span>

        Select-AzureRmSubscription -SubscriptionName $SubscriptionName
3. <span data-ttu-id="151c7-142">Controleer of uw abonnement geregistreerde toouse hello Azure providers voor Recovery Services- en Site Recovery met behulp van de volgende opdrachten Hallo:</span><span class="sxs-lookup"><span data-stu-id="151c7-142">Verify that your subscription is registered toouse hello Azure providers for Recovery Services and Site Recovery, by using hello following commands:</span></span>

   * `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices`
   * `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`

   <span data-ttu-id="151c7-143">In de uitvoer van deze opdrachten, als Hallo Hallo **RegistrationState** te is ingesteld,**geregistreerde**, kunt u doorgaan tooStep 2.</span><span class="sxs-lookup"><span data-stu-id="151c7-143">In hello output of these commands, if hello **RegistrationState** is set too**Registered**, you can proceed tooStep 2.</span></span> <span data-ttu-id="151c7-144">Als dat niet het geval is, moet u ontbrekende provider Hallo registreren in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="151c7-144">If not, you should register hello missing provider in your subscription.</span></span>

   <span data-ttu-id="151c7-145">tooregister hello Azure-provider voor de Site Recovery en de Recovery Services, Hallo volgende opdrachten uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="151c7-145">tooregister hello Azure provider for Site Recovery and Recovery Services, run hello following commands:</span></span>

       Register-AzureRmResourceProvider -ProviderNamespace Microsoft.SiteRecovery
       Register-AzureRmResourceProvider -ProviderNamespace Microsoft.RecoveryServices

   <span data-ttu-id="151c7-146">Controleer of Hallo providers is geregistreerd met behulp van de volgende opdrachten Hallo: `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices` en `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`.</span><span class="sxs-lookup"><span data-stu-id="151c7-146">Verify that hello providers registered successfully by using hello following commands: `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices` and `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`.</span></span>

## <a name="step-2-set-up-hello-recovery-services-vault"></a><span data-ttu-id="151c7-147">Stap 2: Hallo die Recovery Services-kluis instellen</span><span class="sxs-lookup"><span data-stu-id="151c7-147">Step 2: Set up hello Recovery Services vault</span></span>
1. <span data-ttu-id="151c7-148">Maak een Azure Resource Manager-resourcegroep waarin u zult Hallo-kluis maken, of gebruik een bestaande resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="151c7-148">Create an Azure Resource Manager resource group in which you'll create hello vault, or use an existing resource group.</span></span> <span data-ttu-id="151c7-149">U kunt een nieuwe resourcegroep maken met behulp van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="151c7-149">You can create a new resource group by using hello following command:</span></span>

        New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Geo  

    <span data-ttu-id="151c7-150">Indien Hallo $ResourceGroupName variabele Hallo-naam van de resourcegroep Hallo bevat gewenste toocreate en Hallo $Geo variabele bevat hello Azure regio in de resourcegroep van welke toocreate hello (bijvoorbeeld ' Brazilië-Zuid').</span><span class="sxs-lookup"><span data-stu-id="151c7-150">where hello $ResourceGroupName variable contains hello name of hello resource group you want toocreate, and hello $Geo variable contains hello Azure region in which toocreate hello resource group (for example, "Brazil South").</span></span>

    <span data-ttu-id="151c7-151">U kunt een lijst met resourcegroepen in uw abonnement verkrijgen via Hallo `Get-AzureRmResourceGroup` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="151c7-151">You can obtain a list of resource groups in your subscription by using hello `Get-AzureRmResourceGroup` cmdlet.</span></span>
2. <span data-ttu-id="151c7-152">Maak een nieuwe Azure Recovery Services-kluis als volgt:</span><span class="sxs-lookup"><span data-stu-id="151c7-152">Create a new Azure Recovery Services vault as follows:</span></span>

        $vault = New-AzureRmRecoveryServicesVault -Name <string> -ResourceGroupName <string> -Location <string>

    <span data-ttu-id="151c7-153">U kunt een lijst met bestaande kluizen ophalen met behulp van Hallo `Get-AzureRmRecoveryServicesVault` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="151c7-153">You can retrieve a list of existing vaults by using hello `Get-AzureRmRecoveryServicesVault` cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="151c7-154">Als u tooperform bewerkingen op de Site Recovery-kluizen gemaakt met de klassieke portal Hallo of hello Azure Service Management PowerShell-module wenst, kunt u een lijst met dergelijke kluizen ophalen met behulp van Hallo `Get-AzureRmSiteRecoveryVault` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="151c7-154">If you wish tooperform operations on Site Recovery vaults created using hello classic portal or hello Azure Service Management PowerShell module, you can retrieve a list of such vaults by using hello `Get-AzureRmSiteRecoveryVault` cmdlet.</span></span> <span data-ttu-id="151c7-155">Maak een nieuwe Recovery Services-kluis voor alle nieuwe activiteiten.</span><span class="sxs-lookup"><span data-stu-id="151c7-155">You should create a new Recovery Services vault for all new operations.</span></span> <span data-ttu-id="151c7-156">Hallo Site Recovery kluizen die u eerder hebt gemaakt worden ondersteund, maar geen Hallo nieuwste functies.</span><span class="sxs-lookup"><span data-stu-id="151c7-156">hello Site Recovery vaults you've created earlier are supported, but don't have hello latest features.</span></span>
>
>

## <a name="step-3-set-hello-recovery-services-vault-context"></a><span data-ttu-id="151c7-157">Stap 3: Stel Hallo Recovery Services-kluis context</span><span class="sxs-lookup"><span data-stu-id="151c7-157">Step 3: Set hello Recovery Services vault context</span></span>
1. <span data-ttu-id="151c7-158">Hallo kluis context door het uitvoeren van de volgende opdracht Hallo instellen:</span><span class="sxs-lookup"><span data-stu-id="151c7-158">Set hello vault context by running hello following command:</span></span>

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-create-a-hyper-v-site-and-generate-a-new-vault-registration-key-for-hello-site"></a><span data-ttu-id="151c7-159">Stap 4: Een Hyper-V-site maken en een nieuwe kluisregistratiesleutel voor Hallo site genereren.</span><span class="sxs-lookup"><span data-stu-id="151c7-159">Step 4: Create a Hyper-V site and generate a new vault registration key for hello site.</span></span>
1. <span data-ttu-id="151c7-160">Maak een nieuwe Hyper-V-site als volgt:</span><span class="sxs-lookup"><span data-stu-id="151c7-160">Create a new Hyper-V site as follows:</span></span>

        $sitename = "MySite"                #Specify site friendly name
        New-AzureRmSiteRecoverySite -Name $sitename

    <span data-ttu-id="151c7-161">Deze cmdlet wordt een siteherstel taak toocreate Hallo site gestart en retourneert een taakobject Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="151c7-161">This cmdlet starts a Site Recovery job toocreate hello site, and returns a Site Recovery job object.</span></span> <span data-ttu-id="151c7-162">Wachten op Hallo taak toocomplete en controleer of deze Hallo-taak is voltooid.</span><span class="sxs-lookup"><span data-stu-id="151c7-162">Wait for hello job toocomplete and verify that hello job completed successfully.</span></span>

    <span data-ttu-id="151c7-163">U kunt Hallo-taakobject worden opgehaald en Hallo huidige status van taak hello, waardoor controleren met behulp van de cmdlet Get-AzureRmSiteRecoveryJob Hallo.</span><span class="sxs-lookup"><span data-stu-id="151c7-163">You can retrieve hello job object, and thereby check hello current status of hello job, by using hello Get-AzureRmSiteRecoveryJob cmdlet.</span></span>
2. <span data-ttu-id="151c7-164">Genereren en download een registratiesleutel voor Hallo-site, als volgt:</span><span class="sxs-lookup"><span data-stu-id="151c7-164">Generate and download a registration key for hello site, as follows:</span></span>

        $SiteIdentifier = Get-AzureRmSiteRecoverySite -Name $sitename | Select -ExpandProperty SiteIdentifier
        Get-AzureRmRecoveryServicesVaultSettingsFile -Vault $vault -SiteIdentifier $SiteIdentifier -SiteFriendlyName $sitename -Path $Path

    <span data-ttu-id="151c7-165">Kopiëren Hallo gedownload sleutel toohello Hyper-V-host.</span><span class="sxs-lookup"><span data-stu-id="151c7-165">Copy hello downloaded key toohello Hyper-V host.</span></span> <span data-ttu-id="151c7-166">U moet Hallo sleutel tooregister Hallo Hyper-V-host toohello site.</span><span class="sxs-lookup"><span data-stu-id="151c7-166">You need hello key tooregister hello Hyper-V host toohello site.</span></span>

## <a name="step-5-install-hello-azure-site-recovery-provider-and-azure-recovery-services-agent-on-your-hyper-v-host"></a><span data-ttu-id="151c7-167">Stap 5: Hello Azure Site Recovery provider en de Azure Recovery Services-Agent installeren op uw Hyper-V-host</span><span class="sxs-lookup"><span data-stu-id="151c7-167">Step 5: Install hello Azure Site Recovery provider and Azure Recovery Services Agent on your Hyper-V host</span></span>
1. <span data-ttu-id="151c7-168">Hallo installatieprogramma downloaden voor de meest recente versie Hallo van Hallo-provider van de [Microsoft](https://aka.ms/downloaddra).</span><span class="sxs-lookup"><span data-stu-id="151c7-168">Download hello installer for hello latest version of hello provider from [Microsoft](https://aka.ms/downloaddra).</span></span>
2. <span data-ttu-id="151c7-169">Voer Hallo installer op de Hyper-V-host en achter Hallo Hallo-installatie voortgezet toohello registratiestap.</span><span class="sxs-lookup"><span data-stu-id="151c7-169">Run hello installer on your Hyper-V host, and at hello end of hello installation continue toohello registration step.</span></span>
3. <span data-ttu-id="151c7-170">Geef desgevraagd Hallo site registratiecode en voltooid de registratie van Hallo Hyper-V-host toohello site gedownload.</span><span class="sxs-lookup"><span data-stu-id="151c7-170">When prompted, provide hello downloaded site registration key, and complete registration of hello Hyper-V host toohello site.</span></span>
4. <span data-ttu-id="151c7-171">Controleren dat die Hallo Hyper-V-host is geregistreerd toohello site met behulp van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="151c7-171">Verify that hello Hyper-V host is registered toohello site by using hello following command:</span></span>

        $server =  Get-AzureRmSiteRecoveryServer -FriendlyName $server-friendlyname

## <a name="step-6-create-a-replication-policy-and-associate-it-with-hello-protection-container"></a><span data-ttu-id="151c7-172">Stap 6: Een replicatiebeleid maken en deze koppelen aan de beveiligingscontainer Hallo</span><span class="sxs-lookup"><span data-stu-id="151c7-172">Step 6: Create a replication policy and associate it with hello protection container</span></span>
1. <span data-ttu-id="151c7-173">Maak een beleid voor wachtwoordreplicatie als volgt:</span><span class="sxs-lookup"><span data-stu-id="151c7-173">Create a replication policy as follows:</span></span>

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $Recoverypoints = 6                    #specify hello number of recovery points
        $storageaccountID = Get-AzureRmStorageAccount -Name "mystorea" -ResourceGroupName "MyRG" | Select -ExpandProperty Id

        $PolicyResult = New-AzureRmSiteRecoveryPolicy -Name $PolicyName -ReplicationProvider “HyperVReplicaAzure” -ReplicationFrequencyInSeconds $ReplicationFrequencyInSeconds  -RecoveryPoints $Recoverypoints -ApplicationConsistentSnapshotFrequencyInHours 1 -RecoveryAzureStorageAccountId $storageaccountID

    <span data-ttu-id="151c7-174">Selectievakje hello taak tooensure die Hallo replicatie beleid aanmaak slaagt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="151c7-174">Check hello returned job tooensure that hello replication policy creation succeeds.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="151c7-175">Hallo opgegeven opslagaccount moet zich in dezelfde Azure-regio als de Recovery Services-kluis Hallo en moet geo-replicatie is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="151c7-175">hello storage account specified should be in hello same Azure region as your Recovery Services vault, and should have geo-replication enabled.</span></span>
   >
   > * <span data-ttu-id="151c7-176">Als Hallo opgegeven Recovery storage-account van het type Azure Storage (klassiek is), beveiligde failover Hallo machines herstellen Hallo machine tooAzure IaaS (klassiek).</span><span class="sxs-lookup"><span data-stu-id="151c7-176">If hello specified Recovery storage account is of type Azure Storage (Classic), failover of hello protected machines recover hello machine tooAzure IaaS (Classic).</span></span>
   > * <span data-ttu-id="151c7-177">Als Hallo opgegeven Recovery storage-account is van het type Azure Storage (Azure Resource Manager), beveiligde failover Hallo machines herstellen Hallo machine tooAzure IaaS (Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="151c7-177">If hello specified Recovery storage account is of type Azure Storage (Azure Resource Manager), failover of hello protected machines recover hello machine tooAzure IaaS (Azure Resource Manager).</span></span>
   >
   >
2. <span data-ttu-id="151c7-178">Hallo beveiliging container bijbehorende toohello site, als volgt ophalen:</span><span class="sxs-lookup"><span data-stu-id="151c7-178">Get hello protection container corresponding toohello site, as follows:</span></span>

        $protectionContainer = Get-AzureRmSiteRecoveryProtectionContainer
3. <span data-ttu-id="151c7-179">Start Hallo koppeling van de beveiligingscontainer Hallo met replicatiebeleid hello, als volgt:</span><span class="sxs-lookup"><span data-stu-id="151c7-179">Start hello association of hello protection container with hello replication policy, as follows:</span></span>

     <span data-ttu-id="151c7-180">$Policy = get-AzureRmSiteRecoveryPolicy - FriendlyName $PolicyName $associationJob = Start AzureRmSiteRecoveryPolicyAssociationJob-beleid $Policy - PrimaryProtectionContainer $protectionContainer</span><span class="sxs-lookup"><span data-stu-id="151c7-180">$Policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $PolicyName   $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy $Policy -PrimaryProtectionContainer $protectionContainer</span></span>

   <span data-ttu-id="151c7-181">Wacht tot Hallo koppeling taak toocomplete en zorg ervoor dat het met succes voltooid.</span><span class="sxs-lookup"><span data-stu-id="151c7-181">Wait for hello association job toocomplete, and ensure that it completed successfully.</span></span>

## <a name="step-7-enable-protection-for-virtual-machines"></a><span data-ttu-id="151c7-182">Stap 7: Beveiliging voor virtuele machines inschakelen</span><span class="sxs-lookup"><span data-stu-id="151c7-182">Step 7: Enable protection for virtual machines</span></span>
1. <span data-ttu-id="151c7-183">Haal Hallo beveiliging entiteit bijbehorende toohello VM die u wilt dat tooprotect, als volgt:</span><span class="sxs-lookup"><span data-stu-id="151c7-183">Get hello protection entity corresponding toohello VM you want tooprotect, as follows:</span></span>

        $VMFriendlyName = "Fabrikam-app"                    #Name of hello VM
        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -ProtectionContainer $protectionContainer -FriendlyName $VMFriendlyName
2. <span data-ttu-id="151c7-184">Beginnen met het beveiligen van Hallo virtuele machine, als volgt:</span><span class="sxs-lookup"><span data-stu-id="151c7-184">Start protecting hello virtual machine, as follows:</span></span>

        $Ostype = "Windows"                                 # "Windows" or "Linux"
        $DRjob = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionEntity -Policy $Policy -Protection Enable -RecoveryAzureStorageAccountId $storageaccountID  -OS $OStype -OSDiskName $protectionEntity.Disks[0].Name

   > [!IMPORTANT]
   > <span data-ttu-id="151c7-185">Hallo opgegeven opslagaccount moet zich in dezelfde Azure-regio als de Recovery Services-kluis Hallo en moet geo-replicatie is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="151c7-185">hello storage account specified should be in hello same Azure region as your Recovery Services vault, and should have geo-replication enabled.</span></span>
   >
   > * <span data-ttu-id="151c7-186">Als Hallo opgegeven Recovery storage-account van het type Azure Storage (klassiek is), beveiligde failover Hallo machines herstellen Hallo machine tooAzure IaaS (klassiek).</span><span class="sxs-lookup"><span data-stu-id="151c7-186">If hello specified Recovery storage account is of type Azure Storage (Classic), failover of hello protected machines recover hello machine tooAzure IaaS (Classic).</span></span>
   > * <span data-ttu-id="151c7-187">Als Hallo opgegeven Recovery storage-account is van het type Azure Storage (Azure Resource Manager), beveiligde failover Hallo machines herstellen Hallo machine tooAzure IaaS (Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="151c7-187">If hello specified Recovery storage account is of type Azure Storage (Azure Resource Manager), failover of hello protected machines recover hello machine tooAzure IaaS (Azure Resource Manager).</span></span>
   >
   > <span data-ttu-id="151c7-188">Als Hallo VM die u beveiligt meer dan één schijf gekoppelde tooit bevat, besturingssysteemschijf Hallo opgeven met behulp van Hallo *OSDiskName* parameter.</span><span class="sxs-lookup"><span data-stu-id="151c7-188">If hello VM you are protecting has more than one disk attached tooit, specify hello operating system disk by using hello *OSDiskName* parameter.</span></span>
   >
   >
3. <span data-ttu-id="151c7-189">Wachten op Hallo virtuele machines tooreach een beveiligde status na de initiële replicatie Hallo.</span><span class="sxs-lookup"><span data-stu-id="151c7-189">Wait for hello virtual machines tooreach a protected state after hello initial replication.</span></span> <span data-ttu-id="151c7-190">Dit kan duren, afhankelijk van factoren zoals de hoeveelheid gegevens toobe gerepliceerd Hallo en beschikbare bandbreedte van de upstream-tooAzure Hallo.</span><span class="sxs-lookup"><span data-stu-id="151c7-190">This can take a while, depending on factors such as hello amount of data toobe replicated and hello available upstream bandwidth tooAzure.</span></span> <span data-ttu-id="151c7-191">Hallo taakstatus en StateDescription bijgewerkt als volgt bij Hallo VM een beveiligde status bereikt.</span><span class="sxs-lookup"><span data-stu-id="151c7-191">hello job State and StateDescription are updated as follows, upon hello VM reaching a protected state.</span></span>

        PS C:\> $DRjob = Get-AzureRmSiteRecoveryJob -Job $DRjob

        PS C:\> $DRjob | Select-Object -ExpandProperty State
        Succeeded

        PS C:\> $DRjob | Select-Object -ExpandProperty StateDescription
        Completed
4. <span data-ttu-id="151c7-192">Herstel-eigenschappen, zoals Hallo grootte VM-rol en hello Azure-netwerk tooattach Hallo van network interface-kaarten tooupon failover van virtuele machine bijwerken.</span><span class="sxs-lookup"><span data-stu-id="151c7-192">Update recovery properties, such as hello VM role size, and hello Azure network tooattach hello virtual machine's network interface cards tooupon failover.</span></span>

        PS C:\> $nw1 = Get-AzureRmVirtualNetwork -Name "FailoverNw" -ResourceGroupName "MyRG"

        PS C:\> $VMFriendlyName = "Fabrikam-App"

        PS C:\> $VM = Get-AzureRmSiteRecoveryVM -ProtectionContainer $protectionContainer -FriendlyName $VMFriendlyName

        PS C:\> $UpdateJob = Set-AzureRmSiteRecoveryVM -VirtualMachine $VM -PrimaryNic $VM.NicDetailsList[0].NicId -RecoveryNetworkId $nw1.Id -RecoveryNicSubnetName $nw1.Subnets[0].Name

        PS C:\> $UpdateJob = Get-AzureRmSiteRecoveryJob -Job $UpdateJob

        PS C:\> $UpdateJob

        Name             : b8a647e0-2cb9-40d1-84c4-d0169919e2c5
        ID               : /Subscriptions/a731825f-4bf2-4f81-a611-c331b272206e/resourceGroups/MyRG/providers/Microsoft.RecoveryServices/vault
                           s/MyVault/replicationJobs/b8a647e0-2cb9-40d1-84c4-d0169919e2c5
        Type             : Microsoft.RecoveryServices/vaults/replicationJobs
        JobType          : UpdateVmProperties
        DisplayName      : Update hello virtual machine
        ClientRequestId  : 805a22a3-be86-441c-9da8-f32685673112-2015-12-10 17:55:51Z-P
        State            : Succeeded
        StateDescription : Completed
        StartTime        : 10-12-2015 17:55:53 +00:00
        EndTime          : 10-12-2015 17:55:54 +00:00
        TargetObjectId   : 289682c6-c5e6-42dc-a1d2-5f9621f78ae6
        TargetObjectType : ProtectionEntity
        TargetObjectName : Fabrikam-App
        AllowedActions   : {Restart}
        Tasks            : {UpdateVmPropertiesTask}
        Errors           : {}



## <a name="step-8-run-a-test-failover"></a><span data-ttu-id="151c7-193">Stap 8: Een testfailover uitvoeren</span><span class="sxs-lookup"><span data-stu-id="151c7-193">Step 8: Run a test failover</span></span>
1. <span data-ttu-id="151c7-194">Een testtaak voor failover als volgt uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="151c7-194">Run a test failover job, as follows:</span></span>

        $nw = Get-AzureRmVirtualNetwork -Name "TestFailoverNw" -ResourceGroupName "MyRG" #Specify Azure vnet name and resource group

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -FriendlyName $VMFriendlyName -ProtectionContainer $protectionContainer

        $TFjob = Start-AzureRmSiteRecoveryTestFailoverJob -ProtectionEntity $protectionEntity -Direction PrimaryToRecovery -AzureVMNetworkId $nw.Id
2. <span data-ttu-id="151c7-195">Controleer of Hallo test die virtuele machine wordt gemaakt in Azure.</span><span class="sxs-lookup"><span data-stu-id="151c7-195">Verify that hello test VM is created in Azure.</span></span> <span data-ttu-id="151c7-196">(Hallo test failover-taak wordt onderbroken, na het maken van Hallo test virtuele machine in Azure.</span><span class="sxs-lookup"><span data-stu-id="151c7-196">(hello test failover job is suspended, after creating hello test VM in Azure.</span></span> <span data-ttu-id="151c7-197">Hallo-taak is voltooid door het opruimen van artefacten Hallo gemaakt bij het Hallo-taak hervatten, zoals geïllustreerd in de volgende stap Hallo.)</span><span class="sxs-lookup"><span data-stu-id="151c7-197">hello job completes by cleaning up hello created artefacts upon resuming hello job, as illustrated in hello next step.)</span></span>
3. <span data-ttu-id="151c7-198">Volledige Hallo failover, als volgt testen:</span><span class="sxs-lookup"><span data-stu-id="151c7-198">Complete hello test failover, as follows:</span></span>

        $TFjob = Resume-AzureRmSiteRecoveryJob -Job $TFjob

## <a name="next-steps"></a><span data-ttu-id="151c7-199">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="151c7-199">Next Steps</span></span>
<span data-ttu-id="151c7-200">[Lees meer](https://msdn.microsoft.com/library/azure/mt637930.aspx) over Azure Site Recovery met Azure Resource Manager PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="151c7-200">[Read more](https://msdn.microsoft.com/library/azure/mt637930.aspx) about Azure Site Recovery with Azure Resource Manager PowerShell cmdlets.</span></span>
