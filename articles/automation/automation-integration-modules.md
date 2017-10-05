---
title: <span data-ttu-id="59a27-101">Een Azure Automation-integratiemodule maken | Microsoft Docs</span><span class="sxs-lookup"><span data-stu-id="59a27-101">Create an Azure Automation Integration Module | Microsoft Docs</span></span>
description: <span data-ttu-id="59a27-102">Zelfstudie die u helpt bij het maken, testen en bij het voorbeeldgebruik van integratiemodules in Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="59a27-102">Tutorial that walks you through the creation, testing, and example use of  integration modules in Azure Automation.</span></span>
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
ms.openlocfilehash: aeb06276a52e5472667ae0a741fb3007a91910fe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-automation-integration-modules"></a><span data-ttu-id="59a27-103">Azure Automation-integratiemodules</span><span class="sxs-lookup"><span data-stu-id="59a27-103">Azure Automation Integration Modules</span></span>
<span data-ttu-id="59a27-104">PowerShell is de basistechnologie achter Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="59a27-104">PowerShell is the fundamental technology behind Azure Automation.</span></span> <span data-ttu-id="59a27-105">Omdat Azure Automation is gebouwd op PowerShell, zijn de PowerShell-modules bepalend voor de uitbreidbaarheid van Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="59a27-105">Since Azure Automation is built on PowerShell, PowerShell modules are key to the extensibility of Azure Automation.</span></span> <span data-ttu-id="59a27-106">In dit artikel worden de details van het gebruik van Azure Automation van PowerShell-modules, die 'integratiemodules' worden genoemd, besproken en de aanbevolen procedures voor het maken van uw eigen PowerShell-modules om er zeker van te zijn dat ze werken als integratiemodules binnen Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="59a27-106">In this article, we will guide you through the specifics of Azure Automation’s use of PowerShell modules, referred to as “Integration Modules”, and best practices for creating your own PowerShell modules to make sure they work as Integration Modules within Azure Automation.</span></span> 

