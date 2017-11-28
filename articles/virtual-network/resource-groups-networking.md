---
title: aaaNetwork Resource Provider overzicht | Microsoft Docs
description: Meer informatie over Hallo nieuwe Netwerkresourceprovider in Azure Resource Manager
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 79bf09da-4809-45cb-8d21-705616ef24dc
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: 81b8f51fe8ee180d8f7885c6e04eb953904d7be5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="network-resource-provider"></a><span data-ttu-id="a28e7-103">Netwerkresourceprovider</span><span class="sxs-lookup"><span data-stu-id="a28e7-103">Network Resource Provider</span></span>
<span data-ttu-id="a28e7-104">Een basis-behoefte in hedendaagse business geslaagd, is Hallo mogelijkheid toobuild en op grote schaal netwerk-toepassingen op een flexibele, flexibele, veilige en herhaalbare manier beheren.</span><span class="sxs-lookup"><span data-stu-id="a28e7-104">An underpinning need in today’s business success, is hello ability toobuild and manage large scale network aware applications in an agile, flexible, secure and repeatable way.</span></span> <span data-ttu-id="a28e7-105">Azure Resource Manager kunt u toocreate toepassingen, zoals één verzameling van resources in resourcegroepen.</span><span class="sxs-lookup"><span data-stu-id="a28e7-105">Azure Resource Manager enables you toocreate such applications, as a single collection of resources in resource groups.</span></span> <span data-ttu-id="a28e7-106">Deze resources worden beheerd via verschillende resourceproviders onder Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a28e7-106">Such resources are managed through various resource providers under Resource Manager.</span></span>

<span data-ttu-id="a28e7-107">Azure Resource Manager, is afhankelijk van andere resource providers tooprovide toegang tot tooyour bronnen.</span><span class="sxs-lookup"><span data-stu-id="a28e7-107">Azure Resource Manager relies on different resource providers tooprovide access tooyour resources.</span></span> <span data-ttu-id="a28e7-108">Er zijn drie belangrijkste resourceproviders: netwerk, opslag en berekeningen.</span><span class="sxs-lookup"><span data-stu-id="a28e7-108">There are three main resource providers: Network, Storage and Compute.</span></span> <span data-ttu-id="a28e7-109">Dit document wordt besproken Hallo kenmerken en voordelen van Hallo Netwerkresourceprovider, met inbegrip van:</span><span class="sxs-lookup"><span data-stu-id="a28e7-109">This document discusses hello characteristics and benefits of hello Network Resource Provider, including:</span></span>

