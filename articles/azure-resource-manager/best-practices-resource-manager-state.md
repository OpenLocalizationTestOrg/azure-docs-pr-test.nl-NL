---
title: Complexe waarden doorgeven tussen Azure-sjablonen | Microsoft Docs
description: Bevat aanbevolen methoden voor het delen van gegevens van de gebruikersstatus met Azure Resource Manager-sjablonen en gekoppelde sjablonen met behulp van complexe objecten.
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: fd2f5e2d-d56d-4e01-a57d-34f3eaead4a9
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/26/2016
ms.author: tomfitz
ms.openlocfilehash: 23cc4321159a87b61c177b11381646af8bd9eb35
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="share-state-to-and-from-azure-resource-manager-templates"></a><span data-ttu-id="2c0bc-103">Status van de share naar en van Azure Resource Manager-sjablonen</span><span class="sxs-lookup"><span data-stu-id="2c0bc-103">Share state to and from Azure Resource Manager templates</span></span>
<span data-ttu-id="2c0bc-104">Dit onderwerp bevat aanbevolen procedures voor het beheren en delen van de status in sjablonen.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-104">This topic shows best practices for managing and sharing state within templates.</span></span> <span data-ttu-id="2c0bc-105">De parameters en variabelen die worden weergegeven in dit onderwerp vindt u voorbeelden van het type objecten u kunt gemakkelijk uw implementatievereisten te ordenen.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-105">The parameters and variables shown in this topic are examples of the type of objects you can define to conveniently organize your deployment requirements.</span></span> <span data-ttu-id="2c0bc-106">U kunt uw eigen objecten met eigenschapswaarden die geschikt zijn voor uw omgeving implementeren van deze voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-106">From these examples, you can implement your own objects with property values that make sense for your environment.</span></span>

<span data-ttu-id="2c0bc-107">In dit onderwerp maakt deel uit van een grotere technisch document.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-107">This topic is part of a larger whitepaper.</span></span> <span data-ttu-id="2c0bc-108">Om te lezen van het volledige papier, downloaden [World klasse Resource Manager-sjablonen overwegingen en procedures bewezen](http://download.microsoft.com/download/8/E/1/8E1DBEFA-CECE-4DC9-A813-93520A5D7CFE/World Class ARM Templates - Considerations and Proven Practices.pdf).</span><span class="sxs-lookup"><span data-stu-id="2c0bc-108">To read the full paper, download [World Class Resource Manager Templates Considerations and Proven Practices](http://download.microsoft.com/download/8/E/1/8E1DBEFA-CECE-4DC9-A813-93520A5D7CFE/World Class ARM Templates - Considerations and Proven Practices.pdf).</span></span>

## <a name="provide-standard-configuration-settings"></a><span data-ttu-id="2c0bc-109">Geef de standaardconfiguratie-instellingen</span><span class="sxs-lookup"><span data-stu-id="2c0bc-109">Provide standard configuration settings</span></span>
<span data-ttu-id="2c0bc-110">In plaats van een sjabloon die voorziet in totaal flexibiliteit en talloze variaties bieden, wordt een algemene patroon een selectie van bekende configuraties.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-110">Rather than offer a template that provides total flexibility and countless variations, a common pattern is to provide a selection of known configurations.</span></span> <span data-ttu-id="2c0bc-111">Gebruikers kunnen in feite standaard t-shirt grootten zoals sandbox, kleine, middelgrote en grote selecteren.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-111">In effect, users can select standard t-shirt sizes such as sandbox, small, medium, and large.</span></span> <span data-ttu-id="2c0bc-112">Andere voorbeelden van t-shirt grootten zijn de producten, zoals community edition of enterprise edition.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-112">Other examples of t-shirt sizes are product offerings, such as community edition or enterprise edition.</span></span> <span data-ttu-id="2c0bc-113">In andere gevallen mogelijk werklastspecifiek configuraties van een technologie – zoals kaart verminderen of er zijn geen sql.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-113">In other cases, it may be workload-specific configurations of a technology – such as map reduce or no sql.</span></span>

