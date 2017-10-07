---
title: aaaDeploy hello Apparaatbeheer StorSimple-service in Azure | Microsoft Docs
description: Legt uit hoe toocreate en delete Hallo Apparaatbeheer StorSimple-service in hello Azure-portal en beschrijft hoe toomanage serviceregistratiesleutel Hallo.
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/13/2017
ms.author: alkohli
ms.openlocfilehash: b84a907d6b735c8fee7bdc51f9c0074857297d2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-storsimple-device-manager-service-for-storsimple-8000-series-devices"></a>Hallo Apparaatbeheer StorSimple-service voor StorSimple 8000 series apparaten implementeren

## <a name="overview"></a>Overzicht

Hallo StorSimple-apparaat Manager-service wordt uitgevoerd in Microsoft Azure en verbindt toomultiple StorSimple-apparaten. Nadat u Hallo service maakt, kunt u deze toomanage alle Hallo-apparaten die verbonden toohello Apparaatbeheer StorSimple zijn-service vanaf een centrale locatie, waardoor administratieve last voor het minimaliseren.

Deze zelfstudie wordt Hallo stappen die nodig zijn voor Hallo maken, verwijderen, migratie van Hallo-service en het Hallo beheer van Hallo serviceregistratiesleutel beschreven. Hallo-informatie in dit artikel is van toepassing alleen tooStorSimple 8000 series op apparaten. Voor meer informatie over virtuele StorSimple-matrices gaat te[implementeren van een service Manager voor StorSimple-apparaat voor uw virtuele StorSimple-matrix](storsimple-virtual-array-manage-service.md).

## <a name="create-a-service"></a>Een service maken
toocreate een StorSimple-apparaat Manager-service, moet u toohave:

* Een abonnement met een Enterprise Agreement
* Een actieve Microsoft Azure storage-account
* Hallo factuurgegevens die wordt gebruikt voor toegangsbeheer

Alleen Hallo abonnementen met een Enterprise Agreement zijn toegestaan. Microsoft Sponsorship abonnementen die zijn toegestaan in de klassieke Azure-portal Hallo worden niet ondersteund in hello Azure-portal. Hier ziet u Hallo volgende bericht wanneer u een niet-ondersteunde abonnement:

![Abonnement is niet geldig](./media/storsimple-8000-manage-service/subscription-not-valid.jpg)

U kunt ook toogenerate storage-standaardaccount wanneer u Hallo service maakt.

Een enkele service kunt meerdere apparaten beheren. Een apparaat niet kan echter meerdere services omvatten. Een grote onderneming kan meerdere service-exemplaren toowork met verschillende abonnementen behoren, organisaties of zelfs implementatie locaties hebben. 

> [!NOTE]
> U moet afzonderlijke exemplaren van het StorSimple-apparaat Manager service toomanage StorSimple 8000 series apparaten en virtuele StorSimple-matrices.

Volgende stappen toocreate een service Hallo uitvoeren.

[!INCLUDE [storsimple-create-new-service](../../includes/storsimple-8000-create-new-service.md)]


Voor elke service StorSimple Apparaatbeheer bestaan Hallo volgende kenmerken:

* **Naam** – Hallo-naam die is toegewezen tooyour Apparaatbeheer StorSimple-service wanneer deze is gemaakt. **Hallo-servicenaam kan niet worden gewijzigd nadat het Hallo-service wordt gemaakt. Dit geldt ook voor andere entiteiten, zoals apparaten, volumes, volumecontainers en back-upbeleid dat kunnen niet worden gewijzigd in hello Azure-portal.**
* **Status** – status van Hallo-service kan Hallo **Active**, **maken**, of **Online**.
* **Locatie** – Hallo geografische locatie in welke Hallo StorSimple apparaat wordt geïmplementeerd.
* **Abonnement** – hello Facturering abonnement dat is gekoppeld aan uw service.

