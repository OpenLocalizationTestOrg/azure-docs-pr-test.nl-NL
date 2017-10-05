---
title: Technische documentatie van Azure Active Directory voorwaardelijke toegang | Microsoft Docs
description: "Met voorwaardelijk toegangsbeheer controleert de Azure Active Directory de specifieke voorwaarden die u kiest bij het verifiëren van de gebruiker en alvorens deze toegang tot de toepassing. Als deze voorwaarden is voldaan, wordt de gebruiker geverifieerd en toegang te krijgen tot de toepassing."
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
ms.openlocfilehash: ca16a5399f94fd1ab267e0798cade3fd83f75b13
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-conditional-access-technical-reference"></a>Technische documentatie van Azure Active Directory voorwaardelijke toegang

## <a name="services-enabled-with-conditional-access"></a>Services met voorwaardelijke toegang ingeschakeld

Regels voor voorwaardelijke toegang worden ondersteund tussen de verschillende typen voor Azure AD-toepassing. Deze lijst bevat:


* Toepassingen die zijn geregistreerd bij de toepassingsproxy van Azure
* Azure RemoteApp
* Ontwikkelde line-of-business- en multitenant-toepassingen die zijn geregistreerd bij Azure AD
* Dynamics CRM
* Federatieve toepassingen uit de galerie van Azure AD-toepassing
* Microsoft Office 365 Yammer
* Microsoft Office 365 Exchange Online
* Microsoft Office 365 SharePoint Online (inclusief OneDrive voor bedrijven)
* Microsoft Power BI 
* Wachtwoord SSO-toepassingen uit de galerie van Azure AD-toepassing
* Visual Studio Team Services
* Microsoft Teams









## <a name="enable-access-rules"></a>Toegangsregels inschakelen
Elke regel worden ingeschakeld of uitgeschakeld voor een per toepassing basissen. Wanneer regels zijn **ON** wordt ingeschakeld en afgedwongen voor gebruikers die toegang tot de toepassing. Wanneer ze zijn **OFF** ze worden niet gebruikt en heeft geen invloed op de aanmeldingsprocedure gebruikers.

## <a name="applying-rules-to-specific-users"></a>Regels toepassen op specifieke gebruikers
Regels kunnen worden toegepast op bepaalde groepen gebruikers op basis van de beveiligingsgroep door in te stellen **toepassen op**. **Toepassen op** kan worden ingesteld op **alle gebruikers** of **groepen**. Als de waarde **alle gebruikers** regels geldt voor elke gebruiker met toegang tot de toepassing. De **groepen** optie specifieke beveiligings- en distributiegroepen worden geselecteerd, kunnen regels alleen afgedwongen voor deze groepen.

Bij het implementeren van een regel wordt het meestal eerst deze een beperkte set van gebruikers die lid van een pilot-groepen zijn toe te passen. Nadat de regel kan worden toegepast op **alle gebruikers**. Hierdoor wordt de regel moeten worden afgedwongen voor alle gebruikers in de organisatie.

Selecteer groepen kunnen ook worden vrijgesteld van beleid voor gebruik van de **behalve** optie. Leden van deze groepen worden vrijgesteld, zelfs als ze worden weergegeven in een opgenomen groep.

## <a name="at-work-networks"></a>'Op het werk' netwerken
Regels voor voorwaardelijke toegang met een netwerk 'op het werk' afhankelijk zijn van vertrouwde IP-adresbereiken die zijn geconfigureerd in Azure AD, of gebruik van de claim 'binnen corpnet' vanaf AD FS. Deze regelgeving omvat:

* Meervoudige authenticatie niet op het werk
* De toegang niet op het werk blokkeren

Opties voor het opgeven 'op het werk' netwerken

1. Configureren van vertrouwde IP-adresbereiken in de [configuratiepagina multi-factorauthenticatie](../multi-factor-authentication/multi-factor-authentication-whats-next.md). Beleid voor voorwaardelijke toegang gebruiken de geconfigureerde bereiken op elk authenticatie-aanvraag en de uitgifte van tokens voor regels evalueren. 
2. Gebruik van de binnen configureren corpnet claim deze optie kan worden gebruikt met federatieve-adreslijsten, met AD FS. Voor meer informatie over de binnen corpnet claims, Zie [Tusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).


## <a name="rules-based-on-application-sensitivity"></a>Regels op basis van de toepassing gevoeligheid
Regels worden geconfigureerd per toepassing zodat de hoogwaardige services zonder enige impact op de toegang tot andere services worden beveiligd. Regels voor voorwaardelijke toegang kunnen worden geconfigureerd op de **configureren** tabblad van de toepassing. 

Regels die momenteel worden aangeboden:

* **Meervoudige authenticatie**
  
  * Alle gebruikers die dit beleid wordt toegepast op worden te verifiëren via ten minste eenmaal meervoudige verificatie.
* **Meervoudige authenticatie niet op het werk**
  
  * Als dit beleid wordt toegepast, worden alle gebruikers moeten multi-factor authentication-server ten minste eenmaal hebt uitgevoerd als ze vanaf een externe locatie voor niet-werk toegang de service tot. Als ze van een werk naar externe locatie, worden ze vereist multifactor-verificatie uitvoeren bij het openen van de service.
* **De toegang niet op het werk blokkeren** 
  
  * Wanneer gebruikers naar een externe locatie van het werk verplaatsen, wordt deze geblokkeerd als het beleid 'Toegang niet op het werk blokkeren' op ze is toegepast.  Ze worden opnieuw kunnen wanneer op een locatie werk toegang.

## <a name="related-topics"></a>Verwante onderwerpen
* [Beveiligen van toegang tot Office 365 en andere apps die zijn verbonden met Azure Active Directory](active-directory-conditional-access.md)
* [Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)

