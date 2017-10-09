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
# <a name="azure-automation-integration-modules"></a><span data-ttu-id="fc7d8-103">Azure Automation-integratiemodules</span><span class="sxs-lookup"><span data-stu-id="fc7d8-103">Azure Automation Integration Modules</span></span>
<span data-ttu-id="fc7d8-104">PowerShell is Hallo basistechnologie achter Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-104">PowerShell is hello fundamental technology behind Azure Automation.</span></span> <span data-ttu-id="fc7d8-105">Omdat Azure Automation is gebouwd op PowerShell, zijn de PowerShell-modules sleutel toohello uitbreidbaarheid van Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-105">Since Azure Automation is built on PowerShell, PowerShell modules are key toohello extensibility of Azure Automation.</span></span> <span data-ttu-id="fc7d8-106">In dit artikel we leidt u door het Hallo-details van het gebruik van Azure Automation van PowerShell-modules, tooas 'Integratiemodules' waarnaar wordt verwezen en aanbevolen procedures voor het maken van uw eigen PowerShell-modules toomake zeker van te zijn dat ze werken als integratiemodules binnen Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-106">In this article, we will guide you through hello specifics of Azure Automation’s use of PowerShell modules, referred tooas “Integration Modules”, and best practices for creating your own PowerShell modules toomake sure they work as Integration Modules within Azure Automation.</span></span> 

