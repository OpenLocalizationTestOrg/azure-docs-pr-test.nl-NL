---
title: aaaAzure multi-factor Authentication-Veelgestelde vragen | Microsoft Docs
description: "Veelgestelde vragen en antwoorden gerelateerd tooAzure multi-factor Authentication. Multi-factor Authentication is een methode voor het verifiëren van de identiteit van een gebruiker die meer dan een gebruikersnaam en wachtwoord vereist. Dit biedt een extra laag van beveiliging toouser aanmelden en transacties."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 50bb8ac3-5559-4d8b-a96a-799a74978b14
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: kgremban
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c8305cf4c41bf8e9802df192fecdb7e463eff9eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-about-azure-multi-factor-authentication"></a>Veelgestelde vragen over Azure multi-factor Authentication
Deze Veelgestelde vragen over de antwoorden op veelgestelde vragen over Azure multi-factor Authentication en het gebruik van Hallo multi-factor Authentication-service. Het onderverdeeld in vragen over Hallo-service in het algemeen modellen, gebruikerservaringen, facturering en het oplossen van problemen.

## <a name="general"></a>Algemeen
**V: hoe wordt Azure multi-factor Authentication-Server gebruikersgegevens verwerkt?**

Gebruikersgegevens zijn opgeslagen met multi-factor Authentication-Server alleen op Hallo lokale servers. Er wordt geen permanente gebruikersgegevens opgeslagen in Hallo cloud. Wanneer de gebruiker Hallo verificatie in twee stappen uitvoert, verzendt multi-Factor Authentication-Server gegevens toohello Azure multi-factor Authentication-cloudservice gestuurd voor verificatie. Communicatie tussen de multi-factor Authentication-Server en Hallo multi-factor Authentication-cloudservice maakt gebruik van Secure Sockets Layer (SSL) of Transport Layer Security (TLS) via poort 443 uitgaand.

Wanneer verificatieaanvragen toohello cloudservice verzonden worden, gegevens worden verzameld voor de verificatie- en gebruiksgegevens rapporten. Gegevensvelden die zijn opgenomen in de verificatie-Logboeken in twee stappen zijn als volgt:

* **Unieke ID** (beide gebruikers naam of on-premises multi-Factor Authentication Server-ID)
* **Eerste en laatste naam** (optioneel)
* **E-mailadres** (optioneel)
* **Telefoonnummer** (als u een telefoongesprek of SMS-verificatie)
* **Apparaattoken** (als u verificatie voor mobiele Apps)
* **Verificatiemodus**
* **Verificatieresultaat**
* **Naam van de multi-factor Authentication-Server**
* **Multi-factor Authentication-Server IP**
* **Client IP** (indien beschikbaar)

Hallo optionele velden kunnen worden geconfigureerd in de multi-factor Authentication-Server.

Hallo verificatie resultaat (slagen of mislukken) en hello reden als deze is geweigerd, wordt opgeslagen met Hallo verificatiegegevens. Deze gegevens is beschikbaar in de verificatie- en gebruiksrapporten.

