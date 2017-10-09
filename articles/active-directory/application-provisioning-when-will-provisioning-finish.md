---
title: aaaUser tooan Azure AD-galerie toepassing inrichting is nemen uur of langer | Microsoft Docs
description: Hoe toofind uit waarom inrichting tooyour toepassing langer dan u duurt verwacht
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
ms.openlocfilehash: 0658f041724c91ddd1997cc7759393b46680f13a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="user-provisioning-tooan-azure-ad-gallery-application-is-taking-hours-or-more"></a><span data-ttu-id="3b177-103">Gebruikers inrichten tooan Azure AD-galerie toepassing is nemen uur of meer</span><span class="sxs-lookup"><span data-stu-id="3b177-103">User provisioning tooan Azure AD Gallery application is taking hours or more</span></span>

<span data-ttu-id="3b177-104">Tijdens het inschakelen van automatische inrichting voor een toepassing, kan de initiële synchronisatie Hallo duren van 20 minuten tooseveral uren, afhankelijk van de grootte Hallo van hello Azure AD-directory en Hallo aantal gebruikers in het bereik voor het inrichten.</span><span class="sxs-lookup"><span data-stu-id="3b177-104">When first enabling automatic provisioning for an application, hello initial sync can take anywhere from 20 minutes tooseveral hours, depending on hello size of hello Azure AD directory and hello number of users in scope for provisioning.</span></span> 

<span data-ttu-id="3b177-105">Volgende synchronisaties na de initiële synchronisatie Hallo niet sneller als Hallo-service inricht watermerken waarbij Hallo status van beide systemen na de initiële synchronisatie hello, verbeterde prestaties van de volgende synchronisatie worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="3b177-105">Subsequent syncs after hello initial sync be faster, as hello provisioning service stores watermarks that represent hello state of both systems after hello initial sync, improving performance of subsequent syncs.</span></span>

## <a name="how-tooimprove-provisioning-performance"></a><span data-ttu-id="3b177-106">Hoe tooimprove prestaties inrichten</span><span class="sxs-lookup"><span data-stu-id="3b177-106">How tooimprove provisioning performance</span></span>

<span data-ttu-id="3b177-107">Als de initiële synchronisatie Hallo meer dan een paar uur duurt is, is er één dat u tooimprove prestaties kunt doen:</span><span class="sxs-lookup"><span data-stu-id="3b177-107">If hello initial sync is taking more than a few hours, there is one thing you can do tooimprove performance:</span></span>

-   <span data-ttu-id="3b177-108">**Gebruiker het bereik van de filters.**</span><span class="sxs-lookup"><span data-stu-id="3b177-108">**User scoping filters.**</span></span> <span data-ttu-id="3b177-109">Bereik filters kunt u toofine afstemmen Hallo gegevens die Hallo inrichting service uitgepakt vanuit Azure AD door het filteren van gebruikers op basis van specifieke kenmerkwaarden.</span><span class="sxs-lookup"><span data-stu-id="3b177-109">Scoping filters allow you toofine tune hello data that hello provisioning service extracts from Azure AD by filtering out users based on specific attribute values.</span></span> <span data-ttu-id="3b177-110">Zie voor meer informatie over het bereikfilters [inrichten van toepassing op basis van kenmerken met bereikfilters](https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters).</span><span class="sxs-lookup"><span data-stu-id="3b177-110">For more information on scoping filters, see [Attribute-based application provisioning with scoping filters](https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3b177-111">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3b177-111">Next steps</span></span>
[<span data-ttu-id="3b177-112">Automatisch gebruikers inrichten en Deprovisioning tooSaaS toepassingen met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3b177-112">Automate User Provisioning and Deprovisioning tooSaaS Applications with Azure Active Directory</span></span>](active-directory-saas-app-provisioning.md)

