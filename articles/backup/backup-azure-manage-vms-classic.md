---
title: aaaManage monitor virtuele machine van Azure back-ups en | Microsoft Docs
description: Meer informatie over hoe toomanage en de monitor een Azure virtuele machine back-ups
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: 4372944e-d33a-4f6a-bd5f-d04af2842713
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: trinadhk;markgal;
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: cb95e0b3760c96f7fd563c42cb4c635553f48957
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-common-azure-backup-jobs-and-trigger-alerts-in-hello-classic-portal"></a>Algemene Azure Backup-taken en waarschuwingen in de klassieke portal Hallo trigger beheren
> [!div class="op_single_selector"]
> * [Back-ups van virtuele machine in Azure beheren](backup-azure-manage-vms.md)
> * [Klassieke VM-back-ups beheren](backup-azure-manage-vms-classic.md)
>
>

In dit artikel bevat informatie over algemene beheer en controle taken voor het klassieke model virtuele machines in Azure beveiligde.  

> [!NOTE]
> Azure heeft twee implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../azure-resource-manager/resource-manager-deployment-model.md). Zie [voorbereiden van uw omgeving tooback van virtuele machines in Azure](backup-azure-vms-prepare.md) voor meer informatie over het werken met Classic deployment model virtuele machines.
>
> [!IMPORTANT]
>Vanaf maart 2017, kunt u niet meer gebruiken Hallo klassieke portal toocreate Backup-kluizen.
>
> U kunt nu uw back-up kluizen tooRecovery Services-kluizen upgraden. Zie voor meer informatie artikel Hallo [upgraden van een back-up kluis tooa Recovery Services-kluis](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft raadt u tooupgrade uw back-upkluizen tooRecovery Services-kluizen.<br/> U kunt PowerShell toocreate Backup-kluizen niet gebruiken na 15 oktober 2017. **Per 1 november 2017**:
>- Alle resterende Backup-kluizen worden automatisch bijgewerkt tooRecovery Services-kluizen.
>- U niet kunt tooaccess uw back-upgegevens in de klassieke portal Hallo. In plaats daarvan gebruik hello Azure portal tooaccess uw back-upgegevens in Recovery Services-kluizen.

## <a name="manage-protected-virtual-machines"></a>Beveiligde virtuele machines beheren
toomanage beveiligde virtuele machines:

1. tooview en beheren van back-upinstellingen voor een virtuele machine en klik op Hallo **beveiligde Items** tabblad.
2. Klik op Hallo-naam van een beveiligde item toosee hello **back-Details** tabblad u informatie over de laatste back-up Hallo ziet.

    ![Back-up van virtuele machine](./media/backup-azure-manage-vms/backup-vmdetails.png)
3. tooview en de back-upbeleid instellingen beheren voor een virtuele machine en klik op Hallo **beleid** tabblad.

    ![Beleid voor de virtuele machine](./media/backup-azure-manage-vms/manage-policy-settings.png)

    Hallo **back-upbeleid** tabblad ziet u een bestaand beleid Hallo. U kunt zo nodig wijzigen. Als u een nieuw beleid toocreate klikt u op **maken** op Hallo **beleid** pagina. Houd er rekening mee dat als u tooremove wilt een beleid voor deze mag niet gekoppeld aan virtuele machines hebt.

    ![Beleid voor de virtuele machine](./media/backup-azure-manage-vms/backup-vmpolicy.png)
4. U kunt meer informatie over acties of status ophalen voor een virtuele machine op Hallo **taken** pagina. Klik op een taak in Hallo lijst tooget meer gedetailleerde informatie, of taken voor het filter voor een specifieke virtuele machine.

    ![Taken](./media/backup-azure-manage-vms/backup-job.png)

## <a name="on-demand-backup-of-a-virtual-machine"></a>Op aanvraag back-up van een virtuele machine
U kunt op aanvraag back-up van een virtuele machine uitvoeren zodra deze is geconfigureerd voor beveiliging. Als de eerste back-up Hallo in behandeling is voor Hallo virtuele machine, maakt back-up op aanvraag een volledige kopie van Hallo virtuele machine in Azure Backup-kluis. Als de eerste back-up is voltooid, is op aanvraag back-up worden alleen wijzigingen van eerdere back-up van het back-tooAzure verzenden dat wil zeggen het Vault altijd incrementeel.

> [!NOTE]
> Bewaartermijn van een op aanvraag back-up is opgegeven voor het dagelijkse bewaren in de back-upbeleid bijbehorende toohello VM tooretention-waarde ingesteld.  
>
>

tootake op aanvraag back-up van een virtuele machine:

1. Navigeer toohello **beveiligde Items** pagina en selecteer **Azure virtuele Machine** als **Type** (indien nog niet geselecteerd) en klik op **Selecteer**knop.

    ![VM-Type](./media/backup-azure-manage-vms/vm-type.png)
2. Selecteer Hallo virtuele machine waarop u wilt dat back-tootake op aanvraag en klik op **nu back-** knop Hallo onder Hallo pagina aan.

    ![Nu een back-maken](./media/backup-azure-manage-vms/backup-now.png)

    Hiermee maakt u een back-uptaak op Hallo geselecteerde virtuele machine. De bewaartermijn van het herstelpunt dat is gemaakt door middel van deze taak wordt niet hetzelfde zijn dat is opgegeven in het beleid voor Hallo Hallo virtuele machine gekoppeld.

    ![Maken van back-uptaak](./media/backup-azure-manage-vms/creating-job.png)

   > [!NOTE]
   > tooview hello beleid die zijn gekoppeld aan een virtuele machine, detail omlaag in de virtuele machine in Hallo **beveiligde Items** pagina en ga toobackup beleid tab.
   >
   >
3. Zodra het Hallo-taak is gemaakt, kunt u klikken op **taak weergeven** knop in Hallo toast balk toosee Hallo bijbehorende taak in de pagina Hallo-taken.

    ![back-uptaak gemaakt](./media/backup-azure-manage-vms/created-job.png)
4. Na het Hallo-taak is voltooid, een herstelpunt wordt gemaakt waarmee u kunt toorestore Hallo virtuele machine. Dit wordt ook waarde Hallo herstelpunt kolom verhoogd met 1 in **beveiligde Items** pagina.

## <a name="stop-protecting-virtual-machines"></a>Stop de beveiliging van virtuele machines
U kunt toostop Hallo toekomstige back-ups van een virtuele machine met Hallo volgende opties:

* Bewaren van back-upgegevens die zijn gekoppeld aan virtuele machine in Azure Backup-kluis
* Back-upgegevens die zijn gekoppeld aan virtuele machine verwijderen

Als u de back-upgegevens tooretain die zijn gekoppeld aan virtuele machine hebt geselecteerd, kunt u Hallo back-upgegevens toorestore Hallo virtuele machine. Voor prijsinformatie voor zulke virtuele machines, klikt u op [hier](https://azure.microsoft.com/pricing/details/backup/).

de beveiliging van de tooStop voor een virtuele machine:

1. Navigeer te**beveiligde Items** pagina en selecteer **virtuele machine van Azure** als Hallo filtertype (indien nog niet geselecteerd) en klik op **Selecteer** knop.

    ![VM-Type](./media/backup-azure-manage-vms/vm-type.png)
2. Selecteer Hallo virtuele machine en klik op **beveiliging stoppen** Hallo Hallo pagina onderaan in.

    ![Stop de beveiliging](./media/backup-azure-manage-vms/stop-protection.png)
3. Standaard Azure Backup wordt niet verwijderd Hallo back-upgegevens Hallo virtuele machine gekoppeld.

    ![Stop de beveiliging bevestigen](./media/backup-azure-manage-vms/confirm-stop-protection.png)

    Als u back-upgegevens toodelete wilt, selecteert u selectievakje Hallo.

    ![Selectievakje](./media/backup-azure-manage-vms/checkbox.png)

    Selecteer een reden voor het stoppen van Hallo back-up. Dit is optioneel, bieden een reden helpen Azure Backup toowork op Hallo feedback en prioriteren Hallo klant scenario's.
4. Klik op **indienen** knop toosubmit hello **beveiliging stoppen** taak. Klik op **taak weergeven** toosee Hallo bijbehorende Hallo taak in **taken** pagina.

    ![Stop de beveiliging](./media/backup-azure-manage-vms/stop-protect-success.png)

    Als u niet hebt geselecteerd **verwijderen die zijn gekoppeld back-upgegevens** optie tijdens **beveiliging stoppen** wizard, dan zal na een opdracht is voltooid, beveiliging te verandert de status**beveiliging gestopt**. Hallo gegevens blijven met Azure Backup tot deze expliciet worden verwijderd. U kunt altijd Hallo gegevens verwijderen Hallo virtuele machine door in te schakelen Hallo **beveiligde Items** pagina en te klikken op **verwijderen**.

    ![Gestopte beveiliging](./media/backup-azure-manage-vms/protection-stopped-status.png)

    Als u hebt geselecteerd Hallo **verwijderen die zijn gekoppeld back-upgegevens** optie, hello virtuele machine niet deel uit van Hallo **beveiligde Items** pagina.

## <a name="re-protect-virtual-machine"></a>Virtuele machine opnieuw te beveiligen
Als u hebt geen Hallo geselecteerd **koppelen back-upgegevens verwijderen** optie in **beveiliging stoppen**, kunt u Hallo virtuele machine opnieuw beveiligen door Hallo stappen vergelijkbaar toobacking up virtuele geregistreerd machines. Als beveiligd, deze virtuele machine back-upgegevens bewaard voorafgaande toostop beveiliging hebben en herstelpunten zijn gemaakt na het opnieuw te beveiligen.

Na het opnieuw te beveiligen, de beveiligingsstatus Hallo virtuele machine te worden gewijzigd**beveiligde** als er te herstelpunten zijn eerdere**beveiliging stoppen**.

  ![Opnieuw beveiligde virtuele machine](./media/backup-azure-manage-vms/reprotected-status.png)

> [!NOTE]
> Wanneer Hallo virtuele machine opnieuw te beveiligen, kunt u een ander beleid dan Hallo-beleid waarmee virtuele machine in eerste instantie is beveiligd.
>
>

## <a name="unregister-virtual-machines"></a>Hef de registratie van virtuele machines
Als u tooremove Hallo virtuele machine vanuit de back-upkluis Hallo wilt:

1. Klik op Hallo **UNREGISTER** knop Hallo onder Hallo pagina aan.

    ![Schakel de beveiliging](./media/backup-azure-manage-vms/unregister-button.png)

    Een toast-melding wordt weergegeven onder Hallo van welkomstscherm bevestiging aanvragen. Klik op **Ja** toocontinue.

    ![Schakel de beveiliging](./media/backup-azure-manage-vms/confirm-unregister.png)

## <a name="delete-backup-data"></a>Back-up van gegevens verwijderen
U kunt de back-upgegevens Hallo die zijn gekoppeld aan een virtuele machine, ofwel verwijderen:

* Tijdens de taak beveiliging stoppen
* Na een stop de beveiliging is taak voltooid op een virtuele machine

back-upgegevens op een virtuele machine, dat zich in Hallo bevindt toodelete *beveiliging gestopt* status na de voltooiing van een **back-up stoppen** taak:

1. Navigeer toohello **beveiligde Items** pagina en selecteer **Azure virtuele Machine** als *type* en klik op Hallo **Selecteer** knop.

    ![VM-Type](./media/backup-azure-manage-vms/vm-type.png)
2. Selecteer Hallo virtuele machine. Hallo virtuele machine zich **beveiliging gestopt** status.

    ![Beveiliging is gestopt](./media/backup-azure-manage-vms/protection-stopped-b.png)
3. Klik op Hallo **verwijderen** knop Hallo onder Hallo pagina aan.

    ![Back-up verwijderen](./media/backup-azure-manage-vms/delete-backup.png)
4. In Hallo **verwijderen van de back-upgegevens** wizard, selecteert u een reden voor het verwijderen van de back-upgegevens (sterk aanbevolen) en klik op **indienen**.

    ![Back-upgegevens verwijderen](./media/backup-azure-manage-vms/delete-backup-data.png)
5. Hiermee wordt een taak toodelete back-upgegevens van de geselecteerde virtuele machine gemaakt. Klik op **taak weergeven** toosee bijbehorende taak in de pagina taken.

    ![Verwijderen van gegevens is voltooid](./media/backup-azure-manage-vms/delete-data-success.png)

    Zodra het Hallo-taak is voltooid, Hallo vermelding overeenkomstige toohello virtuele machine wordt verwijderd uit **beveiligde items** pagina.

## <a name="dashboard"></a>Dashboard
Op Hallo **Dashboard** pagina die u informatie over virtuele machines in Azure, de opslag- en taken die zijn gekoppeld in Hallo afgelopen 24 uur controleren kunt. U kunt back-status en eventuele bijbehorende back-fouten weergeven.

![Dashboard](./media/backup-azure-manage-vms/dashboard-protectedvms.png)

> [!NOTE]
> Waarden in Hallo dashboard worden elke 24 uur vernieuwd.
>
>

## <a name="auditing-operations"></a>Controle-bewerkingen
Azure backup biedt beoordeling van Hallo 'bewerking logs' van de back-upbewerkingen geactiveerd door zodat u eenvoudig toosee precies welke bewerkingen zijn uitgevoerd op de back-upkluis Hallo Hallo-klant. Operations logs geweldige postmortemkeuring inschakelen en ondersteuning voor back-upbewerkingen Hallo controleren.

Hallo volgende bewerkingen worden vastgelegd in Logboeken van de bewerking:

* Registreren
* Registratie ongedaan maken
* Beveiliging configureren
* Back-up (zowel gepland en op aanvraag back-ups via BackupNow)
* Herstellen
* Stop de beveiliging
* Back-upgegevens verwijderen
* Beleid toevoegen
* Beleid verwijderen
* Bijwerken van beleid
* Taak annuleren

tooview bewerkingslogboeken bijbehorende tooa back-upkluis:

1. Navigeer te**beheerservices** in Azure-portal en klik vervolgens op Hallo **Bewerkingslogboeken** tabblad.

    ![Bewerkingslogboeken](./media/backup-azure-manage-vms/ops-logs.png)
2. Selecteer in het Hallo-filters **back-** als *Type* en geef de naam van back-upkluis Hallo in *servicenaam* en klik op **indienen**.

    ![Bewerking Logboeken filteren](./media/backup-azure-manage-vms/ops-logs-filter.png)
3. Selecteer elke bewerking in Hallo operations Logboeken, en klik **Details** toosee details bijbehorende tooan-bewerking.

    ![Details van bewerking logboeken ophalen](./media/backup-azure-manage-vms/ops-logs-details.png)

    Hallo **Details wizard** bevat informatie over Hallo bewerking geactiveerd, taak-Id, de resource waarop deze bewerking wordt geactiveerd en de begintijd van Hallo-bewerking.

    ![Details van bewerking](./media/backup-azure-manage-vms/ops-logs-details-window.png)

## <a name="alert-notifications"></a>Meldingen van waarschuwingen
U kunt aangepaste waarschuwingsmeldingen voor Hallo taken krijgen in de portal. Dit wordt bereikt door het definiëren van regels voor waarschuwingen op basis van PowerShell van operationele Logboeken gebeurtenissen. Wordt u aangeraden *PowerShell versie 1.3.0 of hoger*.

een aangepaste melding tooalert mislukte back-ups toodefine, een voorbeeld van een opdracht, ziet er als:

```
PS C:\> $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail contoso@microsoft.com
PS C:\> Add-AzureRmLogAlertRule -Name backupFailedAlert -Location "East US" -ResourceGroup RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US -OperationName Microsoft.Backup/backupVault/Backup -Status Failed -TargetResourceId /subscriptions/86eeac34-eth9a-4de3-84db-7a27d121967e/resourceGroups/RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US/providers/microsoft.backupbvtd2/BackupVault/trinadhVault -Actions $actionEmail
```

**ResourceId**: kunt u dit via krijgen Operations Logs pop zoals beschreven in de bovenstaande sectie. ResourceUri die in details pop-upvenster van een bewerking is Hallo ResourceId toobe opgegeven voor deze cmdlet.

**OperationName**: dit Hallo indeling ' Microsoft.Backup/backupvault/<EventName>' indien EventName een van de registratie, Unregister, ConfigureProtection, back-up, herstel, StopProtection, DeleteBackupData is, CreateProtectionPolicy, DeleteProtectionPolicy, UpdateProtectionPolicy

**Status**: ondersteunde waarden zijn-gestart, is geslaagd en mislukt.

**ResourceGroup**: ResourceGroup van Hallo resource waarop de bewerking wordt geactiveerd. U kunt dit verkrijgen van ResourceId waarde. De waarde tussen velden */resourceGroups/* en */providers/* in ResourceId waarde Hallo-waarde voor ResourceGroup is.

**Naam**: naam van de waarschuwingsregel Hallo.

**CustomEmail**: Hallo aangepast e-mailadres toowhich gewenste toosend waarschuwingsmeldingen opgeven

**SendToServiceOwners**: deze optie verzendt waarschuwingsmeldingen tooall beheerders en medebeheerders van Hallo-abonnement. Kan worden gebruikt in **nieuw AzureRmAlertRuleEmail** cmdlet

### <a name="limitations-on-alerts"></a>Beperkingen voor waarschuwingen
Waarschuwingen op basis van gebeurtenissen zijn ondergaan toohello volgende beperkingen:

1. Op alle virtuele machines in de back-upkluis Hallo worden waarschuwingen gegenereerd. U kunt geen aanpassen tooget waarschuwingen voor specifieke set van virtuele machines in een back-upkluis.
2. Deze functie is in Preview. [Meer informatie](../monitoring-and-diagnostics/insights-powershell-samples.md#create-metric-alerts)
3. U ontvangt waarschuwingen van de 'alerts-noreply@mail.windowsazure.com'. U kunt Hallo afzender e-mailbericht op dit moment niet wijzigen.

## <a name="next-steps"></a>Volgende stappen
* [Herstellen van virtuele machines in Azure](backup-azure-restore-vms.md)