* <span data-ttu-id="a28e7-110">**Metagegevens** – u kunt informatie tooresources met tags toevoegen.</span><span class="sxs-lookup"><span data-stu-id="a28e7-110">**Metadata** – you can add information tooresources using tags.</span></span> <span data-ttu-id="a28e7-111">Deze tags mag gebruikte tootrack Resourcegebruik in resourcegroepen en abonnementen.</span><span class="sxs-lookup"><span data-stu-id="a28e7-111">These tags can be used tootrack resource utilization across resource groups and subscriptions.</span></span>
* <span data-ttu-id="a28e7-112">**Meer controle over uw netwerk** - netwerkbronnen los zijn gekoppeld en u ze op een meer gedetailleerd wijze kunt beheren.</span><span class="sxs-lookup"><span data-stu-id="a28e7-112">**Greater control of your network** - network resources are loosely coupled and you can control them in a more granular fashion.</span></span> <span data-ttu-id="a28e7-113">Dit betekent dat u meer flexibiliteit bij het beheren van Hallo netwerkresources.</span><span class="sxs-lookup"><span data-stu-id="a28e7-113">This means you have more flexibility in managing hello networking resources.</span></span>
* <span data-ttu-id="a28e7-114">**Snellere configuratie** -omdat netwerkbronnen los zijn gekoppeld, kunt u maken en organiseren netwerkbronnen parallel.</span><span class="sxs-lookup"><span data-stu-id="a28e7-114">**Faster configuration** - because network resources are loosely coupled, you can create and orchestrate network resources in parallel.</span></span> <span data-ttu-id="a28e7-115">Dit is aanzienlijk verminderd configuratie.</span><span class="sxs-lookup"><span data-stu-id="a28e7-115">This has drastically reduced configuration time.</span></span>
* <span data-ttu-id="a28e7-116">**Op rollen gebaseerd toegangsbeheer** -RBAC standaardrollen aan specifieke beveiligingsbereik bij toevoeging tooallowing Hallo maken van aangepaste rollen voor beveiligde management biedt.</span><span class="sxs-lookup"><span data-stu-id="a28e7-116">**Role Based Access Control** - RBAC provides default roles, with specific security scope, in addition tooallowing hello creation of custom roles for secure management.</span></span>
* <span data-ttu-id="a28e7-117">**Eenvoudiger beheer en implementatie** -het is eenvoudiger toodeploy en beheren van toepassingen sinds kunt kunt u een volledige toepassing stack als één verzameling van resources in een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="a28e7-117">**Easier management and deployment** - it’s easier toodeploy and manage applications since you can can create an entire application stack as a single collection of resources in a resource group.</span></span> <span data-ttu-id="a28e7-118">En snellere toodeploy, omdat u implementeren kunt met alleen het leveren van een sjabloon JSON-nettolading.</span><span class="sxs-lookup"><span data-stu-id="a28e7-118">And faster toodeploy, since you can deploy by simply providing a template JSON payload.</span></span>
* <span data-ttu-id="a28e7-119">**Snelle aanpassing** -kunt u sjablonen van declaratieve-stijl tooenable herhaalbare en snelle aanpassing van implementaties.</span><span class="sxs-lookup"><span data-stu-id="a28e7-119">**Rapid customization** - you can use declarative-style templates tooenable repeatable and rapid customization of deployments.</span></span>
* <span data-ttu-id="a28e7-120">**Herhaalbare aanpassing** -kunt u sjablonen van declaratieve-stijl tooenable herhaalbare en snelle aanpassing van implementaties.</span><span class="sxs-lookup"><span data-stu-id="a28e7-120">**Repeatable customization** - you can use declarative-style templates tooenable repeatable and rapid customization of deployments.</span></span>
* <span data-ttu-id="a28e7-121">**Beheerinterfaces** -kunt u een van de volgende interfaces toomanage Hallo uw resources:</span><span class="sxs-lookup"><span data-stu-id="a28e7-121">**Management interfaces** - you can use any of hello following interfaces toomanage your resources:</span></span>
  * <span data-ttu-id="a28e7-122">REST gebaseerde API</span><span class="sxs-lookup"><span data-stu-id="a28e7-122">REST based API</span></span>
  * <span data-ttu-id="a28e7-123">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a28e7-123">PowerShell</span></span>
  * <span data-ttu-id="a28e7-124">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="a28e7-124">.NET SDK</span></span>
  * <span data-ttu-id="a28e7-125">Node.JS-SDK</span><span class="sxs-lookup"><span data-stu-id="a28e7-125">Node.JS SDK</span></span>
  * <span data-ttu-id="a28e7-126">Java-SDK</span><span class="sxs-lookup"><span data-stu-id="a28e7-126">Java SDK</span></span>
  * <span data-ttu-id="a28e7-127">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a28e7-127">Azure CLI</span></span>
  * <span data-ttu-id="a28e7-128">Preview-portal</span><span class="sxs-lookup"><span data-stu-id="a28e7-128">Preview Portal</span></span>
  * <span data-ttu-id="a28e7-129">Sjabloontaal van Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a28e7-129">Resource Manager template language</span></span>

