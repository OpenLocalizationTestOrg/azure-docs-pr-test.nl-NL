---
title: een Azure Automation-integratiemodule aaaCreate | Microsoft Docs
description: Zelfstudie die u helpt bij Hallo maken, testen en voorbeeld van integratiemodules in Azure Automation.
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: 27798efb-08b9-45d9-9b41-5ad91a3df41e
ms.service: automation
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/13/2017
ms.author: magoedte
ms.openlocfilehash: d4064d8b106496f4dab442024131886c4affccab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-integration-modules"></a>Azure Automation-integratiemodules
PowerShell is Hallo basistechnologie achter Azure Automation. Omdat Azure Automation is gebouwd op PowerShell, zijn de PowerShell-modules sleutel toohello uitbreidbaarheid van Azure Automation. In dit artikel we leidt u door het Hallo-details van het gebruik van Azure Automation van PowerShell-modules, tooas 'Integratiemodules' waarnaar wordt verwezen en aanbevolen procedures voor het maken van uw eigen PowerShell-modules toomake zeker van te zijn dat ze werken als integratiemodules binnen Azure Automation. 

## <a name="what-is-a-powershell-module"></a>Wat is een PowerShell-module?
Een PowerShell-module is een groep PowerShell-cmdlets, zoals **Get-Date** of **Copy-Item**, die kan worden gebruikt vanuit Hallo PowerShell-console, scripts, werkstromen, runbooks en PowerShell DSC-resources, zoals WindowsFeature of File, die kan worden gebruikt vanuit PowerShell DSC-configuraties. Hallo-functionaliteit van PowerShell is zichtbaar via cmdlets en DSC-resources en elke cmdlet/DSC-resource wordt ondersteund door een PowerShell-module veel van die worden geleverd met PowerShell zelf. Bijvoorbeeld, Hallo **Get-Date** cmdlet maakt deel uit van Hallo PowerShell-module Microsoft.PowerShell.Utility en **Copy-Item** cmdlet maakt deel uit van Hallo PowerShell-module Microsoft.PowerShell.Management en Hallo Package DSC-resource maakt deel uit van Hallo PowerShell-module PSDesiredStateConfiguration. Deze modules worden geleverd met PowerShell. Maar veel PowerShell-modules niet worden geleverd als onderdeel van PowerShell en in plaats daarvan met de eerste of van derden producten zoals System Center 2012 Configuration Manager of door Hallo enorme PowerShell-community op locaties zoals PowerShell Gallery worden gedistribueerd.  Hallo-modules zijn nuttig omdat ze complexe taken eenvoudiger via ingekapselde functionaliteit.  Meer informatie over [PowerShell-modules vindt u op MSDN](https://msdn.microsoft.com/library/dd878324%28v=vs.85%29.aspx). 

## <a name="what-is-an-azure-automation-integration-module"></a>Wat is een Azure Automation-integratiemodule?
Een integratiemodule verschilt niet heel veel van een PowerShell-module. De gewoon een PowerShell-module die desgewenst één extra bestand - een metagegevensbestand waarin een Azure Automation verbinding type toobe gebruikt met de cmdlets Hallo-module in runbooks bevat. Optioneel bestand of niet, deze PowerShell-modules kunnen worden geïmporteerd in Azure Automation toomake hun cmdlets beschikbaar voor gebruik in runbooks en de bijbehorende DSC-resources beschikbaar voor gebruik in DSC-configuraties. Achter de schermen hello, Azure Automation slaat deze modules en worden ze op runbooktaken en DSC-compilatie uitvoeringstijd in hello Azure Automation-sandboxes geladen waar runbooks worden uitgevoerd en DSC-configuraties worden gecompileerd.  Eventuele DSC-resources in modules worden ook automatisch geplaatst op Hallo Automation DSC-pull-server, zodat ze kunnen worden opgehaald door machines waarmee wordt geprobeerd tooapply DSC-configuraties.  

We verzenden een aantal Azure PowerShell-modules out of box Hallo in Azure Automation voor toouse u zodat u kunt aan de slag meteen automatiseren van Azure-beheer, maar u kunt de PowerShell-modules voor elk systeem, service of hulpprogramma dat u wilt dat toointegrate met importeren. 

> [!NOTE]
> Bepaalde modules worden verzonden als 'globale modules' in hello Automation-service. Deze globale modules zijn beschikbaar tooyou wanneer u een automation-account maakt, en we ze soms bijwerken die u ze automatisch tooyour automation-account implementeert. Als u niet dat deze wilt automatisch wordt bijgewerkt, kunt u altijd importeren toobe Hallo in dezelfde module zelf en die voorrang boven algemene moduleversie Hallo van die module die we in Hallo-service worden geleverd. 

Hallo-indeling op waarin u een integratiemodulepakket importeert is een gecomprimeerd bestand met dezelfde naam als Hallo-module en met een .zip-extensie Hallo. Het bevat Hallo Windows PowerShell-module en ondersteunende bestanden, inclusief een manifestbestand (.psd1) als het Hallo-module heeft een.

Als een Azure Automation-verbindingstype Hallo-module bevat, moet deze ook een bestand met de naam Hallo bevatten `<ModuleName>-Automation.json` Hiermee worden de eigenschappen van verbindingstype Hallo. Dit is een json-bestand in de modulemap Hallo van uw gecomprimeerde ZIP-bestand geplaatst en Hallo velden bevat een 'verbinding' die is vereist tooconnect toohello systeem of Hallo servicemodule vertegenwoordigt. Uiteindelijk wordt hiermee een verbindingstype gemaakt in Azure Automation. Gebruik van dit bestand kunt u de veldnamen hello, instellen van het type, en of Hallo velden moeten worden versleuteld en / of optioneel, voor het verbindingstype Hallo van Hallo-module. Hallo hieronder vindt u een sjabloon in Hallo json-bestandsindeling:

```
{ 
   "ConnectionFields": [
   {
      "IsEncrypted":  false,
      "IsOptional":  false,
      "Name":  "ComputerName",
      "TypeName":  "System.String"
   },
   {
      "IsEncrypted":  false,
      "IsOptional":  true,
      "Name":  "Username",
      "TypeName":  "System.String"
   },
   {
      "IsEncrypted":  true,
      "IsOptional":  false,
      "Name":  "Password",
   "TypeName":  "System.String"
   }],
   "ConnectionTypeName":  "DataProtectionManager",
   "IntegrationModuleName":  "DataProtectionManager"
}
```

Als u Service Management Automation hebt geïmplementeerd en integratiemodulepakketten voor uw automation-runbooks, moet dit bekend tooyou eruitzien. 

## <a name="authoring-best-practices"></a>Aanbevolen procedures voor ontwerpen
Hoewel integratiemodules in feite PowerShell-modules, er nog steeds een aantal zaken we u aan moet denken bij het ontwerpen van een PowerShell-module toomake deze zo bruikbaar in Azure Automation. Sommige hiervan zijn specifiek voor Azure Automation en sommige zijn nuttig alleen toomake uw modules goed in PowerShell Workflow werkt, ongeacht of u Automation gebruikt. 

1. Neem een samenvatting, beschrijving en help-URI voor elke cmdlet in Hallo-module. In PowerShell kunt u bepaalde help-informatie voor cmdlets tooallow hello tooreceive Help-informatie over het gebruik van deze Hello **Get-Help** cmdlet. U kunt bijvoorbeeld als volgt een samenvatting en Help-URI definiëren voor een PowerShell-module, geschreven in een PSM1-bestand.<br>  
   
    ```
    <#
        .SYNOPSIS
         Gets all outgoing phone numbers for this Twilio account 
    #>
    function Get-TwilioPhoneNumbers {
    [CmdletBinding(DefaultParameterSetName='SpecifyConnectionFields', `
    HelpUri='http://www.twilio.com/docs/api/rest/outgoing-caller-ids')]
    param(
       [Parameter(ParameterSetName='SpecifyConnectionFields', Mandatory=$true)]
       [ValidateNotNullOrEmpty()]
       [string]
       $AccountSid,
   
       [Parameter(ParameterSetName='SpecifyConnectionFields', Mandatory=$true)]
       [ValidateNotNullOrEmpty()]
       [string]
       $AuthToken,
   
       [Parameter(ParameterSetName='UseConnectionObject', Mandatory=$true)]
       [ValidateNotNullOrEmpty()]
       [Hashtable]
       $Connection
    )
   
    $cred = CreateTwilioCredential -Connection $Connection -AccountSid $AccountSid -AuthToken $AuthToken
   
    $uri = "$TWILIO_BASE_URL/Accounts/" + $cred.UserName + "/IncomingPhoneNumbers"
   
    $response = Invoke-RestMethod -Method Get -Uri $uri -Credential $cred
   
    $response.TwilioResponse.IncomingPhoneNumbers.IncomingPhoneNumber
    }
    ```
   <br> Deze gegevens bieden niet alleen getoond deze informatie over het gebruik van Hallo **Get-Help** cmdlet in PowerShell-console Hallo, deze wordt ook weergegeven in dit help-functionaliteit in Azure Automation.  Bijvoorbeeld wanneer u activiteiten invoegt tijdens het ontwerpen van een runbook. Te klikken op 'Gedetailleerde help weergeven' wordt geopend Hallo help-URI in een ander tabblad van Hallo webbrowser u tooaccess Azure Automation.<br>![Help bij integratiemodules](media/automation-integration-modules/automation-integration-module-activitydesc.png)
2. Als de module Hallo wordt uitgevoerd op een extern systeem

    a. Een integratiemodule metagegevensbestand die Hallo informatie die nodig is tooconnect toothat externe systeem definieert, dus Hallo verbindingstype moet bevatten.  
    b. Elke cmdlet in de module Hallo moet kunnen tootake een verbindingsobject (een exemplaar van dat verbindingstype) als een parameter.  

    Cmdlets in Hallo-module worden eenvoudiger toouse in Azure Automation als u toestaat dat een object met de velden van het verbindingstype Hallo Hallo doorgeven als een parameter toohello-cmdlet. Deze manier gebruikers hebben geen toomap parameters van de overeenkomstige parameters Hallo verbinding asset toohello van cmdlet telkens wanneer die ze een cmdlet aanroepen. Op basis van Hallo runbook in bovenstaand voorbeeld, wordt gebruikt een Twilio-verbindingsasset genaamd corptwilio gebruikt tooaccess Twilio en retourneren van alle Hallo telefoonnummers in Hallo-account.  U ziet hoe het Hallo-velden van Hallo verbindingsparameters toohello van Hallo cmdlet toewijzen?<br>
   
    ```
    workflow Get-CorpTwilioPhones
    {
      $CorpTwilio = Get-AutomationConnection -Name 'CorpTwilio'
   
      Get-TwilioPhoneNumbers 
        -AccountSid $CorpTwilio.AccountSid  
        -AuthToken $CorptTwilio.AuthToken
    }
    ```
  
    Een eenvoudigere en betere manier tooapproach dit is het rechtstreeks doorgeven Hallo verbinding object toohello cmdlet-
   
    ```
    workflow Get-CorpTwilioPhones
    {
      $CorpTwilio = Get-AutomationConnection -Name 'CorpTwilio'
   
      Get-TwilioPhoneNumbers -Connection $CorpTwilio
    }
    ```
   
    U kunt gedrag voor uw cmdlets door hen tooaccept een verbindingsobject rechtstreeks als een parameter, in plaats van alleen Verbindingsvelden voor parameters inschakelen. Doorgaans wilt u een parameter die is ingesteld voor elk, zodat een gebruiker die niet met behulp van Azure Automation uw cmdlets aanroepen kan zonder een hashtabel tooact als Hallo-verbindingsobject maken. Parameterset **SpecifyConnectionFields** hieronder vindt u gebruikte toopass Hallo veld verbindingseigenschappen één voor één. **UseConnectionObject** kunt u doorgeeft Hallo meteen via verbinding. Zoals u ziet de cmdlet Send-TwilioSMS in Hallo Hallo [Twilio PowerShell-module](https://gallery.technet.microsoft.com/scriptcenter/Twilio-PowerShell-Module-8a8bfef8) doorgave op beide manieren: 
   
    ```
    function Send-TwilioSMS {
      [CmdletBinding(DefaultParameterSetName='SpecifyConnectionFields', `
      HelpUri='http://www.twilio.com/docs/api/rest/sending-sms')]
      param(
         [Parameter(ParameterSetName='SpecifyConnectionFields', Mandatory=$true)]
         [ValidateNotNullOrEmpty()]
         [string]
         $AccountSid,
   
         [Parameter(ParameterSetName='SpecifyConnectionFields', Mandatory=$true)]
         [ValidateNotNullOrEmpty()]
         [string]
         $AuthToken,
   
         [Parameter(ParameterSetName='UseConnectionObject', Mandatory=$true)]
         [ValidateNotNullOrEmpty()]
         [Hashtable]
         $Connection
   
       )
    }
    ```
   <br>
3. Definieer het uitvoertype voor alle cmdlets in Hallo-module. Een uitvoertype definiëren voor een cmdlet ontwerptijd IntelliSense kunt uitvoer toohelp bepalen van Hallo eigenschappen van de cmdlet hello, voor gebruik tijdens het ontwerpen van. Het is vooral nuttig tijdens Automation runbook grafisch ontwerpen, waarbij ontwerptijdkennis key tooan goede gebruikerservaring met uw module is.<br><br> ![Uitvoertype grafisch runbook](media/automation-integration-modules/runbook-graphical-module-output-type.png)<br> Dit is vergelijkbaar toohello 'vooruit Typ' functionaliteit van een cmdlet-uitvoer in PowerShell ISE zonder toorun deze.<br><br> ![POSH IntelliSense](media/automation-integration-modules/automation-posh-ise-intellisense.png)<br>
4. Cmdlets in Hallo-module neemt niet complexe objecttypen voor parameters. PowerShell Workflow verschilt van PowerShell in het volgende opzicht: complexe typen worden in gedeserialiseerde vorm opgeslagen. Primitieve typen blijven primitieven, maar complexe typen worden geconverteerd tootheir gedeserialiseerd versies, die in wezen Eigenschappenverzamelingen zijn. Als u Hallo gebruikt bijvoorbeeld **Get-Process** cmdlet in een runbook (of een PowerShell-werkstroom eigenlijk), zou het retourneren van een object van type [Deserialized.System.Diagnostic.Process], niet Hallo verwachte [ Type System.Diagnostic.Process]. Dit type heeft alle Hallo dezelfde eigenschappen als niet-gedeserialiseerde type, maar geen van de methoden Hallo Hallo. En als u toopass deze waarde als een parameter tooa cmdlet probeert, waarbij Hallo cmdlet een waarde [System.Diagnostic.Process] voor deze parameter verwacht, ontvangt u Hallo volgende fout: *argumenttransformatie voor parameter 'process' kan niet worden verwerkt. . Fout: "waarde niet converteren Hallo"System.Diagnostics.Process (CcmExec)"van het type"Deserialized.System.Diagnostics.Process"tootype"System.Diagnostics.Process".*   Dit komt doordat er is dat een niet-overeenkomend gegevenstype tussen Hallo verwacht type [System.Diagnostic.Process] en Hallo opgegeven type [Deserialized.System.Diagnostic.Process]. Hallo manier om dit probleem is tooensure Hallo cmdlets van uw module geen complexe typen voor parameters rekening. Hier volgt Hallo verkeerde manier toodo deze.
   
    ```
    function Get-ProcessDescription {
      param (
            [System.Diagnostic.Process] $process
      )
      $process.Description
    }
    ``` 
    <br>
    En hier is Hallo juiste manier, een primitieve die intern kan worden gebruikt door de cmdlet Hallo nemen toograb Hallo complexe object en deze gebruiken. Aangezien de cmdlets worden uitgevoerd in de context van PowerShell hello, wordt niet PowerShell Workflow, in Hallo cmdlet $process Hallo juiste [System.Diagnostic.Process] type.  
   
    ```
    function Get-ProcessDescription {
      param (
            [String] $processName
      )
      $process = Get-Process -Name $processName
   
      $process.Description
    }
    ```
   <br>
   Verbindingsassets in runbooks zijn hashtabellen, die een complex type zijn, en toch lijken deze hashtabellen toobe kunnen toobe doorgegeven in cmdlets voor hun-Connection-parameter, met zonder gecaste uitzondering. In technisch opzicht kunnen sommige PowerShell-typen kunnen toocast van hun geserialiseerde vorm tootheir gedeserialiseerd formulier correct zijn en kunnen daarom worden doorgegeven in cmdlets voor parameters Hallo niet-gedeserialiseerde type accepteren. Hashtabel is daar een van. Het is mogelijk een module-auteur gedefinieerde typen toobe geïmplementeerd op een manier die ze kunnen correct kan deserialiseren, maar er zijn enkele tooconsider-en nadelen. type behoeften toohave een standaardconstructor Hello, hebben alle van de bijbehorende openbare eigenschappen en een PSTypeConverter hebben. Echter, voor al gedefinieerde typen die Hallo module-auteur heeft geen eigenaar bent, is er niet veel te 'oplost', vandaar Hallo aanbeveling tooavoid complexe typen voor parameters helemaal. Ontwerpen van een Runbook tip: als om sommige uw cmdlets reden moet een complex tootake typeparameter, of als u van iemand anders module waarvoor een complex typeparameter, het Hallo-oplossing in PowerShell Workflow-runbooks en PowerShell Workflows in lokale PowerShell is toowrap Hallo cmdlet waarmee het complexe type Hallo wordt gegenereerd en Hallo cmdlet die Hallo complex type in Hallo verbruikt dezelfde InlineScript-activiteit. Aangezien InlineScript wordt de inhoud ervan uitgevoerd als PowerShell in plaats van PowerShell Workflow, Hallo cmdlet Hallo complexe type wordt gegenereerd, dat correcte type zou produceren, gedeserialiseerd niet Hallo complex type zijn.
5. Maak alle cmdlets in Hallo module staatloos. PowerShell Workflow wordt elke cmdlet in Hallo werkstroom aangeroepen in een andere sessie uitgevoerd. Dit betekent dat cmdlets die afhankelijk van de sessiestatus gemaakt zijn / gewijzigd door andere cmdlets in dezelfde module niet in PowerShell Workflow-runbooks werken zullen Hallo.  Hier volgt een voorbeeld van wat niet toodo.
   
    ```
    $globalNum = 0
    function Set-GlobalNum {
       param(
           [int] $num
       )
   
       $globalNum = $num
    }
    function Get-GlobalNumTimesTwo {
       $output = $globalNum * 2
   
       $output
    }
    ```
   <br>
6. Hallo module moet volledig zijn opgenomen in een pakket waarvoor Xcopy kan. Omdat Azure Automation-modules gedistribueerde toohello Automation-sandboxes zijn wanneer runbooks tooexecute moeten, moeten ze toowork onafhankelijk van Hallo host die ze worden uitgevoerd. Dit betekent dat u moet kunnen tooZip Hallo module pakket, verplaatst u het tooany andere host met dezelfde of een nieuwere versie van PowerShell Hallo en laat het laten functioneren wanneer het in die host PowerShell-omgeving geïmporteerd. In de volgorde voor die toohappen moet Hallo module niet afhankelijk zijn van bestanden buiten Hallo modulemap (Hallo die wordt gezipt wanneer u in Azure Automation importeert) of op unieke registerinstellingen op een host, zoals die zijn ingesteld door Hallo installeren van een product. Als deze aanbevolen procedure niet wordt gevolgd, Hallo-module worden niet kan worden gebruikt in Azure Automation.  

## <a name="next-steps"></a>Volgende stappen

* tooget gestart met PowerShell workflow-runbooks, Zie [Mijn eerste PowerShell workflow-runbook](automation-first-runbook-textual.md)
* toolearn meer informatie over het maken van PowerShell-Modules, Zie [een Windows PowerShell-Module schrijven](https://msdn.microsoft.com/library/dd878310%28v=vs.85%29.aspx)

