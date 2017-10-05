---
title: Maken van de basisinfrastructuur in Azure met behulp van Terraform | Microsoft Docs
description: Informatie over het maken van Azure-resources met behulp van Terraform
services: virtual-machines-linux
documentationcenter: virtual-machines
author: echuvyrov
manager: jtalkar
editor: na
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/14/2017
ms.author: echuvyrov
ms.openlocfilehash: 9660a95b440c2e4311829979e270d9f10099f624
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="create-basic-infrastructure-in-azure-by-using-terraform"></a><span data-ttu-id="1588f-103">Maken van de basisinfrastructuur in Azure met behulp van Terraform</span><span class="sxs-lookup"><span data-stu-id="1588f-103">Create basic infrastructure in Azure by using Terraform</span></span>
<span data-ttu-id="1588f-104">In dit artikel beschrijft de stappen die u nemen moet voor het inrichten van een virtuele machine, samen met de onderliggende infrastructuur in Azure.</span><span class="sxs-lookup"><span data-stu-id="1588f-104">This article describes the steps you need to take to provision a virtual machine, together with underlying infrastructure, into Azure.</span></span> <span data-ttu-id="1588f-105">U leert hoe Terraform scripts schrijven en hoe de wijzigingen te visualiseren voordat u ze in uw cloudinfrastructuur.</span><span class="sxs-lookup"><span data-stu-id="1588f-105">You will learn how to write Terraform scripts and how to visualize the changes before you make them in your cloud infrastructure.</span></span> <span data-ttu-id="1588f-106">Ook leert u hoe infrastructuur in Azure maken met behulp van Terraform.</span><span class="sxs-lookup"><span data-stu-id="1588f-106">You also will learn how to create infrastructure in Azure by using Terraform.</span></span>

<span data-ttu-id="1588f-107">Maak een bestand met de naam van \terraform_azure101.tf in een teksteditor naar keuze (Visual Studio Code/Sublime/Vim/enz.) om te beginnen.</span><span class="sxs-lookup"><span data-stu-id="1588f-107">To get started, create a file called \terraform_azure101.tf in your text editor of choice (Visual Studio Code/Sublime/Vim/etc.).</span></span> <span data-ttu-id="1588f-108">De exacte naam van het bestand niet van belang omdat de naam van de map als parameter wordt geaccepteerd Terraform: alle scripts in de map worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="1588f-108">The exact name of the file isn't important because Terraform accepts the folder name as a parameter: all scripts in the folder get executed.</span></span> <span data-ttu-id="1588f-109">Plak de volgende code in het nieuwe bestand:</span><span class="sxs-lookup"><span data-stu-id="1588f-109">Paste the following code in the new file:</span></span>

~~~~
# Configure the Microsoft Azure Provider
# NOTE: if you defined these values as environment variables, you do not have to include this block
provider "azurerm" {
  subscription_id = "your_subscription_id_from_script_execution"
  client_id       = "your_appId_from_script_execution"
  client_secret   = "your_password_from_script_execution"
  tenant_id       = "your_tenant_id_from_script_execution"
}

# create a resource group 
resource "azurerm_resource_group" "helloterraform" {
    name = "terraformtest"
    location = "West US"
}
~~~~
<span data-ttu-id="1588f-110">In de `provider` sectie van het script, geeft u aan Terraform gebruik van een Azure-provider tot inrichten bronnen in het script.</span><span class="sxs-lookup"><span data-stu-id="1588f-110">In the `provider` section of the script, you tell Terraform to use an Azure provider to provision resources in the script.</span></span> <span data-ttu-id="1588f-111">Als u de waarden voor subscription_id, appId, wachtwoord en tenant_id, Zie de [installeren en configureren van Terraform](terraform-install-configure.md) handleiding.</span><span class="sxs-lookup"><span data-stu-id="1588f-111">To get values for subscription_id, appId, password, and tenant_id, see the [Install and configure Terraform](terraform-install-configure.md) guide.</span></span> <span data-ttu-id="1588f-112">Als u omgevingsvariabelen voor de waarden in dit blok hebt gemaakt, moet u niet wilt opnemen.</span><span class="sxs-lookup"><span data-stu-id="1588f-112">If you have created environment variables for the values in this block, you don't need to include it.</span></span> 

