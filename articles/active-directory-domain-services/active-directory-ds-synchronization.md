---
title: 'Azure Active Directory Domain Services: Synchronisatie in beheerde domeinen | Microsoft Docs'
description: Inzicht in synchronisatie in een beheerd domein van Azure Active Directory Domain Services
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 57cbf436-fc1d-4bab-b991-7d25b6e987ef
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 9be25b61823a6b031906f3576395782e73831fc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="synchronization-in-an-azure-ad-domain-services-managed-domain"></a>Een beheerd domein van Azure AD Domain Services-synchronisatie
Hallo volgende diagram illustreert hoe synchronisatie werkt in Azure AD Domain Services beheerde domeinen.

![Synchronisatie-topologie in Azure AD Domain Services](./media/active-directory-domain-services-design-guide/sync-topology.png)

## <a name="synchronization-from-your-on-premises-directory-tooyour-azure-ad-tenant"></a>Synchronisatie van uw lokale directory tooyour Azure AD-tenant
Azure AD Connect-synchronisatie is gebruikte toosynchronize gebruikersaccounts, groepslidmaatschappen en referentie-hashes tooyour Azure AD-tenant. Kenmerken van een gebruiker zoals Hallo UPN-accounts en on-premises SID (security identifier) worden gesynchroniseerd. Als u Azure AD Domain Services gebruikt, zijn verouderde referentie-hashes voor NTLM en Kerberos-verificatie ook tooyour gesynchroniseerde Azure AD-tenant.

Als u terugschrijven configureert, kan veranderingen in uw Azure AD-directory back tooyour op lokale Active Directory worden gesynchroniseerd. Bijvoorbeeld, als u uw wachtwoord met Azure AD selfservice voor wachtwoordherstel wijziging functies wijzigen, Hallo gewijzigd wachtwoord is bijgewerkt in uw on-premises AD-domein.

> [!NOTE]
> Gebruik altijd de meest recente versie Hallo van Azure AD Connect tooensure u oplossingen voor alle bekende fouten hebben.
>
>

## <a name="synchronization-from-your-azure-ad-tenant-tooyour-managed-domain"></a>Synchronisatie van uw Azure AD-tenant tooyour beheerd domein
Accounts van gebruikers, groepslidmaatschappen en referentie-hashes worden gesynchroniseerd vanuit uw Azure AD-tenant tooyour beheerd domein van Azure AD Domain Services. Dit synchronisatieproces is automatisch. U hoeft geen tooconfigure, bewaken of beheren van dit synchronisatieproces. Nadat Hallo eenmalige initiële synchronisatie van uw adreslijst voltooid is, wordt doorgaans duurt ongeveer 20 minuten om de wijzigingen in Azure AD toobe weerspiegeld in uw beheerde domein. Deze synchronisatie-interval toopassword wijzigingen toepast of wijzigingen aangebracht in Azure AD tooattributes.

Hallo-synchronisatieproces is ook een-way/Unidirectioneel aard. Uw beheerde domein is grotendeels alleen-lezen, met uitzondering van eventuele aangepaste OE's die u maakt. Daarom kunt u niet wijzigingen toouser kenmerken, wachtwoorden of groepslidmaatschappen binnen Hallo beheerde domein. Als gevolg hiervan is er geen omgekeerde synchronisatie van wijzigingen in uw beheerde domein back-tooyour Azure AD-tenant.

## <a name="synchronization-from-a-multi-forest-on-premises-environment"></a>Synchronisatie van een forest met meerdere on-premises-omgeving
Veel organisaties hebben een relatief complex on-premises identity-infrastructuur die bestaan uit meerdere accountforests. Azure AD Connect ondersteunt het synchroniseren van gebruikers, groepen en referentie-hashes van omgevingen met meerdere forests tooyour Azure AD-tenant.

Uw Azure AD-tenant is daarentegen een veel eenvoudiger en platte naamruimte. tooenable gebruikers tooreliably toegang tot toepassingen worden beveiligd door Azure AD conflicten UPN tussen gebruikersaccounts in verschillende forests. Uw Azure AD Domain Services beheerd domein bears sluit gelijkenis tooyour Azure AD-tenant. Daarom ziet u een platte OE-structuur in uw beheerde domein. Alle gebruikers en groepen worden opgeslagen in container 'AADDC gebruikers' hello, ongeacht Hallo lokaal domein of forest waarin ze zijn gesynchroniseerd in. U hebt een hiërarchische OU geconfigureerd lokale structuur. Uw beheerde domein heeft echter nog steeds een eenvoudige platte OE-structuur.

## <a name="exclusions---what-isnt-synchronized-tooyour-managed-domain"></a>Uitsluitingen - wat niet wordt gesynchroniseerd tooyour beheerd domein
Hallo zijn volgende objecten of -kenmerken niet gesynchroniseerd tooyour Azure AD-tenant of tooyour beheerde domein:

