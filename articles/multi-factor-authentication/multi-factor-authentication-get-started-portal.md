---
title: Gebruikersportal voor Azure MFA-server | Microsoft Docs
description: Dit is de Azure Multi-Factor Authentication-pagina waarop wordt beschreven hoe u met Azure MFA en de gebruikersportal aan de slag kunt gaan.
services: multi-factor-authentication
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.assetid: 06b419fa-3507-4980-96a4-d2e3960e1772
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2017
ms.author: joflore
ms.reviewer: alexwe
ms.custom: it-pro
ms.openlocfilehash: a4eb403d3d21b7dbe63c2645b488a7bddb6d39fd
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/11/2017
---
# <a name="user-portal-for-the-azure-multi-factor-authentication-server"></a>Gebruikersportal voor de Azure Multi-Factor Authentication-server

De gebruikersportal is een IIS-website waar gebruikers zich kunnen registreren bij Azure Multi-Factor Authentication (MFA) en hun account kunnen beheren. Een gebruiker kan bij de volgende aanmelding zijn telefoonnummer en pincode wijzigen of verificatie in twee stappen overslaan.

Gebruikers kunnen zich bij de gebruikersportal aanmelden met hun gebruikelijke gebruikersnaam en wachtwoord en zullen een telefoonoproep voor verificatie in twee stappen aannemen of beveiligingsvragen beantwoorden om hun verificatie te voltooien. Als gebruikersregistratie is toegestaan, configureren gebruikers hun telefoonnummer en pincode de eerste keer dat ze zich aanmelden bij de gebruikersportal.

Er kunnen beheerders voor de gebruikersportal worden ingesteld. Aan hen kan ook een machtiging worden verleend om nieuwe gebruikers toe te voegen en bestaande gebruikers bij te werken.

Afhankelijk van uw omgeving kan het raadzaam zijn om de gebruikersportal te implementeren op dezelfde server als de Azure Multi-Factor Authentication Server of op een andere internetgerichte server.

![MFA-gebruikersportal](./media/multi-factor-authentication-get-started-portal/portal.png)

> [!NOTE]
> De gebruikersportal is alleen beschikbaar met Multi-Factor Authentication Server. Als u Multi-Factor Authentication in de cloud gebruikt, verwijst u uw gebruikers naar [Uw account instellen voor verificatie in twee stappen](./end-user/multi-factor-authentication-end-user-first-time.md) of [Uw instellingen beheren voor verificatie in twee stappen](./end-user/multi-factor-authentication-end-user-manage-settings.md).

## <a name="install-the-web-service-sdk"></a>De webservice-SDK installeren

Als de SDK van de webservice Azure Multi-Factor Authentication nog **niet** is geïnstalleerd op de Azure MFA-server (Multi-Factor Authentication), geldt voor beide scenario's dat u de volgende stappen moet uitvoeren.

1. Open de console van de Multi-Factor Authentication-server.
2. Ga naar **Webservice-SDK** en selecteer **Webservice-SDK installeren**.
3. Voltooi de installatie met de standaardinstellingen, tenzij u een speciale reden hebt om een andere instelling te kiezen.
4. Bind een SSL-certificaat aan de site in IIS.

