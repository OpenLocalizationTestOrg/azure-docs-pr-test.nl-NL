---
title: 'Azure Active Directory Domain Services: Implementatiescenario''s voor | Microsoft Docs'
description: Implementatiescenario's voor Azure AD Domain Services
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c5216ec9-4c4f-4b7e-830b-9d70cf176b20
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: maheshu
ms.openlocfilehash: 8a64bd8f7c6eba8f6490e10fa62bef195b6b3d5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deployment-scenarios-and-use-cases"></a>Implementatiescenario's en gebruik
In deze sectie bekijken we enkele scenario's en use cases die van Azure Active Directory (AD) Domain Services profiteren.

## <a name="secure-easy-administration-of-azure-virtual-machines"></a>Veilig en eenvoudig beheer van virtuele machines in Azure
Kunt u Azure Active Directory Domain Services toomanage uw virtuele Azure-machines op een gestroomlijnde manier. Virtuele machines van Azure kan worden beheerd domein gekoppelde toohello, zodat u de toouse toolog in uw zakelijke AD-referenties. Deze aanpak voorkomt referentie management problemen zoals het beheren van lokale administrator-accounts op elk van uw virtuele machines in Azure.

Server virtuele machines die beheerd domein gekoppelde toohello worden kan ook worden beheerd en beveiligd met behulp van Groepsbeleid. U kunt toepassen vereiste basislijnen tooyour Azure virtuele machines en vergrendelen overeenkomstig de richtlijnen voor beveiligingsbeleid van het bedrijf. Bijvoorbeeld, kunt u beleid management mogelijkheden toorestrict Hallo soorten groepen van toepassingen die kunnen worden gestart op deze virtuele machines.

![Gestroomlijnd beheer van virtuele machines in Azure](./media/active-directory-domain-services-scenarios/streamlined-vm-administration.png)

Als de servers en andere infrastructuur bereikt einde van de levenscyclus, verplaatst Contoso veel toepassingen momenteel gehost op een lokale toohello cloud. De huidige IT-standaard vereist dat de servers die als host fungeert voor zakelijke toepassingen zijn moeten lid van een domein en beheerd via Groepsbeleid. Contoso IT-beheerder bij voorkeur toodomain join virtuele machines zijn geïmplementeerd in Azure, toomake beheer eenvoudiger. Hierdoor kunnen kunnen beheerders en gebruikers aanmelden met hun bedrijfsreferenties. Op Hallo hetzelfde moment machines kunnen worden geconfigureerd toocomply vereiste basislijnen met Groepsbeleid. Contoso liever niet toohave toodeploy, bewaken en beheren van domeincontrollers in Azure toosecure virtuele machines in Azure. Azure AD Domain Services is daarom een geweldige geschikt is voor deze gebruiksvoorbeeld.

**Opmerkingen bij de implementatie**

Houd rekening met Hallo belangrijke punten voor dit implementatiescenario te volgen:

* Beheerde domeinen die worden geleverd door Azure AD Domain Services bieden een enkele platte eenheidstructuur van organisatie-(organisatie-eenheid) standaard. Alle domein-machines zich bevinden in één OE platte. U kunt aangepaste OE's echter toocreate.
* Azure AD Domain Services biedt ondersteuning voor eenvoudige Groepsbeleid in Hallo vorm van een ingebouwde GPO elke voor Hallo-gebruikers en computers containers. U kunt aangepaste GPO's maken en deze organisatie-eenheden toocustom als doel.
* Hallo AD computer object basisschema biedt ondersteuning voor Azure AD Domain Services. U kunt Hallo computerobject schema niet uitbreiden.

## <a name="lift-and-shift-an-on-premises-application-that-uses-ldap-bind-authentication-tooazure-infrastructure-services"></a>Lift-en-shift een on-premises toepassing die gebruikmaakt van LDAP-binding verificatie tooAzure infrastructuurservices
![LDAP-binding](./media/active-directory-domain-services-scenarios/ldap-bind.png)

Contoso heeft een on-premises toepassing die is aangeschaft via een ISV lang geleden. Hallo-toepassing is in onderhoudsmodus Hallo ISV en aanvragende wijzigingen toohello toepassing is beperkend dure voor Contoso. Deze toepassing is een webgebaseerde frontend die met behulp van een webformulier gebruikersreferenties verzamelt en vervolgens gebruikers worden geverifieerd door het uitvoeren van een LDAP-binding toohello zakelijk Active Directory. Contoso toomigrate wilt dat deze toepassing tooAzure infrastructuurservices. Is het wenselijk dat de toepassing hello werkt zoals is zonder wijzigingen. Gebruikers moeten bovendien kunnen tooauthenticate met hun bestaande bedrijfsreferenties worden en zonder tooretrain gebruikers toodo dingen anders hebben. Met andere woorden, eindgebruikers moet oblivious van waarop Hallo toepassing wordt uitgevoerd en Hallo migratie moet transparante toothem.

**Opmerkingen bij de implementatie**

Houd rekening met Hallo belangrijke punten voor dit implementatiescenario te volgen:

* Zorg ervoor dat de toepassing hello hoeft niet toomodify schrijftijd toohello directory. LDAP schrijftoegang toomanaged domeinen is verstrekt door Azure AD Domain Services wordt niet ondersteund.
* U kunt wachtwoorden rechtstreeks met het beheerde domein Hallo niet wijzigen. Eindgebruikers kunnen ofwel hun wachtwoord wijzigen met behulp van Azure AD-mechanisme voor selfservice voor wachtwoordherstel wijzigen of tegen Hallo on-premises adreslijst. Deze wijzigingen worden automatisch gesynchroniseerd en beschikbaar zijn in Hallo beheerde domein.