## <a name="network-resources"></a><span data-ttu-id="a28e7-130">Netwerkbronnen</span><span class="sxs-lookup"><span data-stu-id="a28e7-130">Network resources</span></span>
<span data-ttu-id="a28e7-131">U kunt nu netwerkbronnen onafhankelijk, beheren in plaats van ze allemaal beheerd via een enkel compute-resource (een virtuele machine).</span><span class="sxs-lookup"><span data-stu-id="a28e7-131">You can now manage network resources independently, instead of having them all managed through a single compute resource (a virtual machine).</span></span> <span data-ttu-id="a28e7-132">Dit zorgt ervoor dat een hogere mate van flexibiliteit en aanpassingsvermogen bij het schrijven van een complex en grote schaal infrastructuur in een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="a28e7-132">This ensures a higher degree of flexibility and agility in composing a complex and large scale infrastructure in a resource group.</span></span>

<span data-ttu-id="a28e7-133">Een conceptuele weergave van een voorbeeldimplementatie met betrekking tot een toepassing met meerdere lagen wordt hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a28e7-133">A conceptual view of a sample deployment involving a multi-tiered application is presented below.</span></span> <span data-ttu-id="a28e7-134">Elke bron die u, zoals NIC's, openbare IP-adressen en virtuele machines ziet, kan afzonderlijk worden beheerd.</span><span class="sxs-lookup"><span data-stu-id="a28e7-134">Each resource you see, such as NICs, public IP addresses, and VMs, can be managed independently.</span></span>

![Netwerk resourcemodel](./media/resource-groups-networking/Figure2.png)

<span data-ttu-id="a28e7-136">Elke bron bevat een gemeenschappelijke set eigenschappen en hun afzonderlijke eigenschap ingesteld.</span><span class="sxs-lookup"><span data-stu-id="a28e7-136">Every resource contains a common set of properties, and their individual property set.</span></span> <span data-ttu-id="a28e7-137">algemene eigenschappen voor Hallo zijn:</span><span class="sxs-lookup"><span data-stu-id="a28e7-137">hello common properties are:</span></span>

| <span data-ttu-id="a28e7-138">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="a28e7-138">Property</span></span> | <span data-ttu-id="a28e7-139">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a28e7-139">Description</span></span> | <span data-ttu-id="a28e7-140">Voorbeeldwaarden</span><span class="sxs-lookup"><span data-stu-id="a28e7-140">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a28e7-141">**naam**</span><span class="sxs-lookup"><span data-stu-id="a28e7-141">**name**</span></span> |<span data-ttu-id="a28e7-142">Unieke resourcenaam.</span><span class="sxs-lookup"><span data-stu-id="a28e7-142">Unique resource name.</span></span> <span data-ttu-id="a28e7-143">Elk resourcetype heeft een eigen naamsbeperkingen.</span><span class="sxs-lookup"><span data-stu-id="a28e7-143">Each resource type has its own naming restrictions.</span></span> |<span data-ttu-id="a28e7-144">PIP01, VM01, NIC01</span><span class="sxs-lookup"><span data-stu-id="a28e7-144">PIP01, VM01, NIC01</span></span> |
| <span data-ttu-id="a28e7-145">**location**</span><span class="sxs-lookup"><span data-stu-id="a28e7-145">**location**</span></span> |<span data-ttu-id="a28e7-146">Azure-regio in welke Hallo bron zich bevindt</span><span class="sxs-lookup"><span data-stu-id="a28e7-146">Azure region in which hello resource resides</span></span> |<span data-ttu-id="a28e7-147">westus, eastus</span><span class="sxs-lookup"><span data-stu-id="a28e7-147">westus, eastus</span></span> |
| <span data-ttu-id="a28e7-148">**ID**</span><span class="sxs-lookup"><span data-stu-id="a28e7-148">**id**</span></span> |<span data-ttu-id="a28e7-149">Unieke identificatie van de URI op basis van</span><span class="sxs-lookup"><span data-stu-id="a28e7-149">Unique URI based identification</span></span> |<span data-ttu-id="a28e7-150">/Subscriptions/<subGUID>/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP</span><span class="sxs-lookup"><span data-stu-id="a28e7-150">/subscriptions/<subGUID>/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP</span></span> |

