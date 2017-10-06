---
title: aaaApplications en browsers die gebruikmaken van regels voor voorwaardelijke toegang in Azure Active Directory | Microsoft Docs
description: Met voorwaardelijk toegangsbeheer controleert de Azure Active Directory voor specifieke condities wanneer het Hallo-gebruiker en toegang tot de toepassing van tooallow verifieert.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 62349fba-3cc0-4ab5-babe-372b3389eff6
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: ca20853bb9f4b22d0b88ddd2f051d658e0d88cf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="applications-and-browsers-that-use-conditional-access-rules-in-azure-active-directory"></a>Toepassingen en browsers die gebruikmaken van regels voor voorwaardelijke toegang in Azure Active Directory

Regels voor voorwaardelijke toegang worden ondersteund in Azure Active Directory (Azure AD)-verbonden toepassingen, vooraf geïntegreerde federatieve software als een dienst (SaaS)-toepassingen, toepassingen die gebruikmaken van wachtwoord eenmalige aanmelding (SSO), line-of-business-toepassingen en toepassingen die gebruikmaken van Azure AD-toepassingsproxy. Zie voor een gedetailleerde lijst met toepassingen waarvoor u voorwaardelijke toegang kunt gebruiken, [Services met voorwaardelijke toegang ingeschakeld](active-directory-conditional-access-technical-reference.md). Voorwaardelijke toegang werkt zowel met mobiele en bureaublad-toepassingen die moderne authenticatie gebruiken. In dit artikel wordt uitgelegd hoe voorwaardelijke toegang werkt in mobiele en bureaublad-apps.

U kunt Azure AD aanmeldingspagina's in toepassingen die gebruikmaken van moderne verificatie gebruiken. Een gebruiker wordt gevraagd met een aanmeldingspagina voor multi-factor authentication. Een bericht weergegeven als Hallo gebruikerstoegang is geblokkeerd. Moderne verificatie is vereist voor Hallo apparaat tooauthenticate in Azure AD, zodat het beleid voor voorwaardelijke toegang op basis van het apparaat worden geëvalueerd.

Het is belangrijk tooknow welke toepassingen kunnen regels voor voorwaardelijke toegang gebruiken en stappen die u nodig tootake toosecure andere toegangspunten toepassing hebt mogelijk hello.

## <a name="applications-that-use-modern-authentication"></a>Toepassingen die gebruikmaken van moderne verificatie
> [!NOTE]
> Als u een beleid voor voorwaardelijke toegang in Azure AD met een gelijkwaardige in Office 365 hebt, configureert u beide beleidsregels voor voorwaardelijke toegang. Deze toepassing zou zijn, bijvoorbeeld tooconditional-toegangsbeleid voor Exchange Online of SharePoint Online.
>
>

Hallo volgende toepassingen ondersteuning bieden voor voorwaardelijke toegang voor Office 365 en andere toepassingen Azure AD-connected-service:


