---
title: aaaPass complexe waarden tussen Azure-sjablonen | Microsoft Docs
description: Bevat aanbevolen methoden voor het gebruik van complexe objecten tooshare statusgegevens met Azure Resource Manager-sjablonen en gekoppelde sjablonen.
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
ms.openlocfilehash: 72df1dee351446cea6ce15269e6db288b1f1db79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="share-state-tooand-from-azure-resource-manager-templates"></a><span data-ttu-id="b1aad-103">Share status tooand van Azure Resource Manager-sjablonen</span><span class="sxs-lookup"><span data-stu-id="b1aad-103">Share state tooand from Azure Resource Manager templates</span></span>
<span data-ttu-id="b1aad-104">Dit onderwerp bevat aanbevolen procedures voor het beheren en delen van de status in sjablonen.</span><span class="sxs-lookup"><span data-stu-id="b1aad-104">This topic shows best practices for managing and sharing state within templates.</span></span> <span data-ttu-id="b1aad-105">Hallo parameters en variabelen die worden weergegeven in dit onderwerp vindt u voorbeelden van het type objecten die u kunt definiëren Hallo tooconveniently uw implementatievereisten organiseren.</span><span class="sxs-lookup"><span data-stu-id="b1aad-105">hello parameters and variables shown in this topic are examples of hello type of objects you can define tooconveniently organize your deployment requirements.</span></span> <span data-ttu-id="b1aad-106">U kunt uw eigen objecten met eigenschapswaarden die geschikt zijn voor uw omgeving implementeren van deze voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="b1aad-106">From these examples, you can implement your own objects with property values that make sense for your environment.</span></span>

