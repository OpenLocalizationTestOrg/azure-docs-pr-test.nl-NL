---
title: aaaBack van Windows server of werkstation tooAzure (klassieke model) | Microsoft Docs
description: Back-up Windows servers of clients tooa back-upkluis in Azure. Ga via de basisprincipes voor het beveiligen van bestanden en mappen tooa Backup-kluis via hello Azure backup-agent.
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: back-upkluis; back-up van een WindowsServer. back-upvensters;
ms.assetid: 3b543bfd-8978-4f11-816a-0498fe14a8ba
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: c8f2a9bed1e5885f5c272c65b9282ededc05850a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-a-windows-server-or-workstation-tooazure-using-hello-classic-portal"></a>Back-up van een Windows server of werkstation tooAzure met Hallo klassieke portal
> [!div class="op_single_selector"]
> * [Klassieke portal](backup-configure-vault-classic.md)
> * [Azure Portal](backup-configure-vault.md)
>
>

In dit artikel bevat informatie over procedures Hallo toofollow tooprepare moet uw omgeving uit te voeren en back-up van een Windows server (of werkstation) tooAzure. Het omvat tevens overwegingen voor het implementeren van uw back-upoplossing. Als u geïnteresseerd bent in het Azure Backup voor Hallo eerst, begeleidt in dit artikel snel u bij Hallo proces.

Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: Resource Manager en classic. In dit artikel wordt behandeld met het klassieke implementatiemodel Hallo. Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.

