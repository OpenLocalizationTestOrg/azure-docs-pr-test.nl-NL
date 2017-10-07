---
title: 'Azure AD Domain Services: Vergelijken Azure AD Domain Services tooDIY domeincontrollers | Microsoft Docs'
description: Vergelijking van Azure Active Directory Domain Services tooDIY-domeincontrollers
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 165249d5-e0e7-4ed1-aa26-91a05a87bdc9
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: maheshu
ms.openlocfilehash: 5e384f6a676e76e4f22ff62d4aeb578bc8481ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodecide-if-azure-ad-domain-services-is-right-for-your-use-case"></a>Hoe toodecide als Azure AD Domain Services geschikt voor uw use case is
U kunt uw workloads in Azure Infrastructure Services implementeren zonder tooworry over het onderhoud van infrastructuur voor identiteiten in Azure met Azure AD Domain Services. Deze beheerde service wijkt af van een normale implementatie van Windows Server Active Directory die u implementeert en beheert zelf. Hallo-service is eenvoudig toodeploy en biedt een geautomatiseerde statuscontrole en herstel. We zijn voortdurend Hallo service tooadd-ondersteuning voor algemene implementatiescenario's in ontwikkeling.

toodecide of toouse Azure AD Domain Services aangeraden Hallo lezen materiaal te volgen:

