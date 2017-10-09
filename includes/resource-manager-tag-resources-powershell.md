<span data-ttu-id="99eb4-101">Versie 3.0 van Hallo AzureRm.Resources module opgenomen belangrijke wijzigingen in hoe u met labels werkt.</span><span class="sxs-lookup"><span data-stu-id="99eb4-101">Version 3.0 of hello AzureRm.Resources module included significant changes in how you work with tags.</span></span> <span data-ttu-id="99eb4-102">Controleer uw versie voordat u doorgaat:</span><span class="sxs-lookup"><span data-stu-id="99eb4-102">Before you proceed, check your version:</span></span>

```powershell
Get-Module -ListAvailable -Name AzureRm.Resources | Select Version
```

<span data-ttu-id="99eb4-103">Als uw resultaten versie 3.0 of hoger, Hallo voorbeelden in dit onderwerp werken met uw omgeving weergeven.</span><span class="sxs-lookup"><span data-stu-id="99eb4-103">If your results show version 3.0 or later, hello examples in this topic work with your environment.</span></span> <span data-ttu-id="99eb4-104">Als u niet over versie 3.0 of hoger beschikt, [werkt u uw versie bij](/powershell/azureps-cmdlets-docs/) met behulp van PowerShell Gallery of Web Platform Installer voordat u verdergaat met dit onderwerp.</span><span class="sxs-lookup"><span data-stu-id="99eb4-104">If you do not have version 3.0 or later, [update your version](/powershell/azureps-cmdlets-docs/) by using PowerShell Gallery or Web Platform Installer before you proceed with this topic.</span></span>

```powershell
Version
-------
3.5.0
```

<span data-ttu-id="99eb4-105">toosee Hallo bestaande codes voor een *resourcegroep*, gebruiken:</span><span class="sxs-lookup"><span data-stu-id="99eb4-105">toosee hello existing tags for a *resource group*, use:</span></span>

```powershell
(Get-AzureRmResourceGroup -Name examplegroup).Tags
```

<span data-ttu-id="99eb4-106">Script retourneert Hallo volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="99eb4-106">That script returns hello following format:</span></span>

```powershell
Name                           Value
----                           -----
Dept                           IT
Environment                    Test
```

<span data-ttu-id="99eb4-107">toosee Hallo bestaande codes voor een *resource met een opgegeven bron-ID*, gebruiken:</span><span class="sxs-lookup"><span data-stu-id="99eb4-107">toosee hello existing tags for a *resource that has a specified resource ID*, use:</span></span>

```powershell
(Get-AzureRmResource -ResourceId {resource-id}).Tags
```

<span data-ttu-id="99eb4-108">Of toosee Hallo bestaande codes voor een *resource met een opgegeven groep en de bron*, gebruiken:</span><span class="sxs-lookup"><span data-stu-id="99eb4-108">Or, toosee hello existing tags for a *resource that has a specified name and resource group*, use:</span></span>

```powershell
(Get-AzureRmResource -ResourceName examplevnet -ResourceGroupName examplegroup).Tags
```

<span data-ttu-id="99eb4-109">tooget *resourcegroepen die beschikken over een specifieke tag*, gebruiken:</span><span class="sxs-lookup"><span data-stu-id="99eb4-109">tooget *resource groups that have a specific tag*, use:</span></span>

```powershell
(Find-AzureRmResourceGroup -Tag @{ Dept="Finance" }).Name 
```

<span data-ttu-id="99eb4-110">tooget *resources met een specifieke tag*, gebruiken:</span><span class="sxs-lookup"><span data-stu-id="99eb4-110">tooget *resources that have a specific tag*, use:</span></span>

```powershell
(Find-AzureRmResource -TagName Dept -TagValue Finance).Name
```

<span data-ttu-id="99eb4-111">Telkens wanneer u labels tooa resource of een resourcegroep hebt toegepast, kunt u bestaande labels op die resource of resourcegroep Hallo overschrijven.</span><span class="sxs-lookup"><span data-stu-id="99eb4-111">Every time you apply tags tooa resource or a resource group, you overwrite hello existing tags on that resource or resource group.</span></span> <span data-ttu-id="99eb4-112">Daarom moet u een andere benadering, op basis van of Hallo resource of resourcegroep bestaande labels heeft.</span><span class="sxs-lookup"><span data-stu-id="99eb4-112">Therefore, you must use a different approach based on whether hello resource or resource group has existing tags.</span></span> 

