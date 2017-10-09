---
title: aaaDeploy hello Site Recovery Mobility-service met Azure Automation DSC | Microsoft Docs
description: Beschrijft hoe toouse Azure Automation DSC tooautomatically hello Azure Site Recovery Mobility-service en Azure-agent implementeren voor VM VMware en fysieke server replicatie tooAzure
services: site-recovery
documentationcenter: 
author: krnese
manager: lorenr
editor: 
ms.assetid: 1f8cd3ac-0522-48eb-a5f0-679ee9192ddb
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: krnese
ms.openlocfilehash: 52cdd13ceb61718a21137180c55db86919af5929
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-mobility-service-with-azure-automation-dsc-for-replication-of-vm"></a>Hallo Mobility-service met Azure Automation DSC voor replicatie van de virtuele machine implementeren
In de Operations Management Suite bieden wij u met een uitgebreide back-up en noodherstel die u als onderdeel van uw bedrijfscontinuïteitsplan kunt gebruiken.

We deze reis samen met Hyper-V gestart met behulp van Hyper-V Replica. Maar er is uitgevouwen toosupport een heterogene setup omdat klanten hebben van meerdere hypervisors en platforms in hun clouds.

Als u VMware werkbelastingen en/of fysieke servers vandaag, een beheerserver wordt uitgevoerd alle hello Azure Site Recovery-onderdelen in uw omgeving toohandle Hallo communicatie- en replicatie met Azure, als Azure de bestemming is.

## <a name="deploy-hello-site-recovery-mobility-service-by-using-automation-dsc"></a>Hallo Site Recovery Mobility-service implementeren met behulp van Automation DSC
Laten we beginnen als volgt een snel overzicht van de werking van deze beheerserver.

Hallo-beheerserver wordt uitgevoerd voor verschillende serverfuncties. Een van deze functies is *configuratie*, die coördineert de communicatie en processen voor replicatie en herstel van gegevens beheert.

Bovendien Hallo *proces* rol fungeert als replicatiegateway. Deze rol ontvangt replicatiegegevens van beveiligde bronmachines, optimaliseert met caching, compressie en codering en stuurt vervolgens tooan Azure storage-account. Een van de functies voor Hallo Procesrol Hallo is ook toopush installatie van de machines tooprotected Hallo Mobility-service en uitvoeren van automatische detectie van virtuele VMware-machines.

Als er een failback vanuit Azure, Hallo *hoofddoel* rol Hallo replicatiegegevens als onderdeel van deze bewerking wordt afgehandeld.

Voor Hallo beveiligde machines moeten we afhankelijk zijn van Hallo *Mobility-service*. Dit onderdeel is geïmplementeerde tooevery machine (VM VMware of fysieke server) die u wilt dat tooreplicate tooAzure. Deze gegevens schrijfbewerkingen op Hallo machine vastgelegd en stuurt ze toohello managementserver (Procesrol).

Wanneer u de bedrijfscontinuïteit betreft bent, is het belangrijk toounderstand uw werkbelastingen, uw infrastructuur en Hallo onderdelen betrokken. U kunt vervolgens voldoen aan Hallo-vereisten voor uw beoogde hersteltijd (RTO) en een beoogd herstelpunt (RPO). In deze context Hallo Mobility-service is sleutel tooensuring die uw workloads worden beveiligd, zoals u zou verwachten.

Hoe kunt u, op een geoptimaliseerde manier ervoor zorgen dat u een betrouwbare beveiligde ingesteld met behulp van een aantal onderdelen van Operations Management Suite hebt?

In dit artikel bevat een voorbeeld van hoe u Azure Automation Desired State Configuration (DSC), samen met de Site is hersteld, tooensure kunt die:

* Hallo Mobility-service en Azure VM-agent zijn geïmplementeerde toohello Windows-machines dat u wilt dat tooprotect.
* Hallo Mobility-service en Azure VM-agent worden altijd uitgevoerd als Azure Hallo replicatiedoel.