## <a name="what-is-a-powershell-module"></a><span data-ttu-id="fc7d8-107">Wat is een PowerShell-module?</span><span class="sxs-lookup"><span data-stu-id="fc7d8-107">What is a PowerShell Module?</span></span>
<span data-ttu-id="fc7d8-108">Een PowerShell-module is een groep PowerShell-cmdlets, zoals **Get-Date** of **Copy-Item**, die kan worden gebruikt vanuit Hallo PowerShell-console, scripts, werkstromen, runbooks en PowerShell DSC-resources, zoals WindowsFeature of File, die kan worden gebruikt vanuit PowerShell DSC-configuraties.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-108">A PowerShell module is a group of PowerShell cmdlets like **Get-Date** or **Copy-Item**, that can be used from hello PowerShell console, scripts, workflows, runbooks, and PowerShell DSC resources like WindowsFeature or File, that can be used from PowerShell DSC configurations.</span></span> <span data-ttu-id="fc7d8-109">Hallo-functionaliteit van PowerShell is zichtbaar via cmdlets en DSC-resources en elke cmdlet/DSC-resource wordt ondersteund door een PowerShell-module veel van die worden geleverd met PowerShell zelf.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-109">All of hello functionality of PowerShell is exposed through cmdlets and DSC resources, and every cmdlet/DSC resource is backed by a PowerShell module, many of which ship with PowerShell itself.</span></span> <span data-ttu-id="fc7d8-110">Bijvoorbeeld, Hallo **Get-Date** cmdlet maakt deel uit van Hallo PowerShell-module Microsoft.PowerShell.Utility en **Copy-Item** cmdlet maakt deel uit van Hallo PowerShell-module Microsoft.PowerShell.Management en Hallo Package DSC-resource maakt deel uit van Hallo PowerShell-module PSDesiredStateConfiguration.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-110">For example, hello **Get-Date** cmdlet is part of hello Microsoft.PowerShell.Utility PowerShell module, and **Copy-Item** cmdlet is part of hello Microsoft.PowerShell.Management PowerShell module and hello Package DSC resource is part of hello PSDesiredStateConfiguration PowerShell module.</span></span> <span data-ttu-id="fc7d8-111">Deze modules worden geleverd met PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-111">Both of these modules ship with PowerShell.</span></span> <span data-ttu-id="fc7d8-112">Maar veel PowerShell-modules niet worden geleverd als onderdeel van PowerShell en in plaats daarvan met de eerste of van derden producten zoals System Center 2012 Configuration Manager of door Hallo enorme PowerShell-community op locaties zoals PowerShell Gallery worden gedistribueerd.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-112">But many PowerShell modules do not ship as part of PowerShell, and are instead distributed with first or third-party products like System Center 2012 Configuration Manager or by hello vast PowerShell community on places like PowerShell Gallery.</span></span>  <span data-ttu-id="fc7d8-113">Hallo-modules zijn nuttig omdat ze complexe taken eenvoudiger via ingekapselde functionaliteit.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-113">hello modules are useful because they make complex tasks simpler through encapsulated functionality.</span></span>  <span data-ttu-id="fc7d8-114">Meer informatie over [PowerShell-modules vindt u op MSDN](https://msdn.microsoft.com/library/dd878324%28v=vs.85%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="fc7d8-114">You can learn more about [PowerShell modules on MSDN](https://msdn.microsoft.com/library/dd878324%28v=vs.85%29.aspx).</span></span> 

## <a name="what-is-an-azure-automation-integration-module"></a><span data-ttu-id="fc7d8-115">Wat is een Azure Automation-integratiemodule?</span><span class="sxs-lookup"><span data-stu-id="fc7d8-115">What is an Azure Automation Integration Module?</span></span>
<span data-ttu-id="fc7d8-116">Een integratiemodule verschilt niet heel veel van een PowerShell-module.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-116">An Integration Module isn't very different from a PowerShell module.</span></span> <span data-ttu-id="fc7d8-117">De gewoon een PowerShell-module die desgewenst één extra bestand - een metagegevensbestand waarin een Azure Automation verbinding type toobe gebruikt met de cmdlets Hallo-module in runbooks bevat.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-117">Its simply a PowerShell module that optionally contains one additional file - a metadata file specifying an Azure Automation connection type toobe used with hello module's cmdlets in runbooks.</span></span> <span data-ttu-id="fc7d8-118">Optioneel bestand of niet, deze PowerShell-modules kunnen worden geïmporteerd in Azure Automation toomake hun cmdlets beschikbaar voor gebruik in runbooks en de bijbehorende DSC-resources beschikbaar voor gebruik in DSC-configuraties.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-118">Optional file or not, these PowerShell modules can be imported into Azure Automation toomake their cmdlets available for use within runbooks and their DSC resources available for use within DSC configurations.</span></span> <span data-ttu-id="fc7d8-119">Achter de schermen hello, Azure Automation slaat deze modules en worden ze op runbooktaken en DSC-compilatie uitvoeringstijd in hello Azure Automation-sandboxes geladen waar runbooks worden uitgevoerd en DSC-configuraties worden gecompileerd.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-119">Behind hello scenes, Azure Automation stores these modules, and at runbook job and DSC compilation job execution time, loads them into hello Azure Automation sandboxes where runbooks are executed and DSC configurations are compiled.</span></span>  <span data-ttu-id="fc7d8-120">Eventuele DSC-resources in modules worden ook automatisch geplaatst op Hallo Automation DSC-pull-server, zodat ze kunnen worden opgehaald door machines waarmee wordt geprobeerd tooapply DSC-configuraties.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-120">Any DSC resources in modules are also automatically placed on hello Automation DSC pull server, so that they can be pulled by machines attempting tooapply DSC configurations.</span></span>  

<span data-ttu-id="fc7d8-121">We verzenden een aantal Azure PowerShell-modules out of box Hallo in Azure Automation voor toouse u zodat u kunt aan de slag meteen automatiseren van Azure-beheer, maar u kunt de PowerShell-modules voor elk systeem, service of hulpprogramma dat u wilt dat toointegrate met importeren.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-121">We ship a number of Azure  PowerShell modules out of hello box in Azure Automation for you toouse so you can get started automating Azure management right away, but you can import PowerShell modules for whatever system, service, or tool you want toointegrate with.</span></span> 

> [!NOTE]
> <span data-ttu-id="fc7d8-122">Bepaalde modules worden verzonden als 'globale modules' in hello Automation-service.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-122">Certain modules are shipped as “global modules” in hello Automation service.</span></span> <span data-ttu-id="fc7d8-123">Deze globale modules zijn beschikbaar tooyou wanneer u een automation-account maakt, en we ze soms bijwerken die u ze automatisch tooyour automation-account implementeert.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-123">These global modules are available tooyou when you create an automation account, and we update them sometimes which automatically pushes them out tooyour automation account.</span></span> <span data-ttu-id="fc7d8-124">Als u niet dat deze wilt automatisch wordt bijgewerkt, kunt u altijd importeren toobe Hallo in dezelfde module zelf en die voorrang boven algemene moduleversie Hallo van die module die we in Hallo-service worden geleverd.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-124">If you don’t want them toobe auto-updated, you can always import hello same module yourself, and that will take precedence over hello global module version of that module that we ship in hello service.</span></span> 

<span data-ttu-id="fc7d8-125">Hallo-indeling op waarin u een integratiemodulepakket importeert is een gecomprimeerd bestand met dezelfde naam als Hallo-module en met een .zip-extensie Hallo.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-125">hello format in which you import an Integration Module package is a compressed file with hello same name as hello module and a .zip extension.</span></span> <span data-ttu-id="fc7d8-126">Het bevat Hallo Windows PowerShell-module en ondersteunende bestanden, inclusief een manifestbestand (.psd1) als het Hallo-module heeft een.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-126">It contains hello Windows PowerShell module and any supporting files, including a manifest file (.psd1) if hello module has one.</span></span>

<span data-ttu-id="fc7d8-127">Als een Azure Automation-verbindingstype Hallo-module bevat, moet deze ook een bestand met de naam Hallo bevatten `<ModuleName>-Automation.json` Hiermee worden de eigenschappen van verbindingstype Hallo.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-127">If hello module should contain an Azure Automation connection type, it must also contain a file with hello name `<ModuleName>-Automation.json` that specifies hello connection type properties.</span></span> <span data-ttu-id="fc7d8-128">Dit is een json-bestand in de modulemap Hallo van uw gecomprimeerde ZIP-bestand geplaatst en Hallo velden bevat een 'verbinding' die is vereist tooconnect toohello systeem of Hallo servicemodule vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-128">This is a json file placed within hello module folder of your compressed .zip file, and contains hello fields of a “connection” that is required tooconnect toohello system or service hello module represents.</span></span> <span data-ttu-id="fc7d8-129">Uiteindelijk wordt hiermee een verbindingstype gemaakt in Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-129">This will end up creating a connection type in Azure Automation.</span></span> <span data-ttu-id="fc7d8-130">Gebruik van dit bestand kunt u de veldnamen hello, instellen van het type, en of Hallo velden moeten worden versleuteld en / of optioneel, voor het verbindingstype Hallo van Hallo-module.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-130">Using this file you can set hello field names, types, and whether hello fields should be encrypted and / or optional, for hello connection type of hello module.</span></span> <span data-ttu-id="fc7d8-131">Hallo hieronder vindt u een sjabloon in Hallo json-bestandsindeling:</span><span class="sxs-lookup"><span data-stu-id="fc7d8-131">hello following is a template in hello json file format:</span></span>

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

<span data-ttu-id="fc7d8-132">Als u Service Management Automation hebt geïmplementeerd en integratiemodulepakketten voor uw automation-runbooks, moet dit bekend tooyou eruitzien.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-132">If you have deployed Service Management Automation and created Integration Modules packages for your automation runbooks, this should look very familiar tooyou.</span></span> 

## <a name="authoring-best-practices"></a><span data-ttu-id="fc7d8-133">Aanbevolen procedures voor ontwerpen</span><span class="sxs-lookup"><span data-stu-id="fc7d8-133">Authoring Best Practices</span></span>
<span data-ttu-id="fc7d8-134">Hoewel integratiemodules in feite PowerShell-modules, er nog steeds een aantal zaken we u aan moet denken bij het ontwerpen van een PowerShell-module toomake deze zo bruikbaar in Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-134">Even though Integration Modules are essentially PowerShell modules, there’s still a number of things we recommend you consider while authoring a PowerShell module, toomake it most usable in Azure Automation.</span></span> <span data-ttu-id="fc7d8-135">Sommige hiervan zijn specifiek voor Azure Automation en sommige zijn nuttig alleen toomake uw modules goed in PowerShell Workflow werkt, ongeacht of u Automation gebruikt.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-135">Some of these are Azure Automation specific, and some of them are useful just toomake your modules work well in PowerShell Workflow, regardless of whether or not you’re using Automation.</span></span> 

1. <span data-ttu-id="fc7d8-136">Neem een samenvatting, beschrijving en help-URI voor elke cmdlet in Hallo-module.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-136">Include a synopsis, description, and help URI for every cmdlet in hello module.</span></span> <span data-ttu-id="fc7d8-137">In PowerShell kunt u bepaalde help-informatie voor cmdlets tooallow hello tooreceive Help-informatie over het gebruik van deze Hello **Get-Help** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-137">In PowerShell, you can define certain help information for cmdlets tooallow hello user tooreceive help on using them with hello **Get-Help** cmdlet.</span></span> <span data-ttu-id="fc7d8-138">U kunt bijvoorbeeld als volgt een samenvatting en Help-URI definiëren voor een PowerShell-module, geschreven in een PSM1-bestand.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-138">For example, here’s how you can define a synopsis and help URI for a PowerShell module written in a .psm1 file.</span></span><br>  
   
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
   <br> <span data-ttu-id="fc7d8-139">Deze gegevens bieden niet alleen getoond deze informatie over het gebruik van Hallo **Get-Help** cmdlet in PowerShell-console Hallo, deze wordt ook weergegeven in dit help-functionaliteit in Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-139">Providing this info will not only show this help using hello **Get-Help** cmdlet in hello PowerShell console, it will also expose this help functionality within Azure Automation.</span></span>  <span data-ttu-id="fc7d8-140">Bijvoorbeeld wanneer u activiteiten invoegt tijdens het ontwerpen van een runbook.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-140">For example, when inserting activities during runbook authoring.</span></span> <span data-ttu-id="fc7d8-141">Te klikken op 'Gedetailleerde help weergeven' wordt geopend Hallo help-URI in een ander tabblad van Hallo webbrowser u tooaccess Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-141">Clicking “View detailed help” will open hello help URI in another tab of hello web browser you’re using tooaccess Azure Automation.</span></span><br><span data-ttu-id="fc7d8-142">![Help bij integratiemodules](media/automation-integration-modules/automation-integration-module-activitydesc.png)</span><span class="sxs-lookup"><span data-stu-id="fc7d8-142">![Integration Module Help](media/automation-integration-modules/automation-integration-module-activitydesc.png)</span></span>
2. <span data-ttu-id="fc7d8-143">Als de module Hallo wordt uitgevoerd op een extern systeem</span><span class="sxs-lookup"><span data-stu-id="fc7d8-143">If hello module runs against a remote system,</span></span>

    <span data-ttu-id="fc7d8-144">a.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-144">a.</span></span> <span data-ttu-id="fc7d8-145">Een integratiemodule metagegevensbestand die Hallo informatie die nodig is tooconnect toothat externe systeem definieert, dus Hallo verbindingstype moet bevatten.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-145">It should contain an Integration Module metadata file that defines hello information needed tooconnect toothat remote system, meaning hello connection type.</span></span>  
    <span data-ttu-id="fc7d8-146">b.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-146">b.</span></span> <span data-ttu-id="fc7d8-147">Elke cmdlet in de module Hallo moet kunnen tootake een verbindingsobject (een exemplaar van dat verbindingstype) als een parameter.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-147">Each cmdlet in hello module should be able tootake in a connection object (an instance of that connection type) as a parameter.</span></span>  

    <span data-ttu-id="fc7d8-148">Cmdlets in Hallo-module worden eenvoudiger toouse in Azure Automation als u toestaat dat een object met de velden van het verbindingstype Hallo Hallo doorgeven als een parameter toohello-cmdlet.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-148">Cmdlets in hello module become easier toouse in Azure Automation if you allow passing an object with hello fields of hello connection type as a parameter toohello cmdlet.</span></span> <span data-ttu-id="fc7d8-149">Deze manier gebruikers hebben geen toomap parameters van de overeenkomstige parameters Hallo verbinding asset toohello van cmdlet telkens wanneer die ze een cmdlet aanroepen.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-149">This way users don’t have toomap parameters of hello connection asset toohello cmdlet's corresponding parameters each time they call a cmdlet.</span></span> <span data-ttu-id="fc7d8-150">Op basis van Hallo runbook in bovenstaand voorbeeld, wordt gebruikt een Twilio-verbindingsasset genaamd corptwilio gebruikt tooaccess Twilio en retourneren van alle Hallo telefoonnummers in Hallo-account.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-150">Based on hello runbook example above, it uses a Twilio connection asset called CorpTwilio tooaccess Twilio and return all hello phone numbers in hello account.</span></span>  <span data-ttu-id="fc7d8-151">U ziet hoe het Hallo-velden van Hallo verbindingsparameters toohello van Hallo cmdlet toewijzen?</span><span class="sxs-lookup"><span data-stu-id="fc7d8-151">Notice how it is mapping hello fields of hello connection toohello parameters of hello cmdlet?</span></span><br>
   
    ```
    workflow Get-CorpTwilioPhones
    {
      $CorpTwilio = Get-AutomationConnection -Name 'CorpTwilio'
   
      Get-TwilioPhoneNumbers 
        -AccountSid $CorpTwilio.AccountSid  
        -AuthToken $CorptTwilio.AuthToken
    }
    ```
  
    <span data-ttu-id="fc7d8-152">Een eenvoudigere en betere manier tooapproach dit is het rechtstreeks doorgeven Hallo verbinding object toohello cmdlet-</span><span class="sxs-lookup"><span data-stu-id="fc7d8-152">An easier and better way tooapproach this is directly passing hello connection object toohello cmdlet -</span></span>
   
    ```
    workflow Get-CorpTwilioPhones
    {
      $CorpTwilio = Get-AutomationConnection -Name 'CorpTwilio'
   
      Get-TwilioPhoneNumbers -Connection $CorpTwilio
    }
    ```
   
    <span data-ttu-id="fc7d8-153">U kunt gedrag voor uw cmdlets door hen tooaccept een verbindingsobject rechtstreeks als een parameter, in plaats van alleen Verbindingsvelden voor parameters inschakelen.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-153">You can enable behavior like this for your cmdlets by allowing them tooaccept a connection object directly as a parameter, instead of just connection fields for parameters.</span></span> <span data-ttu-id="fc7d8-154">Doorgaans wilt u een parameter die is ingesteld voor elk, zodat een gebruiker die niet met behulp van Azure Automation uw cmdlets aanroepen kan zonder een hashtabel tooact als Hallo-verbindingsobject maken.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-154">Usually you’ll want a parameter set for each, so that a user not using Azure Automation can call your cmdlets without constructing a hashtable tooact as hello connection object.</span></span> <span data-ttu-id="fc7d8-155">Parameterset **SpecifyConnectionFields** hieronder vindt u gebruikte toopass Hallo veld verbindingseigenschappen één voor één.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-155">Parameter set **SpecifyConnectionFields** below is used toopass hello connection field properties one by one.</span></span> <span data-ttu-id="fc7d8-156">**UseConnectionObject** kunt u doorgeeft Hallo meteen via verbinding.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-156">**UseConnectionObject** lets you pass hello connection straight through.</span></span> <span data-ttu-id="fc7d8-157">Zoals u ziet de cmdlet Send-TwilioSMS in Hallo Hallo [Twilio PowerShell-module](https://gallery.technet.microsoft.com/scriptcenter/Twilio-PowerShell-Module-8a8bfef8) doorgave op beide manieren:</span><span class="sxs-lookup"><span data-stu-id="fc7d8-157">As you can see, hello Send-TwilioSMS cmdlet in hello [Twilio PowerShell module](https://gallery.technet.microsoft.com/scriptcenter/Twilio-PowerShell-Module-8a8bfef8) allows passing either way:</span></span> 
   
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
3. <span data-ttu-id="fc7d8-158">Definieer het uitvoertype voor alle cmdlets in Hallo-module.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-158">Define output type for all cmdlets in hello module.</span></span> <span data-ttu-id="fc7d8-159">Een uitvoertype definiëren voor een cmdlet ontwerptijd IntelliSense kunt uitvoer toohelp bepalen van Hallo eigenschappen van de cmdlet hello, voor gebruik tijdens het ontwerpen van.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-159">Defining an output type for a cmdlet allows design-time IntelliSense toohelp you determine hello output properties of hello cmdlet, for use during authoring.</span></span> <span data-ttu-id="fc7d8-160">Het is vooral nuttig tijdens Automation runbook grafisch ontwerpen, waarbij ontwerptijdkennis key tooan goede gebruikerservaring met uw module is.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-160">It is especially helpful during Automation runbook graphical authoring, where design time knowledge is key tooan easy user experience with your module.</span></span><br><br> <span data-ttu-id="fc7d8-161">![Uitvoertype grafisch runbook](media/automation-integration-modules/runbook-graphical-module-output-type.png)</span><span class="sxs-lookup"><span data-stu-id="fc7d8-161">![Graphical Runbook Output Type](media/automation-integration-modules/runbook-graphical-module-output-type.png)</span></span><br> <span data-ttu-id="fc7d8-162">Dit is vergelijkbaar toohello 'vooruit Typ' functionaliteit van een cmdlet-uitvoer in PowerShell ISE zonder toorun deze.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-162">This is similar toohello "type ahead" functionality of a cmdlet's output in PowerShell ISE without having toorun it.</span></span><br><br> <span data-ttu-id="fc7d8-163">![POSH IntelliSense](media/automation-integration-modules/automation-posh-ise-intellisense.png)</span><span class="sxs-lookup"><span data-stu-id="fc7d8-163">![POSH IntelliSense](media/automation-integration-modules/automation-posh-ise-intellisense.png)</span></span><br>
4. <span data-ttu-id="fc7d8-164">Cmdlets in Hallo-module neemt niet complexe objecttypen voor parameters.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-164">Cmdlets in hello module should not take complex object types for parameters.</span></span> <span data-ttu-id="fc7d8-165">PowerShell Workflow verschilt van PowerShell in het volgende opzicht: complexe typen worden in gedeserialiseerde vorm opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-165">PowerShell Workflow is different from PowerShell in that it stores complex types in deserialized form.</span></span> <span data-ttu-id="fc7d8-166">Primitieve typen blijven primitieven, maar complexe typen worden geconverteerd tootheir gedeserialiseerd versies, die in wezen Eigenschappenverzamelingen zijn.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-166">Primitive types will stay as primitives, but complex types are converted tootheir deserialized versions, which are essentially property bags.</span></span> <span data-ttu-id="fc7d8-167">Als u Hallo gebruikt bijvoorbeeld **Get-Process** cmdlet in een runbook (of een PowerShell-werkstroom eigenlijk), zou het retourneren van een object van type [Deserialized.System.Diagnostic.Process], niet Hallo verwachte [ Type System.Diagnostic.Process].</span><span class="sxs-lookup"><span data-stu-id="fc7d8-167">For example, if you used hello **Get-Process** cmdlet in a runbook (or a PowerShell Workflow for that matter), it would return an object of type [Deserialized.System.Diagnostic.Process], not hello expected [System.Diagnostic.Process] type.</span></span> <span data-ttu-id="fc7d8-168">Dit type heeft alle Hallo dezelfde eigenschappen als niet-gedeserialiseerde type, maar geen van de methoden Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-168">This type has all hello same properties as hello non-deserialized type, but none of hello methods.</span></span> <span data-ttu-id="fc7d8-169">En als u toopass deze waarde als een parameter tooa cmdlet probeert, waarbij Hallo cmdlet een waarde [System.Diagnostic.Process] voor deze parameter verwacht, ontvangt u Hallo volgende fout: *argumenttransformatie voor parameter 'process' kan niet worden verwerkt. . Fout: "waarde niet converteren Hallo"System.Diagnostics.Process (CcmExec)"van het type"Deserialized.System.Diagnostics.Process"tootype"System.Diagnostics.Process".*</span><span class="sxs-lookup"><span data-stu-id="fc7d8-169">And if you try toopass this value as a parameter tooa cmdlet, where hello cmdlet expects a [System.Diagnostic.Process] value for this parameter, you’ll receive hello following error: *Cannot process argument transformation on parameter 'process'. Error: "Cannot convert hello "System.Diagnostics.Process (CcmExec)" value of type  "Deserialized.System.Diagnostics.Process" tootype "System.Diagnostics.Process".*</span></span>   <span data-ttu-id="fc7d8-170">Dit komt doordat er is dat een niet-overeenkomend gegevenstype tussen Hallo verwacht type [System.Diagnostic.Process] en Hallo opgegeven type [Deserialized.System.Diagnostic.Process].</span><span class="sxs-lookup"><span data-stu-id="fc7d8-170">This is because there is a type mismatch between hello expected [System.Diagnostic.Process] type and hello given [Deserialized.System.Diagnostic.Process] type.</span></span> <span data-ttu-id="fc7d8-171">Hallo manier om dit probleem is tooensure Hallo cmdlets van uw module geen complexe typen voor parameters rekening.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-171">hello way around this issue is tooensure hello cmdlets of your module do not take complex types for parameters.</span></span> <span data-ttu-id="fc7d8-172">Hier volgt Hallo verkeerde manier toodo deze.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-172">Here is hello wrong way toodo it.</span></span>
   
    ```
    function Get-ProcessDescription {
      param (
            [System.Diagnostic.Process] $process
      )
      $process.Description
    }
    ``` 
    <br>
    <span data-ttu-id="fc7d8-173">En hier is Hallo juiste manier, een primitieve die intern kan worden gebruikt door de cmdlet Hallo nemen toograb Hallo complexe object en deze gebruiken.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-173">And here is hello right way, taking in a primitive that can be used internally by hello cmdlet toograb hello complex object and use it.</span></span> <span data-ttu-id="fc7d8-174">Aangezien de cmdlets worden uitgevoerd in de context van PowerShell hello, wordt niet PowerShell Workflow, in Hallo cmdlet $process Hallo juiste [System.Diagnostic.Process] type.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-174">Since cmdlets execute in hello context of PowerShell, not PowerShell Workflow, inside hello cmdlet $process becomes hello correct [System.Diagnostic.Process] type.</span></span>  
   
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
   <span data-ttu-id="fc7d8-175">Verbindingsassets in runbooks zijn hashtabellen, die een complex type zijn, en toch lijken deze hashtabellen toobe kunnen toobe doorgegeven in cmdlets voor hun-Connection-parameter, met zonder gecaste uitzondering.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-175">Connection assets in runbooks are hashtables, which are a complex type, and yet these hashtables seem toobe able toobe passed into cmdlets for their –Connection parameter perfectly, with no cast exception.</span></span> <span data-ttu-id="fc7d8-176">In technisch opzicht kunnen sommige PowerShell-typen kunnen toocast van hun geserialiseerde vorm tootheir gedeserialiseerd formulier correct zijn en kunnen daarom worden doorgegeven in cmdlets voor parameters Hallo niet-gedeserialiseerde type accepteren.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-176">Technically, some PowerShell types are able toocast properly from their serialized form tootheir deserialized form, and hence can be passed into cmdlets for parameters accepting hello non-deserialized type.</span></span> <span data-ttu-id="fc7d8-177">Hashtabel is daar een van.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-177">Hashtable is one of these.</span></span> <span data-ttu-id="fc7d8-178">Het is mogelijk een module-auteur gedefinieerde typen toobe geïmplementeerd op een manier die ze kunnen correct kan deserialiseren, maar er zijn enkele tooconsider-en nadelen.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-178">It’s possible for a module author’s defined types toobe implemented in a way that they can correctly deserialize as well, but there are some trade-offs tooconsider.</span></span> <span data-ttu-id="fc7d8-179">type behoeften toohave een standaardconstructor Hello, hebben alle van de bijbehorende openbare eigenschappen en een PSTypeConverter hebben.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-179">hello type needs toohave a default constructor, have all of its properties public, and have a PSTypeConverter.</span></span> <span data-ttu-id="fc7d8-180">Echter, voor al gedefinieerde typen die Hallo module-auteur heeft geen eigenaar bent, is er niet veel te 'oplost', vandaar Hallo aanbeveling tooavoid complexe typen voor parameters helemaal.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-180">However, for already-defined types that hello module author does not own, there is no way too“fix” them, hence hello recommendation tooavoid complex types for parameters all together.</span></span> <span data-ttu-id="fc7d8-181">Ontwerpen van een Runbook tip: als om sommige uw cmdlets reden moet een complex tootake typeparameter, of als u van iemand anders module waarvoor een complex typeparameter, het Hallo-oplossing in PowerShell Workflow-runbooks en PowerShell Workflows in lokale PowerShell is toowrap Hallo cmdlet waarmee het complexe type Hallo wordt gegenereerd en Hallo cmdlet die Hallo complex type in Hallo verbruikt dezelfde InlineScript-activiteit.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-181">Runbook Authoring tip: If for some reason your cmdlets need tootake a complex type parameter, or you are using someone else’s module that requires a complex type parameter, hello workaround in PowerShell Workflow runbooks and PowerShell Workflows in local PowerShell, is toowrap hello cmdlet that generates hello complex type and hello cmdlet that consumes hello complex type in hello same InlineScript activity.</span></span> <span data-ttu-id="fc7d8-182">Aangezien InlineScript wordt de inhoud ervan uitgevoerd als PowerShell in plaats van PowerShell Workflow, Hallo cmdlet Hallo complexe type wordt gegenereerd, dat correcte type zou produceren, gedeserialiseerd niet Hallo complex type zijn.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-182">Since InlineScript executes its contents as PowerShell rather than PowerShell Workflow, hello cmdlet generating hello complex type would produce that correct type, not hello deserialized complex type.</span></span>
5. <span data-ttu-id="fc7d8-183">Maak alle cmdlets in Hallo module staatloos.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-183">Make all cmdlets in hello module stateless.</span></span> <span data-ttu-id="fc7d8-184">PowerShell Workflow wordt elke cmdlet in Hallo werkstroom aangeroepen in een andere sessie uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-184">PowerShell Workflow runs every cmdlet called in hello workflow in a different session.</span></span> <span data-ttu-id="fc7d8-185">Dit betekent dat cmdlets die afhankelijk van de sessiestatus gemaakt zijn / gewijzigd door andere cmdlets in dezelfde module niet in PowerShell Workflow-runbooks werken zullen Hallo.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-185">This means any cmdlets that depend on session state created / modified by other cmdlets in hello same module will not work in PowerShell Workflow runbooks.</span></span>  <span data-ttu-id="fc7d8-186">Hier volgt een voorbeeld van wat niet toodo.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-186">Here is an example of what not toodo.</span></span>
   
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
6. <span data-ttu-id="fc7d8-187">Hallo module moet volledig zijn opgenomen in een pakket waarvoor Xcopy kan.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-187">hello module should be fully contained in an Xcopy-able package.</span></span> <span data-ttu-id="fc7d8-188">Omdat Azure Automation-modules gedistribueerde toohello Automation-sandboxes zijn wanneer runbooks tooexecute moeten, moeten ze toowork onafhankelijk van Hallo host die ze worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-188">Because Azure Automation modules are distributed toohello Automation sandboxes when runbooks need tooexecute, they need toowork independently of hello host they are running on.</span></span> <span data-ttu-id="fc7d8-189">Dit betekent dat u moet kunnen tooZip Hallo module pakket, verplaatst u het tooany andere host met dezelfde of een nieuwere versie van PowerShell Hallo en laat het laten functioneren wanneer het in die host PowerShell-omgeving geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-189">What this means is that you should be able tooZip up hello module package, move it tooany other host with hello same or newer PowerShell version, and have it function as normal when imported into that host’s PowerShell environment.</span></span> <span data-ttu-id="fc7d8-190">In de volgorde voor die toohappen moet Hallo module niet afhankelijk zijn van bestanden buiten Hallo modulemap (Hallo die wordt gezipt wanneer u in Azure Automation importeert) of op unieke registerinstellingen op een host, zoals die zijn ingesteld door Hallo installeren van een product.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-190">In order for that toohappen, hello module should not depend on any files outside hello module folder (hello folder that gets zipped up when importing into Azure Automation), or on any unique registry settings on a host, such as those set by hello install of a product.</span></span> <span data-ttu-id="fc7d8-191">Als deze aanbevolen procedure niet wordt gevolgd, Hallo-module worden niet kan worden gebruikt in Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="fc7d8-191">If this best practice is not followed, hello module will not be usable in Azure Automation.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="fc7d8-192">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fc7d8-192">Next steps</span></span>

* <span data-ttu-id="fc7d8-193">tooget gestart met PowerShell workflow-runbooks, Zie [Mijn eerste PowerShell workflow-runbook](automation-first-runbook-textual.md)</span><span class="sxs-lookup"><span data-stu-id="fc7d8-193">tooget started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span>
* <span data-ttu-id="fc7d8-194">toolearn meer informatie over het maken van PowerShell-Modules, Zie [een Windows PowerShell-Module schrijven](https://msdn.microsoft.com/library/dd878310%28v=vs.85%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="fc7d8-194">toolearn more about creating PowerShell Modules, see [Writing a Windows PowerShell Module](https://msdn.microsoft.com/library/dd878310%28v=vs.85%29.aspx)</span></span>

