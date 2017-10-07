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
# <a name="network-resource-provider"></a>Netwerkresourceprovider
Een basis-behoefte in hedendaagse business geslaagd, is Hallo mogelijkheid toobuild en op grote schaal netwerk-toepassingen op een flexibele, flexibele, veilige en herhaalbare manier beheren. Azure Resource Manager kunt u toocreate toepassingen, zoals één verzameling van resources in resourcegroepen. Deze resources worden beheerd via verschillende resourceproviders onder Resource Manager.

Azure Resource Manager, is afhankelijk van andere resource providers tooprovide toegang tot tooyour bronnen. Er zijn drie belangrijkste resourceproviders: netwerk, opslag en berekeningen. Dit document wordt besproken Hallo kenmerken en voordelen van Hallo Netwerkresourceprovider, met inbegrip van:

* **Metagegevens** – u kunt informatie tooresources met tags toevoegen. Deze tags mag gebruikte tootrack Resourcegebruik in resourcegroepen en abonnementen.
* **Meer controle over uw netwerk** - netwerkbronnen los zijn gekoppeld en u ze op een meer gedetailleerd wijze kunt beheren. Dit betekent dat u meer flexibiliteit bij het beheren van Hallo netwerkresources.
* **Snellere configuratie** -omdat netwerkbronnen los zijn gekoppeld, kunt u maken en organiseren netwerkbronnen parallel. Dit is aanzienlijk verminderd configuratie.
* **Op rollen gebaseerd toegangsbeheer** -RBAC standaardrollen aan specifieke beveiligingsbereik bij toevoeging tooallowing Hallo maken van aangepaste rollen voor beveiligde management biedt.
* **Eenvoudiger beheer en implementatie** -het is eenvoudiger toodeploy en beheren van toepassingen sinds kunt kunt u een volledige toepassing stack als één verzameling van resources in een resourcegroep. En snellere toodeploy, omdat u implementeren kunt met alleen het leveren van een sjabloon JSON-nettolading.
* **Snelle aanpassing** -kunt u sjablonen van declaratieve-stijl tooenable herhaalbare en snelle aanpassing van implementaties.
* **Herhaalbare aanpassing** -kunt u sjablonen van declaratieve-stijl tooenable herhaalbare en snelle aanpassing van implementaties.
* **Beheerinterfaces** -kunt u een van de volgende interfaces toomanage Hallo uw resources:
  * REST gebaseerde API
  * PowerShell
  * .NET SDK
  * Node.JS-SDK
  * Java-SDK
  * Azure CLI
  * Preview-portal
  * Sjabloontaal van Resource Manager

## <a name="network-resources"></a>Netwerkbronnen
U kunt nu netwerkbronnen onafhankelijk, beheren in plaats van ze allemaal beheerd via een enkel compute-resource (een virtuele machine). Dit zorgt ervoor dat een hogere mate van flexibiliteit en aanpassingsvermogen bij het schrijven van een complex en grote schaal infrastructuur in een resourcegroep.

Een conceptuele weergave van een voorbeeldimplementatie met betrekking tot een toepassing met meerdere lagen wordt hieronder weergegeven. Elke bron die u, zoals NIC's, openbare IP-adressen en virtuele machines ziet, kan afzonderlijk worden beheerd.

![Netwerk resourcemodel](./media/resource-groups-networking/Figure2.png)

Elke bron bevat een gemeenschappelijke set eigenschappen en hun afzonderlijke eigenschap ingesteld. algemene eigenschappen voor Hallo zijn:

| Eigenschap | Beschrijving | Voorbeeldwaarden |
| --- | --- | --- |
| **naam** |Unieke resourcenaam. Elk resourcetype heeft een eigen naamsbeperkingen. |PIP01, VM01, NIC01 |
| **location** |Azure-regio in welke Hallo bron zich bevindt |westus, eastus |
| **ID** |Unieke identificatie van de URI op basis van |/Subscriptions/<subGUID>/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP |

U kunt afzonderlijke eigenschappen van resources in de volgende secties voor Hallo Hallo controleren.

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

## <a name="management-interfaces"></a>Beheerinterfaces
U kunt met behulp van verschillende interfaces Azure VPN-resources kunt beheren. In dit document gaan we in op kabel van deze interfaces: REST-API en sjablonen.

### <a name="rest-api"></a>REST API
Zoals eerder vermeld, kunnen de netwerkbronnen worden beheerd via diverse interfaces, inclusief REST-API, .NET SDK, SDK voor Node.JS, Java SDK, PowerShell, CLI, Azure Portal en sjablonen.

Hallo Rest API voldoen toohello HTTP 1.1-protocol-specificatie. Hallo algemene URI structuur van Hallo API wordt hieronder weergegeven:

    https://management.azure.com/subscriptions/{subscription-id}/providers/{resource-provider-namespace}/locations/{region-location}/register?api-version={api-version}

En Hallo parameters accolades vertegenwoordigen Hallo volgende elementen:

* **abonnement-id** -uw Azure-abonnement-id.
* **naamruimte van een resource provider** -naamruimte voor Hallo provider die wordt gebruikt. Hallo-waarde voor de netwerkresourceprovider Hallo is *Microsoft.Network*.
* **naam van het gebied** -naam van de Azure-regio Hallo

