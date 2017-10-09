---
title: 'Azure Active Directory B2C: Aangepast beleid | Microsoft Docs'
description: Een onderwerp op Azure Active Directory B2C aangepast beleid
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 1ff398a4-2079-4615-94f1-57de22c0aad6
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/04/2017
ms.author: parakhj
ms.openlocfilehash: bada9cf5f1a86f3dd047536f6fd9359c0231a384
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-custom-policies"></a>Azure Active Directory B2C: Aangepast beleid

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

## <a name="what-are-custom-policies"></a>Wat zijn aangepast beleid?

Aangepaste beleidsregels zijn configuratiebestanden die Definieer Hallo gedrag van uw Azure AD B2C-tenant. Terwijl **ingebouwde beleid** zijn vooraf gedefinieerd in hello Azure AD B2C-portal voor hello meest algemene taken van identiteit, aangepaste beleidsregels kunnen volledig worden bewerkt door een identiteit developer toocomplete een bijna onbeperkt aantal taken. Lees verder toodetermine als aangepast beleid bij u en uw identiteitsscenario zijn.

**Aangepast beleid bewerken is niet voor iedereen.** Hallo leerproces is veeleisende, Hallo opstarttijd is langer en toekomstige wijzigingen toocustom beleid waarvoor vergelijkbare expertise toomaintain. Ingebouwde beleid moeten zorgvuldig worden overwogen eerst voor uw scenario voor het gebruik van aangepast beleid.

## <a name="comparing-built-in-policies-and-custom-policies"></a>Beleidsregels voor ingebouwde en aangepaste vergelijken

| | Ingebouwde beleid | aangepast beleid |
|-|-------------------|-----------------|
|Doelgebruikers | Alle app-ontwikkelaars met of zonder identiteit expertise | Identity-professionals: systeemintegrators, adviseurs en interne identiteit teams. Ze vertrouwd bent met OpenIDConnect stromen en id-providers en verificatie op basis van claims begrijpen |
|Configuratiemethode | Azure-portal met een gebruiksvriendelijke gebruikersinterface | XML-bestanden rechtstreeks te bewerken en vervolgens uploaden toohello Azure-portal |
|UI-aanpassing | Volledige aanpassing van de gebruikersinterface, zoals HTML, CSS en jscript-ondersteuning (aangepast domein vereist)<br><br>Meertalige ondersteuning met een aangepaste tekenreeks | Dezelfde |
| Kenmerk aanpassing | Standaard- en aangepaste kenmerken | Dezelfde |
|Token en sessie-management | Aangepaste token en meerdere sessie-opties | Dezelfde |
|ID-Providers| **Vandaag de dag**: vooraf gedefinieerde lokale, sociale provider<br><br>**Toekomstige**: SAML, van op standaarden gebaseerde OIDC OAuth | **Vandaag de dag**: OAUTH, van op standaarden gebaseerde OIDC SAML<br><br>**Toekomstige**: WsFed |
|Identiteit taken (voorbeelden) | Aanmelden of aanmelding met lokale en veel sociale accounts<br><br>Self-service voor wachtwoord opnieuw instellen<br><br>Profiel bewerken<br><br>Multi-factor Auth-scenario 's<br><br>Tokens en sessies aanpassen<br><br>Toegangstoken stroomt | Hallo dezelfde taken als ingebouwde beleidsregels met behulp van aangepaste identiteitsproviders voltooien of het gebruik van aangepaste bereiken<br><br>Inrichten gebruiker in een ander systeem op Hallo moment van inschrijving<br><br>Stuur een welkomstbericht via uw eigen e-provider<br><br>Gebruik een gebruikersarchief buiten B2C<br><br>Valideren van de gebruiker opgegeven informatie met een vertrouwde systeem via API |

## <a name="policy-files"></a>Beleidsbestanden

Een aangepast beleid wordt weergegeven als een of meer XML-bestanden die andere in een hiërarchische keten tooeach verwijzen. Hallo XML-elementen definiëren: Claims schema, claims transformaties, definities van inhoud, profielen van claims-providers en technische en Userjourney indelingsstappen, onder andere elementen.

Het wordt aangeraden de drie typen beleidsbestanden hello gebruiken:

