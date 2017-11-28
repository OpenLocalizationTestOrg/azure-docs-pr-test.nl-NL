---
title: aaaCreate een SQL Server-Machine in Azure PowerShell (Resource Manager) | Microsoft Docs
description: "Bevat de stappen en PowerShell-scripts voor het maken van een virtuele machine in Azure met SQL Server-installatiekopieën voor virtuele machine-galerie."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: 98d50dd8-48ad-444f-9031-5378d8270d7b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/17/2017
ms.author: jroth
ms.openlocfilehash: 2b8cb8f69ff9894a95eab617816a60c8674eeefa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="provision-a-sql-server-virtual-machine-using-azure-powershell-resource-manager"></a><span data-ttu-id="6c24e-103">Inrichten van een SQL Server-virtuele machine met Azure PowerShell (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="6c24e-103">Provision a SQL Server virtual machine using Azure PowerShell (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6c24e-104">Portal</span><span class="sxs-lookup"><span data-stu-id="6c24e-104">Portal</span></span>](virtual-machines-windows-portal-sql-server-provision.md)
> * [<span data-ttu-id="6c24e-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6c24e-105">PowerShell</span></span>](virtual-machines-windows-ps-sql-create.md)
>
>

## <a name="overview"></a><span data-ttu-id="6c24e-106">Overzicht</span><span class="sxs-lookup"><span data-stu-id="6c24e-106">Overview</span></span>
<span data-ttu-id="6c24e-107">Deze zelfstudie laat zien hoe een enkele virtuele machine van Azure met toocreate Hallo **Azure Resource Manager** implementatiemodel met Azure PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="6c24e-107">This tutorial shows you how toocreate a single Azure virtual machine using hello **Azure Resource Manager** deployment model using Azure PowerShell cmdlets.</span></span> <span data-ttu-id="6c24e-108">We gaan een enkele virtuele machine met een enkele schijf van een installatiekopie in Hallo SQL-galerie maken in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="6c24e-108">In this tutorial, we will create a single virtual machine using a single disk drive from an image in hello SQL Gallery.</span></span> <span data-ttu-id="6c24e-109">Nieuwe providers voor Hallo-opslag-, netwerk- en rekenresources die wordt gebruikt door Hallo virtuele machine u kunt maken.</span><span class="sxs-lookup"><span data-stu-id="6c24e-109">We will create new providers for hello storage, network, and compute resources that will be used by hello virtual machine.</span></span> <span data-ttu-id="6c24e-110">Als u bestaande providers voor een van deze resources hebt, kunt u deze providers in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="6c24e-110">If you have existing providers for any of these resources, you can use those providers instead.</span></span>

<span data-ttu-id="6c24e-111">Als u de klassieke versie van dit onderwerp moet hello, Zie [een SQL Server-machine met behulp van Azure PowerShell klassieke inrichten](../classic/ps-sql-create.md).</span><span class="sxs-lookup"><span data-stu-id="6c24e-111">If you need hello classic version of this topic, see [Provision a SQL Server virtual machine using Azure PowerShell Classic](../classic/ps-sql-create.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6c24e-112">Vereisten</span><span class="sxs-lookup"><span data-stu-id="6c24e-112">Prerequisites</span></span>
<span data-ttu-id="6c24e-113">Voor deze zelfstudie hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="6c24e-113">For this tutorial you'll need:</span></span>

* <span data-ttu-id="6c24e-114">Een Azure-account en abonnement voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="6c24e-114">An Azure account and subscription before you start.</span></span> <span data-ttu-id="6c24e-115">Als u niet hebt, zich aanmelden voor een [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6c24e-115">If you don't have one, sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="6c24e-116">[Azure PowerShell)](/powershell/azure/overview), minimale versie van 1.4.0 of hoger (deze zelfstudie geschreven met behulp van versie 1.5.0).</span><span class="sxs-lookup"><span data-stu-id="6c24e-116">[Azure PowerShell)](/powershell/azure/overview), minimum version of 1.4.0 or later (this tutorial written using version 1.5.0).</span></span>
  * <span data-ttu-id="6c24e-117">tooretrieve uw versie, het type **Azure Get-Module - ListAvailable**.</span><span class="sxs-lookup"><span data-stu-id="6c24e-117">tooretrieve your version, type **Get-Module Azure -ListAvailable**.</span></span>

## <a name="configure-your-subscription"></a><span data-ttu-id="6c24e-118">Configureer uw abonnement</span><span class="sxs-lookup"><span data-stu-id="6c24e-118">Configure your subscription</span></span>
<span data-ttu-id="6c24e-119">Open Windows PowerShell en toegang tooyour Azure-account maken door het uitvoeren van de volgende cmdlet Hallo.</span><span class="sxs-lookup"><span data-stu-id="6c24e-119">Open Windows PowerShell and establish access tooyour Azure account by running hello following cmdlet.</span></span> <span data-ttu-id="6c24e-120">U krijgt een teken in het scherm tooenter uw referenties.</span><span class="sxs-lookup"><span data-stu-id="6c24e-120">You will be presented with a sign in screen tooenter your credentials.</span></span> <span data-ttu-id="6c24e-121">Gebruik dezelfde Hallo e-mailadres en wachtwoord toosign in toohello Azure-portal te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6c24e-121">Use hello same email and password that you use toosign in toohello Azure portal.</span></span>

    Add-AzureRmAccount

<span data-ttu-id="6c24e-122">Na het aanmelden is ziet u enkele gegevens op het scherm met Hallo abonnements-id waarmee u zich hebt aangemeld in.</span><span class="sxs-lookup"><span data-stu-id="6c24e-122">After successfully signing in you will see some information on screen that includes hello SubscriptionId with which you signed in.</span></span> <span data-ttu-id="6c24e-123">Dit is Hallo abonnement waarin Hallo bronnen voor deze zelfstudie worden gemaakt tenzij u een ander abonnement tooa wijzigt.</span><span class="sxs-lookup"><span data-stu-id="6c24e-123">This is hello subscription in which hello resources for this tutorial will be created unless you change tooa different subscription.</span></span> <span data-ttu-id="6c24e-124">Als u meerdere SubscriptionIds hebt, Voer Hallo cmdlet tooreturn na een lijst met alle uw SubscriptionIds:</span><span class="sxs-lookup"><span data-stu-id="6c24e-124">If you have multiple SubscriptionIds, run hello following cmdlet tooreturn a list of all of your SubscriptionIds:</span></span>

    Get-AzureRmSubscription

<span data-ttu-id="6c24e-125">toochange tooanother SubscriptionID, uitvoeren van de volgende cmdlet uit met de gewenste SubscriptionId Hallo.</span><span class="sxs-lookup"><span data-stu-id="6c24e-125">toochange tooanother SubscriptionID, run hello following cmdlet with your desired SubscriptionId.</span></span>

    Select-AzureRmSubscription -SubscriptionId xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

## <a name="define-image-variables"></a><span data-ttu-id="6c24e-126">Definieer de installatiekopie van variabelen</span><span class="sxs-lookup"><span data-stu-id="6c24e-126">Define image variables</span></span>
<span data-ttu-id="6c24e-127">toosimplify bruikbaarheid van en kennis van het script uit deze zelfstudie Hallo voltooid, wordt begin met het definiëren van een aantal variabelen.</span><span class="sxs-lookup"><span data-stu-id="6c24e-127">toosimplify usability and understanding of hello completed script from this tutorial, we will start by defining a number of variables.</span></span> <span data-ttu-id="6c24e-128">Het wijzigen van de parameterwaarden Hallo zoals u dat wilt, maar pas op voor de naamgeving beperkingen gerelateerde tooname lengten en speciale tekens bij het wijzigen van Hallo waarden.</span><span class="sxs-lookup"><span data-stu-id="6c24e-128">Change hello parameter values as you see fit, but beware of naming restrictions related tooname lengths and special characters when modifying hello values provided.</span></span>

### <a name="location-and-resource-group"></a><span data-ttu-id="6c24e-129">Locatie en resourcegroep</span><span class="sxs-lookup"><span data-stu-id="6c24e-129">Location and Resource Group</span></span>
<span data-ttu-id="6c24e-130">Gebruik twee variabelen toodefine Hallo gegevens regio en Hallo resourcegroep waarin u Hallo andere bronnen voor Hallo virtuele machine maakt.</span><span class="sxs-lookup"><span data-stu-id="6c24e-130">Use two variables toodefine hello data region and hello resource group into which you will create hello other resources for hello virtual machine.</span></span>

<span data-ttu-id="6c24e-131">Desgewenst wijzigen en vervolgens deze variabelen uitgevoerd Hallo cmdlets tooinitialize te volgen.</span><span class="sxs-lookup"><span data-stu-id="6c24e-131">Modify as desired and then execute hello following cmdlets tooinitialize these variables.</span></span>

    $Location = "SouthCentralUS"
    $ResourceGroupName = "sqlvm1"

### <a name="storage-properties"></a><span data-ttu-id="6c24e-132">Eigenschappen van opslag</span><span class="sxs-lookup"><span data-stu-id="6c24e-132">Storage properties</span></span>
<span data-ttu-id="6c24e-133">Gebruik hello variabelen toodefine Hallo-account en Hallo opslagtype van opslag toobe gebruikt door Hallo virtuele machine te volgen.</span><span class="sxs-lookup"><span data-stu-id="6c24e-133">Use hello following variables toodefine hello storage account and hello type of storage toobe used by hello virtual machine.</span></span>

<span data-ttu-id="6c24e-134">Desgewenst wijzigen en vervolgens deze variabelen uitgevoerd Hallo cmdlet tooinitialize te volgen.</span><span class="sxs-lookup"><span data-stu-id="6c24e-134">Modify as desired and then execute hello following cmdlet tooinitialize these variables.</span></span> <span data-ttu-id="6c24e-135">Houd er rekening mee dat in dit voorbeeld we gebruiken [Premium-opslag](../../../storage/common/storage-premium-storage.md), wat wordt aanbevolen voor productieworkloads.</span><span class="sxs-lookup"><span data-stu-id="6c24e-135">Note that in this example, we are using [Premium Storage](../../../storage/common/storage-premium-storage.md), which is recommended for production workloads.</span></span> <span data-ttu-id="6c24e-136">Zie voor meer informatie over deze richtlijnen en andere aanbevelingen [best practices prestaties for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-performance.md).</span><span class="sxs-lookup"><span data-stu-id="6c24e-136">For details on this guidance and other recommendations, see [Performance best practices for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-performance.md).</span></span>

    $StorageName = $ResourceGroupName + "storage"
    $StorageSku = "Premium_LRS"

### <a name="network-properties"></a><span data-ttu-id="6c24e-137">Eigenschappen van het netwerk</span><span class="sxs-lookup"><span data-stu-id="6c24e-137">Network properties</span></span>
<span data-ttu-id="6c24e-138">Hallo na variabelen toodefine Hallo netwerkinterface, Hallo TCP/IP-toewijzingsmethode, Hallo virtuele-netwerknaam, Hallo virtuele subnet-naam, Hallo bereik van IP-adressen voor het virtuele netwerk hello, Hallo bereik van IP-adressen voor het Hallo-subnet en hello gebruiken openbare domein naam label toobe gebruikt door Hallo-netwerk in Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="6c24e-138">Use hello following variables toodefine hello network interface, hello TCP/IP allocation method, hello virtual network name, hello virtual subnet name, hello range of IP addresses for hello virtual network, hello range of IP addresses for hello subnet, and hello public domain name label toobe used by hello network in hello virtual machine.</span></span>

<span data-ttu-id="6c24e-139">Desgewenst wijzigen en vervolgens deze variabelen uitgevoerd Hallo cmdlet tooinitialize te volgen.</span><span class="sxs-lookup"><span data-stu-id="6c24e-139">Modify as desired and then execute hello following cmdlet tooinitialize these variables.</span></span>

    $InterfaceName = $ResourceGroupName + "ServerInterface"
    $TCPIPAllocationMethod = "Dynamic"
    $VNetName = $ResourceGroupName + "VNet"
    $SubnetName = "Default"
    $VNetAddressPrefix = "10.0.0.0/16"
    $VNetSubnetAddressPrefix = "10.0.0.0/24"
    $DomainName = "sqlvm1"

### <a name="virtual-machine-properties"></a><span data-ttu-id="6c24e-140">Eigenschappen van virtuele machine</span><span class="sxs-lookup"><span data-stu-id="6c24e-140">Virtual machine properties</span></span>
<span data-ttu-id="6c24e-141">Gebruik hello variabelen toodefine Hallo virtuele-machinenaam, Hallo computernaam, de grootte van de virtuele machine Hallo en Hallo besturingssysteem schijfnaam voor Hallo virtuele machine te volgen.</span><span class="sxs-lookup"><span data-stu-id="6c24e-141">Use hello following variables toodefine hello virtual machine name, hello computer name, hello virtual machine size, and hello operating system disk name for hello virtual machine.</span></span>

<span data-ttu-id="6c24e-142">Desgewenst wijzigen en vervolgens deze variabelen uitgevoerd Hallo cmdlet tooinitialize te volgen.</span><span class="sxs-lookup"><span data-stu-id="6c24e-142">Modify as desired and then execute hello following cmdlet tooinitialize these variables.</span></span>

    $VMName = $ResourceGroupName + "VM"
    $ComputerName = $ResourceGroupName + "Server"
    $VMSize = "Standard_DS13"
    $OSDiskName = $VMName + "OSDisk"

### <a name="image-properties"></a><span data-ttu-id="6c24e-143">Eigenschappen van de installatiekopie</span><span class="sxs-lookup"><span data-stu-id="6c24e-143">Image properties</span></span>
<span data-ttu-id="6c24e-144">Gebruik hello variabelen toodefine Hallo installatiekopie toouse voor Hallo virtuele machine te volgen.</span><span class="sxs-lookup"><span data-stu-id="6c24e-144">Use hello following variables toodefine hello image toouse for hello virtual machine.</span></span> <span data-ttu-id="6c24e-145">In dit voorbeeld wordt Hallo SQL Server 2016 Enterprise afbeelding gebruikt.</span><span class="sxs-lookup"><span data-stu-id="6c24e-145">In this example, hello SQL Server 2016 Enterprise image is used.</span></span>

<span data-ttu-id="6c24e-146">Desgewenst wijzigen en vervolgens deze variabelen uitgevoerd Hallo cmdlet tooinitialize te volgen.</span><span class="sxs-lookup"><span data-stu-id="6c24e-146">Modify as desired and then execute hello following cmdlet tooinitialize these variables.</span></span>

    $PublisherName = "MicrosoftSQLServer"
    $OfferName = "SQL2016-WS2016"
    $Sku = "Enterprise"
    $Version = "latest"

<span data-ttu-id="6c24e-147">Houd er rekening mee dat u een volledige lijst met aanbiedingen van SQL Server-installatiekopie met de opdracht Get-AzureRmVMImageOffer Hallo kunt krijgen:</span><span class="sxs-lookup"><span data-stu-id="6c24e-147">Note that you can get a full list of SQL Server image offerings with hello Get-AzureRmVMImageOffer command:</span></span>

    Get-AzureRmVMImageOffer -Location 'East US' -Publisher 'MicrosoftSQLServer'

<span data-ttu-id="6c24e-148">En u Hallo SKU's die beschikbaar zijn voor een aanbieding met de opdracht Get-AzureRmVMImageSku Hallo kunt zien.</span><span class="sxs-lookup"><span data-stu-id="6c24e-148">And you can see hello Skus available for an offering with hello Get-AzureRmVMImageSku command.</span></span> <span data-ttu-id="6c24e-149">Hallo volgende opdracht toont alle SKU's beschikbaar voor Hallo **SQL2014SP1 WS2012R2** bieden.</span><span class="sxs-lookup"><span data-stu-id="6c24e-149">hello following command shows all Skus available for hello **SQL2014SP1-WS2012R2** offer.</span></span>

    Get-AzureRmVMImageSku -Location 'East US' -Publisher 'MicrosoftSQLServer' -Offer 'SQL2014SP1-WS2012R2' | Select Skus

## <a name="create-a-resource-group"></a><span data-ttu-id="6c24e-150">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="6c24e-150">Create a resource group</span></span>
<span data-ttu-id="6c24e-151">Met Hallo Resource Manager-implementatiemodel is het eerste Hallo-object dat u maakt Hallo resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="6c24e-151">With hello Resource Manager deployment model, hello first object that you create is hello resource group.</span></span> <span data-ttu-id="6c24e-152">We gebruiken Hallo [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet toocreate een Azure-resourcegroep en de bijbehorende bronnen met Hallo resource groepsnaam en de locatie die is gedefinieerd door het Hallo-variabelen die u eerder is geïnitialiseerd.</span><span class="sxs-lookup"><span data-stu-id="6c24e-152">We will use hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet toocreate an Azure resource group and its resources with hello resource group name and location defined by hello variables that you previously initialized.</span></span>

<span data-ttu-id="6c24e-153">Hallo cmdlet toocreate na uw nieuwe resourcegroep uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="6c24e-153">Execute hello following cmdlet toocreate your new resource group.</span></span>

    New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Location

## <a name="create-a-storage-account"></a><span data-ttu-id="6c24e-154">Een opslagaccount maken</span><span class="sxs-lookup"><span data-stu-id="6c24e-154">Create a storage account</span></span>
<span data-ttu-id="6c24e-155">Hallo virtuele machine vereist storage-resources voor de besturingssysteemschijf Hallo en Hallo SQL Server-gegevens en logboekbestanden.</span><span class="sxs-lookup"><span data-stu-id="6c24e-155">hello virtual machine requires storage resources for hello operating system disk and for hello SQL Server data and log files.</span></span> <span data-ttu-id="6c24e-156">Voor eenvoud, u kunt één schijf maken voor beide.</span><span class="sxs-lookup"><span data-stu-id="6c24e-156">For simplicity, we will create a single disk for both.</span></span> <span data-ttu-id="6c24e-157">U kunt extra schijven met behulp van Hallo bijvoegen [toevoegen Azure-schijf](/powershell/module/azure/add-azuredisk) cmdlet in volgorde tooplace uw SQL Server-gegevens en logboekbestanden op de speciale schijven.</span><span class="sxs-lookup"><span data-stu-id="6c24e-157">You can attach additional disks later using hello [Add-Azure Disk](/powershell/module/azure/add-azuredisk) cmdlet in order tooplace your SQL Server data and log files on dedicated disks.</span></span> <span data-ttu-id="6c24e-158">We gebruiken Hallo [nieuw AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet toocreate een standard-opslag-account in uw nieuwe resourcegroep en met Hallo opslagaccountnaam opslag Sku-naam en locatie die is gedefinieerd met behulp van Hallo variabelen die u hebt eerder is geïnitialiseerd.</span><span class="sxs-lookup"><span data-stu-id="6c24e-158">We will use hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet toocreate a standard storage account in your new resource group and with hello storage account name, storage Sku name, and location defined using hello variables that you previously initialized.</span></span>

<span data-ttu-id="6c24e-159">Hallo cmdlet toocreate na uw nieuwe opslagaccount uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="6c24e-159">Execute hello following cmdlet toocreate your new storage account.</span></span>

    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageName -SkuName $StorageSku -Kind "Storage" -Location $Location

## <a name="create-network-resources"></a><span data-ttu-id="6c24e-160">Maken van netwerkbronnen</span><span class="sxs-lookup"><span data-stu-id="6c24e-160">Create network resources</span></span>
<span data-ttu-id="6c24e-161">Hallo virtuele machine vereist een aantal netwerkbronnen voor verbinding met het netwerk.</span><span class="sxs-lookup"><span data-stu-id="6c24e-161">hello virtual machine requires a number of network resources for network connectivity.</span></span>

* <span data-ttu-id="6c24e-162">Elke virtuele machine vereist een virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="6c24e-162">Each virtual machine requires a virtual network.</span></span>
* <span data-ttu-id="6c24e-163">Een virtueel netwerk moet ten minste één subnet dat is gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="6c24e-163">A virtual network must have at least one subnet defined.</span></span>
* <span data-ttu-id="6c24e-164">Een netwerkinterface moet worden gedefinieerd met een openbare of een particulier IP-adres.</span><span class="sxs-lookup"><span data-stu-id="6c24e-164">A network interface must be defined with either a public or a private IP address.</span></span>

### <a name="create-a-virtual-network-subnet-configuration"></a><span data-ttu-id="6c24e-165">Een virtueel netwerk subnetconfiguratie maken</span><span class="sxs-lookup"><span data-stu-id="6c24e-165">Create a virtual network subnet configuration</span></span>
<span data-ttu-id="6c24e-166">Er wordt gestart door het maken van de subnetconfiguratie van een voor het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="6c24e-166">We will start by creating a subnet configuration for our virtual network.</span></span> <span data-ttu-id="6c24e-167">In deze zelfstudie maken we een standaard-subnet met Hallo [nieuw AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6c24e-167">For our tutorial, we will create a default subnet using hello [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) cmdlet.</span></span> <span data-ttu-id="6c24e-168">We gaan onze subnetconfiguratie virtueel netwerk maken met de Hallo naam en adres subnetvoorvoegsel gedefinieerd met behulp van Hallo variabelen die u eerder is geïnitialiseerd.</span><span class="sxs-lookup"><span data-stu-id="6c24e-168">We will create our virtual network subnet configuration with hello subnet name and address prefix defined using hello variables that you previously initialized.</span></span>

> [!NOTE]
> <span data-ttu-id="6c24e-169">U kunt aanvullende eigenschappen van Hallo subnetconfiguratie voor virtueel netwerk met behulp van deze cmdlet definiëren, maar dat is buiten bereik Hallo van deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="6c24e-169">You can define additional properties of hello virtual network subnet configuration using this cmdlet, but that is beyond hello scope of this tutorial.</span></span>
>
>

<span data-ttu-id="6c24e-170">Hallo cmdlet toocreate na de configuratie van uw virtuele subnet uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="6c24e-170">Execute hello following cmdlet toocreate your virtual subnet configuration.</span></span>

    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $SubnetName -AddressPrefix $VNetSubnetAddressPrefix

### <a name="create-a-virtual-network"></a><span data-ttu-id="6c24e-171">Een virtueel netwerk maken</span><span class="sxs-lookup"><span data-stu-id="6c24e-171">Create a virtual network</span></span>
<span data-ttu-id="6c24e-172">Vervolgens maken we onze virtueel netwerk met behulp van Hallo [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6c24e-172">Next, we will create our virtual network using hello [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) cmdlet.</span></span> <span data-ttu-id="6c24e-173">We maakt onze virtueel netwerk in uw nieuwe resourcegroep met Hallo-naam, locatie en adresvoorvoegsel gedefinieerd met Hallo variabelen die u eerder is geïnitialiseerd, en Hallo subnetten configureren die u hebt gedefinieerd in de vorige stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="6c24e-173">We will create our virtual network in your new resource group, with hello name, location, and address prefix defined using hello variables that you previously initialized, and using hello subnet configuration that you defined in hello previous step.</span></span>

<span data-ttu-id="6c24e-174">Hallo cmdlet toocreate na het virtuele netwerk uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="6c24e-174">Execute hello following cmdlet toocreate your virtual network.</span></span>

    $VNet = New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName -Location $Location -AddressPrefix $VNetAddressPrefix -Subnet $SubnetConfig

### <a name="create-hello-public-ip-address"></a><span data-ttu-id="6c24e-175">Hallo openbare IP-adres maken</span><span class="sxs-lookup"><span data-stu-id="6c24e-175">Create hello public IP address</span></span>
<span data-ttu-id="6c24e-176">Nu dat we onze virtueel netwerk is gedefinieerd hebben, moeten we tooconfigure een IP-adres voor de connectiviteit toohello virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="6c24e-176">Now that we have our virtual network defined, we need tooconfigure an IP address for connectivity toohello virtual machine.</span></span> <span data-ttu-id="6c24e-177">We gaan een openbaar IP-adres met behulp van dynamische IP-adressen voor toosupport verbinding met Internet maken voor deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="6c24e-177">For this tutorial, we will create a public IP address using dynamic IP addressing toosupport Internet connectivity.</span></span> <span data-ttu-id="6c24e-178">We gebruiken Hallo [nieuw AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) cmdlet toocreate Hallo openbaar IP-adres in Hallo resource gemaakte groep prevously en met het Hallo-naam, locatie, toewijzingsmethode en DNS-domeinnaamlabel gedefinieerd met behulp van Hallo variabelen die u eerder is geïnitialiseerd.</span><span class="sxs-lookup"><span data-stu-id="6c24e-178">We will use hello [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) cmdlet toocreate hello public IP address in hello resource group created prevously and with hello name, location, allocation method, and DNS domain name label defined using hello variables that you previously initialized.</span></span>

> [!NOTE]
> <span data-ttu-id="6c24e-179">U kunt aanvullende eigenschappen Hallo openbare IP-adres met behulp van deze cmdlet definiëren, maar dat is buiten bereik van deze zelfstudie initiële Hallo.</span><span class="sxs-lookup"><span data-stu-id="6c24e-179">You can define additional properties of hello public IP address using this cmdlet, but that is beyond hello scope of this initial tutorial.</span></span> <span data-ttu-id="6c24e-180">U kunt ook een persoonlijk adres of een adres maken met een statisch adres, maar die ook is buiten bereik Hallo van deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="6c24e-180">You could also create a private address or an address with a static address, but that is also beyond hello scope of this tutorial.</span></span>
>
>

<span data-ttu-id="6c24e-181">Hallo cmdlet toocreate na uw openbare IP-adres uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="6c24e-181">Execute hello following cmdlet toocreate your public IP address.</span></span>

    $PublicIp = New-AzureRmPublicIpAddress -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -AllocationMethod $TCPIPAllocationMethod -DomainNameLabel $DomainName

### <a name="create-hello-network-interface"></a><span data-ttu-id="6c24e-182">Hallo-netwerkinterface maken</span><span class="sxs-lookup"><span data-stu-id="6c24e-182">Create hello network interface</span></span>
<span data-ttu-id="6c24e-183">Er zijn nu gereed toocreate Hallo netwerkinterface die de virtuele machine wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="6c24e-183">We are now ready toocreate hello network interface that our virtual machine will use.</span></span> <span data-ttu-id="6c24e-184">We gebruiken Hallo [nieuw AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) cmdlet toocreate onze netwerkinterface in resourcegroep Hallo eerder hebt gemaakt en met Hallo-naam, locatie, subnet en openbaar IP-adres is eerder gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="6c24e-184">We will use hello [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) cmdlet toocreate our network interface in hello resource group created earlier and with hello name, location, subnet and public IP address previously defined.</span></span>

<span data-ttu-id="6c24e-185">Hallo cmdlet toocreate na de netwerkinterface uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="6c24e-185">Execute hello following cmdlet toocreate your network interface.</span></span>

    $Interface = New-AzureRmNetworkInterface -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -SubnetId $VNet.Subnets[0].Id -PublicIpAddressId $PublicIp.Id

## <a name="configure-a-vm-object"></a><span data-ttu-id="6c24e-186">Een VM-object configureren</span><span class="sxs-lookup"><span data-stu-id="6c24e-186">Configure a VM object</span></span>
<span data-ttu-id="6c24e-187">Nu dat we hebben een opslag- en netwerkbronnen die zijn gedefinieerd, zijn we klaar toodefine rekenresources voor Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="6c24e-187">Now that we have storage and network resources defined, we are ready toodefine compute resources for hello virtual machine.</span></span> <span data-ttu-id="6c24e-188">In deze zelfstudie wordt we Geef de grootte van de virtuele machine Hallo en verschillende eigenschappen van het besturingssysteem, geef Hallo netwerkinterface die we eerder hebben gemaakt, blob-opslag te definiëren en geef vervolgens de besturingssysteemschijf Hallo.</span><span class="sxs-lookup"><span data-stu-id="6c24e-188">For our tutorial, we will specify hello virtual machine size and various operating system properties, specify hello network interface that we previously created, define blob storage, and then specify hello operating system disk.</span></span>

### <a name="create-hello-vm-object"></a><span data-ttu-id="6c24e-189">Hallo VM-object maken</span><span class="sxs-lookup"><span data-stu-id="6c24e-189">Create hello VM object</span></span>
<span data-ttu-id="6c24e-190">Er wordt gestart door te geven van de grootte van de virtuele machine Hallo.</span><span class="sxs-lookup"><span data-stu-id="6c24e-190">We will start by specifying hello virtual machine size.</span></span> <span data-ttu-id="6c24e-191">We geven een DS13 voor deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="6c24e-191">For this tutorial, we are specifying a DS13.</span></span> <span data-ttu-id="6c24e-192">We gebruiken Hallo [nieuw AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) cmdlet toocreate een object configureerbare virtuele machine met de naam van de Hallo en grootte die is gedefinieerd met behulp van Hallo variabelen die u eerder is geïnitialiseerd.</span><span class="sxs-lookup"><span data-stu-id="6c24e-192">We will use hello [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) cmdlet toocreate a configurable virtual machine object with hello name and size defined using hello variables that you previously initialized.</span></span>

<span data-ttu-id="6c24e-193">Hallo na cmdlet toocreate Hallo virtuele machine-object worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="6c24e-193">Execute hello following cmdlet toocreate hello virtual machine object.</span></span>

    $VirtualMachine = New-AzureRmVMConfig -VMName $VMName -VMSize $VMSize

### <a name="create-a-credential-object-toohold-hello-name-and-password-for-hello-local-administrator-credentials"></a><span data-ttu-id="6c24e-194">Maak een object toohold Hallo referentienaam en het wachtwoord voor de lokale beheerdersreferenties Hallo</span><span class="sxs-lookup"><span data-stu-id="6c24e-194">Create a credential object toohold hello name and password for hello local administrator credentials</span></span>
<span data-ttu-id="6c24e-195">Voordat we Hallo besturingssysteem eigenschappen voor Hallo virtuele machine instellen kunt, moet toosupply Hallo referenties voor de lokale beheerdersaccount Hallo als een beveiligde tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="6c24e-195">Before we can set hello operating system properties for hello virtual machine, we need toosupply hello credentials for hello local administrator account as a secure string.</span></span> <span data-ttu-id="6c24e-196">tooaccomplish, gebruiken we Hallo [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6c24e-196">tooaccomplish this, we will use hello [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span></span>

<span data-ttu-id="6c24e-197">Hallo volgende cmdlet uitvoeren en typ in Hallo Windows PowerShell-referentie venster Hallo naam en het wachtwoord toouse voor Hallo lokale beheerdersaccount in Hallo Windows virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="6c24e-197">Execute hello following cmdlet and, in hello Windows PowerShell credential request window, type hello name and password toouse for hello local administrator account in hello Windows virtual machine.</span></span>

    $Credential = Get-Credential -Message "Type hello name and password of hello local administrator account."

### <a name="set-hello-operating-system-properties-for-hello-virtual-machine"></a><span data-ttu-id="6c24e-198">Hallo besturingssysteem eigenschappen instellen voor Hallo virtuele machine</span><span class="sxs-lookup"><span data-stu-id="6c24e-198">Set hello operating system properties for hello virtual machine</span></span>
<span data-ttu-id="6c24e-199">We kunnen nu de eigenschappen van het besturingssysteem gereed tooset Hallo van virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="6c24e-199">Now we are ready tooset hello virtual machine's operating system properties.</span></span> <span data-ttu-id="6c24e-200">Gebruiken we Hallo [Set AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) cmdlet tooset type besturingssysteem als Windows hello vereisen Hallo [agent van de virtuele machine](../classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) toobe geïnstalleerd, geef die Hallo cmdlet schakelt automatisch bijwerken en naam van de virtuele machine Hallo Hallo computernaam en Hallo referentie Hallo variabelen die u eerder is geïnitialiseerd met instellen.</span><span class="sxs-lookup"><span data-stu-id="6c24e-200">We will use hello [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) cmdlet tooset hello type of operating system as Windows, require hello [virtual machine agent](../classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) toobe installed, specify that hello cmdlet enables auto update and set hello virtual machine name, hello computer name, and hello credential using hello variables that you previously initialized.</span></span>

<span data-ttu-id="6c24e-201">Hallo volgende cmdlet tooset Hallo besturingssysteem eigenschappen voor uw virtuele machine worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="6c24e-201">Execute hello following cmdlet tooset hello operating system properties for your virtual machine.</span></span>

    $VirtualMachine = Set-AzureRmVMOperatingSystem -VM $VirtualMachine -Windows -ComputerName $ComputerName -Credential $Credential -ProvisionVMAgent -EnableAutoUpdate

### <a name="add-hello-network-interface-toohello-virtual-machine"></a><span data-ttu-id="6c24e-202">Hallo network interface toohello virtuele machine toevoegen</span><span class="sxs-lookup"><span data-stu-id="6c24e-202">Add hello network interface toohello virtual machine</span></span>
<span data-ttu-id="6c24e-203">Vervolgens gaat toevoegen we Hallo netwerkinterface dat we eerder toohello virtuele machine gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6c24e-203">Next, we will add hello network interface that we created previously toohello virtual machine.</span></span> <span data-ttu-id="6c24e-204">We gebruiken Hallo [toevoegen AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) cmdlet tooadd Hallo netwerkinterface Hallo network interface-variabele die u eerder hebt gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="6c24e-204">We will use hello [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) cmdlet tooadd hello network interface using hello network interface variable that you defined earlier.</span></span>

<span data-ttu-id="6c24e-205">Hallo volgende cmdlet tooset Hallo netwerkinterface voor uw virtuele machine worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="6c24e-205">Execute hello following cmdlet tooset hello network interface for your virtual machine.</span></span>

    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $Interface.Id

### <a name="set-hello-blob-storage-location-for-hello-disk-toobe-used-by-hello-virtual-machine"></a><span data-ttu-id="6c24e-206">Hallo blob-opslaglocatie voor Hallo schijf toobe gebruikt door Hallo virtuele machine instellen</span><span class="sxs-lookup"><span data-stu-id="6c24e-206">Set hello blob storage location for hello disk toobe used by hello virtual machine</span></span>
<span data-ttu-id="6c24e-207">Vervolgens wordt er stelt Hallo blob-opslaglocatie voor Hallo schijf toobe gebruikt door Hallo virtuele machine met behulp van Hallo variabelen die u eerder hebt gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="6c24e-207">Next, we will set hello blob storage location for hello disk toobe used by hello virtual machine using hello variables that you defined earlier.</span></span>

<span data-ttu-id="6c24e-208">Hallo na locatie voor de cmdlet tooset Hallo blob-opslag uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="6c24e-208">Execute hello following cmdlet tooset hello blob storage location.</span></span>

    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName + ".vhd"

### <a name="set-hello-operating-system-disk-properties-for-hello-virtual-machine"></a><span data-ttu-id="6c24e-209">Hallo-besturingssysteem schijfeigenschappen instellen voor Hallo virtuele machine</span><span class="sxs-lookup"><span data-stu-id="6c24e-209">Set hello operating system disk properties for hello virtual machine</span></span>
<span data-ttu-id="6c24e-210">Vervolgens wordt we ingesteld Hallo besturingssysteem schijfeigenschappen voor Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="6c24e-210">Next, we will set hello operating system disk properties for hello virtual machine.</span></span> <span data-ttu-id="6c24e-211">We hello gebruiken [Set AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk) cmdlet toospecify die Hallo besturingssysteem voor Hallo virtuele machine, zijn afkomstig van een afbeelding, tooset tooread alleen opslaan in cache (omdat SQL Server wordt geïnstalleerd op Hallo dezelfde schijf) en definiëren naam van de virtuele machine Hallo en Hallo besturingssysteemschijf gedefinieerd met behulp van Hallo variabelen die we eerder hebt gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="6c24e-211">We will use hello [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk) cmdlet toospecify that hello operating system for hello virtual machine will come from an image, tooset caching tooread only (because SQL Server is being installed on hello same disk) and define hello virtual machine name and hello operating system disk defined using hello variables that we defined earlier.</span></span>

<span data-ttu-id="6c24e-212">Hallo volgende cmdlet tooset Hallo besturingssysteem schijfeigenschappen voor uw virtuele machine worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="6c24e-212">Execute hello following cmdlet tooset hello operating system disk properties for your virtual machine.</span></span>

    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -Name $OSDiskName -VhdUri $OSDiskUri -Caching ReadOnly -CreateOption FromImage

### <a name="specify-hello-platform-image-for-hello-virtual-machine"></a><span data-ttu-id="6c24e-213">Hallo platforminstallatiekopie voor Hallo virtuele machine opgeven</span><span class="sxs-lookup"><span data-stu-id="6c24e-213">Specify hello platform image for hello virtual machine</span></span>
<span data-ttu-id="6c24e-214">Onze laatste stap in de configuratie is toospecify hello platforminstallatiekopie voor de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="6c24e-214">Our last configuration step is toospecify hello platform image for our virtual machine.</span></span> <span data-ttu-id="6c24e-215">In deze zelfstudie gebruiken we de meest recente SQL Server 2016 CTP installatiekopie Hallo.</span><span class="sxs-lookup"><span data-stu-id="6c24e-215">For our tutorial, we are using hello latest SQL Server 2016 CTP image.</span></span> <span data-ttu-id="6c24e-216">We gebruiken Hallo [Set AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) cmdlet toouse deze installatiekopie zoals gedefinieerd door het Hallo-variabelen die u eerder hebt gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="6c24e-216">We will use hello [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) cmdlet toouse this image as defined by hello variables that you defined earlier.</span></span>

<span data-ttu-id="6c24e-217">Hallo volgende cmdlet toospecify hello platforminstallatiekopie voor uw virtuele machine worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="6c24e-217">Execute hello following cmdlet toospecify hello platform image for your virtual machine.</span></span>

    $VirtualMachine = Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName $PublisherName -Offer $OfferName -Skus $Sku -Version $Version

## <a name="create-hello-sql-vm"></a><span data-ttu-id="6c24e-218">Hallo SQL VM maken</span><span class="sxs-lookup"><span data-stu-id="6c24e-218">Create hello SQL VM</span></span>
<span data-ttu-id="6c24e-219">Nu u Hallo configuratiestappen hebt voltooid, bent u klaar toocreate Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="6c24e-219">Now that you have finished hello configuration steps, you are ready toocreate hello virtual machine.</span></span> <span data-ttu-id="6c24e-220">We gebruiken Hallo [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) cmdlet toocreate Hallo virtuele machine met behulp van Hallo variabelen die we hebt gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="6c24e-220">We will use hello [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) cmdlet toocreate hello virtual machine using hello variables that we have defined.</span></span>

<span data-ttu-id="6c24e-221">Hallo cmdlet toocreate na uw virtuele machine uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="6c24e-221">Execute hello following cmdlet toocreate your virtual machine.</span></span>

    New-AzureRmVM -ResourceGroupName $ResourceGroupName -Location $Location -VM $VirtualMachine

<span data-ttu-id="6c24e-222">Hallo virtuele machine wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6c24e-222">hello virtual machine is created.</span></span> <span data-ttu-id="6c24e-223">U ziet dat er een standaard opslagaccount voor diagnostische gegevens over opstarten is gemaakt omdat Hallo opslagaccount voor schijf Hallo virtuele machine opgegeven is een premium storage-account.</span><span class="sxs-lookup"><span data-stu-id="6c24e-223">Notice that a standard storage account is created for boot diagnostics because hello specified storage account for hello virtual machine's disk is a premium storage account.</span></span>

<span data-ttu-id="6c24e-224">U kunt nu deze machine weergeven in Azure Portal-toosee hello [het openbare IP-adres en de volledig gekwalificeerde domeinnaam](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="6c24e-224">You can now view this machine in hello Azure Portal toosee [its public IP address and its fully qualified domain name](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

## <a name="example-script"></a><span data-ttu-id="6c24e-225">Voorbeeldscript</span><span class="sxs-lookup"><span data-stu-id="6c24e-225">Example script</span></span>
<span data-ttu-id="6c24e-226">Hallo volgende script bevat Hallo voltooid PowerShell-script voor deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="6c24e-226">hello following script contains hello complete PowerShell script for this tutorial.</span></span> <span data-ttu-id="6c24e-227">Wordt ervan uitgegaan dat u hebt al setup hello Azure-abonnement toouse Hello **Add-AzureRmAccount** en **Select-AzureRmSubscription** opdrachten.</span><span class="sxs-lookup"><span data-stu-id="6c24e-227">It assumes that you have already setup hello Azure subscription toouse with hello **Add-AzureRmAccount** and **Select-AzureRmSubscription** commands.</span></span>

    # Variables
    ## Global
    $Location = "SouthCentralUS"
    $ResourceGroupName = "sqlvm1"
    ## Storage
    $StorageName = $ResourceGroupName + "storage"
    $StorageSku = "Premium_LRS"

    ## Network
    $InterfaceName = $ResourceGroupName + "ServerInterface"
    $VNetName = $ResourceGroupName + "VNet"
    $SubnetName = "Default"
    $VNetAddressPrefix = "10.0.0.0/16"
    $VNetSubnetAddressPrefix = "10.0.0.0/24"
    $TCPIPAllocationMethod = "Dynamic"
    $DomainName = "sqlvm1"

    ##Compute
    $VMName = $ResourceGroupName + "VM"
    $ComputerName = $ResourceGroupName + "Server"
    $VMSize = "Standard_DS13"
    $OSDiskName = $VMName + "OSDisk"

    ##Image
    $PublisherName = "MicrosoftSQLServer"
    $OfferName = "SQL2016-WS2016"
    $Sku = "Enterprise"
    $Version = "latest"

    # Resource Group
    New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Location

    # Storage
    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageName -SkuName $StorageSku -Kind "Storage" -Location $Location

    # Network
    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $SubnetName -AddressPrefix $VNetSubnetAddressPrefix
    $VNet = New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName -Location $Location -AddressPrefix $VNetAddressPrefix -Subnet $SubnetConfig
    $PublicIp = New-AzureRmPublicIpAddress -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -AllocationMethod $TCPIPAllocationMethod -DomainNameLabel $DomainName
    $Interface = New-AzureRmNetworkInterface -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -SubnetId $VNet.Subnets[0].Id -PublicIpAddressId $PublicIp.Id

    # Compute
    $VirtualMachine = New-AzureRmVMConfig -VMName $VMName -VMSize $VMSize
    $Credential = Get-Credential -Message "Type hello name and password of hello local administrator account."
    $VirtualMachine = Set-AzureRmVMOperatingSystem -VM $VirtualMachine -Windows -ComputerName $ComputerName -Credential $Credential -ProvisionVMAgent -EnableAutoUpdate #-TimeZone = $TimeZone
    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $Interface.Id
    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName + ".vhd"
    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -Name $OSDiskName -VhdUri $OSDiskUri -Caching ReadOnly -CreateOption FromImage

    # Image
    $VirtualMachine = Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName $PublisherName -Offer $OfferName -Skus $Sku -Version $Version

    ## Create hello VM in Azure
    New-AzureRmVM -ResourceGroupName $ResourceGroupName -Location $Location -VM $VirtualMachine

## <a name="next-steps"></a><span data-ttu-id="6c24e-228">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6c24e-228">Next steps</span></span>
<span data-ttu-id="6c24e-229">Nadat het Hallo virtuele machine is gemaakt, bent u klaar tooconnect toohello virtuele machine met connectiviteit voor RDP en setup opnieuw uit.</span><span class="sxs-lookup"><span data-stu-id="6c24e-229">After hello virtual machine is created, you are ready tooconnect toohello virtual machine using RDP and setup connectivity.</span></span> <span data-ttu-id="6c24e-230">Zie voor meer informatie [verbinding maken met virtuele Machine van SQL Server op Azure (Resource Manager) tooa](virtual-machines-windows-sql-connect.md).</span><span class="sxs-lookup"><span data-stu-id="6c24e-230">For more information, see [Connect tooa SQL Server Virtual Machine on Azure (Resource Manager)](virtual-machines-windows-sql-connect.md).</span></span>

