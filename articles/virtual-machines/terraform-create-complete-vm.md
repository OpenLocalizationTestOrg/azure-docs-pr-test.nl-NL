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
# <a name="create-basic-infrastructure-in-azure-by-using-terraform"></a>Maken van de basisinfrastructuur in Azure met behulp van Terraform
Dit artikel wordt beschreven Hallo stappen die u nodig hebt tootake tooprovision een virtuele machine, samen met de onderliggende infrastructuur in Azure. U leert hoe toowrite Terraform scripts en hoe toovisualize Hallo verandert voordat u ze in uw cloudinfrastructuur zodat. Ook wordt uitgelegd hoe toocreate infrastructuur in Azure met behulp van Terraform.

tooget gestart, maak een bestand \terraform_azure101.tf aangeroepen in een teksteditor naar keuze (Visual Studio Code/Sublime/Vim/enz.). de exacte naam Hallo van Hallo-bestand niet van belang omdat Terraform Hallo mapnaam als een parameter accepteert: alle scripts in de map Hallo worden uitgevoerd. Plak de volgende code in het nieuwe bestand Hallo Hallo:

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
In Hallo `provider` sectie Hallo script, geeft u aan Terraform toouse een Azure-provider tooprovision resources in Hallo-script. tooget waarden voor subscription_id, appId, wachtwoord en tenant_id, Zie Hallo [installeren en configureren van Terraform](terraform-install-configure.md) handleiding. Als u omgevingsvariabelen voor Hallo waarden in dit blok hebt gemaakt, hoeft u geen tooinclude deze. 

Hallo `azurerm_resource_group` resource Hiermee geeft u Terraform toocreate een nieuwe resourcegroep. U kunt meer brontypen die beschikbaar in Terraform verderop in dit artikel zijn kunt zien.

## <a name="execute-hello-script"></a>Hallo-script uitvoeren
Nadat u Hallo script opslaat, toohello console/vanaf de opdrachtregel sluiten en typ de volgende Hallo:
```
terraform init
```
tooinitialize Terraform provider voor Azure. Typ de volgende Hallo:
```
terraform plan terraformscripts
```
Er wordt ervan uitgegaan dat `terraformscripts` Hallo map is waar Hallo-script is opgeslagen. We Hallo gebruikt `plan` Terraform-opdracht wordt gekeken naar Hallo-resources die zijn gedefinieerd in het Hallo-scripts. Het vergelijkt ze toohello informatie over de status door Terraform worden opgeslagen en vervolgens de uitvoer geplande uitvoering Hallo _zonder_ resources daadwerkelijk maken in Azure. 

Nadat u de vorige opdracht Hallo uitvoert, ziet u dat lijkt op Hallo scherm te volgen:

![Terraform plannen](linux/media/terraform/tf_plan2.png)

Als alles er goed uitziet, richt u deze nieuwe resourcegroep in Azure door Hallo volgende uitvoeren: 
```
terraform apply terraformscripts
```
In hello Azure-portal, ziet u Hallo leeg resourcegroep genaamd `terraformtest`. In Hallo volgende sectie, voegt u een virtuele machine en alle Hallo ondersteunende infrastructuur voor die virtuele machine toohello-resourcegroep.

## <a name="provision-an-ubuntu-vm-with-terraform"></a>Een virtuele Ubuntu-machine met Terraform inrichten
Laten we uitbreiden een virtuele machine met Ubuntu Hallo Terraform script die we met Hallo-informatie die nodig zijn tooprovision hebt gemaakt. Hallo-resources die u in de volgende secties Hallo inrichten zijn:

* Een netwerk met één subnet
* Een netwerkinterfacekaart 
* Een opslagaccount met storage-container
* Een openbaar IP-adres
* Een virtuele machine die gebruikmaakt van alle Hallo eerdere bronnen 

Zie voor uitgebreide documentatie voor elk hello Azure Terraform resources Hallo [Terraform documentatie](https://www.terraform.io/docs/providers/azurerm/index.html).

Hallo volledige versie van Hallo [inrichting script](#complete-terraform-script) is ook voor uw gemak geleverd.

### <a name="extend-hello-terraform-script"></a>Hallo Terraform script uitbreiden
Hallo-script dat is gemaakt met de Hallo resources na uitbreiden: 
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
Hallo vorige script maakt een virtueel netwerk en een subnet binnen dit virtuele netwerk. Houd er rekening mee Hallo verwijzing toohello resourcegroep die u al hebt gemaakt via "${azurerm_resource_group.helloterraform.name}" hello virtuele netwerk en de definitie van subnet Hallo.

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
Hallo vorige script codefragmenten maken een openbare IP-adres en een netwerkinterface die gebruik maakt van Hallo openbare IP-adres gemaakt. Houd er rekening mee Hallo verwijzingen toosubnet_id en public_ip_address_id. Terraform heeft toounderstand ingebouwde intelligentie die Hallo netwerkinterface heeft een afhankelijkheid op Hallo bronnen die nodig toobe gemaakt voordat het maken van de netwerkinterface Hallo Hallo.

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
Hier kunt u een opslagaccount hebt gemaakt en een storage-container binnen dit opslagaccount wordt gedefinieerd. Dit opslagaccount is waar het opslaan van virtuele harde schijven (VHD's) voor de virtuele machine Hallo over toobe gemaakt.

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
Ten slotte maakt Hallo vorige codefragment voor een virtuele machine die gebruikmaakt van alle Hallo resources al ingericht. Een opslagaccount en container voor een VHD, een netwerkinterface met openbare IP- en subnet opgegeven, zijn en resourcegroep Hallo u al hebt gemaakt. Houd er rekening mee Hallo vm_size eigenschap, waarbij Hallo script Hiermee geeft u een Azure A0 SKU.

### <a name="execute-hello-script"></a>Hallo-script uitvoeren
Bij de volledige script Hallo opgeslagen, toohello console/vanaf de opdrachtregel sluiten en typ de volgende Hallo:
```
terraform apply terraformscripts
```
Na enige tijd Hallo bronnen, met inbegrip van een virtuele machine, worden weergegeven in Hallo `terraformtest` resourcegroep in hello Azure-portal.

## <a name="complete-terraform-script"></a>Volledige Terraform script

Is voor uw gemak hieronder Hallo volledige Terraform script die voorziet in alle Hallo infrastructuur besproken in dit artikel.

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

## <a name="next-steps"></a>Volgende stappen
U kunt de basisinfrastructuur in Azure hebt gemaakt met behulp van Terraform. Voor complexere scenario's, inclusief voorbeelden die gebruik load balancers en de virtuele machine worden geschaald sets, Zie talrijke [Terraform voorbeelden voor Azure](https://github.com/hashicorp/terraform/tree/master/examples). Zie voor een bijgewerkte lijst met ondersteunde providers voor Azure Hallo [Terraform documentatie](https://www.terraform.io/docs/providers/azurerm/index.html).
