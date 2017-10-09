
Oplossen van problemen met een Microsoft Azure cloudservice vereist Hallo-service-logboekbestanden op virtuele machines verzamelen als Hallo problemen optreden. U kunt Hallo AzureLogCollector uitbreiding op de aanvraag tooperfom eenmalige verzamelen van Logboeken van een of meer virtuele machines van Cloud Service (van webrollen en werkrollen) en overdracht Hallo verzamelde bestanden tooan Azure storage-account – zonder het extern aanmelden tooany Hallo virtuele machines.

> [!NOTE]
> Beschrijvingen voor de meeste Hallo geregistreerd informatie kunnen worden gevonden op http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.asp.
> 
> 

Er zijn twee modi van verzameling afhankelijk van Hallo typen bestanden toobe verzameld.

* Azure Gast-Agent registreert alleen (GA). Deze modus verzameling bevat alle Hallo logboeken gerelateerde tooAzure Gast agents en andere Azure-onderdelen.
* Alle logboeken (volledig). Deze verzameling modus verzamelt alle bestanden in de modus van NH plus:
  
  * systeem- en gebeurtenislogboeken
  * HTTP-foutlogboeken
  * IIS-logboeken
  * Setup-logboeken
  * andere systeemlogboeken

In beide modi verzameling kunnen aanvullende gegevens verzamelingsmappen worden opgegeven met behulp van een verzameling van Hallo structuur te volgen:

* **Naam**: Hallo-naam van verzameling hello, die wordt gebruikt als Hallo-naam van de submap binnen Hallo zip-bestand toobe verzameld.
* **Locatie**: Hallo pad toohello map op Hallo virtuele machine waar bestand worden verzameld.
* **SearchPattern**: Hallo patroon van Hallo namen van bestanden toobe verzameld. Standaardwaarde is "*"
* **Recursieve**: als het Hallo-bestanden worden verzameld recursief onder Hallo-map.