* **Kenmerken uitgesloten:** u kunt ervoor kiezen tooexclude bepaalde kenmerken worden gesynchroniseerd tooyour Azure AD-tenant van uw lokale domein via Azure AD Connect. Deze uitgesloten kenmerken zijn niet beschikbaar in uw beheerde domein.
* **Groepsbeleid:** groepsbeleidsregels geconfigureerd in uw lokale domein zijn niet gesynchroniseerd tooyour beheerd domein.
* **SYSVOL-share:** op dezelfde manier Hallo inhoud van SYSVOL-share op uw lokale domein Hallo niet zijn gesynchroniseerd tooyour beheerd domein.
* **Computerobjecten:** computerobjecten voor computers die lid tooyour lokaal domein zijn niet gesynchroniseerd tooyour beheerd domein. Deze computers niet op een vertrouwensrelatie heeft met uw beheerde domein en alleen tooyour lokaal domein behoren. In uw beheerde domein vinden computerobjecten alleen voor computers die u hebt expliciet domein toohello domein beheerde.
* **SID-geschiedenis kenmerken voor gebruikers en groepen:** Hallo primaire gebruiker en primaire groeps-SID's van uw lokale domein zijn gesynchroniseerd tooyour beheerd domein. Bestaande SidHistory kenmerken voor gebruikers en groepen worden echter niet gesynchroniseerd vanuit uw lokale domein tooyour beheerde domein.
* **Organisatie-eenheden (OE) structuren:** organisatie-eenheden die zijn gedefinieerd in het domein van uw lokale tooyour beheerd domein niet synchroniseren. Er zijn twee ingebouwde OE's in uw beheerde domein. Uw beheerde domein heeft standaard een platte OE-structuur. U kunt echter te[een aangepaste organisatie-eenheid maken in uw beheerde domein](active-directory-ds-admin-guide-create-ou.md).

## <a name="how-specific-attributes-are-synchronized-tooyour-managed-domain"></a>Hoe specifieke kenmerken gesynchroniseerd tooyour beheerd domein worden
Hallo volgende tabel bevat enkele algemene kenmerken, en wordt beschreven hoe ze zijn gesynchroniseerd tooyour beheerd domein.

| Kenmerk in uw beheerde domein | Bron | Opmerkingen |
|:--- |:--- |:--- |
| UPN |De UPN-kenmerk van de gebruiker in uw Azure AD-tenant |Hallo-UPN-kenmerk van uw Azure AD-tenant is gesynchroniseerd als tooyour beheerd domein. Daarom is het meest betrouwbare manier toosign Hallo in tooyour beheerde domein met behulp van uw UPN. |
| SAMAccountName |Van de gebruiker mailNickname kenmerk in uw Azure AD-tenant of automatisch wordt gegenereerd |Hallo SAMAccountName kenmerk is afkomstig van Hallo mailNickname kenmerk in uw Azure AD-tenant. Als meerdere gebruikersaccounts Hallo dezelfde mailNickname kenmerk Hallo SAMAccountName is automatisch gegenereerd hebt. Als hello mailNickname of de UPN-voorvoegsel van de gebruiker meer dan 20 tekens, is Hallo SAMAccountName automatisch gegenereerde toosatisfy Hallo 20 maximum aantal tekens op SAMAccountName kenmerken. |
| Wachtwoorden |Het wachtwoord van uw Azure AD-tenant van gebruiker |Referentie-hashes voor NTLM of Kerberos-verificatie (ook wel aanvullende referenties) worden gesynchroniseerd vanuit uw Azure AD-tenant. Als uw Azure AD-tenant een gesynchroniseerde tenant is, worden deze referenties zijn afkomstig van het lokale domein. |
| Primaire gebruiker of groep SID |Automatisch gegenereerde |primaire SID voor gebruiker of groep accounts Hallo is automatisch gegenereerd in uw beheerde domein. Dit kenmerk komt niet overeen met de Hallo primaire gebruiker of groep-SID van het Hallo-object in uw on-premises AD-domein. Dit verschil is dat Hallo beheerd domein een andere SID-naamruimte dan uw lokale domein heeft. |
| SID-geschiedenis voor gebruikers en groepen |On-premises primaire gebruiker en groep-SID |Hallo SidHistory-kenmerk voor gebruikers en groepen in uw beheerde domein ingesteld toomatch Hallo bijbehorende primaire gebruiker of groep-SID in uw lokale domein. Deze functie helpt zorg lift-en-verschuiving van lokale toepassingen toohello beheerd domein eenvoudiger, omdat u geen toore ACL-resources hoeft. |