<span data-ttu-id="a28e7-151">U kunt afzonderlijke eigenschappen van resources in de volgende secties voor Hallo Hallo controleren.</span><span class="sxs-lookup"><span data-stu-id="a28e7-151">You can check hello individual properties of resources in hello sections below.</span></span>

[!INCLUDE [virtual-networks-nrp-pip-include](../../includes/virtual-networks-nrp-pip-include.md)]

[!INCLUDE [virtual-networks-nrp-nic-include](../../includes/virtual-networks-nrp-nic-include.md)]

[!INCLUDE [virtual-networks-nrp-nsg-include](../../includes/virtual-networks-nrp-nsg-include.md)]

[!INCLUDE [virtual-networks-nrp-udr-include](../../includes/virtual-networks-nrp-udr-include.md)]

[!INCLUDE [virtual-networks-nrp-vnet-include](../../includes/virtual-networks-nrp-vnet-include.md)]

[!INCLUDE [virtual-networks-nrp-dns-include](../../includes/virtual-networks-nrp-dns-include.md)]

[!INCLUDE [virtual-networks-nrp-lb-include](../../includes/virtual-networks-nrp-lb-include.md)]

[!INCLUDE [virtual-networks-nrp-appgw-include](../../includes/virtual-networks-nrp-appgw-include.md)]

[!INCLUDE [virtual-networks-nrp-vpn-include](../../includes/virtual-networks-nrp-vpn-include.md)]

[!INCLUDE [virtual-networks-nrp-tm-include](../../includes/virtual-networks-nrp-tm-include.md)]

## <a name="management-interfaces"></a><span data-ttu-id="a28e7-152">Beheerinterfaces</span><span class="sxs-lookup"><span data-stu-id="a28e7-152">Management interfaces</span></span>
<span data-ttu-id="a28e7-153">U kunt met behulp van verschillende interfaces Azure VPN-resources kunt beheren.</span><span class="sxs-lookup"><span data-stu-id="a28e7-153">You can manage your Azure networking resources using different interfaces.</span></span> <span data-ttu-id="a28e7-154">In dit document gaan we in op kabel van deze interfaces: REST-API en sjablonen.</span><span class="sxs-lookup"><span data-stu-id="a28e7-154">In this document we will focus on tow of those interfaces: REST API, and templates.</span></span>

### <a name="rest-api"></a><span data-ttu-id="a28e7-155">REST API</span><span class="sxs-lookup"><span data-stu-id="a28e7-155">REST API</span></span>
<span data-ttu-id="a28e7-156">Zoals eerder vermeld, kunnen de netwerkbronnen worden beheerd via diverse interfaces, inclusief REST-API, .NET SDK, SDK voor Node.JS, Java SDK, PowerShell, CLI, Azure Portal en sjablonen.</span><span class="sxs-lookup"><span data-stu-id="a28e7-156">As mentioned earlier, network resources can be managed via a variety of interfaces, including REST API,.NET SDK, Node.JS SDK, Java SDK, PowerShell, CLI, Azure Portal and templates.</span></span>

<span data-ttu-id="a28e7-157">Hallo Rest API voldoen toohello HTTP 1.1-protocol-specificatie.</span><span class="sxs-lookup"><span data-stu-id="a28e7-157">hello Rest API’s conform toohello HTTP 1.1 protocol specification.</span></span> <span data-ttu-id="a28e7-158">Hallo algemene URI structuur van Hallo API wordt hieronder weergegeven:</span><span class="sxs-lookup"><span data-stu-id="a28e7-158">hello general URI structure of hello API is presented below:</span></span>

    https://management.azure.com/subscriptions/{subscription-id}/providers/{resource-provider-namespace}/locations/{region-location}/register?api-version={api-version}

