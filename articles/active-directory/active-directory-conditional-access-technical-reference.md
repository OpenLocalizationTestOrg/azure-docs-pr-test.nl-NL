---
title: technische documentatie voor voorwaardelijke toegang van Active Directory aaaAzure | Microsoft Docs
description: "Met voorwaardelijk toegangsbeheer controleert de Azure Active Directory Hallo bepaalde voorwaarden die u bij het verifiëren van de gebruiker Hallo en alvorens deze toegang toohello toepassing kiezen. Als deze voorwaarden is voldaan, wordt Hallo gebruiker geverifieerd en toegang toohello toepassing toegestaan."
services: active-directory.
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 56a5bade-7dcc-4dcf-8092-a7d4bf5df3c1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: ee201405d1d17f130607a95bf455b60cd222dd0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-conditional-access-technical-reference"></a>Technische documentatie van Azure Active Directory voorwaardelijke toegang

## <a name="services-enabled-with-conditional-access"></a>Services met voorwaardelijke toegang ingeschakeld

Regels voor voorwaardelijke toegang worden ondersteund tussen de verschillende typen voor Azure AD-toepassing. Deze lijst bevat:


* Toepassingen die zijn geregistreerd bij hello Azure-toepassingsproxy
* Azure RemoteApp
* Ontwikkelde line-of-business- en multitenant-toepassingen die zijn geregistreerd bij Azure AD
* Dynamics CRM
* Federatieve toepassingen van hello Azure AD-toepassingsgalerie
* Microsoft Office 365 Yammer
* Microsoft Office 365 Exchange Online
* Microsoft Office 365 SharePoint Online (inclusief OneDrive voor bedrijven)
* Microsoft Power BI 
* Wachtwoord SSO-toepassingen van hello Azure AD-toepassingsgalerie
* Visual Studio Team Services
* Microsoft Teams









## <a name="enable-access-rules"></a>Toegangsregels inschakelen
Elke regel worden ingeschakeld of uitgeschakeld voor een per toepassing basissen. Wanneer regels zijn **ON** wordt ingeschakeld en voor gebruikers die toegang tot de toepassing hello afgedwongen. Wanneer ze zijn **OFF** wordt niet gebruikt en wordt niet impact Hallo gebruikers zich aanmelden ervaring.

## <a name="applying-rules-toospecific-users"></a>Toepassen van regels toospecific gebruikers
Regels kunnen worden toegepast toospecific sets van gebruikers op basis van de beveiligingsgroep door in te stellen **toepassen op**. **Toepassen op** te kunnen worden ingesteld**alle gebruikers** of **groepen**. Als de waarde te**alle gebruikers** Hallo regels gelden tooany gebruiker met toegang toohello toepassing. Hallo **groepen** optie specifieke beveiligings- en distributiepunten groepen toobe is geselecteerd, kunnen regels alleen afgedwongen voor deze groepen.

Bij het implementeren van een regel, is het gebruikelijk dat toofirst toepassen een beperkt aantal gebruikers die lid van een pilot-groepen zijn. Zodra de volledige Hallo regel te kan worden toegepast**alle gebruikers**. Hierdoor wordt toobe afgedwongen voor alle gebruikers in de organisatie Hallo Hallo-regel.

Selecteer groepen kunnen ook worden vrijgesteld van met behulp van Hallo **behalve** optie. Leden van deze groepen worden vrijgesteld, zelfs als ze worden weergegeven in een opgenomen groep.

## <a name="at-work-networks"></a>'Op het werk' netwerken
Regels voor voorwaardelijke toegang met een netwerk 'op het werk' afhankelijk zijn van vertrouwde IP-adresbereiken die zijn geconfigureerd in Azure AD of het gebruik van Hallo 'binnen corpnet' claim vanaf AD FS. Deze regelgeving omvat:

* Meervoudige authenticatie niet op het werk
* De toegang niet op het werk blokkeren

Opties voor het opgeven 'op het werk' netwerken

1. Configureren van vertrouwde IP-adresbereiken in Hallo [configuratiepagina multi-factorauthenticatie](../multi-factor-authentication/multi-factor-authentication-whats-next.md). Beleid voor voorwaardelijke toegang gebruikt op elke aanvraag en -token uitgifte tooevaluate verificatieregels Hallo geconfigureerd bereiken. 
2. Gebruik van Hallo binnen corpnet claim configureren, deze optie kan worden gebruikt met federatieve-adreslijsten, met AD FS. toolearn meer informatie over Hallo binnen corpnet claims, Zie [Tusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).


## <a name="rules-based-on-application-sensitivity"></a>Regels op basis van de toepassing gevoeligheid
Regels worden geconfigureerd per toepassing hello hoogwaardige services toobe beveiligd zonder enige impact op tooother toegangsservices toe. Regels voor voorwaardelijke toegang kunnen worden geconfigureerd op Hallo **configureren** tabblad van de toepassing hello. 

Regels die momenteel worden aangeboden:

* **Meervoudige authenticatie**
  
  * Alle gebruikers die dit beleid toegepast toowill is vereist tooauthenticate via multi-factor authentication-server ten minste één keer worden.
* **Meervoudige authenticatie niet op het werk**
  
  * Als dit beleid wordt toegepast, worden alle gebruikers vereiste toohave uitgevoerd multi-factor authentication-server ten minste eenmaal als ze toegang krijgen Hallo service vanaf een externe locatie niet werken tot. Als ze vanaf een locatie van de tooremote werk verplaatst, worden deze vereiste tooperform multifactor-verificatie bij het openen van Hallo-service.
* **De toegang niet op het werk blokkeren** 
  
  * Wanneer gebruikers van werk tooa externe locatie worden verplaatst, wordt deze geblokkeerd als Hallo 'Toegang niet op het werk blokkeren' beleid is toegepast toothem.  Ze worden opnieuw kunnen wanneer op een locatie werk toegang.

## <a name="related-topics"></a>Verwante onderwerpen
* [Toegang beveiligen tooOffice 365 en andere apps verbonden tooAzure Active Directory](active-directory-conditional-access.md)
* [Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)

