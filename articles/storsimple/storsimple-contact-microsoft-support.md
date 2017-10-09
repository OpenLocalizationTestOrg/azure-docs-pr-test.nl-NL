---
title: aaaLog ondersteuningsticket voor StorSimple 8000 serie | Microsoft Docs
description: Meer informatie over hoe toocreate een ondersteuning vragen en een ondersteuningssessie op uw StorSimple-apparaat te starten.
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 2ebc20fe-f490-4749-8e43-c9fac86f1676
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/27/2017
ms.author: alkohli;anbacker
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e1a3aa3c56e036c782c4fb502c477dc0feaa0ccd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="contact-microsoft-support-for-your-storsimple"></a>Neem contact op met Microsoft ondersteuning voor uw StorSimple
Als u problemen ondervindt met uw Microsoft Azure StorSimple-oplossing, kunt u een serviceaanvraag voor technische ondersteuning. In een online-sessie met de ondersteuningstechnicus moet u mogelijk ook toostart een ondersteuningssessie op uw StorSimple-apparaat. Dit artikel begeleidt u bij:

* Hoe toocreate een ondersteuning vragen.
* Hoe Hallo toostart een ondersteuningssessie in Windows PowerShell-interface van uw StorSimple-apparaat.

Bekijk Hallo [StorSimple 8000 Series ondersteuning Sla's en informatie](https://msdn.microsoft.com/library/mt433077.aspx) voordat u een ondersteuningsaanvraag maken.

## <a name="create-a-support-request"></a>Een ondersteuningsaanvraag maken
Voer Hallo stappen toocreate een verzoek om ondersteuning te volgen:

#### <a name="toocreate-a-support-request"></a>toocreate ondersteuning aan te vragen
1. In Hallo [klassieke Azure-portal](https://manage.windowsazure.com/), in de rechterbovenhoek Hallo op de naam van uw account en klik vervolgens op **contact opnemen met Microsoft ondersteuning**.
   
    ![Neem contact op met MS ondersteuning via ManagementPortal](./media/storsimple-contact-microsoft-support/Ibiza1.png)
2. U zult omgeleid toohello nieuwe Azure-portal (portal.azure.com). Klik op Hallo **nieuw ondersteuningsverzoek** tegel.
   
    ![Neem contact op met MS ondersteuning via de nieuwe portal](./media/storsimple-contact-microsoft-support/Ibiza2.png)
   
    Aan de rechterkant Hallo van welkomstscherm, Hallo **nieuw ondersteuningsverzoek** deelvenster wordt weergegeven. 
   
    ![Nieuw deelvenster voor ondersteuning aanvragen](./media/storsimple-contact-microsoft-support/Ibiza3a.png)
3. In Hallo **basisbeginselen** dialoogvenster, volledige hello te volgen:                                
   
   1. Van Hallo **probleemtype** vervolgkeuzelijst, selecteer **technische**.
   2. Selecteer een **abonnement** uit de vervolgkeuzelijst Hallo.
   3. Van Hallo **Service** vervolgkeuzelijst, selecteer **StorSimple**. 
   4. Selecteer een **ondersteuningsplan** uit de vervolgkeuzelijst Hallo. U moet een betaald ondersteuning plan tooenable technische ondersteuning.
4. Klik op **Volgende**. Hallo **probleem** dialoogvenster wordt weergegeven.
   
    ![Nieuw deelvenster voor ondersteuning aanvragen](./media/storsimple-contact-microsoft-support/Ibiza5a.png) 
5. In Hallo **probleem** dialoogvenster, volledige hello te volgen:
   
   1. Selecteer een **ernst** niveau uit de vervolgkeuzelijst Hallo.
   2. Selecteer een **probleemtype** uit de vervolgkeuzelijst Hallo.
   3. Selecteer een **categorie** uit de vervolgkeuzelijst Hallo. 
   4. In Hallo **Details** vak een korte beschrijving van het probleem.
   5. In Hallo **tijdsbestek** vak, geven Hallo datum, tijd en tijdzone die overeenkomt met de meest recente exemplaar toohello van uw probleem.
   6. Onder **uploaden bestand**, klikt u op Hallo map pictogram toobrowse tooyour support-pakket.
   7. Selecteer Hallo **diagnostische gegevens delen** selectievakje.
6. Klik op **Volgende**. Hallo **contactgegevens** dialoogvenster wordt weergegeven.
   
    ![Nieuw deelvenster voor ondersteuning aanvragen](./media/storsimple-contact-microsoft-support/Ibiza6a.png) 
7. Voer uw contactgegevens en selecteer een contactmethode (telefoon of e-mail). 
8. Selecteer Hallo **contact op met wijzigingen opslaan voor toekomstige ondersteuningsaanvragen** selectievakje.
9. Klik op **Create**.

Nadat u uw aanvraag hebt verzonden, een ondersteuningstechnicus neemt contact met u zo snel mogelijk tooproceed bij uw aanvraag.

## <a name="start-a-support-session-in-windows-powershell-for-storsimple"></a>Een support-sessie te starten in Windows PowerShell voor StorSimple
tootroubleshoot eventuele problemen die u mogelijk ondervindt met Hallo StorSimple-apparaat, moet u tooengage met Hallo Microsoft Support team. Microsoft Support wellicht toouse een ondersteuning sessie toolog op tooyour apparaat. 

Uitvoeren van de volgende Hallo stappen toostart een ondersteuningssessie:

#### <a name="toostart-a-support-session"></a>toostart een ondersteuningssessie
1. Toegang tot Hallo een apparaat via de seriële console Hallo of via een Telnet-sessie vanaf een externe computer. toodo deze, volg de stappen in Hallo [PuTTY gebruiken tooconnect toohello de seriële console apparaat](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).
2. Hallo-sessie die wordt geopend, klikt u op Hallo **Enter** key tooget vanaf de opdrachtprompt.
3. In het menu van de seriële console hello, optie 1, **aanmelden met volledige toegang**.
4. Typ bij Hallo prompt Hallo wachtwoord te volgen: 
   
    `Password1`
5. Typ bij Hallo prompt Hallo volgende opdracht:
   
    `Enable-HcsSupportAccess`
6. Een gecodeerde tekenreeks worden tooyou weergegeven. Kopieer deze tekenreeks in een teksteditor zoals Kladblok.
7. Bewaar deze tekenreeks en verzend het in een e-mailbericht tooMicrosoft ondersteuning. 

> [!IMPORTANT]
> U kunt ondersteuning toegang uitschakelen door het uitvoeren van `Disable-HcsSupportAccess`. Hallo StorSimple-apparaat wordt ook toegangspoging toodisable ondersteuning acht uur nadat het Hallo-sessie is gestart. Het is een best practice toochange referenties voor uw StorSimple-apparaat na het initiëren van een ondersteuningssessie voor.
> 
> 