<span data-ttu-id="1588f-113">De `azurerm_resource_group` resource Hiermee geeft u Terraform om een nieuwe resourcegroep te maken.</span><span class="sxs-lookup"><span data-stu-id="1588f-113">The `azurerm_resource_group` resource instructs Terraform to create a new resource group.</span></span> <span data-ttu-id="1588f-114">U kunt meer brontypen die beschikbaar in Terraform verderop in dit artikel zijn kunt zien.</span><span class="sxs-lookup"><span data-stu-id="1588f-114">You can see more resource types that are available in Terraform later in this article.</span></span>

## <a name="execute-the-script"></a><span data-ttu-id="1588f-115">Het script uitvoeren</span><span class="sxs-lookup"><span data-stu-id="1588f-115">Execute the script</span></span>
<span data-ttu-id="1588f-116">Nadat u het script opslaat, wordt de console/opdrachtregel sluiten en typ het volgende:</span><span class="sxs-lookup"><span data-stu-id="1588f-116">After you save the script, exit to the console/command line, and type the following:</span></span>
```
terraform init
```
<span data-ttu-id="1588f-117">initialiseren Terraform-provider voor Azure.</span><span class="sxs-lookup"><span data-stu-id="1588f-117">to initialize Terraform provider for Azure.</span></span> <span data-ttu-id="1588f-118">Typ het volgende:</span><span class="sxs-lookup"><span data-stu-id="1588f-118">Then type the following:</span></span>
```
terraform plan terraformscripts
```
<span data-ttu-id="1588f-119">Er wordt ervan uitgegaan dat `terraformscripts` is de map waarin het script is opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="1588f-119">We assume that `terraformscripts` is the folder where the script was saved.</span></span> <span data-ttu-id="1588f-120">We gebruiken de `plan` Terraform-opdracht wordt gekeken naar de resources die zijn gedefinieerd in de scripts.</span><span class="sxs-lookup"><span data-stu-id="1588f-120">We used the `plan` Terraform command, which looks at the resources defined in the scripts.</span></span> <span data-ttu-id="1588f-121">Het vergelijkt ze met de informatie over de opgeslagen door Terraform en vervolgens voert u de geplande uitvoering _zonder_ resources daadwerkelijk maken in Azure.</span><span class="sxs-lookup"><span data-stu-id="1588f-121">It compares them to the state information saved by Terraform and then outputs the planned execution _without_ actually creating resources in Azure.</span></span> 

<span data-ttu-id="1588f-122">Nadat u de vorige opdracht uitvoert, ziet u ongeveer het volgende scherm:</span><span class="sxs-lookup"><span data-stu-id="1588f-122">After you execute the previous command, you should see something like the following screen:</span></span>

![Terraform plannen](linux/media/terraform/tf_plan2.png)

<span data-ttu-id="1588f-124">Als alles er goed uitziet, richt u deze nieuwe resourcegroep in Azure door het uitvoeren van de volgende:</span><span class="sxs-lookup"><span data-stu-id="1588f-124">If everything looks correct, provision this new resource group in Azure by executing the following:</span></span> 
```
terraform apply terraformscripts
```
<span data-ttu-id="1588f-125">In de Azure portal, ziet u de nieuwe lege resourcegroep aangeroepen `terraformtest`.</span><span class="sxs-lookup"><span data-stu-id="1588f-125">In the Azure portal, you should see the new empty resource group called `terraformtest`.</span></span> <span data-ttu-id="1588f-126">In de volgende sectie u een een virtuele machine en de ondersteunende infrastructuur voor die virtuele machine toevoegen aan de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="1588f-126">In the following section, you add a virtual machine and all the supporting infrastructure for that virtual machine to the resource group.</span></span>

## <a name="provision-an-ubuntu-vm-with-terraform"></a><span data-ttu-id="1588f-127">Een virtuele Ubuntu-machine met Terraform inrichten</span><span class="sxs-lookup"><span data-stu-id="1588f-127">Provision an Ubuntu VM with Terraform</span></span>
<span data-ttu-id="1588f-128">Laten we het Terraform script dat we hebt gemaakt met de gegevens die nodig zijn voor het inrichten van een virtuele machine met Ubuntu uitbreiden.</span><span class="sxs-lookup"><span data-stu-id="1588f-128">Let's extend the Terraform script we've created with the details that are necessary to provision a virtual machine running Ubuntu.</span></span> <span data-ttu-id="1588f-129">De bronnen die u in de volgende secties inricht zijn:</span><span class="sxs-lookup"><span data-stu-id="1588f-129">The resources that you provision in the following sections are:</span></span>

