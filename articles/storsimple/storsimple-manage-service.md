---
title: aaaDeploy hello StorSimple Manager-service | Microsoft Docs
description: Legt uit hoe toocreate en delete StorSimple Manager-service in de klassieke Azure-portal Hallo Hallo en beschrijft hoe toomanage serviceregistratiesleutel Hallo.
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: bc1d5650-275c-42ed-bc77-cdb596f85943
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/14/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f49b647d91b03bb89ebd0e5cce196e50e3c00296
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-storsimple-manager-service-in-hello-azure-classic-portal"></a>Hallo StorSimple Manager-service in de klassieke Azure-portal Hallo implementeren

## <a name="overview"></a>Overzicht
Hallo StorSimple Manager-service wordt uitgevoerd in Microsoft Azure en verbindt toomultiple StorSimple-apparaten. Nadat u Hallo service maakt, kunt u dit toomanage Hallo apparaten Hallo Microsoft Azure classic portal wordt uitgevoerd in een browser gebruiken. Hiermee kunt u toomonitor alle Hallo-apparaten die verbonden toohello StorSimple Manager zijn-service vanaf een centrale locatie, waardoor administratieve last voor het minimaliseren.

Hallo StorSimple Manager-startpagina geeft een lijst van alle Hallo StorSimple Manager-services die u toomanage uw StorSimple-opslagapparaten gebruiken kunt. Voor elke StorSimple Manager-service Hallo volgende informatie op Hallo StorSimple Manager pagina weergegeven:

* **Naam** – Hallo-naam die is toegewezen tooyour StorSimple Manager-service wanneer deze is gemaakt. **Hallo-servicenaam kan niet worden gewijzigd nadat het Hallo-service wordt gemaakt. Dit geldt ook voor andere entiteiten, zoals apparaten, volumes, volumecontainers en back-upbeleid dat in de klassieke Azure-portal Hallo kunnen niet worden gewijzigd.**
* **Status** – status van Hallo-service kan Hallo **Active**, **maken**, of **Online**.
* **Locatie** – Hallo geografische locatie in welke Hallo StorSimple apparaat wordt geïmplementeerd.
* **Abonnement** – hello Facturering abonnement dat is gekoppeld aan uw service.

Hallo algemene taken die kunnen worden uitgevoerd via de pagina van de StorSimple Manager Hallo zijn:

* Een service maken
* Een service verwijderen
* Hallo-serviceregistratiesleutel ophalen
* Hallo-serviceregistratiesleutel genereren

Deze zelfstudie wordt beschreven hoe tooperform van deze taken.

## <a name="create-a-service"></a>Een service maken
Gebruik Hallo **snelle invoer** optie toocreate een StorSimple Manager-service als u toodeploy uw StorSimple-apparaat. toocreate een service, moet u toohave:

* Een abonnement met een Enterprise Agreement
* Een actieve Microsoft Azure storage-account
* Hallo factuurgegevens die wordt gebruikt voor toegangsbeheer

U kunt ook toogenerate storage-standaardaccount wanneer u Hallo service maakt.

Een enkele service kunt meerdere apparaten beheren. Een apparaat niet kan echter meerdere services omvatten. Een grote onderneming kan meerdere service-exemplaren toowork met verschillende abonnementen behoren, organisaties of zelfs implementatie locaties hebben. Houd er rekening mee dat u verschillende exemplaren van de StorSimple Manager service toomanage StorSimple 8000 series apparaten en virtuele StorSimple-matrices nodig.

> [!IMPORTANT] 
> Als u een niet-gebruikte service gemaakt (geen apparaat bewerkingen zijn uitgevoerd op deze resource) hebt voorafgaande tooAugust 2016, deze kan niet worden beheerd via Azure portal of de klassieke Azure-portal. U wordt aangeraden dat u een nieuwe service in hello Azure-portal maken.

Volgende stappen toocreate een service Hallo uitvoeren.

[!INCLUDE [storsimple-create-new-service](../../includes/storsimple-create-new-service.md)]

## <a name="delete-a-service"></a>Een service verwijderen
Zorg voordat u een service hebt verwijderd, dat geen verbonden apparaten wordt gebruikt. Als het Hallo-service wordt gebruikt, schakelt u Hallo verbonden apparaten. Hallo deactiveren bewerking Hallo verbinding tussen Hallo-apparaat en Hallo service-Server, maar Hallo apparaat-gegevens in de cloud Hallo behouden blijven.