<span data-ttu-id="99eb4-113">tooadd tags tooa *resourcegroep zonder bestaande tags*, gebruiken:</span><span class="sxs-lookup"><span data-stu-id="99eb4-113">tooadd tags tooa *resource group without existing tags*, use:</span></span>

```powershell
Set-AzureRmResourceGroup -Name examplegroup -Tag @{ Dept="IT"; Environment="Test" }
```

<span data-ttu-id="99eb4-114">tooadd tags tooa *bronnengroep met bestaande codes*, Hallo bestaande codes ophalen, Hallo nieuw label toevoegen en Hallo tags toepassen:</span><span class="sxs-lookup"><span data-stu-id="99eb4-114">tooadd tags tooa *resource group that has existing tags*, retrieve hello existing tags, add hello new tag, and reapply hello tags:</span></span>

```powershell
$tags = (Get-AzureRmResourceGroup -Name examplegroup).Tags
$tags += @{Status="Approved"}
Set-AzureRmResourceGroup -Tag $tags -Name examplegroup
```

<span data-ttu-id="99eb4-115">tooadd tags tooa *resource zonder bestaande tags*, gebruiken:</span><span class="sxs-lookup"><span data-stu-id="99eb4-115">tooadd tags tooa *resource without existing tags*, use:</span></span>

```powershell
Set-AzureRmResource -Tag @{ Dept="IT"; Environment="Test" } -ResourceName examplevnet -ResourceGroupName examplegroup
```

<span data-ttu-id="99eb4-116">tooadd tags tooa *resource met bestaande codes*, gebruiken:</span><span class="sxs-lookup"><span data-stu-id="99eb4-116">tooadd tags tooa *resource that has existing tags*, use:</span></span>

```powershell
$tags = (Get-AzureRmResource -ResourceName examplevnet -ResourceGroupName examplegroup).Tags
$tags += @{Status="Approved"}
Set-AzureRmResource -Tag $tags -ResourceName examplevnet -ResourceGroupName examplegroup
```

<span data-ttu-id="99eb4-117">tooapply die alle labels van een resource tooits groepsbronnen en *bestaande labels op Hallo resources niet bewaren*, Hallo script volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="99eb4-117">tooapply all tags from a resource group tooits resources, and *not retain existing tags on hello resources*, use hello following script:</span></span>

```powershell
$groups = Get-AzureRmResourceGroup
foreach ($g in $groups) 
{
    Find-AzureRmResource -ResourceGroupNameEquals $g.ResourceGroupName | ForEach-Object {Set-AzureRmResource -ResourceId $_.ResourceId -Tag $g.Tags -Force } 
}
```

<span data-ttu-id="99eb4-118">tooapply die alle labels van een resource tooits groepsbronnen en *bestaande tags voor resources die geen dubbele waarden behouden*, Hallo script volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="99eb4-118">tooapply all tags from a resource group tooits resources, and *retain existing tags on resources that are not duplicates*, use hello following script:</span></span>

```powershell
$groups = Get-AzureRmResourceGroup
foreach ($g in $groups) 
{
    if ($g.Tags -ne $null) {
        $resources = Find-AzureRmResource -ResourceGroupNameEquals $g.ResourceGroupName 
        foreach ($r in $resources)
        {
            $resourcetags = (Get-AzureRmResource -ResourceId $r.ResourceId).Tags
            foreach ($key in $g.Tags.Keys)
            {
                if ($resourcetags.ContainsKey($key)) { $resourcetags.Remove($key) }
            }
            $resourcetags += $g.Tags
            Set-AzureRmResource -Tag $resourcetags -ResourceId $r.ResourceId -Force
        }
    }
}
```

<span data-ttu-id="99eb4-119">tooremove alle codes doorgeven een leeg hash-tabel:</span><span class="sxs-lookup"><span data-stu-id="99eb4-119">tooremove all tags, pass an empty hash table:</span></span>

```powershell
Set-AzureRmResourceGroup -Tag @{} -Name examplegroup
```



