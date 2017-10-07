---
title: Automation DSC continue implementatie met Chocolatey aaaAzure | Microsoft Docs
description: DevOps continue implementatie met Azure Automation DSC en Chocolatey Pakketbeheer.  Voorbeeld met volledige JSON ARM-sjabloon en de PowerShell-bron.
services: automation
documentationcenter: 
author: eslesar
manager: carmonm
editor: tysonn
ms.assetid: c0baa411-eb76-4f91-8d14-68f68b4805b6
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 10/29/2016
ms.author: golive
ms.openlocfilehash: 60af52af5f834fd48e3a0dc4677919397b53f0f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="usage-example-continuous-deployment-toovirtual-machines-using-automation-dsc-and-chocolatey"></a>Voorbeeld van gebruik: Continue implementatie tooVirtual Machines met behulp van Automation DSC en Chocolatey
In een wereld DevOps zijn er veel extra tooassist met verschillende punten in Hallo continue integratie pijplijn.  Azure Automation gewenst State Configuration (DSC) is een nieuwe toevoeging toohello opties Welkom die DevOps teams kunnen gebruiken.  In dit artikel wordt gedemonstreerd instelling van continue implementatie (CD) voor een Windows-computer.  Kunt u gemakkelijk uitbreiden Hallo techniek tooinclude zoveel Windows-computers, indien nodig in Hallo-rol (bijvoorbeeld een website) en er tooadditional ook rollen.

