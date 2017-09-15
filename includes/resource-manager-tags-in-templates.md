<span data-ttu-id="9aea2-101">Als u een resource wilt taggen tijdens de implementatie, voegt u het element `tags` toe aan de resource die u wilt implementeren.</span><span class="sxs-lookup"><span data-stu-id="9aea2-101">To tag a resource during deployment, add the `tags` element to the resource you are deploying.</span></span> <span data-ttu-id="9aea2-102">Geef de naam en waarde van de tag op.</span><span class="sxs-lookup"><span data-stu-id="9aea2-102">Provide the tag name and value.</span></span>

### <a name="apply-a-literal-value-to-the-tag-name"></a><span data-ttu-id="9aea2-103">Een letterlijke waarde toepassen op de tagnaam</span><span class="sxs-lookup"><span data-stu-id="9aea2-103">Apply a literal value to the tag name</span></span>
<span data-ttu-id="9aea2-104">In het volgende voorbeeld wordt een opslagaccount weergegeven met twee tags (`Dept` en `Environment`) die zijn ingesteld op letterlijke waarden:</span><span class="sxs-lookup"><span data-stu-id="9aea2-104">The following example shows a storage account with two tags (`Dept` and `Environment`) that are set to literal values:</span></span>

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

### <a name="apply-an-object-to-the-tag-element"></a><span data-ttu-id="9aea2-105">Een object toepassen op het tagelement</span><span class="sxs-lookup"><span data-stu-id="9aea2-105">Apply an object to the tag element</span></span>
<span data-ttu-id="9aea2-106">U kunt een objectparameter definiëren waarmee verschillende tags worden opgeslagen en dit object vervolgens toepassen op het tagelement.</span><span class="sxs-lookup"><span data-stu-id="9aea2-106">You can define an object parameter that stores several tags, and apply that object to the tag element.</span></span> <span data-ttu-id="9aea2-107">Elke eigenschap in het object wordt een afzonderlijke tag voor de resource.</span><span class="sxs-lookup"><span data-stu-id="9aea2-107">Each property in the object becomes a separate tag for the resource.</span></span> <span data-ttu-id="9aea2-108">Het volgende voorbeeld heeft een parameter met de naam `tagValues` die wordt toegepast op het tagelement.</span><span class="sxs-lookup"><span data-stu-id="9aea2-108">The following example has a parameter named `tagValues` that is applied to the tag element.</span></span>

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

### <a name="apply-a-json-string-to-the-tag-name"></a><span data-ttu-id="9aea2-109">Een JSON-tekenreeks toepassen op de tagnaam</span><span class="sxs-lookup"><span data-stu-id="9aea2-109">Apply a JSON string to the tag name</span></span>

<span data-ttu-id="9aea2-110">Als u veel waarden wilt opslaan in een enkele tag, past u een JSON-tekenreeks toe die de waarden vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="9aea2-110">To store many values in a single tag, apply a JSON string that represents the values.</span></span> <span data-ttu-id="9aea2-111">De volledige JSON-tekenreeks wordt opgeslagen als een tag met maximaal 256 tekens.</span><span class="sxs-lookup"><span data-stu-id="9aea2-111">The entire JSON string is stored as one tag that cannot exceed 256 characters.</span></span> <span data-ttu-id="9aea2-112">Het volgende voorbeeld heeft een enkele tag met de naam `CostCenter` die verschillende waarden uit een JSON-tekenreeks bevat:</span><span class="sxs-lookup"><span data-stu-id="9aea2-112">The following example has a single tag named `CostCenter` that contains several values from a JSON string:</span></span>  

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