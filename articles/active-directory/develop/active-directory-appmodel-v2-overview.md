---
title: Active Directory v2.0-eindpunt aaaAzure | Microsoft Docs
description: Een inleiding toobuilding apps met zowel Microsoft-Account en Azure Active Directory aanmelden.
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 2dee579f-fdf6-474b-bc2c-016c931eaa27
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: ae5946b02c50ae5a6137dc1decae66c96647e875
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-microsoft-account--azure-ad-users-in-a-single-app"></a>Meld u aan Microsoft-Account en Azure AD-gebruikers in een enkele app
In Hallo voorbij toepassingsontwikkelaar wie toosupport beide persoonlijke Microsoft-accounts wilde en werkaccounts van Azure Active Directory is vereist toointegrate met twee afzonderlijke systemen.  Hallo **Azure AD v2.0-eindpunt** introduceert een nieuwe authenticatie-API-versie waarmee u toosign in beide typen accounts met een eenvoudige integratie.  Apps die gebruikmaken van Hallo v2.0-eindpunt kunnen ook verbruiken, REST-API's Hallo [Microsoft Graph](https://graph.microsoft.io) met behulp van een type account.

## <a name="getting-started"></a>Aan de slag
Kies uw favoriete platform van Hallo lijst toobuild na een app met behulp van onze open-source bibliotheken en frameworks.  U kunt ook gebruik van onze OAuth 2.0 & OpenID Connect protocol documentatie toosend & protocolberichten rechtstreeks zonder met behulp van een bibliotheek auth ontvangen.

<br />

[!INCLUDE [active-directory-v2-quickstart-table](../../../includes/active-directory-v2-quickstart-table.md)]

## <a name="whats-new"></a>Wat is er nieuw
Hallo informatie hier erg nuttig zijn bij het begrijpen van wat is & Wat is niet mogelijk met Hallo v2.0-eindpunt.

* Meer informatie over Hallo [typen apps die u met Hallo v2.0-eindpunt bouwen kunt](active-directory-v2-flows.md).
* Hallo begrijpen [beperkingen, beperkingen en beperkingen](active-directory-v2-limitations.md) met Hallo v2.0-eindpunt.
* Bekijk deze video voor Hallo v2.0-eindpunt overzicht:

>[!VIDEO https://channel9.msdn.com/Events/Build/2017/P4031/player]

## <a name="reference"></a>Naslaginformatie
Deze koppelingen zijn handig voor het Hallo-platform in de diepte verkennen:

* [naslaginformatie over v2.0-Protocol](active-directory-v2-protocols.md)
* [v2.0 tokenverwijzing](active-directory-v2-tokens.md)
* [naslaginformatie over v2.0-bibliotheek](active-directory-v2-libraries.md)
* [Scopes en toestemming in Hallo v2.0-eindpunt](active-directory-v2-scopes.md)
* [Hallo Microsoft Graph](https://graph.microsoft.io)

## <a name="help--support"></a>Help en ondersteuning
Dit zijn Hallo beste locaties tooget helpen met het ontwikkelen op Azure Active Directory.

* [Stack Overflow's tags voor `azure-active-directory` en `adal`](http://stackoverflow.com/questions/tagged/azure-active-directory+or+adal)
* [Feedback op Azure Active Directory](https://feedback.azure.com/forums/169401-azure-active-directory/category/164757-developer-experiences)


> [!NOTE]
> Als u alleen toosign in werk- en schoolaccounts accounts van Azure Active Directory moet, moet u beginnen met onze [ontwikkelaarshandleiding Azure AD](active-directory-developers-guide.md).  Hallo v2.0-eindpunt is bedoeld voor gebruik door ontwikkelaars die expliciet toosign in persoonlijke Microsoft-accounts moeten.

