---
title: "aaaBack up klassieke geïmplementeerde virtuele machines in Azure tooa back-upkluis | Microsoft Docs"
description: Back-up van uw virtuele machines met deze procedures voor back-up van virtuele machine van Azure detecteren en registreren.
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: back-up van virtuele machine. back-up van virtuele machine; back-up en herstel na noodgevallen; VM-back-up
ms.assetid: c0ab5469-65fd-4af5-ae9b-f5d183f82ce8
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: 048e32d9b2bd5bdd7a125225a71a6d805bb4fbd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-azure-virtual-machines-classic-portal"></a>Back-up van virtuele machines in Azure (klassieke portal)
> [!div class="op_single_selector"]
> * [Back-up van virtuele machines tooRecovery Services-kluis](backup-azure-arm-vms.md)
> * [Back-up van virtuele machines tooBackup kluis](backup-azure-vms.md)
>
>

In dit artikel bevat Hallo-procedures voor back-ups van een klassiek geïmplementeerd Azure virtuele machine (VM) tooa Backup-kluis. Er zijn een paar taken die u tootake ten aanzien van moet voordat u kunt back-up van een virtuele machine van Azure. Als u nog niet hebt gedaan in dat geval, volledige Hallo [vereisten](backup-azure-vms-prepare.md) tooprepare uw omgeving voor back-ups van uw virtuele machines.

Zie voor meer informatie, Hallo artikelen op [plannen van uw back-upinfrastructuur VM in Azure](backup-azure-vms-introduction.md) en [virtuele Azure-machines](https://azure.microsoft.com/documentation/services/virtual-machines/).

> [!NOTE]
> Azure heeft twee implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../azure-resource-manager/resource-manager-deployment-model.md). Een back-upkluis kan alleen klassiek geïmplementeerde VM's beveiligen. U kunt geen Resource Manager geïmplementeerde VM's met een back-upkluis. Zie [Back-up van virtuele machines tooRecovery Services-kluis](backup-azure-arm-vms.md) voor meer informatie over het werken met Recovery Services-kluizen.
>
>

Back-ups van virtuele machines in Azure omvat drie belangrijke stappen:

![Drie stappen tooback van een virtuele machine van Azure IaaS](./media/backup-azure-vms/3-steps-for-backup.png)