Als u vragen hebt over het configureren van een SSL-certificaat op een IIS-server, raadpleegt u het artikel [How to Set Up SSL on IIS 7](https://docs.microsoft.com/en-us/iis/manage/configuring-security/how-to-set-up-ssl-on-iis) (SSL configureren in IIS 7).

De webservice-SDK moet met een SSL-certificaat worden beveiligd. Voor dit doel kan een zelfondertekend certificaat worden gebruikt. Importeer het certificaat in het certificaatarchief Vertrouwde basiscertificeringsinstanties van het account Lokale computer op de webserver van de gebruikersportal, zodat daar het certificaat wordt vertrouwd wanneer de SSL-verbinding tot stand wordt gebracht.

![Configuratie van MFA-server - webservice-SDK installeren](./media/multi-factor-authentication-get-started-portal/sdk.png)

## <a name="deploy-the-user-portal-on-the-same-server-as-the-azure-multi-factor-authentication-server"></a>De gebruikersportal op dezelfde server implementeren als de Azure Multi-Factor Authentication-server

Als u de gebruikersportal wilt installeren op **dezelfde server** als de Azure Multi-Factor Authentication-server, moet aan de volgende vereisten worden voldaan:

* IIS, inclusief ASP.NET, en compatibiliteit met IIS 6-metabase (voor IIS 7 of hoger)
* Een account met beheerdersrechten voor de computer en het domein, indien van toepassing. Het account heeft machtigingen nodig om Active Directory-beveiligingsgroepen te maken.
* De gebruikersportal moet zijn beveiligd met een SSL-certificaat.
* De webservice-SDK van Azure Multi-Factor Authentication moet zijn beveiligd met een SSL-certificaat.

Voer de volgende stappen uit om de gebruikersportal te implementeren:

1. Open de console van de Azure Multi-Factor Authentication-server, klik in het menu aan de linkerkant op **Gebruikersportal** en klik daarna op **Gebruikersportal installeren**.
2. Voltooi de installatie met de standaardinstellingen, tenzij u een speciale reden hebt om een andere instelling te kiezen.
3. Een SSL-certificaat aan de site binden in IIS.

   > [!NOTE]
   > Dit SSL-certificaat is meestal een openbaar ondertekend SSL-certificaat.

4. Open op een computer een webbrowser en navigeer naar de URL waar de gebruikersportal is geïnstalleerd (bijvoorbeeld: https://mfa.contoso.com/MultiFactorAuth). Controleer of er geen certificaatwaarschuwingen of -fouten worden weergegeven.

![Installatie van gebruikersportal van MFA-server](./media/multi-factor-authentication-get-started-portal/install.png)

Als u vragen hebt over het configureren van een SSL-certificaat op een IIS-server, raadpleegt u het artikel [How to Set Up SSL on IIS 7](https://docs.microsoft.com/en-us/iis/manage/configuring-security/how-to-set-up-ssl-on-iis) (SSL configureren in IIS 7).

## <a name="deploy-the-user-portal-on-a-separate-server"></a>De gebruikersportal implementeren op een afzonderlijke server

Als de server waarop Azure Multi-Factor Authentication wordt uitgevoerd niet internetgericht is, moet u de gebruikersportal installeren op een **afzonderlijke, internetgerichte server**.

Als uw organisatie gebruikmaakt van de Microsoft Authenticator-app als een van de verificatiemethoden en de gebruikersportal op een eigen server wil implementeren, moet u aan de volgende vereisten voldoen:

* U moet versie 6.0 of een recentere versie van de Azure Multi-Factor Authentication-server gebruiken.
* De gebruikersportal moet zijn geïnstalleerd op een internetgerichte webserver waarop Microsoft Internet Information Services (IIS) 6.x of een recentere versie wordt uitgevoerd.
* Wanneer u IIS 6.x gebruikt, zorgt u ervoor dat ASP.NET v2.0.50727 is geïnstalleerd, is geregistreerd en is ingesteld op **Toegestaan**.
* Wanneer u IIS 7.x of hoger gebruikt, IIS, inclusief basisverificatie, ASP.NET en compatibiliteit met IIS 6-metagegevens.
* De gebruikersportal moet zijn beveiligd met een SSL-certificaat.
* De webservice-SDK van Azure Multi-Factor Authentication moet zijn beveiligd met een SSL-certificaat.
* Zorg dat de gebruikersportal via SSL verbinding kan maken met de webservice-SDK van Azure Multi-Factor Authentication.
* Zorg dat de gebruikersportal bij de webservice-SDK van Azure Multi-Factor Authentication kan verifiëren met behulp van de referenties van een serviceaccount in de beveiligingsgroep PhoneFactor Admins. Dit serviceaccount en deze groep moeten zijn opgenomen in Active Directory als de Azure Multi-Factor Authentication-server wordt uitgevoerd op een server die aan een domein is gekoppeld. Dit serviceaccount en deze groep bevinden zich lokaal op de Azure Multi-Factor Authentication-server als deze niet aan een domein is gekoppeld.

Voor de installatie van de gebruikersportal op een andere server dan de Azure Multi-Factor Authentication-server moeten de volgende stappen worden uitgevoerd:

1. Blader **op de MFA-server** naar het installatiepad (voorbeeld: C:\Program Files\Multi-Factor Authentication-Server) en kopieer het bestand **MultiFactorAuthenticationUserPortalSetup64** naar een locatie die toegankelijk is voor de internetgerichte server waarop u het wilt installeren.
2. Voer **op de internetgerichte webserver** het installatiebestand MultiFactorAuthenticationUserPortalSetup64 uit als beheerder, wijzig de site desgewenst en wijzig de naam van de virtuele map eventueel in een korte naam.
3. Bind een SSL-certificaat aan de site in IIS.

   > [!NOTE]
   > Dit SSL-certificaat is meestal een openbaar ondertekend SSL-certificaat.

4. Blader naar **C:\inetpub\wwwroot\MultiFactorAuth**
5. Bewerk het bestand Web.Config in Kladblok

    * Zoek de sleutel **'USE_WEB_SERVICE_SDK'** en wijzig de waarde **value='false'** in **value='true'**
    * Zoek de sleutel **'WEB_SERVICE_SDK_AUTHENTICATION_USERNAME'** en wijzig **value=''** in **value='DOMAIN\User'** waarbij DOMAIN\User een serviceaccount is dat deel uitmaakt van de groep 'PhoneFactor Admins'.
    * Zoek de sleutel **'WEB_SERVICE_SDK_AUTHENTICATION_PASSWORD'** en wijzig **value=''** in **value='Password"** waarbij Password het wachtwoord is voor het serviceaccount dat is ingevoerd op de vorige regel.
    * Zoek de waarde **https://www.contoso.com/MultiFactorAuthWebServiceSdk/PfWsSdk.asmx** en wijzig deze tijdelijke aanduiding voor een URL in de webservice-URL die we hebben geïnstalleerd in stap 2.
    * Sla het bestand Web.Config op en sluit Kladblok.

6. Open op een computer een webbrowser en navigeer naar de URL waar de gebruikersportal is geïnstalleerd (bijvoorbeeld: https://mfa.contoso.com/MultiFactorAuth). Controleer of er geen certificaatwaarschuwingen of -fouten worden weergegeven.

Als u vragen hebt over het configureren van een SSL-certificaat op een IIS-server, raadpleegt u het artikel [How to Set Up SSL on IIS 7](https://docs.microsoft.com/en-us/iis/manage/configuring-security/how-to-set-up-ssl-on-iis) (SSL configureren in IIS 7).

## <a name="configure-user-portal-settings-in-the-azure-multi-factor-authentication-server"></a>Instellingen voor de gebruikersportal configureren op de Azure Multi-Factor Authentication-server

Nu de gebruikersportal is geïnstalleerd, dient u de Azure Multi-Factor Authentication-server te configureren voor gebruik met de portal.

1. Klik in de console van de Azure Multi-Factor Authentication-server op het pictogram **Gebruikersportal**. Voer op het tabblad Instellingen in het tekstvak **URL gebruikersportal** de URL naar de gebruikersportal in. Als de e-mailfunctionaliteit is ingeschakeld, zal deze URL worden ingevoegd in e-mailberichten die worden verzonden naar gebruikers wanneer ze worden geïmporteerd op de Azure Multi-Factor Authentication-server.
2. Kies de instellingen die u in de gebruikersportal wilt gebruiken. Als u bijvoorbeeld wilt toestaan dat gebruikers hun verificatiemethoden kiezen, zorgt u ervoor dat de optie **Toestaan dat gebruikers de methode selecteren** wordt ingeschakeld, samen met de methoden waaruit ze kunnen kiezen.
3. Geef op het tabblad **Beheerders** aan wie de beheerders moeten zijn. U kunt gedetailleerde beheerdersmachtigingen maken met behulp van de selectievakjes en vervolgkeuzelijsten in de vakken voor toevoegen en bewerken.

Optionele configuratie:
- **Beveiligingsvragen** -Definieer goedgekeurde beveiligingsvragen voor uw omgeving en de taal waarin ze worden weergegeven.
- **Doorgegeven sessies** - Configureer de integratie van de gebruikersportal met een formuliergebaseerde website met MFA.
- **Vertrouwde IP-adressen** -U kunt toestaan dat gebruikers MFA overslaan wanneer ze worden geverifieerd aan de hand van een lijst met vertrouwde IP-adressen of bereiken.

![Configuratie van gebruikersportal van MFA-server](./media/multi-factor-authentication-get-started-portal/config.png)

De Azure Multi-Factor Authentication-server biedt verschillende opties voor de gebruikersportal. De volgende tabel geeft een lijst van deze opties en een verklaring van de taak waarvoor ze worden gebruikt.

| Instellingen van gebruikersportal | Beschrijving |
|:--- |:--- |
| URL gebruikersportal | Hiermee kunt u de URL invoeren van de locatie waar de portal wordt gehost. |
| Primaire authenticatie | Hiermee kunt u opgeven welk verificatietype moet worden gebruikt bij de aanmelding bij de portal. Windows-, Radius- of LDAP-authenticatie. |
| Aanmelden van gebruikers toestaan | Hiermee kunnen gebruikers een gebruikersnaam en wachtwoord invoeren op de aanmeldingspagina voor de gebruikersportal. Als deze optie niet is geselecteerd, worden de vakken grijs weergegeven. |
| Registreren van gebruikers toestaan | Hiermee kunnen gebruikers zich registreren voor Multi-Factor Authentication doordat ze naar een installatiescherm worden geleid waar om aanvullende informatie zoals een telefoonnummer wordt gevraagd. Bij Vragen om alternatief telefoonnummer kunnen gebruikers een tweede telefoonnummer opgeven. Bij Vragen om OATH-token van derden kunnen gebruikers een OATH-token van een derde opgeven. |
| Gebruikers toestaan om eenmalige toegang te initiëren | Hiermee kunt u gebruikers toestaan om eenmalige toegang te initiëren. Als een gebruiker deze optie instelt, wordt deze van kracht wanneer de gebruiker zich de volgende keer aanmeldt. De optie Vragen om bypass-seconden biedt gebruikers een invoervak, waarin zij de standaardwaarde van 300 seconden kunnen wijzigen. Anders duurt de eenmalige toegang slechts 300 seconden. |
| Toestaan dat gebruikers de methode selecteren | Hiermee kunnen gebruikers hun primaire contactmethode opgeven. De volgende methoden zijn beschikbaar: telefoonoproep, sms-bericht, mobiele app of OATH-token. |
| Toestaan dat gebruikers de taal selecteren | Hiermee kunnen gebruikers de taal wijzigen die wordt gebruikt voor de telefoonoproep, het sms-bericht, de mobiele app of het OATH-token. |
| Toestaan dat gebruikers de mobiele app activeren | Hiermee kunnen gebruikers een activeringscode genereren om het activeringsproces van de mobiele app te voltooien dat bij de server wordt gebruikt.  U kunt ook instellen op hoeveel apparaten zij dit kunnen activeren, met een aantal van 1 t/m 10. |
| Beveiligingsvragen gebruiken als terugvaloptie | Hiermee kunt u beveiligingsvragen toestaan als verificatie in twee stappen is mislukt. U kunt opgeven hoeveel beveiligingsvragen juist moeten worden beantwoord. |
| Toestaan dat gebruikers OATH-token van derden koppelen | Hiermee kunnen gebruikers een OATH-token van derden opgeven. |
| OATH-token gebruiken als terugvaloptie | Hiermee kunt u het gebruik van een OATH-token toestaan als verificatie in twee stappen is mislukt. U kunt ook de sessietime-out in minuten opgeven. |
| Logboekregistratie inschakelen | Hiermee schakelt u de logboekregistratie in op de gebruikersportal. De logboekbestanden bevinden zich op: C:\Program Files\Multi-Factor Authentication Server\Logs. |

Deze instellingen zijn zichtbaar voor de gebruiker in de portal zodra deze zijn ingeschakeld en de gebruiker zich bij de gebruikersportal heeft aangemeld.

![Instellingen gebruikersportal](./media/multi-factor-authentication-get-started-portal/portalsettings.png)

### <a name="self-service-user-enrollment"></a>Selfservice voor gebruikersregistratie

Als u wilt dat uw gebruikers zich kunnen aanmelden en registreren, selecteert u op het tabblad Instellingen de opties **Aanmelden van gebruikers toestaan** en **Registreren van gebruikers toestaan**. Houd er rekening mee dat de instellingen die u selecteert, invloed hebben op de gebruikerservaring bij het aanmelden.

Wanneer bijvoorbeeld een gebruiker zich voor het eerst bij de gebruikersportal aanmeldt, wordt de gebruiker naar de pagina met gebruikersinstellingen van Azure Multi-Factor Authentication geleid. Afhankelijk van hoe u Azure Multi-Factor Authentication hebt geconfigureerd, kan een gebruiker al dan niet de verificatiemethode selecteren.

Als de gebruiker de verificatiemethode Spraakoproep selecteert of als de gebruiker vooraf is geconfigureerd om die methode te gebruiken, wordt de gebruiker gevraagd zijn of haar primaire telefoonnummer en, indien van toepassing, zijn of haar toestelnummer op te geven. Mogelijk kan de gebruiker ook een alternatief telefoonnummer invoeren.

![Primaire en alternatieve telefoonnummers registreren](./media/multi-factor-authentication-get-started-portal/backupphone.png)

Als de gebruiker bij de verificatie een pincode moet gebruiken, wordt de gebruiker gevraagd een pincode te maken. Nadat de gebruiker zijn of haar telefoonnummer(s) en pincode (indien van toepassing) heeft ingevoerd, klikt de gebruiker op de knop **Bel me nu om te authenticeren**. Azure Multi-Factor Authentication zal een verificatie door middel van een spraakoproep uitvoeren met behulp van het primaire telefoonnummer van de gebruiker. De gebruiker moet de spraakoproep beantwoorden en zijn of haar pincode invoeren (indien van toepassing) en daarna op # drukken om door te gaan naar de volgende stap van het zelfregistratieproces.

Als de gebruiker de verificatiemethode Sms-bericht selecteert of vooraf is geconfigureerd om die methode te gebruiken, wordt de gebruiker gevraagd zijn of haar mobiele telefoonnummer op te geven. Als de gebruiker bij de verificatie een pincode moet gebruiken, wordt de gebruiker ook gevraagd een pincode op te geven.  Nadat de gebruiker zijn of haar telefoonnummer en pincode (indien van toepassing) heeft ingevoerd, klikt de gebruiker op de knop **Sms me nu om te authenticeren**. Azure Multi-Factor Authentication zal een sms-verificatie uitvoeren met behulp van de mobiele telefoon van de gebruiker. De gebruiker ontvangt een sms-bericht met een eenmalige-wachtwoordcode (OTP). Vervolgens beantwoordt de gebruiker het bericht met die OTP plus de pincode (indien van toepassing).

![Sms gebruikersportal](./media/multi-factor-authentication-get-started-portal/text.png)

Als de gebruiker de verificatiemethode Mobiele app selecteert, wordt de gebruiker op de pagina gevraagd om de Microsoft Authenticator-app op zijn of haar apparaat te installeren en een activeringscode te genereren. Na de installatie van de app klikt de gebruiker op de knop Activeringscode genereren.

> [!NOTE]
> De gebruiker dient pushmeldingen voor het apparaat in te schakelen om de Microsoft Authenticator-app te gebruiken.

Op de pagina worden vervolgens een activeringscode en een URL weergegeven, samen met een afbeelding van een streepjescode. Als de gebruiker bij de verificatie een pincode moet gebruiken, wordt de gebruiker ook gevraagd een pincode op te geven. De gebruiker voert de activeringscode en URL in de Microsoft Authenticator-app in of gebruikt de streepjescodescanner om de afbeelding van de streepjescode te scannen en klikt op de knop Activeren.

Nadat de activering is voltooid, klikt de gebruiker op de knop **Nu verifiëren**. Azure Multi-Factor Authentication zal een verificatie uitvoeren met behulp van de mobiele app van de gebruiker. De gebruiker moet in de mobiele app de pincode invoeren (indien van toepassing) en op de knop Verifiëren drukken om door te gaan naar de volgende stap van het zelfregistratieproces.

Als de beheerders de Azure Multi-Factor Authentication-server hebben geconfigureerd om beveiligingsvragen en antwoorden te verzamelen, wordt de gebruiker hierna naar de pagina Beveiligingsvragen geleid. De gebruiker moet vier beveiligingsvragen selecteren en deze juist beantwoorden.

![Beveiligingsvragen van gebruikersportal](./media/multi-factor-authentication-get-started-portal/secq.png)

De zelfregistratie van de gebruiker is nu voltooid en de gebruiker is aangemeld bij de gebruikersportal. Gebruikers kunnen zich later op elk gewenst moment opnieuw aanmelden bij de gebruikersportal om hun telefoonnummers, pincodes, verificatiemethoden en beveiligingsvragen te wijzigen als dat door de beheerders is toegestaan.

## <a name="next-steps"></a>Volgende stappen

- [Authenticatie met de mobiele app integreren met Azure Multi-Factor Authentication-server](multi-factor-authentication-get-started-server-webservice.md)