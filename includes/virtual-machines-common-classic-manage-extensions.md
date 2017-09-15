


## <a name="using-vm-extensions"></a><span data-ttu-id="1cab5-101">Met behulp van de VM-extensies</span><span class="sxs-lookup"><span data-stu-id="1cab5-101">Using VM Extensions</span></span>
<span data-ttu-id="1cab5-102">Azure VM-extensies implementeren gedrag of functies waarmee een andere programma's werken op Azure Virtual machines (bijvoorbeeld de **WebDeployForVSDevTest** uitbreiding kunt Visual Studio Web Deploy-oplossingen voor uw Azure VM) of geef de mogelijkheid om te communiceren met de virtuele machine te ondersteunen sommige andere gedrag (bijvoorbeeld, kunt u de toegang van de VM-uitbreidingen van PowerShell, de Azure CLI en REST-clients opnieuw instellen of wijzigen van waarden voor externe toegang in uw Azure VM).</span><span class="sxs-lookup"><span data-stu-id="1cab5-102">Azure VM Extensions implement behaviors or features that either help other programs work on Azure VMs (for example, the **WebDeployForVSDevTest** extension allows Visual Studio to Web Deploy solutions on your Azure VM) or provide the ability for you to interact with the VM to support some other behavior (for example, you can use the VM Access extensions from PowerShell, the Azure CLI, and REST clients to reset or modify remote access values on your Azure VM).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1cab5-103">Zie voor een volledige lijst met extensies die door de functies ze ondersteunen [Azure VM-extensies en functies](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1cab5-103">For a complete list of extensions by the features they support, see [Azure VM Extensions and Features](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="1cab5-104">Omdat elke VM-extensie een specifieke functie ondersteunt, precies wat u wel en niet met de extensie is afhankelijk van de extensie.</span><span class="sxs-lookup"><span data-stu-id="1cab5-104">Because each VM extension supports a specific feature, exactly what you can and cannot do with an extension depends on the extension.</span></span> <span data-ttu-id="1cab5-105">Voordat u uw virtuele machine wijzigt, zorg er daarom voor dat u de documentatie voor de VM-extensie die u wilt gebruiken hebt gelezen.</span><span class="sxs-lookup"><span data-stu-id="1cab5-105">Therefore, before modifying your VM, make sure you have read the documentation for the VM Extension you want to use.</span></span> <span data-ttu-id="1cab5-106">Verwijderen van bepaalde extensies VM wordt niet ondersteund; anderen hebben eigenschappen die kunnen worden ingesteld die het gedrag van de virtuele machine drastisch wijzigen.</span><span class="sxs-lookup"><span data-stu-id="1cab5-106">Removing some VM Extensions is not supported; others have properties that can be set that change VM behavior radically.</span></span>
> 
> 

<span data-ttu-id="1cab5-107">De meest algemene taken zijn:</span><span class="sxs-lookup"><span data-stu-id="1cab5-107">The most common tasks are:</span></span>

1. <span data-ttu-id="1cab5-108">Zoeken naar beschikbare uitbreidingen</span><span class="sxs-lookup"><span data-stu-id="1cab5-108">Finding Available Extensions</span></span>
2. <span data-ttu-id="1cab5-109">Bijwerken van geladen uitbreidingen</span><span class="sxs-lookup"><span data-stu-id="1cab5-109">Updating Loaded Extensions</span></span>
3. <span data-ttu-id="1cab5-110">Uitbreidingen toevoegen</span><span class="sxs-lookup"><span data-stu-id="1cab5-110">Adding Extensions</span></span>
4. <span data-ttu-id="1cab5-111">Extensies verwijderen</span><span class="sxs-lookup"><span data-stu-id="1cab5-111">Removing Extensions</span></span>

## <a name="find-available-extensions"></a><span data-ttu-id="1cab5-112">Zoeken naar beschikbare uitbreidingen</span><span class="sxs-lookup"><span data-stu-id="1cab5-112">Find Available Extensions</span></span>
<span data-ttu-id="1cab5-113">U kunt-extensie en met behulp van uitgebreide informatie vinden:</span><span class="sxs-lookup"><span data-stu-id="1cab5-113">You can locate extension and extended information using:</span></span>

