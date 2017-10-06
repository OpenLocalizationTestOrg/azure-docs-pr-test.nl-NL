---
title: aaaTroubleshooting hello automatische registratie van Azure AD-domein voor Windows 10 en Windows Server 2016 computers die lid zijn | Microsoft Docs
description: Het oplossen van problemen Hallo automatische registratie van Azure AD-domein lid zijn van computers voor Windows 10 en Windows Server 2016.
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
ms.openlocfilehash: 3795323ce9392368b412b3e1208868431e59a74b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-tooazure-ad--windows-10-and-windows-server-2016"></a>Automatische registratie van domein het oplossen van problemen die lid zijn van computers tooAzure AD – Windows 10 en Windows Server 2016

In dit onderwerp is van toepassing toohello volgende clients:

-   Windows 10
-   Windows Server 2016

Zie voor andere Windows-clients [computers tooAzure AD probleemoplossing automatische registratie van domein worden toegevoegd voor Windows downlevel-clients](active-directory-device-registration-troubleshoot-windows-legacy.md).

Dit onderwerp wordt ervan uitgegaan dat u hebt geconfigureerd automatische registratie van apparaten domein vermelde in dat wordt beschreven in [hoe tooconfigure automatische registratie van Windows-domein apparaten met Azure Active Directory](active-directory-device-registration-get-started.md) toosupport hello volgen scenario's:

- [Voorwaardelijke toegang op basis van apparaten](active-directory-conditional-access-automatic-device-registration-setup.md)

- [Enterprise-instellingen voor roaming](active-directory-windows-enterprise-state-roaming-overview.md)

- [Windows Hello voor Bedrijven](active-directory-azureadjoin-passport-deployment.md)


Dit document bevat richtlijnen voor probleemoplossing over hoe tooresolve mogelijke problemen. 

Hallo wordt registratie ondersteund in Windows hello Update 10 November 2015 en hoger.  
U kunt het beste Hallo Verjaardag Update gebruikt voor het inschakelen van de bovenstaande Hallo scenario's.

## <a name="step-1-retrieve-hello-registration-status"></a>Stap 1: De registratiestatus Hallo ophalen 

**tooretrieve hello registratiestatus:**

1. Open Hallo-opdrachtprompt als beheerder.

2. Type **dsregcmd/status**



    +----------------------------------------------------------------------+
   | Apparaatstatus |+----------------------------------------------------------------------+
    
        AzureAdJoined : YES
     EnterpriseJoined: Geen apparaat-id: 5820fbe9-60c8-43b0-bb11-44aee233e4e7 vingerafdruk: B753A6679CE720451921302CA873794D94C6204A KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider: Microsoft Platform Crypto-Provider TpmProtected: Ja KeySignTest:: moet uitvoeren met verhoogde bevoegdheden voor tootest.
                  IDP: login.windows.net TenantId: 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName: Contoso AuthCodeUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl: https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl: https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl: https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl: eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ == JoinSrvVersion: 1.0 JoinSrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId: urn: ms-drs:enterpriseregistration.windows.net KeySrvVersion: 1.0 KeySrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId: urn: ms-drs:enterpriseregistration.windows.net DomainJoined: Ja DomainName: CONTOSO
    
    +----------------------------------------------------------------------+
   | Gebruikersstatus |+----------------------------------------------------------------------+
    
                 NgcSet : YES
               NgcKeyId : {C7A9AEDC-780E-4FDA-B200-1AE15561A46B}
        WorkplaceJoined : NO
          WamDefaultSet : YES
    WamDefaultAuthority: organisaties WamDefaultId: https://login.microsoft.com WamDefaultGUID: {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd) AzureAdPrt: Ja



## <a name="step-2-evaluate-hello-registration-status"></a>Stap 2: De registratiestatus Hallo 

Bekijk Hallo velden te volgen en zorg ervoor dat ze Hallo verwachte waarden hebben:

### <a name="azureadjoined--yes"></a>AzureAdJoined: Ja  

Dit veld bevat of Hallo-apparaat is geregistreerd bij Azure AD. Als Hallo waarde wordt weergegeven als 'Nee', worden de registratie is niet voltooid. 

**Mogelijke oorzaken:**

- Verificatie van de computer Hallo voor registratie is mislukt.

- Er is een HTTP-proxy in Hallo organisatie die niet kan worden gedetecteerd door Hallo-computer

- Hallo-computer kan Azure AD voor de verificatie of Azure DRS voor registratie niet bereiken

- Hallo computer mogelijk niet op het interne netwerk van de organisatie van de Hallo of VPN met rechtstreeks tooan lokale AD-domeincontroller.

- Als Hallo computer een TPM heeft, wordt in een verkeerde status.

- Er is mogelijk een onjuiste configuratie van services eerder hebt genoteerd in Hallo-document dat u tooverify opnieuw moet. Algemene voorbeelden zijn:

    - De federatieserver is geen WS-Trust-eindpunten die zijn ingeschakeld

    - De federatieserver mogelijk niet toegestaan voor binnenkomende verificatie vanaf computers in uw netwerk met behulp van geïntegreerde Windows-verificatie.

    - Er is geen Service Connection Point-object dat tooyour geverifieerde domeinnaam op in Azure AD in Hallo AD-forest waar Hallo computer behoort beheerpunten bij

---

### <a name="domainjoined--yes"></a>DomainJoined: Ja  

Dit veld wordt aangegeven of Hallo apparaat lid tooan op lokale Active Directory of niet. Als het Hallo-waarde wordt weergegeven als **Nee**, Hallo apparaat niet automatisch kan registreren met Azure AD. Controleer eerst die Hallo apparaat joins toohello op lokale Active Directory voordat u deze kunt registreren met Azure AD. Als u om lid te worden Hallo computer tooAzure AD rechtstreeks op zoek bent, gaat u tooLearn over de mogelijkheden van Azure Active Directory Join.

---

### <a name="workplacejoined--no"></a>WorkplaceJoined: Nee  

Dit veld bevat of Hallo-apparaat is geregistreerd met Azure AD, maar als een persoonlijk apparaat (gemarkeerd als 'Workplace Joined'). Als deze waarde moet worden weergegeven als 'Nee' voor een computer verbonden met het domein is geregistreerd in Azure AD, maar als deze wordt weergegeven als Ja betekent dit dat is een account voor werk of school toegevoegde voorafgaande toohello computer voltooien registratie. In dit geval worden Hallo-account genegeerd als Hallo Verjaardag Update versie van Windows 10 (1607 wanneer de opdracht WinVer Hallo uitgevoerd in de Hallo venster 'Uitvoeren' of een opdrachtpromptvenster).

---

### <a name="wamdefaultset--yes-and-azureadprt--yes"></a>WamDefaultSet: Ja en AzureADPrt: Ja
  
Deze velden weergeven dat die Hallo-gebruiker is geverifieerd tooAzure AD bij de ondertekening van toohello apparaat. Als ze weergeven volgen 'NO' hello mogelijke oorzaken:

- Ongeldige opslagsleutel (BEURS) in de TPM die zijn gekoppeld aan Hallo apparaat na inschrijving (selectievakje hello KeySignTest tijdens de uitvoering van verhoogde).

- Alternatieve aanmeldings-ID

- HTTP-Proxy is niet gevonden

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie, Hallo [automatische apparaatregistratie Veelgestelde vragen](active-directory-device-registration-faq.md) 