## <a name="what-is-a-powershell-module"></a><span data-ttu-id="59a27-107">Wat is een PowerShell-module?</span><span class="sxs-lookup"><span data-stu-id="59a27-107">What is a PowerShell Module?</span></span>
<span data-ttu-id="59a27-108">Een PowerShell-module is een groep PowerShell-cmdlets, zoals **Get-Date** of **Copy-Item**, die kunnen worden gebruikt vanuit de PowerShell-console, scripts, werkstromen, runbooks en PowerShell DSC-resources, zoals WindowsFeature of File, die kunnen worden gebruikt vanuit PowerShell DSC-configuraties.</span><span class="sxs-lookup"><span data-stu-id="59a27-108">A PowerShell module is a group of PowerShell cmdlets like **Get-Date** or **Copy-Item**, that can be used from the PowerShell console, scripts, workflows, runbooks, and PowerShell DSC resources like WindowsFeature or File, that can be used from PowerShell DSC configurations.</span></span> <span data-ttu-id="59a27-109">Alle functionaliteit van PowerShell is zichtbaar via cmdlets en DSC-resources, en elke cmdlet/DSC-resource wordt ondersteund door een PowerShell-module. Veel van deze modules worden bij PowerShell zelf geleverd.</span><span class="sxs-lookup"><span data-stu-id="59a27-109">All of the functionality of PowerShell is exposed through cmdlets and DSC resources, and every cmdlet/DSC resource is backed by a PowerShell module, many of which ship with PowerShell itself.</span></span> <span data-ttu-id="59a27-110">De cmdlet **Get-Date** maakt bijvoorbeeld deel uit van de PowerShell-module Microsoft.PowerShell.Utility en de cmdlet **Copy-Item** maakt deel uit van de PowerShell-module Microsoft.PowerShell.Management en de Package DSC-resource maakt deel uit van de PowerShell-module PSDesiredStateConfiguration.</span><span class="sxs-lookup"><span data-stu-id="59a27-110">For example, the **Get-Date** cmdlet is part of the Microsoft.PowerShell.Utility PowerShell module, and **Copy-Item** cmdlet is part of the Microsoft.PowerShell.Management PowerShell module and the Package DSC resource is part of the PSDesiredStateConfiguration PowerShell module.</span></span> <span data-ttu-id="59a27-111">Deze modules worden geleverd met PowerShell.</span><span class="sxs-lookup"><span data-stu-id="59a27-111">Both of these modules ship with PowerShell.</span></span> <span data-ttu-id="59a27-112">Maar veel PowerShell-modules worden niet als onderdeel van PowerShell geleverd en worden in plaats daarvan gedistribueerd met producten van Microsoft of van derden zoals System Center 2012 Configuration Manager of door de enorme PowerShell-community op locaties zoals PowerShell Gallery.</span><span class="sxs-lookup"><span data-stu-id="59a27-112">But many PowerShell modules do not ship as part of PowerShell, and are instead distributed with first or third-party products like System Center 2012 Configuration Manager or by the vast PowerShell community on places like PowerShell Gallery.</span></span>  <span data-ttu-id="59a27-113">De modules zijn nuttig omdat ze complexe taken eenvoudiger maken via ingekapselde functionaliteit.</span><span class="sxs-lookup"><span data-stu-id="59a27-113">The modules are useful because they make complex tasks simpler through encapsulated functionality.</span></span>  <span data-ttu-id="59a27-114">Meer informatie over [PowerShell-modules vindt u op MSDN](https://msdn.microsoft.com/library/dd878324%28v=vs.85%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="59a27-114">You can learn more about [PowerShell modules on MSDN](https://msdn.microsoft.com/library/dd878324%28v=vs.85%29.aspx).</span></span> 

## <a name="what-is-an-azure-automation-integration-module"></a><span data-ttu-id="59a27-115">Wat is een Azure Automation-integratiemodule?</span><span class="sxs-lookup"><span data-stu-id="59a27-115">What is an Azure Automation Integration Module?</span></span>
<span data-ttu-id="59a27-116">Een integratiemodule verschilt niet heel veel van een PowerShell-module.</span><span class="sxs-lookup"><span data-stu-id="59a27-116">An Integration Module isn't very different from a PowerShell module.</span></span> <span data-ttu-id="59a27-117">Het is gewoon een PowerShell-module die desgewenst één extra bestand bevat: een metagegevensbestand waarin een Azure Automation-verbindingstype wordt opgegeven dat moet worden gebruikt met de cmdlets van de module in runbooks.</span><span class="sxs-lookup"><span data-stu-id="59a27-117">Its simply a PowerShell module that optionally contains one additional file - a metadata file specifying an Azure Automation connection type to be used with the module's cmdlets in runbooks.</span></span> <span data-ttu-id="59a27-118">Optioneel bestand of niet, deze PowerShell-modules kunnen in Azure Automation worden geïmporteerd om de bijbehorende cmdlets beschikbaar te maken voor gebruik in runbooks en de bijbehorende DSC-resources beschikbaar te maken voor gebruik in DSC-configuraties.</span><span class="sxs-lookup"><span data-stu-id="59a27-118">Optional file or not, these PowerShell modules can be imported into Azure Automation to make their cmdlets available for use within runbooks and their DSC resources available for use within DSC configurations.</span></span> <span data-ttu-id="59a27-119">Achter de schermen worden deze modules in Azure Automation opgeslagen, en bij de uitvoeringstijd van runbooktaken en DSC-compilatietaken worden ze in de Azure Automation-sandboxes geladen waar runbooks worden uitgevoerd en DSC-configuraties worden gecompileerd.</span><span class="sxs-lookup"><span data-stu-id="59a27-119">Behind the scenes, Azure Automation stores these modules, and at runbook job and DSC compilation job execution time, loads them into the Azure Automation sandboxes where runbooks are executed and DSC configurations are compiled.</span></span>  <span data-ttu-id="59a27-120">Eventuele DSC-resources in modules worden ook automatisch op de Automation DSC-pull-server geplaatst, zodat ze kunnen worden opgehaald door machines waarmee wordt geprobeerd DSC-configuraties toe te passen.</span><span class="sxs-lookup"><span data-stu-id="59a27-120">Any DSC resources in modules are also automatically placed on the Automation DSC pull server, so that they can be pulled by machines attempting to apply DSC configurations.</span></span>  

<span data-ttu-id="59a27-121">Een aantal Azure PowerShell-modules worden gebruiksklaar in Azure Automation geleverd zodat u meteen aan de slag kunt gaan met het automatiseren van Azure-beheer, maar u kunt PowerShell-modules importeren voor elk systeem, elke service of elk hulpprogramma waarmee u wilt integreren.</span><span class="sxs-lookup"><span data-stu-id="59a27-121">We ship a number of Azure  PowerShell modules out of the box in Azure Automation for you to use so you can get started automating Azure management right away, but you can import PowerShell modules for whatever system, service, or tool you want to integrate with.</span></span> 

> [!NOTE]
> <span data-ttu-id="59a27-122">Bepaalde modules worden geleverd als ‘algemene modules’ in de service Automation.</span><span class="sxs-lookup"><span data-stu-id="59a27-122">Certain modules are shipped as “global modules” in the Automation service.</span></span> <span data-ttu-id="59a27-123">Wanneer u een Automation-account maakt, zijn deze algemene modules beschikbaar. Wij werken ze soms bij, waarbij de nieuwe versies automatisch in uw Automation-account beschikbaar worden.</span><span class="sxs-lookup"><span data-stu-id="59a27-123">These global modules are available to you when you create an automation account, and we update them sometimes which automatically pushes them out to your automation account.</span></span> <span data-ttu-id="59a27-124">Als u niet wilt dat ze automatisch worden bijgewerkt, kunt u altijd dezelfde module zelf importeren. Die krijgt voorrang op de ‘algemene module’-versie van die module die we bij de service meeleveren.</span><span class="sxs-lookup"><span data-stu-id="59a27-124">If you don’t want them to be auto-updated, you can always import the same module yourself, and that will take precedence over the global module version of that module that we ship in the service.</span></span> 

<span data-ttu-id="59a27-125">De indeling waarin u een integratiemodulepakket importeert, is een gecomprimeerd bestand met dezelfde naam als de module en met een ZIP-extensie.</span><span class="sxs-lookup"><span data-stu-id="59a27-125">The format in which you import an Integration Module package is a compressed file with the same name as the module and a .zip extension.</span></span> <span data-ttu-id="59a27-126">Het bevat de Windows PowerShell-module en ondersteunende bestanden, inclusief een manifestbestand (.psd1) als de module die een heeft.</span><span class="sxs-lookup"><span data-stu-id="59a27-126">It contains the Windows PowerShell module and any supporting files, including a manifest file (.psd1) if the module has one.</span></span>

<span data-ttu-id="59a27-127">Als de module een Azure Automation-verbindingstype moet bevatten, moet deze ook een bestand bevatten met de naam `<ModuleName>-Automation.json`, waarin de eigenschappen van het verbindingstype zijn opgegeven.</span><span class="sxs-lookup"><span data-stu-id="59a27-127">If the module should contain an Azure Automation connection type, it must also contain a file with the name `<ModuleName>-Automation.json` that specifies the connection type properties.</span></span> <span data-ttu-id="59a27-128">Dit is een JSON-bestand dat in de modulemap van uw gecomprimeerde ZIP-bestand is geplaatst. Het bevat de velden van een 'verbinding' die is vereist om verbinding te maken met het systeem of de service die door de module wordt aangegeven.</span><span class="sxs-lookup"><span data-stu-id="59a27-128">This is a json file placed within the module folder of your compressed .zip file, and contains the fields of a “connection” that is required to connect to the system or service the module represents.</span></span> <span data-ttu-id="59a27-129">Uiteindelijk wordt hiermee een verbindingstype gemaakt in Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="59a27-129">This will end up creating a connection type in Azure Automation.</span></span> <span data-ttu-id="59a27-130">Met dit veld kunt u de veldnamen en typen instellen en opgeven of de velden moeten worden versleuteld en/of optioneel moeten zijn, voor het verbindingstype van de module.</span><span class="sxs-lookup"><span data-stu-id="59a27-130">Using this file you can set the field names, types, and whether the fields should be encrypted and / or optional, for the connection type of the module.</span></span> <span data-ttu-id="59a27-131">Hier volgt een sjabloon in de JSON-bestandsindeling:</span><span class="sxs-lookup"><span data-stu-id="59a27-131">The following is a template in the json file format:</span></span>

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

<span data-ttu-id="59a27-132">Als u Service Management Automation hebt geïmplementeerd en integratiemodulepakketten hebt gemaakt voor uw Automation-runbooks, zou deze er bekend moeten uitzien.</span><span class="sxs-lookup"><span data-stu-id="59a27-132">If you have deployed Service Management Automation and created Integration Modules packages for your automation runbooks, this should look very familiar to you.</span></span> 

## <a name="authoring-best-practices"></a><span data-ttu-id="59a27-133">Aanbevolen procedures voor ontwerpen</span><span class="sxs-lookup"><span data-stu-id="59a27-133">Authoring Best Practices</span></span>
<span data-ttu-id="59a27-134">Hoewel integratiemodules in wezen PowerShell-modules zijn, is er toch een aantal zaken waar u aan moet denken bij het ontwerpen van een PowerShell-module, om deze zo bruikbaar mogelijk te maken in Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="59a27-134">Even though Integration Modules are essentially PowerShell modules, there’s still a number of things we recommend you consider while authoring a PowerShell module, to make it most usable in Azure Automation.</span></span> <span data-ttu-id="59a27-135">Sommige hiervan zijn specifiek voor Azure Automation en sommige zijn nuttig om uw modules goed te laten werken in PowerShell Workflow, ongeacht of u Automation gebruikt.</span><span class="sxs-lookup"><span data-stu-id="59a27-135">Some of these are Azure Automation specific, and some of them are useful just to make your modules work well in PowerShell Workflow, regardless of whether or not you’re using Automation.</span></span> 

1. <span data-ttu-id="59a27-136">Neem een samenvatting, beschrijving en Help-URI op voor elke cmdlet in de module.</span><span class="sxs-lookup"><span data-stu-id="59a27-136">Include a synopsis, description, and help URI for every cmdlet in the module.</span></span> <span data-ttu-id="59a27-137">In PowerShell kunt u bepaalde Help-informatie voor cmdlets definiëren, zodat de gebruiker hulp ontvangt bij het gebruik van cmdlets met de cmdlet **Get-Help**.</span><span class="sxs-lookup"><span data-stu-id="59a27-137">In PowerShell, you can define certain help information for cmdlets to allow the user to receive help on using them with the **Get-Help** cmdlet.</span></span> <span data-ttu-id="59a27-138">U kunt bijvoorbeeld als volgt een samenvatting en Help-URI definiëren voor een PowerShell-module, geschreven in een PSM1-bestand.</span><span class="sxs-lookup"><span data-stu-id="59a27-138">For example, here’s how you can define a synopsis and help URI for a PowerShell module written in a .psm1 file.</span></span><br>  
   
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
   <br> <span data-ttu-id="59a27-139">Als u deze informatie opgeeft, wordt deze Help-informatie niet alleen getoond met de cmdlet **Get-Help** in de PowerShell-console, maar wordt deze Help-functionaliteit ook weergegeven in Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="59a27-139">Providing this info will not only show this help using the **Get-Help** cmdlet in the PowerShell console, it will also expose this help functionality within Azure Automation.</span></span>  <span data-ttu-id="59a27-140">Bijvoorbeeld wanneer u activiteiten invoegt tijdens het ontwerpen van een runbook.</span><span class="sxs-lookup"><span data-stu-id="59a27-140">For example, when inserting activities during runbook authoring.</span></span> <span data-ttu-id="59a27-141">Als u op Gedetailleerde Help-informatie weergeven klikt, wordt de Help-URI op een ander tabblad van de webbrowser geopend die u gebruikt voor toegang tot Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="59a27-141">Clicking “View detailed help” will open the help URI in another tab of the web browser you’re using to access Azure Automation.</span></span><br><span data-ttu-id="59a27-142">![Help bij integratiemodules](media/automation-integration-modules/automation-integration-module-activitydesc.png)</span><span class="sxs-lookup"><span data-stu-id="59a27-142">![Integration Module Help](media/automation-integration-modules/automation-integration-module-activitydesc.png)</span></span>
2. <span data-ttu-id="59a27-143">Als de module op een extern systeem wordt uitgevoerd, geldt het volgende:</span><span class="sxs-lookup"><span data-stu-id="59a27-143">If the module runs against a remote system,</span></span>

    <span data-ttu-id="59a27-144">a.</span><span class="sxs-lookup"><span data-stu-id="59a27-144">a.</span></span> <span data-ttu-id="59a27-145">Deze moet een metagegevensbestand voor de integratiemodule bevatten waarin de informatie wordt gedefinieerd die nodig is om verbinding te maken met dat externe systeem, dus het verbindingstype.</span><span class="sxs-lookup"><span data-stu-id="59a27-145">It should contain an Integration Module metadata file that defines the information needed to connect to that remote system, meaning the connection type.</span></span>  
    <span data-ttu-id="59a27-146">b.</span><span class="sxs-lookup"><span data-stu-id="59a27-146">b.</span></span> <span data-ttu-id="59a27-147">Elke cmdlet in de module moet een verbindingsobject (een exemplaar van dat verbindingstype) kunnen bevatten als een parameter.</span><span class="sxs-lookup"><span data-stu-id="59a27-147">Each cmdlet in the module should be able to take in a connection object (an instance of that connection type) as a parameter.</span></span>  

    <span data-ttu-id="59a27-148">Cmdlets in de module worden eenvoudiger te gebruiken in Azure Automation als u toestaat dat een object met de velden van het verbindingstype als een parameter aan de cmdlet wordt doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="59a27-148">Cmdlets in the module become easier to use in Azure Automation if you allow passing an object with the fields of the connection type as a parameter to the cmdlet.</span></span> <span data-ttu-id="59a27-149">Op deze manier hoeven gebruikers parameters van de verbindingsasset niet toe te wijzen aan de overeenkomende parameters van de cmdlet, elke keer dat ze een cmdlet aanroepen.</span><span class="sxs-lookup"><span data-stu-id="59a27-149">This way users don’t have to map parameters of the connection asset to the cmdlet's corresponding parameters each time they call a cmdlet.</span></span> <span data-ttu-id="59a27-150">Op basis van het bovenstaande runbookvoorbeeld wordt een Twilio-verbindingsasset genaamd CorpTwilio gebruikt voor toegang tot Twilio en voor het retourneren van alle telefoonnummers in het account.</span><span class="sxs-lookup"><span data-stu-id="59a27-150">Based on the runbook example above, it uses a Twilio connection asset called CorpTwilio to access Twilio and return all the phone numbers in the account.</span></span>  <span data-ttu-id="59a27-151">Ziet u hoe hiermee de velden van de verbinding worden toegewezen aan de parameters van de cmdlet?</span><span class="sxs-lookup"><span data-stu-id="59a27-151">Notice how it is mapping the fields of the connection to the parameters of the cmdlet?</span></span><br>
   
    ```
    workflow Get-CorpTwilioPhones
    {
      $CorpTwilio = Get-AutomationConnection -Name 'CorpTwilio'
   
      Get-TwilioPhoneNumbers 
        -AccountSid $CorpTwilio.AccountSid  
        -AuthToken $CorptTwilio.AuthToken
    }
    ```
  
    <span data-ttu-id="59a27-152">Een eenvoudigere en betere manier om dit te doen is het rechtstreeks doorgeven van het verbindingsobject aan de cmdlet -</span><span class="sxs-lookup"><span data-stu-id="59a27-152">An easier and better way to approach this is directly passing the connection object to the cmdlet -</span></span>
   
    ```
    workflow Get-CorpTwilioPhones
    {
      $CorpTwilio = Get-AutomationConnection -Name 'CorpTwilio'
   
      Get-TwilioPhoneNumbers -Connection $CorpTwilio
    }
    ```
   
    <span data-ttu-id="59a27-153">U kunt dergelijk gedrag mogelijk maken voor uw cmdlets door deze toe te staan een verbindingsobject rechtstreeks als parameter te accepteren, in plaats van alleen verbindingsvelden voor parameters.</span><span class="sxs-lookup"><span data-stu-id="59a27-153">You can enable behavior like this for your cmdlets by allowing them to accept a connection object directly as a parameter, instead of just connection fields for parameters.</span></span> <span data-ttu-id="59a27-154">Doorgaans wilt u voor elk een parameterset, zodat een gebruiker die Azure Automation niet gebruikt, uw cmdlets kan aanroepen zonder een hash-tabel te bouwen die als het verbindingsobject moet fungeren.</span><span class="sxs-lookup"><span data-stu-id="59a27-154">Usually you’ll want a parameter set for each, so that a user not using Azure Automation can call your cmdlets without constructing a hashtable to act as the connection object.</span></span> <span data-ttu-id="59a27-155">Parameterset **SpecifyConnectionFields** hieronder wordt gebruikt om de eigenschappen van het verbindingsveld één voor één door te geven.</span><span class="sxs-lookup"><span data-stu-id="59a27-155">Parameter set **SpecifyConnectionFields** below is used to pass the connection field properties one by one.</span></span> <span data-ttu-id="59a27-156">Met **UseConnectionObject** kunt u de verbinding rechtstreeks doorgeven.</span><span class="sxs-lookup"><span data-stu-id="59a27-156">**UseConnectionObject** lets you pass the connection straight through.</span></span> <span data-ttu-id="59a27-157">Zoals u kunt zien is voor de cmdlet Send-TwilioSMS in de [Twilio PowerShell-module](https://gallery.technet.microsoft.com/scriptcenter/Twilio-PowerShell-Module-8a8bfef8) de doorgave op beide manieren mogelijk:</span><span class="sxs-lookup"><span data-stu-id="59a27-157">As you can see, the Send-TwilioSMS cmdlet in the [Twilio PowerShell module](https://gallery.technet.microsoft.com/scriptcenter/Twilio-PowerShell-Module-8a8bfef8) allows passing either way:</span></span> 
   
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
3. <span data-ttu-id="59a27-158">Definieer het uitvoertype voor alle cmdlets in de module.</span><span class="sxs-lookup"><span data-stu-id="59a27-158">Define output type for all cmdlets in the module.</span></span> <span data-ttu-id="59a27-159">Als u een uitvoertype voor een cmdlet definieert, kan IntelliSense u tijdens het ontwerpen helpen bij het bepalen van de uitvoereigenschappen van de cmdlet, voor gebruik tijdens het ontwerpen.</span><span class="sxs-lookup"><span data-stu-id="59a27-159">Defining an output type for a cmdlet allows design-time IntelliSense to help you determine the output properties of the cmdlet, for use during authoring.</span></span> <span data-ttu-id="59a27-160">Het is vooral nuttig tijdens het grafisch ontwerpen van een Automation-runbook, waarbij ontwerptijdkennis essentieel is voor een goede gebruikerservaring met uw module.</span><span class="sxs-lookup"><span data-stu-id="59a27-160">It is especially helpful during Automation runbook graphical authoring, where design time knowledge is key to an easy user experience with your module.</span></span><br><br> <span data-ttu-id="59a27-161">![Uitvoertype grafisch runbook](media/automation-integration-modules/runbook-graphical-module-output-type.png)</span><span class="sxs-lookup"><span data-stu-id="59a27-161">![Graphical Runbook Output Type](media/automation-integration-modules/runbook-graphical-module-output-type.png)</span></span><br> <span data-ttu-id="59a27-162">Dit is vergelijkbaar met de functionaliteit 'automatisch aanvullen' van de uitvoer van een cmdlet in PowerShell ISE zonder deze te hoeven uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="59a27-162">This is similar to the "type ahead" functionality of a cmdlet's output in PowerShell ISE without having to run it.</span></span><br><br> <span data-ttu-id="59a27-163">![POSH IntelliSense](media/automation-integration-modules/automation-posh-ise-intellisense.png)</span><span class="sxs-lookup"><span data-stu-id="59a27-163">![POSH IntelliSense](media/automation-integration-modules/automation-posh-ise-intellisense.png)</span></span><br>
4. <span data-ttu-id="59a27-164">Cmdlets in de module mogen geen complexe objecttypen voor parameters hebben.</span><span class="sxs-lookup"><span data-stu-id="59a27-164">Cmdlets in the module should not take complex object types for parameters.</span></span> <span data-ttu-id="59a27-165">PowerShell Workflow verschilt van PowerShell in het volgende opzicht: complexe typen worden in gedeserialiseerde vorm opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="59a27-165">PowerShell Workflow is different from PowerShell in that it stores complex types in deserialized form.</span></span> <span data-ttu-id="59a27-166">Primitieve typen blijven primitieven, maar complexe typen worden geconverteerd naar hun gedeserialiseerde versies, die in wezen eigenschappenverzamelingen zijn.</span><span class="sxs-lookup"><span data-stu-id="59a27-166">Primitive types will stay as primitives, but complex types are converted to their deserialized versions, which are essentially property bags.</span></span> <span data-ttu-id="59a27-167">Als u bijvoorbeeld de cmdlet **Get-Process** hebt gebruikt in een runbook (of een PowerShell Workflow), wordt een object van het type [Deserialized.System.Diagnostic.Process] geretourneerd, niet van het verwachte type [System.Diagnostic.Process].</span><span class="sxs-lookup"><span data-stu-id="59a27-167">For example, if you used the **Get-Process** cmdlet in a runbook (or a PowerShell Workflow for that matter), it would return an object of type [Deserialized.System.Diagnostic.Process], not the expected [System.Diagnostic.Process] type.</span></span> <span data-ttu-id="59a27-168">Dit type heeft dezelfde eigenschappen als het niet-gedeserialiseerde type, maar geen van de methoden van dat type.</span><span class="sxs-lookup"><span data-stu-id="59a27-168">This type has all the same properties as the non-deserialized type, but none of the methods.</span></span> <span data-ttu-id="59a27-169">En als u deze waarde als een parameter probeert door te geven aan een cmdlet, waarbij door de cmdlet een waarde [System.Diagnostic.Process] voor deze parameter wordt verwacht, wordt de volgende foutmelding weergegeven: *Argumenttransformatie kan niet worden verwerkt voor parameter 'process'. Fout: "De waarde "System.Diagnostics.Process (CcmExec)" van type "Deserialized.System.Diagnostics.Process" kan niet worden geconverteerd naar type "System.Diagnostics.Process".*</span><span class="sxs-lookup"><span data-stu-id="59a27-169">And if you try to pass this value as a parameter to a cmdlet, where the cmdlet expects a [System.Diagnostic.Process] value for this parameter, you’ll receive the following error: *Cannot process argument transformation on parameter 'process'. Error: "Cannot convert the "System.Diagnostics.Process (CcmExec)" value of type  "Deserialized.System.Diagnostics.Process" to type "System.Diagnostics.Process".*</span></span>   <span data-ttu-id="59a27-170">Dit komt omdat de typen niet overeenkomen van het verwachte type [System.Diagnostic.Process] en het opgegeven type [Deserialized.System.Diagnostic.Process].</span><span class="sxs-lookup"><span data-stu-id="59a27-170">This is because there is a type mismatch between the expected [System.Diagnostic.Process] type and the given [Deserialized.System.Diagnostic.Process] type.</span></span> <span data-ttu-id="59a27-171">De manier om dit probleem op te lossen is ervoor te zorgen dat de cmdlets van uw module geen complexe typen voor parameters hebben.</span><span class="sxs-lookup"><span data-stu-id="59a27-171">The way around this issue is to ensure the cmdlets of your module do not take complex types for parameters.</span></span> <span data-ttu-id="59a27-172">Dit is de verkeerde manier.</span><span class="sxs-lookup"><span data-stu-id="59a27-172">Here is the wrong way to do it.</span></span>
   
    ```
    function Get-ProcessDescription {
      param (
            [System.Diagnostic.Process] $process
      )
      $process.Description
    }
    ``` 
    <br>
    <span data-ttu-id="59a27-173">En dit is de juiste manier, een primitieve nemen die intern kan worden gebruikt door de cmdlet om het complexe object op te halen en te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="59a27-173">And here is the right way, taking in a primitive that can be used internally by the cmdlet to grab the complex object and use it.</span></span> <span data-ttu-id="59a27-174">Aangezien de cmdlets worden uitgevoerd in de context van PowerShell, en niet PowerShell Workflow, wordt het correcte type in de cmdlet $process [System.Diagnostic.Process].</span><span class="sxs-lookup"><span data-stu-id="59a27-174">Since cmdlets execute in the context of PowerShell, not PowerShell Workflow, inside the cmdlet $process becomes the correct [System.Diagnostic.Process] type.</span></span>  
   
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
   <span data-ttu-id="59a27-175">Verbindingsassets in runbooks zijn hashtabellen, die een complex type zijn, en toch lijken deze hashtabellen te kunnen worden doorgegeven in cmdlets voor hun -Connection-parameter, zonder gecaste uitzondering.</span><span class="sxs-lookup"><span data-stu-id="59a27-175">Connection assets in runbooks are hashtables, which are a complex type, and yet these hashtables seem to be able to be passed into cmdlets for their –Connection parameter perfectly, with no cast exception.</span></span> <span data-ttu-id="59a27-176">In technisch opzicht kunnen sommige PowerShell-typen goed worden gecast van hun geserialiseerde vorm naar hun gedeserialiseerde vorm en kunnen deze daarom worden doorgegeven in cmdlets voor parameters die het niet-gedeserialiseerde type accepteren.</span><span class="sxs-lookup"><span data-stu-id="59a27-176">Technically, some PowerShell types are able to cast properly from their serialized form to their deserialized form, and hence can be passed into cmdlets for parameters accepting the non-deserialized type.</span></span> <span data-ttu-id="59a27-177">Hashtabel is daar een van.</span><span class="sxs-lookup"><span data-stu-id="59a27-177">Hashtable is one of these.</span></span> <span data-ttu-id="59a27-178">Het is mogelijk om gedefinieerde typen van een module-auteur te implementeren op een manier die deze ook correct kan deserialiseren, maar er zijn dan enkele compromissen nodig.</span><span class="sxs-lookup"><span data-stu-id="59a27-178">It’s possible for a module author’s defined types to be implemented in a way that they can correctly deserialize as well, but there are some trade-offs to consider.</span></span> <span data-ttu-id="59a27-179">Het type moet een standaardconstructor hebben, alle eigenschappen van het type moeten openbaar zijn en het type moet een PSTypeConverter hebben.</span><span class="sxs-lookup"><span data-stu-id="59a27-179">The type needs to have a default constructor, have all of its properties public, and have a PSTypeConverter.</span></span> <span data-ttu-id="59a27-180">Voor al gedefinieerde typen waarvan de module-auteur geen eigenaar is, is er echter geen manier om ze 'op te lossen', vandaar de aanbeveling om complexe typen voor parameters helemaal te vermijden.</span><span class="sxs-lookup"><span data-stu-id="59a27-180">However, for already-defined types that the module author does not own, there is no way to “fix” them, hence the recommendation to avoid complex types for parameters all together.</span></span> <span data-ttu-id="59a27-181">Tip voor het ontwerpen van een runbook: als om de een of andere reden een parameter van een complex type nodig is voor uw cmdlets, of u gebruikt de module van iemand anders waarvoor een parameter van een complex type is vereist, is de tijdelijke oplossing in PowerShell Workflow-runbooks en PowerShell Workflows in lokale PowerShell het verpakken van de cmdlet waarmee het complexe type wordt gegenereerd en de cmdlet waarmee het complexe type wordt gebruikt in dezelfde InlineScript-activiteit.</span><span class="sxs-lookup"><span data-stu-id="59a27-181">Runbook Authoring tip: If for some reason your cmdlets need to take a complex type parameter, or you are using someone else’s module that requires a complex type parameter, the workaround in PowerShell Workflow runbooks and PowerShell Workflows in local PowerShell, is to wrap the cmdlet that generates the complex type and the cmdlet that consumes the complex type in the same InlineScript activity.</span></span> <span data-ttu-id="59a27-182">Omdat met InlineScript de inhoud wordt uitgevoerd als PowerShell in plaats van PowerShell Workflow, zou met de cmdlet waarmee het complexe type wordt gegenereerd, dat correcte type worden gemaakt, niet het gedeserialiseerde complexe type.</span><span class="sxs-lookup"><span data-stu-id="59a27-182">Since InlineScript executes its contents as PowerShell rather than PowerShell Workflow, the cmdlet generating the complex type would produce that correct type, not the deserialized complex type.</span></span>
5. <span data-ttu-id="59a27-183">Maak alle cmdlets in de module staatloos.</span><span class="sxs-lookup"><span data-stu-id="59a27-183">Make all cmdlets in the module stateless.</span></span> <span data-ttu-id="59a27-184">In PowerShell Workflow wordt elke cmdlet die in de werkstroom wordt aangeroepen in een andere sessie uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="59a27-184">PowerShell Workflow runs every cmdlet called in the workflow in a different session.</span></span> <span data-ttu-id="59a27-185">Dit betekent dat cmdlets die afhankelijk zijn van de sessiestatus gemaakt/gewijzigd door andere cmdlets in dezelfde module niet zullen werken in PowerShell Workflow-runbooks.</span><span class="sxs-lookup"><span data-stu-id="59a27-185">This means any cmdlets that depend on session state created / modified by other cmdlets in the same module will not work in PowerShell Workflow runbooks.</span></span>  <span data-ttu-id="59a27-186">Hier ziet u een voorbeeld van wat u niet moet doen.</span><span class="sxs-lookup"><span data-stu-id="59a27-186">Here is an example of what not to do.</span></span>
   
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
6. <span data-ttu-id="59a27-187">De module moet volledig zijn opgenomen in een pakket waarvoor Xcopy kan worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="59a27-187">The module should be fully contained in an Xcopy-able package.</span></span> <span data-ttu-id="59a27-188">Omdat Azure Automation-modules worden gedistribueerd naar de Automation-sandboxes wanneer runbooks moeten worden uitgevoerd, moeten ze onafhankelijk van de host werken waarop ze worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="59a27-188">Because Azure Automation modules are distributed to the Automation sandboxes when runbooks need to execute, they need to work independently of the host they are running on.</span></span> <span data-ttu-id="59a27-189">Dit betekent dat u het modulepakket moet kunnen zippen, het verplaatsen naar een andere host met dezelfde of een nieuwere PowerShell-versie en dit normaal moet kunnen laten functioneren wanneer het in de PowerShell-omgeving van die host is geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="59a27-189">What this means is that you should be able to Zip up the module package, move it to any other host with the same or newer PowerShell version, and have it function as normal when imported into that host’s PowerShell environment.</span></span> <span data-ttu-id="59a27-190">Hiervoor mag de module niet afhankelijk zijn van bestanden buiten de modulemap (de map die wordt gezipt wanneer u in Azure Automation importeert), of van unieke registerinstellingen voor een host, zoals die die zijn ingesteld bij de installatie van een product.</span><span class="sxs-lookup"><span data-stu-id="59a27-190">In order for that to happen, the module should not depend on any files outside the module folder (the folder that gets zipped up when importing into Azure Automation), or on any unique registry settings on a host, such as those set by the install of a product.</span></span> <span data-ttu-id="59a27-191">Als deze aanbevolen procedure niet wordt gevolgd, is de module niet bruikbaar in Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="59a27-191">If this best practice is not followed, the module will not be usable in Azure Automation.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="59a27-192">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="59a27-192">Next steps</span></span>

* <span data-ttu-id="59a27-193">Zie [Mijn eerste PowerShell Workflow-runbook](automation-first-runbook-textual.md) om aan de slag te gaan met PowerShell Workflow-runbooks</span><span class="sxs-lookup"><span data-stu-id="59a27-193">To get started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span>
* <span data-ttu-id="59a27-194">Zie [Een Windows PowerShell-module schrijven](https://msdn.microsoft.com/library/dd878310%28v=vs.85%29.aspx) voor meer informatie over het maken van PowerShell-modules.</span><span class="sxs-lookup"><span data-stu-id="59a27-194">To learn more about creating PowerShell Modules, see [Writing a Windows PowerShell Module](https://msdn.microsoft.com/library/dd878310%28v=vs.85%29.aspx)</span></span>