<span data-ttu-id="2c0bc-114">U kunt met complexe objecten variabelen maken die verzamelingen van gegevens, ook wel aangeduid als 'Eigenschappenverzamelingen' bevatten en die gegevens gebruiken om de resource-declaratie in uw sjabloon.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-114">With complex objects, you can create variables that contain collections of data, sometimes known as "property bags" and use that data to drive the resource declaration in your template.</span></span> <span data-ttu-id="2c0bc-115">Deze aanpak geeft goede, bekende configuraties van verschillende grootten die vooraf zijn geconfigureerd voor klanten.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-115">This approach provides good, known configurations of varying sizes that are preconfigured for customers.</span></span> <span data-ttu-id="2c0bc-116">Zonder bekende configuraties moeten gebruikers van de sjabloon cluster formaat op hun eigen bepalen, rekening te houden in resourcebeperkingen platform en rekenen om te identificeren van de resulterende partitionering van storage-accounts en andere bronnen (vanwege beperkingen van cluster grootte en resource).</span><span class="sxs-lookup"><span data-stu-id="2c0bc-116">Without known configurations, users of the template must determine cluster sizing on their own, factor in platform resource constraints, and do math to identify the resulting partitioning of storage accounts and other resources (due to cluster size and resource constraints).</span></span> <span data-ttu-id="2c0bc-117">Naast het maken van een betere ervaring voor de klant, enkele bekende configuraties zijn gemakkelijker te ondersteunen en kunt u een hoger niveau van de dichtheid leveren.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-117">In addition to making a better experience for the customer, a few known configurations are easier to support and can help you deliver a higher level of density.</span></span>

<span data-ttu-id="2c0bc-118">Het volgende voorbeeld laat zien hoe variabelen met complexe objecten voor het voorstellen van verzamelingen van gegevens definiëren.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-118">The following example shows how to define variables that contain complex objects for representing collections of data.</span></span> <span data-ttu-id="2c0bc-119">De verzamelingen definiëren waarden die worden gebruikt voor de grootte van virtuele machine, netwerkinstellingen, besturingssysteeminstellingen en instellingen voor beschikbaarheid.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-119">The collections define values that are used for virtual machine size, network settings, operating system settings and availability settings.</span></span>

    "variables": {
      "tshirtSize": "[variables(concat('tshirtSize', parameters('tshirtSize')))]",
      "tshirtSizeSmall": {
        "vmSize": "Standard_A1",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]",
        "vmCount": 2,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 1,
          "pool": "db",
          "map": [0,0],
          "jumpbox": 0
        }
      },
      "tshirtSizeMedium": {
        "vmSize": "Standard_A3",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-8disk-resources.json')]",
        "vmCount": 2,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 2,
          "pool": "db",
          "map": [0,1],
          "jumpbox": 0
        }
      },
      "tshirtSizeLarge": {
        "vmSize": "Standard_A4",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-16disk-resources.json')]",
        "vmCount": 3,
        "slaveCount": 2,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 2,
          "pool": "db",
          "map": [0,1,1],
          "jumpbox": 0
        }
      },
      "osSettings": {
        "scripts": [
          "[concat(variables('templateBaseUrl'), 'install_postgresql.sh')]",
          "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/shared_scripts/ubuntu/vm-disk-utils-0.1.sh"
        ],
        "imageReference": {
          "publisher": "Canonical",
          "offer": "UbuntuServer",
          "sku": "14.04.2-LTS",
          "version": "latest"
        }
      },
      "networkSettings": {
        "vnetName": "[parameters('virtualNetworkName')]",
        "addressPrefix": "10.0.0.0/16",
        "subnets": {
          "dmz": {
            "name": "dmz",
            "prefix": "10.0.0.0/24",
            "vnet": "[parameters('virtualNetworkName')]"
          },
          "data": {
            "name": "data",
            "prefix": "10.0.1.0/24",
            "vnet": "[parameters('virtualNetworkName')]"
          }
        }
      },
      "availabilitySetSettings": {
        "name": "pgsqlAvailabilitySet",
        "fdCount": 3,
        "udCount": 5
      }
    }

<span data-ttu-id="2c0bc-120">U ziet dat de **tshirtSize** variabele kan de grootte van de t-shirt die u hebt opgegeven via een parameter toevoegen (**kleine**, **gemiddeld**, **grote**) en de tekst **tshirtSize**.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-120">Notice that the **tshirtSize** variable concatenates the t-shirt size you provided through a parameter (**Small**, **Medium**, **Large**) to the text **tshirtSize**.</span></span> <span data-ttu-id="2c0bc-121">U kunt deze variabele gebruiken om op te halen van de bijbehorende complexe objectvariabele voor die t-shirt-grootte.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-121">You use this variable to retrieve the associated complex object variable for that t-shirt size.</span></span>

