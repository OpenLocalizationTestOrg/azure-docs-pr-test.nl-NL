---
title: Onverwachte instemmingsprompt tijdens het aanmelden bij een toepassing | Microsoft Docs
description: "Wanneer een gebruiker ziet een toestemming wordt gevraagd een toepassing die hebt geïntegreerd met Azure AD dat u niet verwacht oplossen"
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
ms.openlocfilehash: e5b823e1251a7221f73efe6838d439f827f9665d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="unexpected-consent-prompt-when-signing-in-to-an-application"></a><span data-ttu-id="1ac2c-103">Onverwachte instemmingsprompt tijdens het aanmelden bij een toepassing</span><span class="sxs-lookup"><span data-stu-id="1ac2c-103">Unexpected consent prompt when signing in to an application</span></span>

<span data-ttu-id="1ac2c-104">Veel toepassingen die zijn geïntegreerd met Azure Active Directory vereisen machtigingen voor verschillende bronnen om te kunnen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="1ac2c-104">Many applications that integrate with Azure Active Directory require permissions to various resources in order to run.</span></span> <span data-ttu-id="1ac2c-105">Wanneer deze resources ook worden geïntegreerd met Azure Active Directory, toegang tot deze is aangevraagd met Azure AD toestemming framework.</span><span class="sxs-lookup"><span data-stu-id="1ac2c-105">When these resources are also integrated with Azure Active Directory, permissions to access them is requested using the Azure AD consent framework.</span></span> 

<span data-ttu-id="1ac2c-106">Dit resulteert in een toestemming vragen dat wordt weergegeven de eerste keer dat een toepassing wordt gebruikt, die vaak is een eenmalige bewerking.</span><span class="sxs-lookup"><span data-stu-id="1ac2c-106">This results in a consent prompt being shown the first time an application is used, which is often a one-time operation.</span></span> 

## <a name="scenarios-in-which-users-see-consent-prompts"></a><span data-ttu-id="1ac2c-107">Scenario's waarin gebruikers zien toestemming vragen</span><span class="sxs-lookup"><span data-stu-id="1ac2c-107">Scenarios in which users see consent prompts</span></span>

<span data-ttu-id="1ac2c-108">Aanvullende prompts kunnen worden verwacht in verschillende scenario's:</span><span class="sxs-lookup"><span data-stu-id="1ac2c-108">Additional prompts can be expected in various scenarios:</span></span>

* <span data-ttu-id="1ac2c-109">De reeks machtigingen die vereist zijn door de toepassing hebt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="1ac2c-109">The set of permissions required by the application have changed.</span></span>

* <span data-ttu-id="1ac2c-110">De gebruiker die oorspronkelijk wil de toepassing is niet een beheerder en nu de toepassing voor het eerst is gebruikt door de gebruiker van een andere (niet-beheerders).</span><span class="sxs-lookup"><span data-stu-id="1ac2c-110">The user who originally consented to the application was not an administrator, and now a different (non-admin) User is using the application for the first time.</span></span>

* <span data-ttu-id="1ac2c-111">De gebruiker die oorspronkelijk wil de toepassing is een beheerder, maar zij geen toestemming geven namens de hele organisatie.</span><span class="sxs-lookup"><span data-stu-id="1ac2c-111">The user who originally consented to the application was an administrator, but they did not consent on-behalf of the entire organization.</span></span>

* <span data-ttu-id="1ac2c-112">De toepassing gebruikmaakt van [incrementele en dynamische toestemming](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-compare#incremental-and-dynamic-consent) om aanvullende machtigingen nadat toestemming in eerste instantie is verleend.</span><span class="sxs-lookup"><span data-stu-id="1ac2c-112">The application is using [incremental and dynamic consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-compare#incremental-and-dynamic-consent) to request additional permissions after consent was initially granted.</span></span> <span data-ttu-id="1ac2c-113">Dit wordt vaak gebruikt als optionele functies van een toepassing extra machtigingen die vereist is voor basisfunctionaliteit niet vereist.</span><span class="sxs-lookup"><span data-stu-id="1ac2c-113">This is often used when optional features of an application additional require permissions beyond those required for baseline functionality.</span></span>

* <span data-ttu-id="1ac2c-114">Toestemming is ingetrokken na in eerste instantie wordt verleend.</span><span class="sxs-lookup"><span data-stu-id="1ac2c-114">Consent was revoked after being granted initially.</span></span>

* <span data-ttu-id="1ac2c-115">De toepassing gevraagd om bevestiging toestemming telkens wanneer deze wordt gebruikt door de ontwikkelaar is geconfigureerd (Opmerking: dit is niet aanbevolen).</span><span class="sxs-lookup"><span data-stu-id="1ac2c-115">The developer has configured the application to require a consent prompt every time it is used (note: this is not best practice).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1ac2c-116">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1ac2c-116">Next steps</span></span>

-   [<span data-ttu-id="1ac2c-117">Apps, machtigingen en toestemming in Azure Active Directory (v1.0 eindpunt)</span><span class="sxs-lookup"><span data-stu-id="1ac2c-117">Apps, permissions, and consent in Azure Active Directory (v1.0 endpoint)</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent)

-   [<span data-ttu-id="1ac2c-118">Scopes, machtigingen en toestemming in Azure Active Directory (v2.0-eindpunt)</span><span class="sxs-lookup"><span data-stu-id="1ac2c-118">Scopes, permissions, and consent in the Azure Active Directory (v2.0 endpoint)</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)


