tootag een bron tijdens de implementatie toevoegen Hallo `tags` element toohello resource die u implementeert. Hallo tagnaam en waarde opgeven.

### <a name="apply-a-literal-value-toohello-tag-name"></a>De naam van een letterlijke waarde toohello tag toepassen
Hallo volgende voorbeeld ziet u een opslagaccount met twee tags (`Dept` en `Environment`) tooliteral waarden zijn ingesteld:

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

### <a name="apply-an-object-toohello-tag-element"></a>Toepassen van een object toohello tag-element
U kunt definiëren van een objectparameter die verschillende labels opslaat en toepassen van dat object toohello tag-element. Elke eigenschap in het Hallo-object wordt een afzonderlijke code voor Hallo resource. Hallo volgende voorbeeld heeft een parameter met de naam `tagValues` toegepaste toohello tag-element is.

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

### <a name="apply-a-json-string-toohello-tag-name"></a>De naam van een JSON-tekenreeks toohello tag toepassen

toostore veel waarden in een enkel label toepassing een JSON-tekenreeks die Hallo waarden vertegenwoordigt. Hallo gehele JSON-tekenreeks wordt opgeslagen als een tag kan niet meer dan 256 tekens. Hallo volgende voorbeeld is een enkel label met de naam `CostCenter` die verschillende waarden van een JSON-tekenreeks bevat:  

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