## <a name="prerequisites"></a>Vereisten
* Een opslagplaats toostore Hallo vereiste installatie
* Een opslagplaats toostore Hallo vereist wachtwoordzin tooregister met Hallo managementserver

  > [!NOTE]
  > Een unieke wachtwoordzin wordt gegenereerd voor elke beheerserver. Als u toodeploy meerdere beheerservers gaat, hebt u tooensure die Hallo juist wachtwoordzin in Hallo passphrase.txt bestand is opgeslagen.
  >
  >
* Windows Management Framework (WMF) 5.0 is geïnstalleerd op Hallo-machines wilt u tooenable voor beveiliging (een vereiste voor Automation DSC)

  > [!NOTE]
  > Als u wilt dat toouse DSC voor Windows-machines waarvoor WMF 4.0 is geïnstalleerd, raadpleegt u Hallo sectie [gebruik DSC in niet-verbonden omgevingen](## Use DSC in disconnected environments).
  

Hallo Mobility-service kan worden geïnstalleerd via de opdrachtregel Hallo en verschillende argumenten. Daarom wordt u toohave Hallo binaire bestanden (nadat ze het uitpakken van uw instellingen) nodig hebt en deze opslaan op een locatie waar u ze met behulp van een DSC-configuratie kunt terugvinden.

## <a name="step-1-extract-binaries"></a>Stap 1: De binaire bestanden uitpakken
1. tooextract hello bestanden die u nodig hebt om deze installatie bladeren toohello directory op de beheerserver te volgen:

    **\Microsoft azure Site Recovery\home\svsystems\pushinstallsvc\repository**

    In deze map ziet u een MSI-bestand met de naam:

    **Microsoft ASR_UA_version_Windows_GA_date_Release.exe**

    Hallo opdracht tooextract Hallo installatieprogramma volgende gebruiken:

    **.\Microsoft-ASR_UA_9.1.0.0_Windows_GA_02May2016_release.exe /q /x:C:\Users\Administrator\Desktop\Mobility_Service\Extract**
2. Selecteer alle bestanden en verzend deze tooa gecomprimeerde map.

U hebt nu Hallo binaire bestanden moet u tooautomate Hallo setup Hallo Mobility-service met behulp van Automation DSC.

### <a name="passphrase"></a>Wachtwoordzin
Vervolgens moet u toodetermine waar u tooplace deze gecomprimeerde map. U kunt een Azure storage-account gebruiken als weergegeven hoger toostore Hallo wachtwoordzin die u nodig hebt voor Hallo setup. Hallo-agent wordt vervolgens registreren met Hallo managementserver als onderdeel van het Hallo-proces.

Hallo wachtwoordzin die u hebt verkregen tijdens de implementatie van de beheerserver Hallo kan tooa tekstbestand als passphrase.txt worden opgeslagen.

Zowel de gecomprimeerde map Hallo en Hallo wachtwoordzin plaatsen in een specifieke container in hello Azure storage-account.

![Locatie van de map](./media/site-recovery-automate-mobilitysevice-install/folder-and-passphrase-location.png)

Als u liever tookeep deze bestanden op een share op uw netwerk, kunt u dit doet. U hoeft alleen maar tooensure dat Hallo DSC-resource die u later gaat gebruiken toegang heeft en Hallo setup en wachtwoordzin krijgt.

## <a name="step-2-create-hello-dsc-configuration"></a>Stap 2: Maak Hallo DSC-configuratie
Hallo-installatie, is afhankelijk van WMF 5.0. Hallo machine toosuccessfully toepassing hello configuratie via Automation DSC, WMF 5.0 moet toobe aanwezig.

Hallo-omgeving maakt gebruik van Hallo voorbeeld DSC-configuratie te volgen:

```powershell
configuration ASRMobilityService {

    $RemoteFile = 'https://knrecstor01.blob.core.windows.net/asr/ASR.zip'
    $RemotePassphrase = 'https://knrecstor01.blob.core.windows.net/asr/passphrase.txt'
    $RemoteAzureAgent = 'http://go.microsoft.com/fwlink/p/?LinkId=394789'
    $LocalAzureAgent = 'C:\Temp\AzureVmAgent.msi'
    $TempDestination = 'C:\Temp\asr.zip'
    $LocalPassphrase = 'C:\Temp\Mobility_service\passphrase.txt'
    $Role = 'Agent'
    $Install = 'C:\Program Files (x86)\Microsoft Azure Site Recovery'
    $CSEndpoint = '10.0.0.115'
    $Arguments = '/Role "{0}" /InstallLocation "{1}" /CSEndpoint "{2}" /PassphraseFilePath "{3}"' -f $Role,$Install,$CSEndpoint,$LocalPassphrase

    Import-DscResource -ModuleName xPSDesiredStateConfiguration

    node localhost {

        File Directory {
            DestinationPath = 'C:\Temp\ASRSetup\'
            Type = 'Directory'            
        }

        xRemoteFile Setup {
            URI = $RemoteFile
            DestinationPath = $TempDestination
            DependsOn = '[File]Directory'
        }

        xRemoteFile Passphrase {
            URI = $RemotePassphrase
            DestinationPath = $LocalPassphrase
            DependsOn = '[File]Directory'
        }

        xRemoteFile AzureAgent {
            URI = $RemoteAzureAgent
            DestinationPath = $LocalAzureAgent
            DependsOn = '[File]Directory'
        }

        Archive ASRzip {
            Path = $TempDestination
            Destination = 'C:\Temp\ASRSetup'
            DependsOn = '[xRemotefile]Setup'
        }

        Package Install {
            Path = 'C:\temp\ASRSetup\ASR\UNIFIEDAGENT.EXE'
            Ensure = 'Present'
            Name = 'Microsoft Azure Site Recovery mobility Service/Master Target Server'
            ProductId = '275197FC-14FD-4560-A5EB-38217F80CBD1'
            Arguments = $Arguments
            DependsOn = '[Archive]ASRzip'
        }

        Package AzureAgent {
            Path = 'C:\Temp\AzureVmAgent.msi'
            Ensure = 'Present'
            Name = 'Windows Azure VM Agent - 2.7.1198.735'
            ProductId = '5CF4D04A-F16C-4892-9196-6025EA61F964'
            Arguments = '/q /l "c:\temp\agentlog.txt'
            DependsOn = '[Package]Install'
        }

        Service ASRvx {
            Name = 'svagents'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service ASR {
            Name = 'InMage Scout Application Service'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service AzureAgentService {
            Name = 'WindowsAzureGuestAgent'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }

        Service AzureTelemetry {
            Name = 'WindowsAzureTelemetryService'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }
    }
}
```
Hallo configuratie doet Hallo volgende:

* Hallo variabelen vertelt Hallo-configuratie waarbij tooget Hallo binaire bestanden voor Hallo Mobility-service en hello Azure VM-agent, waarbij tooget Hallo wachtwoordzin en toostore Hallo uitvoer.
* Hallo configuratie importeert Hallo xPSDesiredStateConfiguration DSC-resource, zodat u kunt `xRemoteFile` toodownload Hallo bestanden uit de opslagplaats Hallo.
* Hallo configuratie maakt een map waar u toostore Hallo binaire bestanden.
* Hallo archief resource wordt Hallo-bestanden in Hallo gecomprimeerde map uitpakken.
* Hallo-pakket installeren resource installeren uit Hallo UNIFIEDAGENT Hallo Mobility-service. EXE-installatieprogramma met specifieke Hallo-argumenten. (Hallo variabelen die Hallo argumenten samenstellen moeten toobe gewijzigd tooreflect uw omgeving.)
* Hallo pakket AzureAgent resource installeert hello Azure VM-agent, die wordt aanbevolen voor elke virtuele machine die wordt uitgevoerd in Azure. Hello Azure VM-agent maakt het ook mogelijk tooadd extensies toohello VM na een failover.
* Hallo zorgt service of meer resources ervoor dat Hallo Mobility-services gerelateerde en hello Azure-services worden altijd uitgevoerd.

Hallo configuratie opslaan als **ASRMobilityService**.

> [!NOTE]
> Houd er rekening mee tooreplace hello CSIP in uw configuratie tooreflect Hallo werkelijke-beheerserver, zodat hello agent goed zijn verbonden en het gebruik van de juiste wachtwoordzin Hallo.
>
>

## <a name="step-3-upload-tooautomation-dsc"></a>Stap 3: TooAutomation DSC uploaden
Omdat Hallo DSC-configuratie die u hebt aangebracht, een vereiste resource DSC-module (xPSDesiredStateConfiguration) importeren wordt, moet u tooimport die module in Automation voordat u Hallo DSC-configuratie uploadt.

Meld u aan tooyour Automation-account te bladeren**activa** > **Modules**, en klik op **bladeren galerie**.

Hier kunt u zoeken naar Hallo-module en importeer het tooyour-account.

![Module importeren](./media/site-recovery-automate-mobilitysevice-install/search-and-import-module.png)

Wanneer u klaar bent, gaat u tooyour machine waar u hello Azure Resource Manager-modules geïnstalleerd hebt en doorgaan tooimport Hallo nieuw gemaakte DSC-configuratie.

### <a name="import-cmdlets"></a>Cmdlets voor importeren
Aanmelden in PowerShell tooyour Azure-abonnement. Wijzig Hallo cmdlets tooreflect uw omgeving en uw Automation-accountgegevens in een variabele vastleggen:

```powershell
$AAAccount = Get-AzureRmAutomationAccount -ResourceGroupName 'KNOMS' -Name 'KNOMSAA'
```

Hallo configuratie tooAutomation DSC met behulp van de volgende cmdlet Hallo uploaden:

```powershell
$ImportArgs = @{
    SourcePath = 'C:\ASR\ASRMobilityService.ps1'
    Published = $true
    Description = 'DSC Config for Mobility Service'
}
$AAAccount | Import-AzureRmAutomationDscConfiguration @ImportArgs
```

### <a name="compile-hello-configuration-in-automation-dsc"></a>Hallo-configuratie in Automation DSC compileren
Vervolgens moet u toocompile Hallo configuratie in Automation DSC, zodat u tooregister knooppunten tooit kunt starten. U bereiken die door het uitvoeren van de volgende cmdlet Hallo:

```powershell
$AAAccount | Start-AzureRmAutomationDscCompilationJob -ConfigurationName ASRMobilityService
```

Dit kan enkele minuten duren, omdat u in feite Hallo configuration toohello gehost DSC-pull service implementeert.

Nadat u Hallo configuratie compileren, kunt u Hallo taakinformatie ophalen met behulp van PowerShell (Get-AzureRmAutomationDscCompilationJob) of met behulp van Hallo [Azure-portal](https://portal.azure.com/).

![Taak ophalen](./media/site-recovery-automate-mobilitysevice-install/retrieve-job.png)

U hebt nu gepubliceerd en uw DSC-configuratie tooAutomation DSC geüpload.

## <a name="step-4-onboard-machines-tooautomation-dsc"></a>Stap 4: Vrijgeven machines tooAutomation DSC
> [!NOTE]
> Een van de Hallo-vereisten voor het voltooien van dit scenario is dat uw Windows-machines worden bijgewerkt met de meest recente versie van WMF Hallo. U kunt downloaden en installeer de juiste versie van Hallo voor uw platform van Hallo [Downloadcentrum](https://www.microsoft.com/download/details.aspx?id=50395).
>
>

U maakt nu een metaconfig voor DSC dat u tooyour knooppunten toepast. toosucceed hierbij moet u tooretrieve Hallo eindpunt-URL en Hallo primaire sleutel voor uw geselecteerde Automation-account in Azure. U vindt deze waarden onder **sleutels** op Hallo **alle instellingen** blade voor Hallo Automation-account.

![Sleutelwaarden](./media/site-recovery-automate-mobilitysevice-install/key-values.png)

In dit voorbeeld hebt u een fysieke server van Windows Server 2012 R2 waarop tooprotect met behulp van Site Recovery.

### <a name="check-for-any-pending-file-rename-operations-in-hello-registry"></a>Controleren of er bestandsbewerkingen rename in Hallo register
Voordat u tooassociate Hallo server met Hallo Automation DSC-eindpunt, wordt u aangeraden te controleren of in behandeling zijnde rename bestandsbewerkingen in Hallo-register. Ze mogelijk verbieden Hallo setup is voltooid vanwege tooa opnieuw opstarten.

Voer Hallo cmdlet tooverify er is geen opnieuw opstarten in behandeling op Hallo-server te volgen:

```powershell
Get-ItemProperty 'HKLM:\SYSTEM\CurrentControlSet\Control\Session Manager\' | Select-Object -Property PendingFileRenameOperations
```
Als u dit leeg ziet, bent u OK tooproceed. Als dat niet het geval is, moet u dit oplossen door het Hallo-server opnieuw opstarten tijdens een onderhoudsvenster.

tooapply Hallo-configuratie op Hallo van server, start Hallo PowerShell Integrated Scripting Environment (ISE) en Voer Hallo script volgen. Dit is in wezen een DSC lokale configuratie die Hallo Local Configuration Manager-engine tooregister Hello Automation DSC-service zoekt en Hallo specifieke configuratie (ASRMobilityService.localhost) ophalen.

```powershell
[DSCLocalConfigurationManager()]
configuration metaconfig {
    param (
        $URL,
        $Key
    )
    node localhost {
        Settings {
            RefreshFrequencyMins = '30'
            RebootNodeIfNeeded = $true
            RefreshMode = 'PULL'
            ActionAfterReboot = 'ContinueConfiguration'
            ConfigurationMode = 'ApplyAndMonitor'
            AllowModuleOverwrite = $true
        }

        ResourceRepositoryWeb AzureAutomationDSC {
            ServerURL = $URL
            RegistrationKey = $Key
        }

        ConfigurationRepositoryWeb AzureAutomationDSC {
            ServerURL = $URL
            RegistrationKey = $Key
            ConfigurationNames = 'ASRMobilityService.localhost'
        }

        ReportServerWeb AzureAutomationDSC {
            ServerURL = $URL
            RegistrationKey = $Key
        }
    }
}
metaconfig -URL 'https://we-agentservice-prod-1.azure-automation.net/accounts/<YOURAAAccountID>' -Key '<YOURAAAccountKey>'

Set-DscLocalConfigurationManager .\metaconfig -Force -Verbose
```

Deze configuratie wordt Hallo Local Configuration Manager engine tooregister zelf met Automation DSC. Ook wordt vastgesteld hoe Hallo engine moet worden toegepast, wat dit moet doen als er een configuratie-afwijking (ApplyAndAutoCorrect) en hoe dit moet doorgaan met Hallo configuratie als een herstart vereist is.

Nadat u dit script uitvoert, mag Hallo knooppunt tooregister beginnen met Automation DSC.

![Knooppunt-registratie in voortgang](./media/site-recovery-automate-mobilitysevice-install/register-node.png)

Als u terug toohello Azure-portal gaat, ziet u dat zojuist geregistreerde Hallo-knooppunt is nu verschenen in Hallo-portal.

![Geregistreerde knooppunt in het Hallo-portal](./media/site-recovery-automate-mobilitysevice-install/registered-node.png)

Op Hallo van server, kunt u de volgende PowerShell-cmdlet tooverify die Hallo knooppunt is correct geregistreerd Hallo uitvoeren:

```powershell
Get-DscLocalConfigurationManager
```

Nadat het Hallo-configuratie is opgehaalde en toegepaste toohello server, kunt u dit controleren door het uitvoeren van de volgende cmdlet Hallo:

```powershell
Get-DscConfigurationStatus
```

Hallo-uitvoer ziet dat die Hallo-server heeft de configuratie is opgehaald:

![Uitvoer](./media/site-recovery-automate-mobilitysevice-install/successful-config.png)

Bovendien setup Hallo Mobility-service heeft een eigen logboekbestanden die kan worden gevonden op *SystemDrive*\ProgramData\ASRSetupLogs.

Dat is alles. U hebt nu geïmplementeerd en geregistreerd Hallo Mobility-service op de gewenste tooprotect met behulp van Site Recovery Hallo-machine. DSC ervoor dat er altijd Hallo vereist-services worden uitgevoerd.

![Geslaagde implementatie](./media/site-recovery-automate-mobilitysevice-install/successful-install.png)

Nadat het Hallo-beheerserver detecteert Hallo geslaagde implementatie, kunt u beveiliging configureren en replicatie op Hallo machine inschakelen met behulp van Site Recovery.

## <a name="use-dsc-in-disconnected-environments"></a>Gebruik van DSC in niet-verbonden omgevingen
Als uw machines niet verbonden toohello Internet, kunt u nog steeds zijn afhankelijk van de DSC-toodeploy en Hallo Mobility-service configureren op Hallo werkbelastingen die u tooprotect wilt.

U kunt uw eigen DSC-pull-server in uw omgeving instantiëren tooessentially Hallo bieden dezelfde mogelijkheden die u via Automation DSC. Dat wil zeggen, Hallo clients haalt binnen Hallo-configuratie (nadat deze geregistreerd) toohello DSC-eindpunt. Een andere optie is echter toomanually push Hallo DSC configuration tooyour machines, lokaal of extern.

Houd er rekening mee dat in dit voorbeeld, wordt er een extra parameter voor Hallo-computernaam. Hallo externe bestanden zich nu op een externe share die toegankelijk moet zijn door Hallo-machines dat u wilt dat tooprotect. Hallo-einde van het Hallo-script enacts Hallo-configuratie en start vervolgens tooapply Hallo DSC configuration toohello target-computer.

### <a name="prerequisites"></a>Vereisten
Zorg ervoor dat Hallo xPSDesiredStateConfiguration PowerShell-module is geïnstalleerd. Voor Windows-computers waarop WMF 5.0 wordt geïnstalleerd, kunt u Hallo xPSDesiredStateConfiguration module installeren door het uitvoeren van de volgende cmdlet op de doelmachines Hallo Hallo:

```powershell
Find-Module -Name xPSDesiredStateConfiguration | Install-Module
```

U kunt ook downloaden en opslaan Hallo-module voor het geval u toodistribute moet het tooWindows machines waarvoor WMF 4.0. Deze cmdlet uitvoeren op een machine waarin PowerShellGet (WMF 5.0) aanwezig is:

```powershell
Save-Module -Name xPSDesiredStateConfiguration -Path <location>
```

Zorg er ook voor WMF 4.0 die Hallo [update voor Windows 8.1 KB2883200](https://www.microsoft.com/download/details.aspx?id=40749) op Hallo computers is geïnstalleerd.

Hallo kan volgende configuratie worden geactiveerd tooWindows machines waarvoor WMF 5.0 en WMF 4.0:

```powershell
configuration ASRMobilityService {
    param (
        [Parameter(Mandatory=$true)]
        [ValidateNotNullOrEmpty()]
        [System.String] $ComputerName
    )

    $RemoteFile = '\\myfileserver\share\asr.zip'
    $RemotePassphrase = '\\myfileserver\share\passphrase.txt'
    $RemoteAzureAgent = '\\myfileserver\share\AzureVmAgent.msi'
    $LocalAzureAgent = 'C:\Temp\AzureVmAgent.msi'
    $TempDestination = 'C:\Temp\asr.zip'
    $LocalPassphrase = 'C:\Temp\Mobility_service\passphrase.txt'
    $Role = 'Agent'
    $Install = 'C:\Program Files (x86)\Microsoft Azure Site Recovery'
    $CSEndpoint = '10.0.0.115'
    $Arguments = '/Role "{0}" /InstallLocation "{1}" /CSEndpoint "{2}" /PassphraseFilePath "{3}"' -f $Role,$Install,$CSEndpoint,$LocalPassphrase

    Import-DscResource -ModuleName xPSDesiredStateConfiguration

    node $ComputerName {      
        File Directory {
            DestinationPath = 'C:\Temp\ASRSetup\'
            Type = 'Directory'            
        }

        xRemoteFile Setup {
            URI = $RemoteFile
            DestinationPath = $TempDestination
            DependsOn = '[File]Directory'
        }

        xRemoteFile Passphrase {
            URI = $RemotePassphrase
            DestinationPath = $LocalPassphrase
            DependsOn = '[File]Directory'
        }

        xRemoteFile AzureAgent {
            URI = $RemoteAzureAgent
            DestinationPath = $LocalAzureAgent
            DependsOn = '[File]Directory'
        }

        Archive ASRzip {
            Path = $TempDestination
            Destination = 'C:\Temp\ASRSetup'
            DependsOn = '[xRemotefile]Setup'
        }

        Package Install {
            Path = 'C:\temp\ASRSetup\ASR\UNIFIEDAGENT.EXE'
            Ensure = 'Present'
            Name = 'Microsoft Azure Site Recovery mobility Service/Master Target Server'
            ProductId = '275197FC-14FD-4560-A5EB-38217F80CBD1'
            Arguments = $Arguments
            DependsOn = '[Archive]ASRzip'
        }

        Package AzureAgent {
            Path = 'C:\Temp\AzureVmAgent.msi'
            Ensure = 'Present'
            Name = 'Windows Azure VM Agent - 2.7.1198.735'
            ProductId = '5CF4D04A-F16C-4892-9196-6025EA61F964'
            Arguments = '/q /l "c:\temp\agentlog.txt'
            DependsOn = '[Package]Install'
        }

        Service ASRvx {
            Name = 'svagents'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service ASR {
            Name = 'InMage Scout Application Service'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service AzureAgentService {
            Name = 'WindowsAzureGuestAgent'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }

        Service AzureTelemetry {
            Name = 'WindowsAzureTelemetryService'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }
    }
}
ASRMobilityService -ComputerName 'MyTargetComputerName'

Start-DscConfiguration .\ASRMobilityService -Wait -Force -Verbose
```

Als u uw eigen DSC-pull-server tooinstantiate op uw bedrijfsnetwerk toomimic Hallo mogelijkheden u krijgen via Automation DSC wilt kunt, Zie [instellen van een DSC-webserver pull](https://msdn.microsoft.com/powershell/dsc/pullserver?f=255&MSPPError=-2147217396).

## <a name="optional-deploy-a-dsc-configuration-by-using-an-azure-resource-manager-template"></a>Optioneel: Een DSC-configuratie met behulp van een Azure Resource Manager-sjabloon implementeren
In dit artikel is gericht op hoe u uw eigen tooautomatically DSC-configuratie kunt maken implementeren Hallo Mobility-service en hello Azure VM-Agent-- en ervoor te zorgen dat ze worden uitgevoerd op Hallo machines dat u wilt dat tooprotect. We hebben ook een Azure Resource Manager-sjabloon die u deze DSC-configuratie tooa nieuwe of bestaande Azure Automation-account implementeert. Hallo-sjabloon gebruikt invoerparameters toocreate Automation activa met Hallo variabelen voor uw omgeving.

Nadat u de sjabloon Hallo implementeert, kunt u gewoon verwijzen toostep 4 in deze handleiding tooonboard uw machines.

Hallo-sjabloon wordt gedaan Hallo volgende:

1. Gebruik een bestaand automatiseringsaccount of een nieuwe maken
2. Invoerparameters voor nemen:
   * ASRRemoteFile--Hallo-locatie waar u Hallo Mobility-service-instellingen hebt opgeslagen
   * ASRPassphrase--Hallo-locatie waar u Hallo passphrase.txt bestand hebt opgeslagen
   * ASRCSEndpoint--Hallo IP-adres van de beheerserver
3. Hallo xPSDesiredStateConfiguration PowerShell-module importeren
4. Maken en Hallo DSC-configuratie compileren

Alle Hallo vorige stappen vindt plaats in de juiste volgorde hello, zodat u uw computers voor beveiliging voor onboarding starten kunt.

Hallo-sjabloon met instructies voor implementatie bevindt zich op [GitHub](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/DSC).

Hallo-sjabloon implementeren met behulp van PowerShell:

```powershell
$RGDeployArgs = @{
    Name = 'DSC3'
    ResourceGroupName = 'KNOMS'
    TemplateFile = 'https://raw.githubusercontent.com/krnese/AzureDeploy/master/OMS/MSOMS/DSC/azuredeploy.json'
    OMSAutomationAccountName = 'KNOMSAA'
    ASRRemoteFile = 'https://knrecstor01.blob.core.windows.net/asr/ASR.zip'
    ASRRemotePassphrase = 'https://knrecstor01.blob.core.windows.net/asr/passphrase.txt'
    ASRCSEndpoint = '10.0.0.115'
    DSCJobGuid = [System.Guid]::NewGuid().ToString()
}
New-AzureRmResourceGroupDeployment @RGDeployArgs -Verbose
```

## <a name="next-steps"></a>Volgende stappen
Nadat u Hallo Mobility service agents implementeert, kunt u [replicatie inschakelen](site-recovery-vmware-to-azure.md) voor Hallo virtuele machines.
