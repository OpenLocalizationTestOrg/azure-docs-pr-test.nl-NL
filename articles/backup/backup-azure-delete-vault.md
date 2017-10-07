---
title: " Een Recovery Services-kluis in Azure verwijderen | Microsoft Docs "
description: Hoe vault toodelete een Azure back-up en herstelservices. Een back-upkluis kan worden aangeroepen, een Azure-cloud-kluis, of de Azure recovery-kluis. Het oplossen van problemen wanneer u een back-upkluis in de klassieke portal Hallo of Azure-portal niet verwijderen.
services: service-name
documentationcenter: dev-center-name
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 5fa08157-2612-4020-bd90-f9e3c3bc1806
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/11/2017
ms.author: markgal;trinadhk
ms.openlocfilehash: 9047f50f4b2c991fbf2454ddcad08073ec7cd975
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="delete-a-recovery-services-vault"></a>Een Recovery Services-kluis verwijderen
Hello Azure Backup-service heeft twee soorten kluizen - Hallo Backup-kluis en Hallo Recovery Services-kluis. Hallo Backup-kluis kwam eerste. Hallo Recovery Services-kluis kwam vervolgens langs toosupport Hallo uitgevouwen Resource Manager-implementaties. Vanwege Hallo kunnen uitgebreide mogelijkheden en Hallo informatie afhankelijkheden die moeten worden opgeslagen in de kluis hello, verwijderen van een back-up of Recovery Services-kluis verwarrend zijn. Dit artikel wordt uitgelegd hoe toodelete Hallo-kluizen in de klassieke portal Hallo en hello Azure-portal.  

| **Implementatietype** | **Portal** | **De kluisnaam van de** |
| --- | --- | --- |
| Klassiek |Klassiek |Back-upkluis |
| Resource Manager |Azure |Recovery Services-kluis |

> [!NOTE]
> Oplossingen die met Resource Manager zijn geïmplementeerd, kunnen niet met Backup-kluizen worden beveiligd. U kunt echter een Recovery Services-kluis gebruiken tooprotect classically geïmplementeerd servers en virtuele machines.  
>

