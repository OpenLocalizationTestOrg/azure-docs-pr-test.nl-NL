---
title: aaaUse labels JSON-indeling tooschedule Azure VM-status | Microsoft Docs
description: In dit artikel laat zien hoe toouse JSON tekenreeksen op labels tooautomate Hallo planning van de virtuele machine opstarten en afsluiten.
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: 6afed5d2-e939-4749-8b2c-9312b4c16fb2
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: magoedte;paulomarquesc
ms.openlocfilehash: f6bbf1dea1c193e5d1010f12f3b1ed63562f9daf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario-using-json-formatted-tags-toocreate-a-schedule-for-azure-vm-startup-and-shutdown"></a>Azure Automation-scenario: een planning voor de virtuele machine van Azure opstarten en afsluiten toocreate met behulp van JSON-indeling tags
Klanten willen vaak tooschedule Hallo opstarten en afsluiten van de virtuele machines toohelp abonnement kosten te verlagen of ondersteuning voor bedrijven en technische vereisten.

Hallo kunt volgende scenario u tooset van geautomatiseerde opstarten en afsluiten van uw virtuele machines met behulp van een label aangeroepen planning op een niveau van de resourcegroep of het niveau van de virtuele machine in Azure. Dit schema kan worden geconfigureerd vanuit zondag tooSaturday een opstarten en afsluiten.

We hebt enkele out-of-the-box-opties. Deze omvatten:

* [Virtuele-machineschaalsets](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) met instellingen voor automatisch schalen die u in staat stellen tooscale in of uit.
* [DevTest Labs](../devtest-lab/devtest-lab-overview.md) -service, die Hallo ingebouwde mogelijkheden is van de planning van bewerkingen voor opstarten en afsluiten.

Deze opties ondersteunen echter alleen specifieke scenario's en kan niet worden toegepast tooinfrastructure-as-a-service (IaaS) virtuele machines.

Wanneer Hallo planning tag toegepaste tooa resourcegroep is, is het ook toegepaste tooall virtuele machines in die resourcegroep. Als een planning ook rechtstreeks toegepaste tooa VM is, hebben Hallo laatste planning voorrang in Hallo volgorde:

1. De resourcegroep toegepaste tooa plannen
2. Toegepaste tooa resourcegroep en de virtuele machine in de resourcegroep Hallo plannen
3. Planning toegepast tooa virtuele machine

In dit scenario wordt in wezen een JSON-tekenreeks met de opgegeven notatie en toegevoegd als Hallo-waarde voor een tag schema genoemd. Een runbook wordt vervolgens een lijst met alle resourcegroepen en virtuele machines en identificeert Hallo schema's voor elke virtuele machine op basis van de eerder vermelde Hallo-scenario. Vervolgens doorlopen Hallo virtuele machines met's die zijn gekoppeld en welke actie moet worden gehouden evalueert. Bijvoorbeeld, bepaalt dat door virtuele machines moeten toobe gestopt, afsluiten of genegeerd.

Deze runbooks verifiëren met behulp van Hallo [Azure uitvoeren als-account](automation-sec-configure-azure-runas-account.md).

