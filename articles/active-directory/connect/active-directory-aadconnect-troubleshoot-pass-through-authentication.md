---
title: 'Azure AD Connect: Problemen met Pass through-verificatie | Microsoft Docs'
description: Dit artikel wordt beschreven hoe tootroubleshoot Pass-through-verificatie voor Azure Active Directory (Azure AD).
services: active-directory
keywords: Problemen met Azure AD Connect Pass through-verificatie, installeert u Active Directory, de vereiste onderdelen voor Azure AD, SSO, Single Sign-on
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: billmath
ms.openlocfilehash: 87130952f660762f91b0a34b05287603b565639f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-active-directory-pass-through-authentication"></a>Problemen met Azure Active Directory Pass-through-verificatie

Dit artikel helpt u bij het oplossen van problemen informatie over veelvoorkomende problemen met betrekking tot Azure AD Pass-through-verificatie.

>[!IMPORTANT]
>Als u gebruiker aanmeldingsproblemen met Pass through-verificatie worden geconfronteerd, geen Hallo functie uitschakelen of Pass through-verificatie Agents verwijderen zonder een toofall alleen in de cloud hoofdbeheerder account opnieuw in. Meer informatie over [toevoegen van een cloudconfiguratie globale beheerdersaccount](../active-directory-users-create-azure-portal.md). Deze stap is van essentieel belang en zorgt ervoor dat u geen toegang buiten uw tenant.

## <a name="general-issues"></a>Algemene problemen

### <a name="check-status-of-hello-feature-and-authentication-agents"></a>Controleer de status van het Hallo-functie en de verificatie-Agents

