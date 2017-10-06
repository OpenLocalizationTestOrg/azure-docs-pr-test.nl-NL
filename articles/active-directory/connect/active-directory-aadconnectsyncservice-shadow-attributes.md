---
title: aaaAzure AD Connect sync-service de kenmerken | Microsoft Docs
description: Hierin wordt beschreven hoe de kenmerken van werken in Azure AD Connect sync-service.
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 1b8665e7488c6078b655f8a3e35519145bacd898
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-service-shadow-attributes"></a>Azure AD Connect sync-service de kenmerken
De meeste kenmerken worden vertegenwoordigd Hallo dezelfde manier in Azure AD omdat ze in uw lokale Active Directory. Maar bepaalde kenmerken hebben sommige speciale verwerking en Hallo-kenmerkwaarde in Azure AD mogelijk anders dan wat Azure AD Connect synchroniseert.

## <a name="introducing-shadow-attributes"></a>Introductie van de kenmerken
Enkele kenmerken hebben twee manieren in Azure AD. Hallo lokale value- en een berekende waarde worden opgeslagen. Deze extra kenmerken worden de kenmerken van genoemd. Hallo twee meest voorkomende kenmerken waarin u zien hoe dit gedrag zijn **userPrincipalName** en **proxyAddress**. Hallo wijziging in de kenmerkwaarden gebeurt wanneer er waarden zijn in deze kenmerken die niet-geverifieerd domeinen. Maar Hallo synchronisatie-engine in Connect Hallo waarde leest in Hallo shadow kenmerk dus vanuit het perspectief, Hallo-kenmerk is bevestigd door Azure AD.

U kunt hello Azure portal of met PowerShell met de kenmerken van Hallo niet zien. Maar wat Hallo concept helpt u tootroubleshoot bepaalde scenario's waarin het Hallo-kenmerk een verschillende waarden voor de on-premises en in Hallo cloud.

toobetter meer inzicht in gedrag Hallo, Bekijk dit voorbeeld van Fabrikam:  
![Domeinen](./media/active-directory-aadconnectsyncservice-shadow-attributes/domains.png)  
Ze hebben meerdere UPN-achtervoegsels in hun lokale Active Directory, maar ze deze alleen hebt gecontroleerd.

### <a name="userprincipalname"></a>UserPrincipalName
Een gebruiker heeft Hallo kenmerkwaarden in een niet-geverifieerd domein te volgen:

| Kenmerk | Waarde |
| --- | --- |
| lokale userPrincipalName | lee.sperry@fabrikam.com |
| Azure AD-shadowUserPrincipalName | lee.sperry@fabrikam.com |
| Azure AD-userPrincipalName | lee.sperry@fabrikam.onmicrosoft.com |

Hallo userPrincipalName kenmerk is Hallo waarde die wordt weergegeven wanneer u PowerShell.

Aangezien Hallo echte lokale kenmerk-waarde wordt opgeslagen in Azure AD, wanneer u Hallo fabrikam.com domein verifiëren, werkt Azure AD Hallo userPrincipalName kenmerk Hallo waarde uit Hallo shadowUserPrincipalName. U hoeft geen toosynchronize eventuele wijzigingen van Azure AD Connect voor deze waarden toobe bijgewerkt.

### <a name="proxyaddresses"></a>proxyAddresses
Hallo hetzelfde proces voor het opnemen van alleen geverifieerde domeinen vindt ook plaats voor proxyAddresses, maar met een aantal extra logica. Hallo geverifieerde domeinen zoekt alleen voor gebruikers postvak wordt uitgevoerd. Een e-mailfunctionaliteit gebruiker of neem contact op met vertegenwoordigen een gebruiker in een andere Exchange-organisatie en u kunt alle waarden in proxyAddresses toothese objecten toevoegen.

Voor een postvakgebruiker, on-premises of in Exchange Online, wordt alleen de waarden voor geverifieerde domeinen weergegeven. Het kan er als volgt uit:

| Kenmerk | Waarde |
| --- | --- |
| lokale proxyAddresses | SMTP:abbie.spencer@fabrikamonline.com</br>smtp:abbie.spencer@fabrikam.com</br>smtp:abbie@fabrikamonline.com |
| Exchange Online proxyAddresses | SMTP:abbie.spencer@fabrikamonline.com</br>smtp:abbie@fabrikamonline.com</br>SIP:abbie.spencer@fabrikamonline.com |

In dit geval  **smtp:abbie.spencer@fabrikam.com**  is verwijderd, omdat dat domein is niet geverifieerd. Maar ook toegevoegd Exchange  **SIP:abbie.spencer@fabrikamonline.com** . Fabrikam nog niet is gebruikt Lync/Skype lokale, maar Azure AD en Exchange Online worden voorbereid voor.

Deze logica voor proxyAddresses is waarnaar wordt verwezen tooas **ProxyCalc**. ProxyCalc wordt aangeroepen met elke wijziging van een gebruiker wanneer:

- Hallo-gebruiker is een service-abonnement dat Exchange Online omvat, zelfs als het Hallo-gebruiker is geen licentie voor Exchange toegewezen. Bijvoorbeeld, als Hallo gebruiker is toegewezen Hallo Office E3 SKU, maar alleen is toegewezen SharePoint Online. Dit geldt zelfs als uw postvak nog steeds lokaal is.
- Hallo kenmerk msExchRecipientTypeDetails heeft een waarde.
- U een wijziging tooproxyAddresses of userPrincipalName.

ProxyCalc kan duren voordat sommige tooprocess tijd een wijziging van een gebruiker en is niet synchroon met hello Azure AD Connect-exportproces.

> [!NOTE]
> Hallo ProxyCalc logica heeft een aantal extra gedrag voor geavanceerde scenario's niet in dit onderwerp wordt beschreven. In dit onderwerp is opgegeven voor u toounderstand Hallo gedrag en niet alle interne logische-document.

### <a name="quarantined-attribute-values"></a>In quarantaine geplaatste kenmerkwaarden
De kenmerken worden ook gebruikt als er dubbele kenmerkwaarden. Zie voor meer informatie [dubbel kenmerk tolerantie](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).

## <a name="see-also"></a>Zie ook
* [Azure AD Connect-synchronisatie](active-directory-aadconnectsync-whatis.md)
* [Uw on-premises identiteiten integreren met Azure Active Directory](active-directory-aadconnect.md).
