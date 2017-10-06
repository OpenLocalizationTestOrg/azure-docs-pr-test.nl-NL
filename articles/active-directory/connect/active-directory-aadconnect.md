---
title: Active Directory verbinden met Azure Active Directory. | Microsoft Docs
description: "Azure AD Connect integreert uw on-premises directory's met Azure Active Directory. Hiermee kunt u een algemene identiteit voor Office 365, Azure en SaaS toepassingen die zijn geïntegreerd met Azure AD tooprovide."
keywords: Inleiding tooAzure AD Connect, overzicht van Azure AD Connect, wat is Azure AD Connect, active directory installeren
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 59bd209e-30d7-4a89-ae7a-e415969825ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: e49f2af4b67e9ed3ad093888541da7c82af0e052
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-your-on-premises-directories-with-azure-active-directory"></a>Uw on-premises directory's integreren met Azure Active Directory
Azure AD Connect integreert uw on-premises directory's met Azure Active Directory. Hiermee kunt u een algemene identiteit voor uw gebruikers voor Office 365, Azure en SaaS toepassingen die zijn geïntegreerd met Azure AD tooprovide. In dit onderwerp leidt u door het Hallo-planning, implementatie en bewerking besproken. Er is een verzameling van koppelingen toohello onderwerpen gerelateerde toothis gebied.