<span data-ttu-id="b1aad-107">In dit onderwerp maakt deel uit van een grotere technisch document.</span><span class="sxs-lookup"><span data-stu-id="b1aad-107">This topic is part of a larger whitepaper.</span></span> <span data-ttu-id="b1aad-108">tooread hello volledige papier downloaden [World klasse Resource Manager-sjablonen overwegingen en procedures bewezen](http://download.microsoft.com/download/8/E/1/8E1DBEFA-CECE-4DC9-A813-93520A5D7CFE/World Class ARM Templates - Considerations and Proven Practices.pdf).</span><span class="sxs-lookup"><span data-stu-id="b1aad-108">tooread hello full paper, download [World Class Resource Manager Templates Considerations and Proven Practices](http://download.microsoft.com/download/8/E/1/8E1DBEFA-CECE-4DC9-A813-93520A5D7CFE/World Class ARM Templates - Considerations and Proven Practices.pdf).</span></span>

## <a name="provide-standard-configuration-settings"></a><span data-ttu-id="b1aad-109">Geef de standaardconfiguratie-instellingen</span><span class="sxs-lookup"><span data-stu-id="b1aad-109">Provide standard configuration settings</span></span>
<span data-ttu-id="b1aad-110">In plaats van een sjabloon die voorziet in totaal flexibiliteit en talloze variaties bieden, is een algemene patroon tooprovide een selectie van bekende configuraties.</span><span class="sxs-lookup"><span data-stu-id="b1aad-110">Rather than offer a template that provides total flexibility and countless variations, a common pattern is tooprovide a selection of known configurations.</span></span> <span data-ttu-id="b1aad-111">Gebruikers kunnen in feite standaard t-shirt grootten zoals sandbox, kleine, middelgrote en grote selecteren.</span><span class="sxs-lookup"><span data-stu-id="b1aad-111">In effect, users can select standard t-shirt sizes such as sandbox, small, medium, and large.</span></span> <span data-ttu-id="b1aad-112">Andere voorbeelden van t-shirt grootten zijn de producten, zoals community edition of enterprise edition.</span><span class="sxs-lookup"><span data-stu-id="b1aad-112">Other examples of t-shirt sizes are product offerings, such as community edition or enterprise edition.</span></span> <span data-ttu-id="b1aad-113">In andere gevallen mogelijk werklastspecifiek configuraties van een technologie – zoals kaart verminderen of er zijn geen sql.</span><span class="sxs-lookup"><span data-stu-id="b1aad-113">In other cases, it may be workload-specific configurations of a technology – such as map reduce or no sql.</span></span>

<span data-ttu-id="b1aad-114">U kunt met complexe objecten variabelen maken die verzamelingen van gegevens, ook wel aangeduid als 'Eigenschappenverzamelingen' bevatten en die gegevens toodrive Hallo de brondeclaratie gebruiken in uw sjabloon.</span><span class="sxs-lookup"><span data-stu-id="b1aad-114">With complex objects, you can create variables that contain collections of data, sometimes known as "property bags" and use that data toodrive hello resource declaration in your template.</span></span> <span data-ttu-id="b1aad-115">Deze aanpak geeft goede, bekende configuraties van verschillende grootten die vooraf zijn geconfigureerd voor klanten.</span><span class="sxs-lookup"><span data-stu-id="b1aad-115">This approach provides good, known configurations of varying sizes that are preconfigured for customers.</span></span> <span data-ttu-id="b1aad-116">Zonder bekende configuraties zijn de gebruikers van de sjabloon Hallo moeten cluster sizing op hun eigen, factor in resourcebeperkingen platform bepalen en de handelingen math tooidentify Hallo resulterende partitionering van storage-accounts en andere bronnen (vanwege toocluster grootte en resourcebeperkingen).</span><span class="sxs-lookup"><span data-stu-id="b1aad-116">Without known configurations, users of hello template must determine cluster sizing on their own, factor in platform resource constraints, and do math tooidentify hello resulting partitioning of storage accounts and other resources (due toocluster size and resource constraints).</span></span> <span data-ttu-id="b1aad-117">Bovendien toomaking een betere ervaring voor de klant hello, enkele bekende configuraties zijn eenvoudiger toosupport en kunnen u een hoger niveau van de dichtheid leveren.</span><span class="sxs-lookup"><span data-stu-id="b1aad-117">In addition toomaking a better experience for hello customer, a few known configurations are easier toosupport and can help you deliver a higher level of density.</span></span>

<span data-ttu-id="b1aad-118">Hallo volgende voorbeeld wordt getoond hoe toodefine variabelen die voor het voorstellen van verzamelingen van gegevens naar complexe objecten bevatten.</span><span class="sxs-lookup"><span data-stu-id="b1aad-118">hello following example shows how toodefine variables that contain complex objects for representing collections of data.</span></span> <span data-ttu-id="b1aad-119">Hallo verzamelingen definiëren waarden die worden gebruikt voor de grootte van virtuele machine, netwerkinstellingen, besturingssysteeminstellingen en instellingen voor beschikbaarheid.</span><span class="sxs-lookup"><span data-stu-id="b1aad-119">hello collections define values that are used for virtual machine size, network settings, operating system settings and availability settings.</span></span>

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

<span data-ttu-id="b1aad-120">U ziet dat Hallo **tshirtSize** variabele worden aaneengeschakeld Hallo t-shirt grootte die u hebt opgegeven via een parameter (**kleine**, **gemiddeld**, **grote**) toohello tekst **tshirtSize**.</span><span class="sxs-lookup"><span data-stu-id="b1aad-120">Notice that hello **tshirtSize** variable concatenates hello t-shirt size you provided through a parameter (**Small**, **Medium**, **Large**) toohello text **tshirtSize**.</span></span> <span data-ttu-id="b1aad-121">U gebruikt deze variabele tooretrieve Hallo gekoppeld complexe objectvariabele dat formaat t-shirt.</span><span class="sxs-lookup"><span data-stu-id="b1aad-121">You use this variable tooretrieve hello associated complex object variable for that t-shirt size.</span></span>

<span data-ttu-id="b1aad-122">Vervolgens kunt u deze variabelen verderop in de sjabloon Hallo raadplegen.</span><span class="sxs-lookup"><span data-stu-id="b1aad-122">You can then reference these variables later in hello template.</span></span> <span data-ttu-id="b1aad-123">Hallo mogelijkheid tooreference met de naam-variabelen en hun eigenschappen Hallo Sjabloonsyntaxis vereenvoudigt en maakt het eenvoudig toounderstand context.</span><span class="sxs-lookup"><span data-stu-id="b1aad-123">hello ability tooreference named-variables and their properties simplifies hello template syntax, and makes it easy toounderstand context.</span></span> <span data-ttu-id="b1aad-124">Hallo volgende voorbeeld definieert een toodeploy resource met behulp van Hallo-objecten die eerder tooset waarden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="b1aad-124">hello following example defines a resource toodeploy by using hello objects shown previously tooset values.</span></span> <span data-ttu-id="b1aad-125">Bijvoorbeeld, Hallo VM-grootte is ingesteld door op te halen Hallo-waarde voor `variables('tshirtSize').vmSize` tijdens het Hallo-waarde voor de schijfgrootte hello wordt opgehaald uit `variables('tshirtSize').diskSize`.</span><span class="sxs-lookup"><span data-stu-id="b1aad-125">For example, hello VM size is set by retrieving hello value for `variables('tshirtSize').vmSize` while hello value for hello disk size is retrieved from `variables('tshirtSize').diskSize`.</span></span> <span data-ttu-id="b1aad-126">Bovendien Hallo URI voor een gekoppelde sjabloon is ingesteld met een waarde voor Hallo `variables('tshirtSize').vmTemplate`.</span><span class="sxs-lookup"><span data-stu-id="b1aad-126">In addition, hello URI for a linked template is set with hello value for `variables('tshirtSize').vmTemplate`.</span></span>

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

## <a name="pass-state-tooa-template"></a><span data-ttu-id="b1aad-127">Status tooa sjabloon doorgeven</span><span class="sxs-lookup"><span data-stu-id="b1aad-127">Pass state tooa template</span></span>
<span data-ttu-id="b1aad-128">U delen staat in een sjabloon via parameters die u tijdens de implementatie opgeeft.</span><span class="sxs-lookup"><span data-stu-id="b1aad-128">You share state into a template through parameters that you provide directly during deployment.</span></span>

<span data-ttu-id="b1aad-129">Hallo volgende parameters voor een lijst met gebruikte in sjablonen.</span><span class="sxs-lookup"><span data-stu-id="b1aad-129">hello following table lists commonly used parameters in templates.</span></span>

| <span data-ttu-id="b1aad-130">Naam</span><span class="sxs-lookup"><span data-stu-id="b1aad-130">Name</span></span> | <span data-ttu-id="b1aad-131">Waarde</span><span class="sxs-lookup"><span data-stu-id="b1aad-131">Value</span></span> | <span data-ttu-id="b1aad-132">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b1aad-132">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b1aad-133">location</span><span class="sxs-lookup"><span data-stu-id="b1aad-133">location</span></span> |<span data-ttu-id="b1aad-134">De tekenreeks in een beperkte lijst met Azure-regio 's</span><span class="sxs-lookup"><span data-stu-id="b1aad-134">String from a constrained list of Azure regions</span></span> |<span data-ttu-id="b1aad-135">Hallo-locatie waar Hallo resources worden geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="b1aad-135">hello location where hello resources are deployed.</span></span> |
| <span data-ttu-id="b1aad-136">storageAccountNamePrefix</span><span class="sxs-lookup"><span data-stu-id="b1aad-136">storageAccountNamePrefix</span></span> |<span data-ttu-id="b1aad-137">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="b1aad-137">String</span></span> |<span data-ttu-id="b1aad-138">Unieke DNS-naam op voor Hallo Opslagaccount waar Hallo van de virtuele machine-schijven worden geplaatst</span><span class="sxs-lookup"><span data-stu-id="b1aad-138">Unique DNS name for hello Storage Account where hello VM's disks are placed</span></span> |
| <span data-ttu-id="b1aad-139">Domeinnaam</span><span class="sxs-lookup"><span data-stu-id="b1aad-139">domainName</span></span> |<span data-ttu-id="b1aad-140">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="b1aad-140">String</span></span> |<span data-ttu-id="b1aad-141">Domeinnaam van Hallo openbaar toegankelijk jumpbox VM Hallo indeling: **{domainName}. { Location}.cloudapp.com** bijvoorbeeld: **mydomainname.westus.cloudapp.azure.com**</span><span class="sxs-lookup"><span data-stu-id="b1aad-141">Domain name of hello publicly accessible jumpbox VM in hello format: **{domainName}.{location}.cloudapp.com** For example: **mydomainname.westus.cloudapp.azure.com**</span></span> |
| <span data-ttu-id="b1aad-142">adminUsername</span><span class="sxs-lookup"><span data-stu-id="b1aad-142">adminUsername</span></span> |<span data-ttu-id="b1aad-143">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="b1aad-143">String</span></span> |<span data-ttu-id="b1aad-144">Gebruikersnaam voor Hallo virtuele machines</span><span class="sxs-lookup"><span data-stu-id="b1aad-144">Username for hello VMs</span></span> |
| <span data-ttu-id="b1aad-145">adminPassword</span><span class="sxs-lookup"><span data-stu-id="b1aad-145">adminPassword</span></span> |<span data-ttu-id="b1aad-146">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="b1aad-146">String</span></span> |<span data-ttu-id="b1aad-147">Wachtwoord voor Hallo virtuele machines</span><span class="sxs-lookup"><span data-stu-id="b1aad-147">Password for hello VMs</span></span> |
| <span data-ttu-id="b1aad-148">tshirtSize</span><span class="sxs-lookup"><span data-stu-id="b1aad-148">tshirtSize</span></span> |<span data-ttu-id="b1aad-149">Tekenreeks van een beperkte lijst aangeboden t-shirt grootten</span><span class="sxs-lookup"><span data-stu-id="b1aad-149">String from a constrained list of offered t-shirt sizes</span></span> |<span data-ttu-id="b1aad-150">Hallo met de naam scale unit grootte tooprovision.</span><span class="sxs-lookup"><span data-stu-id="b1aad-150">hello named scale unit size tooprovision.</span></span> <span data-ttu-id="b1aad-151">Bijvoorbeeld 'Klein', 'Gemiddeld', 'Groot'</span><span class="sxs-lookup"><span data-stu-id="b1aad-151">For example, "Small", "Medium", "Large"</span></span> |
| <span data-ttu-id="b1aad-152">virtualNetworkName</span><span class="sxs-lookup"><span data-stu-id="b1aad-152">virtualNetworkName</span></span> |<span data-ttu-id="b1aad-153">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="b1aad-153">String</span></span> |<span data-ttu-id="b1aad-154">Naam van het virtuele netwerk Hallo die de consument Hallo wil toouse.</span><span class="sxs-lookup"><span data-stu-id="b1aad-154">Name of hello virtual network that hello consumer wants toouse.</span></span> |
| <span data-ttu-id="b1aad-155">enableJumpbox</span><span class="sxs-lookup"><span data-stu-id="b1aad-155">enableJumpbox</span></span> |<span data-ttu-id="b1aad-156">De tekenreeks in een beperkte lijst (ingeschakeld/uitgeschakeld)</span><span class="sxs-lookup"><span data-stu-id="b1aad-156">String from a constrained list (enabled/disabled)</span></span> |<span data-ttu-id="b1aad-157">Parameter die aangeeft of tooenable een jumpbox voor Hallo-omgeving.</span><span class="sxs-lookup"><span data-stu-id="b1aad-157">Parameter that identifies whether tooenable a jumpbox for hello environment.</span></span> <span data-ttu-id="b1aad-158">Waarden: "ingeschakeld", "uitgeschakeld"</span><span class="sxs-lookup"><span data-stu-id="b1aad-158">Values: "enabled", "disabled"</span></span> |

<span data-ttu-id="b1aad-159">Hallo **tshirtSize** parameter die wordt gebruikt in de vorige sectie Hallo is gedefinieerd als:</span><span class="sxs-lookup"><span data-stu-id="b1aad-159">hello **tshirtSize** parameter used in hello previous section is defined as:</span></span>

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
          "Description": "T-shirt size of hello MongoDB deployment"
        }
      }
    }


