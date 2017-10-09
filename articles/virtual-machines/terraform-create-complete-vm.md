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
ms.openlocfilehash: 916a838c118f28b3fbd373188e0acb2afc655081
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-basic-infrastructure-in-azure-by-using-terraform"></a><span data-ttu-id="88d05-103">Maken van de basisinfrastructuur in Azure met behulp van Terraform</span><span class="sxs-lookup"><span data-stu-id="88d05-103">Create basic infrastructure in Azure by using Terraform</span></span>
<span data-ttu-id="88d05-104">Dit artikel wordt beschreven Hallo stappen die u nodig hebt tootake tooprovision een virtuele machine, samen met de onderliggende infrastructuur in Azure.</span><span class="sxs-lookup"><span data-stu-id="88d05-104">This article describes hello steps you need tootake tooprovision a virtual machine, together with underlying infrastructure, into Azure.</span></span> <span data-ttu-id="88d05-105">U leert hoe toowrite Terraform scripts en hoe toovisualize Hallo verandert voordat u ze in uw cloudinfrastructuur zodat.</span><span class="sxs-lookup"><span data-stu-id="88d05-105">You will learn how toowrite Terraform scripts and how toovisualize hello changes before you make them in your cloud infrastructure.</span></span> <span data-ttu-id="88d05-106">Ook wordt uitgelegd hoe toocreate infrastructuur in Azure met behulp van Terraform.</span><span class="sxs-lookup"><span data-stu-id="88d05-106">You also will learn how toocreate infrastructure in Azure by using Terraform.</span></span>

<span data-ttu-id="88d05-107">tooget gestart, maak een bestand \terraform_azure101.tf aangeroepen in een teksteditor naar keuze (Visual Studio Code/Sublime/Vim/enz.).</span><span class="sxs-lookup"><span data-stu-id="88d05-107">tooget started, create a file called \terraform_azure101.tf in your text editor of choice (Visual Studio Code/Sublime/Vim/etc.).</span></span> <span data-ttu-id="88d05-108">de exacte naam Hallo van Hallo-bestand niet van belang omdat Terraform Hallo mapnaam als een parameter accepteert: alle scripts in de map Hallo worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="88d05-108">hello exact name of hello file isn't important because Terraform accepts hello folder name as a parameter: all scripts in hello folder get executed.</span></span> <span data-ttu-id="88d05-109">Plak de volgende code in het nieuwe bestand Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="88d05-109">Paste hello following code in hello new file:</span></span>

~~~~
# Configure hello Microsoft Azure Provider
# NOTE: if you defined these values as environment variables, you do not have tooinclude this block
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
<span data-ttu-id="88d05-110">In Hallo `provider` sectie Hallo script, geeft u aan Terraform toouse een Azure-provider tooprovision resources in Hallo-script.</span><span class="sxs-lookup"><span data-stu-id="88d05-110">In hello `provider` section of hello script, you tell Terraform toouse an Azure provider tooprovision resources in hello script.</span></span> <span data-ttu-id="88d05-111">tooget waarden voor subscription_id, appId, wachtwoord en tenant_id, Zie Hallo [installeren en configureren van Terraform](terraform-install-configure.md) handleiding.</span><span class="sxs-lookup"><span data-stu-id="88d05-111">tooget values for subscription_id, appId, password, and tenant_id, see hello [Install and configure Terraform](terraform-install-configure.md) guide.</span></span> <span data-ttu-id="88d05-112">Als u omgevingsvariabelen voor Hallo waarden in dit blok hebt gemaakt, hoeft u geen tooinclude deze.</span><span class="sxs-lookup"><span data-stu-id="88d05-112">If you have created environment variables for hello values in this block, you don't need tooinclude it.</span></span> 

<span data-ttu-id="88d05-113">Hallo `azurerm_resource_group` resource Hiermee geeft u Terraform toocreate een nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="88d05-113">hello `azurerm_resource_group` resource instructs Terraform toocreate a new resource group.</span></span> <span data-ttu-id="88d05-114">U kunt meer brontypen die beschikbaar in Terraform verderop in dit artikel zijn kunt zien.</span><span class="sxs-lookup"><span data-stu-id="88d05-114">You can see more resource types that are available in Terraform later in this article.</span></span>

