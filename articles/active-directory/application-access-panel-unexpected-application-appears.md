---
title: aaaHow toepassingen worden weergegeven op het toegangsvenster Hallo | Microsoft Docs
description: Waarom een toepassing wordt weergegeven in het deelvenster toegang Hallo
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
ms.reviewr: japere
ms.openlocfilehash: 14ee732c4ed5260cba878e949cf9d90877aee67e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-applications-appear-on-hello-access-panel"></a><span data-ttu-id="a14b5-103">Hoe toepassingen worden weergegeven op het toegangsvenster Hallo</span><span class="sxs-lookup"><span data-stu-id="a14b5-103">How applications appear on hello access panel</span></span>

<span data-ttu-id="a14b5-104">Hallo Toegangspaneel is een portal op Internet waarmee een gebruiker met een werk of schoolaccount in Azure Active Directory (Azure AD) tooview en start cloud-gebaseerde toepassingen die hello Azure AD-beheerder heeft deze toegang verleend tot.</span><span class="sxs-lookup"><span data-stu-id="a14b5-104">hello Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) tooview and start cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="a14b5-105">Deze toepassingen zijn geconfigureerd namens de gebruiker Hallo in hello Azure AD-portal.</span><span class="sxs-lookup"><span data-stu-id="a14b5-105">These applications are configured on behalf of hello user in hello Azure AD portal.</span></span> <span data-ttu-id="a14b5-106">Hallo beheerder kunt inrichten Hallo toohello toepassingsgebruiker rechtstreeks of een gebruiker deel uitmaakt van het Hallo-toepassing die voorkomen op Hallo van de gebruiker Toegangsvenster waardoor tooa-groep.</span><span class="sxs-lookup"><span data-stu-id="a14b5-106">hello admin can provision hello application toohello user directly or tooa group a user is part of resulting in hello application appearing on hello user’s Access Panel.</span></span>

## <a name="general-issues-toocheck-first"></a><span data-ttu-id="a14b5-107">Algemene problemen toocheck eerst</span><span class="sxs-lookup"><span data-stu-id="a14b5-107">General issues toocheck first</span></span>

-   <span data-ttu-id="a14b5-108">Als een toepassing is verwijderd uit een gebruiker of groep Hallo gebruiker lid van is, opnieuw toosign in en uit in het toegangsvenster Hallo van de gebruiker na een paar minuten toosee als toepassing hello wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="a14b5-108">If an application was just removed from a user or group hello user is a member of, try toosign in and out again into hello user’s Access Panel after a few minutes toosee if hello application is removed.</span></span>

-   <span data-ttu-id="a14b5-109">Als u een licentie is verwijderd uit een gebruiker of groep Hallo gebruiker is dat lid van deze kan lang duren, afhankelijk van Hallo omvang en complexiteit van de groep Hallo voor toobe van wijzigingen aangebracht.</span><span class="sxs-lookup"><span data-stu-id="a14b5-109">If a license was just removed from a user or group hello user is a member of this may take a long time, depending on hello size and complexity of hello group for changes toobe made.</span></span> <span data-ttu-id="a14b5-110">Voor extra tijd voordat je je aanmeldt bij Hallo Toegangsvenster toestaan.</span><span class="sxs-lookup"><span data-stu-id="a14b5-110">Allow for extra time before signing into hello Access Panel.</span></span>

## <a name="problems-related-tooassigning-applications-toousers"></a><span data-ttu-id="a14b5-111">Problemen met gerelateerde tooassigning toepassingen toousers</span><span class="sxs-lookup"><span data-stu-id="a14b5-111">Problems related tooassigning applications toousers</span></span>

<span data-ttu-id="a14b5-112">Een gebruiker mogelijk ziet u een toepassing op hun Toegangsvenster omdat ze eerder tooit toegewezen had.</span><span class="sxs-lookup"><span data-stu-id="a14b5-112">A user may be seeing an application on their Access Panel because they had been previously assigned tooit.</span></span> <span data-ttu-id="a14b5-113">Hieronder vindt u enkele toocheck manieren:</span><span class="sxs-lookup"><span data-stu-id="a14b5-113">Below are some ways toocheck:</span></span>

