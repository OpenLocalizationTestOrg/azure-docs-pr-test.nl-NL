---
title: service aaaAzure AD Connect-synchronisatie-functies en configuratie | Microsoft Docs
description: Beschrijving van service aan clientzijde functies voor Azure AD Connect sync-service.
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 213aab20-0a61-434a-9545-c4637628da81
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 7ad05c45bb6b5fd5deaa3466e2936b19d3d9eabb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-service-features"></a>Azure AD Connect sync-service-functies
de synchronisatiefunctie Hallo van Azure AD Connect bestaat uit twee onderdelen:

* Hallo lokale onderdeel **Azure AD Connect-synchronisatie**, ook wel **synchronisatie-engine**.
* Hallo-service die zich in Azure AD ook wel bekend als **Azure AD Connect sync-service**

Dit onderwerp wordt uitgelegd hoe Hallo na functies Hallo **Azure AD Connect-synchronisatieservice** werk en hoe kunt u ze configureren met Windows PowerShell.

Deze instellingen zijn geconfigureerd door Hallo [Azure Active Directory-Module voor Windows PowerShell](http://aka.ms/aadposh). Download en installeer deze afzonderlijk van Azure AD Connect. Hallo-cmdlets die zijn beschreven in dit onderwerp zijn geïntroduceerd in Hallo [versie van de maart 2016 (build 9031.1)](http://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx#Version_9031_1). Als u geen Hallo-cmdlets die zijn beschreven in dit onderwerp of ze geen Hallo dezelfde leiden genereren, moet u ervoor zorgen kunt u de meest recente versie Hallo uitvoeren.

toosee hello configuratie in uw Azure AD-directory uitvoeren `Get-MsolDirSyncFeatures`.  
![Get-MsolDirSyncFeatures resultaat](./media/active-directory-aadconnectsyncservice-features/getmsoldirsyncfeatures.png)

Veel van deze instellingen kunnen alleen worden gewijzigd door Azure AD Connect.

Hallo volgende instellingen kunnen worden geconfigureerd door `Set-MsolDirSyncFeature`:

| DirSyncFeature | Opmerking |
| --- | --- |
| [EnableSoftMatchOnUpn](#userprincipalname-soft-match) |Hiermee maakt objecten toojoin voor userPrincipalName toevoeging tooprimary SMTP-adres. |
| [SynchronizeUpnForManagedUsers](#synchronize-userprincipalname-updates) |Hallo sync engine tooupdate Hallo kenmerk userPrincipalName kunt u gebruikers met beheerde/een licentie (niet-gefedereerde). |

Nadat u een functie hebt ingeschakeld, kunnen deze kan niet worden uitgeschakeld.

> [!NOTE]
> Hallo van 24 augustus 2016 functie *dubbel kenmerk tolerantie* is standaard ingeschakeld voor de nieuwe Azure AD-mappen. Deze functie wordt ook uitgerold en ingeschakeld op de mappen die zijn gemaakt voor deze datum. U ontvangt een e-mailbericht wanneer uw directory over tooget deze functie is ingeschakeld.
> 
> 

Hallo volgende instellingen zijn geconfigureerd voor Azure AD Connect en kan niet worden gewijzigd door `Set-MsolDirSyncFeature`:

| DirSyncFeature | Opmerking |
| --- | --- |
| DeviceWriteback |[Azure AD Connect: Apparaat terugschrijven inschakelen](active-directory-aadconnect-feature-device-writeback.md) |
| DirectoryExtensions |[Azure AD Connect-synchronisatie: Directory-uitbreidingen](active-directory-aadconnectsync-feature-directory-extensions.md) |
| [DuplicateProxyAddressResiliency<br/>DuplicateUPNResiliency](#duplicate-attribute-resiliency) |Hiermee kunt een kenmerk toobe in quarantaine geplaatst wanneer dit is een duplicaat van een ander object in plaats van het gehele object Hallo mislukt tijdens het exporteren. |
| PasswordSync |[Wachtwoordsynchronisatie met Azure AD Connect-synchronisatie implementeren](active-directory-aadconnectsync-implement-password-synchronization.md) |
| UnifiedGroupWriteback |[Voorbeeld: Groep terugschrijven](active-directory-aadconnect-feature-preview.md#group-writeback) |
| UserWriteback |Momenteel niet ondersteund. |

## <a name="duplicate-attribute-resiliency"></a>Dubbel kenmerk tolerantie
In plaats van het mislukken van tooprovision objecten met dubbele UPN's / proxyAddresses, dubbel kenmerk Hallo 'quarantaine' en een tijdelijke-waarde is toegewezen. Wanneer het Hallo-adresconflict is opgelost, Hallo tijdelijke UPN is de juiste waarde toohello automatisch gewijzigd. Zie voor meer informatie [tolerantie voor synchronisatie en dubbel kenmerk](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).

## <a name="userprincipalname-soft-match"></a>UserPrincipalName zachte overeen
Wanneer deze functie is ingeschakeld, soft-match is ingeschakeld voor de UPN in toevoeging toohello [primaire SMTP-adres](https://support.microsoft.com/kb/2641663), die altijd is ingeschakeld. Soft-match is gebruikte toomatch bestaande cloudgebruikers in Azure AD met on-premises gebruikers.

Als u moet toomatch on-premises AD-accounts met bestaande accounts die zijn gemaakt in de cloud Hallo en u geen gebruikmaakt van Exchange Online en deze functie is handig. In dit scenario wordt doorgaans hebt niet u een reden tooset Hallo SMTP-kenmerk in Hallo cloud.

Deze functie op standaard voor nieuw is Azure AD-mappen. U kunt zien of deze functie is ingeschakeld voor u door te voeren:  

```
Get-MsolDirSyncFeatures -Feature EnableSoftMatchOnUpn
```

Als deze functie is niet ingeschakeld voor uw Azure AD-directory, kunt klikt u inschakelen door te voeren:  

```
Set-MsolDirSyncFeature -Feature EnableSoftMatchOnUpn -Enable $true
```

## <a name="synchronize-userprincipalname-updates"></a>UserPrincipalName updates synchroniseren
In het verleden hebben is updates toohello UserPrincipalName kenmerk met de synchronisatieservice Hallo van on-premises geblokkeerd, tenzij beide volgende voorwaarden voldaan wordt:

* Hallo-gebruiker wordt beheerd (niet-gefedereerde).
* Hallo gebruiker heeft geen licentie toegewezen.

Zie voor meer informatie [gebruiker namen in Office 365, Azure of Intune komen niet overeen op premises UPN of de alternatieve aanmeldings-ID Hallo](https://support.microsoft.com/kb/2523192).

Inschakelen van deze functie kunt Hallo sync engine tooupdate Hallo userPrincipalName, wanneer het gewijzigde lokale is en u Wachtwoordsynchronisatie gebruiken. Als u federation gebruikt, wordt deze functie wordt niet ondersteund.

Deze functie op standaard voor nieuw is Azure AD-mappen. U kunt zien of deze functie is ingeschakeld voor u door te voeren:  

```
Get-MsolDirSyncFeatures -Feature SynchronizeUpnForManagedUsers
```

Als deze functie is niet ingeschakeld voor uw Azure AD-directory, kunt klikt u inschakelen door te voeren:  

```
Set-MsolDirSyncFeature -Feature SynchronizeUpnForManagedUsers -Enable $true
```

Nadat u deze functie inschakelt, bestaande userPrincipalName waarden blijft-is. Op de volgende wijziging van Hallo userPrincipalName kenmerk lokale Hallo normale Deltasynchronisatie op gebruikers Hallo UPN bijgewerkt.  

## <a name="see-also"></a>Zie ook
* [Azure AD Connect-synchronisatie](active-directory-aadconnectsync-whatis.md)
* [Uw on-premises identiteiten integreren met Azure Active Directory](active-directory-aadconnect.md).

