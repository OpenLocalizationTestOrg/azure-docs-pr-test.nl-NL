---
title: aaaChange hello Azure Active Directory-tenant in Azure RemoteApp | Microsoft Docs
description: Meer informatie over hoe toochange hello Azure Active Directory-tenant die zijn gekoppeld aan Azure RemoteApp
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 20faf169-6e48-428a-8bdd-f231daff19fa
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d0928b099b7fcfb3ab16077e295d7aaf519c3653
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-azure-active-directory-tenant-in-azure-remoteapp"></a>Hello Azure Active Directory-tenant in Azure RemoteApp wijzigen
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

Azure RemoteApp maakt gebruik van Azure Active Directory (Azure AD) tooallow gebruikerstoegang. Hallo alleen Azure AD-tenant waarmee u in Azure RemoteApp kunt is Hallo die is gekoppeld aan hello Azure-abonnement. U kunt Hallo gekoppeld abonnement weergeven op Hallo **instellingen** pagina in Hallo-portal. Bekijkt hello **Directory** kolom op Hallo **abonnementen** tabblad.

> [!NOTE]
> Voor deze toosucceed wijziging moet u eerst alle gebruikers verwijderen uit bestaande Azure Active Directory-tenant Hallo uit alle Azure RemoteApp-collecties. toodo deze, Ga toohello Azure Portal, Ga toohello **Azure RemoteApp** tabblad en openen van elke Azure RemoteApp-verzameling. Ga toohello **gebruikers** tabblad en gebruikers die deel uitmaken van de huidige Azure Active Directory-tenant tooyour verwijderen. Herhaal dit voor alle bestaande Azure RemoteApp-collecties. Dit niet doet, worden niet kunnen toocreate of patch verzamelingen.
> 
> 

Als u wilt dat een andere tenant toouse, gebruikt u deze stappen toochange Hallo koppeling met uw abonnement:

1. Verwijder eventuele toowhich Azure AD-gebruikers in Hallo-portal, hebt u toegang tooAzure RemoteApp-collecties gegeven. (Zie Opmerking Hallo hierboven voor stappen voor het toodo dit.)
2. Een Microsoft-account (voorheen een Live ID) ingesteld als Hallo-servicebeheerder. (Niet weet dat als u al servicebeheerder Hallo? U vindt hier door te klikken op **instellingen -> beheerders**.) Nu ziet hier u hoe u deze instelling wijzigen:
   
   1. Klik op Hallo-gebruiker in de rechterbovenhoek Hallo en klik vervolgens op **weergeven van mijn factuur**.
   2. Klik op Hallo-abonnement. Klik vervolgens op nieuwe pagina hello, schuif naar beneden en klikt u op **abonnementsgegevens bewerken** in Hallo rechts. (Soort Hallo middelste rechtsonder, als die helpt u bij het vinden.)
   3. Typ Hallo Microsoft-account voor Hallo-gebruiker die Hallo servicebeheerder worden moet.
3. Nu u afmelden bij Hallo-portal en vervolgens weer aanmelden met Microsoft-account die u hebt opgegeven in de vorige stap Hallo Hallo terug.
4. Klik op **Nieuw -> App Services -> Active Directory-Directory > -> Custom maken**.
5. Onder **Directory**, kies **bestaande directory gebruiken**. We zullen toohave toosign buiten Hallo portal nu, dus u **ik ben klaar toobe afgemeld**.
6. Meld u weer in Hallo portal als globale beheerder van de map Hallo gewenste tooadd. (Als u niet al een globale beheerder zijn, kunt u zich na een ronde van aanmelden en vervolgens afmelden.)
7. Wordt u gevraagd wanneer u zich aanmeldt als u wilt dat toouse uw bestaande AD-tenant met uw abonnement. Klik op **doorgaan**, en klik vervolgens op **nu afmelden**.
8. Meld u weer opnieuw en gaat u terug te**instellingen -> abonnementen**. Uw abonnement te selecteren en klik vervolgens op **Directory bewerken**. Selecteer dat u wilt dat toouse hello Azure AD-tenant.

U kunt nu Hallo nieuwe Azure AD-tenant toocontrol toegang toohello Azure-abonnement en tooconfigure gebruikerstoegang gebruiken in Azure RemoteApp.

