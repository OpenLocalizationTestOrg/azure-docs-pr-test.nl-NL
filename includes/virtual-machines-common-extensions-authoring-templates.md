## <a name="overview-of-azure-resource-manager-templates"></a><span data-ttu-id="ee957-101">Overzicht van Azure Resource Manager-sjablonen</span><span class="sxs-lookup"><span data-stu-id="ee957-101">Overview of Azure Resource Manager templates</span></span>
<span data-ttu-id="ee957-102">Azure Resource Manager-sjablonen kunt u toodeclaratively geven hello Azure IaaS-infrastructuur in Json-taal door Hallo afhankelijkheden tussen resources definiëren.</span><span class="sxs-lookup"><span data-stu-id="ee957-102">Azure Resource Manager templates allow you toodeclaratively specify hello Azure IaaS infrastructure in Json language by defining hello dependencies between resources.</span></span> <span data-ttu-id="ee957-103">Raadpleeg onderstaande toohello artikel voor een gedetailleerd overzicht van Azure Resource Manager-sjablonen:</span><span class="sxs-lookup"><span data-stu-id="ee957-103">For a detailed overview of Azure Resource Manager Templates, please refer toohello article below:</span></span>

[<span data-ttu-id="ee957-104">Overzicht van de resourcegroep</span><span class="sxs-lookup"><span data-stu-id="ee957-104">Resource Group Overview</span></span>](../articles/azure-resource-manager/resource-group-overview.md)

## <a name="sample-template-snippet-for-vm-extensions"></a><span data-ttu-id="ee957-105">Voorbeeld sjabloon codefragment voor VM-extensies</span><span class="sxs-lookup"><span data-stu-id="ee957-105">Sample template snippet for VM extensions</span></span>
<span data-ttu-id="ee957-106">VM-extensies implementeren als onderdeel van een Azure Resource Manager-sjabloon, moet u toodeclaratively opgeven voor de configuratie van de uitbreiding Hallo in Hallo sjabloon.</span><span class="sxs-lookup"><span data-stu-id="ee957-106">Deploying VM extensions as part of an Azure Resource Manager template requires you toodeclaratively specify hello extension configuration in hello template.</span></span>
<span data-ttu-id="ee957-107">Hier wordt Hallo-indeling voor het opgeven van de configuratie van Hallo-uitbreiding.</span><span class="sxs-lookup"><span data-stu-id="ee957-107">Here is hello format for specifying hello extension configuration.</span></span>

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

<span data-ttu-id="ee957-108">Zoals u in de bovenstaande Hallo zien kunt, bevat Hallo extensie sjabloon twee hoofdonderdelen:</span><span class="sxs-lookup"><span data-stu-id="ee957-108">As you can see from hello above, hello extension template contains two main parts:</span></span>

1. <span data-ttu-id="ee957-109">Naam, uitgever en versie</span><span class="sxs-lookup"><span data-stu-id="ee957-109">Extension name, publisher and version</span></span>
2. <span data-ttu-id="ee957-110">Configuratie van de uitbreiding.</span><span class="sxs-lookup"><span data-stu-id="ee957-110">Extension Configuration.</span></span>

## <a name="identifying-hello-publisher-type-and-typehandlerversion-for-any-extension"></a><span data-ttu-id="ee957-111">Hallo-uitgever, type en typeHandlerVersion voor elke extensie identificeren</span><span class="sxs-lookup"><span data-stu-id="ee957-111">Identifying hello publisher, type, and typeHandlerVersion for any extension</span></span>
<span data-ttu-id="ee957-112">Azure VM-extensies zijn gepubliceerd door Microsoft en vertrouwd 3e partij uitgevers en elke uitbreiding wordt uniek geïdentificeerd door de uitgever, type en Hallo typeHandlerVersion.</span><span class="sxs-lookup"><span data-stu-id="ee957-112">Azure VM extensions are published by Microsoft and trusted 3rd party publishers and each extension is uniquely identified by its publisher,type and hello typeHandlerVersion.</span></span> <span data-ttu-id="ee957-113">Deze kunnen worden bepaald als volgt:</span><span class="sxs-lookup"><span data-stu-id="ee957-113">These can be determined as following:</span></span>  