- **Een BASE bestand**, die de meeste van Hallo definities en die Azure een compleet codevoorbeeld biedt bevat.  We raden dat u een minimum aantal wijzigingen toothis toohelp bij het oplossen van het bestand en op lange termijn onderhoud van uw beleid maken
- **een extensiebestand** die de unieke configuratiewijzigingen Hallo bevat voor uw tenant
- **een Relying Party (RP)-bestand** namelijk Hallo één taak gerichte bestand die wordt opgeroepen rechtstreeks door Hallo toepassing of service (aka Relying Party).  Lees artikel Hallo van beleid bestand definities voor meer informatie.  Elke unieke taak vereist een eigen RP en afhankelijk van de vereisten voor de huisstijl Hallo nummer mogelijk 'Totaal aantal toepassingen x totale aantal gevallen'.


Ingebouwde beleid in Azure AD B2C volgen Hallo bestand 3 patroon afgebeeld hierboven, maar Hallo developer alleen ziet Hallo Relying Party (RP)-bestand, terwijl het Hallo-portal worden wijzigingen aangebracht in Hallo achtergrond toohello Extensions bestanden.

## <a name="core-concepts-you-should-know-when-using-custom-policies"></a>Belangrijkste concepten waarover die u weten moet wanneer u aangepaste beleidsregels

### <a name="azure-active-directory-b2c"></a>Azure Active Directory B2C

Azure klant identiteits- en toegangsbeheer (CIAM) service management. Hallo-service omvat:

1. Een map van de gebruiker in Hallo vorm van een speciale Azure Active Directory toegankelijk zijn via Microsoft Graph en dat de gebruikersgegevens voor zowel lokale accounts als federatieve accounts bevat 
2. Toegang tot toohello **identiteit ervaring Framework** die vertrouwensrelatie tussen gebruikers en entiteiten ingedeeld en claims doorgegeven tussen deze twee toocomplete een beheertaak identiteit/toegang 
3. Een beveiligingstokenservice (STS) verlenen-id-tokens, vernieuwen tokens, en toegang tokens (en gelijkwaardige SAML asserties) en het valideren van tooprotect resources.

Azure AD B2C communiceert met de id-providers, gebruikers, andere systemen en met Hallo map voor de lokale gebruiker in de reeks tooachieve een taak identiteit (bijvoorbeeld aanmelden voor een gebruiker een nieuwe gebruiker registreren, een wachtwoord opnieuw instellen). Hallo onderliggende platform dat meerdere partijen vertrouwensrelatie te worden ingesteld en deze stappen worden uitgevoerd, heet Hallo identiteit ervaring Framework en een beleid (ook wel het traject van een gebruiker of een framework vertrouwensbeleid) expliciet definieert Hallo actoren, Hallo acties, hello protocollen en Hallo reeks stappen toocomplete.

### <a name="identity-experience-framework"></a>Identity-ervaringsframework

Een volledig worden geconfigureerd, beleid gebaseerde, cloud-gebaseerde Azure-platform die vertrouwensrelatie tussen entiteiten (grotendeels claimproviders) ingedeeld in standaardprotocol indelingen zoals OpenIDConnect OAuth, SAML, WSFed en enkele niet-standaard waarden (bijvoorbeeld REST-API gebaseerd systeem claims kunnen worden uitgewisseld). Hallo I2E maakt gebruiksvriendelijke, whitelabelled optreedt die ondersteuning voor HTML, CSS en jscript.  Vandaag de dag Hallo identiteit ervaring Framework is alleen beschikbaar in context Hallo Hallo Azure AD B2C-service en prioriteit voor de gerelateerde tooCIAM taken.

### <a name="built-in-policies"></a>Ingebouwde beleid

Vooraf gedefinieerde configuratiebestanden op dat direct Hallo gedrag van Azure AD B2C tooperform Hallo meest gebruikte identiteit taken (dat wil zeggen gebruikersregistratie, aanmelding, wachtwoord opnieuw instellen) en communiceren met vertrouwde partijen waarvan relatie ook vooraf is gedefinieerd in Azure AD B2C ( bijvoorbeeld Facebook id-provider, LinkedIn, Microsoft-Account, Google-accounts).  In toekomstige hello, kunnen ook ingebouwde beleidsregels bieden voor aanpassing van de id-providers die doorgaans in de enterprise-realm Hallo zoals Azure Active Directory Premium, Active Directory AD FS, Salesforce-ID-Provider, enzovoort.


### <a name="custom-policies"></a>aangepast beleid

