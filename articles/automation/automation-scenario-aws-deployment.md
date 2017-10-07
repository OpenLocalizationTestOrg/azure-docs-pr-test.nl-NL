---
title: implementatie van een virtuele machine in Amazon Web Services aaaAutomating | Microsoft Docs
description: Dit artikel wordt gedemonstreerd hoe toouse Azure Automation tooautomate maken van een virtuele machine in Amazon Web Service
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 1d85c01a-d795-4523-8194-84fc15b53838
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/14/2017
ms.author: tiandert; bwren
ms.openlocfilehash: dd1f3af47d8700ced85a3ee5a406dde1c1311990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---provision-an-aws-virtual-machine"></a>Azure Automation-scenario: een AWS-virtuele machine inrichten
In dit artikel wordt gedemonstreerd hoe u Azure Automation tooprovision gebruikmaken van een virtuele machine in uw abonnement Amazon Web Service (AWS) en geef die VM een specifieke naam – welke AWS tooas 'tagging' hello VM verwijst.

## <a name="prerequisites"></a>Vereisten
Hallo-toepassing van dit artikel moet u toohave een Azure Automation-account en een AWS-abonnement. Raadpleeg voor meer informatie over een Azure Automation-account instellen en configureren met de referenties van uw AWS-abonnement [verificatie met Amazon Web Services configureren](automation-configure-aws-account.md).  Dit account moet worden gemaakt of bijgewerkt met de referenties van uw AWS-abonnement voordat u doorgaat, omdat we deze account in de onderstaande stappen voor Hallo verwijst.

## <a name="deploy-amazon-web-services-powershell-module"></a>PowerShell-Module voor Amazon Web Services implementeren
Onze VM-inrichting runbook gebruikmaken Hallo AWS PowerShell-module toodo het werk. Hallo te volgen stappen tooadd Hallo module tooyour Automation-account dat is geconfigureerd met de referenties van uw AWS-abonnement uitvoeren.  