## <a name="move-a-service-tooazure-portal"></a>Verplaatsen van een portal tooAzure
StorSimple 8000-serie kunnen nu worden beheerd in hello Azure-portal. Als u een bestaande service toomanage hello StorSimple-apparaten hebt, wordt u aangeraden de service toohello Azure-portal te verplaatsen. Hallo klassieke Azure-portal voor Hallo StorSimple Manager-service is niet beschikbaar na 30 September 2017.

Hallo optie toomigrate toohello Azure-portal is beschikbaar in fasen. Als u een optie toomigrate tooAzure portal niet ziet, maar u wilt toomove en Hallo invloed van de migratie hebt gelezen, zoals beschreven in Hallo [overwegingen voor overgang](#considerations-for-transition), kunt u [een aanvraag indienen](https://aka.ms/ss8000-cx-signup).

### <a name="considerations-for-transition"></a>Overwegingen voor overgang

Hallo gevolgen van migratie toohello nieuwe Azure portal controleren voordat u Hallo-service verdergaat.

#### <a name="before-you-transition"></a>Voordat u overgang

* Uw apparaat wordt Update uitgevoerd 3.0 of hoger. Als het apparaat een oudere versie wordt uitgevoerd, moet u de meest recente updates Hallo installeren. Voor meer informatie gaat te[Update 4 installeren](storsimple-8000-install-update-4.md). Als een StorSimple-Cloud-apparaat (8010/8020), maakt u een nieuwe cloud-apparaat met Update 4.0. 

* Zodra u de nieuwe Azure portal is overgegaan toohello, u niet gebruiken hello Azure classic portal toomanage uw StorSimple-apparaat.

* Hallo overgang ononderbroken is en er is geen uitvaltijd voor Hallo-apparaat.

* Alle Hallo StorSimple-apparaat Managers onder Hallo opgegeven abonnement overgezet.

#### <a name="during-hello-transition"></a>Tijdens de overgang Hallo

* U kunt uw apparaat niet beheren vanuit de portal Hallo.
* Bewerkingen zoals lagen en geplande back-ups blijven toooccur.
* Wis geen oude StorSimple-apparaat Managers Hallo terwijl Hallo overgang uitgevoerd wordt.

#### <a name="after-hello-transition"></a>Na de overgang Hallo

* U kunt niet langer uw apparaten beheren vanuit de klassieke portal Hallo.

* Hallo bestaande Azure Service Management (ASM) PowerShell-cmdlets worden niet ondersteund. Hallo scripts toomanage uw apparaten via hello Azure Resource Manager bijwerken.

* Configuratie van de service en het apparaat worden bewaard. Alle volumes en back-ups zijn ook is overgegaan toohello Azure-portal.

### <a name="begin-transition"></a>Begin overgang

Volgende stappen tootransition Hallo uw service toohello Azure-portal uitvoeren.

1. Ga tooyour bestaande StorSimple Manager-service in de klassieke portal Hallo.

2. U ziet een melding dat informeert Hallo Apparaatbeheer StorSimple-service is nu beschikbaar in hello Azure-portal. Houd er rekening mee dat de service Hallo in hello Azure-portal, waarnaar wordt verwezen tooas StorSimple-apparaat Manager-service is.

    ![Migratie-melding](./media/storsimple-8000-manage-service/service-transition1.jpg)

    1. Zorg ervoor dat u de volledige Hallo-invloed van de migratie hebt bekeken.
    2. Bekijk de lijst Hallo van StorSimple-apparaat Managers die vanuit de klassieke portal Hallo zullen worden verplaatst.

3. Klik op **migreren**. Hallo overgang wordt gestart en duurt een paar minuten toocomplete.

Zodra de Hallo overgang is voltooid, kunt u uw apparaten via Hallo Apparaatbeheer StorSimple-service in hello Azure-portal kunt beheren.

In hello Azure-portal, alleen Hallo StorSimple-apparaten met Update 3.0 en hoger worden ondersteund. Hallo-apparaten met oudere versies in beperkte mate ondersteunt. Hallo tabel summrizes welke bewerkingen worden ondersteund op Hallo apparaat versios voorafgaande tooUpdate 3.0 wordt uitgevoerd zodra u hebt gemigreerd van Hallo klassieke toohello Azure-portal te volgen.

| Bewerking                                                                                                                       | Ondersteund      |
|---------------------------------------------------------------------------------------------------------------------------------|----------------|
| Een apparaat registreren                                                                                                               | Ja            |
| Instellingen voor apparaten zoals algemene-, netwerk- en beveiliging configureren                                                                | Ja            |
| Scannen, downloaden en installeren van updates                                                                                             | Ja            |
| Apparaat deactiveren                                                                                                               | Ja            |
| Apparaat verwijderen                                                                                                                   | Ja            |
| Maken, wijzigen en verwijderen van een volumecontainer                                                                                   | Nee             |
| Maken, wijzigen en verwijderen van een volume                                                                                             | Nee             |
| Maken, wijzigen en verwijderen van een back-upbeleid                                                                                      | Nee             |
| Maak een handmatige back-up                                                                                                            | Nee             |
| Maak een geplande back-up                                                                                                         | Niet van toepassing |
| Herstellen vanuit een back-upset                                                                                                        | Nee             |
| Kloon tooa apparaat met Update 3.0 en hoger <br> Hallo Bronapparaat kan voorafgaande tooUpdate voor versie 3.0 wordt uitgevoerd.                                | Ja            |
| Kloon tooa apparaat waarop eerdere versies-tooUpdate 3.0 wordt uitgevoerd                                                                          | Nee             |
| Failover als Bronapparaat <br> (van een apparaat met versie voorafgaande tooUpdate 3.0 tooa apparaat met Update 3.0 en hoger)                                                               | Ja            |
| Failover als doelapparaat <br> (apparaat tooa software versie voorafgaande tooUpdate 3.0 wordt uitgevoerd)                                                                                   | Nee             |
| Een waarschuwing wissen                                                                                                                  | Ja            |
| Back-upbeleid, back-upcatalogus, volumes, volumecontainers, bewaking grafieken, taken en waarschuwingen die zijn gemaakt in de klassieke portal weergeven | Ja            |
| In-of uitschakelen apparaatcontrollers                                                                                              | Ja            |


## <a name="delete-a-service"></a>Een service verwijderen

Zorg voordat u een service hebt verwijderd, dat geen verbonden apparaten wordt gebruikt. Als het Hallo-service wordt gebruikt, schakelt u Hallo verbonden apparaten. Hallo deactiveren bewerking Hallo verbinding tussen Hallo-apparaat en Hallo service-Server, maar Hallo apparaat-gegevens in de cloud Hallo behouden blijven.

> [!IMPORTANT]
> Als een service is verwijderd, Hallo-bewerking kan niet ongedaan worden gemaakt. Elk apparaat dat werd gebruikt Hallo-service moet toobe reset toofactory standaardwaarden voordat deze kan worden gebruikt met een andere service. In dit scenario Hallo lokale gegevens op het Hallo-apparaat, evenals Hallo-configuratie gaat verloren.

Volgende stappen toodelete een service Hallo uitvoeren.

### <a name="toodelete-a-service"></a>toodelete een service

1. Zoekactie voor Hallo-service die u wilt toodelete. Klik op **Resources** pictogram en klik vervolgens invoer Hallo juiste voorwaarden toosearch. Klik op de gewenste toodelete Hallo-service in zoekresultaten Hallo.

    ![Search-service toodelete](./media/storsimple-8000-manage-service/deletessdevman1.png)

2. Hiermee gaat u blade toohello Apparaatbeheer StorSimple-service. Klik op **Verwijderen**.

    ![Verwijderen van de service](./media/storsimple-8000-manage-service/deletessdevman2.png)

3. Klik op **Ja** in Hallo bevestigingsbericht weergegeven. Het kan enkele minuten duren voordat Hallo service toobe verwijderd.

    ![Verwijdering bevestigen](./media/storsimple-8000-manage-service/deletessdevman3.png)

## <a name="get-hello-service-registration-key"></a>Hallo-serviceregistratiesleutel ophalen

Nadat u een service hebt gemaakt, moet u tooregister uw StorSimple-apparaat met Hallo-service. tooregister uw eerste StorSimple-apparaat, u moet Hallo serviceregistratiesleutel. tooregister extra apparaten met een bestaande StorSimple-service, moet u zowel de registratiesleutel Hallo en Hallo service gegevensversleutelingssleutel (die is gegenereerd op Hallo eerste apparaat tijdens de registratie). Zie voor meer informatie over Hallo service gegevensversleutelingssleutel [StorSimple security](storsimple-8000-security.md). U kunt Hallo registratiesleutel ophalen door het openen van **sleutels** op de blade van uw StorSimple-Apparaatbeheer.

Volgende stappen tooget hello serviceregistratiesleutel Hallo uitvoeren.

[!INCLUDE [storsimple-8000-get-service-registration-key](../../includes/storsimple-8000-get-service-registration-key.md)]

Houd de serviceregistratiesleutel Hallo op een veilige locatie. U moet deze sleutel, evenals Hallo service gegevensversleutelingssleutel, tooregister extra apparaten met deze service. Nadat u hebt verkregen Hallo serviceregistratiesleutel, moet u uw apparaat via Hallo Windows PowerShell voor StorSimple-interface configureren.

Voor meer informatie over het toouse deze sleutel, Zie registratie [stap 3: apparaat configureren en registreren Hallo via Windows PowerShell voor StorSimple](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).

## <a name="regenerate-hello-service-registration-key"></a>Hallo-serviceregistratiesleutel genereren
U moet een serviceregistratiesleutel tooregenerate als u vereiste tooperform sleutel worden gedraaid of als Hallo lijst servicebeheerders is gewijzigd. Wanneer u het Hallo-sleutel opnieuw genereren, wordt Hallo nieuwe sleutel alleen gebruikt voor latere apparaten registreren. Hallo-apparaten die al zijn geregistreerd, worden hierdoor niet beïnvloed door dit proces.

Volgende stappen tooregenerate een serviceregistratiesleutel Hallo uitvoeren.

### <a name="tooregenerate-hello-service-registration-key"></a>tooregenerate hello serviceregistratiesleutel
1. In Hallo **StorSimple Apparaatbeheer** blade te gaan**Management &gt;**  **sleutels**.
    
    ![De blade Sleutels](./media/storsimple-8000-manage-service/regenregkey2.png)

2. In Hallo **sleutels** blade, klikt u op **genereren**.

    ![Klik op opnieuw genereren](./media/storsimple-8000-manage-service/regenregkey3.png)
3. In Hallo **opnieuw genereren serviceregistratiesleutel** blade revisie Hallo-actie vereist wanneer hello sleutels opnieuw worden gegenereerd. Alle Hallo latere apparaten die zijn geregistreerd bij deze service nieuwe registratiecode hello gebruiken. Klik op **genereren** tooconfirm. U wordt gewaarschuwd als Hallo opnieuw genereren voltooid is.

    ![Opnieuw genereren bevestigen](./media/storsimple-8000-manage-service/regenregkey4.png)

4. Een nieuwe registratiecode van de service wordt weergegeven.

5. Kopieer deze sleutel en sla het voor het registreren van nieuwe apparaten aan deze service.



## <a name="change-hello-service-data-encryption-key"></a>De gegevensversleutelingssleutel van Hallo service wijzigen
Sleutels voor gegevenscodering service zijn gebruikte tooencrypt vertrouwelijke gegevens van de klant, zoals opslagaccountreferenties, die worden verzonden vanuit uw StorSimple Manager service toohello StorSimple-apparaat. U moet toochange deze sleutels periodiek als uw IT-organisatie een beleid voor belangrijke draaien op Hallo opslagapparaten heeft. Hallo wijzigingsproces kan worden enigszins verschillen afhankelijk van of er is een apparaat met één of meerdere apparaten, beheerd door Hallo StorSimple Manager-service. Voor meer informatie gaat te[StorSimple-beveiliging en gegevensbescherming](storsimple-8000-security.md).

Gegevensversleutelingssleutel van veranderende Hallo-service is een proces 3-stappen:

1. Met Windows PowerShell-scripts voor Azure Resource Manager, een apparaat toochange Hallo service gegevensversleutelingssleutel autoriseren.
2. Met Windows PowerShell voor StorSimple, Hallo service encryption key gegevenswijziging initiëren.
3. Als u meer dan een StorSimple-apparaat hebt, bijwerken Hallo gegevensversleutelingssleutel van service op Hallo andere apparaten.

### <a name="step-1-use-windows-powershell-script-tooauthorize-a-device-toochange-hello-service-data-encryption-key"></a>Stap 1: Gebruik Windows PowerShell-script tooAuthorize een apparaat toochange Hallo service gegevensversleutelingssleutel
Hallo apparaatbeheerder wordt normaal gesproken aanvragen die service Hallo beheerder een apparaat toochange service gegevensversleutelingssleutels autoriseren. Hallo-servicebeheerder machtigen vervolgens toochange Hallo-Hallo apparaatsleutel.

Deze stap wordt uitgevoerd met behulp van hello Azure Resource Manager gebaseerde script. Hallo-servicebeheerder kunt selecteren van een apparaat dat in aanmerking komende toobe gemachtigd is. Hallo-apparaat is geautoriseerde toostart Hallo service gegevensversleutelingssleutel Wijzig proces. 

Voor meer informatie over het gebruik van Hallo script gaat te[autoriseren ServiceEncryptionRollover.ps1](https://github.com/anoobbacker/storsimpledevicemgmttools/blob/master/Authorize-ServiceEncryptionRollover.ps1)

#### <a name="which-devices-can-be-authorized-toochange-service-data-encryption-keys"></a>Welke apparaten kunnen worden geautoriseerd toochange service gegevensversleutelingssleutels?
Een apparaat moet voldoen aan de criteria na kan pas geautoriseerde tooinitiate service encryption key gegevenswijzigingen worden Hallo:

* Hallo-apparaat moet online toobe in aanmerking komen voor service data encryption wijziging autorisatie.
* U kunt autoriseren hello hetzelfde apparaat opnieuw na 30 minuten als Hallo sleutel wijzigen is niet geïnitieerd.
* U kunt een ander apparaat autoriseren mits Hallo wijziging is niet geïnitieerd door Hallo eerder gemachtigd apparaat. Nadat het nieuwe apparaat Hallo is verleend, kan Hallo oude apparaat Hallo wijziging niet starten.
* U kunt een apparaat kan niet machtigen terwijl Hallo rollover van de gegevensversleutelingssleutel van Hallo-service uitgevoerd wordt.
* Wanneer u enkele Hallo-apparaten die zijn geregistreerd bij service Hallo hebben deze over Hallo versleuteling terwijl andere gebruikers niet hebben, kunt u een apparaat autoriseren. 

### <a name="step-2-use-windows-powershell-for-storsimple-tooinitiate-hello-service-data-encryption-key-change"></a>Stap 2: Gebruik Windows PowerShell voor StorSimple tooinitiate Hallo service gegevens encryption key wijzigen
Deze stap wordt uitgevoerd in Hallo Windows PowerShell voor StorSimple-interface op Hallo geautoriseerd StorSimple-apparaat.

> [!NOTE]
> Er zijn geen bewerkingen kunnen worden uitgevoerd in hello Azure-portal van uw StorSimple Manager-service totdat Hallo sleutelrollover is voltooid.
> 
> 

Als u Hallo apparaat seriële console tooconnect toohello Windows PowerShell-interface gebruikt, voert u Hallo stappen te volgen.

#### <a name="tooinitiate-hello-service-data-encryption-key-change"></a>gegevensversleutelingssleutel van tooinitiate Hallo service wijzigen
1. Selecteer optie 1 toolog op met volledige toegang.
2. Typ het volgende achter de opdrachtprompt Hallo:
   
     `Invoke-HcsmServiceDataEncryptionKeyChange`
3. Nadat het Hallo-cmdlet is voltooid, ontvangt u een nieuwe versleutelingssleutel van de service-gegevens. Kopieer en sla deze sleutel voor gebruik in stap 3 van dit proces. Deze sleutel worden gebruikt tooupdate alle Hallo resterende apparaten die zijn geregistreerd met Hallo StorSimple Manager-service.
   
   > [!NOTE]
   > Dit proces moet worden gestart binnen vier uur na het autoriseren van een StorSimple-apparaat.
   > 
   > 
   
   Deze nieuwe sleutel wordt toohello service toobe gepusht tooall Hallo apparaten die zijn geregistreerd met de Hallo service verzonden. Een waarschuwing wordt vervolgens weergegeven op het servicedashboard Hallo. Hallo-service wordt alle Hallo-bewerkingen op Hallo ingeschreven apparaten uitschakelen en Hallo apparaatbeheerder moet vervolgens tooupdate Hallo service gegevensversleutelingssleutel op Hallo andere apparaten. Echter worden hello i/o's (hosts verzenden gegevens toohello cloud) niet verstoord.
   
   Als u één apparaat geregistreerd tooyour service Hallo rollover-proces is voltooid en kunt u de volgende stap Hallo overslaan. Als u meerdere apparaten geregistreerde tooyour service hebt, gaat u verder toostep 3.

### <a name="step-3-update-hello-service-data-encryption-key-on-other-storsimple-devices"></a>Stap 3: Bijwerken Hallo gegevensversleutelingssleutel van service op andere StorSimple-apparaten
Deze stappen moeten worden uitgevoerd in Windows PowerShell-interface Hallo van uw StorSimple-apparaat als er meerdere apparaten geregistreerde tooyour StorSimple Manager-service. Hallo-sleutel die u hebt verkregen in stap 2 moet de gebruikte tooupdate alle Hallo resterende StorSimple-apparaat is geregistreerd bij Hallo StorSimple Manager-service.

Hallo gegevensversleuteling voor stappen tooupdate Hallo-service op het apparaat na uitvoeren.

#### <a name="tooupdate-hello-service-data-encryption-key"></a>gegevensversleutelingssleutel van tooupdate Hallo-service
1. Windows PowerShell voor StorSimple tooconnect toohello console gebruiken. Selecteer optie 1 toolog op met volledige toegang.
2. Typ het volgende achter de opdrachtprompt Hallo:
   
    `Invoke-HcsmServiceDataEncryptionKeyChange – ServiceDataEncryptionKey`
3. Hallo-service gegevensversleutelingssleutel die u hebt verkregen in bieden [stap 2: gebruik Windows PowerShell voor StorSimple tooinitiate Hallo service encryption key gegevenswijziging](#to-initiate-the-service-data-encryption-key-change).


## <a name="next-steps"></a>Volgende stappen
* Meer informatie over Hallo [StorSimple-implementatieproces](storsimple-8000-deployment-walkthrough-u2.md).
* Meer informatie over [het beheren van uw StorSimple-opslagaccount](storsimple-8000-manage-storage-accounts.md).
* Meer informatie over het te[gebruik Hallo StorSimple Apparaatbeheer service tooadminister uw StorSimple-apparaat](storsimple-8000-manager-service-administration.md).