## <a name="pass-state-toolinked-templates"></a><span data-ttu-id="b1aad-160">Status toolinked sjablonen doorgeven</span><span class="sxs-lookup"><span data-stu-id="b1aad-160">Pass state toolinked templates</span></span>
<span data-ttu-id="b1aad-161">Wanneer u verbinding maakt toolinked sjablonen, vaak gebruik een combinatie van statische en variabelen gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="b1aad-161">When connecting toolinked templates, you often use a mix of static and generated variables.</span></span>

### <a name="static-variables"></a><span data-ttu-id="b1aad-162">Statische variabelen</span><span class="sxs-lookup"><span data-stu-id="b1aad-162">Static variables</span></span>
<span data-ttu-id="b1aad-163">Statische variabelen zijn vaak gebruikte tooprovide basiswaarden, zoals URL's die in een sjabloon worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b1aad-163">Static variables are often used tooprovide base values, such as URLs, that are used throughout a template.</span></span>

<span data-ttu-id="b1aad-164">In Hallo volgende fragment van de sjabloon, `templateBaseUrl` Hiermee geeft u de hoofdlocatie Hallo voor Hallo-sjabloon in GitHub.</span><span class="sxs-lookup"><span data-stu-id="b1aad-164">In hello following template excerpt, `templateBaseUrl` specifies hello root location for hello template in GitHub.</span></span> <span data-ttu-id="b1aad-165">de volgende regel Hallo bouwt u een nieuwe variabele `sharedTemplateUrl` die Hallo basis-URL met bekende naam Hallo van Hallo gedeelde bronnen sjabloon worden aaneengeschakeld.</span><span class="sxs-lookup"><span data-stu-id="b1aad-165">hello next line builds a new variable `sharedTemplateUrl` that concatenates hello base URL with hello known name of hello shared resources template.</span></span> <span data-ttu-id="b1aad-166">Onder deze regel een variabele complexe object is gebruikte toostore een grootte t-shirt waarbij Hallo basis-URL aaneengeschakelde toohello bekende locatie van de configuratie-sjabloon en opgeslagen in Hallo `vmTemplate` eigenschap.</span><span class="sxs-lookup"><span data-stu-id="b1aad-166">Below that line, a complex object variable is used toostore a t-shirt size, where hello base URL is concatenated toohello known configuration template location and stored in hello `vmTemplate` property.</span></span>

