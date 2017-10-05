---
title: Hyper-V-machines repliceren naar Azure in de klassieke portal met PowerShell | Microsoft Docs
description: De replicatie van Hyper-V virtuele machines in VMM-clouds met Site Recovery en PowerShell in de klassieke portal automatiseren
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
ms.openlocfilehash: 581daaaa5cc0cf8be782f834c6bdb3f27ee413fb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="replicate-hyper-v-vms-to-azure-with-powershell-in-the-classic-portal"></a><span data-ttu-id="07c72-103">Hyper-V-machines repliceren naar Azure met PowerShell in de klassieke portal</span><span class="sxs-lookup"><span data-stu-id="07c72-103">Replicate Hyper-V VMs to Azure with PowerShell in the classic portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="07c72-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="07c72-104">Azure Portal</span></span>](site-recovery-vmm-to-azure.md)
> * [<span data-ttu-id="07c72-105">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="07c72-105">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [<span data-ttu-id="07c72-106">Klassieke portal</span><span class="sxs-lookup"><span data-stu-id="07c72-106">Classic Portal</span></span>](site-recovery-vmm-to-azure-classic.md)
> * [<span data-ttu-id="07c72-107">PowerShell - Klassiek</span><span class="sxs-lookup"><span data-stu-id="07c72-107">PowerShell - Classic</span></span>](site-recovery-deploy-with-powershell.md)
>
>

## <a name="overview"></a><span data-ttu-id="07c72-108">Overzicht</span><span class="sxs-lookup"><span data-stu-id="07c72-108">Overview</span></span>
<span data-ttu-id="07c72-109">Azure Site Recovery draagt bij aan uw strategie voor zakelijke continuïteit en noodherstel herstel (BCDR) door replicatie, failovers en herstel van virtuele machines in een aantal implementatiescenario's te organiseren.</span><span class="sxs-lookup"><span data-stu-id="07c72-109">Azure Site Recovery contributes to your business continuity and disaster recovery (BCDR) strategy by orchestrating replication, failover and recovery of virtual machines in a number of deployment scenarios.</span></span> <span data-ttu-id="07c72-110">Zie voor een volledige lijst van de implementatie van scenario's de [Azure Site Recovery-overzicht](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="07c72-110">For a full list of deployment scenarios see the [Azure Site Recovery overview](site-recovery-overview.md).</span></span>

<span data-ttu-id="07c72-111">In dit artikel leest u hoe u PowerShell gebruikt voor het automatiseren van algemene taken die u uitvoeren moet bij het instellen van Azure Site Recovery Hyper-V virtuele machines in System Center VMM-clouds repliceren naar Azure-opslag.</span><span class="sxs-lookup"><span data-stu-id="07c72-111">This article shows you how to use PowerShell to automate common tasks you need to perform when you set up Azure Site Recovery to replicate Hyper-V virtual machines in System Center VMM clouds to Azure storage.</span></span>

<span data-ttu-id="07c72-112">Het artikel bevat vereisten voor het scenario en ziet u het instellen van een Site Recovery-kluis, de Azure Site Recovery Provider installeren op de bron-VMM-server, de server in de kluis registreren, Azure storage-account toevoegen en installeren van de Azure Recovery Services-agent op Hyper-V-hostservers Configureer beveiligingsinstellingen voor VMM-clouds die wordt toegepast op alle beveiligde virtuele machines en schakel vervolgens de beveiliging voor deze virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="07c72-112">The article includes prerequisites for the scenario, and shows you how to set up a Site Recovery vault, install the Azure Site Recovery Provider on the source VMM server, register the server in the vault, add an Azure storage account, install the Azure Recovery Services agent on Hyper-V host servers, configure protection settings for VMM clouds that will be applied to all protected virtual machines, and then enable protection for those virtual machines.</span></span> <span data-ttu-id="07c72-113">Test tenslotte de failover om te controleren of alles naar verwachting werkt.</span><span class="sxs-lookup"><span data-stu-id="07c72-113">Finish up by testing the failover to make sure everything's working as expected.</span></span>

<span data-ttu-id="07c72-114">Als u problemen bij het instellen van dit scenario, stel uw vragen op de [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="07c72-114">If you run into problems setting up this scenario, post your questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

> [!NOTE]
> <span data-ttu-id="07c72-115">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="07c72-115">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="07c72-116">In dit artikel bevat informatie over met behulp van het klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="07c72-116">This article covers using the Classic deployment model.</span></span>
>
>

## <a name="before-you-start"></a><span data-ttu-id="07c72-117">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="07c72-117">Before you start</span></span>
<span data-ttu-id="07c72-118">Zorg ervoor dat u deze vereisten hebt voldaan:</span><span class="sxs-lookup"><span data-stu-id="07c72-118">Make sure you have these prerequisites in place:</span></span>

### <a name="azure-prerequisites"></a><span data-ttu-id="07c72-119">Vereisten voor Azure</span><span class="sxs-lookup"><span data-stu-id="07c72-119">Azure prerequisites</span></span>
* <span data-ttu-id="07c72-120">U hebt een [Microsoft Azure](https://azure.microsoft.com/)-account nodig.</span><span class="sxs-lookup"><span data-stu-id="07c72-120">You'll need a [Microsoft Azure](https://azure.microsoft.com/) account.</span></span> <span data-ttu-id="07c72-121">U kunt beginnen met een [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="07c72-121">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="07c72-122">U hebt een Azure Storage-account nodig om gerepliceerde gegevens op te slaan.</span><span class="sxs-lookup"><span data-stu-id="07c72-122">You'll need an Azure storage account to store replicated data.</span></span> <span data-ttu-id="07c72-123">Het account moet geo-replicatie is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="07c72-123">The account needs geo-replication enabled.</span></span> <span data-ttu-id="07c72-124">Het moet zich in dezelfde regio bevinden als de Azure Site Recovery-kluis en worden gekoppeld aan hetzelfde abonnement.</span><span class="sxs-lookup"><span data-stu-id="07c72-124">It should be in the same region as the Azure Site Recovery vault and be associated with the same subscription.</span></span> <span data-ttu-id="07c72-125">[Meer informatie over Azure storage](../storage/common/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="07c72-125">[Learn more about Azure storage](../storage/common/storage-introduction.md).</span></span>
* <span data-ttu-id="07c72-126">U moet ervoor zorgen dat virtuele machines die u wilt beveiligen, voldoen aan [vereisten van de virtuele machine van Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="07c72-126">You'll need to make sure that virtual machines you want to protect comply with [Azure virtual machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

### <a name="vmm-prerequisites"></a><span data-ttu-id="07c72-127">VMM-vereisten</span><span class="sxs-lookup"><span data-stu-id="07c72-127">VMM prerequisites</span></span>
* <span data-ttu-id="07c72-128">U moet de VMM-server waarop System Center 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="07c72-128">You'll need  VMM server running on System Center 2012 R2.</span></span>
* <span data-ttu-id="07c72-129">U moet ten minste één cloud op de VMM-beheerserver die u wilt beveiligen.</span><span class="sxs-lookup"><span data-stu-id="07c72-129">You'll need at least one cloud on the VMM server you want to protect.</span></span> <span data-ttu-id="07c72-130">De cloud moet bevatten:</span><span class="sxs-lookup"><span data-stu-id="07c72-130">The cloud should contain:</span></span>
  * <span data-ttu-id="07c72-131">Een of meer VMM-hostgroepen.</span><span class="sxs-lookup"><span data-stu-id="07c72-131">One or more VMM host groups.</span></span>
  * <span data-ttu-id="07c72-132">Een of meer Hyper-V-hostservers of -clusters in elke hostgroep.</span><span class="sxs-lookup"><span data-stu-id="07c72-132">One or more Hyper-V host servers or clusters in each host group .</span></span>
  * <span data-ttu-id="07c72-133">Een of meer virtuele machines op de bronserver met Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="07c72-133">One or more virtual machines on the source Hyper-V server.</span></span>

### <a name="hyper-v-prerequisites"></a><span data-ttu-id="07c72-134">Hyper-V-vereisten</span><span class="sxs-lookup"><span data-stu-id="07c72-134">Hyper-V prerequisites</span></span>
* <span data-ttu-id="07c72-135">De Hyper-V-hostservers moeten ten minste draaien **Windows Server 2012** met Hyper-V-rol of **Microsoft Hyper-V Server 2012** en de meest recente updates hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="07c72-135">The host Hyper-V servers must be running at least **Windows Server 2012** with Hyper-V role or **Microsoft Hyper-V Server 2012** and have the latest updates installed.</span></span>
* <span data-ttu-id="07c72-136">Als u Hyper-V in een cluster uitvoert, wordt die clusterbroker niet automatisch gemaakt als u een cluster op basis van een statisch IP-adres hebt.</span><span class="sxs-lookup"><span data-stu-id="07c72-136">If you're running Hyper-V in a cluster note that cluster broker isn't created automatically if you have a static IP address-based cluster.</span></span> <span data-ttu-id="07c72-137">U moet de clusterbroker handmatig configureren.</span><span class="sxs-lookup"><span data-stu-id="07c72-137">You'll need to configure the cluster broker manually.</span></span> <span data-ttu-id="07c72-138">Om dit te doen, in Serverbeheer > Failover Cluster Manager verbinding met het cluster, klikt u op **functie configureren** en selecteer **Hyper-V Replica Broker** in de **rol selecteren** scherm van de wizard maximale beschikbaarheid.</span><span class="sxs-lookup"><span data-stu-id="07c72-138">To do this, in Server Manager > Failover Cluster Manager, connect to the cluster, click **Configure Role** and select **Hyper-V Replica Broker** in the **Select Role** screen of the High Availability wizard.</span></span>
* <span data-ttu-id="07c72-139">Alle Hyper-V-hostserver of het cluster waarvoor u wilt beheren protection moet worden opgenomen in een VMM-cloud.</span><span class="sxs-lookup"><span data-stu-id="07c72-139">Any Hyper-V host server or cluster for which you want to manage protection must be included in a VMM cloud.</span></span>

### <a name="network-mapping-prerequisites"></a><span data-ttu-id="07c72-140">Vereisten voor netwerktoewijzing</span><span class="sxs-lookup"><span data-stu-id="07c72-140">Network mapping prerequisites</span></span>
<span data-ttu-id="07c72-141">Wanneer u virtuele machines in Azure beveiligt, zorgen de koppelingen van netwerktoewijzingen tussen VM-netwerken op de bron-VMM-server en doel-Azure-netwerken voor het volgende:</span><span class="sxs-lookup"><span data-stu-id="07c72-141">When you protect virtual machines in Azure network mapping maps between VM networks on the source VMM server and target Azure networks to enable the following:</span></span>

* <span data-ttu-id="07c72-142">Alle machines die op hetzelfde netwerk failover kunnen verbinden met elkaar, ongeacht welk herstelplan ze zich in.</span><span class="sxs-lookup"><span data-stu-id="07c72-142">All machines which fail over on the same network can connect to each other, irrespective of which recovery plan they are in.</span></span>
* <span data-ttu-id="07c72-143">Als een netwerkgateway is ingesteld in het doel-Azure-netwerk, kunnen virtuele machines worden verbonden met andere on-premises virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="07c72-143">If a network gateway is setup on the target Azure network, virtual machines can connect to other on-premises virtual machines.</span></span>
* <span data-ttu-id="07c72-144">Als u geen netwerktoewijzing configureert, kunnen alleen virtuele machines met failover in hetzelfde herstelplan met elkaar worden verbonden na failover naar Azure.</span><span class="sxs-lookup"><span data-stu-id="07c72-144">If you don’t configure network mapping only virtual machines that fail over in the same recovery plan will be able to connect to each other after failover to Azure.</span></span>

<span data-ttu-id="07c72-145">Als u netwerktoewijzing wilt implementeren, hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="07c72-145">If you want to deploy network mapping you'll need the following:</span></span>

* <span data-ttu-id="07c72-146">De virtuele machines die u wilt beveiligen op de bron-VMM-server, moeten zijn verbonden met een VM-netwerk.</span><span class="sxs-lookup"><span data-stu-id="07c72-146">The virtual machines you want to protect on the source VMM server should be connected to a VM network.</span></span> <span data-ttu-id="07c72-147">Dit netwerk moet zijn gekoppeld aan een logisch netwerk dat is gekoppeld aan de cloud.</span><span class="sxs-lookup"><span data-stu-id="07c72-147">That network should be linked to a logical network that is associated with the cloud.</span></span>
* <span data-ttu-id="07c72-148">Een Azure-netwerk waarmee gerepliceerde virtuele machines verbinding kunnen maken na failover.</span><span class="sxs-lookup"><span data-stu-id="07c72-148">An Azure network to which replicated virtual machines can connect after failover.</span></span> <span data-ttu-id="07c72-149">U selecteert dit netwerk op het moment van failover.</span><span class="sxs-lookup"><span data-stu-id="07c72-149">You'll select this network at the time of failover.</span></span> <span data-ttu-id="07c72-150">Het netwerk moet zich in dezelfde regio bevinden als uw Azure Site Recovery-abonnement.</span><span class="sxs-lookup"><span data-stu-id="07c72-150">The network should be in the same region as your Azure Site Recovery subscription.</span></span>

### <a name="powershell-prerequisites"></a><span data-ttu-id="07c72-151">PowerShell-vereisten</span><span class="sxs-lookup"><span data-stu-id="07c72-151">PowerShell prerequisites</span></span>
<span data-ttu-id="07c72-152">Zorg ervoor dat u hebt Azure PowerShell klaar voor gebruik.</span><span class="sxs-lookup"><span data-stu-id="07c72-152">Make sure you have Azure PowerShell ready to go.</span></span> <span data-ttu-id="07c72-153">Als u al van PowerShell gebruikmaakt, moet u een upgrade uitvoeren naar versie 0.8.10 of hoger.</span><span class="sxs-lookup"><span data-stu-id="07c72-153">If you are already using PowerShell, you'll need to upgrade to version 0.8.10 or later.</span></span> <span data-ttu-id="07c72-154">Zie voor meer informatie over het instellen van PowerShell [installeren en configureren van Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="07c72-154">For information about setting up PowerShell, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="07c72-155">Zodra u hebt ingesteld en PowerShell geconfigureerd, kunt u alle van de beschikbare cmdlets voor de service weergeven [hier](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="07c72-155">Once you have set up and configured PowerShell, you can view all of the available cmdlets for the service [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="07c72-156">Zie voor meer informatie over tips kunt u de cmdlets, zoals hoe parameterwaarden, in- en uitgangen doorgaans worden uitgevoerd in Azure PowerShell gebruiken [aan de slag met Azure-Cmdlets](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="07c72-156">To learn about tips that can help you use the cmdlets, such as how parameter values, inputs, and outputs are typically handled in Azure PowerShell, see [Get Started with Azure Cmdlets](/powershell/azure/get-started-azureps).</span></span>

## <a name="step-1-set-the-subscription"></a><span data-ttu-id="07c72-157">Stap 1: Stel het abonnement</span><span class="sxs-lookup"><span data-stu-id="07c72-157">Step 1: Set the subscription</span></span>
<span data-ttu-id="07c72-158">Voer deze cmdlets in PowerShell:</span><span class="sxs-lookup"><span data-stu-id="07c72-158">In PowerShell, run these cmdlets:</span></span>

```
$UserName = "<user@live.com>"
$Password = "<password>"
$AzureSubscriptionName = "prod_sub1"

$SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
$Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $securePassword
Add-AzureAccount -Credential $Cred;
$AzureSubscription = Select-AzureSubscription -SubscriptionName $AzureSubscriptionName

```

<span data-ttu-id="07c72-159">De elementen in de 'haken"vervangen door uw specifieke gegevens.</span><span class="sxs-lookup"><span data-stu-id="07c72-159">Replace the elements within the "< >" with your specific information.</span></span>

## <a name="step-2-create-a-site-recovery-vault"></a><span data-ttu-id="07c72-160">Stap 2: Een Site Recovery-kluis maken</span><span class="sxs-lookup"><span data-stu-id="07c72-160">Step 2: Create a Site Recovery vault</span></span>
<span data-ttu-id="07c72-161">De elementen in de 'haken"vervangen door uw specifieke gegevens in PowerShell en voer deze opdrachten:</span><span class="sxs-lookup"><span data-stu-id="07c72-161">In PowerShell, replace the elements within the "< >" with your specific information, and run these commands:</span></span>

```

$VaultName = "<testvault123>"
$VaultGeo  = "<Southeast Asia>"
$OutputPathForSettingsFile = "<c:\>"

```


```
New-AzureSiteRecoveryVault -Location $VaultGeo -Name $VaultName;
$vault = Get-AzureSiteRecoveryVault -Name $VaultName;

```

## <a name="step-3-generate-a-vault-registration-key"></a><span data-ttu-id="07c72-162">Stap 3: Een kluisregistratiesleutel genereren</span><span class="sxs-lookup"><span data-stu-id="07c72-162">Step 3: Generate a vault registration key</span></span>
<span data-ttu-id="07c72-163">Genereer een registratiesleutel in de kluis.</span><span class="sxs-lookup"><span data-stu-id="07c72-163">Generate a registration key in the vault.</span></span> <span data-ttu-id="07c72-164">Nadat u Azure Site Recovery Provider hebt gedownload en op de VMM-server hebt geïnstalleerd, gebruikt u deze sleutel om de VMM-server in de kluis te registreren.</span><span class="sxs-lookup"><span data-stu-id="07c72-164">After you download the Azure Site Recovery Provider and install it on the VMM server, you'll use this key to register the VMM server in the vault.</span></span>

1. <span data-ttu-id="07c72-165">Het bestand van de instelling kluis ophalen en instellen van de context:</span><span class="sxs-lookup"><span data-stu-id="07c72-165">Get the vault setting file and set the context:</span></span>

   ```

   $VaultName = "<testvault123>"
   $VaultGeo  = "<Southeast Asia>"
   $OutputPathForSettingsFile = "<c:\>"

   $VaultSetingsFile = Get-AzureSiteRecoveryVaultSettingsFile -Location $VaultGeo -Name $VaultName -Path $OutputPathForSettingsFile;

   ```
2. <span data-ttu-id="07c72-166">De context van de kluis instellen met de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="07c72-166">Set the vault context by running the following commands:</span></span>

   ```

   $VaultSettingFilePath = $vaultSetingsFile.FilePath
   $VaultContext = Import-AzureSiteRecoveryVaultSettingsFile -Path $VaultSettingFilePath -ErrorAction Stop

   ```

## <a name="step-4-install-the-azure-site-recovery-provider"></a><span data-ttu-id="07c72-167">Stap 4: De Azure Site Recovery Provider installeren</span><span class="sxs-lookup"><span data-stu-id="07c72-167">Step 4: Install the Azure Site Recovery Provider</span></span>
1. <span data-ttu-id="07c72-168">Op de VMM-machine, maak een map met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="07c72-168">On the VMM machine, create a directory by running the following command:</span></span>

   ```

   pushd C:\ASR\

   ```
2. <span data-ttu-id="07c72-169">Pak de bestanden met de gedownloade provider door de volgende opdracht uit te voeren</span><span class="sxs-lookup"><span data-stu-id="07c72-169">Extract the files using the downloaded provider by running the following command</span></span>

   ```

   AzureSiteRecoveryProvider.exe /x:. /q

   ```
3. <span data-ttu-id="07c72-170">Installeer de provider met de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="07c72-170">Install the provider using the following commands:</span></span>

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

   <span data-ttu-id="07c72-171">Wacht totdat de installatie is voltooid.</span><span class="sxs-lookup"><span data-stu-id="07c72-171">Wait for the installation to finish.</span></span>
4. <span data-ttu-id="07c72-172">Registreer de server in de kluis die met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="07c72-172">Register the server in the vault using the following command:</span></span>

   ```

   $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
   pushd $BinPath
   $encryptionFilePath = "C:\temp\"
   .\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

   ```

## <a name="step-5-create-an-azure-storage-account"></a><span data-ttu-id="07c72-173">Stap 5: Een Azure storage-account maken</span><span class="sxs-lookup"><span data-stu-id="07c72-173">Step 5: Create an Azure storage account</span></span>
<span data-ttu-id="07c72-174">Als u geen Azure storage-account hebt, kunt u een geo-replicatie ingeschakeld-account maken met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="07c72-174">If you don't have an Azure storage account, create a geo-replication enabled account by running the following command:</span></span>

```

$StorageAccountName = "teststorageacc1"
$StorageAccountGeo  = "Southeast Asia"

New-AzureStorageAccount -StorageAccountName $StorageAccountName -Label $StorageAccountName -Location $StorageAccountGeo;

```

<span data-ttu-id="07c72-175">Houd er rekening mee dat het opslagaccount moet zich in dezelfde regio bevinden als de Azure Site Recovery-service en gekoppeld aan hetzelfde abonnement worden.</span><span class="sxs-lookup"><span data-stu-id="07c72-175">Note that the storage account must be in the same region as the Azure Site Recovery service, and be associated with the same subscription.</span></span>

## <a name="step-6-install-the-azure-recovery-services-agent"></a><span data-ttu-id="07c72-176">Stap 6: De Azure Recovery Services-Agent installeren</span><span class="sxs-lookup"><span data-stu-id="07c72-176">Step 6: Install the Azure Recovery Services Agent</span></span>
<span data-ttu-id="07c72-177">Vanuit de Azure-portal door de Azure Recovery Services-agent te installeren op elke Hyper-V-hostserver die zich in de VMM-clouds die u wilt beveiligen.</span><span class="sxs-lookup"><span data-stu-id="07c72-177">From the Azure portal, install the Azure Recovery Services agent on each Hyper-V host server located in the VMM clouds you want to protect.</span></span>

<span data-ttu-id="07c72-178">Voer de volgende opdracht uit op alle VMM-hosts:</span><span class="sxs-lookup"><span data-stu-id="07c72-178">Run the following command on all VMM hosts:</span></span>

```

marsagentinstaller.exe /q /nu

```


## <a name="step-7-configure-cloud-protection-settings"></a><span data-ttu-id="07c72-179">Stap 7: Cloud configureren beveiligingsinstellingen</span><span class="sxs-lookup"><span data-stu-id="07c72-179">Step 7: Configure cloud protection settings</span></span>
1. <span data-ttu-id="07c72-180">Een profiel van de beveiliging cloud naar Azure maken met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="07c72-180">Create a cloud protection profile to Azure by running the following command:</span></span>

   ```

   $ReplicationFrequencyInSeconds = "300";
   $ProfileResult = New-AzureSiteRecoveryProtectionProfileObject -ReplicationProvider HyperVReplica -RecoveryAzureSubscription $AzureSubscriptionName -RecoveryAzureStorageAccount $StorageAccountName -ReplicationFrequencyInSeconds     $ReplicationFrequencyInSeconds;

   ```
2. <span data-ttu-id="07c72-181">Een beveiligingscontainer ophalen met de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="07c72-181">Get a protection container by running the following commands:</span></span>

   ```

   $PrimaryCloud = "testcloud"
   $protectionContainer = Get-AzureSiteRecoveryProtectionContainer -Name $PrimaryCloud;

   ```
3. <span data-ttu-id="07c72-182">De koppeling van de beveiligingscontainer beginnen met de cloud:</span><span class="sxs-lookup"><span data-stu-id="07c72-182">Start the association of the protection container with the cloud:</span></span>

   ```

   $associationJob = Start-AzureSiteRecoveryProtectionProfileAssociationJob -ProtectionProfile $profileResult -PrimaryProtectionContainer $protectionContainer;        

   ```
4. <span data-ttu-id="07c72-183">Nadat de taak is voltooid, voert u de volgende opdracht uit:</span><span class="sxs-lookup"><span data-stu-id="07c72-183">After the job has finished, run the following command:</span></span>

        $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
        if($job -eq $null -or $job.StateDescription -ne "Completed")
        {
        $isJobLeftForProcessing = $true;
        }


1. <span data-ttu-id="07c72-184">Wanneer de verwerking van de taak is voltooid, kunt u de volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="07c72-184">After the job has finished processing, run the following command:</span></span>

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



<span data-ttu-id="07c72-185">Volg de stappen in om te zien wanneer de bewerking is voltooid, [Monitoractiviteit](#monitor).</span><span class="sxs-lookup"><span data-stu-id="07c72-185">To check the completion of the operation, follow the steps in [Monitor Activity](#monitor).</span></span>

## <a name="step-8-configure-network-mapping"></a><span data-ttu-id="07c72-186">Stap 8: Netwerktoewijzing configureren</span><span class="sxs-lookup"><span data-stu-id="07c72-186">Step 8: Configure network mapping</span></span>
<span data-ttu-id="07c72-187">Controleer voordat u met de netwerktoewijzing begint of de virtuele machines op de bron-VMM-server zijn verbonden met een VM-netwerk.</span><span class="sxs-lookup"><span data-stu-id="07c72-187">Before you begin network mapping verify that virtual machines on the source VMM server are connected to a VM network.</span></span> <span data-ttu-id="07c72-188">Daarnaast maakt u een of meer virtuele netwerken in Azure.</span><span class="sxs-lookup"><span data-stu-id="07c72-188">In addition, create one or more Azure virtual networks.</span></span> <span data-ttu-id="07c72-189">Er kunnen meerdere VM-netwerken worden toegewezen aan één Azure-netwerk.</span><span class="sxs-lookup"><span data-stu-id="07c72-189">Note that multiple VM networks can be mapped to a single Azure network.</span></span>

<span data-ttu-id="07c72-190">Als het doelnetwerk meerdere subnetten heeft en een van deze subnetten dezelfde naam heeft als het subnet waarin de virtuele bronmachine zich bevindt, wordt de gerepliceerde virtuele machine na een failover verbonden met dat doelsubnet.</span><span class="sxs-lookup"><span data-stu-id="07c72-190">Note that if the target network has multiple subnets and one of those subnets has the same name as subnet on which the source virtual machine is located, then the replica virtual machine will be connected to that target subnet after failover.</span></span> <span data-ttu-id="07c72-191">Als er geen een Doelsubnet met een overeenkomende naam beschikbaar is, wordt de virtuele machine verbonden met het eerste subnet in het netwerk.</span><span class="sxs-lookup"><span data-stu-id="07c72-191">If there is not a target subnet with a matching name, the virtual machine will be connected to the first subnet in the network.</span></span>

<span data-ttu-id="07c72-192">De eerste opdracht haalt servers voor de huidige Azure Site Recovery-kluis.</span><span class="sxs-lookup"><span data-stu-id="07c72-192">The first command gets servers for the current Azure Site Recovery vault.</span></span> <span data-ttu-id="07c72-193">De opdracht slaat de Microsoft Azure Site Recovery-servers in de $Servers matrixvariabele.</span><span class="sxs-lookup"><span data-stu-id="07c72-193">The command stores the Microsoft Azure Site Recovery servers in the $Servers array variable.</span></span>

    $Servers = Get-AzureSiteRecoveryServer


<span data-ttu-id="07c72-194">De tweede opdracht wordt de site recovery-netwerk opgehaald voor de eerste server in de matrix $Servers.</span><span class="sxs-lookup"><span data-stu-id="07c72-194">The second command gets the site recovery network for the first server in the $Servers array.</span></span> <span data-ttu-id="07c72-195">De opdracht worden de netwerken in de variabele $Networks opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="07c72-195">The command stores the networks in the $Networks variable.</span></span>

    $Networks = Get-AzureSiteRecoveryNetwork -Server $Servers[0]

<span data-ttu-id="07c72-196">De derde opdracht uw Azure-abonnementen opgehaald met de cmdlet Get-AzureSubscription en slaat vervolgens die waarde in de variabele $Subscriptions.</span><span class="sxs-lookup"><span data-stu-id="07c72-196">The third command gets your Azure subscriptions by using the Get-AzureSubscription cmdlet, and then stores that value in the $Subscriptions variable.</span></span>

    $Subscriptions = Get-AzureSubscription



<span data-ttu-id="07c72-197">De vierde opdracht haalt virtuele netwerken in Azure met behulp van de cmdlet Get-AzureVNetSite en dat de waarde in de variabele $AzureVmNetworks.</span><span class="sxs-lookup"><span data-stu-id="07c72-197">The fourth command gets Azure virtual networks by using the Get-AzureVNetSite cmdlet, and then that value in the $AzureVmNetworks variable.</span></span>

    $AzureVmNetworks = Get-AzureVNetSite



<span data-ttu-id="07c72-198">De laatste cmdlet maakt een toewijzing tussen het primaire netwerk en de virtuele machine van Azure-netwerk.</span><span class="sxs-lookup"><span data-stu-id="07c72-198">The final cmdlet creates a mapping between the primary network and the Azure virtual machine network.</span></span> <span data-ttu-id="07c72-199">De cmdlet geeft het primaire netwerk als het eerste element van $Networks.</span><span class="sxs-lookup"><span data-stu-id="07c72-199">The cmdlet specifies the primary network as the first element of $Networks.</span></span> <span data-ttu-id="07c72-200">De cmdlet geeft een VM-netwerk als het eerste element van $AzureVmNetworks met behulp van de-ID.</span><span class="sxs-lookup"><span data-stu-id="07c72-200">The cmdlet specifies a virtual machine network as the first element of $AzureVmNetworks by using its ID.</span></span> <span data-ttu-id="07c72-201">De opdracht bevat uw Azure-abonnement-ID.</span><span class="sxs-lookup"><span data-stu-id="07c72-201">The command includes your Azure subscription ID.</span></span>

    New-AzureSiteRecoveryNetworkMapping -PrimaryNetwork $Networks[0] -AzureSubscriptionId $Subscriptions[0].SubscriptionId -AzureVMNetworkId $AzureVmNetworks[0].Id


## <a name="step-9-enable-protection-for-virtual-machines"></a><span data-ttu-id="07c72-202">Stap 9: Beveiliging voor virtuele machines inschakelen</span><span class="sxs-lookup"><span data-stu-id="07c72-202">Step 9: Enable protection for virtual machines</span></span>
<span data-ttu-id="07c72-203">Wanneer de servers, clouds en netwerken correct zijn geconfigureerd, kunt u beveiliging voor virtuele machines in de cloud inschakelen.</span><span class="sxs-lookup"><span data-stu-id="07c72-203">After servers, clouds, and networks are configured correctly, you can enable protection for virtual machines in the cloud.</span></span> <span data-ttu-id="07c72-204">Houd rekening met het volgende:</span><span class="sxs-lookup"><span data-stu-id="07c72-204">Note the following:</span></span>

<span data-ttu-id="07c72-205">Virtuele machines moeten voldoen aan [vereisten van de virtuele machine van Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="07c72-205">Virtual machines must meet [Azure virtual machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

<span data-ttu-id="07c72-206">Als u beveiliging wilt inschakelen, moeten het besturingssysteem en de schijfeigenschappen van het besturingssysteem zijn ingesteld voor de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="07c72-206">To enable protection the operating system and operating system disk properties must be set for the virtual machine.</span></span> <span data-ttu-id="07c72-207">Wanneer u een virtuele machine in VMM maakt met een sjabloon voor een virtuele machine, kunt u de eigenschap instellen.</span><span class="sxs-lookup"><span data-stu-id="07c72-207">When you create a virtual machine in VMM using a virtual machine template you can set the property.</span></span> <span data-ttu-id="07c72-208">U kunt deze eigenschappen ook voor bestaande virtuele machines instellen op de tabbladen **Algemeen** en **Hardwareconfiguratie** van de eigenschappen van de virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="07c72-208">You can also set these properties for existing virtual machines on the **General** and **Hardware Configuration** tabs of the virtual machine properties.</span></span> <span data-ttu-id="07c72-209">Als u deze eigenschappen niet in VMM instelt, kunt u ze configureren in de Azure Site Recovery-portal.</span><span class="sxs-lookup"><span data-stu-id="07c72-209">If you don't set these properties in VMM you'll be able to configure them in the Azure Site Recovery portal.</span></span>

1. <span data-ttu-id="07c72-210">Als beveiliging wilt inschakelen, voer de volgende opdracht om op te halen van de beveiligingscontainer:</span><span class="sxs-lookup"><span data-stu-id="07c72-210">To enable protection, run the following command to get the protection container:</span></span>

     <span data-ttu-id="07c72-211">$ProtectionContainer = get-AzureSiteRecoveryProtectionContainer-$CloudName naam</span><span class="sxs-lookup"><span data-stu-id="07c72-211">$ProtectionContainer = Get-AzureSiteRecoveryProtectionContainer -Name $CloudName</span></span>
2. <span data-ttu-id="07c72-212">De entiteit beveiliging (VM) ophalen met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="07c72-212">Get the protection entity (VM) by running the following command:</span></span>

        $protectionEntity = Get-AzureSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer



1. <span data-ttu-id="07c72-213">De DR voor de virtuele machine inschakelen met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="07c72-213">Enable the DR for the VM by running the following command:</span></span>

        $jobResult = Set-AzureSiteRecoveryProtectionEntity -ProtectionEntity $protectionEntity     -Protection Enable -Force



## <a name="test-your-deployment"></a><span data-ttu-id="07c72-214">Uw implementatie testen</span><span class="sxs-lookup"><span data-stu-id="07c72-214">Test your deployment</span></span>
<span data-ttu-id="07c72-215">Als uw implementatie wilt testen kunt u een testfailover voor één virtuele machine, uitvoeren of een herstelplan dat bestaat uit meerdere virtuele machines maken en een testfailover voor het plan uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="07c72-215">To test your deployment you can run a test failover for a single virtual machine, or create a recovery plan consisting of multiple virtual machines and run a test failover for the plan.</span></span> <span data-ttu-id="07c72-216">Met een testfailover wordt uw failover- en herstelmechanisme in een geïsoleerd netwerk gesimuleerd.</span><span class="sxs-lookup"><span data-stu-id="07c72-216">Test failover simulates your failover and recovery mechanism in an isolated network.</span></span> <span data-ttu-id="07c72-217">Houd rekening met het volgende:</span><span class="sxs-lookup"><span data-stu-id="07c72-217">Note that:</span></span>

* <span data-ttu-id="07c72-218">Als u na de failover verbinding wilt maken met de virtuele machine in Azure met Extern bureaublad, schakelt u Verbinding met extern bureaublad in op de virtuele machine voordat u de testfailover uitvoert.</span><span class="sxs-lookup"><span data-stu-id="07c72-218">If you want to connect to the virtual machine in Azure using Remote Desktop after the failover, enable Remote Desktop Connection on the virtual machine before you run the test failover.</span></span>
* <span data-ttu-id="07c72-219">Na een failover gebruikt u een openbaar IP-adres verbinding maken met de virtuele machine in Azure met extern bureaublad.</span><span class="sxs-lookup"><span data-stu-id="07c72-219">After failover, you'll use a public IP address to connect to the virtual machine in Azure using Remote Desktop.</span></span> <span data-ttu-id="07c72-220">Als u dit wilt doen, zorgt u ervoor dat u geen domeinbeleid hebt waarmee het verbinden met een virtuele machine via een openbaar adres wordt verhinderd.</span><span class="sxs-lookup"><span data-stu-id="07c72-220">If you want to do this, ensure you don't have any domain policies that prevent you from connecting to a virtual machine using a public address.</span></span>

<span data-ttu-id="07c72-221">Volg de stappen in om te zien wanneer de bewerking is voltooid, [Monitoractiviteit](#monitor).</span><span class="sxs-lookup"><span data-stu-id="07c72-221">To check the completion of the operation, follow the steps in [Monitor Activity](#monitor).</span></span>

### <a name="create-a-recovery-plan"></a><span data-ttu-id="07c72-222">Een herstelplan maken</span><span class="sxs-lookup"><span data-stu-id="07c72-222">Create a recovery plan</span></span>
1. <span data-ttu-id="07c72-223">Maak een XML-bestand als een sjabloon voor het herstelplan met behulp van de onderstaande gegevens en vervolgens opslaan als 'C:\RPTemplatePath.xml'.</span><span class="sxs-lookup"><span data-stu-id="07c72-223">Create an .xml file as a template for your recovery plan using the data below, and then save it as "C:\RPTemplatePath.xml".</span></span>
2. <span data-ttu-id="07c72-224">Wijzig de RecoveryPlan knooppunt-Id, naam, PrimaryServerId en SecondaryServerId.</span><span class="sxs-lookup"><span data-stu-id="07c72-224">Change the RecoveryPlan node Id, Name, PrimaryServerId, and SecondaryServerId.</span></span>
3. <span data-ttu-id="07c72-225">Wijzigen van het knooppunt ProtectionEntity PrimaryProtectionEntityId (vmid uit VMM).</span><span class="sxs-lookup"><span data-stu-id="07c72-225">Change the ProtectionEntity node PrimaryProtectionEntityId (vmid from VMM).</span></span>
4. <span data-ttu-id="07c72-226">U kunt meer virtuele machines toevoegen door meer ProtectionEntity knooppunten toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="07c72-226">You can add more VMs by adding more ProtectionEntity nodes.</span></span>

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



1. <span data-ttu-id="07c72-227">Vul in de gegevens in de sjabloon:</span><span class="sxs-lookup"><span data-stu-id="07c72-227">Fill in the data in the template:</span></span>

        $TemplatePath = "C:\RPTemplatePath.xml";



1. <span data-ttu-id="07c72-228">De RecoveryPlan maken:</span><span class="sxs-lookup"><span data-stu-id="07c72-228">Create the RecoveryPlan:</span></span>

        $RPCreationJob = New-AzureSiteRecoveryRecoveryPlan -File $TemplatePath -WaitForCompletion;

### <a name="run-a-test-failover"></a><span data-ttu-id="07c72-229">Een testfailover uitvoeren</span><span class="sxs-lookup"><span data-stu-id="07c72-229">Run a test failover</span></span>
1. <span data-ttu-id="07c72-230">Het object RecoveryPlan ophalen met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="07c72-230">Get the RecoveryPlan object by running the following command:</span></span>

     <span data-ttu-id="07c72-231">$RPObject = get-AzureSiteRecoveryRecoveryPlan-naam $RPName;</span><span class="sxs-lookup"><span data-stu-id="07c72-231">$RPObject = Get-AzureSiteRecoveryRecoveryPlan -Name $RPName;</span></span>
2. <span data-ttu-id="07c72-232">Start de testfailover door het uitvoeren van de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="07c72-232">Start the test failover by running the following command:</span></span>

        $jobIDResult = Start-AzureSiteRecoveryTestFailoverJob -RecoveryPlan $RPObject -Direction PrimaryToRecovery;


## <span data-ttu-id="07c72-233"><a name=monitor></a>Voor Monitoractiviteit</span><span class="sxs-lookup"><span data-stu-id="07c72-233"><a name=monitor></a> Monitor Activity</span></span>
<span data-ttu-id="07c72-234">Gebruik de volgende opdrachten voor het bewaken van de activiteit.</span><span class="sxs-lookup"><span data-stu-id="07c72-234">Use the following commands to monitor the activity.</span></span> <span data-ttu-id="07c72-235">Houd er rekening mee dat u wachten tussen taken voor de verwerking moet te voltooien.</span><span class="sxs-lookup"><span data-stu-id="07c72-235">Note that you have to wait in between jobs for the processing to finish.</span></span>

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



## <a name="next-steps"></a><span data-ttu-id="07c72-236">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="07c72-236">Next steps</span></span>
<span data-ttu-id="07c72-237">[Lees meer](/powershell/azure/overview) over Azure Site Recovery PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="07c72-237">[Read more](/powershell/azure/overview) about Azure Site Recovery PowerShell cmdlets.</span></span> <span data-ttu-id="07c72-238"></a>.</span><span class="sxs-lookup"><span data-stu-id="07c72-238"></a>.</span></span>
