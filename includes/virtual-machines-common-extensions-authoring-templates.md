## <a name="overview-of-azure-resource-manager-templates"></a><span data-ttu-id="eb56f-101">Overzicht van Azure Resource Manager-sjablonen</span><span class="sxs-lookup"><span data-stu-id="eb56f-101">Overview of Azure Resource Manager templates</span></span>
<span data-ttu-id="eb56f-102">Azure Resource Manager-sjablonen kunnen u verklarend opgeven van de infrastructuur van Azure IaaS in Json-taal door te definiëren van de afhankelijkheden tussen resources.</span><span class="sxs-lookup"><span data-stu-id="eb56f-102">Azure Resource Manager templates allow you to declaratively specify the Azure IaaS infrastructure in Json language by defining the dependencies between resources.</span></span> <span data-ttu-id="eb56f-103">Raadpleeg de onderstaande artikel voor een gedetailleerd overzicht van Azure Resource Manager-sjablonen:</span><span class="sxs-lookup"><span data-stu-id="eb56f-103">For a detailed overview of Azure Resource Manager Templates, please refer to the article below:</span></span>

[<span data-ttu-id="eb56f-104">Overzicht van de resourcegroep</span><span class="sxs-lookup"><span data-stu-id="eb56f-104">Resource Group Overview</span></span>](../articles/azure-resource-manager/resource-group-overview.md)

## <a name="sample-template-snippet-for-vm-extensions"></a><span data-ttu-id="eb56f-105">Voorbeeld sjabloon codefragment voor VM-extensies</span><span class="sxs-lookup"><span data-stu-id="eb56f-105">Sample template snippet for VM extensions</span></span>
<span data-ttu-id="eb56f-106">Sjabloon moet VM-extensies implementeren als onderdeel van een Azure Resource Manager u de configuratie van de extensie declaratief opgeven in de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="eb56f-106">Deploying VM extensions as part of an Azure Resource Manager template requires you to declaratively specify the extension configuration in the template.</span></span>
<span data-ttu-id="eb56f-107">Hier is de indeling voor het opgeven van de configuratie voor de uitbreiding.</span><span class="sxs-lookup"><span data-stu-id="eb56f-107">Here is the format for specifying the extension configuration.</span></span>

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

<span data-ttu-id="eb56f-108">Zoals u in de bovenstaande zien kunt, bevat de extensie sjabloon twee hoofdonderdelen:</span><span class="sxs-lookup"><span data-stu-id="eb56f-108">As you can see from the above, the extension template contains two main parts:</span></span>

1. <span data-ttu-id="eb56f-109">Naam, uitgever en versie</span><span class="sxs-lookup"><span data-stu-id="eb56f-109">Extension name, publisher and version</span></span>
2. <span data-ttu-id="eb56f-110">Configuratie van de uitbreiding.</span><span class="sxs-lookup"><span data-stu-id="eb56f-110">Extension Configuration.</span></span>

## <a name="identifying-the-publisher-type-and-typehandlerversion-for-any-extension"></a><span data-ttu-id="eb56f-111">Identificatie van de uitgever, het type en de typeHandlerVersion voor elke extensie</span><span class="sxs-lookup"><span data-stu-id="eb56f-111">Identifying the publisher, type, and typeHandlerVersion for any extension</span></span>
<span data-ttu-id="eb56f-112">Azure VM-extensies zijn gepubliceerd door Microsoft en vertrouwd 3e partij uitgevers en elke uitbreiding wordt uniek geïdentificeerd door de uitgever, het type en de typeHandlerVersion.</span><span class="sxs-lookup"><span data-stu-id="eb56f-112">Azure VM extensions are published by Microsoft and trusted 3rd party publishers and each extension is uniquely identified by its publisher,type and the typeHandlerVersion.</span></span> <span data-ttu-id="eb56f-113">Deze kunnen worden bepaald als volgt:</span><span class="sxs-lookup"><span data-stu-id="eb56f-113">These can be determined as following:</span></span>  