<span data-ttu-id="2c0bc-122">U kunt vervolgens verwijzen naar deze variabelen verderop in de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-122">You can then reference these variables later in the template.</span></span> <span data-ttu-id="2c0bc-123">De mogelijkheid om te verwijzen met de naam van de variabelen en hun eigenschappen vereenvoudigt de sjabloonsyntaxis van de en kunt u gemakkelijk om context te begrijpen.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-123">The ability to reference named-variables and their properties simplifies the template syntax, and makes it easy to understand context.</span></span> <span data-ttu-id="2c0bc-124">Het volgende voorbeeld definieert een resourcegroep implementeren met behulp van de objecten die eerder weergegeven waarden in te stellen.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-124">The following example defines a resource to deploy by using the objects shown previously to set values.</span></span> <span data-ttu-id="2c0bc-125">Bijvoorbeeld, de VM-grootte is ingesteld door op te halen van de waarde voor `variables('tshirtSize').vmSize` terwijl de waarde voor de schijfgrootte is opgehaald uit `variables('tshirtSize').diskSize`.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-125">For example, the VM size is set by retrieving the value for `variables('tshirtSize').vmSize` while the value for the disk size is retrieved from `variables('tshirtSize').diskSize`.</span></span> <span data-ttu-id="2c0bc-126">Bovendien de URI voor een gekoppelde sjabloon is ingesteld met de waarde voor `variables('tshirtSize').vmTemplate`.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-126">In addition, the URI for a linked template is set with the value for `variables('tshirtSize').vmTemplate`.</span></span>

    "name": "master-node",
    "type": "Microsoft.Resources/deployments",
    "apiVersion": "2015-01-01",
    "dependsOn": [
        "[concat('Microsoft.Resources/deployments/', 'shared')]"
    ],
    "properties": {
        "mode": "Incremental",
        "templateLink": {
          "uri": "[variables('tshirtSize').vmTemplate]",
          "contentVersion": "1.0.0.0"
        },
        "parameters": {
          "adminPassword": {
            "value": "[parameters('adminPassword')]"
          },
          "replicatorPassword": {
            "value": "[parameters('replicatorPassword')]"
          },
          "osSettings": {
            "value": "[variables('osSettings')]"
          },
          "subnet": {
            "value": "[variables('networkSettings').subnets.data]"
          },
          "commonSettings": {
            "value": {
              "region": "[parameters('region')]",
              "adminUsername": "[parameters('adminUsername')]",
              "namespace": "ms"
            }
          },
          "storageSettings": {
            "value":"[variables('tshirtSize').storage]"
          },
          "machineSettings": {
            "value": {
              "vmSize": "[variables('tshirtSize').vmSize]",
              "diskSize": "[variables('tshirtSize').diskSize]",
              "vmCount": 1,
              "availabilitySet": "[variables('availabilitySetSettings').name]"
            }
          },
          "masterIpAddress": {
            "value": "0"
          },
          "dbType": {
            "value": "MASTER"
          }
        }
      }
    }

## <a name="pass-state-to-a-template"></a><span data-ttu-id="2c0bc-127">Status doorgeven aan een sjabloon</span><span class="sxs-lookup"><span data-stu-id="2c0bc-127">Pass state to a template</span></span>
<span data-ttu-id="2c0bc-128">U delen staat in een sjabloon via parameters die u tijdens de implementatie opgeeft.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-128">You share state into a template through parameters that you provide directly during deployment.</span></span>

<span data-ttu-id="2c0bc-129">De volgende tabel bevat de meest gebruikte parameters in sjablonen.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-129">The following table lists commonly used parameters in templates.</span></span>

