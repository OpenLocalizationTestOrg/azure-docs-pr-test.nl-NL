---
title: aaaCertificate vernieuwen voor Office 365 en Azure AD-gebruikers | Microsoft Docs
description: Dit artikel wordt uitgelegd tooOffice 365 gebruikers hoe tooresolve met e-mailberichten die gebruikers informeren problemen over het vernieuwen van een certificaat.
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: 543b7dc1-ccc9-407f-85a1-a9944c0ba1be
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: b9b309e06949dc5488cd628650be413f366ed347
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="renew-federation-certificates-for-office-365-and-azure-active-directory"></a>Federatiecertificaten vernieuwen voor Office 365 en Azure Active Directory
## <a name="overview"></a>Overzicht
Geslaagde federatie tussen Azure Active Directory (Azure AD) en Active Directory Federation Services (AD FS), Hallo-certificaten die door AD FS toosign beveiliging tokens tooAzure AD moeten overeenkomen met wat in Azure AD is geconfigureerd. Niet overeenkomen, kan leiden toobroken vertrouwen. Azure AD zorgt ervoor dat deze informatie wordt gesynchroniseerd bij het implementeren van AD FS en Webtoepassingsproxy (voor toegang tot het extranet).

In dit artikel vindt u aanvullende informatie toomanage uw token-ondertekening van certificaten en bewaar deze synchroon met Azure AD op Hallo volgende gevallen:

* U implementeert geen Hallo Web Application Proxy en Hallo federatiemetagegevens is daarom niet beschikbaar in Hallo extranet.
* U de standaardconfiguratie Hallo van AD FS niet gebruikt voor token-ondertekening van certificaten.
* U gebruikt een derde partij id-provider.

## <a name="default-configuration-of-ad-fs-for-token-signing-certificates"></a>Standaardconfiguratie van AD FS voor token-ondertekening van certificaten
Hallo-token-ondertekening token ontsleutelen van certificaten worden meestal zelfondertekende certificaten en geschikt zijn voor één jaar. AD FS bevat standaard een proces dat automatisch verlengen wordt genoemd **AutoCertificateRollover**. Als u AD FS 2.0 of hoger, Office 365 en Azure AD automatisch bijwerken van uw certificaat voordat deze verloopt.