* <span data-ttu-id="1cab5-114">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1cab5-114">PowerShell</span></span>
* <span data-ttu-id="1cab5-115">Azure platformoverschrijdende opdrachtregel-Interface (Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="1cab5-115">Azure Cross-Platform Command Line Interface (Azure CLI)</span></span>
* <span data-ttu-id="1cab5-116">Service Management REST API</span><span class="sxs-lookup"><span data-stu-id="1cab5-116">Service Management REST API</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="1cab5-117">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="1cab5-117">Azure PowerShell</span></span>
<span data-ttu-id="1cab5-118">Bepaalde extensies hebben PowerShell-cmdlets die specifiek zijn voor deze, waardoor de configuratie vanuit PowerShell gemakkelijker; maar de volgende cmdlets werkt voor alle VM-extensies.</span><span class="sxs-lookup"><span data-stu-id="1cab5-118">Some extensions have PowerShell cmdlets that are specific to them, which may make their configuration from PowerShell easier; but the following cmdlets work for all VM extensions.</span></span>

<span data-ttu-id="1cab5-119">U kunt de volgende cmdlets gebruiken om informatie over de beschikbare uitbreidingen te verkrijgen:</span><span class="sxs-lookup"><span data-stu-id="1cab5-119">You can use the following cmdlets to obtain information about available extensions:</span></span>

* <span data-ttu-id="1cab5-120">Voor exemplaren van de functie web- of werkrollen kunt u de [Get-AzureServiceAvailableExtension](https://msdn.microsoft.com/library/azure/dn722498.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1cab5-120">For instances of web roles or worker roles, you can use the [Get-AzureServiceAvailableExtension](https://msdn.microsoft.com/library/azure/dn722498.aspx) cmdlet.</span></span>
* <span data-ttu-id="1cab5-121">Voor exemplaren van virtuele Machines, kunt u de [Get-AzureVMAvailableExtension](https://msdn.microsoft.com/library/azure/dn722480.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1cab5-121">For instances of Virtual Machines, you can use the [Get-AzureVMAvailableExtension](https://msdn.microsoft.com/library/azure/dn722480.aspx) cmdlet.</span></span>
  
   <span data-ttu-id="1cab5-122">Het volgende codevoorbeeld ziet u hoe u de gegevens voor de **IaaSDiagnostics** uitbreiding met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1cab5-122">For example, the following code example shows how to list the information for the **IaaSDiagnostics** extension using PowerShell.</span></span>
  
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

### <a name="azure-command-line-interface-azure-cli"></a><span data-ttu-id="1cab5-123">Azure vanaf de opdrachtregel-Interface (Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="1cab5-123">Azure Command Line Interface (Azure CLI)</span></span>
<span data-ttu-id="1cab5-124">Bepaalde extensies zijn Azure CLI-opdrachten die specifiek voor deze zijn (de Docker-VM-extensie is een voorbeeld), die de configuratie kan eenvoudiger; maar de volgende opdrachten beschikbaar voor alle VM-extensies.</span><span class="sxs-lookup"><span data-stu-id="1cab5-124">Some extensions have Azure CLI commands that are specific to them (the Docker VM Extension is one example), which may make their configuration easier; but the following commands work for all VM extensions.</span></span>

<span data-ttu-id="1cab5-125">Kunt u de **azure vm-extensielijst** opdracht voor het verkrijgen van informatie over de beschikbare uitbreidingen en gebruik de **–-json** optie om alle beschikbare informatie over een of meer uitbreidingen weer te geven.</span><span class="sxs-lookup"><span data-stu-id="1cab5-125">You can use the **azure vm extension list** command to obtain information about available extensions, and use the **–-json** option to display all available information about one or more extensions.</span></span> <span data-ttu-id="1cab5-126">Als u de naam van een uitbreiding niet gebruikt, retourneert de opdracht een JSON-beschrijving van alle beschikbare uitbreidingen.</span><span class="sxs-lookup"><span data-stu-id="1cab5-126">If you do not use an extension name, the command returns a JSON description of all available extensions.</span></span>

<span data-ttu-id="1cab5-127">Het volgende codevoorbeeld ziet u hoe u de gegevens voor de **IaaSDiagnostics** uitbreiding met de Azure CLI **azure vm-extensielijst** opdracht en het gebruik de **–-json**  optie voor volledige informatie te retourneren.</span><span class="sxs-lookup"><span data-stu-id="1cab5-127">For example, the following code example shows how to list the information for the **IaaSDiagnostics** extension using the Azure CLI **azure vm extension list** command and uses the **–-json** option to return complete information.</span></span>

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



### <a name="service-management-rest-apis"></a><span data-ttu-id="1cab5-128">REST API's voor Service Management</span><span class="sxs-lookup"><span data-stu-id="1cab5-128">Service Management REST APIs</span></span>
<span data-ttu-id="1cab5-129">U kunt de volgende REST-API's gebruiken om informatie over de beschikbare uitbreidingen te verkrijgen:</span><span class="sxs-lookup"><span data-stu-id="1cab5-129">You can use the following REST APIs to obtain information about available extensions:</span></span>

* <span data-ttu-id="1cab5-130">Voor exemplaren van de functie web- of werkrollen kunt u de [lijst met beschikbare uitbreidingen](https://msdn.microsoft.com/library/dn169559.aspx) bewerking.</span><span class="sxs-lookup"><span data-stu-id="1cab5-130">For instances of web roles or worker roles, you can use the [List Available Extensions](https://msdn.microsoft.com/library/dn169559.aspx) operation.</span></span> <span data-ttu-id="1cab5-131">Als u de versies van de beschikbare uitbreidingen weergeven, kunt u [lijst extensie versies](https://msdn.microsoft.com/library/dn495437.aspx).</span><span class="sxs-lookup"><span data-stu-id="1cab5-131">To list the versions of available extensions, you can use [List Extension Versions](https://msdn.microsoft.com/library/dn495437.aspx).</span></span>
* <span data-ttu-id="1cab5-132">Voor exemplaren van virtuele Machines, kunt u de [lijst Resource-uitbreidingen](https://msdn.microsoft.com/library/dn495441.aspx) bewerking.</span><span class="sxs-lookup"><span data-stu-id="1cab5-132">For instances of Virtual Machines, you can use the [List Resource Extensions](https://msdn.microsoft.com/library/dn495441.aspx) operation.</span></span> <span data-ttu-id="1cab5-133">Als u de versies van de beschikbare uitbreidingen weergeven, kunt u [lijst Resource-uitbreiding versies](https://msdn.microsoft.com/library/dn495440.aspx).</span><span class="sxs-lookup"><span data-stu-id="1cab5-133">To list the versions of available extensions, you can use [List Resource Extension Versions](https://msdn.microsoft.com/library/dn495440.aspx).</span></span>

## <a name="add-update-or-disable-extensions"></a><span data-ttu-id="1cab5-134">Toevoegen, bijwerken of extensies uitschakelen</span><span class="sxs-lookup"><span data-stu-id="1cab5-134">Add, Update, or Disable Extensions</span></span>
<span data-ttu-id="1cab5-135">Uitbreidingen kunnen worden toegevoegd wanneer een exemplaar is gemaakt of ze kunnen worden toegevoegd aan een actief exemplaar.</span><span class="sxs-lookup"><span data-stu-id="1cab5-135">Extensions can be added when an instance is created or they can be added to a running instance.</span></span> <span data-ttu-id="1cab5-136">Uitbreidingen kunnen worden bijgewerkt, uitgeschakeld of verwijderd.</span><span class="sxs-lookup"><span data-stu-id="1cab5-136">Extensions can be updated, disabled, or removed.</span></span> <span data-ttu-id="1cab5-137">U kunt deze acties uitvoeren met behulp van Azure PowerShell-cmdlets of met behulp van de Service Management REST-API-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="1cab5-137">You can perform these actions by using Azure PowerShell cmdlets or by using the Service Management REST API operations.</span></span> <span data-ttu-id="1cab5-138">Parameters zijn vereist voor het installeren en instellen van bepaalde extensies.</span><span class="sxs-lookup"><span data-stu-id="1cab5-138">Parameters are required to install and set up some extensions.</span></span> <span data-ttu-id="1cab5-139">Openbare en persoonlijke parameters worden ondersteund voor uitbreidingen.</span><span class="sxs-lookup"><span data-stu-id="1cab5-139">Public and private parameters are supported for extensions.</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="1cab5-140">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="1cab5-140">Azure PowerShell</span></span>
<span data-ttu-id="1cab5-141">Met Azure PowerShell-cmdlets, is de eenvoudigste manier toevoegen en bijwerken van de uitbreidingen.</span><span class="sxs-lookup"><span data-stu-id="1cab5-141">Using Azure PowerShell cmdlets is the easiest way to add and update extensions.</span></span> <span data-ttu-id="1cab5-142">Wanneer u de extensie-cmdlets gebruikt, geldt de configuratie van de uitbreiding voor de meeste voor u.</span><span class="sxs-lookup"><span data-stu-id="1cab5-142">When you use the extension cmdlets, most of the configuration of the extension is done for you.</span></span> <span data-ttu-id="1cab5-143">Soms moet u wellicht een uitbreiding via programmacode toevoegen.</span><span class="sxs-lookup"><span data-stu-id="1cab5-143">At times, you may need to programmatically add an extension.</span></span> <span data-ttu-id="1cab5-144">Wanneer u om dit te doen, moet u de configuratie van de extensie opgeven.</span><span class="sxs-lookup"><span data-stu-id="1cab5-144">When you need to do this, you must provide the configuration of the extension.</span></span>

<span data-ttu-id="1cab5-145">U kunt de volgende cmdlets gebruiken om te weten of een uitbreiding voor een configuratie van openbare en persoonlijke parameters vereist:</span><span class="sxs-lookup"><span data-stu-id="1cab5-145">You can use the following cmdlets to know whether an extension requires a configuration of public and private parameters:</span></span>

* <span data-ttu-id="1cab5-146">Voor exemplaren van de functie web- of werkrollen kunt u de **Get-AzureServiceAvailableExtension** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1cab5-146">For instances of web roles or worker roles, you can use the **Get-AzureServiceAvailableExtension** cmdlet.</span></span>
* <span data-ttu-id="1cab5-147">Voor exemplaren van virtuele Machines, kunt u de **Get-AzureVMAvailableExtension** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1cab5-147">For instances of Virtual Machines, you can use the **Get-AzureVMAvailableExtension** cmdlet.</span></span>

### <a name="service-management-rest-apis"></a><span data-ttu-id="1cab5-148">REST API's voor Service Management</span><span class="sxs-lookup"><span data-stu-id="1cab5-148">Service Management REST APIs</span></span>
<span data-ttu-id="1cab5-149">Wanneer u een lijst met beschikbare uitbreidingen ophalen met de REST-API's, krijgt u informatie over hoe de extensie is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="1cab5-149">When you retrieve a listing of available extensions by using the REST APIs, you receive information about how the extension is to be configured.</span></span> <span data-ttu-id="1cab5-150">De informatie die wordt geretourneerd mogelijk parameterinformatie dat wordt vertegenwoordigd door een openbare schema en een persoonlijke schema weergeven.</span><span class="sxs-lookup"><span data-stu-id="1cab5-150">The information that is returned might show parameter information represented by a public schema and private schema.</span></span> <span data-ttu-id="1cab5-151">Openbare parameterwaarden worden in query's over de exemplaren geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="1cab5-151">Public parameter values are returned in queries about the instances.</span></span> <span data-ttu-id="1cab5-152">Persoonlijke parameterwaarden worden niet geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="1cab5-152">Private parameter values are not returned.</span></span>

<span data-ttu-id="1cab5-153">U kunt de volgende REST-API's gebruiken om te weten of een uitbreiding voor een configuratie van openbare en persoonlijke parameters vereist:</span><span class="sxs-lookup"><span data-stu-id="1cab5-153">You can use the following REST APIs to know whether an extension requires a configuration of public and private parameters:</span></span>

* <span data-ttu-id="1cab5-154">Voor exemplaren van webrollen of werkrollen, de **PublicConfigurationSchema** en **PrivateConfigurationSchema** elementen bevatten de informatie in het antwoord van de [lijst die beschikbaar zijn Extensies](https://msdn.microsoft.com/library/dn169559.aspx) bewerking.</span><span class="sxs-lookup"><span data-stu-id="1cab5-154">For instances of web roles or worker roles, the **PublicConfigurationSchema** and **PrivateConfigurationSchema** elements contain the information in the response from the [List Available Extensions](https://msdn.microsoft.com/library/dn169559.aspx) operation.</span></span>
* <span data-ttu-id="1cab5-155">Voor exemplaren van virtuele Machines, de **PublicConfigurationSchema** en **PrivateConfigurationSchema** elementen bevatten de informatie in het antwoord van de [lijst Resource Extensies](https://msdn.microsoft.com/library/dn495441.aspx) bewerking.</span><span class="sxs-lookup"><span data-stu-id="1cab5-155">For instances of Virtual Machines, the **PublicConfigurationSchema** and **PrivateConfigurationSchema** elements contain the information in the response from the [List Resource Extensions](https://msdn.microsoft.com/library/dn495441.aspx) operation.</span></span>

> [!NOTE]
> <span data-ttu-id="1cab5-156">Extensies kunnen ook gebruiken voor configuraties die zijn gedefinieerd met JSON.</span><span class="sxs-lookup"><span data-stu-id="1cab5-156">Extensions can also use configurations that are defined with JSON.</span></span> <span data-ttu-id="1cab5-157">Wanneer deze typen uitbreidingen worden gebruikt, alleen de **SampleConfig** element wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="1cab5-157">When these types of extensions are used, only the **SampleConfig** element is used.</span></span>
> 
> 

