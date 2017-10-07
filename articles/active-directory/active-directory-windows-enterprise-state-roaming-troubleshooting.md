---
title: Het oplossen van Enterprise State Roaming instellingen in Azure Active Directory | Microsoft Docs
description: Biedt antwoorden toosome vragen IT-beheerders wellicht over de instellingen en synchroniseren van app-gegevens.
services: active-directory
keywords: Enterprise state roaming instellingen windows cloud, veelgestelde vragen op enterprise state roaming
documentationcenter: 
author: tanning
manager: swadhwa
editor: 
ms.assetid: f45d0515-99f7-42ad-94d8-307bc0d07be5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: markvi
ms.openlocfilehash: 4636d016983426e30d696459f54167b8ad2babcd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
#<a name="troubleshooting-enterprise-state-roaming-settings-in-azure-active-directory"></a>Enterprise State Roaming instellingen voor probleemoplossing in Azure Active Directory

In dit onderwerp bevat informatie over het tootroubleshoot en onderzoeken van problemen met Enterprise State Roaming en bevat een lijst met bekende problemen.

## <a name="preliminary-steps-for-troubleshooting"></a>Voorbereidende stappen voor probleemoplossing 
Verifieer dat Hallo gebruiker en apparaat goed is geconfigureerd en dat alle Hallo vereisten van Enterprise State Roaming door Hallo apparaat- en hello wordt voldaan voordat u begint met het oplossen van problemen. 

1. Windows 10, met de meest recente updates hello, en een minimale versie 1511 (Build van 10586 of hoger) is geïnstalleerd op Hallo-apparaat. 
2. Hallo-apparaat is Azure AD zijn toegevoegd, of het domein en geregistreerd in Azure AD.
3. In de Azure Active Directory-portal Hallo **Enterprise State Roaming** is ingeschakeld voor de map Hallo onder **configureren** > **apparaten**  >  **Gebruikers kunnen instellingen en Enterprise-App-gegevens synchroniseren**. Alle gebruikers zijn geselecteerd, of Hallo gebruiker is ingeschakeld voor het synchroniseren met behulp van de optie Hallo geselecteerd en in de beveiligingsgroep Hallo opgenomen.
4. Hallo gebruiker heeft een Azure Active Directory Premium-abonnement toothem toegewezen.  
5. Hallo-apparaat is opnieuw opgestart en Hallo gebruiker is aangemeld nadat Enterprise State Roaming is ingeschakeld.

## <a name="information-tooinclude-when-you-need-help"></a>Informatie tooinclude wanneer u hulp nodig hebt
Als u niet op uw probleem met de Hallo richtlijnen hieronder oplossen kunt, kunt u contact opnemen met onze ondersteuningsmedewerkers. Wanneer u contact opneemt met ze, wordt het aanbevolen tooinclude Hallo volgende informatie:

- **Algemene beschrijving van de fout Hallo** – zijn er foutberichten gezien door de gebruiker Hallo? Als er geen foutbericht is, beschrijven Hallo onverwacht gedrag, beschreven opgemerkt. Welke functies zijn ingeschakeld voor synchronisatie en wat is Hallo gebruiker toosync verwacht? Meerdere functies niet synchroniseert of it geïsoleerd tooone is?
- **Betrokken gebruikers** – sync Is werkende/mislukt voor een of meer gebruikers? Het aantal apparaten per gebruiker betrokken zijn? Zijn ze niet synchroniseert alle of enkele ervan synchroniseren en sommige niet synchroniseren?
- **Informatie over Hallo gebruiker** – welke identiteit Hallo-gebruiker met toolog in toohello apparaat is? Hoe wordt Hallo gebruiker aangemeld toohello apparaat? Zijn ze deel uitmaken van een geselecteerde beveiligingsgroep toosync toegestaan? 
- **Informatie over Hallo apparaat** : dit apparaat Azure AD join of het domein? Welke build is Hallo apparaat op? Wat zijn de meest recente updates Hallo?
- **Datum / tijd / tijdzone** – wat is Hallo nauwkeurige datum en tijd die u hebt gezien Hallo-fout (inclusief Hallo tijdzone)?
- Met inbegrip van deze informatie helpt ons zo snel mogelijk het probleem kunt oplossen.

