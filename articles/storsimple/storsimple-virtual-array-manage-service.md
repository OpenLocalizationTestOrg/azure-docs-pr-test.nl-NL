---
title: aaaDeploy StorSimple-apparaat Manager-service | Microsoft Docs
description: Legt uit hoe toocreate en delete Hallo Apparaatbeheer StorSimple-service in hello Azure-portal en beschrijft hoe toomanage serviceregistratiesleutel Hallo.
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 28499494-8c4d-4a7f-9d44-94b2b8a93c93
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/29/2016
ms.author: alkohli
ms.openlocfilehash: 9064053addc7b3dfcce08b47e81b38c2e0e1b559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-storsimple-device-manager-service-for-storsimple-virtual-array"></a>Hallo Apparaatbeheer StorSimple-service voor virtuele StorSimple-matrix implementeren
## <a name="overview"></a>Overzicht

Hallo StorSimple-apparaat Manager-service wordt uitgevoerd in Microsoft Azure en verbindt toomultiple StorSimple-apparaten. Nadat u Hallo service maakt, kunt u dit toomanage Hallo apparaten Hallo Microsoft Azure portal wordt uitgevoerd in een browser gebruiken. Hiermee kunt u toomonitor alle Hallo-apparaten die verbonden toohello Apparaatbeheer StorSimple zijn-service vanaf een centrale locatie, waardoor administratieve last voor het minimaliseren.

Hallo algemene taken gerelateerde tooa StorSimple-apparaat Manager-service zijn:

* Een service maken
* Een service verwijderen
* Hallo-serviceregistratiesleutel ophalen
* Hallo-serviceregistratiesleutel genereren

Deze zelfstudie wordt beschreven hoe tooperform van Hallo voorgaande taken. Hallo informatie in dit artikel is van toepassing alleen tooStorSimple virtuele matrices. Voor meer informatie over StorSimple 8000-serie gaat te[een StorSimple Manager-service implementeren](storsimple-manage-service.md).

## <a name="create-a-service"></a>Een service maken

toocreate een service, moet u toohave:

* Een abonnement met een Enterprise Agreement
* Een actieve Microsoft Azure storage-account
* Hallo factuurgegevens die wordt gebruikt voor toegangsbeheer

U kunt ook toogenerate een opslagaccount wanneer u Hallo service maakt.

Een enkele service kunt meerdere apparaten beheren. Een apparaat niet kan echter meerdere services omvatten. Een grote onderneming kan meerdere service-exemplaren toowork met verschillende abonnementen behoren, organisaties of zelfs implementatie locaties hebben.

> [!NOTE]
> U moet afzonderlijke exemplaren van het StorSimple-apparaat Manager service toomanage StorSimple 8000 series apparaten en virtuele StorSimple-matrices.


Volgende stappen toocreate een service Hallo uitvoeren.

[!INCLUDE [storsimple-virtual-array-create-new-service](../../includes/storsimple-virtual-array-create-new-service.md)]

## <a name="delete-a-service"></a>Een service verwijderen

Zorg voordat u een service hebt verwijderd, dat geen verbonden apparaten wordt gebruikt. Als het Hallo-service wordt gebruikt, schakelt u Hallo verbonden apparaten. Hallo deactiveren bewerking Hallo verbinding tussen Hallo-apparaat en Hallo service-Server, maar Hallo apparaat-gegevens in de cloud Hallo behouden blijven.

> [!IMPORTANT]
> Als een service is verwijderd, Hallo-bewerking kan niet ongedaan worden gemaakt. Elk apparaat dat werd gebruikt Hallo-service moet toobe fabrieksinstellingen voordat deze kan worden gebruikt met een andere service. In dit scenario Hallo lokale gegevens op het Hallo-apparaat, evenals Hallo-configuratie niet verloren.
 

Volgende stappen toodelete een service Hallo uitvoeren.

#### <a name="toodelete-a-service"></a>toodelete een service

1. Ga te**alle resources**. Zoek uw StorSimple-apparaat Manager-service. Selecteer desgewenst toodelete Hallo-service.
   
    ![Selecteer de service toodelete](./media/storsimple-virtual-array-manage-service/deleteservice2.png)
2. Ga tooyour service dashboard tooensure er zijn geen apparaten verbonden toohello service. Als er geen apparaten die zijn geregistreerd met deze service zijn, ziet u ook een banner bericht toohello effect. Klik op **Verwijderen**.
   
    ![Verwijderen van de service](./media/storsimple-virtual-array-manage-service/deleteservice3.png)

