---
title: parameters voor invoer aaaRunbook | Microsoft Docs
description: Invoerparameters van Runbook verhogen Hallo flexibiliteit van runbooks doordat u toopass gegevens tooa runbook wanneer deze wordt gestart. In dit artikel beschrijft de verschillende scenario's waar invoerparameters worden gebruikt in runbooks.
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: 4d3dff2c-1f55-498d-9a0e-eee497e5bedb
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/11/2016
ms.author: sngun
ms.openlocfilehash: f3abaf92382e7d41019616bafb14af23cf98dd9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-input-parameters"></a>Invoerparameters voor runbook
Invoerparameters van Runbook verhogen Hallo flexibiliteit van runbooks doordat u toopass gegevens tooit wanneer deze wordt gestart. Hallo-parameters kunt Hallo runbook acties toobe is bedoeld voor specifieke scenario's en omgevingen. In dit artikel begeleidt we u stapsgewijs door verschillende scenario's waar invoerparameters worden gebruikt in runbooks.

## <a name="configure-input-parameters"></a>Invoerparameters configureren
Invoerparameters kunnen worden geconfigureerd in PowerShell en PowerShell Workflow grafische runbooks. Een runbook kan meerdere parameters met verschillende gegevenstypen, of hebben geen parameters helemaal. Invoerparameters kunnen worden verplicht of optioneel en u een standaardwaarde opgeven voor optionele parameters kunt toewijzen. U kunt waarden toewijzen toohello invoerparameters voor een runbook wanneer u deze via een van de beschikbare methoden Hallo starten. Deze methoden omvatten een runbook starten vanuit de portal hello of een webservice. U kunt ook starten als een onderliggend runbook dat inline wordt aangeroepen in een ander runbook.

## <a name="configure-input-parameters-in-powershell-and-powershell-workflow-runbooks"></a>De invoerparameters in PowerShell en PowerShell Workflow-runbooks configureren
PowerShell en [PowerShell Workflow-runbooks](automation-first-runbook-textual.md) in Azure Automation ondersteunen invoerparameters die zijn gedefinieerd via Hallo kenmerken te volgen.  

| **Eigenschap** | **Beschrijving** |
|:--- |:--- |
| Type |Vereist. Hallo-gegevenstype voor de parameterwaarde Hallo verwacht. Elk type .NET is ongeldig. |
| Naam |Vereist. Hallo-naam van Hallo-parameter. Dit moet uniek zijn binnen Hallo runbook, en kan bevatten alleen letters, cijfers of onderstrepingstekens bevatten. Moet beginnen met een letter. |
| Verplicht |Optioneel. Hiermee geeft u op of een waarde voor parameter Hallo moet worden opgegeven. Als u deze te instelt**$true**, en vervolgens moet een waarde worden opgegeven wanneer Hallo runbook wordt gestart. Als u deze te instelt**$false**, en vervolgens een waarde optioneel is. |
| Standaardwaarde |Optioneel.  Hiermee geeft u een waarde die voor de parameter hello worden gebruikt als een waarde niet is doorgegeven als Hallo runbook wordt gestart. Een standaardwaarde kan worden ingesteld voor elke parameter en wordt automatisch doorgevoerd Hallo parameter optionele ongeacht Hallo verplichte instelling. |

Windows PowerShell ondersteunt meer kenmerken van invoerparameters dan die hier worden vermeld, zoals validatie, aliassen en parametersets. Azure Automation ondersteunt echter momenteel alleen Hallo invoerparameters die hierboven worden genoemd.

De parameterdefinitie van een in PowerShell Workflow-runbooks heeft Hallo volgen algemene vorm waarin meerdere parameters zijn gescheiden door komma's.

   ```
     Param
     (
         [Parameter (Mandatory= $true/$false)]
         [Type] Name1 = <Default value>,

         [Parameter (Mandatory= $true/$false)]
         [Type] Name2 = <Default value>
     )
   ```

> [!NOTE]
> Wanneer u parameters, als u geen Hallo opgeeft definieert **verplichte** kenmerk, wordt standaard Hallo parameter wordt beschouwd als optioneel. Ook als u een standaardwaarde voor een parameter in PowerShell Workflow-runbooks instelt, wordt deze verwerkt door PowerShell als een optionele parameter, ongeacht Hallo **verplichte** kenmerkwaarde.
> 
> 

