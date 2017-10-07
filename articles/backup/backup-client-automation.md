---
title: aaaUse PowerShell tooback van Windows Server tooAzure | Microsoft Docs
description: Meer informatie over hoe toodeploy en Azure back-up met behulp van PowerShell beheren
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 65218095-2996-44d9-917b-8c84fc9ac415
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: saurse;markgal;jimpark;nkolli;trinadhk
ms.openlocfilehash: f13224f53abd6fbd132fee4347b0b99e8f5e2678
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-backup-tooazure-for-windows-serverwindows-client-using-powershell"></a>Implementeren en beheren van back-tooAzure voor Windows Server/Windows-clients met behulp van PowerShell
> [!div class="op_single_selector"]
> * [ARM](backup-client-automation.md)
> * [Klassiek](backup-client-automation-classic.md)
>
>

Dit artikel ziet u hoe toouse PowerShell voor het instellen van Azure Backup op Windows Server of een Windows-client en het beheren van back-up en herstel.

## <a name="install-azure-powershell"></a>Azure PowerShell installeren
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

Dit artikel is gericht op Hallo Azure Resource Manager (ARM) en Hallo MS Online back-up PowerShell-cmdlets waarmee u een Recovery Services-kluis in een resourcegroep toouse.

In oktober 2015 is Azure PowerShell 1.0 uitgebracht. Deze release Hallo 0.9.8 release is voltooid en over een aantal belangrijke wijzigingen, met name in Hallo naamgevingspatroon Hallo-cmdlets worden gebracht. 1.0 cmdlets volgen Hallo naamgevingspatroon {werkwoord}-AzureRm {zelfstandig naamwoord}; terwijl Hallo 0.9.8 namen geen bevatten **Rm** (bijvoorbeeld New-AzureRmResourceGroup in plaats van New-AzureResourceGroup). Wanneer u Azure PowerShell 0.9.8 gebruikt, moet u eerst Hallo Resource Manager-modus inschakelen door het uitvoeren van Hallo **Switch Azure AzureResourceManager** opdracht. Met deze opdracht hoeft niet in 1.0 of hoger.

Als u uw scripts die zijn geschreven voor Hallo 0.9.8-omgeving in Hallo 1.0 of hoger omgeving toouse wilt u moet zorgvuldig bijwerken en Hallo scripts te testen in een testomgeving voordat u ze in productie tooavoid onverwachte impact.

