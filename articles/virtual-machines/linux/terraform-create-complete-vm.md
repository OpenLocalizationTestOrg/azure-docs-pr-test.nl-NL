---
title: het basisinfrastructuur aaaCreate in Azure met behulp van Terraform | Microsoft Docs
description: Meer informatie over hoe Azure toocreate resources met behulp van Terraform
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
ms.openlocfilehash: 52591009ee7cb906402b8bca2ce63794ac7afcc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-basic-infrastructure-in-azure-by-using-terraform"></a><span data-ttu-id="c0223-103">Maken van de basisinfrastructuur in Azure met behulp van Terraform</span><span class="sxs-lookup"><span data-stu-id="c0223-103">Create basic infrastructure in Azure by using Terraform</span></span>
<span data-ttu-id="c0223-104">Dit artikel wordt beschreven Hallo stappen die u nodig hebt tootake tooprovision een virtuele machine, samen met de onderliggende infrastructuur in Azure.</span><span class="sxs-lookup"><span data-stu-id="c0223-104">This article describes hello steps you need tootake tooprovision a virtual machine, together with underlying infrastructure, into Azure.</span></span> <span data-ttu-id="c0223-105">U leert hoe toowrite Terraform scripts en hoe toovisualize Hallo verandert voordat u ze in uw cloudinfrastructuur zodat.</span><span class="sxs-lookup"><span data-stu-id="c0223-105">You will learn how toowrite Terraform scripts and how toovisualize hello changes before you make them in your cloud infrastructure.</span></span> <span data-ttu-id="c0223-106">Ook wordt uitgelegd hoe toocreate infrastructuur in Azure met behulp van Terraform.</span><span class="sxs-lookup"><span data-stu-id="c0223-106">You also will learn how toocreate infrastructure in Azure by using Terraform.</span></span>

<span data-ttu-id="c0223-107">tooget gestart, maak een bestand \terraform_azure101.tf aangeroepen in een teksteditor naar keuze (Visual Studio Code/Sublime/Vim/enz.).</span><span class="sxs-lookup"><span data-stu-id="c0223-107">tooget started, create a file called \terraform_azure101.tf in your text editor of choice (Visual Studio Code/Sublime/Vim/etc.).</span></span> <span data-ttu-id="c0223-108">de exacte naam Hallo van Hallo-bestand niet van belang omdat Terraform Hallo mapnaam als een parameter accepteert: alle scripts in de map Hallo worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c0223-108">hello exact name of hello file isn't important because Terraform accepts hello folder name as a parameter: all scripts in hello folder get executed.</span></span> <span data-ttu-id="c0223-109">Plak de volgende code in het nieuwe bestand Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="c0223-109">Paste hello following code in hello new file:</span></span>

~~~~
# Configure hello Microsoft Azure Provider
# NOTE: if you defined these values as environment variables, you do not have tooinclude this block
provider "azurerm" {
  subscription_id = "your_subscription_id_from_script_execution"
  client_id       = "your_appId_from_script_execution"
  client_secret   = "your_password_from_script_execution"
  tenant_id       = "your_tenant_id_from_script_execution"
}

# create a resource group if it doesn't exist
resource "azurerm_resource_group" "helloterraform" {
    name = "terraformtest"
    location = "West US"
}
~~~~
<span data-ttu-id="c0223-110">In Hallo `provider` sectie Hallo script, geeft u aan Terraform toouse een Azure-provider tooprovision resources in Hallo-script.</span><span class="sxs-lookup"><span data-stu-id="c0223-110">In hello `provider` section of hello script, you tell Terraform toouse an Azure provider tooprovision resources in hello script.</span></span> <span data-ttu-id="c0223-111">tooget waarden voor subscription_id, appId, wachtwoord en tenant_id, Zie Hallo [installeren en configureren van Terraform](terraform-install-configure.md) handleiding.</span><span class="sxs-lookup"><span data-stu-id="c0223-111">tooget values for subscription_id, appId, password, and tenant_id, see hello [Install and configure Terraform](terraform-install-configure.md) guide.</span></span> <span data-ttu-id="c0223-112">Als u omgevingsvariabelen voor Hallo waarden in dit blok hebt gemaakt, hoeft u geen tooinclude deze.</span><span class="sxs-lookup"><span data-stu-id="c0223-112">If you have created environment variables for hello values in this block, you don't need tooinclude it.</span></span> 

