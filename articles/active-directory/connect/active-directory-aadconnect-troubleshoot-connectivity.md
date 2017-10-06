---
title: 'Azure AD Connect: Problemen met verbindingen | Microsoft Docs'
description: Legt uit hoe tootroubleshoot connectiviteit problemen met een Azure AD Connect.
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 3aa41bb5-6fcb-49da-9747-e7a3bd780e64
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 60d6b7c4ad8a3ab907c20e598ec9443f115df287
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-connectivity-issues-with-azure-ad-connect"></a>Oplossen van problemen met de netwerkverbinding met Azure AD Connect
Dit artikel wordt uitgelegd hoe de verbinding tussen Azure AD Connect en Azure AD werkt en hoe tootroubleshoot connectiviteit uitgeeft. Deze problemen zijn de meest waarschijnlijke toobe gezien in een omgeving met een proxyserver.

## <a name="troubleshoot-connectivity-issues-in-hello-installation-wizard"></a>Problemen met verbindingen in de installatiewizard Hallo
Azure AD Connect maakt gebruik van moderne verificatie (met Hallo ADAL-bibliotheek) voor verificatie. Hallo-installatiewizard en de juiste Hallo synchronisatie-engine vereisen machine.config toobe omdat deze twee .NET-toepassingen de juiste wijze geconfigureerd.

In dit artikel, laten we zien hoe tooAzure AD in Fabrikam verbinding maakt via de proxy. Hallo-proxyserver heet fabrikamproxy en poort 8080 wordt gebruikt.

Eerst moet u toomake ervoor [ **machine.config** ](active-directory-aadconnect-prerequisites.md#connectivity) correct is geconfigureerd.  
![machineconfig uit te voeren](./media/active-directory-aadconnect-troubleshoot-connectivity/machineconfig.png)

> [!NOTE]
> In sommige blogs niet-Microsoft wordt dat de wijzigingen moeten worden aangebracht toomiiserver.exe.config in plaats daarvan beschreven. Dit bestand is echter overschreven bij elke upgrade dus zelfs als dit tijdens de initiële installatie werkt, Hallo systeem werkt niet bij een eerste upgrade. Daarom wordt aangeraden Hallo tooupdate machine.config in plaats daarvan.
>
>

Hallo-proxyserver moet zijn toegewezen Hallo vereist URL's die zijn geopend. Hallo officiële lijst wordt beschreven in [Office 365-URL's en IP-adresbereiken](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2).

URL's is Hallo tabel Hallo absolute bare minimale toobe kunnen tooconnect tooAzure AD. Deze lijst bevat geen eventuele optionele functies, zoals wachtwoord terugschrijven of Azure AD Connect Health. Het is gedocumenteerde hier toohelp bij het oplossen van de eerste configuratie Hallo.

| URL | Poort | Beschrijving |
| --- | --- | --- |
| mscrl.Microsoft.com |HTTP-/ 80 |Gebruikte toodownload CRL bevat. |
| \*. verisign.com |HTTP-/ 80 |Gebruikte toodownload CRL bevat. |
| \*. entrust.com |HTTP-/ 80 |Gebruikte toodownload CRL geeft een lijst voor MFA. |
| \*.windows.net |HTTPS/443 |Gebruikte toosign in tooAzure AD. |
| Secure.aadcdn.microsoftonline p.com |HTTPS/443 |Gebruikt voor MFA. |
| \*.microsoftonline.com |HTTPS/443 |Tooconfigure uw Azure AD-directory en voor importeren/exporteren gegevens gebruikt. |

