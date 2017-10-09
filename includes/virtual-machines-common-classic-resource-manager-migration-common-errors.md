# <a name="common-errors-during-classic-tooazure-resource-manager-migration"></a>Veelvoorkomende fouten tijdens klassieke tooAzure Resource Manager-migratie
Dit artikel catalogussen Hallo meest voorkomende fouten en oplossingen beschreven tijdens de migratie Hallo van IaaS-middelen van Azure classic deployment model toohello Azure Resource Manager-stack.

## <a name="list-of-errors"></a>Lijst met fouten
| Fouttekenreeks | Oplossing |
| --- | --- |
| Interne serverfout |In sommige gevallen is dit een tijdelijke fout die bij een nieuwe poging is verdwenen. Als u toopersist doorgaat, [Neem contact op met de ondersteuning van Azure](../articles/azure-supportability/how-to-create-azure-support-request.md) als nodig platform logboeken moeten worden onderzocht. <br><br> **Opmerking:** zodra Hallo incident wordt bijgehouden door het Hallo-ondersteuningsteam, neem Probeer niet alle zelf risicobeperking omdat dit mogelijk ongewenste gevolgen voor uw omgeving. |
| Migratie wordt niet ondersteund voor de implementatie {naam-implementatie} in HostedService {naam-gehoste-service} omdat dit een PaaS-implementatie (web-/werkrol) is. |Dit gebeurt wanneer een implementatie een web-/werkrol bevat. Omdat de migratie wordt alleen ondersteund voor virtuele Machines, verwijder Hallo web/worker-rol van Hallo-implementatie en probeer het opnieuw. |
| Sjabloonimplementatie {sjabloonnaam} is mislukt. CorrelationId = {guid} |In Hallo back-end van de migratieservice gebruiken we Azure Resource Manager sjablonen toocreate resources in hello Azure Resource Manager-stack. Aangezien sjablonen idempotent, opnieuw meestal veilig Hallo migratie bewerking tooget voorbij deze fout. Als deze fout zich blijft voordoen toopersist [Neem contact op met de ondersteuning van Azure](../articles/azure-supportability/how-to-create-azure-support-request.md) en geef ze Hallo CorrelationId. <br><br> **Opmerking:** zodra Hallo incident wordt bijgehouden door het Hallo-ondersteuningsteam, neem Probeer niet alle zelf risicobeperking omdat dit mogelijk ongewenste gevolgen voor uw omgeving. |
| Hallo virtuele netwerk {virtuele-netwerk-name} bestaat niet. |Dit kan gebeuren als u Hallo virtueel netwerk hebt gemaakt in Hallo nieuwe Azure portal. Hallo werkelijke virtuele-netwerknaam volgt Hallo patroon ' groep * <VNET name>' |
| VM {vm-naam} in HostedService {naam-gehoste-service} bevat de extensie {naam-extensie}. Deze wordt niet ondersteund in Azure Resource Manager. Het verdient aanbeveling toouninstall op Hallo VM voordat u doorgaat met de migratie. |XML-extensies, zoals BGInfo 1.* worden niet ondersteund in Azure Resource Manager. Daarom kunnen deze extensies niet worden gemigreerd. Deze uitbreidingen zijn links geïnstalleerd op Hallo virtuele machine, worden automatisch verwijderd voordat het Hallo-migratie is voltooid. |
| VM {vm-naam} in HostedService {naam-gehoste-service} bevat de extensie VMSnapshot/VMSnapshotLinux. Deze wordt momenteel niet ondersteund voor migratie. Deze verwijderen vanuit Hallo VM en voeg terug met behulp van Azure Resource Manager nadat Hallo migratie voltooid is |Dit is Hallo scenario waarbij Hallo virtuele machine is geconfigureerd voor Azure Backup. Omdat dit momenteel een niet-ondersteund scenario is, volg Hallo tijdelijke oplossing op https://aka.ms/vmbackupmigration |
| Virtuele machine {vm-naam} in HostedService {gehoste-service-name} bevat de extensie {Extensienaam} met de Status van Hallo VM niet wordt gerapporteerd. Daarom kan deze virtuele machine niet worden gemigreerd. Zorg ervoor dat Hallo status van extensie wordt gerapporteerd of Hallo uitbreiding verwijderen uit Hallo VM en migratie nogmaals uitvoeren. <br><br> VM {vm-naam} in HostedService {naam-gehoste-service} bevat de extensie {naam-extensie}. Deze rapporteert de volgende handlerstatus: {handlerstatus}. Daarom kan niet Hallo VM worden gemigreerd. Zorg ervoor dat Hallo handler Extensiestatus gemeld {handler-status} of deze verwijderen vanuit Hallo VM en migratie nogmaals uitvoeren. <br><br> VM-Agent voor de virtuele machine {vm-naam} in HostedService {gehoste-service-name} is rapportage Hallo algehele agentstatus niet gereed. Daarom kan Hallo VM niet worden gemigreerd, als er een uitbreiding van de machine kan worden gemigreerd. Zorg ervoor dat Hallo VM-Agent rapporteert algemene agentstatus gereed. Raadpleeg toohttps://aka.ms/classiciaasmigrationfaqs. |Azure gastagent & VM-extensies moet uitgaande internet toegang toohello VM storage account toopopulate hun status. Algemene oorzaken van de statusfout zijn <li> een Netwerkbeveiligingsgroep die toohello uitgaande toegang blokkeert internet <li> Als Hallo VNET on-premises DNS-servers en DNS-verbinding verbroken is <br><br> Als u een niet-ondersteunde status toosee doorgaat, kunt u deze kunt verwijderen Hallo extensies tooskip deze controle en verder gaan met de migratie. |
| Migratie wordt niet ondersteund voor de implementatie {naam-implementatie} in HostedService {naam-gehoste-service} omdat deze meerdere beschikbaarheidssets heeft. |Op dit moment kunnen alleen gehoste services die maximaal één beschikbaarheidsset hebben worden gemigreerd. toowork om dit probleem Verplaats Hallo extra beschikbaarheidssets en virtuele machines in deze tooa verschillende sets van beschikbaarheid van de gehoste service. |
| Migratie wordt niet ondersteund voor implementatie {implementatienaam} in HostedService {gehoste-service-naam omdat er virtuele machines die geen deel uitmaken van de Beschikbaarheidsset Hallo Hoewel Hallo HostedService een bevat. |Hallo-oplossing voor dit scenario is tooeither verplaatsen alle Hallo virtuele machines in een enkel beschikbaarheid instellen of verwijderen van alle virtuele machines van Hallo in Hallo gehoste service beschikbaarheidsset. |
| Storage-account/HostedService/virtuele netwerk {virtuele-netwerk-name} is in Hallo-proces wordt gemigreerd en kan daarom niet worden gewijzigd |Deze fout treedt op wanneer de migratiebewerking 'Voorbereiden' Hallo op Hallo resource is voltooid en een bewerking die u een wijziging toohello resource maakt wordt geactiveerd. Vanwege Hallo vergrendeling op Hallo management vlak na "Voorbereiden"-bewerking, alle wijzigingen toohello bronnen worden geblokkeerd. toounlock hello management vlak, kunt u Hallo "Doorvoeren" migratie bewerking toocomplete migratie uitvoeren of Hallo "Afbreken" migratie bewerking tooroll terug Hallo "Voorbereiden"-bewerking. |
| Migratie voor HostedService {naam-gehoste-service} is niet toegestaan omdat de VM {vm-naam} in de service de status: RoleStateUnknown heeft. Migratie is toegestaan wanneer de VM bevindt zich in een van de volgende Hallo Hallo geeft alleen - actief, gestopt, gestopt toewijzing ongedaan gemaakt. |Hallo VM mogelijk worden momenteel uitgevoerd via een statusovergang, meestal tijdens de update-bewerking op Hallo HostedService zoals opnieuw worden opgestart gebeurt, enzovoort-appuitbreiding is geïnstalleerd. Het wordt aanbevolen voor Hallo update bewerking toocomplete op Hallo HostedService voordat u de migratie. |
| Implementatie {implementatienaam} in HostedService {gehoste-service-name} bevat een virtuele machine {vm-naam} met gegevensschijf {gegevens schijf name} waarvan bytes van fysieke blob grootte {size-of-the-vhd-blob-backing-the-data-disk} komt niet overeen met de Hallo VM gegevensschijf logische grootte { Size-of-the-Data-Disk-specified-in-the-VM-API} bytes. Migratie wordt voortgezet zonder een grootte voor de gegevensschijf Hallo voor hello Azure Resource Manager VM opgeven. | Deze fout treedt op als VHD-blob Hallo formaat hebt gewijzigd zonder het Hallo-grootte in Hallo VM API model bijwerken. Gedetailleerde stappen worden [hieronder](#vm-with-data-disk-whose-physical-blob-size-bytes-does-not-match-the-vm-data-disk-logical-size-bytes) beschreven.|
| Er is een opslaguitzondering opgetreden tijdens het valideren van de gegevensschijf {naam-gegevensschijf} met de medialink {Uri-gegevensschijf} voor de virtuele machine {VM-naam} in de cloudservice {naam-cloudservice}. Zorg ervoor dat Hallo VHD media-koppeling is toegankelijk voor deze virtuele machine | Deze fout kan optreden als Hallo schijven Hallo virtuele machine is verwijderd of zijn niet meer worden toegankelijk. Zorg ervoor dat Hallo schijven voor Hallo VM bestaat.|
| De VM {vm-naam} in HostedService {naam-cloudservice} bevat een schijf met MediaLink {vhd-uri} met blobnaam {vhd-blobnaam} die niet wordt ondersteund in Azure Resource Manager. | Deze fout treedt op wanneer het Hallo-naam van Hallo blob heeft een '/' wordt momenteel niet ondersteund in Compute Resource Provider erin. |
| Migratie is niet toegestaan voor de implementatie {implementatienaam} in HostedService {cloud-service-name}, omdat dit geen Hallo regionaal bereik. Raadpleeg toohttp://aka.ms/regionalscope voor het verplaatsen van deze implementatie tooregional scope. | In 2014, Azure aangekondigd dat netwerkresources worden verplaatst van een cluster bereik tooregional bereik. Zie [http://aka.ms/regionalscope] voor meer informatie (http://aka.ms/regionalscope). Deze fout treedt op wanneer het Hallo-implementatie wordt gemigreerd een updatebewerking, die automatisch wordt verplaatst tooa regionaal bereik niet heeft. Beste oplossing is tooeither een eindpunt tooa VM toevoegen of een data toohello VM schijf en probeer vervolgens de migratie. <br> Zie [hoe tooset eindpunten op een klassieke Windows-virtuele machine in Azure](../articles/virtual-machines/windows/classic/setup-endpoints.md#create-an-endpoint) of [gegevens schijf tooa virtuele Windows-machine gemaakt met het klassieke implementatiemodel Hallo koppelen](../articles/virtual-machines/windows/classic/attach-disk.md)|


## <a name="detailed-mitigations"></a>Gedetailleerde oplossingen

### <a name="vm-with-data-disk-whose-physical-blob-size-bytes-does-not-match-hello-vm-data-disk-logical-size-bytes"></a>Virtuele machine met gegevensschijf waarvan fysiek blob-grootte in bytes komt niet overeen met de Hallo VM gegevensschijf logische grootte in bytes.

Dit gebeurt wanneer hello logische grootte gegevensschijf vind niet gesynchroniseerd met de werkelijke grootte van VHD-blob Hallo. Dit u kunt eenvoudig controleren met behulp van de volgende opdrachten Hallo:

#### <a name="verifying-hello-issue"></a>Hallo probleem controleren

```PowerShell
# Store hello VM details in hello VM object
$vm = Get-AzureVM -ServiceName $servicename -Name $vmname

# Display hello data disk properties
# NOTE hello data disk LogicalDiskSizeInGB below which is 11GB. Also note hello MediaLink Uri of hello VHD blob as we'll use this in hello next step
$vm.VM.DataVirtualHardDisks


HostCaching         : None
DiskLabel           : 
DiskName            : coreosvm-coreosvm-0-201611230636240687
Lun                 : 0
LogicalDiskSizeInGB : 11
MediaLink           : https://contosostorage.blob.core.windows.net/vhds/coreosvm-dd1.vhd
SourceMediaLink     : 
IOType              : Standard
ExtensionData       : 

# Now get hello properties of hello blob backing hello data disk above
# NOTE hello size of hello blob is about 15 GB which is different from LogicalDiskSizeInGB above
$blob = Get-AzureStorageblob -Blob "coreosvm-dd1.vhd" -Container vhds 

$blob

ICloudBlob        : Microsoft.WindowsAzure.Storage.Blob.CloudPageBlob
BlobType          : PageBlob
Length            : 16106127872
ContentType       : application/octet-stream
LastModified      : 11/23/2016 7:16:22 AM +00:00
SnapshotTime      : 
ContinuationToken : 
Context           : Microsoft.WindowsAzure.Commands.Common.Storage.AzureStorageContext
Name              : coreosvm-dd1.vhd
```

#### <a name="mitigating-hello-issue"></a>Beperkende Hallo probleem

```PowerShell
# Convert hello blob size in bytes tooGB into a variable which we'll use later
$newSize = [int]($blob.Length / 1GB)

# See hello calculated size in GB
$newSize

15

# Store hello disk name of hello data disk as we'll use this tooidentify hello disk toobe updated
$diskName = $vm.VM.DataVirtualHardDisks[0].DiskName

# Identify hello LUN of hello data disk tooremove
$lunToRemove = $vm.VM.DataVirtualHardDisks[0].Lun

# Now remove hello data disk from hello VM so that hello disk isn't leased by hello VM and it's size can be updated
Remove-AzureDataDisk -LUN $lunToRemove -VM $vm | Update-AzureVm -Name $vmname -ServiceName $servicename

OperationDescription OperationId                          OperationStatus
-------------------- -----------                          ---------------
Update-AzureVM       213xx1-b44b-1v6n-23gg-591f2a13cd16   Succeeded  

# Verify we have hello right disk that's going toobe updated
Get-AzureDisk -DiskName $diskName

AffinityGroup        : 
AttachedTo           : 
IsCorrupted          : False
Label                : 
Location             : East US
DiskSizeInGB         : 11
MediaLink            : https://contosostorage.blob.core.windows.net/vhds/coreosvm-dd1.vhd
DiskName             : coreosvm-coreosvm-0-201611230636240687
SourceImageName      : 
OS                   : 
IOType               : Standard
OperationDescription : Get-AzureDisk
OperationId          : 0c56a2b7-a325-123b-7043-74c27d5a61fd
OperationStatus      : Succeeded

# Now update hello disk toohello new size
Update-AzureDisk -DiskName $diskName -ResizedSizeInGB $newSize -Label $diskName

OperationDescription OperationId                          OperationStatus
-------------------- -----------                          ---------------
Update-AzureDisk     cv134b65-1b6n-8908-abuo-ce9e395ac3e7 Succeeded 

# Now verify that hello "DiskSizeInGB" property of hello disk matches hello size of hello blob 
Get-AzureDisk -DiskName $diskName


AffinityGroup        : 
AttachedTo           : 
IsCorrupted          : False
Label                : coreosvm-coreosvm-0-201611230636240687
Location             : East US
DiskSizeInGB         : 15
MediaLink            : https://contosostorage.blob.core.windows.net/vhds/coreosvm-dd1.vhd
DiskName             : coreosvm-coreosvm-0-201611230636240687
SourceImageName      : 
OS                   : 
IOType               : Standard
OperationDescription : Get-AzureDisk
OperationId          : 1v53bde5-cv56-5621-9078-16b9c8a0bad2
OperationStatus      : Succeeded

# Now we'll add hello disk back toohello VM as a data disk. First we need tooget an updated VM object
$vm = Get-AzureVM -ServiceName $servicename -Name $vmname

Add-AzureDataDisk -Import -DiskName $diskName -LUN 0 -VM $vm -HostCaching ReadWrite | Update-AzureVm -Name $vmname -ServiceName $servicename

OperationDescription OperationId                          OperationStatus
-------------------- -----------                          ---------------
Update-AzureVM       b0ad3d4c-4v68-45vb-xxc1-134fd010d0f8 Succeeded      
```

### <a name="moving-a-vm-tooa-different-subscription-after-completing-migration"></a>Het verplaatsen van een ander VM tooa-abonnement na de migratie is voltooid

Nadat u het migratieproces Hallo hebt voltooid, kunt u toomove Hallo VM tooanother abonnement. Echter, als er een geheim/het certificaat op Hallo VM die verwijst naar een resource Sleutelkluis hello verplaatsen wordt momenteel niet ondersteund. Hallo onderstaande instructies kunt u tooworkaround Hallo probleem. 

#### <a name="powershell"></a>PowerShell
```powershell
$vm = Get-AzureRmVM -ResourceGroupName "MyRG" -Name "MyVM"
Remove-AzureRmVMSecret -VM $vm
Update-AzureRmVM -ResourceGroupName "MyRG" -VM $vm
```
#### <a name="azure-cli-20"></a>Azure CLI 2.0

```bash
az vm update -g "myrg" -n "myvm" --set osProfile.Secrets=[]
```
