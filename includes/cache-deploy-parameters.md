
### <a name="cacheskuname"></a>cacheSKUName
Hallo-prijscategorie van de Hallo nieuwe Azure Redis-Cache.

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

Hallo sjabloon definieert Hallo-waarden die zijn toegestaan voor deze parameter (basis of standaard), en wijst een standaardwaarde (basis) als er geen waarde is opgegeven. Basic kunt u één knooppunt met meerdere groottes van too53 GB beschikbaar.
Standaard biedt twee knooppunten primair/Replica met meerdere groottes van too53 GB en 99,9% SLA beschikbaar.

### <a name="cacheskufamily"></a>cacheSKUFamily
Hallo-familie voor Hallo sku.

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


### <a name="cacheskucapacity"></a>cacheSKUCapacity
Hallo-grootte van de nieuwe Azure Redis-Cache-exemplaar Hallo. 

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


Hallo sjabloon definieert Hallo-waarden die zijn toegestaan voor deze parameter (0, 1, 2, 3, 4, 5 of 6), en wijst een standaardwaarde (1) als er geen waarde is opgegeven. Deze getallen komen overeen toofollowing cachegrootte: 0 = 250 MB, 1 = 1 GB, 2 = 2,5 GB, 3 = 6 GB, 4 = 13 GB, 5 = 26 GB, 6 = 53 GB