## <a name="errors-in-hello-wizard"></a>Fouten in de wizard Hallo
Hallo-installatiewizard maakt gebruik van twee andere beveiligingscontext. Op de pagina Hallo **verbinding tooAzure AD**, het gebruik van Hallo momenteel aangemelde gebruiker. Op de pagina Hallo **configureren**, verandert het toohello [account voor service voor de synchronisatie-engine Hallo Hallo](active-directory-aadconnect-accounts-permissions.md#azure-ad-connect-sync-service-account). Als er een probleem is, verschijnt deze waarschijnlijk al op Hallo **verbinding tooAzure AD** pagina in de wizard Hallo omdat Hallo proxyconfiguratie globale.

Hallo volgende problemen zijn Hallo meest voorkomende fouten die in de installatiewizard Hallo optreden.

### <a name="hello-installation-wizard-has-not-been-correctly-configured"></a>Hallo-installatiewizard niet correct is geconfigureerd
Deze fout wordt weergegeven wanneer het Hallo-wizard zelf Hallo proxy niet bereiken.  
![nomachineconfig](./media/active-directory-aadconnect-troubleshoot-connectivity/nomachineconfig.png)

* Als u deze fout aanhoudt, controleert u of Hallo [machine.config](active-directory-aadconnect-prerequisites.md#connectivity) correct is geconfigureerd.
* Als die er goed uitziet, stappen Hallo in [controleren of de proxy verbinding](#verify-proxy-connectivity) toosee als Hallo probleem buiten Hallo wizard ook aanwezig is.

### <a name="a-microsoft-account-is-used"></a>Een Microsoft-account wordt gebruikt
Als u een **Microsoft-account** in plaats van een **school of organisatie** account, ziet u een algemene fout.  
![Een Microsoft-Account wordt gebruikt](./media/active-directory-aadconnect-troubleshoot-connectivity/unknownerror.png)

### <a name="hello-mfa-endpoint-cannot-be-reached"></a>Hallo MFA-eindpunt kan niet worden bereikt
Deze fout treedt op als hello eindpunt **https://secure.aadcdn.microsoftonline-p.com** kan niet worden bereikt en de globale beheerder heeft MFA ingeschakeld.  
![nomachineconfig](./media/active-directory-aadconnect-troubleshoot-connectivity/nomicrosoftonlinep.png)

* Als u deze fout aanhoudt, controleert u of dat eindpunt Hallo **secure.aadcdn.microsoftonline p.com** toohello proxy is toegevoegd.

### <a name="hello-password-cannot-be-verified"></a>Hallo wachtwoord kan niet worden geverifieerd.
Als Hallo-installatiewizard tooAzure AD verbinding geslaagd is, maar Hallo wachtwoord zelf kan niet worden geverifieerd dat u deze fout te zien:  
![badpassword](./media/active-directory-aadconnect-troubleshoot-connectivity/badpassword.png)

* Hallo-wachtwoord is een tijdelijk wachtwoord en moet worden gewijzigd? Is het juiste wachtwoord voor het daadwerkelijk Hallo? Probeer toosign in toohttps://login.microsoftonline.com (op een andere computer dan hello Azure AD Connect-server) en controleer of Hallo-account kan worden gebruikt.

### <a name="verify-proxy-connectivity"></a>Controleer de proxy-connectiviteit
tooverify als hello Azure AD Connect-server heeft de werkelijke connectiviteit met hello Proxy- en Internet, gebruikt u sommige toosee PowerShell als Hallo proxy toestaat webaanvragen of niet. Voer in een PowerShell-prompt `Invoke-WebRequest -Uri https://adminwebservice.microsoftonline.com/ProvisioningService.svc`. (Technisch hello eerste aanroep is toohttps://login.microsoftonline.com en deze URI werkt ook, maar hello andere URI is sneller toorespond.)

Hallo configuration PowerShell gebruikt in machine.config toocontact Hallo proxy. Hallo-instellingen van winhttp/netsh moeten geen invloed op deze cmdlets.

Als Hallo proxy correct is geconfigureerd, krijgt u de status geslaagd: ![proxy200](./media/active-directory-aadconnect-troubleshoot-connectivity/invokewebrequest200.png)

Als u krijgt **niet kan tooconnect toohello externe server**, PowerShell probeert een directe aanroep toomake zonder Hallo proxy of DNS is niet correct geconfigureerd. Zorg ervoor dat Hallo **machine.config** bestand correct is geconfigureerd.
![unabletoconnect](./media/active-directory-aadconnect-troubleshoot-connectivity/invokewebrequestunable.png)

Als het Hallo-proxy is niet correct geconfigureerd, krijgt u een fout opgetreden: ![proxy200](./media/active-directory-aadconnect-troubleshoot-connectivity/invokewebrequest403.png)
![proxy407](./media/active-directory-aadconnect-troubleshoot-connectivity/invokewebrequest407.png)

| Fout | Foutbericht | Opmerking |
| --- | --- | --- |
| 403 |Is niet toegestaan |Hallo-proxy is niet geopend voor Hallo URL aangevraagde. Hallo-proxyconfiguratie bezoekt en zorg ervoor dat Hallo [URL's](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2) zijn geopend. |
| 407 |Proxyverificatie is vereist |Hallo-proxyserver vereist een aanmelden en geen taaksequencer opgegeven. Als de proxyserver verificatie vereist, zorg ervoor dat toohave deze instelling is geconfigureerd in Hallo machine.config. Controleer ook of dat u domeinaccounts gebruikt voor Hallo-gebruiker die de wizard Hallo en voor het Hallo-serviceaccount. |

## <a name="hello-communication-pattern-between-azure-ad-connect-and-azure-ad"></a>Hallo communicatiepatronen tussen Azure AD Connect en Azure AD
Als u deze voorgaande stappen hebt uitgevoerd en nog steeds geen verbinding kunt maken, u mogelijk op dit moment gaan zo kijken netwerk Logboeken. Deze sectie wordt een patroon normaal en geslaagde verbinding documenteren. Het is ook algemene rood herrings die kan worden genegeerd wanneer u Hallo netwerk logboeken lezen aanbieding.

* Er zijn toohttps://dc.services.visualstudio.com aanroepen. Het is niet vereist toohave die deze URL openen in Hallo-proxy voor Hallo installatie toosucceed en deze aanroepen kan worden genegeerd.
* U ziet dat DNS-omzetting Hallo werkelijke hosts toobe in Hallo DNS-naam ruimte nsatc.net en andere naamruimten niet onder microsoftonline.com bevat. Echter er zijn webserviceaanvragen op Hallo werkelijke servernamen en u hebt geen tooadd deze URL's toohello proxy.
* Hallo eindpunten adminwebservice en provisioningapi detectie eindpunten en toofind Hallo echt eindpunt toouse gebruikt. Deze eindpunten zijn verschillend afhankelijk van uw regio.

### <a name="reference-proxy-logs"></a>Verwijzing proxy-Logboeken
Hier volgt een dump van een werkelijke proxy logboek en Hallo wizard installatiepagina waar is gemaakt (dubbele vermeldingen toohello hetzelfde eindpunt zijn verwijderd). Deze sectie kan worden gebruikt als referentie voor uw eigen logboeken proxy en het netwerk. Hallo werkelijke eindpunten kunnen afwijken in uw omgeving (met name de URL's in *cursief*).

**Verbinding maken met tooAzure AD**

| Time | URL |
| --- | --- |
| 1/11/2016 8:31 |Connect://login.microsoftonline.com:443 |
| 1/11/2016 8:31 |Connect://adminwebservice.microsoftonline.com:443 |
| 1/11/2016 8:32 |verbinding: / /*bba800 anker*. microsoftonline.com:443 |
| 1/11/2016 8:32 |Connect://login.microsoftonline.com:443 |
| 1/11/2016 8:33 |Connect://provisioningapi.microsoftonline.com:443 |
| 1/11/2016 8:33 |verbinding: / /*bwsc02 relay*. microsoftonline.com:443 |

**Configureren**

| Time | URL |
| --- | --- |
| 1/11/2016 8:43 |Connect://login.microsoftonline.com:443 |
| 1/11/2016 8:43 |verbinding: / /*bba800 anker*. microsoftonline.com:443 |
| 1/11/2016 8:43 |Connect://login.microsoftonline.com:443 |
| 1/11/2016 8:44 |Connect://adminwebservice.microsoftonline.com:443 |
| 1/11/2016 8:44 |verbinding: / /*bba900 anker*. microsoftonline.com:443 |
| 1/11/2016 8:44 |Connect://login.microsoftonline.com:443 |
| 1/11/2016 8:44 |Connect://adminwebservice.microsoftonline.com:443 |
| 1/11/2016 8:44 |verbinding: / /*bba800 anker*. microsoftonline.com:443 |
| 1/11/2016 8:44 |Connect://login.microsoftonline.com:443 |
| 1/11/2016 8:46 |Connect://provisioningapi.microsoftonline.com:443 |
| 1/11/2016 8:46 |verbinding: / /*bwsc02 relay*. microsoftonline.com:443 |

**Initiële synchronisatie**

| Time | URL |
| --- | --- |
| 1/11/2016 8:48 |Connect://login.Windows.NET:443 |
| 1/11/2016 8:49 |Connect://adminwebservice.microsoftonline.com:443 |
| 1/11/2016 8:49 |verbinding: / /*bba900 anker*. microsoftonline.com:443 |
| 1/11/2016 8:49 |verbinding: / /*bba800 anker*. microsoftonline.com:443 |

## <a name="authentication-errors"></a>Verificatiefouten
Deze sectie bevat informatie over fouten die kunnen worden geretourneerd van ADAL (Hallo verificatiebibliotheek wordt gebruikt door Azure AD Connect) en PowerShell. Hallo fout uitgelegd kunt u in de volgende stappen te begrijpen.

### <a name="invalid-grant"></a>Ongeldige verlenen
Ongeldige gebruikersnaam of wachtwoord. Zie voor meer informatie [Hallo wachtwoord kan niet worden geverifieerd](#the-password-cannot-be-verified).

### <a name="unknown-user-type"></a>Onbekende gebruikerstype
Uw Azure AD-directory kan niet worden gevonden of opgelost. U probeert misschien toologin met een gebruikersnaam in een niet-geverifieerd domein?

### <a name="user-realm-discovery-failed"></a>Gebruiker Realm detectie is mislukt
Netwerk- of proxyinstellingen configuratieproblemen. Hallo-netwerk kan niet worden bereikt. Zie [problemen met verbindingen in de installatiewizard Hallo](#troubleshoot-connectivity-issues-in-the-installation-wizard).

### <a name="user-password-expired"></a>Gebruikerswachtwoord verlopen
Uw referenties zijn verlopen. Uw wachtwoord wijzigen.

### <a name="authorizationfailure"></a>AuthorizationFailure
Onbekend probleem.

### <a name="authentication-cancelled"></a>Verificatie is geannuleerd
Hallo multi-factor authentication (MFA) uitdaging is geannuleerd.

### <a name="connecttomsonline"></a>ConnectToMSOnline
Verificatie is gelukt, maar er is een verificatieprobleem met Azure AD PowerShell.

### <a name="azurerolemissing"></a>AzureRoleMissing
Verificatie is gelukt. U bent geen hoofdbeheerder.

### <a name="privilegedidentitymanagement"></a>PrivilegedIdentityManagement
Verificatie is gelukt. Beschermde identiteitsbeheer is ingeschakeld en u bent momenteel niet een globale beheerder. Zie voor meer informatie [Privileged Identity Management](../active-directory-privileged-identity-management-getting-started.md).

### <a name="companyinfounavailable"></a>CompanyInfoUnavailable
Verificatie is gelukt. Kan de bedrijfsgegevens niet ophalen uit Azure AD.

### <a name="retrievedomains"></a>RetrieveDomains
Verificatie is gelukt. Kan de domeingegevens niet ophalen uit Azure AD.

### <a name="unexpected-exception"></a>Onverwachte uitzondering
Onverwachte fout opgetreden in de installatiewizard Hallo weergegeven. Kan gebeuren als u toouse probeert een **Microsoft-Account** in plaats van een **school of organisatie-account**.

## <a name="troubleshooting-steps-for-previous-releases"></a>Stappen voor probleemoplossing voor eerdere versies.
Met versies die beginnen met de build-nummer 1.1.105.0 (februari 2016 uitgebracht), Hallo-aanmeldhulp buiten gebruik werd gesteld. Deze sectie en Hallo configuratie mag niet langer zijn vereist, maar wordt opgeslagen als referentie.

Voor Hallo eenmalige aanmelding in assistent toowork, moet winhttp worden geconfigureerd. Deze configuratie kunt u doen met [ **netsh**](active-directory-aadconnect-prerequisites.md#connectivity).  
![Netsh](./media/active-directory-aadconnect-troubleshoot-connectivity/netsh.png)

### <a name="hello-sign-in-assistant-has-not-been-correctly-configured"></a>Hallo-aanmeldhulp is niet correct geconfigureerd
Deze fout wordt weergegeven wanneer Hallo-aanmeldhulp niet Hallo proxy bereiken of Hallo proxy Hallo-aanvraag niet toestaat.
![nonetsh](./media/active-directory-aadconnect-troubleshoot-connectivity/nonetsh.png)

* Als deze fout wordt weergegeven, bekijkt hello proxyconfiguratie in [netsh](active-directory-aadconnect-prerequisites.md#connectivity) en controleer of deze juist is.
  ![netshshow](./media/active-directory-aadconnect-troubleshoot-connectivity/netshshow.png)
* Als die er goed uitziet, stappen Hallo in [controleren of de proxy verbinding](#verify-proxy-connectivity) toosee als Hallo probleem buiten Hallo wizard ook aanwezig is.

## <a name="next-steps"></a>Volgende stappen
Lees meer over het [integreren van uw on-premises identiteiten met Azure Active Directory](active-directory-aadconnect.md).
