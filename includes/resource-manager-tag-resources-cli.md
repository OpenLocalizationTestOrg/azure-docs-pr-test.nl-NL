<span data-ttu-id="5f6d9-101">U kunt een label toevoegen aan een resourcegroep met **azure-groep set**.</span><span class="sxs-lookup"><span data-stu-id="5f6d9-101">To add a tag to a resource group, use **azure group set**.</span></span> <span data-ttu-id="5f6d9-102">Als de resourcegroep geen bestaande labels in de tag doorgeven.</span><span class="sxs-lookup"><span data-stu-id="5f6d9-102">If the resource group does not have any existing tags, pass in the tag.</span></span>

```azurecli
azure group set -n tag-demo-group -t Dept=Finance
```

<span data-ttu-id="5f6d9-103">Labels worden bijgewerkt als geheel.</span><span class="sxs-lookup"><span data-stu-id="5f6d9-103">Tags are updated as a whole.</span></span> <span data-ttu-id="5f6d9-104">Als u een label toevoegen aan een resourcegroep met bestaande labels, geeft u alle codes.</span><span class="sxs-lookup"><span data-stu-id="5f6d9-104">If you want to add a tag to a resource group that has existing tags, pass all the tags.</span></span> 

```azurecli
azure group set -n tag-demo-group -t Dept=Finance;Environment=Production;Project=Upgrade
```

<span data-ttu-id="5f6d9-105">Labels wordt niet overgenomen door de resources in een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="5f6d9-105">Tags are not inherited by resources in a resource group.</span></span> <span data-ttu-id="5f6d9-106">U kunt een label toevoegen aan een resource met **azure-ResourceSet**.</span><span class="sxs-lookup"><span data-stu-id="5f6d9-106">To add a tag to a resource, use **azure resource set**.</span></span> <span data-ttu-id="5f6d9-107">Geeft het nummer van de API-versie voor het brontype dat u het label wilt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="5f6d9-107">Pass the API version number for the resource type that you are adding the tag to.</span></span> <span data-ttu-id="5f6d9-108">Als u nodig hebt voor het ophalen van de API-versie, gebruikt u de volgende opdracht met de resourceprovider voor het type dat u wilt instellen:</span><span class="sxs-lookup"><span data-stu-id="5f6d9-108">If you need to retrieve the API version, use the following command with the resource provider for the type you are setting:</span></span>

```azurecli
azure provider show -n Microsoft.Storage --json
```

<span data-ttu-id="5f6d9-109">Zoek in de resultaten voor het brontype dat u wilt.</span><span class="sxs-lookup"><span data-stu-id="5f6d9-109">In the results, look for the resource type you want.</span></span>

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

<span data-ttu-id="5f6d9-110">Nu bieden die API-versie, de naam van resourcegroep, Resourcenaam, resourcetype en tagwaarde als parameters.</span><span class="sxs-lookup"><span data-stu-id="5f6d9-110">Now, provide that API version, resource group name, resource name, resource type, and tag value as parameters.</span></span>

```azurecli
azure resource set -g tag-demo-group -n storagetagdemo -r Microsoft.Storage/storageAccounts -t Dept=Finance -o 2016-01-01
```

<span data-ttu-id="5f6d9-111">Labels aanwezig rechtstreeks op de resources en resourcegroepen.</span><span class="sxs-lookup"><span data-stu-id="5f6d9-111">Tags exist directly on resources and resource groups.</span></span> <span data-ttu-id="5f6d9-112">Overzicht van de bestaande codes ophalen van een resourcegroep en de bijbehorende bronnen met **azure-groep weergeven**.</span><span class="sxs-lookup"><span data-stu-id="5f6d9-112">To see the existing tags, get a resource group and its resources with **azure group show**.</span></span>

```azurecli
azure group show -n tag-demo-group --json
```

<span data-ttu-id="5f6d9-113">Die resulteert metagegevens over de resourcegroep, inclusief eventuele afsluitcodes toegepast.</span><span class="sxs-lookup"><span data-stu-id="5f6d9-113">Which returns metadata about the resource group, including any tags applied to it.</span></span>

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

<span data-ttu-id="5f6d9-114">U de labels voor een bepaalde bron weergeven met behulp van **azure-resource weergeven**.</span><span class="sxs-lookup"><span data-stu-id="5f6d9-114">You view the tags for a particular resource by using **azure resource show**.</span></span>

```azurecli
azure resource show -g tag-demo-group -n storagetagdemo -r Microsoft.Storage/storageAccounts -o 2016-01-01 --json
```

<span data-ttu-id="5f6d9-115">Voor het ophalen van alle resources met een tagwaarde gebruiken:</span><span class="sxs-lookup"><span data-stu-id="5f6d9-115">To retrieve all the resources with a tag value, use:</span></span>

```azurecli
azure resource list -t Dept=Finance --json
```

<span data-ttu-id="5f6d9-116">Voor het ophalen van alle brongroepen met een tagwaarde gebruiken:</span><span class="sxs-lookup"><span data-stu-id="5f6d9-116">To retrieve all the resource groups with a tag value, use:</span></span>

```azurecli
azure group list -t Dept=Finance
```

<span data-ttu-id="5f6d9-117">U kunt de bestaande labels weergeven in uw abonnement met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="5f6d9-117">You can view the existing tags in your subscription with the following command:</span></span>

```azurecli
azure tag list
```