| <span data-ttu-id="2c0bc-130">Naam</span><span class="sxs-lookup"><span data-stu-id="2c0bc-130">Name</span></span> | <span data-ttu-id="2c0bc-131">Waarde</span><span class="sxs-lookup"><span data-stu-id="2c0bc-131">Value</span></span> | <span data-ttu-id="2c0bc-132">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="2c0bc-132">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2c0bc-133">location</span><span class="sxs-lookup"><span data-stu-id="2c0bc-133">location</span></span> |<span data-ttu-id="2c0bc-134">De tekenreeks in een beperkte lijst met Azure-regio 's</span><span class="sxs-lookup"><span data-stu-id="2c0bc-134">String from a constrained list of Azure regions</span></span> |<span data-ttu-id="2c0bc-135">De locatie waar de resources worden geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-135">The location where the resources are deployed.</span></span> |
| <span data-ttu-id="2c0bc-136">storageAccountNamePrefix</span><span class="sxs-lookup"><span data-stu-id="2c0bc-136">storageAccountNamePrefix</span></span> |<span data-ttu-id="2c0bc-137">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="2c0bc-137">String</span></span> |<span data-ttu-id="2c0bc-138">Unieke DNS-naam voor het Opslagaccount waarin de VM-schijven worden geplaatst</span><span class="sxs-lookup"><span data-stu-id="2c0bc-138">Unique DNS name for the Storage Account where the VM's disks are placed</span></span> |
| <span data-ttu-id="2c0bc-139">Domeinnaam</span><span class="sxs-lookup"><span data-stu-id="2c0bc-139">domainName</span></span> |<span data-ttu-id="2c0bc-140">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="2c0bc-140">String</span></span> |<span data-ttu-id="2c0bc-141">Domeinnaam van het openbaar toegankelijk jumpbox VM in de indeling: **{domainName}. { Location}.cloudapp.com** bijvoorbeeld: **mydomainname.westus.cloudapp.azure.com**</span><span class="sxs-lookup"><span data-stu-id="2c0bc-141">Domain name of the publicly accessible jumpbox VM in the format: **{domainName}.{location}.cloudapp.com** For example: **mydomainname.westus.cloudapp.azure.com**</span></span> |
| <span data-ttu-id="2c0bc-142">adminUsername</span><span class="sxs-lookup"><span data-stu-id="2c0bc-142">adminUsername</span></span> |<span data-ttu-id="2c0bc-143">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="2c0bc-143">String</span></span> |<span data-ttu-id="2c0bc-144">Gebruikersnaam voor de virtuele machines</span><span class="sxs-lookup"><span data-stu-id="2c0bc-144">Username for the VMs</span></span> |
| <span data-ttu-id="2c0bc-145">adminPassword</span><span class="sxs-lookup"><span data-stu-id="2c0bc-145">adminPassword</span></span> |<span data-ttu-id="2c0bc-146">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="2c0bc-146">String</span></span> |<span data-ttu-id="2c0bc-147">Wachtwoord voor de virtuele machines</span><span class="sxs-lookup"><span data-stu-id="2c0bc-147">Password for the VMs</span></span> |
| <span data-ttu-id="2c0bc-148">tshirtSize</span><span class="sxs-lookup"><span data-stu-id="2c0bc-148">tshirtSize</span></span> |<span data-ttu-id="2c0bc-149">Tekenreeks van een beperkte lijst aangeboden t-shirt grootten</span><span class="sxs-lookup"><span data-stu-id="2c0bc-149">String from a constrained list of offered t-shirt sizes</span></span> |<span data-ttu-id="2c0bc-150">De grootte van de eenheid benoemde schalen om in te richten.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-150">The named scale unit size to provision.</span></span> <span data-ttu-id="2c0bc-151">Bijvoorbeeld 'Klein', 'Gemiddeld', 'Groot'</span><span class="sxs-lookup"><span data-stu-id="2c0bc-151">For example, "Small", "Medium", "Large"</span></span> |
| <span data-ttu-id="2c0bc-152">virtualNetworkName</span><span class="sxs-lookup"><span data-stu-id="2c0bc-152">virtualNetworkName</span></span> |<span data-ttu-id="2c0bc-153">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="2c0bc-153">String</span></span> |<span data-ttu-id="2c0bc-154">Naam van het virtuele netwerk dat de gebruiker wil gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-154">Name of the virtual network that the consumer wants to use.</span></span> |
| <span data-ttu-id="2c0bc-155">enableJumpbox</span><span class="sxs-lookup"><span data-stu-id="2c0bc-155">enableJumpbox</span></span> |<span data-ttu-id="2c0bc-156">De tekenreeks in een beperkte lijst (ingeschakeld/uitgeschakeld)</span><span class="sxs-lookup"><span data-stu-id="2c0bc-156">String from a constrained list (enabled/disabled)</span></span> |<span data-ttu-id="2c0bc-157">De parameter die aangeeft of een jumpbox voor de omgeving wordt ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-157">Parameter that identifies whether to enable a jumpbox for the environment.</span></span> <span data-ttu-id="2c0bc-158">Waarden: "ingeschakeld", "uitgeschakeld"</span><span class="sxs-lookup"><span data-stu-id="2c0bc-158">Values: "enabled", "disabled"</span></span> |

<span data-ttu-id="2c0bc-159">De **tshirtSize** parameter die wordt gebruikt in de vorige sectie is gedefinieerd als:</span><span class="sxs-lookup"><span data-stu-id="2c0bc-159">The **tshirtSize** parameter used in the previous section is defined as:</span></span>

    "parameters": {
      "tshirtSize": {
        "type": "string",
        "defaultValue": "Small",
        "allowedValues": [
          "Small",
          "Medium",
          "Large"
        ],
        "metadata": {
          "Description": "T-shirt size of the MongoDB deployment"
        }
      }
    }


## <a name="pass-state-to-linked-templates"></a><span data-ttu-id="2c0bc-160">Status geven aan gekoppelde sjablonen</span><span class="sxs-lookup"><span data-stu-id="2c0bc-160">Pass state to linked templates</span></span>
<span data-ttu-id="2c0bc-161">Bij het verbinden met gekoppelde sjablonen, vaak gebruik van een combinatie van statische en variabelen gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-161">When connecting to linked templates, you often use a mix of static and generated variables.</span></span>

### <a name="static-variables"></a><span data-ttu-id="2c0bc-162">Statische variabelen</span><span class="sxs-lookup"><span data-stu-id="2c0bc-162">Static variables</span></span>
<span data-ttu-id="2c0bc-163">Statische variabelen worden vaak gebruikt base waarden, zoals URL's die worden gebruikt in een sjabloon op te geven.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-163">Static variables are often used to provide base values, such as URLs, that are used throughout a template.</span></span>

