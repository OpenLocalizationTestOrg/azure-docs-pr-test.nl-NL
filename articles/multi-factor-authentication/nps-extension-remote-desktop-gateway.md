---
title: aaaRemote bureaublad-Gateway-integratie met Azure MFA NPS extensie | Microsoft Docs
description: Dit artikel wordt beschreven in uw infrastructuur voor extern bureaublad-gatewayserver integreren met Azure MFA met Hallo Network Policy Server (NPS)-uitbreiding voor Microsoft Azure.
services: active-directory
keywords: Azure MFA integreren van extern bureaublad-Gateway, Azure Active Directory, uitbreiding van Network Policy Server
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
ms.openlocfilehash: ae5f6864416582bd82b787005ca787988d23a813
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
#  <a name="integrate-your-remote-desktop-gateway-infrastructure-using-hello-network-policy-server-nps-extension-and-azure-ad"></a>De infrastructuur van uw extern bureaublad-Gateway met Hallo Network Policy Server (NPS)-extensie en Azure AD integreren

Dit artikel bevat informatie voor het integreren van uw infrastructuur voor extern bureaublad-Gateway met Azure multi-factor Authentication (MFA) met behulp van Hallo Network Policy Server (NPS)-uitbreiding voor Microsoft Azure. 

Hallo Service NPS (Network Policy)-extensie voor Azure kan klanten toosafeguard Remote Authentication Dial-In User Service (RADIUS) clientauthenticatie met behulp van Azure's cloud-gebaseerde [multi-factor Authentication (MFA)](multi-factor-authentication.md). Deze oplossing biedt verificatie in twee stappen voor het toevoegen van een tweede beveiligingslaag beveiliging toouser aanmeldingen en transacties.

In dit artikel bevat stapsgewijze instructies voor het Hallo NPS infrastructuur integreren met Azure MFA met Hallo NPS-extensie voor Azure. Hierdoor veilige verificatie voor gebruikers die zich toolog op tooa extern bureaublad-Gateway. 

Hallo Network Policy and Access Services (NPS) biedt organisaties Hallo mogelijkheid toodo Hallo volgende:
* Centrale locatie voor het Hallo-beheer en controle van netwerkaanvragen definiëren door te geven die een verbinding kunt maken, welke tijdstippen verbindingen zijn toegestaan, Hallo duur van verbindingen en Hallo beveiligingsniveau dat clients moeten gebruiken tooconnect, enzovoort. In plaats van deze beleidsregels geven op elke server VPN- of -Gateway van de extern bureaublad (RD), kunnen deze beleidsregels eenmaal worden opgegeven op een centrale locatie. Hallo RADIUS-protocol biedt Hallo gecentraliseerde verificatie, autorisatie en Accounting (AAA). 
* Instellen en afdwingen van statusbeleid voor Network Access Protection (NAP) client om te bepalen of apparaten onbeperkte of beperkte toegang tot toonetwork bronnen worden verleend.
* Geef een manier tooenforce verificatie en autorisatie voor toegang tot too802.1x-compatibele draadloze toegangspunten en Ethernet-switches.    

