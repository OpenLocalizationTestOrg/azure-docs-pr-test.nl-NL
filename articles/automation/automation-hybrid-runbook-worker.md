---
title: aaaAzure Automation Hybrid Runbook Workers | Microsoft Docs
description: In dit artikel bevat informatie over het installeren en gebruiken van Hybrid Runbook Worker die is een functie van Azure Automation waarmee u toorun runbooks op computers in uw lokale datacentrum of de cloudprovider.
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 06227cda-f3d1-47fe-b3f8-436d2b9d81ee
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: magoedte;bwren
ms.openlocfilehash: ccee35e8324149a79ff692a867e5ce7801299bcb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="automate-resources-in-your-data-center-or-cloud-with-hybrid-runbook-worker"></a>Automatiseren van bronnen in uw datacenter of de cloud met Hybrid Runbook Worker
Runbooks in Azure Automation heeft geen toegang tot resources in andere clouds of in uw on-premises omgeving omdat ze worden uitgevoerd in hello Azure-cloud.  Hallo Hybrid Runbook Worker-functie van Azure Automation kunt u runbooks toorun rechtstreeks op Hallo-computer die als host fungeert voor de rol Hallo en op basis van bronnen in Hallo omgeving toomanage die lokale bronnen. Runbooks zijn opgeslagen en beheerd in Azure Automation en vervolgens geleverd tooone of meer opgegeven computers.  

Deze functionaliteit wordt geïllustreerd in Hallo installatiekopie te volgen:<br>  

![Overzicht van hybride Runbook Worker](media/automation-offering-get-started/automation-infradiagram-networkcomms.png)