<span data-ttu-id="b1aad-167">Hallo voordeel van deze benadering is dat als locatie van de sjabloon hello wordt gewijzigd, hoeft u alleen toochange Hallo statische variabele op één plek die wordt doorgegeven in de gehele Hallo gekoppelde sjablonen.</span><span class="sxs-lookup"><span data-stu-id="b1aad-167">hello benefit of this approach is that if hello template location changes, you only need toochange hello static variable in one place, which passes it throughout hello linked templates.</span></span>

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

### <a name="generated-variables"></a><span data-ttu-id="b1aad-168">Variabelen voor de gegenereerde</span><span class="sxs-lookup"><span data-stu-id="b1aad-168">Generated variables</span></span>
<span data-ttu-id="b1aad-169">Meerdere variabelen worden in toevoeging toostatic variabelen, dynamisch gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="b1aad-169">In addition toostatic variables, several variables are generated dynamically.</span></span> <span data-ttu-id="b1aad-170">Deze sectie worden algemene typen gegenereerde variabelen Hallo.</span><span class="sxs-lookup"><span data-stu-id="b1aad-170">This section identifies some of hello common types of generated variables.</span></span>

#### <a name="tshirtsize"></a><span data-ttu-id="b1aad-171">tshirtSize</span><span class="sxs-lookup"><span data-stu-id="b1aad-171">tshirtSize</span></span>
<span data-ttu-id="b1aad-172">U bent bekend met deze variabele gegenereerde van Hallo bovenstaande voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="b1aad-172">You are familiar with this generated variable from hello examples above.</span></span>