> [!IMPORTANT]
> U kunt nu uw back-up kluizen tooRecovery Services-kluizen upgraden. Zie voor meer informatie artikel Hallo [upgraden van een back-up kluis tooa Recovery Services-kluis](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft raadt u tooupgrade uw back-upkluizen tooRecovery Services-kluizen.<br/> **15 oktober 2017**, u niet langer kunnen toouse PowerShell toocreate Backup-kluizen. <br/> **Vanaf 1 november 2017**:
>- Alle resterende Backup-kluizen worden automatisch bijgewerkt tooRecovery Services-kluizen.
>- U niet kunt tooaccess uw back-upgegevens in de klassieke portal Hallo. In plaats daarvan gebruik hello Azure portal tooaccess uw back-upgegevens in Recovery Services-kluizen.
>

In dit artikel gebruiken we de term hello, kluis, toorefer toohello generieke formulier van Hallo Backup-kluis of Recovery Services-kluis. We gebruiken de formele naam hello, Backup-kluis of Recovery Services-kluis, wanneer deze nodig toodistinguish tussen Hallo kluizen.

## <a name="deleting-a-recovery-services-vault"></a>Een Recovery Services-kluis verwijderen
Verwijderen van een Recovery Services-kluis is een proces één stap - *opgegeven Hallo kluis niet alle resources bevat*. Voordat u een Recovery Services-kluis verwijderen kunt, moet u verwijdert of alle bronnen in het Hallo-kluis. Als u een kluis die bronnen bevat toodelete probeert, krijgt u een fout zoals Hallo installatiekopie te volgen:

![Fout bij het verwijderen van de kluis](./media/backup-azure-delete-vault/vault-deletion-error.png) <br/>

Totdat u bronnen uit de kluis Hallo Hallo hebt uitgeschakeld, te klikken op **probeer** produceert Hallo dezelfde fout. Als u op dit foutbericht wordt weergegeven achtergebleven bent, klikt u op **annuleren** en gebruik Hallo volgende stappen toodelete Hallo resources in Hallo kluis.

### <a name="removing-hello-items-from-a-vault-protecting-a-vm"></a>Hallo-items verwijderen uit een kluis beveiligen van een virtuele machine
Als u al Hallo Recovery Services-kluis opent, toohello tweede stap overslaan.

1. Open hello Azure-portal en van Hallo Dashboard gewenste toodelete Hallo-kluis.

   Als u geen Hallo Recovery Services-kluis vastgemaakt toohello Dashboard op Hallo Hub-menu, klikt u op **meer Services** en typt u in de lijst met resources Hallo **Recovery Services**. Als u te typen begint, Hallo lijstfilters op basis van uw invoer. Klik op **Recovery Services-kluizen**.

   ![Een Recovery Services-kluis maken, stap 1](./media/backup-azure-delete-vault/open-recovery-services-vault.png) <br/>

   Hallo-lijst met Recovery Services-kluizen wordt weergegeven. Selecteer in Hallo lijst gewenste toodelete Hallo-kluis.

   ![Kies kluis in lijst](./media/backup-azure-work-with-vaults/choose-vault-to-delete.png)
2. In het Hallo-kluis weergeven, zoekt u naar op Hallo **Essentials** deelvenster. toodelete een kluis kan niet worden alle beveiligde items. Als er een andere waarde dan nul, onder **back-Upitems** of **back-up van beheerservers**, moet u deze items verwijderen voordat u de kluis Hallo kunt verwijderen.

    ![Bekijk Essentials-deelvenster voor beveiligde items](./media/backup-azure-delete-vault/contoso-bkpvault-settings.png)

    VM's en bestanden/mappen worden beschouwd als back-Upitems en staan in Hallo **back-Upitems** gebied van Hallo Essentials deelvenster. Een DPM-server wordt weergegeven in Hallo **back-up-beheerserver** gebied van Hallo Essentials deelvenster. **Gerepliceerde Items** horen toohello Azure Site Recovery-service.
3. items verwijderen Hallo toobegin beschermd tegen Hallo kluis, zoeken naar Hallo-items in de kluis Hallo. Klik in het kluisdashboard hello **instellingen**, en klik vervolgens op **back-up items** tooopen die blade.

    ![Kies kluis in lijst](./media/backup-azure-delete-vault/open-settings-and-backup-items.png)

    Hallo **back-Upitems** blade bevat afzonderlijke lijsten, op basis van Hallo itemtype: Azure Virtual Machines of bestandsmappen (Zie afbeelding). Hallo itemtype standaardlijst weergegeven is Azure Virtual Machines. tooview hello lijst van bestandsmappen items in de kluis hello, selecteer **bestandsmappen** uit de vervolgkeuzelijst Hallo.
4. Voordat u een item uit Hallo kluis beveiligen van een virtuele machine verwijderen kunt, moet de back-uptaak van Hallo item stoppen en verwijderen van Hallo herstelpuntgegevens. Voer de volgende stappen uit voor elk item in de kluis Hallo:

    a. Op Hallo **back-ups** blade met de rechtermuisknop op Hallo item en in het contextmenu hello, selecteert u **back-up stoppen**.

    ![back-uptaak Hallo stoppen](./media/backup-azure-delete-vault/stop-the-backup-process.png)

    Hallo back-up stoppen blade wordt geopend.

    b. Op Hallo **back-up stoppen** blade van Hallo **kiest u een optie** selecteert u **back-up-gegevens verwijderen** > Hallo-typenaam van Hallo item > en klik op **stoppen back-**.

    Hallo-typenaam van Hallo item, tooverify gewenste toodelete deze. Hallo **back-up stoppen** knop wordt geactiveerd zodra u Hallo-item controleren. Als er geen Hallo tootype Hallo naam dialoogvenster van de back-item hello, u hebt gekozen Hallo **back-upgegevens behouden** optie.

    ![Back-upgegevens verwijderen](./media/backup-azure-delete-vault/stop-backup-blade-delete-backup-data.png)

    Desgewenst kunt u een reden waarom u Hallo gegevens wilt verwijderen, en voeg opmerkingen toe te bieden. Nadat u op **back-up stoppen**, Hallo verwijderen taak toocomplete toestaan voordat u probeert toodelete Hallo kluis. tooverify die Hallo taak is voltooid, Controleer de hello Azure berichten ![verwijderen van de back-upgegevens](./media/backup-azure-delete-vault/messages.png). <br/>
    Zodra het Hallo-taak is voltooid, verschijnt een bericht waarin staat Hallo back-upproces is gestopt en de back-upgegevens Hallo voor het item, is verwijderd.

    c. Na het verwijderen van een item in de lijst hello, op Hallo **back-Upitems** menu, klikt u op **vernieuwen** toosee Hallo resterende items in de kluis Hallo.

      ![Back-upgegevens verwijderen](./media/backup-azure-delete-vault/empty-items-list.png)

      Wanneer er geen items in de lijst hello zijn, schuif toohello **Essentials** deelvenster in de blade Hallo Backup-kluis. Er mag niet een **back-up items**, **back-up van beheerservers**, of **gerepliceerde items** vermeld. Als items worden nog steeds in de kluis hello weergegeven, toostep drie terug en kies een ander item type lijst.  
5. Wanneer er geen items meer op Hallo kluis werkbalk zijn, klikt u op **verwijderen**.

    ![Back-upgegevens verwijderen](./media/backup-azure-delete-vault/delete-vault.png)
6. tooverify dat u wilt dat toodelete Hallo kluis, klikt u op **Ja**.

    Hallo-kluis is verwijderd en Hallo portal retourneert toohello **nieuw** Servicemenu.

## <a name="what-if-i-stopped-hello-backup-process-but-retained-hello-data"></a>Wat gebeurt er als ik back-upproces Hallo gestopt maar Hallo gegevens behouden?
Als u de back-upproces Hallo maar per ongeluk gestopt *bewaard* Hallo gegevens, moet u de back-upgegevens Hallo verwijderen voordat u kunt Hallo kluis verwijderen. back-upgegevens toodelete Hallo:

1. Op Hallo **back-ups** blade met de rechtermuisknop op Hallo item, en in het contextmenu Hallo klikt u op **verwijderen van de back-upgegevens**.

    ![Back-upgegevens verwijderen](./media/backup-azure-delete-vault/delete-backup-data-menu.png)

    Hallo **back-up-gegevens verwijderen** blade wordt geopend.
2. Op Hallo **back-up-gegevens verwijderen** blade, Hallo typenaam Hallo-item en klik op **verwijderen**.

    ![Back-upgegevens verwijderen](./media/backup-azure-delete-vault/delete-retained-vault.png)

    Zodra u Hallo gegevens hebt verwijderd, toostep 4c retourneren en doorgaan met het Hallo-proces.

## <a name="delete-a-vault-used-tooprotect-a-dpm-server"></a>Een kluis gebruikt tooprotect een DPM-server verwijderen
Voordat u een kluis gebruikt tooprotect een DPM-server verwijderen kunt, moet u wissen herstelpunten die zijn gemaakt en vervolgens Hef de registratie op Hallo van Hallo-kluis.

toodelete hello gegevens die zijn gekoppeld aan een beveiligingsgroep:

1. In Hallo DPM Administrator-Console, klikt u op **beveiliging** > Selecteer een beveiligingsgroep > Selecteer Hallo lid van beveiligingsgroep > en klik in het lint Hallo op **verwijderen**.

  Selecteer Hallo lid van beveiligingsgroep tooactivate hello **verwijderen** knop in het lint Hallo. In voorbeeld Hallo Hallo lid is **dummyvm9**. tooselect meerdere leden in de beveiligingsgroep Hallo Hallo Ctrl-toets ingedrukt en klikt u op Hallo leden.

    ![Back-upgegevens verwijderen](./media/backup-azure-delete-vault/az-portal-delete-protection-group.png)

    Hallo **beveiliging stoppen** dialoogvenster wordt geopend.
2. In Hallo **beveiliging stoppen** dialoogvenster Selecteer **beveiligde gegevens verwijderen**, en klik op **beveiliging stoppen**.

    ![Back-upgegevens verwijderen](./media/backup-azure-delete-vault/delete-dpm-protection-group.png)

    toodelete een kluis, u moet wissen of verwijderen, de kluis Hallo van beveiligde gegevens. Afhankelijk van Hallo aantal herstelpunten en gegevens in de beveiligingsgroep hello duurt overal in een paar seconden tooseveral minuten toodelete Hallo gegevens. Hallo **beveiliging stoppen** dialoogvenster Hallo status weergegeven wanneer het Hallo-taak is voltooid.

    ![Back-upgegevens verwijderen](./media/backup-azure-delete-vault/success-deleting-protection-group.png)
3. Herhaal deze procedure voor alle leden in alle beveiligingsgroepen.

    Verwijder alle beveiligde gegevens en bescherming groepen.
4. Na het verwijderen van alle leden uit beveiligingsgroep hello, overschakelen toohello Azure-portal. Open Hallo kluisdashboard en zorg ervoor dat er geen **back-Upitems**, **back-up van beheerservers**, of **gerepliceerde items**. Op de werkbalk kluis Hallo **verwijderen**.

    ![Back-upgegevens verwijderen](./media/backup-azure-delete-vault/delete-vault.png)

    Als er back-up management servers geregistreerd toohello kluis, kunt u Hallo kluis niet verwijderen, zelfs als er geen gegevens in Hallo kluis zijn. Als u Hallo back-up-beheerservers die zijn gekoppeld aan de kluis Hallo verwijderd, maar er servers die worden vermeld in Hallo zijn **Essentials** deelvenster Zie [zoeken Hallo back-up management servers geregistreerde toohello kluis](backup-azure-delete-vault.md#find-the-backup-management-servers-registered-to-the-vault) .
5. tooverify dat u wilt dat toodelete Hallo kluis, klikt u op **Ja**.

    Hallo-kluis is verwijderd en Hallo portal retourneert toohello **nieuw** Servicemenu.

## <a name="delete-a-vault-used-tooprotect-a-production-server"></a>Een kluis gebruikt tooprotect een productieserver verwijderen
Voordat u een kluis gebruikt tooprotect een productieserver verwijderen kunt, moet u verwijderen of de server uit de kluis Hallo Hallo registratie.

toodelete die zijn gekoppeld aan de kluis Hallo Hallo productieserver:

1. Open Hallo kluisdashboard in hello Azure-portal, en klikt u op **instellingen** > **back-upinfrastructuur** > **productieservers**.

    ![Open de blade productieservers](./media/backup-azure-delete-vault/delete-production-server.png)

    Hallo **productieservers** blade wordt geopend en een lijst met alle productieservers in Hallo kluis.

    ![lijst met productieservers](./media/backup-azure-delete-vault/list-of-production-servers.png)
2. Op Hallo **productieservers** blade met de rechtermuisknop op het Hallo-server en klik op **verwijderen**.

    ![productieserver verwijderen ](./media/backup-azure-delete-vault/delete-server-on-production-server-blade.png)

    Hallo **verwijderen** blade wordt geopend.

    ![productieserver verwijderen ](./media/backup-azure-delete-vault/delete-blade.png)
3. Op Hallo **verwijderen** blade Hallo servernaam bevestigen en klikt u op **verwijderen**. U moet correct naamserver hello, tooactivate hello **verwijderen** knop.

    Zodra de kluis Hallo zijn verwijderd, verschijnt een bericht waarin staat Hallo kluis is verwijderd. Schuif terug toohello Essentials deelvenster in het kluisdashboard Hallo na het verwijderen van alle servers in de kluis Hallo.
4. Hallo kluisdashboard, zorg ervoor dat er geen **back-Upitems**, **back-up van beheerservers**, of **gerepliceerde items**. Op de werkbalk kluis Hallo **verwijderen**.
5. tooverify dat u wilt dat toodelete Hallo kluis, klikt u op **Ja**.

    Hallo-kluis is verwijderd en Hallo portal retourneert toohello **nieuw** Servicemenu.

## <a name="delete-a-backup-vault-in-classic-portal"></a>Verwijderen van een back-upkluis in de klassieke portal
Hallo volgende instructies zijn voor het verwijderen van een back-upkluis in de klassieke portal Hallo. Voordat u Hallo Backup-kluis verwijderen kunt, u moet Hallo herstelpunten, verwijderen of een back-up items en verwijder de servers Hallo geregistreerd. Hallo zijn geregistreerde servers Hallo Windows Server, werkstation of virtuele machines die geregistreerd toohello kluis zijn.

1. Open Hallo [klassieke portal](https://manage.windowsazure.com).

2. Selecteer in lijst Hallo van back-upkluizen Hallo kluis gewenste toodelete.

    ![Back-upgegevens verwijderen](./media/backup-azure-delete-vault/classic-portal-delete-vault-open-vault.png)

    Hallo kluisdashboard wordt geopend. Aantal Windows-Servers en/of Azure virtuele machines die zijn gekoppeld aan de kluis Hallo Hallo kijken. Bekijk ook Hallo totale opslag in Azure verbruikt. Stop alle back-uptaken en alle gegevens verwijderen voordat u deze verwijdert Hallo kluis.

3. Klik op Hallo **beveiligde Items** tabblad en klik vervolgens op **beveiliging stoppen**

    ![Back-upgegevens verwijderen](./media/backup-azure-delete-vault/classic-portal-delete-vault-stop-protect.png)

    Hallo **Stop de beveiliging van uw kluis'** dialoogvenster wordt weergegeven.
4. In Hallo **Stop de beveiliging van uw kluis'** dialoogvenster selectievakje **verwijderen die zijn gekoppeld back-upgegevens** en klik op ![vinkje](./media/backup-azure-delete-vault/checkmark.png). <br/>
    U kunt eventueel Kies een reden voor het stoppen van de beveiliging en een opmerking opgeven.

    ![Back-upgegevens verwijderen](./media/backup-azure-delete-vault/classic-portal-delete-vault-verify-stop-protect.png)

    Na het verwijderen van items in de kluis Hallo Hallo wordt Hallo kluis niet leeg zijn.

    ![Back-upgegevens verwijderen](./media/backup-azure-delete-vault/classic-portal-delete-vault-post-delete-data.png)
5. In de lijst Hallo tabbladen worden weergegeven, klikt u op **geregistreerde Items**. Hallo **Type** vervolgkeuzelijst, schakelt u toochoose Hallo type van de server geregistreerd toohello kluis. Hallo-type zijn Windows Server of Azure virtuele Machine. Selecteer Hallo virtuele machine geregistreerde toohello kluis Hallo voorbeeld te volgen, en klik op **Unregister**.

    ![Back-upgegevens verwijderen](./media/backup-azure-delete-vault/classic-portal-unregister.png)

  Als u wilt dat toodelete Hallo registratie voor een Windows-Server van Hallo **Type** vervolgkeuzelijst, selecteer **Windows Server**, klikt u op ![vinkje](./media/backup-azure-delete-vault/checkmark.png) toorefresh Hallo scherm en klik vervolgens op **verwijderen**. <br/>

  ![Windows Server selecteren](./media/backup-azure-delete-vault/select-windows-server.png)

6. In de lijst Hallo tabbladen worden weergegeven, klikt u op **Dashboard** tooopen dat tabblad. Controleer of er zijn geen geregistreerde servers of virtuele machines in Azure wordt beveiligd in cloud Hallo. Controleer ook of dat er zijn geen gegevens in de opslag. Klik op **verwijderen** toodelete Hallo kluis.

    ![Back-upgegevens verwijderen](./media/backup-azure-delete-vault/classic-portal-list-of-tabs-dashboard.png)

    Hallo back-up verwijderen kluis bevestigingsscherm wordt geopend. Selecteer een optie waarom u Hallo kluis wilt verwijderen, en klikt u op ![vinkje](./media/backup-azure-delete-vault/checkmark.png). <br/>

    ![Back-upgegevens verwijderen](./media/backup-azure-delete-vault/classic-portal-delete-vault-confirmation-1.png)

    Hallo-kluis is verwijderd en u de klassieke portal dashboard toohello terug.

### <a name="find-hello-backup-management-servers-registered-toohello-vault"></a>Hallo back-up Management servers geregistreerde toohello kluis vinden
Als u meerdere servers geregistreerd tooa kluis hebt, kan moeilijk tooremember zijn ze. toosee hello servers toohello kluis geregistreerd en verwijder deze:

1. Open Hallo kluisdashboard.
2. In Hallo **Essentials** deelvenster, klikt u op **instellingen** tooopen die blade.

    ![Open de instellingenblade](./media/backup-azure-delete-vault/backup-vault-click-settings.png)
3. Op Hallo **blade instellingen**, klikt u op **back-upinfrastructuur**.
4. Op Hallo **back-upinfrastructuur** blade, klikt u op **back-up-beheerservers**. Hallo back-up-beheerservers blade wordt geopend.

    ![lijst met back-beheerservers](./media/backup-azure-delete-vault/list-of-backup-management-servers.png)
5. een server uit de lijst Hallo toodelete met de rechtermuisknop op Hallo van Hallo-server en klik vervolgens op **verwijderen**.
    Hallo **verwijderen** blade wordt geopend.
6. Op Hallo **verwijderen** blade Hallo-naam van Hallo-server. Als het een lange naam, kunt u kopieert en plakt deze uit Hallo lijst met Servers voor het beheer van back-up. Klik vervolgens op **verwijderen**.  
