---
title: Azure multi-factor Authentication-Server is gestart aaaGetting | Microsoft Docs
description: Dit is hello Azure multi-factor authentication-pagina waarop wordt beschreven hoe tooget de slag met Azure MFA-Server.
services: multi-factor-authentication
keywords: verificatieserver, app-activeringspagina voor azure multi factor authentication, downloaden bij verificatieserver
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.assetid: e94120e4-ed77-44b8-84e4-1c5f7e186a6b
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2017
ms.author: joflore
ms.reviewer: alexwe
ms.custom: it-pro
ms.openlocfilehash: 92a6a586eb96375e92a9455ad64e67221001db81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-hello-azure-multi-factor-authentication-server"></a>Aan de slag met hello Azure multi-factor Authentication-Server

<center>![MFA on-premises](./media/multi-factor-authentication-get-started-server/server2.png)</center>

Nu dat we hebben vastgesteld toouse lokale multi-factor Authentication-Server, gaan we aan de slag. Deze pagina bevat een nieuwe installatie van het Hallo-server en instellen met de lokale Active Directory. Als u al Hallo MFA server zijn geïnstalleerd en tooupgrade zoekt, Zie [toohello Upgrade meest recente Azure multi-factor Authentication-Server](multi-factor-authentication-server-upgrade.md). Als u naar informatie zoekt over het installeren van de webservice NET hello, Zie [Deploying hello Azure multi-factor Authentication Server Mobile App Web Service](multi-factor-authentication-get-started-server-webservice.md).

## <a name="plan-your-deployment"></a>Uw implementatie plannen

Voordat u hello Azure multi-factor Authentication-Server hebt gedownload, moet u bedenken wat uw laden en de vereisten voor hoge beschikbaarheid zijn. Gebruik deze informatie toodecide hoe en waar toodeploy.

Een goede richtlijn voor Hallo en de hoeveelheid geheugen die u nodig het aantal gebruikers Hallo is u regelmatig een tooauthenticate verwacht.

| Gebruikers | RAM |
| ----- | --- |
| 1-10.000 | 4 GB |
| 10.001-50.000 | 8 GB |
| 50.001-100.000 | 12 GB |
| 100.000-200.001 | 16 GB |
| 200.001+ | 32 GB |

U tooset meerdere servers nodig voor hoge beschikbaarheid of taakverdeling? Er zijn een aantal manieren tooset van deze configuratie met Azure MFA-Server. Wanneer u uw eerste Azure MFA-Server installeert, wordt het Hallo-master. Extra servers worden onderliggende en gebruikers- en configuratie automatisch synchroniseren met Hallo master. Vervolgens kunt u een primaire server configureren en Hallo rest fungeren als back-up, of u kunt een taakverdeling tussen alle Hallo servers instellen.

Wanneer een model Azure MFA-Server offline gaat, wordt Hallo ondergeschikte servers kunnen nog steeds verzoeken proces in twee stappen. Echter, u kunt geen toevoegen nieuwe gebruikers en bestaande gebruikers kunnen pas worden bijgewerkt hun instellingen Hallo master weer online is of een ondergeschikte promotie.

### <a name="prepare-your-environment"></a>Uw omgeving voorbereiden

Zorg ervoor dat Hallo-server die u voor Azure multi-factor Authentication gebruikt aan Hallo volgens de vereisten voldoet:

| Vereisten voor Azure Multi-Factor Authentication-server | Beschrijving |
|:--- |:--- |
| Hardware |<li>200 MB aan vasteschijfruimte</li><li>Voor x32 of x64 geschikte processor</li><li>1 GB of meer RAM-geheugen</li> |
| Software |<li>WindowsServer 2008 of hoger als Hallo host een serverbesturingssysteem is</li><li>Windows 7 of hoger als Hallo host een clientbesturingssysteem is</li><li>Microsoft .NET 4.0 Framework</li><li>IIS 7.0 of hoger als installeert Hallo gebruiker portal of web service SDK</li> |

### <a name="azure-mfa-server-components"></a>Onderdelen van Azure MFA-server

Er zijn drie webonderdelen die gezamenlijk de Azure MFA-server vormen:

