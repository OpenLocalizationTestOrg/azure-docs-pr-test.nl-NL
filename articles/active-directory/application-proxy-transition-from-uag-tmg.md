---
title: aaaUpgrade tooAzure AD-toepassingsproxy | Microsoft Docs
description: Kies welke proxy-oplossing werkt het beste als u een van Microsoft Forefront of Unified Access-Gateway upgrade uitvoert.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 7dc2633140b384e25792470dadbb7f3fa7992a2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="compare-remote-access-solutions"></a>Oplossingen voor externe toegang vergelijken

Azure Active Directory-toepassingsproxy is een van twee oplossingen voor externe toegang die Microsoft aanbiedt. Hallo andere is Hallo on-premises versie van Web Application Proxy. Deze twee oplossingen voor eerdere producten die Microsoft aangeboden vervangen: Microsoft Forefront Threat Management Gateway (TMG) en Unified Access Gateway (UAG). Gebruik dit artikel toounderstand hoe deze oplossingen vier tooeach andere vergelijken. Voor de TMG of UAG oplossingen nog steeds via Hallo afgeschaft, gebruik dit artikel toohelp plan uw migratie tooone Hallo Application Proxy. 


## <a name="feature-comparison"></a>Vergelijking van functies

Gebruik deze tabel toounderstand hoe vergelijken tooeach andere Threat Management Gateway (TMG), Unified Access Gateway (UAG), Webtoepassingsproxyserver (WAP) en Azure AD Application Proxy (AP).

| Functie | TMG | UAG | WAP | AP |
| ------- | --- | --- | --- | --- |
| Verificatie via certificaat | Ja | Ja | - | - |
| Browser-apps selectief publiceren | Ja | Ja | Ja | Ja |
| Vooraf-verificatie en eenmalige aanmelding | Ja | Ja | Ja | Ja | 
| Laag-2/3-firewall | Ja | Ja | - | - |
| Proxy-mogelijkheden voor doorsturen | Ja | - | - | - |
| VPN-mogelijkheden | Ja | Ja | - | - |
| Uitgebreide protocolondersteuning | - | Ja | Ja, als via HTTP | Ja, als via HTTP of via Extern bureaublad-Gateway |
| Fungeert als AD FS-proxyserver | - | Ja | Ja | - |
| Een portal voor toegang tot toepassingen | - | Ja | - | Ja |
| Antwoord hoofdtekst koppeling vertaling | Ja | Ja | - | Ja | 
| Verificatie met koppen | - | Ja | - | Ja, met PingAccess | 
| Cloud-scale-beveiliging | - | - | - | Ja | 
| Voorwaardelijke toegang | - | Ja | - | Ja |
| Er zijn geen onderdelen in Hallo gedemilitariseerde zone (DMZ) | - | - | - | Ja |
| Er is geen binnenkomende verbindingen | - | - | - | Ja |

Voor de meeste scenario's, wordt aangeraden Azure AD-toepassing hello moderne oplossing. Web Application Proxy wordt alleen aanbevolen in scenario's waarvoor een proxyserver voor AD FS en u kunt geen aangepaste domeinen in Azure Active Directory gebruiken. 

Azure AD-toepassingsproxy biedt unieke voordelen wanneer vergeleken toosimilar producten, waaronder:

- Azure AD-tooon-premises resources uitbreiden
   - Cloud-scale beveiliging en bescherming
   - Functies zoals voorwaardelijke toegang en multi-factor Authentication zijn eenvoudige tooenable
- Er is geen component in Hallo gedemilitariseerde zone
- Er is geen inkomende verbindingen vereist
- Een toegangspaneel dat uw gebruikers kunnen gaan toofor alle bijbehorende toepassingen, inclusief O365, Azure AD-SaaS-apps geïntegreerde en uw on-premises web-apps. 


## <a name="next-steps"></a>Volgende stappen

- [Azure AD-toepassing tooprovide veilige externe toegang tooon-premises toepassingen gebruiken](active-directory-application-proxy-get-started.md)
- [Overgang van Forefront TMG en UAG tooApplication Proxy](https://blogs.technet.microsoft.com/isablog/2015/06/30/modernizing-microsoft-application-access-with-web-application-proxy-and-azure-active-directory-application-proxy/).
