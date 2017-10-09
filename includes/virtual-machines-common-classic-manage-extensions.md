


## <a name="using-vm-extensions"></a><span data-ttu-id="3de66-101">Met behulp van de VM-extensies</span><span class="sxs-lookup"><span data-stu-id="3de66-101">Using VM Extensions</span></span>
<span data-ttu-id="3de66-102">Azure VM-extensies implementeren gedrag of functies waarmee een andere programma's werken op Azure Virtual machines (bijvoorbeeld Hallo **WebDeployForVSDevTest** extensie kunt Visual Studio tooWeb oplossingen implementeren in uw Azure VM) of geef mogelijkheid voor toointeract met Hallo VM toosupport sommige andere gedrag Hallo (bijvoorbeeld, u kunt gebruiken Hallo VM toegang tot de uitbreidingen van PowerShell, hello Azure CLI en REST clients tooreset of wijzigt u de waarden van de externe toegang in uw Azure VM).</span><span class="sxs-lookup"><span data-stu-id="3de66-102">Azure VM Extensions implement behaviors or features that either help other programs work on Azure VMs (for example, hello **WebDeployForVSDevTest** extension allows Visual Studio tooWeb Deploy solutions on your Azure VM) or provide hello ability for you toointeract with hello VM toosupport some other behavior (for example, you can use hello VM Access extensions from PowerShell, hello Azure CLI, and REST clients tooreset or modify remote access values on your Azure VM).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3de66-103">Zie voor een volledige lijst met uitbreidingen voor het Hallo-functies ze ondersteunen voor [Azure VM-extensies en functies](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3de66-103">For a complete list of extensions by hello features they support, see [Azure VM Extensions and Features](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="3de66-104">Omdat elke VM-extensie een specifieke functie ondersteunt, precies wat u wel en niet met de extensie is afhankelijk van Hallo-extensie.</span><span class="sxs-lookup"><span data-stu-id="3de66-104">Because each VM extension supports a specific feature, exactly what you can and cannot do with an extension depends on hello extension.</span></span> <span data-ttu-id="3de66-105">Voordat u uw virtuele machine wijzigt, zorg er daarom voor dat u Hallo-documentatie voor VM-extensie die u wilt dat toouse Hallo hebt gelezen.</span><span class="sxs-lookup"><span data-stu-id="3de66-105">Therefore, before modifying your VM, make sure you have read hello documentation for hello VM Extension you want toouse.</span></span> <span data-ttu-id="3de66-106">Verwijderen van bepaalde extensies VM wordt niet ondersteund; anderen hebben eigenschappen die kunnen worden ingesteld die het gedrag van de virtuele machine drastisch wijzigen.</span><span class="sxs-lookup"><span data-stu-id="3de66-106">Removing some VM Extensions is not supported; others have properties that can be set that change VM behavior radically.</span></span>
> 
> 

<span data-ttu-id="3de66-107">Hallo meest algemene taken zijn:</span><span class="sxs-lookup"><span data-stu-id="3de66-107">hello most common tasks are:</span></span>

1. <span data-ttu-id="3de66-108">Zoeken naar beschikbare uitbreidingen</span><span class="sxs-lookup"><span data-stu-id="3de66-108">Finding Available Extensions</span></span>
2. <span data-ttu-id="3de66-109">Bijwerken van geladen uitbreidingen</span><span class="sxs-lookup"><span data-stu-id="3de66-109">Updating Loaded Extensions</span></span>
3. <span data-ttu-id="3de66-110">Uitbreidingen toevoegen</span><span class="sxs-lookup"><span data-stu-id="3de66-110">Adding Extensions</span></span>
4. <span data-ttu-id="3de66-111">Extensies verwijderen</span><span class="sxs-lookup"><span data-stu-id="3de66-111">Removing Extensions</span></span>

## <a name="find-available-extensions"></a><span data-ttu-id="3de66-112">Zoeken naar beschikbare uitbreidingen</span><span class="sxs-lookup"><span data-stu-id="3de66-112">Find Available Extensions</span></span>
<span data-ttu-id="3de66-113">U kunt-extensie en met behulp van uitgebreide informatie vinden:</span><span class="sxs-lookup"><span data-stu-id="3de66-113">You can locate extension and extended information using:</span></span>

