---
title: aaaOverview van Azure Active Directory Domain Services | Microsoft Docs
description: Overzicht van Azure Active Directory Domain Services
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 0d47178f-773e-45f9-9ff4-9e8cffa4ffa2
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 2b4884b3b8b639fcca438ddbab0bd3361aac53c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-domain-services"></a>Azure AD Domain Services
## <a name="overview"></a>Overzicht
Azure Infrastructure Services kunt u een breed scala aan oplossingen computergebruik in een flexibele manier toodeploy. Met Azure Virtual Machines, kunt u vrijwel onmiddellijk implementeren en betaalt u alleen door Hallo minuut. Ondersteuning voor Windows, Linux, SQL Server, Oracle, IBM, SAP en BizTalk gebruikt, kunt u elke werkbelasting, een andere taal, op vrijwel elk besturingssysteem implementeren. Deze voordelen inschakelen toomigrate oudere toepassingen die zijn geïmplementeerd op de lokale tooAzure, toosave op de operationele kosten.

Een belangrijk aspect van het migreren van lokale toepassingen tooAzure verwerkt Hallo identiteiten van deze toepassingen. Directory-bewuste toepassingen afhankelijk zijn van LDAP voor lees- of schrijftoegang toohello zakelijk directory of afhankelijk zijn van geïntegreerde Windows-verificatie (Kerberos of NTLM-verificatie) tooauthenticate eindgebruikers. Line-of-business (LOB)-toepassingen die op Windows Server worden doorgaans geïmplementeerd op de machines verbonden met het domein, zodat deze kunnen worden beheerd veilig via Groepsbeleid. too'lift en shift' lokale toepassingen toohello cloud deze afhankelijkheden op Hallo bedrijfsidentiteit infrastructuur nodig toobe opgelost.

Beheerders schakelen vaak tooone Hallo oplossingen toosatisfy Hallo identiteit behoeften van hun toepassingen die zijn geïmplementeerd in Azure te volgen:

* Een site-naar-site VPN-verbinding tussen de werkbelastingen die worden uitgevoerd in Azure Infrastructure Services en Hallo zakelijk directory on-premises implementeren.
* Hallo zakelijke AD domein/forest infrastructuur uitbreiden door het instellen van de replica van domeincontrollers met behulp van virtuele machines in Azure.
* Implementeer een zelfstandig domein in Azure met domeincontrollers die zijn geïmplementeerd als virtuele machines in Azure.

Alle deze benaderingen lijden onder blokkering van de hoge kosten en administratieve overhead. Beheerders zijn vereiste toodeploy domeincontrollers met virtuele machines in Azure. Bovendien ze moeten toomanage veilige, patch, monitor, back-up en het oplossen van deze virtuele machines. Hallo de afhankelijkheid van VPN-verbindingen toohello lokale directory zorgt ervoor dat de werkbelastingen die zijn geïmplementeerd in Azure toobe kwetsbaar tootransient netwerk haperingen of storingen. Deze netwerkstoringen op zijn beurt leiden tot lagere bedrijfstijd en verminderde betrouwbaarheid voor deze toepassingen.

We ontworpen Azure AD Domain Services tooprovide eenvoudiger alternatief.

## <a name="introducing-azure-ad-domain-services"></a>Inleiding tot Azure AD Domain Services
Azure AD Domain Services beheerd domein van services zoals domeindeelname, groep-beleid, LDAP, Kerberos/NTLM-verificatie, die volledig compatibel zijn met Windows Server Active Directory biedt. U kunt deze domeinservices zonder Hallo nodig is voor u toodeploy gebruiken, beheren en domeincontrollers in de cloud Hallo patch. Azure AD Domain Services kan worden geïntegreerd met uw bestaande Azure AD-tenant, waardoor het mogelijk voor gebruikers toolog aan met hun zakelijke referenties. Bovendien kunt u bestaande groepen en gebruikers accounts toosecure toegang tooresources, zodat de soepeler 'lift-en-verschuiving' van een on-premises resources tooAzure infrastructuurservices.

Azure AD Domain Services-functionaliteit werkt naadloos samen ongeacht of uw Azure AD-tenant alleen in de cloud of gesynchroniseerd met uw lokale Active Directory.