## <a name="lift-and-shift-an-on-premises-application-that-uses-ldap-read-tooaccess-hello-directory-tooazure-infrastructure-services"></a>Lift en shift een on-premises toepassing die gebruikmaakt van LDAP lezen tooaccess Hallo directory tooAzure infrastructuurservices
Contoso heeft een on-premises line-of-business (LOB)-toepassing die is ontwikkeld bijna een tien jaar geleden. Deze toepassing is op de hoogte-map en is ontworpen toowork met Windows Server AD. Hallo-toepassing maakt gebruik van LDAP (Lightweight Directory Access Protocol) tooread informatie/kenmerken over gebruikers uit Active Directory. Hallo toepassing niet kenmerken wijzigen of anders schrijven toohello directory. Contoso toomigrate wilt dat deze toepassing tooAzure infrastructuurservices en buiten gebruik stellen Hallo veroudering lokale hardware momenteel deze toepassing te hosten. Hallo-toepassing kan niet herschreven toouse moderne directory API's zoals Hallo REST gebaseerde Azure AD Graph API. Daarom is een optie lift en shift gewenste waarbij toepassing hello gemigreerde toorun in Hallo cloud, zonder de code te wijzigen of herschrijven Hallo toepassing kan worden.

**Opmerkingen bij de implementatie**

Houd rekening met Hallo belangrijke punten voor dit implementatiescenario te volgen:

* Zorg ervoor dat de toepassing hello hoeft niet toomodify schrijftijd toohello directory. LDAP schrijftoegang toomanaged domeinen is verstrekt door Azure AD Domain Services wordt niet ondersteund.
* Zorg ervoor dat de toepassing hello hoeft niet een aangepaste/uitgebreide Active Directory-schema. Schema-uitbreidingen worden niet ondersteund in Azure AD Domain Services.

## <a name="migrate-an-on-premises-service-or-daemon-application-tooazure-infrastructure-services"></a>Migreren van een lokale service of -daemon toepassing tooAzure infrastructuurservices
Sommige toepassingen bestaan uit meerdere lagen, waarin een van de lagen Hallo tooperform geverifieerde aanroepen tooa back-end laag zoals een databaselaag moet. Active Directory-service-accounts worden meestal gebruikt voor deze gebruiksvoorbeelden. U kunt lift en shift dergelijke toepassingen tooAzure infrastructuurservices en gebruik Azure AD Domain Services voor Hallo identiteiten van deze toepassingen. U kunt kiezen toouse Hallo hetzelfde serviceaccount die worden gesynchroniseerd vanuit uw lokale directory tooAzure AD. U kunt ook eerst een aangepaste organisatie-eenheid maken en maakt u een afzonderlijk serviceaccount in die organisatie-eenheid toodeploy dergelijke toepassingen.

![Met behulp van WIA-serviceaccount](./media/active-directory-domain-services-scenarios/wia-service-account.png)

Contoso heeft een op maat gemaakte kluis softwaretoepassing die bestaat uit een webfront-end, een SQL-server en een back-voor FTP-endserver. Geïntegreerde Windows-verificatie van serviceaccounts is gebruikte tooauthenticate Hallo web-front-end toohello FTP-server. Hallo-webfront-end is toorun ingesteld als een service-account. Hallo back-endserver is geconfigureerd tooauthorize toegang vanaf Hallo-serviceaccount voor Hallo webfront-end. Contoso verkiest niet toohave toodeploy een domain controller virtuele machine in Hallo cloud toomove deze toepassing tooAzure infrastructuurservices. Contoso IT-beheerder Hallo-servers waarop Hallo webfront-end, SQL server en Hallo FTP-server tooAzure virtuele machines kunt implementeren. Deze machines bent gekoppelde tooan Azure AD Domain Services beheerd domein. Vervolgens kunt gebruiken Hallo hetzelfde serviceaccount in hun on-premises directory voor verificatiedoeleinden Hallo-app. Dit serviceaccount is toohello gesynchroniseerde Azure AD Domain Services beheerd domein en is beschikbaar voor gebruik.

**Opmerkingen bij de implementatie**

Houd rekening met Hallo belangrijke punten voor dit implementatiescenario te volgen:

* Zorg ervoor dat de toepassing hello gebruikmaakt van gebruikersnaam en wachtwoord voor verificatie. Certificaat/op basis van smartcardverificatie wordt niet ondersteund door Azure AD Domain Services.
* U kunt wachtwoorden rechtstreeks met het beheerde domein Hallo niet wijzigen. Eindgebruikers kunnen ofwel hun wachtwoord wijzigen met behulp van Azure AD-mechanisme voor selfservice voor wachtwoordherstel wijzigen of tegen Hallo on-premises adreslijst. Deze wijzigingen worden automatisch gesynchroniseerd en beschikbaar zijn in Hallo beheerde domein.

## <a name="windows-server-remote-desktop-services-deployments-in-azure"></a>Implementaties in Azure voor Windows Server extern bureaublad-services
U kunt Azure AD Domain Services tooprovide beheerde AD domain services-tooyour extern bureaublad-servers geïmplementeerd in Azure.

Zie hoe te voor meer informatie over dit implementatiescenario[Azure AD Domain Services integreren in uw implementatie RDS](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/rds-azure-adds).
