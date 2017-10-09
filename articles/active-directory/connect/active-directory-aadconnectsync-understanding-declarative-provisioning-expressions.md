---
title: 'Azure AD Connect: Expressies declaratieve inrichting | Microsoft Docs'
description: Hallo-expressies voor declaratieve inrichting uitgelegd.
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: e3ea53c8-3801-4acf-a297-0fb9bb1bf11d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 516bcf1991c608d33aefc19551254d8b2bfc024f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-understanding-declarative-provisioning-expressions"></a>Azure AD Connect-synchronisatie: inzicht declaratieve inrichting expressies
Azure AD Connect-synchronisatie is gebaseerd op het declaratieve inrichting is geïntroduceerd in Forefront Identity Manager 2010. Hiermee kunt u tooimplement bedrijfslogica op de identiteit van de volledige integratie zonder Hallo nodig toowrite gecompileerde code.

Een essentieel onderdeel van de declaratieve inrichting is Hallo expressie die wordt gebruikt in kenmerkstromen. Hallo-taal die wordt gebruikt, is een subset van Microsoft Visual Basic® for Applications (VBA). Deze taal wordt gebruikt in Microsoft Office en ook door gebruikers met de ervaring van VBScript wordt herkend. Hallo declaratieve inrichting expressietaal wordt alleen gebruikt voor functies en is niet een gestructureerde taal. Er zijn geen methoden of instructies. Functies in plaats daarvan zijn genest tooexpress programma stroom.

Zie voor meer informatie [toohello Visual Basic voor toepassingen Naslaggids voor Office 2013 Welkom](https://msdn.microsoft.com/library/gg264383.aspx).

Hallo kenmerken zijn sterk getypeerd. Een functie accepteert alleen de kenmerken van het juiste type Hallo. Het is ook hoofdlettergevoelig. Zowel functienamen en kenmerknamen moeten juiste hoofdlettergebruik of een fout gegenereerd.

## <a name="language-definitions-and-identifiers"></a>Taal definities en id 's
* Functies hebben een naam die wordt gevolgd door argumenten tussen vierkante haken: functienaam (argument 1, argument N).
* Kenmerken worden geïdentificeerd door vierkante haken: [attributeName]
* Parameters zijn geïdentificeerd door procenttekens: % ParameterName %
* Tekenreeksconstanten tussen aanhalingstekens worden geplaatst: bijvoorbeeld 'Contoso' (Opmerking: rechte aanhalingstekens moet gebruiken "" en niet slimme aanhalingstekens "")
* Numerieke waarden worden uitgedrukt zonder aanhalingstekens en verwachte toobe decimal. Hexadecimale waarden worden voorafgegaan door & H. Bijvoorbeeld, 98052 & HFF
* Boole-waarden worden uitgedrukt met constanten: True, False.
* Ingebouwde constanten en letterlijke waarden worden uitgedrukt met alleen de naam: NULL, CRLF, IgnoreThisFlow

### <a name="functions"></a>Functies
Declaratieve inrichting veel functies tooenable Hallo mogelijkheid tootransform kenmerkwaarden gebruikt. Deze functies kunnen worden genest zodat Hallo resultaat van een functie in de functie tooanother wordt doorgegeven.

`Function1(Function2(Function3()))`

Hallo volledige lijst met functies vindt u in Hallo [werken verwijzing](active-directory-aadconnectsync-functions-reference.md).

### <a name="parameters"></a>Parameters
Een parameter is gedefinieerd door een Connector of door een beheerder met behulp van PowerShell. Gewoonlijk bevatten waarden die afwijken van het systeem toosystem parameters, bijvoorbeeld de naam van de domeingebruiker Hallo HALLO hallo bevindt zich in. Deze parameters kunnen worden gebruikt in kenmerkstromen.

Hallo Active Directory-Connector opgegeven Hallo parameters voor binnenkomende synchronisatieregels te volgen:

| Parameternaam | Opmerking |
| --- | --- |
| Domain.Netbios |NetBIOS-indeling van Hallo domein dat momenteel wordt geïmporteerd, bijvoorbeeld FABRIKAMSALES |
| Domain.FQDN |FQDN-indeling van Hallo domein dat momenteel wordt geïmporteerd, bijvoorbeeld sales.fabrikam.com |
| Domain.LDAP |LDAP-indeling van Hallo domein dat momenteel wordt geïmporteerd, bijvoorbeeld DC = verkoop, DC = fabrikam, DC = com |
| Forest.Netbios |NetBIOS-indeling van Hallo forestnaam momenteel wordt geïmporteerd, bijvoorbeeld FABRIKAMCORP |
| Forest.FQDN |FQDN-indeling van Hallo forestnaam momenteel wordt geïmporteerd, bijvoorbeeld fabrikam.com |
| Forest.LDAP |LDAP-indeling van Hallo forestnaam momenteel wordt geïmporteerd, bijvoorbeeld DC = fabrikam, DC = com |

Hallo system biedt Hallo volgende parameter, die gebruikte tooget Hallo-id van Hallo Connector momenteel wordt uitgevoerd:  
`Connector.ID`

Hier volgt een voorbeeld waarin gevuld Hallo metaverse-kenmerk domein met Hallo NetBIOS-naam van het Hallo-domein waar de gebruiker Hallo zich bevindt:  
`domain` <- `%Domain.Netbios%`

### <a name="operators"></a>Operators
Hallo volgende operators kan worden gebruikt:

* **Vergelijking**: <, < =, <>, =, >, > =
* **Wiskunde**: +, -, \*, -
* **Tekenreeks**: & (samenvoegen)
* **Logische**: & & (en) || (of)
* **Evaluatievolgorde**:)