> [!NOTE]
> Het maken van back-ups van virtuele machines is een lokaal proces. U kunt geen back-up virtuele machines in één regio tooa back-upkluis in een andere regio. Daarom moet u een back-upkluis in elke Azure-regio maken wanneer er virtuele machines die wordt een back-up.
>
> [!IMPORTANT]
> Vanaf maart 2017, kunt u niet meer gebruiken Hallo klassieke portal toocreate Backup-kluizen.
> U kunt nu uw back-up kluizen tooRecovery Services-kluizen upgraden. Zie voor meer informatie artikel Hallo [upgraden van een back-up kluis tooa Recovery Services-kluis](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft raadt u tooupgrade uw back-upkluizen tooRecovery Services-kluizen.<br/> U kunt PowerShell toocreate Backup-kluizen niet gebruiken na 15 oktober 2017. **Per 1 november 2017**:
>- Alle resterende Backup-kluizen worden automatisch bijgewerkt tooRecovery Services-kluizen.
>- U niet kunt tooaccess uw back-upgegevens in de klassieke portal Hallo. In plaats daarvan gebruik hello Azure portal tooaccess uw back-upgegevens in Recovery Services-kluizen.
>

## <a name="step-1---discover-azure-virtual-machines"></a>Stap 1: virtuele machines van Azure detecteren
een nieuw toegevoegde toohello abonnement voor virtuele machines (VM's) worden geïdentificeerd voordat u registreert, tooensure Hallo detectieproces uitvoeren. Hallo wordt een query uitgevoerd Azure voor Hallo lijst met virtuele machines in het Hallo-abonnement, samen met aanvullende informatie zoals Hallo cloudservicenaam en Hallo regio.

1. Meld u aan toohello [klassieke portal](http://manage.windowsazure.com/)
2. Klik in de lijst hello Azure-Services, op **Recovery Services** tooopen Hallo lijst met kluizen back-up en herstel van de Site.
    ![Lijst van de kluis openen](./media/backup-azure-vms/choose-vault-list.png)
3. Selecteer in de lijst van de Hallo met Backup-kluizen, Hallo kluis tooback van een virtuele machine.

    Als dit is een nieuwe kluis Hallo portal geopend toohello **Quick Start** pagina.

    ![Geregistreerde items menu openen](./media/backup-azure-vms/vault-quick-start.png)

    Als de kluis Hallo eerder is geconfigureerd, Hallo wordt geopend menu toohello meest recent hebben gebruikt.
4. Hallo kluismenu (bovenaan Hallo Hallo pagina) en klik op **geregistreerde Items**.

    ![Geregistreerde items menu openen](./media/backup-azure-vms/vault-menu.png)
5. Van Hallo **Type** selecteert u **Azure virtuele Machine**.

    ![Workload selecteren](./media/backup-azure-vms/discovery-select-workload.png)
6. Klik op **DISCOVER** Hallo Hallo pagina onderaan in.
    ![Detectieknop](./media/backup-azure-vms/discover-button-only.png)

    Hallo detectieproces kan enkele minuten duren tabelindeling van Hallo virtuele machines. Er is een melding aan de onderkant Hallo van welkomstscherm waarmee u weet dat Hallo-proces wordt uitgevoerd.

    ![VM's detecteren](./media/backup-azure-vms/discovering-vms.png)

    Hallo melding wijzigt zodra het Hallo-proces is voltooid. Als het detectieproces Hallo Hallo virtuele machines niet gevonden, controleert u eerst dat Hallo VMs bestaan. Als Hallo virtuele machines bestaat, zorg er in zijn Hallo VMs Hallo dezelfde regio bevinden als de back-upkluis Hallo. Als VMs Hallo bestaan en zijn in dezelfde regio Hallo, zorg ervoor dat Hallo VM's zijn niet reeds geregistreerde tooa back-upkluis. Als een virtuele machine toegewezen tooa back-upkluis wordt is het niet beschikbaar toobe toegewezen tooother back-upkluizen.

    ![Detectie uitgevoerd](./media/backup-azure-vms/discovery-complete.png)

    Zodra u hebt nieuwe items Hallo gedetecteerd, gaat u tooStep 2 en registreren van uw virtuele machines.

## <a name="step-2---register-azure-virtual-machines"></a>Stap 2: Register virtuele machines in Azure
Registreren van een virtuele machine van Azure tooassociate met hello Azure Backup-service. Dit is meestal een eenmalige activiteit.

1. Navigeer toohello back-upkluis in **Recovery Services** in hello Azure-portal en klik vervolgens op **geregistreerde Items**.
2. Selecteer **Azure virtuele Machine** uit de vervolgkeuzelijst Hallo.

    ![Workload selecteren](./media/backup-azure-vms/discovery-select-workload.png)
3. Klik op **REGISTREREN** Hallo Hallo pagina onderaan in.
    ![Registratieknop](./media/backup-azure-vms/register-button-only.png)
4. In Hallo **Items registreren** snelmenu, selecteer Hallo virtuele machines die u tooregister wilt. Als er twee of meer virtuele machines met Hallo dezelfde naam, gebruikt u Hallo cloud service toodistinguish ertussen.

   > [!TIP]
   > U kunt in meerdere virtuele machines tegelijkertijd registreren.
   >
   >

    Voor elke virtuele machine die u hebt geselecteerd wordt een taak gemaakt.
5. Klik op **taak weergeven** in Hallo melding toogo toohello **taken** pagina.

    ![Taak registreren](./media/backup-azure-vms/register-create-job.png)

    Hallo virtuele machine wordt ook weergegeven in de lijst met geregistreerde items, inclusief Hallo status van de bewerking voor de registratie Hallo Hallo.

    ![Status 1 registreren](./media/backup-azure-vms/register-status01.png)

    Wanneer het Hallo-bewerking is voltooid, Hallo status tooreflect Hallo gewijzigd *geregistreerd* status.

    ![Registratie van status 2](./media/backup-azure-vms/register-status02.png)

## <a name="step-3---protect-azure-virtual-machines"></a>Stap 3: Azure virtuele machines beveiligen
U kunt nu een back-up en retentie beleid voor Hallo virtuele machine instellen. Meerdere virtuele machines kunnen worden beveiligd met behulp van één actie beveiligen.

Azure Backup-kluizen gemaakt nadat mei 2015 worden geleverd met een standaardbeleid ingebouwd in Hallo kluis. Dit standaardbeleid wordt geleverd met een standaard bewaartermijn van 30 dagen en een eenmaal dagelijks back-upschema.

1. Navigeer toohello back-upkluis in **Recovery Services** in hello Azure-portal en klik vervolgens op **geregistreerde Items**.
2. Selecteer **Azure virtuele Machine** uit de vervolgkeuzelijst Hallo.

    ![Workload selecteren in de portal](./media/backup-azure-vms/select-workload.png)
3. Klik op **beveiligen** Hallo Hallo pagina onderaan in.

    Hallo **wizard Items beveiligen** wordt weergegeven. Hallo-wizard is alleen een lijst met virtuele machines die zijn geregistreerd en niet beveiligd. Hallo virtuele machines die u tooprotect wilt selecteren.

    Als er twee of meer virtuele machines met Hallo dezelfde naam, gebruikt u Hallo cloud service toodistinguish tussen Hallo virtuele machines.

   > [!TIP]
   > U kunt meerdere virtuele machines tegelijk beveiligen.
   >
   >

    ![Beveiliging op schaal configureren](./media/backup-azure-vms/protect-at-scale.png)

4. Kies een **back-upschema** tooback van Hallo virtuele machines die u hebt geselecteerd. U kunt kiezen uit een bestaande set met beleidsregels of definieer een nieuwe.

    Aan elk back-upbeleid kunnen meerdere virtuele machines zijn gekoppeld. Echter, Hallo virtuele machine kan alleen worden gekoppeld aan een beleid op elk gewenst moment in de tijd.

    ![Beveiligen met een nieuw beleid](./media/backup-azure-vms/policy-schedule.png)

   > [!NOTE]
   > Een back-upbeleid bevat een bewaarschema voor Hallo geplande back-ups. Als u een bestaande back-upbeleid selecteert, kunt u opties in de volgende stap Hallo Hallo niet wijzigen.
   >
   >

5. Kies een **bewaartermijn** tooassociate met Hallo back-ups.

    ![Beveiligen met flexibele bewaren](./media/backup-azure-vms/policy-retention.png)

    Bewaarbeleid geeft Hallo tijdsduur voor het opslaan van een back-up. U kunt verschillende Bewaarbeleidsregels op basis van wanneer Hallo back-up is gemaakt. Een back-uppunt worden dagelijks uitgevoerd (die fungeert als een operationele herstelpunt) kan bijvoorbeeld 90 dagen worden bewaard. Ter vergelijking moet een back-uppunt die is genomen op Hallo einde van elk kwartaal (voor auditdoeleinden) mogelijk toobe bewaard voor veel maanden of jaren.

    ![Er wordt een back-up van de virtuele machine gemaakt met een herstelpunt](./media/backup-azure-vms/long-term-retention.png)

    In deze voorbeeldafbeelding:

   * **Dagelijkse bewaarbeleid**: back-ups dagelijks die zijn opgeslagen voor 30 dagen.
   * **Wekelijkse bewaarbeleid**: back-ups die elke week op zondag 104 weken blijven behouden.
   * **Maandelijkse bewaarbeleid**: back-ups die op Hallo laatste zondag van elke maand worden bewaard gedurende 120 maanden.
   * **Jaarlijks bewaarbeleid**: back-ups die op Hallo van eerste zondag van elke januari 99 jaar worden bewaard.

     Een taak tooconfigure Hallo protection-beleid wordt gemaakt en koppelt Hallo virtuele machines toothat beleid voor elke virtuele machine die u hebt geselecteerd.
6. tooview hello lijst met **beveiliging configureren** taken in Hallo kluizen menu, klikt u op **taken** en selecteer **beveiliging configureren** van Hallo **bewerking**  filter.

    ![Beveiligingstaak configureren ](./media/backup-azure-vms/protect-configureprotection.png)

## <a name="initial-backup"></a>Eerste back-up
Zodra het Hallo virtuele machine is beveiligd met een beleid, wordt deze weergegeven onder Hallo **beveiligde Items** tabblad met Hallo status *beveiligd - (in behandeling van eerste back-up)*. Hallo eerste geplande back-up is standaard Hallo *eerste back-up*.

tootrigger hello eerste back-up onmiddellijk na de configuratie van beveiliging:

1. Hallo Hallo onderaan in **beveiligde Items** pagina, klikt u op **back-up nu**.

    Hello Azure Backup-service maakt een back-uptaak voor de eerste back-upbewerking Hallo.
2. Klik op Hallo **taken** tabblad tooview Hallo lijst met taken.

    ![Back-up wordt uitgevoerd](./media/backup-azure-vms/protect-inprogress.png)

> [!NOTE]
> Tijdens de back-upbewerking hello verstrekt hello Azure Backup-service een toohello opdracht Backup-extensie in elke virtuele machine tooflush alle taken schrijven en een consistente momentopname.
>
>

Wanneer Hallo eerste back-up is voltooid, status van Hallo virtuele machine in Hallo Hallo **beveiligde Items** tabblad *beveiligde*.

![Er wordt een back-up van de virtuele machine gemaakt met een herstelpunt](./media/backup-azure-vms/protect-backedupvm.png)

## <a name="viewing-backup-status-and-details"></a>Back-status en details weer te geven
Als beveiligd, het aantal virtuele machine Hallo verhoogt ook de in Hallo **Dashboard** pagina overzicht. Hallo **Dashboard** pagina bevat ook het aantal taken van de afgelopen 24 uur die waren Hallo Hallo *geslaagde*, hebben *mislukt*, en zijn *Bezig*. Op Hallo **taken** pagina, gebruikt u Hallo **Status**, **bewerking**, of **van** en **naar** toofilter menu's Hallo-taken.

![Status van de back-up in dashboardpagina](./media/backup-azure-vms/dashboard-protectedvms.png)

Waarden in Hallo dashboard worden elke 24 uur vernieuwd.

## <a name="troubleshooting-errors"></a>Het oplossen van problemen
Als u problemen tijdens het back-ups maken van uw virtuele machine, bekijkt hello [VM probleemoplossingsartikel](backup-azure-vms-troubleshoot.md) voor hulp.

## <a name="next-steps"></a>Volgende stappen
* [Uw virtuele machines beheren en controleren](backup-azure-manage-vms.md)
* [Virtuele machines herstellen](backup-azure-restore-vms.md)