[Download de meest recente PowerShell-versie Hallo](https://github.com/Azure/azure-powershell/releases) (minimaal vereiste versie is: 1.0.0)

[!INCLUDE [arm-getting-setup-powershell](../../includes/arm-getting-setup-powershell.md)]

## <a name="create-a-recovery-services-vault"></a>Een Recovery Services-kluis maken
volgende stappen uit Hallo leiden u bij het maken van een Recovery Services-kluis. Een Recovery Services-kluis is anders dan een back-upkluis.

1. Als u van Azure Backup voor Hallo eerst gebruikmaakt, moet u Hallo **registreren AzureRMResourceProvider** cmdlet tooregister hello Azure Recovery Service provider met uw abonnement.

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. Hallo Recovery Services-kluis is een ARM-bron, dus u tooplace moet deze binnen een resourcegroep. U kunt een bestaande resourcegroep gebruiken of een nieuwe maken. Bij het maken van een nieuwe resourcegroep Hallo naam en locatie voor resourcegroep Hallo opgeven.  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "WestUS"
    ```
3. Gebruik Hallo **nieuw AzureRmRecoveryServicesVault** cmdlet toocreate Hallo nieuwe kluis. Zorg ervoor dat toospecify dezelfde locatie voor de kluis Hallo Hallo werd gebruikt voor de resourcegroep Hallo.

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "WestUS"
    ```
4. Geef een Hallo van opslag redundantie toouse; u kunt [lokaal redundante opslag (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) of [geografisch redundante opslag (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage). Hallo volgende voorbeeld ziet Hallo BackupStorageRedundancy - optie voor testVault tooGeoRedundant is ingesteld.

   > [!TIP]
   > Veel Azure Backup-cmdlets vereisen Hallo Recovery Services-kluis object als invoer. Daarom is het handige toostore Hallo back-up Recovery Services-kluis object in een variabele.
   >
   >

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testVault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

## <a name="view-hello-vaults-in-a-subscription"></a>Hallo-kluizen in een abonnement weergeven
Gebruik **Get-AzureRmRecoveryServicesVault** tooview Hallo lijst met alle kluizen in het huidige abonnement Hallo. U kunt deze opdracht toocheck of een nieuwe kluis is gemaakt of toosee welke kluizen zijn beschikbaar in het Hallo-abonnement.

Hallo-opdracht uitvoeren **Get-AzureRmRecoveryServicesVault**, en alle kluizen in Hallo abonnement worden weergegeven.

```
PS C:\> Get-AzureRmRecoveryServicesVault
Name              : Contoso-vault
ID                : /subscriptions/1234
Type              : Microsoft.RecoveryServices/vaults
Location          : WestUS
ResourceGroupName : Contoso-docs-rg
SubscriptionId    : 1234-567f-8910-abc
Properties        : Microsoft.Azure.Commands.RecoveryServices.ARSVaultProperties
```


## <a name="installing-hello-azure-backup-agent"></a>Hello Azure backup-agent installeren
Voordat u hello Azure backup-agent hebt geïnstalleerd, moet u toohave Hallo installatieprogramma gedownload en aanwezig is op Hallo van Windows Server. U kunt de nieuwste versie van de Hallo van Hallo installer krijgen van Hallo [Microsoft Download Center](http://aka.ms/azurebackup_agent) of van de dashboardpagina Hallo Recovery Services-kluis van. Hallo-installatieprogramma opslaan tooan toegankelijke locatie zoals * C:\Downloads\*.

U kunt ook gebruik PowerShell tooget Hallo downloader:
 
 ```
 $MarsAURL = 'Http://Aka.Ms/Azurebackup_Agent'
 $WC = New-Object System.Net.WebClient
 $WC.DownloadFile($MarsAURL,'C:\downloads\MARSAgentInstaller.EXE')
 C:\Downloads\MARSAgentInstaller.EXE /q
 ```

tooinstall Hallo agent uitvoeren Hallo volgende opdracht in een PowerShell-console met verhoogde bevoegdheid:

```
PS C:\> MARSAgentInstaller.exe /q
```

Dit met alle standaardopties voor Hallo Hallo-agent hebt geïnstalleerd. Hallo installatie duurt een paar minuten op Hallo achtergrond. Als u geen Hallo opgeeft */nu* optie vervolgens Hallo **Windows Update** venster wordt geopend na Hallo Hallo installatie toocheck voor eventuele updates. Wanneer is geïnstalleerd, weergegeven Hallo agent in Hallo lijst met geïnstalleerde programma's.

toosee hello lijst met geïnstalleerde programma's, gaat u te**Configuratiescherm** > **programma's** > **programma's en onderdelen**.

![Agent is geïnstalleerd](./media/backup-client-automation/installed-agent-listing.png)

### <a name="installation-options"></a>Opties voor de installatie
alle opties die beschikbaar zijn via Hallo toosee Hallo opdrachtregelprogramma, Hallo volgende opdracht gebruiken:

```
PS C:\> MARSAgentInstaller.exe /?
```

Hallo beschikbare opties zijn onder andere:

| Optie | Details | Standaard |
| --- | --- | --- |
| /q |Stille installatie |- |
| / p: 'locatie' |Pad toohello installatiemap op voor hello Azure backup-agent. |C:\Program Files\Microsoft Azure Recovery Services-Agent |
| / s: 'locatie' |Pad toohello cachemap voor hello Azure backup-agent. |C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch |
| /m |Opt-in tooMicrosoft Update |- |
| /nu |Niet controleren op updates nadat de installatie is voltooid |- |
| /d |Hiermee verwijdert u Microsoft Azure Recovery Services-Agent |- |
| /pH |Host-proxyadres |- |
| /PO |Proxy-Host-poortnummer |- |
| /Pu |De Proxygebruikersnaam voor de Host |- |
| /PW |Proxy-wachtwoord |- |

## <a name="registering-windows-server-or-windows-client-machine-tooa-recovery-services-vault"></a>Registreren van Windows Server of Windows client machine tooa Recovery Services-kluis
Nadat u Hallo Recovery Services-kluis hebt gemaakt, de nieuwste agent Hallo en Hallo kluisreferenties downloaden en opslaan in een handige locatie zoals C:\Downloads.

```
PS C:\> $credspath = "C:\downloads"
PS C:\> $credsfilename = Get-AzureRmRecoveryServicesVaultSettingsFile -Backup -Vault $vault1 -Path  $credspath
```

Voer Hallo op Hallo Windows Server of Windows-clientcomputer [Start OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet tooregister Hallo machine met de Hallo kluis.
Deze en andere cmdlets gebruikt voor back-up, zijn afkomstig van Hallo MSONLINE module welke Mars AgentInstaller toegevoegd als onderdeel van het installatieproces Hallo Hallo. 

het installatieprogramma van Agent Hallo Hallo $Env niet bijgewerkt: PSModulePath variabele. Dit betekent dat module automatisch laden is mislukt. tooresolve dit kunt u doen Hallo volgende:

```
PS C:\>  $Env:psmodulepath += ';C:\Program Files\Microsoft Azure Recovery Services Agent\bin\Modules
```

U kunt ook kunt u handmatig laden Hallo module in uw script als volgt:

```
PS C:\>  Import-Module  'C:\Program Files\Microsoft Azure Recovery Services Agent\bin\Modules\MSOnlineBackup'

```

Zodra u Hallo Online Backup-cmdlets geladen, kunt u referenties voor de kluis Hallo registreren:


```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-OBRegistration-VaultCredentials $cred -Confirm:$false
CertThumbprint      :7a2ef2caa2e74b6ed1222a5e89288ddad438df2
SubscriptionID      : ef4ab577-c2c0-43e4-af80-af49f485f3d1
ServiceResourceName: testvault
Region              :WestUS
Machine registration succeeded.
```

> [!IMPORTANT]
> Gebruik geen relatieve paden toospecify hello kluisreferentiebestand. U moet een absoluut pad opgeven als een cmdlet invoer toohello.
>
>

## <a name="networking-settings"></a>Netwerkinstellingen
Wanneer de connectiviteit Hallo Hallo Windows machine toohello die Internet via een proxyserver is, kunnen Hallo proxy-instellingen ook worden opgegeven toohello agent. In dit voorbeeld is het geen proxyserver zodat we alle informatie met betrekking tot de proxy expliciet wordt gewist.

Bandbreedtegebruik kan ook worden beheerd met Hallo opties ```work hour bandwidth``` en ```non-work hour bandwidth``` voor een bepaald aantal dagen van week Hallo.

Hallo-proxy en bandbreedte details van de instelling wordt gedaan met behulp van Hallo [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) cmdlet:

```
PS C:\> Set-OBMachineSetting -NoProxy
Server properties updated successfully.

PS C:\> Set-OBMachineSetting -NoThrottle
Server properties updated successfully.
```

## <a name="encryption-settings"></a>Versleutelingsinstellingen
Hallo back-upgegevens verzonden tooAzure back-up is versleutelde tooprotect Hallo vertrouwelijkheid van Hallo-gegevens. Hallo-wachtwoordzin voor versleuteling is Hallo 'password' toodecrypt Hallo gegevens op Hallo moment van terugzetten.

```
PS C:\> ConvertTo-SecureString -String "Complex!123_STRING" -AsPlainText -Force | Set-OBMachineSetting
PS C:\> $PassPhrase = ConvertTo-SecureString -String "Complex!123_STRING" -AsPlainText -Force 
PS C:\> $PassCode   = 'AzureR0ckx'
PS C:\> Set-OBMachineSetting -EncryptionPassPhrase $PassPhrase
Server properties updated successfully
```

> [!IMPORTANT]
> Hallo wachtwoordzin gegevens veilig en beveiligd houden als deze eenmaal is ingesteld. U kunt toorestore gegevens van Azure zonder deze wachtwoordzin niet zijn.
>
>

## <a name="back-up-files-and-folders"></a>Back-up maken van bestanden en mappen
Alle back-ups van Windows-Servers en clients tooAzure back-up worden geregeld door een beleid. Hallo-beleid bestaat uit drie delen:

1. Een **back-upschema** die aangeeft wanneer back-ups moeten toobe gemaakt en gesynchroniseerd met Hallo-service.
2. Een **bewaarschema** die aangeeft hoe lang tooretain Hallo herstelpunten in Azure.
3. Een **opnemen of uitsluiten opgeven van een bestand** die bepaalt wat moet een back-up.

In dit document, omdat er bij het automatiseren van back-up, gebruiken we dat er niets is geconfigureerd. We beginnen met het maken van een nieuwe back-upbeleid Hallo met [nieuw OBPolicy](https://technet.microsoft.com/library/hh770416.aspx) cmdlet.

```
PS C:\> $newpolicy = New-OBPolicy
```

Op dit moment Hallo beleid leeg is en andere cmdlets zijn benodigde toodefine welke items worden opgenomen of uitgesloten, wanneer back-ups wordt uitgevoerd en waarbij Hallo back-ups worden opgeslagen.

### <a name="configuring-hello-backup-schedule"></a>Back-upschema Hallo configureren
eerst Hallo Hallo 3 delen van een beleid is de back-upschema hello, die is gemaakt met een Hallo [nieuw OBSchedule](https://technet.microsoft.com/library/hh770401) cmdlet. back-upschema Hallo definieert wanneer back-ups moeten toobe genomen. Bij het maken van een schema moet u de invoerparameters toospecify 2:

* **Dagen van week Hallo** Hallo back-up moet worden uitgevoerd. U kunt back-uptaak Hallo op slechts één dag, of elke dag van week hello of een combinatie van daartussen uitvoeren.
* **Hallo tijdstippen** wanneer Hallo back-up moet worden uitgevoerd. U kunt definiëren up too3 verschillende tijdstippen Hallo wanneer Hallo back-up wordt geactiveerd.

U kunt bijvoorbeeld een back-upbeleid dat wordt uitgevoerd op 4 uur elke zaterdag en zondag configureren.

```
PS C:\> $sched = New-OBSchedule -DaysofWeek Saturday, Sunday -TimesofDay 16:00
```

Hallo back-upschema moet toobe die zijn gekoppeld aan een beleid en dit kan worden gerealiseerd met behulp van Hallo [Set OBSchedule](https://technet.microsoft.com/library/hh770407) cmdlet.

```
PS C:> Set-OBSchedule -Policy $newpolicy -Schedule $sched
BackupSchedule : 4:00 PM Saturday, Sunday, Every 1 week(s) DsList : PolicyName : RetentionPolicy : State : New PolicyState : Valid
```
### <a name="configuring-a-retention-policy"></a>Een bewaarbeleid configureren
Hallo bewaarbeleid definieert hoe lang herstel die zijn gemaakt vanuit een back-uptaken worden bewaard. Bij het maken van een nieuw bewaarbeleid Hallo met [nieuw OBRetentionPolicy](https://technet.microsoft.com/library/hh770425) cmdlet, kunt u opgeven aantal dagen dat de back-up herstelpunten Hallo Hallo moet toobe behouden met Azure Backup. Hallo in het volgende voorbeeld wordt een bewaarbeleid van 7 dagen ingesteld.

```
PS C:\> $retentionpolicy = New-OBRetentionPolicy -RetentionDays 7
```

Hallo bewaarbeleid moet worden gekoppeld met de belangrijkste Hallo-beleid met de cmdlet Hallo [Set OBRetentionPolicy](https://technet.microsoft.com/library/hh770405):

```
PS C:\> Set-OBRetentionPolicy -Policy $newpolicy -RetentionPolicy $retentionpolicy

BackupSchedule  : 4:00 PM
                  Saturday, Sunday,
                  Every 1 week(s)
DsList          :
PolicyName      :
RetentionPolicy : Retention Days : 7

                  WeeklyLTRSchedule :
                  Weekly schedule is not set

                  MonthlyLTRSchedule :
                  Monthly schedule is not set

                  YearlyLTRSchedule :
                  Yearly schedule is not set

State           : New
PolicyState     : Valid
```
### <a name="including-and-excluding-files-toobe-backed-up"></a>Opnemen en uitsluiten van bestanden toobe back-up
Een ```OBFileSpec``` object definieert Hallo bestanden toobe opgenomen en uitgesloten van een back-up. Dit is een reeks regels dat bereik uit Hallo bestanden en mappen op een computer beveiligde. U kunt als veel bestand opgenomen of uitgesloten regels zoals vereist en deze koppelen aan een beleid hebben. Wanneer u een nieuw OBFileSpec-object maakt, kunt u:

* Hallo-bestanden en mappen toobe opgenomen opgeven
* Hallo-bestanden en mappen toobe uitgesloten opgeven
* Geef recursieve back-up van gegevens in een map (of) of op het hoogste niveau bestanden alleen Hallo in de opgegeven map Hallo een back-.

Hallo laatstgenoemde wordt bereikt door middel van Hallo - niet-recursieve vlag in Hallo nieuw OBFileSpec-opdracht.

In onderstaande Hallo voorbeeld, we back-up volume C: en D: en Hallo OS binaire bestanden in de map Windows hello en tijdelijke mappen uitsluiten. toodo zodat maken we twee bestandsspecificaties Hallo met [nieuw OBFileSpec](https://technet.microsoft.com/library/hh770408) cmdlet - één voor insluiting en één voor uitsluiting. Zodra het Hallo-bestandsspecificaties zijn gemaakt, deze zijn gekoppeld aan Hallo beleid met behulp van Hallo [toevoegen OBFileSpec](https://technet.microsoft.com/library/hh770424) cmdlet.

```
PS C:\> $inclusions = New-OBFileSpec -FileSpec @("C:\", "D:\")

PS C:\> $exclusions = New-OBFileSpec -FileSpec @("C:\windows", "C:\temp") -Exclude

PS C:\> Add-OBFileSpec -Policy $newpolicy -FileSpec $inclusions

BackupSchedule  : 4:00 PM
                  Saturday, Sunday,
                  Every 1 week(s)
DsList          : {DataSource
                  DatasourceId:0
                  Name:C:\
                  FileSpec:FileSpec
                  FileSpec:C:\
                  IsExclude:False
                  IsRecursive:True

                  , DataSource
                  DatasourceId:0
                  Name:D:\
                  FileSpec:FileSpec
                  FileSpec:D:\
                  IsExclude:False
                  IsRecursive:True

                  }
PolicyName      :
RetentionPolicy : Retention Days : 7

                  WeeklyLTRSchedule :
                  Weekly schedule is not set

                  MonthlyLTRSchedule :
                  Monthly schedule is not set

                  YearlyLTRSchedule :
                  Yearly schedule is not set

State           : New
PolicyState     : Valid


PS C:\> Add-OBFileSpec -Policy $newpolicy -FileSpec $exclusions

BackupSchedule  : 4:00 PM
                  Saturday, Sunday,
                  Every 1 week(s)
DsList          : {DataSource
                  DatasourceId:0
                  Name:C:\
                  FileSpec:FileSpec
                  FileSpec:C:\
                  IsExclude:False
                  IsRecursive:True
                  ,FileSpec
                  FileSpec:C:\windows
                  IsExclude:True
                  IsRecursive:True
                  ,FileSpec
                  FileSpec:C:\temp
                  IsExclude:True
                  IsRecursive:True

                  , DataSource
                  DatasourceId:0
                  Name:D:\
                  FileSpec:FileSpec
                  FileSpec:D:\
                  IsExclude:False
                  IsRecursive:True

                  }
PolicyName      :
RetentionPolicy : Retention Days : 7

                  WeeklyLTRSchedule :
                  Weekly schedule is not set

                  MonthlyLTRSchedule :
                  Monthly schedule is not set

                  YearlyLTRSchedule :
                  Yearly schedule is not set

State           : New
PolicyState     : Valid
```

### <a name="applying-hello-policy"></a>Hallo-beleid wordt toegepast
Nu Hallo group policy object is voltooid en heeft een bijbehorende back-upschema, bewaarbeleid en een lijst opnemen of uitsluiten van bestanden. Dit beleid kan nu worden toegezegd voor Azure Backup toouse. Voordat u nieuwe Hallo toepassen beleid Zorg ervoor dat er geen bestaande back-upbeleid gekoppeld aan Hallo-server met behulp van Hallo [verwijderen OBPolicy](https://technet.microsoft.com/library/hh770415) cmdlet. Verwijderen van het Hallo-beleid wordt om bevestiging gevraagd. bevestiging van tooskip hello gebruiken Hallo ```-Confirm:$false``` vlag met Hallo-cmdlet.

```
PS C:> Get-OBPolicy | Remove-OBPolicy
Microsoft Azure Backup Are you sure you want tooremove this backup policy? This will delete all hello backed up data. [Y] Yes [A] Yes tooAll [N] No [L] No tooAll [S] Suspend [?] Help (default is "Y"):
```

Hallo group policy object doorvoeren wordt gedaan met behulp van Hallo [Set OBPolicy](https://technet.microsoft.com/library/hh770421) cmdlet. Dit wordt ook gevraagd om bevestiging. bevestiging van tooskip hello gebruiken Hallo ```-Confirm:$false``` vlag met Hallo-cmdlet.

```
PS C:> Set-OBPolicy -Policy $newpolicy
Microsoft Azure Backup Do you want toosave this backup policy ? [Y] Yes [A] Yes tooAll [N] No [L] No tooAll [S] Suspend [?] Help (default is "Y"):
BackupSchedule : 4:00 PM Saturday, Sunday, Every 1 week(s)
DsList : {DataSource
         DatasourceId:4508156004108672185
         Name:C:\
         FileSpec:FileSpec
         FileSpec:C:\
         IsExclude:False
         IsRecursive:True,

         FileSpec
         FileSpec:C:\windows
         IsExclude:True
         IsRecursive:True,

         FileSpec
         FileSpec:C:\temp
         IsExclude:True
         IsRecursive:True,

         DataSource
         DatasourceId:4508156005178868542
         Name:D:\
         FileSpec:FileSpec
         FileSpec:D:\
         IsExclude:False
         IsRecursive:True
    }
PolicyName : c2eb6568-8a06-49f4-a20e-3019ae411bac
RetentionPolicy : Retention Days : 7
              WeeklyLTRSchedule :
              Weekly schedule is not set

              MonthlyLTRSchedule :
              Monthly schedule is not set

              YearlyLTRSchedule :
              Yearly schedule is not set
State : Existing PolicyState : Valid
```

U kunt details Hallo Hallo bestaande back-upbeleid met Hallo weergeven [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) cmdlet. U kunt inzoomen verder met Hallo [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) cmdlet voor back-upschema Hallo en Hallo [Get-OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) cmdlet voor het bewaarbeleid Hallo

```
PS C:> Get-OBPolicy | Get-OBSchedule
SchedulePolicyName : 71944081-9950-4f7e-841d-32f0a0a1359a
ScheduleRunDays : {Saturday, Sunday}
ScheduleRunTimes : {16:00:00}
State : Existing

PS C:> Get-OBPolicy | Get-OBRetentionPolicy
RetentionDays : 7
RetentionPolicyName : ca3574ec-8331-46fd-a605-c01743a5265e
State : Existing

PS C:> Get-OBPolicy | Get-OBFileSpec
FileName : *
FilePath : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\
FileSpec : D:\
IsExclude : False
IsRecursive : True

FileName : *
FilePath : \?\Volume{cdd41007-a22f-11e2-be6c-806e6f6e6963}\
FileSpec : C:\
IsExclude : False
IsRecursive : True

FileName : *
FilePath : \?\Volume{cdd41007-a22f-11e2-be6c-806e6f6e6963}\windows
FileSpec : C:\windows
IsExclude : True
IsRecursive : True

FileName : *
FilePath : \?\Volume{cdd41007-a22f-11e2-be6c-806e6f6e6963}\temp
FileSpec : C:\temp
IsExclude : True
IsRecursive : True
```

### <a name="performing-an-ad-hoc-backup"></a>Een ad-hoc back-up maken
Wanneer een back-upbeleid is ingesteld Hallo back-ups per Hallo schema uitgevoerd. Activering van een ad-hoc back-up is ook mogelijk met behulp van Hallo [Start OBBackup](https://technet.microsoft.com/library/hh770426) cmdlet:

```
PS C:> Get-OBPolicy | Start-OBBackup
Initializing
Taking snapshot of volumes...
Preparing storage...
Generating backup metadata information and preparing hello metadata VHD...
Data transfer is in progress. It might take longer since it is hello first backup and all data needs toobe transferred...
Data transfer completed and all backed up data is in hello cloud. Verifying data integrity...
Data transfer completed
In progress...
Job completed.
hello backup operation completed successfully.
```

## <a name="restore-data-from-azure-backup"></a>Gegevens terugzetten vanuit Azure Backup
Deze sectie leidt u door Hallo stappen voor het automatiseren van herstel van gegevens vanuit Azure Backup. Dit omvat dus Hallo stappen te volgen:

1. Kies het bronvolume Hallo
2. Kies een back-punt toorestore
3. Kies een item toorestore
4. Trigger Hallo herstelproces

### <a name="picking-hello-source-volume"></a>Hallo bronvolume verzamelen
In de volgorde toorestore een item uit Azure Backup moet u eerst tooidentify Hallo bron van Hallo-item. Aangezien we Hallo opdrachten in de context van een Windows-Server of een Windows-client hello uitvoeren je, is al Hallo machine geïdentificeerd. volgende stap bij het identificeren van bron Hallo Hallo is tooidentify Hallo volume met het. Een lijst van volumes of bronnen wordt een back-up van deze computer kan worden opgehaald door het uitvoeren van Hallo [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) cmdlet. Met deze opdracht retourneert een matrix van alle Hallo bronnen back-up van deze server /-client.

```
PS C:> $source = Get-OBRecoverableSource
PS C:> $source
FriendlyName : C:\
RecoverySourceName : C:\
ServerName : myserver.microsoft.com

FriendlyName : D:\
RecoverySourceName : D:\
ServerName : myserver.microsoft.com
```

### <a name="choosing-a-backup-point-from-which-toorestore"></a>Een back-uppunt kiezen in welke toorestore
U een lijst met back-uppunten door het uitvoeren van Hallo ophalen [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet met de juiste parameters. In ons voorbeeld kiest Hallo meest recente back-punt voor het bronvolume Hallo *D:* en gebruik deze toorecover een specifiek bestand.

```
PS C:> $rps = Get-OBRecoverableItem -Source $source[1]
IsDir : False
ItemNameFriendly : D:\
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\
LocalMountPoint : D:\
MountPointName : D:\
Name : D:\
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize :
ItemLastModifiedTime :

IsDir : False
ItemNameFriendly : D:\
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\
LocalMountPoint : D:\
MountPointName : D:\
Name : D:\
PointInTime : 17-Jun-15 6:31:31 AM
ServerName : myserver.microsoft.com
ItemSize :
ItemLastModifiedTime :
```
Hallo-object ```$rps``` is een matrix met back-uppunten. Hallo eerste element is het laatste herstelpunt Hallo en ne Hallo-element is Hallo oudste punt. toochoose hello laatste herstelpunt, gebruiken we ```$rps[0]```.

### <a name="choosing-an-item-toorestore"></a>Een item toorestore kiezen
tooidentify hello exacte bestand of map toorestore, recursief hello gebruiken [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet. Die hiërarchie manier Hallo map kan worden gebladerd uitsluitend met Hallo ```Get-OBRecoverableItem```.

In dit voorbeeld als we toorestore Hallo bestand wilt *finances.xls* we kan verwijzen naar dat als u met Hallo object ```$filesFolders[1]```.

```
PS C:> $filesFolders = Get-OBRecoverableItem $rps[0]
PS C:> $filesFolders
IsDir : True
ItemNameFriendly : D:\MyData\
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\MyData\
LocalMountPoint : D:\
MountPointName : D:\
Name : MyData
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize :
ItemLastModifiedTime : 15-Jun-15 8:49:29 AM

PS C:> $filesFolders = Get-OBRecoverableItem $filesFolders[0]
PS C:> $filesFolders
IsDir : False
ItemNameFriendly : D:\MyData\screenshot.oxps
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\MyData\screenshot.oxps
LocalMountPoint : D:\
MountPointName : D:\
Name : screenshot.oxps
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize : 228313
ItemLastModifiedTime : 21-Jun-14 6:45:09 AM

IsDir : False
ItemNameFriendly : D:\MyData\finances.xls
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\MyData\finances.xls
LocalMountPoint : D:\
MountPointName : D:\
Name : finances.xls
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize : 96256
ItemLastModifiedTime : 21-Jun-14 6:43:02 AM
```

U kunt ook zoeken naar items toorestore met Hallo ```Get-OBRecoverableItem``` cmdlet. In ons voorbeeld toosearch voor *finances.xls* we kan een ingang krijgen op Hallo-bestand door deze opdracht uit te voeren:

```
PS C:\> $item = Get-OBRecoverableItem -RecoveryPoint $rps[0] -Location "D:\MyData" -SearchString "finance*"
```

### <a name="triggering-hello-restore-process"></a>Activerende Hallo herstelproces
tootrigger hello herstelproces, moeten we eerst toospecify Hallo herstelopties. Dit kan worden gedaan met behulp van Hallo [nieuw OBRecoveryOption](https://technet.microsoft.com/library/hh770417.aspx) cmdlet. In dit voorbeeld gaan we ervan uit dat we toorestore Hallo bestanden te willen*C:\temp*. Laten we ook uitgaan dat we willen tooskip bestanden die al aanwezig op de doelmap Hallo *C:\temp*. toocreate dergelijke een hersteloptie Hallo volgende opdracht gebruiken:

```
PS C:\> $recovery_option = New-OBRecoveryOption -DestinationPath "C:\temp" -OverwriteType Skip
```

Hallo herstelproces nu te activeren met behulp van Hallo [Start OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) opdracht op Hallo geselecteerd ```$item``` van uitvoer Hallo Hallo ```Get-OBRecoverableItem``` cmdlet:

```
PS C:\> Start-OBRecovery -RecoverableItem $item -RecoveryOption $recover_option
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Job completed.
hello recovery operation completed successfully.
```


## <a name="uninstalling-hello-azure-backup-agent"></a>Hello Azure backup-agent verwijderen
Verwijderen hello Azure backup-agent kan worden gedaan met behulp van de volgende opdracht Hallo:

```
PS C:\> .\MARSAgentInstaller.exe /d /q
```

Hallo agent binaire bestanden verwijderen van de machine Hallo heeft enkele tooconsider gevolgen:

* Hallo-bestandsfilter uit Hallo machine wordt verwijderd en bijhouden van wijzigingen is gestopt.
* Alle beleidsgegevens van Hallo machine wordt verwijderd, maar Hallo beleidsgegevens blijft toobe opgeslagen in het Hallo-service.
* Alle back-upschema's worden verwijderd en er is geen verdere back-ups worden gemaakt.

Echter gegevens die zijn opgeslagen in Azure blijft Hallo en door u aan de hand van Hallo bewaren beleid setup wordt bewaard. Oudere punten worden automatisch verouderde.

## <a name="remote-management"></a>Extern beheer
Alle Hallo management rond hello Azure backup-agent, beleid en gegevensbronnen kan op afstand worden uitgevoerd via PowerShell. Hallo-machine die op afstand worden beheerd moet toobe correct voorbereid.

Hallo WinRM-service is standaard geconfigureerd voor handmatig opstarten. Opstarttype Hello te moet worden ingesteld*automatische* en Hallo-service moet worden gestart. tooverify die Hallo WinRM-service wordt uitgevoerd, Hallo-waarde van de eigenschap Status Hallo moet *met*.

```
PS C:\> Get-Service WinRM

Status   Name               DisplayName
------   ----               -----------
Running  winrm              Windows Remote Management (WS-Manag...
```

PowerShell moet worden geconfigureerd voor externe toegang.

```
PS C:\> Enable-PSRemoting -force
WinRM is already set up tooreceive requests on this computer.
WinRM has been updated for remote management.
WinRM firewall exception enabled.

PS C:\> Set-ExecutionPolicy unrestricted -force
```

Hallo-machine kan nu worden beheerd op afstand - van Hallo Hallo agent-installatie wordt gestart. Bijvoorbeeld, Hallo script volgen Hallo agent toohello externe computer worden gekopieerd en installeert deze.

```
PS C:\> $dloc = "\\REMOTESERVER01\c$\Windows\Temp"
PS C:\> $agent = "\\REMOTESERVER01\c$\Windows\Temp\MARSAgentInstaller.exe"
PS C:\> $args = "/q"
PS C:\> Copy-Item "C:\Downloads\MARSAgentInstaller.exe" -Destination $dloc - force

PS C:\> $s = New-PSSession -ComputerName REMOTESERVER01
PS C:\> Invoke-Command -Session $s -Script { param($d, $a) Start-Process -FilePath $d $a -Wait } -ArgumentList $agent $args
```

## <a name="next-steps"></a>Volgende stappen
Voor meer informatie over Azure Backup voor Windows Server /-Client, Zie

* [Inleiding tooAzure back-up](backup-introduction-to-azure-backup.md)
* [Back-up van Windows-Servers](backup-configure-vault.md)