#### <a name="networksettings"></a><span data-ttu-id="b1aad-173">networkSettings</span><span class="sxs-lookup"><span data-stu-id="b1aad-173">networkSettings</span></span>
<span data-ttu-id="b1aad-174">In een Hallo capaciteit, mogelijkheid of bereik voor end-to-end-oplossingssjabloon maken gekoppelde sjablonen meestal resources die bestaan op een netwerk.</span><span class="sxs-lookup"><span data-stu-id="b1aad-174">In a capacity, capability, or end-to-end scoped solution template, hello linked templates typically create resources that exist on a network.</span></span> <span data-ttu-id="b1aad-175">Een eenvoudige benadering is toouse complexe object toostore netwerkinstellingen en ze toolinked sjablonen doorgeven.</span><span class="sxs-lookup"><span data-stu-id="b1aad-175">One straightforward approach is toouse a complex object toostore network settings and pass them toolinked templates.</span></span>

<span data-ttu-id="b1aad-176">Hieronder ziet u een voorbeeld van netwerkinstellingen communiceren.</span><span class="sxs-lookup"><span data-stu-id="b1aad-176">An example of communicating network settings can be seen below.</span></span>

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

#### <a name="availabilitysettings"></a><span data-ttu-id="b1aad-177">availabilitySettings</span><span class="sxs-lookup"><span data-stu-id="b1aad-177">availabilitySettings</span></span>
<span data-ttu-id="b1aad-178">Resources die zijn gemaakt in de gekoppelde sjablonen worden vaak geplaatst in een beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="b1aad-178">Resources created in linked templates are often placed in an availability set.</span></span> <span data-ttu-id="b1aad-179">In Hallo voorbeeld te volgen, naam van de beschikbaarheidsset Hallo is opgegeven en ook Hallo foutdomein en domein aantal toouse bijwerken.</span><span class="sxs-lookup"><span data-stu-id="b1aad-179">In hello following example, hello availability set name is specified and also hello fault domain and update domain count toouse.</span></span>

    "availabilitySetSettings": {
      "name": "pgsqlAvailabilitySet",
      "fdCount": 3,
      "udCount": 5
    }

<span data-ttu-id="b1aad-180">Als u meerdere beschikbaarheidssets (bijvoorbeeld één voor hoofdknooppunten) en een andere voor gegevensknooppunten, kunt u een naam op als een voorvoegsel moet, Geef meerdere beschikbaarheidssets of Hallo model eerder weergegeven voor het maken van een variabele voor een specifieke t-shirt grootte volgen.</span><span class="sxs-lookup"><span data-stu-id="b1aad-180">If you need multiple availability sets (for example, one for master nodes and another for data nodes), you can use a name as a prefix, specify multiple availability sets, or follow hello model shown earlier for creating a variable for a specific t-shirt size.</span></span>

