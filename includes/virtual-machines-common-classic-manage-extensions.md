


## <a name="using-vm-extensions"></a>Met behulp van de VM-extensies
Azure VM-extensies implementeren gedrag of functies waarmee een andere programma's werken op Azure Virtual machines (bijvoorbeeld Hallo **WebDeployForVSDevTest** extensie kunt Visual Studio tooWeb oplossingen implementeren in uw Azure VM) of geef mogelijkheid voor toointeract met Hallo VM toosupport sommige andere gedrag Hallo (bijvoorbeeld, u kunt gebruiken Hallo VM toegang tot de uitbreidingen van PowerShell, hello Azure CLI en REST clients tooreset of wijzigt u de waarden van de externe toegang in uw Azure VM).

> [!IMPORTANT]
> Zie voor een volledige lijst met uitbreidingen voor het Hallo-functies ze ondersteunen voor [Azure VM-extensies en functies](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Omdat elke VM-extensie een specifieke functie ondersteunt, precies wat u wel en niet met de extensie is afhankelijk van Hallo-extensie. Voordat u uw virtuele machine wijzigt, zorg er daarom voor dat u Hallo-documentatie voor VM-extensie die u wilt dat toouse Hallo hebt gelezen. Verwijderen van bepaalde extensies VM wordt niet ondersteund; anderen hebben eigenschappen die kunnen worden ingesteld die het gedrag van de virtuele machine drastisch wijzigen.
> 
> 

Hallo meest algemene taken zijn:

1. Zoeken naar beschikbare uitbreidingen
2. Bijwerken van geladen uitbreidingen
3. Uitbreidingen toevoegen
4. Extensies verwijderen

## <a name="find-available-extensions"></a>Zoeken naar beschikbare uitbreidingen
U kunt-extensie en met behulp van uitgebreide informatie vinden:

* PowerShell
* Azure platformoverschrijdende opdrachtregel-Interface (Azure CLI)
* Service Management REST API

### <a name="azure-powershell"></a>Azure PowerShell
Bepaalde extensies hebben PowerShell-cmdlets die zijn specifieke toothem, waardoor de configuratie vanuit PowerShell gemakkelijker; maar hello volgende cmdlets werkt voor alle VM-extensies.

U kunt Hallo cmdlets tooobtain informatie over de beschikbare uitbreidingen te volgen:

* Voor exemplaren van webrollen en werkrollen kunt u Hallo [Get-AzureServiceAvailableExtension](https://msdn.microsoft.com/library/azure/dn722498.aspx) cmdlet.
* Voor exemplaren van virtuele Machines, kunt u Hallo [Get-AzureVMAvailableExtension](https://msdn.microsoft.com/library/azure/dn722480.aspx) cmdlet.
  
   Bijvoorbeeld Hallo volgende code voorbeeld ziet u hoe de gegevens voor Hallo toolist **IaaSDiagnostics** uitbreiding met behulp van PowerShell.
  
      PS C:\> Get-AzureVMAvailableExtension -ExtensionName IaaSDiagnostics
  
      Publisher                   : Microsoft.Azure.Diagnostics
      ExtensionName               : IaaSDiagnostics
      Version                     : 1.2
      Label                       : Microsoft Monitoring Agent Diagnostics
      Description                 : Microsoft Monitoring Agent Extension
      PublicConfigurationSchema   :
      PrivateConfigurationSchema  :
      IsInternalExtension         : False
      SampleConfig                :
      ReplicationCompleted        : True
      Eula                        :
      PrivacyUri                  :
      HomepageUri                 :
      IsJsonExtension             : True
      DisallowMajorVersionUpgrade : False
      SupportedOS                 :
      PublishedDate               :
      CompanyName                 :

### <a name="azure-command-line-interface-azure-cli"></a>Azure vanaf de opdrachtregel-Interface (Azure CLI)
Bepaalde extensies zijn Azure CLI-opdrachten die specifieke toothem (Hallo Docker VM-extensie is een voorbeeld), die de configuratie kan eenvoudiger; maar Hallo volgende opdrachten uit voor alle VM-extensies.

Kunt u Hallo **azure vm-extensielijst** opdracht tooobtain informatie over de beschikbare uitbreidingen en gebruik Hallo **–-json** optie toodisplay alle beschikbare informatie over een of meer uitbreidingen. Als u de naam van een uitbreiding niet gebruikt, retourneert Hallo opdracht een JSON-beschrijving van alle beschikbare uitbreidingen.

Hallo volgende codevoorbeeld ziet u bijvoorbeeld hoe toolist informatie voor Hallo Hallo **IaaSDiagnostics** met behulp van de extensie Azure CLI Hallo **azure vm-extensielijst** opdracht en het gebruik Hallo **–-json** optie tooreturn volledige informatie.

    $ azure vm extension list -n IaaSDiagnostics --json
    [
      {
        "publisher": "Microsoft.Azure.Diagnostics",
        "name": "IaaSDiagnostics",
        "version": "1.2",
        "label": "Microsoft Monitoring Agent Diagnostics",
        "description": "Microsoft Monitoring Agent Extension",
        "replicationCompleted": true,
        "isJsonExtension": true
      }
    ]



### <a name="service-management-rest-apis"></a>REST API's voor Service Management
U kunt Hallo REST-API's tooobtain informatie over de beschikbare uitbreidingen te volgen:

* Voor exemplaren van webrollen en werkrollen kunt u Hallo [lijst met beschikbare uitbreidingen](https://msdn.microsoft.com/library/dn169559.aspx) bewerking. toolist hello versies van de beschikbare uitbreidingen, kunt u [lijst extensie versies](https://msdn.microsoft.com/library/dn495437.aspx).
* Voor exemplaren van virtuele Machines, kunt u Hallo [lijst Resource-uitbreidingen](https://msdn.microsoft.com/library/dn495441.aspx) bewerking. toolist hello versies van de beschikbare uitbreidingen, kunt u [lijst Resource-uitbreiding versies](https://msdn.microsoft.com/library/dn495440.aspx).

## <a name="add-update-or-disable-extensions"></a>Toevoegen, bijwerken of extensies uitschakelen
Uitbreidingen kunnen worden toegevoegd wanneer een exemplaar is gemaakt of ze kunnen worden toegevoegd met een exemplaar van tooa. Uitbreidingen kunnen worden bijgewerkt, uitgeschakeld of verwijderd. U kunt deze acties uitvoeren met behulp van Azure PowerShell-cmdlets of via Hallo Service Management REST-API-bewerkingen. Parameters zijn vereist tooinstall en bepaalde extensies instellen. Openbare en persoonlijke parameters worden ondersteund voor uitbreidingen.

### <a name="azure-powershell"></a>Azure PowerShell
Met Azure PowerShell-cmdlets is Hallo gemakkelijkste manier tooadd en update-extensies. Wanneer u Hallo extensie cmdlets gebruikt, wordt de meeste Hallo configuratie van de uitbreiding Hallo geldt voor u. Soms moet u mogelijk een extensie tooprogrammatically toevoegen. Wanneer u toodo dit moet, moet u Hallo configuratie van de uitbreiding Hallo opgeven.

Hallo cmdlets tooknow te volgen of een uitbreiding is een configuratie van openbare en persoonlijke parameters vereist, kunt u gebruiken:

* Voor exemplaren van webrollen en werkrollen kunt u Hallo **Get-AzureServiceAvailableExtension** cmdlet.
* Voor exemplaren van virtuele Machines, kunt u Hallo **Get-AzureVMAvailableExtension** cmdlet.

### <a name="service-management-rest-apis"></a>REST API's voor Service Management
Wanneer u een lijst met beschikbare uitbreidingen ophalen met behulp van Hallo REST-API's, krijgt u informatie over hoe Hallo extensie toobe geconfigureerd is. Hallo-informatie die wordt geretourneerd mogelijk parameterinformatie dat wordt vertegenwoordigd door een openbare schema en een persoonlijke schema weergeven. Openbare parameterwaarden worden in query's over Hallo exemplaren geretourneerd. Persoonlijke parameterwaarden worden niet geretourneerd.

Hallo tooknow REST-API's te volgen of een uitbreiding is een configuratie van openbare en persoonlijke parameters vereist, kunt u gebruiken:

* Voor exemplaren van webrollen of werkrollen, Hallo **PublicConfigurationSchema** en **PrivateConfigurationSchema** elementen bevatten informatie in het antwoord Hallo HALLO hallo [lijst Beschikbare uitbreidingen](https://msdn.microsoft.com/library/dn169559.aspx) bewerking.
* Voor exemplaren van virtuele Machines Hallo **PublicConfigurationSchema** en **PrivateConfigurationSchema** elementen bevatten informatie in het antwoord Hallo HALLO hallo [lijst Resource-uitbreidingen](https://msdn.microsoft.com/library/dn495441.aspx) bewerking.

> [!NOTE]
> Extensies kunnen ook gebruiken voor configuraties die zijn gedefinieerd met JSON. Wanneer deze typen uitbreidingen worden gebruikt, alleen Hallo **SampleConfig** element wordt gebruikt.
> 
> 

