---
title: computers voor beheer door Azure Automation DSC aaaOnboarding | Microsoft Docs
description: Hoe toosetup machines voor beheer met Azure Automation DSC
services: automation
documentationcenter: dev-center-name
author: eslesar
manager: carmonm
ms.assetid: da13e1f5-2a1c-443b-8e3b-9f0d6f9e4810
ms.service: automation
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: TBD
ms.date: 12/13/2016
ms.author: eslesar
ms.openlocfilehash: ef15801fec2ffea4ba62dcba2fbe9af09268e424
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="onboarding-machines-for-management-by-azure-automation-dsc"></a>Computers voorbereiden voor beheer door Azure Automation DSC

## <a name="why-manage-machines-with-azure-automation-dsc"></a>Waarom machines met een Azure Automation DSC beheren?

Zoals [PowerShell Desired State Configuration](https://technet.microsoft.com/library/dn249912.aspx), Azure Automation Desired State Configuration is een eenvoudige maar krachtige, configuration management-service voor DSC-knooppunten (fysieke en virtuele machines) in een cloud of on-premises datacenter. Hiermee kunt schaalbaarheid in duizenden computers snel en eenvoudig vanuit een centrale, veilige locatie. U kunt eenvoudig vrijgeven machines, toewijzen ze declaratieve configuraties en rapporten weergeven met elk van de computer de compatibiliteitsstatus van toohello gewenst die u hebt opgegeven. Hello Azure Automation DSC-beheerlaag is tooDSC welke hello Azure Automation-beheerlaag is tooPowerShell scripting. Met andere woorden, in Hallo dezelfde manier die u helpt Azure Automation PowerShell-scripts beheren, ook helpt u bij het beheren van DSC-configuraties. Zie toolearn meer informatie over de voordelen van het gebruik van Azure Automation DSC Hallo [overzicht van Azure Automation DSC](automation-dsc-overview.md).

Gebruikte toomanage diverse computers kan worden uitgevoerd met Azure Automation DSC:

* Virtuele machines in Azure (klassiek)
* Virtuele machines van Azure
* Amazon Web Services (AWS) virtuele machines
* Fysiek virtueel Windows machines on-premises of in een cloud dan Azure/AWS
* Fysiek virtueel Linux-machines on-premises in Azure of in een cloud dan Azure

Daarnaast bent u niet klaar toomanage machineconfiguratie vanuit de cloud hello, kan Azure Automation DSC ook worden gebruikt als een eindpunt in het rapport alleen-lezen. Hiermee kunt u de gewenste configuratie tooset (push) via DSC on-premises en uitgebreide rapportage details weergeven over de naleving Hallo knooppunt gewenst status in Azure Automation.

Hallo secties na een overzicht van hoe u vrijgeven elk type machine tooAzure Automation DSC kunt.

## <a name="azure-virtual-machines-classic"></a>Virtuele machines in Azure (klassiek)

Met Azure Automation DSC kunt u eenvoudig vrijgeven virtuele machines in Azure (klassiek) voor Configuratiebeheer met hello Azure-portal of PowerShell. Achter de schermen Hallo en zonder een beheerder met tooremote in Hallo VM registreert hello Azure VM Desired State Configuration-extensie Hallo VM bij Azure Automation DSC. Aangezien hello Azure VM Desired State Configuration extensie asynchroon uitgevoerd, stappen tootrack voortgangsgegevens of het oplossen van deze beschikbaar zijn in Hallo [ **probleemoplossing voor Azure virtuele machine voorbereiden** ](#troubleshooting-azure-virtual-machine-onboarding)hieronder.

### <a name="azure-portal"></a>Azure Portal

In Hallo [Azure-portal](http://portal.azure.com/), klikt u op **Bladeren** -> **virtuele machines (klassiek)**. Selecteer de gewenste tooonboard virtuele machine van Windows hello. Klik op Hallo van de virtuele machine dashboard blade **alle instellingen** -> **extensies** -> **toevoegen**  ->   **Azure Automation DSC** -> **maken**. Voer Hallo [PowerShell DSC Local Configuration Manager-waarden](https://msdn.microsoft.com/powershell/dsc/metaconfig4) vereist is voor uw gebruiksvoorbeeld registratiecode voor uw Automation-account en registratie-URL en eventueel een knooppunt configuratie tooassign toohello VM.

![](./media/automation-dsc-onboarding/DSC_Onboarding_1.png)

toofind Hallo registratie-URL's en -sleutel voor Hallo Automation-account tooonboard Hallo machine, Zie Hallo [ **registratie Secure** ](#secure-registration) hieronder.

### <a name="powershell"></a>PowerShell

```powershell
# log in tooboth Azure Service Management and Azure Resource Manager
Add-AzureAccount
Add-AzureRmAccount

# fill in correct values for your VM/Automation account here
$VMName = ""
$ServiceName = ""
$AutomationAccountName = ""
$AutomationAccountResourceGroup = ""

# fill in hello name of a Node Configuration in Azure Automation DSC, for this VM tooconform to
$NodeConfigName = ""

# get Azure Automation DSC registration info
$Account = Get-AzureRmAutomationAccount -ResourceGroupName $AutomationAccountResourceGroup -Name $AutomationAccountName
$RegistrationInfo = $Account | Get-AzureRmAutomationRegistrationInfo

# use hello DSC extension tooonboard hello VM for management with Azure Automation DSC
$VM = Get-AzureVM -Name $VMName -ServiceName $ServiceName

$PublicConfiguration = ConvertTo-Json -Depth 8 @{
    SasToken = ""
    ModulesUrl = "https://eus2oaasibizamarketprod1.blob.core.windows.net/automationdscpreview/RegistrationMetaConfigV2.zip"
    ConfigurationFunction = "RegistrationMetaConfigV2.ps1\RegistrationMetaConfigV2"

# update these PowerShell DSC Local Configuration Manager defaults if they do not match your use case.
# See https://technet.microsoft.com/library/dn249922.aspx?f=255&MSPPError=-2147217396 for more details
    Properties = @{
    RegistrationKey = @{
        UserName = 'notused'
        Password = 'PrivateSettingsRef:RegistrationKey'
    }
    RegistrationUrl = $RegistrationInfo.Endpoint
    NodeConfigurationName = $NodeConfigName
    ConfigurationMode = "ApplyAndMonitor"
    ConfigurationModeFrequencyMins = 15
    RefreshFrequencyMins = 30
    RebootNodeIfNeeded = $False
    ActionAfterReboot = "ContinueConfiguration"
    AllowModuleOverwrite = $False
    }
}

$PrivateConfiguration = ConvertTo-Json -Depth 8 @{
    Items = @{
        RegistrationKey = $RegistrationInfo.PrimaryKey
    }
}

$VM = Set-AzureVMExtension `
    -VM $vm `
    -Publisher Microsoft.Powershell `
    -ExtensionName DSC `
    -Version 2.19 `
    -PublicConfiguration $PublicConfiguration `
    -PrivateConfiguration $PrivateConfiguration `
    -ForceUpdate

$VM | Update-AzureVM
```

## <a name="azure-virtual-machines"></a>Virtuele machines van Azure

Azure Automation DSC kunt u eenvoudig vrijgeven Azure virtuele machines voor Configuratiebeheer, via hello Azure-portal, Azure Resource Manager-sjablonen of PowerShell. Achter de schermen Hallo en zonder een beheerder met tooremote in Hallo VM registreert hello Azure VM Desired State Configuration-extensie Hallo VM bij Azure Automation DSC. Aangezien hello Azure VM Desired State Configuration extensie asynchroon uitgevoerd, stappen tootrack voortgangsgegevens of het oplossen van deze beschikbaar zijn in Hallo [ **probleemoplossing voor Azure virtuele machine voorbereiden** ](#troubleshooting-azure-virtual-machine-onboarding)hieronder.

### <a name="azure-portal"></a>Azure Portal

In Hallo [Azure-portal](https://portal.azure.com/), navigeer toohello Azure Automation-account waar u tooonboard virtuele machines. Klik op het dashboard van Automation-account bij hello, **DSC-knooppunten** -> **toevoegen Azure VM**.

Onder **tooonboard van virtuele machines selecteren**, selecteer een of meer Azure virtual machines tooonboard.

![](./media/automation-dsc-onboarding/DSC_Onboarding_2.png)

Onder **registratiegegevens configureren**, Voer Hallo [PowerShell DSC Local Configuration Manager-waarden](https://msdn.microsoft.com/powershell/dsc/metaconfig4) vereist zijn voor uw gebruiksvoorbeeld en eventueel een knooppunt configuratie tooassign toohello VM.

![](./media/automation-dsc-onboarding/DSC_Onboarding_3.png)

### <a name="azure-resource-manager-templates"></a>Azure Resource Manager-sjablonen

Azure virtuele machines kunnen worden geïmplementeerd en vrijgegeven tooAzure Automation DSC via Azure Resource Manager-sjablonen. Zie [configureren van een virtuele machine via de DSC-extensie en Azure Automation DSC](https://azure.microsoft.com/documentation/templates/dsc-extension-azure-automation-pullserver/) voor een van de voorbeeldsjabloon die onboards een bestaande VM-tooAzure Automation DSC. toofind hello registratie sleutel en registratie-URL genomen als invoer in deze sjabloon Zie Hallo [ **registratie Secure** ](#secure-registration) hieronder.

### <a name="powershell"></a>PowerShell

Hallo [registreren AzureRmAutomationDscNode](/powershell/module/azurerm.automation/register-azurermautomationdscnode) cmdlet gebruikte tooonboard virtuele machines in Azure portal via PowerShell Hallo kan zijn.

## <a name="amazon-web-services-aws-virtual-machines"></a>Amazon Web Services (AWS) virtuele machines

U kunt eenvoudig vrijgeven Amazon Web Services virtuele machines voor Configuratiebeheer door Azure Automation DSC met Hallo AWS DSC-Toolkit. U kunt meer informatie over Hallo toolkit [hier](https://blogs.msdn.microsoft.com/powershell/2016/04/20/aws-dsc-toolkit/).

## <a name="physicalvirtual-windows-machines-on-premises-or-in-a-cloud-other-than-azureaws"></a>Fysiek virtueel Windows machines on-premises of in een cloud dan Azure/AWS

Lokale Windows-machines en Windows-machines in niet-Azure-clouds (zoals Amazon Web Services) kunnen ook worden vrijgegeven tooAzure Automation DSC zolang ze beschikken over uitgaande toegang toohello internet via een paar eenvoudige stappen:

1. Zorg ervoor dat Hallo meest recente versie van [WMF 5](http://aka.ms/wmf5latest) is geïnstalleerd op Hallo machines gewenste tooonboard tooAzure Automation DSC.
2. Volg de aanwijzingen Hallo in sectie [ **genereren DSC metaconfigurations** ](#generating-dsc-metaconfigurations) hieronder toogenerate map met de Hallo DSC metaconfigurations nodig.
3. Hallo PowerShell DSC-metaconfiguratie toe toohello machines gewenste tooonboard extern toe te passen. **Hallo-machine met deze opdracht wordt uitgevoerd vanaf moet hebben Hallo meest recente versie van [WMF 5](http://aka.ms/wmf5latest) geïnstalleerd**:

    ```powershell
    Set-DscLocalConfigurationManager -Path C:\Users\joe\Desktop\DscMetaConfigs -ComputerName MyServer1, MyServer2
    ```

4. Als u niet op afstand Hallo PowerShell DSC metaconfigurations toepassen, kopieert u Hallo metaconfigurations map uit stap 2 op elke machine tooonboard. Roep vervolgens **Set DscLocalConfigurationManager** lokaal op elke machine tooonboard.
5. Hello Azure-portal of cmdlets, Controleer of de Hallo machines tooonboard nu weergegeven als DSC-knooppunten die zijn geregistreerd in Azure Automation-account gebruiken.

## <a name="physicalvirtual-linux-machines-on-premises-in-azure-or-in-a-cloud-other-than-azure"></a>Fysiek virtueel Linux-machines on-premises in Azure of in een cloud dan Azure

Lokale Linux-machines, Linux-machines in Azure, en Linux-machines in niet-Azure-clouds kunnen ook worden vrijgegeven tooAzure Automation DSC zolang ze beschikken over uitgaande toegang toohello internet via een paar eenvoudige stappen:

1. Zorg ervoor dat Hallo meest recente versie van [PowerShell Desired State Configuration voor Linux](https://github.com/Microsoft/PowerShell-DSC-for-Linux) is geïnstalleerd op Hallo machines gewenste tooonboard tooAzure Automation DSC.
2. Als hello [standaardinstellingen voor PowerShell DSC Local Configuration Manager](https://msdn.microsoft.com/powershell/dsc/metaconfig4) overeenkomen met uw gebruiksvoorbeeld en gewenste tooonboard machines zoals dat zij **beide** halen uit en tooAzure Automation DSC rapporteren:

   + Gebruik op elke Linux machine tooonboard tooAzure Automation DSC, Register.py tooonboard met behulp van PowerShell DSC Local Configuration Manager standaard Hallo:

     `/opt/microsoft/dsc/Scripts/Register.py <Automation account registration key> <Automation account registration URL>`

   + toofind hello registratie sleutel en registratie-URL voor uw Automation-account, Zie Hallo [ **registratie Secure** ](#secure-registration) hieronder.

     Als hello PowerShell DSC Local Configuration Manager standaard **doen** **niet** overeenkomen met uw gebruiksvoorbeeld, of het gewenste tooonboard machines zo dat ze worden alleen tooAzure Automation DSC gerapporteerd, maar niet kunnen ophalen configuratie of het PowerShell-modules, volgt u stap 3-6. Ga anders verder rechtstreeks toostep 6.

3. Volg de aanwijzingen Hallo in Hallo [ **genereren DSC metaconfigurations** ](#generating-dsc-metaconfigurations) sectie hieronder toogenerate map met de Hallo nodig DSC metaconfigurations.
4. Hallo PowerShell DSC-metaconfiguratie toe toohello machines gewenste tooonboard extern toe te passen:

    ```powershell
    $SecurePass = ConvertTo-SecureString -String "<root password>" -AsPlainText -Force
    $Cred = New-Object System.Management.Automation.PSCredential "root", $SecurePass
    $Opt = New-CimSessionOption -UseSsl -SkipCACheck -SkipCNCheck -SkipRevocationCheck

    # need a CimSession for each Linux machine tooonboard

    $Session = New-CimSession -Credential $Cred -ComputerName <your Linux machine> -Port 5986 -Authentication basic -SessionOption $Opt

    Set-DscLocalConfigurationManager -CimSession $Session -Path C:\Users\joe\Desktop\DscMetaConfigs
    ```

Hallo-machine met deze opdracht wordt uitgevoerd vanaf moet hebben Hallo meest recente versie van [WMF 5](http://aka.ms/wmf5latest) geïnstalleerd.

1. Als u geen Hallo PowerShell DSC metaconfigurations op afstand voor elke tooonboard Linux-machine toepassen kopieert u Hallo metaconfiguratie overeenkomstige toothat machine uit de map Hallo in stap 5 op Hallo Linux-machine. Roep vervolgens `SetDscLocalConfigurationManager.py` lokaal op elke Linux-machine u tooonboard tooAzure Automation DSC wilt:

   `/opt/microsoft/dsc/Scripts/SetDscLocalConfigurationManager.py -configurationmof <path toometaconfiguration file>`

2. Hello Azure-portal of cmdlets, Controleer of de Hallo machines tooonboard nu weergegeven als DSC-knooppunten die zijn geregistreerd in Azure Automation-account gebruiken.

## <a name="generating-dsc-metaconfigurations"></a>DSC-metaconfigurations genereren

toogenerically vrijgeven een tooAzure Automation DSC machine een [DSC-metaconfiguratie toe](https://msdn.microsoft.com/en-us/powershell/dsc/metaconfig) kan worden gegenereerd die, wanneer toegepast, vertelt Hallo DSC-agent op Hallo machine toopull uit en/of tooAzure Automation DSC rapporteren. DSC-metaconfigurations voor Azure Automation DSC kan worden gegenereerd met behulp van een PowerShell DSC-configuratie, of hello Azure Automation PowerShell-cmdlets.

> [!NOTE]
> DSC-metaconfigurations bevatten Hallo geheimen nodig tooonboard een machine tooan Automation-account voor beheer. Zorg ervoor dat tooproperly beveiligen eventuele DSC-metaconfigurations die u maakt of verwijder ze na gebruik.

### <a name="using-a-dsc-configuration"></a>Met behulp van een DSC-configuratie

1. Open Hallo PowerShell ISE als beheerder op een virtuele machine in uw lokale omgeving. Hallo-machine moet zijn de meest recente versie Hallo van [WMF 5](http://aka.ms/wmf5latest) geïnstalleerd.
2. Kopieer Hallo script lokaal te volgen. Dit script bevat een PowerShell DSC-configuratie voor het maken van metaconfigurations en een opdracht tookick uit Hallo metaconfiguratie maken.

    ```powershell
    # hello DSC configuration that will generate metaconfigurations
    [DscLocalConfigurationManager()]
    Configuration DscMetaConfigs
    {

        param
        (
            [Parameter(Mandatory=$True)]
            [String]$RegistrationUrl,

            [Parameter(Mandatory=$True)]
            [String]$RegistrationKey,

            [Parameter(Mandatory=$True)]
            [String[]]$ComputerName,

            [Int]$RefreshFrequencyMins = 30,

            [Int]$ConfigurationModeFrequencyMins = 15,

            [String]$ConfigurationMode = "ApplyAndMonitor",

            [String]$NodeConfigurationName,

            [Boolean]$RebootNodeIfNeeded= $False,

            [String]$ActionAfterReboot = "ContinueConfiguration",

            [Boolean]$AllowModuleOverwrite = $False,

            [Boolean]$ReportOnly
        )

        if(!$NodeConfigurationName -or $NodeConfigurationName -eq "")
        {
            $ConfigurationNames = $null
        }
        else
        {
            $ConfigurationNames = @($NodeConfigurationName)
        }

        if($ReportOnly)
        {
        $RefreshMode = "PUSH"
        }
        else
        {
        $RefreshMode = "PULL"
        }

        Node $ComputerName
        {

            Settings
            {
                RefreshFrequencyMins = $RefreshFrequencyMins
                RefreshMode = $RefreshMode
                ConfigurationMode = $ConfigurationMode
                AllowModuleOverwrite = $AllowModuleOverwrite
                RebootNodeIfNeeded = $RebootNodeIfNeeded
                ActionAfterReboot = $ActionAfterReboot
                ConfigurationModeFrequencyMins = $ConfigurationModeFrequencyMins
            }

            if(!$ReportOnly)
            {
            ConfigurationRepositoryWeb AzureAutomationDSC
                {
                    ServerUrl = $RegistrationUrl
                    RegistrationKey = $RegistrationKey
                    ConfigurationNames = $ConfigurationNames
                }

                ResourceRepositoryWeb AzureAutomationDSC
                {
                ServerUrl = $RegistrationUrl
                RegistrationKey = $RegistrationKey
                }
            }

            ReportServerWeb AzureAutomationDSC
            {
                ServerUrl = $RegistrationUrl
                RegistrationKey = $RegistrationKey
            }
        }
    }

    # Create hello metaconfigurations
    # TODO: edit hello below as needed for your use case
    $Params = @{
        RegistrationUrl = '<fill me in>';
        RegistrationKey = '<fill me in>';
        ComputerName = @('<some VM tooonboard>', '<some other VM tooonboard>');
        NodeConfigurationName = 'SimpleConfig.webserver';
        RefreshFrequencyMins = 30;
        ConfigurationModeFrequencyMins = 15;
        RebootNodeIfNeeded = $False;
        AllowModuleOverwrite = $False;
        ConfigurationMode = 'ApplyAndMonitor';
        ActionAfterReboot = 'ContinueConfiguration';
        ReportOnly = $False;  # Set too$True toohave machines only report tooAA DSC but not pull from it
    }

    # Use PowerShell splatting toopass parameters toohello DSC configuration being invoked
    # For more info about splatting, run: Get-Help -Name about_Splatting
    DscMetaConfigs @Params
    ```

3. Vul Hallo registratiecode en URL in voor uw Automation-account, evenals de namen van Hallo machines tooonboard Hallo. Alle andere parameters zijn optioneel. toofind hello registratie sleutel en registratie-URL voor uw Automation-account, Zie Hallo [ **registratie Secure** ](#secure-registration) hieronder.
4. Als u Hallo machines tooreport DSC status informatie tooAzure Automation DSC wilt, maar geen pull-configuratie of het PowerShell-modules, stelt u Hallo **ReportOnly** parameter tootrue.
5. Hallo-script uitvoeren. U hebt nu een map met de naam **DscMetaConfigs** die in uw werkmap Hallo PowerShell DSC metaconfigurations voor Hallo machines tooonboard (als administrator):

    ```powershell
    Set-DscLocalConfigurationManager -Path ./DscMetaConfigs
    ```

### <a name="using-hello-azure-automation-cmdlets"></a>Met behulp van hello Azure Automation cmdlets

Als Hallo PowerShell DSC Local Configuration Manager standaardwaarden overeenkomen met uw gebruiksvoorbeeld en u wilt dat tooonboard machines zo dat ze zowel pull van en tooAzure Automation DSC rapporteren, bieden hello Azure Automation cmdlets een vereenvoudigde methode voor het genereren van Hallo DSC metaconfigurations nodig:

1. Open Hallo PowerShell-console of PowerShell ISE als beheerder op een virtuele machine in uw lokale omgeving.
2. Verbinding maken met behulp van tooAzure Resource Manager **Add-AzureRmAccount**
3. Hallo PowerShell DSC metaconfigurations downloaden voor Hallo-machines die u wilt dat tooonboard van Hallo Automation-account toowhich gewenste tooonboard knooppunten:

    ```powershell
    # Define hello parameters for Get-AzureRmAutomationDscOnboardingMetaconfig using PowerShell Splatting
    $Params = @{

        ResourceGroupName = 'ContosoResources'; # hello name of hello ARM Resource Group that contains your Azure Automation Account
        AutomationAccountName = 'ContosoAutomation'; # hello name of hello Azure Automation Account where you want a node on-boarded to
        ComputerName = @('web01', 'web02', 'sql01'); # hello names of hello computers that hello meta configuration will be generated for
        OutputFolder = "$env:UserProfile\Desktop\";
    }
    # Use PowerShell splatting toopass parameters toohello Azure Automation cmdlet being invoked
    # For more info about splatting, run: Get-Help -Name about_Splatting
    Get-AzureRmAutomationDscOnboardingMetaconfig @Params
    ```
    
4. U hebt nu een map met de naam ***DscMetaConfigs***, met Hallo PowerShell DSC metaconfigurations voor Hallo machines tooonboard (als administrator):
    
    ```powershell
    Set-DscLocalConfigurationManager -Path $env:UserProfile\Desktop\DscMetaConfigs
    ```

## <a name="secure-registration"></a>Beveiligde registratie

Machines kunnen veilig on-board tooan Azure Automation-account via Hallo WMF 5 DSC-registratie protocol, waardoor een DSC-knooppunt tooauthenticate tooa Pull-PowerShell DSC V2 of Reporting server (met inbegrip van Azure Automation DSC). Hallo knooppunt registreert toohello server op een **registratie URL**, verificatie uitvoert met behulp van een **registratiesleutel**. Tijdens de registratie Hallo DSC-knooppunt en DSC-Pull/Reporting-server om te onderhandelen over een uniek certificaat voor dit knooppunt toouse voor verificatie toohello server na registratie. Dit proces wordt voorkomen dat de knooppunten van imitatie van een die andere, zoals wanneer een knooppunt is geknoeid en gedragen met kwaadaardige bedoelingen vrijgegeven. Na registratie Hallo registratiesleutel wordt niet gebruikt voor verificatie opnieuw en wordt verwijderd uit het Hallo-knooppunt.

U krijgt Hallo vereiste informatie voor Hallo DSC-registratie protocol van Hallo **sleutels beheren** blade in hello Azure preview-portal. Deze blade openen door te klikken op Hallo sleutelpictogram op Hallo **Essentials** deelvenster voor Hallo Automation-account.

![](./media/automation-dsc-onboarding/DSC_Onboarding_4.png)

* Registratie-URL is Hallo URL veld in de blade sleutels beheren Hallo.
* Registratiecode is Hallo primaire toegangssleutel of secundaire toegangssleutel Hallo sleutels beheren blade. De sleutel kan worden gebruikt.

Voor extra beveiliging Hallo toegang primaire en secundaire sleutels van een Automation-account op elk gewenst moment kunnen worden hersteld (op Hallo **sleutels beheren** blade) tooprevent toekomstige knooppunt registraties met vorige sleutels.

## <a name="troubleshooting-azure-virtual-machine-onboarding"></a>Het voorbereiden van de virtuele machine van Azure oplossen

Azure Automation DSC kunt u eenvoudig Azure Windows VM's vrijgeven voor Configuratiebeheer. Hallo Desired State Configuration van Azure VM-extensie is achter de schermen hello, gebruikte tooregister Hallo VM met Azure Automation DSC. Aangezien hello Azure VM Desired State Configuration-extensie wordt asynchroon uitgevoerd, kunnen de voortgang bijhouden en probleemoplossing van de uitvoering ervan belangrijk zijn.

> [!NOTE]
> Een methode voor het voorbereiden op een tooAzure Windows virtuele machine in Azure Automation DSC die gebruikmaakt van hello Azure VM Desired State Configuration-extensie Hallo knooppunt tooshow up tooan uur duren kan als geregistreerd in Azure Automation. Dit is vanwege toohello installatie van Windows Management Framework 5.0 op Hallo VM door hello Azure VM DSC-extensie, die vereist tooonboard Hallo VM tooAzure Automation DSC is.

tootroubleshoot of weergave Hallo-status van hello Azure VM Desired State Configuration extensie, hello Azure-portal navigeert toohello VM wordt vrijgegeven, vervolgens klikt u op -> **alle instellingen** -> **extensies**   ->  **DSC**. Voor meer informatie kunt u **gedetailleerde status weergeven**.

[![](./media/automation-dsc-onboarding/DSC_Onboarding_5.png)](https://technet.microsoft.com/library/dn249912.aspx)

## <a name="certificate-expiration-and-reregistration"></a>Vervaldatum van het certificaat en servernaam

Na de registratie van een machine als een DSC-knooppunt in Azure Automation DSC zijn er een aantal redenen waarom u tooreregister dat knooppunt in Hallo toekomstige wellicht:

* Na de registratie wordt elk knooppunt automatisch onderhandeld over een uniek certificaat voor verificatie, die na één jaar verloopt. Hallo protocol voor PowerShell DSC-registratie kan niet op dit moment automatisch certificaten vernieuwen wanneer ze bijna zijn verlopen, zodat u tooreregister Hallo knooppunten een jaar later moet. Voordat het opnieuw te registreren, moet u ervoor zorgen dat elk knooppunt wordt uitgevoerd op de Windows Management Framework 5.0 RTM. Als verificatiecertificaat van een knooppunt is verlopen en Hallo knooppunt niet is geregistreerd, Hallo knooppunt kan niet toocommunicate met Azure Automation en zal worden gemarkeerd als 'Unresponsive'. Servernaam uitgevoerd 90 dagen of minder van certificaat de verlooptijd van Hallo of op elk gewenst moment na de verlooptijd van Hallo certificaat, resulteert in een nieuw certificaat wordt gegenereerd en gebruikt.
* toochange eventuele [PowerShell DSC Local Configuration Manager-waarden](https://msdn.microsoft.com/powershell/dsc/metaconfig4) die tijdens de initiële registratie van Hallo-knooppunt, zoals ConfigurationMode zijn ingesteld. Deze waarden DSC-agent kunnen op dit moment alleen worden gewijzigd via servernaam. Hallo een uitzondering is Hallo toohello knooppunt toegewezen knooppuntconfiguratie--dit kan rechtstreeks worden gewijzigd in Azure Automation DSC.

Servernaam kan worden uitgevoerd in Hallo dezelfde manier als u geregistreerd Hallo-knooppunt in eerste instantie met behulp van een Hallo onboarding methoden in dit document worden beschreven. U hoeft niet toounregister een knooppunt uit Azure Automation DSC voordat deze opnieuw te registreren.

## <a name="related-articles"></a>Verwante artikelen

* [Overzicht van Azure Automation DSC](automation-dsc-overview.md)
* [Azure Automation DSC-cmdlets](/powershell/module/azurerm.automation/#automation)
* [Azure Automation DSC-prijzen](https://azure.microsoft.com/pricing/details/automation/)