### <a name="renewal-notification-from-hello-office-365-portal-or-an-email"></a>Melding van de vernieuwing van Hallo Office 365-portal of een e-mailbericht
> [!NOTE]
> Als u hebt ontvangen een e-mailbericht of een portalmelding toorenew waarin u wordt gevraagd uw certificaat voor Office, Zie [beheren wijzigingen tootoken handtekeningcertificaten](#managecerts) toocheck als u geen actie tootake nodig. Microsoft is op de hoogte van een mogelijk probleem die toonotifications voor certificaatvernieuwing wordt verzonden leiden kan, zelfs wanneer er is geen actie vereist.
>
>

Azure AD probeert toomonitor Hallo federatiemetagegevens en update Hallo voor token-ondertekening van certificaten, zoals aangegeven door deze metagegevens. 30 dagen voordat het verloopt Hallo van Hallo voor token-ondertekening van certificaten, Azure AD gecontroleerd of er nieuwe certificaten beschikbaar zijn door Hallo federatiemetagegevens.

* Als deze kan Hallo federatiemetagegevens pollen en Hallo nieuwe certificaten ophalen, is geen e-mailmeldingen of de waarschuwing op Hallo Office 365-portal toohello gebruiker verstrekt.
* Als er geen Hallo nieuwe token-ondertekening van certificaten ophalen, ofwel omdat Hallo federatiemetagegevens kan niet worden bereikt of automatische certificaataanvraag rollover niet is ingeschakeld, Azure AD geeft een e-mailbericht en een waarschuwing in Hallo Office 365-portal.

![Office 365-portal melding](./media/active-directory-aadconnect-o365-certs/notification.png)

> [!IMPORTANT]
> Als u AD FS, tooensure bedrijfscontinuïteit, Controleer of uw servers hebt Hallo na updates zodat verificatiefouten voor bekende problemen wordt niet bijgewerkt. Dit vermindert bekende problemen van AD FS proxy-server voor deze vernieuwing en toekomstige vernieuwingsperioden:
>
> Server 2012 R2 - [Windows Server mei 2014 updatepakket](http://support.microsoft.com/kb/2955164)
>
> Server 2008 R2 en 2012 - [verificatie via proxy is mislukt in Windows Server 2012 of Windows 2008 R2 SP1](http://support.microsoft.com/kb/3094446)
>
>

## Controleer als Hallo certificaten toobe bijgewerkt moeten<a name="managecerts"></a>
### <a name="step-1-check-hello-autocertificaterollover-state"></a>Stap 1: Controleer de status van de AutoCertificateRollover Hallo
Open PowerShell op uw AD FS-server. Controleer of Hallo AutoCertificateRollover waarde tooTrue is ingesteld.

    Get-Adfsproperties

![AutoCertificateRollover](./media/active-directory-aadconnect-o365-certs/autocertrollover.png)

>[!NOTE] 
>Als u AD FS 2.0 gebruikt, moet u eerst Add-Pssnapin Microsoft.Adfs.Powershell uitvoeren.

### <a name="step-2-confirm-that-ad-fs-and-azure-ad-are-in-sync"></a>Stap 2: Controleer of de AD FS en Azure AD gesynchroniseerd zijn
Open hello Azure AD PowerShell-prompt op uw AD FS-server en tooAzure AD connect.

> [!NOTE]
> U kunt downloaden via Azure AD PowerShell [hier](https://technet.microsoft.com/library/jj151815.aspx).
>
>

    Connect-MsolService

Controleer Hallo certificaten die zijn geconfigureerd in AD FS en Azure AD-vertrouwensrelatie eigenschappen voor Hallo opgegeven domein.

    Get-MsolFederationProperty -DomainName <domain.name> | FL Source, TokenSigningCertificate

![Get-MsolFederationProperty](./media/active-directory-aadconnect-o365-certs/certsync.png)

Als de vingerafdrukken in beide Hallo Hallo uitvoer overeenkomen, uw certificaten zijn gesynchroniseerd met Azure AD.

### <a name="step-3-check-if-your-certificate-is-about-tooexpire"></a>Stap 3: Controleren of het certificaat over tooexpire
Controleer in de uitvoer van Get-MsolFederationProperty of Get-AdfsCertificate Hallo Hallo datum onder "Niet na." Als Hallo datum minder dan 30 dagen verwijderd is, moet u actie ondernemen.

| AutoCertificateRollover | Met Azure AD gesynchroniseerde certificaten | Federatiemetagegevens is openbaar toegankelijk | Geldigheid | Actie |
|:---:|:---:|:---:|:---:|:---:|
| Ja |Ja |Ja |- |Geen actie nodig. Zie [automatisch verlengen token-ondertekening certificaat](#autorenew). |
| Ja |Nee |- |Minder dan 15 dagen |Onmiddellijk vernieuwen. Zie [vernieuwen token-ondertekening handmatig van het certificaat](#manualrenew). |
| Nee |- |- |Minder dan 30 dagen |Onmiddellijk vernieuwen. Zie [vernieuwen token-ondertekening handmatig van het certificaat](#manualrenew). |

\[-] Maakt niet uit.

## Hallo voor token-ondertekening certificaat automatisch vernieuwen (aanbevolen)<a name="autorenew"></a>
U hoeft niet tooperform handmatige stappen uitgevoerd als beide Hallo volgende waar zijn:

* U hebt geïmplementeerd Web Application Proxy, die toegang toohello federatiemetagegevens van extranet Hallo kunt inschakelen.
* U gebruikt standaardconfiguratie Hallo AD FS (AutoCertificateRollover is ingeschakeld).

Controleer de volgende tooconfirm dat certificaat Hallo Hallo kan automatisch worden bijgewerkt.

**1. Hallo AD FS-eigenschap AutoCertificateRollover moet tooTrue worden ingesteld.** Hiermee wordt aangegeven dat AD FS automatisch gegenereerd nieuwe token-ondertekening en tokenontsleuteling certificaten, voordat Hallo oude zijn verlopen.

**2. Hallo AD FS federation-metagegevens is openbaar toegankelijk.** Controleer of uw federatiemetagegevens openbaar toegankelijk is door te navigeren toohello Volg URL vanaf een computer op het openbare internet (op het bedrijfsnetwerk Hallo) Hallo:

/federationmetadata/2007-06/federationmetadata.xml https:// (your_FS_name)

waar `(your_FS_name) `is vervangen door Hallo hostnaam van federation service gebruikmaakt van uw organisatie, zoals fs.contoso.com.  Als u kunnen tooverify van deze instellingen is, u hoeft geen toodo iets anders.  

Voorbeeld: https://fs.contoso.com/federationmetadata/2007-06/federationmetadata.xml

## Hallo voor token-ondertekening certificaat handmatig vernieuwen<a name="manualrenew"></a>
U kunt toorenew certificaten voor tokenondertekening Hallo handmatig. Bijvoorbeeld: hello volgende scenario's kunnen werken beter voor handmatige vernieuwing:

* Token handtekeningcertificaten zijn geen zelfondertekende certificaten. Hallo meest voorkomende reden hiervoor is dat AD FS-certificaten die zijn ingeschreven door een organisatie-certificeringsinstantie wordt beheerd door uw organisatie.
* Netwerkbeveiliging is niet toegestaan voor federatieve metagegevens toobe Hallo openbaar beschikbaar.

In deze scenario's, elke keer dat u bijwerken Hallo voor token-ondertekening van certificaten, moet u ook bijwerken uw Office 365-domein met behulp van Hallo PowerShell-opdracht Update MsolFederatedDomain.

### <a name="step-1-ensure-that-ad-fs-has-new-token-signing-certificates"></a>Stap 1: Zorg ervoor dat AD FS nieuwe token-ondertekening van certificaten
**Configuratie van de niet-standaard**

Als u een niet-standaard configuratie van AD FS (waarbij **AutoCertificateRollover** te is ingesteld,**False**), gebruikt u waarschijnlijk aangepaste certificaten (niet zelf ondertekend). Zie voor meer informatie over hoe toorenew Hallo AD FS-token-ondertekening certificaten [richtlijnen voor klanten die gebruikmaken van AD FS niet zelfondertekend certificaten](https://msdn.microsoft.com/library/azure/JJ933264.aspx#BKMK_NotADFSCert).

**Federatiemetagegevens is niet openbaar beschikbaar**

Daarentegen op Hallo als **AutoCertificateRollover** te is ingesteld,**True**, maar uw federatiemetagegevens is niet openbaar toegankelijk, eerst voor zorgen dat nieuwe certificaten voor tokenondertekening zijn gegenereerd door AD FS. Bevestig hebt u een nieuw token-ondertekening van certificaten door duurt Hallo stappen te volgen:

1. Controleer of u bent aangemeld op toohello primaire AD FS-server.
2. Controleer Hallo huidige handtekeningcertificaten in AD FS door een PowerShell-opdrachtvenster openen en het Hallo volgende opdracht uitvoeren:

    PS C:\>Get-ADFSCertificate – CertificateType token-ondertekening

   > [!NOTE]
   > Als u AD FS 2.0 gebruikt, moet u eerst Add-Pssnapin Microsoft.Adfs.Powershell uitvoeren.
   >
   >
3. Bekijk de opdrachtuitvoer Hallo op alle certificaten die worden vermeld. Als AD FS is een nieuw certificaat gegenereerd, ziet u twee certificaten in de uitvoer van de Hallo: één voor welke Hallo **IsPrimary** waarde is **True** en Hallo **NotAfter** datum is binnen vijf dagen en één waarvoor **IsPrimary** is **False** en **NotAfter** over een jaar in toekomstige Hallo is.
4. Als u slechts één certificaat dat wordt weergegeven en Hallo **NotAfter** datum is binnen vijf dagen, moet u een nieuw certificaat toogenerate.
5. een nieuw certificaat toogenerate uitvoeren Hallo volgende opdracht achter de PowerShell-opdrachtprompt: `PS C:\>Update-ADFSCertificate –CertificateType token-signing`.
6. Hallo-update controleren door het uitvoeren van de opdracht opnieuw na Hallo: PS C:\>Get-ADFSCertificate – CertificateType token-ondertekening

Twee certificaten zou nu moeten worden vermeld, die een **NotAfter** ongeveer een jaar in toekomstige Hallo en voor welke Hallo **IsPrimary** waarde is **False**.

### <a name="step-2-update-hello-new-token-signing-certificates-for-hello-office-365-trust"></a>Stap 2: Hallo nieuwe token-ondertekening van certificaten voor Office 365 Hallo vertrouwensrelatie bijwerken
Office 365 met Hallo nieuwe token ondertekenen certificaten toobe gebruikt voor de vertrouwensrelatie met Hallo als volgt bijgewerkt.

1. Open Hallo Microsoft Azure Active Directory-Module voor Windows PowerShell.
2. Voer $cred = Get-Credential. Wanneer deze cmdlet wordt u gevraagd om referenties, typt u de referenties van uw cloud-beheerder serviceaccount.
3. Uitvoeren van Connect MsolService – $cred referenties. Deze cmdlet verbindt toohello-cloudservice. Maken van een context die u verbindt toohello cloud-service is vereist voordat u een van de aanvullende cmdlets Hallo door Hallo-hulpprogramma geïnstalleerd.
4. Als u deze opdrachten op een computer die geen primaire Hallo AD FS-federatieserver uitvoert, voert u Set-MSOLAdfscontext-Computer <AD FS primary server>, waarbij <AD FS primary server> Hallo interne FQDN-naam van Hallo primaire AD FS-server is. Deze cmdlet maakt een context die u verbindt tooAD FS.
5. Voer Update-MSOLFederatedDomain – DomainName <domain>. Deze cmdlet Hallo instellingen vanaf AD FS in Hallo cloudservice-updates en Hallo vertrouwensrelatie bestaat tussen twee Hallo configureert.

> [!NOTE]
> Als u toosupport meerdere topleveldomeinen, zoals contoso.com en fabrikam.com moet, moet u Hallo **SupportMultipleDomain** overschakelen met cmdlets. Zie voor meer informatie [ondersteuning voor meerdere domeinen van het hoogste niveau](active-directory-aadconnect-multiple-domains.md).
>
>

## Azure AD-vertrouwensrelatie herstellen met behulp van Azure AD Connect<a name="connectrenew"></a>
Als u uw AD FS-farm en Azure AD-vertrouwensrelatie met behulp van Azure AD Connect geconfigureerd, kunt u Azure AD Connect toodetect kunt gebruiken als u tootake een actie voor uw token-ondertekening van certificaten. Als u toorenew Hallo certificaten nodig hebt, kunt u Azure AD Connect toodo dus.

Zie voor meer informatie [Hallo vertrouwensrelatie repareren](active-directory-aadconnect-federation-management.md).