> [!NOTE]
> **Meld u aan de beheerde domein toohello Hallo UPN-indeling:** Hallo SAMAccountName kenmerk mogelijk automatisch wordt gegenereerd voor sommige gebruikersaccounts in uw beheerde domein. Als meerdere gebruikers hebben Hallo hetzelfde kenmerk voor mailNickname of gebruikers overmatig lange UPN voorvoegsels, Hallo SAMAccountName voor deze gebruikers kan worden automatisch wordt gegenereerd. Daarom is Hallo SAMAccountName-indeling (bijvoorbeeld ' CONTOSO100\joeuser') niet altijd een betrouwbare manier toosign in toohello domein. Gebruikers automatisch gegenereerde SAMAccountName kan afwijken van de UPN-voorvoegsel. Gebruik Hallo UPN-indeling (bijvoorbeeld 'joeuser@contoso100.com') toosign in toohello beheerd domein betrouwbaar.
>
>

### <a name="attribute-mapping-for-user-accounts"></a>Toewijzing van de kenmerken voor gebruikersaccounts
Hallo volgende tabel ziet u hoe specifieke kenmerken voor gebruikersobjecten in uw Azure AD-tenant gesynchroniseerd toocorresponding kenmerken in uw beheerde domein zijn.

| Gebruikerskenmerk in uw Azure AD-tenant | Gebruikerskenmerk in uw beheerde domein |
|:--- |:--- |
| accountEnabled |userAccountControl (sets of wist Hallo ACCOUNT_DISABLED bit) |
| city |L |
| Land |CO |
| Afdeling |Afdeling |
| Weergavenaam |Weergavenaam |
| facsimileTelephoneNumber |facsimileTelephoneNumber |
| Voornaam |Voornaam |
| Functie |titel |
| E-mail |E-mail |
| mailNickname |msDS-AzureADMailNickname |
| mailNickname |SAMAccountName (soms mogelijk automatisch gegenereerd) |
| mobiele |mobiele |
| object-id |msDS-AzureADObjectId |
| onPremiseSecurityIdentifier |SID-geschiedenis |
| passwordPolicies |userAccountControl (sets of wist Hallo DONT_EXPIRE_PASSWORD bit) |
| physicalDeliveryOfficeName |physicalDeliveryOfficeName |
| Postcode |Postcode |
| preferredLanguage |preferredLanguage |
| state |St |
| StreetAddress |StreetAddress |
| Achternaam |SN |
| telephoneNumber |telephoneNumber |
| UserPrincipalName |UserPrincipalName |

### <a name="attribute-mapping-for-groups"></a>Toewijzing van de kenmerken voor groepen
Hallo volgende tabel ziet u hoe specifieke kenmerken voor groepsobjecten in uw Azure AD-tenant gesynchroniseerd toocorresponding kenmerken in uw beheerde domein zijn.

| Kenmerk van de groep in uw Azure AD-tenant | Het kenmerk Group in uw beheerde domein |
|:--- |:--- |
| Weergavenaam |Weergavenaam |
| Weergavenaam |SAMAccountName (soms mogelijk automatisch gegenereerd) |
| E-mail |E-mail |
| mailNickname |msDS-AzureADMailNickname |
| object-id |msDS-AzureADObjectId |
| onPremiseSecurityIdentifier |SID-geschiedenis |
| securityenabled moet |groupType |

## <a name="objects-that-are-not-synchronized-tooyour-azure-ad-tenant-from-your-managed-domain"></a>Objecten die niet zijn gesynchroniseerd tooyour Azure AD-tenant van uw beheerde domein
Als in een voorgaande sectie van dit artikel wordt beschreven, vindt er geen synchronisatie van uw beheerde domein back-tooyour Azure AD-tenant. U kunt ervoor kiezen te[maken van een aangepaste organisatie-eenheid (OE)](active-directory-ds-admin-guide-create-ou.md) in uw beheerde domein. Bovendien kunt u andere organisatie-eenheden, gebruikers, groepen of serviceaccounts binnen deze aangepaste organisatie-eenheden. Geen Hallo-objecten die zijn gemaakt in aangepaste OE's gesynchroniseerd back tooyour Azure AD-tenant. Deze objecten zijn beschikbaar voor gebruik binnen uw beheerde domein. Deze objecten zijn daarom niet zichtbaar met behulp van Azure AD PowerShell-cmdlets, Azure AD Graph API of via de gebruikersinterface voor hello Azure AD-beheer.

## <a name="related-content"></a>Gerelateerde inhoud
* [Onderdelen - Azure AD Domain Services](active-directory-ds-features.md)
* [Implementatiescenario - Azure AD Domain Services](active-directory-ds-scenarios.md)
* [Overwegingen voor Azure AD Domain Services netwerken](active-directory-ds-networking.md)
* [Aan de slag met Azure AD Domain Services](active-directory-ds-getting-started.md)
