<span data-ttu-id="3ada2-101">tootag een bron tijdens de implementatie toevoegen Hallo `tags` element toohello resource die u implementeert.</span><span class="sxs-lookup"><span data-stu-id="3ada2-101">tootag a resource during deployment, add hello `tags` element toohello resource you are deploying.</span></span> <span data-ttu-id="3ada2-102">Hallo tagnaam en waarde opgeven.</span><span class="sxs-lookup"><span data-stu-id="3ada2-102">Provide hello tag name and value.</span></span>

### <a name="apply-a-literal-value-toohello-tag-name"></a><span data-ttu-id="3ada2-103">De naam van een letterlijke waarde toohello tag toepassen</span><span class="sxs-lookup"><span data-stu-id="3ada2-103">Apply a literal value toohello tag name</span></span>
<span data-ttu-id="3ada2-104">Hallo volgende voorbeeld ziet u een opslagaccount met twee tags (`Dept` en `Environment`) tooliteral waarden zijn ingesteld:</span><span class="sxs-lookup"><span data-stu-id="3ada2-104">hello following example shows a storage account with two tags (`Dept` and `Environment`) that are set tooliteral values:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat('storage', uniqueString(resourceGroup().id))]",
      "location": "[resourceGroup().location]",
      "tags": {
        "Dept": "Finance",
        "Environment": "Production"
      },
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": { }
    }
    ]
}
```

### <a name="apply-an-object-toohello-tag-element"></a><span data-ttu-id="3ada2-105">Toepassen van een object toohello tag-element</span><span class="sxs-lookup"><span data-stu-id="3ada2-105">Apply an object toohello tag element</span></span>
<span data-ttu-id="3ada2-106">U kunt definiëren van een objectparameter die verschillende labels opslaat en toepassen van dat object toohello tag-element.</span><span class="sxs-lookup"><span data-stu-id="3ada2-106">You can define an object parameter that stores several tags, and apply that object toohello tag element.</span></span> <span data-ttu-id="3ada2-107">Elke eigenschap in het Hallo-object wordt een afzonderlijke code voor Hallo resource.</span><span class="sxs-lookup"><span data-stu-id="3ada2-107">Each property in hello object becomes a separate tag for hello resource.</span></span> <span data-ttu-id="3ada2-108">Hallo volgende voorbeeld heeft een parameter met de naam `tagValues` toegepaste toohello tag-element is.</span><span class="sxs-lookup"><span data-stu-id="3ada2-108">hello following example has a parameter named `tagValues` that is applied toohello tag element.</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "tagValues": {
      "type": "object",
      "defaultValue": {
        "Dept": "Finance",
        "Environment": "Production"
      }
    }
  },
  "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat('storage', uniqueString(resourceGroup().id))]",
      "location": "[resourceGroup().location]",
      "tags": "[parameters('tagValues')]",
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": {}
    }
  ]
}
```

### <a name="apply-a-json-string-toohello-tag-name"></a><span data-ttu-id="3ada2-109">De naam van een JSON-tekenreeks toohello tag toepassen</span><span class="sxs-lookup"><span data-stu-id="3ada2-109">Apply a JSON string toohello tag name</span></span>

<span data-ttu-id="3ada2-110">toostore veel waarden in een enkel label toepassing een JSON-tekenreeks die Hallo waarden vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="3ada2-110">toostore many values in a single tag, apply a JSON string that represents hello values.</span></span> <span data-ttu-id="3ada2-111">Hallo gehele JSON-tekenreeks wordt opgeslagen als een tag kan niet meer dan 256 tekens.</span><span class="sxs-lookup"><span data-stu-id="3ada2-111">hello entire JSON string is stored as one tag that cannot exceed 256 characters.</span></span> <span data-ttu-id="3ada2-112">Hallo volgende voorbeeld is een enkel label met de naam `CostCenter` die verschillende waarden van een JSON-tekenreeks bevat:</span><span class="sxs-lookup"><span data-stu-id="3ada2-112">hello following example has a single tag named `CostCenter` that contains several values from a JSON string:</span></span>  

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat('storage', uniqueString(resourceGroup().id))]",
      "location": "[resourceGroup().location]",
      "tags": {
        "CostCenter": "{\"Dept\":\"Finance\",\"Environment\":\"Production\"}"
      },
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": { }
    }
    ]
}
```