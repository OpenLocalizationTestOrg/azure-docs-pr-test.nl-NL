---
title: aaaHow tooAssign gebruikers tooapplications | Microsoft Docs
description: Begrijpen hoe gebruikers tooan toepassing in uw tenant worden toegewezen
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
ms.openlocfilehash: 4df60c7d723140d0d1bbd6ba8b34aa4e762d1138
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooassign-users-tooapplications"></a><span data-ttu-id="8513e-103">Hoe tooassign gebruikers tooapplications</span><span class="sxs-lookup"><span data-stu-id="8513e-103">How tooassign users tooapplications</span></span>

<span data-ttu-id="8513e-104">In dit artikel kunt u toounderstand hoe gebruikers tooan toepassing in uw tenant worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="8513e-104">This article help you toounderstand how users get assigned tooan application in your tenant.</span></span>

## <a name="how-do-users-get-assigned-tooan-application-in-azure-ad"></a><span data-ttu-id="8513e-105">Hoe gebruikers worden toegewezen tooan toepassing in Azure AD?</span><span class="sxs-lookup"><span data-stu-id="8513e-105">How do users get assigned tooan application in Azure AD?</span></span>

<span data-ttu-id="8513e-106">Voor een gebruiker tooaccess een toepassing, moet eerst worden toegewezen tooit op een bepaalde manier.</span><span class="sxs-lookup"><span data-stu-id="8513e-106">For a user tooaccess an application, they must first be assigned tooit in some way.</span></span> <span data-ttu-id="8513e-107">Toewijzing kan worden uitgevoerd door een beheerder, een zakelijke gemachtigde of soms Hallo gebruiker zelf.</span><span class="sxs-lookup"><span data-stu-id="8513e-107">Assignment can be performed by an administrator, a business delegate, or sometimes, hello user themselves.</span></span> <span data-ttu-id="8513e-108">Hieronder worden beschreven Hallo manieren gebruikers tooapplications kunnen worden toegewezen:</span><span class="sxs-lookup"><span data-stu-id="8513e-108">Below describes hello ways users can get assigned tooapplications:</span></span>

1.  <span data-ttu-id="8513e-109">Een beheerder [wijst een gebruiker](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) rechtstreeks toohello-toepassing</span><span class="sxs-lookup"><span data-stu-id="8513e-109">An administrator [assigns a user](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) toohello application directly</span></span>

2.  <span data-ttu-id="8513e-110">Een beheerder [wijst een groep](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) die Hallo gebruiker lid is van toepassing toohello, met inbegrip van:</span><span class="sxs-lookup"><span data-stu-id="8513e-110">An administrator [assigns a group](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) that hello user is a member of toohello application, including:</span></span>

  * <span data-ttu-id="8513e-111">Een groep die on-premises is gesynchroniseerd</span><span class="sxs-lookup"><span data-stu-id="8513e-111">A group that was synchronized from on-premises</span></span>

  * <span data-ttu-id="8513e-112">Een statische beveiligingsgroep gemaakt in de cloud Hallo</span><span class="sxs-lookup"><span data-stu-id="8513e-112">A static security group created in hello cloud</span></span>

  * <span data-ttu-id="8513e-113">Een [dynamische beveiligingsgroep](https://docs.microsoft.com/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal) gemaakt in de cloud Hallo</span><span class="sxs-lookup"><span data-stu-id="8513e-113">A [dynamic security group](https://docs.microsoft.com/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal) created in hello cloud</span></span>

  * <span data-ttu-id="8513e-114">Een Office 365-groep gemaakt in de cloud Hallo</span><span class="sxs-lookup"><span data-stu-id="8513e-114">An Office 365 group created in hello cloud</span></span>

  * <span data-ttu-id="8513e-115">Hallo [alle gebruikers](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-dedicated-groups) groep</span><span class="sxs-lookup"><span data-stu-id="8513e-115">hello [All Users](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-dedicated-groups) group</span></span>

3.  <span data-ttu-id="8513e-116">Een beheerder activeert [Self-service toegang tot de toepassing](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) tooallow een gebruiker tooadd wordt gebruikt door een toepassing hello [toepassing Toegangspaneel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **App toevoegen** functie **zonder goedkeuring van bedrijven**</span><span class="sxs-lookup"><span data-stu-id="8513e-116">An administrator enables [Self-service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) tooallow a user tooadd an application using hello [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Add App** feature **without business approval**</span></span>

4.  <span data-ttu-id="8513e-117">Een beheerder activeert [Self-service toegang tot de toepassing](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) tooallow een gebruiker tooadd wordt gebruikt door een toepassing hello [toepassing Toegangspaneel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **App toevoegen** onderdeel, maar alleen toestaan **ith voorafgaande goedkeuring van een geselecteerde verzameling business goedkeurders**</span><span class="sxs-lookup"><span data-stu-id="8513e-117">An administrator enables [Self-service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) tooallow a user tooadd an application using hello [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Add App** feature, but only w**ith prior approval from a selected set of business approvers**</span></span>

5.  <span data-ttu-id="8513e-118">Een beheerder activeert [groepsbeheer met Self-service](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) tooallow de toojoin van een gebruiker een groep die een toepassing is toegewezen, te**zonder goedkeuring van bedrijven**</span><span class="sxs-lookup"><span data-stu-id="8513e-118">An administrator enables [Self-service Group Management](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) tooallow a user toojoin a group that an application is assigned too**without business approval**</span></span>

6.  <span data-ttu-id="8513e-119">Een beheerder activeert [groepsbeheer met Self-service](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) tooallow de toojoin van een gebruiker een groep die een toepassing is toegewezen aan, maar alleen **met voorafgaande goedkeuring van een geselecteerde verzameling business goedkeurders**</span><span class="sxs-lookup"><span data-stu-id="8513e-119">An administrator enables [Self-service Group Management](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) tooallow a user toojoin a group that an application is assigned to, but only **with prior approval from a selected set of business approvers**</span></span>

7.  <span data-ttu-id="8513e-120">Een beheerder wijst een gebruiker van de licentie tooa rechtstreeks voor een eerste toepassing van derden, zoals [Microsoft Office 365](http://products.office.com/)</span><span class="sxs-lookup"><span data-stu-id="8513e-120">An administrator assigns a license tooa user directly for a first party application, like [Microsoft Office 365](http://products.office.com/)</span></span>

8.  <span data-ttu-id="8513e-121">Een beheerder wijst een licentiegroep tooa die Hallo gebruiker lid is van tooa eerste of een toepassing, zoals [Microsoft Office 365](http://products.office.com/)</span><span class="sxs-lookup"><span data-stu-id="8513e-121">An administrator assigns a license tooa group that hello user is a member of tooa first party application, like [Microsoft Office 365](http://products.office.com/)</span></span>

9.  <span data-ttu-id="8513e-122">Een [beheerder instemt tooan toepassing](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) toobe gebruikt door alle gebruikers en vervolgens een gebruiker zich aanmeldt toohello toepassing</span><span class="sxs-lookup"><span data-stu-id="8513e-122">An [administrator consents tooan application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) toobe used by all users and then a user signs in toohello application</span></span>

10. <span data-ttu-id="8513e-123">Een gebruiker [tooan toepassing instemt](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) zelf wanneer u zich aanmeldt in toohello toepassing</span><span class="sxs-lookup"><span data-stu-id="8513e-123">A user [consents tooan application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) themselves by signing in toohello application</span></span>

## <a name="next-steps"></a><span data-ttu-id="8513e-124">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8513e-124">Next steps</span></span>
[<span data-ttu-id="8513e-125">Toepassingen beheren met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8513e-125">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
