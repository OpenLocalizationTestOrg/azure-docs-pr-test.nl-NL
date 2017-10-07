---
title: aaaUser-portal voor Azure MFA-Server | Microsoft Docs
description: Dit is hello Azure multi-factor authentication-pagina waarop wordt beschreven hoe tooget de slag met Azure MFA en Hallo gebruikersportal.
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
ms.openlocfilehash: 0e36644c3d780249fb98d5da654e9d267c63561a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="user-portal-for-hello-azure-multi-factor-authentication-server"></a>Gebruikersportal voor hello Azure multi-factor Authentication-Server

Hallo-gebruikersportal is een IIS-website die u kunt gebruikers tooenroll in Azure multi-factor Authentication (MFA) en hun accounts kunnen onderhouden. Een gebruiker kan hun telefoonnummer wijzigen, hun PINCODE wijzigen of kies toobypass verificatie in twee stappen tijdens de volgende aanmelding.

Gebruikers toohello gebruikersportal met hun normale gebruikersnaam en wachtwoord aanmelden, vervolgens een aanroep van de verificatie in twee stappen voltooien of beveiliging vragen toocomplete hun verificatie te beantwoorden. Als gebruikersregistratie is toegestaan, configureren gebruikers hun telefoonnummer en PINCODE Hallo eerste keer dat ze zich in de gebruikersportal toohello.

Beheerders van gebruikersportal kan worden ingesteld en verleend machtiging tooadd nieuwe gebruikers en bestaande gebruikers bijwerken.

Afhankelijk van uw omgeving, kunt u het Hallo-gebruikersportal toodeploy op Hallo dezelfde server als de Azure multi-factor Authentication-Server of op een andere internetgerichte server.

![MFA-gebruikersportal](./media/multi-factor-authentication-get-started-portal/portal.png)

> [!NOTE]
> Hallo-gebruikersportal is alleen beschikbaar met multi-factor Authentication-Server. Als u multi-factor Authentication in Hallo cloud gebruikt, raadpleegt u uw gebruikers toohello [Set-up uw account voor verificatie in twee stappen](./end-user/multi-factor-authentication-end-user-first-time.md) of [beheren van uw instellingen voor verificatie in twee stappen](./end-user/multi-factor-authentication-end-user-manage-settings.md).

## <a name="install-hello-web-service-sdk"></a>Hallo webservice SDK installeren

In beide scenario's moet hello Azure multi-factor Authentication Web Service SDK is **niet** op Hallo Azure multi-factor Authentication (MFA)-Server zijn geïnstalleerd, volledige Hallo onderstaande stappen.

1. Open de console van Hallo multi-factor Authentication-Server.
2. Ga toohello **Web Service SDK** en selecteer **Web Service SDK installeren**.
3. Volledige Hallo installeren met behulp van Hallo standaardwaarden tenzij u toochange hoeft ze om een bepaalde reden.
4. Binden van een SSL-certificaat toohello-website in IIS.