Zie voor een technisch overzicht van Hallo Hybrid Runbook Worker-rol en implementatie overwegingen [Automation architectuuroverzicht](automation-offering-get-started.md#automation-architecture-overview).    

## <a name="hybrid-runbook-worker-groups"></a>Hybrid Runbook Worker-groepen
Elke Hybrid Runbook Worker is lid van een hybride Runbook Worker-groep die u opgeeft wanneer u Hallo-agent installeren.  Een groep kan één agent bevatten, maar u kunt meerdere agents installeren in een groep voor hoge beschikbaarheid.

Wanneer u een runbook op een hybride Runbook Worker start, geeft u Hallo-groep die op wordt uitgevoerd.  leden van de groep Hallo Hallo bepalen welke worker services Hallo-aanvraag.  U kunt een bepaalde worker niet opgeven.

## <a name="relationship-tooservice-management-automation"></a>Relatie tooService Management Automation
[Service Management Automation (SMA)](https://technet.microsoft.com/library/dn469260.aspx) kunt u toorun Hallo dezelfde runbooks die worden ondersteund door Azure Automation in uw lokale datacentrum. SMA wordt doorgaans samen met Windows Azure Pack geïmplementeerd als Windows Azure Pack, een grafische interface voor SMA management bevat. In tegenstelling tot Azure Automation is SMA vereist een lokale installatie met web servers toohost Hallo API, een database toocontain runbooks en SMA-configuratie en runbooktaken tooexecute Runbook Workers. Azure Automation biedt deze services in de cloud Hallo en alleen moet u toomaintain Hallo Hybrid Runbook Workers in uw lokale omgeving.

Als u een bestaande SMA-gebruiker bent, kunt u uw runbooks tooAzure Automation toobe gebruikt met Hybrid Runbook Worker zonder wijzigingen, ervan uitgaande dat ze hun eigen tooresources verificatie uitvoeren, zoals beschreven in [runbooks worden uitgevoerd op een hybride Runbook Werknemer](automation-hrw-run-runbooks.md).  Runbooks in SMA worden uitgevoerd in context Hallo van Hallo-serviceaccount op Hallo worker-server die u dat de verificatie voor Hallo runbooks bepalen kan.

U kunt Hallo criteria toodetermine te volgen of Azure Automation met Hybrid Runbook Worker- of Service Management Automation meer geschikt voor uw vereisten is.

* SMA vereist een lokale installatie van de onderliggende onderdelen die verbonden tooWindows Azure Pack zijn als een grafische beheerinterface vereist is. Meer lokale bronnen nodig zijn met hogere onderhoudskosten dan Azure Automation, die alleen een agent geïnstalleerd op de lokale runbook workers moet. Hallo-agents worden beheerd door Operations Management Suite en verdere verlagen de onderhoudskosten.
* Azure Automation slaat de runbooks in de cloud Hallo en zorgt ervoor dat deze tooon-premises hybride Runbook Workers. Als uw beveiligingsbeleid dit gedrag niet toelaat, moet u SMA gebruiken.
* SMA is opgenomen in System Center; en is daarom een System Center 2012 R2-licentie vereist. Azure Automation is gebaseerd op een abonnementsmodel gelaagde.
* Azure Automation heeft geavanceerde functies zoals grafische runbooks die niet beschikbaar in SMA.

## <a name="installing-hello-windows-hybrid-runbook-worker"></a>Hallo Windows Hybrid Runbook Worker installeren 

tooinstall en configureren van een hybride Runbook Worker van Windows, er zijn twee methoden beschikbaar.  Hallo aanbevolen methode is met behulp van een runbook toocompletely automatiseren Hallo vereist Automation tooconfigure een Windows-computer.  de tweede methode Hallo volgt de installatie van een stapsgewijze procedure toomanually en configureert Hallo-functie.  

> [!NOTE]
> toomanage hello configuratie van uw servers Hallo Hybrid Runbook Worker-rol met Desired State Configuration (DSC) ondersteunen, moet u tooadd als DSC-knooppunten.  Voor meer informatie over het voorbereiden voor beheer met DSC, Zie [machines voorbereiden voor beheer door Azure Automation DSC](automation-dsc-onboarding.md).           
><br>
>Als u Hallo inschakelt [Update beheeroplossing](../operations-management-suite/oms-solution-update-management.md), elke Windows-computer verbonden tooyour OMS-werkruimte wordt automatisch geconfigureerd als hybride Runbook Worker toosupport runbooks opgenomen in deze oplossing.  Het is echter niet geregistreerd bij de Hybrid Worker-groepen in uw Automation-account al gedefinieerd.  Hallo-computer kan worden toegevoegd tooa Hybrid Runbook Worker-groep in uw Automation-account toosupport Automation-runbooks, zolang u dezelfde voor zowel Hallo oplossing als hybride Runbook Worker-groepslidmaatschap account Hallo gebruikt.  Deze functionaliteit is tooversion 7.2.12024.0 Hallo Hybrid Runbook Worker toegevoegd.  

Bekijk Hallo volgende informatie met betrekking tot Hallo [hardware- en softwarevereisten](automation-offering-get-started.md#hybrid-runbook-worker) en [informatie voor het voorbereiden van uw netwerk](automation-offering-get-started.md#network-planning) voordat u begint met het implementeren van een hybride Runbook Worker.  Nadat u hebt een runbook worker is geïmplementeerd, controleren [runbooks worden uitgevoerd op een hybride Runbook Worker](automation-hrw-run-runbooks.md) toolearn hoe tooconfigure uw runbooks tooautomate verwerkt in uw on-premises datacentrum of andere cloudomgeving.  
 
### <a name="automated-deployment"></a>Geautomatiseerde implementatie

Uitvoeren van de volgende Hallo stappen tooautomate Hallo installatie en configuratie van Hallo Windows Hybrid Worker-rol.  

1. Hallo downloaden *nieuw OnPremiseHybridWorker.ps1* script vanaf Hallo [PowerShell Gallery](https://www.powershellgallery.com/packages/New-OnPremiseHybridWorker/1.0/DisplayScript) direct vanuit het Hallo-computers Hallo Hybrid Runbook Worker-rol of vanuit een andere computer in uw omgeving en kopieer het toohello worker.  

    Hallo *nieuw OnPremiseHybridWorker.ps1* script Hallo parameters tijdens het uitvoeren van volgende vereist:

  * *AutomationAccountName* (verplicht) - Hallo-naam van uw Automation-account.  
  * *ResourceGroupName* (verplicht) - Hallo-naam van resourcegroep Hallo die zijn gekoppeld aan uw Automation-account.  
  * *HybridGroupName* (verplicht) - Hallo-naam van een Hybrid Runbook Worker-groep die u opgeeft als doel voor Hallo runbooks die dit scenario te ondersteunen. 
  *  *SubscriptionID* (verplicht) - hello Azure-abonnements-Id die uw Automation-account in.
  *  *WorkspaceName* (optioneel) - Hallo OMS Werkruimtenaam.  Als u een OMS-werkruimte niet hebt, worden de Hallo script maakt en configureert u een.  

     > [!NOTE]
     > Hallo alleen Automation regio's ondersteund voor de integratie met OMS zijn momenteel - **Australië-Zuidoost**, **VS-Oost 2**, **Zuidoost-Azië**, en **West Europa**.  Als uw Automation-account zich niet in een van deze regio's, Hallo script maakt een OMS-werkruimte, maar er een waarschuwingsbericht weergegeven dat er kan geen koppeling ze samen.
     > 
2. Start op uw computer **Windows PowerShell** van Hallo **Start** scherm in de beheerdersmodus.  
3. Ga vanuit Hallo PowerShell opdrachtregel-shell, toohello map Hallo script u hebt gedownload en het wijzigen van waarden voor parameters Hallo uitvoeren *- AutomationAccountName*, *- ResourceGroupName* , *- HybridGroupName*, *- SubscriptionId*, en *- WorkspaceName*.

     > [!NOTE] 
     > Vraag tooauthenticate met Azure bent u nadat u Hallo-script uitvoeren.  U **moet** aanmelden met een account dat lid is van de rol Abonnementsbeheerders hello en medebeheerder van Hallo-abonnement.  
     >  
    
        .\New-OnPremiseHybridWorker.ps1 -AutomationAccountName <NameofAutomationAccount> `
        -ResourceGroupName <NameofOResourceGroup> -HybridGroupName <NameofHRWGroup> `
        -SubscriptionId <AzureSubscriptionId> -WorkspaceName <NameOfOMSWorkspace>

4. U bent na vragen aan gebruiker tooagree tooinstall **NuGet** en u na vragen aan gebruiker tooauthenticate met uw Azure-referenties.<br><br> ![Uitvoering van script New-OnPremiseHybridWorker](media/automation-hybrid-runbook-worker/new-onpremisehybridworker-scriptoutput.png)

5. Nadat Hallo-script voltooid is, ziet Hallo Hybrid Worker-groepen blade Hallo nieuwe groep en het aantal leden of als een bestaande groep Hallo aantal leden wordt verhoogd.  U kunt Hallo groep selecteren in de lijst Hallo op Hallo **Hybrid Worker-groepen** blade en selecteer Hallo **Hybrid Workers** tegel.  Op Hallo **Hybrid Workers** blade ziet u elk lid van het Hallo-groep die wordt vermeld.  

### <a name="manual-deployment"></a>Handmatige implementatie 
De eerste twee stappen Hallo eenmaal uitvoeren voor uw Automation-omgeving en herhaal vervolgens de resterende stappen voor elke computer worker Hallo.

#### <a name="1-create-operations-management-suite-workspace"></a>1. Operations Management Suite-werkruimte maken
Als u nog geen een Operations Management Suite-werkruimte, maakt u een met instructies voor [beheren van uw werkruimte](../log-analytics/log-analytics-manage-access.md). Als u al hebt, kunt u een bestaande werkruimte gebruiken.

#### <a name="2-add-automation-solution-toooperations-management-suite-workspace"></a>2. Automation-oplossing tooOperations Management Suite-werkruimte toevoegen
Oplossingen toevoegen functionaliteit tooOperations Management Suite.  Hallo Automation-oplossing voegt u functionaliteit voor Azure Automation biedt ook ondersteuning voor hybride Runbook Worker.  Wanneer u Hallo oplossing tooyour werkruimte toevoegt, worden deze automatisch duwt worker onderdelen toohello agentcomputer die u in de volgende stap Hallo installeren wilt af.

Volg de instructies Hallo voor [tooadd een oplossing met behulp van Hallo oplossingen galerie](../log-analytics/log-analytics-add-solutions.md) tooadd hello **Automation** oplossing tooyour Operations Management Suite-werkruimte.

#### <a name="3-install-hello-microsoft-monitoring-agent"></a>3. Hallo Microsoft Monitoring Agent installeren
Hallo Microsoft Monitoring Agent verbindt computers tooOperations Management Suite.  Wanneer u Hallo-agent op uw on-premises computer installeren en verbindt u deze werkruimte tooyour, wordt deze automatisch Hallo-onderdelen die vereist zijn voor hybride Runbook Worker te downloaden.

Volg de instructies Hallo voor [verbinding maken met Windows-computers tooLog Analytics](../log-analytics/log-analytics-windows-agents.md) tooinstall Hallo-agent op Hallo on-premises computer.  U kunt dit proces herhalen voor meerdere computers tooadd tooyour omgeving met meerdere werknemers.

Wanneer Hallo-agent heeft tooOperations Management Suite is verbonden, wordt het weergegeven op Hallo **verbonden bronnen** tabblad Hallo Operations Management Suite **instellingen** deelvenster.  U kunt controleren die Hallo-agent correct Hallo Automation-oplossing heeft gedownload wanneer er een map met de naam **AzureAutomationFiles** in C:\Program Files\Microsoft Monitoring Agent\Agent.  Hallo Hybrid Runbook Worker tooconfirm Hallo-versie, kunt u navigeren tooC:\Program Files\Microsoft Agent\Agent\AzureAutomation\ bewaking en Opmerking Hallo \\ *versie* submap.   

#### <a name="4-install-hello-runbook-environment-and-connect-tooazure-automation"></a>4. Hallo runbook-omgeving installeren en verbinding maken met tooAzure Automation
Wanneer u een agent tooOperations Management Suite toevoegt, Hallo Automation-oplossing pushes omlaag Hallo **HybridRegistration** PowerShell-module, waarin Hallo **Add-HybridRunbookWorker** cmdlet.  U gebruikt deze cmdlet tooinstall hello runbook-omgeving op Hallo-computer en bij Azure Automation registreren.

Open een PowerShell-sessie in de beheerdersmodus en Voer Hallo opdrachten tooimport Hallo module te volgen.

    cd "C:\Program Files\Microsoft Monitoring Agent\Agent\AzureAutomation\<version>\HybridRegistration"
    Import-Module HybridRegistration.psd1

Voer Hallo **Add-HybridRunbookWorker** Hallo syntaxis met de cmdlet:

    Add-HybridRunbookWorker –GroupName <String> -EndPoint <Url> -Token <String>

Hallo informatie vereist voor deze cmdlet uit Hallo **sleutels beheren** blade in hello Azure-portal.  Deze blade openen door te selecteren van Hallo **sleutels** optie uit Hallo **instellingen** blade in uw Automation-account.

![Overzicht van hybride Runbook Worker](media/automation-hybrid-runbook-worker/elements-panel-keys.png)

* **GroupName** heet Hallo Hallo Hybrid Runbook Worker-groep. Als deze groep al in Hallo automation-account bestaat, wordt de huidige computer Hallo tooit toegevoegd.  Als deze niet bestaat nog, wordt deze toegevoegd.
* **Eindpunt** Hallo is **URL** veld Hallo **sleutels beheren** blade.
* **Token** Hallo is **primaire toegangssleutel** in Hallo **sleutels beheren** blade.  

Gebruik Hallo **-uitgebreide** overschakelen met **Add-HybridRunbookWorker** tooreceive gedetailleerde informatie over het Hallo-installatie.

#### <a name="5-install-powershell-modules"></a>5. PowerShell-modules installeren
Runbooks kunt u elk Hallo activiteiten en cmdlets die zijn gedefinieerd in Hallo modules geïnstalleerd in uw Azure Automation-omgeving.  Deze modules worden niet automatisch geïmplementeerde tooon lokale computers, moet u deze handmatig installeren.  Hallo-uitzondering is hello Azure-module, dat standaard toocmdlets toegang bieden voor alle Azure-services en activiteiten voor Azure Automation is geïnstalleerd.

Aangezien Hallo primaire doel van Hallo Hybrid Runbook Worker-functie toomanage lokale bronnen is, moet u waarschijnlijk tooinstall Hallo modules die ondersteuning bieden voor deze resources.  U kunt te verwijzen[Modules installeren](http://msdn.microsoft.com/library/dd878350.aspx) voor informatie over het installeren van Windows PowerShell-modules.  Modules die zijn geïnstalleerd, moeten zich in een locatie waarnaar wordt verwezen door de omgevingsvariabele PSModulePath zodat ze automatisch worden geïmporteerd door Hallo hybride worker.  Zie voor meer informatie [wijzigen Hallo installatiepad PSModulePath](https://msdn.microsoft.com/library/dd878326%28v=vs.85%29.aspx). 

## <a name="removing-hybrid-runbook-worker"></a>Hybride Runbook Worker verwijderen 
U kunt een of meer Hybrid Runbook Workers verwijderen uit een groep of u kunt Hallo-groep verwijderen afhankelijk van uw vereisten.  een hybride Runbook Worker uit een on-premises computer, tooremove uitvoeren Hallo stappen te volgen.

1. Navigeer in hello Azure-portal, tooyour Automation-account.  
2. Van Hallo **instellingen** blade Selecteer **sleutels** en noteer de waarden voor veld Hallo **URL** en **primaire toegangssleutel**.  Deze informatie moet u voor de volgende stap Hallo.
3. Open een PowerShell-sessie in de beheerdersmodus en voer de volgende Hallo command - `Remove-HybridRunbookWorker -url <URL> -key <PrimaryAccessKey>`.  Gebruik Hallo **-uitgebreide** overschakelen voor een gedetailleerd logboek van Hallo verwijderingsproces.

> [!NOTE]
> Hallo Microsoft Monitoring Agent wordt niet verwijderd van computer Hallo alleen Hallo-functionaliteit en configuratie van Hallo Hybrid Runbook Worker-rol.  

## <a name="remove-hybrid-worker-groups"></a>Hybrid Worker-groepen verwijderen
een groep tooremove, moet u eerst tooremove Hallo Hybrid Runbook Worker vanaf elke computer die lid is van het Hallo-groep met Hallo procedure eerder weergegeven en Voer Hallo stappen tooremove Hallo groep te volgen.  

1. Hallo Automation-account openen in hello Azure-portal.
2. Selecteer Hallo **Hybrid Worker-groepen** tegel en in Hallo **Hybrid Worker-groepen** blade, selecteer Hallo-groep die u wenst dat toodelete.  Na het selecteren van de specifieke groep Hallo Hallo **Hybrid worker-groep** eigenschappenblade wordt weergegeven.<br> ![Blade Hybrid Runbook Worker-groep](media/automation-hybrid-runbook-worker/automation-hybrid-runbook-worker-group-properties.png)   
3. Klik op de eigenschappenblade Hallo voor de geselecteerde groep hello, **verwijderen**.  Een bericht weergegeven waarin wordt gevraagd tooconfirm u deze actie, selecteer **Ja** als u weet zeker dat u tooproceed.<br> ![Dialoogvenster voor bevestiging groep verwijderen](media/automation-hybrid-runbook-worker/automation-hybrid-runbook-worker-confirm-delete.png)<br> Dit kan duren enkele seconden toocomplete en u kunt de voortgang onder volgen **meldingen** in Hallo-menu.  

## <a name="troubleshooting"></a>Problemen oplossen 
Hallo Hybrid Runbook Worker is afhankelijk Hallo van Microsoft Monitoring Agent toocommunicate met uw Automation-account tooregister Hallo worker, ontvangen van runbooktaken en status rapporteren. Als de registratie van de werknemer Hallo mislukt, volgen hier enkele mogelijke oorzaken voor Hallo-fout:  

1. Hallo hybride worker zich achter een proxy of firewall.  
    Controleer of Hallo computer heeft uitgaande toegang too*.azure-automation.net op poort 443.  

2. Hallo computer Hallo hybride worker wordt uitgevoerd op is kleiner dan de minimale hardwarevereisten Hallo [vereisten](automation-offering-get-started.md#hybrid-runbook-worker).  
    Computers met Hallo Hybrid Runbook Worker moet voldoen aan de minimale hardwarevereisten Hallo voordat u deze toohost deze functie. Anders Hallo computer, afhankelijk van het Resourcegebruik van andere achtergrondprocessen en conflicten veroorzaakt door runbooks tijdens het uitvoeren van Hallo, kennis wordt er meer dan worden gebruikt en ervoor zorgen dat de runbook-taak vertragingen of time-outs.
   Bevestig de aangewezen toorun Hallo Hybrid Runbook Worker functie Hallo-computer voldoet aan de minimale hardwarevereisten Hallo.  Zo ja, monitor CPU en geheugen gebruik toodetermine een correlatie tussen Hallo prestaties van Hybrid Runbook Worker-processen en vensters.  Als er geheugen of CPU-belasting, dit kan wijzen op Hallo nodig tooupgrade of extra processors toevoegen of verhoging van het geheugen tooaddress resource knelpunt Hallo en los Hallo-fout. Selecteer een andere berekeningsresource die u kunt ondersteuning voor de minimale vereisten Hallo en schalen wanneer werkbelasting eisen duiden op dat een verhoging is nodig.
    
3. Hallo service Microsoft Monitoring Agent wordt niet uitgevoerd.  
    Als de service Microsoft Monitoring Agent Windows hello niet wordt uitgevoerd, dit voorkomt dat Hallo Hybrid Runbook Worker communicatie met Azure Automation.  Controleer of Hallo-agent wordt uitgevoerd door te voeren van de volgende opdracht in PowerShell Hallo: `get-service healthservice`.  Als Hallo-service wordt gestopt, voert u Hallo volgende opdracht in PowerShell toostart Hallo-service: `start-service healthservice`.  

4. In Hallo **toepassingen en Services Logs\Operations Manager** gebeurtenislogboek, ziet u gebeurtenis 4502 en EventMessage met **Microsoft.EnterpriseManagement.HealthService.AzureAutomation.HybridAgent**Hello volgende beschrijving: *aangeboden door de service Hallo Hallo-certificaat <wsid>. oms.opinsights.azure.com is niet uitgegeven door een certificeringsinstantie die wordt gebruikt voor Microsoft-services. Neem contact op met uw beheerder netwerk toosee als er een proxy die TLS/SSL-communicatie wordt onderschept worden uitgevoerd. Hallo artikel KB3126513 bevat extra informatie over probleemoplossing voor problemen met de netwerkverbinding.*
    Dit kan worden veroorzaakt door uw proxy- of firewall blockking communicatie tooMicrosoft Azure.  Controleer of Hallo computer uitgaande toegang too*.azure-automation.net op poort 443.

Logboeken worden lokaal opgeslagen op elke worker hybride op C:\ProgramData\Microsoft\System Center\Orchestrator\7.2\SMA\Sandboxes.  U kunt controleren of er zijn geen waarschuwing of foutgebeurtenissen geschreven toohello **toepassingen en Services Logs\Microsoft-SMA\Operations** en **toepassingen en Services Logs\Operations Manager** in het gebeurtenislogboek die duidt dit op een verbindings- of andere probleem met betrekking tot onboarding Hallo rol tooAzure Automation of probleem tijdens het normale bewerkingen uitvoeren.  

## <a name="next-steps"></a>Volgende stappen
Bekijk [runbooks worden uitgevoerd op een hybride Runbook Worker](automation-hrw-run-runbooks.md) toolearn hoe tooconfigure uw runbooks tooautomate verwerkt in uw on-premises datacentrum of andere cloudomgeving.
