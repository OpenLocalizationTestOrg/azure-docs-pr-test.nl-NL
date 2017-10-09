---
title: aanbevolen procedures voor MFA aaaSecurity | Microsoft Docs
description: Dit document bevat de aanbevolen procedures om het gebruik van Azure MFA met Azure-accounts
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 3be7d968-96bb-4320-8701-869fd04a2595
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 7f18c2592764878b842d81783b321a05f29ee3d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="security-best-practices-for-using-azure-multi-factor-authentication-with-azure-ad-accounts"></a>Aanbevolen beveiligingsprocedures voor het gebruik van Azure multi-factor Authentication met Azure AD-accounts

Verificatie in twee stappen is Hallo voorkeur keuze voor de meeste organisaties die tooenhance hun verificatieproces willen. Azure multi-factor Authentication (MFA) helpt bedrijven die voldoen aan de vereisten voor beveiliging en naleving en tegelijkertijd een eenvoudige aanmeldingservaring voor gebruikers. In dit artikel bevat informatie over een aantal tips waarmee u rekening houden moet bij het plannen van de overstap op Hallo van Azure MFA.

## <a name="deploy-azure-mfa-in-hello-cloud"></a>Azure MFA in Hallo cloud implementeren

Er zijn twee manieren tooenable Azure MFA voor alle gebruikers.

* Licenties voor elke gebruiker (ofwel Azure MFA, Azure AD Premium of Enterprise Mobility + Security) kopen
* Een multi-factor Authentication-Provider en betalen per gebruiker of per authenticatie maken

### <a name="licenses"></a>Licenties
![EMS](./media/multi-factor-authentication-security-best-practices/ems.png)

Als u Azure AD Premium of Enterprise Mobility + Security licenties hebt, hebt u al Azure MFA. Alles extra tooextend Hallo in twee stappen verificatie mogelijkheid tooall gebruikers nodig niet voor uw organisatie. U hoeft alleen een licentie tooa gebruiker tooassign en vervolgens kunt u MFA.

Overweeg bij het instellen van multi-factor Authentication, Hallo tips te volgen:

* Maak geen een per authenticatie multi-factor Authentication-Provider. Als u dit doet, kan u betaalt voor aanvragen voor verificatie van gebruikers die al licenties terechtkomen.
* Als er niet voldoende licenties voor alle gebruikers, kunt u een per gebruiker multi-factor Authentication-Provider toocover Hallo rest van uw organisatie. 
* Azure AD Connect is alleen vereist als u uw on-premises Active Directory-omgeving met een Azure Active directory synchroniseert. Als u een Azure AD-directory niet is gesynchroniseerd met een lokaal exemplaar van Active Directory gebruikt, hoeft u geen Azure AD Connect.

### <a name="multi-factor-auth-provider"></a>Multi-factor Authentication-Provider
![Multi-factor Authentication-Provider](./media/multi-factor-authentication-security-best-practices/authprovider.png)

Als er geen licenties met Azure MFA, kunt u een MFA Auth-Provider maken. 

Bij het maken van Hallo Auth-Provider, u moet een map tooselect en overweeg Hallo volgende details:

* U hoeft niet een Azure AD-directory toocreate een multi-Factor Authentication-Provider, maar u krijgt meer functionaliteit met een. Hallo volgende kenmerken worden ingeschakeld wanneer u Hallo Auth-Provider aan een Azure Active directory koppelen:  
  * Uitbreiden in twee stappen verificatie tooall uw gebruikers  
  * Uw globale beheerders aanvullende functies, zoals het Hallo-beheerportal, aangepaste begroeting en rapporten bieden.
* Als u uw on-premises Active Directory-omgeving met een Azure Active directory synchroniseert, moet u de DirSync- of AAD Sync. Als u een Azure AD-directory niet is gesynchroniseerd met een lokaal exemplaar van Active Directory gebruikt, hoeft u niet DirSync of AAD Sync.
* Kies Hallo verbruik model die het beste past bij uw bedrijf. Zodra u Hallo gebruiksmodel selecteert, kunt u deze niet wijzigen. Hallo twee modellen zijn:
  * Per verificatie: berekent u voor elke verificatie. Dit model gebruiken als u wilt dat de verificatie in twee stappen voor iedereen die toegang heeft tot een bepaalde app, niet voor specifieke gebruikers.
  * Per ingeschakelde gebruiker: berekent u voor elke gebruiker die u voor Azure MFA inschakelen. Dit model gebruiken als u sommige gebruikers met Azure AD Premium of Enterprise Mobility Suite licenties en andere zonder hebt.