1. Open uw webbrowser en navigeer toohello [PowerShell Gallery](http://www.powershellgallery.com/packages/AWSPowerShell/) en klik op Hallo **implementeren tooAzure Automation knop**.<br><br> ![AWS PS Module-Import](./media/automation-scenario-aws-deployment/powershell-gallery-download-awsmodule.png)
2. Gaat u toohello Azure-aanmeldingspagina en als de verificatie is gelukt, u worden gerouteerde toohello Azure-Portal en krijgt Hallo blade te volgen.<br><br> ![Blade voor import-Module](./media/automation-scenario-aws-deployment/deploy-aws-powershell-module-parameters.png)
3. Selecteer Hallo resourcegroep van Hallo **resourcegroep** vervolgkeuzelijst en geef op de blade Parameters Hallo Hallo volgende informatie:
   
   * Van Hallo **nieuw of bestaand Automation-Account (tekenreeks)** vervolgkeuzelijst Selecteer **bestaande**.  
   * In Hallo **Automation-accountnaam (tekenreeks)** typt u in de exacte naam Hallo Hallo Automation-account met Hallo referenties voor uw AWS-abonnement.  Bijvoorbeeld, als u een specifiek account met de naam gemaakt **AWSAutomation**, is dat u typt in Hallo vak.
   * Selecteer Hallo juiste regio uit Hallo **Automation-Accountlocatie** vervolgkeuzelijst.
4. Wanneer u het invoeren van Hallo vereiste gegevens hebt voltooid, klikt u op **maken**.
   
   > [!NOTE]
   > Terwijl een PowerShell-module in Azure Automation importeert, het is ook het uitpakken van Hallo-cmdlets en deze activiteiten niet weergegeven worden tot Hallo-module is volledig voltooid importeren en uitpakken van Hallo-cmdlets. Dit proces kan enkele minuten duren.  
   > <br>
   > 
   > 
5. Open uw Automation-account waarnaar wordt verwezen in stap 3 in hello Azure Portal.
6. Klik op Hallo **activa** tegel en op Hallo **activa** blade, selecteer Hallo **Modules** tegel.
7. Op Hallo **Modules** blade ziet u Hallo **AWSPowerShell** module in de lijst Hallo.

## <a name="create-aws-deploy-vm-runbook"></a>Maak AWS VM runbook implementeren
Eenmaal Hallo die AWS PowerShell-Module is geïmplementeerd, we kunnen nu schrijven een runbook tooautomate inrichten van een virtuele machine in AWS met een PowerShell-script. Hallo onderstaande stappen wordt gedemonstreerd hoe tooleverage systeemeigen PowerShell-script in Azure Automation.  

> [!NOTE]
> Ga naar Hallo voor verdere informatie over opties en informatie met betrekking tot dit script [PowerShell Gallery](https://www.powershellgallery.com/packages/New-AwsVM/DisplayScript).
> 

1. Hallo PowerShell-script New-AwsVM Hallo PowerShell Gallery downloaden met een PowerShell-sessie openen en Hallo volgende te typen:<br>
   ```
   Save-Script -Name New-AwsVM -Path <path>
   ```
   <br>
2. Open uw Automation-account uit hello Azure Portal, en klikt u op Hallo **Runbooks** tegel.  
3. Van Hallo **Runbooks** blade Selecteer **een runbook toevoegen**.
4. Op Hallo **een runbook toevoegen** blade Selecteer **snelle invoer** (een nieuw runbook maken).
5. Op Hallo **Runbook** eigenschappenblade, typ een naam in het naamvak Hallo voor uw runbook en van Hallo **runbooktype** vervolgkeuzelijst Selecteer **PowerShell**, en klik vervolgens op  **Maak**.<br><br> ![Blade voor import-Module](./media/automation-scenario-aws-deployment/runbook-quickcreate-properties.png)
6. Wanneer Hallo PowerShell-Runbook bewerken blade wordt weergegeven, kopiëren en plakken van Hallo PowerShell-script in Hallo runbook authoring canvas.<br><br> ![Runbook PowerShell-Script](./media/automation-scenario-aws-deployment/runbook-powershell-script.png)<br>
   
    > [!NOTE]
    > Houd er rekening mee Hallo volgende bij het werken met Hallo voorbeeld PowerShell-script:
    > 
    > * Hallo-runbook bevat een aantal standaardwaarden voor parameters. Alle standaardwaarden evalueren en indien nodig bijwerken.
    > * Als u uw AWS-referenties hebt opgeslagen als een referentieasset met anders dan de naam **AWScred**, moet u tooupdate Hallo script op regel 57 toomatch dienovereenkomstig.  
    > * Als u werkt met Hallo AWS CLI-opdrachten in PowerShell met name met dit voorbeeldrunbook moet u Hallo AWS regio. Anders mislukt Hallo-cmdlets.  Weergave AWS onderwerp [Geef AWS regio](http://docs.aws.amazon.com/powershell/latest/userguide/pstools-installing-specifying-region.html) in Hallo AWS-hulpprogramma's voor PowerShell-document voor meer informatie.  
    >

7. een lijst met namen van de installatiekopie via uw AWS-abonnement tooretrieve PowerShell ISE Start en Hallo AWS PowerShell-Module importeren.  Verificatie uitvoeren tegen AWS door te vervangen **Get-AutomationPSCredential** in uw omgeving ISE met **AWScred = Get-Credential**.  Hiermee wordt u gevraagd uw referenties en u kunt opgeven uw **toegangssleutel-ID** voor Hallo gebruikersnaam en **geheime toegangssleutel** Hallo wachtwoord.  Zie Hallo voorbeeld hieronder:  

        #Sample tooget hello AWS VM available images
        #Please provide hello path where you have downloaded hello AWS PowerShell module
        Import-Module AWSPowerShell
        $AwsRegion = "us-west-2"
        $AwsCred = Get-Credential
        $AwsAccessKeyId = $AwsCred.UserName
        $AwsSecretKey = $AwsCred.GetNetworkCredential().Password
   
        # Set up hello environment tooaccess AWS
        Set-AwsCredentials -AccessKey $AwsAccessKeyId -SecretKey $AwsSecretKey -StoreAs AWSProfile
        Set-DefaultAWSRegion -Region $AwsRegion
   
        Get-EC2ImageByName -ProfileName AWSProfile

    Hallo wordt volgende uitvoer geretourneerd:<br><br>
   ![AWS-installatiekopieën ophalen](./media/automation-scenario-aws-deployment/powershell-ise-output.png)<br>  
8. Kopieer en plak Hallo een van de namen van Hallo afbeeldingen in een Automation-variabele waarnaar wordt verwezen in Hallo runbook als **$InstanceType**. Omdat in dit voorbeeld gebruiken we Hallo AWS gratis abonnement gelaagde, gebruiken we **t2.micro** in ons voorbeeld runbook.  
9. Hallo runbook opslaan en klik vervolgens op **publiceren** toopublish hello runbook en vervolgens **Ja** wanneer u wordt gevraagd.

### <a name="testing-hello-aws-vm-runbook"></a>Hallo AWS VM runbook testen
Voordat we met testen Hallo runbook doorgaat, moeten we tooverify leest. Specifiek:  

* Een actief voor het verifiëren met AWS is aangemaakt aangeroepen **AWScred** of Hallo-script is bijgewerkte tooreference Hallo-naam van de referentie-element.    
* Hallo AWS PowerShell-module is geïmporteerd in Azure Automation  
* Een nieuw runbook gemaakt en de parameterwaarden zijn gecontroleerd en bijgewerkt indien nodig  
* **Logboekregistratie van uitgebreide records** en optioneel **logboekregistratie van voortgangsrecords** onder Hallo runbook instelling **logboekregistratie en tracering** te zijn ingesteld**op**.<br><br> ![Runbook-logboekregistratie en tracering](./media/automation-scenario-aws-deployment/runbook-settings-logging-and-tracing.png)  

1. We toostart hello runbook wilt, dus klik op **Start** en klik vervolgens op **OK** wanneer de blade Runbook starten hello wordt geopend.
2. Geef op de blade Runbook starten hello, een **VMname**.  Accepteer de standaardwaarden Hallo voor Hallo andere parameters die u eerder een vooraf in Hallo script geconfigureerd.  Klik op **OK** toostart hello runbooktaak.<br><br> ![Nieuw AwsVM runbook starten](./media/automation-scenario-aws-deployment/runbook-start-job-parameters.png)
3. Een taakdeelvenster wordt geopend voor Hallo runbooktaak die we zojuist hebben gemaakt. Sluit dit venster.
4. We de voortgang van de uitvoer van de taak en de weergave van de Hallo kunt bekijken **Streams** door het selecteren van Hallo **alle logboeken** via de runbookblade taak Hallo tegel.<br><br> ![Stroomuitvoer](./media/automation-scenario-aws-deployment/runbook-job-streams-output.png)
5. tooconfirm hello VM wordt ingericht, meld u aan bij Hallo AWS-beheerconsole als u momenteel niet is aangemeld.<br><br> ![AWS-console geïmplementeerd VM](./media/automation-scenario-aws-deployment/aws-instances-status.png)

## <a name="next-steps"></a>Volgende stappen
* Zie tooget gestart met grafische runbooks [Mijn eerste grafische runbook](automation-first-runbook-graphical.md)
* tooget gestart met PowerShell workflow-runbooks, Zie [Mijn eerste PowerShell workflow-runbook](automation-first-runbook-textual.md)
* tooknow meer informatie over runbooktypen, hun voordelen en beperkingen, Zie [Azure Automation-runbooktypen](automation-runbook-types.md)
* Zie [Systeemeigen PowerShell-scriptondersteuning in Azure Automation](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/) voor meer informatie over de functie voor PowerShelll-scriptondersteuning