## <a name="prerequisites"></a>Vereisten
* Moet u een opslagaccount toohave voor uitbreiding toosave gegenereerd zip-bestanden.
* Moet u ervoor zorgen dat u van Azure PowerShell-Cmdlets V0.8.0 gebruikmaakt of hoger. Zie voor meer informatie [Azure downloadt](https://azure.microsoft.com/downloads/).

## <a name="add-hello-extension"></a>Hallo-extensie toevoegen
U kunt [Microsoft Azure PowerShell](https://msdn.microsoft.com/library/dn495240.aspx) cmdlets of [Service REST-API's](https://msdn.microsoft.com/library/ee460799.aspx) tooadd hello AzureLogCollector-extensie.

Hallo voor Cloud-Services, Azure Powershell-cmdlet voor bestaande **Set AzureServiceExtension**, kunnen worden gebruikt tooenable Hallo-extensie voor rolinstanties Cloudservice. Elke keer dat deze extensie via deze cmdlet is ingeschakeld, wordt op Hallo geselecteerd rolexemplaren van de geselecteerde rollen logboekverzameling geactiveerd.

Hallo bestaande Azure Powershell-cmdlet voor virtuele Machines, **Set AzureVMExtension**, gebruikte tooenable Hallo-extensie op virtuele Machines kunnen worden. Elke keer dat deze uitbreiding is ingeschakeld via Hallo-cmdlets, wordt op elk exemplaar logboekverzameling geactiveerd.

Deze uitbreiding gebruikt intern, Hallo PublicConfiguration JSON-indeling en PrivateConfiguration. Hallo volgt Hallo-indeling van een voorbeeld van JSON voor openbare en persoonlijke configuratie.

### <a name="publicconfiguration"></a>PublicConfiguration
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

### <a name="privateconfiguration"></a>PrivateConfiguration
    {

    }

> [!NOTE]
> Deze extensie niet hoeft **privateConfiguration**. U kunt alleen een lege structuur bieden voor Hallo **– PrivateConfiguration** argument.
> 
> 

U kunt een van twee Hallo volgen na stappen tooadd hello AzureLogCollector tooone of meer exemplaren van een Cloudservice of virtuele Machine van de geselecteerde rollen, welke triggers Hallo verzamelingen op elke virtuele machine toorun en Hallo verzamelde bestanden tooAzure account verzenden opgegeven.

## <a name="adding-as-a-service-extension"></a>Als een extensie toe te voegen
1. Ga als volgt Hallo instructies tooconnect Azure PowerShell tooyour abonnement.
2. Geef Hallo servicenaam, sleuf, rollen en functie exemplaren toowhich gewenste tooadd en Hallo AzureLogCollector-extensie inschakelen.
   
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
3. Hallo aanvullende gegevensmap waarvoor bestanden worden verzameld op te geven (deze stap is optioneel).
   
        #add one location
        $a1 = New-Object PSObject
   
        $a1 | Add-Member -MemberType NoteProperty -Name "Name" -Value "StorageData"
        $a1 | Add-Member -MemberType NoteProperty -Name "SearchPattern" -Value "*"
        $a1 | Add-Member -MemberType NoteProperty -Name "Location" -Value "%roleroot%storage"  #%roleroot% is normally E: or F: drive
        $a1 | Add-Member -MemberType NoteProperty -Name "Recursive" -Value "true"
   
        $AdditionalDataList+= $a1
              #more locations can be added....
   
   > [!NOTE]
   > U kunt token `%roleroot%` toospecify Hallo rol basisstation omdat deze geen gebruik maakt van een vast station.
   > 
   > 
4. Geef hello Azure storage-accountnaam en sleutels toowhich verzamelde bestanden worden geüpload.
   
        $StorageAccountName = 'YourStorageAccountName'
        $StorageAccountKey  = ‘YouStorageAccountKey'
5. Hallo SetAzureServiceLogCollector.ps1 (opgenomen achter Hallo Hallo artikel) als volgt tooenable hello AzureLogCollector uitbreiding-aanroep voor een Cloudservice. Als het Hallo-uitvoering is voltooid, kunt u Hallo geüpload bestand onder vinden`https://YouareStorageAccountName.blob.core.windows.net/vmlogs`
   
        .\SetAzureServiceLogCollector.ps1 -ServiceName YourCloudServiceName  -Roles $roles  -Instances $instances –Mode $mode -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey -AdditionDataLocationList $AdditionalDataList

Hallo volgt Hallo definitie van Hallo parameters doorgegeven toohello script. (Deze wordt gekopieerd lager dan ook.)

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

* *ServiceName*: de naam van uw cloud-service.
* *Rollen*: een lijst met functies, zoals 'WebRole1' of 'WorkerRole1'.
* *Exemplaren*: een lijst met namen Hallo rolinstanties gescheiden door komma--Hallo jokertekens tekenreeks gebruiken (' * ') voor alle rolexemplaren.
* *Sleuf*: naam van de site. 'Productie' of 'Fasering'.
* *Modus*: Verzamelmodus. 'Volledige' of 'GA'.
* *StorageAccountName*: naam van Azure storage-account voor het opslaan van gegevens verzameld.
* *StorageAccountKey*: naam van de Azure-opslagsleutel-account.
* *AdditionalDataLocationList*: een lijst met Hallo structuur te volgen:
  
      {
      String Name,
      String Location,
      String SearchPattern,
      Bool   Recursive
      }

## <a name="adding-as-a-vm-extension"></a>Toe te voegen als een VM-extensie
Ga als volgt Hallo instructies tooconnect Azure PowerShell tooyour abonnement.

1. Hallo-servicenaam, VM en Hallo Verzamelmodus opgeven.
   
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
2. Geef hello Azure storage-accountnaam en sleutels toowhich verzamelde bestanden worden geüpload.
   
        $StorageAccountName = 'YourStorageAccountName'
        $StorageAccountKey  = ‘YouStorageAccountKey'
3. Hallo SetAzureVMLogCollector.ps1 (opgenomen achter Hallo Hallo artikel) als volgt tooenable hello AzureLogCollector uitbreiding-aanroep voor een Cloudservice. Als het Hallo-uitvoering is voltooid, kunt u Hallo geüpload bestand onder https://YouareStorageAccountName.blob.core.windows.net/vmlogs vinden

Hallo volgt Hallo definitie van Hallo parameters doorgegeven toohello script. (Deze wordt gekopieerd lager dan ook.)

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

* Servicenaam: Cloudservicenaam van uw service.
* Naam van de VMName Hallo Hallo VM.
* Modus: Modus voor het verzamelen. 'Volledige' of 'GA'.
* StorageAccountName: De naam van Azure storage-account voor het opslaan van verzamelde gegevens.
* StorageAccountKey: De naam van de sleutel van de Azure storage-account.
* AdditionalDataLocationList: Een lijst met Hallo structuur te volgen:

```
      {
        String Name,
        String Location,
        String SearchPattern,
        Bool   Recursive
      }
```

## <a name="extention-powershell-script-files"></a>Extensie PowerShell-Script bestanden
SetAzureServiceLogCollector.ps1

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


SetAzureVMLogCollector.ps1

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

## <a name="next-steps"></a>Volgende stappen
U kunt nu controleren of uw logboeken kopiëren van een zeer eenvoudige locatie.

