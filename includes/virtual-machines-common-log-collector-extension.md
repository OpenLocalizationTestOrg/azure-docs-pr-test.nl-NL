
<span data-ttu-id="85941-101">Oplossen van problemen met een Microsoft Azure cloudservice vereist Hallo-service-logboekbestanden op virtuele machines verzamelen als Hallo problemen optreden.</span><span class="sxs-lookup"><span data-stu-id="85941-101">Diagnosing issues with an Microsoft Azure cloud service requires collecting hello service’s log files on virtual machines as hello issues occur.</span></span> <span data-ttu-id="85941-102">U kunt Hallo AzureLogCollector uitbreiding op de aanvraag tooperfom eenmalige verzamelen van Logboeken van een of meer virtuele machines van Cloud Service (van webrollen en werkrollen) en overdracht Hallo verzamelde bestanden tooan Azure storage-account – zonder het extern aanmelden tooany Hallo virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="85941-102">You can use hello AzureLogCollector extension on-demand tooperfom one-time collection of logs from one or more Cloud Service VMs (from both web roles and worker roles) and transfer hello collected files tooan Azure storage account – all without remotely logging on tooany of hello VMs.</span></span>

> [!NOTE]
> <span data-ttu-id="85941-103">Beschrijvingen voor de meeste Hallo geregistreerd informatie kunnen worden gevonden op http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.asp.</span><span class="sxs-lookup"><span data-stu-id="85941-103">Descriptions for most of hello logged information can be found at http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.asp.</span></span>
> 
> 

<span data-ttu-id="85941-104">Er zijn twee modi van verzameling afhankelijk van Hallo typen bestanden toobe verzameld.</span><span class="sxs-lookup"><span data-stu-id="85941-104">There are two modes of collection dependent on hello types of files toobe collected.</span></span>

* <span data-ttu-id="85941-105">Azure Gast-Agent registreert alleen (GA).</span><span class="sxs-lookup"><span data-stu-id="85941-105">Azure Guest Agent Logs only (GA).</span></span> <span data-ttu-id="85941-106">Deze modus verzameling bevat alle Hallo logboeken gerelateerde tooAzure Gast agents en andere Azure-onderdelen.</span><span class="sxs-lookup"><span data-stu-id="85941-106">This collection mode includes all hello logs related tooAzure guest agents and other Azure components.</span></span>
* <span data-ttu-id="85941-107">Alle logboeken (volledig).</span><span class="sxs-lookup"><span data-stu-id="85941-107">All Logs (Full).</span></span> <span data-ttu-id="85941-108">Deze verzameling modus verzamelt alle bestanden in de modus van NH plus:</span><span class="sxs-lookup"><span data-stu-id="85941-108">This collection mode will collect all files in GA mode plus:</span></span>
  
  * <span data-ttu-id="85941-109">systeem- en gebeurtenislogboeken</span><span class="sxs-lookup"><span data-stu-id="85941-109">system and application event logs</span></span>
  * <span data-ttu-id="85941-110">HTTP-foutlogboeken</span><span class="sxs-lookup"><span data-stu-id="85941-110">HTTP error logs</span></span>
  * <span data-ttu-id="85941-111">IIS-logboeken</span><span class="sxs-lookup"><span data-stu-id="85941-111">IIS Logs</span></span>
  * <span data-ttu-id="85941-112">Setup-logboeken</span><span class="sxs-lookup"><span data-stu-id="85941-112">Setup logs</span></span>
  * <span data-ttu-id="85941-113">andere systeemlogboeken</span><span class="sxs-lookup"><span data-stu-id="85941-113">other system logs</span></span>

<span data-ttu-id="85941-114">In beide modi verzameling kunnen aanvullende gegevens verzamelingsmappen worden opgegeven met behulp van een verzameling van Hallo structuur te volgen:</span><span class="sxs-lookup"><span data-stu-id="85941-114">In both collection modes, additional data collection folders can be specified by using a collection of hello following structure:</span></span>