| Target-Service| Platform| Toepassing |
| --- | --- | --- |
| Alle services van de app mijn Apps| Android en iOS| Beleid voor apps MFA en locatie. Apparaten op basis van beleid worden niet ondersteund.|
| Azure RemoteApp-service| Windows 10, Windows 8.1, Windows 7, iOS, Android en Mac OS X| Azure RemoteApp|
| Dynamics CRM| Windows 10, Windows 8.1, Windows 7, iOS en Android| Dynamics CRM-app|
| Microsoft Teams| Windows 10, Windows 8.1, Windows 7, iOS/Android- en MAC OS x| Services van Microsoft-Teams - Hiermee bepaalt u alle services die ondersteuning bieden voor Microsoft-Teams en alle bijbehorende Client-Apps - bureaublad van Windows, MAC OS X, iOS, Android, WP en webclient|
| Office 365 Exchange Online| Windows 10| Agenda-mail/mensen app, Outlook 2016, Outlook 2013 (met moderne verificatie), Skype voor bedrijven (met moderne verificatie)|
| Office 365 Exchange Online| Windows 8.1, Windows 7| Outlook 2016, Outlook 2013 (met moderne verificatie), Skype voor bedrijven (met moderne verificatie)|
| Office 365 Exchange Online| iOS| Mobiele app voor Outlook|
| Office 365 Exchange Online| Mac OS X| Outlook 2016 (Office voor Mac OS)|
| Office 365 SharePoint Online| Windows 10| Apps van Office 2016, Office Universal-apps, Office 2013 (met moderne verificatie), OneDrive sync-client (Zie [notities](https://support.office.com/en-US/article/Azure-Active-Directory-conditional-access-with-the-OneDrive-sync-client-on-Windows-028d73d7-4b86-4ee0-8fb7-9a209434b04e)), Office-groepen ondersteuning is gepland voor toekomstige hello, ondersteuning voor SharePoint-app gepland voor toekomstige Hallo|
| Office 365 SharePoint Online| Windows 8.1, Windows 7| Apps van Office 2016, Office 2013 (met moderne verificatie), OneDrive synchroniseren client (Zie [notities](https://support.office.com/en-US/article/Azure-Active-Directory-conditional-access-with-the-OneDrive-sync-client-on-Windows-028d73d7-4b86-4ee0-8fb7-9a209434b04e))|
| Office 365 SharePoint Online| voor iOS, Android| Office mobile-apps|
| Office 365 SharePoint Online| Mac OS X| Office 2016 voor Mac OS (Word, Excel, PowerPoint, OneNote alleen). OneDrive voor bedrijven ondersteuning voor toekomstige Hallo gepland|
| Office 365 Yammer| Windows 10, iOS, Android| De app Yammer Office|
| Power BI-service| Windows 10, Windows 8.1, Windows 7 en iOS| Power BI-app. Hallo Power BI-app voor Android biedt momenteel geen ondersteuning voor voorwaardelijke toegang op basis van apparaten.|
| Visual Studio Team Services| Windows 10, Windows 8.1, Windows 7, iOS en Android| Visual Studio Team Services-app|








## <a name="applications-that-do-not-use-modern-authentication"></a>Toepassingen die geen van moderne verificatie gebruikmaken
Op dit moment moet u andere methoden tooblock toegang tooapps die geen van moderne verificatie gebruikmaken gebruiken. Toegangsregels voor apps die moderne verificatie niet gebruikt worden niet afgedwongen door voorwaardelijke toegang. Dit is vooral overweging voor toegang tot Exchange en SharePoint. De meeste eerdere versies van apps oudere access control protocollen gebruiken.

### <a name="control-access-in-office-365-sharepoint-online"></a>Toegang beheren in Office 365 SharePoint Online
U kunt de verouderde protocollen voor toegang tot SharePoint uitschakelen met behulp van de cmdlet Set-SPOTenant Hallo. Gebruik deze cmdlet tooprevent Office-clients die gebruikmaken van niet-moderne verificatieprotocollen toegang tot SharePoint Online-bronnen.

**Voorbeeldopdracht**:`Set-SPOTenant -LegacyAuthProtocolsEnabled $false`

### <a name="control-access-in-office-365-exchange-online"></a>Toegang beheren in Office 365 Exchange Online
Exchange biedt twee hoofdcategorieën van protocollen. Hallo volgend opties voor het controleren en selecteer vervolgens Hallo-beleid dat geschikt is voor uw organisatie.

* **Exchange ActiveSync**. Standaard worden de beleidsregels voor voorwaardelijke toegang voor multi-factor authentication-server en de locatie niet afgedwongen voor Exchange ActiveSync. U moet tooprotect toegang toothese services door het configureren van Exchange ActiveSync-beleid rechtstreeks of door Exchange ActiveSync worden geblokkeerd via regels voor Active Directory Federation Services (AD FS).
* **Verouderde protocollen**. U kunt de verouderde protocollen met AD FS blokkeren. Dit voorkomt dat toegang tooolder Office-clients, zoals Office 2013 zonder moderne verificatie is ingeschakeld en eerdere versies van Office.

### <a name="use-ad-fs-tooblock-legacy-protocol"></a>AD FS tooblock legacy-protocol gebruiken
U kunt Hallo voorbeeld uitgifte autorisatie regels tooblock verouderde protocol toegang op Hallo AD FS-niveau te volgen. Kiezen uit twee algemene configuraties.

#### <a name="option-1-allow-exchange-activesync-and-allow-legacy-apps-but-only-on-hello-intranet"></a>Optie 1: Toestaan van Exchange ActiveSync en oudere apps, maar alleen op Hallo intranet toestaan
Door toe te passen Hallo na drie regels toohello AD FS relying party trust voor Microsoft Office 365-Identiteitsplatform, Exchange ActiveSync-verkeer en browser en moderne verificatieverkeer, toegang hebben. Hallo extranet worden oudere apps geblokkeerd.

##### <a name="rule-1"></a>Regel 1
    @RuleName = "Allow all intranet traffic"
    c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "true"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");

##### <a name="rule-2"></a>Regel 2
    @RuleName = "Allow Exchange ActiveSync"
    c1:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application", Value == "Microsoft.Exchange.ActiveSync"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");

##### <a name="rule-3"></a>Regel 3
    @RuleName = "Allow extranet browser and browser dialog traffic"
    c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] &&
    c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value =~ "(/adfs/ls)|(/adfs/oauth2)"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");

#### <a name="option-2-allow-exchange-activesync-and-block-legacy-apps"></a>Optie 2: Exchange ActiveSync toestaan en blokkeren van verouderde apps
Door toe te passen Hallo na drie regels toohello AD FS relying party trust voor Microsoft Office 365-Identiteitsplatform, Exchange ActiveSync-verkeer en browser en moderne verificatieverkeer, toegang hebben. Verouderde apps worden geblokkeerd vanaf elke locatie.

##### <a name="rule-1"></a>Regel 1
    @RuleName = "Allow all intranet traffic only for browser and modern authentication clients"
    c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "true"] &&
    c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value =~ "(/adfs/ls)|(/adfs/oauth2)"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");


##### <a name="rule-2"></a>Regel 2
    @RuleName = "Allow Exchange ActiveSync"
    c1:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application", Value == "Microsoft.Exchange.ActiveSync"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");