De configuratiebestanden die Hallo gedrag van identiteit ervaring Framework in uw Azure AD B2C-tenant definiëren. Er is een aangepast beleid toegankelijk als een of meer XML-bestanden (Zie beleidsbestanden definities) die worden uitgevoerd door Hallo identiteit ervaring Framework wordt aangeroepen door een relying party (bijvoorbeeld een toepassing). Aangepaste beleidsregels kunnen worden rechtstreeks bewerkt door een identiteit developer toocomplete een bijna onbeperkt aantal taken. Ontwikkelaars configureren aangepast beleid moeten definiëren Hallo vertrouwde relaties in detail zorgvuldige tooinclude metagegevens-eindpunten, de exacte claims exchange-definities en certificaten, sleutels en geheimen naar wens door elke identiteitsprovider configureren.

## <a name="policy-file-definitions-for-identity-experience-framework-trustframeworks"></a>Beleid bestand definities voor de identiteit ervaring Framework Trustframeworks

### <a name="policy-files"></a>Beleidsbestanden

Een aangepast beleid wordt weergegeven als een of meer XML-bestanden die andere in een hiërarchische keten tooeach verwijzen. Hallo XML-elementen definiëren: Claims schema, claims transformaties, definities van inhoud, profielen van claims-providers en technische en Userjourney indelingsstappen, onder andere elementen.  Het wordt aangeraden de drie typen beleidsbestanden hello gebruiken:

- **Een BASE bestand**, die de meeste van Hallo definities en die Azure een compleet codevoorbeeld biedt bevat.  We raden dat u een minimum aantal wijzigingen toothis toohelp bij het oplossen van het bestand en op lange termijn onderhoud van uw beleid maken
- **een extensiebestand** die de unieke configuratiewijzigingen Hallo bevat voor uw tenant
- **een Relying Party (RP)-bestand** namelijk Hallo één taak gerichte bestand die wordt opgeroepen rechtstreeks door Hallo toepassing of service (aka Relying Party).  Lees artikel Hallo van beleid bestand definities voor meer informatie.  Elke unieke taak vereist een eigen RP en afhankelijk van de vereisten voor de huisstijl Hallo nummer mogelijk 'Totaal aantal toepassingen x totale aantal gevallen'.

![Beleid voor bestandstypen](media/active-directory-b2c-overview-custom/active-directory-b2c-overview-custom-policy-files.png)

| Bestand met beleidsregel van type | Voorbeelden bestandsnaam | Aanbevolen gebruik | Neemt over van |
|---------------------|--------------------|-----------------|---------------|
| BASE |TrustFrameworkBase.xml<br><br>Mytenant.onmicrosoft.com-B2C-1A_BASE1.xml | Bevat Hallo core claims schema, claimtransformaties, claimproviders en gebruiker trajecten geconfigureerd door Microsoft<br><br>Minimale wijzigingen toothis bestand maken | Geen |
| Extensie (EXT) | TrustFrameworkExtensions.xml<br><br>Mytenant.onmicrosoft.com-B2C-1A_EXT.xml | Uw wijzigingen toohello hier BASE bestand consolideren<br><br>Gewijzigde claimproviders<br><br>Gewijzigde gebruiker trajecten<br><br>Uw eigen aangepaste schemadefinities | BASE-bestand |
| Relying Party (RP) | B2C_1A_sign_up_sign_in.XML| Token vorm en sessie instellingen hier wijzigen| Extensions(ext) bestand |

### <a name="inheritance-model"></a>Overnamemodel

Wanneer een toepassing hello RP beleidsbestand aanroept, wordt Hallo identiteit ervaring Framework in B2C alle Hallo elementen toevoegen van BASE, en vervolgens van EXTENSIES en ten slotte van Hallo RP beleid bestand tooassemble Hallo huidige beleid van kracht.  Elementen van Hallo hetzelfde type en de naam in Hallo RP-bestand overschrijven die in Hallo UITBREIDINGEN en EXTENSIES onderdrukkingen BASE.

**Ingebouwde beleid** in Azure AD B2C Hallo bestand 3 patroon afgebeeld hierboven, maar Hallo developer alleen ziet Hallo Relying Party (RP)-bestand, terwijl het Hallo-portal worden wijzigingen aangebracht in Hallo achtergrond toohello Extensions bestanden volgen.  Alle Azure AD B2C deelt een BASE beleidsbestand dat wordt beheerd Hallo van hello Azure B2C-team en vaak wordt bijgewerkt.