* <span data-ttu-id="85941-115">**Naam**: Hallo-naam van verzameling hello, die wordt gebruikt als Hallo-naam van de submap binnen Hallo zip-bestand toobe verzameld.</span><span class="sxs-lookup"><span data-stu-id="85941-115">**Name**: hello name of hello collection, which will be used as hello name of subfolder inside hello zip file toobe collected.</span></span>
* <span data-ttu-id="85941-116">**Locatie**: Hallo pad toohello map op Hallo virtuele machine waar bestand worden verzameld.</span><span class="sxs-lookup"><span data-stu-id="85941-116">**Location**: hello path toohello folder on hello virtual machine where file will be collected.</span></span>
* <span data-ttu-id="85941-117">**SearchPattern**: Hallo patroon van Hallo namen van bestanden toobe verzameld.</span><span class="sxs-lookup"><span data-stu-id="85941-117">**SearchPattern**: hello pattern of hello names of files toobe collected.</span></span> <span data-ttu-id="85941-118">Standaardwaarde is "*"</span><span class="sxs-lookup"><span data-stu-id="85941-118">Default is “*”</span></span>
* <span data-ttu-id="85941-119">**Recursieve**: als het Hallo-bestanden worden verzameld recursief onder Hallo-map.</span><span class="sxs-lookup"><span data-stu-id="85941-119">**Recursive**: if hello files will be collected recursively under hello folder.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="85941-120">Vereisten</span><span class="sxs-lookup"><span data-stu-id="85941-120">Prerequisites</span></span>
* <span data-ttu-id="85941-121">Moet u een opslagaccount toohave voor uitbreiding toosave gegenereerd zip-bestanden.</span><span class="sxs-lookup"><span data-stu-id="85941-121">You need toohave a storage account for extension toosave generated zip files.</span></span>
* <span data-ttu-id="85941-122">Moet u ervoor zorgen dat u van Azure PowerShell-Cmdlets V0.8.0 gebruikmaakt of hoger.</span><span class="sxs-lookup"><span data-stu-id="85941-122">You must make sure that you are using Azure PowerShell Cmdlets V0.8.0 or above.</span></span> <span data-ttu-id="85941-123">Zie voor meer informatie [Azure downloadt](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="85941-123">For more information, see [Azure Downloads](https://azure.microsoft.com/downloads/).</span></span>

## <a name="add-hello-extension"></a><span data-ttu-id="85941-124">Hallo-extensie toevoegen</span><span class="sxs-lookup"><span data-stu-id="85941-124">Add hello extension</span></span>
<span data-ttu-id="85941-125">U kunt [Microsoft Azure PowerShell](https://msdn.microsoft.com/library/dn495240.aspx) cmdlets of [Service REST-API's](https://msdn.microsoft.com/library/ee460799.aspx) tooadd hello AzureLogCollector-extensie.</span><span class="sxs-lookup"><span data-stu-id="85941-125">You can use [Microsoft Azure PowerShell](https://msdn.microsoft.com/library/dn495240.aspx) cmdlets or [Service Management REST APIs](https://msdn.microsoft.com/library/ee460799.aspx) tooadd hello AzureLogCollector extension.</span></span>

<span data-ttu-id="85941-126">Hallo voor Cloud-Services, Azure Powershell-cmdlet voor bestaande **Set AzureServiceExtension**, kunnen worden gebruikt tooenable Hallo-extensie voor rolinstanties Cloudservice.</span><span class="sxs-lookup"><span data-stu-id="85941-126">For Cloud Services, hello existing Azure Powershell cmdlet, **Set-AzureServiceExtension**, can be used tooenable hello extension on Cloud Service role instances.</span></span> <span data-ttu-id="85941-127">Elke keer dat deze extensie via deze cmdlet is ingeschakeld, wordt op Hallo geselecteerd rolexemplaren van de geselecteerde rollen logboekverzameling geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="85941-127">Every time this extension is enabled through this cmdlet, log collection is triggered on hello selected role instances of selected roles.</span></span>

<span data-ttu-id="85941-128">Hallo bestaande Azure Powershell-cmdlet voor virtuele Machines, **Set AzureVMExtension**, gebruikte tooenable Hallo-extensie op virtuele Machines kunnen worden.</span><span class="sxs-lookup"><span data-stu-id="85941-128">For Virtual Machines, hello existing Azure Powershell cmdlet, **Set-AzureVMExtension**, can be used tooenable hello extension on Virtual Machines.</span></span> <span data-ttu-id="85941-129">Elke keer dat deze uitbreiding is ingeschakeld via Hallo-cmdlets, wordt op elk exemplaar logboekverzameling geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="85941-129">Every time this extension is enabled through hello cmdlets, log collection is triggered on each instance.</span></span>

<span data-ttu-id="85941-130">Deze uitbreiding gebruikt intern, Hallo PublicConfiguration JSON-indeling en PrivateConfiguration.</span><span class="sxs-lookup"><span data-stu-id="85941-130">Internally, this extension uses hello JSON-based PublicConfiguration and PrivateConfiguration.</span></span> <span data-ttu-id="85941-131">Hallo volgt Hallo-indeling van een voorbeeld van JSON voor openbare en persoonlijke configuratie.</span><span class="sxs-lookup"><span data-stu-id="85941-131">hello following is hello layout of a sample JSON for public and private configuration.</span></span>

### <a name="publicconfiguration"></a><span data-ttu-id="85941-132">PublicConfiguration</span><span class="sxs-lookup"><span data-stu-id="85941-132">PublicConfiguration</span></span>
    {
        "Instances":  "*",
        "Mode":  "Full",
        "SasUri":  "SasUri tooyour storage account with sp=wl",
        "AdditionalData":
        [
          {
                  "Name":  "StorageData",
                  "Location":  "%roleroot%storage",
                  "SearchPattern":  "*.*",
                  "Recursive":  "true"
          },
          {
                "Name":  "CustomDataFolder2",
                "Location":  "c:\customFolder",
                "SearchPattern":  "*.log",
                "Recursive":  "false"
          },
        ]
    }

### <a name="privateconfiguration"></a><span data-ttu-id="85941-133">PrivateConfiguration</span><span class="sxs-lookup"><span data-stu-id="85941-133">PrivateConfiguration</span></span>
    {

    }

> [!NOTE]
> <span data-ttu-id="85941-134">Deze extensie niet hoeft **privateConfiguration**.</span><span class="sxs-lookup"><span data-stu-id="85941-134">This extension doesn’t need **privateConfiguration**.</span></span> <span data-ttu-id="85941-135">U kunt alleen een lege structuur bieden voor Hallo **– PrivateConfiguration** argument.</span><span class="sxs-lookup"><span data-stu-id="85941-135">You can just provide an empty structure for hello **–PrivateConfiguration** argument.</span></span>
> 
> 

<span data-ttu-id="85941-136">U kunt een van twee Hallo volgen na stappen tooadd hello AzureLogCollector tooone of meer exemplaren van een Cloudservice of virtuele Machine van de geselecteerde rollen, welke triggers Hallo verzamelingen op elke virtuele machine toorun en Hallo verzamelde bestanden tooAzure account verzenden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="85941-136">You can follow one of hello two following steps tooadd hello AzureLogCollector tooone or more instances of a Cloud Service or Virtual Machine of selected roles, which triggers hello collections on each VM toorun and send hello collected files tooAzure account specified.</span></span>

## <a name="adding-as-a-service-extension"></a><span data-ttu-id="85941-137">Als een extensie toe te voegen</span><span class="sxs-lookup"><span data-stu-id="85941-137">Adding as a Service Extension</span></span>
1. <span data-ttu-id="85941-138">Ga als volgt Hallo instructies tooconnect Azure PowerShell tooyour abonnement.</span><span class="sxs-lookup"><span data-stu-id="85941-138">Follow hello instructions tooconnect Azure PowerShell tooyour subscription.</span></span>
2. <span data-ttu-id="85941-139">Geef Hallo servicenaam, sleuf, rollen en functie exemplaren toowhich gewenste tooadd en Hallo AzureLogCollector-extensie inschakelen.</span><span class="sxs-lookup"><span data-stu-id="85941-139">Specify hello service name, slot, roles, and role instances toowhich you want tooadd and enable hello AzureLogCollector extension.</span></span>
   
        #Specify your cloud service name
        $ServiceName = 'extensiontest2'
   
        #Specify hello slot. 'Production' or 'Staging'
        $slot = 'Production'
   
        #Specified hello roles on which hello extension will be installed and enabled
        $roles = @("WorkerRole1","WebRole1")
   
        #Specify hello instances on which extension will be installed and enabled.  Use wildcard * for all instances
        $instances = @("*")
   
        #Specify hello collection mode, "Full" or "GA"
        $mode = "GA"
3. <span data-ttu-id="85941-140">Hallo aanvullende gegevensmap waarvoor bestanden worden verzameld op te geven (deze stap is optioneel).</span><span class="sxs-lookup"><span data-stu-id="85941-140">Specify hello additional data folder for which files will be collected (this step is optional).</span></span>
   
        #add one location
        $a1 = New-Object PSObject
   
        $a1 | Add-Member -MemberType NoteProperty -Name "Name" -Value "StorageData"
        $a1 | Add-Member -MemberType NoteProperty -Name "SearchPattern" -Value "*"
        $a1 | Add-Member -MemberType NoteProperty -Name "Location" -Value "%roleroot%storage"  #%roleroot% is normally E: or F: drive
        $a1 | Add-Member -MemberType NoteProperty -Name "Recursive" -Value "true"
   
        $AdditionalDataList+= $a1
              #more locations can be added....
   
   > [!NOTE]
   > <span data-ttu-id="85941-141">U kunt token `%roleroot%` toospecify Hallo rol basisstation omdat deze geen gebruik maakt van een vast station.</span><span class="sxs-lookup"><span data-stu-id="85941-141">You can use token `%roleroot%` toospecify hello role root drive since it doesn’t use a fixed drive.</span></span>
   > 
   > 
4. <span data-ttu-id="85941-142">Geef hello Azure storage-accountnaam en sleutels toowhich verzamelde bestanden worden geüpload.</span><span class="sxs-lookup"><span data-stu-id="85941-142">Provide hello Azure storage account name and key toowhich collected files will be uploaded.</span></span>
   
        $StorageAccountName = 'YourStorageAccountName'
        $StorageAccountKey  = ‘YouStorageAccountKey'
5. <span data-ttu-id="85941-143">Hallo SetAzureServiceLogCollector.ps1 (opgenomen achter Hallo Hallo artikel) als volgt tooenable hello AzureLogCollector uitbreiding-aanroep voor een Cloudservice.</span><span class="sxs-lookup"><span data-stu-id="85941-143">Call hello SetAzureServiceLogCollector.ps1 (included at hello end of hello article) as follows tooenable hello AzureLogCollector extension for a Cloud Service.</span></span> <span data-ttu-id="85941-144">Als het Hallo-uitvoering is voltooid, kunt u Hallo geüpload bestand onder vinden`https://YouareStorageAccountName.blob.core.windows.net/vmlogs`</span><span class="sxs-lookup"><span data-stu-id="85941-144">Once hello execution is completed, you can find hello uploaded file under `https://YouareStorageAccountName.blob.core.windows.net/vmlogs`</span></span>
   
        .\SetAzureServiceLogCollector.ps1 -ServiceName YourCloudServiceName  -Roles $roles  -Instances $instances –Mode $mode -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey -AdditionDataLocationList $AdditionalDataList

<span data-ttu-id="85941-145">Hallo volgt Hallo definitie van Hallo parameters doorgegeven toohello script.</span><span class="sxs-lookup"><span data-stu-id="85941-145">hello following is hello definition of hello parameters passed toohello script.</span></span> <span data-ttu-id="85941-146">(Deze wordt gekopieerd lager dan ook.)</span><span class="sxs-lookup"><span data-stu-id="85941-146">(This is copied below as well.)</span></span>

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
      [Parameter(Mandatory=$true)]
    [string]   $ServiceName,

    [Parameter(Mandatory=$false)]
    [string[]] $Roles ,

    [Parameter(Mandatory=$false)]
    [string[]] $Instances,

    [Parameter(Mandatory=$false)]
    [string]   $Slot = 'Production',

    [Parameter(Mandatory=$false)]
    [string]   $Mode = 'Full',

    [Parameter(Mandatory=$false)]
    [string]   $StorageAccountName,

    [Parameter(Mandatory=$false)]
    [string]   $StorageAccountKey,

    [Parameter(Mandatory=$false)]
    [PSObject[]] $AdditionDataLocationList = $null
    )

* <span data-ttu-id="85941-147">*ServiceName*: de naam van uw cloud-service.</span><span class="sxs-lookup"><span data-stu-id="85941-147">*ServiceName*: Your cloud service name.</span></span>
* <span data-ttu-id="85941-148">*Rollen*: een lijst met functies, zoals 'WebRole1' of 'WorkerRole1'.</span><span class="sxs-lookup"><span data-stu-id="85941-148">*Roles*: A list of roles, such as “WebRole1” or ”WorkerRole1”.</span></span>
* <span data-ttu-id="85941-149">*Exemplaren*: een lijst met namen Hallo rolinstanties gescheiden door komma--Hallo jokertekens tekenreeks gebruiken (' * ') voor alle rolexemplaren.</span><span class="sxs-lookup"><span data-stu-id="85941-149">*Instances*: A list of hello names of role instances separated by comma -- use hello wildcard string (“*”) for all role instances.</span></span>
* <span data-ttu-id="85941-150">*Sleuf*: naam van de site.</span><span class="sxs-lookup"><span data-stu-id="85941-150">*Slot*: Slot name.</span></span> <span data-ttu-id="85941-151">'Productie' of 'Fasering'.</span><span class="sxs-lookup"><span data-stu-id="85941-151">“Production” or “Staging”.</span></span>
* <span data-ttu-id="85941-152">*Modus*: Verzamelmodus.</span><span class="sxs-lookup"><span data-stu-id="85941-152">*Mode*: Collection mode.</span></span> <span data-ttu-id="85941-153">'Volledige' of 'GA'.</span><span class="sxs-lookup"><span data-stu-id="85941-153">“Full” or “GA”.</span></span>
* <span data-ttu-id="85941-154">*StorageAccountName*: naam van Azure storage-account voor het opslaan van gegevens verzameld.</span><span class="sxs-lookup"><span data-stu-id="85941-154">*StorageAccountName*: Name of Azure storage account for storing collected data.</span></span>
* <span data-ttu-id="85941-155">*StorageAccountKey*: naam van de Azure-opslagsleutel-account.</span><span class="sxs-lookup"><span data-stu-id="85941-155">*StorageAccountKey*: Name of Azure storage account key.</span></span>
* <span data-ttu-id="85941-156">*AdditionalDataLocationList*: een lijst met Hallo structuur te volgen:</span><span class="sxs-lookup"><span data-stu-id="85941-156">*AdditionalDataLocationList*: A list of hello following structure:</span></span>
  
      {
      String Name,
      String Location,
      String SearchPattern,
      Bool   Recursive
      }

## <a name="adding-as-a-vm-extension"></a><span data-ttu-id="85941-157">Toe te voegen als een VM-extensie</span><span class="sxs-lookup"><span data-stu-id="85941-157">Adding as a VM Extension</span></span>
<span data-ttu-id="85941-158">Ga als volgt Hallo instructies tooconnect Azure PowerShell tooyour abonnement.</span><span class="sxs-lookup"><span data-stu-id="85941-158">Follow hello instructions tooconnect Azure PowerShell tooyour subscription.</span></span>

1. <span data-ttu-id="85941-159">Hallo-servicenaam, VM en Hallo Verzamelmodus opgeven.</span><span class="sxs-lookup"><span data-stu-id="85941-159">Specify hello service name, VM, and hello collection mode.</span></span>
   
        #Specify your cloud service name
        $ServiceName = 'YourCloudServiceName'
   
        #Specify hello VM name
        $VMName = "'YourVMName'"
   
        #Specify hello collection mode, "Full" or "GA"
        $mode = "GA"
   
        Specify hello additional data folder for which files will be collected (this step is optional).
   
        #add one location
        $a1 = New-Object PSObject
   
        $a1 | Add-Member -MemberType NoteProperty -Name "Name" -Value "StorageData"
        $a1 | Add-Member -MemberType NoteProperty -Name "SearchPattern" -Value "*"
        $a1 | Add-Member -MemberType NoteProperty -Name "Location" -Value "%roleroot%storage"  #%roleroot% is normally E: or F: drive
        $a1 | Add-Member -MemberType NoteProperty -Name "Recursive" -Value "true"
   
        $AdditionalDataList+= $a1
              #more locations can be added....
2. <span data-ttu-id="85941-160">Geef hello Azure storage-accountnaam en sleutels toowhich verzamelde bestanden worden geüpload.</span><span class="sxs-lookup"><span data-stu-id="85941-160">Provide hello Azure storage account name and key toowhich collected files will be uploaded.</span></span>
   
        $StorageAccountName = 'YourStorageAccountName'
        $StorageAccountKey  = ‘YouStorageAccountKey'
3. <span data-ttu-id="85941-161">Hallo SetAzureVMLogCollector.ps1 (opgenomen achter Hallo Hallo artikel) als volgt tooenable hello AzureLogCollector uitbreiding-aanroep voor een Cloudservice.</span><span class="sxs-lookup"><span data-stu-id="85941-161">Call hello SetAzureVMLogCollector.ps1 (included at hello end of hello article) as follows tooenable hello AzureLogCollector extension for a Cloud Service.</span></span> <span data-ttu-id="85941-162">Als het Hallo-uitvoering is voltooid, kunt u Hallo geüpload bestand onder https://YouareStorageAccountName.blob.core.windows.net/vmlogs vinden</span><span class="sxs-lookup"><span data-stu-id="85941-162">Once hello execution is completed, you can find hello uploaded file under https://YouareStorageAccountName.blob.core.windows.net/vmlogs</span></span>

<span data-ttu-id="85941-163">Hallo volgt Hallo definitie van Hallo parameters doorgegeven toohello script.</span><span class="sxs-lookup"><span data-stu-id="85941-163">hello following is hello definition of hello parameters passed toohello script.</span></span> <span data-ttu-id="85941-164">(Deze wordt gekopieerd lager dan ook.)</span><span class="sxs-lookup"><span data-stu-id="85941-164">(This is copied below as well.)</span></span>

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
        [Parameter(Mandatory=$true)]
      [string]   $ServiceName,

      [Parameter(Mandatory=$false)]
      [string] $VMName ,

        [Parameter(Mandatory=$false)]
      [string]   $Mode = 'Full',

      [Parameter(Mandatory=$false)]
      [string]   $StorageAccountName,

      [Parameter(Mandatory=$false)]
      [string]   $StorageAccountKey,

      [Parameter(Mandatory=$false)]
      [PSObject[]] $AdditionDataLocationList = $null
      )

* <span data-ttu-id="85941-165">Servicenaam: Cloudservicenaam van uw service.</span><span class="sxs-lookup"><span data-stu-id="85941-165">ServiceName: Your cloud service name.</span></span>
* <span data-ttu-id="85941-166">Naam van de VMName Hallo Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="85941-166">VMName hello name of hello VM.</span></span>
* <span data-ttu-id="85941-167">Modus: Modus voor het verzamelen.</span><span class="sxs-lookup"><span data-stu-id="85941-167">Mode: Collection mode.</span></span> <span data-ttu-id="85941-168">'Volledige' of 'GA'.</span><span class="sxs-lookup"><span data-stu-id="85941-168">“Full” or “GA”.</span></span>
* <span data-ttu-id="85941-169">StorageAccountName: De naam van Azure storage-account voor het opslaan van verzamelde gegevens.</span><span class="sxs-lookup"><span data-stu-id="85941-169">StorageAccountName: Name of Azure storage account for storing collected data.</span></span>
* <span data-ttu-id="85941-170">StorageAccountKey: De naam van de sleutel van de Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="85941-170">StorageAccountKey: Name of Azure storage account key.</span></span>
* <span data-ttu-id="85941-171">AdditionalDataLocationList: Een lijst met Hallo structuur te volgen:</span><span class="sxs-lookup"><span data-stu-id="85941-171">AdditionalDataLocationList: A list of hello following structure:</span></span>

```
      {
        String Name,
        String Location,
        String SearchPattern,
        Bool   Recursive
      }
```

## <a name="extention-powershell-script-files"></a><span data-ttu-id="85941-172">Extensie PowerShell-Script bestanden</span><span class="sxs-lookup"><span data-stu-id="85941-172">Extention PowerShell Script files</span></span>
<span data-ttu-id="85941-173">SetAzureServiceLogCollector.ps1</span><span class="sxs-lookup"><span data-stu-id="85941-173">SetAzureServiceLogCollector.ps1</span></span>

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
                  [Parameter(Mandatory=$true)]
                  [string]   $ServiceName,

                  [Parameter(Mandatory=$false)]
                  [string[]] $Roles ,

                  [Parameter(Mandatory=$false)]
                  [string[]] $Instances = '*',

                  [Parameter(Mandatory=$false)]
                  [string]   $Slot = 'Production',

                  [Parameter(Mandatory=$false)]
                  [string]   $Mode = 'Full',

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountName,

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountKey,

                  [Parameter(Mandatory=$false)]
                  [PSObject[]] $AdditionDataLocationList = $null
            )

    $publicConfig = New-Object PSObject

    if ($Instances -ne $null -and $Instances.Count -gt 0)  #Instances should be seperated by ,
    {
        $instanceText = $Instances[0]
        for ($i = 1;$i -lt $Instances.Count;$i++)
        {
              $instanceText = $instanceText+ "," + $Instances[$i]
          }
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Instances" -Value $instanceText
    }
    else  #For all instances if not specified.  hello value should be a space or *
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Instances" -Value " "
    }

    if ($Mode -ne $null )
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value $Mode
    }
    else
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value "Full"
    }

    #
    #we need tooget hello Sasuri from StorageAccount and containers
    #
    $context = New-AzureStorageContext -Protocol https -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

    $ContainerName = "azurelogcollectordata"
    $existingContainer = Get-AzureStorageContainer -Context $context |  Where-Object { $_.Name -like $ContainerName}
    if ($existingContainer -eq $null)
    {
        "Container ($ContainerName) doesn't exist. Creating it now.."
        New-AzureStorageContainer -Context $context -Name $ContainerName -Permission off
    }

    $ExpiryTime =  [DateTime]::Now.AddMinutes(120).ToString("o")
    $SasUri = New-AzureStorageContainerSASToken -ExpiryTime $ExpiryTime -FullUri -Name $ContainerName -Permission rwl -Context $context
    $publicConfig | Add-Member -MemberType NoteProperty -Name "SasUri" -Value $SasUri

    #
    #Add AdditionalData toocollect data from additional folders
    #
    if ($AdditionDataLocationList -ne $null )
    {
      $publicConfig | Add-Member -MemberType NoteProperty -Name "AdditionalData" -Value $AdditionDataLocationList
    }

    #
    # Convert it tooJSON format
    #
    $publicConfigJSON = $publicConfig | ConvertTo-Json
    "publicConfig is:  $publicConfigJSON"

    #we just provide a empty privateConfig object
    $privateconfig = "{
    }"

    if ($Roles -ne $null)
    {
          Set-AzureServiceExtension -Service $ServiceName -Slot $Slot -Role $Roles -ExtensionName 'AzureLogCollector' -ProviderNamespace Microsoft.WindowsAzure.Compute -PublicConfiguration $publicConfigJSON -PrivateConfiguration $privateconfig -Version 1.0 -Verbose
    }
    else
    {
          Set-AzureServiceExtension -Service $ServiceName -Slot $Slot  -ExtensionName 'AzureLogCollector' -ProviderNamespace Microsoft.WindowsAzure.Compute -PublicConfiguration $publicConfigJSON -PrivateConfiguration $privateconfig -Version 1.0 -Verbose
    }

    #
    #This is an optional step: generate a sasUri toohello container so it can be shared with other people if nened
    #
    $SasExpireTime = [DateTime]::Now.AddMinutes(120).ToString("o")
    $SasUri = New-AzureStorageContainerSASToken -ExpiryTime $ExpiryTime -FullUri -Name $ContainerName -Permission rl -Context $context
    $SasUri = $SasUri + "&restype=container&comp=list"
    Write-Output "hello container for uploaded file can be accessed using this link:`r`n$sasuri"