## <a name="execute-hello-script"></a><span data-ttu-id="88d05-115">Hallo-script uitvoeren</span><span class="sxs-lookup"><span data-stu-id="88d05-115">Execute hello script</span></span>
<span data-ttu-id="88d05-116">Nadat u Hallo script opslaat, toohello console/vanaf de opdrachtregel sluiten en typ de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="88d05-116">After you save hello script, exit toohello console/command line, and type hello following:</span></span>
```
terraform init
```
<span data-ttu-id="88d05-117">tooinitialize Terraform provider voor Azure.</span><span class="sxs-lookup"><span data-stu-id="88d05-117">tooinitialize Terraform provider for Azure.</span></span> <span data-ttu-id="88d05-118">Typ de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="88d05-118">Then type hello following:</span></span>
```
terraform plan terraformscripts
```
<span data-ttu-id="88d05-119">Er wordt ervan uitgegaan dat `terraformscripts` Hallo map is waar Hallo-script is opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="88d05-119">We assume that `terraformscripts` is hello folder where hello script was saved.</span></span> <span data-ttu-id="88d05-120">We Hallo gebruikt `plan` Terraform-opdracht wordt gekeken naar Hallo-resources die zijn gedefinieerd in het Hallo-scripts.</span><span class="sxs-lookup"><span data-stu-id="88d05-120">We used hello `plan` Terraform command, which looks at hello resources defined in hello scripts.</span></span> <span data-ttu-id="88d05-121">Het vergelijkt ze toohello informatie over de status door Terraform worden opgeslagen en vervolgens de uitvoer geplande uitvoering Hallo _zonder_ resources daadwerkelijk maken in Azure.</span><span class="sxs-lookup"><span data-stu-id="88d05-121">It compares them toohello state information saved by Terraform and then outputs hello planned execution _without_ actually creating resources in Azure.</span></span> 

<span data-ttu-id="88d05-122">Nadat u de vorige opdracht Hallo uitvoert, ziet u dat lijkt op Hallo scherm te volgen:</span><span class="sxs-lookup"><span data-stu-id="88d05-122">After you execute hello previous command, you should see something like hello following screen:</span></span>

![Terraform plannen](linux/media/terraform/tf_plan2.png)

<span data-ttu-id="88d05-124">Als alles er goed uitziet, richt u deze nieuwe resourcegroep in Azure door Hallo volgende uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="88d05-124">If everything looks correct, provision this new resource group in Azure by executing hello following:</span></span> 
```
terraform apply terraformscripts
```
<span data-ttu-id="88d05-125">In hello Azure-portal, ziet u Hallo leeg resourcegroep genaamd `terraformtest`.</span><span class="sxs-lookup"><span data-stu-id="88d05-125">In hello Azure portal, you should see hello new empty resource group called `terraformtest`.</span></span> <span data-ttu-id="88d05-126">In Hallo volgende sectie, voegt u een virtuele machine en alle Hallo ondersteunende infrastructuur voor die virtuele machine toohello-resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="88d05-126">In hello following section, you add a virtual machine and all hello supporting infrastructure for that virtual machine toohello resource group.</span></span>

## <a name="provision-an-ubuntu-vm-with-terraform"></a><span data-ttu-id="88d05-127">Een virtuele Ubuntu-machine met Terraform inrichten</span><span class="sxs-lookup"><span data-stu-id="88d05-127">Provision an Ubuntu VM with Terraform</span></span>
<span data-ttu-id="88d05-128">Laten we uitbreiden een virtuele machine met Ubuntu Hallo Terraform script die we met Hallo-informatie die nodig zijn tooprovision hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="88d05-128">Let's extend hello Terraform script we've created with hello details that are necessary tooprovision a virtual machine running Ubuntu.</span></span> <span data-ttu-id="88d05-129">Hallo-resources die u in de volgende secties Hallo inrichten zijn:</span><span class="sxs-lookup"><span data-stu-id="88d05-129">hello resources that you provision in hello following sections are:</span></span>

