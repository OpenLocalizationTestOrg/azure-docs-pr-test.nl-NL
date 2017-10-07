---
title: aaaTroubleshooting hybride Azure Active Directory die lid zijn van apparaten met Windows 10 en Windows Server 2016 | Microsoft Docs
description: Apparaten met Windows 10 en Windows Server 2016 probleemoplossing hybride Azure Active Directory worden toegevoegd.
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
ms.date: 08/17/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: cc252d1d0684d6632694afc8a367327794228c19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hybrid-azure-active-directory-joined-windows-10-and-windows-server-2016-devices"></a>Het oplossen van hybride Azure Active Directory die lid zijn van Windows 10 en Windows Server 2016-apparaten 

In dit onderwerp is van toepassing toohello volgende clients:

-   Windows 10
-   Windows Server 2016

Zie voor andere Windows-clients [probleemoplossing hybride Azure Active Directory die lid zijn van de downlevel-apparaten](device-management-troubleshoot-hybrid-join-windows-legacy.md).

Dit onderwerp wordt ervan uitgegaan dat u hebt [geconfigureerde hybride Azure Active Directory die lid zijn van de apparaten](device-management-hybrid-azuread-joined-devices-setup.md) toosupport Hallo volgen scenario's:

- Voorwaardelijke toegang op basis van apparaten

- [Enterprise-instellingen voor roaming](active-directory-windows-enterprise-state-roaming-overview.md)

- [Windows Hello voor Bedrijven](active-directory-azureadjoin-passport-deployment.md)


Dit document bevat richtlijnen voor probleemoplossing over hoe tooresolve mogelijke problemen. 


Voor Windows 10 en Windows Server 2016 hybride Azure Active Directory join ondersteunt Hallo Windows 10 November 2015 Update en hoger. U kunt het beste Hallo Verjaardag update gebruikt.

## <a name="step-1-retrieve-hello-join-status"></a>Stap 1: Hallo join status ophalen 

**tooretrieve hello join-status:**

1. Open Hallo opdrachtprompt als beheerder

2. Type **dsregcmd/status**



    +----------------------------------------------------------------------+
   | Apparaatstatus |+----------------------------------------------------------------------+
    
        AzureAdJoined: YES
     EnterpriseJoined: Geen apparaat-id: 5820fbe9-60c8-43b0-bb11-44aee233e4e7 vingerafdruk: B753A6679CE720451921302CA873794D94C6204A KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider: Microsoft Platform Crypto-Provider TpmProtected: Ja KeySignTest:: moet uitvoeren met verhoogde bevoegdheden voor tootest.
                  IDP: login.windows.net TenantId: 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName: Contoso AuthCodeUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl: https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl: https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl: https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl: eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ == JoinSrvVersion: 1.0 JoinSrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId: urn: ms-drs:enterpriseregistration.windows.net KeySrvVersion: 1.0 KeySrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId: urn: ms-drs:enterpriseregistration.windows.net DomainJoined: Ja DomainName: CONTOSO
    
    +----------------------------------------------------------------------+
   | Gebruikersstatus |+----------------------------------------------------------------------+
    
                 NgcSet: YES
               NgcKeyId: {C7A9AEDC-780E-4FDA-B200-1AE15561A46B}
        WorkplaceJoined: NO
          WamDefaultSet: YES
    WamDefaultAuthority: organisaties WamDefaultId: https://login.microsoft.com WamDefaultGUID: {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd) AzureAdPrt: Ja



## <a name="step-2-evaluate-hello-join-status"></a>Stap 2: De Hallo join-status 

Bekijk Hallo velden te volgen en zorg ervoor dat ze Hallo verwachte waarden hebben:

### <a name="azureadjoined--yes"></a>AzureAdJoined: Ja  

Dit veld geeft aan of het Hallo-apparaat is verbonden met Azure AD. Als de waarde Hallo **Nee**, Hallo join tooAzure AD is nog niet voltooid. 

**Mogelijke oorzaken:**

- Verificatie van de computer Hallo voor een join is mislukt.

- Er is een HTTP-proxy in Hallo organisatie die niet kan worden gedetecteerd door Hallo-computer

- Hallo-computer kan niet bereiken tooauthenticate Azure AD of Azure DRS voor registratie

- Hallo computer mogelijk niet op het interne netwerk van de organisatie van de Hallo of VPN met rechtstreeks tooan lokale AD-domeincontroller.

- Als het Hallo-computer heeft een TPM, kan het zijn in orde.

- Er zijn mogelijk een onjuiste configuratie van Hallo services eerder hebt genoteerd in Hallo-document dat u tooverify opnieuw moet. Algemene voorbeelden zijn:

    - De federatieserver is geen WS-Trust-eindpunten die zijn ingeschakeld

    - De federatieserver kan geen binnenkomende verificatie vanaf computers in uw netwerk met behulp van geïntegreerde Windows-verificatie.

    - Er is geen Service Connection Point-object dat tooyour geverifieerde domeinnaam op in Azure AD in Hallo AD-forest waar Hallo computer behoort beheerpunten bij

---

### <a name="domainjoined--yes"></a>DomainJoined: Ja  

Dit veld geeft aan of het Hallo-apparaat is lid van tooan op lokale Active Directory of niet. Als de waarde Hallo **Nee**, Hallo-apparaat een hybride Azure AD join kan niet worden uitgevoerd.  

---

### <a name="workplacejoined--no"></a>WorkplaceJoined: Nee  

Dit veld wordt aangegeven of het Hallo-apparaat is geregistreerd bij Azure AD als een persoonlijk apparaat (gemarkeerd als *Workplace Joined*). Deze waarde moet **Nee** voor een domein computer die ook hybride Azure AD die lid zijn. Als de waarde Hallo **Ja**, een account voor werk of school voorafgaande toohello voltooiing Hallo hybride Azure AD join is toegevoegd. Hallo-account wordt in dit geval genegeerd wanneer Hallo Verjaardag Update versie van Windows 10 (1607).

---

### <a name="wamdefaultset--yes-and-azureadprt--yes"></a>WamDefaultSet: Ja en AzureADPrt: Ja
  
Deze velden wordt aangegeven of de gebruiker Hallo tooAzure AD heeft geverifieerd bij de aanmelding toohello apparaat. Als de waarden Hallo **Nee**, kan worden voldaan:

- Ongeldige opslagsleutel (BEURS) in de TPM die zijn gekoppeld aan Hallo apparaat na inschrijving (selectievakje hello KeySignTest tijdens de uitvoering van verhoogde).

- Alternatieve aanmeldings-ID

- HTTP-Proxy is niet gevonden

## <a name="next-steps"></a>Volgende stappen

Bekijk voor vragen Hallo [Apparaatbeheer Veelgestelde vragen](device-management-faq.md) 
