gebruik van een resourcegroep tag tooa tooadd **azure-groep set**. Als Hallo resourcegroep geen bestaande labels doorgeven in Hallo-code.

```azurecli
azure group set -n tag-demo-group -t Dept=Finance
```

Labels worden bijgewerkt als geheel. Als u een tag tooa resourcegroep met de bestaande codes tooadd wilt, slagen voor alle Hallo-tags. 

```azurecli
azure group set -n tag-demo-group -t Dept=Finance;Environment=Production;Project=Upgrade
```

Labels wordt niet overgenomen door de resources in een resourcegroep. een bron van de tooa tag tooadd gebruiken **azure-ResourceSet**. Hallo versienummer van de API voor Hallo brontype dat u Hallo tag om te toevoegt slagen. Als u tooretrieve Hallo API-versie moet, gebruikt u Hallo volgende opdracht met Hallo resourceprovider voor het type Hallo die u instelt:

```azurecli
azure provider show -n Microsoft.Storage --json
```

Zoek in Hallo-resultaten voor Hallo resource dat die u wilt.

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

Labels aanwezig rechtstreeks op de resources en resourcegroepen. toosee hello bestaande tags kunnen ophalen van een resourcegroep en de bijbehorende bronnen met **azure-groep weergeven**.

```azurecli
azure group show -n tag-demo-group --json
```

Die resulteert metagegevens over Hallo-resourcegroep, met inbegrip van eventuele tooit labels worden toegepast.

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

U Hallo labels voor een bepaalde bron weergeven met behulp van **azure-resource weergeven**.

```azurecli
azure resource show -g tag-demo-group -n storagetagdemo -r Microsoft.Storage/storageAccounts -o 2016-01-01 --json
```

tooretrieve alle Hallo resources met een tagwaarde gebruiken:

```azurecli
azure resource list -t Dept=Finance --json
```

tooretrieve alle Hallo bronnengroepen met een tagwaarde gebruiken:

```azurecli
azure group list -t Dept=Finance
```

U kunt bestaande Hallo-codes in uw abonnement bekijken met de volgende opdracht Hallo:

```azurecli
azure tag list
```