Hallo worden volgende HTTP-methoden ondersteund bij het maken van aanroepen toohello REST-API:

* **PUT** : wordt gebruikt toocreate resource van een bepaald type, een broneigenschap of een koppeling tussen resources wijzigen.
* **OPHALEN van** -tooretrieve informatie voor een ingerichte bron gebruikt.
* **Verwijder** -toodelete een bestaande resource gebruikt.

Zowel Hallo-aanvraag en -antwoord voldoen tooa JSON-nettolading indeling. Zie voor meer informatie [Azure Resource Management API's](https://msdn.microsoft.com/library/azure/dn948464.aspx).

### <a name="resource-manager-template-language"></a>Sjabloontaal van Resource Manager
U kunt ook een declaratieve programming stijl toobuild gebruiken en netwerkbronnen beheren met behulp van Hallo sjabloontaal Resource Manager, in toevoeging toomanaging bronnen imperatively (via API's of SDK).

Een voorbeeld-weergave van een sjabloon wordt hieronder:

    {
      "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
      "contentVersion": "<version-number-of-template>",
      "parameters": { <parameter-definitions-of-template> },
      "variables": { <variable-definitions-of-template> },
      "resources": [ { <definition-of-resource-to-deploy> } ],
      "outputs": { <output-of-template> }    
    }

Hallo-sjabloon is voornamelijk een JSON-beschrijving van Hallo bronnen en Hallo exemplaarwaarden opgenomen via parameters. Hallo in het volgende voorbeeld mag gebruikte toocreate een virtueel netwerk met 2 subnetten.

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

U hebt de mogelijkheid Hallo Hallo parameterwaarden handmatig te bieden wanneer een sjabloon gebruikt, of kunt u een parameterbestand. Hallo in het volgende voorbeeld toont een mogelijke reeks parameter waarden toobe met bovenstaande Hallo-sjabloon gebruikt:

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


belangrijkste voordelen van het gebruik van sjablonen Hallo zijn:

* U kunt een complexe infrastructuur in een resourcegroep in een declaratieve style opbouwen. Hallo orchestration van het Hallo-bronnen, waaronder het Afhankelijkheidsbeheer van maken, wordt verwerkt door Resource Manager.
* Hallo-infrastructuur kan worden gemaakt op een herhaalbare manier over verschillende regio's en binnen een regio gewoon door parameters te wijzigen.
* Hallo declaratieve stijl leidt tooshorter doorlooptijd bij het opbouwen van Hallo sjablonen en implementeren van Hallo-infrastructuur.

Zie voor voorbeeldsjablonen [Azure-snelstartsjablonen](https://github.com/Azure/azure-quickstart-templates).

Zie voor meer informatie over Hallo sjabloontaal Resource Manager [Azure Resource Manager sjabloontaal](../azure-resource-manager/resource-group-authoring-templates.md).

Hallo voorbeeldsjabloon bovenstaande gebruikt Hallo virtueel netwerk en bronnen van het subnet. Er zijn andere netwerkbronnen die kunt u onderstaande:

### <a name="using-a-template"></a>Met behulp van een sjabloon
U kunt services tooAzure vanuit een sjabloon implementeren met behulp van PowerShell, AzureCLI, of door het uitvoeren van een toodeploy Klik vanuit GitHub. toodeploy services van een sjabloon in GitHub, uitvoeren Hallo stappen:

1. Hallo template3 bestand openen vanuit GitHub. Open bijvoorbeeld [virtueel netwerk met twee subnetten](https://github.com/Azure/azure-quickstart-templates/tree/master/101-virtual-network).
2. Klik op **tooAzure implementeren**, en vervolgens weer aanmelden op toohello Azure-portal met uw referenties.
3. Controleer of de sjabloon Hallo en klik vervolgens op **opslaan**.
4. Klik op **parameters bewerken** en selecteer een locatie zoals *VS-West*, voor Hallo vnet en subnetten.
5. Wijzig indien nodig, Hallo **ADDRESSPREFIX** en **SUBNETPREFIX** parameters en klik vervolgens op **OK**.
6. Klik op **Selecteer een resourcegroep** en klik vervolgens op Hallo resourcegroep gewenste tooadd hello vnet en subnetten aan. U kunt ook een nieuwe resourcegroep maken door te klikken op **of nieuwe maken**.
7. Klik op **Create**. Let op Hallo tegel om weer te geven **inrichting sjabloonimplementatie**. Nadat het Hallo-implementatie is voltooid, ziet u een scherm vergelijkbare tooone hieronder.

![Voorbeeld sjabloonimplementatie](./media/resource-groups-networking/Figure6.png)

## <a name="next-steps"></a>Volgende stappen
[Taal van Azure Resource Manager-sjabloon](../azure-resource-manager/resource-group-authoring-templates.md)

[Azure-netwerken – gebruikte sjablonen](https://github.com/Azure/azure-quickstart-templates)

[Azure Resource Manager versus klassieke implementatie](../azure-resource-manager/resource-manager-deployment-model.md)

[Overzicht van Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)