Normaal gesproken organisaties gebruiken toosimplify NPS (RADIUS) en centraliseer het Hallo-beheer van VPN-beleid. Echter veel organisaties ook NPS toosimplify gebruiken en centraliseer het Hallo-beheer van extern bureaublad bureaublad Verbindingsautorisatiebeleid (RD CAP's). 

Organisaties kunnen ook NPS worden geïntegreerd met Azure MFA tooenhance beveiliging en een hoge mate van compatibiliteit bieden. Dit zorgt ervoor dat gebruikers tot stand toolog van verificatie in twee stappen op toohello extern bureaublad-Gateway brengen. Voor gebruikers toobe toegang verleend, moeten ze bieden de combinatie van gebruikersnaam en wachtwoord met informatie die gebruiker Hallo heeft in het besturingselement. Deze informatie moet worden vertrouwd en eenvoudig niet wordt gedupliceerd, zoals een mobiele telefoonnummer, een vast, een toepassing op een mobiel apparaat, enzovoort.

De beschikbaarheid van de voorafgaande toohello Hallo NPS-extensie voor Azure, klanten die tooimplement %0 verificatie willen geïntegreerd NPS en Azure MFA-omgevingen tooconfigure had en onderhouden van een afzonderlijke MFA-Server in on-premises omgeving Hallo als beschreven in [extern bureaublad-Gateway en Azure multi-factor Authentication-Server met behulp van RADIUS](multi-factor-authentication-get-started-server-rdg.md).

Hallo-beschikbaarheid van Hallo NPS-extensie voor Azure biedt nu organisaties Hallo keuze toodeploy een on-premises op basis van MFA oplossing of een cloud-verificatie op basis van MFA-oplossing toosecure RADIUS-client.

## <a name="authentication-flow"></a>Verificatiestroom

Voor gebruikers verleend toobe toegang toonetwork resources via een extern bureaublad-Gateway, moeten voldoen aan Hallo condities die zijn opgegeven in een extern bureaublad-Verbindingsverificatiebeleid (RD CAP) en een extern bureaublad-bronautorisatiebeleid (RD RAP). RD CAP's opgeven die gemachtigde tooconnect tooRD Gateways. RD RAP's Hallo-netwerkbronnen, zoals externe bureaubladen of externe apps opgeven die Hallo-gebruiker is toegestaan tooconnect toothrough Hallo RD-Gateway. 

Een extern bureaublad-Gateway kan worden geconfigureerd toouse een centraal beleid store voor RD CAP's. RD RAP's niet een centraal beleid gebruiken zoals ze worden verwerkt op Hallo RD-Gateway. Een voorbeeld van een extern bureaublad-Gateway geconfigureerd toouse een centraal beleid store voor RD CAP's is een RADIUS-client tooanother NPS-server die als Hallo centraal beleid store fungeert.

Wanneer Hallo NPS-extensie voor Azure is geïntegreerd met hello NPS- en extern bureaublad-Gateway, is geslaagd Hallo-authenticatiestroom als volgt:

1. Hallo extern bureaublad-gatewayserver ontvangt een verificatieaanvraag van een resource externe bureaubladgebruiker tooconnect tooa, zoals een extern bureaublad-sessie. Hallo extern bureaublad-gatewayserver fungeert als een RADIUS-client, converteert tooa Hallo-RADIUS-toegangsaanvraag aanvraagbericht en verzendt Hallo-bericht toohello RADIUS (NPS)-server waarop NPS-extensie Hallo is geïnstalleerd. 
2. Hallo gebruikersnaam en wachtwoord combinatie is geverifieerd in Active Directory en Hallo gebruiker is geverifieerd.
3. Als alle Hallo voorwaarden zoals opgegeven in de NPS-verbindingsaanvraag Hallo en netwerkbeleid hello wordt voldaan (bijvoorbeeld de tijd van de dag of groep lidmaatschap beperkingen), een aanvraag voor de secundaire verificatie met Azure MFA Hallo NPS-extensie wordt geactiveerd. 
4. Azure MFA communiceert met Azure AD, haalt Hallo Gebruikersdetails en voert Hallo secundaire verificatie via Hallo-methode is geconfigureerd door de gebruiker hello (SMS-bericht, mobiele app, enzovoort). 
5. Bij voltooiing van Hallo MFA uitdaging communiceert Azure MFA Hallo resultaat toohello NPS-extensie.
6. Hallo NPS-server waarop het Hallo-uitbreiding is geïnstalleerd verzendt een bericht RADIUS Access-Accept voor Hallo RD CAP beleid toohello extern bureaublad-gatewayserver.
7. Hallo gebruiker toegang verleend toohello aangevraagd netwerkbron via Hallo RD-Gateway.

## <a name="prerequisites"></a>Vereisten
Deze sectie details Hallo vereisten nodig voordat de integratie van Azure MFA met Hallo extern bureaublad-Gateway. Voordat u begint, moet u de volgende vereisten is voldaan Hallo hebben.  

* Infrastructuur voor extern bureaublad-Services (RDS)
* Azure MFA-licentie
* Windows Server-software
* De rol en Network Policy and Access Services (NPS)
* Azure AD gesynchroniseerd met on-premises AD dat 
* GUID-ID van Azure Active Directory

### <a name="remote-desktop-services-rds-infrastructure"></a>Infrastructuur voor extern bureaublad-Services (RDS)
U moet beschikken over een werkende extern bureaublad-Services (RDS)-infrastructuur. Als u dat niet doet, kunt u deze infrastructuur snel maken in Azure start met behulp van de volgende Hallo snelle sjabloon: [implementatie van extern bureaublad Sessieverzameling maken](https://github.com/Azure/azure-quickstart-templates/tree/ad20c78b36d8e1246f96bb0e7a8741db481f957f/rds-deployment). 

Als u wilt maken toomanually een on-premises RDS infrastructuur snel voor testdoeleinden, volg Hallo stappen toodeploy een. 
**Meer informatie**: [RDS implementeren met Azure snel starten](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/rds-in-azure) en [Basic RDS infrastructuur implementeren](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/rds-deploy-infrastructure). 

### <a name="licenses"></a>Licenties
Vereist, is een licentie voor Azure MFA, die beschikbaar via een Azure AD Premium, Enterprise Mobility plus Security (EMS) of een MFA-abonnement is. Zie voor meer informatie [hoe tooget Azure multi-factor Authentication](multi-factor-authentication-versions-plans.md). Voor testdoeleinden kunt u een proefabonnement.

### <a name="software"></a>Software
Hallo NPS-uitbreiding vereist Windows Server 2008 R2 SP1 of hoger met Hallo NPS-functieservice is geïnstalleerd. Alle Hallo stappen in deze sectie zijn uitgevoerd met behulp van Windows Server 2016.

### <a name="network-policy-and-access-services-nps-role"></a>De rol en Network Policy and Access Services (NPS)
Hallo NPS-rolservice biedt Hallo RADIUS-server en client-functionaliteit, evenals een netwerktoegangsbeleid health-service. Deze functie moet worden geïnstalleerd op ten minste twee computers in uw infrastructuur: extern bureaublad-Gateway en een andere Hallo lidserver of domeincontroller. Hallo-functie is standaard al aanwezig op Hallo computer geconfigureerd als Hallo extern bureaublad-Gateway.  U moet ook Hallo NPS serverfunctie installeren op ten minste op een andere computer, zoals een lidserver of domeincontroller.

Voor informatie over het installeren van de functie NPS Hallo service WindowsServer 2012 of ouder, Zie [installeren van een NAP-statusbeleidsserver](https://technet.microsoft.com/library/dd296890.aspx). Zie voor een beschrijving van best practices voor NPS, inclusief Hallo aanbeveling tooinstall NPS op een domeincontroller [Best Practices voor NPS](https://technet.microsoft.com/library/cc771746).

### <a name="azure-active-directory-synched-with-on-premises-active-directory"></a>Azure Active Directory worden gesynchroniseerd met de lokale Active Directory 
toouse hello NPS-extensie, on-premises gebruikers moeten worden gesynchroniseerd met Azure AD en ingeschakeld voor MFA. Deze sectie wordt ervan uitgegaan dat de on-premises gebruikers zijn gesynchroniseerd met Azure AD via AD Connect. Voor informatie over Azure AD connect, Zie [uw on-premises adreslijsten integreren met Azure Active Directory](../active-directory/connect/active-directory-aadconnect.md). 

### <a name="azure-active-directory-guid-id"></a>GUID-ID van Azure Active Directory
tooinstall NPS, moet u tooknow Hallo GUID van hello Azure AD. Hieronder vindt u instructies voor het vinden van Hallo GUID van hello Azure AD.

## <a name="configure-multi-factor-authentication"></a>Multi-factor Authentication configureren 
Deze sectie geeft instructies voor het integreren van Azure MFA met Hallo extern bureaublad-Gateway. U moet als beheerder hello Azure MFA-service configureren voordat gebruikers hun apparaten meerledige of toepassingen zichzelf kunnen registreren.

Volg de stappen Hallo in [aan de slag met Azure multi-factor Authentication in de cloud Hallo](multi-factor-authentication-get-started-cloud.md) tooenable MFA voor uw Azure AD-gebruikers. 

### <a name="configure-accounts-for-two-step-verification"></a>Accounts configureren voor verificatie in twee stappen
Wanneer een account is ingeschakeld voor MFA, u niet kunt aanmelden beheerst tooresources door Hallo MFA-beleid totdat u hebt een vertrouwd apparaat toouse is geconfigureerd voor de tweede verificatiefactor Hallo hebt geverifieerd met behulp van verificatie in twee stappen.

Volg de stappen Hallo in [wat Azure multi-factor Authentication betekent voor mij?](./end-user/multi-factor-authentication-end-user.md) toounderstand en uw apparaten correct configureren voor meervoudige verificatie met uw gebruikersaccount.

## <a name="install-and-configure-nps-extension"></a>Installeren en configureren van NPS-uitbreiding
Deze sectie bevat instructies voor het configureren van RDS infrastructuur toouse Azure MFA voor clientverificatie Hello extern bureaublad-Gateway.

### <a name="acquire-azure-active-directory-guid-id"></a>ID van Azure Active Directory-GUID verkrijgen

Als onderdeel van het Hallo-configuratie van Hallo NPS-extensie moet u beheerdersreferenties toosupply en hello Azure AD-ID voor uw Azure AD-tenant. Hallo stappen laten zien hoe tooget hello tenant-id.

1. Meld u aan toohello [Azure-portal](https://portal.azure.com) als globale beheerder van de Hallo van hello Azure-tenant.
2. Selecteer in de Hallo linkernavigatiebalk, Hallo **Azure Active Directory** pictogram.
3. Selecteer **eigenschappen**.
4. In de eigenschappenblade Hallo naast Hallo map-ID, klikt u op Hallo **kopie** pictogram, zoals hieronder aangegeven, toocopy Hallo ID tooclipboard.

 ![Eigenschappen](./media/nps-extension-remote-desktop-gateway/image1.png)

### <a name="install-hello-nps-extension"></a>Hallo NPS uitbreiding installeren
Hallo NPS uitbreiding installeren op een server met Network Policy Hallo en Access Services (NPS)-functie geïnstalleerd. Dit fungeert als Hallo RADIUS-server voor uw ontwerp. 

>[!Important]
> Zorg ervoor dat u niet Hallo NPS-extensie op uw server voor extern bureaublad-Gateway installeert.
> 

1. Hallo downloaden [NPS extensie](https://aka.ms/npsmfa). 
2. Hallo setup uitvoerbaar bestand (NpsExtnForAzureMfaInstaller.exe) toohello NPS-server kopiëren.
3. Dubbelklik op het Hallo-NPS-server op **NpsExtnForAzureMfaInstaller.exe**. Als u wordt gevraagd, klikt u op **uitvoeren**.
4. Controleer in Hallo NPS-extensie voor Azure MFA-dialoogvenster Hallo softwarelicentievoorwaarden, Controleer **ik ga akkoord toohello licentievoorwaarden**, en klik op **installeren**.
 
  ![Azure MFA-instellingen](./media/nps-extension-remote-desktop-gateway/image2.png)

5. Klik op Sluiten in Hallo NPS-extensie voor Azure MFA-dialoogvenster. 

  ![NPS-extensie voor Azure MFA](./media/nps-extension-remote-desktop-gateway/image3.png)

### <a name="configure-certificates-for-use-with-hello-nps-extension-using-a-powershell-script"></a>Configureren van certificaten voor gebruik met Hallo NPS-extensie met een PowerShell-script
Vervolgens moet u tooconfigure certificaten voor gebruik door Hallo NPS extensie tooensure beveiligde communicatie en zekerheid. Hallo NPS onderdelen zijn Windows PowerShell-script waarmee een zelfondertekend certificaat voor gebruik met NPS worden geconfigureerd. 

Hallo script voert Hallo van de volgende activiteiten:

* Een zelfondertekend certificaat gemaakt
* Koppelt de openbare sleutel van certificaat tooservice principal over Azure AD
* Winkels Hallo certificaat in archief van de lokale machine Hallo
* Verleent toegang tot persoonlijke sleutel toohello-netwerkgebruiker toohello-certificaat
* Network Policy Server-service wordt opnieuw gestart

Als u wilt uw eigen certificaten toouse, u moet tooassociate Hallo publiek van uw certificaat toohello service principle op Azure AD, enzovoort.

toouse hello script, Hallo extensie voorzien van uw Azure AD-beheerdersreferenties en hello Azure AD-tenant-ID die u eerder hebt gekopieerd. Hallo-script uitvoeren op elke NPS-server waarop u Hallo NPS uitbreiding hebt geïnstalleerd. Vervolgens Hallo na:

1. Open een administratieve Windows PowerShell-prompt.
2. Typ achter de PowerShell-prompt Hallo **cd 'c:\Program Files\Microsoft\AzureMfa\Config'**, en druk op **ENTER**.
3. Type _.\AzureMfsNpsExtnConfigSetup.ps1_, en druk op **ENTER**. Hallo script controleert toosee als hello Azure Active Directory PowerShell-module is geïnstalleerd. Als niet geïnstalleerd, installeert Hallo script Hallo-module voor u.

  ![Azure AD PowerShell](./media/nps-extension-remote-desktop-gateway/image4.png)
  
4. Nadat Hallo script Hallo-installatie van de PowerShell-module Hallo heeft geverifieerd, wordt het dialoogvenster hello Azure Active Directory PowerShell-module weergegeven. In het dialoogvenster hello, Voer uw Azure AD-referenties en het wachtwoord en klikt u op **aanmelden**.

  ![Powershell-account openen](./media/nps-extension-remote-desktop-gateway/image5.png)

5. Wanneer u wordt gevraagd, plak Hallo tenant-ID u toohello Klembord eerder hebt gekopieerd en druk op **ENTER**.

  ![Tenant-ID invoeren](./media/nps-extension-remote-desktop-gateway/image6.png)

6. Hallo script maakt een zelfondertekend certificaat en andere configuratiewijzigingen uitvoert. Hallo-uitvoer moet zoals Hallo afbeelding hieronder wordt weergegeven.

  ![Zelfondertekend certificaat](./media/nps-extension-remote-desktop-gateway/image7.png)

## <a name="configure-nps-components-on-remote-desktop-gateway"></a>NPS-onderdelen in extern bureaublad-Gateway configureren
In deze sectie configureert u Hallo-Verbindingsautorisatiebeleid voor extern bureaublad-Gateway en andere instellingen voor RADIUS.

Hallo-authenticatiestroom is vereist dat RADIUS-berichten worden uitgewisseld tussen Hallo extern bureaublad-Gateway en Hallo NPS-server waarop Hallo NPS-Server is geïnstalleerd. Dit betekent dat u instellingen voor RADIUS-client moet configureren op zowel extern bureaublad-Gateway als Hallo NPS-server waarop NPS-extensie Hallo is geïnstalleerd. 

### <a name="configure-remote-desktop-gateway-connection-authorization-policies-toouse-central-store"></a>Extern bureaublad-Gateway verbinding beleid toouse centrale verificatiearchief configureren
Extern bureaublad Verbindingsautorisatiebeleid (RD CAP's) opgeven Hallo-vereisten voor aangesloten tooa extern bureaublad-Gateway-server. Extern bureaublad Verbindingsautorisatiebeleid kan lokaal worden opgeslagen (standaard) of ze kunnen worden opgeslagen in een centraal RD CAP-archief waarop NPS wordt uitgevoerd. tooconfigure integratie van Azure MFA met RDS, moet u toospecify Hallo gebruik van een centrale store.

1. Open op Hallo extern bureaublad-gatewayserver, **Serverbeheer**. 
2. Klik op het menu Hallo **hulpprogramma's**, wijst u te**extern bureaublad-Services**, en klik vervolgens op **extern bureaublad-gatewaybeheer**.

  ![Externe bureaubladservices](./media/nps-extension-remote-desktop-gateway/image8.png)

3. Hallo RD-Gateway Manager, met de rechtermuisknop op  **\[servernaam\] (lokaal)**, en klik op **eigenschappen**.

  ![Servernaam](./media/nps-extension-remote-desktop-gateway/image9.png)

4. Selecteer in de Hallo eigenschappen in het dialoogvenster Hallo **RD CAP** tabblad archief.
5. Selecteer het tabblad Hallo RD CAP-archief voor **centrale Server met NPS**. 
6. In Hallo **Voer een naam of IP-adres voor Hallo-server met NPS** veld, type Hallo IP-adres of de servernaam van Hallo-server waarop u Hallo NPS uitbreiding hebt geïnstalleerd.

  ![Voer de naam of IP-adres](./media/nps-extension-remote-desktop-gateway/image10.png)
  
7. Klik op **Add**.
8. In Hallo **gedeelde geheim** in het dialoogvenster voert u een gedeeld geheim en klik vervolgens op **OK**. Zorg ervoor dat u dit gedeelde geheim vastlegt en Hallo record veilig opslaan.

 >[!NOTE]
 >Gedeelde geheim gebruikt tooestablish vertrouwensrelatie tussen Hallo RADIUS-servers en clients. Een lange en complexe wachtwoord maken.
 >

 ![Gedeeld geheim](./media/nps-extension-remote-desktop-gateway/image11.png)

9. Klik op **OK** tooclose Hallo dialoogvenster.

### <a name="configure-radius-timeout-value-on-remote-desktop-gateway-nps"></a>RADIUS-time-outwaarde op extern bureaublad-Gateway NPS configureren
Er tooensure is tijd toovalidate gebruikers referenties, verificatie in twee stappen uitvoeren, antwoorden ontvangen en berichten tooRADIUS reageren, nodig tooadjust Hallo RADIUS-time-outwaarde is.

1. Klik op Hallo extern bureaublad-gatewayserver, in Serverbeheer op **extra**, en klik vervolgens op **Network Policy Server**. 
2. In Hallo **NPS (lokaal)** console, vouw **RADIUS-Clients en Servers**, en selecteer **externe RADIUS-Server**.

 ![Externe RADIUS-Server](./media/nps-extension-remote-desktop-gateway/image12.png)

3. Dubbelklik in het detailvenster hello, **groep TS-GATEWAYSERVER**.

 >[!NOTE]
 >Deze groep van RADIUS-Server is gemaakt toen u de centrale server Hallo voor NPS-beleid hebt geconfigureerd. Hallo RD-Gateway stuurt RADIUS-berichten toothis server of de groep servers als meer dan één in Hallo-groep.
 >

4. In Hallo **eigenschappen TS GATEWAY SERVERGROEP** in het dialoogvenster, selecteer Hallo IP-adres of naam van de NPS-server die u hebt geconfigureerd toostore RD CAP's Hallo en klik vervolgens op **bewerken**. 

 ![Groep TS-gatewayserver](./media/nps-extension-remote-desktop-gateway/image13.png)

5. In Hallo **RADIUS-Server bewerken** dialoogvenster, selecteer Hallo **Load Balancing** tabblad.
6. In Hallo **Load Balancing** tabblad in Hallo **verwijderd van het aantal seconden zonder reactie voordat de aanvraag wordt beschouwd als** veld, wijzigt u de standaardwaarde Hallo van 3 tooa waarde tussen 30 en 60 seconden.
7. In Hallo **aantal seconden tussen aanvragen wanneer de server wordt geïdentificeerd als niet beschikbaar** veld, wijzigt u de standaardwaarde Hallo van 30 seconden tooa-waarde die gelijk tooor groter zijn dan u hebt opgegeven in de vorige stap Hallo Hallo-waarde is.

 ![RADIUS-Server bewerken](./media/nps-extension-remote-desktop-gateway/image14.png)

8.  Klik twee maal tooclose Hallo-dialoogvensters.

### <a name="verify-connection-request-policies"></a>Controleer of u beleid voor verbindingsaanvragen 
Bij het configureren van Hallo RD-Gateway toouse een centraal beleid store voor Verbindingsautorisatiebeleid, is Hallo RD-Gateway standaard geconfigureerd tooforward CAP aanvragen toohello NPS-server. Hallo NPS-server met Azure MFA-extensie Hallo geïnstalleerd, worden de processen Hallo RADIUS-toegangsaanvraag. Hallo stappen ziet u hoe tooverify Hallo standaardverbinding beleid aanvragen. 

1. Op Hallo RD-Gateway in Hallo NPS (lokaal)-console, vouw **beleid**, en selecteer **beleid voor verbindingsaanvragen**.
2. Met de rechtermuisknop op **verbinding beleid**, en dubbelklik op **TS GATEWAY-AUTORISATIEBELEID**.
3. In Hallo **TS GATEWAY-AUTORISATIEBELEID eigenschappen** dialoogvenster vak, klikt u op Hallo **instellingen** tabblad.
4. Op **instellingen** tabblad onder verbindingsaanvraag, klikt u op **verificatie**. RADIUS-client is geconfigureerd tooforward aanvragen voor verificatie.

 ![Verificatie-instellingen](./media/nps-extension-remote-desktop-gateway/image15.png)
 
5. Klik op **annuleren**. 

## <a name="configure-nps-on-hello-server-where-hello-nps-extension-is-installed"></a>NPS configureren op Hallo-server waarop NPS extensie Hallo is geïnstalleerd
Hallo NPS-server waar Hallo NPS extensie geïnstalleerde behoeften toobe kunnen tooexchange RADIUS-berichten met Hallo NPS-server op Hallo van extern bureaublad-Gateway is. exchange-tooenable dit bericht, moet u tooconfigure Hallo NPS-onderdelen op Hallo-server waarop Hallo NPS-extensie-service is geïnstalleerd. 

### <a name="register-server-in-active-directory"></a>Server registreren in Active Directory
toofunction goed in dit scenario Hallo NPS-server moet toobe geregistreerd in Active Directory.

1. Open **Serverbeheer**.
2. Klik in Serverbeheer op **extra**, en klik vervolgens op **Network Policy Server**. 
3. Hallo Network Policy Server-console met de rechtermuisknop op **NPS (lokaal)**, en klik vervolgens op **server registreren in Active Directory**. 
4. Klik op **OK** twee keer.

 ![Server registreren in AD](./media/nps-extension-remote-desktop-gateway/image16.png)

5. Laat Hallo console geopend voor de volgende procedure Hallo.

### <a name="create-and-configure-radius-client"></a>Maak en configureer de RADIUS-client 
Hallo extern bureaublad-Gateway moet toobe geconfigureerd als een RADIUS-client toohello NPS-server. 

1. Op Hallo NPS-server waarop NPS extensie Hallo is geïnstalleerd, in Hallo **NPS (lokaal)** console, met de rechtermuisknop op **RADIUS-Clients** en klik op **nieuw**.

 ![Nieuwe RADIUS-Clients](./media/nps-extension-remote-desktop-gateway/image17.png)

2. In Hallo **nieuwe RADIUS-client** dialoogvenster Geef een beschrijvende naam, zoals _Gateway_, en Hallo IP-adres of de DNS-naam van Hallo extern bureaublad-gatewayserver. 
3. In Hallo **gedeeld geheim** en Hallo **Bevestig het gedeelde geheim** velden, Voer Hallo dezelfde geheim dat u eerder hebt gebruikt.

 ![Naam en adres](./media/nps-extension-remote-desktop-gateway/image18.png)

4. Klik op **OK** dialoogvenster voor tooclose Hallo nieuwe RADIUS-client.

### <a name="configure-network-policy"></a>Netwerkbeleid configureren
Intrekken Hallo NPS-server met hello Azure MFA-extensie is Hallo aangewezen centrale beleidsarchief voor Hallo verbinding autorisatie beleid (CAP). Daarom moet u tooimplement een LIMIET op Hallo NPS-server tooauthorize geldige verbindingen aanvragen.  

1. Vouw in de NPS (lokaal)-console Hallo **beleid**, en klik op **netwerkbeleid**.
2. Met de rechtermuisknop op **verbindingen tooother-servers voor clienttoegang**, en klik op **beleid dubbele**. 

 ![Dubbele beleid](./media/nps-extension-remote-desktop-gateway/image19.png)

3. Met de rechtermuisknop op **kopie van verbindingen tooother-servers voor clienttoegang**, en klik op **eigenschappen**.

 ![Eigenschappen van het netwerk](./media/nps-extension-remote-desktop-gateway/image20.png)

4. In Hallo **kopie van verbindingen tooother-servers voor clienttoegang** in het dialoogvenster beleidsnaam, Voer in een geschikte naam zoals **RDG_CAP**. Controleer **beleid ingeschakeld**, en selecteer **toegang verlenen**. Selecteer desgewenst in het Type toegang tot het netwerk, **extern bureaublad-Gateway**, of u kunt dit als laten **onbepaald**.

 ![Kopie van verbindingen](./media/nps-extension-remote-desktop-gateway/image21.png)

5.  Klik op Hallo **beperkingen** tabblad en Controleer **toestaan clients tooconnect zonder een verificatiemethode te onderhandelen**.

 ![Clients toestaan tooconnect](./media/nps-extension-remote-desktop-gateway/image22.png)

6. Klik desgewenst op Hallo **voorwaarden** tabblad en voorwaarden waaraan moeten worden voldaan voor Hallo verbinding toobe gemachtigd, bijvoorbeeld lidmaatschap van een specifieke windowsgroep toevoegen.

 ![Voorwaarden](./media/nps-extension-remote-desktop-gateway/image23.png)

7. Klik op **OK**. Wanneer de vraag tooview hello bijbehorende Help-onderwerp, klikt u op **Nee**.
8. Zorg ervoor dat het nieuwe beleid boven Hallo van Hallo-lijst, dat Hallo beleid is ingeschakeld, en dat toegang wordt verleend.

 ![Netwerkbeleid](./media/nps-extension-remote-desktop-gateway/image24.png)

## <a name="verify-configuration"></a>Configuratie controleren
tooverify hello configuratie, moet u toolog op Hallo van extern bureaublad-Gateway met een geschikte RDP-client. Niet zeker toouse een account dat is toegestaan door uw Verbindingsautorisatiebeleid en is ingeschakeld voor Azure MFA. 

Als weergeven in onderstaande afbeelding voor hello, kunt u Hallo **Remote Desktop Web Access** pagina.

![Extern bureaublad-webtoegang](./media/nps-extension-remote-desktop-gateway/image25.png)

Nadat het is uw referenties invoeren voor primaire verificatie, ziet Hallo extern bureaublad-verbinding in het dialoogvenster u een status van externe verbinding tot stand brengen, zoals hieronder wordt weergegeven. 

Als u met secundaire verificatiemethode Hallo die u eerder hebt geconfigureerd in de Azure MFA verifiëren, bent u verbonden toohello resource. Als de secundaire verificatie Hallo niet lukt, worden u tooresource toegang geweigerd. 

![Externe verbinding tot stand brengen](./media/nps-extension-remote-desktop-gateway/image26.png)

In onderstaande Hallo verificator Hallo voorbeeld is de app op een Windows phone gebruikte tooprovide Hallo secundaire verificatie.

![Accounts](./media/nps-extension-remote-desktop-gateway/image27.png)

Nadat u bent geverifieerd met behulp van de secundaire authenticatiemethode hello, kunt u bent aangemeld bij Hallo extern bureaublad-Gateway als normaal. Hallo aanmelden proces is echter veiliger dan het anders zou zijn, omdat u vereiste toouse een methode van de secundaire verificatie via een mobiele app op een vertrouwd apparaat.

### <a name="view-event-viewer-logs-for-successful-logon-events"></a>Logboeken voor geslaagde aanmeldingsgebeurtenissen weergeven
tooview hello geslaagde aanmelden gebeurtenissen in Logboeken van de Windows-Logboeken hello, kunt u na de Windows PowerShell-opdracht tooquery Hallo Windows Terminal Services en Windows-beveiligingslogboeken Hallo uitgeven.

tooquery geslaagde aanmelding gebeurtenissen in Hallo Gateway operationele logboeken _(gebeurtenis logboeken\logboeken toepassingen en Services Logs\Microsoft\Windows\TerminalServices-Gateway\Operational_, Hallo volgende opdrachten gebruiken:

* _Get-WinEvent - logboeknaam Microsoft-Windows-TerminalServices-Gateway/operationeel_ | waar {$_.ID - eq '300'} | FL 
* Deze opdracht geeft Windows-gebeurtenissen die gebruiker Hallo voldaan autorisatie beleid resourcevereisten (RD RAP) en heeft toegang gekregen weergeven.

![Logboeken weergeven](./media/nps-extension-remote-desktop-gateway/image28.png)

* _Get-WinEvent - logboeknaam Microsoft-Windows-TerminalServices-Gateway/operationeel_ | waar {$_.ID - eq "200"} | FL
* Deze opdracht geeft Hallo-gebeurtenissen die worden weergegeven wanneer de gebruiker verbinding autorisatievereisten voldaan.

![Verbindingsverificatie](./media/nps-extension-remote-desktop-gateway/image29.png)

U kunt dit logboek en filter ook bekijken op de gebeurtenis-id's, 300 en 200. tooquery geslaagde aanmeldingsgebeurtenissen in Hallo-logboeken voor beveiliging Hallo volgende opdracht gebruiken:

* _Get-WinEvent - logboeknaam beveiliging_ | waar {$_.ID - eq '6272'} | FL 
* Met deze opdracht kan worden uitgevoerd op een centrale NPS Hallo of Hallo van extern bureaublad-gatewayserver. 

![Geslaagde aanmeldingsgebeurtenissen](./media/nps-extension-remote-desktop-gateway/image30.png)

U kunt ook beveiligingslogboek Hallo Hallo Network Policy and Access Services aangepaste weergave of bekijken, zoals hieronder wordt weergegeven:

![Network Policy and Access Services](./media/nps-extension-remote-desktop-gateway/image31.png)

Op Hallo server waar u Hallo NPS-extensie voor Azure MFA hebt geïnstalleerd, vindt u Event Viewer-logboeken toestelnummer op specifieke toohello _toepassingen en Services Logs\Microsoft\AzureMfa_. 

![Toepassing van de logboeken](./media/nps-extension-remote-desktop-gateway/image32.png)

## <a name="troubleshoot-guide"></a>Problemen met de gids

Als Hallo configuratie niet werkt zoals verwacht, is het Hallo eerste plaats toostart tootroubleshoot tooverify die gebruiker Hallo is geconfigureerde toouse Azure MFA. Hallo gebruiker verbinding toohello [Azure-portal](https://portal.azure.com). Als gebruikers wordt gevraagd om secundaire verificatie en kunnen worden geverifieerd, kunt u een onjuiste configuratie van Azure MFA elimineren.

Als Azure MFA voor Hallo gebruiker (s) werkt, moet u relevante gebeurtenislogboeken Hallo bekijken. Het gaat hierbij om Hallo gebeurtenis voor beveiliging, operationele Gateway en Azure MFA logboeken die worden beschreven in de vorige sectie Hallo. 

Hieronder volgt een voorbeeld van uitvoer van beveiligingslogboek met een mislukte aanmeldingsgebeurtenis (gebeurtenis-ID 6273).

![Mislukte aanmeldingsgebeurtenis](./media/nps-extension-remote-desktop-gateway/image33.png)

Hieronder vindt u een bijbehorende gebeurtenis uit Hallo AzureMFA Logboeken:

![Azure MFA-logboek](./media/nps-extension-remote-desktop-gateway/image34.png)

Geavanceerde tooperform problemen met de opties, Raadpleeg Hallo NPS indeling databaselogboekbestanden waarop Hallo NPS-service is geïnstalleerd. Deze logboekbestanden worden gemaakt in _%SystemRoot%\System32\Logs_ map als CSV-bestanden. 

Voor een beschrijving van deze logboekbestanden, Zie [interpreteren NPS indeling databaselogboekbestanden](https://technet.microsoft.com/library/cc771748.aspx). Hallo-items in deze logboekbestanden kunnen moeilijk toointerpret zonder ze te importeren in een database of een werkblad worden. U kunt verschillende IAS parsers vinden online tooassist die u in het interpreteren van logboekbestanden Hallo. 

Hallo onderstaande afbeelding ziet u uitvoer Hallo van een dergelijke downloadbare [shareware toepassing](http://www.deepsoftware.com/iasviewer). 

![Shareware app](./media/nps-extension-remote-desktop-gateway/image35.png)

Ten slotte voor extra opties oplossen, kunt u een programma voor protocolanalyse, dergelijke [Microsoft Message Analyzer](https://technet.microsoft.com/library/jj649776.aspx). 

Hallo afbeelding hieronder van Microsoft Message Analyzer toont netwerkverkeer gefilterd op RADIUS-protocol met gebruikersnaam Hallo **Contoso\AliceC**.

![Microsoft Message Analyzer](./media/nps-extension-remote-desktop-gateway/image36.png)

## <a name="next-steps"></a>Volgende stappen
[Hoe tooget Azure multi-factor Authentication](multi-factor-authentication-versions-plans.md)

[Extern bureaublad-gateway en Azure Multi-Factor Authentication-server met behulp van RADIUS](multi-factor-authentication-get-started-server-rdg.md)

[Uw on-premises adreslijsten integreren met Azure Active Directory](../active-directory/connect/active-directory-aadconnect.md)
