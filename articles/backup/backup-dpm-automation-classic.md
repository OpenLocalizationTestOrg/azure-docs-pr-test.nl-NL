---
title: 'Azure Backup: Gebruik PowerShell tooback up DPM workloads | Microsoft Docs'
description: Meer informatie over hoe toodeploy en beheren van Azure Backup voor Data Protection Manager (DPM) met behulp van PowerShell
services: backup
documentationcenter: 
author: Nkolli1
manager: shreeshd
editor: 
ms.assetid: bcbcef79-9d33-4e84-a558-9866614f2cae
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: nkolli;trinadhk;anuragm;markgal
ms.openlocfilehash: 48ebe6b520857836e89749ffb6fe83d1f14c5597
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-backup-tooazure-for-data-protection-manager-dpm-servers-using-powershell"></a>Implementeren en beheren van back-tooAzure voor Data Protection Manager (DPM) servers met behulp van PowerShell
> [!div class="op_single_selector"]
> * [ARM](backup-dpm-automation.md)
> * [Klassiek](backup-dpm-automation-classic.md)
>
>

Dit artikel wordt uitgelegd hoe toouse PowerShell tooback boven- en DPM-gegevens herstellen vanaf een back-upkluis. Microsoft raadt u aan met behulp van de Recovery Services-kluizen voor alle nieuwe implementaties. Als u een nieuwe Azure Backup-gebruiker bent, gebruikt u Hallo artikel [implementeren en beheren van Data Protection Manager gegevens tooAzure met behulp van PowerShell](backup-dpm-automation.md), zodat u uw gegevens in een Recovery Services-kluis opslaat.