3. Wanneer u om bevestiging gevraagd, klikt u op **Ja** in Hallo bevestigingsbericht weergegeven. 
   
    ![Service verwijderen bevestigen](./media/storsimple-virtual-array-manage-service/deleteservice4.png)
4. Het kan enkele minuten duren voordat Hallo service toobe verwijderd. Na het Hallo is service verwijderd, u ontvangt een melding.
   
    ![Geslaagde service verwijderen](./media/storsimple-virtual-array-manage-service/deleteservice6.png)

lijst met services Hello wordt vernieuwd.

 ![Bijgewerkte lijst met services](./media/storsimple-virtual-array-manage-service/deleteservice7.png)

## <a name="get-hello-service-registration-key"></a>Hallo-serviceregistratiesleutel ophalen
Nadat u een service hebt gemaakt, moet u tooregister uw StorSimple-apparaat met Hallo-service. tooregister uw eerste StorSimple-apparaat, u moet Hallo serviceregistratiesleutel. tooregister extra apparaten met een bestaande StorSimple-service, moet u zowel de registratiesleutel Hallo en Hallo service gegevensversleutelingssleutel (die is gegenereerd op Hallo eerste apparaat tijdens de registratie). Zie voor meer informatie over Hallo service gegevensversleutelingssleutel [StorSimple security](storsimple-security.md). U kunt Hallo registratiesleutel ophalen door het openen van Hallo **sleutels** blade voor uw service.

Volgende stappen tooget hello serviceregistratiesleutel Hallo uitvoeren.

#### <a name="tooget-hello-service-registration-key"></a>tooget hello serviceregistratiesleutel
1. In Hallo **StorSimple Apparaatbeheer** blade te gaan**Management &gt;**  **sleutels**.
   
   ![De blade Sleutels](./media/storsimple-virtual-array-manage-service/getregkey2.png)
2. In Hallo **sleutels** blade een serviceregistratiesleutel wordt weergegeven. Kopieer de registratiesleutel Hallo Hallo kopie pictogram. 

Houd de serviceregistratiesleutel Hallo op een veilige locatie. U moet deze sleutel, evenals Hallo service gegevensversleutelingssleutel, tooregister extra apparaten met deze service. Nadat u hebt verkregen Hallo serviceregistratiesleutel, moet u tooconfigure uw apparaat via Hallo Windows PowerShell voor StorSimple-interface.

## <a name="regenerate-hello-service-registration-key"></a>Hallo-serviceregistratiesleutel genereren
U moet een serviceregistratiesleutel tooregenerate als u vereiste tooperform sleutel worden gedraaid of als Hallo lijst servicebeheerders is gewijzigd. Wanneer u het Hallo-sleutel opnieuw genereren, wordt Hallo nieuwe sleutel alleen gebruikt voor latere apparaten registreren. Hallo-apparaten die al zijn geregistreerd, worden hierdoor niet beïnvloed door dit proces.

Volgende stappen tooregenerate een serviceregistratiesleutel Hallo uitvoeren.

#### <a name="tooregenerate-hello-service-registration-key"></a>tooregenerate hello serviceregistratiesleutel
1. In Hallo **StorSimple Apparaatbeheer** blade te gaan**Management &gt;**  **sleutels**.
   
   ![De blade Sleutels](./media/storsimple-virtual-array-manage-service/getregkey2.png)
2. In Hallo **sleutels** blade, klikt u op **genereren**.
   
   ![Klik op opnieuw genereren](./media/storsimple-virtual-array-manage-service/getregkey5.png)
3. In Hallo **opnieuw genereren serviceregistratiesleutel** blade revisie Hallo-actie vereist wanneer hello sleutels opnieuw worden gegenereerd. Alle Hallo latere apparaten die zijn geregistreerd bij deze service zal nieuwe registratiecode Hallo gebruiken. Klik op **genereren** tooconfirm. U wordt gewaarschuwd als Hallo-registratie voltooid is.
   
   ![Bevestig sleutel opnieuw genereren](./media/storsimple-virtual-array-manage-service/getregkey3.png)
4. Een nieuwe registratiecode van de service wordt weergegeven.
   
    ![Bevestig sleutel opnieuw genereren](./media/storsimple-virtual-array-manage-service/getregkey4.png)
   
   Kopieer deze sleutel en sla het voor het registreren van nieuwe apparaten aan deze service.

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over hoe te[aan de slag](storsimple-virtual-array-deploy1-portal-prep.md) met een virtueel StorSimple-matrix.
* Meer informatie over hoe te[beheren van uw StorSimple-apparaat](storsimple-ova-web-ui-admin.md).