![Continue implementatie voor IaaS VM 's](./media/automation-dsc-cd-chocolatey/cdforiaasvm.png)

## <a name="at-a-high-level"></a>Op hoog niveau
Er is heel wat hier, maar gelukkig kunnen worden onderverdeeld in twee belangrijkste processen: 

* Schrijven van code testen, maken en publiceren installatiepakketten voor de primaire en secundaire versies van Hallo-systeem. 
* Maken en beheren van virtuele machines die u installeert en Hallo code uitvoeren in hello-pakketten.  

Als beide core processen uitgevoerd worden, is een korte stap tooautomatically Hallo updatepakket naar nieuwe versies worden gemaakt en geïmplementeerd op een bepaalde virtuele machine wordt uitgevoerd.

## <a name="component-overview"></a>Onderdelenoverzicht van het
Pakket managers zoals [apt get-](https://en.wikipedia.org/wiki/Advanced_Packaging_Tool) in Hallo Linux wereld, maar niet zoveel in Windows-wereld Hallo vrij bekend zijn.  [Chocolatey](https://chocolatey.org/) is zo'n ding en van Scott Hanselman [blog](http://www.hanselman.com/blog/IsTheWindowsUserReadyForAptget.aspx) op Hallo onderwerp is een uitstekende inleiding.  Kortom, kunt Chocolatey u tooinstall pakketten vanuit een centrale opslagplaats van pakketten in een Windows-systeem met Hallo-opdrachtregel.  U kunt maken en beheren van uw eigen opslagplaats en Chocolatey kunt pakketten installeren van een willekeurig aantal opslagplaatsen die u opgeeft.

Desired State Configuration (DSC) ([overzicht](https://technet.microsoft.com/library/dn249912.aspx)) is een PowerShell-hulpprogramma waarmee u toodeclare Hallo configuratie die u voor een machine wilt.  U kunt bijvoorbeeld, "Ik wil Chocolatey geïnstalleerd, ik wil dat IIS is geïnstalleerd, ik wil dat de poort 80 is geopend, ik wil versie 1.0.0 van mijn website geïnstalleerd."  Hallo DSC Local Configuration Manager implementeert (LCM) dat de configuratie. Een DSC-Pull-Server bevat een opslagplaats van configuraties voor uw machines. Hallo LCM op elke machine controleert in periodiek toosee als de configuratie ervan overeenkomt met de opgeslagen configuratie Hallo. Het kan status rapporteren of toobring Hallo machine weer in uitlijning met de opgeslagen configuratie Hallo proberen. Hallo opgeslagen configuratie op Hallo pull-server toocause een machine of een reeks machines toocome uitgelijnd met de configuratie Hallo gewijzigd, kunt u bewerken.

Azure Automation is een beheerde service in Microsoft Azure waarmee u tooautomate diverse taken met behulp van runbooks, knooppunten, referenties, bronnen en activa zoals schema's en globale variabelen. Azure Automation DSC breidt deze automatisering mogelijkheid tooinclude PowerShell DSC-hulpprogramma's.  Hier volgt een geweldige [overzicht](automation-dsc-overview.md).

Een DSC-Resource is een module van code die de specifieke mogelijkheden, zoals het beheren van netwerken, Active Directory of SQL Server is.  Hallo Chocolatey DSC-Resource weet hoe tooaccess een NuGet-Server (onder andere) pakketten downloaden, installeren van pakketten, enzovoort.  Er zijn veel andere DSC-Resources in Hallo [PowerShell Gallery](http://www.powershellgallery.com/packages?q=dsc+resources&prerelease=&sortOrder=package-title).  Deze modules zijn geïnstalleerd in uw Azure Automation DSC-Pull-Server (door u) zodat ze kunnen worden gebruikt door uw configuraties.

Resource Manager-sjablonen bieden een declaratieve manier voor het genereren van uw infrastructuur - items zoals netwerken, subnetten, netwerkbeveiliging en routering, load balancers, NIC's en virtuele machines.  Hier volgt een [artikel](../azure-resource-manager/resource-manager-deployment-model.md) dat vergelijkt Resource Manager-implementatiemodel (declaratieve) Hallo Hello Azure Service Management (ASM of klassiek) implementatie model (imperatieve) en wordt besproken Hallo core resource providers, compute, opslag en netwerk.

Een belangrijke functie van een Resource Manager-sjabloon is de mogelijkheid tooinstall een VM-extensie in Hallo VM als deze ingericht.  Een VM-extensie heeft specifieke mogelijkheden, zoals een aangepast script uitvoeren, antivirussoftware installeren of uitvoeren van een script DSC-configuratie.  Er zijn vele andere typen van VM-extensies.

## <a name="quick-trip-around-hello-diagram"></a>Snelle reis rond Hallo-diagram
Vanaf de bovenkant hello, schrijft u uw code bouwen en testen en vervolgens een installatiepakket maken.  Chocolatey kan verschillende soorten installatiepakketten, zoals ZIP MSI, MSU, verwerken.  En u hebt volledige kracht van de werkelijke installatie van PowerShell toodo Hallo Hallo als systeemeigen mogelijkheden van Chocolatey niet erg up tooit.  Hallo-pakket in ergens bereikbaar – een opslagplaats pakket geplaatst.  In dit voorbeeld gebruik van een openbare map in een Azure blob storage-account gebruikt, maar deze kan overal worden.  Chocolatey werkt systeemeigen met NuGet-servers en enkele andere voor het beheer van de pakketmetagegevens van het.  [In dit artikel](https://github.com/chocolatey/choco/wiki/How-To-Host-Feed) Hallo opties beschreven.  In dit voorbeeld gebruik NuGet gebruikt.  Een Nuspec zijn metagegevens over uw pakketten.  Hallo Nuspec van zijn 'gecompileerd' in de NuPkg en opgeslagen in een NuGet-server.  Wanneer de configuratie van aanvragen van een pakket met de naam en verwijst naar een NuGet-server, Hallo Chocolatey DSC-Resource (nu op Hallo VM) Hallo pakket pakt het voor u en installeert.  U kunt ook een specifieke versie van een pakket aanvragen.

Er is een Azure Resource Manager (ARM)-sjabloon in Hallo onder linkergedeelte van Hallo afbeelding.  In dit voorbeeld gebruik registreert Hallo VM-extensie Hallo VM Hello Azure Automation DSC Pull-Server (dat wil zeggen, een pull-server) als een knooppunt.  Hallo-configuratie wordt opgeslagen in Hallo pull-server.  Dat deze twee keer wordt opgeslagen: eenmaal als tekst zonder opmaak en wanneer gecompileerd als een MOF-bestand (voor die over zaken weten.)  In de portal Hallo is Hallo MOF 'knooppuntconfiguratie' (als tegengestelde toosimply "configuratie").  De Hallo artefacten die is gekoppeld aan een knooppunt zodat Hallo knooppunt de configuratie ervan weet.  Details hieronder laten zien hoe tooassign Hallo knooppunt toohello configuratieknooppunt.

U bent waarschijnlijk al bezig Hallo bits Hallo boven of de meeste van deze.  Maken van Hallo nuspec, compileren en opgeslagen in een NuGet-server is een kleine ding.  En u bent al het beheer van virtuele machines.  Hallo volgende stap toocontinuous implementatie duurt vereist Hallo pull-server (eenmaal) instellen, registreert uw knooppunten (één keer), en maken en opslaan van er Hallo-configuratie (in eerste instantie).  Vernieuw vervolgens pakketten zijn bijgewerkt en geïmplementeerd toohello-opslagplaats, hello configuratie- en knooppuntconfiguratie in Hallo pull-server (Herhaal indien nodig).

Als u begint niet met een ARM-sjabloon, maar dat is ook OK.  Er zijn een PowerShell-cmdlets die zijn ontworpen toohelp registreert u uw virtuele machines met Hallo pull-server en alle Hallo rest. Zie voor meer informatie in dit artikel: [machines voorbereiden voor beheer door Azure Automation DSC](automation-dsc-onboarding.md)

## <a name="step-1-setting-up-hello-pull-server-and-automation-account"></a>Stap 1: Hallo pull-server en de automation-account instellen
Op een geverifieerde (Add-AzureRmAccount) PowerShell-opdrachtregel: (kan enkele minuten duren terwijl Hallo pull-server is ingesteld)

    New-AzureRmResourceGroup –Name MY-AUTOMATION-RG –Location MY-RG-LOCATION-IN-QUOTES
    New-AzureRmAutomationAccount –ResourceGroupName MY-AUTOMATION-RG –Location MY-RG-LOCATION-IN-QUOTES –Name MY-AUTOMATION-ACCOUNT 

U kunt uw automation-account in een van de volgende regio's (aka locatie) Hallo plaatsen: VS-Oost 2, Zuid-centraal VS, Gov ons Virginia, West-Europa, Zuidoost-Azië, Japan-Oost, India centraal en Australië-Zuidoost, Canada centraal, Noord-Europa.

## <a name="step-2-vm-extension-tweaks-toohello-arm-template"></a>Stap 2: VM-extensie trucs toohello ARM-sjabloon
Details voor registratie bij de virtuele machine (via Hallo PowerShell DSC-VM-extensie) opgegeven in deze [Snelstartsjabloon met de Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/dsc-extension-azure-automation-pullserver).  Deze stap registreert uw nieuwe virtuele machine met Hallo pull-server in de lijst Hallo van DSC-knooppunten.  Onderdeel van deze registratie is Hallo configuratie toobe toegepast toohello knooppunt op te geven.  Deze knooppuntconfiguratie nog niet is voorzien tooexist Hallo pull-server zodat deze OK die stap 4 wanneer dit wordt gedaan voor Hallo eerst is.  Maar hier in stap 2 hoeft u toohave beslist Hallo-naam van Hallo knooppunt en de naam van de Hallo van Hallo-configuratie.  In dit voorbeeld gebruik Hallo-knooppunt is 'isvbox' en Hallo-configuratie is 'ISVBoxConfig'.  Hallo configuratie knooppuntnaam (toobe opgegeven in DeploymentTemplate.json) is daarom 'ISVBoxConfig.isvbox'.  

## <a name="step-3-adding-required-dsc-resources-toohello-pull-server"></a>Stap 3: Vereist DSC-resources toohello pull-server toevoegen
Hallo PowerShell Gallery is providers tooinstall DSC-resources in uw Azure Automation-account.  Navigeer toohello resource u wilt en klikt u op Hallo 'Implementeren tooAzure Automation'.

![Voorbeeld van PowerShell Gallery](./media/automation-dsc-cd-chocolatey/xNetworking.PNG)

Een andere methode onlangs toegevoegd toohello Azure Portal kunt u toopull in nieuwe modules of update bestaande modules. Klik in het Hallo Automation-Account resource Hallo activa tegel en ten slotte Hallo Modules tegel.  Hallo bladeren galerie pictogram kunt u toosee Hallo lijst met modules in de galerie hello, Inzoomen op gegevens en uiteindelijk importeren in uw Automation-Account. Dit is een uitstekende manier tookeep uw modules up toodate van tijd tootime. En importfunctie Hallo controleert afhankelijkheden met andere modules tooensure die niets niet synchroon.

Of er is Hallo handmatige benadering.  Hallo-mapstructuur van een Module van de PowerShell-integratie voor een Windows-computer verschilt enigszins van Hallo mapstructuur werd verwacht door hello Azure Automation.  Hiervoor moet een kleine aanpassingen van uw kant.  Maar het is niet moeilijk en het slechts één keer per resource voltooid (tenzij u wilt dat tooupgrade in toekomstige.)  Zie voor meer informatie over het ontwerpen van PowerShell integratiemodules in dit artikel: [Azure Automation-integratiemodules ontwerpen](https://azure.microsoft.com/blog/authoring-integration-modules-for-azure-automation/)

* Hallo-module die u nodig hebt op uw werkstation als volgt installeren:
  * Installeer [Windows Management Framework, v5](http://aka.ms/wmf5latest) (niet nodig voor Windows 10)
  * `Install-Module –Name MODULE-NAME`<: grijpers Hallo module op basis van Hallo PowerShell Gallery 
* Kopiëren Hallo modulemap van `c:\Program Files\WindowsPowerShell\Modules\MODULE-NAME` tooa tijdelijke map 
* Voorbeelden en documentatie verwijderen uit de hoofdmap Hallo 
* ZIP Hallo hoofdmap, naming Hallo ZIP-bestand exact dezelfde Hallo als Hallo-map 
* Hallo ZIP-bestand in een bereikbaar HTTP-locatie, zoals de blob-opslag in een Azure Storage-Account worden geplaatst.
* Voer deze PowerShell:
  
      New-AzureRmAutomationModule `
          -ResourceGroupName MY-AUTOMATION-RG -AutomationAccountName MY-AUTOMATION-ACCOUNT `
          -Name MODULE-NAME –ContentLink "https://STORAGE-URI/CONTAINERNAME/MODULE-NAME.zip"

Hallo opgenomen voorbeeld voert deze stappen voor cChoco en xNetworking. Zie Hallo [notities](#notes) voor speciale verwerking voor cChoco.

## <a name="step-4-adding-hello-node-configuration-toohello-pull-server"></a>Stap 4: Hallo knooppunt configuratie toohello pull-server toevoegen
Er zijn geen speciale over Hallo eerste keer dat u uw configuratie in Hallo pull-server en compileren importeren.  Alle volgende importeren compileert Hallo dezelfde configuratie uiterlijk exact Hallo dezelfde.  Telkens wanneer u uw pakket bijwerken en het uit tooproduction u doen in deze stap nadat u hebt gecontroleerd Hallo-configuratiebestand toopush moet is juist – inclusief Hallo nieuwe versie van het pakket.  Ga als volgt Hallo-configuratiebestand en PowerShell:

ISVBoxConfig.ps1:

    Configuration ISVBoxConfig 
    { 
        Import-DscResource -ModuleName cChoco 
        Import-DscResource -ModuleName xNetworking

        Node "isvbox" {   

            cChocoInstaller installChoco 
            { 
                InstallDir = "C:\choco" 
            }

            WindowsFeature installIIS 
            { 
                Ensure="Present" 
                Name="Web-Server" 
            }

            xFirewall WebFirewallRule 
            { 
                Direction = "Inbound" 
                Name = "Web-Server-TCP-In" 
                DisplayName = "Web Server (TCP-In)" 
                Description = "IIS allow incoming web site traffic." 
                DisplayGroup = "IIS Incoming Traffic" 
                State = "Enabled" 
                Access = "Allow" 
                Protocol = "TCP" 
                LocalPort = "80" 
                Ensure = "Present" 
            }

            cChocoPackageInstaller trivialWeb 
            {            
                Name = "trivialweb" 
                Version = "1.0.0" 
                Source = “MY-NUGET-V2-SERVER-ADDRESS” 
                DependsOn = "[cChocoInstaller]installChoco", 
                "[WindowsFeature]installIIS" 
            } 
        }    
    }

Nieuw-ConfigurationScript.ps1:

    Import-AzureRmAutomationDscConfiguration ` 
        -ResourceGroupName MY-AUTOMATION-RG –AutomationAccountName MY-AUTOMATION-ACCOUNT ` 
        -SourcePath C:\temp\AzureAutomationDsc\ISVBoxConfig.ps1 ` 
        -Published –Force

    $jobData = Start-AzureRmAutomationDscCompilationJob ` 
        -ResourceGroupName MY-AUTOMATION-RG –AutomationAccountName MY-AUTOMATION-ACCOUNT ` 
        -ConfigurationName ISVBoxConfig 

    $compilationJobId = $jobData.Id

    Get-AzureRmAutomationDscCompilationJob ` 
        -ResourceGroupName MY-AUTOMATION-RG –AutomationAccountName MY-AUTOMATION-ACCOUNT ` 
        -Id $compilationJobId

Het resultaat van deze stappen in een nieuwe configuratie van de knooppunten met de naam 'ISVBoxConfig.isvbox' hello pull-server wordt geplaatst.  Hallo knooppunt configuratienaam is gebouwd als 'configurationName.nodeName'.

## <a name="step-5-creating-and-maintaining-package-metadata"></a>Stap 5: Het maken en onderhouden van pakketmetagegevens
Voor elk pakket dat u in de opslagplaats voor Hallo pakket zetten, moet u een nuspec die wordt beschreven.  Die nuspec moet worden gecompileerd en opgeslagen in de NuGet-server. Dit proces wordt beschreven [hier](http://docs.nuget.org/create/creating-and-publishing-a-package).  U kunt MyGet.org gebruiken als een NuGet-server.  Ze deze service verkocht, maar hebben een starter SKU is gratis.  NuGet.org vindt u instructies voor het installeren van uw eigen NuGet-server van uw persoonlijke pakketten is.

## <a name="step-6-tying-it-all-together"></a>Stap 6: Alles samenvoegen koppelende
Telkens wanneer een versie QA is geslaagd en is goedgekeurd voor implementatie, Hallo-pakket is gemaakt, nuspec en nupkg bijgewerkt en toohello NuGet-server geïmplementeerd.  Hallo-configuratie (stap 4 hierboven) moet bovendien bijgewerkte tooagree met Hallo nieuwe versienummer.  Het moet worden verzonden toohello pull-server en gecompileerde.  Vanaf dat moment is toohello VM's afhankelijk zijn van deze configuratie toopull Hallo update en deze installeren.  Elk van deze updates zijn eenvoudige - slechts een of twee regels van PowerShell.  In geval van de Hallo van Visual Studio Team Services, zijn sommige van deze ingekapseld in de build-taken die u een worden samengesteld in een build keten kunnen.  Dit [artikel](https://www.visualstudio.com/en-us/docs/alm-devops-feature-index#continuous-delivery) biedt meer details.  Dit [GitHub-repo-](https://github.com/Microsoft/vso-agent-tasks) details Hallo diverse beschikbare build-taken.

## <a name="notes"></a>Opmerkingen
In dit voorbeeld gebruik begint met een virtuele machine van een algemene Windows Server 2012 R2-afbeelding van hello Azure-galerie.  U kunt starten vanuit een opgeslagen installatiekopie en vervolgens vanaf daar met Hallo DSC-configuratie aanpassen.  Configuratie die is standaard uitbreidbaar wijzigen in een installatiekopie is echter veel moeilijker dan het Hallo-configuratie met behulp van DSC dynamisch bij te werken.

U hebt geen toouse een ARM-sjabloon en Hallo VM-extensie toouse deze techniek met uw virtuele machines.  En uw VM's geen toobe op Azure toobe onder beheer van de CD.  Alle die is vereist is dat Chocolatey geïnstalleerd en hello LCM geconfigureerd op Hallo VM zodat deze waarbij Hallo pull-server is.  

Natuurlijk wanneer u een pakket op een virtuele machine die in gebruik is genomen bijwerkt, moet u tootake die VM buiten rotatie Hallo-update is geïnstalleerd.  Hoe u dit doen varieert.  Bijvoorbeeld, met een VM achter een Load Balancer van Azure, kunt u toevoegen een aangepaste test.  Tijdens het bijwerken van Hallo VM hebben Hallo test eindpunt een 400 retourneren.  Hallo tweak nodig toocause deze wijziging zijn binnen uw configuratie kan Hallo tweak tooswitch weer tooreturning een 200 zodra het Hallo-update is voltooid.

Volledige bron voor dit voorbeeld gebruik is in [deze Visual Studio-project](https://github.com/sebastus/ARM/tree/master/CDIaaSVM) op GitHub.

## <a name="related-articles"></a>Verwante artikelen
* [Overzicht van Azure Automation DSC](automation-dsc-overview.md)
* [Azure Automation DSC-cmdlets](https://msdn.microsoft.com/library/mt244122.aspx)
* [Computers voorbereiden voor beheer door Azure Automation DSC](automation-dsc-onboarding.md)

