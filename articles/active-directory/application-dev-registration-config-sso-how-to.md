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
# <a name="how-tooconfigure-a-new-multi-tenant-application"></a><span data-ttu-id="4961a-103">Hoe tooconfigure een nieuwe toepassing met meerdere tenants</span><span class="sxs-lookup"><span data-stu-id="4961a-103">How tooconfigure a new multi-tenant application</span></span>

<span data-ttu-id="4961a-104">Federatieve eenmalige aanmelding (SSO) inschakelen in uw app wordt automatisch ingeschakeld wanneer federeren via Azure AD voor OpenID Connect, SAML 2.0 of WS Fed.</span><span class="sxs-lookup"><span data-stu-id="4961a-104">Enabling federated single sign-on (SSO) in your app is automatically enabled when federating through Azure AD for OpenID Connect, SAML 2.0, or WS-Fed.</span></span> <span data-ttu-id="4961a-105">Als uw eindgebruikers toosign in ondanks dat al een bestaande sessie met Azure AD, is het waarschijnlijk dat uw app is mogelijk onjuist geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="4961a-105">If your end users are having toosign in despite already having an existing session with Azure AD, it’s likely your app may be misconfigured.</span></span>

* <span data-ttu-id="4961a-106">Als u van ADAL/MSAL gebruikmaakt, controleert u of u hebt **PromptBehavior** instellen te**automatisch** plaats **altijd**.</span><span class="sxs-lookup"><span data-stu-id="4961a-106">If you’re using ADAL/MSAL, make sure you have **PromptBehavior** set too**Auto** rather than **Always**.</span></span>

* <span data-ttu-id="4961a-107">Als u een mobiele app maakt, moet u mogelijk aanvullende configuraties tooenable brokered of niet-brokered eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="4961a-107">If you’re building a mobile app, you may need additional configurations tooenable brokered or non-brokered SSO.</span></span>

<span data-ttu-id="4961a-108">Zie voor Android, [SSO naar Cross-App in Android inschakelen](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android).</span><span class="sxs-lookup"><span data-stu-id="4961a-108">For Android, see [Enabling Cross App SSO in Android](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android).</span></span><br>

<span data-ttu-id="4961a-109">Zie voor iOS, [SSO naar Cross-App in iOS inschakelen](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios).</span><span class="sxs-lookup"><span data-stu-id="4961a-109">For iOS, see [Enabling Cross App SSO in iOS](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4961a-110">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4961a-110">Next steps</span></span>

[<span data-ttu-id="4961a-111">Azure AD-SSO</span><span class="sxs-lookup"><span data-stu-id="4961a-111">Azure AD SSO</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis)<br>

[<span data-ttu-id="4961a-112">Kruislings SSO in Android-App inschakelen</span><span class="sxs-lookup"><span data-stu-id="4961a-112">Enabling Cross App SSO in Android</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android)<br>

[<span data-ttu-id="4961a-113">SSO naar Cross-App in iOS inschakelen</span><span class="sxs-lookup"><span data-stu-id="4961a-113">Enabling Cross App SSO in iOS</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios)<br>

[<span data-ttu-id="4961a-114">Integratie van Apps tooAzureAD</span><span class="sxs-lookup"><span data-stu-id="4961a-114">Integrating Apps tooAzureAD</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications)<br>

[<span data-ttu-id="4961a-115">Toestemming en rollen voor AzureAD v2.0 geconvergeerde Apps</span><span class="sxs-lookup"><span data-stu-id="4961a-115">Consent and Permissioning for AzureAD v2.0 converged Apps</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)<br>

[<span data-ttu-id="4961a-116">AzureAD StackOverflow</span><span class="sxs-lookup"><span data-stu-id="4961a-116">AzureAD StackOverflow</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