##### <a name="rule-3"></a>Regel 3
    @RuleName = "Allow extranet browser and browser dialog traffic"
    c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] &&
    c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value =~ "(/adfs/ls)|(/adfs/oauth2)"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");


## <a name="supported-browsers-for-device-based-policies"></a>Ondersteunde browsers voor apparaten op basis van beleid 

Alleen krijgt u toegang voor apparaten op basis van beleid dat controleren voor apparaatcompatibiliteit en -domein bij Azure AD kunt identificeren en Hallo apparaat verifiëren. Tijdens het meeste controles, zoals de locatie en werk op de meeste apparaten en browsers, MFA verplicht apparaatbeleid Hallo OS-versie en browsers die hieronder worden vermeld. Toegang wordt geblokkeerd voor gebruikers op niet-ondersteunde browser of Hallo-besturingssystemen wanneer een apparaatbeleid geïmplementeerd is. 

| OS                     | Browsers                 | Ondersteuning     |
| :--                    | :--                      | :-:         |
| Windows 10                 | IE, rand                 | ![Selecteren][1] |
| Windows 10                 | Chrome                   | Preview     |
| 8 Win / 8.1            | IE, Chrome               | ![Selecteren][1] |
| Win 7                  | IE, Chrome               | ![Selecteren][1] |
| iOS                    | Safari                   | ![Selecteren][1] |
| Android                | Chrome                   | ![Selecteren][1] |
| Windows Phone          | IE, rand                 | ![Selecteren][1] |
| Windows Server 2016    | IE, rand                 | ![Selecteren][1] |
| Windows Server 2016    | Chrome                   | Binnenkort beschikbaar |
| Windows Server 2012 R2 | IE, Chrome               | ![Selecteren][1] |
| Windows Server 2008 R2 | IE, Chrome               | ![Selecteren][1] |
| Mac OS                 | Safari                   | ![Selecteren][1] |
| Mac OS                 | Chrome                   | Binnenkort beschikbaar |

> [!NOTE]
> Voor ondersteuning van Chrome, moet u Windows 10 auteurs Update en installeer Hallo extensie gevonden [hier](https://chrome.google.com/webstore/detail/windows-10-accounts/ppnbnpeolgkicgegkbkbjmhlideopiji).
>
>

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie [voorwaardelijke toegang in Azure Active Directory](active-directory-conditional-access.md)




<!--Image references-->
[1]: ./media/active-directory-conditional-access-supported-apps/ic195031.png


