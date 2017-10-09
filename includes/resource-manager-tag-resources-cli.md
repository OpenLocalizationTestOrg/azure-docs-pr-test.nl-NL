<span data-ttu-id="cb713-101">gebruik van een resourcegroep tag tooa tooadd **azure-groep set**.</span><span class="sxs-lookup"><span data-stu-id="cb713-101">tooadd a tag tooa resource group, use **azure group set**.</span></span> <span data-ttu-id="cb713-102">Als Hallo resourcegroep geen bestaande labels doorgeven in Hallo-code.</span><span class="sxs-lookup"><span data-stu-id="cb713-102">If hello resource group does not have any existing tags, pass in hello tag.</span></span>

```azurecli
azure group set -n tag-demo-group -t Dept=Finance
```

<span data-ttu-id="cb713-103">Labels worden bijgewerkt als geheel.</span><span class="sxs-lookup"><span data-stu-id="cb713-103">Tags are updated as a whole.</span></span> <span data-ttu-id="cb713-104">Als u een tag tooa resourcegroep met de bestaande codes tooadd wilt, slagen voor alle Hallo-tags.</span><span class="sxs-lookup"><span data-stu-id="cb713-104">If you want tooadd a tag tooa resource group that has existing tags, pass all hello tags.</span></span> 

```azurecli
azure group set -n tag-demo-group -t Dept=Finance;Environment=Production;Project=Upgrade
```

<span data-ttu-id="cb713-105">Labels wordt niet overgenomen door de resources in een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="cb713-105">Tags are not inherited by resources in a resource group.</span></span> <span data-ttu-id="cb713-106">een bron van de tooa tag tooadd gebruiken **azure-ResourceSet**.</span><span class="sxs-lookup"><span data-stu-id="cb713-106">tooadd a tag tooa resource, use **azure resource set**.</span></span> <span data-ttu-id="cb713-107">Hallo versienummer van de API voor Hallo brontype dat u Hallo tag om te toevoegt slagen.</span><span class="sxs-lookup"><span data-stu-id="cb713-107">Pass hello API version number for hello resource type that you are adding hello tag to.</span></span> <span data-ttu-id="cb713-108">Als u tooretrieve Hallo API-versie moet, gebruikt u Hallo volgende opdracht met Hallo resourceprovider voor het type Hallo die u instelt:</span><span class="sxs-lookup"><span data-stu-id="cb713-108">If you need tooretrieve hello API version, use hello following command with hello resource provider for hello type you are setting:</span></span>

```azurecli
azure provider show -n Microsoft.Storage --json
```

<span data-ttu-id="cb713-109">Zoek in Hallo-resultaten voor Hallo resource dat die u wilt.</span><span class="sxs-lookup"><span data-stu-id="cb713-109">In hello results, look for hello resource type you want.</span></span>

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

<span data-ttu-id="cb713-110">Nu bieden die API-versie, de naam van resourcegroep, Resourcenaam, resourcetype en tagwaarde als parameters.</span><span class="sxs-lookup"><span data-stu-id="cb713-110">Now, provide that API version, resource group name, resource name, resource type, and tag value as parameters.</span></span>

```azurecli
azure resource set -g tag-demo-group -n storagetagdemo -r Microsoft.Storage/storageAccounts -t Dept=Finance -o 2016-01-01
```

<span data-ttu-id="cb713-111">Labels aanwezig rechtstreeks op de resources en resourcegroepen.</span><span class="sxs-lookup"><span data-stu-id="cb713-111">Tags exist directly on resources and resource groups.</span></span> <span data-ttu-id="cb713-112">toosee hello bestaande tags kunnen ophalen van een resourcegroep en de bijbehorende bronnen met **azure-groep weergeven**.</span><span class="sxs-lookup"><span data-stu-id="cb713-112">toosee hello existing tags, get a resource group and its resources with **azure group show**.</span></span>

```azurecli
azure group show -n tag-demo-group --json
```

<span data-ttu-id="cb713-113">Die resulteert metagegevens over Hallo-resourcegroep, met inbegrip van eventuele tooit labels worden toegepast.</span><span class="sxs-lookup"><span data-stu-id="cb713-113">Which returns metadata about hello resource group, including any tags applied tooit.</span></span>

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

<span data-ttu-id="cb713-114">U Hallo labels voor een bepaalde bron weergeven met behulp van **azure-resource weergeven**.</span><span class="sxs-lookup"><span data-stu-id="cb713-114">You view hello tags for a particular resource by using **azure resource show**.</span></span>

```azurecli
azure resource show -g tag-demo-group -n storagetagdemo -r Microsoft.Storage/storageAccounts -o 2016-01-01 --json
```

<span data-ttu-id="cb713-115">tooretrieve alle Hallo resources met een tagwaarde gebruiken:</span><span class="sxs-lookup"><span data-stu-id="cb713-115">tooretrieve all hello resources with a tag value, use:</span></span>

```azurecli
azure resource list -t Dept=Finance --json
```

<span data-ttu-id="cb713-116">tooretrieve alle Hallo bronnengroepen met een tagwaarde gebruiken:</span><span class="sxs-lookup"><span data-stu-id="cb713-116">tooretrieve all hello resource groups with a tag value, use:</span></span>

```azurecli
azure group list -t Dept=Finance
```

<span data-ttu-id="cb713-117">U kunt bestaande Hallo-codes in uw abonnement bekijken met de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="cb713-117">You can view hello existing tags in your subscription with hello following command:</span></span>

```azurecli
azure tag list
```