Als u vragen over het configureren van een SSL-certificaat op een IIS-server hebt, raadpleegt u Hallo artikel [hoe tooSet SSL op IIS](https://docs.microsoft.com/en-us/iis/manage/configuring-security/how-to-set-up-ssl-on-iis).

Hallo Web Service SDK moet worden beveiligd met een SSL-certificaat. Voor dit doel kan een zelfondertekend certificaat worden gebruikt. Hallo-certificaat importeren in Hallo 'Trusted Root Certification Authorities' archief van de lokale computeraccount Hallo op Hallo User Portal-webserver, zodat wordt dat certificaat vertrouwd wanneer Hallo SSL-verbinding tot stand brengen.

![Configuratie van MFA-server - webservice-SDK installeren](./media/multi-factor-authentication-get-started-portal/sdk.png)

## <a name="deploy-hello-user-portal-on-hello-same-server-as-hello-azure-multi-factor-authentication-server"></a>De gebruikersportal Hallo op Hallo implementeren dezelfde server als hello Azure multi-factor Authentication-Server

Hallo volgende vereisten worden vereist tooinstall hello gebruikersportal op Hallo **dezelfde server** zoals hello Azure multi-factor Authentication-Server:

* IIS, inclusief ASP.NET, en compatibiliteit met IIS 6-metabase (voor IIS 7 of hoger)
* Een account met beheerdersrechten voor Hallo-computer en domein indien van toepassing. Hallo-account moet machtigingen toocreate Active Directory-beveiligingsgroepen.
* Beveilig de gebruikersportal Hallo met een SSL-certificaat.
* Hello Azure multi-factor Authentication Web Service SDK is beveiligd met een SSL-certificaat.

toodeploy Hallo gebruiker portal, volg deze stappen:

1. Open de console van hello Azure multi-factor Authentication-Server, klikt u op Hallo **Gebruikersportal** pictogram in Hallo links menu, klikt u op **Gebruikersportal installeren**.
2. Volledige Hallo installeren met behulp van Hallo standaardwaarden tenzij u toochange hoeft ze om een bepaalde reden.
3. Binden van een SSL-certificaat toohello-website in IIS

   > [!NOTE]
   > Dit SSL-certificaat is meestal een openbaar ondertekend SSL-certificaat.

4. Open een webbrowser op een computer en navigeer toohello-URL waar de gebruikersportal Hallo is geïnstalleerd (voorbeeld: https://mfa.contoso.com/MultiFactorAuth). Controleer of er geen certificaatwaarschuwingen of -fouten worden weergegeven.

![Installatie van gebruikersportal van MFA-server](./media/multi-factor-authentication-get-started-portal/install.png)

Als u vragen over het configureren van een SSL-certificaat op een IIS-server hebt, raadpleegt u Hallo artikel [hoe tooSet SSL op IIS](https://docs.microsoft.com/en-us/iis/manage/configuring-security/how-to-set-up-ssl-on-iis).

## <a name="deploy-hello-user-portal-on-a-separate-server"></a>Hallo-gebruikersportal op een afzonderlijke server implementeren

Als het Hallo-server waarop de Azure multi-factor Authentication-Server wordt uitgevoerd, is niet verbonden met internet, moet u Hallo gebruikersportal installeren op een **afzonderlijk, internetgerichte server**.

Als uw organisatie gebruikt Microsoft Authenticator-app als een van de verificatiemethoden Hallo Hallo en toodeploy hello gebruikersportal op een eigen server wilt, voltooit u Hallo volgens de vereisten:

* Gebruik 6.0 of hoger van hello Azure multi-factor Authentication-Server.
* Hallo-gebruikersportal installeren op een internetgerichte webserver met Microsoft internet Information Services (IIS) 6.x of hoger.
* Wanneer u IIS 6.x, zorg ervoor dat ASP.NET v2.0.50727 is geïnstalleerd, is geregistreerd en ingesteld te**toegestane**.
* Wanneer u IIS 7.x of hoger gebruikt, IIS, inclusief basisverificatie, ASP.NET en compatibiliteit met IIS 6-metagegevens.
* Beveilig de gebruikersportal Hallo met een SSL-certificaat.
* Hello Azure multi-factor Authentication Web Service SDK is beveiligd met een SSL-certificaat.
* Zorg ervoor dat gebruikersportal Hallo verbinding kan maken van Azure multi-factor Authentication Web Service SDK toohello via SSL.
* Zorg ervoor dat gebruikersportal hello toohello Azure multi-factor Authentication Web Service SDK kan worden geverifieerd met behulp van Hallo-referenties van een serviceaccount in Hallo "PhoneFactor Admins" beveiligingsgroep. Dit serviceaccount en deze groep moeten bestaan in Active Directory als hello Azure multi-factor Authentication-Server wordt uitgevoerd op een domein-server. Dit serviceaccount en deze groep bevinden zich lokaal op Hallo Azure multi-factor Authentication-Server als geen gekoppelde tooa-domein is.

Hallo-gebruikersportal installeren op een andere server dan hello Azure multi-factor Authentication-Server vereist Hallo stappen te volgen:

1. **Op Hallo MFA-Server**, bladeren installatiepad toohello (voorbeeld: C:\Program Files\Multi-Factor Authentication-Server), en het Hallo-bestand kopiëren **MultiFactorAuthenticationUserPortalSetup64** tooa locatie toegankelijk toohello internetgerichte server waarop u het wilt installeren.
2. **Op Hallo internetgerichte webserver**, Hallo MultiFactorAuthenticationUserPortalSetup64-installatiebestand uitvoeren als beheerder, Hallo Site desgewenst wijzigen en Hallo virtuele directory tooa korte naam wijzigen als u wilt.
3. Binden van een SSL-certificaat toohello-website in IIS.

   > [!NOTE]
   > Dit SSL-certificaat is meestal een openbaar ondertekend SSL-certificaat.

4. Te bladeren**C:\inetpub\wwwroot\MultiFactorAuth**
5. Hallo Web.Config-bestand in Kladblok bewerken

    * Hallo sleutel vinden **'USE_WEB_SERVICE_SDK'** en wijzig **waarde = "false"** te**waarde = "true"**
    * Hallo sleutel vinden **'Sleutels WEB_SERVICE_SDK_AUTHENTICATION_USERNAME'** en wijzig **waarde = ""** te**waarde = 'Domein\gebruiker'** waar domein\gebruiker is een Service-Account dat deel uitmaakt van 'PhoneFactor Admins'-groep.
    * Hallo sleutel vinden **'WEB_SERVICE_SDK_AUTHENTICATION_PASSWORD'** en wijzig **waarde = ""** te**waarde = 'Password'** waar het wachtwoord is Hallo-wachtwoord voor Hallo Service Het account is ingevoerd in de vorige regel Hallo.
    * Hallo waarde zoeken **https://www.contoso.com/MultiFactorAuthWebServiceSdk/PfWsSdk.asmx** en wijzigt u deze tijdelijke aanduiding voor URL toohello Web Service SDK-URL die we in stap 2 hebt geïnstalleerd.
    * Sla Hallo Web.Config-bestand op en sluit Kladblok.

6. Open een webbrowser op een computer en navigeer toohello-URL waar de gebruikersportal Hallo is geïnstalleerd (voorbeeld: https://mfa.contoso.com/MultiFactorAuth). Controleer of er geen certificaatwaarschuwingen of -fouten worden weergegeven.

Als u vragen over het configureren van een SSL-certificaat op een IIS-server hebt, raadpleegt u Hallo artikel [hoe tooSet SSL op IIS](https://docs.microsoft.com/en-us/iis/manage/configuring-security/how-to-set-up-ssl-on-iis).

## <a name="configure-user-portal-settings-in-hello-azure-multi-factor-authentication-server"></a>Instellingen voor gebruikersportal in hello Azure multi-factor Authentication-Server configureren

Nu dat Hallo gebruikersportal is geïnstalleerd, moet u tooconfigure hello Azure multi-factor Authentication-Server toowork met Hallo-portal.

1. Klik in-console hello Azure multi-factor Authentication-Server op Hallo **Gebruikersportal** pictogram. Voer op tabblad Instellingen Hallo Hallo URL toohello gebruikersportal in Hallo **Gebruikersportal-URL** textbox. Als e-mailfunctionaliteit is ingeschakeld, wordt deze URL is opgenomen in Hallo e-mails die toousers worden verzonden wanneer ze worden geïmporteerd in hello Azure multi-factor Authentication-Server.
2. Hallo instellingen kiezen dat u wilt dat toouse in Hallo Gebruikersportal. Bijvoorbeeld gebruikers zijn niet toegestaan als toochoose hun verificatiemethoden ervoor zorgen dat **toestaan dat gebruikers de methode tooselect** is ingeschakeld, samen met de Hallo methoden waaruit ze kunnen kiezen.
3. Definiëren die beheerders moeten zich op Hallo **beheerders** tabblad. U kunt gedetailleerde beheerdersmachtigingen met Hallo selectievakjes en vervolgkeuzelijsten in Hallo toevoegen/bewerken vakken maken.

Optionele configuratie:
- **Beveiligingsvragen** -definiëren beveiligingsvragen voor uw omgeving en Hallo taal ze worden weergegeven in goedgekeurd.
- **Doorgegeven sessies** - Configureer de integratie van de gebruikersportal met een formuliergebaseerde website met MFA.
- **Goedgekeurde IP-adressen** -toestaan dat gebruikers tooskip MFA bij het verifiëren van een lijst met goedgekeurde IP-adressen of adresbereiken.

![Configuratie van gebruikersportal van MFA-server](./media/multi-factor-authentication-get-started-portal/config.png)

Azure multi-factor Authentication-server biedt verschillende opties voor de gebruikersportal Hallo. Hallo bevat volgende tabel een lijst van deze opties en een beschrijving van wat ze worden gebruikt.

| Instellingen van gebruikersportal | Beschrijving |
|:--- |:--- |
| URL gebruikersportal | Voer Hallo-URL van de waar Hallo portal wordt gehost. |
| Primaire authenticatie | Hallo type verificatie toouse opgeven als u zich aanmeldt toohello-portal. Windows-, Radius- of LDAP-authenticatie. |
| Toestaan dat gebruikers toolog in | Toestaan dat gebruikers tooenter een gebruikersnaam en wachtwoord op Hallo aanmeldingspagina voor de gebruikersportal Hallo. Als deze optie niet is geselecteerd, worden Hallo vakken grijs weergegeven. |
| Registreren van gebruikers toestaan | Een gebruiker tooenroll in multi-factor Authentication doordat ze tooa setup-scherm waarin wordt ze gevraagd om aanvullende informatie zoals een telefoonnummer toestaan. Vragen om alternatief telefoonnummer gebruikers toospecify een tweede telefoonnummer kunnen. Vragen om de derde partij OATH-token kunt toospecify gebruikers een OATH-token van derden. |
| Toestaan dat gebruikers tooinitiate eenmalig overslaan | Toestaan dat gebruikers tooinitiate eenmalig overslaan. Als een gebruiker deze optie stelt, duurt het effect Hallo zodra Hallo gebruiker zich aanmeldt. Vragen om bypass seconden biedt Hallo-gebruiker met een selectievakje dat zij Hallo standaardwaarde van 300 seconden kunnen wijzigen. Anders geldt Hallo eenmalig overslaan slechts 300 seconden. |
| Gebruikers toestaan tooselect methode | Toestaan dat gebruikers toospecify zijn primaire contactmethode. De volgende methoden zijn beschikbaar: telefoonoproep, sms-bericht, mobiele app of OATH-token. |
| Toestaan dat gebruikers de taal tooselect | Toestaan dat gebruikers toochange Hallo taal die wordt gebruikt voor het Hallo-telefoongesprek, tekstbericht, mobiele app of OATH-token. |
| Toestaan dat gebruikers tooactivate mobiele app | Toestaan dat gebruikers toogenerate een code toocomplete Hallo mobiele app activeren activeringsproces dat wordt gebruikt met Hallo-server.  U kunt ook het aantal apparaten kunnen worden geactiveerd Hallo instellen Hallo app op tussen 1 en 10. |
| Beveiligingsvragen gebruiken als terugvaloptie | Hiermee kunt u beveiligingsvragen toestaan als verificatie in twee stappen is mislukt. U kunt het aantal beveiligingsvragen juist moeten worden beantwoord Hallo opgeven. |
| OATH-token van gebruikers tooassociate van derden toestaan | Toestaan dat gebruikers toospecify OATH-token van een derde partij. |
| OATH-token gebruiken als terugvaloptie | Bieden voor Hallo gebruik van een OATH-token als verificatie in twee stappen niet geslaagd is. U kunt ook Hallo sessietime-out in minuten opgeven. |
| Logboekregistratie inschakelen | Logboekregistratie inschakelen op Hallo gebruikersportal. Hallo logboekbestanden bevinden zich op: C:\Program Files\Multi-Factor Authentication Server\Logs. |

Deze instellingen worden zichtbaar toohello gebruiker in de portal Hallo zodra ze zijn ingeschakeld en deze in de gebruikersportal toohello zijn ondertekend.

![Instellingen gebruikersportal](./media/multi-factor-authentication-get-started-portal/portalsettings.png)

### <a name="self-service-user-enrollment"></a>Selfservice voor gebruikersregistratie

Als u wilt dat uw gebruikers toosign in en inschrijven, moet u Hallo **toestaan dat gebruikers toolog in** en **gebruikersregistratie toestaan** opties onder het tabblad Hallo-instellingen. Houd er rekening mee dat Hallo-instellingen die u selecteert, invloed zijn op Hallo aanmelden gebruikerservaring.

Wanneer een gebruiker zich in de gebruikersportal toohello voor Hallo eerst, worden ze bijvoorbeeld vervolgens toohello gebruikersinstellingen van Azure multi-factor Authentication-pagina genomen. Afhankelijk van hoe u Azure multi-factor Authentication hebt geconfigureerd, Hallo-gebruiker kan worden kunnen tooselect de verificatiemethode.

Als ze Hallo Spraakoproep verificatiemethode selecteren of vooraf geconfigureerde toouse die methode is, vraagt Hallo pagina Hallo gebruiker tooenter hun primaire telefoonnummer en de extensie, indien van toepassing. Ze kunnen ook worden toegestaan tooenter een alternatief telefoonnummer.

![Primaire en alternatieve telefoonnummers registreren](./media/multi-factor-authentication-get-started-portal/backupphone.png)

Als de gebruiker Hallo vereist toouse een PINCODE bij de verificatie, vraagt Hallo pagina hen toocreate een PINCODE. Na het invoeren van hun telefoonnummer (s) en PINCODE (indien van toepassing), klikt de gebruiker Hallo op Hallo **Bel Me nu tooAuthenticate** knop. Azure multi-factor Authentication voert een telefonische oproep verificatie toohello gebruiker primaire telefoonnummer. Hallo-gebruiker moet beantwoorden Hallo telefoongesprek en hun PINCODE invoeren (indien van toepassing) en druk op # toomove op de volgende stap van het zelfregistratieproces hello toohello.

Als Hallo gebruiker verificatiemethode Hallo-tekstbericht selecteert of vooraf geconfigureerde toouse die methode is, vraagt Hallo pagina Hallo gebruiker naar het nummer van hun mobiele telefoon. Als de gebruiker Hallo vereist toouse een PINCODE bij de verificatie, vraagt Hallo pagina ook hen tooenter een PINCODE.  Na het invoeren van hun telefoonnummer en PINCODE (indien van toepassing), klikt de gebruiker Hallo op Hallo **SMS Me nu tooAuthenticate** knop. Azure multi-factor Authentication voert een SMS-verificatie toohello gebruiker mobiele telefoon. Hallo gebruiker ontvangt Hallo SMS-bericht met een een-eenmalig-OTP (wachtwoordcode) en vervolgens antwoorden toohello bericht met die Eenmalige plus de PINCODE (indien van toepassing).

![Sms gebruikersportal](./media/multi-factor-authentication-get-started-portal/text.png)

Hallo-gebruiker selecteert Hallo mobiele App verificatiemethode, Hallo pagina Hallo gebruiker tooinstall Hallo Microsoft Authenticator-app op hun apparaat gevraagd als een activeringscode genereren. Na de installatie van Hallo app klikt Hallo gebruiker op de knop activeringscode genereren Hallo.

> [!NOTE]
> toouse hello Microsoft Authenticator-app moet Hallo gebruiker pushmeldingen voor hun apparaat inschakelen.

Hallo pagina geeft een activeringscode en URL samen met een streepjescode. Als de gebruiker Hallo vereist toouse een PINCODE bij de verificatie, vraagt Hallo pagina bovendien hen tooenter een PINCODE. Hallo gebruiker voert Hallo activeringscode en URL in Hallo Microsoft Authenticator-app of Hallo scanner tooscan Hallo streepjescode streepjescode gebruikt en klikt op de knop activeren Hallo.

Nadat het Hallo-activering is voltooid, Hallo gebruiker Hallo **Verifieer Me nu** knop. Azure multi-factor Authentication voert een verificatie toohello gebruiker mobiele app. Hallo-gebruiker moet hun PINCODE invoeren (indien van toepassing) en drukt u op de knop Authenticeren Hallo in hun toomove mobiele app op de volgende stap van het zelfregistratieproces hello toohello.

Als beheerders Hallo hebt geconfigureerd hello Azure multi-factor Authentication-Server toocollect beveiligingsvragen en antwoorden, Hallo gebruiker hierna toohello beveiligingsvragen pagina. Hallo-gebruiker moet vier beveiligingsvragen selecteren en antwoorden tootheir geselecteerd vragen geven.

![Beveiligingsvragen van gebruikersportal](./media/multi-factor-authentication-get-started-portal/secq.png)

Hallo gebruiker inschrijving is nu voltooid en Hallo gebruiker is aangemeld in toohello gebruikersportal. Kunnen gebruikers zich aanmelden terug in de gebruikersportal toohello op elk gewenst moment in toekomstige toochange Hallo hun telefoonnummers, pincodes, verificatiemethoden en beveiligingsvragen als de methoden wijzigen door de beheerders is toegestaan.

## <a name="next-steps"></a>Volgende stappen

- [Hello Azure multi-factor Authentication Server Mobile App Web Service implementeren](multi-factor-authentication-get-started-server-webservice.md)
