---
title: 'Azure AD Connect-synchronisatie: inzicht krijgen in gebruikers en contactpersonen | Microsoft Docs'
description: Verklaart gebruikers en contactpersonen in Azure AD Connect-synchronisatie.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 8d204647-213a-4519-bd62-49563c421602
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi;andkjell
ms.openlocfilehash: 4d80648c53a2981eb2626338913ed2282423f183
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-understanding-users-and-contacts"></a>Azure AD Connect-synchronisatie: inzicht krijgen in gebruikers en contactpersonen
Er zijn verschillende redenen waarom hebt u meerdere Active Directory-forests en er zijn diverse verschillende implementatietopologieën. Algemene modellen bevat de implementatie van een account-resource en GAL sync'ed forests na een fusie & overname. Maar zelfs als er pure modellen, hybride modellen, ook worden gebruikt. Hallo standaardconfiguratie in Azure AD Connect-synchronisatie wordt niet wordt ervan uitgegaan dat een bepaald model maar, afhankelijk van hoe zoeken van overeenkomende gebruikers is geselecteerd in de installatiehandleiding hello, verschillende problemen kunnen worden waargenomen.

In dit onderwerp doorlopen we het gedrag van de standaardconfiguratie Hallo in bepaalde topologieën. We doorlopen Hallo-configuratie en Hallo synchronisatie regeleditor gebruikte toolook op Hallo configuratie kan worden.

Er zijn enkele algemene regels Hallo-configuratie wordt ervan uitgegaan dat:

* Ongeacht die we importeren uit Hallo bron Active Directory's bestellen, moet Hallo eindresultaat altijd worden Hallo dezelfde.
* Een actieve account altijd draagt bij aanmelden informatie, met inbegrip van **userPrincipalName** en **sourceAnchor**.
* Een uitgeschakeld account bijdragen userPrincipalName en sourceAnchor, tenzij het een gekoppeld postvak als er geen actieve account toobe gevonden.
* Een account met een gekoppeld postvak wordt nooit worden gebruikt voor userPrincipalName en sourceAnchor. Ervan wordt uitgegaan dat er een actieve account later worden gevonden.
* Een contact-object mogelijk ingerichte tooAzure AD als een contactpersoon of als een gebruiker. U weet niet zeker totdat alle bron Active Directory-forests zijn verwerkt.

## <a name="contacts"></a>Contactpersonen
Contactpersonen die een gebruiker in een ander forest dat is gebruikelijk dat na een fusie & overname waarbij een oplossing GALSync twee of meer Exchange-forests is bridging. altijd lid wordt van Hallo connector ruimte toohello metaverse met behulp van e-mailkenmerk Hallo Hallo contact-object. Als er al een contactpersoon of gebruikersobject Hello dezelfde e-mailadres, Hallo objecten aan elkaar worden gekoppeld. Dit is geconfigureerd in de regel Hallo **In uit Active Directory: Neem contact op met Join**. Er is ook een regel met naam **In uit Active Directory: Neem contact op met algemene** met een kenmerk stroom toohello metaverse-kenmerk **sourceObjectType** met Hallo constante **Contact**. Deze regel bevat een zeer lage prioriteit als elk gebruikersobject gekoppelde toohello is dezelfde metaverse-object en vervolgens Hallo regel **In uit Active Directory-gebruiker algemene** Hallo waarde gebruikerskenmerk toothis zal bijdragen. Met deze regel heeft dit kenmerk Hallo waarde contact op met als er geen gebruiker is toegevoegd en Hallo gebruiker waarde als er ten minste één gebruiker zijn gevonden.

Hallo uitgaande regel voor het inrichten van een object tooAzure AD **uit tooAAD: Neem contact op met Join** maakt contact-object als hello metaverse-kenmerk **sourceObjectType** te is ingesteld**Neem contact op met** . Als dit kenmerk is ingesteld, te**gebruiker**, vervolgens Hallo regel **uit tooAAD – gebruiker toevoegen** in plaats daarvan maakt een gebruikersobject.
Het is mogelijk dat een object wordt gepromoveerd van contactpersoon tooUser wanneer meer bron Active Directory's worden geïmporteerd en gesynchroniseerd.

