---
title: ontwerpoverwegingen voor aaaAzure Active Directory hybride identiteit - strategie voor hybride identity lifecycle ingebruikname bepalen | Microsoft Docs
description: "Helpt bij het definiëren van Hallo hybride identiteit beheertaken volgens toohello opties die beschikbaar zijn voor elke fase van de levenscyclus."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: 420b6046-bd9b-4fce-83b0-72625878ae71
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 86ec0a9896f069bc93e49e06006954848f8e4d48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="determine-hybrid-identity-lifecycle-adoption-strategy"></a>Hybride identity lifecycle acceptatie strategie bepalen
In deze taak definieert u Hallo-strategie voor het beheer van identiteiten voor hybride identiteit toomeet Hallo zakelijke vereisten van uw oplossing die u hebt gedefinieerd in [beheertaken voor hybride identiteit bepalen](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md).

toodefine hello hybride identiteit beheertaken volgens toohello end-to-end-identity lifecycle die eerder in deze stap worden gepresenteerd, hebt u tooconsider Hallo opties die beschikbaar zijn voor elke fase van de levenscyclus.

## <a name="access-management-and-provisioning"></a>Toegang tot beheer en inrichting
Met een beheersysteem goede account toegang tot kunt uw organisatie bijhouden nauwkeurig die toegang tot toowhat informatie binnen de organisatie Hallo heeft.

Toegangsbeheer is een kritieke functie van een gecentraliseerde, één punt inrichting systeem. Naast het beveiligen van vertrouwelijke gegevens zichtbaar toegangsbeheer bestaande accounts met niet-goedgekeurde autorisaties of zijn niet meer nodig. verouderd toocontrol-accounts, Hallo inrichting koppelingen samen systeemgegevens met gezaghebbende informatie over het Hallo-gebruikers die eigenaar Hallo-accounts. Identiteitsgegevens van gemachtigde gebruikers worden meestal onderhouden in Hallo-databases en mappen van human resources.

Accounts in geavanceerde IT-bedrijven honderden parameters die Hallo instanties definiëren bevatten en deze gegevens kunnen worden beheerd door uw provisioning-systeem. Nieuwe gebruikers kunnen worden geïdentificeerd met Hallo-gegevens die u van de gezaghebbende bron Hallo opgeeft. Hallo toegang aanvraag goedkeuring mogelijkheid initieert Hallo processen die worden ingericht voor deze resource goedkeuren (of weigeren).

