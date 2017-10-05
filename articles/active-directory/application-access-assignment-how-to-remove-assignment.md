---
title: Het verwijderen van een gebruiker toegang tot een toepassing | Microsoft Docs
description: Begrijpen hoe een gebruiker toegang tot een toepassing te verwijderen
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
ms.openlocfilehash: 497429e7bf62f7e1d67ea429d6b858725f843688
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-remove-a-users-access-to-an-application"></a><span data-ttu-id="55899-103">Het verwijderen van een gebruiker toegang tot een toepassing</span><span class="sxs-lookup"><span data-stu-id="55899-103">How to remove a user's access to an application</span></span>

<span data-ttu-id="55899-104">In dit artikel helpt u bij het begrijpen hoe een gebruiker toegang tot een toepassing te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="55899-104">This article help you to understand how to remove a user's access to an application.</span></span>

## <a name="i-want-to-remove-a-specific-users-or-groups-assignment-to-an-application"></a><span data-ttu-id="55899-105">Ik wil een specifieke gebruiker of groep van toewijzing aan een toepassing verwijderen</span><span class="sxs-lookup"><span data-stu-id="55899-105">I want to remove a specific user’s or group’s assignment to an application</span></span>

<span data-ttu-id="55899-106">Als u wilt verwijderen van een gebruiker of groepstoewijzing aan een toepassing, volg de stappen in de [de toewijzing van een gebruiker of groep verwijderen uit een enterprise-app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) artikel.</span><span class="sxs-lookup"><span data-stu-id="55899-106">To remove a user or group assignment to an application, follow the steps listed in the [Remove a user or group assignment from an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) article.</span></span>

<span data-ttu-id="55899-107">. ## ik wil alle toegang tot een toepassing voor elke gebruiker uitschakelen</span><span class="sxs-lookup"><span data-stu-id="55899-107">.## I want to disable all access to an application for every user</span></span>

<span data-ttu-id="55899-108">Schakel alle gebruikersaanmeldingen tot een toepassing die de stappen die worden vermeld in de [gebruikersaanmeldingen een enterprise-App in Azure Active Directory uitschakelen](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) artikel.</span><span class="sxs-lookup"><span data-stu-id="55899-108">To disable all user sign-ins to an application, follow the steps listed in the [Disable user sign-ins for an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) article.</span></span>

## <a name="i-want-to-delete-an-application-entirely"></a><span data-ttu-id="55899-109">Ik wil een toepassing volledig verwijderen</span><span class="sxs-lookup"><span data-stu-id="55899-109">I want to delete an application entirely</span></span>

<span data-ttu-id="55899-110">Naar **verwijderen van een toepassing**, volgt u onderstaande instructies:</span><span class="sxs-lookup"><span data-stu-id="55899-110">To **delete an application**, follow the instructions below:</span></span>

1.  <span data-ttu-id="55899-111">Open de [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="55899-111">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="55899-112">Open de **Azure Active Directory-extensie** door te klikken op **meer services** onderaan in het navigatiemenu belangrijkste linkerkant.</span><span class="sxs-lookup"><span data-stu-id="55899-112">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="55899-113">Typ in **' Azure Active Directory**' in het zoekvak filter en selecteer de **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="55899-113">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="55899-114">Klik op **bedrijfstoepassingen** in het menu van Azure Active Directory linkerkant navigatie.</span><span class="sxs-lookup"><span data-stu-id="55899-114">Click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="55899-115">Klik op **alle toepassingen** om een lijst met al uw toepassingen weer te geven.</span><span class="sxs-lookup"><span data-stu-id="55899-115">Click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="55899-116">Als u de toepassing die u wilt weergeven die hier niet ziet, gebruikt u de **Filter** besturingselement aan de bovenkant van de **lijst met alle toepassingen** en stel de **weergeven** optie naar **alle toepassingen.**</span><span class="sxs-lookup"><span data-stu-id="55899-116">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="55899-117">Selecteer de toepassing die u wilt verwijderen.</span><span class="sxs-lookup"><span data-stu-id="55899-117">Select the application you want to delete.</span></span>

7.  <span data-ttu-id="55899-118">Nadat de toepassing wordt geladen, klikt u op **verwijderen** pictogram van de bovenste toepassing **overzicht** blade.</span><span class="sxs-lookup"><span data-stu-id="55899-118">Once the application loads, click **Delete** icon from the top application’s **Overview** blade.</span></span>

## <a name="i-want-to-disable-all-future-user-consent-operations-to-any-application"></a><span data-ttu-id="55899-119">Ik wil alle bewerkingen van toekomstige gebruikers toestemming voor elke toepassing uitschakelen</span><span class="sxs-lookup"><span data-stu-id="55899-119">I want to disable all future user consent operations to any application</span></span>

<span data-ttu-id="55899-120">Toestemming van de gebruiker uitschakelt voor uw hele directory te voorkomen dat eindgebruikers ermee akkoord dat elke toepassing.</span><span class="sxs-lookup"><span data-stu-id="55899-120">Disabling user consent for your entire directory prevent end users from consenting to any application.</span></span> <span data-ttu-id="55899-121">Beheerders kunnen nog steeds op behalves van de gebruiker toestemming.</span><span class="sxs-lookup"><span data-stu-id="55899-121">Administrators can still consent on user’s behalves.</span></span> <span data-ttu-id="55899-122">Meer informatie over de toepassing toestemming en waarom u niet wilt doen, of lezen [wat gebruikers- en toestemming van de beheerder](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).</span><span class="sxs-lookup"><span data-stu-id="55899-122">To learn more about application consent, and why you may or may not wish to do this, read [Understanding user and admin consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).</span></span>

<span data-ttu-id="55899-123">Naar **uitschakelen alle toekomstige gebruikers toestemming bewerkingen in uw hele directory**, volgt u onderstaande instructies:</span><span class="sxs-lookup"><span data-stu-id="55899-123">To **disable all future user consent operations in your entire directory**, follow the instructions below:</span></span>

1.  <span data-ttu-id="55899-124">Open de [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="55899-124">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="55899-125">Open de **Azure Active Directory-extensie** door te klikken op **meer services** onderaan in het navigatiemenu belangrijkste linkerkant.</span><span class="sxs-lookup"><span data-stu-id="55899-125">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="55899-126">Typ in **' Azure Active Directory**' in het zoekvak filter en selecteer de **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="55899-126">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="55899-127">Klik op **gebruikers en groepen** in het navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="55899-127">Click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="55899-128">Klik op **gebruikersinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="55899-128">Click **User settings**.</span></span>

6.  <span data-ttu-id="55899-129">Alle toekomstige gebruikers toestemming bewerkingen uitschakelen door in te stellen de **gebruikers kunnen toestaan dat apps toegang tot hun gegevens** in-of uitschakelen op **Nee** en klik op de **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="55899-129">Disable all future user consent operations by setting the **Users can allow apps to access their data** toggle to **No** and click the **Save** button.</span></span>


# <a name="next-steps"></a><span data-ttu-id="55899-130">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="55899-130">Next steps</span></span>
[<span data-ttu-id="55899-131">Toegang tot apps beheren</span><span class="sxs-lookup"><span data-stu-id="55899-131">Managing access to apps</span></span>](active-directory-managing-access-to-apps.md)