## <a name="billing"></a>Facturering
De meeste vragen over facturering kunnen worden beantwoord door te verwijzen tooeither hello [pagina met prijzen van multi-factor Authentication](https://azure.microsoft.com/pricing/details/multi-factor-authentication/) of Hallo documentatie over [hoe tooget Azure multi-factor Authentication](multi-factor-authentication-versions-plans.md).

**V: is mijn organisatie kosten in rekening gebracht voor het verzenden van Hallo telefoongesprekken en SMS-berichten die worden gebruikt voor verificatie?**

Nee, u niet weet in rekening gebracht voor afzonderlijke telefoongesprekken geplaatst of SMS-berichten verzonden toousers via de Azure multi-factor Authentication. Als u een MFA-provider per authenticatie gebruikt, wordt u gefactureerd voor elke verificatie, maar niet voor Hallo-methode die wordt gebruikt.

Uw gebruikers mogelijk worden kosten in rekening gebracht voor Hallo telefoongesprekken of SMS-berichten ontvangen volgens tootheir persoonlijke telefoonservice.

**V: bevat Hallo per gebruiker factureringsmodel in rekening voor alle ingeschakelde gebruikers of alleen Hallo die verificatie in twee stappen uitgevoerd?**

Facturering is gebaseerd op Hallo aantal gebruikers die zijn geconfigureerd toouse multi-factor Authentication, ongeacht of ze verificatie in twee stappen die maand uitgevoerd.

**V: hoe werkt multi-factor Authentication facturering?**

Wanneer u een MFA-provider per gebruiker of per authenticatie maakt, wordt de Azure-abonnement van uw organisatie gefactureerd maandelijks op basis van gebruik. Deze factureringsmodel is vergelijkbaar toohow Azure stuklijsten voor informatie over het gebruik van virtuele machines en websites.

Wanneer u een abonnement voor Azure multi-factor Authentication koopt, betaalt uw organisatie alleen Hallo jaarlijkse licentiekosten voor elke gebruiker. MFA licenties en Office 365, Azure AD Premium of Enterprise Mobility + Security bundels wordt gefactureerd op deze manier. 

Meer informatie over de opties in [hoe tooget Azure multi-factor Authentication](multi-factor-authentication-versions-plans.md).

**V: is er een gratis versie van Azure multi-factor Authentication?**

In sommige gevallen Ja.

Multi-factor Authentication voor beheerders van Azure biedt een subset van functies kosteloos voor toegang tot Azure MFA tooMicrosoft online services, waaronder hello Azure en Office 365-beheerder portals. Deze aanbieding is alleen van toepassing tooglobal beheerders in Azure Active Directory-exemplaren waarvoor geen Hallo volledige versie van Azure MFA via een MFA-licentie, een bundel of een zelfstandige op basis van verbruik-provider. Als uw beheerders Hallo gratis versie gebruiken, en vervolgens het aanschaffen van een volledige versie van Azure MFA, zijn alle globale beheerders met verhoogde bevoegdheid toohello versie automatisch betaald.

Multi-factor Authentication voor Office 365-gebruikers biedt een subset van functies kosteloos voor toegang tot Azure MFA tooOffice 365 services, met inbegrip van Exchange Online en SharePoint Online. Deze aanbieding geldt toousers die beschikken over een Office 365-licentie is toegewezen, wanneer de overeenkomende instantie Hallo van Azure Active Directory heeft geen Hallo volledige versie van Azure MFA via een MFA-licentie, een bundel of een zelfstandige op basis van verbruik provider.

**V: kan mijn organisatie tussen per gebruiker en per authenticatie verbruik factureringsmodellen op elk gewenst moment schakelen?**

Als uw organisatie MFA als zelfstandige service met facturering op basis van verbruik koopt, kiest u een factureringsmodel selecteren bij het maken van een MFA-provider. U kunt Hallo facturering model niet wijzigen nadat een MFA-provider is gemaakt. U kunt echter Hallo MFA-provider verwijderen en maak vervolgens een met een ander facturering model.

Wanneer een MFA-provider is gemaakt, kan het gekoppelde tooan Azure Active Directory (ook wel ' Azure AD-tenant') zijn. Als hello huidige MFA-Provider gekoppelde tooan Azure AD-tenant, kunt u veilig Hallo MFA-provider verwijderen en een gekoppelde toohello dezelfde Azure AD-tenant maken. U kunt ook als u onvoldoende MFA, Azure AD Premium of Enterprise Mobility + Security (EMS) licenties toocover alle gebruikers die zijn ingeschakeld voor MFA aangeschaft, kunt u verwijderen Hallo MFA-provider helemaal.

Als uw MFA-provider *niet* gekoppelde tooan Azure AD-tenant, of u koppelen Hallo nieuwe MFA-provider tooa andere Azure AD-tenant, instellingen en configuratie-opties niet worden overgedragen. Bovendien moet bestaande Azure MFA-Servers toobe opnieuw geactiveerd met behulp van activering referenties gegenereerd via Hallo nieuwe MFA-Provider. Hallo MFA Servers toolink reactiveren ze toohello nieuwe MFA-Provider heeft geen invloed op telefoongesprek en tekstberichtverificatie, maar de mobiele app meldingen niet meer zal werken voor alle gebruikers totdat ze Hallo mobiele app activeren.

Meer informatie over MFA-providers in [aan de slag met een Azure multi-factor Authentication-Provider](multi-factor-authentication-get-started-auth-provider.md).

**V: kan mijn organisatie schakelen tussen op basis van verbruik facturering en abonnementen (een licentie-model) op elk gewenst moment?**

In sommige gevallen Ja.

Als uw directory een *per gebruiker* Azure multi-factor Authentication-provider, kunt u MFA licenties toevoegen. Gebruikers met licenties zijn niet worden geteld in Hallo per gebruiker op basis van verbruik facturering. Gebruikers zonder licentie kunnen nog steeds worden ingeschakeld voor MFA via Hallo MFA-provider. Als u koopt en wijs licenties voor alle gebruikers toouse multi-Factor Authentication geconfigureerd, kunt u hello Azure multi-factor Authentication-provider verwijderen. Als u meer gebruikers dan licenties in toekomstige Hallo hebt, kunt u altijd een andere per gebruiker MFA-provider maken.

Als uw directory een *per authenticatie* Azure multi-factor Authentication-provider, elke verificatie worden altijd gefactureerd als Hallo MFA-provider gekoppelde tooyour abonnement is. U kunt MFA licenties toousers toewijzen, maar u hebt nog steeds worden gefactureerd voor elke aanvraag van de verificatie in twee stappen of ze afkomstig zijn van iemand met een MFA-licentie toegewezen of niet.

**V: bevat mijn organisatie toouse hebben en synchroniseren van identiteiten toouse Azure multi-factor Authentication?**

Als uw organisatie gebruikmaakt van een factureringsmodel op basis van verbruik, wordt Azure Active Directory is optioneel, maar niet vereist. Als de MFA-provider niet gekoppelde tooan Azure AD-tenant, kunt u alleen de Azure multi-factor Authentication-Server of hello Azure multi-factor Authentication SDK on-premises implementeren.

Azure Active Directory is vereist voor Hallo licentiemodel omdat licenties toohello Azure AD-tenant worden toegevoegd wanneer u koopt en deze toousers in Hallo directory toewijzen.

## <a name="manage-and-support-user-accounts"></a>Beheer en de ondersteuning van gebruikersaccounts

**V: wat moet ik mijn toodo gebruikers als ze niet reageert op hun telefoon hebt ontvangen of geen hun telefoon met hen hebt?**

Alle gebruikers geconfigureerd ideale geval meer dan één verificatiemethode. Vertel tootry meldt u zich opnieuw, maar een andere verificatiemethode op de aanmeldingspagina Hallo selecteren.

U kunt uw gebruikers toohello aanwijzen [eindgebruiker probleemoplossingsgids](./end-user/multi-factor-authentication-end-user-troubleshoot.md).


**V: wat moet ik doen als een van mijn gebruikers niet in tootheir-account ophalen kan?**

U kunt Hallo gebruikersaccount opnieuw instellen door ze te maken toogo via het registratieproces Hallo opnieuw. Meer informatie over [beheren van instellingen voor gebruikers en apparaten met Azure multi-factor Authentication in de cloud Hallo](multi-factor-authentication-manage-users-and-devices.md).

**V: wat moet ik doen als een van mijn gebruikers verliest een telefoon die met behulp van app-wachtwoorden?**

tooprevent onbevoegde toegang, Hallo van alle gebruikers app-wachtwoorden te verwijderen. Nadat het Hallo-gebruiker heeft een vervangende-apparaat, kunnen ze Hallo wachtwoorden opnieuw maken. Meer informatie over [beheren van instellingen voor gebruikers en apparaten met Azure multi-factor Authentication in de cloud Hallo](multi-factor-authentication-manage-users-and-devices.md).

**V: Wat gebeurt er als een gebruiker zich niet aanmelden toonon-browser-apps?**

Als uw organisatie nog steeds oude clients, en u gebruikt [toegestaan gebruik van app-wachtwoorden Hallo](multi-factor-authentication-whats-next.md#app-passwords), en vervolgens uw gebruikers toothese oudere clients met hun gebruikersnaam en wachtwoord kunnen niet aanmelden. In plaats daarvan moeten te[app-wachtwoorden instellen](./end-user/multi-factor-authentication-end-user-app-passwords.md). Uw gebruikers moeten uitschakelen (verwijderen) hun gegevens aanmelden, start Hallo app opnieuw en meld u aan met hun gebruikersnaam en *app-wachtwoord* in plaats van hun normale wachtwoord.

Als uw organisatie geen oudere clients, moet u niet toestaan uw gebruikers toocreate app-wachtwoorden.

> [!NOTE]
> Moderne verificatie voor clients met Office 2013
>
> App-wachtwoorden zijn alleen nodig voor apps die moderne verificatie niet ondersteunen. Clients met Office 2013 moderne verificatieprotocollen ondersteunen, maar moeten toobe geconfigureerd. Nieuwere Office-clients ondersteunen automatisch moderne verificatieprotocollen. Zie voor meer informatie, Hallo [Office 2013 modern authentication public preview aankondiging](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/).

**V: Mijn gebruikers zeggen dat ze niet soms Hallo-SMS-bericht ontvangen of zij tootwo manier tekstberichten reageren maar Hallo verificatie een optreedt time-out.**

Levering van tekstberichten en ontvangst van antwoorden in SMS in twee richtingen niet worden gegarandeerd omdat er hebt factoren die van invloed kunnen zijn op Hallo betrouwbaarheid van Hallo-service. Deze factoren omvatten Hallo bestemming land, Hallo mobiele telefoon carrier en sterkte Hallo-signaal.

Als uw gebruikers vaak problemen hebt met betrouwbaar tekstberichten ontvangen, zien ze toouse Hallo mobiele app of telefoongesprek methode in plaats daarvan. Hallo mobiele app kan meldingen zowel via Wi-Fi-verbindingen voor mobiel en ontvangen. Bovendien kunt Hallo mobiele app verificatiecodes genereren, zelfs wanneer het Hallo-apparaat heeft geen signaal helemaal. Hallo Microsoft Authenticator-app is beschikbaar voor [Android](http://go.microsoft.com/fwlink/?Linkid=825072), [IOS](http://go.microsoft.com/fwlink/?Linkid=825073), en [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071).

Als u de SMS-berichten gebruiken moet, wordt u aangeraden SMS in één richting in plaats van SMS in twee richtingen indien mogelijk. SMS in één richting is betrouwbaarder en kunnen gebruikers zich niet steeds globale SMS-berichten van beantwoorden tooa SMS-bericht dat is verzonden vanaf een ander land.

**V: kan ik Hallo hoeveelheid tijd Mijn gebruikers tooenter Hallo verificatiecode van een SMS-bericht voordat een optreedt Hallo system time-out wijzigen?**

In sommige gevallen Ja. 

Voor SMS in één richting met Azure MFA-Server v7.0 of hoger, kunt u configureren Hallo-out instelling door een registersleutel. Nadat de MFA-cloudservice Hallo Hallo SMS-bericht verzendt, geretourneerd verificatiecode hello (of een eenmalige wachtwoordcode) toohello MFA-Server. Hallo MFA-Server slaat Hallo code in het geheugen voor 300 seconden standaard. Als Hallo gebruiker niet eerder Hallo Hallo-code invoeren 300 seconden zijn verstreken, wordt de verificatie geweigerd. Gebruik deze stappen toochange Hallo standaardtime-out instellen:

1. Ga tooHKLM\Software\Wow6432Node\Positive Networks\PhoneFactor.
2. Maak een DWORD-registersleutel aangeroepen **pfsvc_pendingSmsTimeoutSeconds** en Hallo tijd in seconden dat u wilt dat hello Azure MFA-Server toostore eenmalige wachtwoordcodes instellen.

>[!TIP] 
>Als u meerdere Servers voor MFA hebt, kent alleen Hallo een dat de oorspronkelijke verificatieaanvraag Hallo verwerkt Hallo bevestigingscode die toohello gebruiker is verzonden. Wanneer de gebruiker Hallo Hallo-code opgeeft, Hallo verificatie aanvraag toovalidate inzage toohello dezelfde server. Als het Hallo-codevalidatie wordt tooa andere server worden verzonden, wordt Hallo verificatie geweigerd. 

Voor SMS in twee richtingen met Azure MFA-Server, kunt u de time-outinstelling Hallo configureren in Hallo MFA-beheerportal. Als gebruikers niet toohello SMS binnen de gedefinieerde time-outperiode Hallo reageert, wordt de verificatie geweigerd. 

U kunt Hallo time-outinstelling niet configureren voor eenzijdige SMS met Azure MFA in Hallo cloud (inclusief Hallo uitbreiding van AD FS-adapter of Hallo Network Policy Server). Azure AD slaat Hallo verificatiecode voor 180 seconden. 

**V: kan ik Hardwaretokens gebruiken met Azure multi-factor Authentication-Server?**

Als u Azure multi-factor Authentication-Server gebruikt, kunt u Open verificatie (OATH) op basis van tijd, eenmalig wachtwoord (TOTP)-tokens van derde importeren en ze vervolgens gebruiken voor verificatie in twee stappen.

U kunt ActiveIdentity-tokens die TOTP OATH-tokens zijn als u Hallo geheime sleutel in een CSV-bestand te plaatsen en tooAzure multi-factor Authentication-Server importeren gebruiken. U kunt OATH-tokens met Active Directory Federation Services (ADFS), formulieren gebaseerde verificatie van Internet Information Server (IIS) en Remote Authentication Dial-In User Service (RADIUS) gebruiken, zolang het clientsysteem Hallo Hallo gebruikersinvoer kan accepteren.

U kunt van derden TOTP OATH-tokens importeren met de volgende indelingen Hallo:  

- Draagbare symmetrische sleutelcontainer (PSKC)  
- CSV als Hallo-bestand een serienummer, een geheime sleutel in Base-32-notatie hebben en een tijdsinterval bevat  

**V: kan ik Azure multi-factor Authentication-Server toosecure Terminal Services gebruiken?**

Ja, maar als u van Windows Server 2012 R2 gebruikmaakt of later u alleen Terminal Services beveiligen kunt met behulp van extern bureaublad-Gateway (RD-Gateway).

Wijzigingen in de beveiliging in Windows Server 2012 R2 gewijzigd hoe Azure multi-factor Authentication-Server verbinding maakt met toohello Local Security Authority (LSA) beveiligingspakket in Windows Server 2012 en eerdere versies. Voor versies van Terminal Services in Windows Server 2012 of ouder, kunt u [beveiligen van een toepassing met de Windows-verificatie](multi-factor-authentication-get-started-server-windows.md#to-secure-an-application-with-windows-authentication-use-the-following-procedure). Als u Windows Server 2012 R2 gebruikt, moet u extern bureaublad-Gateway.

**V: ik beller-ID in de MFA-Server hebt geconfigureerd, maar mijn gebruikers nog steeds multi-factor Authentication-oproepen ontvangen van een anonieme aanroeper.**

Wanneer multi-factor Authentication-oproepen worden geplaatst door Hallo telefoon openbaar netwerk, worden soms ze gerouteerd via een luchtvaartmaatschappij die biedt geen ondersteuning voor beller-ID. Als gevolg hiervan beller-ID kan niet worden gegarandeerd, hoewel Hallo multi-factor Authentication-systeem altijd verzonden.

**V: waarom mijn gebruikers worden na vragen aan gebruiker tooregister hun beveiligingsgegevens?**
Er zijn diverse redenen die gebruikers kunnen worden na vragen aan gebruiker tooregister hun beveiligingsinformatie:

- Hallo-gebruiker is ingeschakeld voor meervoudige verificatie door de beheerder in Azure AD, maar heeft geen beveiligingsinformatie nog geregistreerd voor hun rekening.
- Hallo-gebruiker is ingeschakeld voor de selfservice voor wachtwoordherstel in Azure AD. Hallo beveiligingsgegevens helpt ze hun wachtwoord in toekomstige Hallo opnieuw instellen als ze deze ooit vergeet.
- Hallo gebruiker toegang krijgen tot een toepassing die een voorwaardelijk beleid toorequire MFA is en nog niet eerder is geregistreerd voor MFA.
- Hallo gebruiker registreren van een apparaat met Azure AD (inclusief Azure AD Join), en uw organisatie MFA voor apparaatregistratie is vereist, maar Hallo gebruiker niet eerder is geregistreerd voor MFA.
- Hallo gebruiker genereert Windows Hello voor bedrijven in Windows 10 (waarvoor MFA is vereist) en nog niet eerder is geregistreerd voor MFA.
- Hallo organisatie heeft gemaakt en een registratieprocedure voor MFA-beleid dat toegepast toohello gebruiker is ingeschakeld.
- Hallo gebruiker eerder is geregistreerd voor MFA, maar een verificatiemethode die een beheerder heeft sindsdien uitgeschakeld hebt gekozen. Hallo-gebruiker moet daarom registratieprocedure voor MFA doorlopen opnieuw tooselect een nieuwe standaardmethode voor verificatie.


## <a name="errors"></a>Fouten
**V: wat moeten gebruikers doen als ze een foutbericht 'authenticatie-aanvraag is niet voor een geactiveerd account' zien wanneer u meldingen van de mobiele app?**

Vertel toofollow deze procedure tooremove hun account van de mobiele app hello, opnieuw toevoegen:

1. Ga te[uw Azure-portal profiel](https://account.activedirectory.windowsazure.com/profile/) en meld u aan met uw organisatieaccount.
2. Selecteer **aanvullende beveiligingsverificatie**.
3. Hallo bestaande account verwijderen uit de mobiele app Hallo.
4. Klik op **configureren**, en volg Hallo instructies tooreconfigure Hallo mobiele app.

**V: wat moeten gebruikers doen als ze een foutbericht 0x800434D4L ziet wanneer niet-browsertoepassing tooa aanmelden?**

Hallo 0x800434D4L fout treedt op wanneer u toosign in tooa niet-browsertoepassing probeert, geïnstalleerd op een lokale computer, dat niet werkt met accounts waarvoor verificatie in twee stappen.

Een tijdelijke oplossing voor deze fout is toohave afzonderlijke gebruikersaccounts voor admin-gerelateerde en niet-beheerders bewerkingen. U kunt later postvakken tussen uw beheerdersaccount en niet-beheerdersaccount koppelen zodat u tooOutlook aanmelden kunt met behulp van uw niet-beheerdersaccount. Voor meer informatie over deze oplossing informatie over hoe te[geven een Hallo beheerder mogelijkheid tooopen en bekijkt hello inhoud van postvak in van een gebruiker](http://help.outlook.com/141/gg709759.aspx?sl=1).

## <a name="next-steps"></a>Volgende stappen
Als uw vraag hier niet beantwoord, laat u dit in de opmerkingen Hallo HALLO hallo pagina onderaan in. Of Hier volgen enkele aanvullende opties voor het Help-informatie:

* Zoeken Hallo [Microsoft Support Knowledge Base](https://www.microsoft.com/en-us/Search/result.aspx?form=mssupport&q=phonefactor&form=mssupport) voor oplossingen toocommon technische problemen.
* Zoeken en bladeren technische vragen en antwoorden van Hallo-community of uw eigen vraag in Hallo [Azure Active Directory-forums](https://social.msdn.microsoft.com/Forums/azure/newthread?category=windowsazureplatform&forum=WindowsAzureAD&prof=required).
* Als u een oudere PhoneFactor-klant bent en u vragen hebt of hulp bij het opnieuw instellen van een wachtwoord, gebruikt u Hallo [wachtwoordherstel](mailto:phonefactorsupport@microsoft.com) tooopen een ondersteuningsaanvraag te koppelen.
* Neem contact op met een supportmedewerker via [ondersteuning van Azure multi-factor Authentication-Server (PhoneFactor)](https://support.microsoft.com/oas/default.aspx?prid=14947). Wanneer u contact met ons, is het handig als u zo veel mogelijk gegevens over uw probleem mogelijk kunt opnemen. Informatie die kunt u opgeven omvat Hallo pagina waar u hebt gezien Hallo fout, Hallo specifieke foutcode Hallo specifieke sessie-ID en Hallo-ID van Hallo-gebruiker die Hallo fout hebt gezien.
