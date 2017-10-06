---
title: 'Azure AD Connect-synchronisatie: onopzettelijke verwijderingen voorkomen | Microsoft Docs'
description: Dit onderwerp wordt beschreven hello te voorkomen dat de functie onopzettelijk verwijderen (onopzettelijke verwijderingen voorkomen) in Azure AD Connect.
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 6b852cb4-2850-40a1-8280-8724081601f7
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 159597f8354806fcaea1430e0ff84956338592a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-prevent-accidental-deletes"></a>Azure AD Connect-synchronisatie: onopzettelijke verwijderingen voorkomen
Dit onderwerp wordt beschreven hello te voorkomen dat de functie onopzettelijk verwijderen (onopzettelijke verwijderingen voorkomen) in Azure AD Connect.

Wanneer de installatie van Azure AD Connect te voorkomen dat onopzettelijke verwijderingen is standaard ingeschakeld en geconfigureerde toonot een exporteren met meer dan 500 Verwijderingen toestaan. Deze functie is ontworpen tooprotect tegen onbedoeld configuratie wordt gewijzigd en wijzigingen tooyour on-premises adreslijst die veel gebruikers en andere objecten zou beïnvloeden.

## <a name="what-is-prevent-accidental-deletes"></a>Wat is onopzettelijke verwijderingen voorkomen
Algemene scenario's, wanneer er veel verwijderingen omvatten:

* Wijzigingen te[filteren](active-directory-aadconnectsync-configure-filtering.md) waar een volledige [organisatie-eenheid](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering) of [domein](active-directory-aadconnectsync-configure-filtering.md#domain-based-filtering) is uitgeschakeld.
* Alle objecten in een organisatie-eenheid worden verwijderd.
* De naam van een organisatie-eenheid wordt gewijzigd zodat alle objecten in deze worden beschouwd als toobe buiten het bereik van synchronisatie.

de standaardwaarde Hallo van 500 objecten kan worden gewijzigd met PowerShell met `Enable-ADSyncExportDeletionThreshold`. U moet deze waarde toofit Hallo grootte van uw organisatie configureren. Aangezien Hallo sync scheduler wordt elke 30 minuten uitgevoerd, is Hallo waarde Hallo aantal verwijderingen gezien binnen 30 minuten.

Als er geëxporteerd te veel verwijderingen gefaseerde toobe tooAzure AD, en vervolgens hello export stopt en u een e-mail als volgt ontvangt:

![E-mailadres onopzettelijke verwijderingen voorkomen](./media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/email.png)

> *Hello (technische contactpersoon). (Tijd) Hallo identiteit synchronisatieservice gedetecteerd dat het aantal verwijderingen Hallo Hallo geconfigureerde exportverwijderingsdrempel instellen voor (organisatienaam) overschreden. Een totaal van (getal) objecten zijn in deze identiteitssynchronisatie uitvoeren voor verwijdering verzonden. Dit bereikt of overschreden Hallo geconfigureerd waarde voor drempel voor verwijdering van objecten (getal). Moet je tooprovide bevestiging dat deze verwijderingen moeten worden verwerkt voordat er wordt voortgezet. Zie Hallo onopzettelijke verwijderingen voor meer informatie over Hallo fout weergegeven in dit e-mailbericht te blokkeren.*
>
> 

U ziet ook Hallo status `stopped-deletion-threshold-exceeded` wanneer u zoeken in Hallo **Synchronization Service Manager** gebruikersinterface voor Hallo Export profile.
![Onopzettelijke verwijderingen Sync Service Manager UI voorkomen](./media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/syncservicemanager.png)

Als dit werd niet verwacht, onderzoek en corrigerende acties uitvoeren. toosee welke objecten over toobe verwijderd, Hallo te volgen:

1. Start **synchronisatieservice** van Hallo Menu Start.
2. Ga te**Connectors**.
3. Selecteer Hallo Connector met het type **Azure Active Directory**.
4. Onder **acties** toohello rechts, selecteer **Connectorgebied zoeken**.
5. In het pop-upvenster onder Hallo **bereik**, selecteer **verbroken omdat** en kiest u een tijdstip in de afgelopen Hallo. Klik op **Search**. Deze pagina bevat een overzicht van alle objecten over toobe verwijderd. Door te klikken op elk item, kunt u aanvullende informatie over Hallo-object ophalen. U kunt ook klikken op **kolominstelling** tooadd extra kenmerken toobe zichtbaar in Hallo raster.

![Connectorgebied zoeken](./media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/searchcs.png)

Desgewenst alle Hallo verwijderingen worden vervolgens Hallo te volgen:

1. tooretrieve hello huidige exportverwijderingsdrempel instellen, voer de PowerShell-cmdlet Hallo `Get-ADSyncExportDeletionThreshold`. Geef een globale beheerder van Azure AD-account en wachtwoord. Hallo-standaardwaarde is 500.
2. tootemporarily deze beveiliging uitschakelen en kunt u deze verwijdert doorlopen, voer de PowerShell-cmdlet Hallo: `Disable-ADSyncExportDeletionThreshold`. Geef een globale beheerder van Azure AD-account en wachtwoord.
   ![Referenties](./media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/credentials.png)
3. Hello Azure Active Directory-Connector nog steeds is geselecteerd, selecteer Hallo actie **uitvoeren** en selecteer **exporteren**.
4. toore inschakelen Hallo beveiliging, voer de PowerShell-cmdlet Hallo: `Enable-ADSyncExportDeletionThreshold -DeletionThreshold 500`. 500 vervangen door Hallo-waarde die u bij het ophalen van het huidige exportverwijderingsdrempel instellen Hallo opgemerkt. Geef een globale beheerder van Azure AD-account en wachtwoord.

## <a name="next-steps"></a>Volgende stappen
**Overzichtsonderwerpen**

* [Azure AD Connect-synchronisatie: inzicht en synchronisatie aanpassen](active-directory-aadconnectsync-whatis.md)
* [Uw on-premises identiteiten integreren met Azure Active Directory](active-directory-aadconnect.md)