| Fase van de levenscyclus | On-premises | Cloud | Hybride |
| --- | --- | --- | --- |
| Accountbeheer en inrichting |Met behulp van Active Directory® Domain Services (AD DS)-serverfunctie hello, kunt u een schaalbare, veilige en beheerbare infrastructuur maken voor gebruikers- en resourcebeheer en ondersteuning bieden voor Active directory-toepassingen zoals Microsoft® Exchange Server. <br><br> [U kunt groepen in AD DS, via een Identity manager inrichten](https://technet.microsoft.com/library/ff686261.aspx) <br>[U kunt gebruikers in AD DS inrichten](https://technet.microsoft.com/library/ff686263.aspx) <br><br> Beheerders kunnen access control toomanage gebruiker toegang tot tooshared bronnen gebruiken om beveiligingsredenen. In Active Directory en toegangsbeheer op Hallo objectniveau door verschillende niveaus van toegang en machtigingen, tooobjects, instelling wordt beheerd zoals volledig beheer, schrijven, lezen of geen toegang. Toegangsbeheer in Active Directory wordt gedefinieerd hoe verschillende gebruikers Active Directory-objecten kunt gebruiken. Standaard worden de machtigingen voor objecten in Active Directory de veiligste instelling toohello ingesteld. |U hebt een account voor elke gebruiker die toegang hebben tot een Microsoft-cloudservice toocreate. U kunt ook gebruikersaccounts wijzigen of verwijderen wanneer ze niet meer nodig zijn. Gebruikers hebben geen administrator-machtigingen, maar u kunt deze desgewenst toewijzen. Zie voor meer informatie [gebruikers beheren in Azure AD](active-directory-create-users.md). <br><br> Binnen Azure Active Directory is een van de belangrijkste functies Hallo Hallo mogelijkheid toomanage toegang tooresources. Deze resources kunnen deel uitmaken van de directory hello, net als bij Hallo machtigingen toomanage objecten door middel van rollen in Hallo directory of resources die externe toohello directory, zoals SaaS-toepassingen, Azure-services, en SharePoint-sites of on-premises bronnen. <br><br> Oplossing voor het beheer van een center van Azure Active Directory is Hallo Hallo-beveiligingsgroep. de resource-eigenaar hello (of Hallo beheerder van Hallo directory) kunt toewijzen een groep tooprovide een bepaalde toegang rechts toohello bronnen die ze eigenaar. leden van de groep Hallo HALLO hallo toegang worden verstrekt en Hallo resource-eigenaar kunt Hallo rechts toomanage Hallo ledenlijst van een groep toosomeone anders – zoals een afdeling of een sitebeheerder helpdesk delegeren<br> <br> Hallo beheren groepen in Azure AD-onderwerp vindt u meer informatie over het beheren van toegang tot en met groepen. |Active Directory-identiteiten in de cloud Hallo via synchronisatie en Federatie uitbreiden |

## <a name="role-based-access-control"></a>Op rollen gebaseerd toegangsbeheer
Op rollen gebaseerde toegangsbeheer (RBAC) maakt gebruik van functies en beleidsregels tooevaluate inrichting, testen en uw bedrijfsprocessen en regels voor het verlenen van toegang toousers afdwingen. Sleutel beheerders beleidsregels voor de inrichting maken en toewijzen van gebruikers tooroles en die sets met rechten tooresources voor deze rollen definiëren. RBAC breidt Hallo identity management-oplossing toouse op basis van software processen en handmatige tussenkomst van de gebruiker in Hallo inrichtingsproces verminderen.
Azure AD-RBAC kunt Hallo bedrijf toorestrict Hallo hoeveelheid bewerkingen die een persoon uitvoeren kunt nadat hij toegang tot tooAzure-beheerportal heeft. Met behulp van RBAC toocontrol toegang toohello portal nadert IT-beheerders ca Gemachtigdentoegang met behulp van Hallo toegangsbeheer te volgen:

* **Op basis van een groep roltoewijzing**: U toegang kunt geven tooAzure AD-groepen die kunnen worden gesynchroniseerd vanuit uw lokale Active Directory. Hiermee kunt u tooleverage Hallo bestaande investeringen die uw organisatie heeft aangebracht in tooling en processen voor het beheren van groepen. U kunt ook Hallo overgedragen groep management-functie van Azure AD Premium.
* **Gebruik de ingebouwde rollen in Azure**: kunt u drie rollen: eigenaar, bijdrager en Reader tooensure dat gebruikers en groepen machtiging toodo alleen Hallo taken die ze toodo hun werk nodig hebt.
* **Gedetailleerde toegang tooresources**: U kunt toewijzen toousers rollen en groepen voor een bepaald abonnement, resourcegroep of een afzonderlijke Azure resource, zoals een website of de database. Op deze manier kunt u ervoor zorgen dat gebruikers hebben toegang tot tooall Hallo-bronnen die ze nodig hebben en geen toegang tot tooresources dat ze niet toomanage hoeven.

## <a name="provisioning-and-other-customization-options"></a>Inrichting en andere aanpassingsopties
Uw team kunt zakelijke vereisten en -abonnementen toodecide hoeveel toocustomize Hallo identiteitsoplossing gebruiken. Een grote onderneming mogelijk bijvoorbeeld een gefaseerde implementatieschema voor werkstromen en aangepaste adapters die is gebaseerd op een tijdlijn voor toepassingen die veel worden gebruikt op locaties incrementeel-inrichting. Een andere aanpassing planning overwegen voor twee of meer toepassingen toobe ingericht in de hele organisatie, na een geslaagde test leveren. Interactie van de toepassing van de gebruiker kan worden aangepast en procedures voor het inrichten van resources mogelijk gewijzigde tooaccommodate geautomatiseerde inrichting.

U kunt inrichting ervan ongedaan tooremove een service of het onderdeel. Een account opheffen van inrichting betekent bijvoorbeeld dat Hallo-account van een resource wordt verwijderd.

Hallo hybride modellen voor het leveren van bronnen combineert aanvraag en methoden op basis van rollen, die beide worden ondersteund door Azure AD. Voor een subset van werknemers of beheerde systemen kan handig zijn tooautomate toegang met toewijzing op basis van rollen. Een bedrijf mogelijk ook andere aanvragen of uitzonderingen door een model op basis van aanvraag verwerkt. Sommige bedrijven kunnen beginnen met handmatige toewijzing en ontwikkelen voor een hybride-model, met een doel van een volledig op rollen gebaseerde implementatie op een later tijdstip.

Andere bedrijven mogelijk vinden het niet praktisch voor zakelijke redenen tooachieve voltooid op rollen gebaseerde inrichting en het doel een benadering hybride als een gewenste doelstelling. Nog andere bedrijven mogelijk worden voldaan met alleen op aanvraag gebaseerde inrichting, en niet wilt tooinvest extra moeite toodefine en beheren op basis van functies, geautomatiseerde beleidsregels voor de inrichting.

## <a name="license-management"></a>Licentiebeheer
Licentiebeheer in Azure AD op basis van een groep kan beheerders gebruikers tooa beveiligingsgroep toewijzen en Azure AD automatisch toegewezen licenties tooall Hallo leden van Hallo-groep. Als een gebruiker wordt vervolgens toegevoegd aan of verwijderd uit groep hello, een licentie worden automatisch toegewezen aan of verwijderd afhankelijk van wat geschikt.

U kunt groepen die u vanuit synchroniseert on-premises AD of beheren in Azure AD. Deze koppeling met Azure AD premium groepsbeheer met Self-Service kunt u eenvoudig delegeren licentie toewijzing toohello juiste besluitvormers. U kunt erop vertrouwen problemen zoals licentie conflicten en ontbrekende locatiegegevens automatisch worden gesorteerd uit.

## <a name="self-regulating-user-administration"></a>Zelf marktregulerende Gebruikersbeheer
Wanneer uw organisatie wordt tooprovision bronnen voor alle interne organisaties gestart, kunt u Hallo-functionaliteit voor het beheer van zelf marktregulerende gebruikers implementeren. Hallo voordelen en de voordelen van inrichting gebruikers kunt u optimaal buiten de grenzen van de organisatie. In deze omgeving een wijziging in de status van een gebruiker automatisch doorgevoerd in de toegangsrechten op organisatie grenzen en locaties. U kunt inrichten kosten te verlagen en stroomlijnen Hallo toegangs- en processen. Hallo implementatie realiseert Hallo mogelijkheden van de implementatie van op rollen gebaseerde toegangsbeheer voor end-to-end-toegangsbeheer in uw organisatie. U kunt beheerdersrechten verlagen door geautomatiseerde procedures voor de betreffende gebruikers inrichten. U kunt de beveiliging verbeteren door de beveiliging wordt afgedwongen, automatiseren en stroomlijnen en levenscyclusbeheer van gebruiker en resources worden ingericht voor grote gebruiker populaties centraliseren.

> [!NOTE]
> Zie voor meer informatie, instellen van Azure AD voor toepassingsbeheer voor toegang tot selfservice
> 
> 

Azure AD (recht gebaseerd) op basis van een licentie services werk door een abonnement in uw Azure AD-directory-service-tenant activeren. Zodra het Hallo-abonnement actief is worden Hallo servicefuncties beheerd door beheerders van directory-service en die wordt gebruikt door gebruikers met een licentie. Zie voor meer informatie, hoe biedt Azure AD licensing work?
Integratie met andere leveranciers 3e

Azure Active Directory biedt eenmalige aanmelding op en verbeterde toepassing toegang beveiliging toothousands van SaaS-toepassingen en on-premises webtoepassingen. Zie voor een gedetailleerde lijst met Azure Active Directory-toepassingsgalerie voor ondersteunde SaaS-toepassingen, Azure Active Directory federatiecompatibiliteitslijst: van derden id-providers die gebruikt tooimplement worden kunnen eenmalige aanmelding

## <a name="define-synchronization-management"></a>Synchronisatie management definiëren
Wanneer u uw on-premises directory's integreert met Azure AD, worden uw gebruikers productiever omdat zij één identiteit hebben voor toegang tot zowel resources in de cloud als on-premises. Met deze integratie kunnen gebruikers en organisaties profiteren van de volgende Hallo:

* Organisaties kunnen gebruikers met een algemene hybride identiteit bieden voor on-premises of cloud-gebaseerde services gebruik van Windows Server Active Directory en vervolgens te verbinden tooAzure Active Directory.
* Beheerders kunnen voorwaardelijke toegang op basis van de bron van toepassing, apparaat en gebruikers-id, netwerklocatie en multi-factor authentication-server opgeven.
* Gebruikers kunnen gebruikmaken van hun gemeenschappelijke identiteit via accounts in Azure AD tooOffice 365, Intune, SaaS-apps en toepassingen van derden.
* Ontwikkelaars kunnen ontwikkelen van toepassingen die gebruikmaken van algemene identiteitsmodel hello, integratie van toepassingen in Active Directory on-premises of Azure voor cloud-gebaseerde toepassingen

Hallo bevat volgende afbeelding een voorbeeld van een weergave op hoog niveau van het synchronisatieproces identiteit.

![](./media/hybrid-id-design-considerations/identitysync.png)

Synchronisatieproces van identiteit

Hallo na tabel toocompare Hallo Synchronisatieopties bekijken:

| Optie voor synchronisatie | Voordelen | Nadelen |
| --- | --- | --- |
| Synchronisatie gebaseerde (via DirSync of AADConnect) |Gebruikers en groepen die zijn gesynchroniseerd vanaf de on-premises en cloud <br>  **Beleidsbeheer**: accountbeleid kunnen worden ingesteld via Active Directory waarmee Hallo beheerder Hallo mogelijkheid toomanage wachtwoordbeleid, werkstation, beperkingen, uitsluiting besturingselementen, en meer, zonder extra tooperform taken in de cloud Hallo.  <br>  **Toegangsbeheer**: toegang toohello cloudservice kunt beperken zodat Hallo services kunnen worden geopend via bedrijfsomgeving Hallo via online servers of beide. <br>  Verminderd ondersteuningsoproepen: als gebruikers minder wachtwoorden tooremember hebben, zijn deze minder waarschijnlijk tooforget ze. <br>  Beveiliging: Identiteit van gebruikers en informatie zijn beveiligd, omdat alle Hallo-servers en services die worden gebruikt in eenmalige aanmelding onder de knie en lokale beheerd. <br>  Ondersteuning voor sterke verificatie: U sterke verificatie (ook wel tweeledige verificatie genoemd) kunt gebruiken met Hallo-cloudservice. Echter, als u sterke verificatie gebruikt, moet u eenmalige aanmelding. | |
| Op basis van Federation (via AD FS) |Ingeschakeld door de beveiligingstokenservice (STS). Wanneer u een STS tooprovide één aanmelding toegang met een Microsoft-cloudservice configureren, maakt u een federatieve vertrouwensrelatie tussen uw lokale STS en Hallo federatieve domein dat u hebt opgegeven in uw Azure AD-tenant. <br> Eindgebuikers toouse Hallo dezelfde referenties tooobtain toegang tot toomultiple bronnen set <br>eindgebruikers kunnen geen toomaintain meerdere sets met referenties. Nog Hallo gebruikers hebben tooprovide hun referenties tooeach een Hallo deelnemende resources., B2B en B2C scenario's ondersteund. |Vereist speciale personeel voor implementatie en het onderhoud van de specifieke on-premises AD FS-servers. Zijn er beperkingen op Hallo gebruik van sterke verificatie als u uw STS toouse AD FS plannen. Zie voor meer informatie [geavanceerde opties configureren voor AD FS 2.0](http://go.microsoft.com/fwlink/?linkid=235649). |

> [!NOTE]
> Zie voor meer informatie, [uw on-premises identiteiten integreren met Azure Active Directory](active-directory-aadconnect.md).
> 
> 

## <a name="see-also"></a>Zie ook
[Overzicht ontwerpoverwegingen](active-directory-hybrid-identity-design-considerations-overview.md)

