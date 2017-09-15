
### <a name="cacheskuname"></a><span data-ttu-id="5c230-101">cacheSKUName</span><span class="sxs-lookup"><span data-stu-id="5c230-101">cacheSKUName</span></span>
<span data-ttu-id="5c230-102">De prijscategorie van de nieuwe Azure Redis-Cache.</span><span class="sxs-lookup"><span data-stu-id="5c230-102">The pricing tier of the new Azure Redis Cache.</span></span>

    "cacheSKUName": {
      "type": "string",
      "allowedValues": [
        "Basic",
        "Standard"
      ],
      "defaultValue": "Basic",
      "metadata": {
        "description": "The pricing tier of the new Azure Redis Cache."
      }
    },

<span data-ttu-id="5c230-103">De sjabloon definieert de waarden die zijn toegestaan voor deze parameter (basis of standaard) en een standaardwaarde (basis) wordt toegewezen als er geen waarde is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="5c230-103">The template defines the values that are permitted for this parameter (Basic or Standard), and assigns a default value (Basic) if no value is specified.</span></span> <span data-ttu-id="5c230-104">Basic biedt één knooppunt met meerdere groottes beschikbaar up tot 53 GB.</span><span class="sxs-lookup"><span data-stu-id="5c230-104">Basic provides a single node with multiple sizes available up to 53 GB.</span></span>
<span data-ttu-id="5c230-105">Standaard biedt twee knooppunten primair/Replica met meerdere groottes beschikbaar om aan de SLA 53 GB en 99,9%.</span><span class="sxs-lookup"><span data-stu-id="5c230-105">Standard provides two-node Primary/Replica with multiple sizes available up to 53 GB and 99.9% SLA.</span></span>

### <a name="cacheskufamily"></a><span data-ttu-id="5c230-106">cacheSKUFamily</span><span class="sxs-lookup"><span data-stu-id="5c230-106">cacheSKUFamily</span></span>
<span data-ttu-id="5c230-107">De familie voor de sku.</span><span class="sxs-lookup"><span data-stu-id="5c230-107">The family for the sku.</span></span>

    "cacheSKUFamily": {
      "type": "string",
      "allowedValues": [
        "C"
      ],
      "defaultValue": "C",
      "metadata": {
        "description": "The family for the sku."
      }
    },


### <a name="cacheskucapacity"></a><span data-ttu-id="5c230-108">cacheSKUCapacity</span><span class="sxs-lookup"><span data-stu-id="5c230-108">cacheSKUCapacity</span></span>
<span data-ttu-id="5c230-109">De grootte van het nieuwe exemplaar van Azure Redis-Cache.</span><span class="sxs-lookup"><span data-stu-id="5c230-109">The size of the new Azure Redis Cache instance.</span></span> 

    "cacheSKUCapacity": {
      "type": "int",
      "allowedValues": [
        0,
        1,
        2,
        3,
        4,
        5,
        6
      ],
      "defaultValue": 0,
      "metadata": {
        "description": "The size of the new Azure Redis Cache instance. "
      }
    }


<span data-ttu-id="5c230-110">De sjabloon definieert de waarden die zijn toegestaan voor deze parameter (0, 1, 2, 3, 4, 5 of 6), en wijst een standaardwaarde (1) als er geen waarde is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="5c230-110">The template defines the values that are permitted for this parameter (0, 1, 2, 3, 4, 5 or 6), and assigns a default value (1) if no value is specified.</span></span> <span data-ttu-id="5c230-111">Deze getallen die overeenkomen met de volgende cachegrootte: 0 = 250 MB, 1 = 1 GB, 2 = 2,5 GB, 3 = 6 GB, 4 = 13 GB, 5 = 26 GB, 6 = 53 GB</span><span class="sxs-lookup"><span data-stu-id="5c230-111">Those numbers correspond to following cache sizes: 0 = 250 MB, 1 = 1 GB, 2 = 2.5 GB, 3 = 6 GB, 4 = 13 GB, 5 = 26 GB, 6 = 53 GB</span></span>

