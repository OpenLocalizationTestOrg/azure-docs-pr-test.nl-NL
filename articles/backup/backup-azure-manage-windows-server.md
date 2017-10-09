---
title: aaaManage Azure recovery services-kluizen en servers | Microsoft Docs
description: Gebruik deze zelfstudie toolearn hoe toomanage Azure recovery services-kluizen en servers.
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: tysonn
ms.assetid: 4eea984b-7ed6-4600-ac60-99d2e9cb6d8a
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: markgal
ms.openlocfilehash: b4c35c86faa0828b3c63a13b85c095c0cbaba50e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-azure-recovery-services-vaults-and-servers-for-windows-machines"></a>Azure Recovery Services-kluizen en -servers controleren en beheren voor Windows-machines
> [!div class="op_single_selector"]
> * [Resource Manager](backup-azure-manage-windows-server.md)
> * [Klassiek](backup-azure-manage-windows-server-classic.md)
>
>

In dit artikel vindt u een overzicht van Hallo back-monitor en beheertaken die beschikbaar is via hello Azure portal en Hallo Microsoft Azure Backup-agent. In dit artikel wordt ervan uitgegaan dat u al een Azure-abonnement en ten minste één Recovery Services-kluis hebt gemaakt.

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]


## <a name="open-a-recovery-services-vault"></a>Een Recovery Services-kluis openen

Hallo Recovery Services-kluisdashboard ziet u Hallo details of kenmerken van een Recovery Services-kluis.

