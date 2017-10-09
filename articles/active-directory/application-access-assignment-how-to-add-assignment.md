---
title: aaaHow tooassign gebruikers en groepen tooan toepassing | Microsoft Docs
description: Gebruikers toegang tot toohello toepassingen toogrant toewijzen
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
ms.openlocfilehash: e039a26e4b8f88ad747354859f1071b8f74b6789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooassign-users-and-groups-tooan-application"></a><span data-ttu-id="376a2-103">Hoe tooassign gebruikers en groepen tooan toepassing</span><span class="sxs-lookup"><span data-stu-id="376a2-103">How tooassign users and groups tooan application</span></span>

<span data-ttu-id="376a2-104">Voordat u uw gebruikers kunnen Hallo hieronder voor een bepaalde toepassing doen, moet u toofirst **ze toohello toepassing toewijzen** toogrant ze toegang krijgen tot:</span><span class="sxs-lookup"><span data-stu-id="376a2-104">Before your users can do any of hello below for a specific application, you need toofirst **assign them toohello application** toogrant them access:</span></span>

-   <span data-ttu-id="376a2-105">Toegang tot een toepassing met behulp van **rechtstreeks navigeren in de URL van de toepassing toohello** (ook wel bekend als Serviceprovider geïnitieerde eenmalige aanmelding).</span><span class="sxs-lookup"><span data-stu-id="376a2-105">Access an application by **navigating toohello application’s URL directly** (also known as SP-initiated sign-on).</span></span>

-   <span data-ttu-id="376a2-106">Toegang tot een toepassing met behulp van Hallo **toegangs-URL van gebruiker** op een toepassing **eigenschappen** pagina (ook wel bekend als IDP geïnitieerde aanmelding).</span><span class="sxs-lookup"><span data-stu-id="376a2-106">Access an application by using hello **User Access URL** on an application’s **Properties** page (also known as IDP-initiated sign on).</span></span>

