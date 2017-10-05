U kunt een label toevoegen aan een resourcegroep met **azure-groep set**. Als de resourcegroep geen bestaande labels in de tag doorgeven.

```azurecli
azure group set -n tag-demo-group -t Dept=Finance
```

Labels worden bijgewerkt als geheel. Als u een label toevoegen aan een resourcegroep met bestaande labels, geeft u alle codes. 

```azurecli
azure group set -n tag-demo-group -t Dept=Finance;Environment=Production;Project=Upgrade
```

Labels wordt niet overgenomen door de resources in een resourcegroep. U kunt een label toevoegen aan een resource met **azure-ResourceSet**. Geeft het nummer van de API-versie voor het brontype dat u het label wilt toevoegen. Als u nodig hebt voor het ophalen van de API-versie, gebruikt u de volgende opdracht met de resourceprovider voor het type dat u wilt instellen:

```azurecli
azure provider show -n Microsoft.Storage --json
```

Zoek in de resultaten voor het brontype dat u wilt.

```azurecli
"resourceTypes": [
{
  "resourceType": "storageAccounts",
  ...
  "apiVersions": [
    "2016-01-01",
    "2015-06-15",
    "2015-05-01-preview"
  ]
}
...
```

Nu bieden die API-versie, de naam van resourcegroep, Resourcenaam, resourcetype en tagwaarde als parameters.

```azurecli
azure resource set -g tag-demo-group -n storagetagdemo -r Microsoft.Storage/storageAccounts -t Dept=Finance -o 2016-01-01
```

Labels aanwezig rechtstreeks op de resources en resourcegroepen. Overzicht van de bestaande codes ophalen van een resourcegroep en de bijbehorende bronnen met **azure-groep weergeven**.

```azurecli
azure group show -n tag-demo-group --json
```

Die resulteert metagegevens over de resourcegroep, inclusief eventuele afsluitcodes toegepast.

```azurecli
{
  "id": "/subscriptions/4705409c-9372-42f0-914c-64a504530837/resourceGroups/tag-demo-group",
  "name": "tag-demo-group",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "location": "southcentralus",
  "tags": {
    "Dept": "Finance",
    "Environment": "Production",
    "Project": "Upgrade"
  },
  ...
}
```

U de labels voor een bepaalde bron weergeven met behulp van **azure-resource weergeven**.

```azurecli
azure resource show -g tag-demo-group -n storagetagdemo -r Microsoft.Storage/storageAccounts -o 2016-01-01 --json
```

Voor het ophalen van alle resources met een tagwaarde gebruiken:

```azurecli
azure resource list -t Dept=Finance --json
```

Voor het ophalen van alle brongroepen met een tagwaarde gebruiken:

```azurecli
azure group list -t Dept=Finance
```

U kunt de bestaande labels weergeven in uw abonnement met de volgende opdracht:

```azurecli
azure tag list
```
