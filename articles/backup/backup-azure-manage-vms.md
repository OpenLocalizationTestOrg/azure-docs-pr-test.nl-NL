---
title: "Resource Manager geïmplementeerde virtuele machine back-ups aaaManage | Microsoft Docs"
description: "Meer informatie over hoe toomanage en monitor Resource Manager geïmplementeerde virtuele machine back-ups"
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: f3050283-d60f-472d-b464-cb844e70d67e
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: trinadhk;markgal
ms.openlocfilehash: 241fc4b2a29c5cd8b8b0ee8efbf8ba4e96c6a7ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-virtual-machine-backups"></a>Back-ups van een virtuele Azure-machine beheren
> [!div class="op_single_selector"]
> * [Back-ups van virtuele machine in Azure beheren](backup-azure-manage-vms.md)
> * [Klassieke VM-back-ups beheren](backup-azure-manage-vms-classic.md)
>
>

Dit artikel biedt richtlijnen voor het beheren van VM-back-ups en wordt uitgelegd Hallo waarschuwingen voor back-informatie beschikbaar is in het Hallo-portaldashboard. Hallo-instructies in dit artikel is van toepassing toousing virtuele machines in een Recovery Services-kluizen. In dit artikel omvat niet Hallo maken van virtuele machines, en ook wordt uitgelegd hoe tooprotect virtuele machines. Zie voor een primer over het beveiligen van Azure Resource Manager geïmplementeerde VM's in Azure met een Recovery Services-kluis [eerste kennismaking: Maak een Back-up van virtuele machines tooa Recovery Services-kluis](backup-azure-vms-first-look-arm.md).

## <a name="manage-vaults-and-protected-virtual-machines"></a>Kluizen en beveiligde virtuele machines beheren
Hallo Recovery Services-kluisdashboard biedt in hello Azure-portal, toegang tooinformation over Hallo kluis, inclusief:

* Hallo meest recente back-upmomentopname, dat ook de meest recente herstelpunt Hallo < br\>
* back-upbeleid Hallo < br\>
* totale grootte van alle back-upmomentopnamen < br\>
* aantal virtuele machines die zijn beveiligd met de kluis Hallo < br\>

Veel beheertaken met een back-up van de virtuele machine beginnen met het Hallo-kluis openen in Hallo-dashboard. Echter, omdat kluizen gebruikte tooprotect tooview om details over een bepaalde virtuele machine, opent u meerdere items (of meerdere virtuele machines) kunnen zijn Hallo item kluisdashboard. Hallo volgende procedure laat zien u hoe tooopen hello *kluisdashboard* en ga vervolgens door toohello *kluisdashboard item*. Er zijn 'tips' in beide procedures die wijzen op hoe tooadd Hallo kluis en item toohello vault Azure-dashboard met behulp van Hallo pincode toodashboard opdracht. Pincode toodashboard is een manier voor het maken van een snelkoppeling toohello kluis of een item. Ook kunt u veelgebruikte opdrachten uitvoeren vanaf Hallo snelkoppeling.

> [!TIP]
> Als er meerdere dashboards en blades geopend, gebruikt u Hallo donker blauw schuifregelaar Hallo onderaan Hallo venster tooslide hello Azure dashboard heen en weer in.
>
>

![Volledige weergave met een schuifregelaar](./media/backup-azure-manage-vms/bottom-slider.png)

