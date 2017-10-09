---
title: aaaHow tooconfigure een nieuwe toepassing met meerdere tenants | Microsoft Docs
description: Hoe tooconfigure eenmalige aanmelding voor een aangepaste toepassing ontwikkeling en registreren met Azure AD.
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 4d3499d8885933516d6597fa9f87bcf88cd5a428
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-a-new-multi-tenant-application"></a>Hoe tooconfigure een nieuwe toepassing met meerdere tenants

Federatieve eenmalige aanmelding (SSO) inschakelen in uw app wordt automatisch ingeschakeld wanneer federeren via Azure AD voor OpenID Connect, SAML 2.0 of WS Fed. Als uw eindgebruikers toosign in ondanks dat al een bestaande sessie met Azure AD, is het waarschijnlijk dat uw app is mogelijk onjuist geconfigureerd.

* Als u van ADAL/MSAL gebruikmaakt, controleert u of u hebt **PromptBehavior** instellen te**automatisch** plaats **altijd**.

* Als u een mobiele app maakt, moet u mogelijk aanvullende configuraties tooenable brokered of niet-brokered eenmalige aanmelding.

Zie voor Android, [SSO naar Cross-App in Android inschakelen](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android).<br>

Zie voor iOS, [SSO naar Cross-App in iOS inschakelen](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios).

## <a name="next-steps"></a>Volgende stappen

[Azure AD-SSO](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis)<br>

[Kruislings SSO in Android-App inschakelen](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android)<br>

[SSO naar Cross-App in iOS inschakelen](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios)<br>

[Integratie van Apps tooAzureAD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications)<br>

[Toestemming en rollen voor AzureAD v2.0 geconvergeerde Apps](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)<br>

[AzureAD StackOverflow](http://stackoverflow.com/questions/tagged/azure-active-directory)
