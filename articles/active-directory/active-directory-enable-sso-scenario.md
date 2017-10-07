---
title: aaaManaging toepassingen met Azure Active Directory | Microsoft Docs
description: Dit artikel Hallo voordelen van Azure Active Directory integreren met uw on-premises, cloud en SaaS-toepassingen.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 95b96f10-2d5c-4b78-8af8-d3657a24140f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: asteen
ms.openlocfilehash: 0016f8b433e101d8a150bc6d9be3931851578241
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-applications-with-azure-active-directory"></a>Toepassingen beheren met Azure Active Directory
Afgezien van werkstroom Hallo of inhoud hebben bedrijven twee basisvereisten voor alle toepassingen:

1. de productiviteit tooincrease toepassingen moeten gemakkelijk toodiscover en toegang
2. tooenable beveiliging en beheeracties Hallo organisatie moet controle en toezicht op wie kan en daadwerkelijk is toegang tot elke toepassing

In Hallo wereld van cloud-toepassingen die deze best kan worden bereikt met behulp van de identiteit toocontrol '*die is toegestaan toodo wat*'.

In het computing terminologie:

* *Wie* staat bekend als *identiteit* -Hallo beheer van gebruikers en groepen
* *Wat* staat bekend als *toegangsbeheer* – Hallo beheer van toegang tot tooprotected bronnen