#### <a name="storagesettings"></a><span data-ttu-id="b1aad-181">storageSettings</span><span class="sxs-lookup"><span data-stu-id="b1aad-181">storageSettings</span></span>
<span data-ttu-id="b1aad-182">Details van de opslag worden vaak gedeeld met gekoppelde sjablonen.</span><span class="sxs-lookup"><span data-stu-id="b1aad-182">Storage details are often shared with linked templates.</span></span> <span data-ttu-id="b1aad-183">In Hallo voorbeeld hieronder, een *storageSettings* object bevat informatie over Hallo storage-account en de container namen.</span><span class="sxs-lookup"><span data-stu-id="b1aad-183">In hello example below, a *storageSettings* object provides details about hello storage account and container names.</span></span>

    "storageSettings": {
        "vhdStorageAccountName": "[parameters('storageAccountName')]",
        "vhdContainerName": "[variables('vmStorageAccountContainerName')]",
        "destinationVhdsContainer": "[concat('https://', parameters('storageAccountName'), variables('vmStorageAccountDomain'), '/', variables('vmStorageAccountContainerName'), '/')]"
    }

#### <a name="ossettings"></a><span data-ttu-id="b1aad-184">osSettings</span><span class="sxs-lookup"><span data-stu-id="b1aad-184">osSettings</span></span>
<span data-ttu-id="b1aad-185">Met gekoppelde sjablonen moet u mogelijk toopass besturingssysteem instellingen toovarious knooppunten typen andere configuratie voor bekende typen.</span><span class="sxs-lookup"><span data-stu-id="b1aad-185">With linked templates, you may need toopass operating system settings toovarious nodes types across different known configuration types.</span></span> <span data-ttu-id="b1aad-186">Een complex object is een eenvoudige manier toostore en delen informatie over het besturingssysteem en maakt het ook eenvoudiger toosupport meerdere besturingssystemen kiezen voor implementatie.</span><span class="sxs-lookup"><span data-stu-id="b1aad-186">A complex object is an easy way toostore and share operating system information and also makes it easier toosupport multiple operating system choices for deployment.</span></span>

<span data-ttu-id="b1aad-187">Hallo volgende voorbeeld ziet u een object voor *osSettings*:</span><span class="sxs-lookup"><span data-stu-id="b1aad-187">hello following example shows an object for *osSettings*:</span></span>

    "osSettings": {
      "imageReference": {
        "publisher": "Canonical",
        "offer": "UbuntuServer",
        "sku": "14.04.2-LTS",
        "version": "latest"
      }
    }

#### <a name="machinesettings"></a><span data-ttu-id="b1aad-188">machineSettings</span><span class="sxs-lookup"><span data-stu-id="b1aad-188">machineSettings</span></span>
<span data-ttu-id="b1aad-189">Een gegenereerde variabele *machineSettings* is een complex object met een combinatie van core variabelen voor het maken van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="b1aad-189">A generated variable, *machineSettings* is a complex object containing a mix of core variables for creating a VM.</span></span> <span data-ttu-id="b1aad-190">Hallo-variabelen zijn beheerdersgebruikersnaam en wachtwoord, een voorvoegsel voor Hallo VM-namen en een verwijzing naar het afbeelding van het besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="b1aad-190">hello variables include administrator user name and password, a prefix for hello VM names, and an operating system image reference.</span></span>

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

<span data-ttu-id="b1aad-191">Houd er rekening mee dat *osImageReference* haalt de waarden van Hallo Hallo *osSettings* variabele in Hallo belangrijkste sjabloon worden gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="b1aad-191">Note that *osImageReference* retrieves hello values from hello *osSettings* variable defined in hello main template.</span></span> <span data-ttu-id="b1aad-192">Dit betekent dat u kunt eenvoudig hello besturingssysteem wijzigen voor een VM-geheel of op basis van Hallo voorkeur van de consument van een sjabloon.</span><span class="sxs-lookup"><span data-stu-id="b1aad-192">That means you can easily change hello operating system for a VM—entirely or based on hello preference of a template consumer.</span></span>

