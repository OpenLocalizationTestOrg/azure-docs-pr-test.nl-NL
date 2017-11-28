---
title: aaaAssign groepen tooAzure AD-apps | Microsoft-Docs
description: Hoe tooimplement groepstoewijzing voor Azure-toepassingen.
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
ms.openlocfilehash: 086619df09c13bf259afc3128d45ed804b99e519
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="assign-azure-active-directory-groups-tooan-application"></a><span data-ttu-id="65f42-103">Azure Active Directory-groepen tooan toepassing toewijzen</span><span class="sxs-lookup"><span data-stu-id="65f42-103">Assign Azure Active Directory groups tooan application</span></span>
<span data-ttu-id="65f42-104">Voordat u gebruikers en groepen tooan toepassing toewijzen kunt, moet u de toewijzing van gebruiker vereisen.</span><span class="sxs-lookup"><span data-stu-id="65f42-104">Before you can assign users and groups tooan application, you must require user assignment.</span></span> <span data-ttu-id="65f42-105">toolearn hoe toorequire Gebruikerstoewijzing, Zie Hallo [Gebruikerstoewijzing vereisen](active-directory-applications-guiding-developers-requiring-user-assignment.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="65f42-105">toolearn how toorequire user assignment, see hello [Requiring User Assignment](active-directory-applications-guiding-developers-requiring-user-assignment.md) article.</span></span>

<span data-ttu-id="65f42-106">In dit artikel wordt ervan uitgegaan dat u groepen in Hallo active directory die u voor deze toepassing gebruikt al hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="65f42-106">This article assumes that you have already created groups in hello active directory you are using for this application.</span></span>

## <a name="assigning-groups-tooan-application"></a><span data-ttu-id="65f42-107">Groepen tooan toepassing toewijzen</span><span class="sxs-lookup"><span data-stu-id="65f42-107">Assigning Groups tooan Application</span></span>
1. <span data-ttu-id="65f42-108">Meld u bij toohello Azure-portal met een administratoraccount.</span><span class="sxs-lookup"><span data-stu-id="65f42-108">Log in toohello Azure portal with an administrator account.</span></span>
2. <span data-ttu-id="65f42-109">Klik op Hallo **alle Items** item in het hoofdmenu Hallo.</span><span class="sxs-lookup"><span data-stu-id="65f42-109">Click on hello **All Items** item in hello main menu.</span></span>
3. <span data-ttu-id="65f42-110">Hallo-map die u voor de toepassing hello gebruikt te kiezen.</span><span class="sxs-lookup"><span data-stu-id="65f42-110">Choose hello directory you are using for hello application.</span></span>
4. <span data-ttu-id="65f42-111">Klik op Hallo **toepassingen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="65f42-111">Click on hello **APPLICATIONS** tab.</span></span>
5. <span data-ttu-id="65f42-112">Selecteer Hallo-toepassing uit het Hallo-lijst met toepassingen die zijn gekoppeld aan deze map.</span><span class="sxs-lookup"><span data-stu-id="65f42-112">Select hello application from hello list of applications associated with this directory.</span></span>
6. <span data-ttu-id="65f42-113">Klik op Hallo **gebruikers en groepen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="65f42-113">Click hello **USERS AND GROUPS** tab.</span></span>
7. <span data-ttu-id="65f42-114">Hallo-filterlijst van groepen in uw active directory via Hallo **groepen** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="65f42-114">Filter hello list of groups in your active directory by using hello **Groups** dropdown list.</span></span>
8. <span data-ttu-id="65f42-115">Hallo groep selecteren.</span><span class="sxs-lookup"><span data-stu-id="65f42-115">Select hello group.</span></span>
9. <span data-ttu-id="65f42-116">Klik op **toewijzen**.</span><span class="sxs-lookup"><span data-stu-id="65f42-116">Click **ASSIGN**.</span></span>
10. <span data-ttu-id="65f42-117">Klik op **Ja** wanneer u wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="65f42-117">Click **yes** when prompted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="65f42-118">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="65f42-118">Next Steps</span></span>
[!INCLUDE [active-directory-applications-guiding-developers-for-lob-applications-toc.md](../../includes/active-directory-applications-guiding-developers-for-lob-applications-toc.md)]
