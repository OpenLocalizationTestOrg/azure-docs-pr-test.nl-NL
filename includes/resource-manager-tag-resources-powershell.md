Versie 3.0 van Hallo AzureRm.Resources module opgenomen belangrijke wijzigingen in hoe u met labels werkt. Controleer uw versie voordat u doorgaat:

```powershell
Get-Module -ListAvailable -Name AzureRm.Resources | Select Version
```

Als uw resultaten versie 3.0 of hoger, Hallo voorbeelden in dit onderwerp werken met uw omgeving weergeven. Als u niet over versie 3.0 of hoger beschikt, [werkt u uw versie bij](/powershell/azureps-cmdlets-docs/) met behulp van PowerShell Gallery of Web Platform Installer voordat u verdergaat met dit onderwerp.

```powershell
Version
-------
3.5.0
```

toosee Hallo bestaande codes voor een *resourcegroep*, gebruiken:

```powershell
(Get-AzureRmResourceGroup -Name examplegroup).Tags
```

Script retourneert Hallo volgende indeling:

```powershell
Name                           Value
----                           -----
Dept                           IT
Environment                    Test
```

toosee Hallo bestaande codes voor een *resource met een opgegeven bron-ID*, gebruiken:

```powershell
(Get-AzureRmResource -ResourceId {resource-id}).Tags
```

Of toosee Hallo bestaande codes voor een *resource met een opgegeven groep en de bron*, gebruiken:

```powershell
(Get-AzureRmResource -ResourceName examplevnet -ResourceGroupName examplegroup).Tags
```

tooget *resourcegroepen die beschikken over een specifieke tag*, gebruiken:

```powershell
(Find-AzureRmResourceGroup -Tag @{ Dept="Finance" }).Name 
```

tooget *resources met een specifieke tag*, gebruiken:

```powershell
(Find-AzureRmResource -TagName Dept -TagValue Finance).Name
```

Telkens wanneer u labels tooa resource of een resourcegroep hebt toegepast, kunt u bestaande labels op die resource of resourcegroep Hallo overschrijven. Daarom moet u een andere benadering, op basis van of Hallo resource of resourcegroep bestaande labels heeft. 

tooadd tags tooa *resourcegroep zonder bestaande tags*, gebruiken:

```powershell
Set-AzureRmResourceGroup -Name examplegroup -Tag @{ Dept="IT"; Environment="Test" }
```

tooadd tags tooa *bronnengroep met bestaande codes*, Hallo bestaande codes ophalen, Hallo nieuw label toevoegen en Hallo tags toepassen:

```powershell
$tags = (Get-AzureRmResourceGroup -Name examplegroup).Tags
$tags += @{Status="Approved"}
Set-AzureRmResourceGroup -Tag $tags -Name examplegroup
```

tooadd tags tooa *resource zonder bestaande tags*, gebruiken:

```powershell
Set-AzureRmResource -Tag @{ Dept="IT"; Environment="Test" } -ResourceName examplevnet -ResourceGroupName examplegroup
```

tooadd tags tooa *resource met bestaande codes*, gebruiken:

```powershell
$tags = (Get-AzureRmResource -ResourceName examplevnet -ResourceGroupName examplegroup).Tags
$tags += @{Status="Approved"}
Set-AzureRmResource -Tag $tags -ResourceName examplevnet -ResourceGroupName examplegroup
```

tooapply die alle labels van een resource tooits groepsbronnen en *bestaande labels op Hallo resources niet bewaren*, Hallo script volgende gebruiken:

```powershell
$groups = Get-AzureRmResourceGroup
foreach ($g in $groups) 
{
    Find-AzureRmResource -ResourceGroupNameEquals $g.ResourceGroupName | ForEach-Object {Set-AzureRmResource -ResourceId $_.ResourceId -Tag $g.Tags -Force } 
}
```

tooapply die alle labels van een resource tooits groepsbronnen en *bestaande tags voor resources die geen dubbele waarden behouden*, Hallo script volgende gebruiken:

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

tooremove alle codes doorgeven een leeg hash-tabel:

```powershell
Set-AzureRmResourceGroup -Tag @{} -Name examplegroup
```