<span data-ttu-id="c0223-113">Hallo `azurerm_resource_group` resource Hiermee geeft u Terraform toocreate een nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="c0223-113">hello `azurerm_resource_group` resource instructs Terraform toocreate a new resource group.</span></span> <span data-ttu-id="c0223-114">U kunt meer brontypen die beschikbaar in Terraform verderop in dit artikel zijn kunt zien.</span><span class="sxs-lookup"><span data-stu-id="c0223-114">You can see more resource types that are available in Terraform later in this article.</span></span>

## <a name="execute-hello-script"></a><span data-ttu-id="c0223-115">Hallo-script uitvoeren</span><span class="sxs-lookup"><span data-stu-id="c0223-115">Execute hello script</span></span>
<span data-ttu-id="c0223-116">Nadat u Hallo script opslaat, toohello console/vanaf de opdrachtregel sluiten en typ de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="c0223-116">After you save hello script, exit toohello console/command line, and type hello following:</span></span>
```
terraform init
```
 <span data-ttu-id="c0223-117">tooinitialize hello Terraform provider voor Azure.</span><span class="sxs-lookup"><span data-stu-id="c0223-117">tooinitialize hello Terraform provider for Azure.</span></span> <span data-ttu-id="c0223-118">Wijzig Hallo directory te**terraformscripts**, en het probleem Hallo de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="c0223-118">Then change hello directory too**terraformscripts**, and issue hello following command:</span></span>
```
terraform plan
```
<span data-ttu-id="c0223-119">We Hallo gebruikt `plan` Terraform-opdracht wordt gekeken naar Hallo-resources die zijn gedefinieerd in het Hallo-scripts.</span><span class="sxs-lookup"><span data-stu-id="c0223-119">We used hello `plan` Terraform command, which looks at hello resources defined in hello scripts.</span></span> <span data-ttu-id="c0223-120">Het vergelijkt ze toohello informatie over de status door Terraform worden opgeslagen en vervolgens de uitvoer geplande uitvoering Hallo _zonder_ resources daadwerkelijk maken in Azure.</span><span class="sxs-lookup"><span data-stu-id="c0223-120">It compares them toohello state information saved by Terraform and then outputs hello planned execution _without_ actually creating resources in Azure.</span></span> 

<span data-ttu-id="c0223-121">Nadat u de vorige opdracht Hallo uitvoert, ziet u dat lijkt op Hallo scherm te volgen:</span><span class="sxs-lookup"><span data-stu-id="c0223-121">After you execute hello previous command, you should see something like hello following screen:</span></span>

![Terraform plannen](./media/terraform/tf_plan2.png)

<span data-ttu-id="c0223-123">Als alles er goed uitziet, richt u deze nieuwe resourcegroep in Azure door Hallo volgende uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="c0223-123">If everything looks correct, provision this new resource group in Azure by executing hello following:</span></span> 
```
terraform apply
```
<span data-ttu-id="c0223-124">In hello Azure-portal, ziet u Hallo leeg resourcegroep genaamd `terraformtest`.</span><span class="sxs-lookup"><span data-stu-id="c0223-124">In hello Azure portal, you should see hello new empty resource group called `terraformtest`.</span></span> <span data-ttu-id="c0223-125">In Hallo volgende sectie, voegt u een virtuele machine en alle Hallo ondersteunende infrastructuur voor die virtuele machine toohello-resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="c0223-125">In hello following section, you add a virtual machine and all hello supporting infrastructure for that virtual machine toohello resource group.</span></span>

## <a name="provision-an-ubuntu-vm-with-terraform"></a><span data-ttu-id="c0223-126">Een virtuele Ubuntu-machine met Terraform inrichten</span><span class="sxs-lookup"><span data-stu-id="c0223-126">Provision an Ubuntu VM with Terraform</span></span>
<span data-ttu-id="c0223-127">Laten we uitbreiden een virtuele machine met Ubuntu Hallo Terraform script die we met Hallo-informatie die nodig zijn tooprovision hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c0223-127">Let's extend hello Terraform script we've created with hello details that are necessary tooprovision a virtual machine running Ubuntu.</span></span> <span data-ttu-id="c0223-128">Hallo-resources die u in de volgende secties Hallo inrichten zijn:</span><span class="sxs-lookup"><span data-stu-id="c0223-128">hello resources that you provision in hello following sections are:</span></span>