<span data-ttu-id="2c0bc-164">In het volgende fragment van de sjabloon `templateBaseUrl` geeft de hoofdmaplocatie voor de sjabloon in GitHub.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-164">In the following template excerpt, `templateBaseUrl` specifies the root location for the template in GitHub.</span></span> <span data-ttu-id="2c0bc-165">De volgende regel maakt een nieuwe variabele `sharedTemplateUrl` die de basis-URL met de bekende naam van de sjabloon gedeelde bronnen worden aaneengeschakeld.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-165">The next line builds a new variable `sharedTemplateUrl` that concatenates the base URL with the known name of the shared resources template.</span></span> <span data-ttu-id="2c0bc-166">Onder deze regel een variabele complexe object wordt gebruikt voor het opslaan van de grootte van een t-shirt, waarbij de basis-URL naar de locatie van de sjabloon bekende configuratie samengevoegd en opgeslagen in de `vmTemplate` eigenschap.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-166">Below that line, a complex object variable is used to store a t-shirt size, where the base URL is concatenated to the known configuration template location and stored in the `vmTemplate` property.</span></span>

<span data-ttu-id="2c0bc-167">Het voordeel van deze benadering is dat als de sjabloonlocatie wijzigt, u alleen hoeft de statische variabele op één plek die wordt doorgegeven in de gekoppelde sjablonen te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-167">The benefit of this approach is that if the template location changes, you only need to change the static variable in one place, which passes it throughout the linked templates.</span></span>

    "variables": {
      "templateBaseUrl": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/postgresql-on-ubuntu/",
      "sharedTemplateUrl": "[concat(variables('templateBaseUrl'), 'shared-resources.json')]",
      "tshirtSizeSmall": {
        "vmSize": "Standard_A1",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]",
        "vmCount": 2,
        "slaveCount": 1,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 1,
          "pool": "db",
          "map": [0,0],
          "jumpbox": 0
        }
      }
    }

### <a name="generated-variables"></a><span data-ttu-id="2c0bc-168">Variabelen voor de gegenereerde</span><span class="sxs-lookup"><span data-stu-id="2c0bc-168">Generated variables</span></span>
<span data-ttu-id="2c0bc-169">Naast statische variabelen worden verschillende variabelen dynamisch gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-169">In addition to static variables, several variables are generated dynamically.</span></span> <span data-ttu-id="2c0bc-170">Deze sectie worden enkele van de algemene typen gegenereerde variabelen.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-170">This section identifies some of the common types of generated variables.</span></span>

#### <a name="tshirtsize"></a><span data-ttu-id="2c0bc-171">tshirtSize</span><span class="sxs-lookup"><span data-stu-id="2c0bc-171">tshirtSize</span></span>
<span data-ttu-id="2c0bc-172">U bent bekend met deze gegenereerde variabele van de bovenstaande voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-172">You are familiar with this generated variable from the examples above.</span></span>

#### <a name="networksettings"></a><span data-ttu-id="2c0bc-173">networkSettings</span><span class="sxs-lookup"><span data-stu-id="2c0bc-173">networkSettings</span></span>
<span data-ttu-id="2c0bc-174">In een capaciteit, de mogelijkheid of de end-to-end bereik oplossingssjabloon maken de gekoppelde sjablonen meestal resources die bestaan op een netwerk.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-174">In a capacity, capability, or end-to-end scoped solution template, the linked templates typically create resources that exist on a network.</span></span> <span data-ttu-id="2c0bc-175">Een eenvoudige benadering is het gebruik van een complex object op te slaan netwerkinstellingen en aan de gekoppelde sjablonen door te geven.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-175">One straightforward approach is to use a complex object to store network settings and pass them to linked templates.</span></span>

<span data-ttu-id="2c0bc-176">Hieronder ziet u een voorbeeld van netwerkinstellingen communiceren.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-176">An example of communicating network settings can be seen below.</span></span>

    "networkSettings": {
      "vnetName": "[parameters('virtualNetworkName')]",
      "addressPrefix": "10.0.0.0/16",
      "subnets": {
        "dmz": {
          "name": "dmz",
          "prefix": "10.0.0.0/24",
          "vnet": "[parameters('virtualNetworkName')]"
        },
        "data": {
          "name": "data",
          "prefix": "10.0.1.0/24",
          "vnet": "[parameters('virtualNetworkName')]"
        }
      }
    }

#### <a name="availabilitysettings"></a><span data-ttu-id="2c0bc-177">availabilitySettings</span><span class="sxs-lookup"><span data-stu-id="2c0bc-177">availabilitySettings</span></span>
<span data-ttu-id="2c0bc-178">Resources die zijn gemaakt in de gekoppelde sjablonen worden vaak geplaatst in een beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-178">Resources created in linked templates are often placed in an availability set.</span></span> <span data-ttu-id="2c0bc-179">In het volgende voorbeeld wordt de naam van de beschikbaarheidsset is opgegeven en ook het domein met fouten en het updatedomein voor het gebruik van tellen.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-179">In the following example, the availability set name is specified and also the fault domain and update domain count to use.</span></span>

    "availabilitySetSettings": {
      "name": "pgsqlAvailabilitySet",
      "fdCount": 3,
      "udCount": 5
    }

