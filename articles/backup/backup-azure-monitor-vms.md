---
title: "Resource Manager geïmplementeerde virtuele machine back-ups aaaMonitor | Microsoft Docs"
description: "Controleer gebeurtenissen en waarschuwingen van de back-ups van Resource Manager geïmplementeerde virtuele machine. Verzenden van e-mail op basis van waarschuwingen."
services: backup
documentationcenter: dev-center-name
author: markgalioto
manager: carmonm
editor: 
ms.assetid: fed32015-2db2-44f8-b204-d89f6fd1bea2
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/21/2016
ms.author: markgal;trinadhk;giridham;
ms.openlocfilehash: bf45cbaa05621b2365c26bafa1bd8223a444c1fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-alerts-for-azure-virtual-machine-backups"></a>Waarschuwingen voor back-ups van een virtuele Azure-machine controleren
Waarschuwingen zijn reacties van Hallo-service een drempelwaarde bereikt of overschreden. Weten wanneer start problemen kan worden essentiële tookeeping bedrijfskosten omlaag. Waarschuwingen doorgaans niet plaats op een planning en het is daarom nuttig tooknow zo snel mogelijk na het optreden van waarschuwingen. Bijvoorbeeld, als een back-up of herstel de taak is mislukt, een waarschuwing binnen vijf minuten van Hallo-fout optreedt. In het kluisdashboard Hallo bevat Hallo tegel waarschuwingen voor back-up kritiek en waarschuwingsniveau gebeurtenissen. In het back-up waarschuwingsinstellingen hello, kunt u alle gebeurtenissen weergeven. Maar wat moet u doen als een waarschuwing treedt op wanneer u aan een afzonderlijke probleem werkt? Als u niet weet wanneer Hallo waarschuwing gebeurt, kan dat een kleine ongemak zijn of deze gegevens in gevaar kan brengen. toomake zorgen dat de juiste mensen Hallo zich bewust bent van een waarschuwing - wanneer zich voordoet, Hallo service toosend waarschuwingsmeldingen via e-mail configureren. Zie voor meer informatie over het instellen van e-mailmeldingen [meldingen configureren](backup-azure-monitor-vms.md#configure-notifications).

## <a name="how-do-i-find-information-about-hello-alerts"></a>Hoe vind ik informatie over waarschuwingen Hallo?
tooview informatie over het Hallo-gebeurtenis die een waarschuwing heeft veroorzaakt, moet u back-up waarschuwingen-blade Hallo openen. Er zijn twee manieren tooopen Hallo back-up waarschuwingen-blade: van waarschuwingen voor back-up-tegel in het kluisdashboard Hallo Hallo of Hallo waarschuwingen en gebeurtenissen blade.

tooopen hello back-up waarschuwingen-blade van waarschuwingen voor back-up tegel:

* Op Hallo **waarschuwingen voor back-up** tegel op het kluisdashboard hello, klikt u op **Kritiek** of **waarschuwing** tooview Hallo operationele gebeurtenissen voor die ernstniveau.

    ![Tegel back-waarschuwingen](./media/backup-azure-monitor-vms/backup-alerts-tile.png)

tooopen hello waarschuwingen voor back-up blade Hallo waarschuwingen en gebeurtenissen blade:

1. Hallo kluisdashboard, klik op **alle instellingen**. ![Knop voor alle instellingen](./media/backup-azure-monitor-vms/all-settings-button.png)
2. Op Hallo **instellingen** blade, klikt u op **waarschuwingen en gebeurtenissen**. ![Knop voor waarschuwingen en gebeurtenissen](./media/backup-azure-monitor-vms/alerts-and-events-button.png)
3. Op Hallo **waarschuwingen en gebeurtenissen** blade, klikt u op **waarschuwingen voor back-up**. ![Knop voor back-waarschuwingen](./media/backup-azure-monitor-vms/backup-alerts.png)

    Hallo **waarschuwingen voor back-up** blade wordt geopend en u geeft Hallo gefilterde waarschuwingen.

    ![Tegel back-waarschuwingen](./media/backup-azure-monitor-vms/backup-alerts-critical.png)
4. tooview gedetailleerde informatie over een bepaalde waarschuwing, in de lijst Hallo van gebeurtenissen, klikt u op de waarschuwing tooopen Hallo de **Details** blade.

    ![Gebeurtenisdetails](./media/backup-azure-monitor-vms/audit-logs-event-detail.png)

    toocustomize hello kenmerken weergegeven in de lijst hello, Zie [aanvullende gebeurtenis kenmerken weergeven](backup-azure-monitor-vms.md#view-additional-event-attributes)

## <a name="configure-notifications"></a>Meldingen configureren
 Hallo service toosend e-mailmeldingen voor waarschuwingen Hallo die gedurende een Hallo voorbij het uur of bepaalde wanneer bepaalde typen gebeurtenissen optreden, kunt u configureren.

tooset van e-mailmeldingen voor waarschuwingen

1. Klik op het Hallo waarschuwingen voor back-up menu **meldingen configureren**

    ![Back-menu van waarschuwingen](./media/backup-azure-monitor-vms/backup-alerts-menu.png)

    Hallo configureren meldingen blade wordt geopend.

    ![Blade meldingen configureren](./media/backup-azure-monitor-vms/configure-notifications.png)
2. Klik op Hallo configureren meldingen blade voor e-mailmeldingen **op**.

    Hallo ontvangers en ernst dialoogvensters hebt een ster volgende toothem omdat deze informatie vereist is. Geef ten minste één e-mailadres en selecteer ten minste één ernst.
3. In Hallo **ontvangers (E-mail)** dialoogvenster type Hallo e-mailadressen voor wie Hallo meldingen ontvangen. Gebruik de indeling Hallo: username@domainname.com. Scheid meerdere e-mailadressen met een puntkomma (;).
4. In Hallo **hoogte** gebied kiezen **Per waarschuwing** toosend melding wanneer hello opgegeven waarschuwing optreedt, of **per uur Digest** toosend een samenvatting voor Hallo afgelopen uur.
5. In Hallo **ernst** dialoogvenster, kiest u een of meer niveaus dat u wilt dat tootrigger e-mailmeldingen.
6. Klik op **Opslaan**.

   ### <a name="what-alert-types-are-available-for-azure-iaas-vm-backup"></a>Welke typen waarschuwingen zijn beschikbaar voor back-up van Azure IaaS VM?
   | Waarschuwingsniveau | Waarschuwingen verzonden |
   | --- | --- |
   | Kritieke |Back-upfouten, herstelfout |
   | Waarschuwing |Geen |
   | Informatief |Geen |

### <a name="are-there-situations-where-email-isnt-sent-even-if-notifications-are-configured"></a>Zijn er situaties waarin het e-mailbericht zelfs niet is verzonden nadat er meldingen zijn geconfigureerd?
Zijn er situaties waarin een waarschuwing niet is verzonden, hoewel Hallo meldingen juist is geconfigureerd. Volgende situaties e-mailmeldingen in Hallo worden niet tooavoid waarschuwing ruis verzonden:

* Als meldingen geconfigureerde tooHourly Digest, en er een waarschuwing gegenereerd en binnen Hallo uur is opgelost.
* Hallo-taak is geannuleerd.
* Een back-uptaak wordt geactiveerd en mislukt en een andere back-uptaak wordt uitgevoerd.
* Een geplande back-uptaak voor een VM Resource Manager-functionaliteit wordt gestart, maar Hallo VM bestaat niet meer.

## <a name="customize-your-view-of-events"></a>De weergave van gebeurtenissen aanpassen
Hallo **controlelogboeken** instelling wordt geleverd met een vooraf gedefinieerde set filters en kolommen met gegevens over operationele gebeurtenissen. U kunt Hallo weergave aanpassen zodat wanneer Hallo **gebeurtenissen** blade wordt geopend, laat zien u Hallo informatie die u wilt.

1. In Hallo [kluisdashboard](backup-azure-manage-vms.md#open-a-recovery-services-vault-in-the-dashboard), klik op Bladeren-tooand **controlelogboeken** tooopen hello **gebeurtenissen** blade.

    ![Controlelogboeken](./media/backup-azure-monitor-vms/audit-logs-1606-1.png)

    Hallo **gebeurtenissen** blade toohello operationele gebeurtenissen gefilterd voor de huidige Hallo-kluis wordt geopend.

    ![Controlefilter Logboeken](./media/backup-azure-monitor-vms/audit-logs-filter.png)

    Hallo-blade bevat Hallo lijst met kritieke, fout, waarschuwing en informatieve gebeurtenissen geregistreerd die is opgetreden in Hallo afgelopen week. Hallo tijdsspanne is een standaardwaarde ingesteld in Hallo **Filter**. Hallo **gebeurtenissen** blade ziet u ook een staafdiagram bijhouden wanneer Hallo gebeurtenissen zijn opgetreden. Als u niet toosee Hallo staafdiagram in Hallo wilt **gebeurtenissen** menu, klikt u op **verbergen grafiek** tootoggle uit Hallo-grafiek. de standaardweergave Hallo van gebeurtenissen bevat informatie voor bewerking, niveau, Status, bronnen en tijd. Zie voor informatie over het blootstellen van extra kenmerken van de gebeurtenis, Hallo sectie [uitbreiden gebeurtenisgegevens](backup-azure-monitor-vms.md#view-additional-event-attributes).
2. Voor meer informatie over een operationele gebeurtenissen, in Hallo **bewerking** kolom, klikt u op een tooopen operationele gebeurtenissen van de blade. Hallo-blade bevat gedetailleerde informatie over Hallo gebeurtenissen. Gebeurtenissen zijn gegroepeerd op hun correlatie-ID en een lijst van Hallo gebeurtenissen die in de tijdsspanne Hallo opgetreden.

    ![Details van bewerking](./media/backup-azure-monitor-vms/audit-logs-details-window.png)
3. tooview gedetailleerde informatie over een bepaalde gebeurtenis, in de lijst Hallo van gebeurtenissen, klikt u op Hallo gebeurtenis tooopen de **Details** blade.

    ![Gebeurtenisdetails](./media/backup-azure-monitor-vms/audit-logs-details-window-deep.png)

    Hallo gebeurtenisniveau informatie is minder gedetailleerd Hallo informatie opgehaald. Als u liever dat veel informatie over elke gebeurtenis te zien en tooadd wilt dat dit veel toohello toegelicht **gebeurtenissen** blade, Zie de sectie Hallo [uitbreiden gebeurtenisgegevens](backup-azure-monitor-vms.md#view-additional-event-attributes).

## <a name="customize-hello-event-filter"></a>Gebeurtenisfilter Hallo aanpassen
Gebruik Hallo **Filter** tooadjust of kies Hallo-informatie die wordt weergegeven in een bepaalde blade. toofilter hello gebeurtenisgegevens:

1. In Hallo [kluisdashboard](backup-azure-manage-vms.md#open-a-recovery-services-vault-in-the-dashboard), klik op Bladeren-tooand **controlelogboeken** tooopen hello **gebeurtenissen** blade.

    ![Controlelogboeken](./media/backup-azure-monitor-vms/audit-logs-1606-1.png)

    Hallo **gebeurtenissen** blade toohello operationele gebeurtenissen gefilterd voor de huidige Hallo-kluis wordt geopend.

    ![Controlefilter Logboeken](./media/backup-azure-monitor-vms/audit-logs-filter.png)
2. Op Hallo **gebeurtenissen** menu, klikt u op **Filter** tooopen die blade.

    ![Open de blade filteren](./media/backup-azure-monitor-vms/audit-logs-filter-button.png)
3. Op Hallo **Filter** blade Hallo aanpassen **niveau**, **tijdsspanne**, en **aanroeper** filters. Hallo zijn andere filters niet beschikbaar omdat ze zijn tooprovide Hallo actuele informatie ingesteld voor Hallo Recovery Services-kluis.

    ![Details van de audit-logboeken-query](./media/backup-azure-monitor-vms/filter-blade.png)

    U kunt opgeven dat Hallo **niveau** van gebeurtenis: kritiek, fout, waarschuwing of ter informatie. U kunt een combinatie van gebeurtenisniveaus, maar u moet ten minste één niveau geselecteerd hebben. Schakelen Hallo niveau in- of uitschakelen. Hallo **tijdsspanne** -filter kunt u toospecify Hallo tijdsduur voor het vastleggen van gebeurtenissen. Als u een aangepaste tijdsspanne gebruikt, kunt u Hallo start en eindtijd.
4. Nadat u klaar tooquery Hallo operations logboeken met uw filter bent, klikt u op **Update**. Hallo resultaten weergeven in Hallo **gebeurtenissen** blade.

    ![Details van bewerking](./media/backup-azure-monitor-vms/edited-list-of-events.png)

### <a name="view-additional-event-attributes"></a>Aanvullende gebeurtenis weergavekenmerken
Met behulp van Hallo **kolommen** knop, kunt u aanvullende gebeurtenis kenmerken tooappear in de lijst Hallo op Hallo **gebeurtenissen** blade. de standaardlijst Hallo van gebeurtenissen geeft informatie weer voor bewerking, niveau, Status, bronnen en tijd. tooenable extra kenmerken:

1. Op Hallo **gebeurtenissen** blade, klikt u op **kolommen**.

    ![Open kolommen](./media/backup-azure-monitor-vms/audi-logs-column-button.png)

    Hallo **kolommen kiezen** blade wordt geopend.

    ![Blade kolommen](./media/backup-azure-monitor-vms/columns-blade.png)
2. tooselect hello kenmerk, klikt u op Hallo selectievakje. Hallo kenmerk selectievakje in-of uitschakelen in- of uitschakelen.
3. Klik op **opnieuw** tooreset Hallo lijst van kenmerken in Hallo **gebeurtenissen** blade. Gebruik na het toevoegen of verwijderen van kenmerken in de lijst hello, **opnieuw** tooview Hallo nieuwe lijst met kenmerken van de gebeurtenis.
4. Klik op **Update** tooupdate Hallo gegevens in Hallo gebeurtenis kenmerken. Hallo volgende tabel bevat informatie over elk kenmerk.

| Kolomnaam | Beschrijving |
| --- | --- |
| Bewerking |Hallo-naam van Hallo-bewerking |
| Niveau |Hallo niveau van Hallo-bewerking waarden zijn: informatief, waarschuwing, fout of kritiek |
| Status |Beschrijvende status van Hallo-bewerking |
| Resource |URL waarmee Hallo resource; ook wel bekend als Hallo resource-ID |
| Time |Tijd, gemeten vanaf Hallo huidige tijd, wanneer Hallo gebeurtenis heeft plaatsgevonden |
| Caller |Wie of wat aangeroepen of Hallo gebeurtenis; Hallo-systeem of een gebruiker |
| tijdstempel |Hallo tijd wanneer Hallo gebeurtenis is geactiveerd |
| Resourcegroep |de gekoppelde resourcegroep Hallo |
| Resourcetype |interne resourcetype Hallo gebruikt door Resource Manager |
| Abonnements-id |Hallo abonnements-ID die is gekoppeld |
| Category |Categorie van Hallo-gebeurtenis |
| Correlatie-ID |Gemeenschappelijke op verwante gebeurtenissen |

## <a name="use-powershell-toocustomize-alerts"></a>Gebruik PowerShell toocustomize waarschuwingen
U kunt aangepaste waarschuwingsmeldingen voor Hallo taken krijgen in Hallo-portal. Deze taken, tooget definiëren op basis van PowerShell waarschuwing regels op Hallo operationele legt gebeurtenissen vast. Gebruik *PowerShell versie 1.3.0 of hoger*.

toodefine een aangepaste melding tooalert mislukte back-ups, gebruikt een opdracht zoals Hallo script volgen:

```
PS C:\> $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail contoso@microsoft.com
PS C:\> Add-AzureRmLogAlertRule -Name backupFailedAlert -Location "East US" -ResourceGroup RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US -OperationName Microsoft.RecoveryServices/recoveryServicesVault/Backup -Status Failed -TargetResourceId /subscriptions/86eeac34-eth9a-4de3-84db-7a27d121967e/resourceGroups/RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US/providers/Microsoft.RecoveryServices/vaults/trinadhVault -Actions $actionEmail
```

**ResourceId** : kunt u downloaden ResourceId Hallo controlelogboeken. Hallo ResourceId is een URL die is opgegeven in de kolom van de bron Hallo van Hallo bewerkingslogboeken.

**OperationName** : OperationName heeft Hallo indeling ' Microsoft.RecoveryServices/recoveryServicesVault/*EventName*"waar *EventName* kan:<br/>

* Registreren <br/>
* Registratie ongedaan maken <br/>
* ConfigureProtection <br/>
* Back-up <br/>
* Herstellen <br/>
* StopProtection <br/>
* DeleteBackupData <br/>
* CreateProtectionPolicy <br/>
* DeleteProtectionPolicy <br/>
* UpdateProtectionPolicy <br/>

**Status** : ondersteunde waarden zijn gestart, is voltooid of mislukt.

**ResourceGroup** : dit is Hallo resourcegroep toowhich Hallo resource behoort. U kunt toevoegen Hallo resourcegroep kolom toohello gegenereerde logboeken. Resourcegroep is een van de beschikbare soorten Hallo van informatie over de gebeurtenis.

**Naam** : naam van de waarschuwingsregel Hallo.

**CustomEmail** : Geef Hallo aangepast e-mailadres toowhich gewenste toosend een melding van waarschuwingen

**SendToServiceOwners** : deze optie verzendt waarschuwingsmeldingen tooall beheerders en medebeheerders van Hallo-abonnement. Kan worden gebruikt in **nieuw AzureRmAlertRuleEmail** cmdlet

### <a name="limitations-on-alerts"></a>Beperkingen voor waarschuwingen
Waarschuwingen op basis van gebeurtenissen zijn onderwerp toohello volgende beperkingen:

1. Waarschuwingen worden verzonden op alle virtuele machines in Hallo die Recovery Services-kluis. Hallo-waarschuwing voor een subset van virtuele machines in een Recovery Services-kluis kan niet worden aangepast.
2. Deze functie is in Preview. [Meer informatie](../monitoring-and-diagnostics/insights-powershell-samples.md#create-metric-alerts)
3. Waarschuwingen worden verzonden vanuit 'alerts-noreply@mail.windowsazure.com'. U kunt Hallo afzender e-mailbericht op dit moment niet wijzigen.

## <a name="next-steps"></a>Volgende stappen
Gebeurtenislogboeken geweldige postmortemkeuring inschakelen en ondersteuning voor back-upbewerkingen Hallo controleren. Hallo volgende bewerkingen worden geregistreerd:

* Registreren
* Registratie ongedaan maken
* Beveiliging configureren
* Back-up (zowel gepland en de back-up op aanvraag)
* Herstellen
* Stop de beveiliging
* Back-upgegevens verwijderen
* Beleid toevoegen
* Beleid verwijderen
* Bijwerken van beleid
* Taak annuleren

Voor een brede uitleg van gebeurtenissen, bewerkingen en controlelogboeken over hello Azure-services, Zie Hallo artikel [gebeurtenissen bekijken en controlelogboeken](../monitoring-and-diagnostics/insights-debugging-with-events.md).

Bekijk voor meer informatie over het opnieuw maken van een virtuele machine vanaf een herstelpunt [Azure Virtual machines herstellen](backup-azure-restore-vms.md). Als u informatie over het beveiligen van uw virtuele machines, Zie [eerste kennismaking: Maak een Back-up van virtuele machines tooa Recovery Services-kluis](backup-azure-vms-first-look-arm.md). Meer informatie over beheertaken Hallo voor VM-back-ups in Hallo artikel [beheren Azure virtuele machine back-ups](backup-azure-manage-vms.md).
