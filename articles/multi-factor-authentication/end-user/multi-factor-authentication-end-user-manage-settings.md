---
title: aaaManage uw verificatie-instellingen voor in twee stappen | Microsoft Docs
description: Beheren hoe u Azure multi-factor Authentication, inclusief het aanpassen van uw contactgegevens of configureren van uw apparaten gebruiken.
services: multi-factor-authentication
keywords: multifactor-verificatie-client, verificatieprobleem, correlatie-ID
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: d3372d9a-9ad1-4609-bdcf-2c4ca9679a3b
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: kgremban
ms.custom: end-user
ms.openlocfilehash: 2c974b08c584943f3c5a6b9bf16497d1706e8329
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-settings-for-two-step-verification"></a>De instellingen voor verificatie in twee stappen beheren
Dit artikel bevat antwoorden op vragen over hoe tooupdate instellingen voor de verificatie of meervoudige verificatie in twee stappen. Als u problemen met aanmelden tooyour account hebt, raadpleeg dan te[problemen hebt met verificatie in twee stappen](multi-factor-authentication-end-user-troubleshoot.md) voor hulp bij probleemoplossing.

## <a name="where-toofind-hello-settings-page"></a>Waar toofind instellingenpagina Hallo
Afhankelijk van hoe uw bedrijf van Azure multi-factor Authentication instellen, zijn er enkele locaties waar u uw instellingen zoals uw telefoonnummer wijzigen kunt.

Als uw IT-beheerder een specifieke URL of verificatie in twee stappen van stappen toomanage verzonden, volgt u deze instructies. Hallo instructies te volgen moet anders werken voor alle andere. Als u deze stappen maar niet ziet Hallo dezelfde opties, waardoor uw werk of school hun eigen portal wordt aangepast. Vraag uw beheerder voor Hallo koppeling tooyour Azure multi-factor Authentication-portal.

1. Aanmelden te[https://myapps.microsoft.com](https://myapps.microsoft.com)  
2. Selecteer de accountnaam van uw in de rechterbovenhoek Hallo en selecteer vervolgens **profiel**.  
3. Selecteer **aanvullende beveiligingsverificatie**.  

    ![Myapps](./media/multi-factor-authentication-end-user-manage/myapps1.png)
4. Hallo extra beveiliging verificatie pagina wordt geladen met uw instellingen.

    ![Proofup](./media/multi-factor-authentication-end-user-manage/proofup.png)

## <a name="i-want-toochange-my-phone-number-or-add-a-secondary-number"></a>Ik wilt toochange mijn telefoonnummer of een secundaire nummer toevoegen
Het is belangrijk tooconfigure een telefoonnummer van de secundaire verificatie.  Omdat uw primaire telefoon nummer en uw mobiele app zijn waarschijnlijk op Hallo dezelfde telefoon, Hallo secundaire telefoonnummer is de enige manier Hallo kunt u zich kunt tooget weer toegang tot je account als uw telefoon is kwijtgeraakt of gestolen.

> [!NOTE]
> Als u geen toegang tooyour primaire telefoonnummer en opvragen in tooyour account hulp nodig hebt, raadpleegt u onze help-onderwerpen in [problemen hebt met verificatie in twee stappen](multi-factor-authentication-end-user-troubleshoot.md).  

**toochange uw primaire telefoonnummer:**  

1. Op Hallo extra beveiliging verificatie pagina Hallo tekstvak selecteren met uw huidige telefoonnummer en met uw nieuwe telefoonnummer te bewerken.  
2. Selecteer **Opslaan**.  
3. Als dit Hallo getal dat u voor uw voorkeursoptie voor verificatie-optie gebruikt is, hebt u tooverify Hallo nieuw nummer voordat u deze kunt opslaan.  

**een tweede telefoonnummer tooadd:**  

1. Klik op Hallo extra beveiliging verificatie pagina selectievakje Hallo naast te**telefoon voor alternatieve authenticatie.**  
2. Voer uw secundaire telefoonnummer in het tekstvak Hallo.  
3. Selecteer **opslaan** en uw wijzigingen zijn voltooid.  

## <a name="require-two-step-verification-again-on-a-device-youve-marked-as-trusted"></a>Verificatie in twee stappen opnieuw op een apparaat dat u hebt gemarkeerd als vertrouwd vereisen

Afhankelijk van de instellingen van uw organisatie, moet u wellicht een selectievakje met de tekst ' niet opnieuw vragen voor **X** dagen ' wanneer u verificatie in twee stappen uitvoeren op uw browser. Als u dit selectievakje inschakelt en uw apparaat kwijtraakt of denkt dat uw account is geknoeid moet u uw apparaten in twee stappen verificatie tooall weer. 

1. Selecteer op Hallo extra beveiliging verificatie pagina **multi factor authentication herstellen op eerder vertrouwde apparaten**.
2. Hallo wanneer die u zich op elk apparaat aanmeldt, moet u de verificatie in twee stappen na vragen aan gebruiker tooperform. 

## <a name="how-do-i-clean-up-microsoft-authenticator-from-my-old-device-and-move-tooa-new-one"></a>Hoe Microsoft Authenticator opschonen van mijn oude apparaat en ik tooa nieuwe verplaatsen?
Wanneer u Hallo-app van uw apparaat of opnieuw instellen van Hallo apparaat verwijdert, verwijdert Hallo activering op Hallo back-end niet meer. Zie voor meer informatie [Microsoft Authenticator](microsoft-authenticator-app-how-to.md).

## <a name="next-steps"></a>Volgende stappen
* Problemen oplossen met tips en help op [problemen hebt met verificatie in twee stappen](multi-factor-authentication-end-user-troubleshoot.md)
* Instellen van [app-wachtwoorden](multi-factor-authentication-end-user-app-passwords.md) voor alle apps die verificatie in twee stappen niet ondersteunen.