* Web Service SDK - Hiermee schakelt u communicatie met andere onderdelen Hallo en op Hallo Azure MFA-toepassingsserver is geïnstalleerd
* Gebruikersportal - IIS-website die u kunt gebruikers tooenroll in Azure multi-factor Authentication (MFA) en hun accounts kunnen onderhouden.
* Mobiele Web-App Service - kunnen met behulp van een mobiele app, zoals Hallo Microsoft Authenticator-app voor verificatie in twee stappen.

Alle drie onderdelen kunnen worden geïnstalleerd op Hallo dezelfde server als Hallo-server verbonden met internet is. Als splitsen Hallo onderdelen, Hallo Web Service SDK is geïnstalleerd op Hallo Azure MFA-toepassingsserver en Hallo Gebruikersportal en de webservice voor mobiele App zijn geïnstalleerd op een internetgerichte server.

### <a name="azure-multi-factor-authentication-server-firewall-requirements"></a>Firewallvereisten voor Azure Multi-Factor Authentication-server

Elke MFA-server moet kunnen toocommunicate op poort 443 uitgaand toohello adressen te volgen:

* https://pfd.phonefactor.net
* https://pfd2.phonefactor.net
* https://css.phonefactor.net

Als firewalls voor uitgaand verkeer op poort 443 worden beperkt, opent u de volgende IP-adresbereiken Hallo:

| IP-subnet | Netmasker | IP-bereik |
|:---: |:---: |:---: |
| 134.170.116.0/25 |255.255.255.128 |134.170.116.1 – 134.170.116.126 |
| 134.170.165.0/25 |255.255.255.128 |134.170.165.1 – 134.170.165.126 |
| 70.37.154.128/25 |255.255.255.128 |70.37.154.129 – 70.37.154.254 |

Als u Hallo Gebeurtenisbevestiging functie niet gebruikt en uw gebruikers tooverify mobiele apps van apparaten in het bedrijfsnetwerk Hallo niet gebruikt, hoeft u alleen Hallo bereiken te volgen:

| IP-subnet | Netmasker | IP-bereik |
|:---: |:---: |:---: |
| 134.170.116.72/29 |255.255.255.248 |134.170.116.72 – 134.170.116.79 |
| 134.170.165.72/29 |255.255.255.248 |134.170.165.72 – 134.170.165.79 |
| 70.37.154.200/29 |255.255.255.248 |70.37.154.201 – 70.37.154.206 |

## <a name="download-hello-azure-multi-factor-authentication-server"></a>Hello Azure multi-factor Authentication-Server downloaden