* <span data-ttu-id="1588f-130">Een netwerk met één subnet</span><span class="sxs-lookup"><span data-stu-id="1588f-130">A network with a single subnet</span></span>
* <span data-ttu-id="1588f-131">Een netwerkinterfacekaart</span><span class="sxs-lookup"><span data-stu-id="1588f-131">A network interface card</span></span> 
* <span data-ttu-id="1588f-132">Een opslagaccount met storage-container</span><span class="sxs-lookup"><span data-stu-id="1588f-132">A storage account with a storage container</span></span>
* <span data-ttu-id="1588f-133">Een openbaar IP-adres</span><span class="sxs-lookup"><span data-stu-id="1588f-133">A public IP</span></span>
* <span data-ttu-id="1588f-134">Een virtuele machine die gebruikmaakt van de eerdere bronnen</span><span class="sxs-lookup"><span data-stu-id="1588f-134">A virtual machine that utilizes all the previous resources</span></span> 

<span data-ttu-id="1588f-135">Zie voor uitgebreide documentatie voor elk van de resources Azure Terraform de [Terraform documentatie](https://www.terraform.io/docs/providers/azurerm/index.html).</span><span class="sxs-lookup"><span data-stu-id="1588f-135">For thorough documentation for each of the Azure Terraform resources, see the [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).</span></span>

<span data-ttu-id="1588f-136">De volledige versie van de [inrichting script](#complete-terraform-script) is ook voor uw gemak geleverd.</span><span class="sxs-lookup"><span data-stu-id="1588f-136">The full version of the [provisioning script](#complete-terraform-script) is also provided for convenience.</span></span>

### <a name="extend-the-terraform-script"></a><span data-ttu-id="1588f-137">Het script Terraform uitbreiden</span><span class="sxs-lookup"><span data-stu-id="1588f-137">Extend the Terraform script</span></span>
<span data-ttu-id="1588f-138">Uitbreiden van het script dat is gemaakt met de volgende bronnen:</span><span class="sxs-lookup"><span data-stu-id="1588f-138">Extend the script that was created with the following resources:</span></span> 
~~~~
# create a virtual network
resource "azurerm_virtual_network" "helloterraformnetwork" {
    name = "acctvn"
    address_space = ["10.0.0.0/16"]
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
}

# create subnet
resource "azurerm_subnet" "helloterraformsubnet" {
    name = "acctsub"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    virtual_network_name = "${azurerm_virtual_network.helloterraformnetwork.name}"
    address_prefix = "10.0.2.0/24"
}
~~~~
<span data-ttu-id="1588f-139">Het vorige script maakt een virtueel netwerk en een subnet binnen dit virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="1588f-139">The previous script creates a virtual network and a subnet within that virtual network.</span></span> <span data-ttu-id="1588f-140">Noteer de verwijzing naar de resourcegroep die u al hebt gemaakt via "${azurerm_resource_group.helloterraform.name}' in het virtuele netwerk en de subnetdefinitie van.</span><span class="sxs-lookup"><span data-stu-id="1588f-140">Note the reference to the resource group you have created already via "${azurerm_resource_group.helloterraform.name}" in both the virtual network and the subnet definition.</span></span>

~~~~
# create public IP
resource "azurerm_public_ip" "helloterraformips" {
    name = "terraformtestip"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    public_ip_address_allocation = "dynamic"

    tags {
        environment = "TerraformDemo"
    }
}

# create network interface
resource "azurerm_network_interface" "helloterraformnic" {
    name = "tfni"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"

    ip_configuration {
        name = "testconfiguration1"
        subnet_id = "${azurerm_subnet.helloterraformsubnet.id}"
        private_ip_address_allocation = "static"
        private_ip_address = "10.0.2.5"
        public_ip_address_id = "${azurerm_public_ip.helloterraformips.id}"
    }
}
~~~~
<span data-ttu-id="1588f-141">De vorige script codefragmenten maken een openbaar IP-adres en een netwerkinterface die gebruik maakt van het openbare IP-adres gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1588f-141">The previous script snippets create a public IP and a network interface that makes use of the public IP created.</span></span> <span data-ttu-id="1588f-142">Noteer de verwijzingen naar subnet_id en public_ip_address_id.</span><span class="sxs-lookup"><span data-stu-id="1588f-142">Note the references to subnet_id and public_ip_address_id.</span></span> <span data-ttu-id="1588f-143">Terraform beschikt over ingebouwde intelligentie om te begrijpen dat de netwerkinterface afhankelijk is van de resources die moeten worden gemaakt voordat het maken van de netwerkinterface.</span><span class="sxs-lookup"><span data-stu-id="1588f-143">Terraform has built-in intelligence to understand that the network interface has a dependency on the resources that need to be created before the creation of the network interface.</span></span>

~~~~
# create a random id
resource "random_id" "randomId" {
  byte_length = 4
}

# create storage account
resource "azurerm_storage_account" "helloterraformstorage" {
    name                = "tfstorage${random_id.randomId.hex}"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    location = "westus"
    account_type = "Standard_LRS"

    tags {
        environment = "staging"
    }
}

# create storage container
resource "azurerm_storage_container" "helloterraformstoragestoragecontainer" {
    name = "vhd"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    storage_account_name = "${azurerm_storage_account.helloterraformstorage.name}"
    container_access_type = "private"
    depends_on = ["azurerm_storage_account.helloterraformstorage"]
}
~~~~
<span data-ttu-id="1588f-144">Hier kunt u een opslagaccount hebt gemaakt en een storage-container binnen dit opslagaccount wordt gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="1588f-144">Here, you created a storage account and defined a storage container within that storage account.</span></span> <span data-ttu-id="1588f-145">Dit opslagaccount is waar het opslaan van virtuele harde schijven (VHD's) voor de virtuele machine gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1588f-145">This storage account is where you store virtual hard disks (VHDs) for the virtual machine about to be created.</span></span>

~~~~
# create virtual machine
resource "azurerm_virtual_machine" "helloterraformvm" {
    name = "terraformvm"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    network_interface_ids = ["${azurerm_network_interface.helloterraformnic.id}"]
    vm_size = "Standard_A0"

    storage_image_reference {
        publisher = "Canonical"
        offer = "UbuntuServer"
        sku = "14.04.2-LTS"
        version = "latest"
    }

    storage_os_disk {
        name = "myosdisk"
        vhd_uri = "${azurerm_storage_account.helloterraformstorage.primary_blob_endpoint}${azurerm_storage_container.helloterraformstoragestoragecontainer.name}/myosdisk.vhd"
        caching = "ReadWrite"
        create_option = "FromImage"
    }

    os_profile {
        computer_name = "hostname"
        admin_username = "testadmin"
        admin_password = "Password1234!"
    }

    os_profile_linux_config {
        disable_password_authentication = false
    }

    tags {
        environment = "staging"
    }
}
~~~~
<span data-ttu-id="1588f-146">Ten slotte maakt het vorige codefragment u een virtuele machine die gebruikmaakt van alle resources die al ingericht.</span><span class="sxs-lookup"><span data-stu-id="1588f-146">Finally, the previous snippet creates a virtual machine that utilizes all the resources provisioned already.</span></span> <span data-ttu-id="1588f-147">Een opslagaccount en container voor een VHD, een netwerkinterface met openbare IP- en subnet opgegeven, zijn en de resourcegroep waarin u al hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1588f-147">They are a storage account and container for a VHD, a network interface with public IP and subnet specified, and the resource group you already created.</span></span> <span data-ttu-id="1588f-148">Let op de eigenschap vm_size, waarbij het script een Azure A0 SKU geeft.</span><span class="sxs-lookup"><span data-stu-id="1588f-148">Note the vm_size property, where the script specifies an Azure A0 SKU.</span></span>

### <a name="execute-the-script"></a><span data-ttu-id="1588f-149">Het script uitvoeren</span><span class="sxs-lookup"><span data-stu-id="1588f-149">Execute the script</span></span>
<span data-ttu-id="1588f-150">Terugkeren naar de console/opdrachtregel met het volledige script opgeslagen, en typ het volgende:</span><span class="sxs-lookup"><span data-stu-id="1588f-150">With the full script saved, exit to the console/command line and type the following:</span></span>
```
terraform apply terraformscripts
```
<span data-ttu-id="1588f-151">Na enige tijd de bronnen, met inbegrip van een virtuele machine, worden weergegeven in de `terraformtest` resourcegroep in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1588f-151">After some time, the resources, including a virtual machine, appear in the `terraformtest` resource group in the Azure portal.</span></span>

## <a name="complete-terraform-script"></a><span data-ttu-id="1588f-152">Volledige Terraform script</span><span class="sxs-lookup"><span data-stu-id="1588f-152">Complete Terraform script</span></span>

<span data-ttu-id="1588f-153">Voor uw gemak ziet hieronder u het volledige Terraform-script dat voorziet in alle van de infrastructuur die wordt besproken in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="1588f-153">For your convenience, below is the complete Terraform script that provisions all of the infrastructure discussed in this article.</span></span>

```
variable "resourcesname" {
  default = "helloterraform"
}

# Configure the Microsoft Azure Provider
provider "azurerm" {
  subscription_id = "XXX"
  client_id       = "XXX"
  client_secret   = "XXX"
  tenant_id       = "XXX"
}

# create a resource group if it doesn't exist
resource "azurerm_resource_group" "helloterraform" {
    name = "terraformtest"
    location = "West US"
}

# create virtual network
resource "azurerm_virtual_network" "helloterraformnetwork" {
    name = "tfvn"
    address_space = ["10.0.0.0/16"]
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
}

# create subnet
resource "azurerm_subnet" "helloterraformsubnet" {
    name = "tfsub"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    virtual_network_name = "${azurerm_virtual_network.helloterraformnetwork.name}"
    address_prefix = "10.0.2.0/24"
}


# create public IPs
resource "azurerm_public_ip" "helloterraformips" {
    name = "terraformtestip"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    public_ip_address_allocation = "dynamic"

    tags {
        environment = "TerraformDemo"
    }
}

# create network interface
resource "azurerm_network_interface" "helloterraformnic" {
    name = "tfni"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"

    ip_configuration {
        name = "testconfiguration1"
        subnet_id = "${azurerm_subnet.helloterraformsubnet.id}"
        private_ip_address_allocation = "static"
        private_ip_address = "10.0.2.5"
        public_ip_address_id = "${azurerm_public_ip.helloterraformips.id}"
    }
}

# create a random id
resource "random_id" "randomId" {
  byte_length = 4
}

# create storage account
resource "azurerm_storage_account" "helloterraformstorage" {
    name                = "tfstorage${random_id.randomId.hex}"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    location = "westus"
    account_type = "Standard_LRS"

    tags {
        environment = "staging"
    }
}

# create storage container
resource "azurerm_storage_container" "helloterraformstoragestoragecontainer" {
    name = "vhd"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    storage_account_name = "${azurerm_storage_account.helloterraformstorage.name}"
    container_access_type = "private"
    depends_on = ["azurerm_storage_account.helloterraformstorage"]
}

# create virtual machine
resource "azurerm_virtual_machine" "helloterraformvm" {
    name = "terraformvm"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    network_interface_ids = ["${azurerm_network_interface.helloterraformnic.id}"]
    vm_size = "Standard_A0"

    storage_image_reference {
        publisher = "Canonical"
        offer = "UbuntuServer"
        sku = "14.04.2-LTS"
        version = "latest"
    }

    storage_os_disk {
        name = "myosdisk"
        vhd_uri = "${azurerm_storage_account.helloterraformstorage.primary_blob_endpoint}${azurerm_storage_container.helloterraformstoragestoragecontainer.name}/myosdisk.vhd"
        caching = "ReadWrite"
        create_option = "FromImage"
    }

    os_profile {
        computer_name = "hostname"
        admin_username = "testadmin"
        admin_password = "Password1234!"
    }

    os_profile_linux_config {
        disable_password_authentication = false
    }

    tags {
        environment = "staging"
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="1588f-154">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1588f-154">Next steps</span></span>
<span data-ttu-id="1588f-155">U kunt de basisinfrastructuur in Azure hebt gemaakt met behulp van Terraform.</span><span class="sxs-lookup"><span data-stu-id="1588f-155">You have created basic infrastructure in Azure by using Terraform.</span></span> <span data-ttu-id="1588f-156">Voor complexere scenario's, inclusief voorbeelden die gebruik load balancers en de virtuele machine worden geschaald sets, Zie talrijke [Terraform voorbeelden voor Azure](https://github.com/hashicorp/terraform/tree/master/examples).</span><span class="sxs-lookup"><span data-stu-id="1588f-156">For more complex scenarios, including examples that use load balancers and virtual machine scale sets, see numerous [Terraform examples for Azure](https://github.com/hashicorp/terraform/tree/master/examples).</span></span> <span data-ttu-id="1588f-157">Zie voor een bijgewerkte lijst met ondersteunde providers voor Azure de [Terraform documentatie](https://www.terraform.io/docs/providers/azurerm/index.html).</span><span class="sxs-lookup"><span data-stu-id="1588f-157">For an up-to-date list of supported Azure providers, see the [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).</span></span>
