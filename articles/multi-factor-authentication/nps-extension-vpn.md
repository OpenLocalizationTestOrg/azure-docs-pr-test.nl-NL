---
title: integratie met Azure MFA met NPS extensie aaaVPN | Microsoft Docs
description: Dit artikel wordt de VPN-infrastructuur integreren met Azure MFA met Hallo Network Policy Server (NPS)-uitbreiding voor Microsoft Azure.
services: active-directory
keywords: Azure MFA integreren van VPN-, Azure Active Directory, uitbreiding van Network Policy Server
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: kgremban
ms.reviewer: jsnow
ms.custom: it-pro
ms.openlocfilehash: 5e120f7633121385d9cc5d7bec97ecaa1ec7cf19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-your-vpn-infrastructure-with-azure-multi-factor-authentication-mfa-using-hello-network-policy-server-nps-extension-for-azure"></a>Uw VPN-infrastructuur integreren met Azure multi-factor Authentication (MFA) met behulp van Hallo Network Policy Server (NPS)-extensie voor Azure

## <a name="overview"></a>Overzicht

Hallo Service NPS (Network Policy)-extensie voor Azure, waarmee organisaties toosafeguard Remote Authentication Dial-In User Service (RADIUS)-clientauthenticatie met behulp van cloud-gebaseerde [Azure multi-factor Authentication (MFA)](multi-factor-authentication-get-started-server-rdg.md), waarmee u verificatie in twee stappen.

Dit artikel bevat instructies voor het Hallo NPS infrastructuur integreren met Azure MFA met Hallo NPS-extensie voor verificatie van de Azure tooenable-beveiligde in twee stappen voor gebruikers die zich tooconnect tooyour netwerk via een VPN. 

Hallo Network Policy and Access Services (NPS) biedt organisaties Hallo mogelijkheden voor het volgende:

* Geef de centrale locatie voor het Hallo-beheer en controle over het netwerk aanvragen toospecify die verbinding, welke tijdstippen verbindingen zijn toegestaan, maken kan Hallo duur van verbindingen en Hallo beveiligingsniveau dat clients moeten gebruiken tooconnect, enzovoort. In plaats van deze beleidsregels op elke server VPN of extern bureaublad (RD) Gateway opgeeft, kunnen deze beleidsregels één keer worden opgegeven in een centrale locatie. Hallo RADIUS-protocol wordt gebruikt tooprovide Hallo gecentraliseerde verificatie, autorisatie en Accounting (AAA). 
* Instellen en afdwingen van statusbeleid voor Network Access Protection (NAP) client om te bepalen of apparaten onbeperkte of beperkte toegang tot toonetwork bronnen worden verleend.
* Geef een manier tooenforce verificatie en autorisatie voor toegang tot too802.1x-compatibele draadloze toegangspunten en Ethernet-switches.    