### <a name="open-a-recovery-services-vault-in-hello-dashboard"></a>Open een Recovery Services-kluis in Hallo dashboard:
1. Meld u aan toohello [Azure-portal](https://portal.azure.com/).
2. Klik op het menu Hub Hallo **Bladeren** en typt u in de lijst met resources Hallo **Recovery Services**. Als u te typen begint, Hallo lijstfilters op basis van uw invoer. Klik op **Recovery Services-kluis**.

    ![Een Recovery Services-kluis maken, stap 1](./media/backup-azure-manage-vms/browse-to-rs-vaults.png) <br/>

    Hallo-lijst met Recovery Services-kluizen worden weergegeven.

    ![Lijst met Recovery Services-kluizen ](./media/backup-azure-manage-vms/list-o-vaults.png) <br/>

   > [!TIP]
   > Als u een kluis toohello Azure Dashboard vastmaken, is deze kluis direct toegankelijk wanneer u hello Azure-portal opent. toopin een toohello kluisdashboard in Hallo kluis lijst met de rechtermuisknop op het Hallo-kluis en selecteer **pincode toodashboard**.
   >
   >
3. Selecteer uit de lijst met kluizen Hallo Hallo kluis tooopen het dashboard. Wanneer u selecteert Hallo kluis, Hallo kluisdashboard en Hallo **instellingen** blade geopend. Hallo in Hallo installatiekopie te volgen, **Contoso kluis** dashboard is gemarkeerd.

    ![Opent kluisdashboard en de blade instellingen](./media/backup-azure-manage-vms/full-view-rs-vault.png)

### <a name="open-a-vault-item-dashboard"></a>Een kluisdashboard item openen
In de vorige procedure Hallo u Hallo kluisdashboard geopend. tooopen hello item kluisdashboard:

1. In de kluisdashboard Hallo op Hallo **back-Upitems** tegel, klikt u op **Azure Virtual Machines**.

    ![Tegel back-items openen](./media/backup-azure-manage-vms/contoso-vault-1606.png)

    Hallo **back-ups** blade geeft een lijst van de laatste back-uptaak Hallo voor elk item. In dit voorbeeld is er één virtuele machine, demovm-markgal beveiligd door deze kluis.  

    ![Tegel back-items](./media/backup-azure-manage-vms/backup-items-blade.png)

   > [!TIP]
   > U kunt een kluis item toohello Azure Dashboard vastmaken voor eenvoudige toegang. een item kluis in Hallo kluis itemlijst, Hallo-item met de rechtermuisknop en selecteer toopin **pincode toodashboard**.
   >
   >
2. In Hallo **back-Upitems** blade, klik op Hallo item tooopen Hallo kluis item dashboard.

    ![Tegel back-items](./media/backup-azure-manage-vms/backup-items-blade-select-item.png)

    Hallo item kluisdashboard en de bijbehorende **instellingen** blade geopend.

    ![Dashboard van de back-ups met de blade instellingen](./media/backup-azure-manage-vms/item-dashboard-settings.png)

    Van Hallo item kluisdashboard, kunt u veel Sleutelbeheer taken, zoals uitvoeren:

   * beleidsregels wijzigen of maak een nieuwe back-upbeleid < br\>
   * herstelpunten weergeven en hun status consistentie Zie < br\>
   * op aanvraag back-up van een virtuele machine < br\>
   * Stop de beveiliging van virtuele machines < br\>
   * beveiliging van een virtuele machine hervatten < br\>
   * verwijderen van een back-upgegevens (of herstelpunt) < br\>
   * [terugzetten van back-schijven](backup-azure-arm-restore-vms.md#restore-backed-up-disks) < br\>

Voor Hallo procedures te volgen, is het Hallo beginpunt Hallo item kluisdashboard.

## <a name="manage-backup-policies"></a>Back-upbeleid beheren
1. Op Hallo [item kluisdashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), klikt u op **alle instellingen** tooopen hello **instellingen** blade.

    ![De blade back-upbeleid](./media/backup-azure-manage-vms/all-settings-button.png)
2. Op Hallo **instellingen** blade, klikt u op **back-up maken van beleid** tooopen die blade.

    Op de blade Hallo worden Hallo back-upfrequentie en bewaartermijn bereik details weergegeven.

    ![De blade back-upbeleid](./media/backup-azure-manage-vms/backup-policy-blade.png)
3. Van Hallo **back-upbeleid kiezen** menu:

   * toochange beleidsregels, selecteer een ander beleid en klik op **opslaan**. Hallo nieuwe beleid wordt onmiddellijk toegepaste toohello kluis. < br\>
   * selecteert u een beleid toocreate **nieuw**.

     ![Back-up van virtuele machine](./media/backup-azure-manage-vms/backup-policy-create-new.png)

     Zie voor instructies over het maken van een back-upbeleid [een back-upbeleid definiëren](backup-azure-manage-vms.md#defining-a-backup-policy).

[!INCLUDE [backup-create-backup-policy-for-vm](../../includes/backup-create-backup-policy-for-vm.md)]

> [!NOTE]
> Bij het beheren van back-upbeleid, zorg ervoor dat toofollow Hallo [aanbevolen procedures](backup-azure-vms-introduction.md#best-practices) voor optimale prestaties van de back-up
>
>

## <a name="on-demand-backup-of-a-virtual-machine"></a>Op aanvraag back-up van een virtuele machine
U kunt op aanvraag back-up van een virtuele machine uitvoeren zodra deze is geconfigureerd voor beveiliging. Als de eerste back-up Hallo in behandeling is, maakt back-up op aanvraag een volledige kopie van Hallo virtuele machine in Hallo die Recovery Services-kluis. Als Hallo eerste back-up is voltooid, wordt een op aanvraag back-up alleen wijzigingen verzenden vanuit Hallo eerdere momentopname, toohello Recovery Services-kluis. Dat wil zeggen, zijn volgende back-ups altijd incrementeel.

> [!NOTE]
> Hallo bewaartermijn voor een op aanvraag back-up is Hallo bewaren waarde opgegeven voor Hallo dagelijkse back-uppunt in Hallo-beleid. Als er geen dagelijkse back-uppunt is ingeschakeld, wordt de wekelijkse back-uppunt Hallo gebruikt.
>
>

tootrigger op aanvraag back-up van een virtuele machine:

* Op Hallo [item kluisdashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), klikt u op **back-up nu**.

    ![Back-up nu knop](./media/backup-azure-manage-vms/backup-now-button.png)

    Hallo portal zorgt ervoor dat u wilt dat toostart een back-uptaak op aanvraag. Klik op **Ja** toostart Hallo back-uptaak.

    ![Back-up nu knop](./media/backup-azure-manage-vms/backup-now-check.png)

    Hallo back-uptaak maakt een herstelpunt. Hallo bewaartermijn van het herstelpunt Hallo is hetzelfde als de bewaartermijn is opgegeven in het Hallo-beleid die zijn gekoppeld aan de virtuele machine Hallo Hallo. tootrack hello uitgevoerd voor Hallo-taak in het kluisdashboard hello, klikt u op Hallo **back-uptaken** tegel.  

## <a name="stop-protecting-virtual-machines"></a>Stop de beveiliging van virtuele machines
Als u toostop beveiligen van een virtuele machine kiest, wordt u gevraagd als u wilt dat tooretain Hallo-herstelpunten. Er zijn twee manieren toostop beveiligende virtuele machines:

* alle toekomstige back-uptaken stoppen en verwijderen van alle herstelpunten, of
* alle toekomstige back-uptaken stoppen, maar laat Hallo herstelpunten <br/>

Er is een kosten in verband met het verlaten van Hallo herstelpunten in de opslag. Hallo voordeel van verlaten Hallo herstelpunten is echter dat kunt u later Hallo virtuele machine herstellen indien gewenst. Zie voor informatie over kosten voor het Hallo verlaten Hallo herstelpunten Hallo [prijsinformatie](https://azure.microsoft.com/pricing/details/backup/). Als u toodelete alle herstelpunten kiest, kunt u Hallo virtuele machine niet herstellen.

de beveiliging van de toostop voor een virtuele machine:

1. Op Hallo [item kluisdashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), klikt u op **back-up stoppen**.

    ![Back-knop stoppen](./media/backup-azure-manage-vms/stop-backup-button.png)

    Hallo back-up stoppen blade wordt geopend.

    ![Back-blade stoppen](./media/backup-azure-manage-vms/stop-backup-blade.png)
2. Op Hallo **back-up stoppen** blade kiezen of tooretain of delete Hallo back-upgegevens. Hallo-informatie in biedt informatie over uw keuze.

    ![Stop de beveiliging](./media/backup-azure-manage-vms/retain-or-delete-option.png)
3. Als u back-upgegevens van tooretain Hallo hebt gekozen, gaat u verder toostep 4. Als u de back-upgegevens toodelete kiest, moet u bevestigen dat u toostop Hallo back-ups wilt en herstelpunten Hallo - Hallo-typenaam van Hallo item verwijderd.

    ![Controle stoppen](./media/backup-azure-manage-vms/item-verification-box.png)

    Als u niet zeker weet wat de itemnaam hello, Beweeg de muisaanwijzer over Hallo uitroepteken tooview Hallo naam. Hallo-naam van Hallo item is ook onder **back-up stoppen** Hallo boven aan het Hallo-blade.
4. Geef optioneel een **reden** of **Opmerking**.
5. toostop hello back-uptaak voor het huidige item hello, klikt u op ![back-knop stoppen](./media/backup-azure-manage-vms/stop-backup-button-blue.png)

    Een melding laat u weten Hallo back-uptaken zijn gestopt.

    ![Stop de beveiliging bevestigen](./media/backup-azure-manage-vms/stop-message.png)

## <a name="resume-protection-of-a-virtual-machine"></a>Beveiliging van een virtuele machine hervatten
Als hello **back-up gegevens behouden** optie hebt gekozen wanneer beveiliging voor Hallo virtuele machine is gestopt, is het mogelijk tooresume beveiliging. Als hello **back-up-gegevens verwijderen** optie hebt gekozen, en vervolgens beveiliging voor Hallo virtuele machine niet hervatten.

tooresume beveiliging voor Hallo virtuele machine

1. Op Hallo [item kluisdashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), klikt u op **back-up hervatten**.

    ![Beveiliging hervatten](./media/backup-azure-manage-vms/resume-backup-button.png)

    Hallo Backup-beleid blade wordt geopend.

   > [!NOTE]
   > Wanneer Hallo virtuele machine opnieuw te beveiligen, kunt u een ander beleid dan Hallo-beleid waarmee virtuele machine in eerste instantie is beveiligd.
   >
   >
2. Volg de stappen Hallo in [back-upbeleid beheren](backup-azure-manage-vms.md#manage-backup-policies) tooassign Hallo beleid voor Hallo virtuele machine.

    Zodra de back-upbeleid Hallo toegepaste toohello virtuele machine is, ziet u Hallo-bericht te volgen.

    ![Met succes beveiligde VM](./media/backup-azure-manage-vms/success-message.png)

## <a name="delete-backup-data"></a>Back-up van gegevens verwijderen
U kunt back-up Hallo-gegevens die zijn gekoppeld aan een virtuele machine tijdens Hallo verwijderen **back-up stoppen** taak, of telkens wanneer na Hallo back-uptaak is voltooid. Zelfs mogelijk nuttig toowait dagen of weken voordat Hallo herstelpunten worden verwijderd. In tegenstelling tot het herstellen van herstelpunten, wanneer het verwijderen van de back-upgegevens, kunt u specifieke recovery points toodelete niet kiezen. Als u ervoor toodelete uw back-upgegevens kiest, verwijdert u alle herstelpunten Hallo item is gekoppeld.

Hallo volgende procedure wordt ervan uitgegaan Hallo back-uptaak voor Hallo virtuele machine is gestopt of uitgeschakeld. Zodra het Hallo back-uptaak is uitgeschakeld, Hallo **back-up hervatten** en **back-up verwijderen** opties zijn beschikbaar in Hallo item kluisdashboard.

![Hervat en knoppen verwijderen](./media/backup-azure-manage-vms/resume-delete-buttons.png)

back-upgegevens op een virtuele machine met Hallo toodelete *back-up uitgeschakeld*:

1. Op Hallo [item kluisdashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), klikt u op **verwijderen back-up**.

    ![VM-Type](./media/backup-azure-manage-vms/delete-backup-buttom.png)

    Hallo **back-up-gegevens verwijderen** blade wordt geopend.

    ![VM-Type](./media/backup-azure-manage-vms/delete-backup-blade.png)
2. Typenaam Hallo Hallo item tooconfirm dat u wilt dat toodelete Hallo-herstelpunten.

    ![Controle stoppen](./media/backup-azure-manage-vms/item-verification-box.png)

    Als u niet zeker weet wat de itemnaam hello, Beweeg de muisaanwijzer over Hallo uitroepteken tooview Hallo naam. Hallo-naam van Hallo item is ook onder **back-up-gegevens verwijderen** Hallo boven aan het Hallo-blade.
3. Geef optioneel een **reden** of **Opmerking**.
4. toodelete hello back-gegevens voor het huidige item hello, klikt u op ![back-knop stoppen](./media/backup-azure-manage-vms/delete-button.png)

    Een melding laat u weten Hallo back-upgegevens is verwijderd.

## <a name="next-steps"></a>Volgende stappen
Bekijk voor meer informatie over het opnieuw maken van een virtuele machine vanaf een herstelpunt [Azure Virtual machines herstellen](backup-azure-restore-vms.md). Als u informatie over het beveiligen van uw virtuele machines, Zie [eerste kennismaking: Maak een Back-up van virtuele machines tooa Recovery Services-kluis](backup-azure-vms-first-look-arm.md). Zie voor informatie over de controle van gebeurtenissen, [waarschuwingen voor back-ups van virtuele machine van Azure controleren](backup-azure-monitor-vms.md).