1. Meld u aan toohello [Azure-portal](https://portal.azure.com) als beheerder.
2. Selecteer aan de linkerkant Hallo **Active Directory**
3. Klik op **Gebruikers en groepen**.
4. Klik op **Alle gebruikers**.
5. Klik op **Multi-Factor Authentication**.
6. Selecteer **Service-instellingen** onder **Multi-Factor Authentication**.

   ![Pagina met service-instellingen](./media/multi-factor-authentication-get-started-server/servicesettings.png)

6. Klik op Hallo services instellingenpagina onderaan Hallo welkomstscherm op **Ga toohello portal**. Er wordt een nieuwe pagina geopend.
7. Klik op **Downloads**.
8. Klik op Hallo **downloaden** koppelen en Hallo installatieprogramma opslaan.

   ![MFA-server downloaden](./media/multi-factor-authentication-get-started-server/download4.png)

9. Houd deze pagina open als tooit na actieve Hallo-installatieprogramma wordt verwezen.

## <a name="install-and-configure-hello-azure-multi-factor-authentication-server"></a>Installeer en configureer hello Azure multi-factor Authentication-Server

U kunt nu dat u hebt gedownload Hallo-server installeren en configureren. Zorg ervoor dat die u wilt installeren op Hallo-server voldoet aan de vereisten in Hallo sectie plannen.

1. Dubbelklik op Hallo uitvoerbare.
2. Scherm installatiemap selecteren hello, Controleer op Hallo map juist is en klik op **volgende**.
3. Zodra het Hallo-installatie is voltooid, klikt u op **voltooien**.  Hallo-configuratiewizard wordt gestart.
4. Controleer op Hallo configuration wizard welkomstscherm **overslaan met behulp van verificatie-configuratiewizard Hallo** en klik op **volgende**.  Hallo-wizard wordt gesloten en Hallo-server wordt gestart.

   ![Cloud](./media/multi-factor-authentication-get-started-server/skip2.png)

5. Terug op de pagina Hallo die we gedownload Hallo-server uit, klikt u op Hallo **Activeringsreferenties** knop. Kopieer deze informatie naar hello Azure MFA-Server in de vakken Hallo opgegeven en klikt u op **activeren**.

## <a name="send-users-an-email"></a>E-mail verzenden naar gebruikers

implementatie van tooease, MFA-Server toocommunicate met uw gebruikers toestaan. MFA-Server kan een e-tooinform verzenden ze dat ze zijn geregistreerd voor verificatie in twee stappen.

Hallo e-mail die u verzendt moet worden bepaald door de configuratie van uw gebruikers voor verificatie in twee stappen. Bijvoorbeeld, als u de telefoonnummers kunnen tooimport uit de directory van het bedrijf Hallo, Hallo e-mail moet bevatten Hallo standaard telefoonnummers zodat gebruikers welke tooexpect weten. Als u telefoonnummers niet importeert, of uw gebruikers gaan toouse Hallo mobiele app, verzendt een e-mail waarin wordt verwezen ze toocomplete hun Accountregistratie. Omvatten een hyperlink toohello Azure multi-factor Authentication-Gebruikersportal in Hallo e-mailbericht.

Hallo-inhoud van e-mail Hallo is ook afhankelijk van Hallo verificatiemethode van die is ingesteld voor de gebruiker hello (telefoonoproep, SMS of mobiele app).  Bijvoorbeeld, als de gebruiker Hallo vereist toouse een PINCODE bij de verificatie, Hallo e wordt uitgelegd welke PINCODE initieel is ingesteld op.  Gebruikers zijn vereiste toochange hun PINCODE tijdens de eerste verificatie.

### <a name="configure-email-and-email-templates"></a>E-mailberichten en e-mailsjablonen configureren

Klik op Hallo e-mailpictogram links tooset Hallo Hallo-instellingen opgeven voor het verzenden van deze e-mailberichten. Deze pagina is waarin u Hallo SMTP-informatie van uw e-mail-server en verzend e-mailadres kunt invoeren door te controleren Hallo **verzenden e-mails toousers** selectievakje.

![E-mailconfiguratie van MFA-server](./media/multi-factor-authentication-get-started-server/email1.png)

Op tabblad Hallo inhoud van E-mail ziet u Hallo e-mailsjablonen die zijn beschikbaar toochoose uit. Afhankelijk van hoe u de verificatie van gebruikers tooperform in twee stappen hebt geconfigureerd, kiest u Hallo-sjabloon die het beste past bij.

![E-mailsjablonen voor MFA-server](./media/multi-factor-authentication-get-started-server/email2.png)

## <a name="import-users-from-active-directory"></a>Gebruikers uit Active Directory importeren

Nu die Hallo-server is geïnstalleerd. wilt u tooadd gebruikers. U kunt toocreate ze handmatig gebruikers importeren uit Active Directory of automatische synchronisatie met Active Directory configureren.

### <a name="manual-import-from-active-directory"></a>Handmatig importeren uit Active Directory

1. Selecteer in hello Azure MFA-Server op Hallo links **gebruikers**.
2. Selecteer onderaan Hallo **importeren uit Active Directory**.
3. Nu kunt u ofwel zoeken naar afzonderlijke gebruikers of zoeken Hallo AD-directory voor organisatie-eenheden met gebruikers.  In dit geval opgeven we Hallo gebruikers organisatie-eenheid.
4. Markeer alle Hallo gebruikers op Hallo rechts en klik op **importeren**.  Normaal verschijnt dan een pop-upvenster met de melding dat het importeren is gelukt.  Venster sluiten Hallo-importeren.

   ![Gebruikers importeren op MFA-server](./media/multi-factor-authentication-get-started-server/import2.png)

### <a name="automated-synchronization-with-active-directory"></a>Automatische synchronisatie met Active Directory

1. Selecteer in hello Azure MFA-Server op Hallo links **Adreslijstintegratie**.
2. Navigeer toohello **synchronisatie** tabblad.
3. Kies onderin Hallo **toevoegen**
4. In Hallo **synchronisatie-Item toevoegen** dat verschijnt kiezen Hallo domein, organisatie-eenheid **of** beveiligingsgroep, instellingen, standaardinstellingen voor methode en taal standaardinstellingen voor de synchronisatie van de taak en klik op **Toevoegen**.
5. Selectievakje Hallo **synchronisatie met Active Directory inschakelen** en kies een **synchronisatie-interval** tussen een minuut en 24 uur.

## <a name="how-hello-azure-multi-factor-authentication-server-handles-user-data"></a>Hoe hello Azure multi-factor Authentication-Server omgaat met gebruikersgegevens

Wanneer u Hallo multi-factor Authentication (MFA) Server on-premises, gebruikt, worden de gegevens van een gebruiker wordt opgeslagen in Hallo lokale servers. Er wordt geen permanente gebruikersgegevens opgeslagen in Hallo cloud. Wanneer de gebruiker Hallo een verificatie in twee stappen uitvoert, verzendt Hallo MFA-Server gegevens toohello Azure MFA cloud service tooperform Hallo verificatie. Wanneer deze verificatieaanvragen toohello cloudservice verzonden worden, worden hello volgende velden verzonden in Hallo-aanvraag en logbestanden zodat ze beschikbaar in de verificatie-/ gebruiksrapporten van de klant Hallo zijn. Aantal Hallo velden zijn optioneel, zodat ze kunnen worden ingeschakeld of uitgeschakeld in Hallo multi-factor Authentication-Server. Hallo-communicatie van Hallo MFA-Server toohello MFA-cloudservice maakt gebruik van SSL/TLS via poort 443 uitgaand. Deze velden zijn:

* Unieke id - gebruikersnaam of interne MFA-server-id
* Voor- en achternaam (optioneel)
* E-mailadres (optioneel)
* Telefoonnummer - bij het voeren van een telefoongesprek of bij sms-verificatie
* Apparaattoken - bij verificatie met behulp van de mobiele app
* Verificatiemodus
* Verificatieresultaat
* Naam van MFA-server
* IP van MFA-server
* Client-IP – indien beschikbaar

Bovendien toohello bovenstaande velden, Hallo verificatie resultaat (geslaagd/geweigerd) en de reden voor eventuele weigeringen is ook opgeslagen met Hallo verificatiegegevens en beschikbaar via de verificatie-/ gebruiksrapporten Hallo.

## <a name="back-up-and-restore-azure-mfa-server"></a>Back-ups maken van Azure MFA-server en deze terugzetten

Om ervoor te zorgen dat er een goede back-up is een belangrijke stap tootake met elk systeem.

tooback van Azure MFA-Server, zorg ervoor dat er een kopie van Hallo **C:\Program Files\Multi-Factor Authentication Server\Data** map inclusief Hallo **PhoneFactor.pfdata** bestand. 

In geval een terugzetten is vereist, volledige Hallo volgende stappen uit:

1. Installeer de Azure MFA-server op een nieuwe server.
2. Activeren Hallo van nieuwe Azure MFA-Server.
3. Stop Hallo **MultiFactorAuth** service.
4. Hallo overschrijven **PhoneFactor.pfdata** Hello een back-up kopiëren.
5. Hallo Start **MultiFactorAuth** service.

Hallo nieuwe server is nu actief en werkend met Hallo oorspronkelijke gegevens back-up-configuratie en de gebruiker.

## <a name="next-steps"></a>Volgende stappen

- Installeren en configureren van Hallo [Gebruikersportal](multi-factor-authentication-get-started-portal.md) voor selfservice van gebruiker.
- Installeren en configureren met Azure MFA-Server Hallo [Active Directory Federation Service](multi-factor-authentication-get-started-adfs.md), [RADIUS-verificatie](multi-factor-authentication-get-started-server-radius.md), of [LDAP-verificatie](multi-factor-authentication-get-started-server-ldap.md).
- [Externe bureaublad-gateway en Azure Multi-Factor Authentication-server met behulp van RADIUS](multi-factor-authentication-get-started-server-rdg.md) instellen en configureren.
- [Hello Azure multi-factor Authentication Server Mobile App Web Service implementeren](multi-factor-authentication-get-started-server-webservice.md).
- [Geavanceerde scenario's met Azure Multi-Factor Authentication en VPN's van derden](multi-factor-authentication-advanced-vpn-configurations.md).