### <a name="azure-ad-domain-services-for-cloud-only-organizations"></a>Azure AD Domain Services voor organisaties die alleen in de cloud
Een cloud Azure AD-tenant (vaak waarnaar wordt verwezen tooas ' beheerde tenants') beschikt niet over een lokale identiteit footprint. Met andere woorden, zijn gebruikersaccounts, hun wachtwoorden en groepslidmaatschappen alle systeemeigen toohello cloud - dat wil zeggen, gemaakt en beheerd in Azure AD. Kijk eens naar dat Contoso een alleen is-Azure AD-tenant. Zoals u in de volgende illustratie Hallo, heeft de beheerder van Contoso een virtueel netwerk geconfigureerd in Azure-infrastructuurservices. Toepassingen en serverwerkbelastingen worden geïmplementeerd in dit virtuele netwerk in Azure virtuele machines. Aangezien Contoso een alleen-tenant is, worden alle gebruikers-id's, hun referenties en groepslidmaatschappen gemaakt en beheerd in Azure AD.

![Overzicht van Azure AD Domain Services](./media/active-directory-domain-services-overview/aadds-overview.png)

Contoso IT-beheerder kan Azure AD Domain Services inschakelt voor hun Azure AD-tenant en kies toomake domain services beschikbaar zijn in dit virtuele netwerk. Daarna Azure AD Domain Services voorziet in een beheerd domein en beschikbaar in het virtuele netwerk Hallo. Alle gebruikersaccounts, groepslidmaatschappen en de referenties van de gebruiker is beschikbaar in de Contoso Azure AD-tenant zijn ook beschikbaar in deze nieuwe domein. Deze functie kunnen gebruikers in Hallo organisatie toosign in toohello domein met hun bedrijfsreferenties - bijvoorbeeld om op afstand toodomain-computers die lid zijn via Extern bureaublad verbinding te maken. Beheerders kunnen toegang tooresources in Hallo-domein met een bestaande groepslidmaatschappen inrichten. Toepassingen die zijn geïmplementeerd in virtuele machines op Hallo virtueel netwerk kunnen functies zoals domeindeelname, LDAP lees-, LDAP-binding, NTLM en Kerberos-verificatie en Groepsbeleid gebruiken.

Enkele van de meest kenmerkende aspecten van Hallo beheerd domein die is ingericht door Azure AD Domain Services zijn als volgt:

* Contoso IT-beheerder niet hoeft toomanage, patch of dit domein of de domeincontrollers voor dit beheerde domein controleren.
* Er is geen noodzaak toomanage AD-replicatie voor dit domein. Accounts van gebruikers, groepslidmaatschappen en referenties van van Contoso Azure AD-tenant zijn automatisch beschikbaar binnen dit beheerde domein.
* Omdat Hallo domein wordt beheerd door Azure AD Domain Services, Contoso van IT-beheerder heeft geen domein- of Ondernemingsadministrator-bevoegdheden voor dit domein.

### <a name="azure-ad-domain-services-for-hybrid-organizations"></a>Azure AD Domain Services voor hybride organisaties
Organisaties met een hybride IT-infrastructuur gebruiken een combinatie van cloud-bronnen en lokale bronnen. Deze organisaties synchroniseren van identiteitsgegevens van hun lokale directory tootheir Azure AD-tenant. Hybride organisaties gezocht meer toomigrate van hun lokale toepassingen toohello cloud, met name oudere directory-bewuste toepassingen, kunnen Azure AD Domain Services nuttig toothem zijn.

Litware Corporation heeft geïmplementeerd [Azure AD Connect](../active-directory/active-directory-aadconnect.md), toosynchronize identiteitsgegevens van hun lokale directory tootheir Azure AD-tenant. Hallo identiteitsgegevens die wordt gesynchroniseerd bevat gebruikersaccounts, hun referentie-hashes voor verificatie (Wachtwoordsynchronisatie) en groepslidmaatschappen.

> [!NOTE]
> **Wachtwoordsynchronisatie is verplicht voor hybride organisaties toouse Azure AD Domain Services**. Deze vereiste is omdat gebruikers referenties zijn nodig in Hallo beheerd domein verstrekt door Azure AD Domain Services, tooauthenticate deze gebruikers via NTLM of Kerberos-verificatiemethoden.
>
>

