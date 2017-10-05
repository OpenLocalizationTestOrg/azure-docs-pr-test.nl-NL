---
title: Problemen met aanmelden bij een toepassing ontwikkelde aangepaste | Microsoft Docs
description: Algemene rrors die kan worden veroorzaakt door u niet kunt aanmelden bij een toepassing die u hebt ontwikkeld met Azure AD
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
ms.openlocfilehash: b0df23e040a73d18968f547eef7347f14cc577c6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="problems-signing-in-to-an-custom-developed-application"></a><span data-ttu-id="63e09-103">Problemen met aanmelden bij een toepassing ontwikkelde aangepaste</span><span class="sxs-lookup"><span data-stu-id="63e09-103">Problems signing in to an custom-developed application</span></span>

<span data-ttu-id="63e09-104">Er zijn verschillende fouten die kunnen worden veroorzaakt door u niet kunt aanmelden bij een app.</span><span class="sxs-lookup"><span data-stu-id="63e09-104">There are several errors that could be causing you to not be able to sign into an app.</span></span> <span data-ttu-id="63e09-105">De belangrijkste reden mensen optreden die dit probleem is onjuist geconfigureerd apps.</span><span class="sxs-lookup"><span data-stu-id="63e09-105">The biggest reason people encounter this problem is misconfigured apps.</span></span>

## <a name="errors-related-to--misconfigured-apps"></a><span data-ttu-id="63e09-106">Fouten met betrekking tot onjuist geconfigureerde apps</span><span class="sxs-lookup"><span data-stu-id="63e09-106">Errors related to  misconfigured apps</span></span>

* <span data-ttu-id="63e09-107">Controleer of zowel de configuraties in de portal overeenkomen met wat u hebt in uw app.</span><span class="sxs-lookup"><span data-stu-id="63e09-107">Verify both the configurations in the portal match what you have in your app.</span></span> <span data-ttu-id="63e09-108">In het bijzonder vergelijken Client-toepassing-ID, antwoord-URL's, Clientcodes geheimen en App-ID-URI.</span><span class="sxs-lookup"><span data-stu-id="63e09-108">Specifically, compare Client/Application ID, Reply URLs, Client Secrets/Keys, and App ID URI.</span></span>

* <span data-ttu-id="63e09-109">Vergelijk de resource die u bij het aanvragen van toegang tot in de code met de geconfigureerde machtigingen in de **vereiste Resources** tabblad om ervoor te zorgen dat u resources die u hebt geconfigureerd voor het alleen aanvragen.</span><span class="sxs-lookup"><span data-stu-id="63e09-109">Compare the resource you’re requesting access to in code with the configured permissions in the **Required Resources** tab to make sure you only request resources you’ve configured.</span></span>

* <span data-ttu-id="63e09-110">Zie [Azure AD StackOverflow](http://stackoverflow.com/questions/tagged/azure-active-directory) voor vergelijkbare fouten of problemen.</span><span class="sxs-lookup"><span data-stu-id="63e09-110">See [Azure AD StackOverflow](http://stackoverflow.com/questions/tagged/azure-active-directory) for any similar errors or problems.</span></span>

## <a name="next-steps"></a><span data-ttu-id="63e09-111">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="63e09-111">Next steps</span></span>

[<span data-ttu-id="63e09-112">Ontwikkelaarshandleiding voor Azure AD</span><span class="sxs-lookup"><span data-stu-id="63e09-112">Azure AD Developer Guide</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide)<br>

[<span data-ttu-id="63e09-113">Toestemming en het integreren van Apps naar Azure AD</span><span class="sxs-lookup"><span data-stu-id="63e09-113">Consent and Integrating Apps to Azure AD</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications>)<br>

[<span data-ttu-id="63e09-114">Toestemming en rollen voor Azure AD v2.0 geconvergeerde Apps</span><span class="sxs-lookup"><span data-stu-id="63e09-114">Consent and Permissioning for Azure AD v2.0 converged Apps</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)<br>

[<span data-ttu-id="63e09-115">Azure AD-StackOverflow</span><span class="sxs-lookup"><span data-stu-id="63e09-115">Azure AD StackOverflow</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory>)