## <a name="troubleshooting-and-diagnosing-issues"></a>Het oplossen van problemen en het onderzoeken van problemen
Deze sectie vindt u suggesties over het tootroubleshoot en onderzoeken van problemen gerelateerde tooEnterprise State Roaming.

## <a name="verify-sync-and-hello-sync-your-settings-settings-page"></a>Controleer of de synchronisatie en instellingenpagina 'Uw instellingen synchroniseren' Hallo 

1. Domein dat is geconfigureerd na toevoeging aan uw Windows 10-PC-tooa tooallow Enterprise State Roaming, meld u aan met uw werkaccount. Ga te**instellingen** > **Accounts** > **uw synchronisatie-instellingen** en controleer of de synchronisatie en Hallo afzonderlijke instellingen op, en die boven Hallo van Hallo instellingenpagina geeft aan dat u met uw werkaccount synchroniseert. Hallo hetzelfde account wordt ook gebruikt als uw aanmeldingsaccount in bevestigen **instellingen** > **Accounts** > **uw Info**. 
2. Controleer of de synchronisatie door sommige wijzigingen op de oorspronkelijke computer hello, zoals het verplaatsen van Hallo taakbalk toohello of bovenste rechts van welkomstscherm werkt over meerdere machines. Bekijkt hello wijziging toohello tweede machine doorgegeven binnen vijf minuten. 
 - Welkomstscherm vergrendelen en ontgrendelen (Win + L) kunt u een synchronisatie activeren.
 - Moet u hetzelfde aanmeldingsaccount op beide computers voor synchronisatie toowork – Hallo Enterprise State Roaming is gebonden toohello gebruikersaccount en niet Hallo computeraccount.

**Potentiële probleem**: Hallo instellingenpagina heeft Hallo Schakelknoppen lichter gekleurd weergegeven en in plaats van een account te zien, ziet u Hallo tekst 'enkele Windows-onderdelen zijn alleen beschikbaar als u een Microsoft-account of werkaccount'. Dit probleem kan zich voordoen voor apparaten die zijn ingesteld toobe domein- en tooAzure AD geregistreerd, maar Hallo apparaat tooAzure AD niet is geverifieerd. Een mogelijke oorzaak is dat het apparaatbeleid Hallo moet worden toegepast, maar deze toepassing verloopt asynchroon en een paar uur vertraging kan optreden. Dit probleem, volg de stappen Hallo in controleren tooverify Hallo apparaat registratie status toocheck als dit Hallo geval.

### <a name="verify-hello-device-registration-status"></a>Hallo apparaat registratiestatus controleren
Enterprise State Roaming vereist Hallo apparaat toobe geregistreerd in Azure AD. Hoewel niet specifiek tooEnterprise State Roaming Hallo onderstaande instructies, kunt u controleren dat Hallo Windows 10-Client is geregistreerd, en status van de vingerafdruk van instellingen voor de URL van Azure AD, NGC en andere informatie.

1.  Open Hallo-opdrachtprompt verlaagde bevoegdheden. toodo open dit in Windows hello uitvoeren starten (Win + R) en typ 'cmd' tooopen.
2.  Zodra het Hallo-opdrachtprompt is geopend, typt u "*dsregcmd.exe/status*'.
3.  Voor de verwachte uitvoer Hallo **AzureAdJoined** veldwaarde moet 'Ja' **WamDefaultSet** veldwaarde moet worden 'Ja' en Hallo **WamDefaultGUID** veldwaarde moet een GUID met '(AzureAd)' hello achter.