-   <span data-ttu-id="376a2-107">Zie een toepassing worden weergegeven op hun [toepassing Toegangsvenster](https://myapps.microsoft.com/) of mobiele toepassing.</span><span class="sxs-lookup"><span data-stu-id="376a2-107">See an application appear on their [Application Access Panel](https://myapps.microsoft.com/) or mobile application.</span></span>

-   <span data-ttu-id="376a2-108">Zie een toepassing worden weergegeven op hun [startprogramma voor toepassingen van Office 365](https://support.office.com/article/Meet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a).</span><span class="sxs-lookup"><span data-stu-id="376a2-108">See an application appear on their [Office 365 Application Launcher](https://support.office.com/article/Meet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a).</span></span>

## <a name="methods-tooassign-applications-with-azure-active-directory"></a><span data-ttu-id="376a2-109">Methoden tooassign toepassingen met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="376a2-109">Methods tooassign applications with Azure Active Directory</span></span> 

<span data-ttu-id="376a2-110">Er zijn 3 manieren kunt u toepassingen met Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="376a2-110">There are 3 ways you can assign applications with Azure Active Directory:</span></span>

-   [<span data-ttu-id="376a2-111">Een gebruiker toewijzen rechtstreeks tooan toepassing als een beheerder</span><span class="sxs-lookup"><span data-stu-id="376a2-111">Assign a user directly tooan application as an administrator</span></span>](#assign-a-user-directly-as-an-administrator)

-   [<span data-ttu-id="376a2-112">Een groep worden toegewezen rechtstreeks tooan toepassing als een beheerder</span><span class="sxs-lookup"><span data-stu-id="376a2-112">Assign a group directly tooan application as an administrator</span></span>](#assign-a-group-directly-to-an-application-as-an-administrator)

-   [<span data-ttu-id="376a2-113">Selfservice toepassing toegang tooallow gebruikers toofind hun eigen toepassingen inschakelen</span><span class="sxs-lookup"><span data-stu-id="376a2-113">Enable self-service application access tooallow users toofind their own applications</span></span>](#enable-self-service-application-access-to-allow-users-to-find-their-own-applications)

## <a name="assign-a-user-directly-as-an-administrator"></a><span data-ttu-id="376a2-114">Een gebruiker toewijzen rechtstreeks als een beheerder</span><span class="sxs-lookup"><span data-stu-id="376a2-114">Assign a user directly as an administrator</span></span>

<span data-ttu-id="376a2-115">tooassign een of meer gebruikers tooan toepassing rechtstreeks Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="376a2-115">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="376a2-116">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="376a2-116">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="376a2-117">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="376a2-117">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="376a2-118">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="376a2-118">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="376a2-119">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="376a2-119">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="376a2-120">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="376a2-120">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="376a2-121">Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**</span><span class="sxs-lookup"><span data-stu-id="376a2-121">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="376a2-122">Hallo-toepassing die u wilt dat een lijst met gebruikers toofrom hello tooassign selecteren.</span><span class="sxs-lookup"><span data-stu-id="376a2-122">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="376a2-123">Nadat de toepassing hello wordt geladen, klikt u op **gebruikers en groepen** uit van de toepassing hello linkerkant navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="376a2-123">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="376a2-124">Klik op Hallo **toevoegen** knop boven op Hallo **gebruikers en groepen** lijst tooopen hello **toevoegen toewijzing** blade.</span><span class="sxs-lookup"><span data-stu-id="376a2-124">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="376a2-125">Klik op Hallo **gebruikers en groepen** selector van Hallo **toevoegen toewijzing** blade.</span><span class="sxs-lookup"><span data-stu-id="376a2-125">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="376a2-126">Type in Hallo **volledige naam** of **e-mailadres** van Hallo gebruiker u geïnteresseerd bent in het toewijzen van Hallo **zoeken op naam of e-mailadres** zoekvak.</span><span class="sxs-lookup"><span data-stu-id="376a2-126">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="376a2-127">Beweeg de muisaanwijzer over Hallo **gebruiker** in Hallo lijst tooreveal een **selectievakje**.</span><span class="sxs-lookup"><span data-stu-id="376a2-127">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="376a2-128">Klik op het profiel foto of een logo tooadd Hallo selectievakje volgende toohello van gebruiker uw gebruiker toohello **geselecteerde** lijst.</span><span class="sxs-lookup"><span data-stu-id="376a2-128">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="376a2-129">**Optioneel:** indien te gewenst**toevoegen van meer dan één gebruiker**, type in een andere **volledige naam** of **e-mailadres** in Hallo **zoeken op naam of e-mailadres** zoekvak en klikt u op Hallo selectievakje tooadd voor deze gebruiker toohello **geselecteerde** lijst.</span><span class="sxs-lookup"><span data-stu-id="376a2-129">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="376a2-130">Wanneer u klaar bent met het selecteren van gebruikers, klikt u op Hallo **Selecteer** knop tooadd ze toohello lijst met gebruikers en groepen toobe toegewezen toohello toepassing.</span><span class="sxs-lookup"><span data-stu-id="376a2-130">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="376a2-131">**Optioneel:** klikt u op Hallo **rol selecteren** selector in Hallo **toevoegen toewijzing** blade tooselect een rol tooassign toohello gebruikers die u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="376a2-131">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="376a2-132">Klik op Hallo **toewijzen** knop tooassign Hallo toepassing toohello gebruikers geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="376a2-132">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="376a2-133">Hallo-gebruikers die u hebt geselecteerd worden na een korte periode, kunnen toolaunch deze toepassingen met behulp van methoden die worden beschreven in Hallo oplossing beschrijving sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="376a2-133">After a short period of time, hello users you have selected be able toolaunch these applications using hello methods described in hello solution description section.</span></span>

## <a name="assign-a-group-directly-tooan-application-as-an-administrator"></a><span data-ttu-id="376a2-134">Een groep worden toegewezen rechtstreeks tooan toepassing als een beheerder</span><span class="sxs-lookup"><span data-stu-id="376a2-134">Assign a group directly tooan application as an administrator</span></span>

<span data-ttu-id="376a2-135">tooassign een of meer groepen tooan toepassing rechtstreeks Hallo stappen hieronder:</span><span class="sxs-lookup"><span data-stu-id="376a2-135">tooassign one or more groups tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="376a2-136">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="376a2-136">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="376a2-137">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="376a2-137">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="376a2-138">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="376a2-138">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="376a2-139">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="376a2-139">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="376a2-140">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="376a2-140">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="376a2-141">Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**</span><span class="sxs-lookup"><span data-stu-id="376a2-141">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="376a2-142">Hallo-toepassing die u wilt dat een lijst met gebruikers toofrom hello tooassign selecteren.</span><span class="sxs-lookup"><span data-stu-id="376a2-142">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="376a2-143">Nadat de toepassing hello wordt geladen, klikt u op **gebruikers en groepen** uit van de toepassing hello linkerkant navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="376a2-143">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="376a2-144">Klik op Hallo **toevoegen** knop boven op Hallo **gebruikers en groepen** lijst tooopen hello **toevoegen toewijzing** blade.</span><span class="sxs-lookup"><span data-stu-id="376a2-144">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="376a2-145">Klik op Hallo **gebruikers en groepen** selector van Hallo **toevoegen toewijzing** blade.</span><span class="sxs-lookup"><span data-stu-id="376a2-145">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="376a2-146">Type in Hallo **volledige groepsnaam** van Hallo groep u geïnteresseerd bent in het toewijzen van Hallo **zoeken op naam of e-mailadres** zoekvak.</span><span class="sxs-lookup"><span data-stu-id="376a2-146">Type in hello **full group name** of hello group you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="376a2-147">Beweeg de muisaanwijzer over Hallo **groep** in Hallo lijst tooreveal een **selectievakje**.</span><span class="sxs-lookup"><span data-stu-id="376a2-147">Hover over hello **group** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="376a2-148">Klik op het profiel foto of een logo tooadd Hallo selectievakje volgende toohello van de groep uw gebruiker toohello **geselecteerde** lijst.</span><span class="sxs-lookup"><span data-stu-id="376a2-148">Click hello checkbox next toohello group’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="376a2-149">**Optioneel:** indien te gewenst**toevoegen van meer dan één groep**, type in een andere **volledige groepsnaam** in Hallo **zoeken op naam of e-mailadres** zoekvak en klikt u op Hallo selectievakje tooadd van deze groep toohello **geselecteerde** lijst.</span><span class="sxs-lookup"><span data-stu-id="376a2-149">**Optional:** If you would like too**add more than one group**, type in another **full group name** into hello **Search by name or email address** search box, and click hello checkbox tooadd this group toohello **Selected** list.</span></span>

13. <span data-ttu-id="376a2-150">Wanneer u klaar bent met groepen te selecteren, klikt u op Hallo **Selecteer** knop tooadd ze toohello lijst met gebruikers en groepen toobe toegewezen toohello toepassing.</span><span class="sxs-lookup"><span data-stu-id="376a2-150">When you are finished selecting groups, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="376a2-151">**Optioneel:** klikt u op Hallo **rol selecteren** selector in Hallo **toevoegen toewijzing** blade tooselect een rol tooassign toohello groepen die u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="376a2-151">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello groups you have selected.</span></span>

15. <span data-ttu-id="376a2-152">Klik op Hallo **toewijzen** knop tooassign Hallo toepassing toohello geselecteerde groepen.</span><span class="sxs-lookup"><span data-stu-id="376a2-152">Click hello **Assign** button tooassign hello application toohello selected groups.</span></span>

<span data-ttu-id="376a2-153">Hallo gebruikers binnen Hallo-groepen die u hebt geselecteerd worden na een korte periode, kunnen toolaunch deze toepassingen met behulp van methoden die worden beschreven in Hallo oplossing beschrijving sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="376a2-153">After a short period of time, hello users within hello groups you have selected be able toolaunch these applications using hello methods described in hello solution description section.</span></span> <span data-ttu-id="376a2-154">Als dit dynamische groepen zijn, mogelijk zijn er enkele aanvullende verwerking vertraging in deze toewijzingen worden weergegeven voor gebruikers binnen deze groepen toegewezen.</span><span class="sxs-lookup"><span data-stu-id="376a2-154">If these are dynamic groups, there may be some additional processing delay in these assignments appearing for users within these assigned groups.</span></span>

## <a name="enable-self-service-application-access-tooallow-users-toofind-their-own-applications"></a><span data-ttu-id="376a2-155">Selfservice toepassing toegang tooallow gebruikers toofind hun eigen toepassingen inschakelen</span><span class="sxs-lookup"><span data-stu-id="376a2-155">Enable self-service application access tooallow users toofind their own applications</span></span>

<span data-ttu-id="376a2-156">Toegang tot de toepassing zelf is een uitstekende manier tooallow gebruikers tooself-toepassingen detecteren, eventueel Hallo business groep toestaan tooapprove toothose toepassingen.</span><span class="sxs-lookup"><span data-stu-id="376a2-156">Self-service application access is a great way tooallow users tooself-discover applications, optionally allow hello business group tooapprove access toothose applications.</span></span> <span data-ttu-id="376a2-157">U kunt toestaan Hallo business groep toomanage Hallo referenties toegewezen gebruikers toothose voor wachtwoord eenmalige aanmelding op toepassingen rechtstreeks vanuit hun panelen toegang.</span><span class="sxs-lookup"><span data-stu-id="376a2-157">You can allow hello business group toomanage hello credentials assigned toothose users for Password Single-Sign On Applications right from their access panels.</span></span>

<span data-ttu-id="376a2-158">tooenable selfservice toepassing toegang tooan toepassing hello stappen hieronder:</span><span class="sxs-lookup"><span data-stu-id="376a2-158">tooenable self-service application access tooan application, follow hello steps below:</span></span>

1.  <span data-ttu-id="376a2-159">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="376a2-159">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="376a2-160">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="376a2-160">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="376a2-161">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="376a2-161">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="376a2-162">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="376a2-162">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="376a2-163">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="376a2-163">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="376a2-164">Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**</span><span class="sxs-lookup"><span data-stu-id="376a2-164">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="376a2-165">Selecteer gewenste tooenable Self-service toofrom Hallo toegangslijst Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="376a2-165">Select hello application you want tooenable Self-service access toofrom hello list.</span></span>

7.  <span data-ttu-id="376a2-166">Nadat de toepassing hello wordt geladen, klikt u op **Self-service** uit van de toepassing hello linkerkant navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="376a2-166">Once hello application loads, click **Self-service** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="376a2-167">tooenable toegang tot de toepassing Self-service voor deze toepassing, schakelt u Hallo **toorequest access toothis-toepassing voor gebruikers toestaan?** te schakelen**Ja.**</span><span class="sxs-lookup"><span data-stu-id="376a2-167">tooenable Self-service application access for this application, turn hello **Allow users toorequest access toothis application?** toggle too**Yes.**</span></span>

9.  <span data-ttu-id="376a2-168">Tooselect hello toowhich gebruikers die een groep aanvragen toegang toothis toepassing moet worden toegevoegd, klik vervolgens op Hallo selector volgende toohello label **toowhich groep moet worden toegewezen gebruikers worden toegevoegd?** en selecteert u een groep.</span><span class="sxs-lookup"><span data-stu-id="376a2-168">Next, tooselect hello group toowhich users who request access toothis application should be added, click hello selector next toohello label **toowhich group should assigned users be added?** and select a group.</span></span>

10. <span data-ttu-id="376a2-169">**Optioneel:** als u toorequire goedkeuring van een zakelijke wenst voordat gebruikers toegang kunt krijgen, stelt u Hallo **moeten worden goedgekeurd voordat u verleent toegang toothis toepassing?** te schakelen**Ja**.</span><span class="sxs-lookup"><span data-stu-id="376a2-169">**Optional:** If you wish toorequire a business approval before users are allowed access, set hello **Require approval before granting access toothis application?** toggle too**Yes**.</span></span>

11. <span data-ttu-id="376a2-170">**Optioneel: voor toepassingen die gebruikmaken van wachtwoord eenmalige aanmelding alleen op** desgewenst tooallow deze bedrijven goedkeurders toospecify Hallo wachtwoorden die worden verzonden toothis toepassingen voor goedgekeurde gebruikers instellen Hallo **toestaan goedkeurders tooset wachtwoorden van de gebruiker voor deze toepassing?**  te schakelen**Ja**.</span><span class="sxs-lookup"><span data-stu-id="376a2-170">**Optional: For applications using password single-sign on only,** if you wish tooallow those business approvers toospecify hello passwords that are sent toothis application for approved users, set hello **Allow approvers tooset user’s passwords for this application?** toggle too**Yes**.</span></span>

12. <span data-ttu-id="376a2-171">**Optioneel:** toospecify Hallo business goedkeurders die mogen tooapprove toegang toothis toepassing, klikt u op Hallo selector volgende toohello label **die tooapprove access toothis-toepassing is toegestaan?** tooselect up too10 afzonderlijke business goedkeurders.</span><span class="sxs-lookup"><span data-stu-id="376a2-171">**Optional:** toospecify hello business approvers who are allowed tooapprove access toothis application, click hello selector next toohello label **Who is allowed tooapprove access toothis application?** tooselect up too10 individual business approvers.</span></span>

  >[!NOTE]
  ><span data-ttu-id="376a2-172">Groepen worden niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="376a2-172">Groups are not supported.</span></span>
  >
  >

13. <span data-ttu-id="376a2-173">**Optioneel:** **voor toepassingen die functies zichtbaar**, indien tooassign Self-service goedgekeurde gebruikers tooa rol gewenst, klikt u op Hallo selector volgende toohello **toowhich rol moeten gebruikers worden toegewezen in dit toepassing?**  tooselect Hallo rol toowhich deze gebruikers moeten worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="376a2-173">**Optional:** **For applications which expose roles**, if you wish tooassign self-service approved users tooa role, click hello selector next toohello **toowhich role should users be assigned in this application?** tooselect hello role toowhich these users should be assigned.</span></span>

14. <span data-ttu-id="376a2-174">Klik op Hallo **opslaan** knop bovenaan Hallo Hallo blade toofinish.</span><span class="sxs-lookup"><span data-stu-id="376a2-174">Click hello **Save** button at hello top of hello blade toofinish.</span></span>

<span data-ttu-id="376a2-175">Nadat u de configuratie van Self-Service toepassing hebt voltooid, gebruikers tootheir kunnen navigeren [toepassing Toegangspaneel](https://myapps.microsoft.com/) en klik op Hallo **+ toevoegen** knop toofind Hallo apps toowhich u hebt ingeschakeld Selfservice toegang.</span><span class="sxs-lookup"><span data-stu-id="376a2-175">Once you complete Self-service application configuration, users can navigate tootheir [Application Access Panel](https://myapps.microsoft.com/) and click hello **+Add** button toofind hello apps toowhich you have enabled Self-service access.</span></span> <span data-ttu-id="376a2-176">Zakelijke goedkeurders er ook een melding in hun [Toegangspaneel toepassing](https://myapps.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="376a2-176">Business approvers also see a notification in their [Application Access Panel](https://myapps.microsoft.com/).</span></span> <span data-ttu-id="376a2-177">U kunt een melding wanneer een gebruiker toegang tooan toepassing waarvoor goedkeuring is aangevraagd e-mail inschakelen.</span><span class="sxs-lookup"><span data-stu-id="376a2-177">You can enable an email notifying them when a user has requested access tooan application that requires their approval.</span></span> 

<span data-ttu-id="376a2-178">Deze goedkeuringen ondersteuning voor één goedkeuringswerkstromen, wat betekent dat als u meerdere goedkeurders opgeeft, kan een enkele fiatteur goedkeurder access toohello-toepassing.</span><span class="sxs-lookup"><span data-stu-id="376a2-178">These approvals support single approval workflows only, meaning that if you specify multiple approvers, any single approver may approver access toohello application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="376a2-179">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="376a2-179">Next steps</span></span>
[<span data-ttu-id="376a2-180">Bieden van eenmalige aanmelding tooyour apps met toepassingsproxy</span><span class="sxs-lookup"><span data-stu-id="376a2-180">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
