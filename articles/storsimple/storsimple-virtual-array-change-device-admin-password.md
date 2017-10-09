---
title: beheerderswachtwoord voor aaaChange virtuele matrix StorSimple-apparaat | Microsoft Docs
description: Hierin wordt beschreven hoe toouse ofwel hello Azure portal of virtuele StorSimple-matrix web UI toochange Hallo beheerderswachtwoord apparaat.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 11490814-d9fd-4dc7-9c3b-55dd2c23eaf1
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 531b395df7aeade0a909360797c6b0f0abd9fd1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-storsimple-virtual-array-device-administrator-password-via-storsimple-device-manager"></a>Hallo virtuele StorSimple-matrix apparaat beheerderswachtwoord via StorSimple Apparaatbeheer wijzigen

## <a name="overview"></a>Overzicht

Wanneer u Hallo Windows PowerShell-interface tooaccess Hallo virtuele StorSimple-matrix, bent u vereiste tooenter het beheerderswachtwoord voor een apparaat. Wanneer Hallo StorSimple-apparaat eerst is ingericht en is gestart, is het standaardwachtwoord Hallo *Wachtwoord1*. Voor beveiliging van uw gegevens Hallo Hallo standaardwachtwoord verloopt Hallo eerste keer is dat u zich aanmelden en u vereiste toochange zijn dit wachtwoord.

U kunt ook beide Hallo lokale web UI of hello Azure portal toochange Hallo wachtwoord apparaatbeheerder op elk gewenst moment nadat Hallo-apparaat is geïmplementeerd in uw productieomgeving. Elk van deze procedures wordt beschreven in dit artikel.

 ![Blade voor apparaten](./media/storsimple-virtual-array-change-device-admin-password/ova-devices-blade.png)

## <a name="use-hello-azure-portal-toochange-hello-password"></a>Hello Azure portal toochange Hallo wachtwoord gebruiken

Volgende stappen toochange Hallo beheerderswachtwoord apparaat via de Azure-portal Hallo Hallo uitvoeren.

#### <a name="toochange-hello-device-administrator-password-via-hello-azure-portal"></a>toochange hello beheerderswachtwoord apparaat via hello Azure-portal

1. Op de startpagina van Hallo-service, selecteer uw service, dubbelklikt u op Hallo servicenaam en klik vervolgens in Hallo **Management** sectie, klikt u op **apparaten**. Hiermee opent u Hallo **apparaten** blade met een lijst met alle apparaten in uw virtuele StorSimple-matrix.

2. In Hallo **apparaten** blade, dubbelklikt u op Hallo-apparaat dat een wijziging van wachtwoord vereist.

3. In Hallo **instellingen** blade voor uw apparaat, klikt u op **beveiliging**.

4. In Hallo **beveiligingsinstellingen** blade Hallo te volgen:
   
   1. Schuif omlaag toohello **apparaat beheerderswachtwoord** sectie. Geef een administrator-wachtwoord van 8 too15 tekens bevat.
   2. Hallo wachtwoord bevestigen.
   3. Klik op **opslaan** Hallo boven aan het Hallo-blade.

Hallo beheerder het wachtwoord van het apparaat is nu bijgewerkt. U kunt dit apparaat gewijzigde wachtwoord tooaccess Hallo lokaal gebruiken.

![Blade Security-instellingen](./media/storsimple-virtual-array-change-device-admin-password/ova-change-device-pwd.png)

## <a name="use-hello-local-web-ui-toochange-hello-password"></a>Hallo lokale web UI toochange Hallo wachtwoord gebruiken

Volgende stappen toochange Hallo beheerderswachtwoord apparaat via Hallo lokale webgebruikersinterface Hallo uitvoeren.

#### <a name="toochange-hello-device-administrator-password-via-hello-local-web-ui"></a>toochange hello beheerderswachtwoord apparaat via Hallo lokale webgebruikersinterface

1. Klik in Hallo lokale web UI op **onderhoud** > **wachtwoordwijziging** voor uw apparaat.
   
    ![Wachtwoord1 wijzigen](./media/storsimple-virtual-array-change-device-admin-password/image40.png)
2. Voer Hallo **huidige wachtwoord**.
3. Geef een **nieuw wachtwoord**. Hallo-wachtwoord moet ten minste 8 tekens lang zijn. Deze moet 3 van 4 van Hallo volgende bevatten: hoofdletters, kleine letters, numerieke en speciale tekens.
   
    Denk eraan dat uw wachtwoord mag niet Hallo hetzelfde als de laatste 24 wachtwoorden Hallo.
4. Hallo wachtwoord tooconfirm opnieuw het.
   
    ![Wachtwoord2 wijzigen](./media/storsimple-virtual-array-change-device-admin-password/image41.png)
5. Klik onder aan de pagina Hallo Hallo op **toepassen**. het nieuwe wachtwoord Hallo nu wordt toegepast. Als het Hallo-wachtwoordwijziging niet is geslaagd, ziet u Hallo volgende fout:
   
    ![Fout bij het](./media/storsimple-virtual-array-change-device-admin-password/image42.png)
   
    Nadat het Hallo-wachtwoord is bijgewerkt, wordt u gewaarschuwd. Vervolgens kunt u dit apparaat gewijzigde wachtwoord tooaccess Hallo lokaal.


## <a name="next-steps"></a>Volgende stappen
Meer informatie over hoe te[beheren van uw virtuele StorSimple-matrix](storsimple-ova-web-ui-admin.md).