Een voorbeeld: Stel Hallo invoerparameters configureren voor een PowerShell Workflow-runbook die uitvoer meer informatie over virtuele machines, één VM of alle virtuele machines binnen een resourcegroep. Dit runbook heeft twee parameters zoals weergegeven in de volgende schermafbeelding Hallo: Hallo-naam van de virtuele machine en de naam van de resourcegroep Hallo Hallo.

![Werkstroom voor automatisering van PowerShell](media/automation-runbook-input-parameters/automation-01-powershellworkflow.png)

In deze parameterdefinitie Hallo parameters **$VMName** en **$resourceGroupName** eenvoudige parameters van het type tekenreeks zijn. PowerShell en PowerShell Workflow-runbooks ondersteunen echter alle eenvoudige typen en complexe typen, zoals **object** of **PSCredential** voor invoerparameters.

Als uw runbook een invoerparameter objecttype heeft, gebruik vervolgens een hashtabel PowerShell met (naam, waarde) toopass in een waarde-paren. Bijvoorbeeld, als er Hallo parameter in een runbook te volgen:

     [Parameter (Mandatory = $true)]
     [object] $FullName

U kunt vervolgens Hallo na waarde toohello parameter doorgeven:

    @{"FirstName"="Joe";"MiddleName"="Bob";"LastName"="Smith"}


## <a name="configure-input-parameters-in-graphical-runbooks"></a>De invoerparameters in grafische runbooks configureren
te[configureren van een grafisch runbook](automation-first-runbook-graphical.md) met invoerparameters we maken een grafisch runbook die meer informatie over virtuele machines, ofwel een enkele virtuele machine of alle virtuele machines binnen een resourcegroep. Configureren van een runbook bestaat uit twee belangrijkste activiteiten, zoals hieronder wordt beschreven.

[**Runbooks verifiëren met Azure uitvoeren als-account** ](automation-sec-configure-azure-runas-account.md) tooauthenticate met Azure.