Bijvoorbeeld in een topologie GALSync vindt we contact op met objecten voor iedereen in de tweede forest Hallo wanneer we de eerste forest Hallo importeert. Dit wordt nieuwe contactpersoon objecten in Hallo AAD-Connector voorbereiden. Wanneer we later importeren en synchroniseren van de tweede forest hello, we Hallo echte gebruikers zoeken en toevoegen toohello bestaande metaverse-objecten. We vervolgens contact Hallo-object in AAD verwijderen en een nieuw gebruikersobject in plaats daarvan maakt.

Als u een topologie waarbij gebruikers worden weergegeven als contactpersonen hebt, zorg er dan voor dat u toomatch gebruikers op Hallo e-mailkenmerk in Hallo installatiehandleiding. Als u een andere optie selecteert, wordt u een configuratie van de afhankelijke volgorde hebben. Neem contact op met objecten altijd op Hallo e-mailkenmerk wordt toegevoegd, maar gebruikersobjecten wordt alleen op Hallo e-mailkenmerk toegevoegd als deze optie is geselecteerd in de installatiehandleiding Hallo. U kan vervolgens eindigen met twee verschillende objecten in de metaverse Hallo Hello dezelfde e-mailkenmerk als Hallo contact-object is geïmporteerd voordat Hallo gebruikersobject. Tijdens de export tooAzure AD, een fout gegenereerd. Dit gedrag is inherent aan het ontwerp en zou wijzen op beschadigde gegevens of die Hallo-topologie is niet juist geïdentificeerd tijdens de installatie van Hallo.

## <a name="disabled-accounts"></a>Uitgeschakelde accounts
Uitgeschakelde accounts worden ook tooAzure AD gesynchroniseerd. Uitgeschakelde accounts zijn algemene toorepresent bronnen in Exchange, bijvoorbeeld vergaderruimten. Hallo-uitzondering is gebruikers met een gekoppeld postvak; zoals eerder vermeld, wordt deze nooit een account tooAzure AD inrichten.

Hallo veronderstelling is dat als een uitgeschakelde gebruikersaccount wordt gevonden, wordt er een andere actieve account later geen wordt gevonden en Hallo-object ingerichte tooAzure AD met Hallo userPrincipalName en sourceAnchor gevonden. In geval zal een andere actieve account lid worden toohello hetzelfde metaverse-object, klikt u vervolgens de userPrincipalName en sourceAnchor wordt gebruikt.

## <a name="changing-sourceanchor"></a>SourceAnchor wijzigen
Wanneer een object is geëxporteerd is en vervolgens het tooAzure AD geen toegestane toochange hello sourceAnchor meer. Hallo-object is wanneer geëxporteerde Hallo metaverse-kenmerk **cloudSourceAnchor** is ingesteld met Hallo **sourceAnchor** waarde geaccepteerd door Azure AD. Als **sourceAnchor** wordt gewijzigd en niet overeen met **cloudSourceAnchor**, Hallo regel **uit tooAAD – gebruiker toevoegen** genereert fout Hallo **kenmerk sourceAnchor is gewijzigd**. In dit geval Hallo configuratie of gegevens moeten worden gecorrigeerd Hallo dus dezelfde sourceAnchor is aanwezig in Hallo metaverse opnieuw voordat het Hallo-object kan opnieuw worden gesynchroniseerd.

## <a name="additional-resources"></a>Aanvullende resources
* [Azure AD Connect-synchronisatie: Synchronisatie-opties voor aanpassen](active-directory-aadconnectsync-whatis.md)
* [Uw on-premises identiteiten integreren met Azure Active Directory](active-directory-aadconnect.md)