* Hallo-overzicht van [functies die worden aangeboden door Azure AD Domain Services](active-directory-ds-features.md).
* Bekijk algemene [implementatiescenario's voor Azure AD Domain Services](active-directory-ds-scenarios.md).
* Ten slotte [vergelijken van Azure AD Domain Services tooa Doe AD optie](active-directory-ds-comparison.md#compare-azure-ad-domain-services-to-diy-ad-domain-in-azure).

## <a name="compare-azure-ad-domain-services-toodiy-ad-domain-in-azure"></a>Azure AD Domain Services tooDIY AD-domein in Azure vergelijken
Hallo kunt volgende tabel u kiezen tussen Azure AD Domain Services gebruiken en beheren van uw eigen AD-infrastructuur in Azure.

| **Functie** | **Azure AD Domain Services** | **'Doe' AD in virtuele machines in Azure** |
| --- |:---:|:---:|
| [**Beheerde service**](active-directory-ds-comparison.md#managed-service) |**&#x2713;** |**& #x 2715;** |
| [**Beveiligde implementaties**](active-directory-ds-comparison.md#secure-deployments) |**&#x2713;** |Toosecure hello implementatie moet de beheerder. |
| [**DNS-server**](active-directory-ds-comparison.md#dns-server) |**& #x 2713;**  (service beheerd) |**&#x2713;** |
| [**Domein- of Enterprise administrator-bevoegdheden**](active-directory-ds-comparison.md#domain-or-enterprise-administrator-privileges) |**& #x 2715;** |**&#x2713;** |
| [**Aan domein toevoegen**](active-directory-ds-comparison.md#domain-join) |**&#x2713;** |**&#x2713;** |
| [**Met behulp van NTLM en Kerberos-verificatie van domeinen**](active-directory-ds-comparison.md#domain-authentication-using-ntlm-and-kerberos) |**&#x2713;** |**&#x2713;** |
| [**Kerberos-beperkte overdracht**](active-directory-ds-comparison.md#kerberos-constrained-delegation)|op basis van bronnen|op basis van een resource & op basis van een account|
| [**Aangepaste OE-structuur**](active-directory-ds-comparison.md#custom-ou-structure) |**&#x2713;** |**&#x2713;** |
| [**Schema-uitbreidingen**](active-directory-ds-comparison.md#schema-extensions) |**& #x 2715;** |**&#x2713;** |
| [**AD-domein/forest vertrouwt**](active-directory-ds-comparison.md#ad-domain-or-forest-trusts) |**& #x 2715;** |**&#x2713;** |
| [**LDAP lezen**](active-directory-ds-comparison.md#ldap-read) |**&#x2713;** |**&#x2713;** |
| [**Beveiligde LDAP (LDAPS)**](active-directory-ds-comparison.md#secure-ldap) |**&#x2713;** |**&#x2713;** |
| [**LDAP-schrijven**](active-directory-ds-comparison.md#ldap-write) |**& #x 2715;** |**&#x2713;** |
| [**Groepsbeleid**](active-directory-ds-comparison.md#group-policy) |**&#x2713;** |**&#x2713;** |
| [**Geografisch verspreide implementaties**](active-directory-ds-comparison.md#geo-dispersed-deployments) |**& #x 2715;** |**&#x2713;** |

#### <a name="managed-service"></a>Beheerde service
Azure AD Domain Services-domeinen worden beheerd door Microsoft. U beschikt niet over tooworry over patchen, updates, bewaking, back-ups en beschikbaarheid van uw domein. Deze beheertaken worden aangeboden als een service door Microsoft Azure voor uw beheerde domeinen.

#### <a name="secure-deployments"></a>Beveiligde implementaties
Hallo beheerd domein is veilig volgens de aanbevelingen voor de beveiliging van Microsoft voor AD-implementaties vergrendeld. Deze aanbevelingen voortvloeien uit Hallo AD-productteam tientallen jaren ervaring engineering en de ondersteunende AD-implementaties. Doe implementaties, moet u de specifieke implementatie tootake stappen toolock omlaag/beveiligen van uw omgeving.

#### <a name="dns-server"></a>DNS-server
Een beheerd domein van Azure AD Domain Services omvat beheerde DNS-services. Leden van Hallo ' AAD DC' beheerdersgroep kunnen DNS op Hallo beheerd domein beheren. Leden van deze groep zijn volledige DNS-beheer bevoegdheden voor Hallo beheerde domein opgegeven. DNS-beheer kan worden uitgevoerd met behulp van Hallo 'DNS-beheerconsole' in hello Remote Server Administration Tools (RSAT) pakket opgenomen.
[Meer informatie](active-directory-ds-admin-guide-administer-dns.md)

#### <a name="domain-or-enterprise-administrator-privileges"></a>Domein- of Ondernemingsadministrator-bevoegdheden
Deze verhoogde bevoegdheden zijn niet beschikbaar op een beheerde AAD-DS-domein. Toepassingen waarvoor deze verhoogde bevoegdheden kunnen niet worden geïmplementeerd bij AAD DS beheerde domeinen. Een kleinere subset van beheerdersbevoegdheden is beschikbaar toomembers van Hallo gedelegeerd beheergroep 'AAD DC-beheerders' genoemd. Deze bevoegdheden opnemen bevoegdheden tooconfigure DNS-, Groepsbeleid configureren, krijgen administrator-bevoegdheden op domein machines enzovoort.

#### <a name="domain-join"></a>Aan domein toevoegen
U kunt deelnemen aan de virtuele machines toohello beheerd domein vergelijkbare toohow koppelen van computers tooan AD-domein.

#### <a name="domain-authentication-using-ntlm-and-kerberos"></a>Met behulp van NTLM en Kerberos-verificatie van domeinen
Met Azure AD Domain Services, kunt u uw zakelijke referenties tooauthenticate met Hallo beheerde domein. Referenties zijn gesynchroniseerd met uw Azure AD-tenant. Gesynchroniseerde tenants Azure AD Connect zorgt ervoor dat wijzigingen aangebracht toocredentials lokale gesynchroniseerde tooAzure AD. Met een configuratie voor doe domein, moet u mogelijk tooset van een domein AD-vertrouwensrelatie met uw on-premises AD voor tooauthenticate gebruikers met hun bedrijfsreferenties. Mogelijk moet u ook tooset van AD-replicatie tooensure dat wachtwoorden tooyour Azure domain controller virtuele machines synchroniseren.

#### <a name="kerberos-constrained-delegation"></a>Kerberos-beperkte overdracht
U hebt geen beheerder van domein bevoegdheden op een beheerd domein van Active Directory Domain Services. Daarom configureren u Kerberos-beperkte overdracht (Traditioneel) op basis van het account niet. U kunt echter veiliger Hallo configureren bronnen gebaseerde beperkte delegering.
[Meer informatie](active-directory-ds-enable-kcd.md)

#### <a name="custom-ou-structure"></a>Aangepaste OE-structuur
Leden van Hallo ' AAD DC' beheerdersgroep kunnen maken van aangepaste OE's binnen Hallo beheerd domein. Gebruikers die aangepaste OE's maken zijn volledige beheerdersrechten worden verleend via Hallo organisatie-eenheid.
[Meer informatie](active-directory-ds-admin-guide-create-ou.md)

#### <a name="schema-extensions"></a>Schema-uitbreidingen
U kunt de basisschema Hallo van een beheerd domein van Azure AD Domain Services niet uitbreiden. Toepassingen die afhankelijk van extensies tooAD schema (bijvoorbeeld nieuwe kenmerken onder Hallo gebruikersobject zijn) kunnen niet worden opgeheven en daarom verplaatst tooAAD DS-domeinen.

#### <a name="ad-domain-or-forest-trusts"></a>AD-domein of Forest-vertrouwensrelaties
Beheerde domeinen niet geconfigureerde tooset van vertrouwensrelaties (binnenkomend en uitgaand) met andere domeinen. Daarom resource forest implementatiescenario's Azure AD Domain Services niet gebruiken. Implementaties waarbij u liever niet toosynchronize wachtwoorden tooAzure AD niet op dezelfde manier Azure AD Domain Services gebruiken.

#### <a name="ldap-read"></a>LDAP lezen
Hallo beheerd domein ondersteunt LDAP lezen werkbelastingen. Daarom kunt u toepassingen waarmee leesbewerkingen op basis van het beheerde domein Hallo LDAP implementeren.

#### <a name="secure-ldap"></a>Beveiligde LDAP
U kunt Azure AD Domain Services tooprovide beveiligde LDAP toegang tooyour is beheerd domein, met inbegrip van via internet Hallo.
[Meer informatie](active-directory-ds-admin-guide-configure-secure-ldap.md)

#### <a name="ldap-write"></a>LDAP-schrijven
Hallo beheerde domein is alleen-lezen voor gebruikersobjecten. Toepassingen die LDAP schrijfbewerkingen op basis van kenmerken van het gebruikersobject Hallo uitvoeren werkt daarom niet in een beheerd domein. Bovendien kunnen niet wachtwoorden van gebruikers worden gewijzigd in Hallo beheerd domein. Een ander voorbeeld is de wijziging van groepslidmaatschappen of kenmerken binnen Hallo beheerde domein, dit is niet toegestaan. Eventuele wijzigingen toouser kenmerken of wachtwoorden die zijn aangebracht in Azure AD (via PowerShell/Azure-portal) of on-premises AD worden gesynchroniseerd toohello AAD-DS beheerd domein.

#### <a name="group-policy"></a>Groepsbeleid
Er is een ingebouwde GPO elke voor Hallo 'AADDC Computers' en 'AADDC gebruikers' containers. U kunt deze ingebouwde groepsbeleidsobjecten tooconfigure Groepsbeleid aanpassen. Leden van Hallo ' AAD DC' beheerdersgroep kunnen ook aangepaste groepsbeleidsobjecten maken, en koppel deze tooexisting OE's (met inbegrip van aangepaste OE's).
[Meer informatie](active-directory-ds-admin-guide-administer-group-policy.md)

#### <a name="geo-dispersed-deployments"></a>Geografisch verspreide implementaties
Azure AD Domain Services beheerde domeinen zijn beschikbaar in één virtueel netwerk in Azure. Voor scenario's die beschikbaar domain controllers toobe in meerdere Azure-regio's op Hallo wereld vereisen, instellen van domeincontrollers in Azure IaaS VM's is mogelijk beter alternatief Hallo.


## <a name="do-it-yourself-diy-ad-deployment-options"></a>'Doe' (DIY) AD-implementatieopties
Mogelijk hebt u gebruiksvoorbeelden implementatie hier moet u enkele van Hallo-functies die worden aangeboden door een Windows Server AD-installatie. Overweeg een Hallo volgend Doe (DIY)-opties in deze gevallen:

* **Zelfstandig cloud domein:** kunt u een zelfstandige cloud domein' gebruik van Azure virtuele machines die zijn geconfigureerd als domeincontrollers instellen. Deze infrastructuur is niet geïntegreerd met uw on-premises AD-omgeving. Deze optie vereist een andere set 'cloud referenties' toologin/beheren van virtuele machines in de cloud Hallo.
* **Implementatie van de bron-forest:** u kunt een domein instellen in Hallo resource foresttopologie gebruik van Azure virtuele machines die zijn geconfigureerd als domeincontroller. Vervolgens kunt u een AD-vertrouwensrelatie configureren met uw on-premises AD-omgeving. U kunt computers (Azure VM's) toothis bron-forest in de cloud Hallo lid van een domein. Gebruikersverificatie gebeurt via ofwel een VPN-en ExpressRoute-verbinding tooyour on-premises adreslijst.
* **Uitbreiden van uw lokale domein tooAzure:** u verbinding kunt maken van een virtuele Azure-netwerk tooyour on-premises netwerk via een VPN-en ExpressRoute-verbinding. Met deze instelling kunt u virtuele Azure-machines toobe gekoppelde tooyour on-premises AD dat. Een ander alternatief is toopromote replicadomeincontrollers van uw lokale domein in Azure als een virtuele machine. U kunt vervolgens deze functie tooreplicate instellen via een VPN-en ExpressRoute-verbinding tooyour on-premises adreslijst. Deze implementatiemodus breidt effectief uw lokale domein tooAzure.

> [!NOTE]
> U wordt bepaald door een optie voor ZELFOPLOSSING is beter geschikt voor use cases in uw implementatie. Houd rekening met [delen feedback](active-directory-ds-contact-us.md) toohelp ons inzicht in hoe functies kunt u in toekomstige hello Azure AD Domain Services hebt gekozen. Deze feedback kunnen we evolueren Hallo service toobetter gesorteerde die uw implementatie moet en use cases.
>
>

We hebben gepubliceerd [richtlijnen voor het implementeren van Windows Server Active Directory op Azure Virtual Machines](https://msdn.microsoft.com/library/azure/jj156090.aspx) toohelp eenvoudiger ZELFOPLOSSING installaties.

## <a name="related-content"></a>Gerelateerde inhoud
* [Onderdelen - Azure AD Domain Services](active-directory-ds-features.md)
* [Implementatiescenario - Azure AD Domain Services](active-directory-ds-scenarios.md)
* [Richtlijnen voor het implementeren van Windows Server Active Directory op virtuele Machines in Azure](https://msdn.microsoft.com/library/azure/jj156090.aspx)