Zie voor meer informatie [Network Policy Server (NPS)](https://docs.microsoft.com/windows-server/networking/technologies/nps/nps-top). 

tooenhance beveiliging en bieden hoge mate van compatibiliteit, organisaties NPS kunnen integreren met Azure MFA tooensure die gebruikers gebruiken verificatie in twee stappen toobe kunnen verbinding maken met de virtuele poort toohello op Hallo VPN-server. Voor gebruikers toobe toegang verleend, moeten ze bieden de combinatie van gebruikersnaam en wachtwoord met informatie die gebruiker Hallo heeft in het besturingselement. Deze informatie moet worden vertrouwd en eenvoudig niet wordt gedupliceerd, zoals een mobiele telefoonnummer, een vast, een toepassing op een mobiel apparaat, enzovoort.

De beschikbaarheid van de voorafgaande toohello Hallo NPS-extensie voor Azure, klanten die tooimplement %0 verificatie willen geïntegreerd NPS en Azure MFA-omgevingen tooconfigure had en onderhouden van een afzonderlijke MFA-Server in on-premises omgeving Hallo als beschreven in extern bureaublad-Gateway en Azure multi-factor Authentication-Server met behulp van RADIUS.

Hallo-beschikbaarheid van Hallo NPS-extensie voor Azure biedt nu organisaties Hallo keuze toodeploy een on-premises op basis van MFA oplossing of een cloud-verificatie op basis van MFA-oplossing toosecure RADIUS-client.
 
## <a name="authentication-flow"></a>Verificatiestroom
Wanneer een gebruiker verbinding tooa virtuele poort op een VPN-server maakt, moeten ze eerst verifiëren met verschillende protocollen, waardoor Hallo gebruik van een combinatie van gebruikersnaam en wachtwoord en de verificatiemethoden op basis van certificaten. 

In tooauthenticating toevoegen en controleren van identiteit, moeten gebruikers Hallo inbellen machtigingen nodig hebben. In de eenvoudige implementaties inbellen machtigingen toegewezen die toegang toestaan ingesteld rechtstreeks op Hallo Active Directory-gebruikersobjecten. 

 ![Eigenschappen van de gebruiker](./media/nps-extension-vpn/image1.png)

Elke VPN-server verleent of weigert op basis van beleid gedefinieerd voor elke lokale VPN-server voor eenvoudige implementaties.

In implementaties van grotere en meer schaalbare, Hallo beleidsregels die verlenen of weigeren VPN-toegang op RADIUS-servers worden gecentraliseerd. In dit geval fungeert Hallo VPN-server als een access-server (RADIUS-client) waarmee verbindingsaanvragen en account berichten tooa RADIUS-server. tooconnect toohello virtuele poort op Hallo VPN-server, gebruikers moeten worden geverifieerd en voldoen aan Hallo voorwaarden centraal gedefinieerd op RADIUS-servers. 

Wanneer Hallo NPS-extensie voor Azure is geïntegreerd met Hallo NPS, is geslaagd Hallo-authenticatiestroom als volgt:

1. Hallo VPN-server ontvangt een verificatieaanvraag van een VPN-gebruiker met Hallo gebruikersnaam en wachtwoord tooconnect tooa resource, zoals een extern bureaublad-sessie. 
2. Fungeert als een RADIUS-client, VPN-server tooa Hallo-RADIUS-toegangsaanvraag aanvraagbericht converteert en verzendt Hallo-bericht (wachtwoord wordt gecodeerd) toohello RADIUS (NPS)-server waarop NPS extensie Hallo is geïnstalleerd. 
3. Hallo gebruikersnaam en wachtwoord combinatie is geverifieerd in Active Directory. Als Hallo gebruikersnaam / wachtwoord is onjuist, Hallo RADIUS-Server stuurt een Access-Reject-bericht. 
4. Als alle omstandigheden, zoals in de opgegeven NPS-verbindingsaanvraag Hallo en netwerkbeleid wordt voldaan (bijvoorbeeld de tijd van de dag of groep lidmaatschap beperkingen), een aanvraag voor de secundaire verificatie met Azure MFA Hallo NPS-extensie wordt geactiveerd. 
5. Azure MFA communiceert met Azure Active Directory, haalt Hallo Gebruikersdetails en voert Hallo secundaire verificatie via Hallo-methode is geconfigureerd door de gebruiker hello (SMS-bericht, mobiele app, enzovoort). 
6. Bij voltooiing van Hallo MFA uitdaging communiceert Azure MFA Hallo resultaat toohello NPS-extensie.
7. Nadat de verbindingspoging Hallo is geverifieerd en geautoriseerd, stuurt Hallo NPS-server waarop het Hallo-uitbreiding is geïnstalleerd een RADIUS-Access-Accept-bericht toohello VPN-server (RADIUS-client).
8. Hallo gebruiker krijgt toegang tot toohello virtuele poort op de VPN-server en er wordt een versleutelde VPN-tunnel.

## <a name="prerequisites"></a>Vereisten
Deze sectie details Hallo vereisten nodig voordat de integratie van Azure MFA met Hallo extern bureaublad-Gateway. Voordat u begint, moet u de volgende vereisten is voldaan Hallo hebben.

* VPN-infrastructuur
* De rol en Network Policy and Access Services (NPS)
* Azure MFA-licentie
* Windows Server-software
* Bibliotheken
* Azure AD gesynchroniseerd met on-premises AD dat 
* GUID-ID van Azure Active Directory

### <a name="vpn-infrastructure"></a>VPN-infrastructuur
In dit artikel wordt ervan uitgegaan dat u hebt een werkende VPN-infrastructuur met behulp van Microsoft Windows Server 2016 aanwezig en die Hallo VPN-server momenteel niet geconfigureerd tooforward verbinding aanvragen tooa RADIUS-server is. Hallo VPN-infrastructuur toouse centrale RADIUS-server configureert u in deze handleiding.

Als u geen een werkende-infrastructuur aanwezig zijn, kunt u deze infrastructuur snel maken door de volgende Hallo richtlijnen in talloze zelfstudies met VPN-installatie die u op Hallo van Microsoft en derden sites vinden kunt. 

### <a name="network-policy-and-access-services-nps-role"></a>De rol en Network Policy and Access Services (NPS)

Hallo NPS-rolservice biedt Hallo RADIUS-server en clientfunctionaliteit. In dit artikel wordt ervan uitgegaan dat u Hallo NPS-rol op een lidserver of domeincontroller hebt geïnstalleerd in uw omgeving. RADIUS configureert u voor een VPN-configuratie in deze handleiding. Hallo NPS-rol installeren op een server _andere_ dan de VPN-server.

Windows Server 2012-service of hoger, Zie voor informatie over het installeren van de functie NPS Hallo [installeren van een NAP-statusbeleidsserver](https://technet.microsoft.com/library/dd296890.aspx). Beleid voor NAP (Network Access) is afgeschaft in Windows Server 2016. Zie voor een beschrijving van best practices voor NPS, inclusief Hallo aanbeveling tooinstall NPS op een domeincontroller [Best Practices voor NPS](https://technet.microsoft.com/library/cc771746).

### <a name="licenses"></a>Licenties

Vereist, is een licentie voor Azure MFA, die beschikbaar via een Azure AD Premium, Enterprise Mobility plus Security (EMS) of een MFA-abonnement is. Zie voor meer informatie [hoe tooget Azure multi-factor Authentication](multi-factor-authentication-versions-plans.md). Voor testdoeleinden kunt u een proefabonnement.

### <a name="software"></a>Software

Hallo NPS-uitbreiding vereist Windows Server 2008 R2 SP1 of hoger met Hallo NPS-functieservice is geïnstalleerd. Alle Hallo stappen in deze handleiding zijn uitgevoerd met behulp van Windows Server 2016.

### <a name="libraries"></a>Bibliotheken

Hallo na twee tapewisselaars zijn vereist:

* [Visual C++ Redistributable Packages for Visual Studio 2013 (X64)](https://www.microsoft.com/download/details.aspx?id=40784)
* _Microsoft Azure Active Directory-Module voor Windows PowerShell versie 1.1.166.0_ of hoger. Zie voor de meest recente release Hallo en installatie-instructies [Microsoft Azure Active Directory PowerShell-Module Release versiegeschiedenis](https://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx).

Deze bibliotheken worden niet geleverd met Hallo NPS extensie setup-bestanden (versie 0.9.1.2), ondanks de bestaande documentatie die anders wordt aangegeven. U moet ten minste Hallo Visual C++ Redistributable Packages installeren voor Visual Studio 2013. Hallo Microsoft Azure Active Directory-Module voor Windows PowerShell is geïnstalleerd, als deze nog niet aanwezig is, via een configuratiescript die u als onderdeel van het installatieproces Hallo uitvoert. Er is geen tooinstall nodig deze module tevoren als deze nog niet is geïnstalleerd.

### <a name="azure-active-directory-synched-with-on-premises-active-directory"></a>Azure Active Directory worden gesynchroniseerd met de lokale Active Directory 

toouse hello NPS-extensie, on-premises gebruikers moeten worden gesynchroniseerd met Azure Active Directory en ingeschakeld voor multi-factor Authentication. Deze handleiding wordt ervan uitgegaan dat de on-premises gebruikers zijn gesynchroniseerd met Azure Active Directory met AD Connect. Hieronder vindt u instructies voor het inschakelen van gebruikers voor MFA.
Voor informatie over Azure AD connect, Zie [uw on-premises adreslijsten integreren met Azure Active Directory](../active-directory/connect/active-directory-aadconnect.md). 

### <a name="azure-active-directory-guid-id"></a>GUID-ID van Azure Active Directory 
tooinstall Hallo NPS, moet u tooknow Hallo GUID van hello Azure Active Directory. Instructies voor het vinden van Hallo GUID van hello Azure Active Directory zijn beschikbaar in de volgende sectie Hallo.

## <a name="configure-radius-for-vpn-connections"></a>RADIUS voor VPN-verbindingen configureren

Als u Hallo NPS-serverfunctie hebt geïnstalleerd op een lidserver, kunt u tooconfigure tooauthenticate moet en VPN-client die aanvragen van VPN-verbindingen toestaan. 

Deze sectie wordt ervan uitgegaan dat u Hallo Network Policy Server-functie hebt geïnstalleerd, maar hebben geen deze heeft geconfigureerd voor gebruik in uw infrastructuur.

>[!NOTE]
>Als u al een werkende VPN-server die gebruikmaakt van een gecentraliseerde RADIUS-server voor verificatie, kunt u deze sectie overslaan.
>

### <a name="register-server-in-active-directory"></a>Server registreren in Active Directory
toofunction goed in dit scenario Hallo NPS-server moet toobe geregistreerd in Active Directory.

1. Open Serverbeheer.
2. Klik in Serverbeheer op **extra**, en klik vervolgens op **Network Policy Server**. 
3. Hallo Network Policy Server-console met de rechtermuisknop op **NPS (lokaal)**, en klik vervolgens op **server registreren in Active Directory**. Klik op **OK** twee keer.

 ![Network Policy Server](./media/nps-extension-vpn/image2.png)

4. Laat Hallo console geopend voor de volgende procedure Hallo.

### <a name="use-wizard-tooconfigure-radius-server"></a>Wizard tooconfigure RADIUS-server gebruiken
U kunt een standaard (door de wizard gebaseerd) of geavanceerde configuratie optie tooconfigure Hallo RADIUS-server. Deze sectie wordt ervan uitgegaan Hallo gebruik van Hallo standaardconfiguratie op basis van een wizard optie.

1. Klik in Hallo Network Policy Server console **NPS (lokaal)**.
2. Selecteer onder configuratie van de standaard **RADIUS-Server voor inbel- of VPN-verbindingen**, en klik vervolgens op **configureren van VPN- of inbelverbindingen**.

 ![VPN configureren](./media/nps-extension-vpn/image3.png)

3. Selecteer op Hallo Selecteer inbel- of virtuele particuliere netwerk verbindingen Type pagina **VPN-verbindingen**, en klik op **volgende**.

 ![Virtueel particulier netwerk](./media/nps-extension-vpn/image4.png)

4. Klik op Hallo Geef inbel- of VPN-Server pagina op **toevoegen**.
5. In Hallo **nieuwe RADIUS-client** in het dialoogvenster een beschrijvende naam opgeven, Voer Hallo herleidbare naam of IP-adres van Hallo VPN-server en een gedeeld geheim wachtwoord invoeren. Deze gedeelde geheime wachtwoord lange en complexe maken. Als u dit nodig voor de stappen in de volgende sectie hello, noteert u dit wachtwoord.

 ![Nieuwe RADIUS-Client](./media/nps-extension-vpn/image5.png)

6. Klik op **OK**, en vervolgens **volgende**.
7. Op Hallo **verificatiemethoden configureren** pagina, accepteer de standaardinstelling hello (Microsoft Encrypted Authentication versie 2 (MS-CHAPv2) of kies een andere optie en klik op **volgende**.

  >[!NOTE]
  >Als u Extensible Authentication Protocol (EAP) configureert, moet u MS-CHAPv2 of PEAP. Er zijn geen andere EAP wordt ondersteund.
 
8. Op de pagina Hallo gebruikersgroepen opgeven op **toevoegen** en selecteer een geschikte groep, indien aanwezig. Anders laat Hallo selectie leeg toogrant-tooall gebruikers.

 ![Gebruikersgroepen opgeven](./media/nps-extension-vpn/image7.png)

9. Klik op **Volgende**.
10. Op de pagina IP-Filters opgeven Hallo op **volgende**.
11. Op Hallo versleutelingsinstellingen opgeven pagina Hallo standaardinstellingen accepteren en klik op **volgende**.

 ![Versleuteling opgeven](./media/nps-extension-vpn/image8.png)

12. Geef de naam van een Realm hello, laat op Hallo naam leeg, Hallo standaardinstelling hebt geaccepteerd en op **volgende**.

 ![Een Realm opgeven](./media/nps-extension-vpn/image9.png)

13. Hallo nieuwe voltooien inbel- of -pagina voor VPN-verbindingen en RADIUS-clients en klik op **voltooien**.

 ![Verbindingen voltooien](./media/nps-extension-vpn/image10.png)

### <a name="verify-radius-configuration"></a>Controleer of de RADIUS-configuratie
Deze sectie details hebt gemaakt met behulp van de wizard Hallo Hallo-configuratie.

1. Vouw de RADIUS-Clients op Hallo NPS-server in Hallo NPS (lokaal)-console en selecteer **RADIUS-Clients**.
2. Met de rechtermuisknop in het deelvenster details Hallo Hallo RADIUS-client die u hebt gemaakt met de wizard en klikt u op **eigenschappen**. Hallo-eigenschappen voor uw RADIUS-client (Hallo VPN-server) moeten vergelijkbaar toothose hieronder weergegeven.

 ![VPN-eigenschappen](./media/nps-extension-vpn/image11.png)

3. Klik op **annuleren**.
4. Vouw op Hallo NPS-server in de NPS (lokaal)-console Hallo **beleid**, en selecteer **beleid voor verbindingsaanvragen**. U ziet Hallo VPN-verbindingen beleid dat lijkt op Hallo in onderstaande afbeelding.

 ![Verbindingsaanvragen](./media/nps-extension-vpn/image12.png)

5. Selecteer onder beleidsregels, **netwerkbeleid**. U moet een beleid met virtuele particuliere netwerk (VPN)-verbindingen dat lijkt op Hallo in onderstaande afbeelding.

 ![Eigenschappen van het netwerk](./media/nps-extension-vpn/image13.png)

## <a name="configure-vpn-server-toouse-radius-authentication"></a>VPN-Server toouse RADIUS-verificatie configureren
In deze sectie configureert u Hallo VPN-server toouse RADIUS-verificatie. Deze sectie wordt ervan uitgegaan dat u een werkende configuratie van VPN-server hebt, maar Hallo VPN-server toouse RADIUS-verificatie niet hebt geconfigureerd. Na het configureren van Hallo VPN-server, kunt u bevestigen dat de configuratie werkt zoals verwacht.

>[!NOTE]
>Als u VPN-serverconfiguratie die gebruikmaakt van RADIUS-verificatie hebt, kunt u deze sectie overslaan.
>

### <a name="configure-authentication-provider"></a>Verificatieprovider configureren
1. Open Serverbeheer op Hallo VPN-server.
2. Klik in Serverbeheer op **extra**, en vervolgens **Routing and Remote Access**.
3. Hallo Routing and Remote Access-console met de rechtermuisknop op  **\[servernaam\] (lokaal)**, en klik vervolgens op **eigenschappen**.

 ![Routering en RAS](./media/nps-extension-vpn/image14.png)
 
4. In Hallo **[servernaam} (lokaal) eigenschappen** dialoogvenster vak, klikt u op Hallo **beveiliging** tabblad. 
5. Op Hallo **beveiliging** tabblad onder verificatieprovider, klikt u op **RADIUS-verificatie**, en vervolgens **configureren**.

 ![RADIUS-verificatie](./media/nps-extension-vpn/image15.png)
 
6. Hallo RADIUS-verificatie in het dialoogvenster klikt u op **toevoegen**.
7. Hallo in RADIUS-Server toevoegen in de servernaam, naam of het Hallo-IP-adres Hallo van Hallo RADIUS-server die u hebt geconfigureerd in de vorige sectie Hallo toevoegen.
8. Klik in het gedeeld geheim op **wijziging** en voeg Hallo gedeeld geheim wachtwoord die u hebt gemaakt en u eerder hebt genoteerd.
9. Wijzig in Time-out (seconden), Hallo waarde tooa waarde tussen **30** en **60**. Dit is noodzakelijk tooallow voldoende tijd toocomplete Hallo tweede verificatiefactor.
 
 ![RADIUS-Server toevoegen](./media/nps-extension-vpn/image16.png)
 
10. Klik op **OK** totdat u alle dialoogvensters sluiten.

### <a name="test-vpn-connectivity"></a>VPN-verbindingen testen
In deze sectie maakt bevestigen u dat Hallo VPN-client is geverifieerd en gemachtigd door Hallo RADIUS-server wanneer u tooconnect tooVPN virtuele poort probeert. Deze sectie wordt ervan uitgegaan dat u gebruikmaakt van Windows 10 als een VPN-client. 

>[!NOTE]
>Als u al een VPN-client tooconnect toohello VPN-server geconfigureerd en Hallo-instellingen hebt opgeslagen, kunt u Hallo stappen gerelateerde tooconfiguring en opslaan van een VPN-verbindingsobject overslaan.
>

1. Klik op de VPN-client-computer **Start**, en vervolgens **instellingen** (tandwielpictogram pictogram).
2. Klik in de instellingen van venster **netwerk en Internet**.
3. Klik op **VPN**.
4. Klik op **een VPN-verbinding toevoegen**.
5. In een VPN-verbinding toevoegen, Windows (ingebouwd) opgeven, zoals Hallo VPN-provider en klik vervolgens voltooid Hallo resterende velden naar gelang van toepassing, en klik op **opslaan**. 

 ![VPN-verbinding toevoegen](./media/nps-extension-vpn/image17.png)
 
6. Open Hallo **Netwerkcentrum** in het Configuratiescherm.
7. Klik op **Adapterinstellingen wijzigen**.

 ![Adapterinstellingen wijzigen](./media/nps-extension-vpn/image18.png)

8. Met de rechtermuisknop op Hallo VPN-netwerkverbinding en klik op Eigenschappen. 

 ![Eigenschappen van VPN-netwerk](./media/nps-extension-vpn/image19.png)

9. Klik in de Hallo VPN-eigenschappen in het dialoogvenster op Hallo **beveiliging** tabblad. 
10. Zorg ervoor dat alleen op het tabblad Beveiliging Hallo **Microsoft CHAP Version 2 (MS-CHAP v2)** is geselecteerd en klik op OK.

 ![Protocollen toestaan](./media/nps-extension-vpn/image20.png)

11. Met de rechtermuisknop op Hallo VPN-verbinding en klikt u op **Connect**.
12. Klik op de pagina instellingen Hallo **Connect**.

Een geslaagde verbinding wordt weergegeven in het beveiligingslogboek Hallo op Hallo RADIUS-server als gebeurtenis-ID 6272, zoals hieronder wordt weergegeven.

 ![Eigenschappen van gebeurtenis](./media/nps-extension-vpn/image21.png)

## <a name="troubleshoot-guide"></a>Problemen met de gids
Wordt ervan uitgegaan dat uw VPN-configuratie werkte voordat u Hallo VPN-server toouse een gecentraliseerde RADIUS-server voor verificatie en autorisatie geconfigureerd. In dit geval is het waarschijnlijk dat Hallo probleem kan worden veroorzaakt door een onjuiste configuratie van Hallo RADIUS-Server of Hallo gebruik van een ongeldige gebruikersnaam of wachtwoord. Bijvoorbeeld, als u alternatieve UPN-achtervoegsel Hallo Hallo gebruikersnaam gebruikt, Hallo aanmeldingspoging mislukken (moet u dezelfde accountnaam voor de beste resultaten Hallo). 

Deze problemen, een toostart ideaal plaats is tooexamine Hallo beveiligingslogboek op tootroubleshoot Hallo RADIUS-server. zoeken naar toosave tijd gebeurtenissen, kunt u Hallo op basis van rollen en Network Policy and Access Server aangepaste weergave in Logboeken, zoals u hierna ziet. Gebeurtenis-ID 6273 geeft aan waar hello Network Policy Server toegang tooa gebruiker geweigerde gebeurtenissen. 

 ![Logboeken](./media/nps-extension-vpn/image22.png)
 
## <a name="configure-multi-factor-authentication"></a>Multi-factor Authentication configureren
Deze sectie geeft instructies voor het inschakelen van gebruikers voor MFA en voor het instellen van accounts voor verificatie in twee stappen. 

### <a name="enable-multi-factor-authentication"></a>Multi-Factor Authentication inschakelen
In deze sectie schakelt u Azure AD-accounts voor MFA. Gebruik Hallo **klassieke portal** tooenable gebruikers voor MFA. 

1. Open een browser en te navigeren[https://manage.windowsazure.com](https://manage.windowsazure.com). 
2. Meld u aan als beheerder Hallo.
3. Klik in het linkernavigatievenster hello, Hallo Portal **ACTIVE DIRECTORY**.

 ![Standaard-map](./media/nps-extension-vpn/image23.png)

4. Klik in de kolom naam Hallo op **standaarddirectory** (of een andere map, indien van toepassing).
5. Klik op de pagina snel starten Hallo **configureren**.

 ![Standaard configureren](./media/nps-extension-vpn/image24.png)

6. Op de pagina configureren hello, schuif naar beneden en klik in de sectie multi-factor authentication hello, op **service-instellingen beheren**.

 ![MFA-instellingen beheren](./media/nps-extension-vpn/image25.png)
 
7. Controleer de standaardinstellingen service Hallo op Hallo multi-factor authentication-pagina, en klik vervolgens op **gebruikers**. 

 ![MFA-gebruikers](./media/nps-extension-vpn/image26.png)
 
8. Selecteer op Hallo gebruikers pagina Hallo gebruikers die u tooenable voor MFA wenst en klik vervolgens op **inschakelen**.

 ![Eigenschappen](./media/nps-extension-vpn/image27.png)
 
9. Wanneer u wordt gevraagd, klikt u op **multi-factor auth inschakelen**.

 ![Schakel MFA in](./media/nps-extension-vpn/image28.png)
 
10. Klik op **Sluiten**. 
11. Hallo pagina vernieuwen. Hallo MFA status is gewijzigd tooEnabled.

Voor meer informatie over de gebruikers voor multi-factor Authentication tooenable zien [aan de slag met Azure multi-factor Authentication in de cloud Hallo](multi-factor-authentication-get-started-cloud.md). 

### <a name="configure-accounts-for-two-step-verification"></a>Accounts configureren voor verificatie in twee stappen
Wanneer een account voor MFA is ingeschakeld, kunnen gebruikers zich niet kunnen toosign in tooresources beheerst door de MFA-beleid Hallo totdat ze een vertrouwd apparaat toouse voor Hallo tweede verificatiefactor gelet gebruikt verificatie in twee stappen hebt geconfigureerd.

In deze sectie configureert u een vertrouwd apparaat voor gebruik met verificatie in twee stappen. Er zijn diverse opties beschikbaar voor u tooconfigure deze, waaronder de volgende Hallo:

* **Mobiele app**. U installeren Hallo Microsoft Authenticator-app op een Windows Phone, Android of iOS-apparaat. Afhankelijk van uw organisatie beleid, bent u vereiste toouse Hallo app in een van de twee modi: meldingen ontvangen voor verificaties (een gestuurd tooyour apparaat) of verificatiecode gebruiken (vereist tooenter een verificatie-code updates van elke 30 seconden). 
* **Mobiele telefoon telefoongesprek of tekstbericht**. U kunt ofwel een automatisch telefoongesprek of SMS-bericht ontvangen. Met de optie telefoonoproep Hallo, Hallo-oproep wordt beantwoord en druk op Hallo # aanmelding tooauthenticate. Met de optie van de tekst hello, kunt u toohello tekstbericht te beantwoorden of Hallo verificatiecode opgeven in Hallo-aanmelden-interface.
* **Office-telefoongesprek**. Dit proces is hetzelfde als die voor geautomatiseerde telefoongesprekken hierboven beschreven Hallo.

Volg deze instructies voor het instellen van een apparaat toouse Hallo mobiele app tooreceive push-melding voor verificatie.

1. Meld u aan te[https://aka.ms/mfasetup](https://aka.ms/mfasetup) of een site, zoals [https://portal.azure.com](https://portal.azure.com), waarin u tooauthenticate met uw referenties MFA-functionaliteit vereist. 
2. Bij het aanmelden met uw gebruikersnaam en wachtwoord, krijgt u een scherm waarin tooset Hallo-account voor aanvullende beveiligingsverificatie wordt gevraagd.

 ![Extra beveiliging](./media/nps-extension-vpn/image29.png)

3. Klik op **het nu instellen**.
4. Selecteer een type contactpersoon (telefoon voor authenticatie, zakelijke telefoonnummer of mobiele app) op Hallo extra beveiliging verificatie pagina. Vervolgens selecteert u een land of regio en selecteer een methode. Hallo methode hangt af van de contactpersoon dat die u selecteert. Bijvoorbeeld, als u de mobiele app kiest, kunt u selecteren of meldingen voor tooreceive voor verificatie of toouse een verificatiecode. Hallo in de volgende procedure wordt ervan uitgegaan dat u kiest **mobiele app** als Hallo contactpersoon type.

 ![Telefoon-verificatie](./media/nps-extension-vpn/image30.png)

5. Selecteer mobiele app, klik op **ontvangen van meldingen voor verificatie**, en vervolgens **instellen**. 

 ![Verificatie van de mobiele App](./media/nps-extension-vpn/image31.png)
 
6. Als u dit nog niet hebt gedaan, mobiele Hallo authenticator-app op uw apparaat installeert. 
7. Volg de instructies Hallo in Hallo mobiele app tooscan Hallo gepresenteerd QR-code of Hallo gegevens handmatig invoeren en klik vervolgens op **gedaan**.

 ![Mobiele App configureren](./media/nps-extension-vpn/image32.png)

8. Klik op Hallo extra beveiliging verificatie pagina op **Contact met mij opnemen** en antwoord verzonden toonotification tooyour apparaat.
9. Voer een telefoonnummer op Hallo extra beveiliging verificatie pagina als u toegang toohello mobiele app verliest en klikt u op **volgende**.

 ![Mobiele telefoonnummer](./media/nps-extension-vpn/image33.png)
 
10. Klik op Hallo aanvullende beveiligingsverificatie, **gedaan**.

Hallo-apparaat is nu geconfigureerd tooprovide een tweede methode voor verificatie. Zie voor meer informatie over het instellen van accounts voor verificatie in twee stappen [Mijn account voor verificatie in twee stappen instellen](./end-user/multi-factor-authentication-end-user-first-time.md).

## <a name="install-and-configure-nps-extension"></a>Installeren en configureren van NPS-uitbreiding

Deze sectie bevat instructies voor het configureren van VPN-toouse Azure MFA voor clientverificatie Hello VPN-Server.

Nadat u installeren en configureren van de NPS-uitbreiding hello, alle RADIUS gebaseerde clientverificatie dat is verwerkt door deze server is vereist toouse Azure MFA. Als niet alle VPN-gebruikers zijn geregistreerd bij Azure MFA, kunt u een andere RADIUS-server tooauthenticate gebruikers die geen geconfigureerde toouse MFA instellen. Of u kunt een registervermelding waarmee gebruikers met een handicap tooprovide een tweede verificatiefactor alleen maken als deze zijn ingeschreven in MFA. 

Maak een nieuwe tekenreekswaarde met de naam _REQUIRE_USER_MATCH in HKLM\SOFTWARE\Microsoft\AzureMfa_, en stel Hallo waarde tooTRUE of ONWAAR. 

 ![Gebruikersovereenkomst vereist](./media/nps-extension-vpn/image34.png)
 
Als het Hallo-waarde is ingesteld tooTRUE of niet is ingesteld, worden alle verificatieaanvragen onderwerp tooan MFA uitdaging. Als het Hallo-waarde is tooFALSE ingesteld, worden MFA uitdagingen alleen toousers die zijn ingeschreven bij MFA uitgegeven. Gebruik alleen Hallo FALSE instelling tests of in een productieomgeving gedurende een periode voorbereiding.

### <a name="acquire-azure-active-directory-guid-id"></a>ID van Azure Active Directory-GUID verkrijgen

Als onderdeel van het Hallo-configuratie van Hallo NPS-extensie moet u beheerdersreferenties toosupply en hello Azure Active Directory-ID voor uw Azure AD-tenant. Hallo stappen hieronder ziet u hoe tooget hello tenant-id.

1. Meld u aan toohello Azure-portal op [https://portal.azure.com](https://portal.azure.com) als globale beheerder van de Hallo van hello Azure-tenant.
2. Klik in het Hallo linkernavigatiebalk, op Hallo **Azure Active Directory** pictogram.
3. Klik op **Eigenschappen**.
4. toocopy uw map-ID toohello Klembord, selecteer Hallo **kopie** pictogram.
 
 ![Map-ID](./media/nps-extension-vpn/image35.png)

### <a name="install-hello-nps-extension"></a>Hallo NPS uitbreiding installeren
Hallo NPS-uitbreiding moet toobe geïnstalleerd op een server met Network Policy Hallo en toegang tot Services (NPS)-functie is geïnstalleerd en die functies als Hallo RADIUS-server in uw ontwerp. Installeer geen Hallo NPS-extensie op uw extern bureaublad-Server.

1. Download Hallo NPS-extensie van [https://aka.ms/npsmfa](https://aka.ms/npsmfa). 
2. Hallo setup uitvoerbaar bestand (NpsExtnForAzureMfaInstaller.exe) toohello NPS-server kopiëren.
3. Dubbelklik op het Hallo-NPS-server op **NpsExtnForAzureMfaInstaller.exe**. Als u wordt gevraagd, klikt u op **uitvoeren**.
4. Controleer in Hallo NPS-extensie voor Azure MFA-dialoogvenster Hallo softwarelicentievoorwaarden, Controleer **ik ga akkoord toohello licentievoorwaarden**, en klik op **installeren**.

 ![NPS-uitbreiding](./media/nps-extension-vpn/image36.png)
 
5. In Hallo NPS-extensie voor Azure MFA-dialoogvenster, klikt u op **sluiten**.  

 ![Setup is voltooid](./media/nps-extension-vpn/image37.png) 
 
### <a name="configure-certificates-for-use-with-hello-nps-extension-using-a-powershell-script"></a>Configureren van certificaten voor gebruik met Hallo NPS-extensie met een PowerShell-script
beveiligde communicatie tooensure en zekerheid, moet u tooconfigure certificaten voor gebruik door Hallo NPS-uitbreiding. Hallo NPS onderdelen zijn Windows PowerShell-script waarmee een zelfondertekend certificaat voor gebruik met NPS worden geconfigureerd. 

Hallo script voert Hallo van de volgende activiteiten:

* Een zelfondertekend certificaat gemaakt
* Koppelt de openbare sleutel van certificaat tooservice principal over Azure AD
* Winkels Hallo certificaat in archief van de lokale machine Hallo
* Verleent toegang tot toohello van het certificaat van persoonlijke sleutels toohello netwerkgebruiker
* Network Policy Server-service wordt opnieuw gestart

Als u wilt uw eigen certificaten toouse, u moet tooassociate Hallo publiek van uw certificaat toohello service principle op Azure AD, enzovoort.
toouse hello script, Hallo extensie voorzien van uw Azure Active Directory-beheerdersreferenties en hello Azure Active Directory-tenant-ID u eerder hebt gekopieerd. Hallo-script uitvoeren op elke NPS-server waarop u Hallo NPS extensie installeert.

1. Open een administratieve Windows PowerShell-prompt.
2. Typ achter de PowerShell-prompt Hallo _cd 'c:\Program Files\Microsoft\AzureMfa\Config'_, en druk op **ENTER**.
3. Type _.\AzureMfsNpsExtnConfigSetup.ps1_, en druk op **ENTER**. 
 * Hallo script controleert toosee als hello Azure Active Directory PowerShell-module is geïnstalleerd. Als dit niet is geïnstalleerd, installeert Hallo script Hallo-module voor u.
 
 ![PowerShell](./media/nps-extension-vpn/image38.png)
 
4. Nadat Hallo script Hallo-installatie van de PowerShell-module Hallo heeft geverifieerd, wordt het dialoogvenster hello Azure Active Directory PowerShell-module weergegeven. In het dialoogvenster hello, Voer uw Azure AD-referenties en het wachtwoord en klikt u op **aanmelden**. 
 
 ![PowerShell aanmelden](./media/nps-extension-vpn/image39.png)
 
5. Wanneer u wordt gevraagd, plak Hallo tenant-ID u toohello Klembord eerder hebt gekopieerd en druk op **ENTER**. 

 ![Tenant-id](./media/nps-extension-vpn/image40.png)

6. Hallo script maakt een zelfondertekend certificaat en andere configuratiewijzigingen uitvoert. Hallo-uitvoer is vergelijkbaar met Hallo afbeelding hieronder wordt weergegeven.

 ![Zelf-ondertekend certificaat](./media/nps-extension-vpn/image41.png)

7. Hallo-server opnieuw opstarten.
 
### <a name="verify-configuration"></a>Configuratie controleren
tooverify hello configuratie, moet u tooestablish een nieuwe VPN-verbinding met VPN-server. Nadat het is uw referenties invoeren voor primaire verificatie, Hallo VPN-verbinding wordt gewacht op Hallo secundaire verificatie toosucceed voordat Hallo-verbinding tot stand is gebracht, zoals hieronder wordt weergegeven. 

 ![Configuratie controleren](./media/nps-extension-vpn/image42.png)

Als u met secundaire verificatiemethode Hallo die u eerder hebt geconfigureerd in de Azure MFA verifiëren, bent u verbonden toohello resource. Als de secundaire verificatie Hallo niet lukt, worden u tooresource toegang geweigerd. 

In onderstaande Hallo verificator Hallo voorbeeld is de app op een Windows phone gebruikte tooprovide Hallo secundaire verificatie.

 ![Het Account verifiëren](./media/nps-extension-vpn/image43.png)

Nadat u bent geverifieerd met behulp van de secundaire methode hello, kunt u access toohello virtuele poort op Hallo VPN-server zijn toegekend. Omdat u vereiste toouse een methode van de secundaire verificatie via een mobiele app op een vertrouwd apparaat was, Hallo-logboek in proces is echter veiliger dan het zou doen met alleen een gebruikersnaam / wachtwoord combinatie.

### <a name="view-event-viewer-logs-for-successful-logon-events"></a>Logboeken voor geslaagde aanmeldingsgebeurtenissen weergeven
tooview Hallo geslaagde aanmeldingsgebeurtenissen worden geregistreerd in Logboeken van de Windows-Logboeken Hallo, kunt u Windows PowerShell-opdracht tooquery Hallo beveiligingslogboek van Windows op Hallo NPS-server na Hallo uitgeven.

tooquery geslaagde aanmeldingsgebeurtenissen in Hallo-logboeken voor beveiliging Hallo opdracht, na gebruiken
* _Get-WinEvent - logboeknaam beveiliging_ | waar {$_.ID - eq '6272'} | FL 

 ![Beveiliging-Logboeken](./media/nps-extension-vpn/image44.png)
 
U kunt ook beveiligingslogboek Hallo Hallo Network Policy and Access Services aangepaste weergave of bekijken, zoals hieronder wordt weergegeven:

 ![Beleid voor toegang tot het netwerk](./media/nps-extension-vpn/image45.png)

Op Hallo server waar u Hallo NPS-extensie voor Azure MFA hebt geïnstalleerd, vindt u Event Viewer-logboeken toestelnummer op specifieke toohello **toepassingen en Services Logs\Microsoft\AzureMfa**. 

* _Get-WinEvent - logboeknaam beveiliging_ | waar {$_.ID - eq '6272'} | FL

 ![Aantal gebeurtenissen](./media/nps-extension-vpn/image46.png)

## <a name="troubleshoot-guide"></a>Problemen met de gids
Als het Hallo-configuratie werkt niet zoals verwacht, is een goede plaats toostart tootroubleshoot tooverify die gebruiker Hallo geconfigureerde toouse Azure MFA is. Hallo gebruiker verbinding te maken hebben[https://portal.azure.com](https://portal.azure.com). Als deze wordt gevraagd om secundaire verificatie en kunnen worden geverifieerd, kunt u een onjuiste configuratie van Azure MFA elimineren.

Als Azure MFA voor Hallo gebruiker (s) werkt, moet u relevante gebeurtenislogboeken Hallo bekijken. Het gaat hierbij om Hallo gebeurtenis voor beveiliging, operationele Gateway en Azure MFA logboeken die worden beschreven in de vorige sectie Hallo. 

Hieronder volgt een voorbeeld van uitvoer van beveiligingslogboek met een mislukte aanmeldingsgebeurtenis (gebeurtenis-ID 6273):

 ![Beveiligingslogboek](./media/nps-extension-vpn/image47.png)

Hieronder vindt u een bijbehorende gebeurtenis uit Hallo AzureMFA Logboeken:

 ![Azure MFA-Logboeken](./media/nps-extension-vpn/image48.png)

Geavanceerde tooperform problemen met de opties, Raadpleeg Hallo NPS indeling databaselogboekbestanden waarop Hallo NPS-service is geïnstalleerd. Deze logboekbestanden worden gemaakt in _%SystemRoot%\System32\Logs_ map als CSV-bestanden. Voor een beschrijving van deze logboekbestanden, Zie [interpreteren NPS indeling databaselogboekbestanden](https://technet.microsoft.com/library/cc771748.aspx). 

Hallo-items in deze logboekbestanden zijn moeilijk toointerpret zonder ze te importeren in een database of een werkblad. U vindt een getal van IAS parsers online tooassist Hallo u in het interpreteren van logboekbestanden. Hieronder vindt u Hallo-uitvoer van een dergelijke downloadbare [shareware toepassing](http://www.deepsoftware.com/iasviewer): 

 ![Shareware toepassing](./media/nps-extension-vpn/image49.png)

Ten slotte voor extra opties oplossen, kunt u een programma voor protocolanalyse zoals Wireshark of [Microsoft Message Analyzer](https://technet.microsoft.com/library/jj649776.aspx). Hallo toont volgende afbeelding van Wireshark Hallo RADIUS-berichten tussen Hallo VPN-server en Hallo NPS-server.

 ![Microsoft Message Analyzer](./media/nps-extension-vpn/image50.png)

Zie voor meer informatie [uw bestaande NPS-infrastructuur integreren met Azure multi-factor Authentication](multi-factor-authentication-nps-extension.md).  

## <a name="next-steps"></a>Volgende stappen
[Hoe tooget Azure multi-factor Authentication](multi-factor-authentication-versions-plans.md)

[Extern bureaublad-gateway en Azure Multi-Factor Authentication-server met behulp van RADIUS](multi-factor-authentication-get-started-server-rdg.md)

[Uw on-premises adreslijsten integreren met Azure Active Directory](../active-directory/connect/active-directory-aadconnect.md)