Beide onderdelen samen worden aangeduid als *identiteit en toegang Management (IAM)*, die is gedefinieerd door Hallo [Gartner](http://www.gartner.com/it-glossary/identity-and-access-management-iam) als een groep '*Hallo beveiliging discipline waarmee Hallo rechts personen tooaccess Hallo juiste resources op Hallo rechtermuisknop tijden voor de redenen waarom Hallo*'.

OK, wat is Hallo probleem? Als de IAM *niet beheerd* op één locatie met een geïntegreerde oplossing:

* Identiteit beheerders tooindividually maken en bijwerken van gebruikersaccounts in alle toepassingen afzonderlijk, hebben een activiteit redundante en tijd in beslag neemt.
* Gebruikers hebben toomemorize meerdere referenties tooaccess Hallo toepassingen die ze toowork met. Als gevolg hiervan gebruikers vaak toowrite omlaag hun wachtwoorden of andere beheeroplossingen voor wachtwoord waardoor gegevens beveiligingsrisico's gebruiken.
* Redundante tijdrovend activiteiten kort Hallo gebruikers en beheerders op de bedrijfsactiviteiten verhogen van de onderrand van uw bedrijf werkt.

Ja, wat in het algemeen wordt voorkomen dat organisaties uit gebruik nemen van geïntegreerde IAM-oplossingen?

* Meest technische oplossingen zijn gebaseerd op software-platforms die toobe geïmplementeerd en aangepast door elke organisatie voor hun eigen toepassingen nodig.
* Cloud-toepassingen zijn vaak met een hogere snelheid dan IT-organisatie kan worden geïntegreerd met bestaande IAM-oplossingen vastgesteld.
* Beveiliging en bewaking tooling vereist aanvullende aanpassing en integratie tooachieve uitgebreide E2E scenario's.

## <a name="azure-active-directory-integrated-with-applications"></a>Azure Active Directory is geïntegreerd met toepassingen
Azure Active Directory is een uitgebreide Identity als een Service (IDaaS) van Microsoft die:

* Hiermee kunt u IAM als een cloudservice 
* Voorziet in centraal toegangsbeleid beheer, eenmalige aanmelding (SSO) en rapportage 
* Ondersteunt de geïntegreerde access management voor [duizenden toepassingen](https://azure.microsoft.com/marketplace/active-directory/) in Hallo-toepassingsgalerie, met inbegrip van Salesforce, Google Apps, Box, Concur en meer. 

Met Azure Active Directory, alle toepassingen u publiceren voor uw partners en klanten (werk of consumer) Hallo hebben dezelfde mogelijkheden voor identiteits- en toegangsbeheer.<br> Dit kunt u toosignificantly uw operationele kosten te verlagen.

Wat gebeurt er als u een toepassing die nog niet wordt vermeld in het Hallo-toepassingsgalerie tooimplement nodig? Dit is wat tijd in beslag dan eenmalige aanmelding configureren voor toepassingen van Hallo-toepassingsgalerie, biedt Azure AD u een wizard waarmee u de Hallo-configuratie.

Hallo-waarde van Azure AD zich verder uitstrekt dan 'net' cloud-toepassingen. U kunt deze ook gebruiken met on-premises toepassingen via een beveiligde externe toegang. Met veilige externe toegang, kunt u Hallo Hallo nodig om VPN-verbindingen of andere implementaties van traditionele RAS-beheer te elimineren.

Azure AD levert Hallo oplossing toohello hoofdgegevens beveiliging en productiviteit problemen doordat centraal toegangsbeleid beheer en eenmalige aanmelding (SSO) voor al uw toepassingen.

* Gebruikers hebben toegang tot meerdere toepassingen met één aanmelding geeft meer tijd tooincome genereren of zakelijke operationele activiteiten uitgevoerd.
* Identity-beheerders kunnen tooapplications op één plek toegang beheren.

Hallo-voordeel voor Hallo gebruiker en voor uw bedrijf is duidelijk. U gaat nu bekijkt hello voordelen voor een identiteit beheerder en het Hallo-organisatie.

## <a name="integrated-application-benefits"></a>Voordelen van de geïntegreerde toepassing
Hallo SSO-proces bestaat uit twee stappen:

* Verificatie, Hallo proces Hallo gebruikersidentiteit te valideren.
* Autorisatie, besluit tooenable Hallo of blokkeren van toegang tooa resource met een toegangsbeleid.

Als u Azure AD toomanage-toepassingen en schakel eenmalige aanmelding:

* Verificatie is uitgevoerd op de on-premises-(bijvoorbeeld AD) of Azure AD-account van de gebruiker Hallo.
* Autorisatie wordt uitgevoerd op Hallo Azure AD-toewijzing en beveiliging beleid consistent eindgebruiker gezorgd en zodat u tooadd toewijzing, locaties en MFA voorwaarden op elke toepassing, ongeacht de interne mogelijkheden.

Het belangrijk toounderstand die Hallo manier Hallo autorisatie wordt gepubliceerd op de doeltoepassing Hallo varieert, afhankelijk van hoe de toepassing hello is geïntegreerd met Azure AD.

* **Toepassingen die vooraf zijn geïntegreerd door serviceprovider** zoals Office 365 en Azure, dit zijn toepassingen rechtstreeks op Azure AD is gebouwd en afhankelijk van de uitgebreide mogelijkheden voor identiteits- en toegangsbeheer. Toegang toothese toepassingen via directory informatie en token-uitgifte is ingeschakeld.
* **Toepassingen die vooraf zijn geïntegreerd door Microsoft en aangepaste toepassingen** dit onafhankelijke cloudtoepassingen die afhankelijk zijn van een interne applicatie directory en kunnen werken onafhankelijk van Azure AD zijn. Toegang toothese toepassingen door uitgifte van een toepassing specifieke referentie toegewezen tooan toepassing account is ingeschakeld. Afhankelijk van de mogelijkheden van de toepassing hello mogelijk Hallo referentie een federation-token of gebruikersnaam en wachtwoord voor een account dat u eerder in de toepassing hello is ingericht.
* **On-premises toepassingen** toepassingen zijn gepubliceerd via hello Azure AD-toepassingsproxy voornamelijk toegang tooon-premises toepassingen inschakelen. Deze toepassingen afhankelijk zijn van een centrale on-premises adreslijst zoals Windows Server Active Directory. Toegang toothese toepassingen wordt ingeschakeld door de activering van Hallo proxy toodeliver Hallo inhoud toohello end gebruiker van toepassing bij het naleven van Hallo lokale aanmelding vereiste.

Bijvoorbeeld, als een gebruiker lid wordt van uw organisatie, moet u toocreate een account voor Hallo gebruiker in Azure AD voor primaire Hallo aanmelding bewerkingen. Als deze gebruiker toegang tooa beheerde toepassing zoals Salesforce vereist, ook toocreate een account nodig voor deze gebruiker in Salesforce en koppel deze toohello Azure-account toomake SSO werk. Wanneer Hallo gebruiker uw organisatie verlaat, verdient het aanbeveling toodelete hello Azure AD-account en alle bijbehorende equivalent accounts in Hallo IAM winkels van Hallo gebruiker toegang had tot Hallo-toepassingen.

## <a name="access-detection"></a>Detectie toegang
In moderne ondernemingen zijn IT-afdelingen vaak niet op de hoogte van alle Hallo cloud-toepassingen die worden gebruikt. In combinatie met Cloud App Discovery biedt Azure AD u een oplossing toodetect deze toepassingen.

## <a name="account-management"></a>Accountbeheer
Oudsher is het beheren van accounts in Hallo verschillende toepassingen is een handmatig proces uitgevoerd door IT of ondersteuning voor persoonlijke in Hallo-organisatie. Accountbeheer Azure AD volledig geautomatiseerd tussen alle serviceprovider geïntegreerde toepassingen en die vooraf zijn geïntegreerd met Microsoft ondersteuning van geautomatiseerde gebruikersinrichting of SAML JIT toepassingen.

## <a name="automated-user-provisioning"></a>Automatisch gebruikers inrichten
Sommige toepassingen bieden automatiseringsinterfaces voor het maken en verwijderen (of deactivering) van accounts. Als een provider een interface biedt, wordt gebruikt door Azure AD. Dit vermindert de operationele kosten omdat administratieve taken automatisch gebeurt en verbetert de beveiliging van uw omgeving Hallo omdat hierdoor minder kans op onbevoegde toegang Hallo.

## <a name="access-management"></a>Toegangsbeheer
Met behulp van Azure AD kunt u access tooapplications met afzonderlijke of regel aangestuurd toewijzingen beheren. U kunt ook toegang management toohello juiste mensen in Hallo organisatie zorgt Hallo best toezicht en verminderen Hallo last van de helpdesk delegeren.

## <a name="on-premises-applications"></a>On-premises toepassingen
Hallo ingebouwd in toepassingsproxy kunt u uw on-premises toepassingen tooyour gebruikers, wat resulteert in beide consistente toegang ervaring met moderne cloud-toepassing en Hallo voordelen van Azure AD-bewaking, rapportage en beveiligingsmogelijkheden toopublish .

## <a name="reporting-and-monitoring"></a>Rapportage- en controle
Azure AD biedt u vooraf geïntegreerde rapportage en monitoring mogelijkheden waarmee u tooknow wie heeft toegang tot tooapplications en wanneer ze daadwerkelijk gebruikt.

## <a name="related-capabilities"></a>Verwante mogelijkheden
U kunt uw toepassingen met gedetailleerde toegangsbeleid en vooraf geïntegreerde MFA beveiligen met Azure AD. Zie informatie over Azure MFA toolearn [Azure MFA](https://azure.microsoft.com/services/multi-factor-authentication/).

## <a name="getting-started"></a>Aan de slag
tooget gestart toepassingen integreren met Azure AD te kijken hoe Hallo [integratie van Azure Active Directory met toepassingen aan de slag](active-directory-integrating-applications-getting-started.md).

## <a name="see-also"></a>Zie ook
[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)

