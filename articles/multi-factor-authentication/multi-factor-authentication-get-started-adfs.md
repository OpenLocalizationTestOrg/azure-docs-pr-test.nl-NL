---
title: aaaTwo stap verificatie- en AD FS - Azure MFA | Microsoft Docs
description: Dit is hello Azure multi-factor authentication-pagina waarop wordt beschreven hoe tooget de slag met Azure MFA en AD FS.
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 44fbba68-6cf9-46c1-a9df-736580b68ae3
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/23/2017
ms.author: kgremban
ms.openlocfilehash: 7c1c925039d3cb753ba60e286168e5869faeae4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-multi-factor-authentication-and-active-directory-federation-services"></a>Aan de slag met Azure Multi-Factor Authentication en Active Directory Federation Services
<center>![Cloud](./media/multi-factor-authentication-get-started-adfs/adfs.png)</center>

Als uw organisatie met behulp van AD FS uw on-premises Active Directory heeft gefedereerd met Azure Active Directory, zijn er twee opties voor het gebruik van Azure Multi-Factor Authentication.

* Cloudresources beveiligen met Azure Multi-Factor Authentication of Active Directory Federation Services
* Cloudresources en on-premises resources beveiligen met behulp van de Azure Multi-Factor Authentication-server

Hallo volgende tabel geeft een overzicht van de verificatie-ervaring Hallo tussen het beveiligen van resources met Azure multi-factor Authentication en AD FS

| Verificatie-ervaring - op browser gebaseerde apps | Verificatie-ervaring - niet op browser gebaseerde apps |
|:--- |:--- |:--- |
| Beveiligen van Azure AD-resources met Azure Multi-Factor Authentication |<li>de eerste verificatiestap Hello wordt uitgevoerd on-premises met AD FS.</li> <li>Hallo tweede stap bestaat uit een telefonische methode die wordt uitgevoerd met cloudverificatie.</li> |
| Azure AD-resources beveiligen met behulp van Active Directory Federation Services |<li>de eerste verificatiestap Hello wordt uitgevoerd on-premises met AD FS.</li><li>de tweede stap Hallo is on-premises uitgevoerd door Hallo claim naleven.</li> |

Valkuilen met app-wachtwoorden voor federatieve gebruikers:

* App-wachtwoorden worden gecontroleerd met cloudverificatie en daarom worden federaties omzeild. Federatie wordt alleen actief gebruikt bij het instellen van het app-wachtwoord.
* On-premises instellingen voor toegangsbeheer van client worden niet herkend door app-wachtwoorden.
* U raakt on-premises mogelijkheden voor logboekregistratie bij verificatie voor app-wachtwoorden kwijt.
* Account uitschakelen/verwijderen kan duren voordat toothree uur voor directory-synchronisatie uitschakelen/verwijderen van app-wachtwoorden in de cloud-identiteit Hallo vertragen.

## <a name="next-steps"></a>Volgende stappen
Zie voor informatie over het instellen van Azure multi-factor Authentication of hello Azure multi-factor Authentication-Server met AD FS Hallo artikelen te volgen:

* [Cloudresources beveiligen met behulp van Azure Multi-Factor Authentication en AD FS](multi-factor-authentication-get-started-adfs-cloud.md)
* [Cloudresources en on-premises resources beveiligen met behulp van de Azure Multi-Factor Authentication-server met Windows Server 2012 R2 AD FS](multi-factor-authentication-get-started-adfs-w2k12.md)
* [Cloudresources en on-premises resources beveiligen met behulp van de Azure Multi-Factor Authentication-server met AD FS 2.0](multi-factor-authentication-get-started-adfs-adfs2.md)