#### <a name="vmscripts"></a><span data-ttu-id="b1aad-193">vmScripts</span><span class="sxs-lookup"><span data-stu-id="b1aad-193">vmScripts</span></span>
<span data-ttu-id="b1aad-194">Hallo *vmScripts* object bevat details over Hallo scripts toodownload en uitvoeren op een VM-instantie, inclusief externe en interne verwijzingen.</span><span class="sxs-lookup"><span data-stu-id="b1aad-194">hello *vmScripts* object contains details about hello scripts toodownload and execute on a VM instance, including outside and inside references.</span></span> <span data-ttu-id="b1aad-195">Buiten bevatten verwijzingen Hallo-infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="b1aad-195">Outside references include hello infrastructure.</span></span>
<span data-ttu-id="b1aad-196">Binnen verwijzingen zijn hello geïnstalleerd software is geïnstalleerd en configuratie.</span><span class="sxs-lookup"><span data-stu-id="b1aad-196">Inside references include hello installed software installed and configuration.</span></span>

<span data-ttu-id="b1aad-197">Gebruik van Hallo *scriptsToDownload* eigenschap toolist Hallo scripts toodownload toohello VM.</span><span class="sxs-lookup"><span data-stu-id="b1aad-197">You use hello *scriptsToDownload* property toolist hello scripts toodownload toohello VM.</span></span> <span data-ttu-id="b1aad-198">Dit object bevat ook verwijzingen toocommand regel argumenten voor verschillende soorten acties.</span><span class="sxs-lookup"><span data-stu-id="b1aad-198">This object also contains references toocommand-line arguments for different types of actions.</span></span> <span data-ttu-id="b1aad-199">Deze acties omvatten het uitvoeren van de standaardinstallatie Hallo voor elke afzonderlijke knooppunten, een installatie die wordt uitgevoerd nadat alle knooppunten worden geïmplementeerd en eventuele extra scripts die mogelijk specifieke tooa opgegeven sjabloon.</span><span class="sxs-lookup"><span data-stu-id="b1aad-199">These actions include executing hello default installation for each individual node, an installation that runs after all nodes are deployed, and any additional scripts that may be specific tooa given template.</span></span>

<span data-ttu-id="b1aad-200">In dit voorbeeld is van een sjabloon die wordt gebruikt toodeploy MongoDB, die een hoge beschikbaarheid voor instellingen toodeliver vereist.</span><span class="sxs-lookup"><span data-stu-id="b1aad-200">This example is from a template used toodeploy MongoDB, which requires an arbiter toodeliver high availability.</span></span> <span data-ttu-id="b1aad-201">Hallo *arbiterNodeInstallCommand* te zijn toegevoegd*vmScripts* tooinstall Hallo instellingen.</span><span class="sxs-lookup"><span data-stu-id="b1aad-201">hello *arbiterNodeInstallCommand* has been added too*vmScripts* tooinstall hello arbiter.</span></span>

<span data-ttu-id="b1aad-202">sectie met sjabloonvariabelen Hallo is waar u Hallo variabelen die Hallo specifieke tekst tooexecute Hallo script met de juiste waarden Hallo definiëren vinden.</span><span class="sxs-lookup"><span data-stu-id="b1aad-202">hello variables section is where you find hello variables that define hello specific text tooexecute hello script with hello proper values.</span></span>

    "vmScripts": {
        "scriptsToDownload": [
            "[concat(variables('scriptUrl'), 'mongodb-', variables('osFamilySpec').osName, '-install.sh')]",
            "[concat(variables('sharedScriptUrl'), 'vm-disk-utils-0.1.sh')]"
        ],
        "regularNodeInstallCommand": "[variables('installCommand')]",
        "lastNodeInstallCommand": "[concat(variables('installCommand'), ' -l')]",
        "arbiterNodeInstallCommand": "[concat(variables('installCommand'), ' -a')]"
    },


## <a name="return-state-from-a-template"></a><span data-ttu-id="b1aad-203">Geretourneerde status van een sjabloon</span><span class="sxs-lookup"><span data-stu-id="b1aad-203">Return state from a template</span></span>
<span data-ttu-id="b1aad-204">Niet alleen kunt u gegevens doorgeven aan een sjabloon, kunt u ook share back toohello aanroepen gegevenssjabloon.</span><span class="sxs-lookup"><span data-stu-id="b1aad-204">Not only can you pass data into a template, you can also share data back toohello calling template.</span></span> <span data-ttu-id="b1aad-205">In Hallo **levert** gedeelte van een gekoppelde sjabloon, kunt u sleutel-waardeparen die kunnen worden gebruikt door de bronsjabloon Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="b1aad-205">In hello **outputs** section of a linked template, you can provide key/value pairs that can be consumed by hello source template.</span></span>