## <a name="download-hello-runbooks-for-hello-scenario"></a>Hallo runbooks voor Hallo scenario downloaden
Dit scenario bestaat uit vier PowerShell Workflow-runbooks die u van Hallo downloaden kunt [TechNet-galerie](https://gallery.technet.microsoft.com/Azure-Automation-Runbooks-84f0efc7) of Hallo [GitHub](https://github.com/paulomarquesdacosta/azure-automation-scheduled-shutdown-and-startup) opslagplaats voor dit project.

| Runbook | Beschrijving |
| --- | --- |
| Test ResourceSchedule |Controleert de planning van elke virtuele machine en afsluiten of opstarten, afhankelijk van het Hallo-planning wordt uitgevoerd. |
| Voeg ResourceSchedule |Hallo planning tag tooa VM of de resource wordt groep toegevoegd. |
| Update ResourceSchedule |Hallo bestaande planning tag wijzigt door deze te vervangen door een nieuwe. |
| Verwijder ResourceSchedule |Hallo planning tag verwijdert uit een groep VM of de resource. |

## <a name="install-and-configure-this-scenario"></a>Dit scenario installeren en configureren
### <a name="install-and-publish-hello-runbooks"></a>Installeren en Hallo runbooks publiceren
Na het downloaden van Hallo runbooks, kunt u deze importeren met behulp van Hallo-procedure in [maken of importeren van een runbook in Azure Automation](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-azure-automation).  Elk runbook gepubliceerd nadat deze is geïmporteerd in uw Automation-account.

### <a name="add-a-schedule-toohello-test-resourceschedule-runbook"></a>Een planning toohello Test ResourceSchedule runbook toevoegen
Volg deze stappen tooenable Hallo planning voor Hallo Test ResourceSchedule runbook. Dit is het Hallo runbook die controleert van welke virtuele machines moet worden gestart, afsluiten, of leeg is.

1. Open uw Automation-account van hello Azure-portal, en klik vervolgens op Hallo **Runbooks** tegel.
2. Op Hallo **Test ResourceSchedule** blade, klikt u op Hallo **planningen** tegel.
3. Op Hallo **planningen** blade, klikt u op **toevoegen van een planning**.
4. Op Hallo **planningen** blade Selecteer **koppelen van een planning tooyour runbook**. Selecteer vervolgens **Maak een nieuwe planning**.
5. Op Hallo **nieuwe planning** blade, typt u Hallo-naam van dit schema, bijvoorbeeld: *HourlyExecution*.
6. Voor de planning Hallo **Start**, Hallo start tooan uur tijdsinterval instellen.
7. Selecteer **terugkeerpatroon**, en vervolgens voor **herhaald elke interval**, selecteer **1 uur**.
8. Controleer **instellen dat verlopen** te is ingesteld,**Nee**, en klik vervolgens op **maken** toosave het nieuwe schema.
9. Op Hallo **planning Runbook** Selecteer opties blade **Parameters en uitvoerinstellingen**. In Hallo Test ResourceSchedule **Parameters** blade Voer Hallo-naam van uw abonnement in Hallo **SubscriptionName** veld.  Dit is alleen Hallo-parameter die zijn voor het Hallo-runbook vereist.  Wanneer u klaar bent, klikt u op **OK**.

Hallo runbookschema moet eruitzien als volgende Hallo wanneer dit voltooid:

![Geconfigureerde Test ResourceSchedule runbook](./media/automation-scenario-start-stop-vm-wjson-tags/automation-schedule-config.png)<br>

## <a name="format-hello-json-string"></a>Indeling Hallo JSON-tekenreeks
Deze oplossing in feite duurt een JSON tekenreeks met de opgegeven notatie en toegevoegd als waarde voor een label Hallo aangeroepen planning. Een runbook wordt vervolgens een lijst met alle resourcegroepen en virtuele machines en identificeert Hallo schema's voor elke virtuele machine.

Hallo runbook worden doorlopen via Hallo virtuele machines met schema's die zijn gekoppeld en controleert welke acties moeten worden genomen. Hallo Hieronder volgt een voorbeeld van hoe Hallo oplossingen moeten worden opgemaakt:

```json
{
    "TzId": "Eastern Standard Time",
    "0": {
        "S": "11",
        "E": "17"
    },
    "1": {
        "S": "9",
        "E": "19"
    },
    "2": {
        "S": "9",
        "E": "19"
    },
}
```

Hier volgt een aantal gedetailleerde informatie over deze structuur:

1. Hallo-indeling van dit JSON-structuur is geoptimaliseerd toowork Hallo 256 tekens beperking weg te nemen van de waarde van een enkel label in Azure.
2. *TzId* vertegenwoordigt Hallo tijdzone van Hallo virtuele machine. Deze ID kan worden verkregen met behulp van Hallo TimeZoneInfo .NET-klasse in een PowerShell-sessie--**[System.TimeZoneInfo]:: GetSystemTimeZones()**.

   ![GetSystemTimeZones in PowerShell](./media/automation-scenario-start-stop-vm-wjson-tags/automation-get-timzone-powershell.png)

   * Weekdagen worden aangeduid met een numerieke waarde van nul toosix. Hallo waarde nul is gelijk aan zondag.
   * Hallo begintijd vertegenwoordigd door Hallo **S** kenmerk en de waarde ervan zich in een 24-uurs notatie.
   * Hallo wordt afgesloten of end tijd vertegenwoordigd Hello **E** kenmerk en de waarde ervan zich in een 24-uurs notatie.

     Als hello **S** en **E** kenmerken elke hebben een waarde van nul (0), Hallo virtuele machine blijft in de huidige status op Hallo moment van evaluatie.
3. Als u tooskip evaluatie voor een specifieke dag van week hello wilt, niet een sectie toevoegen voor die dag van week Hallo. In Hallo na bijvoorbeeld alleen maandag wordt geëvalueerd en hello andere dagen van week Hallo worden genegeerd:

    ```json
    {
        "TzId": "Eastern Standard Time",
        "1": {
            "S": "11",
            "E": "17"
        }
    }
    ```

## <a name="tag-resource-groups-or-vms"></a>Tag-resourcegroepen of VM 's
tooshut omlaag virtuele machines, moet u tootag Hallo virtuele machines of Hallo resourcegroepen waar ze zich bevinden. Virtuele machines waarvoor geen een label voor de planning worden niet geëvalueerd. Ze zijn niet daarom gestart of afgesloten.

Er zijn twee manieren tootag resourcegroepen of VM's met deze oplossing. U kunt dit doen rechtstreeks vanuit Hallo-portal. Of u kunt Hallo toevoegen ResourceSchedule, Update-ResourceSchedule en verwijder ResourceSchedule runbooks.

### <a name="tag-through-hello-portal"></a>Tag via Hallo-portal
Volg deze stappen tootag een virtuele machine of de resourcegroep in Hallo-portal:

1. Hallo JSON-tekenreeks plat en controleer of er geen spaties.  Uw JSON-tekenreeks moet er als volgt uitzien:

    ```json
    {"TzId":"Eastern Standard Time","0":{"S":"11","E":"17"},"1":{"S":"9","E":"19"},"2": {"S":"9","E":"19"},"3":{"S":"9","E":"19"},"4":{"S":"9","E":"19"},"5":{"S":"9","E":"19"},"6":{"S":"11","E":"17"}}
    ```

2. Selecteer Hallo **Tag** pictogram voor een virtuele machine of de resource groep tooapply dit schema.

   ![Optie voor VM-tag](./media/automation-scenario-start-stop-vm-wjson-tags/automation-vm-tag-option.png)

3. Labels zijn gedefinieerd een sleutel-waardepaar te volgen. Type **planning** in Hallo **sleutel** veld en plak Hallo JSON-tekenreeks in Hallo **waarde** veld. Klik op **Opslaan**. Uw nieuwe code wordt nu weergegeven in de lijst Hallo van codes voor uw resource.

   ![VM planning label](./media/automation-scenario-start-stop-vm-wjson-tags/automation-vm-schedule-tag.png)

### <a name="tag-from-powershell"></a>Label van PowerShell
Alle geïmporteerde runbooks bevatten help-informatie aan begin Hallo van Hallo-script dat wordt beschreven hoe tooexecute runbooks rechtstreeks vanuit PowerShell Hallo. U kunt Hallo toevoegen ScheduleResource en Update ScheduleResource runbooks aanroepen vanuit PowerShell. U doen dit door het doorgeven van de vereiste parameters die u in staat stellen tag Hallo toocreate of update voor een groep VM of de resource buiten Hallo-portal.

toocreate, toevoegen en verwijderen van de labels via PowerShell, moet u eerst te[uw PowerShell-omgeving instellen voor Azure](/powershell/azure/overview). Nadat het Hallo-installatie is voltooid, kunt u doorgaan met de Hallo stappen te volgen.

### <a name="create-a-schedule-tag-with-powershell"></a>Een label schema maken met PowerShell
1. Open een PowerShell-sessie. Gebruik vervolgens Hallo tooauthenticate voorbeeld met het Run As-account en uw toospecify een abonnement te volgen:

    ```powershell
    $Conn = Get-AutomationConnection -Name AzureRunAsConnection
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

2. Definieer de planning hash-tabel. Hier volgt een voorbeeld van hoe moet worden opgebouwd:

    ```powershell
    $schedule= @{ "TzId"="Eastern Standard Time"; "0"= @{"S"="11";"E"="17"};"1"= @{"S"="9";"E"="19"};"2"= @{"S"="9";"E"="19"};"3"= @{"S"="9";"E"="19"};"4"= @{"S"="9";"E"="19"};"5"= @{"S"="9";"E"="19"};"6"= @{"S"="11";"E"="17"}}
    ```

3. Hallo-parameters die door Hallo runbook vereist zijn definiëren. In de Hallo voorbeeld te volgen, zijn we die gericht is op een virtuele machine:

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"; "VmName"="VM01";"Schedule"=$schedule}
    ```

    Als u een resourcegroep bent tagging, verwijdert u Hallo *VMName* parameter van Hallo $params hash-tabel als volgt:

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"; "Schedule"=$schedule}
    ```

4. Voer Hallo toevoegen ResourceSchedule runbook met Hallo parameters toocreate Hallo planning tag te volgen:

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Add-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

5. een code van de groep of virtuele machine voor resource, tooupdate uitvoeren Hallo **Update ResourceSchedule** runbook met de Hallo volgende parameters:

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Update-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

### <a name="remove-a-schedule-tag-with-powershell"></a>Verwijderen van een label planning met PowerShell
1. Open een PowerShell-sessie en Hallo na tooauthenticate met het Run As-account en uw tooselect uitvoeren en een abonnement opgeven:

    ```powershell
    Conn = Get-AutomationConnection -Name AzureRunAsConnection
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

2. Hallo-parameters die door Hallo runbook vereist zijn definiëren. In de Hallo voorbeeld te volgen, zijn we die gericht is op een virtuele machine:

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01";"VmName"="VM01"}
    ```

    Als u een label van een resourcegroep verwijderen wilt, verwijdert u Hallo *VMName* parameter van Hallo $params hash-tabel als volgt:

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"}
    ```

3. Hallo verwijderen ResourceSchedule runbook tooremove Hallo planning tag uitvoeren:

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Remove-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

4. Hallo verwijderen ResourceSchedule runbook tooupdate een code van de groep of virtuele machine voor resource, uitvoeren met Hallo volgende parameters:

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Remove-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

> [!NOTE]
> We raden u proactief deze runbooks (en status van de virtuele machines Hallo) tooverify die uw virtuele machines worden afgesloten bewaken en dienovereenkomstig gestart.
>

tooview hello details van Hallo Test ResourceSchedule runbook taak hello Azure-portal, selecteer Hallo **taken** tegel van Hallo runbook. Hallo taak overzicht Hallo invoerparameters en Hallo uitvoer streamen, Daarnaast toogeneral informatie over het Hallo-taak en eventuele uitzonderingen als ze zich heeft voorgedaan.

Hallo **taakoverzicht** berichten van de uitvoer, waarschuwingen en fouten streams Hallo bevat. Selecteer Hallo **uitvoer** tooview tegel gedetailleerde resultaten van Hallo runbook-uitvoering.

![Test ResourceSchedule uitvoer](./media/automation-scenario-start-stop-vm-wjson-tags/automation-job-output.png)

## <a name="next-steps"></a>Volgende stappen
* tooget gestart met PowerShell workflow-runbooks, Zie [Mijn eerste PowerShell workflow-runbook](automation-first-runbook-textual.md).
* toolearn meer informatie over runbooktypen, en hun voordelen en beperkingen, Zie [Azure Automation-runbooktypen](automation-runbook-types.md).
* Zie voor meer informatie over PowerShell-script ondersteuningsfuncties [systeemeigen PowerShell-scriptondersteuning in Azure Automation](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/).
* toolearn meer informatie over logboekregistratie van runbook- en uitvoer, Zie [Runbook uitvoer en berichten in Azure Automation](automation-runbook-output-and-messages.md).
* meer informatie over een Azure uitvoeren als-account en hoe tooauthenticate uw runbooks met behulp van, Zie toolearn [runbooks met Azure uitvoeren als-account verifiëren](automation-sec-configure-azure-runas-account.md).
