---
title: problemen met algemene Azure Automation aaaTroubleshooting | Microsoft Docs
description: Dit artikel bevat informatie toohelp en oplossen van veelvoorkomende fouten van Azure Automation.
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
tags: top-support-issue
keywords: Fout bij het Automation, het oplossen van problemen probleem
ms.assetid: 5f3cfe61-70b0-4e9c-b892-d02daaeee07d
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/26/2017
ms.author: sngun; v-reagie
ms.openlocfilehash: eb7d1cc5726f2b7a86c860e8f0c8340fa4221b2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-common-issues-in-azure-automation"></a>Het oplossen van veelvoorkomende problemen in Azure Automation 
Dit artikel vindt u hulp het oplossen van veelvoorkomende fouten u tegenkomen in Azure Automation en mogelijke oplossingen tooresolve stelt ze.

## <a name="authentication-errors-when-working-with-azure-automation-runbooks"></a>Verificatiefouten bij het werken met Azure Automation-runbooks
### <a name="scenario-sign-in-tooazure-account-failed"></a>Scenario: Meld u aan tooAzure-Account is mislukt
**Fout:** foutbericht Hallo "Unknown_user_type: onbekende gebruikerstype" bij het werken met de cmdlets Add-AzureAccount of Login-AzureRmAccount Hallo.

**Reden voor fout Hallo:** deze fout treedt op als de referentienaam asset Hallo niet geldig is of als hello geen gebruikersnaam en wachtwoord waarmee u toosetup Hallo Automation-referentieasset geldig zijn.

**Tips voor probleemoplossing:** In order toodetermine wat er mis is, ondernemen Hallo stappen te volgen:  

1. Zorg ervoor dat er geen speciale tekens, inclusief Hallo  **@**  teken in Hallo Automation asset referentienaam dat u van tooconnect tooAzure gebruikmaakt.  
2. Controleer dat u Hallo gebruikersnaam en wachtwoord die zijn opgeslagen in Azure Automation-referentie Hallo in uw lokale PowerShell ISE-editor kunt gebruiken. U kunt dit doen door het uitvoeren van Hallo-cmdlets in Hallo PowerShell ISE te volgen:  

        $Cred = Get-Credential  
        #Using Azure Service Management   
        Add-AzureAccount –Credential $Cred  
        #Using Azure Resource Manager  
        Login-AzureRmAccount –Credential $Cred