## <a name="before-you-start"></a>Voordat u begint
tooback u een server of client tooAzure, moet u een Azure-account. Als u niet hebt, kunt u een [gratis account](https://azure.microsoft.com/free/) binnen een paar minuten.

## <a name="create-a-backup-vault"></a>Een back-upkluis maken
tooback van bestanden en mappen van een server of client, moet u een back-upkluis in Hallo geografische regio waar u toostore Hallo gegevens toocreate.

> [!IMPORTANT]
> Vanaf maart 2017, kunt u niet meer gebruiken Hallo klassieke portal toocreate Backup-kluizen.
>
> U kunt nu uw back-up kluizen tooRecovery Services-kluizen upgraden. Zie voor meer informatie artikel Hallo [upgraden van een back-up kluis tooa Recovery Services-kluis](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft raadt u tooupgrade uw back-upkluizen tooRecovery Services-kluizen.<br/> **15 oktober 2017**, u niet langer kunnen toouse PowerShell toocreate Backup-kluizen. <br/> **Vanaf 1 november 2017**:
>- Alle resterende Backup-kluizen worden automatisch bijgewerkt tooRecovery Services-kluizen.
>- U niet kunt tooaccess uw back-upgegevens in de klassieke portal Hallo. In plaats daarvan gebruik hello Azure portal tooaccess uw back-upgegevens in Recovery Services-kluizen.
>


## <a name="download-hello-vault-credential-file"></a>Download het kluisreferentiebestand Hallo
Hallo lokale machine moet toobe geverifieerd met een back-upkluis voordat de back-up tooAzure gegevens kunt maken. Hallo-verificatie wordt bereikt door *vault referenties*. Hallo kluisreferentiebestand is gedownload via een beveiligd kanaal vanuit de klassieke portal Hallo. Hallo privésleutel voor certificaten niet bewaard is gebleven in Hallo portal of Hallo-service.

### <a name="toodownload-hello-vault-credential-file-tooa-local-machine"></a>toodownload hello kluis referentie bestand tooa lokale computer
1. Klik in het Hallo navigatiedeelvenster links op **Recovery Services**, en selecteer vervolgens Hallo back-upkluis die u hebt gemaakt.

    ![IR voltooid](./media/backup-configure-vault-classic/rs-left-nav.png)
2. Klik op de pagina snel starten Hallo **kluisreferenties downloaden**.

   klassieke portal Hallo genereert een kluisreferentie met behulp van een combinatie van Hallo kluisnaam en Hallo huidige datum. Hallo kluisreferentiebestand wordt alleen gebruikt tijdens de registratiewerkstroom hello en verloopt na 48 uur.

   Hallo kluisreferentiebestand kan worden gedownload vanuit Hallo-portal.
3. Klik op **opslaan** toodownload Hallo kluis referentie bestand toohello map Downloads van Hallo lokale account. U kunt ook selecteren **OpslaanAls** van Hallo **opslaan** menu toospecify een locatie voor Hallo kluisreferentiebestand.

   > [!NOTE]
   > Zorg ervoor dat het kluisreferentiebestand hello wordt opgeslagen in een locatie die toegankelijk is vanaf uw computer. Als deze is opgeslagen in een blok in het bestandsshare- of -bericht, Controleer of u Hallo machtigingen tooaccess deze.
   >
   >

## <a name="download-install-and-register-hello-backup-agent"></a>Downloaden, installeren en registreren Hallo backup-agent
Nadat u de back-upkluis hello en download Hallo kluisreferentiebestand maakt, moet u een agent geïnstalleerd op elk van uw Windows-machines.

### <a name="toodownload-install-and-register-hello-agent"></a>toodownload, installeren en het Hallo-agent registreren
1. Klik op **Recovery Services**, en selecteer vervolgens Hallo back-upkluis die u tooregister met een server wilt.
2. Klik op Hallo-agent op de pagina snel starten Hallo **Agent voor Windows Server of System Center Data Protection Manager of Windows client**. Klik vervolgens op **Opslaan**.

    ![Opslaan van agent](./media/backup-configure-vault-classic/agent.png)
3. Nadat het Hallo MARSagentinstaller.exe bestand is gedownload, klikt u op **uitvoeren** (of dubbelklik op **MARSAgentInstaller.exe** van Hallo opgeslagen locatie).
4. Hallo-installatiemap en de cachemap die vereist zijn voor de agent Hallo kiezen en klik vervolgens op **volgende**. Hallo cachelocatie die u opgeeft moet minimaal 5 procent van de back-upgegevens Hallo gelijk tooat vrije ruimte.
5. U kunt blijven tooconnect toohello Internet via Hallo standaard proxy-instellingen.             Als u een proxy server tooconnect toohello Internet, op de pagina proxyconfiguratie Hallo gebruikt, selecteert u Hallo **gebruiken van aangepaste proxyinstellingen** selectievakje en voer vervolgens Hallo proxy server-gegevens. Als u een geverifieerde proxyserver gebruikt, Voer Hallo Gebruikersdetails van naam en het wachtwoord en klik vervolgens op **volgende**.
6. Klik op **installeren** toobegin Hallo agent-installatie. Hallo backup-agent installeert .NET Framework 4.5 en Windows PowerShell (als deze nog niet is geïnstalleerd) toocomplete Hallo-installatie.
7. Nadat het Hallo-agent is geïnstalleerd, klikt u op **gaan tooRegistration** toocontinue met Hallo workflow.
8. Blader op Hallo kluis identificatie pagina tooand Selecteer Hallo kluis referentie-bestand dat u eerder hebt gedownload.

    Hallo kluisreferentiebestand is geldig voor alleen 48 uur nadat deze gedownload van Hallo-portal. Als er een fout optreedt op wordt deze pagina (zoals 'kluisreferenties opgegeven bestand is verlopen), aanmelden toohello portal en download het kluisreferentiebestand Hallo opnieuw.

    Zorg ervoor dat Hallo kluisreferentiebestand is beschikbaar in een locatie die toegankelijk zijn voor het Hallo-installatieprogramma. Als u toegang-gerelateerde fouten optreden, kopieert u Hallo kluis referentie tooa tijdelijke bestandslocatie op Hallo dezelfde machine en probeer Hallo opnieuw.

    Als u een kluis referentie-fout optreedt, zoals 'kluis ongeldige referenties opgegeven', wordt Hallo-bestand is beschadigd of geen meest recente referenties die zijn gekoppeld aan de herstelservice Hallo hebben Hallo. Probeer opnieuw na het downloaden van een nieuw kluisreferentiebestand via de portal Hallo Hallo. Deze fout kan ook optreden als een gebruiker klikt op Hallo **kluisreferentie downloaden** optie meerdere keren in snel achter elkaar. In dit geval wordt is alleen Hallo laatste kluisreferentiebestand geldig.
9. Op de pagina van de instelling voor wachtwoordversleuteling hello, moet u een wachtwoordzin genereren of voorzien van een wachtwoordzin (minimaal 16 tekens). Houd er rekening mee toosave Hallo wachtwoordzin op een veilige locatie.
10. Klik op **Voltooien**. Wizard Server registreren Hallo registreren Hallo-server met back-up.

    > [!WARNING]
    > Als u kwijtraakt of Hallo wachtwoordzin vergeet, niet Hallo back-upgegevens te herstellen door Microsoft helpen. U eigenaar Hallo wachtwoordzin voor versleuteling en Microsoft heeft geen zichtbaarheid van Hallo wachtwoordzin die u gebruikt. Hallo-bestand in een veilige locatie opslaan omdat deze tijdens een herstelbewerking wordt vereist.
    >
    >

11. Nadat de versleutelingssleutel Hallo is ingesteld, laat u Hallo **Start Microsoft Azure Recovery Services Agent** selectievakje geselecteerd en klik vervolgens op **sluiten**.

## <a name="complete-hello-initial-backup"></a>De eerste back-up voltooid Hallo
Hallo eerste back-up bevat twee belangrijke taken uitvoeren:

* Maken van back-upschema Hallo
* Back-ups van bestanden en mappen voor Hallo eerst

Nadat de back-upbeleid Hallo Hallo eerste back-up is voltooid wordt gemaakt van back-uppunten die u gebruiken kunt als u toorecover Hallo gegevens nodig. back-upbeleid Hallo doet dit op basis van het Hallo-schema dat u definieert.

### <a name="tooschedule-hello-backup"></a>tooschedule hello back-up
1. Open Hallo Microsoft Azure backup-agent. (Automatisch wordt geopend als u Hallo **Start Microsoft Azure Recovery Services Agent** selectievakje is ingeschakeld wanneer u de Wizard Server registreren Hallo gesloten.) U vindt deze door te zoeken naar **Microsoft Azure Backup** op uw machine.

    ![Hello Azure backup-agent starten](./media/backup-configure-vault-classic/snap-in-search.png)
2. Klik in de back-up-agent Hallo **back-up plannen**.

    ![Een back-up van de Windows Server plannen](./media/backup-configure-vault-classic/schedule-backup-close.png)
3. Op Hallo aan de slag pagina van de Wizard Back-up plannen hello, klikt u op **volgende**.
4. Klik op Hallo Items selecteren tooBackup pagina op **Items toevoegen**.
5. Selecteer Hallo bestanden en mappen die u wilt tooback en klik vervolgens op **OK**.
6. Klik op **Volgende**.
7. Op Hallo **back-upschema specificeren** pagina, geeft u Hallo **back-upschema** en klik op **volgende**.

    U kunt dagelijkse back-ups (maximaal drie keer per dag en wekelijkse back-ups plannen.

    ![Items voor back-up van Windows Server](./media/backup-configure-vault-classic/specify-backup-schedule-close.png)

   > [!NOTE]
   > Zie voor meer informatie over hoe toospecify back-upschema Hallo Hallo artikel [met Azure Backup tooreplace uw tape-infrastructuur](backup-azure-backup-cloud-as-tape.md).
   >
   >

8. Op Hallo **retentiebeleid selecteren** pagina, selecteer Hallo **bewaarbeleid** voor Hallo back-up.

    Hallo bewaarbeleid geeft Hallo duur waarvoor Hallo back-up wordt opgeslagen. In plaats van alleen 'plat beleid' voor alle back-uppunten geven, kunt u verschillende Bewaarbeleidsregels op basis van wanneer Hallo back-up. Uw behoeften, kunt u Hallo dagelijkse, wekelijkse, maandelijkse en jaarlijkse bewaren beleid toomeet wijzigen.
9. Kies op Hallo eerste back-uptype kiezen pagina Hallo-type voor eerste back-up. Hallo-optie ingesteld laat **automatisch via netwerk Hallo** geselecteerd en klik vervolgens op **volgende**.

    U kunt back-up automatisch via netwerk hello, of u offline back-ups. Hallo rest van dit artikel beschrijft Hallo-proces voor het automatisch een back-up maken. Als u liever toodo een offline back-up, Hallo artikel lezen [Offline back-werkstroom in Azure Backup](backup-azure-backup-import-export.md) voor meer informatie.
10. Op de bevestigingspagina Hallo Hallo informatie bekijken en klik vervolgens op **voltooien**.
11. Nadat het Hallo-wizard is voltooid voor het maken van back-upschema hello, klikt u op **sluiten**.

### <a name="enable-network-throttling-optional"></a>Netwerkbeperking (optioneel) inschakelen
Hallo backup-agent biedt netwerkbeperking. Gebeurtenisbeperking bepaalt hoe de netwerkbandbreedte tijdens de gegevensoverdracht wordt gebruikt. Dit besturingselement kan nuttig zijn als u tooback van gegevens tijdens werkuren nodig maar niet dat Hallo back-upproces toointerfere met andere internetverkeer wilt. Beperking van toepassing is tooback up- en herstelbewerkingen.

**netwerkbeperking tooenable**

1. Klik in de back-up-agent Hallo **eigenschappen wijzigen**.

    ![Eigenschappen wijzigen](./media/backup-configure-vault-classic/change-properties.png)
2. Op Hallo **bandbreedtebeperking** tabblad, selecteer Hallo **inschakelen voor gebruik van internetbandbreedte voor back-upbewerkingen** selectievakje.

    ![Netwerkbeperking](./media/backup-configure-vault-classic/throttling-dialog.png)
3. Nadat u hebt ingeschakeld beperking, geef Hallo bandbreedte toegestaan voor back-up van de gegevensoverdracht tijdens **werkuren** en **niet-werkuren**.

    Hallo bandbreedte waarden begint in 512 kilobits per seconde (Kbps) en omhoog too1, 023 megabytes per seconde (MBps) kunnen gaan. U kunt ook Hallo start aanwijzen en voltooien voor **werkuren**, en welke dagen van week Hallo worden beschouwd als werkdagen. Uren buiten aangewezen werk uren worden beschouwd als niet-werk uren.
4. Klik op **OK**.

### <a name="tooback-up-now"></a>tooback u nu
1. Klik in het Hallo-Backup-agent op **nu een Back-Up maken** toocomplete Hallo eerste seeding via Hallo netwerk.

    ![Nu back-up maken van Windows Server](./media/backup-configure-vault-classic/backup-now.png)
2. Op de bevestigingspagina Hallo revisie Hallo-instellingen die de Wizard Back-Up nu Hallo tooback Hallo machine gebruikt. Klik vervolgens op **Back-up maken**.
3. Klik op **sluiten** tooclose Hallo-wizard. Als u dit doet voordat Hallo back-upproces is voltooid, blijft Hallo wizard toorun op Hallo achtergrond.

Nadat de eerste back-up Hallo is voltooid, Hallo **taak voltooid** status wordt weergegeven in Hallo back-up-console.

![IR voltooid](./media/backup-configure-vault-classic/ircomplete.png)

## <a name="next-steps"></a>Volgende stappen
* Aanmelden voor een [gratis Azure-account](https://azure.microsoft.com/free/).

Zie voor meer informatie over back-ups van virtuele machines of andere werkbelastingen:

* [Back-up van IaaS VM 's](backup-azure-vms-prepare.md)
* [Back-up van werkbelastingen tooAzure met Microsoft Azure Backup-Server](backup-azure-microsoft-azure-backup.md)
* [Back-up van werkbelastingen tooAzure met DPM](backup-azure-dpm-introduction.md)
