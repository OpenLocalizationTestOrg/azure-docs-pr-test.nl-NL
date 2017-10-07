---
title: aaaGetting de slag met Azure Automation DSC | Microsoft Docs
description: Uitleg en voorbeelden van Hallo meest algemene taken in Azure Automation Desired State Configuration (DSC)
services: automation
documentationcenter: na
author: eslesar
manager: carmonm
editor: tysonn
ms.assetid: a3816593-70a3-403b-9a43-d5555fd2cee2
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: na
ms.date: 11/21/2016
ms.author: magoedte;eslesar
ms.openlocfilehash: 82910c96e928b9264c2e1b52a5c98dc47273dcc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-automation-dsc"></a>Aan de slag met Azure Automation DSC
Dit onderwerp wordt uitgelegd hoe toodo Hallo meest algemene taken met Azure Automation Desired State Configuration (DSC), zoals het maken, importeren, en compileren configuraties, voorbereiding machines te beheren, en het weergeven van rapporten. Zie voor een overzicht van wat Azure Automation DSC is, [overzicht van Azure Automation DSC](automation-dsc-overview.md). Zie voor documentatie DSC [Windows PowerShell Desired Configuration overzicht](https://msdn.microsoft.com/PowerShell/dsc/overview).

Dit onderwerp bevat een stapsgewijze handleiding toousing Azure Automation DSC. Als u een Voorbeeldomgeving is al ingesteld zonder het Hallo-stappen die worden beschreven in dit onderwerp wilt, kunt u [Hallo volgende ARM-sjabloon](https://github.com/azureautomation/automation-packs/tree/master/102-sample-automation-setup). Deze sjabloon stelt u een voltooide Azure Automation DSC-omgeving, met inbegrip van een virtuele machine van Azure die wordt beheerd door Azure Automation DSC.

## <a name="prerequisites"></a>Vereisten
toocomplete hello voorbeelden in dit onderwerp, Hallo volgende is vereist:

* Een Azure Automation-account. Zie [Azure Uitvoeren-als-account](automation-sec-configure-azure-runas-account.md) voor instructies over het maken van een Azure Automation Uitvoeren-als-account.
* Een Azure Resource Manager VM (niet-klassieke) met Windows Server 2008 R2 of hoger. Zie voor instructies over het maken van een virtuele machine [uw eerste virtuele Windows-machine maken in hello Azure-portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md)

## <a name="creating-a-dsc-configuration"></a>Maken van een DSC-configuratie
We gaan een eenvoudige maken [DSC-configuratie](https://msdn.microsoft.com/powershell/dsc/configurations) die ervoor zorgt Hallo aanwezigheid of afwezigheid van Hallo **webserver** Windows functie (IIS), afhankelijk van hoe u knooppunten toewijzen.

1. Start Windows PowerShell ISE hello (of een teksteditor).
2. Typ na de tekst hello:
   
    ```powershell
    configuration TestConfig
    {
        Node WebServer
        {
            WindowsFeature IIS
            {
                Ensure               = 'Present'
                Name                 = 'Web-Server'
                IncludeAllSubFeature = $true
   
            }
        }
   
        Node NotWebServer
        {
            WindowsFeature IIS
            {
                Ensure               = 'Absent'
                Name                 = 'Web-Server'
   
            }
        }
        }
    ```
3. Hallo bestand opslaan als `TestConfig.ps1`.

Deze configuratie wordt één resource in elk blok knooppunt hello [WindowsFeature resource](https://msdn.microsoft.com/powershell/dsc/windowsfeatureresource), die ervoor zorgt Hallo aanwezigheid of afwezigheid van Hallo **webserver** functie.

## <a name="importing-a-configuration-into-azure-automation"></a>Een configuratie te importeren in Azure Automation
We je vervolgens Hallo configuratie importeren in Hallo Automation-account.

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Klik op het menu Hub Hallo **alle resources** en vervolgens Hallo naam van uw Automation-account.
3. Op Hallo **Automation-account** blade, klikt u op **DSC-configuraties**.
4. Op Hallo **DSC-configuraties** blade, klikt u op **toevoegen van een configuratie**.
5. Op Hallo **configuratie importeren** blade, bladeren toohello `TestConfig.ps1` bestand op uw computer.
   
    ![Schermopname van Hallo ** importeren configuratie ** blade](./media/automation-dsc-getting-started/AddConfig.png)
6. Klik op **OK**.

## <a name="viewing-a-configuration-in-azure-automation"></a>Een configuratie weergeven in Azure Automation
Nadat u een configuratie hebt geïmporteerd, kunt u deze bekijken in hello Azure-portal.

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Klik op het menu Hub Hallo **alle resources** en vervolgens Hallo naam van uw Automation-account.
3. Op Hallo **Automation-account** blade, klikt u op **DSC-configuraties**
4. Op Hallo **DSC-configuraties** blade, klikt u op **TestConfig** (dit is de naam Hallo van Hallo-configuratie die u hebt geïmporteerd in de vorige procedure Hallo).
5. Op Hallo **TestConfig configuratie** blade, klikt u op **weergave configuratiebron**.
   
    ![Schermafbeelding van Hallo TestConfig configuratie tabblad](./media/automation-dsc-getting-started/ViewConfigSource.png)
   
    Een **TestConfig configuratiebron** blade geopend waarin Hallo PowerShell-code voor Hallo-configuratie.

## <a name="compiling-a-configuration-in-azure-automation"></a>Een Azure Automation-configuratie compileren
Voordat u een knooppunt van de status van de gewenste tooa toepassen kunt, moet een DSC-configuratie definiëren die status worden gecompileerd naar een of meer knooppuntconfiguraties (MOF document) en op Hallo Automation DSC-Pull-Server geplaatst. Zie voor een gedetailleerdere beschrijving van het compileren van configuraties in Azure Automation DSC [compileren van configuraties in Azure Automation DSC](automation-dsc-compile.md). Zie voor meer informatie over het compileren van configuraties [DSC-configuraties](https://msdn.microsoft.com/PowerShell/DSC/configurations).

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Klik op het menu Hub Hallo **alle resources** en vervolgens Hallo naam van uw Automation-account.
3. Op Hallo **Automation-account** blade, klikt u op **DSC-configuraties**
4. Op Hallo **DSC-configuraties** blade, klikt u op **TestConfig** (Hallo-naam van Hallo eerder geïmporteerd configuratie).
5. Op Hallo **TestConfig configuratie** blade, klikt u op **compileren**, en klik vervolgens op **Ja**. Hiermee start u een Compilatietaak.
   
    ![Schermafbeelding van Hallo TestConfig configuratie tabblad compileren knop markeren](./media/automation-dsc-getting-started/CompileConfig.png)

> [!NOTE]
> Wanneer u een configuratie in Azure Automation compileert, wordt deze automatisch een gemaakt knooppunt configuratie MOF-bestanden toohello pull-server geïmplementeerd.
> 
> 

## <a name="viewing-a-compilation-job"></a>Een Compilatietaak weergeven
Nadat u een compilatie gestart, kunt u deze bekijken in Hallo **compilatietaken** -tegel in Hallo **configuratie** blade. Hallo **compilatietaken** tegel bevat momenteel wordt uitgevoerd, voltooid en mislukte taken. Wanneer u een taak compilatie blade opent, ziet u informatie over deze taak inclusief eventuele fouten of waarschuwingen opgetreden, invoerparameters gebruikt in Hallo-configuratie en compilatie Logboeken.

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Klik op het menu Hub Hallo **alle resources** en vervolgens Hallo naam van uw Automation-account.
3. Op Hallo **Automation-account** blade, klikt u op **DSC-configuraties**.
4. Op Hallo **DSC-configuraties** blade, klikt u op **TestConfig** (Hallo-naam van Hallo eerder geïmporteerd configuratie).
5. Op Hallo **compilatietaken** tegel Hallo **TestConfig configuratie** blade, klik op een van de Hallo taken die worden vermeld. Een **Compilatietaak** blade wordt geopend, gelabeld met Hallo datum op waarop Hallo Compilatietaak is gestart.
   
    ![Schermafbeelding van Hallo Compilatietaak tabblad](./media/automation-dsc-getting-started/CompilationJob.png)
6. Klik op een tegel in Hallo **Compilatietaak** blade toosee verdere details over Hallo-taak.

## <a name="viewing-node-configurations"></a>Knooppuntconfiguraties weergeven
Voltooiing van een Compilatietaak maakt een of meer nieuwe knooppuntconfiguraties. De knooppuntconfiguratie van een is een MOF-document dat is geïmplementeerd toohello pull-server en gereed toobe opgehaald en toegepast door een of meer knooppunten. U kunt Hallo knooppuntconfiguraties weergeven in uw Automation-account in Hallo **DSC-knooppuntconfiguraties** blade. De configuratie van een knooppunt heeft een naam met Hallo formulier *ConfigurationName*. *NodeName*.

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Klik op het menu Hub Hallo **alle resources** en vervolgens Hallo naam van uw Automation-account.
3. Op Hallo **Automation-account** blade, klikt u op **DSC-knooppuntconfiguraties**.
   
    ![Schermafbeelding van tabblad voor Hallo DSC-knooppuntconfiguraties](./media/automation-dsc-getting-started/NodeConfigs.png)

## <a name="onboarding-an-azure-vm-for-management-with-azure-automation-dsc"></a>Voorbereiden op een virtuele machine van Azure voor beheer met Azure Automation DSC
U kunt Azure Automation DSC toomanage virtuele Azure-machines (Classic en Resource Manager), lokale VM's Linux machines, AWS virtuele machines en fysieke machines lokale gebruiken. In dit onderwerp wordt uitgelegd hoe tooonboard alleen Azure Resource Manager virtuele machines. Zie voor informatie over de voorbereiding andere soorten machines, [machines voorbereiden voor beheer door Azure Automation DSC](automation-dsc-onboarding.md).

### <a name="tooonboard-an-azure-resource-manager-vm-for-management-by-azure-automation-dsc"></a>tooonboard een Azure Resource Manager-VM voor beheer door Azure Automation DSC
1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Klik op het menu Hub Hallo **alle resources** en vervolgens Hallo naam van uw Automation-account.
3. Op Hallo **Automation-account** blade, klikt u op **DSC-knooppunten**.
4. In Hallo **DSC-knooppunten** blade, klikt u op **toevoegen Azure VM**.
   
    ![Schermafbeelding van Hallo DSC-knooppunten tabblad hello Azure VM toevoegen knop markeren](./media/automation-dsc-getting-started/OnboardVM.png)
5. In Hallo **Azure Virtual machines toevoegen** blade, klikt u op **tooonboard van virtuele machines selecteren**.
6. In Hallo **Selecteer VMs** blade Selecteer Hallo VM die u wilt tooonboard en klikt u op **OK**.
   
   > [!IMPORTANT]
   > Dit moet een Azure Resource Manager-VM met Windows Server 2008 R2 of hoger.
   > 
   > 
7. In Hallo **Azure Virtual machines toevoegen** blade, klikt u op **registratiegegevens configureren**.
8. In Hallo **registratie** blade Hallo naam invoeren van knooppuntconfiguratie Hallo gewenste tooapply toohello VM in Hallo **knooppunt configuratienaam** vak. Dit moet exact overeenkomen met de Hallo-naam van de knooppuntconfiguratie van een in Hallo Automation-account. Op dit moment een naam opgeven is optioneel. U kunt Hallo toegewezen knooppuntconfiguratie na onboarding Hallo knooppunt wijzigen.
   Controleer **knooppunt opnieuw opstarten indien nodig**, en klik vervolgens op **OK**.
   
    ![Schermafbeelding van tabblad voor Hallo-registratie](./media/automation-dsc-getting-started/RegisterVM.png)
   
    Hallo-knooppuntconfiguratie die u hebt opgegeven zijn toegepaste toohello VM met een interval dat is opgegeven door Hallo **frequentie van de configuratiemodus**, en Hallo VM, controleren op updates toohello knooppunt configureren met een interval dat is opgegeven door Hallo  **Vernieuwingsfrequentie**. Zie voor meer informatie over het gebruik van deze waarden [configureren Hallo Local Configuration Manager](https://msdn.microsoft.com/PowerShell/DSC/metaConfig).
9. In Hallo **Azure Virtual machines toevoegen** blade, klikt u op **maken**.

Azure start Hallo proces van het voorbereidingsproces Hallo VM. Wanneer deze voltooid is, Hallo VM wordt weergegeven in Hallo **DSC-knooppunten** blade in Hallo Automation-account.

## <a name="viewing-hello-list-of-dsc-nodes"></a>Hallo-lijst van de DSC-knooppunten
U kunt Hallo lijst weergeven met alle machines die vrijgegeven voor management in uw Automation-account in Hallo zijn **DSC-knooppunten** blade.

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Klik op het menu Hub Hallo **alle resources** en vervolgens Hallo naam van uw Automation-account.
3. Op Hallo **Automation-account** blade, klikt u op **DSC-knooppunten**.

## <a name="viewing-reports-for-dsc-nodes"></a>Weergeven van rapporten voor DSC-knooppunten
Elke keer dat Azure Automation DSC een consistentiecontrole uit op een beheerde knooppunt voert verzendt Hallo knooppunt een status rapport back toohello pull-server. U kunt deze rapporten kunt weergeven op de blade Hallo voor dat knooppunt.

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Klik op het menu Hub Hallo **alle resources** en vervolgens Hallo naam van uw Automation-account.
3. Op Hallo **Automation-account** blade, klikt u op **DSC-knooppunten**.
4. Op Hallo **rapporten** tegel, klikt u op Hallo rapporten in de lijst Hallo.
   
    ![Schermafbeelding van tabblad voor Hallo-rapport](./media/automation-dsc-getting-started/NodeReport.png)

Op Hallo blade voor een afzonderlijk rapport, kunt u zien Hallo statusinformatie voor de bijbehorende consistentie Hallo volgende controleren:

* statusrapportage Hallo — of Hallo knooppunt 'Compatibele', 'Mislukt' Hallo-configuratie of Hallo-knooppunt is 'Niet-compatibel' (wanneer Hallo-knooppunt is in **applyandmonitor** Hallo-modus en de machine is niet in Hallo gewenst status).
* Hallo begintijd voor Hallo consistentiecontrole uit.
* de totale runtime Hallo Hallo consistentie van controleren.
* Controleer de consistentie Hallo type.
* Eventuele fouten, met inbegrip van de fout Hallo-bericht en de fout. 
* Eventuele DSC-resources in Hallo configuratie en status van elke resource (Hallo-knooppunt is of Hallo gewenst status voor die bron) Hallo gebruikt, kunt u op elke resource tooget meer gedetailleerde informatie voor die bron.
* Hallo-naam, IP-adres en configuratiemodus van Hallo-knooppunt.

U kunt ook klikken op **onbewerkte rapport weergeven** toosee Hallo feitelijke gegevens die Hallo knooppunt toohello server verzendt. Zie voor meer informatie over het gebruik van die gegevens [met behulp van een DSC-rapportserver](https://msdn.microsoft.com/powershell/dsc/reportserver).

Het kan even duren wanneer een knooppunt vrijgegeven is voordat de eerste rapport Hallo beschikbaar is. Mogelijk moet u toowait up too30 minuten voor de eerste rapport Hallo nadat u vrijgeven een knooppunt.

## <a name="reassigning-a-node-tooa-different-node-configuration"></a>Opnieuw toewijzen van een ander knooppunt knooppuntconfiguratie van de tooa
U kunt een knooppunt toouse een ander knooppuntconfiguratie toewijzen dan Hallo een die oorspronkelijk was toegewezen.

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Klik op het menu Hub Hallo **alle resources** en vervolgens Hallo naam van uw Automation-account.
3. Op Hallo **Automation-account** blade, klikt u op **DSC-knooppunten**.
4. Op Hallo **DSC-knooppunten** blade, klik op de naam van de Hallo Hallo-knooppunt dat u wilt dat tooreassign.
5. Klik op de blade voor dat knooppunt Hallo **toewijzen knooppunt**.
   
    ![Schermafbeelding van Hallo knooppunt tabblad Hallo toewijzen knooppunt knop markeren](./media/automation-dsc-getting-started/AssignNode.png)
6. Op Hallo **knooppuntconfiguratie toewijzen** blade, selecteer Hallo knooppunt configuratie toowhich u wilt dat tooassign Hallo knooppunt en klik vervolgens op **OK**.
   
    ![Schermafbeelding van tabblad voor Hallo knooppuntconfiguratie toewijzen](./media/automation-dsc-getting-started/AssignNodeConfig.png)

## <a name="unregistering-a-node"></a>De registratie van een knooppunt
Als u niet langer een knooppunt toobe beheerd door Azure Automation DSC wilt, kunt u de registratie verwijderen.

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Klik op het menu Hub Hallo **alle resources** en vervolgens Hallo naam van uw Automation-account.
3. Op Hallo **Automation-account** blade, klikt u op **DSC-knooppunten**.
4. Op Hallo **DSC-knooppunten** blade, klik op de naam van de Hallo Hallo-knooppunt dat u wilt dat toounregister.
5. Klik op de blade voor dat knooppunt Hallo **Unregister**.
   
    ![Schermafbeelding van Hallo knooppunt tabblad Hallo Unregister knop markeren](./media/automation-dsc-getting-started/UnregisterNode.png)

## <a name="related-articles"></a>Verwante artikelen
* [Overzicht van Azure Automation DSC](automation-dsc-overview.md)
* [Computers voorbereiden voor beheer door Azure Automation DSC](automation-dsc-onboarding.md)
* [Windows PowerShell Desired State Configuration-overzicht](https://msdn.microsoft.com/powershell/dsc/overview)
* [Azure Automation DSC-cmdlets](/powershell/module/azurerm.automation/#automation)
* [Azure Automation DSC-prijzen](https://azure.microsoft.com/pricing/details/automation/)