**Potentiële probleem**: **WamDefaultSet** en **AzureAdJoined** zowel "Nee" hebben in de waarde van veld Hallo Hallo-apparaat is lid van een domein en geregistreerd bij Azure AD en Hallo-apparaat wordt niet gesynchroniseerd. Als het dit weergegeven wordt, Hallo apparaat mogelijk toowait voor beleid toobe toegepast of Hallo-verificatie voor Hallo-apparaat is mislukt bij het verbinden van tooAzure AD. Hallo gebruiker wellicht toowait enkele uren Hallo beleid toobe toegepast. Andere stappen voor probleemoplossing, omvat mogelijk opnieuw uit te voeren automatische registratie door ondertekening uit en weer in of startende Hallo taak in de Taakplanner. In sommige gevallen kan met '*dsregcmd.exe /leave*' in een opdrachtpromptvenster, opnieuw opstarten en het opnieuw proberen registratie kunnen dit probleem oplossen.


**Potentiële probleem**: Hallo veld voor **AzureAdSettingsUrl** is leeg en hello apparaat is komt niet synchroniseren. Hallo gebruiker mag hebben laatst heeft aangemeld toohello apparaat voordat Enterprise State Roaming is ingeschakeld in Azure Active Hallo Directory-Portal. Hallo-apparaat opnieuw opstarten en Hallo gebruikersaanmelding hebben. Probeer eventueel Hallo IT-beheerder uitschakelen en gebruikers kunnen synchronisatie-instellingen en Enterprise-App-gegevens opnieuw in te schakelen met in Hallo-portal. Zodra weer wordt ingeschakeld, opnieuw opstarten Hallo apparaat en Hallo gebruikersaanmelding hebben. Als dit niet wordt opgelost probleem hello, **AzureAdSettingsUrl** mag niet leeg zijn in geval van een certificaat met onjuiste apparaat Hallo. In dit geval wordt uitgevoerd '*dsregcmd.exe /leave*' in een opdrachtpromptvenster, opnieuw opstarten en het opnieuw proberen registratie kunnen dit probleem oplossen.

