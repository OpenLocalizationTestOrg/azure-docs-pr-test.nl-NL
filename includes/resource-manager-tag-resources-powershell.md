<span data-ttu-id="30ef0-101">Versie 3.0 van de module AzureRm.Resources bevatte belangrijke wijzigingen in de manier waarop u tags kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="30ef0-101">Version 3.0 of the AzureRm.Resources module included significant changes in how you work with tags.</span></span> <span data-ttu-id="30ef0-102">Controleer uw versie voordat u doorgaat:</span><span class="sxs-lookup"><span data-stu-id="30ef0-102">Before you proceed, check your version:</span></span>

```powershell
Get-Module -ListAvailable -Name AzureRm.Resources | Select Version
```

<span data-ttu-id="30ef0-103">Als uw resultaten versie 3.0 of hoger weergeven, werken de voorbeelden in dit onderwerp met uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="30ef0-103">If your results show version 3.0 or later, the examples in this topic work with your environment.</span></span> <span data-ttu-id="30ef0-104">Als u niet over versie 3.0 of hoger beschikt, [werkt u uw versie bij](/powershell/azureps-cmdlets-docs/) met behulp van PowerShell Gallery of Web Platform Installer voordat u verdergaat met dit onderwerp.</span><span class="sxs-lookup"><span data-stu-id="30ef0-104">If you do not have version 3.0 or later, [update your version](/powershell/azureps-cmdlets-docs/) by using PowerShell Gallery or Web Platform Installer before you proceed with this topic.</span></span>

```powershell
Version
-------
3.5.0
```

<span data-ttu-id="30ef0-105">Gebruik het volgende om de bestaande tags van een *resourcegroep* te bekijken:</span><span class="sxs-lookup"><span data-stu-id="30ef0-105">To see the existing tags for a *resource group*, use:</span></span>

```powershell
(Get-AzureRmResourceGroup -Name examplegroup).Tags
```

<span data-ttu-id="30ef0-106">Dat script retourneert de volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="30ef0-106">That script returns the following format:</span></span>

```powershell
Name                           Value
----                           -----
Dept                           IT
Environment                    Test
```

<span data-ttu-id="30ef0-107">Gebruik het volgende om de bestaande tags te bekijken van een *resource met een opgegeven bron-id*:</span><span class="sxs-lookup"><span data-stu-id="30ef0-107">To see the existing tags for a *resource that has a specified resource ID*, use:</span></span>

```powershell
(Get-AzureRmResource -ResourceId {resource-id}).Tags
```

<span data-ttu-id="30ef0-108">Of gebruik het volgende om de bestaande tags te bekijken van een *resource met een opgegeven naam en resourcegroep*:</span><span class="sxs-lookup"><span data-stu-id="30ef0-108">Or, to see the existing tags for a *resource that has a specified name and resource group*, use:</span></span>

```powershell
(Get-AzureRmResource -ResourceName examplevnet -ResourceGroupName examplegroup).Tags
```

<span data-ttu-id="30ef0-109">Gebruik het volgende om de *resourcegroepen met een specifieke tag* op te halen:</span><span class="sxs-lookup"><span data-stu-id="30ef0-109">To get *resource groups that have a specific tag*, use:</span></span>

```powershell
(Find-AzureRmResourceGroup -Tag @{ Dept="Finance" }).Name 
```

<span data-ttu-id="30ef0-110">Gebruik het volgende om de *resources met een specifieke tag* op te halen:</span><span class="sxs-lookup"><span data-stu-id="30ef0-110">To get *resources that have a specific tag*, use:</span></span>

```powershell
(Find-AzureRmResource -TagName Dept -TagValue Finance).Name
```

