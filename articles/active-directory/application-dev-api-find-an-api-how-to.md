---
title: aaaHow toofind een specifieke API die nodig zijn voor een toepassing ontwikkelde aangepaste | Microsoft Docs
description: Hoe tooconfigure Hallo machtigingen die u nodig hebt tooaccess een bepaalde API in uw aangepaste ontwikkeld voor Azure AD-toepassing
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
ms.openlocfilehash: 7331129204d8b34b4ef9671749bd702f893768ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toofind-a-specific-api-needed-for-a-custom-developed-application"></a><span data-ttu-id="6105e-103">Hoe toofind een specifieke API die nodig zijn voor een toepassing ontwikkelde aangepaste</span><span class="sxs-lookup"><span data-stu-id="6105e-103">How toofind a specific API needed for a custom-developed application</span></span>

<span data-ttu-id="6105e-104">Toegang tooAPIs vereist configuratie van toegang bereikwaarden en functies.</span><span class="sxs-lookup"><span data-stu-id="6105e-104">Access tooAPIs require configuration of access scopes and roles.</span></span> <span data-ttu-id="6105e-105">Als u uw resource toepassing API's tooclient webtoepassingen tooexpose wilt, moet u tooconfigure toegangsbereiken en rollen voor Hallo API.</span><span class="sxs-lookup"><span data-stu-id="6105e-105">If you want tooexpose your resource application web APIs tooclient applications, you need tooconfigure access scopes and roles for hello API.</span></span> <span data-ttu-id="6105e-106">Als u wilt dat een client toepassing tooaccess een web-API, moet u tooconfigure machtigingen tooaccess Hallo API in app-registratie Hallo.</span><span class="sxs-lookup"><span data-stu-id="6105e-106">If you want a client application tooaccess a web API, you need tooconfigure permissions tooaccess hello API in hello app registration.</span></span>

## <a name="configuring-a-resource-application-tooexpose-web-apis"></a><span data-ttu-id="6105e-107">Configureren van een resource toepassing tooexpose-web-API 's</span><span class="sxs-lookup"><span data-stu-id="6105e-107">Configuring a resource application tooexpose web APIs</span></span>

<span data-ttu-id="6105e-108">Bij het blootstellen van uw web-API, Hallo API worden weergegeven in Hallo **selecteert u een API** lijst bij het toevoegen van machtigingen tooan app-registratie.</span><span class="sxs-lookup"><span data-stu-id="6105e-108">When you expose your web API, hello API be displayed in hello **Select an API** list when adding permissions tooan app registration.</span></span> <span data-ttu-id="6105e-109">toegangsbereiken tooadd, stappen Hallo die worden beschreven in [tooyour resource toepassing toegang toe te voegen scopes](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#adding-access-scopes-to-your-resource-application).</span><span class="sxs-lookup"><span data-stu-id="6105e-109">tooadd access scopes, follow hello steps outlined in [adding access scopes tooyour resource application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#adding-access-scopes-to-your-resource-application).</span></span>

## <a name="configuring-a-client-application-tooaccess-web-apis"></a><span data-ttu-id="6105e-110">Configureren van een client toepassing tooaccess-web-API 's</span><span class="sxs-lookup"><span data-stu-id="6105e-110">Configuring a client application tooaccess web APIs</span></span>

<span data-ttu-id="6105e-111">Wanneer u de registratie van de app tooyour machtigingen toevoegt, kunt u **API toegang toevoegen** tooexposed web-API's.</span><span class="sxs-lookup"><span data-stu-id="6105e-111">When you add permissions tooyour app registration, you can **add API access** tooexposed web APIs.</span></span> <span data-ttu-id="6105e-112">tooaccess web-API's, Hallo stappen die worden beschreven in [toevoegen referenties of machtigingen tooaccess web-API's](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#to-add-credentials-or-permissions-to-access-web-apis).</span><span class="sxs-lookup"><span data-stu-id="6105e-112">tooaccess web APIs, follow hello steps outlined in [add credentials or permissions tooaccess web APIs](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#to-add-credentials-or-permissions-to-access-web-apis).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6105e-113">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6105e-113">Next steps</span></span>

-   [<span data-ttu-id="6105e-114">Toepassingen integreren met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6105e-114">Integrating applications with Azure Active Directory</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications)

-   [<span data-ttu-id="6105e-115">Understanding hello Azure Active Directory-toepassingsmanifest</span><span class="sxs-lookup"><span data-stu-id="6105e-115">Understanding hello Azure Active Directory application manifest</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-manifest)


