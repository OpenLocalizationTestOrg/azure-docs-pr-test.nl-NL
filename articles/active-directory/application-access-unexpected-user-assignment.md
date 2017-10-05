---
title: Hoe gebruikers toewijzen voor toepassingen | Microsoft Docs
description: Begrijpen hoe gebruikers worden toegewezen aan een toepassing in uw tenant
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
ms.openlocfilehash: 916238ba402a2555bac620d7f08e02799d981ae0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-assign-users-to-applications"></a><span data-ttu-id="47eed-103">Gebruikers toewijzen aan toepassingen</span><span class="sxs-lookup"><span data-stu-id="47eed-103">How to assign users to applications</span></span>

<span data-ttu-id="47eed-104">In dit artikel helpt u bij het begrijpen hoe gebruikers worden toegewezen aan een toepassing in uw tenant.</span><span class="sxs-lookup"><span data-stu-id="47eed-104">This article help you to understand how users get assigned to an application in your tenant.</span></span>

## <a name="how-do-users-get-assigned-to-an-application-in-azure-ad"></a><span data-ttu-id="47eed-105">Hoe gebruikers worden toegewezen aan een toepassing in Azure AD?</span><span class="sxs-lookup"><span data-stu-id="47eed-105">How do users get assigned to an application in Azure AD?</span></span>

<span data-ttu-id="47eed-106">Voor een gebruiker toegang tot een toepassing, moeten ze eerst worden toegewezen aan deze op een bepaalde manier.</span><span class="sxs-lookup"><span data-stu-id="47eed-106">For a user to access an application, they must first be assigned to it in some way.</span></span> <span data-ttu-id="47eed-107">Toewijzing kan worden uitgevoerd door een beheerder, een gemachtigde bedrijven of soms wordt de gebruiker zelf.</span><span class="sxs-lookup"><span data-stu-id="47eed-107">Assignment can be performed by an administrator, a business delegate, or sometimes, the user themselves.</span></span> <span data-ttu-id="47eed-108">Beschrijving van de manieren waarop gebruikers kunnen worden toegewezen aan toepassingen hieronder:</span><span class="sxs-lookup"><span data-stu-id="47eed-108">Below describes the ways users can get assigned to applications:</span></span>

1.  <span data-ttu-id="47eed-109">Een beheerder [wijst een gebruiker](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) tot de toepassing rechtstreeks</span><span class="sxs-lookup"><span data-stu-id="47eed-109">An administrator [assigns a user](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) to the application directly</span></span>

2.  <span data-ttu-id="47eed-110">Een beheerder [wijst een groep](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) dat de gebruiker lid van de toepassing is, met inbegrip van:</span><span class="sxs-lookup"><span data-stu-id="47eed-110">An administrator [assigns a group](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) that the user is a member of to the application, including:</span></span>

  * <span data-ttu-id="47eed-111">Een groep die on-premises is gesynchroniseerd</span><span class="sxs-lookup"><span data-stu-id="47eed-111">A group that was synchronized from on-premises</span></span>

  * <span data-ttu-id="47eed-112">Een statische beveiligingsgroep gemaakt in de cloud</span><span class="sxs-lookup"><span data-stu-id="47eed-112">A static security group created in the cloud</span></span>

  * <span data-ttu-id="47eed-113">Een [dynamische beveiligingsgroep](https://docs.microsoft.com/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal) gemaakt in de cloud</span><span class="sxs-lookup"><span data-stu-id="47eed-113">A [dynamic security group](https://docs.microsoft.com/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal) created in the cloud</span></span>

  * <span data-ttu-id="47eed-114">Een Office 365-groep gemaakt in de cloud</span><span class="sxs-lookup"><span data-stu-id="47eed-114">An Office 365 group created in the cloud</span></span>

  * <span data-ttu-id="47eed-115">De [alle gebruikers](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-dedicated-groups) groep</span><span class="sxs-lookup"><span data-stu-id="47eed-115">The [All Users](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-dedicated-groups) group</span></span>

3.  <span data-ttu-id="47eed-116">Een beheerder activeert [Self-service toegang tot de toepassing](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) om toe te staan om toe te voegen met een toepassing met behulp van een gebruiker de [toepassing Toegangspaneel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **App toevoegen** functie **zonder goedkeuring van bedrijven**</span><span class="sxs-lookup"><span data-stu-id="47eed-116">An administrator enables [Self-service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) to allow a user to add an application using the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Add App** feature **without business approval**</span></span>

4.  <span data-ttu-id="47eed-117">Een beheerder activeert [Self-service toegang tot de toepassing](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) om toe te staan om toe te voegen met een toepassing met behulp van een gebruiker de [toepassing Toegangspaneel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **App toevoegen** onderdeel, maar alleen w**ith voorafgaande goedkeuring van een geselecteerde verzameling business goedkeurders**</span><span class="sxs-lookup"><span data-stu-id="47eed-117">An administrator enables [Self-service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) to allow a user to add an application using the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Add App** feature, but only w**ith prior approval from a selected set of business approvers**</span></span>

5.  <span data-ttu-id="47eed-118">Een beheerder activeert [groepsbeheer met Self-service](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) zodat een gebruiker lid worden van een groep die een toepassing is toegewezen aan **zonder goedkeuring van bedrijven**</span><span class="sxs-lookup"><span data-stu-id="47eed-118">An administrator enables [Self-service Group Management](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) to allow a user to join a group that an application is assigned to **without business approval**</span></span>

6.  <span data-ttu-id="47eed-119">Een beheerder activeert [groepsbeheer met Self-service](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) zodat een gebruiker lid worden van een groep die een toepassing is toegewezen aan, maar alleen **met voorafgaande goedkeuring van een geselecteerde verzameling business goedkeurders**</span><span class="sxs-lookup"><span data-stu-id="47eed-119">An administrator enables [Self-service Group Management](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) to allow a user to join a group that an application is assigned to, but only **with prior approval from a selected set of business approvers**</span></span>

7.  <span data-ttu-id="47eed-120">Een beheerder een licentie toegewezen aan een gebruiker rechtstreeks voor een eerste toepassing van derden, zoals [Microsoft Office 365](http://products.office.com/)</span><span class="sxs-lookup"><span data-stu-id="47eed-120">An administrator assigns a license to a user directly for a first party application, like [Microsoft Office 365](http://products.office.com/)</span></span>

8.  <span data-ttu-id="47eed-121">Een beheerder een licentie aan een groep toewijst die de gebruiker lid is van een eerste toepassing van derden, zoals is [Microsoft Office 365](http://products.office.com/)</span><span class="sxs-lookup"><span data-stu-id="47eed-121">An administrator assigns a license to a group that the user is a member of to a first party application, like [Microsoft Office 365](http://products.office.com/)</span></span>

9.  <span data-ttu-id="47eed-122">Een [beheerder instemt met een toepassing](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) moet worden gebruikt door alle gebruikers en vervolgens een gebruiker zich aanmeldt bij de toepassing</span><span class="sxs-lookup"><span data-stu-id="47eed-122">An [administrator consents to an application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) to be used by all users and then a user signs in to the application</span></span>

10. <span data-ttu-id="47eed-123">Een gebruiker [instemt met een toepassing](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) zich aanmeldt bij de toepassing</span><span class="sxs-lookup"><span data-stu-id="47eed-123">A user [consents to an application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) themselves by signing in to the application</span></span>

## <a name="next-steps"></a><span data-ttu-id="47eed-124">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="47eed-124">Next steps</span></span>
[<span data-ttu-id="47eed-125">Toepassingen beheren met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="47eed-125">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