> [!IMPORTANT] 
> Als een service is verwijderd, Hallo-bewerking kan niet ongedaan worden gemaakt. Elk apparaat dat werd gebruikt Hallo-service moet toobe fabrieksinstellingen voordat deze kan worden gebruikt met een andere service. In dit scenario Hallo lokale gegevens op het Hallo-apparaat, evenals Hallo-configuratie niet verloren.

Volgende stappen toodelete een service Hallo uitvoeren.

### <a name="toodelete-a-service"></a>toodelete een service
1. Op Hallo **StorSimple Manager-service** pagina desgewenst toodelete Selecteer Hallo-service.
2. Klik op **verwijderen** Hallo Hallo pagina onderaan in.
3. Klik op **Ja** in Hallo bevestigingsbericht weergegeven. Het kan enkele minuten duren voordat Hallo service toobe verwijderd.

## <a name="get-hello-service-registration-key"></a>Hallo-serviceregistratiesleutel ophalen
Nadat u een service hebt gemaakt, moet u tooregister uw StorSimple-apparaat met Hallo-service. tooregister uw eerste StorSimple-apparaat, u moet Hallo serviceregistratiesleutel. tooregister extra apparaten met een bestaande StorSimple-service, moet u zowel de registratiesleutel Hallo en Hallo service gegevensversleutelingssleutel (die is gegenereerd op Hallo eerste apparaat tijdens de registratie). Zie voor meer informatie over Hallo service gegevensversleutelingssleutel [StorSimple security](storsimple-security.md). U kunt Hallo registratiesleutel ophalen door het openen van **registratiesleutel** op Hallo **Services** pagina.

Volgende stappen tooget hello serviceregistratiesleutel Hallo uitvoeren.

[!INCLUDE [storsimple-get-service-registration-key](../../includes/storsimple-get-service-registration-key.md)]

Houd de serviceregistratiesleutel Hallo op een veilige locatie. U moet deze sleutel, evenals Hallo service gegevensversleutelingssleutel, tooregister extra apparaten met deze service. Nadat u hebt verkregen Hallo serviceregistratiesleutel, moet u tooconfigure uw apparaat via Hallo Windows PowerShell voor StorSimple-interface.

Voor meer informatie over het toouse deze sleutel, Zie registratie [stap 3: apparaat configureren en registreren Hallo via Windows PowerShell voor StorSimple](storsimple-deployment-walkthrough.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).

## <a name="regenerate-hello-service-registration-key"></a>Hallo-serviceregistratiesleutel genereren
U moet een serviceregistratiesleutel tooregenerate als u vereiste tooperform sleutel worden gedraaid of als Hallo lijst servicebeheerders is gewijzigd. Wanneer u het Hallo-sleutel opnieuw genereren, wordt Hallo nieuwe sleutel alleen gebruikt voor latere apparaten registreren. Hallo-apparaten die al zijn geregistreerd, worden hierdoor niet beïnvloed door dit proces.

Volgende stappen tooregenerate een serviceregistratiesleutel Hallo uitvoeren.

### <a name="tooregenerate-hello-service-registration-key"></a>tooregenerate hello serviceregistratiesleutel
1. Op Hallo **StorSimple Manager-service** pagina, klikt u op **registratiesleutel**.
2. In Hallo **Serviceregistratiesleutel** in het dialoogvenster, klikt u op **genereren**.
3. Hier ziet u een bevestigingsbericht. Klik op **OK** toocontinue met hello wordt opnieuw gegenereerd.
4. Een nieuwe registratiecode van de service wordt weergegeven.
5. Kopieer deze sleutel en sla het voor het registreren van nieuwe apparaten aan deze service.
6. Klik op het vinkje Hallo ![Vinkje](./media/storsimple-manage-service/HCS_CheckIcon.png) tooclose dit dialoogvenster.

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over Hallo [StorSimple-implementatieproces](storsimple-deployment-walkthrough-u2.md).
* Meer informatie over [het beheren van uw StorSimple-opslagaccount](storsimple-manage-storage-accounts.md).
* Meer informatie over het te[gebruik Hallo StorSimple Manager service tooadminister uw StorSimple-apparaat](storsimple-manager-service-administration.md).