<span data-ttu-id="a28e7-159">En Hallo parameters accolades vertegenwoordigen Hallo volgende elementen:</span><span class="sxs-lookup"><span data-stu-id="a28e7-159">And hello parameters in braces represent hello following elements:</span></span>

* <span data-ttu-id="a28e7-160">**abonnement-id** -uw Azure-abonnement-id.</span><span class="sxs-lookup"><span data-stu-id="a28e7-160">**subscription-id** - your Azure subscription id.</span></span>
* <span data-ttu-id="a28e7-161">**naamruimte van een resource provider** -naamruimte voor Hallo provider die wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a28e7-161">**resource-provider-namespace** - namespace for hello provider being used.</span></span> <span data-ttu-id="a28e7-162">Hallo-waarde voor de netwerkresourceprovider Hallo is *Microsoft.Network*.</span><span class="sxs-lookup"><span data-stu-id="a28e7-162">hello value for hello network resource provider is *Microsoft.Network*.</span></span>
* <span data-ttu-id="a28e7-163">**naam van het gebied** -naam van de Azure-regio Hallo</span><span class="sxs-lookup"><span data-stu-id="a28e7-163">**region-name** - hello Azure region name</span></span>

<span data-ttu-id="a28e7-164">Hallo worden volgende HTTP-methoden ondersteund bij het maken van aanroepen toohello REST-API:</span><span class="sxs-lookup"><span data-stu-id="a28e7-164">hello following HTTP methods are supported when making calls toohello REST API:</span></span>

* <span data-ttu-id="a28e7-165">**PUT** : wordt gebruikt toocreate resource van een bepaald type, een broneigenschap of een koppeling tussen resources wijzigen.</span><span class="sxs-lookup"><span data-stu-id="a28e7-165">**PUT** - used toocreate a resource of a given type, modify a resource property or change an association between resources.</span></span>
* <span data-ttu-id="a28e7-166">**OPHALEN van** -tooretrieve informatie voor een ingerichte bron gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a28e7-166">**GET** - used tooretrieve information for a provisioned resource.</span></span>
* <span data-ttu-id="a28e7-167">**Verwijder** -toodelete een bestaande resource gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a28e7-167">**DELETE** - used toodelete an existing resource.</span></span>

