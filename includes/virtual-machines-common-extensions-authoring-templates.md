## <a name="overview-of-azure-resource-manager-templates"></a>Overzicht van Azure Resource Manager-sjablonen
Azure Resource Manager-sjablonen kunt u toodeclaratively geven hello Azure IaaS-infrastructuur in Json-taal door Hallo afhankelijkheden tussen resources definiëren. Raadpleeg onderstaande toohello artikel voor een gedetailleerd overzicht van Azure Resource Manager-sjablonen:

[Overzicht van de resourcegroep](../articles/azure-resource-manager/resource-group-overview.md)

## <a name="sample-template-snippet-for-vm-extensions"></a>Voorbeeld sjabloon codefragment voor VM-extensies
VM-extensies implementeren als onderdeel van een Azure Resource Manager-sjabloon, moet u toodeclaratively opgeven voor de configuratie van de uitbreiding Hallo in Hallo sjabloon.
Hier wordt Hallo-indeling voor het opgeven van de configuratie van Hallo-uitbreiding.

      {
      "type": "Microsoft.Compute/virtualMachines/extensions",
      "name": "MyExtension",
      "apiVersion": "2015-05-01-preview",
      "location": "[parameters('location')]",
      "dependsOn": ["[concat('Microsoft.Compute/virtualMachines/',parameters('vmName'))]"],
      "properties":
      {
      "publisher": "Publisher Namespace",
      "type": "extension Name",
      "typeHandlerVersion": "extension version",
      "settings": {
      // Extension specific configuration goes in here.
      }
      }
      }

Zoals u in de bovenstaande Hallo zien kunt, bevat Hallo extensie sjabloon twee hoofdonderdelen:

1. Naam, uitgever en versie
2. Configuratie van de uitbreiding.

## <a name="identifying-hello-publisher-type-and-typehandlerversion-for-any-extension"></a>Hallo-uitgever, type en typeHandlerVersion voor elke extensie identificeren
Azure VM-extensies zijn gepubliceerd door Microsoft en vertrouwd 3e partij uitgevers en elke uitbreiding wordt uniek geïdentificeerd door de uitgever, type en Hallo typeHandlerVersion. Deze kunnen worden bepaald als volgt:  

