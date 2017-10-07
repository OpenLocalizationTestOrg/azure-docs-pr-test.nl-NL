---
title: 'Azure AD Connect: Volgende stappen en hoe Azure AD Connect toomanage | Microsoft Docs'
description: Meer informatie over hoe tooextend standaardconfiguratie en operationele taken Hallo voor Azure AD Connect.
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: c18bee36-aebf-4281-b8fc-3fe14116f1a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 4404aaff24d54d76b83baca3b331a6a250ba4c03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="next-steps-and-how-toomanage-azure-ad-connect"></a>Volgende stappen en hoe toomanage Azure AD Connect
Gebruik Hallo operationele procedures in dit artikel toocustomize verbinding maken met Azure Active Directory (Azure AD) toomeet behoeften en de vereisten van uw organisatie.  

## <a name="add-additional-sync-admins"></a>Voeg aanvullende sync beheerders toe
Standaard worden alleen Hallo-gebruiker die Hallo installatie en lokale Administrators kunnen toomanage hello geïnstalleerd synchronisatie-engine. Voor andere personen toobe kunnen tooaccess en beheren van Hallo synchronisatie-engine, Hallo groep ADSyncAdmins op de lokale server Hallo vinden en ze toothis groep toevoegen.

## <a name="assign-licenses-tooazure-ad-premium-and-enterprise-mobility-suite-users"></a>Toewijzen van licenties tooAzure AD Premium en Enterprise Mobility Suite-gebruikers
Nu dat uw gebruikers zijn gesynchroniseerd toohello cloud, moet u tooassign ze een licentie zodat ze kunnen aan de slag met cloud-apps, zoals Office 365.

### <a name="tooassign-an-azure-ad-premium-or-enterprise-mobility-suite-license"></a>tooassign een Azure AD Premium of Enterprise Mobility Suite-licentie

1. Meld u aan toohello Azure-portal als een beheerder.
2. Selecteer aan de linkerkant Hallo **Active Directory**.
3. Op Hallo **Active Directory** pagina, dubbelklikt u op Hallo map waaraan u tooset-up wilt Hallo-gebruikers.
4. Selecteer Hallo bovenaan de pagina directory Hallo in **licenties**.
5. Op Hallo **licenties** pagina **Active Directory Premium** of **Enterprise Mobility Suite**, en klik vervolgens op **toewijzen**.
6. Selecteer in het dialoogvenster Hallo Hallo-gebruikers u wilt tooassign licenties aan en klik vervolgens op Hallo vinkje pictogram toosave Hallo wijzigingen.

## <a name="verify-hello-scheduled-synchronization-task"></a>Controleer of de geplande synchronisatietaak Hallo
Gebruik hello Azure portal toocheck Hallo status van een synchronisatie.

### <a name="tooverify-hello-scheduled-synchronization-task"></a>tooverify hello geplande synchronisatietaak
1. Meld u aan toohello Azure-portal als een beheerder.
2. Selecteer aan de linkerkant Hallo **Active Directory**.
3. Op Hallo **Active Directory** pagina, dubbelklikt u op Hallo map waaraan u tooset-up wilt Hallo-gebruikers.
4. Selecteer Hallo bovenaan de pagina directory Hallo in **Adreslijstintegratie**.
5. Onder **integratie met lokale active directory**, opmerking Hallo tijd van laatste synchronisatie.

<center>![Tijd van de Directory-synchronisatie](./media/active-directory-aadconnect-whats-next/verify.png)</center>

## <a name="start-a-scheduled-synchronization-task"></a>Start een geplande synchronisatietaak
Als u een synchronisatietaak toorun moet, kunt u dit doen door nogmaals via hello Azure AD Connect-wizard uit te voeren.  U moet uw Azure AD-referenties tooprovide.  Selecteer in de wizard Hallo Hallo **Synchronisatieopties aanpassen** en op **volgende** toomove via Hallo-wizard. Zorg ervoor dat Hallo aan het einde van Hallo **Hallo synchronisatieproces gestart zodra Hallo eerste configuratie is voltooid** is ingeschakeld.

<center>![Synchronisatie starten](./media/active-directory-aadconnect-whats-next/startsynch.png)</center>

Zie voor meer informatie over hello Azure AD Connect-synchronisatie Scheduler [met Azure AD Connect Scheduler](active-directory-aadconnectsync-feature-scheduler.md).

## <a name="additional-tasks-available-in-azure-ad-connect"></a>Aanvullende taken die beschikbaar zijn in Azure AD Connect
Na de initiële installatie van Azure AD Connect, kunt u altijd Hallo wizard opnieuw starten vanuit hello Azure AD Connect start pagina of het bureaublad snelkoppeling.  U ziet dat een aantal nieuwe opties in Hallo vorm van aanvullende taken opnieuw de verbinding met de wizard Hallo biedt.  

Hallo volgende tabel geeft een samenvatting van deze taken en een korte beschrijving van elke taak.

![Lijst met extra taken](./media/active-directory-aadconnect-whats-next/addtasks.png)

| Extra taak | Beschrijving |
| --- | --- |
| **Weergave Hallo geselecteerde scenario** |Uw huidige Azure AD Connect-oplossing weergeven.  Dit omvat algemene instellingen, gesynchroniseerd mappen en de synchronisatie-instellingen. |
| **Opties voor synchronisatie aanpassen** |De huidige configuratie Hallo zoals het toevoegen van aanvullende configuratie van Active Directory-forests toohello of synchronisatie-opties, zoals gebruikers, groepen, apparaat of wachtwoord terugschrijven inschakelen wijzigen. |
| **Faseringsmodus inschakelen** |Fase-informatie die niet direct is gesynchroniseerd en niet geëxporteerd tooAzure AD of op de lokale Active Directory.  Met deze functie kunt u synchronisaties Hallo bekijken voordat ze optreden. |

## <a name="next-steps"></a>Volgende stappen
Meer informatie over [uw on-premises identiteiten integreren met Azure Active Directory](active-directory-aadconnect.md).
