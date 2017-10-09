
### <a name="cacheskuname"></a><span data-ttu-id="12a07-101">cacheSKUName</span><span class="sxs-lookup"><span data-stu-id="12a07-101">cacheSKUName</span></span>
<span data-ttu-id="12a07-102">Hallo-prijscategorie van de Hallo nieuwe Azure Redis-Cache.</span><span class="sxs-lookup"><span data-stu-id="12a07-102">hello pricing tier of hello new Azure Redis Cache.</span></span>

    "cacheSKUName": {
      "type": "string",
      "allowedValues": [
        "Basic",
        "Standard"
      ],
      "defaultValue": "Basic",
      "metadata": {
        "description": "hello pricing tier of hello new Azure Redis Cache."
      }
    },

<span data-ttu-id="12a07-103">Hallo sjabloon definieert Hallo-waarden die zijn toegestaan voor deze parameter (basis of standaard), en wijst een standaardwaarde (basis) als er geen waarde is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="12a07-103">hello template defines hello values that are permitted for this parameter (Basic or Standard), and assigns a default value (Basic) if no value is specified.</span></span> <span data-ttu-id="12a07-104">Basic kunt u één knooppunt met meerdere groottes van too53 GB beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="12a07-104">Basic provides a single node with multiple sizes available up too53 GB.</span></span>
<span data-ttu-id="12a07-105">Standaard biedt twee knooppunten primair/Replica met meerdere groottes van too53 GB en 99,9% SLA beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="12a07-105">Standard provides two-node Primary/Replica with multiple sizes available up too53 GB and 99.9% SLA.</span></span>

### <a name="cacheskufamily"></a><span data-ttu-id="12a07-106">cacheSKUFamily</span><span class="sxs-lookup"><span data-stu-id="12a07-106">cacheSKUFamily</span></span>
<span data-ttu-id="12a07-107">Hallo-familie voor Hallo sku.</span><span class="sxs-lookup"><span data-stu-id="12a07-107">hello family for hello sku.</span></span>

    "cacheSKUFamily": {
      "type": "string",
      "allowedValues": [
        "C"
      ],
      "defaultValue": "C",
      "metadata": {
        "description": "hello family for hello sku."
      }
    },


### <a name="cacheskucapacity"></a><span data-ttu-id="12a07-108">cacheSKUCapacity</span><span class="sxs-lookup"><span data-stu-id="12a07-108">cacheSKUCapacity</span></span>
<span data-ttu-id="12a07-109">Hallo-grootte van de nieuwe Azure Redis-Cache-exemplaar Hallo.</span><span class="sxs-lookup"><span data-stu-id="12a07-109">hello size of hello new Azure Redis Cache instance.</span></span> 

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
        "description": "hello size of hello new Azure Redis Cache instance. "
      }
    }


<span data-ttu-id="12a07-110">Hallo sjabloon definieert Hallo-waarden die zijn toegestaan voor deze parameter (0, 1, 2, 3, 4, 5 of 6), en wijst een standaardwaarde (1) als er geen waarde is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="12a07-110">hello template defines hello values that are permitted for this parameter (0, 1, 2, 3, 4, 5 or 6), and assigns a default value (1) if no value is specified.</span></span> <span data-ttu-id="12a07-111">Deze getallen komen overeen toofollowing cachegrootte: 0 = 250 MB, 1 = 1 GB, 2 = 2,5 GB, 3 = 6 GB, 4 = 13 GB, 5 = 26 GB, 6 = 53 GB</span><span class="sxs-lookup"><span data-stu-id="12a07-111">Those numbers correspond toofollowing cache sizes: 0 = 250 MB, 1 = 1 GB, 2 = 2.5 GB, 3 = 6 GB, 4 = 13 GB, 5 = 26 GB, 6 = 53 GB</span></span>