![Azure AD Domain Services voor Litware Corporation](./media/active-directory-domain-services-overview/aadds-overview-synced-tenant.png)

Hallo ziet voorafgaande illustratie u hoe organisaties met een hybride IT-infrastructuur, zoals Litware Corporation, Azure AD Domain Services. De toepassingen en serverwerkbelastingen waarvoor domeinservices van Litware zijn geïmplementeerd in een virtueel netwerk in Azure Infrastructure Services. Van Litware IT-beheerder kan Azure AD Domain Services inschakelt voor hun Azure AD-tenant en kies toomake een beheerd domein beschikbaar zijn in dit virtuele netwerk. Aangezien Litware een organisatie met een hybride IT-infrastructuur is, zijn gebruikersaccounts, groepen en referenties gesynchroniseerd tootheir Azure AD-tenant van hun on-premises directory. Met deze functie kunnen gebruikers toosign in toohello domein met hun bedrijfsreferenties - bijvoorbeeld bij het verbinden op afstand toomachines deel toohello domein via Extern bureaublad. Beheerders kunnen toegang tooresources in Hallo-domein met een bestaande groepslidmaatschappen inrichten. Toepassingen die zijn geïmplementeerd in virtuele machines op Hallo virtueel netwerk kunnen functies zoals domeindeelname, LDAP lees-, LDAP-binding, NTLM en Kerberos-verificatie en Groepsbeleid gebruiken.

Enkele van de meest kenmerkende aspecten van Hallo beheerd domein die is ingericht door Azure AD Domain Services zijn als volgt:

* Hallo beheerd domein is een zelfstandig domein. Het is niet een uitbreiding van van Litware lokaal domein.
* Van Litware IT-beheerder heeft geen toomanage, patch of monitor domeincontrollers nodig voor dit beheerde domein.
* Er is geen noodzaak toomanage AD-replicatie toothis domein. Accounts van gebruikers, groepslidmaatschappen en referenties van van Litware on-premises adreslijst zijn gesynchroniseerd tooAzure AD via Azure AD Connect. Deze accounts van gebruikers, groepslidmaatschappen en referenties automatisch beschikbaar zijn in Hallo beheerde domein.
* Omdat Hallo domein wordt beheerd door Azure AD Domain Services, Litware van IT-beheerder heeft geen domein- of Ondernemingsadministrator-bevoegdheden voor dit domein.

## <a name="benefits"></a>Voordelen
Met Azure AD Domain Services, kunt u profiteren van Hallo volgende voordelen:

* **Eenvoudige** – u kunt voldoen aan Hallo identiteiten van virtuele machines geïmplementeerd tooAzure infrastructuurservices met een paar eenvoudige klikken. U niet nodig toodeploy en infrastructuur voor identiteiten in Azure of setup connectiviteit back tooyour on-premises identity infrastructuur te beheren.
* **Geïntegreerde** : Azure AD Domain Services is nauw geïntegreerd met uw Azure AD-tenant. U kunt nu Azure AD gebruiken als een map voor geïntegreerde enterprise cloud-gebaseerde die behoeften van uw moderne toepassingen en de traditionele directory-bewuste toepassingen toohello caters.
* **Compatibel** : Azure AD Domain Services is gebouwd op Hallo beproefde hoogwaardige bedrijfsinfrastructuur van Windows Server Active Directory. Daarom kunnen uw toepassingen afhankelijk van een grotere mate van compatibiliteit met Windows Server Active Directory-functies. Niet alle functies die beschikbaar zijn in Windows Server AD zijn momenteel beschikbaar zijn in Azure AD Domain Services. Beschikbare functies zijn echter compatibel is met de Hallo bijbehorende Windows Server AD-functies die u in uw on-premises infrastructuur op te vertrouwen. Hallo LDAP, vormen Kerberos, NTLM, Groepsbeleid en domain join-mogelijkheden een goed ontwikkelde aanbieding die zijn getest en verfijnd via verschillende versies van Windows Server.
* **Rendabele** – met Azure AD Domain Services, kunt u voorkomen dat Hallo infrastructuur en werkbelasting die is gekoppeld aan het beheren van identiteit infrastructuur toosupport traditionele directory-bewuste toepassingen. U kunt deze toepassingen tooAzure infrastructuurservices verplaatsen en profiteren van lagere operationele kosten.
