## <a name="overview-of-azure-resource-manager-templates"></a>Overzicht van Azure Resource Manager-sjablonen
Azure Resource Manager-sjablonen kunnen u verklarend opgeven van de infrastructuur van Azure IaaS in Json-taal door te definiëren van de afhankelijkheden tussen resources. Raadpleeg de onderstaande artikel voor een gedetailleerd overzicht van Azure Resource Manager-sjablonen:

[Overzicht van de resourcegroep](../articles/azure-resource-manager/resource-group-overview.md)

## <a name="sample-template-snippet-for-vm-extensions"></a>Voorbeeld sjabloon codefragment voor VM-extensies
Sjabloon moet VM-extensies implementeren als onderdeel van een Azure Resource Manager u de configuratie van de extensie declaratief opgeven in de sjabloon.
Hier is de indeling voor het opgeven van de configuratie voor de uitbreiding.

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

Zoals u in de bovenstaande zien kunt, bevat de extensie sjabloon twee hoofdonderdelen:

1. Naam, uitgever en versie
2. Configuratie van de uitbreiding.

## <a name="identifying-the-publisher-type-and-typehandlerversion-for-any-extension"></a>Identificatie van de uitgever, het type en de typeHandlerVersion voor elke extensie
Azure VM-extensies zijn gepubliceerd door Microsoft en vertrouwd 3e partij uitgevers en elke uitbreiding wordt uniek geïdentificeerd door de uitgever, het type en de typeHandlerVersion. Deze kunnen worden bepaald als volgt:  

