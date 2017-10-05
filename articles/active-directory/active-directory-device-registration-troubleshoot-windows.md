---
title: Het oplossen van de automatische registratie van Azure AD-domein aangesloten computers voor Windows 10 en Windows Server 2016 | Microsoft Docs
description: Het oplossen van de automatische registratie van Azure AD-domein lid zijn van computers voor Windows 10 en Windows Server 2016.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: cdc25576-37f2-4afb-a786-f59ba4c284c2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 5b7f95f302f716d9221b5fae59aa2df5c956a524
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-to-azure-ad--windows-10-and-windows-server-2016"></a>Het oplossen van automatische registratie van domein computers toegevoegd aan Azure AD. – Windows 10 en Windows Server 2016

In dit onderwerp is van toepassing op de volgende clients:

-   Windows 10
-   Windows Server 2016

Zie voor andere Windows-clients [probleemoplossing automatische registratie van domein aangesloten computers naar Azure AD voor Windows downlevel-clients](active-directory-device-registration-troubleshoot-windows-legacy.md).

Dit onderwerp wordt ervan uitgegaan dat u hebt geconfigureerd automatische registratie van apparaten domein vermelde in dat wordt beschreven in [automatische registratie van Windows-domein-apparaten met Azure Active Directory configureren](active-directory-device-registration-get-started.md) ter ondersteuning van de volgende scenario's:

- [Voorwaardelijke toegang op basis van apparaten](active-directory-conditional-access-automatic-device-registration-setup.md)

- [Enterprise-instellingen voor roaming](active-directory-windows-enterprise-state-roaming-overview.md)

- [Windows Hello voor Bedrijven](active-directory-azureadjoin-passport-deployment.md)


Dit document bevat richtlijnen voor probleemoplossing over de mogelijke problemen kunt oplossen. 

De registratie wordt ondersteund in de Windows Update 10 November 2015 en hoger.  
U wordt aangeraden de Update Verjaardag gebruiken voor het inschakelen van de bovenstaande scenario's.

## <a name="step-1-retrieve-the-registration-status"></a>Stap 1: De registratiestatus ophalen 

**De registratiestatus ophalen:**

1. Open de opdrachtprompt als beheerder.

2. Type **dsregcmd/status**



    +----------------------------------------------------------------------+
   | Apparaatstatus |+----------------------------------------------------------------------+
    
        AzureAdJoined : YES
     EnterpriseJoined: Geen apparaat-id: 5820fbe9-60c8-43b0-bb11-44aee233e4e7 vingerafdruk: B753A6679CE720451921302CA873794D94C6204A KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider: Microsoft Platform Crypto-Provider TpmProtected: Ja KeySignTest:: moet worden uitgevoerd met verhoogde bevoegdheden te testen.
                  IDP: login.windows.net TenantId: 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName: Contoso AuthCodeUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl: https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl: https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl: https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl: eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ == JoinSrvVersion: 1.0 JoinSrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId: urn: ms-drs:enterpriseregistration.windows.net KeySrvVersion: 1.0 KeySrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId: urn: ms-drs:enterpriseregistration.windows.net DomainJoined: Ja DomainName: CONTOSO
    
    +----------------------------------------------------------------------+
   | Gebruikersstatus |+----------------------------------------------------------------------+
    
                 NgcSet : YES
               NgcKeyId : {C7A9AEDC-780E-4FDA-B200-1AE15561A46B}
        WorkplaceJoined : NO
          WamDefaultSet : YES
    WamDefaultAuthority: organisaties WamDefaultId: https://login.microsoft.com WamDefaultGUID: {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd) AzureAdPrt: Ja



## <a name="step-2-evaluate-the-registration-status"></a>Stap 2: De registratiestatus van de 

Bekijk de volgende velden en zorg ervoor dat ze de verwachte waarden hebben:

### <a name="azureadjoined--yes"></a>AzureAdJoined: Ja  

Dit veld geeft aan of het apparaat is geregistreerd bij Azure AD. Als de waarde wordt weergegeven als 'Nee', worden de registratie is niet voltooid. 

**Mogelijke oorzaken:**

- Verificatie van de computer voor de registratie is mislukt.

- Er is een HTTP-proxy in de organisatie die door de computer kan niet worden gedetecteerd

- De computer kan niet aangemeld bij Azure AD voor de verificatie of Azure DRS voor registratie

- De computer mogelijk niet op het interne netwerk van de organisatie of VPN-met direct zicht regel met een on-premises AD-domeincontroller.

- Als de computer een TPM heeft, wordt in een verkeerde status.

- Er is mogelijk een onjuiste configuratie van services eerder hebt genoteerd in het document dat moet u opnieuw te verifiëren. Algemene voorbeelden zijn:

    - De federatieserver is geen WS-Trust-eindpunten die zijn ingeschakeld

    - De federatieserver mogelijk niet toegestaan voor binnenkomende verificatie vanaf computers in uw netwerk met behulp van geïntegreerde Windows-verificatie.

    - Er is geen object van het Service Connection Point die verwijst naar de domeinnaam van uw geverifieerde in Azure AD in de AD-forest waar de computer deel uitmaakt

---

### <a name="domainjoined--yes"></a>DomainJoined: Ja  

Dit veld wordt aangegeven of het apparaat is verbonden met een lokale Active Directory of niet. Als de waarde wordt weergegeven als **Nee**, het apparaat niet automatisch kan registreren met Azure AD. Controleer eerst het apparaat lid wordt aan de lokale Active Directory, voordat u deze kunt registreren met Azure AD. Als u de computer lid te worden naar Azure AD rechtstreeks zoekt, gaat u naar meer informatie over de mogelijkheden van Azure Active Directory Join.

---

### <a name="workplacejoined--no"></a>WorkplaceJoined: Nee  

Dit veld geeft aan of het apparaat is geregistreerd met Azure AD, maar als een persoonlijk apparaat (gemarkeerd als 'Workplace Joined'). Als deze waarde moet worden weergegeven als 'Nee' voor een domeincomputer geregistreerd in Azure AD, maar als deze wordt weergegeven als Ja betekent dit dat een account voor werk of school voordat de computer die ooit is toegevoegd. In dit geval wordt het account genegeerd als de verjaardag Update versie van Windows 10 (1607 wanneer de WinVer uitgevoerd opdracht in het venster 'Uitvoeren' of een opdrachtprompt).

---

### <a name="wamdefaultset--yes-and-azureadprt--yes"></a>WamDefaultSet: Ja en AzureADPrt: Ja
  
Deze velden weergeven dat de gebruiker heeft geverifieerd naar Azure AD bij het aanmelden bij het apparaat. Als u 'Nee' weergeven ze dat de volgende oorzaken hebben:

- Ongeldige opslagsleutel (BEURS) in de TPM die zijn gekoppeld aan het apparaat na inschrijving (Controleer de KeySignTest tijdens de uitvoering van verhoogde).

- Alternatieve aanmeldings-ID

- HTTP-Proxy is niet gevonden

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie de [automatische apparaatregistratie Veelgestelde vragen](active-directory-device-registration-faq.md) 