* <span data-ttu-id="3de66-114">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3de66-114">PowerShell</span></span>
* <span data-ttu-id="3de66-115">Azure platformoverschrijdende opdrachtregel-Interface (Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="3de66-115">Azure Cross-Platform Command Line Interface (Azure CLI)</span></span>
* <span data-ttu-id="3de66-116">Service Management REST API</span><span class="sxs-lookup"><span data-stu-id="3de66-116">Service Management REST API</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="3de66-117">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="3de66-117">Azure PowerShell</span></span>
<span data-ttu-id="3de66-118">Bepaalde extensies hebben PowerShell-cmdlets die zijn specifieke toothem, waardoor de configuratie vanuit PowerShell gemakkelijker; maar hello volgende cmdlets werkt voor alle VM-extensies.</span><span class="sxs-lookup"><span data-stu-id="3de66-118">Some extensions have PowerShell cmdlets that are specific toothem, which may make their configuration from PowerShell easier; but hello following cmdlets work for all VM extensions.</span></span>

<span data-ttu-id="3de66-119">U kunt Hallo cmdlets tooobtain informatie over de beschikbare uitbreidingen te volgen:</span><span class="sxs-lookup"><span data-stu-id="3de66-119">You can use hello following cmdlets tooobtain information about available extensions:</span></span>

* <span data-ttu-id="3de66-120">Voor exemplaren van webrollen en werkrollen kunt u Hallo [Get-AzureServiceAvailableExtension](https://msdn.microsoft.com/library/azure/dn722498.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3de66-120">For instances of web roles or worker roles, you can use hello [Get-AzureServiceAvailableExtension](https://msdn.microsoft.com/library/azure/dn722498.aspx) cmdlet.</span></span>
* <span data-ttu-id="3de66-121">Voor exemplaren van virtuele Machines, kunt u Hallo [Get-AzureVMAvailableExtension](https://msdn.microsoft.com/library/azure/dn722480.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3de66-121">For instances of Virtual Machines, you can use hello [Get-AzureVMAvailableExtension](https://msdn.microsoft.com/library/azure/dn722480.aspx) cmdlet.</span></span>
  
   <span data-ttu-id="3de66-122">Bijvoorbeeld Hallo volgende code voorbeeld ziet u hoe de gegevens voor Hallo toolist **IaaSDiagnostics** uitbreiding met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3de66-122">For example, hello following code example shows how toolist the information for hello **IaaSDiagnostics** extension using PowerShell.</span></span>
  
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

### <a name="azure-command-line-interface-azure-cli"></a><span data-ttu-id="3de66-123">Azure vanaf de opdrachtregel-Interface (Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="3de66-123">Azure Command Line Interface (Azure CLI)</span></span>
<span data-ttu-id="3de66-124">Bepaalde extensies zijn Azure CLI-opdrachten die specifieke toothem (Hallo Docker VM-extensie is een voorbeeld), die de configuratie kan eenvoudiger; maar Hallo volgende opdrachten uit voor alle VM-extensies.</span><span class="sxs-lookup"><span data-stu-id="3de66-124">Some extensions have Azure CLI commands that are specific toothem (hello Docker VM Extension is one example), which may make their configuration easier; but hello following commands work for all VM extensions.</span></span>

<span data-ttu-id="3de66-125">Kunt u Hallo **azure vm-extensielijst** opdracht tooobtain informatie over de beschikbare uitbreidingen en gebruik Hallo **–-json** optie toodisplay alle beschikbare informatie over een of meer uitbreidingen.</span><span class="sxs-lookup"><span data-stu-id="3de66-125">You can use hello **azure vm extension list** command tooobtain information about available extensions, and use hello **–-json** option toodisplay all available information about one or more extensions.</span></span> <span data-ttu-id="3de66-126">Als u de naam van een uitbreiding niet gebruikt, retourneert Hallo opdracht een JSON-beschrijving van alle beschikbare uitbreidingen.</span><span class="sxs-lookup"><span data-stu-id="3de66-126">If you do not use an extension name, hello command returns a JSON description of all available extensions.</span></span>

<span data-ttu-id="3de66-127">Hallo volgende codevoorbeeld ziet u bijvoorbeeld hoe toolist informatie voor Hallo Hallo **IaaSDiagnostics** met behulp van de extensie Azure CLI Hallo **azure vm-extensielijst** opdracht en het gebruik Hallo **–-json** optie tooreturn volledige informatie.</span><span class="sxs-lookup"><span data-stu-id="3de66-127">For example, hello following code example shows how toolist hello information for hello **IaaSDiagnostics** extension using hello Azure CLI **azure vm extension list** command and uses hello **–-json** option tooreturn complete information.</span></span>

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



### <a name="service-management-rest-apis"></a><span data-ttu-id="3de66-128">REST API's voor Service Management</span><span class="sxs-lookup"><span data-stu-id="3de66-128">Service Management REST APIs</span></span>
<span data-ttu-id="3de66-129">U kunt Hallo REST-API's tooobtain informatie over de beschikbare uitbreidingen te volgen:</span><span class="sxs-lookup"><span data-stu-id="3de66-129">You can use hello following REST APIs tooobtain information about available extensions:</span></span>

* <span data-ttu-id="3de66-130">Voor exemplaren van webrollen en werkrollen kunt u Hallo [lijst met beschikbare uitbreidingen](https://msdn.microsoft.com/library/dn169559.aspx) bewerking.</span><span class="sxs-lookup"><span data-stu-id="3de66-130">For instances of web roles or worker roles, you can use hello [List Available Extensions](https://msdn.microsoft.com/library/dn169559.aspx) operation.</span></span> <span data-ttu-id="3de66-131">toolist hello versies van de beschikbare uitbreidingen, kunt u [lijst extensie versies](https://msdn.microsoft.com/library/dn495437.aspx).</span><span class="sxs-lookup"><span data-stu-id="3de66-131">toolist hello versions of available extensions, you can use [List Extension Versions](https://msdn.microsoft.com/library/dn495437.aspx).</span></span>
* <span data-ttu-id="3de66-132">Voor exemplaren van virtuele Machines, kunt u Hallo [lijst Resource-uitbreidingen](https://msdn.microsoft.com/library/dn495441.aspx) bewerking.</span><span class="sxs-lookup"><span data-stu-id="3de66-132">For instances of Virtual Machines, you can use hello [List Resource Extensions](https://msdn.microsoft.com/library/dn495441.aspx) operation.</span></span> <span data-ttu-id="3de66-133">toolist hello versies van de beschikbare uitbreidingen, kunt u [lijst Resource-uitbreiding versies](https://msdn.microsoft.com/library/dn495440.aspx).</span><span class="sxs-lookup"><span data-stu-id="3de66-133">toolist hello versions of available extensions, you can use [List Resource Extension Versions](https://msdn.microsoft.com/library/dn495440.aspx).</span></span>

## <a name="add-update-or-disable-extensions"></a><span data-ttu-id="3de66-134">Toevoegen, bijwerken of extensies uitschakelen</span><span class="sxs-lookup"><span data-stu-id="3de66-134">Add, Update, or Disable Extensions</span></span>
<span data-ttu-id="3de66-135">Uitbreidingen kunnen worden toegevoegd wanneer een exemplaar is gemaakt of ze kunnen worden toegevoegd met een exemplaar van tooa.</span><span class="sxs-lookup"><span data-stu-id="3de66-135">Extensions can be added when an instance is created or they can be added tooa running instance.</span></span> <span data-ttu-id="3de66-136">Uitbreidingen kunnen worden bijgewerkt, uitgeschakeld of verwijderd.</span><span class="sxs-lookup"><span data-stu-id="3de66-136">Extensions can be updated, disabled, or removed.</span></span> <span data-ttu-id="3de66-137">U kunt deze acties uitvoeren met behulp van Azure PowerShell-cmdlets of via Hallo Service Management REST-API-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="3de66-137">You can perform these actions by using Azure PowerShell cmdlets or by using hello Service Management REST API operations.</span></span> <span data-ttu-id="3de66-138">Parameters zijn vereist tooinstall en bepaalde extensies instellen.</span><span class="sxs-lookup"><span data-stu-id="3de66-138">Parameters are required tooinstall and set up some extensions.</span></span> <span data-ttu-id="3de66-139">Openbare en persoonlijke parameters worden ondersteund voor uitbreidingen.</span><span class="sxs-lookup"><span data-stu-id="3de66-139">Public and private parameters are supported for extensions.</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="3de66-140">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="3de66-140">Azure PowerShell</span></span>
<span data-ttu-id="3de66-141">Met Azure PowerShell-cmdlets is Hallo gemakkelijkste manier tooadd en update-extensies.</span><span class="sxs-lookup"><span data-stu-id="3de66-141">Using Azure PowerShell cmdlets is hello easiest way tooadd and update extensions.</span></span> <span data-ttu-id="3de66-142">Wanneer u Hallo extensie cmdlets gebruikt, wordt de meeste Hallo configuratie van de uitbreiding Hallo geldt voor u.</span><span class="sxs-lookup"><span data-stu-id="3de66-142">When you use hello extension cmdlets, most of hello configuration of hello extension is done for you.</span></span> <span data-ttu-id="3de66-143">Soms moet u mogelijk een extensie tooprogrammatically toevoegen.</span><span class="sxs-lookup"><span data-stu-id="3de66-143">At times, you may need tooprogrammatically add an extension.</span></span> <span data-ttu-id="3de66-144">Wanneer u toodo dit moet, moet u Hallo configuratie van de uitbreiding Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="3de66-144">When you need toodo this, you must provide hello configuration of hello extension.</span></span>

<span data-ttu-id="3de66-145">Hallo cmdlets tooknow te volgen of een uitbreiding is een configuratie van openbare en persoonlijke parameters vereist, kunt u gebruiken:</span><span class="sxs-lookup"><span data-stu-id="3de66-145">You can use hello following cmdlets tooknow whether an extension requires a configuration of public and private parameters:</span></span>

* <span data-ttu-id="3de66-146">Voor exemplaren van webrollen en werkrollen kunt u Hallo **Get-AzureServiceAvailableExtension** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3de66-146">For instances of web roles or worker roles, you can use hello **Get-AzureServiceAvailableExtension** cmdlet.</span></span>
* <span data-ttu-id="3de66-147">Voor exemplaren van virtuele Machines, kunt u Hallo **Get-AzureVMAvailableExtension** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3de66-147">For instances of Virtual Machines, you can use hello **Get-AzureVMAvailableExtension** cmdlet.</span></span>

### <a name="service-management-rest-apis"></a><span data-ttu-id="3de66-148">REST API's voor Service Management</span><span class="sxs-lookup"><span data-stu-id="3de66-148">Service Management REST APIs</span></span>
<span data-ttu-id="3de66-149">Wanneer u een lijst met beschikbare uitbreidingen ophalen met behulp van Hallo REST-API's, krijgt u informatie over hoe Hallo extensie toobe geconfigureerd is.</span><span class="sxs-lookup"><span data-stu-id="3de66-149">When you retrieve a listing of available extensions by using hello REST APIs, you receive information about how hello extension is toobe configured.</span></span> <span data-ttu-id="3de66-150">Hallo-informatie die wordt geretourneerd mogelijk parameterinformatie dat wordt vertegenwoordigd door een openbare schema en een persoonlijke schema weergeven.</span><span class="sxs-lookup"><span data-stu-id="3de66-150">hello information that is returned might show parameter information represented by a public schema and private schema.</span></span> <span data-ttu-id="3de66-151">Openbare parameterwaarden worden in query's over Hallo exemplaren geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="3de66-151">Public parameter values are returned in queries about hello instances.</span></span> <span data-ttu-id="3de66-152">Persoonlijke parameterwaarden worden niet geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="3de66-152">Private parameter values are not returned.</span></span>

<span data-ttu-id="3de66-153">Hallo tooknow REST-API's te volgen of een uitbreiding is een configuratie van openbare en persoonlijke parameters vereist, kunt u gebruiken:</span><span class="sxs-lookup"><span data-stu-id="3de66-153">You can use hello following REST APIs tooknow whether an extension requires a configuration of public and private parameters:</span></span>

* <span data-ttu-id="3de66-154">Voor exemplaren van webrollen of werkrollen, Hallo **PublicConfigurationSchema** en **PrivateConfigurationSchema** elementen bevatten informatie in het antwoord Hallo HALLO hallo [lijst Beschikbare uitbreidingen](https://msdn.microsoft.com/library/dn169559.aspx) bewerking.</span><span class="sxs-lookup"><span data-stu-id="3de66-154">For instances of web roles or worker roles, hello **PublicConfigurationSchema** and **PrivateConfigurationSchema** elements contain hello information in hello response from hello [List Available Extensions](https://msdn.microsoft.com/library/dn169559.aspx) operation.</span></span>
* <span data-ttu-id="3de66-155">Voor exemplaren van virtuele Machines Hallo **PublicConfigurationSchema** en **PrivateConfigurationSchema** elementen bevatten informatie in het antwoord Hallo HALLO hallo [lijst Resource-uitbreidingen](https://msdn.microsoft.com/library/dn495441.aspx) bewerking.</span><span class="sxs-lookup"><span data-stu-id="3de66-155">For instances of Virtual Machines, hello **PublicConfigurationSchema** and **PrivateConfigurationSchema** elements contain hello information in hello response from hello [List Resource Extensions](https://msdn.microsoft.com/library/dn495441.aspx) operation.</span></span>

> [!NOTE]
> <span data-ttu-id="3de66-156">Extensies kunnen ook gebruiken voor configuraties die zijn gedefinieerd met JSON.</span><span class="sxs-lookup"><span data-stu-id="3de66-156">Extensions can also use configurations that are defined with JSON.</span></span> <span data-ttu-id="3de66-157">Wanneer deze typen uitbreidingen worden gebruikt, alleen Hallo **SampleConfig** element wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="3de66-157">When these types of extensions are used, only hello **SampleConfig** element is used.</span></span>
> 
> 