<span data-ttu-id="2c0bc-180">Als u meerdere beschikbaarheidssets (bijvoorbeeld één voor hoofdknooppunten) en een andere voor gegevensknooppunten, kunt u een naam op als een voorvoegsel moet, meerdere beschikbaarheidssets opgeven of het model eerder weergegeven voor het maken van een variabele voor een specifieke t-shirt grootte volgen.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-180">If you need multiple availability sets (for example, one for master nodes and another for data nodes), you can use a name as a prefix, specify multiple availability sets, or follow the model shown earlier for creating a variable for a specific t-shirt size.</span></span>

#### <a name="storagesettings"></a><span data-ttu-id="2c0bc-181">storageSettings</span><span class="sxs-lookup"><span data-stu-id="2c0bc-181">storageSettings</span></span>
<span data-ttu-id="2c0bc-182">Details van de opslag worden vaak gedeeld met gekoppelde sjablonen.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-182">Storage details are often shared with linked templates.</span></span> <span data-ttu-id="2c0bc-183">In het voorbeeld hieronder, een *storageSettings* object bevat informatie over de namen van de storage-account en de container.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-183">In the example below, a *storageSettings* object provides details about the storage account and container names.</span></span>

    "storageSettings": {
        "vhdStorageAccountName": "[parameters('storageAccountName')]",
        "vhdContainerName": "[variables('vmStorageAccountContainerName')]",
        "destinationVhdsContainer": "[concat('https://', parameters('storageAccountName'), variables('vmStorageAccountDomain'), '/', variables('vmStorageAccountContainerName'), '/')]"
    }

#### <a name="ossettings"></a><span data-ttu-id="2c0bc-184">osSettings</span><span class="sxs-lookup"><span data-stu-id="2c0bc-184">osSettings</span></span>
<span data-ttu-id="2c0bc-185">Met gekoppelde sjablonen, moet u wellicht besturingssysteeminstellingen doorgeven aan verschillende knooppunten in verschillende andere configuratie voor bekende typen.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-185">With linked templates, you may need to pass operating system settings to various nodes types across different known configuration types.</span></span> <span data-ttu-id="2c0bc-186">Een complex object is een eenvoudige manier voor het opslaan en delen van informatie over het besturingssysteem en is het eenvoudiger voor de ondersteuning van meerdere besturingssystemen kiezen voor implementatie.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-186">A complex object is an easy way to store and share operating system information and also makes it easier to support multiple operating system choices for deployment.</span></span>

<span data-ttu-id="2c0bc-187">Het volgende voorbeeld ziet u een object voor *osSettings*:</span><span class="sxs-lookup"><span data-stu-id="2c0bc-187">The following example shows an object for *osSettings*:</span></span>

    "osSettings": {
      "imageReference": {
        "publisher": "Canonical",
        "offer": "UbuntuServer",
        "sku": "14.04.2-LTS",
        "version": "latest"
      }
    }

#### <a name="machinesettings"></a><span data-ttu-id="2c0bc-188">machineSettings</span><span class="sxs-lookup"><span data-stu-id="2c0bc-188">machineSettings</span></span>
<span data-ttu-id="2c0bc-189">Een gegenereerde variabele *machineSettings* is een complex object met een combinatie van core variabelen voor het maken van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-189">A generated variable, *machineSettings* is a complex object containing a mix of core variables for creating a VM.</span></span> <span data-ttu-id="2c0bc-190">De variabelen zijn gebruikersnaam en wachtwoord, een voorvoegsel voor de VM-namen en een verwijzing naar het afbeelding van het besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-190">The variables include administrator user name and password, a prefix for the VM names, and an operating system image reference.</span></span>

    "machineSettings": {
        "adminUsername": "[parameters('adminUsername')]",
        "adminPassword": "[parameters('adminPassword')]",
        "machineNamePrefix": "mongodb-",
        "osImageReference": {
            "publisher": "[variables('osFamilySpec').imagePublisher]",
            "offer": "[variables('osFamilySpec').imageOffer]",
            "sku": "[variables('osFamilySpec').imageSKU]",
            "version": "latest"
        }
    },

<span data-ttu-id="2c0bc-191">Houd er rekening mee dat *osImageReference* haalt de waarden van de *osSettings* variabele gedefinieerd in de belangrijkste sjabloon.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-191">Note that *osImageReference* retrieves the values from the *osSettings* variable defined in the main template.</span></span> <span data-ttu-id="2c0bc-192">Dit betekent dat u kunt gemakkelijk het besturingssysteem wijzigen voor een VM-geheel of op basis van de voorkeur van de consument van een sjabloon.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-192">That means you can easily change the operating system for a VM—entirely or based on the preference of a template consumer.</span></span>