Operators geëvalueerde links tooright en Hallo hebben dezelfde prioriteit voor evaluatie. Dat wil zeggen, Hallo \* (vermenigvuldiger) wordt niet geëvalueerd vóór - (aftrekken). 2\*(5 + 3) is dezelfde niet als 2 Hallo\*5 + 3. Hallo vierkante haken () worden gebruikt toochange Hallo evaluatie bestellen als er geen evaluatievolgorde tooright niet juist.

## <a name="multi-valued-attributes"></a>Kenmerken met meerdere waarden
Hallo functies kunnen worden uitgevoerd op kenmerken van zowel één waarde en meerdere waarden. Voor meerdere waarden kenmerken Hallo functie werkt via elke waarde en is van toepassing hello dezelfde functie tooevery waarde.

Bijvoorbeeld:  
`Trim([proxyAddresses])`Voer een Trim van elke waarde in Hallo proxyAddress-kenmerk.  
`Word([proxyAddresses],1,"@") & "@contoso.com"`Voor elke waarde met een @-sign, vervang Hallo-domein met @contoso.com.  
`IIF(InStr([proxyAddresses],"SIP:")=1,NULL,[proxyAddresses])`Hallo SIP-adres zoeken en verwijderen uit het Hallo-waarden.

## <a name="next-steps"></a>Volgende stappen
* Lees meer over Hallo configuratiemodel in [Understanding declaratieve inrichting](active-directory-aadconnectsync-understanding-declarative-provisioning.md).
* Zie hoe declaratieve inrichting is gebruikte out of box in [Understanding Hallo standaardconfiguratie](active-directory-aadconnectsync-understanding-default-configuration.md).
* Zie hoe een praktisch toomake wijzigen met behulp van declaratieve inrichting [hoe een wijziging toohello toomake standaard configuratie](active-directory-aadconnectsync-change-the-configuration.md).

**Overzichtsonderwerpen**

* [Azure AD Connect-synchronisatie: inzicht en synchronisatie aanpassen](active-directory-aadconnectsync-whatis.md)
* [Uw on-premises identiteiten integreren met Azure Active Directory](active-directory-aadconnect.md)

**Onderwerpen met naslaginformatie**

* [Azure AD Connect-synchronisatie: functieverwijzing](active-directory-aadconnectsync-functions-reference.md)