Zorg ervoor dat Hallo Pass through-verificatie-functie is nog steeds **ingeschakeld** ziet u op de status van uw tenant en Hallo van verificatie Agents **Active**, en niet **inactief**. U kunt de status controleren door te gaan toohello **Azure AD Connect** blade op Hallo [Azure Active Directory-beheercentrum](https://aad.portal.azure.com/).

![Azure Active Directory-beheercentrum - blade van Azure AD Connect](./media/active-directory-aadconnect-pass-through-authentication/pta7.png)

![Azure Active Directory-beheercentrum - blade Pass through-verificatie](./media/active-directory-aadconnect-pass-through-authentication/pta11.png)

### <a name="user-facing-sign-in-error-messages"></a>Gebruikersgerichte aanmelden foutberichten

Als Hallo-gebruiker kan niet toosign in Pass through-verificatie gebruikt, kunnen ze Zie een van de Hallo gebruikersgerichte fouten op Hallo Azure AD in het scherm volgen: 

|Fout|Beschrijving|Oplossing
| --- | --- | ---
|AADSTS80001|Kan geen tooconnect tooActive Directory|Zorg dat de agentservers maken deel uit van Hallo dezelfde AD-forest als Hallo gebruikers waarvan de wachtwoorden toobe gevalideerd moeten en ze kunnen tooconnect tooActive Directory zijn.  
|AADSTS8002|Er is een time-out opgetreden verbindende tooActive Directory|Controleer tooensure dat Active Directory beschikbaar is en toorequests van Hallo agents reageert.
|AADSTS80004|Hallo gebruikersnaam doorgegeven toohello agent is niet geldig|Zorg ervoor dat Hallo gebruiker probeert toosign met de juiste gebruikersnaam Hallo.
|AADSTS80005|Validatie onvoorspelbare WebException aangetroffen|Een tijdelijke fout. Hallo aanvraag opnieuw proberen. Als deze toofail blijft, moet u contact op met Microsoft ondersteuning.
|AADSTS80007|Er is een fout opgetreden communiceert met Active Directory|Hallo agent logboeken voor meer informatie en controleer of dat de Active Directory wordt uitgevoerd zoals verwacht.

### <a name="sign-in-failure-reasons-on-hello-azure-active-directory-admin-center"></a>Aanmelding mislukt redenen op Hallo Azure Active Directory-beheercentrum

Beginnen met het oplossen van problemen met aanmelden gebruiker door te kijken Hallo [aanmeldingsactiviteiten rapport](../active-directory-reporting-activity-sign-ins.md) op Hallo [Azure Active Directory-beheercentrum](https://aad.portal.azure.com/).

![Azure Active Directory-beheercentrum - aanmeldingen rapport](./media/active-directory-aadconnect-pass-through-authentication/pta4.png)

Navigeer te**Azure Active Directory** -> **aanmeldingen** op Hallo [Azure Active Directory-beheercentrum](https://aad.portal.azure.com/) en klik op een specifieke gebruiker aanmelden activiteit. Zoek naar Hallo **SIGN-IN-FOUTCODE** veld. Hallo-waarde voor dat veld tooa oorzaak en oplossing met behulp van de volgende tabel Hallo toewijzen:

|Aanmelden foutcode|Aanmelding mislukt reden|Oplossing
| --- | --- | ---
| 50144 | Het Active Directory-wachtwoord van de gebruiker is verlopen. | Wachtwoord opnieuw instellen van Hallo gebruiker in uw lokale Active Directory.
| 80001 | Er is geen verificatieagent beschikbaar. | Installeren en registreren van een verificatie-Agent.
| 80002 | Er is een time-out opgetreden bij de wachtwoordvalidatie voor de verificatieagent. | Controleer of uw Active Directory bereikbaar is vanaf Hallo verificatie-Agent is.
| 80003 | Ongeldig antwoord ontvangen door de verificatieagent. | Als Hallo probleem consistent reproduceerbare tussen meerdere gebruikers, Controleer uw Active Directory-configuratie.
| 80004 | Onjuiste UPN (user principal name) gebruikt voor aanmeldingsaanvraag. | Hallo gebruiker toosign met de juiste gebruikersnaam Hallo vraag.
| 80005 | Verificatieagent: er is een fout opgetreden. | Tijdelijke fout. Probeer het later opnieuw.
| 80007 | Verificatie-Agent kan geen tooconnect tooActive Directory. | Controleer of uw Active Directory bereikbaar is vanaf Hallo verificatie-Agent is.
| 80010 | Wachtwoord voor de Agent kan geen toodecrypt verificatie. | Als Hallo probleem consistent reproduceerbare, installeren en registreren van een nieuwe Agent voor verificatie. En Hallo huidige verwijderen. 
| 80011 | Verificatie-Agent kan geen tooretrieve ontsleutelingssleutel. | Als Hallo probleem consistent reproduceerbare, installeren en registreren van een nieuwe Agent voor verificatie. En Hallo huidige verwijderen.

## <a name="authentication-agent-installation-issues"></a>Agent-installatie verificatieproblemen

### <a name="an-unexpected-error-occurred"></a>Er is een onverwachte fout opgetreden

[Verzamelen van Logboeken van de agent](#collecting-pass-through-authentication-agent-logs) van Hallo-server en neem contact op met Microsoft Support met het probleem.

## <a name="authentication-agent-registration-issues"></a>Problemen met de registratie van de verificatie-Agent

### <a name="registration-of-hello-authentication-agent-failed-due-tooblocked-ports"></a>Registratie van Hallo verificatie-Agent is mislukt vanwege tooblocked poorten

Zorg ervoor dat Hallo-server op welke Hallo verificatie-Agent is geïnstalleerd kan communiceren met onze service-URL's en poorten die worden vermeld [hier](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-1-check-prerequisites).

### <a name="registration-of-hello-authentication-agent-failed-due-tootoken-or-account-authorization-errors"></a>Registratie van Hallo verificatie-Agent is mislukt vanwege tootoken of account autorisatie-fouten

Zorg ervoor dat u een cloudconfiguratie globale beheerdersaccount voor Azure AD Connect of zelfstandige verificatie-Agent-installatie en registratie-bewerkingen. Er is een bekend probleem met MFA ingeschakeld globale beheerdersaccounts; MFA tijdelijk (alleen toocomplete Hallo bewerkingen) uitschakelen als tijdelijke oplossing.

### <a name="an-unexpected-error-occurred"></a>Er is een onverwachte fout opgetreden

[Verzamelen van Logboeken van de agent](#collecting-pass-through-authentication-agent-logs) van Hallo-server en neem contact op met Microsoft Support met het probleem.

## <a name="authentication-agent-uninstallation-issues"></a>Verificatieproblemen Agent verwijderen

### <a name="warning-message-when-uninstalling-azure-ad-connect"></a>Waarschuwingsbericht tijdens het verwijderen van Azure AD Connect

Als u Pass-through-verificatie ingeschakeld op uw tenant zijn en u toouninstall Azure AD Connect probeert, ziet u Hallo volgende waarschuwing weergegeven: 'gebruikers zich niet kunnen toosign in tooAzure AD tenzij u andere agents Pass through-verificatie hebt geïnstalleerd op andere servers."

Zorg ervoor dat de instellingen van uw [hoge beschikbaar](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability) voordat u Azure AD Connect tooavoid op te splitsen gebruikersaanmelding verwijderen.

## <a name="issues-with-enabling-hello-feature"></a>Problemen met het Hallo-functie inschakelen

### <a name="enabling-hello-feature-failed-because-there-were-no-authentication-agents-available"></a>Hallo-functie kan niet worden ingeschakeld omdat er geen verificatie Agents beschikbaar

U toohave moet ten minste één actieve verificatie-Agent tooenable Pass through-verificatie op uw tenant. U kunt een verificatie-Agent installeren Azure AD Connect of een zelfstandige verificatie-Agent installeren.

### <a name="enabling-hello-feature-failed-due-tooblocked-ports"></a>Het inschakelen van de functie Hallo mislukt als gevolg van tooblocked poorten

Zorg ervoor dat Hallo-server waarop Azure AD Connect is geïnstalleerd kan communiceren met onze service-URL's en poorten die worden vermeld [hier](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-1-check-prerequisites).

### <a name="enabling-hello-feature-failed-due-tootoken-or-account-authorization-errors"></a>Het inschakelen van de functie Hallo mislukt als gevolg van tootoken of account autorisatie-fouten

Zorg ervoor dat u een cloudconfiguratie globale beheerdersaccount gebruiken wanneer u Hallo-functie inschakelen. Er is een bekend probleem met multi-factor authentication (MFA)-globale beheerdersaccounts; ingeschakeld MFA tijdelijk (alleen toocomplete Hallo bewerking) uitschakelen als tijdelijke oplossing.

## <a name="exchange-activesync-configuration-issues"></a>Problemen met Exchange ActiveSync-configuratie

Dit zijn Hallo veelvoorkomende problemen bij het configureren van Exchange ActiveSync-ondersteuning voor verificatie met Pass-through.

### <a name="exchange-powershell-issue"></a>Exchange PowerShell probleem

Als u Hallo ziet '**een parameter kan niet worden gevonden die overeenkomt met de naam van de 'PerTenantSwitchToESTSEnabled'\.**' Fout tijdens het uitvoeren van Hallo `Set-OrganizationConfig` Exchange PowerShell opdracht, neem contact op met Microsoft Support.

### <a name="exchange-activesync-not-working"></a>Exchange ActiveSync werkt niet

Hallo configuratie van kracht enige tijd tootake - Hallo periode is afhankelijk van uw omgeving. Neem contact op met Microsoft Support als Hallo situatie blijft bestaan gedurende een lange periode.

## <a name="collecting-pass-through-authentication-agent-logs"></a>Logboeken verzamelen Pass through-verificatie-Agent

Afhankelijk van het type Hallo van het probleem die wellicht hebt, moet u toolook op verschillende plaatsen voor logboeken Pass through-verificatie-Agent.

### <a name="authentication-agent-event-logs"></a>De gebeurtenislogboeken van de verificatie-Agent

Fouten gerelateerd toohello verificatie-Agent, opent u Hallo toepassing Logboeken op Hallo-server en controleer onder **toepassing en Service Logs\Microsoft\AzureAdConnect\AuthenticationAgent\Admin**.

Voor gedetailleerde analytics inschakelen Hallo ' ' sessielogboek. Hallo verificatie-Agent niet uitvoeren met dit logboek ingeschakeld tijdens normale bewerkingen. alleen gebruiken voor het oplossen van problemen. Hallo logboekinhoud zijn alleen zichtbaar nadat Hallo logboek weer is uitgeschakeld.

### <a name="detailed-trace-logs"></a>Gedetailleerde traceerlogboeken

tootroubleshoot gebruiker, mislukte aanmeldingen, zoekt u naar Logboeken met traceringen op **%programdata%\Microsoft\Azure AD Authentication Agent\Trace verbinding\\**. Deze logboeken bevatten redenen waarom een specifieke gebruiker aanmelden is mislukt met de functie voor Hallo Pass through-verificatie. Deze fouten zijn ook toegewezen toohello-Aanmeldingsfout redenen weergegeven in de voorgaande Hallo [tabel](#sign-in-failure-reasons-on-the-Azure-portal). Hier volgt een voorbeeld van invoer voor logboek:

```
    AzureADConnectAuthenticationAgentService.exe Error: 0 : Passthrough Authentication request failed. RequestId: 'df63f4a4-68b9-44ae-8d81-6ad2d844d84e'. Reason: '1328'.
        ThreadId=5
        DateTime=xxxx-xx-xxTxx:xx:xx.xxxxxxZ
```

U kunt beschrijvende details van Hallo-fout ('1328' in het voorgaande voorbeeld Hallo) ophalen door het openen van het Hallo-opdrachtprompt en actieve Hallo volgende opdracht (Opmerking: '1328' vervangen door Hallo foutnummer die u in uw logboeken ziet):

`Net helpmsg 1328`

![Pass-through-verificatie](./media/active-directory-aadconnect-pass-through-authentication/pta3.png)

### <a name="domain-controller-logs"></a>Registreert domeincontroller

Als logboekregistratie is ingeschakeld, als u meer informatie vindt u in de beveiligingslogboeken Hallo van uw domeincontrollers. Een eenvoudige manier tooquery aanmelden aanvragen dat is verzonden door Agents van Pass through-verificatie is als volgt:

```
    <QueryList>
    <Query Id="0" Path="Security">
    <Select Path="Security">*[EventData[Data[@Name='ProcessName'] and (Data='C:\Program Files\Microsoft Azure AD Connect Authentication Agent\AzureADConnectAuthenticationAgentService.exe')]]</Select>
    </Query>
    </QueryList>
```

### <a name="performance-monitor-counters"></a>Prestatiemeteritems

Een andere manier toomonitor verificatie Agents is tootrack specifieke prestatiemeteritems op elke server waarop Hallo verificatie-Agent is geïnstalleerd. Gebruik Hallo volgen algemene items (**# PTA verificaties**, **#PTA mislukt verificaties** en **#PTA geslaagde verificaties**) en fout-prestatiemeteritems (**Verificatiefouten # PTA**):

![Pass through-verificatie Prestatiemeter](./media/active-directory-aadconnect-pass-through-authentication/pta12.png)

>[!IMPORTANT]
>Pass through-verificatie biedt hoge beschikbaarheid met behulp van meerdere verificatie Agents en _niet_ taakverdeling. Afhankelijk van uw configuratie _niet_ alle verificatie-Agents ongeveer ontvangen _gelijk_ aantal aanvragen. Het is mogelijk dat een specifieke verificatie-Agent helemaal geen verkeer ontvangt.