-   [<span data-ttu-id="a14b5-114">Controleren of een gebruiker toohello toepassing is toegewezen</span><span class="sxs-lookup"><span data-stu-id="a14b5-114">Check if a user is assigned toohello application</span></span>](#check-if-a-user-is-assigned-to-the-application)

-   [<span data-ttu-id="a14b5-115">Controleer of een gebruiker zich onder een licentie gerelateerde toohello toepassing</span><span class="sxs-lookup"><span data-stu-id="a14b5-115">Check if a user is under a license related toohello application</span></span>](#check-if-a-user-is-under-a-license-related-to-the-application)


### <a name="check-if-a-user-is-assigned-toohello-application"></a><span data-ttu-id="a14b5-116">Controleren of een gebruiker toohello toepassing is toegewezen</span><span class="sxs-lookup"><span data-stu-id="a14b5-116">Check if a user is assigned toohello application</span></span>

<span data-ttu-id="a14b5-117">toocheck als een gebruiker is toegewezen toohello-toepassing hello volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="a14b5-117">toocheck if a user is assigned toohello application, follow hello steps below:</span></span>

1.  <span data-ttu-id="a14b5-118">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="a14b5-118">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="a14b5-119">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="a14b5-119">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="a14b5-120">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="a14b5-120">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="a14b5-121">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="a14b5-121">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="a14b5-122">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="a14b5-122">click **All Applications** tooview a list of all your applications.</span></span>

6.  <span data-ttu-id="a14b5-123">**Search** voor Hallo-naam van de betrokken Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="a14b5-123">**Search** for hello name of hello application in question.</span></span>

7.  <span data-ttu-id="a14b5-124">Klik op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="a14b5-124">click **Users and groups**.</span></span>

8.  <span data-ttu-id="a14b5-125">Controleer toosee als de gebruiker toohello toepassing is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="a14b5-125">Check toosee if your user is assigned toohello application.</span></span>

  * <span data-ttu-id="a14b5-126">Als u tooremove Hallo gebruiker van toepassing hello wilt, **klikt u op Hallo rij** van Hallo gebruiker en selecteer **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="a14b5-126">If you want tooremove hello user from hello application, **click hello row** of hello user and select **delete**.</span></span>

### <a name="check-if-a-user-is-under-a-license-related-toohello-application"></a><span data-ttu-id="a14b5-127">Controleer of een gebruiker zich onder een licentie gerelateerde toohello toepassing</span><span class="sxs-lookup"><span data-stu-id="a14b5-127">Check if a user is under a license related toohello application</span></span>

<span data-ttu-id="a14b5-128">toocheck een gebruiker de toegewezen licenties, Hallo stappen hieronder:</span><span class="sxs-lookup"><span data-stu-id="a14b5-128">toocheck a user’s assigned licenses, follow hello steps below:</span></span>

1.  <span data-ttu-id="a14b5-129">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="a14b5-129">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="a14b5-130">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="a14b5-130">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="a14b5-131">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="a14b5-131">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="a14b5-132">Klik op **gebruikers en groepen** in het navigatiemenu Hallo.</span><span class="sxs-lookup"><span data-stu-id="a14b5-132">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="a14b5-133">Klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="a14b5-133">click **All users**.</span></span>

6.  <span data-ttu-id="a14b5-134">**Search** voor u geïnteresseerd in het bent Hallo-gebruiker en **klikt u op Hallo rij** tooselect.</span><span class="sxs-lookup"><span data-stu-id="a14b5-134">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="a14b5-135">Klik op **licenties** toosee welke licenties Hallo gebruiker momenteel is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="a14b5-135">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

   * <span data-ttu-id="a14b5-136">Hallo Toegangsvenster van de gebruiker als Hallo gebruiker tooan dit eerste partij Office-toepassingen tooappear inschakelen op Office-licentie is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="a14b5-136">If hello user is assigned tooan Office license this enable First Party Office applications tooappear on hello user’s Access Panel.</span></span>

## <a name="problems-related-tooassigning-applications-toogroups"></a><span data-ttu-id="a14b5-137">Problemen met gerelateerde tooassigning toepassingen toogroups</span><span class="sxs-lookup"><span data-stu-id="a14b5-137">Problems related tooassigning applications toogroups</span></span>

<span data-ttu-id="a14b5-138">Een gebruiker mogelijk ziet u een toepassing op hun Toegangsvenster omdat ze deel uitmaken van een groep die de toepassing hello is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="a14b5-138">A user may be seeing an application on their Access Panel because they are part of a group that has been assigned hello application.</span></span> <span data-ttu-id="a14b5-139">Hieronder vindt u enkele toocheck manieren:</span><span class="sxs-lookup"><span data-stu-id="a14b5-139">Below are some ways toocheck:</span></span>

-   [<span data-ttu-id="a14b5-140">Controleer de groepslidmaatschappen van een gebruiker</span><span class="sxs-lookup"><span data-stu-id="a14b5-140">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="a14b5-141">Als een gebruiker lid is van een groep tooa licentie toegewezen controleren</span><span class="sxs-lookup"><span data-stu-id="a14b5-141">Check if a user is a member of a group assigned tooa license</span></span>](#check-if-a-user-is-a-member-of-a-group-assigned-to-a-license)

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="a14b5-142">Controleer de groepslidmaatschappen van een gebruiker</span><span class="sxs-lookup"><span data-stu-id="a14b5-142">Check a user’s group memberships</span></span>

<span data-ttu-id="a14b5-143">toocheck een groepslidmaatschap, Hallo stappen hieronder:</span><span class="sxs-lookup"><span data-stu-id="a14b5-143">toocheck a group’s membership, follow hello steps below:</span></span>

1.  <span data-ttu-id="a14b5-144">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="a14b5-144">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="a14b5-145">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="a14b5-145">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="a14b5-146">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="a14b5-146">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="a14b5-147">Klik op **gebruikers en groepen** in het navigatiemenu Hallo.</span><span class="sxs-lookup"><span data-stu-id="a14b5-147">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="a14b5-148">Klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="a14b5-148">click **All users**.</span></span>

6.  <span data-ttu-id="a14b5-149">**Search** voor u geïnteresseerd in het bent Hallo-gebruiker en **klikt u op Hallo rij** tooselect.</span><span class="sxs-lookup"><span data-stu-id="a14b5-149">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="a14b5-150">Klik op **groepen.**</span><span class="sxs-lookup"><span data-stu-id="a14b5-150">click **Groups.**</span></span>

8.  <span data-ttu-id="a14b5-151">Controleer de toosee als de gebruiker deel uit van een groep die is toegewezen toohello-toepassing maakt.</span><span class="sxs-lookup"><span data-stu-id="a14b5-151">Check toosee if your user is part of a Group assigned toohello application.</span></span>

   * <span data-ttu-id="a14b5-152">Als u tooremove Hallo gebruiker uit groep Hallo wilt **klikt u op Hallo rij** van Hallo groep en selecteer verwijderen.</span><span class="sxs-lookup"><span data-stu-id="a14b5-152">If you want tooremove hello user from hello group, **click hello row** of hello group and select delete.</span></span>

### <a name="check-if-a-user-is-a-member-of-a-group-assigned-tooa-license"></a><span data-ttu-id="a14b5-153">Als een gebruiker lid is van een groep tooa licentie toegewezen controleren</span><span class="sxs-lookup"><span data-stu-id="a14b5-153">Check if a user is a member of a group assigned tooa license</span></span>

1.  <span data-ttu-id="a14b5-154">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="a14b5-154">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="a14b5-155">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="a14b5-155">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="a14b5-156">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="a14b5-156">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="a14b5-157">Klik op **gebruikers en groepen** in het navigatiemenu Hallo.</span><span class="sxs-lookup"><span data-stu-id="a14b5-157">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="a14b5-158">Klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="a14b5-158">click **All users**.</span></span>

6.  <span data-ttu-id="a14b5-159">**Search** voor u geïnteresseerd in het bent Hallo-gebruiker en **klikt u op Hallo rij** tooselect.</span><span class="sxs-lookup"><span data-stu-id="a14b5-159">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="a14b5-160">Klik op **groepen.**</span><span class="sxs-lookup"><span data-stu-id="a14b5-160">click **Groups.**</span></span>

8.  <span data-ttu-id="a14b5-161">Klik op Hallo rij van een bepaalde groep.</span><span class="sxs-lookup"><span data-stu-id="a14b5-161">click hello row of a specific group.</span></span>

9.  <span data-ttu-id="a14b5-162">Klik op **licenties** toosee welke licenties Hallo groep tooit is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="a14b5-162">click **Licenses** toosee which licenses hello group has assigned tooit.</span></span>

  * <span data-ttu-id="a14b5-163">Hallo Toegangsvenster van de gebruiker als Hallo groep tooan dit mogelijk bepaalde tooappear eerste partij Office-toepassingen inschakelen op Office-licentie is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="a14b5-163">If hello group is assigned tooan Office license this may enable certain First Party Office applications tooappear on hello user’s Access Panel.</span></span>


## <a name="if-these-troubleshooting-steps-do-not-hello-resolve-hello-issue"></a><span data-ttu-id="a14b5-164">Als deze stappen voor probleemoplossing niet Hallo Hallo probleem oplossen</span><span class="sxs-lookup"><span data-stu-id="a14b5-164">If these troubleshooting steps do not hello resolve hello issue</span></span>

<span data-ttu-id="a14b5-165">Open een ondersteuningsticket Hello volgende informatie, indien beschikbaar:</span><span class="sxs-lookup"><span data-stu-id="a14b5-165">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="a14b5-166">Correlatie fout-ID</span><span class="sxs-lookup"><span data-stu-id="a14b5-166">Correlation error ID</span></span>

-   <span data-ttu-id="a14b5-167">UPN (e-mailadres van de gebruiker)</span><span class="sxs-lookup"><span data-stu-id="a14b5-167">UPN (user email address)</span></span>

-   <span data-ttu-id="a14b5-168">Tenant-id</span><span class="sxs-lookup"><span data-stu-id="a14b5-168">Tenant ID</span></span>

-   <span data-ttu-id="a14b5-169">Browsertype</span><span class="sxs-lookup"><span data-stu-id="a14b5-169">Browser type</span></span>

-   <span data-ttu-id="a14b5-170">Tijdzone en de tijd/tijdsbestek tijdens fout optreedt</span><span class="sxs-lookup"><span data-stu-id="a14b5-170">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="a14b5-171">Fiddler traceringen</span><span class="sxs-lookup"><span data-stu-id="a14b5-171">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="a14b5-172">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a14b5-172">Next steps</span></span>
[<span data-ttu-id="a14b5-173">Toepassingen beheren met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a14b5-173">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