#### <a name="vmscripts"></a><span data-ttu-id="2c0bc-193">vmScripts</span><span class="sxs-lookup"><span data-stu-id="2c0bc-193">vmScripts</span></span>
<span data-ttu-id="2c0bc-194">De *vmScripts* object bevat informatie over de scripts voor het downloaden en uitvoeren op een VM-instantie, inclusief externe en interne verwijzingen.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-194">The *vmScripts* object contains details about the scripts to download and execute on a VM instance, including outside and inside references.</span></span> <span data-ttu-id="2c0bc-195">Verwijzingen zijn buiten de infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-195">Outside references include the infrastructure.</span></span>
<span data-ttu-id="2c0bc-196">Binnen verwijzingen bevatten de geïnstalleerde software die is geïnstalleerd en de configuratie.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-196">Inside references include the installed software installed and configuration.</span></span>

<span data-ttu-id="2c0bc-197">U gebruikt de *scriptsToDownload* eigenschap voor een lijst met de scripts voor het downloaden van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-197">You use the *scriptsToDownload* property to list the scripts to download to the VM.</span></span> <span data-ttu-id="2c0bc-198">Dit object bevat ook verwijzingen naar opdrachtregelargumenten voor verschillende soorten acties.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-198">This object also contains references to command-line arguments for different types of actions.</span></span> <span data-ttu-id="2c0bc-199">Deze acties omvatten het uitvoeren van de standaardinstallatie voor elke afzonderlijke knooppunten, een installatie die wordt uitgevoerd nadat alle knooppunten worden geïmplementeerd en eventuele extra scripts die specifiek zijn voor een bepaalde sjabloon.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-199">These actions include executing the default installation for each individual node, an installation that runs after all nodes are deployed, and any additional scripts that may be specific to a given template.</span></span>

<span data-ttu-id="2c0bc-200">In dit voorbeeld is van een sjabloon die wordt gebruikt voor het implementeren van MongoDB, waarvoor een instellingen voor het leveren van hoge beschikbaarheid.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-200">This example is from a template used to deploy MongoDB, which requires an arbiter to deliver high availability.</span></span> <span data-ttu-id="2c0bc-201">De *arbiterNodeInstallCommand* is toegevoegd aan *vmScripts* voor het installeren van de instellingen.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-201">The *arbiterNodeInstallCommand* has been added to *vmScripts* to install the arbiter.</span></span>

<span data-ttu-id="2c0bc-202">De sectie met sjabloonvariabelen is waar het vinden van de variabelen die de specifieke tekst voor het uitvoeren van het script met de juiste waarden te definiëren.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-202">The variables section is where you find the variables that define the specific text to execute the script with the proper values.</span></span>

    "vmScripts": {
        "scriptsToDownload": [
            "[concat(variables('scriptUrl'), 'mongodb-', variables('osFamilySpec').osName, '-install.sh')]",
            "[concat(variables('sharedScriptUrl'), 'vm-disk-utils-0.1.sh')]"
        ],
        "regularNodeInstallCommand": "[variables('installCommand')]",
        "lastNodeInstallCommand": "[concat(variables('installCommand'), ' -l')]",
        "arbiterNodeInstallCommand": "[concat(variables('installCommand'), ' -a')]"
    },


## <a name="return-state-from-a-template"></a><span data-ttu-id="2c0bc-203">Geretourneerde status van een sjabloon</span><span class="sxs-lookup"><span data-stu-id="2c0bc-203">Return state from a template</span></span>
<span data-ttu-id="2c0bc-204">Niet alleen kunt u gegevens kunt doorgeven in een sjabloon kunt u ook gegevens terug naar de aanroepende sjabloon delen.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-204">Not only can you pass data into a template, you can also share data back to the calling template.</span></span> <span data-ttu-id="2c0bc-205">In de **levert** gedeelte van een gekoppelde sjabloon, kunt u sleutel-waardeparen die kunnen worden gebruikt door de bronsjabloon opgeven.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-205">In the **outputs** section of a linked template, you can provide key/value pairs that can be consumed by the source template.</span></span>

<span data-ttu-id="2c0bc-206">Het volgende voorbeeld laat zien hoe de privé IP-adres in een gekoppelde sjabloon gegenereerd doorgeven.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-206">The following example shows how to pass the private IP address generated in a linked template.</span></span>

    "outputs": {
        "masterip": {
            "value": "[reference(concat(variables('nicName'),0)).ipConfigurations[0].properties.privateIPAddress]",
            "type": "string"
         }
    }