1. Meld u aan toohello [Azure Portal](https://portal.azure.com/) met behulp van uw Azure-abonnement.
2. Klik op het menu Hub Hallo **meer Services**.

    ![Lijst met Recovery Services-kluizen stap 1 openen](./media/backup-azure-manage-windows-server/open-rs-vault-list.png) <br/>

3. Wilt u tooopen een Recovery Services-kluis. Begint te typen in het dialoogvenster Hallo **Recovery Services**. Als u te typen begint, Hallo lijst gefilterd op basis van uw invoer. Klik op **Recovery Services-kluizen** toodisplay Hallo lijst met Recovery Services-kluizen in uw abonnement.

    ![Een Recovery Services-kluis maken, stap 1](./media/backup-azure-manage-windows-server/browse-to-rs-vaults-2.png) <br/>

    Hallo-lijst met Recovery Services-kluizen wordt geopend.

    ![Een Recovery Services-kluis maken, stap 1](./media/backup-azure-manage-windows-server/list-of-rs-vaults.png) <br/>

4. Selecteer uit de lijst met kluizen Hallo Hallo-naam van Hallo gewenste tooopen Recovery Services-kluis. Hallo Recovery Services-kluis dashboard blade wordt geopend.

    ![Recovery services-kluisdashboard](./media/backup-azure-manage-windows-server/rs-vault-blade.png) <br/>

    Nu u Hallo Recovery Services-kluis hebt geopend, proberen Hallo bewaking of management-taken.

## <a name="monitor-backup-jobs-and-alerts"></a>Monitor voor back-uptaken en waarschuwingen

U taken bewaken en waarschuwingen van Hallo Recovery Services-kluis dashboard, waar u zien:

* Details van de back-waarschuwingen
* Bestanden en mappen, evenals virtuele machines in Azure wordt beveiligd in cloud Hallo
* Totale opslagruimte is verbruikt in Azure
* Status van de back-uptaak

![Taken van de back-dashboard](./media/backup-azure-manage-windows-server/dashboard-tiles.png)

Te klikken op Hallo van gegevens in elk van deze tegels wordt Hallo gekoppeld blade geopend waarin u gerelateerde taken beheren.

Vanaf de bovenkant van de Hallo Hallo Dashboard:

* Instellingen geeft toegang tot beschikbare back-uptaken.
* Back-up - kunt u back-up van nieuwe bestanden en mappen (of virtuele Azure-machines) toohello Recovery Services-kluis.
* DELETE - als een recovery services-kluis niet meer wordt gebruikt, kunt u deze verwijderen toofree opslagruimte vrij. Verwijderen is alleen ingeschakeld nadat alle beveiligde servers zijn verwijderd uit de kluis Hallo.

![Taken van de back-dashboard](./media/backup-azure-manage-windows-server/dashboard-tasks.png)

## <a name="alerts-for-backups-using-azure-backup-agent"></a>Waarschuwingen voor back-ups met Azure backup-agent:
| Waarschuwingsniveau | Waarschuwingen verzonden |
| --- | --- |
| Kritieke |Back-upfouten, herstelfout |
| Waarschuwing |Back-up is voltooid met waarschuwingen (indien minder dan honderd bestanden zijn niet back-up vervaldatums toocorruption problemen en meer dan 1 miljoen bestanden zijn met succes back-up) |
| Informatief |Geen |

## <a name="manage-backup-alerts"></a>Back-up waarschuwingen beheren
Klik op Hallo **waarschuwingen voor back-up** tegel tooopen hello **waarschuwingen voor back-up** blade waarschuwingen en beheren.

![Back-waarschuwingen](./media/backup-azure-manage-windows-server/manage-backup-alerts.png)

Hallo back-up waarschuwingen tegel u ziet Hallo aantal:

* kritieke waarschuwingen niet omgezet in de afgelopen 24 uur
* waarschuwingen niet omgezet in de afgelopen 24 uur

Op elk van deze koppelingen te klikken gaat u verder toohello **waarschuwingen voor back-up** blade met een gefilterde weergave van waarschuwingen (kritieke of waarschuwingsstatus).

Hallo waarschuwingen voor back-up blade u:

* Kies Hallo relevante informatie tooinclude met waarschuwingen.

    ![Kolommen kiezen](./media/backup-azure-manage-windows-server/choose-alerts-colunms.png)
* Waarschuwingen filteren op ernst, status en beginnen of eindigen tijden.

    ![Waarschuwingen filteren](./media/backup-azure-manage-windows-server/filter-alerts.png)
* Meldingen configureren voor de ernst, frequentie en ontvangers, evenals waarschuwingen inschakelen of uitschakelen.

    ![Waarschuwingen filteren](./media/backup-azure-manage-windows-server/configure-notifications.png)

Als **Per waarschuwing** is geselecteerd als Hallo **hoogte** frequentie geen groepering of vermindering van e-mailberichten optreedt. Elke waarschuwing resulteert in 1 melding. Dit is de standaardinstelling Hallo en Hallo resolutie e ook onmiddellijk wordt verstuurd.

Als **per uur Digest** is geselecteerd als Hallo **hoogte** frequentie één e-mailbericht verzonden toohello gebruiker melden dat er nieuwe waarschuwingen gegenereerd in Hallo afgelopen uur niet opgelost. Een resolutie e-mailbericht wordt verzonden aan Hallo einde van Hallo uur.

Waarschuwingen kunnen worden verzonden voor Hallo volgende ernstniveaus:

* Kritieke
* Waarschuwing
* Informatie

Deactiveren van Hallo waarschuwing Hello **deactiveren** knop in Hallo-taakblade voor meer informatie. Wanneer u klikt op deactiveert, kunt u de opmerkingen bij de resolutie opgeven.

U Hallo kolommen kiezen gewenste tooappear als onderdeel van de waarschuwing Hallo Hello **kolommen kiezen** knop.

> [!NOTE]
> Van Hallo **instellingen** blade u back-waarschuwingen beheren door te selecteren **bewaking en rapporten > waarschuwingen en gebeurtenissen > back-waarschuwingen** en vervolgens te klikken op **Filter** of  **Meldingen configureren**.
>
>

## <a name="manage-backup-items"></a>Back-up-items beheren
Het beheren van lokale back-ups is nu beschikbaar in de beheerportal Hallo. Hallo Hallo sectie van de back-up van Hallo dashboard en **back-ups** tegel ziet u het aantal back-items Hallo beveiligd toohello kluis.

Klik op **bestandsmappen** in Hallo tegel back-Upitems.

![Tegel back-items](./media/backup-azure-manage-windows-server/backup-items-tile.png)

Hallo back-Items er wordt een blade geopend met Hallo filteren set tooFile-map waarin u zien hoe elke specifieke back-up item weergegeven.

![Back-items](./media/backup-azure-manage-windows-server/backup-item-list.png)

Als u een specifiek item in de back-up uit Hallo lijst selecteert, ziet u Hallo essentiële gegevens voor het item.

> [!NOTE]
> Van Hallo **instellingen** blade u bestanden en mappen beheren door te selecteren **beveiligde Items > back-Upitems** en selecteren **bestandsmappen** van Hallo vervolgkeuzemenu.
>
>

![Back-items uit de instellingen voor](./media/backup-azure-manage-windows-server/backup-files-and-folders.png)

## <a name="manage-backup-jobs"></a>Back-uptaken beheren
Back-uptaken voor zowel on-premises (wanneer Hallo lokale server is een back-up tooAzure) en Azure back-ups worden weergegeven in het Hallo-dashboard.

In de sectie van de back-up van dashboard Hallo Hallo ziet Hallo back-up taak tegel u het aantal taken Hallo:

* wordt uitgevoerd
* mislukt in Hallo afgelopen 24 uur.

toomanage uw back-uptaken, klikt u op Hallo **back-uptaken** tegel, die Hallo back-uptaken blade wordt geopend.

![Back-items uit de instellingen voor](./media/backup-azure-manage-windows-server/backup-jobs.png)

Wijzigen van Hallo-informatie beschikbaar is in de blade van de back-uptaken Hallo Hello **kolommen kiezen** knop bovenaan Hallo Hallo pagina.

Gebruik Hallo **Filter** knop tooselect tussen bestanden en mappen en back-up van virtuele machine van Azure.

Als u uw back-ups van bestanden en mappen niet ziet, klikt u op **Filter** knop bovenaan Hallo Hallo pagina en selecteer **bestanden en mappen** in Hallo itemtype menu.

> [!NOTE]
> Van Hallo **instellingen** blade u back-uptaken beheren door te selecteren **bewaking en rapporten > taken > back-uptaken** en selecteren **bestandsmappen** in de vervolgkeuzelijst Hallo menu.
>
>

## <a name="monitor-backup-usage"></a>Gebruik back-up controleren
In de sectie van de back-up van dashboard Hallo Hallo ziet Hallo back-up gebruik tegel u Hallo opslag in Azure verbruikt. Opslaggebruik is voorzien:

* LRS-opslaggebruik voor de cloud die is gekoppeld aan de kluis Hallo
* Cloud GRS gebruik van opslag die is gekoppeld aan het Hallo-kluis

## <a name="manage-your-production-servers"></a>Uw productieservers beheren
Klik op toomanage uw productieservers **instellingen**.

Klik onder beheren op **back-upinfrastructuur > productieservers**.

Hallo productieservers blade een lijst met alle beschikbare productieservers. Klik op een server in Hallo lijst tooopen Hallo-servergegevens.

![Beveiligde items](./media/backup-azure-manage-windows-server/production-server-list.png)


## <a name="open-hello-azure-backup-agent"></a>Open hello Azure backup-agent
Open Hallo **Microsoft Azure backup-agent** (vindt u het door te zoeken naar uw computer *Microsoft Azure Backup*).

![Een Windows Server back-up plannen](./media/backup-azure-manage-windows-server/snap-in-search.png)

Van Hallo **acties** beschikbaar op Hallo van Hallo back-upagent console u uitvoeren Hallo beheertaken te volgen:

* Server registreren
* Back-up plannen
* Nu een back-maken
* Eigenschappen wijzigen

![Microsoft Azure Backup agent console acties](./media/backup-azure-manage-windows-server/console-actions.png)

> [!NOTE]
> te**gegevens herstellen**, Zie [herstellen van bestanden tooa WindowsServer of Windows-clientcomputer](backup-azure-restore-windows-server.md).
>
>

## <a name="modify-hello-backup-schedule"></a>Back-upschema Hallo wijzigen
1. Klik in de Microsoft Azure Backup-agent Hallo **back-up plannen**.

    ![Een Windows Server back-up plannen](./media/backup-azure-manage-windows-server/schedule-backup.png)
2. In Hallo **de Wizard Back-up plannen** laat Hallo **wijzigingen aanbrengen toobackup items of tijden** optie is geselecteerd en klik op **volgende**.

    ![Een Windows Server back-up plannen](./media/backup-azure-manage-windows-server/modify-or-stop-a-scheduled-backup.png)
3. Als u wilt dat tooadd of items op Hallo wijzigen **Items selecteren tooBackup** scherm op **Items toevoegen**.

    U kunt ook instellen **Uitsluitingsinstellingen** via deze pagina in de wizard Hallo. Als u tooexclude bestanden wilt of bestandstypen Hallo procedure voor het toevoegen van lezen [uitsluitingsinstellingen](#manage-exclusion-settings).
4. Hallo-bestanden en mappen u wilt tooback omhoog en klik op selecteren **OK**.

    ![Een Windows Server back-up plannen](./media/backup-azure-manage-windows-server/add-items-modify.png)
5. Geef Hallo **back-upschema** en klik op **volgende**.

    U kunt de dag (maximaal 3 keer per dag) of een wekelijkse back-ups plannen.

    ![Items voor back-up van Windows Server](./media/backup-azure-manage-windows-server/specify-backup-schedule-modify-close.png)

   > [!NOTE]
   > Geven de back-upschema hello wordt gedetailleerd uitgelegd in dit [artikel](backup-azure-backup-cloud-as-tape.md).
   >

6. Selecteer Hallo **bewaarbeleid** voor Hallo back-up en klik op **volgende**.

    ![Items voor back-up van Windows Server](./media/backup-azure-manage-windows-server/select-retention-policy-modify.png)
7. Op Hallo **bevestiging** scherm Hallo-gegevens bekijken en op **voltooien**.
8. Zodra het Hallo-wizard is voltooid voor het maken van Hallo **back-upschema**, klikt u op **sluiten**.

    Na het wijzigen van beveiliging, kunt u bevestigen dat back-ups correct worden geactiveerd door te gaan toohello **taken** tabblad en te bevestigen dat de wijzigingen worden doorgevoerd in Hallo back-up van taken.

## <a name="enable-network-throttling"></a>Netwerkbeperking inschakelen

Hello Azure backup-agent biedt een tabblad bandbreedtebeperking waarmee u toocontrol hoe netwerkbandbreedte wordt gebruikt tijdens de gegevensoverdracht. Dit besturingselement kan nuttig zijn als u tooback van gegevens tijdens werkuren nodig maar niet dat Hallo back-upproces toointerfere met andere internetverkeer wilt. Beperken van de gegevens overdracht van toepassing is tooback up en herstelbewerkingen.  

tooenable beperken:

1. In Hallo **backup-agent**, klikt u op **eigenschappen wijzigen**.
2. Op Hallo ** tabblad beperking, selecteer **inschakelen voor gebruik van internetbandbreedte voor back-upbewerkingen**.

    ![Netwerkbeperking](./media/backup-azure-manage-windows-server/throttling-dialog.png)

    Wanneer u de beperking hebt ingeschakeld, geef Hallo bandbreedte toegestaan voor back-up van de gegevensoverdracht tijdens **werkuren** en **niet-werkuren**.

    Hallo bandbreedte waarden begint in 512 kB per seconde (Kbps) en omhoog too1023 megabytes per seconde (Mbps) kunnen gaan. U kunt ook Hallo start aanwijzen en voltooien voor **werkuren**, en welke dagen van week Hallo worden beschouwd als werk dagen. Hallo tijd buiten werkuren aangewezen Hallo is niet-werkuren toobe beschouwd.
3. Klik op **OK**.

## <a name="manage-exclusion-settings"></a>Uitsluitingsinstellingen voor beheren
1. Open Hallo **Microsoft Azure backup-agent** (u vindt deze door te zoeken naar uw computer *Microsoft Azure Backup*).

    ![Een Windows Server back-up plannen](./media/backup-azure-manage-windows-server/snap-in-search.png)
2. Klik in de Microsoft Azure Backup-agent Hallo **back-up plannen**.

    ![Een Windows Server back-up plannen](./media/backup-azure-manage-windows-server/schedule-backup.png)
3. Laat in de Wizard Back-up plannen Hallo Hallo **wijzigingen aanbrengen toobackup items of tijden** optie is geselecteerd en klik op **volgende**.

    ![Een Windows Server back-up plannen](./media/backup-azure-manage-windows-server/modify-or-stop-a-scheduled-backup.png)
4. Klik op **uitsluitingen instellingen**.

    ![Een Windows Server back-up plannen](./media/backup-azure-manage-windows-server/exclusion-settings.png)
5. Klik op **uitsluiting toevoegen**.

    ![Een Windows Server back-up plannen](./media/backup-azure-manage-windows-server/add-exclusion.png)
6. Selecteer Hallo locatie en klik vervolgens op **OK**.

    ![Een Windows Server back-up plannen](./media/backup-azure-manage-windows-server/exclusion-location.png)
7. Hallo-bestandsextensie toevoegen in Hallo **bestandstype** veld.

    ![Een Windows Server back-up plannen](./media/backup-azure-manage-windows-server/exclude-file-type.png)

    Een uitbreiding .mp3 toevoegen

    ![Een Windows Server back-up plannen](./media/backup-azure-manage-windows-server/exclude-mp3.png)

    tooadd een andere extensie, klikt u op **uitsluiting toevoegen** en voert u een ander bestandstype (extensie .jpeg toevoegen).

    ![Een Windows Server back-up plannen](./media/backup-azure-manage-windows-server/exclude-jpg.png)
8. Wanneer u alle Hallo extensies hebt toegevoegd, klikt u op **OK**.
9. Doorloopt u de Wizard Back-up plannen Hallo door te klikken op **volgende** tot Hallo **bevestigingspagina**, klikt u vervolgens op **voltooien**.

    ![Een Windows Server back-up plannen](./media/backup-azure-manage-windows-server/finish-exclusions.png)

## <a name="frequently-asked-questions"></a>Veelgestelde vragen
**W1. Hallo back-uptaak status wordt als voltooid in hello Azure backup-agent, waarom niet het ophalen van onmiddellijk weergegeven in de portal?**

A1. Er wordt op maximale vertraging van 15 minuten tussen Hallo back-uptaak status weerspiegeld in hello Azure backup-agent en hello Azure-portal.

**Q.2 als een back-uptaak is mislukt, hoe lang duurt tooraise een waarschuwing?**

A.2 een waarschuwing wordt gegenereerd binnen de 20 minuten Hallo Azure back-upfouten.

**Q3. Is er een aanvraag waarin een e-mailbericht niet verzonden als meldingen zijn geconfigureerd?**

A3. Hieronder vindt u Hallo gevallen wanneer Hallo melding wordt niet in volgorde tooreduce Hallo waarschuwing ruis verzonden:

* Als meldingen per uur zijn geconfigureerd en er een waarschuwing gegenereerd en binnen Hallo uur opgelost
* Taak is geannuleerd.
* Tweede back-uptaak is mislukt, omdat de oorspronkelijke back-uptaak wordt uitgevoerd.

## <a name="troubleshooting-monitoring-issues"></a>Het oplossen van problemen met bewaking
**Probleem:** taken en/of waarschuwingen van hello Azure backup-agent worden niet weergegeven in het Hallo-portal.

**Stappen voor probleemoplossing:** Hallo proces, ```OBRecoveryServicesManagementAgent```, verzendt Hallo taak en waarschuwing gegevens toohello Azure Backup-service. Tijd tot tijd dit proces zijn vastgelopen of afsluiten.

1. tooverify hello proces niet wordt uitgevoerd, opent u **Taakbeheer** en controleer of hello ```OBRecoveryServicesManagementAgent``` proces wordt uitgevoerd.
2. Ervan uitgaande dat Hallo proces niet wordt uitgevoerd, opent u **Configuratiescherm** en blader Hallo lijst met services. Starten of opnieuw starten **Microsoft Azure Recovery Services Management Agent**.

    Ga voor meer informatie Hallo logboeken op:<br/>
   `<AzureBackup_agent_install_folder>\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider*`Bijvoorbeeld:<br/>
   `C:\Program Files\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider0.errlog`

## <a name="next-steps"></a>Volgende stappen
* [WindowsServer of Windows-Client uit Azure herstellen](backup-azure-restore-windows-server.md)
* toolearn meer informatie over Azure Backup, Zie [overzicht van Azure-back-up](backup-introduction-to-azure-backup.md)
* Ga naar Hallo [Azure back-up-Forum](http://go.microsoft.com/fwlink/p/?LinkId=290933)