### <a name="supportability"></a>Ondersteuning
Aangezien de meeste gebruikers gewend toousing alleen wachtwoorden tooauthenticate, is het belangrijk dat uw bedrijf wijst u alleen op tooall gebruikers met betrekking tot dit proces. Deze afhankelijkheid kan Hallo kans dat gebruikers contact opnemen met uw helpdesk voor verwante tooMFA kleine problemen verminderen. Er zijn echter enkele scenario's tijdelijk uitschakelen MFA waar nodig is. Gebruik Hallo volgen richtlijnen toounderstand hoe toohandle de scenario's:

* Training van uw ondersteuningsbeheerder personeel toohandle scenario's waarbij Hallo gebruiker niet aanmelden omdat Hallo mobiele app of telefoon geen een melding of telefoongesprek ontvangt. Technische ondersteuning kunt [inschakelen eenmalig overslaan](multi-factor-authentication-whats-next.md#one-time-bypass) tooallow een tooauthenticate gebruiker één keer door 'overslaan' verificatie in twee stappen. Hallo bypass is tijdelijk en verloopt na een opgegeven aantal seconden.
* Houd rekening met Hallo [goedgekeurde IP-adressen mogelijkheid](multi-factor-authentication-whats-next.md#trusted-ips) in Azure MFA manier toominimize in twee stappen te controleren. Met deze functie kunnen beheerders van een tenant beheerd of federatieve verificatie in twee stappen voor gebruikers die vanaf een lokaal intranet van het bedrijf Hallo aanmelden zich omzeilen. Hallo-functies zijn beschikbaar voor Azure AD-tenants die Azure AD Premium of Enterprise Mobility Suite Azure multi-factor Authentication-licenties hebt.

## <a name="best-practices-for-an-on-premises-deployment"></a>Aanbevolen procedures voor een on-premises implementatie
Als uw bedrijf tooleverage eigen infrastructuur tooenable MFA besloot, moet u een Azure multi-factor Authentication-Server lokale toodeploy. Hallo MFA-Server-onderdelen worden weergegeven in het volgende diagram Hallo:

![Standaard MFA-Server-onderdelen: console, synchronisatie-engine, -beheerportal, cloudservice](./media/multi-factor-authentication-security-best-practices/server.png) \*niet standaard geïnstalleerd \** geïnstalleerd maar niet standaard is ingeschakeld

Azure multi-factor Authentication-Server kunt cloud bronnen en on-premises resources beveiligen met behulp van de federatieserver. U moet de AD FS hebt en laat het gefedereerd met Azure AD-tenant.
Overweeg bij het instellen van multi-factor Authentication-Server, Hallo volgende details:

* Als u met Active Directory Federation Services (AD FS) beveiligen wilt, wordt de eerste verificatiestap hello wordt uitgevoerd van Azure AD-resources on-premises met AD FS. de tweede stap Hallo is on-premises uitgevoerd door Hallo claim naleven.
* U hebt geen tooinstall hello Azure multi-factor Authentication-Server uw federatieve AD FS-server. Hallo multi-factor Authentication-Adapter voor AD FS moet echter worden geïnstalleerd op een Windows Server 2012 R2 waarop AD FS wordt uitgevoerd. U kunt Hallo-server installeren op een andere computer, zolang het is een ondersteunde versie en Hallo AD FS-adapter afzonderlijk installeren op uw federatieve AD FS-server. 
* Hallo multi-factor Authentication AD FS-Adapter van de installatiewizard maakt een beveiligingsgroep met de naam PhoneFactor Admins in uw Active Directory en vervolgens uw AD FS-service-account toothis groep toegevoegd. Verifieer dat Hallo PhoneFactor Admins-groep is gemaakt op uw domeincontroller en die Hallo AD FS-serviceaccount lid van deze groep is. Indien nodig, Hallo AD FS-service-account toohello PhoneFactor Admins-groep op uw domeincontroller handmatig toevoegen.

### <a name="user-portal"></a>Gebruikersportal
Hallo-gebruikersportal kunt selfservice mogelijkheden en biedt een volledige set met mogelijkheden voor het beheer van gebruiker. Deze wordt uitgevoerd in een website van Internet Information Server (IIS). Dit onderdeel volgen richtlijnen tooconfigure hello gebruiken:

* Gebruik IIS 6 of hoger
* Installeren en registreren van ASP.NET v2.0.507207
* Zorg ervoor dat deze server kan worden geïmplementeerd in een perimeternetwerk

### <a name="app-passwords"></a>App-wachtwoorden
Als uw organisatie is gefedereerd voor eenmalige aanmelding met Azure AD en u gaat toobe met Azure MFA, vervolgens mee worden Hallo volgende details:

* Hallo app-wachtwoord wordt gecontroleerd door Azure AD en wordt daarom overgeslagen federation. Federatie wordt alleen gebruikt bij het instellen van app-wachtwoorden.
* Voor federatieve gebruikers (SSO), worden wachtwoorden opgeslagen in Hallo organisatie-id. Als de gebruiker Hallo Hallo bedrijf verlaat, heeft dat info tooflow tooorganizational id met behulp van DirSync. Account uitschakelen/verwijderen kan duren voordat toothree uren toosync dat er een vertraging uitschakelen/verwijderen van app-wachtwoorden in Azure AD.
* On-premises instellingen voor toegangsbeheer van client worden niet herkend door het app-wachtwoord.
* Er is geen mogelijkheid lokale verificatie logboekregistratie/controle is beschikbaar voor app-wachtwoorden.
* Bepaalde geavanceerde architectuur ontwerpen mogelijk met een combinatie van organisatie-gebruikersnaam en wachtwoorden app bij het gebruik van verificatie in twee stappen met clients, afhankelijk van waar ze verifiëren. Voor clients die worden geverifieerd bij een on-premises infrastructuur, gebruikt u een organisatie-gebruikersnaam en wachtwoord. Voor clients die worden geverifieerd bij Azure AD, zou u Hallo app-wachtwoord gebruiken.
* Gebruikers kunnen geen app-wachtwoorden maken standaard. Als u tooallow gebruikers toocreate app-wachtwoorden nodig hebt, selecteert u Hallo **kunnen gebruikers toocreate app-wachtwoorden toosign in niet-browsertoepassingen** optie.

## <a name="additional-considerations"></a>Aanvullende overwegingen
Gebruik deze lijst voor aanvullende overwegingen en richtlijnen voor elk onderdeel dat is geïmplementeerd op de lokale:

- Azure Multi-Factor Authentication instellen met [Active Directory Federation Services](multi-factor-authentication-get-started-adfs.md).
- Installeren en configureren met Azure MFA-Server Hallo [RADIUS-verificatie](multi-factor-authentication-get-started-server-radius.md).
- Installeren en configureren met Azure MFA-Server Hallo [IIS-verificatie](multi-factor-authentication-get-started-server-iis.md).
- Installeren en configureren met Azure MFA-Server Hallo [Windows-verificatie](multi-factor-authentication-get-started-server-windows.md).
- Installeren en configureren met Azure MFA-Server Hallo [LDAP-verificatie](multi-factor-authentication-get-started-server-ldap.md).
- Installeren en configureren met Azure MFA-Server Hallo [extern bureaublad-Gateway en Azure multi-factor Authentication-Server met behulp van RADIUS](multi-factor-authentication-get-started-server-rdg.md).
- Installeren en configureren van de synchronisatie tussen hello Azure MFA-Server en [Windows Server Active Directory](multi-factor-authentication-get-started-server-dirint.md).
- [Hello Azure multi-factor Authentication Server Mobile App Web Service implementeren](multi-factor-authentication-get-started-server-webservice.md).
- [Geavanceerde VPN-configuratie met Azure multi-factor Authentication](multi-factor-authentication-advanced-vpn-configurations.md) voor Cisco ASA, Citrix Netscaler en Juniper/Pulse Secure VPN-apparaten met behulp van de LDAP-Adreslijst of RADIUS.

## <a name="next-steps"></a>Volgende stappen
In dit artikel worden enkele aanbevolen procedures voor Azure MFA gemarkeerd, maar er zijn andere bronnen die u kunt ook tijdens het plannen van uw implementatie MFA gebruiken. Hallo onderstaande lijst bevat enkele belangrijke artikelen die u tijdens dit proces helpen kunnen:

* [Rapporten in Azure multi-factor Authentication](multi-factor-authentication-manage-reports.md)
* [Hallo in twee stappen verificatie registratie ervaring](multi-factor-authentication-end-user-first-time.md)
* [Veelgestelde vragen over Azure multi-factor Authentication](multi-factor-authentication-faq.md)

