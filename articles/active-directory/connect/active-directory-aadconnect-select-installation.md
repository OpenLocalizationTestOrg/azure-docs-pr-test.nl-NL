---
title: 'Azure AD Connect: Uw installatietype selecteren | Microsoft Docs'
description: In dit onderwerp leert u hoe tooselect Hallo installatie toouse Typ voor Azure AD Connect
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: a700e59eb05947ee1dbd9993141200c9340b2f1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="select-which-installation-type-toouse-for-azure-ad-connect"></a>Selecteer welk type installatie toouse voor Azure AD Connect
Azure AD Connect heeft twee installatietypen voor nieuwe installatie: Express en aangepast. Dit onderwerp helpt u toodecide die optie toouse tijdens de installatie.

## <a name="express"></a>Express
Express is de meest voorkomende optie Hallo en wordt gebruikt door ongeveer 90% van alle nieuwe installaties. Was ontworpen tooprovide een configuratie die geschikt is voor Hallo meest voorkomende klant scenario's.

Er wordt vanuit gegaan:

- U hebt een enkele Active Directory lokale forest.
- U hebt een enterprise-beheerdersaccount die voor Hallo installatie kunt u.
- U hebt minder dan 100.000 objecten in uw lokale Active Directory.

U krijgt:

- [Wachtwoordsynchronisatie](active-directory-aadconnectsync-implement-password-synchronization.md) van lokale tooAzure AD voor eenmalige aanmelding.
- Een configuratie die wordt gesynchroniseerd [gebruikers, groepen, contactpersonen en Windows 10-computers](active-directory-aadconnectsync-understanding-default-configuration.md).
- Synchronisatie van alle in aanmerking komende objecten in alle domeinen en alle OE's.
- [Automatische upgrade](active-directory-aadconnect-feature-automatic-upgrade.md) is ingeschakeld toomake zeker dat u altijd Hallo meest recente versie gebruiken.

Opties voor waar u Express nog steeds kunt gebruiken:

- Als u niet dat toosynchronize alle OE's wilt, u kunt nog steeds gebruiken Express en op de laatste pagina hello, het vakje **Start het synchronisatieproces Hallo...** *. Vervolgens Hallo-installatiewizard opnieuw uitvoeren en wijzigen van Hallo OE's in [configuratieopties](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options) en geplande synchronisatie inschakelen.
- Wilt u tooenable een Hallo-functies in Azure AD Premium, zoals wachtwoord terugschrijven. Ga eerst via snelle tooget Hallo initiële installatie is voltooid. Vervolgens Hallo-installatiewizard opnieuw uitvoeren en wijzigen van Hallo [configuratieopties](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options).

## <a name="custom"></a>Aangepast telefoonnummer
Hallo aangepaste pad kunt veel meer opties dan express. Het moet worden gebruikt in alle gevallen waarbij Hallo-configuratie wordt beschreven in de vorige sectie voor snelle niet representatief is voor uw organisatie.

Gebruiken wanneer:

- U hebt geen toegang tot tooan enterprise-beheerdersaccount in Active Directory.
- U hebt meer dan één forest of u van plan bent toosynchronize meer dan één forest in toekomstige Hallo.
- U kunt domeinen hebt in uw forest niet bereikbaar is vanaf Hallo Connect-server.
- U van plan bent toouse federation of Pass through-verificatie voor de gebruiker zich aanmelden.
- U hebt meer dan 100.000 objecten en moet toouse een volledige SQL Server.
- U van plan bent toouse filteren op basis van een groep en niet alleen domein of filteren op basis van organisatie-eenheid.

## <a name="upgrade-from-dirsync"></a>Upgraden van DirSync
Als u momenteel DirSync gebruikt, stappen Hallo in [Upgrade van DirSync](active-directory-aadconnect-dirsync-upgrade-get-started.md) tooupgrade uw bestaande configuratie. Er zijn twee verschillende upgrade-opties:

- In-place upgrade tooinstall verbinding maken op Hallo dezelfde server.
- Parallelle implementatie tooinstall Connect op een nieuwe server tijdens het Hallo bestaande DirSync-server nog steeds operationeel is.

## <a name="upgrade-from-azure-ad-sync"></a>Upgrade uitvoeren vanaf Azure AD Sync
Als u Azure AD Sync momenteel gebruikt, wordt u Hallo volgen kunt [dezelfde stappen](active-directory-aadconnect-upgrade-previous-version.md) als wanneer u een van de nieuwere versie tooa één verbinding maken upgrade. Er zijn twee verschillende upgrade-opties:

- In-place upgrade tooinstall verbinding maken op Hallo dezelfde server.
- Swing migratie tooinstall Connect op een nieuwe server tijdens het Hallo bestaande Azure AD Sync-server nog steeds operationeel is.

## <a name="migrate-from-fim2010-or-mim2016"></a>Migreren van FIM 2010 wachtwoordherstelextensies of MIM2016
Als u momenteel Forefront Identity Manager 2010 of Microsoft Identity Manager 2016 Hello Azure AD-Connector gebruikt, is de enige optie een migratie. Volg de stappen Hallo in [swing migratie](active-directory-aadconnect-upgrade-previous-version.md#swing-migration). FIM 2010 wachtwoordherstelextensies/MIM2016 in stappen van hello, vervangen een melding van Azure AD Sync.

## <a name="next-steps"></a>Volgende stappen
Afhankelijk van de optie Hallo u toouse hebt geselecteerd, Hallo tabel gebruiken van inhoud toohello links toofind uw artikel Hello gedetailleerde stappen.
