---
title: aaaChoose tussen Azure MFA-cloud of server | Microsoft Docs
description: Kies Hallo multi-factor authentication-beveiligingsoplossing die geschikt is voor u door het, wat wil ik het toosecure en waar zich Mijn gebruikers zich bevinden.  Kies vervolgens de cloud, MFA-Server of AD FS.
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: ec2270ea-13d7-4ebc-8a00-fa75ce6c746d
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/23/2017
ms.author: kgremban
ms.openlocfilehash: bd9639e5f744f586d9143c6e90b105ed645eecb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="choose-hello-azure-multi-factor-authentication-solution-for-you"></a>Kies hello Azure multi-factor Authentication-oplossing voor u
Omdat er verschillende versies van Azure multi-factor Authentication (MFA), moet we enkele vragen toofigure controleren welke versie is de juiste één toouse Hallo beantwoorden.  Deze vragen zijn:

* [Wat heb ik toosecure geprobeerd](#what-am-i-trying-to-secure)
* [Waar bevinden de Hallo gebruikers zich](#where-are-the-users-located)
* [Welke functies heb ik nodig?](#what-featured-do-i-need)

Hallo volgende secties bevatten richtlijnen voor het vaststellen van elk van deze antwoorden.

## <a name="what-am-i-trying-toosecure"></a>Wat heb ik toosecure geprobeerd?
toodetermine hello juist in twee stappen verificatie oplossing eerst moeten we Hallo vraag van wat u tijdens het toosecure met een tweede methode voor verificatie zijn beantwoord.  Is het een toepassing die deel uitmaakt van Azure?  Of een systeem met externe toegang?  Door te bepalen wat we proberen toosecure, kunnen we Hallo vraag waarin multi-factor Authentication toobe ingeschakeld moet beantwoorden.  

| Wat zijn u tijdens het toosecure | MFA in de cloud Hallo | MFA-server |
| --- |:---:|:---:|
| Eigen Microsoft-apps |● |● |
| SaaS-apps in app-galerie Hallo |● |  |
| Webtoepassingen die zijn gepubliceerd via de toepassingsproxy van Azure AD |● |  |
| IIS-toepassingen die niet zijn gepubliceerd via toepassingsproxy van Azure AD | |● |
| Externe toegang zoals VPN, RDG | ● | ● |

## <a name="where-are-hello-users-located"></a>Waar bevinden de Hallo gebruikers zich
Vervolgens kijken waar onze gebruikers zich bevinden toodetermine Hallo juiste oplossing toouse kunt of in Hallo cloud of on-premises met Hallo MFA-Server.

| Locatie van gebruikers | MFA in de cloud Hallo | MFA-server |
| --- |:---:|:---:|
| Azure Active Directory |● | |
| Azure AD en on-premises AD dat gebruikmaakt van federatie met AD FS |● |● |
| Azure AD en on-premises AD dat gebruikmaakt van DirSync, Azure AD Sync, Azure AD Connect - geen wachtwoordsynchronisatie |● |● |
| Azure AD en on-premises AD dat gebruikmaakt van DirSync, Azure AD Sync, Azure AD Connect - met wachtwoordsynchronisatie |● | |
| On-premises Active Directory | |● |

## <a name="what-features-do-i-need"></a>Welke functies heb ik nodig?
Hallo vergelijkt volgende tabel Hallo-functies die beschikbaar met multi-factor Authentication in de cloud Hallo en Hello multi-factor Authentication-Server zijn.

| Functie | MFA in de cloud Hallo | MFA-server |
| --- |:---:|:---:|
| Meldingen op mobiele app als een tweede factor | ● | ● |
| Een verificatiecode op mobiele app als een tweede factor | ● | ● |
| Telefoonoproep als tweede factor | ● | ● |
| Sms in één richting als tweede factor | ● | ● |
| Sms in twee richtingen als tweede factor | | ● |
| Hardwaretokens als tweede factor | | ● |
| App-wachtwoorden voor Office 365-clients die geen ondersteuning voor MFA bieden | ● | |
| Beheerdercontrole over verificatiemethoden | ● | ● |
| Pincodemodus | | ● |
| Fraudewaarschuwing |● | ● |
| MFA-rapporten |● | ● |
| Eenmalige toegang | | ● |
| Aangepaste begroeting voor telefoongesprekken | ● | ● |
| Aanpasbare nummerweergave voor telefoongesprekken | ● | ● |
| Goedgekeurde IP-adressen | ● | ● |
| MFA herinneren voor vertrouwde apparaten | ● | |
| Voorwaardelijke toegang | ● | ● |
| Cache |  | ● |

## <a name="next-steps"></a>Volgende stappen

Nu dat we hebben vastgesteld of toouse cloud multi-factor authentication-server of Hallo MFA-Server on-premises, we aan de slag kunt instellen en gebruiken van Azure multi-factor Authentication. **Hallo pictogram voor uw scenario selecteren**

<center>




[![Cloud](./media/multi-factor-authentication-get-started/cloud2.png)](multi-factor-authentication-get-started-cloud.md)  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[![Server](./media/multi-factor-authentication-get-started/server2.png)](multi-factor-authentication-get-started-server.md) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </center>