> [!IMPORTANT]
> U kunt nu uw back-up kluizen tooRecovery Services-kluizen upgraden. Zie voor meer informatie artikel Hallo [upgraden van een back-up kluis tooa Recovery Services-kluis](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft raadt u tooupgrade uw back-upkluizen tooRecovery Services-kluizen. U kunt PowerShell toocreate Backup-kluizen niet gebruiken na 15 oktober 2017. **Per 1 november 2017**:
>- Alle resterende Backup-kluizen worden automatisch bijgewerkt tooRecovery Services-kluizen.
>- U niet kunt tooaccess uw back-upgegevens in de klassieke portal Hallo. In plaats daarvan gebruik hello Azure portal tooaccess uw back-upgegevens in Recovery Services-kluizen.
>

## <a name="setting-up-hello-powershell-environment"></a>Hallo PowerShell-omgeving instellen
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

Voordat u PowerShell toomanage back-ups van Data Protection Manager tooAzure gebruiken kunt, moet u toohave Hallo juiste omgeving in PowerShell. Bij Hallo begin van de PowerShell-sessie hello, ervoor te zorgen dat u na de opdracht tooimport Hallo rechts modules Hallo uitvoeren en u toocorrectly verwijzing Hallo DPM-cmdlets kunt:

```
PS C:> & "C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin\DpmCliInitScript.ps1"

Welcome toohello DPM Management Shell!

Full list of cmdlets: Get-Command
Only DPM cmdlets: Get-DPMCommand
Get general help: help
Get help for a cmdlet: help <cmdlet-name> or <cmdlet-name> -?
Get definition of a cmdlet: Get-Command <cmdlet-name> -Syntax
Sample DPM scripts: Get-DPMSampleScript
```

## <a name="setup-and-registration"></a>De installatie en registratie
toobegin:

1. [Download de meest recente PowerShell](https://github.com/Azure/azure-powershell/releases) (minimaal vereiste versie is: 1.0.0)
2. Hello Azure Backup commandlets inschakelen door het overschakelen te*AzureResourceManager* modus met behulp van Hallo **Switch AzureMode** commandlet:

```
PS C:\> Switch-AzureMode AzureResourceManager
```

Hallo kunnen volgende installatie en registratietaken worden geautomatiseerd met PowerShell:

* Een back-upkluis maken
* Hello Azure backup-agent installeren
* Registreren bij hello Azure Backup-service
* Netwerkinstellingen
* Versleutelingsinstellingen

### <a name="create-a-backup-vault"></a>Een back-upkluis maken
> [!WARNING]
> Voor klanten die gebruikmaken van Azure Backup voor Hallo eerst, moet u tooregister hello Azure Backup-provider toobe gebruikt met uw abonnement. Dit kan worden gedaan door het uitvoeren van de volgende opdracht Hallo: Register AzureProvider - ProviderNamespace 'Microsoft.Backup'
>
>

U kunt een nieuwe back-upkluis met Hallo maken **nieuw AzureRMBackupVault** commandlet. Hallo back-upkluis is een ARM-bron, dus u tooplace moet deze binnen een resourcegroep. Voer Hallo volgende opdrachten in een verhoogde Azure PowerShell-console:

```
PS C:\> New-AzureResourceGroup –Name “test-rg” -Region “West US”
PS C:\> $backupvault = New-AzureRMBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GRS
```

U kunt een lijst met alle Hallo back-upkluizen krijgen in een bepaald abonnement met behulp van Hallo **Get-AzureRMBackupVault** commandlet.

### <a name="installing-hello-azure-backup-agent-on-a-dpm-server"></a>Hello Azure backup-agent installeren op een DPM-Server
Voordat u hello Azure backup-agent hebt geïnstalleerd, moet u toohave Hallo installatieprogramma gedownload en aanwezig is op Hallo van Windows Server. U kunt de nieuwste versie van de Hallo van Hallo installer krijgen van Hallo [Microsoft Download Center](http://aka.ms/azurebackup_agent) of van de dashboardpagina Hallo back-upkluis. Hallo-installatieprogramma opslaan tooan toegankelijke locatie zoals * C:\Downloads\*.

tooinstall hello agent, Hallo volgende opdracht in een PowerShell-console met verhoogde bevoegdheden uitvoeren **op de DPM-server Hallo**:

```
PS C:\> MARSAgentInstaller.exe /q
```

Dit met alle standaardopties voor Hallo Hallo-agent hebt geïnstalleerd. Hallo installatie duurt een paar minuten op Hallo achtergrond. Als u geen Hallo opgeeft */nu* optie Hallo **Windows Update** venster wordt geopend na Hallo Hallo installatie toocheck voor eventuele updates.

Hallo-agent wordt weergegeven in de lijst met geïnstalleerde programma Hallo. toosee hello lijst met geïnstalleerde programma's, gaat u te**Configuratiescherm** > **programma's** > **programma's en onderdelen**.

![Agent is geïnstalleerd](./media/backup-dpm-automation/installed-agent-listing.png)

#### <a name="installation-options"></a>Opties voor de installatie
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

### <a name="registering-with-hello-azure-backup-service"></a>Registreren bij hello Azure Backup-service
Voordat u met hello Azure Backup-service registreren kunt, moet u tooensure die Hallo [vereisten](backup-azure-dpm-introduction.md) wordt voldaan. U moet doen:

* Een geldige Azure-abonnement hebt
* Hebt u een back-upkluis

toodownload hello kluisreferenties, Voer Hallo **Get-AzureBackupVaultCredentials** commandlet in een Azure PowerShell-console en opslaan in een handige locatie, zoals * C:\Downloads\*.

```
PS C:\> $credspath = "C:\"
PS C:\> $credsfilename = Get-AzureRMBackupVaultCredentials -Vault $backupvault -TargetLocation $credspath
PS C:\> $credsfilename
f5303a0b-fae4-4cdb-b44d-0e4c032dde26_backuprg_backuprn_2015-08-11--06-22-35.VaultCredentials
```

Registreren Hallo-machine met de Hallo kluis wordt gedaan met behulp van Hallo [Start DPMCloudRegistration](https://technet.microsoft.com/library/jj612787) cmdlet:

```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-DPMCloudRegistration -DPMServerName "TestingServer" -VaultCredentialsFilePath $cred
```

Deze DPM-Server met de naam 'TestingServer' hello worden geregistreerd bij Microsoft Azure-kluis Hallo opgegeven met referenties-kluis.

> [!IMPORTANT]
> Gebruik geen relatieve paden toospecify hello kluisreferentiebestand. U moet een absoluut pad opgeven als een cmdlet invoer toohello.
>
>

### <a name="initial-configuration-settings"></a>Configuratie-instellingen
Zodra hello DPM-Server is geregistreerd bij hello Azure Backup-kluis, wordt deze gestart met de standaardinstellingen van het abonnement. Deze abonnementsinstellingen omvatten netwerken, versleuteling en Hallo faseringsgebied. toobegin veranderende Hallo abonnementsinstellingen die u moet toofirst krijgen een ingang voor Hallo bestaande (standaard)-instellingen met Hallo [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) cmdlet:

```
$setting = Get-DPMCloudSubscriptionSetting -DPMServerName "TestingServer"
```

Alle wijzigingen zijn aangebracht toothis lokale PowerShell-object ```$setting``` en vervolgens volledige Hallo-object is doorgevoerd tooDPM en Azure Backup toosave ze met behulp van Hallo [Set DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet. U moet toouse hello ```–Commit``` vlag tooensure die Hallo wijzigingen worden doorgevoerd. Hallo-instellingen worden niet toegepast en door Azure Backup gebruikt tenzij doorgevoerd.

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

### <a name="networking"></a>Netwerken
Als Hallo connectiviteit van Hallo DPM machine toohello Azure Backup-service op Hallo internet via een proxyserver, mag Hallo proxyserverinstellingen voor back-ups toosucceed worden opgegeven. Dit wordt gedaan met behulp van Hallo ```-ProxyServer```, ```-ProxyPort```, ```-ProxyUsername``` en Hallo ```ProxyPassword``` parameters Hello [Set DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet. In dit voorbeeld is het geen proxyserver zodat we alle informatie met betrekking tot de proxy expliciet wordt gewist.

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoProxy
```

Bandbreedtegebruik kan ook worden beheerd met opties ```-WorkHourBandwidth``` en ```-NonWorkHourBandwidth``` voor een bepaald aantal dagen van week Hallo. In dit voorbeeld stelt we niet beperking.

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoThrottle
```

### <a name="configuring-hello-staging-area"></a>Hallo faseringsgebied configureren
Hello Azure Backup agent wordt uitgevoerd op Hallo DPM-server moet een tijdelijke opslag voor gegevens die zijn teruggezet vanuit een Hallo cloud (lokaal faseringsgebied). Hallo faseringsgebied met Hallo configureren [Set DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet en Hallo ```-StagingAreaPath``` parameter.

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -StagingAreaPath "C:\StagingArea"
```

Hallo bovenstaande voorbeeld Hallo faseringsgebied te worden ingesteld*C:\StagingArea* in PowerShell-object Hallo ```$setting```. Zorg ervoor dat Hallo opgegeven map bestaat al, anders Hallo laatste doorvoering van de abonnementsinstellingen Hallo zal mislukken.

### <a name="encryption-settings"></a>Versleutelingsinstellingen
Hallo back-upgegevens verzonden tooAzure back-up is versleutelde tooprotect Hallo vertrouwelijkheid van Hallo-gegevens. Hallo-wachtwoordzin voor versleuteling is Hallo 'password' toodecrypt Hallo gegevens op Hallo moment van terugzetten. Het is belangrijk tookeep deze gegevens veilig en beveiligd als deze eenmaal is ingesteld.

In volgende Hallo voorbeeld wordt de eerste opdracht Hallo converteert Hallo ```passphrase123456789``` tooa veilige tekenreeks en wijst Hallo veilige tekenreeks toohello variabele met de naam ```$Passphrase```. de tweede opdracht Hallo Hallo veilige tekenreeks wordt ingesteld in ```$Passphrase``` Hallo wachtwoord voor het versleutelen van back-ups.

```
PS C:\> $Passphrase = ConvertTo-SecureString -string "passphrase123456789" -AsPlainText -Force

PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -EncryptionPassphrase $Passphrase
```

> [!IMPORTANT]
> Hallo wachtwoordzin gegevens veilig en beveiligd houden als deze eenmaal is ingesteld. U zich niet kunnen toorestore gegevens van Azure zonder deze wachtwoordzin.
>
>

Op dit moment moet aangebracht alle Hallo vereist wijzigingen toohello ```$setting``` object. Houd er rekening mee toocommit Hallo wijzigingen.

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="protect-data-tooazure-backup"></a>Gegevens tooAzure back-up beveiligen
In deze sectie maakt u een server productie tooDPM toevoegen en Beveilig vervolgens toolocal Hallo-DPM gegevensopslag en vervolgens tooAzure back-up. In de voorbeelden hello wordt gedemonstreerd hoe tooback van bestanden en mappen. Hallo logica kan eenvoudig worden uitgebreide toobackup elke DPM-ondersteunde gegevensbron. Alle DPM--ups worden geregeld door een Protection Group (PG) met vier onderdelen:

1. **Leden** is een lijst van alle beveiligbare objecten voor hello (ook wel bekend als *gegevensbronnen* in DPM) dat u wilt dat tooprotect in Hallo dezelfde beveiligingsgroep. U kunt bijvoorbeeld tooprotect productie, virtuele machines in een beveiligingsgroep en SQL Server-databases in een andere beveiligingsgroep als ze mogelijk andere back-upvereisten heeft. Voordat u kunt back-up elke gegevensbron op een productieserver moet u ervoor Hallo toomake DPM-Agent op Hallo-server is geïnstalleerd en wordt beheerd door DPM. Volg de stappen voor Hallo [DPM-Agent installeren Hallo](https://technet.microsoft.com/library/bb870935.aspx) en het koppelen van toohello DPM-Server nodig.
2. **Methode voor gegevensbeveiliging** geeft Hallo back-up doellocaties - tape, schijf- en cloud. In ons voorbeeld beveiligen we gegevens toohello lokale schijf en toohello cloud.
3. Een **back-upschema** die aangeeft wanneer back-ups moeten toobe genomen en hoe vaak hello gegevens moeten worden gesynchroniseerd tussen Hallo DPM-Server en Hallo productieserver.
4. Een **bewaarschema** die aangeeft hoe lang tooretain Hallo herstelpunten in Azure.

### <a name="creating-a-protection-group"></a>Een beveiligingsgroep maken
Eerst maakt u een nieuwe beveiligingsgroep met Hallo [nieuw DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) cmdlet.

```
PS C:\> $PG = New-DPMProtectionGroup -DPMServerName " TestingServer " -Name "ProtectGroup01"
```

Hallo hierboven cmdlet maakt een beveiligingsgroep met de naam *ProtectGroup01*. Een bestaande beveiligingsgroep kan ook later tooadd back-toohello Azure-cloud worden gewijzigd. Echter toomake wijzigingen toohello beveiligingsgroep - nieuwe of bestaande - moeten we tooget een koppeling op een *bewerkbaar* -object op met de Hallo [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) cmdlet.

```
PS C:\> $MPG = Get-ModifiableProtectionGroup $PG
```

### <a name="adding-group-members-toohello-protection-group"></a>Groep leden toohello beveiligingsgroep toevoegen
Elke DPM-Agent kent Hallo-lijst van gegevensbronnen op Hallo van server waarop deze is geïnstalleerd. tooadd een datasource-toohello beveiligingsgroep, Hallo DPM-Agent behoeften toofirst verzend een lijst van Hallo gegevensbronnen back toohello DPM-server. Een of meer gegevensbronnen zijn geselecteerd en toohello beveiligingsgroep toegevoegd. Hallo PowerShell stappen die nodig zijn tooget bereiken hiervan zijn:

1. Haal een lijst met alle servers die door DPM wordt beheerd via Hallo DPM-Agent.
2. Kies een specifieke server.
3. Haal een lijst van alle gegevensbronnen op Hallo-server.
4. Kies een of meer gegevensbronnen en toohello beveiligingsgroep toevoegen

Hallo-lijst met servers op welke Hallo DPM-Agent is geïnstalleerd en wordt beheerd door Hallo DPM-Server wordt verkregen door hello [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) cmdlet. In dit voorbeeld wordt filteren en alleen PS configureren met de naam *productionserver01* voor back-up.

```
PS C:\> $server = Get-ProductionServer -DPMServerName "TestingServer" | where {($_.servername) –contains “productionserver01”
```

Nu ophalen Hallo-lijst van gegevensbronnen op ```$server``` met Hallo [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605) cmdlet. In dit voorbeeld zijn er filteren voor Hallo volume * D:\* die we willen tooconfigure voor back-up. Deze gegevensbron wordt vervolgens toegevoegd aan toohello beveiligingsgroep met Hallo [toevoegen DPMChildDatasource](https://technet.microsoft.com/library/hh881732) cmdlet. Houd er rekening mee toouse hello *modifable* protection group-object ```$MPG``` toomake Hallo toevoegingen.

```
PS C:\> $DS = Get-Datasource -ProductionServer $server -Inquire | where { $_.Name -contains “D:\” }

PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS
```

Herhaal deze stap zo vaak als nodig is, totdat u alle Hallo gekozen gegevensbronnen toohello beveiligingsgroep hebt toegevoegd. U kunt ook starten met slechts één gegevensbron en volledige Hallo-werkstroom voor het maken van Hallo beveiligingsgroep en voeg meer gegevensbronnen toohello beveiligingsgroep op een later tijdstip.

### <a name="selecting-hello-data-protection-method"></a>Hallo-methode voor gegevensbeveiliging selecteren
Zodra het Hallo-gegevensbronnen zijn toegevoegd toohello beveiligingsgroep, de volgende stap Hallo methode voor gegevensbeveiliging van toospecify Hallo Hallo met is [Set DPMProtectionType](https://technet.microsoft.com/library/hh881725) cmdlet. In dit voorbeeld wordt Hallo beveiligingsgroep worden ingesteld voor de lokale schijf en de cloud back-up. U moet ook toospecify Hallo gegevensbron die u wilt dat tooprotect toocloud met Hallo [toevoegen DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) cmdlet uit met - Online vlag.

```
PS C:\> Set-DPMProtectionType -ProtectionGroup $MPG -ShortTerm Disk –LongTerm Online
PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS –Online
```

### <a name="setting-hello-retention-range"></a>Hallo bewaartermijn instellen
Hallo bewaartermijn voor de back-uppunten Hallo Hallo met ingesteld [Set DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet. Terwijl kan het lijken alsof oneven tooset Hallo bewaren voordat de back-upschema Hallo is gedefinieerd, met behulp van Hallo ```Set-DPMPolicyObjective``` cmdlet stelt automatisch een standaard back-upschema die vervolgens kan worden gewijzigd. Het is altijd mogelijk tooset Hallo back-upschema eerst en Hallo bewaarbeleid na.

In onderstaande Hallo voorbeeld stelt Hallo cmdlet Hallo bewaren parameters voor back-ups van schijf. Dit, back-ups behouden voor 10 dagen en gegevens synchroniseren om de 6 uur tussen Hallo productieserver en Hallo DPM-server. Hallo ```SynchronizationFrequencyMinutes``` bevat geen definitie van hoe vaak een back-up is gemaakt, maar hoe vaak gegevens gekopieerde toohello DPM-server; zo voorkomt u dat back-ups te groot.

```
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -RetentionRangeInDays 10 -SynchronizationFrequencyMinutes 360
```

Hallo bewaartermijnen voor back-ups gaat tooAzure (DPM verwijst toothese als Online back-ups) kunnen worden geconfigureerd voor [langdurig bewaren volgens een schema opa-vader-zoon (algemene)](backup-azure-backup-cloud-as-tape.md). Dat wil zeggen, kunt u een gecombineerde bewaarbeleid met betrekking tot dagelijks, wekelijks, maandelijks en jaarlijks bewaarbeleid definiëren. In dit voorbeeld wordt een matrix die vertegenwoordigt Hallo complexe bewaarschema die we willen maken en configureer vervolgens bewaartermijn Hallo Hallo met [Set DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.

```
PS C:\> $RRlist = @()
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 180, Days)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 104, Weeks)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 60, Month)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 10, Years)
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -OnlineRetentionRangeList $RRlist
```

### <a name="set-hello-backup-schedule"></a>Set Hallo back-upschema
DPM een back-upschema standaard automatisch ingesteld als u de doelstelling van het Hallo-beveiliging met Hallo opgeeft ```Set-DPMPolicyObjective``` cmdlet. toochange hello standaardplanningen, gebruik Hallo [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet gevolgd door Hallo [Set DPMPolicySchedule](https://technet.microsoft.com/library/hh881723) cmdlet.

```
PS C:\> $onlineSch = Get-DPMPolicySchedule -ProtectionGroup $mpg -LongTerm Online
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[0] -TimesOfDay 02:00
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[1] -TimesOfDay 02:00 -DaysOfWeek Sa,Su –Interval 1
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[2] -TimesOfDay 02:00 -RelativeIntervals First,Third –DaysOfWeek Sa
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[3] -TimesOfDay 02:00 -DaysOfMonth 2,5,8,9 -Months Jan,Jul
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```

In vorige Hallo voorbeeld ```$onlineSch``` is een matrix met vier elementen met Hallo bestaande online beveiligingsschema voor Hallo beveiligingsgroep in Hallo algemene schema:

1. ```$onlineSch[0]```Hallo dagelijks schema bevat
2. ```$onlineSch[1]```Hallo wekelijks schema bevat
3. ```$onlineSch[2]```bevat Hallo maandelijks schema
4. ```$onlineSch[3]```Hallo jaarlijkse planning bevat

Dus als u toomodify Hallo wekelijkse planning moet, u toorefer toohello moet ```$onlineSch[1]```.

### <a name="initial-backup"></a>Eerste back-up
Back-ups van een gegevensbron voor Hallo eerst, moet DPM toocreate een eerste replica die u een kopie van Hallo datasource toobe beveiligd op de DPM-replicavolume maakt. Deze activiteit kunnen ofwel worden gepland voor een bepaald tijdstip of handmatig kan worden geactiveerd, met behulp van Hallo [Set DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) cmdlet met de parameter Hallo ```-NOW```.

```
PS C:\> Set-DPMReplicaCreationMethod -ProtectionGroup $MPG -NOW
```
### <a name="changing-hello-size-of-dpm-replica--recovery-point-volume"></a>Grootte van de DPM-Replica en herstelpuntvolume van Hallo wijzigen
U kunt ook wijzigen Hallo grootte van de DPM-replicavolume, evenals een gebruik van de volume Shadow Copy [Set DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) cmdlet zoals in Hallo onderstaand voorbeeld: Get-DatasourceDiskAllocation - Datasource $DS Set-DatasourceDiskAllocation - Datasource $DS - ProtectionGroup $MPG-handmatige - ReplicaArea (2 gb) - ShadowCopyArea (2 gb)

### <a name="committing-hello-changes-toohello-protection-group"></a>Beveiligingsgroep de toohello Hallo wijzigingen doorvoeren
Ten slotte moeten Hallo wijzigingen toobe voordat DPM Hallo back-up per Hallo nieuwe beveiligingsgroep configuratie kan worden toegewezen. Dit wordt gedaan met behulp van Hallo [Set DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) cmdlet.

```
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```
## <a name="view-hello-backup-points"></a>Weergave Hallo back-punten
U kunt Hallo [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) tooget cmdlet een lijst van alle herstelpunten voor een datasource. In dit voorbeeld wordt:

* alle Hallo PGs op Hallo DPM-server die worden opgeslagen in een matrix ophalen```$PG```
* Hallo gegevensbronnen bijbehorende toohello ophalen```$PG[0]```
* alle Hallo herstelpunten voor een gegevensbron niet ophalen.

```
PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online
```

## <a name="restore-data-protected-on-azure"></a>Herstellen van gegevens die zijn beveiligd op Azure
Herstellen van gegevens is een combinatie van een ```RecoverableItem``` object en een ```RecoveryOption``` object. In de vorige sectie hello wij een lijst met back-uppunten Hallo voor een datasource.

In Hallo onderstaande voorbeeld ziet u hoe toorestore een Hyper-V virtuele machine van Azure Backup door back-uppunten combineren met Hallo als doel voor herstel. Dit omvat:

* Maken van een hersteloptie Hallo met [nieuw DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) cmdlet.
* Ophalen Hallo-matrix van back-punten met Hallo ```Get-DPMRecoveryPoint``` cmdlet.
* Een back-punt toorestore uit te kiezen.

```
PS C:\> $RecoveryOption = New-DPMRecoveryOption -HyperVDatasource -TargetServer "HVDCenter02" -RecoveryLocation AlternateHyperVServer -RecoveryType Recover -TargetLocation “C:\VMRecovery”

PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online

PS C:\> Restore-DPMRecoverableItem -RecoverableItem $RecoveryPoints[0] -RecoveryOption $RecoveryOption
```

Hallo-opdrachten kunnen gemakkelijk worden uitgebreid voor elk gegevensbrontype.

## <a name="next-steps"></a>Volgende stappen
* Zie voor meer informatie over Azure Backup voor DPM [inleiding tooDPM back-up](backup-azure-dpm-introduction.md)
