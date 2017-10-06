---
title: aaaManage Azure Backup-kluizen en servers Azure met behulp van het klassieke implementatiemodel Hallo | Microsoft Docs
description: Gebruik deze zelfstudie toolearn hoe toomanage Azure Backup-kluizen en servers.
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: tysonn
ms.assetid: f175eb12-0905-437f-91fd-eaee03ab6e81
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: markgal;
ms.openlocfilehash: 6c38b04f4a76604bfd639a9b2d58237ce44e2386
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-backup-vaults-and-servers-using-hello-classic-deployment-model"></a>Azure Backup-kluizen en servers met het klassieke implementatiemodel Hallo beheren
> [!div class="op_single_selector"]
> * [Resource Manager](backup-azure-manage-windows-server.md)
> * [Klassiek](backup-azure-manage-windows-server-classic.md)
>
>

In dit artikel vindt u een overzicht van Hallo Backup-beheertaken beschikbaar via de klassieke Azure-portal Hallo en Hallo Microsoft Azure Backup agent.

> [!IMPORTANT]
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../azure-resource-manager/resource-manager-deployment-model.md). In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel. Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.

> [!IMPORTANT]
> U kunt nu uw back-up kluizen tooRecovery Services-kluizen upgraden. Zie voor meer informatie artikel Hallo [upgraden van een back-up kluis tooa Recovery Services-kluis](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft raadt u tooupgrade uw back-upkluizen tooRecovery Services-kluizen.<br/> U kunt PowerShell toocreate Backup-kluizen niet gebruiken na 15 oktober 2017. **Per 1 november 2017**:
>- Alle resterende Backup-kluizen worden automatisch bijgewerkt tooRecovery Services-kluizen.
>- U niet kunt tooaccess uw back-upgegevens in de klassieke portal Hallo. In plaats daarvan gebruik hello Azure portal tooaccess uw back-upgegevens in Recovery Services-kluizen.
>

## <a name="management-portal-tasks"></a>Beheertaken voor de portal
1. Meld u aan toohello [beheerportal](https://manage.windowsazure.com).
2. Klik op **Recovery Services**, klikt u op Hallo-naam van back-upkluis tooview Hallo pagina snel starten.

    ![Recovery services](./media/backup-azure-manage-windows-server-classic/rs-left-nav.png)

Met de opties Hallo Hallo boven aan de pagina snel starten hello, ziet u de beschikbare beheertaken Hallo.

![Tabbladen beheren](./media/backup-azure-manage-windows-server-classic/qs-page.png)

### <a name="dashboard"></a>Dashboard
Selecteer **Dashboard** toosee Hallo gebruik overzicht voor Hallo-server. Hallo **overzicht gebruik** omvat:

* Hallo van Windows-Servers geregistreerd toocloud
* Hallo aantal virtuele machines in Azure wordt beveiligd in cloud
* Hallo totale opslag in Azure verbruikt
* Hallo-status van recente taken

Onderin Hallo Hallo Dashboard kunt u Hallo volgende taken uitvoeren:

* **Certificaten beheren** - als een certificaat is gebruikte tooregister Hallo-server en gebruik vervolgens dit tooupdate Hallo-certificaat. Als u referenties voor de kluis, gebruik geen **certificaat beheren**.
* **Verwijder** -verwijderingen Hallo huidige back-upkluis. Als u een back-upkluis niet meer wordt gebruikt, kunt u deze toofree opslagruimte vrij verwijderen. **Verwijder** is alleen ingeschakeld nadat alle geregistreerde servers zijn verwijderd uit de kluis Hallo.

![Taken van de back-dashboard](./media/backup-azure-manage-windows-server-classic/dashboard-tasks.png)

## <a name="registered-items"></a>Geregistreerde items
Selecteer **geregistreerde Items** tooview Hallo namen van Hallo-servers die zijn geregistreerd toothis kluis.

![Geregistreerde items](./media/backup-azure-manage-windows-server-classic/registered-items.png)

Hallo **Type** filter standaard tooAzure virtuele Machine. tooview hello namen van Hallo-servers die geregistreerd toothis kluis zijn, selecteer **WindowsServer** van Hallo vervolgkeuzemenu.

Hier kunt u Hallo volgende taken uitvoeren:

* **Opnieuw registreren toestaan** : wanneer deze optie is geselecteerd voor een server die u kunt Hallo **registratiewizard** in Hallo lokale Microsoft Azure Backup agent tooregister Hallo-server met Hallo back-upkluis een tweede keer . Mogelijk moet u toore uit het register vanwege fout tooan in als een server had toobe opnieuw opgebouwd of Hallo-certificaat.
* **Verwijder** -een server verwijderen van de back-upkluis Hallo. Alle Hallo opgeslagen gegevens die zijn gekoppeld aan het Hallo-server wordt onmiddellijk verwijderd.

    ![Geregistreerde items taken](./media/backup-azure-manage-windows-server-classic/registered-items-tasks.png)

## <a name="protected-items"></a>Beveiligde items
Selecteer **beveiligde Items** tooview Hallo items die back-ups zijn van Hallo-servers.

![Beveiligde items](./media/backup-azure-manage-windows-server-classic/protected-items.png)

## <a name="configure"></a>Configureren
Van Hallo **configureren** tabblad kunt u de juiste opslagoptie redundantie Hallo selecteren. Hallo best tijd tooselect Hallo redundantie opslagoptie is direct na het maken van een kluis en voordat computers geregistreerde tooit zijn.

> [!WARNING]
> Als een item geregistreerde toohello kluis is, wordt de opslagoptie redundantie Hallo is vergrendeld en kan niet worden gewijzigd.
>
>

![Configureren](./media/backup-azure-manage-windows-server-classic/configure.png)

Raadpleeg dit artikel voor meer informatie over [redundantie van gegevensopslag](../storage/common/storage-redundancy.md).

## <a name="microsoft-azure-backup-agent-tasks"></a>Microsoft Azure Backup agent-taken
### <a name="console"></a>Console
Open Hallo **Microsoft Azure backup-agent** (u vindt deze door te zoeken naar uw computer *Microsoft Azure Backup*).

![Back-upagent](./media/backup-azure-manage-windows-server-classic/snap-in-search.png)

Van Hallo **acties** beschikbaar op Hallo van Hallo back-upagent console kunt u Hallo volgende beheertaken uitvoeren:

* Server registreren
* Back-up plannen
* Nu een back-maken
* Eigenschappen wijzigen

![Console agentacties](./media/backup-azure-manage-windows-server-classic/console-actions.png)

> [!NOTE]
> te**gegevens herstellen**, Zie [herstellen van bestanden tooa WindowsServer of Windows-clientcomputer](backup-azure-restore-windows-server.md).
>
>

### <a name="modify-an-existing-backup"></a>Wijzigen van een bestaande back-up
1. Klik in de Microsoft Azure Backup-agent Hallo **back-up plannen**.

    ![Een Windows Server back-up plannen](./media/backup-azure-manage-windows-server-classic/schedule-backup.png)
2. In Hallo **de Wizard Back-up plannen** laat Hallo **wijzigingen aanbrengen toobackup items of tijden** optie is geselecteerd en klik op **volgende**.

    ![Een geplande back-up wijzigen](./media/backup-azure-manage-windows-server-classic/modify-or-stop-a-scheduled-backup.png)
3. Als u wilt dat tooadd of items op Hallo wijzigen **Items selecteren tooBackup** scherm op **Items toevoegen**.

    U kunt ook instellen **Uitsluitingsinstellingen** via deze pagina in de wizard Hallo. Als u tooexclude bestanden wilt of bestandstypen Hallo procedure voor het toevoegen van lezen [uitsluitingsinstellingen](#exclusion-settings).
4. Hallo-bestanden en mappen u wilt tooback omhoog en klik op selecteren **OK**.

    ![Items toevoegen](./media/backup-azure-manage-windows-server-classic/add-items-modify.png)
5. Geef Hallo **back-upschema** en klik op **volgende**.

    U kunt de dag (maximaal 3 keer per dag) of een wekelijkse back-ups plannen.

    ![Uw back-upschema opgeven](./media/backup-azure-manage-windows-server-classic/specify-backup-schedule-modify-close.png)

   > [!NOTE]
   > Geven de back-upschema hello wordt gedetailleerd uitgelegd in dit [artikel](backup-azure-backup-cloud-as-tape.md).
   >
   >
6. Selecteer Hallo **bewaarbeleid** voor Hallo back-up en klik op **volgende**.

    ![Selecteer uw bewaarbeleid](./media/backup-azure-manage-windows-server-classic/select-retention-policy-modify.png)
7. Op Hallo **bevestiging** scherm Hallo-gegevens bekijken en op **voltooien**.
8. Zodra het Hallo-wizard is voltooid voor het maken van Hallo **back-upschema**, klikt u op **sluiten**.

    Na het wijzigen van beveiliging, kunt u bevestigen dat back-ups correct worden geactiveerd door te gaan toohello **taken** tabblad en te bevestigen dat de wijzigingen worden doorgevoerd in Hallo back-up van taken.

### <a name="enable-network-throttling"></a>Netwerkbeperking inschakelen
Hello Azure backup-agent biedt een tabblad bandbreedtebeperking waarmee u toocontrol hoe netwerkbandbreedte wordt gebruikt tijdens de gegevensoverdracht. Dit besturingselement kan nuttig zijn als u tooback van gegevens tijdens werkuren nodig maar niet dat Hallo back-upproces toointerfere met andere internetverkeer wilt. Beperken van de gegevens overdracht van toepassing is tooback up en herstelbewerkingen.  

tooenable beperken:

1. In Hallo **backup-agent**, klikt u op **eigenschappen wijzigen**.
2. Selecteer Hallo **inschakelen voor gebruik van internetbandbreedte voor back-upbewerkingen** selectievakje.

    ![Netwerkbeperking](./media/backup-azure-manage-windows-server-classic/throttling-dialog.png)
3. Wanneer u de beperking hebt ingeschakeld, geef Hallo bandbreedte toegestaan voor back-up van de gegevensoverdracht tijdens **werkuren** en **niet-werkuren**.

    Hallo bandbreedte waarden begint in 512 kB per seconde (Kbps) en omhoog too1023 megabytes per seconde (Mbps) kunnen gaan. U kunt ook Hallo start aanwijzen en voltooien voor **werkuren**, en welke dagen van week Hallo worden beschouwd als werk dagen. Hallo tijd buiten werkuren aangewezen Hallo is niet-werkuren toobe beschouwd.
4. Klik op **OK**.

## <a name="exclusion-settings"></a>Uitsluitingsinstellingen
1. Open Hallo **Microsoft Azure backup-agent** (u vindt deze door te zoeken naar uw computer *Microsoft Azure Backup*).

    ![Open back-upagent](./media/backup-azure-manage-windows-server-classic/snap-in-search.png)
2. Klik in de Microsoft Azure Backup-agent Hallo **back-up plannen**.

    ![Een Windows Server back-up plannen](./media/backup-azure-manage-windows-server-classic/schedule-backup.png)
3. Laat in de Wizard Back-up plannen Hallo Hallo **wijzigingen aanbrengen toobackup items of tijden** optie is geselecteerd en klik op **volgende**.

    ![Een schema wijzigen](./media/backup-azure-manage-windows-server-classic/modify-or-stop-a-scheduled-backup.png)
4. Klik op **uitsluitingen instellingen**.

    ![Items selecteren tooexclude](./media/backup-azure-manage-windows-server-classic/exclusion-settings.png)
5. Klik op **uitsluiting toevoegen**.

    ![Uitsluitingen toevoegen](./media/backup-azure-manage-windows-server-classic/add-exclusion.png)
6. Selecteer Hallo locatie en klik vervolgens op **OK**.

    ![Selecteer een locatie voor uitsluiting](./media/backup-azure-manage-windows-server-classic/exclusion-location.png)
7. Hallo-bestandsextensie toevoegen in Hallo **bestandstype** veld.

    ![Door het bestandstype uitsluiten](./media/backup-azure-manage-windows-server-classic/exclude-file-type.png)

    Een uitbreiding .mp3 toevoegen

    ![Voorbeeld van een type](./media/backup-azure-manage-windows-server-classic/exclude-mp3.png)

    tooadd een andere extensie, klikt u op **uitsluiting toevoegen** en voert u een ander bestandstype (extensie .jpeg toevoegen).

    ![Voorbeeld van een ander type](./media/backup-azure-manage-windows-server-classic/exclude-jpg.png)
8. Wanneer u alle Hallo extensies hebt toegevoegd, klikt u op **OK**.
9. Doorloopt u de Wizard Back-up plannen Hallo door te klikken op **volgende** tot Hallo **bevestigingspagina**, klikt u vervolgens op **voltooien**.

    ![Uitsluiting bevestigen](./media/backup-azure-manage-windows-server-classic/finish-exclusions.png)

## <a name="next-steps"></a>Volgende stappen
* [WindowsServer of Windows-Client uit Azure herstellen](backup-azure-restore-windows-server.md)
* toolearn meer informatie over Azure Backup, Zie [overzicht van Azure-back-up](backup-introduction-to-azure-backup.md)
* Ga naar Hallo [Azure back-up-Forum](http://go.microsoft.com/fwlink/p/?LinkId=290933)