<span data-ttu-id="85941-174">SetAzureVMLogCollector.ps1</span><span class="sxs-lookup"><span data-stu-id="85941-174">SetAzureVMLogCollector.ps1</span></span>

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
                  [Parameter(Mandatory=$true)]
                  [string]   $ServiceName,

                  [Parameter(Mandatory=$false)]
                  [string] $VMName ,

                  [Parameter(Mandatory=$false)]
                  [string]   $Mode = 'Full',

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountName,

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountKey,

                  [Parameter(Mandatory=$false)]
                  [PSObject[]] $AdditionDataLocationList = $null
            )

    $publicConfig = New-Object PSObject
    $publicConfig | Add-Member -MemberType NoteProperty -Name "Instances" -Value "*"

    if ($Mode -ne $null )
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value $Mode
    }
    else
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value "Full"
    }

    #
    #we need tooget hello Sasuri from StorageAccount and containers
    #
    $context = New-AzureStorageContext -Protocol https -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

    $ContainerName = "azurelogcollectordata"
    $existingContainer = Get-AzureStorageContainer -Context $context |  Where-Object { $_.Name -like $ContainerName}
    if ($existingContainer -eq $null)
    {
        "Container ($ContainerName) doesn't exist. Creating it now.."
        New-AzureStorageContainer -Context $context -Name $ContainerName -Permission off
    }

    $ExpiryTime =  [DateTime]::Now.AddMinutes(90).ToString("o")
    $SasUri = New-AzureStorageContainerSASToken -ExpiryTime $ExpiryTime -FullUri -Name $ContainerName -Permission rwl -Context $context
    $publicConfig | Add-Member -MemberType NoteProperty -Name "SasUri" -Value $SasUri

    #
    #Add AdditionalData toocollect data from additional folders
    #
    if ($AdditionDataLocationList -ne $null )
    {
      $publicConfig | Add-Member -MemberType NoteProperty -Name "AdditionalData" -Value $AdditionDataLocationList
    }

    #
    # Convert it tooJSON format
    #
    $publicConfigJSON = $publicConfig | ConvertTo-Json

    Write-Output "PublicConfigurtion is: \r\n$publicConfigJSON"

    #
    #we just provide a empty privateConfig object
    #
    $privateconfig = "{
    }"

    if ($VMName -ne $null )
    {
          $VM = Get-AzureVM -ServiceName $ServiceName -Name $VMName
          $VM.VM.OSVirtualHardDisk.OS

          if ($VM.VM.OSVirtualHardDisk.OS -like '*Windows*')
          {
                Set-AzureVMExtension -VM $VM -ExtensionName "AzureLogCollector" -Publisher Microsoft.WindowsAzure.Compute -PublicConfiguration $publicConfigJSON -PrivateConfiguration $privateconfig -Version 1.* | Update-AzureVM -Verbose

                #
                #We will check hello VM status toofind if operation by extension has been completed or not. hello completion of hello operation,either succeed or fail, can be indicated by
                #hello presence of SubstatusList field.
                #
                $Completed = $false
                while ($Completed -ne $true)
                {
                        $VM = Get-AzureVM -ServiceName $ServiceName -Name $VMName
                        $status = $VM.ResourceExtensionStatusList | Where-Object {$_.HandlerName -eq "Microsoft.WindowsAzure.Compute.AzureLogCollector"}

                        if ( ($status.Code -ne 0) -and ($status.Status -like '*error*'))
                        {
                            Write-Output "Error status is returned: $($Status.ExtensionSettingStatus.FormattedMessage.Message)."
                              $Completed = $true
                        }
                        elseif (($status.ExtensionSettingStatus.SubstatusList -eq $null -or $status.ExtensionSettingStatus.SubstatusList.Count -lt 1))
                        {
                              $Completed = $false
                              Write-Output "Waiting for operation toocomplete..."
                        }
                        else
                        {
                              $Completed = $true
                              Write-Output "Operation completed."

                        $UploadedFileUri = $Status.ExtensionSettingStatus.SubStatusList[0].FormattedMessage.Message
                              $blob = New-Object Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob($UploadedFileUri)

                      #
                            # This is an optional step:  For easier access toohello file, we can generate a read-only SasUri directly toohello file
                              #
                              $ExpiryTimeRead =  [DateTime]::Now.AddMinutes(120).ToString("o")
                              $ReadSasUri = New-AzureStorageBlobSASToken -ExpiryTime $ExpiryTimeRead  -FullUri  -Blob  $blob.name -Container $blob.Container.Name -Permission r -Context $context

                            Write-Output "hello uploaded file can be accessed using this link: $ReadSasUri"

                              #
                              #This is an optional step:  Remove hello extension after we are done
                              #
                              Get-AzureVM -ServiceName $ServiceName -Name $VMName | Set-AzureVMExtension -Publisher Microsoft.WindowsAzure.Compute -ExtensionName "AzureLogCollector" -Version 1.* -Uninstall | Update-AzureVM -Verbose

                        }
                        Start-Sleep -s 5
                }
          }
          else
          {
              Write-Output "VM OS Type is not Windows, hello extension cannot be enabled"
          }

    }
    else
    {
      Write-Output "VM name is not specified, hello extension cannot be enabled"
    }

## <a name="next-steps"></a><span data-ttu-id="85941-175">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="85941-175">Next Steps</span></span>
<span data-ttu-id="85941-176">U kunt nu controleren of uw logboeken kopiëren van een zeer eenvoudige locatie.</span><span class="sxs-lookup"><span data-stu-id="85941-176">Now you can examine or copy your logs from one very simple location.</span></span>