<span data-ttu-id="a28e7-168">Zowel Hallo-aanvraag en -antwoord voldoen tooa JSON-nettolading indeling.</span><span class="sxs-lookup"><span data-stu-id="a28e7-168">Both hello request and response conform tooa JSON payload format.</span></span> <span data-ttu-id="a28e7-169">Zie voor meer informatie [Azure Resource Management API's](https://msdn.microsoft.com/library/azure/dn948464.aspx).</span><span class="sxs-lookup"><span data-stu-id="a28e7-169">For more details, see [Azure Resource Management APIs](https://msdn.microsoft.com/library/azure/dn948464.aspx).</span></span>

### <a name="resource-manager-template-language"></a><span data-ttu-id="a28e7-170">Sjabloontaal van Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a28e7-170">Resource Manager template language</span></span>
<span data-ttu-id="a28e7-171">U kunt ook een declaratieve programming stijl toobuild gebruiken en netwerkbronnen beheren met behulp van Hallo sjabloontaal Resource Manager, in toevoeging toomanaging bronnen imperatively (via API's of SDK).</span><span class="sxs-lookup"><span data-stu-id="a28e7-171">In addition toomanaging resources imperatively (via APIs or SDK), you can also use a declarative programming style toobuild and manage network resources by using hello Resource Manager Template Language.</span></span>

<span data-ttu-id="a28e7-172">Een voorbeeld-weergave van een sjabloon wordt hieronder:</span><span class="sxs-lookup"><span data-stu-id="a28e7-172">A sample representation of a template is provided below –</span></span>

    {
      "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
      "contentVersion": "<version-number-of-template>",
      "parameters": { <parameter-definitions-of-template> },
      "variables": { <variable-definitions-of-template> },
      "resources": [ { <definition-of-resource-to-deploy> } ],
      "outputs": { <output-of-template> }    
    }

<span data-ttu-id="a28e7-173">Hallo-sjabloon is voornamelijk een JSON-beschrijving van Hallo bronnen en Hallo exemplaarwaarden opgenomen via parameters.</span><span class="sxs-lookup"><span data-stu-id="a28e7-173">hello template is primarily a JSON description of hello resources and hello instance values injected via parameters.</span></span> <span data-ttu-id="a28e7-174">Hallo in het volgende voorbeeld mag gebruikte toocreate een virtueel netwerk met 2 subnetten.</span><span class="sxs-lookup"><span data-stu-id="a28e7-174">hello example below can be used toocreate a virtual network with 2 subnets.</span></span>

    {
        "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/VNET.json",
        "contentVersion": "1.0.0.0",
        "parameters" : {
          "location": {
            "type": "String",
            "allowedValues": ["East US", "West US", "West Europe", "East Asia", "South East Asia"],
            "metadata" : {
              "Description" : "Deployment location"
            }
          },
          "virtualNetworkName":{
            "type" : "string",
            "defaultValue":"myVNET",
            "metadata" : {
              "Description" : "VNET name"
            }
          },
          "addressPrefix":{
            "type" : "string",
            "defaultValue" : "10.0.0.0/16",
            "metadata" : {
              "Description" : "Address prefix"
            }

          },
          "subnet1Name": {
            "type" : "string",
            "defaultValue" : "Subnet-1",
            "metadata" : {
              "Description" : "Subnet 1 Name"
            }
          },
          "subnet2Name": {
            "type" : "string",
            "defaultValue" : "Subnet-2",
            "metadata" : {
              "Description" : "Subnet 2 name"
            }
          },
          "subnet1Prefix" : {
            "type" : "string",
            "defaultValue" : "10.0.0.0/24",
            "metadata" : {
              "Description" : "Subnet 1 Prefix"
            }
          },
          "subnet2Prefix" : {
            "type" : "string",
            "defaultValue" : "10.0.1.0/24",
            "metadata" : {
              "Description" : "Subnet 2 Prefix"
            }
          }
        },
        "resources": [
        {
          "apiVersion": "2015-05-01-preview",
          "type": "Microsoft.Network/virtualNetworks",
          "name": "[parameters('virtualNetworkName')]",
          "location": "[parameters('location')]",
          "properties": {
            "addressSpace": {
              "addressPrefixes": [
                "[parameters('addressPrefix')]"
              ]
            },
            "subnets": [
              {
                "name": "[parameters('subnet1Name')]",
                "properties" : {
                  "addressPrefix": "[parameters('subnet1Prefix')]"
                }
              },
              {
                "name": "[parameters('subnet2Name')]",
                "properties" : {
                  "addressPrefix": "[parameters('subnet2Prefix')]"
                }
              }
            ]
          }
        }
        ]
    }

<span data-ttu-id="a28e7-175">U hebt de mogelijkheid Hallo Hallo parameterwaarden handmatig te bieden wanneer een sjabloon gebruikt, of kunt u een parameterbestand.</span><span class="sxs-lookup"><span data-stu-id="a28e7-175">You have hello option of providing hello parameter values manually when using a template, or you can use a parameter file.</span></span> <span data-ttu-id="a28e7-176">Hallo in het volgende voorbeeld toont een mogelijke reeks parameter waarden toobe met bovenstaande Hallo-sjabloon gebruikt:</span><span class="sxs-lookup"><span data-stu-id="a28e7-176">hello example below shows a possible set of parameter values toobe used with hello template above:</span></span>

    {
      "location": {
          "value": "East US"
      },
      "virtualNetworkName": {
          "value": "VNET1"
      },
      "subnet1Name": {
          "value": "Subnet1"
      },
      "subnet2Name": {
          "value": "Subnet2"
      },
      "addressPrefix": {
          "value": "192.168.0.0/16"
      },
      "subnet1Prefix": {
          "value": "192.168.1.0/24"
      },
      "subnet2Prefix": {
          "value": "192.168.2.0/24"
      }
    }


<span data-ttu-id="a28e7-177">belangrijkste voordelen van het gebruik van sjablonen Hallo zijn:</span><span class="sxs-lookup"><span data-stu-id="a28e7-177">hello main advantages of using templates are:</span></span>

* <span data-ttu-id="a28e7-178">U kunt een complexe infrastructuur in een resourcegroep in een declaratieve style opbouwen.</span><span class="sxs-lookup"><span data-stu-id="a28e7-178">You can build a complex infrastructure in a resource group in a declarative style.</span></span> <span data-ttu-id="a28e7-179">Hallo orchestration van het Hallo-bronnen, waaronder het Afhankelijkheidsbeheer van maken, wordt verwerkt door Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a28e7-179">hello orchestration of creating hello resources, including dependency management, is handled by Resource Manager.</span></span>
* <span data-ttu-id="a28e7-180">Hallo-infrastructuur kan worden gemaakt op een herhaalbare manier over verschillende regio's en binnen een regio gewoon door parameters te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="a28e7-180">hello infrastructure can be created in a repeatable way across various regions and within a region by simply changing parameters.</span></span>
* <span data-ttu-id="a28e7-181">Hallo declaratieve stijl leidt tooshorter doorlooptijd bij het opbouwen van Hallo sjablonen en implementeren van Hallo-infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="a28e7-181">hello declarative style leads tooshorter lead time in building hello templates and rolling out hello infrastructure.</span></span>

<span data-ttu-id="a28e7-182">Zie voor voorbeeldsjablonen [Azure-snelstartsjablonen](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="a28e7-182">For sample templates, see [Azure quickstart templates](https://github.com/Azure/azure-quickstart-templates).</span></span>

<span data-ttu-id="a28e7-183">Zie voor meer informatie over Hallo sjabloontaal Resource Manager [Azure Resource Manager sjabloontaal](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="a28e7-183">For more information on hello Resource Manager Template Language, see [Azure Resource Manager Template Language](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="a28e7-184">Hallo voorbeeldsjabloon bovenstaande gebruikt Hallo virtueel netwerk en bronnen van het subnet.</span><span class="sxs-lookup"><span data-stu-id="a28e7-184">hello sample template above uses hello virtual network and subnet resources.</span></span> <span data-ttu-id="a28e7-185">Er zijn andere netwerkbronnen die kunt u onderstaande:</span><span class="sxs-lookup"><span data-stu-id="a28e7-185">There are other network resources you can use as listed below:</span></span>

### <a name="using-a-template"></a><span data-ttu-id="a28e7-186">Met behulp van een sjabloon</span><span class="sxs-lookup"><span data-stu-id="a28e7-186">Using a template</span></span>
<span data-ttu-id="a28e7-187">U kunt services tooAzure vanuit een sjabloon implementeren met behulp van PowerShell, AzureCLI, of door het uitvoeren van een toodeploy Klik vanuit GitHub.</span><span class="sxs-lookup"><span data-stu-id="a28e7-187">You can deploy services tooAzure from a template by using PowerShell, AzureCLI, or by performing a click toodeploy from GitHub.</span></span> <span data-ttu-id="a28e7-188">toodeploy services van een sjabloon in GitHub, uitvoeren Hallo stappen:</span><span class="sxs-lookup"><span data-stu-id="a28e7-188">toodeploy services from a template in GitHub, execute hello following steps:</span></span>

1. <span data-ttu-id="a28e7-189">Hallo template3 bestand openen vanuit GitHub.</span><span class="sxs-lookup"><span data-stu-id="a28e7-189">Open hello template3 file from GitHub.</span></span> <span data-ttu-id="a28e7-190">Open bijvoorbeeld [virtueel netwerk met twee subnetten](https://github.com/Azure/azure-quickstart-templates/tree/master/101-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="a28e7-190">As an example, open [Virtual network with two subnets](https://github.com/Azure/azure-quickstart-templates/tree/master/101-virtual-network).</span></span>
2. <span data-ttu-id="a28e7-191">Klik op **tooAzure implementeren**, en vervolgens weer aanmelden op toohello Azure-portal met uw referenties.</span><span class="sxs-lookup"><span data-stu-id="a28e7-191">Click on **Deploy tooAzure**, and then sign in on toohello Azure portal with your credentials.</span></span>
3. <span data-ttu-id="a28e7-192">Controleer of de sjabloon Hallo en klik vervolgens op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="a28e7-192">Verify hello template, and then click **Save**.</span></span>
4. <span data-ttu-id="a28e7-193">Klik op **parameters bewerken** en selecteer een locatie zoals *VS-West*, voor Hallo vnet en subnetten.</span><span class="sxs-lookup"><span data-stu-id="a28e7-193">Click **Edit parameters** and select a location, such as *West US*, for hello vnet and subnets.</span></span>
5. <span data-ttu-id="a28e7-194">Wijzig indien nodig, Hallo **ADDRESSPREFIX** en **SUBNETPREFIX** parameters en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="a28e7-194">If necessary, change hello **ADDRESSPREFIX** and **SUBNETPREFIX** parameters, and then click **OK**.</span></span>
6. <span data-ttu-id="a28e7-195">Klik op **Selecteer een resourcegroep** en klik vervolgens op Hallo resourcegroep gewenste tooadd hello vnet en subnetten aan.</span><span class="sxs-lookup"><span data-stu-id="a28e7-195">Click **Select a resource group** and then click on hello resource group you want tooadd hello vnet and subnets to.</span></span> <span data-ttu-id="a28e7-196">U kunt ook een nieuwe resourcegroep maken door te klikken op **of nieuwe maken**.</span><span class="sxs-lookup"><span data-stu-id="a28e7-196">Alternatively, you can create a new resource group by clicking **Or create new**.</span></span>
7. <span data-ttu-id="a28e7-197">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="a28e7-197">Click **Create**.</span></span> <span data-ttu-id="a28e7-198">Let op Hallo tegel om weer te geven **inrichting sjabloonimplementatie**.</span><span class="sxs-lookup"><span data-stu-id="a28e7-198">Notice hello tile displaying **Provisioning Template deployment**.</span></span> <span data-ttu-id="a28e7-199">Nadat het Hallo-implementatie is voltooid, ziet u een scherm vergelijkbare tooone hieronder.</span><span class="sxs-lookup"><span data-stu-id="a28e7-199">Once hello deployment is done, you will see a screen similar tooone below.</span></span>

![Voorbeeld sjabloonimplementatie](./media/resource-groups-networking/Figure6.png)

## <a name="next-steps"></a><span data-ttu-id="a28e7-201">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a28e7-201">Next steps</span></span>
[<span data-ttu-id="a28e7-202">Taal van Azure Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="a28e7-202">Azure Resource Manager Template Language</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)

[<span data-ttu-id="a28e7-203">Azure-netwerken – gebruikte sjablonen</span><span class="sxs-lookup"><span data-stu-id="a28e7-203">Azure Networking – commonly used templates</span></span>](https://github.com/Azure/azure-quickstart-templates)

[<span data-ttu-id="a28e7-204">Azure Resource Manager versus klassieke implementatie</span><span class="sxs-lookup"><span data-stu-id="a28e7-204">Azure Resource Manager vs. classic deployment</span></span>](../azure-resource-manager/resource-manager-deployment-model.md)

[<span data-ttu-id="a28e7-205">Overzicht van Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a28e7-205">Azure Resource Manager Overview</span></span>](../azure-resource-manager/resource-group-overview.md)

