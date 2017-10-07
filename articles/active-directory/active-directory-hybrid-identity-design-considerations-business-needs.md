---
title: ontwerpoverwegingen voor aaaAzure Active Directory hybride identiteit - identiteitsvereisten bepalen | Microsoft Docs
description: Hallo bedrijfsbehoeften van die toodefine Hallo vereisten voor Hallo hybride identiteit leiden identificeren.
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: de690978-84ef-41ad-9dfe-785722d343a1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: b2f1cad923b0f08ededa0d8f9a4ea8e799956e54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="determine-identity-requirements-for-your-hybrid-identity-solution"></a>Identiteitsvereisten bepalen voor uw oplossing voor hybride identiteit
Hallo eerste stap bij het ontwerpen van een hybride identiteitsoplossing is toodetermine Hallo vereisten voor Hallo business organisatie die zal worden gebruik van deze oplossing.  Hybride identiteit wordt gestart als een ondersteunende rol (ondersteund alle cloudoplossingen door verificatie te bieden) en wordt tooprovide nieuwe en interessante mogelijkheden die nieuwe werkbelastingen voor gebruikers te ontgrendelen.  Deze werkbelastingen of services die u wenst dat tooadopt voor uw gebruikers worden Hallo-vereisten voor hybride identiteit het ontwerp van Hallo bepaald.  Deze werkbelastingen en services moeten tooleverage hybride identiteit zowel on-premises en in de cloud Hallo.  

U moet toogo deze belangrijke aspecten van Hallo business toounderstand wat het is nu een vereiste is en welke Hallo bedrijf van plan voor toekomstige Hallo. Als u geen Hallo zichtbaarheid van Hallo lange termijnstrategie voor het ontwerp van hybride identiteit, zijn waarschijnlijk dat uw oplossing niet zal schaalbare Hallo zakelijke behoeften groei en veranderingen.   T hij diagram hieronder bevat een voorbeeld van een hybride identiteit architectuur en Hallo werkbelastingen die zijn voor gebruikers wordt ontgrendeld. Dit is slechts een voorbeeld van alle Hallo nieuwe mogelijkheden die kunnen worden ontgrendeld en geleverd met een strategie voor een solide hybride identiteit. 

Sommige onderdelen die deel van de architectuur van Hallo hybride identiteit uitmaken![](./media/hybrid-id-design-considerations/hybrid-identity-architechture.png)

## <a name="determine-business-needs"></a>Bedrijfsbehoeften vaststellen
Elk bedrijf kent verschillende behoeften, zelfs als deze bedrijven deel van Hallo uitmaken dezelfde bedrijfstak Hallo echte zakelijke behoeften verschillen. U kunt nog steeds gebruikmaken van best practices uit de industrie Hallo maar uiteindelijk het Hallo bedrijfsbehoeften van die toodefine Hallo vereisten voor Hallo hybride identiteit leiden is. 

Zorg ervoor dat uw bedrijf voor vragen tooidentify tooanswer Hallo volgende nodig:

* Is uw bedrijf op zoek toocut IT-operationele kosten?
* Is uw bedrijf op zoek toosecure cloud activa (SaaS-apps, infrastructuur)?
* Is uw bedrijf toomodernize Zoek uw IT-afdeling?
  * Zijn uw gebruikers meer mobiele en veeleisende IT toocreate uitzonderingen in uw DMZ tooallow ander type verkeer tooaccess verschillende bronnen?
  * Heeft uw bedrijf oudere apps die nodig gepubliceerd toobe zijn toothese moderne gebruikers, maar die niet eenvoudig toorewrite?
  * Heeft uw bedrijf moet tooaccomplish al deze taken en brengt u het op Hallo onder toezicht hetzelfde moment?
* Is uw bedrijf identiteit van de toosecure gebruikers opzoeken en risico's te beperken door nieuwe hulpprogramma's die gebruikmaken van de kennis van de Microsoft Azure-beveiliging expertise lokale Hallo te brengen?
* Is uw bedrijf tooget rid Hallo probeert gevreesde 'externe' accounts on-premises en verplaatst u ze toohello cloud waar ze niet langer een inactieve bedreiging binnen uw on-premises omgeving zijn?

## <a name="analyze-on-premises-identity-infrastructure"></a>On-premises identity infrastructuur analyseren
Nu u een idee hebt met betrekking tot de zakelijke vereisten van uw bedrijf, moet u tooevaluate uw on-premises identity-infrastructuur. Deze evaluatie is belangrijk voor het definiëren van Hallo technische vereisten toointegrate uw huidige oplossing toohello cloud identity identiteitsbeheersysteem. Zorg ervoor dat tooanswer Hallo vragen te volgen:

* Welke oplossing voor verificatie en autorisatie biedt uw bedrijf gebruik van lokale? 
* Heeft uw bedrijf momenteel synchronisatie van lokale services?
* Maakt uw bedrijf gebruik van een derde partij-ID-Providers (IdP)?

U moet ook toobe op de hoogte van Hallo cloud-services die uw bedrijf kan hebben. Uitvoeren van een beoordeling toounderstand Hallo huidige integratie met SaaS-IaaS of PaaS-modellen in uw omgeving is heel belangrijk. Zorg ervoor dat tooanswer Hallo vragen tijdens deze beoordeling te volgen:

* Heeft uw bedrijf geïntegreerd met een cloudserviceprovider?
* Zo ja, welke services worden gebruikt?
* Deze integratie momenteel is in productie of is het een test?

