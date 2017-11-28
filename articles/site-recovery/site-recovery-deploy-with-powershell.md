---
title: aaaReplicate Hyper-V-machines tooAzure in de klassieke portal Hallo met PowerShell | Microsoft Docs
description: Hallo replicatie van Hyper-V virtuele machines in VMM-clouds met Site Recovery en PowerShell in de klassieke portal Hallo automatiseren
services: site-recovery
documentationcenter: 
author: bsiva
manager: abhiag
editor: tysonn
ms.assetid: 9011f567-e0b4-4306-951a-b30da19f5db6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: bsiva
ms.openlocfilehash: d6847b46ac227209e6890de4ab603b23f827360f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-vms-tooazure-with-powershell-in-hello-classic-portal"></a><span data-ttu-id="ef09f-103">Hyper-V-machines tooAzure met PowerShell in de klassieke portal Hallo repliceren</span><span class="sxs-lookup"><span data-stu-id="ef09f-103">Replicate Hyper-V VMs tooAzure with PowerShell in hello classic portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ef09f-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="ef09f-104">Azure Portal</span></span>](site-recovery-vmm-to-azure.md)
> * [<span data-ttu-id="ef09f-105">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ef09f-105">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [<span data-ttu-id="ef09f-106">Klassieke portal</span><span class="sxs-lookup"><span data-stu-id="ef09f-106">Classic Portal</span></span>](site-recovery-vmm-to-azure-classic.md)
> * [<span data-ttu-id="ef09f-107">PowerShell - Klassiek</span><span class="sxs-lookup"><span data-stu-id="ef09f-107">PowerShell - Classic</span></span>](site-recovery-deploy-with-powershell.md)
>
>

## <a name="overview"></a><span data-ttu-id="ef09f-108">Overzicht</span><span class="sxs-lookup"><span data-stu-id="ef09f-108">Overview</span></span>
<span data-ttu-id="ef09f-109">Azure Site Recovery draagt bij aan tooyour zakelijke continuïteit en noodherstel (BCDR) strategie door replicatie, failovers en herstel van virtuele machines in een aantal implementatiescenario's te organiseren.</span><span class="sxs-lookup"><span data-stu-id="ef09f-109">Azure Site Recovery contributes tooyour business continuity and disaster recovery (BCDR) strategy by orchestrating replication, failover and recovery of virtual machines in a number of deployment scenarios.</span></span> <span data-ttu-id="ef09f-110">Voor een volledige lijst van de implementatie van scenario's Hallo Zie [Azure Site Recovery-overzicht](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ef09f-110">For a full list of deployment scenarios see hello [Azure Site Recovery overview](site-recovery-overview.md).</span></span>

<span data-ttu-id="ef09f-111">Dit artikel laat zien hoe toouse PowerShell tooautomate algemene taken moet u tooperform bij het instellen van Azure Site Recovery tooreplicate Hyper-V virtuele machines in System Center VMM-clouds tooAzure opslag.</span><span class="sxs-lookup"><span data-stu-id="ef09f-111">This article shows you how toouse PowerShell tooautomate common tasks you need tooperform when you set up Azure Site Recovery tooreplicate Hyper-V virtual machines in System Center VMM clouds tooAzure storage.</span></span>

<span data-ttu-id="ef09f-112">Hallo artikel bevat vereisten voor Hallo scenario en ziet u hoe tooset van Site Recovery-kluis installeert Azure Site Recovery Provider op de bronserver VMM Hallo Hallo, Hallo-server registreren in de kluis hello, Azure storage-account toevoegen, hello Azure installeren Recovery Services-agent op Hyper-V-hostservers Configureer beveiligingsinstellingen voor VMM-clouds die wordt toegepast tooall beveiligde virtuele machines, en schakel vervolgens de beveiliging voor deze virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="ef09f-112">hello article includes prerequisites for hello scenario, and shows you how tooset up a Site Recovery vault, install hello Azure Site Recovery Provider on hello source VMM server, register hello server in hello vault, add an Azure storage account, install hello Azure Recovery Services agent on Hyper-V host servers, configure protection settings for VMM clouds that will be applied tooall protected virtual machines, and then enable protection for those virtual machines.</span></span> <span data-ttu-id="ef09f-113">Voltooien door failover toomake testen Hallo controleren of dat alles werkt zoals verwacht.</span><span class="sxs-lookup"><span data-stu-id="ef09f-113">Finish up by testing hello failover toomake sure everything's working as expected.</span></span>

<span data-ttu-id="ef09f-114">Als u problemen bij het instellen van dit scenario, stel uw vragen op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="ef09f-114">If you run into problems setting up this scenario, post your questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

> [!NOTE]
> <span data-ttu-id="ef09f-115">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="ef09f-115">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="ef09f-116">In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="ef09f-116">This article covers using hello Classic deployment model.</span></span>
>
>

## <a name="before-you-start"></a><span data-ttu-id="ef09f-117">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="ef09f-117">Before you start</span></span>
<span data-ttu-id="ef09f-118">Zorg ervoor dat u deze vereisten hebt voldaan:</span><span class="sxs-lookup"><span data-stu-id="ef09f-118">Make sure you have these prerequisites in place:</span></span>

### <a name="azure-prerequisites"></a><span data-ttu-id="ef09f-119">Vereisten voor Azure</span><span class="sxs-lookup"><span data-stu-id="ef09f-119">Azure prerequisites</span></span>
* <span data-ttu-id="ef09f-120">U hebt een [Microsoft Azure](https://azure.microsoft.com/)-account nodig.</span><span class="sxs-lookup"><span data-stu-id="ef09f-120">You'll need a [Microsoft Azure](https://azure.microsoft.com/) account.</span></span> <span data-ttu-id="ef09f-121">U kunt beginnen met een [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ef09f-121">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="ef09f-122">U moet een Azure storage-account toostore gerepliceerde gegevens.</span><span class="sxs-lookup"><span data-stu-id="ef09f-122">You'll need an Azure storage account toostore replicated data.</span></span> <span data-ttu-id="ef09f-123">Hallo-account moet geo-replicatie is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="ef09f-123">hello account needs geo-replication enabled.</span></span> <span data-ttu-id="ef09f-124">Deze moet in dezelfde regio als de Azure Site Recovery-kluis Hallo Hallo en worden gekoppeld aan hetzelfde abonnement Hallo.</span><span class="sxs-lookup"><span data-stu-id="ef09f-124">It should be in hello same region as hello Azure Site Recovery vault and be associated with hello same subscription.</span></span> <span data-ttu-id="ef09f-125">[Meer informatie over Azure storage](../storage/common/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ef09f-125">[Learn more about Azure storage](../storage/common/storage-introduction.md).</span></span>
* <span data-ttu-id="ef09f-126">U moet zorgen dat virtuele machines die u wilt dat tooprotect voldoen aan toomake [vereisten van de virtuele machine van Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="ef09f-126">You'll need toomake sure that virtual machines you want tooprotect comply with [Azure virtual machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

### <a name="vmm-prerequisites"></a><span data-ttu-id="ef09f-127">VMM-vereisten</span><span class="sxs-lookup"><span data-stu-id="ef09f-127">VMM prerequisites</span></span>
* <span data-ttu-id="ef09f-128">U moet de VMM-server waarop System Center 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="ef09f-128">You'll need  VMM server running on System Center 2012 R2.</span></span>
* <span data-ttu-id="ef09f-129">U moet ten minste één cloud op Hallo gewenste tooprotect VMM-server.</span><span class="sxs-lookup"><span data-stu-id="ef09f-129">You'll need at least one cloud on hello VMM server you want tooprotect.</span></span> <span data-ttu-id="ef09f-130">Hallo cloud moet bevatten:</span><span class="sxs-lookup"><span data-stu-id="ef09f-130">hello cloud should contain:</span></span>
  * <span data-ttu-id="ef09f-131">Een of meer VMM-hostgroepen.</span><span class="sxs-lookup"><span data-stu-id="ef09f-131">One or more VMM host groups.</span></span>
  * <span data-ttu-id="ef09f-132">Een of meer Hyper-V-hostservers of -clusters in elke hostgroep.</span><span class="sxs-lookup"><span data-stu-id="ef09f-132">One or more Hyper-V host servers or clusters in each host group .</span></span>
  * <span data-ttu-id="ef09f-133">Een of meer virtuele machines op Hallo bron Hyper-V-server.</span><span class="sxs-lookup"><span data-stu-id="ef09f-133">One or more virtual machines on hello source Hyper-V server.</span></span>

### <a name="hyper-v-prerequisites"></a><span data-ttu-id="ef09f-134">Hyper-V-vereisten</span><span class="sxs-lookup"><span data-stu-id="ef09f-134">Hyper-V prerequisites</span></span>
* <span data-ttu-id="ef09f-135">Hallo Hyper-V-hostservers moeten ten minste draaien **Windows Server 2012** met Hyper-V-rol of **Microsoft Hyper-V Server 2012** en hebben Hallo nieuwste updates zijn geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="ef09f-135">hello host Hyper-V servers must be running at least **Windows Server 2012** with Hyper-V role or **Microsoft Hyper-V Server 2012** and have hello latest updates installed.</span></span>
* <span data-ttu-id="ef09f-136">Als u Hyper-V in een cluster uitvoert, wordt die clusterbroker niet automatisch gemaakt als u een cluster op basis van een statisch IP-adres hebt.</span><span class="sxs-lookup"><span data-stu-id="ef09f-136">If you're running Hyper-V in a cluster note that cluster broker isn't created automatically if you have a static IP address-based cluster.</span></span> <span data-ttu-id="ef09f-137">U moet tooconfigure hello clusterbroker handmatig.</span><span class="sxs-lookup"><span data-stu-id="ef09f-137">You'll need tooconfigure hello cluster broker manually.</span></span> <span data-ttu-id="ef09f-138">toodo dit door in Serverbeheer > Failoverclusterbeheer toohello cluster verbinding, klikt u op **functie configureren** en selecteer **Hyper-V Replica Broker** in Hallo **rol selecteren**scherm van de wizard maximale beschikbaarheid Hallo.</span><span class="sxs-lookup"><span data-stu-id="ef09f-138">toodo this, in Server Manager > Failover Cluster Manager, connect toohello cluster, click **Configure Role** and select **Hyper-V Replica Broker** in hello **Select Role** screen of hello High Availability wizard.</span></span>
* <span data-ttu-id="ef09f-139">Alle Hyper-V-hostserver of het cluster waarvoor u de toomanage beveiliging moet worden opgenomen in een VMM-cloud.</span><span class="sxs-lookup"><span data-stu-id="ef09f-139">Any Hyper-V host server or cluster for which you want toomanage protection must be included in a VMM cloud.</span></span>

### <a name="network-mapping-prerequisites"></a><span data-ttu-id="ef09f-140">Vereisten voor netwerktoewijzing</span><span class="sxs-lookup"><span data-stu-id="ef09f-140">Network mapping prerequisites</span></span>
<span data-ttu-id="ef09f-141">Als u virtuele machines in Azure koppelingen van Netwerktoewijzingen tussen VM-netwerken op Hallo bron-VMM-server beveiligen en gericht op Azure-netwerken tooenable Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="ef09f-141">When you protect virtual machines in Azure network mapping maps between VM networks on hello source VMM server and target Azure networks tooenable hello following:</span></span>

* <span data-ttu-id="ef09f-142">Alle machines die een failover op Hallo dezelfde netwerk verbinding kan maken van andere, ongeacht welk herstelplan ze tooeach.</span><span class="sxs-lookup"><span data-stu-id="ef09f-142">All machines which fail over on hello same network can connect tooeach other, irrespective of which recovery plan they are in.</span></span>
* <span data-ttu-id="ef09f-143">Als een netwerkgateway ingesteld op Hallo Azure-doelnetwerk is, kunnen virtuele machines verbinding tooother on-premises virtuele machines maken.</span><span class="sxs-lookup"><span data-stu-id="ef09f-143">If a network gateway is setup on hello target Azure network, virtual machines can connect tooother on-premises virtual machines.</span></span>
* <span data-ttu-id="ef09f-144">Als u niet configureert netwerk alleen virtuele machines met failover in Hallo dezelfde toewijzing herstelplan kunnen tooconnect tooeach andere worden na failover tooAzure.</span><span class="sxs-lookup"><span data-stu-id="ef09f-144">If you don’t configure network mapping only virtual machines that fail over in hello same recovery plan will be able tooconnect tooeach other after failover tooAzure.</span></span>

<span data-ttu-id="ef09f-145">Als u wilt dat de netwerktoewijzing toodeploy moet u de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="ef09f-145">If you want toodeploy network mapping you'll need hello following:</span></span>

* <span data-ttu-id="ef09f-146">Hallo virtuele machines die u wilt dat tooprotect op Hallo bron-VMM-server moet zijn verbonden tooa VM-netwerk.</span><span class="sxs-lookup"><span data-stu-id="ef09f-146">hello virtual machines you want tooprotect on hello source VMM server should be connected tooa VM network.</span></span> <span data-ttu-id="ef09f-147">Dit netwerk moet gekoppelde tooa logisch netwerk dat is gekoppeld aan Hallo cloud.</span><span class="sxs-lookup"><span data-stu-id="ef09f-147">That network should be linked tooa logical network that is associated with hello cloud.</span></span>
* <span data-ttu-id="ef09f-148">Een Azure-netwerk toowhich gerepliceerde virtuele machines verbinding kunnen maken na een failover.</span><span class="sxs-lookup"><span data-stu-id="ef09f-148">An Azure network toowhich replicated virtual machines can connect after failover.</span></span> <span data-ttu-id="ef09f-149">U selecteert dit netwerk op Hallo moment van failover.</span><span class="sxs-lookup"><span data-stu-id="ef09f-149">You'll select this network at hello time of failover.</span></span> <span data-ttu-id="ef09f-150">Hallo-netwerk moet zich in Hallo dezelfde regio bevinden als uw Azure Site Recovery-abonnement.</span><span class="sxs-lookup"><span data-stu-id="ef09f-150">hello network should be in hello same region as your Azure Site Recovery subscription.</span></span>

### <a name="powershell-prerequisites"></a><span data-ttu-id="ef09f-151">PowerShell-vereisten</span><span class="sxs-lookup"><span data-stu-id="ef09f-151">PowerShell prerequisites</span></span>
<span data-ttu-id="ef09f-152">Zorg ervoor dat u Azure PowerShell gereed toogo hebt.</span><span class="sxs-lookup"><span data-stu-id="ef09f-152">Make sure you have Azure PowerShell ready toogo.</span></span> <span data-ttu-id="ef09f-153">Als u al van PowerShell gebruikmaakt, moet u tooupgrade tooversion 0.8.10 of hoger.</span><span class="sxs-lookup"><span data-stu-id="ef09f-153">If you are already using PowerShell, you'll need tooupgrade tooversion 0.8.10 or later.</span></span> <span data-ttu-id="ef09f-154">Zie voor meer informatie over het instellen van PowerShell [hoe tooinstall en configureren van Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="ef09f-154">For information about setting up PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="ef09f-155">Zodra u hebt ingesteld en geconfigureerd PowerShell, kunt u alle beschikbare Hallo-cmdlets voor Hallo service weergeven [hier](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ef09f-155">Once you have set up and configured PowerShell, you can view all of hello available cmdlets for hello service [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="ef09f-156">Zie toolearn over tips waarmee u Hallo-cmdlets, zoals hoe parameterwaarden, in- en uitgangen doorgaans worden uitgevoerd in Azure PowerShell gebruiken kunt [aan de slag met Azure-Cmdlets](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="ef09f-156">toolearn about tips that can help you use hello cmdlets, such as how parameter values, inputs, and outputs are typically handled in Azure PowerShell, see [Get Started with Azure Cmdlets](/powershell/azure/get-started-azureps).</span></span>

## <a name="step-1-set-hello-subscription"></a><span data-ttu-id="ef09f-157">Stap 1: Stel Hallo-abonnement</span><span class="sxs-lookup"><span data-stu-id="ef09f-157">Step 1: Set hello subscription</span></span>
<span data-ttu-id="ef09f-158">Voer deze cmdlets in PowerShell:</span><span class="sxs-lookup"><span data-stu-id="ef09f-158">In PowerShell, run these cmdlets:</span></span>

```
$UserName = "<user@live.com>"
$Password = "<password>"
$AzureSubscriptionName = "prod_sub1"

$SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
$Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $securePassword
Add-AzureAccount -Credential $Cred;
$AzureSubscription = Select-AzureSubscription -SubscriptionName $AzureSubscriptionName

```

<span data-ttu-id="ef09f-159">Hallo-elementen in Hallo "haken" vervangen door uw specifieke gegevens.</span><span class="sxs-lookup"><span data-stu-id="ef09f-159">Replace hello elements within hello "< >" with your specific information.</span></span>

## <a name="step-2-create-a-site-recovery-vault"></a><span data-ttu-id="ef09f-160">Stap 2: Een Site Recovery-kluis maken</span><span class="sxs-lookup"><span data-stu-id="ef09f-160">Step 2: Create a Site Recovery vault</span></span>
<span data-ttu-id="ef09f-161">Hallo-elementen in Hallo "haken" vervangen door uw specifieke gegevens in PowerShell en voer deze opdrachten:</span><span class="sxs-lookup"><span data-stu-id="ef09f-161">In PowerShell, replace hello elements within hello "< >" with your specific information, and run these commands:</span></span>

```

$VaultName = "<testvault123>"
$VaultGeo  = "<Southeast Asia>"
$OutputPathForSettingsFile = "<c:\>"

```


```
New-AzureSiteRecoveryVault -Location $VaultGeo -Name $VaultName;
$vault = Get-AzureSiteRecoveryVault -Name $VaultName;

```

## <a name="step-3-generate-a-vault-registration-key"></a><span data-ttu-id="ef09f-162">Stap 3: Een kluisregistratiesleutel genereren</span><span class="sxs-lookup"><span data-stu-id="ef09f-162">Step 3: Generate a vault registration key</span></span>
<span data-ttu-id="ef09f-163">Genereer een registratiesleutel in Hallo kluis.</span><span class="sxs-lookup"><span data-stu-id="ef09f-163">Generate a registration key in hello vault.</span></span> <span data-ttu-id="ef09f-164">Nadat u hello Azure Site Recovery Provider downloaden en op Hallo VMM-server installeren, gebruikt u deze sleutel tooregister Hallo VMM-server in Hallo kluis.</span><span class="sxs-lookup"><span data-stu-id="ef09f-164">After you download hello Azure Site Recovery Provider and install it on hello VMM server, you'll use this key tooregister hello VMM server in hello vault.</span></span>

1. <span data-ttu-id="ef09f-165">Hallo kluis instellingenbestand ophalen en Hallo context instellen:</span><span class="sxs-lookup"><span data-stu-id="ef09f-165">Get hello vault setting file and set hello context:</span></span>

   ```

   $VaultName = "<testvault123>"
   $VaultGeo  = "<Southeast Asia>"
   $OutputPathForSettingsFile = "<c:\>"

   $VaultSetingsFile = Get-AzureSiteRecoveryVaultSettingsFile -Location $VaultGeo -Name $VaultName -Path $OutputPathForSettingsFile;

   ```
2. <span data-ttu-id="ef09f-166">Hallo kluis context door het uitvoeren van de volgende opdrachten Hallo instellen:</span><span class="sxs-lookup"><span data-stu-id="ef09f-166">Set hello vault context by running hello following commands:</span></span>

   ```

   $VaultSettingFilePath = $vaultSetingsFile.FilePath
   $VaultContext = Import-AzureSiteRecoveryVaultSettingsFile -Path $VaultSettingFilePath -ErrorAction Stop

   ```

## <a name="step-4-install-hello-azure-site-recovery-provider"></a><span data-ttu-id="ef09f-167">Stap 4: Hello Azure Site Recovery Provider installeren</span><span class="sxs-lookup"><span data-stu-id="ef09f-167">Step 4: Install hello Azure Site Recovery Provider</span></span>
1. <span data-ttu-id="ef09f-168">Maak een map door het uitvoeren van de volgende opdracht Hallo op Hallo-VMM-machine:</span><span class="sxs-lookup"><span data-stu-id="ef09f-168">On hello VMM machine, create a directory by running hello following command:</span></span>

   ```

   pushd C:\ASR\

   ```
2. <span data-ttu-id="ef09f-169">Hallo-bestanden met behulp van de provider Hallo gedownload door het uitvoeren van de volgende opdracht Hallo uitpakken</span><span class="sxs-lookup"><span data-stu-id="ef09f-169">Extract hello files using hello downloaded provider by running hello following command</span></span>

   ```

   AzureSiteRecoveryProvider.exe /x:. /q

   ```
3. <span data-ttu-id="ef09f-170">Hallo-provider met behulp van de volgende opdrachten Hallo installeren:</span><span class="sxs-lookup"><span data-stu-id="ef09f-170">Install hello provider using hello following commands:</span></span>

   ```

   .\SetupDr.exe /i

   ```

   ```

   $installationRegPath = "hklm:\software\Microsoft\Microsoft System Center Virtual Machine Manager Server\DRAdapter"
   do
   {
     $isNotInstalled = $true;
     if(Test-Path $installationRegPath)
     {
         $isNotInstalled = $false;
     }
   }While($isNotInstalled)

   ```

   <span data-ttu-id="ef09f-171">Wachten op Hallo installatie toofinish.</span><span class="sxs-lookup"><span data-stu-id="ef09f-171">Wait for hello installation toofinish.</span></span>
4. <span data-ttu-id="ef09f-172">Hallo-server registreren in met behulp van de volgende opdracht Hallo Hallo-kluis:</span><span class="sxs-lookup"><span data-stu-id="ef09f-172">Register hello server in hello vault using hello following command:</span></span>

   ```

   $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
   pushd $BinPath
   $encryptionFilePath = "C:\temp\"
   .\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

   ```

## <a name="step-5-create-an-azure-storage-account"></a><span data-ttu-id="ef09f-173">Stap 5: Een Azure storage-account maken</span><span class="sxs-lookup"><span data-stu-id="ef09f-173">Step 5: Create an Azure storage account</span></span>
<span data-ttu-id="ef09f-174">Als u geen Azure storage-account hebt, kunt u een geo-replicatie ingeschakeld-account maken door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="ef09f-174">If you don't have an Azure storage account, create a geo-replication enabled account by running hello following command:</span></span>

```

$StorageAccountName = "teststorageacc1"
$StorageAccountGeo  = "Southeast Asia"

New-AzureStorageAccount -StorageAccountName $StorageAccountName -Label $StorageAccountName -Location $StorageAccountGeo;

```

<span data-ttu-id="ef09f-175">Houd er rekening mee dat Hallo storage-account moet in dezelfde regio bevinden als de service Azure Site Recovery Hallo Hallo en worden gekoppeld aan hetzelfde abonnement Hallo.</span><span class="sxs-lookup"><span data-stu-id="ef09f-175">Note that hello storage account must be in hello same region as hello Azure Site Recovery service, and be associated with hello same subscription.</span></span>

## <a name="step-6-install-hello-azure-recovery-services-agent"></a><span data-ttu-id="ef09f-176">Stap 6: Hello Azure Recovery Services-Agent installeren</span><span class="sxs-lookup"><span data-stu-id="ef09f-176">Step 6: Install hello Azure Recovery Services Agent</span></span>
<span data-ttu-id="ef09f-177">Hello Azure-portal installeren hello Azure Recovery Services-agent op elke Hyper-V-hostserver die zich in de VMM-clouds hello wilt u tooprotect.</span><span class="sxs-lookup"><span data-stu-id="ef09f-177">From hello Azure portal, install hello Azure Recovery Services agent on each Hyper-V host server located in hello VMM clouds you want tooprotect.</span></span>

<span data-ttu-id="ef09f-178">Voer Hallo opdracht op alle VMM-hosts te volgen:</span><span class="sxs-lookup"><span data-stu-id="ef09f-178">Run hello following command on all VMM hosts:</span></span>

```

marsagentinstaller.exe /q /nu

```


## <a name="step-7-configure-cloud-protection-settings"></a><span data-ttu-id="ef09f-179">Stap 7: Cloud configureren beveiligingsinstellingen</span><span class="sxs-lookup"><span data-stu-id="ef09f-179">Step 7: Configure cloud protection settings</span></span>
1. <span data-ttu-id="ef09f-180">Maak een cloud beveiliging profiel tooAzure door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="ef09f-180">Create a cloud protection profile tooAzure by running hello following command:</span></span>

   ```

   $ReplicationFrequencyInSeconds = "300";
   $ProfileResult = New-AzureSiteRecoveryProtectionProfileObject -ReplicationProvider HyperVReplica -RecoveryAzureSubscription $AzureSubscriptionName -RecoveryAzureStorageAccount $StorageAccountName -ReplicationFrequencyInSeconds     $ReplicationFrequencyInSeconds;

   ```
2. <span data-ttu-id="ef09f-181">Een beveiligingscontainer door het uitvoeren van de volgende opdrachten Hallo ophalen:</span><span class="sxs-lookup"><span data-stu-id="ef09f-181">Get a protection container by running hello following commands:</span></span>

   ```

   $PrimaryCloud = "testcloud"
   $protectionContainer = Get-AzureSiteRecoveryProtectionContainer -Name $PrimaryCloud;

   ```
3. <span data-ttu-id="ef09f-182">Koppeling van de beveiligingscontainer Hallo Hallo beginnen met Hallo cloud:</span><span class="sxs-lookup"><span data-stu-id="ef09f-182">Start hello association of hello protection container with hello cloud:</span></span>

   ```

   $associationJob = Start-AzureSiteRecoveryProtectionProfileAssociationJob -ProtectionProfile $profileResult -PrimaryProtectionContainer $protectionContainer;        

   ```
4. <span data-ttu-id="ef09f-183">Nadat het Hallo-taak is voltooid, voert u Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="ef09f-183">After hello job has finished, run hello following command:</span></span>

        $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
        if($job -eq $null -or $job.StateDescription -ne "Completed")
        {
        $isJobLeftForProcessing = $true;
        }


1. <span data-ttu-id="ef09f-184">Nadat het Hallo taak zijn verwerkt, voert u Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="ef09f-184">After hello job has finished processing, run hello following command:</span></span>

        Do
        {
        $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
        Write-Host "Job State:{0}, StateDescription:{1}" -f Job.State, $job.StateDescription;
        if($job -eq $null -or $job.StateDescription -ne "Completed")
        {
            $isJobLeftForProcessing = $true;
        }

        if($isJobLeftForProcessing)
        {
            Start-Sleep -Seconds 60
        }
        }While($isJobLeftForProcessing)



<span data-ttu-id="ef09f-185">Hallo-bewerking is toocheck Hallo voltooid Hallo stappen in [Monitoractiviteit](#monitor).</span><span class="sxs-lookup"><span data-stu-id="ef09f-185">toocheck hello completion of hello operation, follow hello steps in [Monitor Activity](#monitor).</span></span>

## <a name="step-8-configure-network-mapping"></a><span data-ttu-id="ef09f-186">Stap 8: Netwerktoewijzing configureren</span><span class="sxs-lookup"><span data-stu-id="ef09f-186">Step 8: Configure network mapping</span></span>
<span data-ttu-id="ef09f-187">Voordat u begint met de netwerktoewijzing controleert u of virtuele machines op de bronserver VMM Hallo verbonden tooa VM-netwerk.</span><span class="sxs-lookup"><span data-stu-id="ef09f-187">Before you begin network mapping verify that virtual machines on hello source VMM server are connected tooa VM network.</span></span> <span data-ttu-id="ef09f-188">Daarnaast maakt u een of meer virtuele netwerken in Azure.</span><span class="sxs-lookup"><span data-stu-id="ef09f-188">In addition, create one or more Azure virtual networks.</span></span> <span data-ttu-id="ef09f-189">Houd er rekening mee dat meerdere VM-netwerken kunnen bestaan uit toegewezen tooa één Azure-netwerk.</span><span class="sxs-lookup"><span data-stu-id="ef09f-189">Note that multiple VM networks can be mapped tooa single Azure network.</span></span>

<span data-ttu-id="ef09f-190">Houd er rekening mee dat als Hallo doelnetwerk meerdere subnetten heeft en een van deze subnetten Hallo heeft dezelfde naam als het subnet waarop Hallo bron virtual machine zich bevindt, wordt Hallo replica virtuele machine na een failover worden verbonden toothat Doelsubnet.</span><span class="sxs-lookup"><span data-stu-id="ef09f-190">Note that if hello target network has multiple subnets and one of those subnets has hello same name as subnet on which hello source virtual machine is located, then hello replica virtual machine will be connected toothat target subnet after failover.</span></span> <span data-ttu-id="ef09f-191">Als er geen een Doelsubnet met een overeenkomende naam beschikbaar is, worden Hallo virtuele machine verbonden toohello eerste subnet in het Hallo-netwerk.</span><span class="sxs-lookup"><span data-stu-id="ef09f-191">If there is not a target subnet with a matching name, hello virtual machine will be connected toohello first subnet in hello network.</span></span>

<span data-ttu-id="ef09f-192">de eerste opdracht Hallo opgehaald servers voor de huidige Azure Site Recovery-kluis Hallo.</span><span class="sxs-lookup"><span data-stu-id="ef09f-192">hello first command gets servers for hello current Azure Site Recovery vault.</span></span> <span data-ttu-id="ef09f-193">Hallo opdracht slaat Hallo Microsoft Azure Site Recovery-servers in Hallo $Servers matrixvariabele.</span><span class="sxs-lookup"><span data-stu-id="ef09f-193">hello command stores hello Microsoft Azure Site Recovery servers in hello $Servers array variable.</span></span>

    $Servers = Get-AzureSiteRecoveryServer


<span data-ttu-id="ef09f-194">de tweede opdracht Hallo ophalen Hallo een netwerk met site recovery voor de eerste server Hallo in Hallo $Servers matrix.</span><span class="sxs-lookup"><span data-stu-id="ef09f-194">hello second command gets hello site recovery network for hello first server in hello $Servers array.</span></span> <span data-ttu-id="ef09f-195">Hallo opdracht slaat Hallo netwerken in Hallo $Networks variabele.</span><span class="sxs-lookup"><span data-stu-id="ef09f-195">hello command stores hello networks in hello $Networks variable.</span></span>

    $Networks = Get-AzureSiteRecoveryNetwork -Server $Servers[0]

<span data-ttu-id="ef09f-196">Hallo derde opdracht uw Azure-abonnementen opgehaald met behulp van de cmdlet Get-AzureSubscription hello en slaat deze waarde op in Hallo $Subscriptions variabele.</span><span class="sxs-lookup"><span data-stu-id="ef09f-196">hello third command gets your Azure subscriptions by using hello Get-AzureSubscription cmdlet, and then stores that value in hello $Subscriptions variable.</span></span>

    $Subscriptions = Get-AzureSubscription



<span data-ttu-id="ef09f-197">Hallo vierde opdracht haalt virtuele netwerken in Azure met behulp van de cmdlet Get-AzureVNetSite hello en dat de waarde in Hallo $AzureVmNetworks variabele.</span><span class="sxs-lookup"><span data-stu-id="ef09f-197">hello fourth command gets Azure virtual networks by using hello Get-AzureVNetSite cmdlet, and then that value in hello $AzureVmNetworks variable.</span></span>

    $AzureVmNetworks = Get-AzureVNetSite



<span data-ttu-id="ef09f-198">Hallo laatste cmdlet maakt een toewijzing tussen Hallo primaire netwerk en hello Azure virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="ef09f-198">hello final cmdlet creates a mapping between hello primary network and hello Azure virtual machine network.</span></span> <span data-ttu-id="ef09f-199">het primaire netwerk Hallo geeft Hallo cmdlet als Hallo eerste element van $Networks.</span><span class="sxs-lookup"><span data-stu-id="ef09f-199">hello cmdlet specifies hello primary network as hello first element of $Networks.</span></span> <span data-ttu-id="ef09f-200">Hallo cmdlet geeft een VM-netwerk als eerste element van $AzureVmNetworks Hallo met behulp van de-ID.</span><span class="sxs-lookup"><span data-stu-id="ef09f-200">hello cmdlet specifies a virtual machine network as hello first element of $AzureVmNetworks by using its ID.</span></span> <span data-ttu-id="ef09f-201">Hallo-opdracht bevat uw Azure-abonnement-ID.</span><span class="sxs-lookup"><span data-stu-id="ef09f-201">hello command includes your Azure subscription ID.</span></span>

    New-AzureSiteRecoveryNetworkMapping -PrimaryNetwork $Networks[0] -AzureSubscriptionId $Subscriptions[0].SubscriptionId -AzureVMNetworkId $AzureVmNetworks[0].Id


## <a name="step-9-enable-protection-for-virtual-machines"></a><span data-ttu-id="ef09f-202">Stap 9: Beveiliging voor virtuele machines inschakelen</span><span class="sxs-lookup"><span data-stu-id="ef09f-202">Step 9: Enable protection for virtual machines</span></span>
<span data-ttu-id="ef09f-203">Nadat de servers, clouds en netwerken correct zijn geconfigureerd, kunt u beveiliging voor virtuele machines in de cloud Hallo inschakelen.</span><span class="sxs-lookup"><span data-stu-id="ef09f-203">After servers, clouds, and networks are configured correctly, you can enable protection for virtual machines in hello cloud.</span></span> <span data-ttu-id="ef09f-204">Let op Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="ef09f-204">Note hello following:</span></span>

<span data-ttu-id="ef09f-205">Virtuele machines moeten voldoen aan [vereisten van de virtuele machine van Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="ef09f-205">Virtual machines must meet [Azure virtual machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

<span data-ttu-id="ef09f-206">tooenable beveiliging Hallo-besturingssysteem en de schijfeigenschappen besturingssysteem moeten worden ingesteld voor Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="ef09f-206">tooenable protection hello operating system and operating system disk properties must be set for hello virtual machine.</span></span> <span data-ttu-id="ef09f-207">Wanneer u een virtuele machine in VMM met een virtuele machine-sjabloon maakt, kunt u Hallo-eigenschap instellen.</span><span class="sxs-lookup"><span data-stu-id="ef09f-207">When you create a virtual machine in VMM using a virtual machine template you can set hello property.</span></span> <span data-ttu-id="ef09f-208">U kunt deze eigenschappen voor de bestaande virtuele machines ook instellen op Hallo **algemene** en **hardwareconfiguratie** tabbladen van de eigenschappen van de virtuele machine Hallo.</span><span class="sxs-lookup"><span data-stu-id="ef09f-208">You can also set these properties for existing virtual machines on hello **General** and **Hardware Configuration** tabs of hello virtual machine properties.</span></span> <span data-ttu-id="ef09f-209">Als u deze eigenschappen niet ingesteld in VMM, moet u kunnen tooconfigure ze in hello Azure Site Recovery-portal.</span><span class="sxs-lookup"><span data-stu-id="ef09f-209">If you don't set these properties in VMM you'll be able tooconfigure them in hello Azure Site Recovery portal.</span></span>

1. <span data-ttu-id="ef09f-210">tooenable beveiliging Hallo opdracht tooget hello beveiligingscontainer volgende uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="ef09f-210">tooenable protection, run hello following command tooget hello protection container:</span></span>

     <span data-ttu-id="ef09f-211">$ProtectionContainer = get-AzureSiteRecoveryProtectionContainer-$CloudName naam</span><span class="sxs-lookup"><span data-stu-id="ef09f-211">$ProtectionContainer = Get-AzureSiteRecoveryProtectionContainer -Name $CloudName</span></span>
2. <span data-ttu-id="ef09f-212">Hallo beveiligde entiteit (VM) door het uitvoeren van de volgende opdracht Hallo ophalen:</span><span class="sxs-lookup"><span data-stu-id="ef09f-212">Get hello protection entity (VM) by running hello following command:</span></span>

        $protectionEntity = Get-AzureSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer



1. <span data-ttu-id="ef09f-213">Hallo DR voor Hallo VM inschakelen door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="ef09f-213">Enable hello DR for hello VM by running hello following command:</span></span>

        $jobResult = Set-AzureSiteRecoveryProtectionEntity -ProtectionEntity $protectionEntity     -Protection Enable -Force



## <a name="test-your-deployment"></a><span data-ttu-id="ef09f-214">Uw implementatie testen</span><span class="sxs-lookup"><span data-stu-id="ef09f-214">Test your deployment</span></span>
<span data-ttu-id="ef09f-215">tootest plannen voor uw implementatie kunt u een testfailover voor één virtuele machine uitvoeren of maken van een herstelplan dat bestaat uit meerdere virtuele machines en een testfailover voor Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="ef09f-215">tootest your deployment you can run a test failover for a single virtual machine, or create a recovery plan consisting of multiple virtual machines and run a test failover for hello plan.</span></span> <span data-ttu-id="ef09f-216">Met een testfailover wordt uw failover- en herstelmechanisme in een geïsoleerd netwerk gesimuleerd.</span><span class="sxs-lookup"><span data-stu-id="ef09f-216">Test failover simulates your failover and recovery mechanism in an isolated network.</span></span> <span data-ttu-id="ef09f-217">Opmerking:</span><span class="sxs-lookup"><span data-stu-id="ef09f-217">Note that:</span></span>

* <span data-ttu-id="ef09f-218">Als u tooconnect toohello virtuele machine in Azure met extern bureaublad na een failover Hallo wilt, moet u verbinding met extern bureaublad inschakelen op Hallo virtuele machine voordat u Hallo testfailover uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="ef09f-218">If you want tooconnect toohello virtual machine in Azure using Remote Desktop after hello failover, enable Remote Desktop Connection on hello virtual machine before you run hello test failover.</span></span>
* <span data-ttu-id="ef09f-219">Na een failover gebruikt u een openbaar IP-adres tooconnect toohello virtuele machine in Azure met behulp van extern bureaublad.</span><span class="sxs-lookup"><span data-stu-id="ef09f-219">After failover, you'll use a public IP address tooconnect toohello virtual machine in Azure using Remote Desktop.</span></span> <span data-ttu-id="ef09f-220">Als u toodo dit wilt, zorg ervoor dat u geen domeinbeleid hebt geïmplementeerd die verhinderen dat u verbinding maakt tooa virtuele machine via een openbaar adres.</span><span class="sxs-lookup"><span data-stu-id="ef09f-220">If you want toodo this, ensure you don't have any domain policies that prevent you from connecting tooa virtual machine using a public address.</span></span>

<span data-ttu-id="ef09f-221">Hallo-bewerking is toocheck Hallo voltooid Hallo stappen in [Monitoractiviteit](#monitor).</span><span class="sxs-lookup"><span data-stu-id="ef09f-221">toocheck hello completion of hello operation, follow hello steps in [Monitor Activity](#monitor).</span></span>

### <a name="create-a-recovery-plan"></a><span data-ttu-id="ef09f-222">Een herstelplan maken</span><span class="sxs-lookup"><span data-stu-id="ef09f-222">Create a recovery plan</span></span>
1. <span data-ttu-id="ef09f-223">Maken van een XML-bestand als een sjabloon voor het herstelplan met behulp van onderstaande Hallo-gegevens en deze opslaan als 'C:\RPTemplatePath.xml'.</span><span class="sxs-lookup"><span data-stu-id="ef09f-223">Create an .xml file as a template for your recovery plan using hello data below, and then save it as "C:\RPTemplatePath.xml".</span></span>
2. <span data-ttu-id="ef09f-224">Hallo RecoveryPlan knooppunt Id, naam, PrimaryServerId en SecondaryServerId wijzigen.</span><span class="sxs-lookup"><span data-stu-id="ef09f-224">Change hello RecoveryPlan node Id, Name, PrimaryServerId, and SecondaryServerId.</span></span>
3. <span data-ttu-id="ef09f-225">Hallo ProtectionEntity knooppunt PrimaryProtectionEntityId (vmid uit VMM) wijzigen.</span><span class="sxs-lookup"><span data-stu-id="ef09f-225">Change hello ProtectionEntity node PrimaryProtectionEntityId (vmid from VMM).</span></span>
4. <span data-ttu-id="ef09f-226">U kunt meer virtuele machines toevoegen door meer ProtectionEntity knooppunten toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="ef09f-226">You can add more VMs by adding more ProtectionEntity nodes.</span></span>

        <#
        <?xml version="1.0" encoding="utf-16"?>
        <RecoveryPlan Id="d0323b26-5be2-471b-addc-0a8742796610" Name="rp-test"     PrimaryServerId="9350a530-d5af-435b-9f2b-b941b5d9fcd5"     SecondaryServerId="21a9403c-6ec1-44f2-b744-b4e50b792387" Description=""     Version="V2014_07">
          <Actions />
          <ActionGroups>
            <ShutdownAllActionGroup Id="ShutdownAllActionGroup">
              <PreActionSequence />
              <PostActionSequence />
            </ShutdownAllActionGroup>
            <FailoverAllActionGroup Id="FailoverAllActionGroup">
              <PreActionSequence />
              <PostActionSequence />
            </FailoverAllActionGroup>
            <BootActionGroup Id="DefaultActionGroup">
              <PreActionSequence />
              <PostActionSequence />
              <ProtectionEntity PrimaryProtectionEntityId="d4c8ce92-a613-4c63-9b03-    cf163cc36ef8" />
            </BootActionGroup>
          </ActionGroups>
          <ActionGroupSequence>
            <ActionGroup Id="ShutdownAllActionGroup" ActionId="ShutdownAllActionGroup"     Before="FailoverAllActionGroup" />
            <ActionGroup Id="FailoverAllActionGroup" ActionId="FailoverAllActionGroup"     After="ShutdownAllActionGroup" Before="DefaultActionGroup" />
            <ActionGroup Id="DefaultActionGroup" ActionId="DefaultActionGroup" After="FailoverAllActionGroup"/>
          </ActionGroupSequence>
        </RecoveryPlan>
        #>



1. <span data-ttu-id="ef09f-227">Hallo-gegevens in de sjabloon Hallo invullen:</span><span class="sxs-lookup"><span data-stu-id="ef09f-227">Fill in hello data in hello template:</span></span>

        $TemplatePath = "C:\RPTemplatePath.xml";



1. <span data-ttu-id="ef09f-228">Hallo RecoveryPlan maken:</span><span class="sxs-lookup"><span data-stu-id="ef09f-228">Create hello RecoveryPlan:</span></span>

        $RPCreationJob = New-AzureSiteRecoveryRecoveryPlan -File $TemplatePath -WaitForCompletion;

### <a name="run-a-test-failover"></a><span data-ttu-id="ef09f-229">Een testfailover uitvoeren</span><span class="sxs-lookup"><span data-stu-id="ef09f-229">Run a test failover</span></span>
1. <span data-ttu-id="ef09f-230">Hallo RecoveryPlan object ophalen door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="ef09f-230">Get hello RecoveryPlan object by running hello following command:</span></span>

     <span data-ttu-id="ef09f-231">$RPObject = get-AzureSiteRecoveryRecoveryPlan-naam $RPName;</span><span class="sxs-lookup"><span data-stu-id="ef09f-231">$RPObject = Get-AzureSiteRecoveryRecoveryPlan -Name $RPName;</span></span>
2. <span data-ttu-id="ef09f-232">Start de testfailover Hallo door het uitvoeren van Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="ef09f-232">Start hello test failover by running hello following command:</span></span>

        $jobIDResult = Start-AzureSiteRecoveryTestFailoverJob -RecoveryPlan $RPObject -Direction PrimaryToRecovery;


## <span data-ttu-id="ef09f-233"><a name=monitor></a>Voor Monitoractiviteit</span><span class="sxs-lookup"><span data-stu-id="ef09f-233"><a name=monitor></a> Monitor Activity</span></span>
<span data-ttu-id="ef09f-234">Gebruik hello opdrachten toomonitor Hallo activiteit te volgen.</span><span class="sxs-lookup"><span data-stu-id="ef09f-234">Use hello following commands toomonitor hello activity.</span></span> <span data-ttu-id="ef09f-235">Houd er rekening mee dat u toowait Between-taken voor Hallo verwerking toofinish hebt.</span><span class="sxs-lookup"><span data-stu-id="ef09f-235">Note that you have toowait in between jobs for hello processing toofinish.</span></span>

    Do
    {
            $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
            Write-Host "Job State:{0}, StateDescription:{1}" -f Job.State, $job.StateDescription;
            if($job -eq $null -or $job.StateDescription -ne "Completed")
            {
                $isJobLeftForProcessing = $true;
            }

        if($isJobLeftForProcessing)
            {
                Start-Sleep -Seconds 60
            }
    }While($isJobLeftForProcessing)



## <a name="next-steps"></a><span data-ttu-id="ef09f-236">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ef09f-236">Next steps</span></span>
<span data-ttu-id="ef09f-237">[Lees meer](/powershell/azure/overview) over Azure Site Recovery PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="ef09f-237">[Read more](/powershell/azure/overview) about Azure Site Recovery PowerShell cmdlets.</span></span> <span data-ttu-id="ef09f-238"></a>.</span><span class="sxs-lookup"><span data-stu-id="ef09f-238"></a>.</span></span>
