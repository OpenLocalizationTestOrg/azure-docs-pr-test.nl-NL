---
title: aaaTroubleshoot foutcodes voor hello Azure MFA NPS extensie | Microsoft Docs
description: Hulp bij het oplossen van problemen met Hallo NPS-extensie voor Azure multi-factor Authentication met specifieke oplossingen voor algemene foutberichten
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 8b602954364c6e9f801d86edca6432bd8446c58b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="resolve-error-messages-from-hello-nps-extension-for-azure-multi-factor-authentication"></a>Foutberichten van Hallo NPS-extensie voor Azure multi-factor Authentication oplossen

Als u fouten Hello NPS-extensie voor Azure multi-factor Authentication optreden, gebruikt u dit artikel tooreach een oplossing sneller. 

## <a name="troubleshooting-steps-for-common-errors"></a>Probleemoplossing voor veelvoorkomende fouten

| Foutcode | Stappen voor probleemoplossing |
| ---------- | --------------------- |
| **CONTACT_SUPPORT** | [Neem contact op met ondersteuning](#contact-microsoft-support), en het Hallo-lijst met stappen voor het verzamelen van Logboeken worden vermeld. Geef zoveel mogelijk gegevens over wat er gebeurd voordat de fout hello is, met inbegrip van tenant-id en de UPN (user Principal name). |
| **CLIENT_CERT_INSTALL_ERROR** | Mogelijk zijn er een probleem is met hoe Hallo-clientcertificaat is geïnstalleerd of die zijn gekoppeld aan uw tenant. Volg de instructies in Hallo [probleemoplossing Hallo MFA NPS extensie](multi-factor-authentication-nps-extension.md#troubleshooting) tooinvestigate client cert problemen. |
| **ESTS_TOKEN_ERROR** | Volg de instructies in Hallo [probleemoplossing Hallo MFA NPS extensie](multi-factor-authentication-nps-extension.md#troubleshooting) tooinvestigate client cert en ADAL-token problemen. |
| **HTTPS_COMMUNICATION_ERROR** | Hallo NPS-server is tooreceive reacties van Azure MFA. Controleer of de firewalls geopend bidirectioneel voor verkeer tooand van https://adnotifications.windowsazure.com zijn |
| **HTTP_CONNECT_ERROR** | Controleer of u https://adnotifications.windowsazure.com en https://login.microsoftonline.com/ kan bereiken op Hallo-server met NPS-extensie hello. Als deze sites niet laden, controleert u de verbinding op die server. |
| **REGISTRY_CONFIG_ERROR** | Er ontbreekt een sleutel in het register voor de toepassing hello, hetgeen kan Hallo Hallo [PowerShell-script](multi-factor-authentication-nps-extension.md#install-the-nps-extension) na de installatie is niet uitgevoerd. Fout bij het Hallo-bericht moet Hallo ontbrekende sleutel bevatten. Zorg ervoor dat u de sleutel Hallo onder HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\AzureMfa hebt. |
| **REQUEST_FORMAT_ERROR** <br> RADIUS-aanvraag ontbreken verplichte userName\Identifier Radius-kenmerk. Controleren of NPS RADIUS-aanvragen wordt ontvangen | Deze fout duidt normaal gesproken een installatieprobleem. Hallo NPS-uitbreiding moet worden geïnstalleerd in de NPS-servers die RADIUS-aanvragen kunnen ontvangen. NPS-servers die zijn geïnstalleerd als de afhankelijkheden voor services zoals RDG en RRAS geen radius-aanvragen worden ontvangen. Uitbreiding van NPS werkt niet als geïnstalleerd via dergelijke installaties en -fouten af omdat Hallo details van Hallo authenticatie-aanvraag kan niet worden gelezen. |
| **REQUEST_MISSING_CODE** | Zorg ervoor dat Hallo wachtwoord versleutelingsprotocol tussen hello NPS- en NAS-servers Hallo secundaire verificatiemethode die u ondersteunt. **PAP** ondersteunt alle Hallo-verificatiemethoden van Azure MFA in de cloud Hallo: telefoonoproep, eenzijdige SMS-bericht, mobiele-appmelding en verificatiecode mobiele app. **CHAPv2** en **EAP** telefoongesprek en mobiele-appmelding ondersteunen. |
| **USERNAME_CANONICALIZATION_ERROR** | Verifieer dat Hallo gebruiker aanwezig in uw lokale Active Directory-exemplaar is en die Hallo NPS-Service machtigingen tooaccess Hallo map heeft. Als u de vertrouwensrelaties tussen forests, [contact op met ondersteuning](#contact-microsoft-support) voor verdere assistentie. |


   

### <a name="alternate-login-id-errors"></a>Alternatieve aanmeldings-ID-fouten

| Foutcode | Foutbericht | Stappen voor probleemoplossing |
| ---------- | ------------- | --------------------- |
| **ALTERNATE_LOGIN_ID_ERROR** | Fout: userObjectSid opzoeken is mislukt | Controleer of dat deze gebruiker Hallo bestaat in uw lokale Active Directory-exemplaar. Als u de vertrouwensrelaties tussen forests, [contact op met ondersteuning](#contact-microsoft-support) voor verdere assistentie. |
| **ALTERNATE_LOGIN_ID_ERROR** | Fout: Er is een alternatieve LoginId lookup mislukt | Controleren of LDAP_ALTERNATE_LOGINID_ATTRIBUTE tooa is ingesteld [geldig active directory-kenmerk](https://msdn.microsoft.com/library/ms675090(v=vs.85).aspx). <br><br> Als LDAP_FORCE_GLOBAL_CATALOG tooTrue is ingesteld of LDAP_LOOKUP_FORESTS is geconfigureerd met een niet-lege waarde, moet u controleren of u een globale catalogus hebt geconfigureerd en dat Hallo AlternateLoginId kenmerk tooit wordt toegevoegd. <br><br> Als LDAP_LOOKUP_FORESTS is geconfigureerd met een niet-lege waarde, moet u controleren of Hallo-waarde juist is. Als er meer dan één naam van het forest, moeten Hallo namen worden gescheiden met puntkomma's, geen spaties. <br><br> Als deze stappen Hallo-probleem niet oplost [contact op met ondersteuning](#contact-microsoft-support) voor meer informatie. |
| **ALTERNATE_LOGIN_ID_ERROR** | Fout: Alternatieve LoginId waarde is leeg | Controleer of dat Hallo AlternateLoginId-kenmerk is geconfigureerd voor Hallo gebruiker. |


## <a name="errors-your-users-may-encounter"></a>Uw gebruikers kunnen ondervinden fouten

| Foutcode | Foutbericht | Stappen voor probleemoplossing |
| ---------- | ------------- | --------------------- |
| **AccessDenied** | Tenant van de aanroeper heeft geen machtigingen toodo verificatie voor Hallo-gebruiker | Controleer of hello tenant en Hallo domein van Hallo UPN (user Principal name) zijn Hallo dezelfde. Bijvoorbeeld, zorg ervoor dat user@contoso.com probeert tooauthenticate toohello Contoso-tenant. Hallo UPN vertegenwoordigt een geldige gebruiker voor de tenant Hallo in Azure. |
| **AuthenticationMethodNotConfigured** | Hallo opgegeven verificatiemethode niet is geconfigureerd voor het Hallo-gebruiker | Hallo-gebruiker toevoegen of controleren van hun verificatiemethoden volgens de instructies in toohello [beheren van uw instellingen voor verificatie in twee stappen](./end-user/multi-factor-authentication-end-user-manage-settings.md). |
| **AuthenticationMethodNotSupported** | Opgegeven verificatiemethode wordt niet ondersteund. | Alle logboeken met deze fout te verzamelen en [contact op met ondersteuning](#contact-microsoft-support). Wanneer u contact op met ondersteuning, bieden Hallo gebruikersnaam en het Hallo secundaire verificatiemethode die Hallo fout heeft veroorzaakt. |
| **BecAccessDenied** | MSODS Bec aanroep heeft geretourneerd van de toegang is geweigerd, waarschijnlijk-Hallo username is niet gedefinieerd in Hallo-tenant | Hallo aanwezig is in Active Directory lokale, maar de gebruiker is niet gesynchroniseerd naar Azure AD door AD Connect. Of Hallo gebruiker ontbreekt voor Hallo-tenant. Hallo gebruiker tooAzure AD toevoegen en toe te voegen hun verificatiemethoden volgens de instructies in toohello [beheren van uw instellingen voor verificatie in twee stappen](./end-user/multi-factor-authentication-end-user-manage-settings.md). |
| **InvalidFormat** of **StrongAuthenticationServiceInvalidParameter** | Hallo telefoonnummer heeft een onherkenbare indeling | Hallo gebruiker corrigeren hun telefoonnummers verificatie hebben. |
| **InvalidSession** | Hallo opgegeven sessie is ongeldig of verlopen | Hallo-sessie heeft meer dan drie minuten toocomplete genomen. Controleer of u die gebruiker Hallo Hallo verificatiecode invoeren of reageert niet toohello app-melding binnen drie minuten na het Hallo-verificatieaanvraag initiëren. Als dat niet Hallo probleem is verholpen, controleert u er zijn geen netwerkvertragingen tussen de client, NAS-Server, NPS-Server en hello Azure MFA-eindpunt.  |
| **NoDefaultAuthenticationMethodIsConfigured** | Er is geen standaardverificatiemethode is geconfigureerd voor het Hallo-gebruiker | Hallo-gebruiker toevoegen of controleren van hun verificatiemethoden volgens de instructies in toohello [beheren van uw instellingen voor verificatie in twee stappen](./end-user/multi-factor-authentication-end-user-manage-settings.md). Controleer of u die Hallo gebruiker heeft ervoor gekozen een standaardmethode voor verificatie en geconfigureerd die methode voor hun rekening. |
| **OathCodePinIncorrect** | Onjuiste code en pincode ingevoerd. | Deze fout wordt niet verwacht in Hallo NPS-extensie. Als de gebruiker tegenkomt, [contact op met ondersteuning](#contact-microsoft-support) voor hulp bij probleemoplossing. |
| **ProofDataNotFound** | Bewijs gegevens niet is geconfigureerd voor Hallo opgegeven verificatiemethode. | Hallo gebruiker probeert een andere verificatiemethode of Voeg een nieuwe verificatiemethoden volgens de instructies in toohello [beheren van uw instellingen voor verificatie in twee stappen](./end-user/multi-factor-authentication-end-user-manage-settings.md). Als gebruiker Hallo toosee deze fout nadat u hebt bevestigd blijft dat hun verificatiemethode correct is ingesteld [contact op met ondersteuning](#contact-microsoft-support). |
| **SMSAuthFailedWrongCodePinEntered** | Onjuiste code en pincode ingevoerd. (OneWaySMS) | Deze fout wordt niet verwacht in Hallo NPS-extensie. Als de gebruiker tegenkomt, [contact op met ondersteuning](#contact-microsoft-support) voor hulp bij probleemoplossing. |
| **TenantIsBlocked** | Tenant is geblokkeerd | [Neem contact op met ondersteuning](#contact-microsoft-support) met map-ID van de eigenschappenpagina hello Azure AD in hello Azure-portal. |
| **UserNotFound** | Hallo opgegeven gebruiker is niet gevonden. | Hallo-tenant is niet langer zichtbaar als actief in Azure AD. Controleer of uw abonnement actief is en u Hallo hebt vereist eerste apps van derden. Controleer ook of Hallo tenant in het certificaatonderwerp Hallo is zoals verwacht en Hallo-certificaat is nog steeds geldig en geregistreerde onder Hallo service-principal. |

## <a name="messages-your-users-may-encounter-that-arent-errors"></a>Berichten die uw gebruikers kunnen ondervinden die zich niet fouten

Uw gebruikers kunnen soms berichten ophalen van multi-factor Authentication omdat hun authenticatie-aanvraag is mislukt. Deze fouten in Hallo product van de configuratie niet, maar zijn opzettelijk waarschuwingen waarin wordt uitgelegd waarom een verificatieaanvraag is geweigerd.

| Foutcode | Foutbericht | Aanbevolen stappen | 
| ---------- | ------------- | ----------------- |
| **OathCodeIncorrect** | Onjuiste code entered\OATH Code is onjuist | Niet door een fout gebruiker heeft onjuiste code ingevoerd. | Hallo gebruiker Hallo onjuiste code ingevoerd. Hebben ze opnieuw proberen door een nieuwe code aanvragen of meldt u zich opnieuw. | 
| **SMSAuthFailedMaxAllowedCodeRetryReached** | Maximale toegestane code opnieuw proberen is bereikt | Hallo-gebruiker is Hallo verificatie uitdaging te vaak mislukt. Afhankelijk van uw instellingen mogelijk moeten toobe gedeblokkeerd nu door een beheerder.  |
| **SMSAuthFailedWrongCodeEntered** | Code verkeerd ingevoerde/tekst bericht OTP onjuist | Hallo gebruiker Hallo onjuiste code ingevoerd. Hebben ze opnieuw proberen door een nieuwe code aanvragen of meldt u zich opnieuw. |

## <a name="errors-that-require-support"></a>Fouten die ondersteuning nodig hebt

Als u een van deze fouten optreden, raden we u [contact op met ondersteuning](#contact-microsoft-support) voor diagnostische informatie. Er is geen standaard ingesteld van de stappen die deze fouten kunt oplossen. Wanneer u Neem contact op met ondersteuning, moet u ervoor dat tooinclude als veel informatie mogelijk over Hallo stappen die tooan fout geleid en uw tenant.

| Foutcode | Foutbericht |
| ---------- | ------------- |
| **InvalidParameter** | Aanvraag mag niet null zijn |
| **InvalidParameter** | Object-id mag geen null of leeg zijn voor ReplicationScope: {0} |
| **InvalidParameter** | lengte van NaamBedrijf Hallo \{0} \ is langer dan Hallo maximaal toegestane lengte {1} |
| **InvalidParameter** | UserPrincipalName moet niet null of leeg zijn |
| **InvalidParameter** | Hallo opgegeven dat tenantid zich niet in de juiste indeling |
| **InvalidParameter** | Sessie-id mag geen null of leeg zijn |
| **InvalidParameter** | Kan ProofData van aanvraag of Msods niet omzetten. Hallo ProofData is onbekend |
| **InternalError** |  |
| **OathCodePinIncorrect** |  |
| **VersionNotSupported** |  |
| **MFAPinNotSetup** |  |

## <a name="next-steps"></a>Volgende stappen

### <a name="troubleshoot-user-accounts"></a>Gebruikersaccounts oplossen

Als uw gebruikers zijn [problemen hebt met verificatie in twee stappen](./end-user/multi-factor-authentication-end-user-troubleshoot.md), helpen ze problemen diagnosticeren zelf. 

### <a name="contact-microsoft-support"></a>Neem contact op met Microsoft ondersteuning

Als u meer hulp nodig hebt, neem dan contact op met een supportmedewerker via [ondersteuning van Azure multi-factor Authentication-Server](https://support.microsoft.com/oas/default.aspx?prid=14947). Wanneer u contact met ons, is het handig als u zo veel mogelijk gegevens over uw probleem mogelijk kunt opnemen. Informatie die kunt u opgeven omvat Hallo pagina waar u hebt gezien Hallo fout met een specifieke fout code, Hallo bepaalde sessie-ID, Hallo-ID van gebruiker Hallo Hallo die Hallo fout hebt gezien en logboeken voor foutopsporing.

toocollect foutopsporingslogboeken voor ondersteuning van diagnostische gegevens, gebruikt u Hallo stappen te volgen: 

1. Open een opdrachtprompt als Administrator en voer deze opdrachten uit:

   ```
   Mkdir c:\NPS
   Cd NPS
   netsh trace start Scenario=NetConnection capture=yes tracefile=c:\NPS\nettrace.etl
   logman create trace "NPSExtension" -ow -o c:\NPS\NPSExtension.etl -p {7237ED00-E119-430B-AB0F-C63360C8EE81} 0xffffffffffffffff 0xff -nb 16 16 -bs 1024 -mode Circular -f bincirc -max 4096 -ets
   logman update trace "NPSExtension" -p {EC2E6D3A-C958-4C76-8EA4-0262520886FF} 0xffffffffffffffff 0xff -ets
   ```

2. Reproduceer Hallo probleem

3. Stop Hallo tracering met de volgende opdrachten:

   ```
   logman stop "NPSExtension" -ets
   netsh trace stop
   wevtutil epl AuthNOptCh C:\NPS\%computername%_AuthNOptCh.evtx
   wevtutil epl AuthZOptCh C:\NPS\%computername%_AuthZOptCh.evtx
   wevtutil epl AuthZAdminCh C:\NPS\%computername%_AuthZAdminCh.evtx
   Start .
   ```

4. Hallo-inhoud van Hallo C:\NPS map ZIP en Hallo ZIP-bestand toohello ondersteuningsaanvraag koppelen.