## <a name="enterprise-state-roaming-and-multi-factor-authentication"></a>Enterprise State Roaming en meervoudige verificatie 
Onder bepaalde omstandigheden kunnen Enterprise State Roaming mislukken toosync gegevens als Azure multi-factor Authentication is geconfigureerd. Zie voor meer informatie over deze problemen ondersteuningsdocument Hallo [KB3193683](https://support.microsoft.com/kb/3193683). 

**Potentiële probleem**: als het apparaat geconfigureerde toorequire multi-factor Authentication op Hallo Azure Active Directory-beheerportal is, u toosync instellingen mislukken tijdens het aanmelden met een wachtwoord tooa Windows 10-apparaat. Dit type configuratie van multi-factor Authentication is beoogde tooprotect Azure administrator-account. Beheerder gebruikers mogelijk nog steeds kunnen toosync door zich tootheir Windows 10-apparaten met hun Microsoft Passport voor Work PINCODE of door multi-factor Authentication in te voeren bij het openen van andere Azure-services zoals Office 365.

**Potentiële probleem**: synchronisatie kan mislukken als Hallo beheerder configureert u beleid voor voorwaardelijke toegang van Hallo Active Directory Federation Services multi-factor Authentication en het Hallo-toegangstoken op Hallo-apparaat is verlopen. Zorg ervoor dat u aanmelden en afmelden met behulp van Hallo Microsoft Passport voor Work PINCODE of multi-factor Authentication voltooid tijdens het openen van andere Azure-services zoals Office 365.

###<a name="event-viewer"></a>Logboeken
Voor geavanceerde probleemoplossing, kan de Event Viewer gebruikte toofind specifieke fouten zijn. Deze worden beschreven in de onderstaande tabel voor Hallo. Hallo-gebeurtenissen kunnen u vinden onder Logboeken > Logboeken toepassingen en Services > **Microsoft** > **Windows** > **SettingSync** en voor problemen met het synchroniseren van identiteitsgerelateerde **Microsoft** > **Windows** > **Azure AD**.


## <a name="known-issues"></a>Bekende problemen

### <a name="sync-does-not-work-on-devices-that-have-apps-side-loaded-using-mdm-software"></a>Synchronisatie werkt niet op apparaten met apps ' side-loaded met behulp van de MDM-software

Is van invloed op apparaten met Hallo Windows 10 Verjaardag Update (versie 1607). Hallo gebeurtenis-ID 6013 met fout 80070259 is vaak zichtbaar in Logboeken onder logboeken van Hallo SettingSync Azure.

**Aanbevolen actie**  
Zorg ervoor dat Windows 10 Hallo v1607 client Hallo 23 augustus 2016 cumulatieve Update ([KB3176934](https://support.microsoft.com/kb/3176934) OS bouwen 14393.82). 

---

### <a name="internet-explorer-favorites-do-not-sync"></a>Favorieten in Internet Explorer synchroniseert geen

Is van invloed op apparaten met Hallo Windows 10 November Update (versie 1511).

**Aanbevolen actie**  
Zorg ervoor dat Windows 10 Hallo v1511 client Hallo juli 2016 cumulatieve Update ([KB3172985](https://support.microsoft.com/kb/3172985) OS bouwen 10586.494).

---

### <a name="theme-is-not-syncing-as-well-as-data-protected-with-windows-information-protection"></a>Thema synchroniseert niet, evenals gegevens die worden beveiligd met Windows Information Protection 

tooprevent gegevenslekken van gegevens die worden beveiligd met [Windows Information Protection](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-wip) wordt niet meer gesynchroniseerd tot en met Enterprise State Roaming voor apparaten met Windows 10 Verjaardag Update Hallo.



**Aanbevolen actie**  
Geen. Dit probleem mogelijk worden opgelost door tooWindows toekomstige updates.

---

### <a name="date-time-and-region-settings-do-not-sync-on-domain-joined-device"></a>Instellingen voor datum, tijd en regio Synchroniseer niet op domein-apparaat 
  
Apparaten die lid zijn van een domein niet krijgen met synchronisatie voor Hallo datum, tijd en regio instellen: automatische tijd. Met automatische tijd kan onderdrukking Hallo andere instellingen voor datum, tijd en de regio en ervoor zorgen dat deze instellingen niet toosync. 

**Aanbevolen actie**  
Geen. 

---

### <a name="uac-prompts-when-syncing-passwords"></a>UAC wordt gevraagd wanneer wachtwoorden synchroniseren

Is van invloed op apparaten met Hallo Windows 10 November Update (versie 1511) met een draadloze NIC die is geconfigureerd toosync wachtwoorden.

**Aanbevolen actie**  
Zorg ervoor dat Windows 10 Hallo v1511 client Hallo cumulatieve Update ([KB3140743](https://support.microsoft.com/kb/3140743) OS bouwen 10586.494).

---

### <a name="sync-does-not-work-on-devices-that-use-smart-card-for-login"></a>Synchronisatie werkt niet op apparaten die gebruikmaken van de smartcard voor aanmelding
Als u toosign in tooyour Windows-apparaat met een smartcard of virtuele smartcard probeert, zal instellingen synchroniseren niet meer werken.     

**Aanbevolen actie**  
Geen. Dit probleem mogelijk worden opgelost door tooWindows toekomstige updates.

---

### <a name="domain-joined-device-is-not-syncing-after-leaving-corporate-network"></a>Domein-apparaat wordt niet gesynchroniseerd na het verlaten van bedrijfsnetwerk     
Domein apparaten geregistreerd tooAzure die AD synchronisatiefout optreden kan als Hallo-apparaat externe voor langere tijd en domeinverificatie kan niet worden voltooid.

**Aanbevolen actie**  
Verbinding maken met Hallo apparaat tooa bedrijfsnetwerk zodat de synchronisatie kan worden hervat.

---

 ### <a name="azure-ad-joined-device-is-not-syncing-and-hello-user-has-a-mixed-case-user-principal-name"></a>Azure AD join-apparaat niet wordt gesynchroniseerd en Hallo gebruiker heeft een gemengde case User Principal-naam.
 Als Hallo gebruiker een gemengde aanvraag UPN (bv UserName in plaats van de gebruikersnaam heeft) en Hallo gebruiker zich op een Azure AD join-apparaat dat is bijgewerkt van Windows 10-Build 10586 too14393, mislukken Hallo gebruikersapparaat toosync. 

**Aanbevolen actie**  
Hallo gebruiker toounjoin nodig hebt en Hallo apparaat toohello cloud weer. toodo deze, meld u aan als gebruiker van de lokale beheerder Hallo en loskoppelen van Hallo apparaat door te gaan**instellingen** > **System** > **over** en selecteer ' Beheer of Verbreek de verbinding tussen werk of school'. Opruimen van de onderstaande Hallo-bestanden en Azure AD Join Hallo apparaat opnieuw in **instellingen** > **System** > **over** en 'verbinden te selecteren tooWork of op School'. Doorgaan toojoin Hallo apparaat tooAzure Active Directory en volledige Hallo-stroom.

In Hallo opruimen, opruimen Hallo volgende bestanden:
- Settings.dat in`C:\Users\<Username>\AppData\Local\Packages\Microsoft.AAD.BrokerPlugin_cw5n1h2txyewy\Settings\`
- Alle Hallo bestanden onder de map Hallo`C:\Users\<Username>\AppData\Local\Packages\Microsoft.AAD.BrokerPlugin_cw5n1h2txyewy\AC\TokenBroker\Account`

---

### <a name="event-id-6065-80070533-this-user-cant-sign-in-because-this-account-is-currently-disabled"></a>Gebeurtenis-ID 6065:80070533 die deze gebruiker zich niet aanmelden omdat dit account is momenteel uitgeschakeld.  
In Logboeken onder Hallo SettingSync/Debug Logboeken, deze fout ziet wanneer de referenties van gebruiker Hallo zijn verlopen. Het kan ook optreden wanneer Hallo tenant automatisch geen AzureRMS ingericht. 

**Aanbevolen actie**  
In het eerste geval hello, hebben hun referenties en aanmelding toohello apparaat bijwerken met de nieuwe referenties Hallo Hallo-gebruiker. toosolve hello AzureRMS probleem, doorgaan met de Hallo stappen in [KB3193791](https://support.microsoft.com/kb/3193791). 

---

### <a name="event-id-1098-error-0xcaa5001c-token-broker-operation-failed"></a>Gebeurtenis-ID 1098: Fout: 0xCAA5001C Token broker-bewerking is mislukt  
In Logboeken onder Hallo AAD/operationeel voor Logboeken, deze fout kan worden gezien met gebeurtenis 1104: aanroep van de invoegtoepassing AAD Cloud Azië Get-token heeft een fout geretourneerd: 0xC000005F. Dit probleem treedt op als er machtigingen of mist eigendom kenmerken.    

**Aanbevolen actie**  
Doorgaan met de Hallo hier vermelde stappen [KB3196528](https://support.microsoft.com/kb/3196528).  



## <a name="next-steps"></a>Volgende stappen

- Gebruik Hallo [User Voice-forum](https://feedback.azure.com/forums/169401-azure-active-directory/category/158658-enterprise-state-roaming) tooprovide feedback en maak suggesties over hoe tooimprove Enterprise State Roaming.

- Zie voor meer informatie, Hallo [Enterprise State Roaming overzicht](active-directory-windows-enterprise-state-roaming-overview.md). 

## <a name="related-topics"></a>Verwante onderwerpen
* [Overzicht van zwervende Enterprise](active-directory-windows-enterprise-state-roaming-overview.md)
* [Enterprise-status roaming in Azure Active Directory inschakelen](active-directory-windows-enterprise-state-roaming-enable.md)
* [Instellingen en veelgestelde vragen voor dataroaming](active-directory-windows-enterprise-state-roaming-faqs.md)
* [Groep beleid en de MDM-instellingen voor synchronisatie van instellingen](active-directory-windows-enterprise-state-roaming-group-policy-settings.md)
* [Windows 10 zwervende naslaginformatie](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md)