[**Get-AzureRmVm** ](https://msdn.microsoft.com/library/mt603718.aspx) tooget Hallo eigenschappen van een virtuele machines.

U kunt Hallo [ **Write-Output** ](https://technet.microsoft.com/library/hh849921.aspx) activiteit toooutput Hallo namen van virtuele machines. Hallo activiteit **Get-AzureRmVm** accepteert twee parameters hello **virtuele-machinenaam** en Hallo **Resourcegroepnaam**. Omdat deze parameters voor verschillende waarden telkens wanneer die u Hallo runbook start vereist kunnen, kunt u invoerparameters tooyour runbook kunt toevoegen. Hier volgen Hallo tooadd invoerparameters-stappen:

1. Selecteer Hallo grafisch runbook uit Hallo **Runbooks** blade en klik vervolgens op [ **bewerken** ](automation-graphical-authoring-intro.md) deze.
2. Hallo runbookeditor, klik op **invoer en uitvoer** tooopen hello **invoer en uitvoer** blade.
   
    ![Grafisch runbook automatisering](media/automation-runbook-input-parameters/automation-02-graphical-runbok-editor.png)
3. Hallo **invoer en uitvoer** blade geeft een lijst van invoerparameters die zijn gedefinieerd voor Hallo runbook weer. Op deze blade kunt u een nieuwe invoerparameter toevoegen of Hallo configuratie van een bestaande invoerparameter bewerken. tooadd een nieuwe parameter voor Hallo runbook, klikt u op **invoer toevoegen** tooopen hello **runbookinvoerparameter** blade. U kunt daar Hallo volgende parameters configureren:
   
   | **Eigenschap** | **Beschrijving** |
   |:--- |:--- |
   | Naam |Vereist.  Hallo-naam van Hallo-parameter. Dit moet uniek zijn binnen Hallo runbook, en kan bevatten alleen letters, cijfers of onderstrepingstekens bevatten. Moet beginnen met een letter. |
   | Beschrijving |Optioneel. Beschrijving van het Hallo-doel van de invoerparameter. |
   | Type |Optioneel. Hallo-gegevenswaarde die wordt verwacht voor het Hallo-parameterwaarde. De van de ondersteunde parametertypen zijn **tekenreeks**, **Int32**, **Int64**, **decimale**, **Booleaanse**, **DateTime**, en **Object**. Als een gegevenstype dat niet is geselecteerd, is de standaardwaarde te**tekenreeks**. |
   | Verplicht |Optioneel. Hiermee geeft u op of een waarde voor parameter Hallo moet worden opgegeven. Als u ervoor kiest **Ja**, en vervolgens moet een waarde worden opgegeven wanneer Hallo runbook wordt gestart. Als u ervoor kiest **geen**, en vervolgens een waarde niet vereist is als Hallo runbook wordt gestart en een standaardwaarde kan worden ingesteld. |
   | Standaardwaarde |Optioneel. Hiermee geeft u een waarde die voor de parameter hello worden gebruikt als een waarde niet is doorgegeven als Hallo runbook wordt gestart. Een standaardwaarde kan worden ingesteld voor een parameter die is niet verplicht. Kies een standaardwaarde tooset **aangepaste**. Deze waarde wordt gebruikt, tenzij een andere waarde wordt opgegeven als Hallo runbook wordt gestart. Kies **geen** als u niet tooprovide wilt een standaardwaarde. |
   
    ![Nieuwe invoer toevoegen](media/automation-runbook-input-parameters/automation-runbook-input-parameter-new.png)
4. Twee parameters maken met de volgende eigenschappen die worden gebruikt door Hallo Hallo **Get-AzureRmVm** activiteit:
   
   * **Parameter1:**
     
     * Naam - VMName
     * Type - tekenreeks
     * Verplicht - Nee
   * **Parameter2:**
     
     * Naam - resourceGroupName
     * Type - tekenreeks
     * Verplicht - Nee
     * Standaardwaarde - aangepast
     * Aangepaste standaardwaarde - \<naam van resourcegroep Hallo Hallo virtuele machines met >
5. Nadat u Hallo parameters toevoegen, klikt u op **OK**.  U kunt ze nu weergeven in Hallo **invoer en uitvoer blade**. Klik op **OK** opnieuw, en klik vervolgens op **opslaan** en **publiceren** uw runbook.

## <a name="assign-values-tooinput-parameters-in-runbooks"></a>Waarden toewijzen tooinput parameters in runbooks
U kunt waarden tooinput parameters doorgeven in runbooks in Hallo volgen scenario's.

### <a name="start-a-runbook-and-assign-parameters"></a>Een runbook Start en parameters toe te wijzen
Een runbook kan op veel verschillende manieren worden gestart: via hello Azure-portal, met een webhook, met PowerShell-cmdlets, hello REST-API of Hello SDK. Hieronder besproken verschillende methoden voor een runbook starten en het toewijzen van parameters.

#### <a name="start-a-published-runbook-by-using-hello-azure-portal-and-assign-parameters"></a>Een gepubliceerd runbook start met behulp van hello Azure-portal en parameters toewijzen
Wanneer u [hello runbook starten](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal), Hallo **Runbook starten** blade wordt geopend en kunt u waarden voor Hallo-parameters die u zojuist hebt gemaakt.

![Aan de slag met Hallo-portal](media/automation-runbook-input-parameters/automation-04-startrunbookusingportal.png)

Hallo-label onder het invoervak hello ziet u Hallo kenmerken die zijn ingesteld voor parameter Hallo. Kenmerken zijn verplicht of optioneel, type en de standaardwaarde. Hallo help ballon volgende toohello parameternamen ziet u alle Hallo belangrijke informatie die u toomake beslissingen te nemen over parameter invoerwaarden nodig. Deze informatie omvat of een parameter verplicht of optioneel is. Dit omvat ook Hallo type en de standaardwaarde (indien aanwezig) en andere nuttige notities.

![Ballon met Help](media/automation-runbook-input-parameters/automation-05-helpbaloon.png)

> [!NOTE]
> Ondersteuning voor parameters van type String **leeg** tekenreekswaarden.  Invoeren **[EmptyString]** in Hallo invoerparameter vak geeft een lege tekenreeks toohello-parameter. Ook de parameters van het type tekenreeks niet ondersteunen **Null** waarden worden doorgegeven. Als u waarde toohello tekenreeksparameter gebruikt niet slaagt, wordt klikt u vervolgens PowerShell geïnterpreteerd als null.
> 
> 

#### <a name="start-a-published-runbook-by-using-powershell-cmdlets-and-assign-parameters"></a>Een gepubliceerd runbook start met behulp van PowerShell-cmdlets en parameters toewijzen
* **Azure Resource Manager-cmdlets:** kunt u beginnen met een Automation-runbook is gemaakt in een resourcegroep met [Start AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx).
  
  **Voorbeeld:**
  
  ```
  $params = @{“VMName”=”WSVMClassic”;”resourceGroupeName”=”WSVMClassicSG”}
  
  Start-AzureRmAutomationRunbook -AutomationAccountName “TestAutomation” -Name “Get-AzureVMGraphical” –ResourceGroupName $resourceGroupName -Parameters $params
  ```
* **Azure Service Management-cmdlets:** kunt u beginnen met een automation-runbook dat is gemaakt in een standaardresourcegroep met behulp van [Start AzureAutomationRunbook](https://msdn.microsoft.com/library/dn690259.aspx).
  
  **Voorbeeld:**
  
  ```
  $params = @{“VMName”=”WSVMClassic”; ”ServiceName”=”WSVMClassicSG”}
  
  Start-AzureAutomationRunbook -AutomationAccountName “TestAutomation” -Name “Get-AzureVMGraphical” -Parameters $params
  ```

> [!NOTE]
> Wanneer u een runbook start met behulp van PowerShell-cmdlets, een standaardparameter **MicrosoftApplicationManagementStartedBy** wordt gemaakt met de waarde Hallo **PowerShell**. U kunt deze parameter weergeven in Hallo **taakgegevens** blade.  
> 
> 

#### <a name="start-a-runbook-by-using-an-sdk-and-assign-parameters"></a>Een runbook start met behulp van een SDK en parameters toe te wijzen
* **Azure Resource Manager-methode:** kunt u een runbook start met behulp van Hallo SDK van een programmeertaal. Hieronder ziet u een C#-codefragment voor het starten van een runbook in uw Automation-account. U vindt alle Hallo-code op onze [GitHub-opslagplaats](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ResourceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).  
  
  ```
   public Job StartRunbook(string runbookName, IDictionary<string, string> parameters = null)
      {
        var response = AutomationClient.Jobs.Create(resourceGroupName, automationAccount, new JobCreateParameters
         {
            Properties = new JobCreateProperties
             {
                Runbook = new RunbookAssociationProperty
                 {
                   Name = runbookName
                 },
                   Parameters = parameters
             }
         });
      return response.Job;
      }
  ```
* **Azure Service Management-methode:** kunt u een runbook start met behulp van Hallo SDK van een programmeertaal. Hieronder ziet u een C#-codefragment voor het starten van een runbook in uw Automation-account. U vindt alle Hallo-code op onze [GitHub-opslagplaats](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ServiceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).
  
  ```      
  public Job StartRunbook(string runbookName, IDictionary<string, string> parameters = null)
    {
      var response = AutomationClient.Jobs.Create(automationAccount, new JobCreateParameters
    {
      Properties = new JobCreateProperties
         {
           Runbook = new RunbookAssociationProperty
         {
           Name = runbookName
              },
                Parameters = parameters
              }
       });
      return response.Job;
    }
  ```
  
  toostart deze methode maakt een woordenlijst toostore hello runbook-parameters, **VMName** en **resourceGroupName**, en de bijbehorende waarden. Hallo runbook start. Hieronder vindt u Hallo C# codefragment voor het aanroepen van Hallo-methode die hierboven gedefinieerd.
  
  ```
  IDictionary<string, string> RunbookParameters = new Dictionary<string, string>();
  
  // Add parameters toohello dictionary.
  RunbookParameters.Add("VMName", "WSVMClassic");
  RunbookParameters.Add("resourceGroupName", "WSSC1");
  
  //Call hello StartRunbook method with parameters
  StartRunbook(“Get-AzureVMGraphical”, RunbookParameters);
  ```

#### <a name="start-a-runbook-by-using-hello-rest-api-and-assign-parameters"></a>Een runbook start met behulp van Hallo REST-API en parameters toe te wijzen
Een runbooktaak worden gemaakt en gestart met hello Azure Automation REST-API met behulp van Hallo **plaatsen** methode met de volgende Hallo URI van de aanvraag.

    https://management.core.windows.net/<subscription-id>/cloudServices/<cloud-service-name>/resources/automation/~/automationAccounts/<automation-account-name>/jobs/<job-id>?api-version=2014-12-08`

Vervang in Hallo aanvraag-URI, Hallo volgende parameters:

* **abonnement-id:** uw Azure-abonnement-ID.  
* **cloud-service-naam:** Hallo-naam van Hallo cloud toowhich Hallo serviceaanvraag moet worden verzonden.  
* **Automation-account-name:** Hallo-naam van uw automation-account die wordt gehost binnen Hallo opgegeven cloudservice.  
* **taak-id:** hello GUID voor Hallo-taak. GUID's in PowerShell kunnen worden gemaakt met behulp van Hallo **[GUID]::NewGuid(). ToString()** opdracht.

Gebruik in volgorde toopass parameters toohello runbooktaak, Hallo aanvraagtekst. Het duurt Hallo twee eigenschappen in JSON-indeling te volgen:

* **Runbooknaam:** vereist. Hallo de naam van Hallo runbook voor Hallo taak toostart.  
* **Runbook-parameters:** optioneel. Een dictionary van parameterlijst Hallo in (naam, waarde) waar de naam moet van het type tekenreeks en de waarde is een geldig JSON-waarde opmaken.

Als u wilt dat toostart hello **Get-AzureVMTextual** runbook dat eerder is gemaakt met **VMName** en **resourceGroupName** gebruiken als parameters Hallo volgende JSON-indeling voor Hallo aanvraagtekst.

   ```
    {
      "properties":{
        "runbook":{
        "name":"Get-AzureVMTextual"},
      "parameters":{
         "VMName":"WSVMClassic",
         "resourceGroupName":”WSCS1”}
        }
    }
   ```

Een HTTP-statuscode 201 wordt geretourneerd als het Hallo-taak is gemaakt. Raadpleeg voor meer informatie over antwoordheaders en antwoordtekst Hallo toohello artikel over het te[een runbooktaak maken met behulp van Hallo REST-API.](https://msdn.microsoft.com/library/azure/mt163849.aspx)

### <a name="test-a-runbook-and-assign-parameters"></a>Een runbook testen en parameters toewijzen
Wanneer u [test Hallo conceptversie van uw runbook](automation-testing-runbook.md) Hallo Hallo test-optie gebruikt, **testen** blade wordt geopend en kunt u waarden voor Hallo-parameters die u zojuist hebt gemaakt.

![Testen en parameters toewijzen](media/automation-runbook-input-parameters/automation-06-testandassignparameters.png)

### <a name="link-a-schedule-tooa-runbook-and-assign-parameters"></a>Een planning tooa runbook koppelen en parameters toewijzen
U kunt [een planning koppelen](automation-schedules.md) tooyour runbook zodanig dat Hallo runbook wordt gestart op een bepaald tijdstip. U toewijzen invoerparameters wanneer u Hallo planning maakt en Hallo runbook deze waarden worden gebruikt wanneer deze wordt gestart door Hallo schema. U kunt Hallo planning niet opslaan, totdat alle verplichte parameterwaarden zijn opgegeven.

![Plannen en parameters toewijzen](media/automation-runbook-input-parameters/automation-07-scheduleandassignparameters.png)

### <a name="create-a-webhook-for-a-runbook-and-assign-parameters"></a>Een webhook voor een runbook maken en toewijzen van parameters
Kunt u een [webhook](automation-webhooks.md) voor uw runbook en invoerparameters van runbook configureren. U kunt Hallo webhook niet opslaan, totdat alle verplichte parameterwaarden zijn opgegeven.

![Webhook maken en toewijzen van parameters](media/automation-runbook-input-parameters/automation-08-createwebhookandassignparameters.png)

Als u een runbook met behulp van een webhook uitvoert, Hallo vooraf gedefinieerde invoerparameter  **[Webhookdata](automation-webhooks.md#details-of-a-webhook)**  wordt verzonden, samen met de Hallo invoerparameters die u hebt gedefinieerd. U kunt klikken op tooexpand hello **WebhookData** parameter voor meer informatie.

![WebhookData-parameter](media/automation-runbook-input-parameters/automation-09-webhook-data-parameters.png)

## <a name="next-steps"></a>Volgende stappen
* Zie voor meer informatie over runbookinvoer en uitvoer [Azure Automation: runbook invoer, uitvoer en geneste runbooks](https://azure.microsoft.com/blog/azure-automation-runbook-input-output-and-nested-runbooks/).
* Zie voor meer informatie over de verschillende manieren toostart een runbook [een runbook starten](automation-starting-a-runbook.md).
* tooedit tekstueel runbook te verwijzen[bewerken tekstuele runbooks](automation-edit-textual-runbook.md).
* een grafisch runbook tooedit te verwijzen[grafisch ontwerpen in Azure Automation](automation-graphical-authoring-intro.md).