<span data-ttu-id="2c0bc-207">In de belangrijkste sjabloon kunt u die gegevens gebruiken met de volgende syntaxis:</span><span class="sxs-lookup"><span data-stu-id="2c0bc-207">Within the main template, you can use that data with the following syntax:</span></span>

    "[reference('master-node').outputs.masterip.value]"

<span data-ttu-id="2c0bc-208">U kunt deze expressie in de sectie uitvoer of de sectie resources van de belangrijkste sjabloon gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-208">You can use this expression in either the outputs section or the resources section of the main template.</span></span> <span data-ttu-id="2c0bc-209">U kunt de expressie in het gedeelte variabelen niet gebruiken omdat deze afhankelijk van de runtimestatus van de is.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-209">You cannot use the expression in the variables section because it relies on the runtime state.</span></span> <span data-ttu-id="2c0bc-210">U kunt deze waarde van de belangrijkste sjabloon gebruiken:</span><span class="sxs-lookup"><span data-stu-id="2c0bc-210">To return this value from the main template, use:</span></span>

    "outputs": {
      "masterIpAddress": {
        "value": "[reference('master-node').outputs.masterip.value]",
        "type": "string"
      }

<span data-ttu-id="2c0bc-211">Zie voor een voorbeeld van het gebruik van de uitvoer-gedeelte van een gekoppelde sjabloon om terug te keren gegevensschijven voor een virtuele machine [meerdere gegevensschijven maken voor een virtuele Machine](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="2c0bc-211">For an example of using the outputs section of a linked template to return data disks for a virtual machine, see [Creating multiple data disks for a Virtual Machine](resource-group-create-multiple.md).</span></span>

## <a name="define-authentication-settings-for-virtual-machine"></a><span data-ttu-id="2c0bc-212">Verificatie-instellingen voor virtuele machine definiëren</span><span class="sxs-lookup"><span data-stu-id="2c0bc-212">Define authentication settings for virtual machine</span></span>
<span data-ttu-id="2c0bc-213">U kunt hetzelfde patroon eerder weergegeven voor configuratie-instellingen gebruiken om op te geven van de verificatie-instellingen voor een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-213">You can use the same pattern shown previously for configuration settings to specify the authentication settings for a virtual machine.</span></span> <span data-ttu-id="2c0bc-214">U maakt een parameter voor het doorgeven in het type verificatie.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-214">You create a parameter for passing in the type of authentication.</span></span>

    "parameters": {
      "authenticationType": {
        "allowedValues": [
          "password",
          "sshPublicKey"
        ],
        "defaultValue": "password",
        "metadata": {
          "description": "Authentication type"
        },
        "type": "string"
      }
    }

<span data-ttu-id="2c0bc-215">Toevoegen van variabelen voor de verschillende typen en een variabele voor het opslaan van welk type voor deze implementatie op basis van de waarde van de parameter wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-215">You add variables for the different authentication types, and a variable to store which type is used for this deployment based on the value of the parameter.</span></span>

    "variables": {
      "osProfile": "[variables(concat('osProfile', parameters('authenticationType')))]",
      "osProfilepassword": {
        "adminPassword": "[parameters('adminPassword')]",
        "adminUsername": "notused",
        "computerName": "[parameters('vmName')]",
        "customData": "[base64(variables('customData'))]"
      },
      "osProfilesshPublicKey": {
        "adminUsername": "notused",
        "computerName": "[parameters('vmName')]",
        "customData": "[base64(variables('customData'))]",
        "linuxConfiguration": {
          "disablePasswordAuthentication": "true",
          "ssh": {
            "publicKeys": [
              {
                "keyData": "[parameters('sshPublicKey')]",
                "path": "/home/notused/.ssh/authorized_keys"
              }
            ]
          }
        }
      }
    }

<span data-ttu-id="2c0bc-216">Bij het definiëren van de virtuele machine, stelt u de **osProfile** aan de variabele die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2c0bc-216">When defining the virtual machine, you set the **osProfile** to the variable you created.</span></span>

    {
      "type": "Microsoft.Compute/virtualMachines",
      ...
      "osProfile": "[variables('osProfile')]"
    }


## <a name="next-steps"></a><span data-ttu-id="2c0bc-217">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2c0bc-217">Next steps</span></span>
* <span data-ttu-id="2c0bc-218">Zie voor meer informatie over de secties van de sjabloon, [Azure Resource Manager-sjablonen ontwerpen](resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="2c0bc-218">To learn about the sections of the template, see [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md)</span></span>
* <span data-ttu-id="2c0bc-219">Zie voor de functies die beschikbaar in een sjabloon zijn [Azure Resource Manager-sjabloonfuncties](resource-group-template-functions.md)</span><span class="sxs-lookup"><span data-stu-id="2c0bc-219">To see the functions that are available within a template, see [Azure Resource Manager Template Functions](resource-group-template-functions.md)</span></span>