<span data-ttu-id="b1aad-206">Hallo volgende voorbeeld ziet u hoe toopass Hallo privé IP-adres in een gekoppelde sjabloon gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="b1aad-206">hello following example shows how toopass hello private IP address generated in a linked template.</span></span>

    "outputs": {
        "masterip": {
            "value": "[reference(concat(variables('nicName'),0)).ipConfigurations[0].properties.privateIPAddress]",
            "type": "string"
         }
    }

<span data-ttu-id="b1aad-207">In de belangrijkste sjabloon hello, kunt u die gegevens Hello de volgende syntaxis:</span><span class="sxs-lookup"><span data-stu-id="b1aad-207">Within hello main template, you can use that data with hello following syntax:</span></span>

    "[reference('master-node').outputs.masterip.value]"

<span data-ttu-id="b1aad-208">U kunt deze expressie in Hallo uitvoer sectie of Hallo resources gedeelte van de belangrijkste sjabloon hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b1aad-208">You can use this expression in either hello outputs section or hello resources section of hello main template.</span></span> <span data-ttu-id="b1aad-209">U kunt Hallo expressie gebruiken in de sectie met sjabloonvariabelen Hallo omdat is afhankelijk van de runtimestatus Hallo.</span><span class="sxs-lookup"><span data-stu-id="b1aad-209">You cannot use hello expression in hello variables section because it relies on hello runtime state.</span></span> <span data-ttu-id="b1aad-210">tooreturn hello belangrijkste sjabloon gebruiken voor deze waarde:</span><span class="sxs-lookup"><span data-stu-id="b1aad-210">tooreturn this value from hello main template, use:</span></span>

    "outputs": {
      "masterIpAddress": {
        "value": "[reference('master-node').outputs.masterip.value]",
        "type": "string"
      }

<span data-ttu-id="b1aad-211">Zie voor een voorbeeld van het gebruik van Hallo sectie van een gekoppelde sjabloon tooreturn gegevensschijven voor een virtuele machine levert, [meerdere gegevensschijven maken voor een virtuele Machine](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="b1aad-211">For an example of using hello outputs section of a linked template tooreturn data disks for a virtual machine, see [Creating multiple data disks for a Virtual Machine](resource-group-create-multiple.md).</span></span>

## <a name="define-authentication-settings-for-virtual-machine"></a><span data-ttu-id="b1aad-212">Verificatie-instellingen voor virtuele machine definiëren</span><span class="sxs-lookup"><span data-stu-id="b1aad-212">Define authentication settings for virtual machine</span></span>
<span data-ttu-id="b1aad-213">U kunt Hallo hetzelfde patroon dat eerder voor configuratie-instellingen toospecify Hallo verificatie-instellingen voor een virtuele machine wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="b1aad-213">You can use hello same pattern shown previously for configuration settings toospecify hello authentication settings for a virtual machine.</span></span> <span data-ttu-id="b1aad-214">U maakt een parameter voor het doorgeven in Hallo type verificatie.</span><span class="sxs-lookup"><span data-stu-id="b1aad-214">You create a parameter for passing in hello type of authentication.</span></span>

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

<span data-ttu-id="b1aad-215">U toevoegen variabelen voor de verschillende verificatietypen Hallo en een variabele toostore welk type wordt gebruikt voor deze implementatie op basis van de waarde van parameter Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="b1aad-215">You add variables for hello different authentication types, and a variable toostore which type is used for this deployment based on hello value of hello parameter.</span></span>

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

<span data-ttu-id="b1aad-216">Bij het definiëren van Hallo virtuele machine u Hallo instellen **osProfile** toohello variabele die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b1aad-216">When defining hello virtual machine, you set hello **osProfile** toohello variable you created.</span></span>

    {
      "type": "Microsoft.Compute/virtualMachines",
      ...
      "osProfile": "[variables('osProfile')]"
    }


## <a name="next-steps"></a><span data-ttu-id="b1aad-217">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b1aad-217">Next steps</span></span>
* <span data-ttu-id="b1aad-218">toolearn hello secties van de sjabloon hello, Zie [Azure Resource Manager-sjablonen ontwerpen](resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="b1aad-218">toolearn about hello sections of hello template, see [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md)</span></span>
* <span data-ttu-id="b1aad-219">Zie toosee Hallo functies die beschikbaar zijn in een sjabloon [Azure Resource Manager-sjabloonfuncties](resource-group-template-functions.md)</span><span class="sxs-lookup"><span data-stu-id="b1aad-219">toosee hello functions that are available within a template, see [Azure Resource Manager Template Functions](resource-group-template-functions.md)</span></span>