* <span data-ttu-id="88d05-130">Een netwerk met één subnet</span><span class="sxs-lookup"><span data-stu-id="88d05-130">A network with a single subnet</span></span>
* <span data-ttu-id="88d05-131">Een netwerkinterfacekaart</span><span class="sxs-lookup"><span data-stu-id="88d05-131">A network interface card</span></span> 
* <span data-ttu-id="88d05-132">Een opslagaccount met storage-container</span><span class="sxs-lookup"><span data-stu-id="88d05-132">A storage account with a storage container</span></span>
* <span data-ttu-id="88d05-133">Een openbaar IP-adres</span><span class="sxs-lookup"><span data-stu-id="88d05-133">A public IP</span></span>
* <span data-ttu-id="88d05-134">Een virtuele machine die gebruikmaakt van alle Hallo eerdere bronnen</span><span class="sxs-lookup"><span data-stu-id="88d05-134">A virtual machine that utilizes all hello previous resources</span></span> 

<span data-ttu-id="88d05-135">Zie voor uitgebreide documentatie voor elk hello Azure Terraform resources Hallo [Terraform documentatie](https://www.terraform.io/docs/providers/azurerm/index.html).</span><span class="sxs-lookup"><span data-stu-id="88d05-135">For thorough documentation for each of hello Azure Terraform resources, see hello [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).</span></span>

<span data-ttu-id="88d05-136">Hallo volledige versie van Hallo [inrichting script](#complete-terraform-script) is ook voor uw gemak geleverd.</span><span class="sxs-lookup"><span data-stu-id="88d05-136">hello full version of hello [provisioning script](#complete-terraform-script) is also provided for convenience.</span></span>

### <a name="extend-hello-terraform-script"></a><span data-ttu-id="88d05-137">Hallo Terraform script uitbreiden</span><span class="sxs-lookup"><span data-stu-id="88d05-137">Extend hello Terraform script</span></span>
<span data-ttu-id="88d05-138">Hallo-script dat is gemaakt met de Hallo resources na uitbreiden:</span><span class="sxs-lookup"><span data-stu-id="88d05-138">Extend hello script that was created with hello following resources:</span></span> 
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
<span data-ttu-id="88d05-139">Hallo vorige script maakt een virtueel netwerk en een subnet binnen dit virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="88d05-139">hello previous script creates a virtual network and a subnet within that virtual network.</span></span> <span data-ttu-id="88d05-140">Houd er rekening mee Hallo verwijzing toohello resourcegroep die u al hebt gemaakt via "${azurerm_resource_group.helloterraform.name}" hello virtuele netwerk en de definitie van subnet Hallo.</span><span class="sxs-lookup"><span data-stu-id="88d05-140">Note hello reference toohello resource group you have created already via "${azurerm_resource_group.helloterraform.name}" in both hello virtual network and hello subnet definition.</span></span>

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
<span data-ttu-id="88d05-141">Hallo vorige script codefragmenten maken een openbare IP-adres en een netwerkinterface die gebruik maakt van Hallo openbare IP-adres gemaakt.</span><span class="sxs-lookup"><span data-stu-id="88d05-141">hello previous script snippets create a public IP and a network interface that makes use of hello public IP created.</span></span> <span data-ttu-id="88d05-142">Houd er rekening mee Hallo verwijzingen toosubnet_id en public_ip_address_id.</span><span class="sxs-lookup"><span data-stu-id="88d05-142">Note hello references toosubnet_id and public_ip_address_id.</span></span> <span data-ttu-id="88d05-143">Terraform heeft toounderstand ingebouwde intelligentie die Hallo netwerkinterface heeft een afhankelijkheid op Hallo bronnen die nodig toobe gemaakt voordat het maken van de netwerkinterface Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="88d05-143">Terraform has built-in intelligence toounderstand that hello network interface has a dependency on hello resources that need toobe created before hello creation of hello network interface.</span></span>

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
<span data-ttu-id="88d05-144">Hier kunt u een opslagaccount hebt gemaakt en een storage-container binnen dit opslagaccount wordt gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="88d05-144">Here, you created a storage account and defined a storage container within that storage account.</span></span> <span data-ttu-id="88d05-145">Dit opslagaccount is waar het opslaan van virtuele harde schijven (VHD's) voor de virtuele machine Hallo over toobe gemaakt.</span><span class="sxs-lookup"><span data-stu-id="88d05-145">This storage account is where you store virtual hard disks (VHDs) for hello virtual machine about toobe created.</span></span>

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
<span data-ttu-id="88d05-146">Ten slotte maakt Hallo vorige codefragment voor een virtuele machine die gebruikmaakt van alle Hallo resources al ingericht.</span><span class="sxs-lookup"><span data-stu-id="88d05-146">Finally, hello previous snippet creates a virtual machine that utilizes all hello resources provisioned already.</span></span> <span data-ttu-id="88d05-147">Een opslagaccount en container voor een VHD, een netwerkinterface met openbare IP- en subnet opgegeven, zijn en resourcegroep Hallo u al hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="88d05-147">They are a storage account and container for a VHD, a network interface with public IP and subnet specified, and hello resource group you already created.</span></span> <span data-ttu-id="88d05-148">Houd er rekening mee Hallo vm_size eigenschap, waarbij Hallo script Hiermee geeft u een Azure A0 SKU.</span><span class="sxs-lookup"><span data-stu-id="88d05-148">Note hello vm_size property, where hello script specifies an Azure A0 SKU.</span></span>

### <a name="execute-hello-script"></a><span data-ttu-id="88d05-149">Hallo-script uitvoeren</span><span class="sxs-lookup"><span data-stu-id="88d05-149">Execute hello script</span></span>
<span data-ttu-id="88d05-150">Bij de volledige script Hallo opgeslagen, toohello console/vanaf de opdrachtregel sluiten en typ de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="88d05-150">With hello full script saved, exit toohello console/command line and type hello following:</span></span>
```
terraform apply terraformscripts
```
<span data-ttu-id="88d05-151">Na enige tijd Hallo bronnen, met inbegrip van een virtuele machine, worden weergegeven in Hallo `terraformtest` resourcegroep in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="88d05-151">After some time, hello resources, including a virtual machine, appear in hello `terraformtest` resource group in hello Azure portal.</span></span>

## <a name="complete-terraform-script"></a><span data-ttu-id="88d05-152">Volledige Terraform script</span><span class="sxs-lookup"><span data-stu-id="88d05-152">Complete Terraform script</span></span>

<span data-ttu-id="88d05-153">Is voor uw gemak hieronder Hallo volledige Terraform script die voorziet in alle Hallo infrastructuur besproken in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="88d05-153">For your convenience, below is hello complete Terraform script that provisions all of hello infrastructure discussed in this article.</span></span>

```
variable "resourcesname" {
  default = "helloterraform"
}

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

## <a name="next-steps"></a><span data-ttu-id="88d05-154">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="88d05-154">Next steps</span></span>
<span data-ttu-id="88d05-155">U kunt de basisinfrastructuur in Azure hebt gemaakt met behulp van Terraform.</span><span class="sxs-lookup"><span data-stu-id="88d05-155">You have created basic infrastructure in Azure by using Terraform.</span></span> <span data-ttu-id="88d05-156">Voor complexere scenario's, inclusief voorbeelden die gebruik load balancers en de virtuele machine worden geschaald sets, Zie talrijke [Terraform voorbeelden voor Azure](https://github.com/hashicorp/terraform/tree/master/examples).</span><span class="sxs-lookup"><span data-stu-id="88d05-156">For more complex scenarios, including examples that use load balancers and virtual machine scale sets, see numerous [Terraform examples for Azure](https://github.com/hashicorp/terraform/tree/master/examples).</span></span> <span data-ttu-id="88d05-157">Zie voor een bijgewerkte lijst met ondersteunde providers voor Azure Hallo [Terraform documentatie](https://www.terraform.io/docs/providers/azurerm/index.html).</span><span class="sxs-lookup"><span data-stu-id="88d05-157">For an up-to-date list of supported Azure providers, see hello [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).</span></span>
