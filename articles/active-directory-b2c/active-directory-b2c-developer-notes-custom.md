---
title: 'Azure Active Directory B2C: Opmerkingen voor ontwikkelaars op het gebruik van aangepast beleid | Microsoft Docs'
description: Opmerkingen voor ontwikkelaars over het configureren en onderhouden van Azure AD B2C met aangepast beleid
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 05/05/2017
ms.author: joroja
ms.openlocfilehash: 979b8a264eb819ee4a208b9171a53a5ffbf062c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes-for-azure-active-directory-b2c-custom-policy-public-preview"></a>Releaseopmerkingen voor openbare preview van Azure Active Directory B2C aangepast beleid
Hallo functieset aangepast beleid is nu beschikbaar voor evaluatie onder public preview voor alle Azure Active Directory B2C (Azure AD B2C) klanten. Deze functieset is gericht op ontwikkelaars van geavanceerde identiteit Hallo meest complexe identiteitsoplossingen bouwen.  

Vandaag de dag, vereist deze functieset ontwikkelaars tooconfigure Hallo identiteit ervaring Framework rechtstreeks via XML-bestand bewerken. Deze methode van de configuratie is een krachtige en complexe. Geavanceerde identiteit ontwikkelaars met Hallo moet identiteit ervaring Framework plannen tooinvest enige tijd voor het voltooien van de zelfstudies en verwijzing naar documenten te lezen. 

## <a name="features-included-in-this-public-preview"></a>Functies in deze openbare preview
Hallo nieuwe functies geïntroduceerd in de openbare preview hello, kunnen ontwikkelaars Hallo volgende taken uitvoeren:<br>

* Maken en uploaden aangepaste verificatie gebruiker trajecten met behulp van aangepast beleid. 
   * Gebruikers reizen stapsgewijze als kunnen worden uitgewisseld tussen claimproviders beschrijven. 
   * Definieer Voorwaardelijke vertakkingen in trajecten van de gebruiker. 
* REST-API-diensten in uw aangepaste verificatie gebruiker trajecten worden geïntegreerd.  
* Federatie met de id-providers die compatibel met de Hallo OpenIDConnect standaard zijn toevoegen. <br>
* Toevoegen van Federatie met de id-providers die toohello SAML 2.0-protocol voldoen. 

## <a name="terms-of-hello-public-preview"></a>Gebruiksvoorwaarden Hallo openbare preview

* We raden u toouse Hallo nieuwe functies voor evaluatiedoeleinden.<br>
* De nieuwe functies zijn niet bedoeld voor gebruik in een productieomgeving.<br>
* Service level agreements (Sla) toohello nieuwe functies zijn niet van toepassing. <br>
* Ondersteuningsaanvragen kunnen worden ingediend via reguliere ondersteuningskanalen. <br>
* Er is geen toegezegde opgegeven voor algemene beschikbaarheid.<br>
* Onze goeddunken, en voor welke reden dan ook, kunt Microsoft markeren en weigeren of scenario's en gebruiker trajecten die groter is dan Hallo bereik van hello Azure AD B2C product Freelance tooserve als een klant identiteits- en toegangsbeheer (CIAM) beheerplatform beperken.

## <a name="responsibilities-of-custom-policy-feature-set-developers"></a>De verantwoordelijkheden van aangepast beleid functieset ontwikkelaars
Handmatige beleidsconfiguratie verleent toegang lager niveau toohello onderliggende platform van Azure AD B2C en resulteert in het Hallo maken van een unieke, volledig aanpasbare vertrouwensrelatie-framework. Het aantal mogelijke permutaties met aangepaste identiteitsproviders, vertrouwensrelaties, integraties met externe services en stapsgewijze werkstromen plaats hogere eisen op Hallo geavanceerde ontwikkelaars die ze gebruiken.

toofully voordeel van de openbare preview hello, het is raadzaam dat ontwikkelaars verbruikt Hallo aangepast beleid functieset toohello richtlijnen voldoen:
* Vertrouwd raken met de Hallo configuratie taal Hallo identiteit ervaring Engine en sleutel/geheimen management.
* Eigenaar worden van scenario's en aangepaste integraties.
* Methodisch scenariotests uitvoeren.
* Ga als volgt software ontwikkelings- en staging-best practices met ten minste één ontwikkelings- en testomgeving en een productie-omgeving.
* Blijf op de hoogte over nieuwe ontwikkelingen van Hallo id-providers en -services die u met integreert. Bijvoorbeeld: bijhouden van wijzigingen in geheimen en van geplande en ongeplande wijzigingen toohello service.
* Actieve bewaking hebt ingesteld en bewaak Hallo reactiesnelheid van productieomgevingen.
* Neem contact op met e-mailadressen actueel te houden en blijven responsief toohello Microsoft live-site-team e-mailberichten.
* Tijdige actie ondernemen als aanbevolen toodo Hallo van Microsoft-team voor live-site. 


>[!NOTE]
>Deze functies worden uiteindelijk misschien opgenomen in Azure AD ingebouwde beleid, zodat ze beter toegankelijk tooall ontwikkelaars.

## <a name="next-steps"></a>Volgende stappen
[Aan de slag met aangepaste beleidsregels](active-directory-b2c-get-started-custom.md).
