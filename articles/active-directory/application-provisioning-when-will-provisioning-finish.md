---
title: Gebruikers inrichten tot een galerie van Azure AD-toepassing is nemen uur of langer | Microsoft Docs
description: Nagaan waarom het inrichten van uw toepassing duurt langer dan verwacht
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
ms.openlocfilehash: 183d60cbbbc8d02f7cd3cacc160453c45717ef0d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="user-provisioning-to-an-azure-ad-gallery-application-is-taking-hours-or-more"></a><span data-ttu-id="ffe5a-103">Nemen uur of meer is gebruikers inrichten tot een galerie van Azure AD-toepassing</span><span class="sxs-lookup"><span data-stu-id="ffe5a-103">User provisioning to an Azure AD Gallery application is taking hours or more</span></span>

<span data-ttu-id="ffe5a-104">Tijdens het inschakelen van automatische inrichting voor een toepassing, kan de eerste synchronisatie overal van 20 minuten tot enkele uren duren, afhankelijk van de grootte van de Azure AD-directory en het aantal gebruikers in het bereik voor het inrichten.</span><span class="sxs-lookup"><span data-stu-id="ffe5a-104">When first enabling automatic provisioning for an application, the initial sync can take anywhere from 20 minutes to several hours, depending on the size of the Azure AD directory and the number of users in scope for provisioning.</span></span> 

<span data-ttu-id="ffe5a-105">Volgende synchronisaties na de eerste synchronisatie worden sneller, omdat de inrichting service watermerken die de status van beide systemen na de eerste synchronisatie slaat, verbeterde prestaties van de volgende synchronisaties vertegenwoordigen.</span><span class="sxs-lookup"><span data-stu-id="ffe5a-105">Subsequent syncs after the initial sync be faster, as the provisioning service stores watermarks that represent the state of both systems after the initial sync, improving performance of subsequent syncs.</span></span>

## <a name="how-to-improve-provisioning-performance"></a><span data-ttu-id="ffe5a-106">Inrichting prestaties verbeteren</span><span class="sxs-lookup"><span data-stu-id="ffe5a-106">How to improve provisioning performance</span></span>

<span data-ttu-id="ffe5a-107">Als de eerste synchronisatie meer dan een paar uur duurt, is er één dat die u doen kunt om prestaties te verbeteren:</span><span class="sxs-lookup"><span data-stu-id="ffe5a-107">If the initial sync is taking more than a few hours, there is one thing you can do to improve performance:</span></span>

-   <span data-ttu-id="ffe5a-108">**Gebruiker het bereik van de filters.**</span><span class="sxs-lookup"><span data-stu-id="ffe5a-108">**User scoping filters.**</span></span> <span data-ttu-id="ffe5a-109">Bereik filters kunt u nauwkeurig afstemmen de gegevens die de inrichting service van Azure AD extraheert door het filteren van gebruikers op basis van specifieke kenmerkwaarden.</span><span class="sxs-lookup"><span data-stu-id="ffe5a-109">Scoping filters allow you to fine tune the data that the provisioning service extracts from Azure AD by filtering out users based on specific attribute values.</span></span> <span data-ttu-id="ffe5a-110">Zie voor meer informatie over het bereikfilters [inrichten van toepassing op basis van kenmerken met bereikfilters](https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters).</span><span class="sxs-lookup"><span data-stu-id="ffe5a-110">For more information on scoping filters, see [Attribute-based application provisioning with scoping filters](https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ffe5a-111">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ffe5a-111">Next steps</span></span>
[<span data-ttu-id="ffe5a-112">Gebruiker inrichting en het opheffen van inrichting voor SaaS-toepassingen met Azure Active Directory automatiseren</span><span class="sxs-lookup"><span data-stu-id="ffe5a-112">Automate User Provisioning and Deprovisioning to SaaS Applications with Azure Active Directory</span></span>](active-directory-saas-app-provisioning.md)

