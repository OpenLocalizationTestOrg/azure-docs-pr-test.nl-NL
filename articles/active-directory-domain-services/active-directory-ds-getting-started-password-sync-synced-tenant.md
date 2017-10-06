---
title: 'Azure AD Domain Services: wachtwoordsynchronisatie inschakelen | Microsoft Docs'
description: Aan de slag met Azure Active Directory Domain Services
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 8731f2b2-661c-4f3d-adba-2c9e06344537
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/30/2017
ms.author: maheshu
ms.openlocfilehash: a7a6ee0f83d3d9bdaf236717efb39155a26934e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-password-synchronization-tooazure-active-directory-domain-services"></a>Wachtwoord synchronisatie tooAzure Active Directory Domain Services inschakelen
Tijdens de vorige taken hebt u Azure Active Directory Domain Services ingeschakeld voor uw Azure Active Directory-tenant (Azure AD). de volgende taak Hallo is tooenable synchronisatie van referentie-hashes die vereist zijn voor NT LAN Manager (NTLM) en Kerberos-verificatie tooAzure AD Domain Services. Nadat u een referentie-synchronisatie hebt ingesteld, kunnen gebruikers zich aanmelden in toohello beheerde domein met hun bedrijfsreferenties.

Hallo stappen die nodig zijn verschillend voor de gebruiker alleen in de cloud accounts tegenover gebruikersaccounts die worden gesynchroniseerd vanuit uw lokale directory met Azure AD Connect. Als uw Azure AD-tenant een combinatie van heeft cloud alleen gebruikers en gebruikers van uw on-premises AD, moet u tooperform na beide stappen.

<br>

> [!div class="op_single_selector"]
> * **Alleen in de cloud gebruikersaccounts**: [wachtwoorden synchroniseren voor alleen in de cloud gebruikersaccounts tooyour beheerd domein](active-directory-ds-getting-started-password-sync.md)
> * **Lokale gebruikersaccounts**: [wachtwoorden synchroniseren voor gebruikersaccounts die zijn gesynchroniseerd vanuit uw on-premises AD tooyour beheerd domein](active-directory-ds-getting-started-password-sync-synced-tenant.md)
>
>

<br>

## <a name="task-5-enable-password-synchronization-tooyour-managed-domain-for-user-accounts-synced-with-your-on-premises-ad"></a>Taak 5: inschakelen wachtwoord synchronisatie tooyour beheerd domein voor gebruikersaccounts die zijn gesynchroniseerd met uw on-premises AD
Een gesynchroniseerde Azure AD-tenant toosynchronize met van uw organisatie on-premises directory via Azure AD Connect is ingesteld. Azure AD Connect wordt standaard NTLM en Kerberos-referentie-hashes tooAzure AD niet gesynchroniseerd. toouse Azure AD Domain Services, moet u tooconfigure Azure AD Connect toosynchronize referentie-hashes voor NTLM en Kerberos-verificatie. Hallo stappen te volgen inschakelen synchronisatie van referentie-hashes Hallo vereist vanuit uw lokale directory tooyour Azure AD-tenant.

> [!NOTE]
> Als uw organisatie gebruikersaccounts die worden gesynchroniseerd vanuit uw on-premises directory, moet synchronisatie van NTLM en Kerberos-hashes in volgorde toouse Hallo beheerde domein inschakelen. Een gesynchroniseerde gebruikersaccount is een account dat is gemaakt in uw on-premises directory en is gesynchroniseerd tooyour Azure AD-tenant met Azure AD Connect.
>
>

### <a name="install-or-update-azure-ad-connect"></a>Azure AD Connect installeren of bijwerken
Installeren van de meest recente aanbevolen Hallo versie van Azure AD Connect op een domein die lid zijn van de computer. Als u een bestaand exemplaar van Azure AD Connect-installatie hebt, moet u tooupdate deze toouse Hallo meest recente versie van Azure AD Connect. tooavoid bekende problemen/fouten optreden die mogelijk al zijn opgelost, zorg ervoor dat u altijd de meest recente versie Hallo van Azure AD Connect gebruiken.

**[Azure AD Connect downloaden](http://www.microsoft.com/download/details.aspx?id=47594)**

Aanbevolen versie: **1.1.553.0** - gepubliceerd op 27 juni 2017.

> [!WARNING]
> U moet installeren Hallo meest recente versie van Azure AD Connect tooenable hello toosynchronize tooyour Azure AD-tenant oude wachtwoord referenties (vereist voor NTLM en Kerberos-verificatie) aanbevolen. Deze functionaliteit is niet beschikbaar in eerdere versies van Azure AD Connect of met Hallo oudere DirSync-hulpprogramma.
>
>

Installatie-instructies voor Azure AD Connect zijn beschikbaar in de volgende Hallo artikel - [aan de slag met Azure AD Connect](../active-directory/active-directory-aadconnect.md)

### <a name="enable-synchronization-of-ntlm-and-kerberos-credential-hashes-tooazure-ad"></a>Synchronisatie van NTLM en Kerberos-referentie-hashes tooAzure AD inschakelen
Hallo volgende PowerShell-script op elk AD-forest tooforce volledige Wachtwoordsynchronisatie, uitvoeren en schakel alle on-premises gebruikers de referentie-hashes toosync tooyour Azure AD-tenant. Dit script kunt Hallo referentie-hashes voor NTLM of Kerberos-verificatie toobe gesynchroniseerde tooyour Azure AD-tenant.

```
$adConnector = "<CASE SENSITIVE AD CONNECTOR NAME>"  
$azureadConnector = "<CASE SENSITIVE AZURE AD CONNECTOR NAME>"  
Import-Module adsync  
$c = Get-ADSyncConnector -Name $adConnector  
$p = New-Object Microsoft.IdentityManagement.PowerShell.ObjectModel.ConfigurationParameter "Microsoft.Synchronize.ForceFullPasswordSync", String, ConnectorGlobal, $null, $null, $null
$p.Value = 1  
$c.GlobalParameters.Remove($p.Name)  
$c.GlobalParameters.Add($p)  
$c = Add-ADSyncConnector -Connector $c  
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $azureadConnector -Enable $false   
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $azureadConnector -Enable $true  
```

Afhankelijk van Hallo grootte van uw directory (aantal gebruikers, groepen enzovoort), synchronisatie van de referentie-hashes tooAzure AD tijd in beslag neemt. Hallo wachtwoorden, worden gebruikt op Hallo Azure AD Domain Services beheerd domein kort nadat Hallo referentie-hashes zijn tooAzure AD gesynchroniseerd.

<br>

## <a name="related-content"></a>Gerelateerde inhoud
* [Inschakelen wachtwoord synchronisatie tooAAD Domain Services voor een alleen-Azure AD-directory](active-directory-ds-getting-started-password-sync.md)
* [Een beheerd domein van Azure AD Domain Services beheren](active-directory-ds-admin-guide-administer-domain.md)
* [Deelnemen aan een Windows virtuele machine tooan Azure AD Domain Services beheerd domein](active-directory-ds-admin-guide-join-windows-vm.md)
* [Deelnemen aan een Red Hat Enterprise Linux virtuele machine tooan Azure AD Domain Services beheerd domein](active-directory-ds-admin-guide-join-rhel-linux-vm.md)
