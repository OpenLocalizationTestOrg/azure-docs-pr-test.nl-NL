---
title: Maken van een SQL Server-Machine in Azure PowerShell (Resource Manager) | Microsoft Docs
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
ms.openlocfilehash: aa90a1d017af5f477407ab33f0580904472f412b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="provision-a-sql-server-virtual-machine-using-azure-powershell-resource-manager"></a><span data-ttu-id="12463-103">Inrichten van een SQL Server-virtuele machine met Azure PowerShell (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="12463-103">Provision a SQL Server virtual machine using Azure PowerShell (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="12463-104">Portal</span><span class="sxs-lookup"><span data-stu-id="12463-104">Portal</span></span>](virtual-machines-windows-portal-sql-server-provision.md)
> * [<span data-ttu-id="12463-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="12463-105">PowerShell</span></span>](virtual-machines-windows-ps-sql-create.md)
>
>

## <a name="overview"></a><span data-ttu-id="12463-106">Overzicht</span><span class="sxs-lookup"><span data-stu-id="12463-106">Overview</span></span>
<span data-ttu-id="12463-107">Deze zelfstudie ziet u het maken van een enkele Azure virtuele machine met de **Azure Resource Manager** implementatiemodel met Azure PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="12463-107">This tutorial shows you how to create a single Azure virtual machine using the **Azure Resource Manager** deployment model using Azure PowerShell cmdlets.</span></span> <span data-ttu-id="12463-108">We gaan een enkele virtuele machine met behulp van één schijf station van een installatiekopie in de SQL-galerie maken in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="12463-108">In this tutorial, we will create a single virtual machine using a single disk drive from an image in the SQL Gallery.</span></span> <span data-ttu-id="12463-109">Nieuwe providers voor de opslag-, netwerk- en rekenresources die wordt gebruikt door de virtuele machine u kunt maken.</span><span class="sxs-lookup"><span data-stu-id="12463-109">We will create new providers for the storage, network, and compute resources that will be used by the virtual machine.</span></span> <span data-ttu-id="12463-110">Als u bestaande providers voor een van deze resources hebt, kunt u deze providers in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="12463-110">If you have existing providers for any of these resources, you can use those providers instead.</span></span>

<span data-ttu-id="12463-111">Als u de klassieke versie van dit onderwerp, Zie [een SQL Server-machine met behulp van Azure PowerShell klassieke inrichten](../classic/ps-sql-create.md).</span><span class="sxs-lookup"><span data-stu-id="12463-111">If you need the classic version of this topic, see [Provision a SQL Server virtual machine using Azure PowerShell Classic](../classic/ps-sql-create.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="12463-112">Vereisten</span><span class="sxs-lookup"><span data-stu-id="12463-112">Prerequisites</span></span>
<span data-ttu-id="12463-113">Voor deze zelfstudie hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="12463-113">For this tutorial you'll need:</span></span>

* <span data-ttu-id="12463-114">Een Azure-account en abonnement voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="12463-114">An Azure account and subscription before you start.</span></span> <span data-ttu-id="12463-115">Als u niet hebt, zich aanmelden voor een [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="12463-115">If you don't have one, sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="12463-116">[Azure PowerShell)](/powershell/azure/overview), minimale versie van 1.4.0 of hoger (deze zelfstudie geschreven met behulp van versie 1.5.0).</span><span class="sxs-lookup"><span data-stu-id="12463-116">[Azure PowerShell)](/powershell/azure/overview), minimum version of 1.4.0 or later (this tutorial written using version 1.5.0).</span></span>
  * <span data-ttu-id="12463-117">Voor het ophalen van uw versie, typ **Azure Get-Module - ListAvailable**.</span><span class="sxs-lookup"><span data-stu-id="12463-117">To retrieve your version, type **Get-Module Azure -ListAvailable**.</span></span>

## <a name="configure-your-subscription"></a><span data-ttu-id="12463-118">Configureer uw abonnement</span><span class="sxs-lookup"><span data-stu-id="12463-118">Configure your subscription</span></span>
<span data-ttu-id="12463-119">Open Windows PowerShell en toegang tot uw Azure-account maken door de volgende cmdlet.</span><span class="sxs-lookup"><span data-stu-id="12463-119">Open Windows PowerShell and establish access to your Azure account by running the following cmdlet.</span></span> <span data-ttu-id="12463-120">U krijgt een teken in het scherm uw referenties in te voeren.</span><span class="sxs-lookup"><span data-stu-id="12463-120">You will be presented with a sign in screen to enter your credentials.</span></span> <span data-ttu-id="12463-121">Gebruik dezelfde e-mailadres en wachtwoord dat u aan te melden bij de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="12463-121">Use the same email and password that you use to sign in to the Azure portal.</span></span>

    Add-AzureRmAccount

<span data-ttu-id="12463-122">Na het aanmelden is ziet u enkele gegevens op het scherm met de abonnements-id waarmee u zich hebt aangemeld in.</span><span class="sxs-lookup"><span data-stu-id="12463-122">After successfully signing in you will see some information on screen that includes the SubscriptionId with which you signed in.</span></span> <span data-ttu-id="12463-123">Dit is het abonnement waarin de bronnen voor deze zelfstudie wordt worden gemaakt, tenzij u naar een ander abonnement wijzigen.</span><span class="sxs-lookup"><span data-stu-id="12463-123">This is the subscription in which the resources for this tutorial will be created unless you change to a different subscription.</span></span> <span data-ttu-id="12463-124">Als u meerdere SubscriptionIds hebt, voer de volgende cmdlet voor een lijst van alle uw SubscriptionIds:</span><span class="sxs-lookup"><span data-stu-id="12463-124">If you have multiple SubscriptionIds, run the following cmdlet to return a list of all of your SubscriptionIds:</span></span>

    Get-AzureRmSubscription

<span data-ttu-id="12463-125">Als u wilt een andere abonnements-id, moet u de volgende cmdlet uitvoeren met de gewenste abonnements-id.</span><span class="sxs-lookup"><span data-stu-id="12463-125">To change to another SubscriptionID, run the following cmdlet with your desired SubscriptionId.</span></span>

    Select-AzureRmSubscription -SubscriptionId xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

## <a name="define-image-variables"></a><span data-ttu-id="12463-126">Definieer de installatiekopie van variabelen</span><span class="sxs-lookup"><span data-stu-id="12463-126">Define image variables</span></span>
<span data-ttu-id="12463-127">Om te vereenvoudigen bruikbaarheid van en kennis van de voltooide script uit deze zelfstudie, wordt we gestart door een aantal variabelen definiëren.</span><span class="sxs-lookup"><span data-stu-id="12463-127">To simplify usability and understanding of the completed script from this tutorial, we will start by defining a number of variables.</span></span> <span data-ttu-id="12463-128">Wijzig de parameterwaarden zoals u dat wilt, maar pas op voor de naamgeving van beperkingen met betrekking tot de naam van lengten en speciale tekens bij het wijzigen van de opgegeven waarden.</span><span class="sxs-lookup"><span data-stu-id="12463-128">Change the parameter values as you see fit, but beware of naming restrictions related to name lengths and special characters when modifying the values provided.</span></span>

### <a name="location-and-resource-group"></a><span data-ttu-id="12463-129">Locatie en resourcegroep</span><span class="sxs-lookup"><span data-stu-id="12463-129">Location and Resource Group</span></span>
<span data-ttu-id="12463-130">Twee variabelen gebruiken voor het definiëren van het gegevensgebied en de resourcegroep waarin u de andere bronnen voor de virtuele machine maakt.</span><span class="sxs-lookup"><span data-stu-id="12463-130">Use two variables to define the data region and the resource group into which you will create the other resources for the virtual machine.</span></span>

<span data-ttu-id="12463-131">Naar wens wijzigen en vervolgens de volgende cmdlets voor het initialiseren van deze variabelen wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="12463-131">Modify as desired and then execute the following cmdlets to initialize these variables.</span></span>

    $Location = "SouthCentralUS"
    $ResourceGroupName = "sqlvm1"

### <a name="storage-properties"></a><span data-ttu-id="12463-132">Eigenschappen van opslag</span><span class="sxs-lookup"><span data-stu-id="12463-132">Storage properties</span></span>
<span data-ttu-id="12463-133">De volgende variabelen gebruiken voor het definiëren van de storage-account en het type opslag moet worden gebruikt door de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="12463-133">Use the following variables to define the storage account and the type of storage to be used by the virtual machine.</span></span>

<span data-ttu-id="12463-134">Naar wens wijzigen en vervolgens de volgende cmdlet om te initialiseren van deze variabelen wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="12463-134">Modify as desired and then execute the following cmdlet to initialize these variables.</span></span> <span data-ttu-id="12463-135">Houd er rekening mee dat in dit voorbeeld we gebruiken [Premium-opslag](../../../storage/common/storage-premium-storage.md), wat wordt aanbevolen voor productieworkloads.</span><span class="sxs-lookup"><span data-stu-id="12463-135">Note that in this example, we are using [Premium Storage](../../../storage/common/storage-premium-storage.md), which is recommended for production workloads.</span></span> <span data-ttu-id="12463-136">Zie voor meer informatie over deze richtlijnen en andere aanbevelingen [best practices prestaties for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-performance.md).</span><span class="sxs-lookup"><span data-stu-id="12463-136">For details on this guidance and other recommendations, see [Performance best practices for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-performance.md).</span></span>

    $StorageName = $ResourceGroupName + "storage"
    $StorageSku = "Premium_LRS"

### <a name="network-properties"></a><span data-ttu-id="12463-137">Eigenschappen van het netwerk</span><span class="sxs-lookup"><span data-stu-id="12463-137">Network properties</span></span>
<span data-ttu-id="12463-138">De volgende variabelen gebruiken voor het definiëren van de netwerkinterface, de TCP/IP-toewijzingsmethode, naam van het virtuele netwerk, de naam van de virtuele subnet, het bereik van IP-adressen voor het virtuele netwerk, het bereik van IP-adressen voor het subnet en het openbare domein-naamlabel moet worden gebruikt door het netwerk in de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="12463-138">Use the following variables to define the network interface, the TCP/IP allocation method, the virtual network name, the virtual subnet name, the range of IP addresses for the virtual network, the range of IP addresses for the subnet, and the public domain name label to be used by the network in the virtual machine.</span></span>

<span data-ttu-id="12463-139">Naar wens wijzigen en vervolgens de volgende cmdlet om te initialiseren van deze variabelen wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="12463-139">Modify as desired and then execute the following cmdlet to initialize these variables.</span></span>

    $InterfaceName = $ResourceGroupName + "ServerInterface"
    $TCPIPAllocationMethod = "Dynamic"
    $VNetName = $ResourceGroupName + "VNet"
    $SubnetName = "Default"
    $VNetAddressPrefix = "10.0.0.0/16"
    $VNetSubnetAddressPrefix = "10.0.0.0/24"
    $DomainName = "sqlvm1"

### <a name="virtual-machine-properties"></a><span data-ttu-id="12463-140">Eigenschappen van virtuele machine</span><span class="sxs-lookup"><span data-stu-id="12463-140">Virtual machine properties</span></span>
<span data-ttu-id="12463-141">De volgende variabelen gebruiken voor het definiëren van de naam van de virtuele machine, de computernaam, de grootte van de virtuele machine en de naam van de besturingssysteem-schijf voor de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="12463-141">Use the following variables to define the virtual machine name, the computer name, the virtual machine size, and the operating system disk name for the virtual machine.</span></span>

<span data-ttu-id="12463-142">Naar wens wijzigen en vervolgens de volgende cmdlet om te initialiseren van deze variabelen wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="12463-142">Modify as desired and then execute the following cmdlet to initialize these variables.</span></span>

    $VMName = $ResourceGroupName + "VM"
    $ComputerName = $ResourceGroupName + "Server"
    $VMSize = "Standard_DS13"
    $OSDiskName = $VMName + "OSDisk"

### <a name="image-properties"></a><span data-ttu-id="12463-143">Eigenschappen van de installatiekopie</span><span class="sxs-lookup"><span data-stu-id="12463-143">Image properties</span></span>
<span data-ttu-id="12463-144">De volgende variabelen gebruiken voor het definiëren van de afbeelding moet worden gebruikt voor de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="12463-144">Use the following variables to define the image to use for the virtual machine.</span></span> <span data-ttu-id="12463-145">In dit voorbeeld wordt de installatiekopie van het SQL Server 2016 Enterprise gebruikt.</span><span class="sxs-lookup"><span data-stu-id="12463-145">In this example, the SQL Server 2016 Enterprise image is used.</span></span>

<span data-ttu-id="12463-146">Naar wens wijzigen en vervolgens de volgende cmdlet om te initialiseren van deze variabelen wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="12463-146">Modify as desired and then execute the following cmdlet to initialize these variables.</span></span>

    $PublisherName = "MicrosoftSQLServer"
    $OfferName = "SQL2016-WS2016"
    $Sku = "Enterprise"
    $Version = "latest"

<span data-ttu-id="12463-147">Houd er rekening mee dat u een volledige lijst met aanbiedingen van SQL Server-installatiekopie met de opdracht Get-AzureRmVMImageOffer kunt krijgen:</span><span class="sxs-lookup"><span data-stu-id="12463-147">Note that you can get a full list of SQL Server image offerings with the Get-AzureRmVMImageOffer command:</span></span>

    Get-AzureRmVMImageOffer -Location 'East US' -Publisher 'MicrosoftSQLServer'

<span data-ttu-id="12463-148">En u ziet de SKU's die beschikbaar zijn voor een aanbieding met de opdracht Get-AzureRmVMImageSku.</span><span class="sxs-lookup"><span data-stu-id="12463-148">And you can see the Skus available for an offering with the Get-AzureRmVMImageSku command.</span></span> <span data-ttu-id="12463-149">De volgende opdracht toont alle SKU's beschikbaar zijn voor de **SQL2014SP1 WS2012R2** bieden.</span><span class="sxs-lookup"><span data-stu-id="12463-149">The following command shows all Skus available for the **SQL2014SP1-WS2012R2** offer.</span></span>

    Get-AzureRmVMImageSku -Location 'East US' -Publisher 'MicrosoftSQLServer' -Offer 'SQL2014SP1-WS2012R2' | Select Skus

## <a name="create-a-resource-group"></a><span data-ttu-id="12463-150">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="12463-150">Create a resource group</span></span>
<span data-ttu-id="12463-151">Met het Resource Manager-implementatiemodel is het eerste object die u maakt de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="12463-151">With the Resource Manager deployment model, the first object that you create is the resource group.</span></span> <span data-ttu-id="12463-152">We gebruiken de [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet voor het maken van een Azure-resourcegroep en de bijbehorende resources met de naam van een resourcegroep en locatie die is gedefinieerd door de variabelen die u eerder is geïnitialiseerd.</span><span class="sxs-lookup"><span data-stu-id="12463-152">We will use the [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet to create an Azure resource group and its resources with the resource group name and location defined by the variables that you previously initialized.</span></span>

<span data-ttu-id="12463-153">Voer de volgende cmdlet als u wilt maken van uw nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="12463-153">Execute the following cmdlet to create your new resource group.</span></span>

    New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Location

## <a name="create-a-storage-account"></a><span data-ttu-id="12463-154">Een opslagaccount maken</span><span class="sxs-lookup"><span data-stu-id="12463-154">Create a storage account</span></span>
<span data-ttu-id="12463-155">De virtuele machine vereist storage-resources voor de besturingssysteemschijf en voor de SQL Server-gegevens en logboekbestanden.</span><span class="sxs-lookup"><span data-stu-id="12463-155">The virtual machine requires storage resources for the operating system disk and for the SQL Server data and log files.</span></span> <span data-ttu-id="12463-156">Voor eenvoud, u kunt één schijf maken voor beide.</span><span class="sxs-lookup"><span data-stu-id="12463-156">For simplicity, we will create a single disk for both.</span></span> <span data-ttu-id="12463-157">U kunt extra schijven koppelen later via de [toevoegen Azure-schijf](/powershell/module/azure/add-azuredisk) cmdlet om te kunnen plaatsen van uw SQL Server-gegevens en logboekbestanden op schijven met specifieke bestanden.</span><span class="sxs-lookup"><span data-stu-id="12463-157">You can attach additional disks later using the [Add-Azure Disk](/powershell/module/azure/add-azuredisk) cmdlet in order to place your SQL Server data and log files on dedicated disks.</span></span> <span data-ttu-id="12463-158">We gebruiken de [nieuw AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet een standard-opslag-account maken in uw nieuwe resourcegroep en met de naam van het opslagaccount, opslag Sku-naam en locatie die is gedefinieerd met behulp van de variabelen die u eerder is geïnitialiseerd.</span><span class="sxs-lookup"><span data-stu-id="12463-158">We will use the [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet to create a standard storage account in your new resource group and with the storage account name, storage Sku name, and location defined using the variables that you previously initialized.</span></span>

<span data-ttu-id="12463-159">De volgende cmdlet als u wilt maken van uw nieuwe opslagaccount worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="12463-159">Execute the following cmdlet to create your new storage account.</span></span>

    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageName -SkuName $StorageSku -Kind "Storage" -Location $Location

## <a name="create-network-resources"></a><span data-ttu-id="12463-160">Maken van netwerkbronnen</span><span class="sxs-lookup"><span data-stu-id="12463-160">Create network resources</span></span>
<span data-ttu-id="12463-161">De virtuele machine vereist een aantal netwerkbronnen voor verbinding met het netwerk.</span><span class="sxs-lookup"><span data-stu-id="12463-161">The virtual machine requires a number of network resources for network connectivity.</span></span>

* <span data-ttu-id="12463-162">Elke virtuele machine vereist een virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="12463-162">Each virtual machine requires a virtual network.</span></span>
* <span data-ttu-id="12463-163">Een virtueel netwerk moet ten minste één subnet dat is gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="12463-163">A virtual network must have at least one subnet defined.</span></span>
* <span data-ttu-id="12463-164">Een netwerkinterface moet worden gedefinieerd met een openbare of een particulier IP-adres.</span><span class="sxs-lookup"><span data-stu-id="12463-164">A network interface must be defined with either a public or a private IP address.</span></span>

### <a name="create-a-virtual-network-subnet-configuration"></a><span data-ttu-id="12463-165">Een virtueel netwerk subnetconfiguratie maken</span><span class="sxs-lookup"><span data-stu-id="12463-165">Create a virtual network subnet configuration</span></span>
<span data-ttu-id="12463-166">Er wordt gestart door het maken van de subnetconfiguratie van een voor het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="12463-166">We will start by creating a subnet configuration for our virtual network.</span></span> <span data-ttu-id="12463-167">In deze zelfstudie maken we een standaard subnet met de [nieuw AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="12463-167">For our tutorial, we will create a default subnet using the [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) cmdlet.</span></span> <span data-ttu-id="12463-168">We gaan onze subnetconfiguratie virtueel netwerk maken met de naam en adres subnetvoorvoegsel gedefinieerd met behulp van de variabelen die u eerder is geïnitialiseerd.</span><span class="sxs-lookup"><span data-stu-id="12463-168">We will create our virtual network subnet configuration with the subnet name and address prefix defined using the variables that you previously initialized.</span></span>

> [!NOTE]
> <span data-ttu-id="12463-169">U kunt aanvullende eigenschappen van de configuratie van het virtuele netwerk subnet met deze cmdlet definiëren, maar dat is buiten het bereik van deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="12463-169">You can define additional properties of the virtual network subnet configuration using this cmdlet, but that is beyond the scope of this tutorial.</span></span>
>
>

<span data-ttu-id="12463-170">De volgende cmdlet als u wilt maken van uw virtuele subnet-configuratie worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="12463-170">Execute the following cmdlet to create your virtual subnet configuration.</span></span>

    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $SubnetName -AddressPrefix $VNetSubnetAddressPrefix

### <a name="create-a-virtual-network"></a><span data-ttu-id="12463-171">Een virtueel netwerk maken</span><span class="sxs-lookup"><span data-stu-id="12463-171">Create a virtual network</span></span>
<span data-ttu-id="12463-172">Vervolgens maken we onze virtueel netwerk met behulp van de [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="12463-172">Next, we will create our virtual network using the [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) cmdlet.</span></span> <span data-ttu-id="12463-173">We gaan het virtuele netwerk in uw nieuwe resourcegroep maken, met de naam, de locatie en het adres voorvoegsel gedefinieerd met behulp van de variabelen die u eerder is geïnitialiseerd en de subnet-configuratie die u hebt gedefinieerd in de vorige stap.</span><span class="sxs-lookup"><span data-stu-id="12463-173">We will create our virtual network in your new resource group, with the name, location, and address prefix defined using the variables that you previously initialized, and using the subnet configuration that you defined in the previous step.</span></span>

<span data-ttu-id="12463-174">De volgende cmdlet als u wilt maken van het virtuele netwerk worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="12463-174">Execute the following cmdlet to create your virtual network.</span></span>

    $VNet = New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName -Location $Location -AddressPrefix $VNetAddressPrefix -Subnet $SubnetConfig

### <a name="create-the-public-ip-address"></a><span data-ttu-id="12463-175">Het openbare IP-adres maken</span><span class="sxs-lookup"><span data-stu-id="12463-175">Create the public IP address</span></span>
<span data-ttu-id="12463-176">Nu we hebben onze virtueel netwerk is gedefinieerd, moet er een IP-adres configureren voor verbinding met de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="12463-176">Now that we have our virtual network defined, we need to configure an IP address for connectivity to the virtual machine.</span></span> <span data-ttu-id="12463-177">We gaan een openbaar IP-adres met behulp van dynamische IP-adressen ter ondersteuning van verbinding met Internet maken voor deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="12463-177">For this tutorial, we will create a public IP address using dynamic IP addressing to support Internet connectivity.</span></span> <span data-ttu-id="12463-178">We gebruiken de [nieuw AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) cmdlet voor het maken van het openbare IP-adres in de groep gemaakt resource prevously en met de naam, locatie, toewijzingsmethode en DNS-domeinnaamlabel gedefinieerd met behulp van de variabelen die u eerder is geïnitialiseerd.</span><span class="sxs-lookup"><span data-stu-id="12463-178">We will use the [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) cmdlet to create the public IP address in the resource group created prevously and with the name, location, allocation method, and DNS domain name label defined using the variables that you previously initialized.</span></span>

> [!NOTE]
> <span data-ttu-id="12463-179">U kunt aanvullende eigenschappen van het openbare IP-adres met behulp van deze cmdlet definiëren, maar dat is buiten het bereik van deze eerste zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="12463-179">You can define additional properties of the public IP address using this cmdlet, but that is beyond the scope of this initial tutorial.</span></span> <span data-ttu-id="12463-180">U kunt ook een persoonlijk adres of een adres maken met een statisch adres, maar die ook is buiten het bereik van deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="12463-180">You could also create a private address or an address with a static address, but that is also beyond the scope of this tutorial.</span></span>
>
>

<span data-ttu-id="12463-181">Voer de volgende cmdlet als u wilt maken van uw openbare IP-adres.</span><span class="sxs-lookup"><span data-stu-id="12463-181">Execute the following cmdlet to create your public IP address.</span></span>

    $PublicIp = New-AzureRmPublicIpAddress -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -AllocationMethod $TCPIPAllocationMethod -DomainNameLabel $DomainName

### <a name="create-the-network-interface"></a><span data-ttu-id="12463-182">De netwerkinterface maken</span><span class="sxs-lookup"><span data-stu-id="12463-182">Create the network interface</span></span>
<span data-ttu-id="12463-183">Er zijn nu gereed voor het maken van de netwerkinterface die de virtuele machine wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="12463-183">We are now ready to create the network interface that our virtual machine will use.</span></span> <span data-ttu-id="12463-184">We gebruiken de [nieuw AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) cmdlet onze netwerkinterface maken in de resourcegroep die eerder hebt gemaakt en met de naam, locatie, subnet en openbaar IP-adres dat eerder is gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="12463-184">We will use the [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) cmdlet to create our network interface in the resource group created earlier and with the name, location, subnet and public IP address previously defined.</span></span>

<span data-ttu-id="12463-185">De volgende cmdlet als u wilt maken van de netwerkinterface worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="12463-185">Execute the following cmdlet to create your network interface.</span></span>

    $Interface = New-AzureRmNetworkInterface -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -SubnetId $VNet.Subnets[0].Id -PublicIpAddressId $PublicIp.Id

## <a name="configure-a-vm-object"></a><span data-ttu-id="12463-186">Een VM-object configureren</span><span class="sxs-lookup"><span data-stu-id="12463-186">Configure a VM object</span></span>
<span data-ttu-id="12463-187">Nu dat we hebben een opslag- en netwerkbronnen die zijn gedefinieerd, zijn er klaar voor het definiëren van rekenresources voor de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="12463-187">Now that we have storage and network resources defined, we are ready to define compute resources for the virtual machine.</span></span> <span data-ttu-id="12463-188">In deze zelfstudie wordt wij Geef de grootte van de virtuele machine en de verschillende eigenschappen van het besturingssysteem, de netwerkinterface die we eerder hebt gemaakt, blob-opslag te definiëren en geef vervolgens de schijf van het besturingssysteem opgeven.</span><span class="sxs-lookup"><span data-stu-id="12463-188">For our tutorial, we will specify the virtual machine size and various operating system properties, specify the network interface that we previously created, define blob storage, and then specify the operating system disk.</span></span>

### <a name="create-the-vm-object"></a><span data-ttu-id="12463-189">Het VM-object maken</span><span class="sxs-lookup"><span data-stu-id="12463-189">Create the VM object</span></span>
<span data-ttu-id="12463-190">Er wordt gestart door te geven van de grootte van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="12463-190">We will start by specifying the virtual machine size.</span></span> <span data-ttu-id="12463-191">We geven een DS13 voor deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="12463-191">For this tutorial, we are specifying a DS13.</span></span> <span data-ttu-id="12463-192">We gebruiken de [nieuw AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) cmdlet geen object configureerbare virtuele machine maken met de naam en de grootte die is gedefinieerd met behulp van de variabelen die u eerder is geïnitialiseerd.</span><span class="sxs-lookup"><span data-stu-id="12463-192">We will use the [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) cmdlet to create a configurable virtual machine object with the name and size defined using the variables that you previously initialized.</span></span>

<span data-ttu-id="12463-193">De volgende cmdlet als u wilt maken van het object van de virtuele machine worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="12463-193">Execute the following cmdlet to create the virtual machine object.</span></span>

    $VirtualMachine = New-AzureRmVMConfig -VMName $VMName -VMSize $VMSize

### <a name="create-a-credential-object-to-hold-the-name-and-password-for-the-local-administrator-credentials"></a><span data-ttu-id="12463-194">Maken van een referentieobject voor het opslaan van de naam en het wachtwoord voor de lokale administrator-referenties</span><span class="sxs-lookup"><span data-stu-id="12463-194">Create a credential object to hold the name and password for the local administrator credentials</span></span>
<span data-ttu-id="12463-195">Voordat we de eigenschappen van het besturingssysteem voor de virtuele machine instellen kunt, moet de referenties voor het lokale administrator-account als een beveiligde tekenreeks opgeven.</span><span class="sxs-lookup"><span data-stu-id="12463-195">Before we can set the operating system properties for the virtual machine, we need to supply the credentials for the local administrator account as a secure string.</span></span> <span data-ttu-id="12463-196">U kunt dit doen we gebruiken de [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="12463-196">To accomplish this, we will use the [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span></span>

<span data-ttu-id="12463-197">De volgende cmdlet uitvoeren en typ de naam en het wachtwoord moet worden gebruikt voor het lokale administrator-account in de virtuele machine van Windows in het venster Windows PowerShell-referentie.</span><span class="sxs-lookup"><span data-stu-id="12463-197">Execute the following cmdlet and, in the Windows PowerShell credential request window, type the name and password to use for the local administrator account in the Windows virtual machine.</span></span>

    $Credential = Get-Credential -Message "Type the name and password of the local administrator account."

### <a name="set-the-operating-system-properties-for-the-virtual-machine"></a><span data-ttu-id="12463-198">Stel de eigenschappen van het besturingssysteem voor de virtuele machine</span><span class="sxs-lookup"><span data-stu-id="12463-198">Set the operating system properties for the virtual machine</span></span>
<span data-ttu-id="12463-199">We kunnen nu klaar voor het instellen van eigenschappen van het besturingssysteem van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="12463-199">Now we are ready to set the virtual machine's operating system properties.</span></span> <span data-ttu-id="12463-200">We gebruiken de [Set AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) cmdlet in te stellen van het type besturingssysteem als Windows, vereisen de [agent van de virtuele machine](../classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) om te worden geïnstalleerd, opgeven dat de cmdlet mogelijk automatisch bijwerken maakt en stel de naam van de virtuele machine, de computernaam en de referentie die met behulp van de variabelen die u eerder is geïnitialiseerd.</span><span class="sxs-lookup"><span data-stu-id="12463-200">We will use the [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) cmdlet to set the type of operating system as Windows, require the [virtual machine agent](../classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) to be installed, specify that the cmdlet enables auto update and set the virtual machine name, the computer name, and the credential using the variables that you previously initialized.</span></span>

<span data-ttu-id="12463-201">De volgende cmdlet om in te stellen van de eigenschappen van het besturingssysteem voor uw virtuele machine worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="12463-201">Execute the following cmdlet to set the operating system properties for your virtual machine.</span></span>

    $VirtualMachine = Set-AzureRmVMOperatingSystem -VM $VirtualMachine -Windows -ComputerName $ComputerName -Credential $Credential -ProvisionVMAgent -EnableAutoUpdate

### <a name="add-the-network-interface-to-the-virtual-machine"></a><span data-ttu-id="12463-202">Voeg de netwerkinterface op de virtuele machine</span><span class="sxs-lookup"><span data-stu-id="12463-202">Add the network interface to the virtual machine</span></span>
<span data-ttu-id="12463-203">We zullen de netwerkinterface die is gemaakt vervolgens eerder toevoegen aan de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="12463-203">Next, we will add the network interface that we created previously to the virtual machine.</span></span> <span data-ttu-id="12463-204">We gebruiken de [toevoegen AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) cmdlet om toe te voegen van de netwerkinterface met behulp van de network interface-variabele die u eerder hebt gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="12463-204">We will use the [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) cmdlet to add the network interface using the network interface variable that you defined earlier.</span></span>

<span data-ttu-id="12463-205">De volgende cmdlet om in te stellen van de netwerkinterface voor uw virtuele machine worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="12463-205">Execute the following cmdlet to set the network interface for your virtual machine.</span></span>

    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $Interface.Id

### <a name="set-the-blob-storage-location-for-the-disk-to-be-used-by-the-virtual-machine"></a><span data-ttu-id="12463-206">Stel de locatie van de blob-opslag voor de schijf moet worden gebruikt door de virtuele machine</span><span class="sxs-lookup"><span data-stu-id="12463-206">Set the blob storage location for the disk to be used by the virtual machine</span></span>
<span data-ttu-id="12463-207">We Stel vervolgens de blob-opslaglocatie voor de schijf moet worden gebruikt door de virtuele machine met behulp van de variabelen die u eerder hebt gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="12463-207">Next, we will set the blob storage location for the disk to be used by the virtual machine using the variables that you defined earlier.</span></span>

<span data-ttu-id="12463-208">De volgende cmdlet om de locatie van blob storage worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="12463-208">Execute the following cmdlet to set the blob storage location.</span></span>

    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName + ".vhd"

### <a name="set-the-operating-system-disk-properties-for-the-virtual-machine"></a><span data-ttu-id="12463-209">Het besturingssysteem van de eigenschappen van de schijf voor de virtuele machine instellen</span><span class="sxs-lookup"><span data-stu-id="12463-209">Set the operating system disk properties for the virtual machine</span></span>
<span data-ttu-id="12463-210">Vervolgens we wordt het besturingssysteem schijfeigenschappen instellen voor de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="12463-210">Next, we will set the operating system disk properties for the virtual machine.</span></span> <span data-ttu-id="12463-211">We gebruiken de [Set AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk) cmdlet om op te geven dat het besturingssysteem voor de virtuele machine, zijn afkomstig van een afbeelding om in te stellen om alleen-lezen (omdat SQL Server wordt geïnstalleerd op dezelfde schijf) en definieer de naam van de virtuele machine en de besturingssysteemschijf is gedefinieerd met behulp van de variabelen die we eerder hebt gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="12463-211">We will use the [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk) cmdlet to specify that the operating system for the virtual machine will come from an image, to set caching to read only (because SQL Server is being installed on the same disk) and define the virtual machine name and the operating system disk defined using the variables that we defined earlier.</span></span>

<span data-ttu-id="12463-212">De volgende cmdlet voor het instellen van het besturingssysteem schijfeigenschappen voor uw virtuele machine worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="12463-212">Execute the following cmdlet to set the operating system disk properties for your virtual machine.</span></span>

    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -Name $OSDiskName -VhdUri $OSDiskUri -Caching ReadOnly -CreateOption FromImage

### <a name="specify-the-platform-image-for-the-virtual-machine"></a><span data-ttu-id="12463-213">Geef de platforminstallatiekopie voor de virtuele machine</span><span class="sxs-lookup"><span data-stu-id="12463-213">Specify the platform image for the virtual machine</span></span>
<span data-ttu-id="12463-214">Onze laatste stap in de configuratie is de platform-afbeelding voor de virtuele machine opgeven.</span><span class="sxs-lookup"><span data-stu-id="12463-214">Our last configuration step is to specify the platform image for our virtual machine.</span></span> <span data-ttu-id="12463-215">In deze zelfstudie gebruiken we de meest recente SQL Server 2016 CTP-installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="12463-215">For our tutorial, we are using the latest SQL Server 2016 CTP image.</span></span> <span data-ttu-id="12463-216">We gebruiken de [Set AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) cmdlet deze installatiekopie te gebruiken zoals gedefinieerd door de variabelen die u eerder hebt gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="12463-216">We will use the [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) cmdlet to use this image as defined by the variables that you defined earlier.</span></span>

<span data-ttu-id="12463-217">De volgende cmdlet om op te geven van de platforminstallatiekopie voor uw virtuele machine worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="12463-217">Execute the following cmdlet to specify the platform image for your virtual machine.</span></span>

    $VirtualMachine = Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName $PublisherName -Offer $OfferName -Skus $Sku -Version $Version

## <a name="create-the-sql-vm"></a><span data-ttu-id="12463-218">De virtuele machine van SQL maken</span><span class="sxs-lookup"><span data-stu-id="12463-218">Create the SQL VM</span></span>
<span data-ttu-id="12463-219">Nu u de configuratiestappen hebt voltooid, bent u klaar om te maken van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="12463-219">Now that you have finished the configuration steps, you are ready to create the virtual machine.</span></span> <span data-ttu-id="12463-220">We gebruiken de [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) cmdlet voor het maken van de virtuele machine met behulp van de variabelen die we hebt gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="12463-220">We will use the [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) cmdlet to create the virtual machine using the variables that we have defined.</span></span>

<span data-ttu-id="12463-221">De volgende cmdlet als u wilt maken van uw virtuele machine worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="12463-221">Execute the following cmdlet to create your virtual machine.</span></span>

    New-AzureRmVM -ResourceGroupName $ResourceGroupName -Location $Location -VM $VirtualMachine

<span data-ttu-id="12463-222">De virtuele machine wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="12463-222">The virtual machine is created.</span></span> <span data-ttu-id="12463-223">U ziet dat er een standaard opslagaccount voor diagnostische gegevens over opstarten is gemaakt omdat het opgegeven opslagaccount voor de schijf van de virtuele machine een premium-opslagaccount is.</span><span class="sxs-lookup"><span data-stu-id="12463-223">Notice that a standard storage account is created for boot diagnostics because the specified storage account for the virtual machine's disk is a premium storage account.</span></span>

<span data-ttu-id="12463-224">U kunt nu deze machine weergeven in de Azure-Portal om te zien [het openbare IP-adres en de volledig gekwalificeerde domeinnaam](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="12463-224">You can now view this machine in the Azure Portal to see [its public IP address and its fully qualified domain name](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

## <a name="example-script"></a><span data-ttu-id="12463-225">Voorbeeldscript</span><span class="sxs-lookup"><span data-stu-id="12463-225">Example script</span></span>
<span data-ttu-id="12463-226">Het volgende script bevat de volledige PowerShell-script voor deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="12463-226">The following script contains the complete PowerShell script for this tutorial.</span></span> <span data-ttu-id="12463-227">Er wordt vanuit gegaan dat u al ingesteld hebt voor gebruik met de Azure-abonnement de **Add-AzureRmAccount** en **Select-AzureRmSubscription** opdrachten.</span><span class="sxs-lookup"><span data-stu-id="12463-227">It assumes that you have already setup the Azure subscription to use with the **Add-AzureRmAccount** and **Select-AzureRmSubscription** commands.</span></span>

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
    $Credential = Get-Credential -Message "Type the name and password of the local administrator account."
    $VirtualMachine = Set-AzureRmVMOperatingSystem -VM $VirtualMachine -Windows -ComputerName $ComputerName -Credential $Credential -ProvisionVMAgent -EnableAutoUpdate #-TimeZone = $TimeZone
    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $Interface.Id
    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName + ".vhd"
    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -Name $OSDiskName -VhdUri $OSDiskUri -Caching ReadOnly -CreateOption FromImage

    # Image
    $VirtualMachine = Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName $PublisherName -Offer $OfferName -Skus $Sku -Version $Version

    ## Create the VM in Azure
    New-AzureRmVM -ResourceGroupName $ResourceGroupName -Location $Location -VM $VirtualMachine

## <a name="next-steps"></a><span data-ttu-id="12463-228">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="12463-228">Next steps</span></span>
<span data-ttu-id="12463-229">Nadat de virtuele machine is gemaakt, bent u klaar om te verbinden met de virtuele machine met RDP en setup connectiviteit.</span><span class="sxs-lookup"><span data-stu-id="12463-229">After the virtual machine is created, you are ready to connect to the virtual machine using RDP and setup connectivity.</span></span> <span data-ttu-id="12463-230">Zie voor meer informatie [Connect op een virtuele Machine in Azure (Resource Manager) van SQL Server](virtual-machines-windows-sql-connect.md).</span><span class="sxs-lookup"><span data-stu-id="12463-230">For more information, see [Connect to a SQL Server Virtual Machine on Azure (Resource Manager)](virtual-machines-windows-sql-connect.md).</span></span>