* <span data-ttu-id="c0223-129">Een netwerk met één subnet</span><span class="sxs-lookup"><span data-stu-id="c0223-129">A network with a single subnet</span></span>
* <span data-ttu-id="c0223-130">Een netwerkinterfacekaart</span><span class="sxs-lookup"><span data-stu-id="c0223-130">A network interface card</span></span> 
* <span data-ttu-id="c0223-131">Een opslagaccount voor diagnostische gegevens Hallo-virtuele machine</span><span class="sxs-lookup"><span data-stu-id="c0223-131">A storage account for hello virtual machine diagnostics</span></span>
* <span data-ttu-id="c0223-132">Een openbaar IP-adres</span><span class="sxs-lookup"><span data-stu-id="c0223-132">A public IP</span></span>
* <span data-ttu-id="c0223-133">Een virtuele machine die gebruikmaakt van alle Hallo eerdere bronnen</span><span class="sxs-lookup"><span data-stu-id="c0223-133">A virtual machine that utilizes all hello previous resources</span></span> 

<span data-ttu-id="c0223-134">Zie voor uitgebreide documentatie voor elk hello Azure Terraform resources Hallo [Terraform documentatie](https://www.terraform.io/docs/providers/azurerm/index.html).</span><span class="sxs-lookup"><span data-stu-id="c0223-134">For thorough documentation for each of hello Azure Terraform resources, see hello [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).</span></span>

<span data-ttu-id="c0223-135">Hallo volledige versie van Hallo [inrichting script](#complete-terraform-script) is ook voor uw gemak geleverd.</span><span class="sxs-lookup"><span data-stu-id="c0223-135">hello full version of hello [provisioning script](#complete-terraform-script) is also provided for convenience.</span></span>

### <a name="extend-hello-terraform-script"></a><span data-ttu-id="c0223-136">Hallo Terraform script uitbreiden</span><span class="sxs-lookup"><span data-stu-id="c0223-136">Extend hello Terraform script</span></span>
<span data-ttu-id="c0223-137">Hallo-script dat is gemaakt met de Hallo resources na uitbreiden:</span><span class="sxs-lookup"><span data-stu-id="c0223-137">Extend hello script that was created with hello following resources:</span></span> 
~~~~
# create a virtual network
resource "azurerm_virtual_network" "helloterraformnetwork" {
    name = "acctvn"
    address_space = ["10.0.0.0/16"]
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"

    tags {
        environment = "Terraform Demo"
    }
}

# create subnet
resource "azurerm_subnet" "helloterraformsubnet" {
    name = "acctsub"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    virtual_network_name = "${azurerm_virtual_network.helloterraformnetwork.name}"
    address_prefix = "10.0.2.0/24"
}
~~~~
<span data-ttu-id="c0223-138">Hallo vorige script maakt een virtueel netwerk en een subnet binnen dit virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="c0223-138">hello previous script creates a virtual network and a subnet within that virtual network.</span></span> <span data-ttu-id="c0223-139">Houd er rekening mee Hallo verwijzing toohello resourcegroep die u al hebt gemaakt via "${azurerm_resource_group.helloterraform.name}" hello virtuele netwerk en de definitie van subnet Hallo.</span><span class="sxs-lookup"><span data-stu-id="c0223-139">Note hello reference toohello resource group you have created already via "${azurerm_resource_group.helloterraform.name}" in both hello virtual network and hello subnet definition.</span></span>

~~~~
# create public IP
resource "azurerm_public_ip" "helloterraformips" {
    name = "terraformtestip"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    public_ip_address_allocation = "dynamic"

    tags {
        environment = "Terraform Demo"
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

    tags {
        environment = "Terraform Demo"
    }
}
~~~~
<span data-ttu-id="c0223-140">Hallo vorige script codefragmenten maken een openbare IP-adres en een netwerkinterface die gebruik maakt van Hallo openbare IP-adres gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c0223-140">hello previous script snippets create a public IP and a network interface that makes use of hello public IP created.</span></span> <span data-ttu-id="c0223-141">Houd er rekening mee Hallo verwijzingen toosubnet_id en public_ip_address_id.</span><span class="sxs-lookup"><span data-stu-id="c0223-141">Note hello references toosubnet_id and public_ip_address_id.</span></span> <span data-ttu-id="c0223-142">Terraform heeft toounderstand ingebouwde intelligentie die Hallo netwerkinterface heeft een afhankelijkheid op Hallo bronnen die nodig toobe gemaakt voordat het maken van de netwerkinterface Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="c0223-142">Terraform has built-in intelligence toounderstand that hello network interface has a dependency on hello resources that need toobe created before hello creation of hello network interface.</span></span>

~~~~
# create a random id
resource "random_id" "randomId" {
  keepers = {
    # Generate a new id only when a new resource group is defined
    resource_group = "${azurerm_resource_group.helloterraform.name}"
  }

  byte_length = 8
}

# create storage account
resource "azurerm_storage_account" "helloterraformstorage" {
    name                = "diag${random_id.randomId.hex}"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    location = "West US"
    account_type = "Standard_LRS"

    tags {
        environment = "Terraform Demo"
    }
}
~~~~
<span data-ttu-id="c0223-143">Hier kunt u een opslagaccount hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c0223-143">Here, you created a storage account.</span></span> <span data-ttu-id="c0223-144">Dit opslagaccount is waar Hallo virtuele machine de details van diagnostische gegevens worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="c0223-144">This storage account is where hello virtual machine will store its diagnostics details.</span></span>

~~~~
# create virtual machine
resource "azurerm_virtual_machine" "helloterraformvm" {
    name = "terraformvm"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    network_interface_ids = ["${azurerm_network_interface.helloterraformnic.id}"]
    vm_size = "Standard_DS1_v2"

    os_profile {
        computer_name = "hostname"
        admin_username = "azureuser"
        admin_password = ""
    }

    os_profile_linux_config {
        disable_password_authentication = true

        ssh_keys {
            path = "/home/azureuser/.ssh/authorized_keys"
            key_data = "... INSERT OPENSSH PUBLIC KEY HERE ..."
        }
    }

    storage_image_reference {
        publisher = "Canonical"
        offer = "UbuntuServer"
        sku = "16.04.0-LTS"
        version = "latest"
    }

    storage_os_disk {
        name = "myosdisk"
        managed_disk_type = "Premium_LRS"
        create_option = "FromImage"
    } 

    boot_diagnostics {
        enabled = "true"
        storage_uri = "${azurerm_storage_account.helloterraformstorage.primary_blob_endpoint}"
    }

    tags {
        environment = "Terraform Demo"
    }
}
~~~~
<span data-ttu-id="c0223-145">Ten slotte maakt Hallo vorige codefragment voor een virtuele machine die gebruikmaakt van alle Hallo resources al ingericht.</span><span class="sxs-lookup"><span data-stu-id="c0223-145">Finally, hello previous snippet creates a virtual machine that utilizes all hello resources provisioned already.</span></span> <span data-ttu-id="c0223-146">Ze zijn van een opslagaccount voor diagnostische gegevens Hallo-virtuele machine, een netwerkinterface met openbare IP- en het opgegeven subnet en resourcegroep Hallo u al hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c0223-146">They are a storage account for hello virtual machine diagnostics, a network interface with public IP and subnet specified, and hello resource group you already created.</span></span> <span data-ttu-id="c0223-147">Houd er rekening mee Hallo vm_size eigenschap, waarbij Hallo script Hiermee geeft u een Azure standaard DS1v2 SKU.</span><span class="sxs-lookup"><span data-stu-id="c0223-147">Note hello vm_size property, where hello script specifies an Azure Standard DS1v2 SKU.</span></span>

<span data-ttu-id="c0223-148">U staat op het vereiste toosupply openbare SSH-sleutel.</span><span class="sxs-lookup"><span data-stu-id="c0223-148">You are required toosupply an SSH public key.</span></span> <span data-ttu-id="c0223-149">Hallo-waarde voor openbare sleutel in sectie Hallo plaatsen **... INVOEGEN OPENSSH OPENBARE SLEUTEL HIER...**  hierboven.</span><span class="sxs-lookup"><span data-stu-id="c0223-149">Place hello public key value into hello section **... INSERT OPENSSH PUBLIC KEY HERE ...** above.</span></span> <span data-ttu-id="c0223-150">U kunt een bestaande ssh sleutelpaar of volgen Hallo [Windows](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/ssh-from-windows) of [Linux/Mac OS](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/mac-create-ssh-keys) documentatie toogenerate Hallo sleutelpaar.</span><span class="sxs-lookup"><span data-stu-id="c0223-150">You can use an existing ssh key pair or follow hello [Windows](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/ssh-from-windows) or [Linux/macOS](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/mac-create-ssh-keys) documentation toogenerate hello key pair.</span></span>

### <a name="execute-hello-script"></a><span data-ttu-id="c0223-151">Hallo-script uitvoeren</span><span class="sxs-lookup"><span data-stu-id="c0223-151">Execute hello script</span></span>
<span data-ttu-id="c0223-152">Bij de volledige script Hallo opgeslagen, toohello console/vanaf de opdrachtregel sluiten en typ de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="c0223-152">With hello full script saved, exit toohello console/command line and type hello following:</span></span>
```
terraform apply
```
<span data-ttu-id="c0223-153">Na enige tijd Hallo bronnen, met inbegrip van een virtuele machine, worden weergegeven in Hallo `terraformtest` resourcegroep in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="c0223-153">After some time, hello resources, including a virtual machine, appear in hello `terraformtest` resource group in hello Azure portal.</span></span>

## <a name="complete-terraform-script"></a><span data-ttu-id="c0223-154">Volledige Terraform script</span><span class="sxs-lookup"><span data-stu-id="c0223-154">Complete Terraform script</span></span>

<span data-ttu-id="c0223-155">Is voor uw gemak hieronder Hallo volledige Terraform script die voorziet in alle Hallo infrastructuur besproken in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="c0223-155">For your convenience, below is hello complete Terraform script that provisions all of hello infrastructure discussed in this article.</span></span>

```
# Configure hello Microsoft Azure Provider
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

# create a virtual network
resource "azurerm_virtual_network" "helloterraformnetwork" {
    name = "acctvn"
    address_space = ["10.0.0.0/16"]
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"

    tags {
        environment = "Terraform Demo"
    }
}

# create subnet
resource "azurerm_subnet" "helloterraformsubnet" {
    name = "acctsub"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    virtual_network_name = "${azurerm_virtual_network.helloterraformnetwork.name}"
    address_prefix = "10.0.2.0/24"
}

# create public IP
resource "azurerm_public_ip" "helloterraformips" {
    name = "terraformtestip"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    public_ip_address_allocation = "dynamic"

    tags {
        environment = "Terraform Demo"
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

    tags {
        environment = "Terraform Demo"
    }
}

# create a random id
resource "random_id" "randomId" {
  keepers = {
    # Generate a new id only when a new resource group is defined
    resource_group = "${azurerm_resource_group.helloterraform.name}"
  }

  byte_length = 8
}

# create storage account
resource "azurerm_storage_account" "helloterraformstorage" {
    name                = "diag${random_id.randomId.hex}"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    location = "West US"
    account_type = "Standard_LRS"

    tags {
        environment = "Terraform Demo"
    }
}

# create virtual machine
resource "azurerm_virtual_machine" "helloterraformvm" {
    name = "terraformvm"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    network_interface_ids = ["${azurerm_network_interface.helloterraformnic.id}"]
    vm_size = "Standard_DS1_v2"

    os_profile {
        computer_name = "hostname"
        admin_username = "azureuser"
        admin_password = ""
    }

    os_profile_linux_config {
        disable_password_authentication = true

        ssh_keys {
            path = "/home/azureuser/.ssh/authorized_keys"
            key_data = "... INSERT OPENSSH PUBLIC KEY HERE ..."
        }
    }

    storage_image_reference {
        publisher = "Canonical"
        offer = "UbuntuServer"
        sku = "16.04.0-LTS"
        version = "latest"
    }

    storage_os_disk {
        name = "myosdisk"
        managed_disk_type = "Premium_LRS"
        create_option = "FromImage"
    } 

    boot_diagnostics {
        enabled = "true"
        storage_uri = "${azurerm_storage_account.helloterraformstorage.primary_blob_endpoint}"
    }

    tags {
        environment = "Terraform Demo"
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="c0223-156">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c0223-156">Next steps</span></span>
<span data-ttu-id="c0223-157">U kunt de basisinfrastructuur in Azure hebt gemaakt met behulp van Terraform.</span><span class="sxs-lookup"><span data-stu-id="c0223-157">You have created basic infrastructure in Azure by using Terraform.</span></span> <span data-ttu-id="c0223-158">Voor complexere scenario's, inclusief voorbeelden die gebruik load balancers en de virtuele machine worden geschaald sets, Zie talrijke [Terraform voorbeelden voor Azure](https://github.com/hashicorp/terraform/tree/master/examples).</span><span class="sxs-lookup"><span data-stu-id="c0223-158">For more complex scenarios, including examples that use load balancers and virtual machine scale sets, see numerous [Terraform examples for Azure](https://github.com/hashicorp/terraform/tree/master/examples).</span></span> <span data-ttu-id="c0223-159">Zie voor een bijgewerkte lijst met ondersteunde providers voor Azure Hallo [Terraform documentatie](https://www.terraform.io/docs/providers/azurerm/index.html).</span><span class="sxs-lookup"><span data-stu-id="c0223-159">For an up-to-date list of supported Azure providers, see hello [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).</span></span>
