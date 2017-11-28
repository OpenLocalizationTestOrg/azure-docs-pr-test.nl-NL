---
title: Het configureren van een nieuwe toepassing met meerdere tenants | Microsoft Docs
description: Het configureren van eenmalige aanmelding voor een aangepaste toepassing ontwikkelt en registreren met Azure AD.
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
ms.openlocfilehash: 0fdc58d82d9cd2e7edac33cc5af4b98d2fd06c56
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-a-new-multi-tenant-application"></a><span data-ttu-id="ffa17-103">Het configureren van een nieuwe toepassing met meerdere tenants</span><span class="sxs-lookup"><span data-stu-id="ffa17-103">How to configure a new multi-tenant application</span></span>

<span data-ttu-id="ffa17-104">Federatieve eenmalige aanmelding (SSO) inschakelen in uw app wordt automatisch ingeschakeld wanneer federeren via Azure AD voor OpenID Connect, SAML 2.0 of WS Fed.</span><span class="sxs-lookup"><span data-stu-id="ffa17-104">Enabling federated single sign-on (SSO) in your app is automatically enabled when federating through Azure AD for OpenID Connect, SAML 2.0, or WS-Fed.</span></span> <span data-ttu-id="ffa17-105">Als uw eindgebruikers aan te melden ondanks dat al een bestaande sessie met Azure AD, is het waarschijnlijk dat uw app is mogelijk onjuist geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="ffa17-105">If your end users are having to sign in despite already having an existing session with Azure AD, it’s likely your app may be misconfigured.</span></span>

* <span data-ttu-id="ffa17-106">Als u van ADAL/MSAL gebruikmaakt, controleert u of u hebt **PromptBehavior** ingesteld op **automatisch** plaats **altijd**.</span><span class="sxs-lookup"><span data-stu-id="ffa17-106">If you’re using ADAL/MSAL, make sure you have **PromptBehavior** set to **Auto** rather than **Always**.</span></span>

* <span data-ttu-id="ffa17-107">Als u een mobiele app maakt, moet u mogelijk aanvullende configuraties brokered of niet-brokered eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="ffa17-107">If you’re building a mobile app, you may need additional configurations to enable brokered or non-brokered SSO.</span></span>

<span data-ttu-id="ffa17-108">Zie voor Android, [SSO naar Cross-App in Android inschakelen](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android).</span><span class="sxs-lookup"><span data-stu-id="ffa17-108">For Android, see [Enabling Cross App SSO in Android](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android).</span></span><br>

<span data-ttu-id="ffa17-109">Zie voor iOS, [SSO naar Cross-App in iOS inschakelen](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios).</span><span class="sxs-lookup"><span data-stu-id="ffa17-109">For iOS, see [Enabling Cross App SSO in iOS](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ffa17-110">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ffa17-110">Next steps</span></span>

[<span data-ttu-id="ffa17-111">Azure AD-SSO</span><span class="sxs-lookup"><span data-stu-id="ffa17-111">Azure AD SSO</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis)<br>

[<span data-ttu-id="ffa17-112">Kruislings SSO in Android-App inschakelen</span><span class="sxs-lookup"><span data-stu-id="ffa17-112">Enabling Cross App SSO in Android</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android)<br>

[<span data-ttu-id="ffa17-113">SSO naar Cross-App in iOS inschakelen</span><span class="sxs-lookup"><span data-stu-id="ffa17-113">Enabling Cross App SSO in iOS</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios)<br>

[<span data-ttu-id="ffa17-114">Integratie van Apps AzureAD</span><span class="sxs-lookup"><span data-stu-id="ffa17-114">Integrating Apps to AzureAD</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications)<br>

[<span data-ttu-id="ffa17-115">Toestemming en rollen voor AzureAD v2.0 geconvergeerde Apps</span><span class="sxs-lookup"><span data-stu-id="ffa17-115">Consent and Permissioning for AzureAD v2.0 converged Apps</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)<br>

[<span data-ttu-id="ffa17-116">AzureAD StackOverflow</span><span class="sxs-lookup"><span data-stu-id="ffa17-116">AzureAD StackOverflow</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