<span data-ttu-id="30ef0-111">Wanneer u tags op een resource of resourcegroep toepast, overschrijft u de bestaande tags van die resource of resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="30ef0-111">Every time you apply tags to a resource or a resource group, you overwrite the existing tags on that resource or resource group.</span></span> <span data-ttu-id="30ef0-112">Als u een resource of resourcegroep hebt met bestaande tags, gaat u anders te werk dan wanneer dat niet het geval is.</span><span class="sxs-lookup"><span data-stu-id="30ef0-112">Therefore, you must use a different approach based on whether the resource or resource group has existing tags.</span></span> 

<span data-ttu-id="30ef0-113">Gebruik het volgende om tags toe te voegen aan een *resourcegroep zonder bestaande tags*:</span><span class="sxs-lookup"><span data-stu-id="30ef0-113">To add tags to a *resource group without existing tags*, use:</span></span>

```powershell
Set-AzureRmResourceGroup -Name examplegroup -Tag @{ Dept="IT"; Environment="Test" }
```

<span data-ttu-id="30ef0-114">Als u tags wilt toevoegen aan een *resourcegroep met bestaande tags*, haalt u de bestaande tags op, voegt u de nieuwe tag toe en past u de tags opnieuw toe:</span><span class="sxs-lookup"><span data-stu-id="30ef0-114">To add tags to a *resource group that has existing tags*, retrieve the existing tags, add the new tag, and reapply the tags:</span></span>

```powershell
$tags = (Get-AzureRmResourceGroup -Name examplegroup).Tags
$tags += @{Status="Approved"}
Set-AzureRmResourceGroup -Tag $tags -Name examplegroup
```

<span data-ttu-id="30ef0-115">Gebruik het volgende om tags toe te voegen aan een *resource zonder bestaande tags*:</span><span class="sxs-lookup"><span data-stu-id="30ef0-115">To add tags to a *resource without existing tags*, use:</span></span>

```powershell
Set-AzureRmResource -Tag @{ Dept="IT"; Environment="Test" } -ResourceName examplevnet -ResourceGroupName examplegroup
```

<span data-ttu-id="30ef0-116">Gebruik het volgende om tags toe te voegen aan een *resource met bestaande tags*:</span><span class="sxs-lookup"><span data-stu-id="30ef0-116">To add tags to a *resource that has existing tags*, use:</span></span>

```powershell
$tags = (Get-AzureRmResource -ResourceName examplevnet -ResourceGroupName examplegroup).Tags
$tags += @{Status="Approved"}
Set-AzureRmResource -Tag $tags -ResourceName examplevnet -ResourceGroupName examplegroup
```

<span data-ttu-id="30ef0-117">Gebruik het volgende script als u alle tags van een resourcegroep op de bijbehorende resources wilt toepassen *zonder de bestaande tags voor de resources te behouden*:</span><span class="sxs-lookup"><span data-stu-id="30ef0-117">To apply all tags from a resource group to its resources, and *not retain existing tags on the resources*, use the following script:</span></span>

```powershell
$groups = Get-AzureRmResourceGroup
foreach ($g in $groups) 
{
    Find-AzureRmResource -ResourceGroupNameEquals $g.ResourceGroupName | ForEach-Object {Set-AzureRmResource -ResourceId $_.ResourceId -Tag $g.Tags -Force } 
}
```

<span data-ttu-id="30ef0-118">Gebruik het volgende script als u alle tags van een resourcegroep op de bijbehorende resources wilt toepassen *en de bestaande tags voor de resources die geen dubbele waarden zijn, wilt behouden*:</span><span class="sxs-lookup"><span data-stu-id="30ef0-118">To apply all tags from a resource group to its resources, and *retain existing tags on resources that are not duplicates*, use the following script:</span></span>

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

<span data-ttu-id="30ef0-119">Geef een lege hash-tabel door om alle tags te verwijderen:</span><span class="sxs-lookup"><span data-stu-id="30ef0-119">To remove all tags, pass an empty hash table:</span></span>

```powershell
Set-AzureRmResourceGroup -Tag @{} -Name examplegroup
```



