---
title: Groepen toewijzen aan Azure AD-apps | Microsoft-Docs
description: Klik hier voor meer informatie over het implementeren van de groepstoewijzing van de voor Azure-toepassingen.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: 
ms.assetid: 29b5ba89-a1c7-4f1f-a294-248a40106617
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: kgremban
ms.custom: H1Hack27Feb2017
robots: noindex
ms.openlocfilehash: e0b0b87a454db96747f024e81882fe83d62fdbe2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="assign-azure-active-directory-groups-to-an-application"></a><span data-ttu-id="a1348-103">Azure Active Directory-groepen toewijzen aan een toepassing</span><span class="sxs-lookup"><span data-stu-id="a1348-103">Assign Azure Active Directory groups to an application</span></span>
<span data-ttu-id="a1348-104">Voordat u gebruikers en groepen aan een toepassing toewijzen kunt, moet u de toewijzing van gebruiker vereisen.</span><span class="sxs-lookup"><span data-stu-id="a1348-104">Before you can assign users and groups to an application, you must require user assignment.</span></span> <span data-ttu-id="a1348-105">Zie voor informatie over het vereisen van de gebruiker is toegewezen, de [Gebruikerstoewijzing vereisen](active-directory-applications-guiding-developers-requiring-user-assignment.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="a1348-105">To learn how to require user assignment, see the [Requiring User Assignment](active-directory-applications-guiding-developers-requiring-user-assignment.md) article.</span></span>

<span data-ttu-id="a1348-106">In dit artikel wordt ervan uitgegaan dat u groepen in de active directory die u voor deze toepassing gebruikt al hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a1348-106">This article assumes that you have already created groups in the active directory you are using for this application.</span></span>

## <a name="assigning-groups-to-an-application"></a><span data-ttu-id="a1348-107">Groepen toewijzen aan een toepassing</span><span class="sxs-lookup"><span data-stu-id="a1348-107">Assigning Groups to an Application</span></span>
1. <span data-ttu-id="a1348-108">Aanmelden bij de Azure-portal met een administratoraccount.</span><span class="sxs-lookup"><span data-stu-id="a1348-108">Log in to the Azure portal with an administrator account.</span></span>
2. <span data-ttu-id="a1348-109">Klik op de **alle Items** item in het hoofdmenu.</span><span class="sxs-lookup"><span data-stu-id="a1348-109">Click on the **All Items** item in the main menu.</span></span>
3. <span data-ttu-id="a1348-110">Kies de map die u voor de toepassing gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a1348-110">Choose the directory you are using for the application.</span></span>
4. <span data-ttu-id="a1348-111">Klik op de **toepassingen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="a1348-111">Click on the **APPLICATIONS** tab.</span></span>
5. <span data-ttu-id="a1348-112">Selecteer de toepassing uit de lijst met toepassingen die zijn gekoppeld aan deze map.</span><span class="sxs-lookup"><span data-stu-id="a1348-112">Select the application from the list of applications associated with this directory.</span></span>
6. <span data-ttu-id="a1348-113">Klik op de **gebruikers en groepen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="a1348-113">Click the **USERS AND GROUPS** tab.</span></span>
7. <span data-ttu-id="a1348-114">De lijst met groepen in uw active directory filteren met behulp van de **groepen** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="a1348-114">Filter the list of groups in your active directory by using the **Groups** dropdown list.</span></span>
8. <span data-ttu-id="a1348-115">Selecteer de groep.</span><span class="sxs-lookup"><span data-stu-id="a1348-115">Select the group.</span></span>
9. <span data-ttu-id="a1348-116">Klik op **toewijzen**.</span><span class="sxs-lookup"><span data-stu-id="a1348-116">Click **ASSIGN**.</span></span>
10. <span data-ttu-id="a1348-117">Klik op **Ja** wanneer u wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="a1348-117">Click **yes** when prompted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a1348-118">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a1348-118">Next Steps</span></span>
[!INCLUDE [active-directory-applications-guiding-developers-for-lob-applications-toc.md](../../includes/active-directory-applications-guiding-developers-for-lob-applications-toc.md)]