> [!IMPORTANT]
> [Azure AD Connect is Hallo aanbevolen manier tooconnect uw on-premises directory met Azure AD en Office 365. Dit is een fantastische tijd tooupgrade tooAzure AD Connect van Windows Azure Active Directory-synchronisatie (DirSync) of Azure AD Sync omdat deze hulpprogramma's zijn nu afgeschaft en zal bereiken op 13 April 2017 ondersteuning eindigt.](active-directory-aadconnect-dirsync-deprecated.md)
> 
> 

![Wat is Azure AD Connect?](media/active-directory-aadconnect/arch.png)

## <a name="why-use-azure-ad-connect"></a>Waarom Azure AD Connect gebruiken?
Wanneer u uw on-premises directory's integreert met Azure AD, worden uw gebruikers productiever omdat zij één identiteit hebben voor toegang tot zowel resources in de cloud als on-premises. Gebruikers en organisaties profiteren van de volgende Hallo:

* Gebruikers met een één identiteit tooaccess on-premises toepassingen en cloudservices zoals Office 365.
* Eén hulpprogramma tooprovide een gemakkelijke implementatie-ervaring voor synchronisatie en aanmelden.
* Biedt de nieuwste mogelijkheden Hallo voor uw scenario's. Azure AD Connect vervangt oudere versies van hulpprogramma's voor identiteitsintegratie zoals DirSync en Azure AD Sync. Zie voor meer informatie [Vergelijking hybride hulpprogramma’s voor identiteitsdirecory-integratie ](../active-directory-hybrid-identity-design-considerations-tools-comparison.md).

### <a name="how-azure-ad-connect-works"></a>Hoe Azure AD werkt
Azure Active Directory Connect bestaat uit drie primaire onderdelen: Synchronisatieservices Hallo Hallo optioneel Active Directory Federation Services-onderdeel en Hallo bewakingsonderdeel [Azure AD Connect Health](../connect-health/active-directory-aadconnect-health.md) .

<center>![Azure AD Connect Stack](./media/active-directory-aadconnect-how-it-works/AADConnectStack2.png)
</center>

* Synchronisatie : met dit onderdeel worden gebruikers, groepen en andere objecten aangemaakt. Het is ook om te controleren of Hallo cloud komt overeen met de gegevens van de identiteit voor uw on-premises gebruikers en groepen.
* AD FS - federatie is een optioneel onderdeel van Azure AD Connect en kan gebruikte tooconfigure een hybride omgeving met een on-premises AD FS-infrastructuur. Dit kan worden gebruikt door organisaties tooaddress complexe implementaties, zoals domeindeelname SSO, afdwinging van AD-aanmelden-beleid, en smartcard of 3e partij MFA.
* Statusbewaking - Azure AD Connect Health kan goede bewaking en een centrale locatie in Azure portal tooview Hallo bieden deze activiteit. Zie voor meer informatie [Azure Active Directory Connect Health](../connect-health/active-directory-aadconnect-health.md).

## <a name="install-azure-ad-connect"></a>Azure AD Connect installeren
U vindt Hallo downloaden voor Azure AD Connect op [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=615771).

| Oplossing | Scenario |
| --- | --- |
| Voordat u begint - [hardware- en vereisten](active-directory-aadconnect-prerequisites.md) |<li>Stappen toocomplete voordat u begint met tooinstall Azure AD Connect.</li> |
| [Snelle instellingen](active-directory-aadconnect-get-started-express.md) |<li>Als u één AD-forest vervolgens dit Hallo verdient optie toouse.</li> <li>Gebruiker meld u aan met Hallo dezelfde wachtwoorden met Wachtwoordsynchronisatie.</li> |
| [Aangepaste instellingen](active-directory-aadconnect-get-started-custom.md) |<li>Wordt gebruikt wanneer u meerdere forests hebt. Ondersteunt vele on-premises [topologieën](active-directory-aadconnect-topologies.md).</li> <li>Pas uw aanmeldingsoptie aan zoals ADFS voor federatie of gebruik een externe identiteitsprovider.</li> <li>Synchronisatiefuncties, zoals filteren en terugschrijven, aanpassen.</li> |
| [Upgraden van DirSync](active-directory-aadconnect-dirsync-upgrade-get-started.md) |<li>Wordt gebruikt wanneer u een bestaande DirSync-server hebt die al actief is.</li> |
| [Upgraden van Azure AD Sync of Azure AD Connect](active-directory-aadconnect-upgrade-previous-version.md) |<li>Er zijn verschillende methoden, afhankelijk van uw voorkeur.</li> |

[Na de installatie](active-directory-aadconnect-whats-next.md) moet u controleren of deze werkt zoals verwacht en licenties toewijzen toohello gebruikers.

### <a name="next-steps-tooinstall-azure-ad-connect"></a>Volgende stappen tooInstall Azure AD Connect
|Onderwerp |Koppeling|  
| --- | --- |
|Azure AD Connect downloaden | [Azure AD Connect downloaden](http://go.microsoft.com/fwlink/?LinkId=615771)|
|Installeren met behulp van snelle instellingen | [Snelle installatie van Azure AD Connect](./active-directory-aadconnect-get-started-express.md)|
|Installeren met behulp van aangepaste instellingen | [Aangepaste installatie van Azure AD Connect](./active-directory-aadconnect-get-started-custom.md)|
|Upgraden van DirSync | [Upgraden van Azure AD-synchronisatiehulpprogramma (DirSync)](./active-directory-aadconnect-dirsync-upgrade-get-started.md)|
|Na installatie | [Hallo-installatie verifiëren en licenties toewijzen](active-directory-aadconnect-whats-next.md)|

### <a name="learn-more-about-install-azure-ad-connect"></a>Meer informatie over Azure AD Connect installeren
Wilt u er ook tooprepare voor [operationele](active-directory-aadconnectsync-operations.md) problemen. U kunt toohave een stand-by-server zodat u eenvoudig terug vallen kunt in als er een [na noodgevallen](active-directory-aadconnectsync-operations.md#disaster-recovery). Als u van plan frequente configuratiewijzigingen van toomake bent, moet u plannen voor een [faseringsmodus](active-directory-aadconnectsync-operations.md#staging-mode) server.

|Onderwerp |Koppeling|  
| --- | --- |
|Ondersteunde topologieën | [Topologieën voor Azure AD Connect](active-directory-aadconnect-topologies.md)|
|Ontwerpconcepten | [Ontwerpconcepten van Azure AD Connect](active-directory-aadconnect-design-concepts.md)|
|Accounts die worden gebruikt voor installatie | [Meer informatie over referenties en machtigingen van Azure AD Connect](./active-directory-aadconnect-accounts-permissions.md)|
|Operationele planning | [Azure AD Connect-synchronisatie: operationele taken en overwegingen](active-directory-aadconnectsync-operations.md)|
|Opties aanmelden gebruiker | [Opties van Azure AD Connect voor het aanmelden van gebruikers](active-directory-aadconnect-user-signin.md)|

## <a name="configure-sync-features"></a>Synchronisatie-functies configureren
Azure AD Connect wordt geleverd met verschillende functies die u in of uit kunt schakelen of die standaard zijn ingesteld. Sommige functies vereisen mogelijk meer configuratie in bepaalde scenario's en topologieën.

[Filteren](active-directory-aadconnectsync-configure-filtering.md) wordt gebruikt als u wilt dat toolimit welke objecten zijn tooAzure AD gesynchroniseerd. Alle gebruikers, contactpersonen, groepen en Windows 10-computers worden standaard gesynchroniseerd. U kunt wijzigen Hallo filteren op basis van domeinen, OE's of kenmerken.

[Wachtwoordsynchronisatie](active-directory-aadconnectsync-implement-password-synchronization.md) Hallo wachtwoordhash in Active Directory tooAzure AD synchroniseert. Hallo eindgebruikers kunt Hallo hetzelfde wachtwoord on-premises en in de cloud Hallo maar alleen beheren op één locatie te gebruiken. Omdat deze gebruikmaakt van uw lokale Active Directory als Hallo-instantie, kunt u ook uw eigen wachtwoordbeleid gebruiken.

[Wachtwoord terugschrijven](../active-directory-passwords-getting-started.md) uw toochange gebruikers toestaan en hun wachtwoorden in de cloud Hallo opnieuw instellen en hebt u uw lokale wachtwoordbeleid dat wordt toegepast.

[Apparaat terugschrijven](active-directory-aadconnect-feature-device-writeback.md) kan een apparaat is geregistreerd in Azure AD-toobe geschreven tooon lokale Active Directory zodat deze kan worden gebruikt voor voorwaardelijke toegang.

Hallo [onopzettelijk verwijderen voorkomen](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md) functie is standaard ingeschakeld en beschermt uw clouddirectory tegen meerdere verwijderingen op Hallo hetzelfde moment. Er kunnen standaard 500 verwijderingen per keer gedaan worden. U kunt deze instelling wijzigen, afhankelijk van de grootte van uw organisatie.

[Automatische upgrade](active-directory-aadconnect-feature-automatic-upgrade.md) is standaard ingeschakeld voor installaties van snelle instellingen en zorgt ervoor dat uw Azure AD Connect is altijd toodate met de meest recente release Hallo.

### <a name="next-steps-tooconfigure-sync-features"></a>Volgende stappen tooconfigure synchronisatie-functies
|Onderwerp |Koppeling|  
| --- | --- |
|Filtering configureren | [Azure AD Connect-synchronisatie: filtering configureren](active-directory-aadconnectsync-configure-filtering.md)|
|Wachtwoordsynchronisatie | [Azure AD Connect-synchronisatie: wachtwoordsynchronisatie implementeren](active-directory-aadconnectsync-implement-password-synchronization.md)|
|Wachtwoord terugschrijven | [Aan de slag met wachtwoordbeheer](../active-directory-passwords-getting-started.md)|
|Apparaat terugschrijven | [Apparaat terugschrijven inschakelen in Azure AD Connect](active-directory-aadconnect-feature-device-writeback.md)|
|Onopzettelijke verwijderingen voorkomen | [Azure AD Connect-synchronisatie: onopzettelijke verwijderingen voorkomen](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md)|
|Automatische upgrade | [Azure AD Connect: automatische upgrade](active-directory-aadconnect-feature-automatic-upgrade.md)|

## <a name="customize-azure-ad-connect-sync"></a>Azure AD Connect-synchronisatie aanpassen
Azure AD Connect-synchronisatie wordt geleverd met een standaardconfiguratie die beoogde toowork voor de meeste klanten en topologieën. Maar er zijn altijd situaties waarin de standaardconfiguratie Hallo werkt niet en moet worden aangepast. Is het ondersteunde toomake wijzigingen gedaan worden zoals beschreven in deze sectie en gekoppelde onderwerpen.

Als u nog niet eerder met een synchronisatie-topologie voordat u toostart toounderstand Hallo basisbeginselen wilt en voorwaarden zoals beschreven in Hallo Hallo [technische concepten](active-directory-aadconnectsync-technical-concepts.md). Azure AD Connect is Hallo ontwikkeling van MIIS2003, ILM2007 en FIM 2010. Zelfs als er dingen identiek zijn, is er ook veel gewijzigd.

Hallo [standaardconfiguratie](active-directory-aadconnectsync-understanding-default-configuration.md) wordt ervan uitgegaan dat er mogelijk meer dan één forest in Hallo-configuratie. In deze topologieën kan een gebruikersobject worden weergegeven als een contactpersoon in een andere forest. Hallo gebruiker mogelijk ook een gekoppeld postvak in een andere bron-forest. Hallo-gedrag van de standaardconfiguratie hello wordt beschreven in [gebruikers en contactpersonen](active-directory-aadconnectsync-understanding-users-and-contacts.md).

gesynchroniseerde Hallo configuratiemodel heet [declaratieve inrichting](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md). Hallo geavanceerde kenmerkstromen gebruiken [functies](active-directory-aadconnectsync-functions-reference.md) tooexpress kenmerk transformaties. U kunt zien en Hallo gehele configuratie controleren met de hulpprogramma's die wordt geleverd met Azure AD Connect. Als u configuratiewijzigingen toomake nodig hebt, controleert u of u volgt Hallo [aanbevolen procedures](active-directory-aadconnectsync-best-practices-changing-default-configuration.md) dus is het eenvoudiger tooadopt nieuwe releases.

### <a name="next-steps-toocustomize-azure-ad-connect-sync"></a>Volgende stappen toocustomize Azure AD Connect-synchronisatie
|Onderwerp |Koppeling|  
| --- | --- |
|Alle artikelen over Azure AD Connect-synchronisatie | [Azure AD Connect-synchronisatie](active-directory-aadconnectsync-whatis.md)|
|Technische concepten | [Azure AD Connect-synchronisatie: technische concepten](active-directory-aadconnectsync-technical-concepts.md)|
|Understanding Hallo standaardconfiguratie | [Azure AD Connect-synchronisatie: inzicht Hallo standaardconfiguratie](active-directory-aadconnectsync-understanding-default-configuration.md)|
|Inzicht krijgen in gebruikers en contactpersonen | [Azure AD Connect-synchronisatie: inzicht krijgen in gebruikers en contactpersonen](active-directory-aadconnectsync-understanding-users-and-contacts.md)|
|Declaratieve inrichting | [Azure AD Connect-synchronisatie: inzicht krijgen in expressies declaratieve inrichting](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md)|
|Hallo standaard-configuratie wijzigen | [Aanbevolen procedures voor het wijzigen van de standaardconfiguratie Hallo](active-directory-aadconnectsync-best-practices-changing-default-configuration.md)|

## <a name="configure-federation-features"></a>Federatiekenmerken configureren
ADFS kan worden geconfigureerd toosupport [meerdere domeinen](active-directory-aadconnect-multiple-domains.md). Stel dat u hebt meerdere populaire domeinen, moet u toouse voor Federatie.

Als uw ADFS-server niet geconfigureerd tooautomatically update certificaten van Azure AD is of als u een niet-ADFS-oplossing, klikt u wordt gewaarschuwd wanneer er te[certificaten bijwerken](active-directory-aadconnect-o365-certs.md).

### <a name="next-steps-tooconfigure-federation-features"></a>Volgende stappen tooconfigure Federatie-functies
|Onderwerp |Koppeling|  
| --- | --- |
|Alle AD FS-artikelen | [Azure AD Connect en federatie](active-directory-aadconnectfed-whatis.md)|
|ADFS configureren met subdomeinen | [Ondersteuning voor meerdere domeinen voor federatie met Azure AD](active-directory-aadconnect-multiple-domains.md)|
|AD FS-farm beheren | [AD FS-beheer en aanpassingen met Azure AD Connect](active-directory-aadconnect-federation-management.md)|
|Handmatig bijwerken van de federatiecertificaten | [Federatiecertificaten vernieuwen voor Office 365 en Azure AD](active-directory-aadconnect-o365-certs.md)|

## <a name="more-information-and-references"></a>Meer informatie en verwijzingen
|Onderwerp |Koppeling|  
| --- | --- |
|Versiegeschiedenis | [Versiegeschiedenis](active-directory-aadconnect-version-history.md)|
|Vergelijk DirSync Azure, ADSync en Azure AD Connect | [Hulpprogramma's voor vergelijking van adreslijstintegratie](../active-directory-hybrid-identity-design-considerations-tools-comparison.md)|
|Niet-ADFS compatibiliteitslijst voor Azure AD | [Compatibiliteitslijst voor Azure AD-federatie](active-directory-aadconnect-federation-compatibility.md)|
|Configureren van een SAML 2.0 Idp|[Een SAML 2.0-id-provider (IdP) gebruiken voor eenmalige aanmelding](active-directory-aadconnect-federation-saml-idp.md)|
|Gesynchroniseerde kenmerken | [Gesynchroniseerde kenmerken](active-directory-aadconnectsync-attributes-synchronized.md)|
|Bewaken met behulp van Azure AD Connect Health | [Azure AD Connect Health (Engelstalig)](../connect-health/active-directory-aadconnect-health.md)|
|Veelgestelde vragen | [Veelgestelde vragen over Azure AD Connect](active-directory-aadconnect-faq.md)|

**Aanvullende resources**

Ignite 2015-presentatie over het uitbreiden van uw lokale mappen toohello cloud.

> [!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3862/player]
> 
> 