3. Als uw verificatie is mislukt lokaal, dit betekent dat u uw Azure Active Directory-referenties correct hebt ingesteld. Raadpleeg te[verifiëren met Azure Active Directory tooAzure](https://azure.microsoft.com/blog/azure-automation-authenticating-to-azure-using-azure-active-directory/) blog post tooget hello Azure Active Directory-account juist ingesteld.  

### <a name="scenario-unable-toofind-hello-azure-subscription"></a>Scenario: Kan geen toofind hello Azure-abonnement
**Fout:** foutbericht Hallo ' Hallo abonnement met de naam ``<subscription name>`` is niet gevonden ' als u werkt met Hallo Select-AzureSubscription of Select-AzureRmSubscription-cmdlets.

**Reden voor fout Hallo:** deze fout treedt op als de naam van de Hallo-abonnement niet geldig is of als hello Azure Active Directory-gebruiker die tooget Hallo-abonnementsgegevens probeert is niet geconfigureerd als een beheerder van Hallo-abonnement.

**Tips voor probleemoplossing:** In volgorde toodetermine als u hebt geverifieerd tooAzure en hebt toegang toohello abonnement waarvoor u tooselect, nemen Hallo stappen te volgen:  

1. Zorg ervoor dat u Hallo uitvoert **Add-AzureAccount** voordat u Hallo **Select-AzureSubscription** cmdlet.  
2. Als u nog steeds deze foutmelding ziet, wijzigt u uw code door toe te voegen Hallo **Get-AzureSubscription** cmdlet na Hallo **Add-AzureAccount** cmdlet vervolgens Hallo code wordt uitgevoerd.  Nu controleren als Hallo-uitvoer van Get-AzureSubscription de details van uw abonnement bevat.  

   * Als u niet alle abonnementsgegevens in Hallo uitvoer ziet, betekent dit dat Hallo abonnement nog niet is geïnitialiseerd.  
   * Als Hallo-abonnementsgegevens in Hallo uitvoer wordt weergegeven, moet u ervoor zorgen dat u ID of naam van het juiste abonnement Hallo Hello **Select-AzureSubscription** cmdlet.   

### <a name="scenario-authentication-tooazure-failed-because-multi-factor-authentication-is-enabled"></a>Scenario: TooAzure verificatie is mislukt omdat de multi-factor authentication is ingeschakeld
**Fout:** foutbericht Hallo ' Add-AzureAccount: AADSTS50079: sterke verificatie inschrijving (bewijs-up) is vereist ' bij het verifiëren van tooAzure met uw Azure-gebruikersnaam en wachtwoord.

**Reden voor fout Hallo:** als u multi-factor authentication-server op uw Azure-account hebt, kunt u een Azure Active Directory gebruiker tooauthenticate tooAzure niet gebruiken.  In plaats daarvan moet u toouse een certificaat of een service-principal tooauthenticate tooAzure.

**Tips voor probleemoplossing:** toouse een certificaat met hello Azure Service Management-cmdlets, Raadpleeg te[maken en het toevoegen van een certificaat toomanage Azure services.](http://blogs.technet.com/b/orchestrator/archive/2014/04/11/managing-azure-services-with-the-microsoft-azure-automation-preview-service.aspx) een service-principal met Azure Resource Manager-cmdlets toouse te verwijzen[service principal met Azure portal maken](../azure-resource-manager/resource-group-create-service-principal-portal.md) en [verifiëren van een service-principal met Azure Resource Manager.](../azure-resource-manager/resource-group-authenticate-service-principal.md)

## <a name="common-errors-when-working-with-runbooks"></a>Veelvoorkomende fouten bij het werken met runbooks
### <a name="scenario-hello-runbook-job-start-was-attempted-three-times-but-it-failed-toostart-each-time"></a>Scenario: begin van de taak Hallo runbook is drie keer geprobeerd, maar het toostart niet elke keer
**Fout:** uw runbook is mislukt met fout Hallo "' Hallo-taak is drie keer geprobeerd maar deze is mislukt."

**Reden voor fout Hallo:** deze fout kan zijn veroorzaakt door Hallo volgende redenen:  

1. Limiet voor geheugen.  We hebben limieten op hoeveel geheugen tooa Sandbox toegewezen gedocumenteerd [Servicelimieten Automation](../azure-subscription-service-limits.md#automation-limits) zodat een taak deze mislukken kan als er meer dan 400 MB geheugen gebruikt. 

2. Incompatibele module.  Dit kan gebeuren als de module-afhankelijkheden zijn niet juist en als dat niet het geval is, uw runbook doorgaans retourneert een '-opdracht niet gevonden' of 'Kan niet binden voor parameter'-bericht. 

**Tips voor probleemoplossing:** een van de volgende oplossingen Hallo Hallo-probleem opgelost:  

* Voorgestelde methoden toowork binnen de geheugenlimiet Hallo zijn toosplit Hallo werkbelasting tussen meerdere runbooks, zo veel mogelijk gegevens in het geheugen niet toowrite onnodige de uitvoer van uw runbooks niet verwerken of houd rekening met het aantal controlepunten die u in uw PowerShell schrijven workflow-runbooks.  

* U moet tooupdate uw Azure-modules door Hallo stappen te volgen [hoe tooupdate Azure PowerShell-modules in Azure Automation](automation-update-azure-modules.md).  


### <a name="scenario-runbook-fails-because-of-deserialized-object"></a>Scenario: Runbook is mislukt vanwege deserialiseerbaar object
**Fout:** uw runbook is mislukt met fout Hallo ' parameter kan niet binden ``<ParameterName>``. Kan niet worden geconverteerd Hallo ``<ParameterType>`` waarde van het type Deserialized ``<ParameterType>`` tootype ``<ParameterType>``'.

**Reden voor fout Hallo:** als uw runbook een PowerShell Workflow is, wordt opgeslagen naar complexe objecten in een gedeserialiseerde notatie in volgorde toopersist uw runbook-status als Hallo workflow wordt onderbroken.  

**Tips voor probleemoplossing:**  
Een van de volgende drie oplossingen Hallo wordt dit probleem oplossen:

1. Als u complexe objecten van een cmdlet tooanother zijn sluizen, moet u deze cmdlets verpakken in een InlineScript.  
2. Hallo-naam of waarde die u nodig hebt doorgegeven van complexe object Hallo in plaats van het gehele object hello wordt doorgegeven.  
3. Een PowerShell-runbook gebruiken in plaats van een PowerShell Workflow-runbook.  

### <a name="scenario-runbook-job-failed-because-hello-allocated-quota-exceeded"></a>Scenario: De Runbook-taak is mislukt omdat Hallo quotum is overschreden toegewezen
**Fout:** de runbooktaak is mislukt met fout Hallo 'hello quotum voor Hallo maandelijkse totale taakuitvoeringstijd is bereikt voor dit abonnement'.

**Reden voor fout Hallo:** deze fout treedt op wanneer hello taakuitvoering overschrijdt Hallo 500 minuut beschikbare quotum voor uw account. Dit quotum geldt tooall soorten taken uitvoeren zoals het testen van een taak, start een taak vanuit de portal hello, een taak wordt uitgevoerd met behulp van webhooks en plannen van een taak tooexecute via beide hello Azure-portal of in uw datacenter. Zie informatie over prijzen voor automatisering toolearn [Automation prijzen](https://azure.microsoft.com/pricing/details/automation/).

**Tips voor probleemoplossing:** als u wilt dat toouse meer dan 500 minuten per maand u toochange moet verwerken van uw abonnement op Hallo gratis laag toohello basisstaffel. U kunt toohello basisstaffel upgraden door duurt Hallo stappen te volgen:  

1. Meld u aan tooyour Azure-abonnement  
2. Hallo gewenst tooupgrade Automation-account selecteren  
3. Klik op **instellingen** > **prijscategorie en gebruik** > **prijscategorie**  
4. Op Hallo **Kies uw prijscategorie** blade Selecteer **Basic**    

### <a name="scenario-cmdlet-not-recognized-when-executing-a-runbook"></a>Scenario: Cmdlet is niet herkend bij het uitvoeren van een runbook
**Fout:** de runbooktaak is mislukt met fout Hallo '``<cmdlet name>``: Hallo term ``<cmdlet name>`` niet wordt herkend als Hallo-naam van een cmdlet, functie, scriptbestand of programma. "

**Reden voor fout Hallo:** deze fout wordt veroorzaakt wanneer PowerShell-engine Hallo Hallo cmdlet die u in uw runbook gebruikt niet kan vinden.  Dit kan zijn omdat Hallo-module met de cmdlet Hallo in het Hallo-account ontbreekt, er een naamconflict met de runbooknaam van een is, of Hallo cmdlet ook in een andere module bestaat en automatisering Hallo-naam kan niet worden omgezet.

**Tips voor probleemoplossing:** een van de volgende oplossingen Hallo Hallo-probleem opgelost:  

* Controleer u de naam van de cmdlet Hallo correct hebt ingevoerd.  
* Zorg ervoor dat cmdlet Hallo bestaat in uw Automation-account en er zijn geen conflicten. tooverify als Hallo cmdlet aanwezig is, opent u een runbook in de bewerkingsmodus en zoek naar Hallo cmdlet of wilt u toofind in Hallo-bibliotheek uitvoeren **Get-Command ``<CommandName>``** .  Zodra u deze cmdlet Hallo hebt gevalideerd beschikbaar toohello account is, en dat er geen naam conflicteert met andere cmdlets of runbooks, toe te voegen toohello canvas en zorg ervoor dat u gebruikmaakt van een geldige parameters ingesteld in uw runbook.  
* Als er een naamconflict en Hallo cmdlet beschikbaar in twee verschillende modules is, kunt u deze kunt oplossen met behulp van de volledig gekwalificeerde naam Hallo voor Hallo-cmdlet. U kunt bijvoorbeeld **ModuleName\CmdletName**.  
* Als u Hallo runbook lokaal worden uitgevoerd in een hybrid worker-groep, moet u ervoor zorgen dat Hallo is module-cmdlet op Hallo-machine die als host fungeert voor Hallo hybride worker geïnstalleerd.

### <a name="scenario-a-long-running-runbook-consistently-fails-with-hello-exception-hello-job-cannot-continue-running-because-it-was-repeatedly-evicted-from-hello-same-checkpoint"></a>Scenario: Een langdurige runbook consistent is mislukt met uitzondering van Hallo: ' hello taak kan niet worden voortgezet omdat deze meerdere keren verwijdering uit Hallo dezelfde controlepunt '.
**Reden voor fout Hallo:** dit is de ontwerp-gedrag vanwege toohello 'Evenredige verdeling' bewaking van de processen in Azure Automation, waarmee automatisch een runbook wordt geblokkeerd als deze meer dan drie uur wordt uitgevoerd. Echter, Hallo foutbericht geretourneerd biedt geen 'nu' opties. Een runbook kan worden onderbroken voor een aantal oorzaken hebben. Onderbreekt de geval voornamelijk vanwege tooerrors. Bijvoorbeeld, een niet-onderschepte uitzondering in een runbook, een netwerkstoring of vastlopen van een op Hallo Hallo runbook met Runbook-Worker, wordt alle Hallo runbook toobe onderbroken veroorzaken en starten vanaf de laatste controlepunt wanneer hervat.

**Tips voor probleemoplossing:** Hallo beschreven oplossing tooavoid dit probleem is toouse controlepunten in een werkstroom.  meer te verwijzen toolearn[Learning PowerShell-werkstromen](automation-powershell-workflow.md#checkpoints).  Een gedetailleerde informatie over het 'Evenredige verdeling' en de controlepunten vindt u in dit artikel blog [met behulp van controlepunten in Runbooks](https://azure.microsoft.com/en-us/blog/azure-automation-reliable-fault-tolerant-runbook-execution-using-checkpoints/).

## <a name="common-errors-when-importing-modules"></a>Veelvoorkomende fouten bij het importeren van modules
### <a name="scenario-module-fails-tooimport-or-cmdlets-cant-be-executed-after-importing"></a>Scenario: Module niet kan tooimport of cmdlets kan niet worden uitgevoerd na het importeren
**Fout:** een module tooimport mislukt of is geïmporteerd, maar geen cmdlets worden opgehaald.

**Reden voor fout Hallo:** enkele algemene oorzaken dat een module worden mogelijk niet met succes geïmporteerd tooAzure Automation zijn:  

* Hallo-structuur komt niet overeen met de Hallo structuur dat Automation moet het toobe in.  
* Hallo-module is afhankelijk van een andere module die niet geïmplementeerd tooyour Automation-account is.  
* Hallo-module ontbreekt de bijbehorende afhankelijkheden in de map Hallo.  
* Hallo **nieuw AzureRmAutomationModule** cmdlet wordt gebruikte tooupload Hallo module en kunt u niet de volledige opslagpad Hallo hebt gegeven of Hallo-module niet geladen via een openbaar toegankelijke URL.  

**Tips voor probleemoplossing:**  
Een van de volgende oplossingen Hallo Hallo-probleem opgelost:  

* Zorg ervoor dat die module Hallo volgt Hallo volgende indeling:  
  ModuleName.Zip  **->**  ModuleName of het versienummer  **->**  (ModuleName.psm1, ModuleName.psd1)
* Hallo .psd1 bestand openen en controleert u of Hallo-module afhankelijkheden heeft.  Als dit het geval is, uploadt u deze modules toohello Automation-account.  
* Zorg ervoor dat eventuele waarnaar wordt verwezen dll's aanwezig zijn in de modulemap Hallo.  

## <a name="common-errors-when-working-with-desired-state-configuration-dsc"></a>Veelvoorkomende fouten bij het werken met Desired State Configuration (DSC)
### <a name="scenario-node-is-in-failed-status-with-a-not-found-error"></a>Scenario: Het knooppunt bevindt zich in de status mislukt met een 'Niet gevonden'-fout
**Fout:** Hallo knooppunt heeft een rapport met **mislukt** status en met de fout Hallo ' Hallo poging tooget Hallo actie van de server https://``<url>``//accounts/``<account-id>``/Nodes(AgentId=``<agent-id>``) / GetDscAction is mislukt omdat een geldige configuratie ``<guid>`` kan niet worden gevonden. "

**Reden voor fout Hallo:** deze fout treedt meestal op wanneer hello knooppunt tooa configuratienaam (bijvoorbeeld ABC) is toegewezen in plaats van een knooppunt configuratienaam (bijvoorbeeld ABC. WebServer).  

**Tips voor probleemoplossing:**  

* Zorg ervoor dat u knooppunt met 'knooppunt configuratienaam' en niet Hallo 'configuratie op de naam' hello toewijst.  
* U kunt een knooppunt tooa knooppunt in het gebruik van Azure portal of met een PowerShell-cmdlet kunt toewijzen.

  * In volgorde tooassign knooppunt tooa met de configuratie van knooppunt met Azure portal, opent u Hallo **DSC-knooppunten** blade vervolgens selecteert u een knooppunt en klik op **toewijzen knooppuntconfiguratie** knop.  
  * In de volgorde tooassign knooppunt tooa met de configuratie van knooppunt met behulp van PowerShell-cmdlet, gebruikt u **Set AzureRmAutomationDscNode** cmdlet

### <a name="scenario--no-node-configurations-mof-files-were-produced-when-a-configuration-is-compiled"></a>Scenario: Er is geen knooppuntconfiguraties (MOF-bestanden) zijn gemaakt tijdens het compileren van een configuratie
**Fout:** DSC-Compilatietaak wordt onderbroken met de Hallo-fout: 'compilatie is voltooid, maar er is geen configuratie knooppunt .mofs zijn gegenereerd'.

**Reden voor fout Hallo:** wanneer Hallo expressie na Hallo **knooppunt** -sleutelwoord in Hallo DSC-configuratie te evalueert $null en geen knooppuntconfiguraties wordt geproduceerd.    

**Tips voor probleemoplossing:**  
Een van de volgende oplossingen Hallo Hallo-probleem opgelost:  

* Zorg ervoor dat Hallo expressie volgende toohello **knooppunt** -sleutelwoord in Hallo configuratiedefinitie is niet te evalueren $null.  
* Als u ConfigurationData doorgeeft bij het compileren van Hallo configuratie, zorgt u ervoor dat u Hallo verwachte waarden doorgeeft die Hallo-configuratie is vereist uit [ConfigurationData](automation-dsc-compile.md#configurationdata).

### <a name="scenario--hello-dsc-node-report-becomes-stuck-in-progress-state"></a>Scenario: Hallo DSC-knooppunt rapport wordt de status 'wordt uitgevoerd' vastgelopen
**Fout:** DSC Agent levert 'Er is geen exemplaar gevonden met de opgegeven eigenschapswaarden '.

**Reden voor fout Hallo:** u uw versie van WMF hebt bijgewerkt en WMI zijn beschadigd.  

**Tips voor probleemoplossing:** Hallo-instructies in Hallo [DSC bekende problemen en beperkingen](https://msdn.microsoft.com/powershell/wmf/5.0/limitation_dsc) toofix Hallo probleem.

### <a name="scenario--unable-toouse-a-credential-in-a-dsc-configuration"></a>Scenario: Kan geen toouse een referentie in een DSC-configuratie
**Fout:** DSC-Compilatietaak is onderbroken met de Hallo-fout: "System.InvalidOperationException fout bij het verwerken van de eigenschap '-referentie van het type ``<some resource name>``: omzetten en opslaan van een versleutelde wachtwoord als leesbare tekst is alleen toegestaan als PSDscAllowPlainTextPassword is tootrue ingesteld'.

**Reden voor fout Hallo:** u een referentie in een configuratie hebt gebruikt maar geen juiste **ConfigurationData** tooset **PSDscAllowPlainTextPassword** tootrue voor elk knooppunt de configuratie.  

**Tips voor probleemoplossing:**  

* Zorg ervoor toopass in de juiste Hallo **ConfigurationData** tooset **PSDscAllowPlainTextPassword** tootrue voor elke knooppuntconfiguratie vermeld in het Hallo-configuratie. Voor meer informatie raadpleegt u te[activa in Azure Automation DSC](automation-dsc-compile.md#assets).

## <a name="next-steps"></a>Volgende stappen
Als u bovenstaande stappen voor probleemoplossing Hallo hebt gevolgd en Hallo antwoord niet kunt vinden, kunt u opties voor aanvullende ondersteuning Hallo hieronder kunt bekijken.

* Help opvragen van Azure-experts. Verzenden van uw probleem toohello [MSDN Azure of Stack Overflow-forums.](https://azure.microsoft.com/support/forums/).
* Het bestand is een incident voor ondersteuning van Azure. Ga toohello [site ondersteuning van Azure](https://azure.microsoft.com/support/options/) en klik op **ondersteuning krijgen** onder **technische en ondersteuning voor facturering**.
* Post een bericht een aanvraag voor een Script op [Script Center](https://azure.microsoft.com/documentation/scripts/) als u een Azure Automation-runbookoplossing of een integratiemodule zoekt.
* Feedback geven of functieaanvragen voor Azure Automation post een bericht op [User Voice](https://feedback.azure.com/forums/34192--general-feedback).