> [!NOTE]
> Als u geen een nauwkeurige toewijzing van al uw apps hebben en cloud services, kunt u Hallo Cloud App Discovery-hulpprogramma. Dit hulpprogramma kunt u uw IT-afdeling met zichtbaarheid van het bedrijf van uw organisatie en consumenten cloud-apps opgeven. Die het eenvoudiger dan ooit toodiscover shadow IT in uw organisatie, inclusief informatie over gebruikspatronen en alle gebruikers toegang tot uw cloudtoepassingen. Zie tooget gestart [Cloud app discovery](active-directory-cloudappdiscovery-whatis.md).
> 
> 

## <a name="evaluate-identity-integration-requirements"></a>Identity Integratievereisten evalueren
Vervolgens moet u tooevaluate Hallo identity Integratievereisten. Deze evaluatie is belangrijk toodefine Hallo technische vereisten voor hoe gebruikers worden geverifieerd, hoe de aanwezigheid van de organisatie Hallo eruitziet in Hallo cloud, hoe Hallo organisatie autorisatie wordt toegestaan en welke Hallo gebruikerservaring gaat toobe is. Zorg ervoor dat tooanswer Hallo vragen te volgen:

* Uw organisatie gebruikt federation-, standaard-verificatie of beide?
* Een vereiste voor Federatie is?  Vanwege de volgende Hallo:
  * Eenmalige aanmelding op basis van Kerberos
  * Uw bedrijf heeft een on-premises toepassingen (ofwel intern of 3e party gemaakt) die gebruikmaakt van SAML of vergelijkbare federation-mogelijkheden.
  * MFA via smartcards. RSA SecurID, enzovoort.
  * Toegangsregels voor clients die Hallo onderstaande vragen oplossen:
    1. Kan ik alle tooOffice voor externe toegang op basis van IP-adres Hallo van client Hallo 365 blokkeren?
    2. Kan ik alle externe toegang tooOffice 365, met uitzondering van Exchange ActiveSync blokkeren?
    3. Ik kan alle externe toegang tooOffice 365, met uitzondering van de browser gebaseerde apps (OWA, gesimuleerde Productieorder) blokkeren
    4. Ik kan alle externe toegang tooOffice 365 blokkeren voor leden van de aangewezen AD-groepen
* Beveiligingscontrole/problemen
* Al bestaande investeringen in federatieve verificatie
* Welke naam wordt onze organisatie gebruiken voor onze domein in de cloud Hallo?
* Heeft Hallo organisatie een aangepast domein?
  1. Is dat domein openbare en eenvoudig controleerbare via DNS?
  2. Als dit niet het geval is, klikt u vervolgens hebt u een openbaar domein die gebruikte tooregister een alternatieve UPN in AD kunnen worden?
* Hallo-id's, gelijk zijn voor weergave van de cloud? 
* Heeft Hallo organisatie apps die integratie met cloudservices vereist?
* Hallo organisatie beschikt over meerdere domeinen en alle standard of federatieve verificatie gebruikt?

## <a name="evaluate-applications-that-run-in-your-environment"></a>Toepassingen die worden uitgevoerd in uw omgeving te evalueren
Nu u een idee met betrekking tot uw on-premises hebt en cloud-infrastructuur, moet u tooevaluate Hallo toepassingen die worden uitgevoerd in deze omgevingen. Deze evaluatie is belangrijk toodefine Hallo technische vereisten toointegrate deze toepassingen toohello cloud identity management-systeem. Zorg ervoor dat tooanswer Hallo vragen te volgen:

* Waar wordt onze toepassingen woont?
* Krijgen gebruikers toegang tot on-premises toepassingen?  In de cloud Hallo? Of beide?
* Zijn er plannen tootake Hallo bestaande toepassing werklast en verplaatst u ze toohello cloud?
* Zijn er plannen toodevelop nieuwe toepassingen die zich on-premises bevinden of in Hallo cloud cloud-verificatie wordt gebruikt?

## <a name="evaluate-user-requirements"></a>Gebruikersvereisten evalueren
Hebt u ook de vereisten van de gebruiker Hallo tooevaluate. Deze evaluatie is belangrijk toodefine Hallo stappen die nodig zijn voor voor de twee locaties en gebruikers te helpen als ze toohello cloud overgang. Zorg ervoor dat tooanswer Hallo vragen te volgen:

* Krijgen gebruikers toegang tot toepassingen lokale?
* Krijgen gebruikers toegang tot toepassingen in de cloud Hallo?
* Hoe kan gebruikers meestal aanmelding tootheir on-premises omgeving?
* Hoe wordt gebruikers aanmelden toohello cloud?

> [!NOTE]
> Zorg ervoor dat tootake notities van elk antwoord en Hallo logica achter Hallo antwoord begrijpt. [Vereisten voor respons op incidenten bepalen](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md) gaat over het Hallo-opties die beschikbaar zijn en -professionals/nadelen van elke optie.  Moet door deze vragen die u selecteert welke optie het beste past bij uw bedrijf te beantwoorden.
> 
> 

## <a name="next-steps"></a>Volgende stappen
[Vereisten voor directory-synchronisatie bepalen](active-directory-hybrid-identity-design-considerations-directory-sync-requirements.md)

## <a name="see-also"></a>Zie ook
[Overzicht ontwerpoverwegingen](active-directory-hybrid-identity-design-considerations-overview.md)

