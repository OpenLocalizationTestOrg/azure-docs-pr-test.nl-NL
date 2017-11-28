---
title: Gebruikers en groepen toewijzen aan een toepassing | Microsoft Docs
description: Gebruikers toewijzen aan de toepassing om toegang te verlenen
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
ms.openlocfilehash: 61536612e0dd5102b8f5e911c350826846f5ed77
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-assign-users-and-groups-to-an-application"></a><span data-ttu-id="08267-103">Gebruikers en groepen toewijzen aan een toepassing</span><span class="sxs-lookup"><span data-stu-id="08267-103">How to assign users and groups to an application</span></span>

<span data-ttu-id="08267-104">Voordat u uw gebruikers kunnen doen van de hieronder voor een specifieke toepassing, moet u eerst **toewijzen aan de toepassing** ze om toegang te verlenen:</span><span class="sxs-lookup"><span data-stu-id="08267-104">Before your users can do any of the below for a specific application, you need to first **assign them to the application** to grant them access:</span></span>

-   <span data-ttu-id="08267-105">Toegang tot een toepassing met behulp van **navigeren naar de URL van de toepassing rechtstreeks** (ook wel bekend als Serviceprovider geïnitieerde eenmalige aanmelding).</span><span class="sxs-lookup"><span data-stu-id="08267-105">Access an application by **navigating to the application’s URL directly** (also known as SP-initiated sign-on).</span></span>

-   <span data-ttu-id="08267-106">Toegang tot een toepassing met behulp van de **toegangs-URL van gebruiker** op een toepassing **eigenschappen** pagina (ook wel bekend als IDP geïnitieerde aanmelding).</span><span class="sxs-lookup"><span data-stu-id="08267-106">Access an application by using the **User Access URL** on an application’s **Properties** page (also known as IDP-initiated sign on).</span></span>

-   <span data-ttu-id="08267-107">Zie een toepassing worden weergegeven op hun [toepassing Toegangsvenster](https://myapps.microsoft.com/) of mobiele toepassing.</span><span class="sxs-lookup"><span data-stu-id="08267-107">See an application appear on their [Application Access Panel](https://myapps.microsoft.com/) or mobile application.</span></span>

-   <span data-ttu-id="08267-108">Zie een toepassing worden weergegeven op hun [startprogramma voor toepassingen van Office 365](https://support.office.com/article/Meet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a).</span><span class="sxs-lookup"><span data-stu-id="08267-108">See an application appear on their [Office 365 Application Launcher](https://support.office.com/article/Meet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a).</span></span>

## <a name="methods-to-assign-applications-with-azure-active-directory"></a><span data-ttu-id="08267-109">Methoden voor het toewijzen van toepassingen met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="08267-109">Methods to assign applications with Azure Active Directory</span></span> 

<span data-ttu-id="08267-110">Er zijn 3 manieren kunt u toepassingen met Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="08267-110">There are 3 ways you can assign applications with Azure Active Directory:</span></span>

-   [<span data-ttu-id="08267-111">Een gebruiker toewijzen rechtstreeks aan een toepassing als een beheerder</span><span class="sxs-lookup"><span data-stu-id="08267-111">Assign a user directly to an application as an administrator</span></span>](#assign-a-user-directly-as-an-administrator)

-   [<span data-ttu-id="08267-112">Een groep rechtstreeks aan een toepassing als een beheerder toewijzen</span><span class="sxs-lookup"><span data-stu-id="08267-112">Assign a group directly to an application as an administrator</span></span>](#assign-a-group-directly-to-an-application-as-an-administrator)

-   [<span data-ttu-id="08267-113">Toegang tot de toepassing Self-Service gebruikers kunnen hun eigen toepassingen zoeken inschakelen</span><span class="sxs-lookup"><span data-stu-id="08267-113">Enable self-service application access to allow users to find their own applications</span></span>](#enable-self-service-application-access-to-allow-users-to-find-their-own-applications)

## <a name="assign-a-user-directly-as-an-administrator"></a><span data-ttu-id="08267-114">Een gebruiker toewijzen rechtstreeks als een beheerder</span><span class="sxs-lookup"><span data-stu-id="08267-114">Assign a user directly as an administrator</span></span>

<span data-ttu-id="08267-115">Als u wilt toewijzen een of meer gebruikers rechtstreeks naar een toepassing, de volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="08267-115">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="08267-116">Open de [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="08267-116">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="08267-117">Open de **Azure Active Directory-extensie** door te klikken op **meer services** onderaan in het navigatiemenu belangrijkste linkerkant.</span><span class="sxs-lookup"><span data-stu-id="08267-117">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="08267-118">Typ in **' Azure Active Directory**' in het zoekvak filter en selecteer de **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="08267-118">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="08267-119">Klik op **bedrijfstoepassingen** in het menu van Azure Active Directory linkerkant navigatie.</span><span class="sxs-lookup"><span data-stu-id="08267-119">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="08267-120">Klik op **alle toepassingen** om een lijst met al uw toepassingen weer te geven.</span><span class="sxs-lookup"><span data-stu-id="08267-120">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="08267-121">Als u de toepassing die u wilt weergeven die hier niet ziet, gebruikt u de **Filter** besturingselement aan de bovenkant van de **lijst met alle toepassingen** en stel de **weergeven** optie naar **alle toepassingen.**</span><span class="sxs-lookup"><span data-stu-id="08267-121">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="08267-122">Selecteer de toepassing die u wilt toewijzen van een gebruiker in de lijst.</span><span class="sxs-lookup"><span data-stu-id="08267-122">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="08267-123">Nadat de toepassing wordt geladen, klikt u op **gebruikers en groepen** van navigatiemenu links aan de van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="08267-123">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="08267-124">Klik op de **toevoegen** knop boven de **gebruikers en groepen** lijst openen de **toevoegen toewijzing** blade.</span><span class="sxs-lookup"><span data-stu-id="08267-124">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="08267-125">Klik op de **gebruikers en groepen** selector van de **toevoegen toewijzing** blade.</span><span class="sxs-lookup"><span data-stu-id="08267-125">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="08267-126">Typ in het **volledige naam** of **e-mailadres** van de gebruiker die u geïnteresseerd bent in toewijzen in de **zoeken op naam of e-mailadres** zoekvak.</span><span class="sxs-lookup"><span data-stu-id="08267-126">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="08267-127">Beweeg de muisaanwijzer over de **gebruiker** in de lijst om weer te geven een **selectievakje**.</span><span class="sxs-lookup"><span data-stu-id="08267-127">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="08267-128">Klik op het selectievakje naast de profielfoto van de gebruiker of het logo voor uw gebruiker toevoegen aan de **geselecteerde** lijst.</span><span class="sxs-lookup"><span data-stu-id="08267-128">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="08267-129">**Optioneel:** als u wilt **toevoegen van meer dan één gebruiker**, type in een andere **volledige naam** of **e-mailadres** in de **zoeken op naam of e-mailadres** zoekvak en klik op het selectievakje voor deze gebruiker toevoegen aan de **geselecteerde** lijst.</span><span class="sxs-lookup"><span data-stu-id="08267-129">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="08267-130">Wanneer u klaar bent met het selecteren van gebruikers, klikt u op de **Selecteer** om toe te voegen aan de lijst met gebruikers en groepen kunnen worden toegewezen aan de toepassing.</span><span class="sxs-lookup"><span data-stu-id="08267-130">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="08267-131">**Optioneel:** klikt u op de **rol selecteren** selector in de **toevoegen toewijzing** blade te selecteren van een rol toewijzen aan de gebruikers die u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="08267-131">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="08267-132">Klik op de **toewijzen** knop de toepassing toewijzen aan de geselecteerde gebruikers.</span><span class="sxs-lookup"><span data-stu-id="08267-132">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="08267-133">Na een korte periode, de gebruikers die u hebt geselecteerd mogelijk om deze toepassingen met behulp van de methoden die worden beschreven in de sectie oplossing beschrijving te starten.</span><span class="sxs-lookup"><span data-stu-id="08267-133">After a short period of time, the users you have selected be able to launch these applications using the methods described in the solution description section.</span></span>

## <a name="assign-a-group-directly-to-an-application-as-an-administrator"></a><span data-ttu-id="08267-134">Een groep rechtstreeks aan een toepassing als een beheerder toewijzen</span><span class="sxs-lookup"><span data-stu-id="08267-134">Assign a group directly to an application as an administrator</span></span>

<span data-ttu-id="08267-135">Als u wilt toewijzen een of meer groepen rechtstreeks aan een toepassing, de volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="08267-135">To assign one or more groups to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="08267-136">Open de [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="08267-136">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="08267-137">Open de **Azure Active Directory-extensie** door te klikken op **meer services** onderaan in het navigatiemenu belangrijkste linkerkant.</span><span class="sxs-lookup"><span data-stu-id="08267-137">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="08267-138">Typ in **' Azure Active Directory**' in het zoekvak filter en selecteer de **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="08267-138">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="08267-139">Klik op **bedrijfstoepassingen** in het menu van Azure Active Directory linkerkant navigatie.</span><span class="sxs-lookup"><span data-stu-id="08267-139">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="08267-140">Klik op **alle toepassingen** om een lijst met al uw toepassingen weer te geven.</span><span class="sxs-lookup"><span data-stu-id="08267-140">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="08267-141">Als u de toepassing die u wilt weergeven die hier niet ziet, gebruikt u de **Filter** besturingselement aan de bovenkant van de **lijst met alle toepassingen** en stel de **weergeven** optie naar **alle toepassingen.**</span><span class="sxs-lookup"><span data-stu-id="08267-141">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="08267-142">Selecteer de toepassing die u wilt toewijzen van een gebruiker in de lijst.</span><span class="sxs-lookup"><span data-stu-id="08267-142">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="08267-143">Nadat de toepassing wordt geladen, klikt u op **gebruikers en groepen** van navigatiemenu links aan de van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="08267-143">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="08267-144">Klik op de **toevoegen** knop boven de **gebruikers en groepen** lijst openen de **toevoegen toewijzing** blade.</span><span class="sxs-lookup"><span data-stu-id="08267-144">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="08267-145">Klik op de **gebruikers en groepen** selector van de **toevoegen toewijzing** blade.</span><span class="sxs-lookup"><span data-stu-id="08267-145">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="08267-146">Typ in het **volledige groepsnaam** van de groep die u geïnteresseerd bent in toewijzen in de **zoeken op naam of e-mailadres** zoekvak.</span><span class="sxs-lookup"><span data-stu-id="08267-146">Type in the **full group name** of the group you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="08267-147">Beweeg de muisaanwijzer over de **groep** in de lijst om weer te geven een **selectievakje**.</span><span class="sxs-lookup"><span data-stu-id="08267-147">Hover over the **group** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="08267-148">Schakel het selectievakje in naast de profielfoto of het logo voor uw gebruiker toevoegen aan de groep de **geselecteerde** lijst.</span><span class="sxs-lookup"><span data-stu-id="08267-148">Click the checkbox next to the group’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="08267-149">**Optioneel:** als u wilt **toevoegen van meer dan één groep**, type in een andere **volledige groepsnaam** in de **zoeken op naam of e-mailadres** zoekvak en klik op het selectievakje in om toe te voegen van deze groep de **geselecteerde** lijst.</span><span class="sxs-lookup"><span data-stu-id="08267-149">**Optional:** If you would like to **add more than one group**, type in another **full group name** into the **Search by name or email address** search box, and click the checkbox to add this group to the **Selected** list.</span></span>

13. <span data-ttu-id="08267-150">Wanneer u klaar bent met groepen te selecteren, klikt u op de **Selecteer** om toe te voegen aan de lijst met gebruikers en groepen kunnen worden toegewezen aan de toepassing.</span><span class="sxs-lookup"><span data-stu-id="08267-150">When you are finished selecting groups, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="08267-151">**Optioneel:** klikt u op de **rol selecteren** selector in de **toevoegen toewijzing** blade te selecteren van een rol toewijzen aan de groepen die u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="08267-151">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the groups you have selected.</span></span>

15. <span data-ttu-id="08267-152">Klik op de **toewijzen** knop de toepassing toewijzen aan de geselecteerde groepen.</span><span class="sxs-lookup"><span data-stu-id="08267-152">Click the **Assign** button to assign the application to the selected groups.</span></span>

<span data-ttu-id="08267-153">Na een korte periode, de gebruikers binnen de groepen die u hebt geselecteerd mogelijk om deze toepassingen met behulp van de methoden die worden beschreven in de sectie oplossing beschrijving te starten.</span><span class="sxs-lookup"><span data-stu-id="08267-153">After a short period of time, the users within the groups you have selected be able to launch these applications using the methods described in the solution description section.</span></span> <span data-ttu-id="08267-154">Als dit dynamische groepen zijn, mogelijk zijn er enkele aanvullende verwerking vertraging in deze toewijzingen worden weergegeven voor gebruikers binnen deze groepen toegewezen.</span><span class="sxs-lookup"><span data-stu-id="08267-154">If these are dynamic groups, there may be some additional processing delay in these assignments appearing for users within these assigned groups.</span></span>

## <a name="enable-self-service-application-access-to-allow-users-to-find-their-own-applications"></a><span data-ttu-id="08267-155">Toegang tot de toepassing Self-Service gebruikers kunnen hun eigen toepassingen zoeken inschakelen</span><span class="sxs-lookup"><span data-stu-id="08267-155">Enable self-service application access to allow users to find their own applications</span></span>

<span data-ttu-id="08267-156">Toegang tot de toepassing zelf is een uitstekende manier om toestaan dat gebruikers zelf detecteren toepassingen, toestaan de bedrijfsgroep goedkeuren van toegang tot deze toepassingen.</span><span class="sxs-lookup"><span data-stu-id="08267-156">Self-service application access is a great way to allow users to self-discover applications, optionally allow the business group to approve access to those applications.</span></span> <span data-ttu-id="08267-157">U kunt de bedrijfsgroep voor het beheren van de referenties die zijn toegewezen aan deze gebruikers voor het recht wachtwoord eenmalige aanmelding op toepassingen van hun panelen toegang toestaan.</span><span class="sxs-lookup"><span data-stu-id="08267-157">You can allow the business group to manage the credentials assigned to those users for Password Single-Sign On Applications right from their access panels.</span></span>

<span data-ttu-id="08267-158">Voor self-service toepassing toegang tot een toepassing, de volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="08267-158">To enable self-service application access to an application, follow the steps below:</span></span>

1.  <span data-ttu-id="08267-159">Open de [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="08267-159">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="08267-160">Open de **Azure Active Directory-extensie** door te klikken op **meer services** onderaan in het navigatiemenu belangrijkste linkerkant.</span><span class="sxs-lookup"><span data-stu-id="08267-160">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="08267-161">Typ in **' Azure Active Directory**' in het zoekvak filter en selecteer de **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="08267-161">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="08267-162">Klik op **bedrijfstoepassingen** in het menu van Azure Active Directory linkerkant navigatie.</span><span class="sxs-lookup"><span data-stu-id="08267-162">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="08267-163">Klik op **alle toepassingen** om een lijst met al uw toepassingen weer te geven.</span><span class="sxs-lookup"><span data-stu-id="08267-163">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="08267-164">Als u de toepassing die u wilt weergeven die hier niet ziet, gebruikt u de **Filter** besturingselement aan de bovenkant van de **lijst met alle toepassingen** en stel de **weergeven** optie naar **alle toepassingen.**</span><span class="sxs-lookup"><span data-stu-id="08267-164">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="08267-165">Selecteer de toepassing die u wilt inschakelen, Self-service toegang tot in de lijst.</span><span class="sxs-lookup"><span data-stu-id="08267-165">Select the application you want to enable Self-service access to from the list.</span></span>

7.  <span data-ttu-id="08267-166">Nadat de toepassing wordt geladen, klikt u op **Self-service** van navigatiemenu links aan de van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="08267-166">Once the application loads, click **Self-service** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="08267-167">Voor self-service toepassing toegang voor deze toepassing, schakelt u de **toestaan dat gebruikers toegang tot deze toepassing aanvragen?** in-of uitschakelen op **Ja.**</span><span class="sxs-lookup"><span data-stu-id="08267-167">To enable Self-service application access for this application, turn the **Allow users to request access to this application?** toggle to **Yes.**</span></span>

9.  <span data-ttu-id="08267-168">Klik vervolgens op de selector naast het label om te selecteren in de groep waartoe gebruikers die aanvragen toegang tot deze toepassing moet worden toegevoegd, **voor welke groep toegewezen gebruikers worden toegevoegd?** en selecteert u een groep.</span><span class="sxs-lookup"><span data-stu-id="08267-168">Next, to select the group to which users who request access to this application should be added, click the selector next to the label **To which group should assigned users be added?** and select a group.</span></span>

10. <span data-ttu-id="08267-169">**Optioneel:** als u wilt een zakelijke goedkeuringsprocedure voordat gebruikers toegang hebben, stelt u de **moeten worden goedgekeurd voordat het verlenen van toegang tot deze toepassing?** in-of uitschakelen op **Ja**.</span><span class="sxs-lookup"><span data-stu-id="08267-169">**Optional:** If you wish to require a business approval before users are allowed access, set the **Require approval before granting access to this application?** toggle to **Yes**.</span></span>

11. <span data-ttu-id="08267-170">**Optioneel: voor toepassingen die gebruikmaken van wachtwoord eenmalige aanmelding alleen op** als u deze bedrijven fiatteurs om op te geven van de wachtwoorden die worden verzonden naar deze toepassing voor goedgekeurde gebruikers toestaan wilt, stelt u de **fiatteurs instellen van wachtwoorden voor deze toepassing van de gebruiker toestaan?** in-of uitschakelen op **Ja**.</span><span class="sxs-lookup"><span data-stu-id="08267-170">**Optional: For applications using password single-sign on only,** if you wish to allow those business approvers to specify the passwords that are sent to this application for approved users, set the **Allow approvers to set user’s passwords for this application?** toggle to **Yes**.</span></span>

12. <span data-ttu-id="08267-171">**Optioneel:** om op te geven de zakelijke fiatteurs die zijn toegestaan voor het goedkeuren van toegang tot deze toepassing, klikt u op de selector naast het label **die is toegestaan voor het goedkeuren van toegang tot deze toepassing?** maximaal 10 afzonderlijke business goedkeurders selecteren.</span><span class="sxs-lookup"><span data-stu-id="08267-171">**Optional:** To specify the business approvers who are allowed to approve access to this application, click the selector next to the label **Who is allowed to approve access to this application?** to select up to 10 individual business approvers.</span></span>

  >[!NOTE]
  ><span data-ttu-id="08267-172">Groepen worden niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="08267-172">Groups are not supported.</span></span>
  >
  >

13. <span data-ttu-id="08267-173">**Optioneel:** **voor toepassingen die functies zichtbaar**, als u wilt Self-service goedgekeurde gebruikers toewijzen aan een rol, klikt u op de selector naast de **welke rol u gebruikers wilt toewijzen in deze toepassing?** om de rol waaraan u deze gebruikers worden toegewezen te selecteren.</span><span class="sxs-lookup"><span data-stu-id="08267-173">**Optional:** **For applications which expose roles**, if you wish to assign self-service approved users to a role, click the selector next to the **To which role should users be assigned in this application?** to select the role to which these users should be assigned.</span></span>

14. <span data-ttu-id="08267-174">Klik op de **opslaan** knop aan de bovenkant van de blade om te voltooien.</span><span class="sxs-lookup"><span data-stu-id="08267-174">Click the **Save** button at the top of the blade to finish.</span></span>

<span data-ttu-id="08267-175">Nadat u de configuratie van Self-Service toepassing hebt voltooid, gebruikers kunnen navigeren naar hun [toepassing Toegangspaneel](https://myapps.microsoft.com/) en klik op de **+ toevoegen** om te zoeken van de apps waarmee u toegang tot selfservice hebt ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="08267-175">Once you complete Self-service application configuration, users can navigate to their [Application Access Panel](https://myapps.microsoft.com/) and click the **+Add** button to find the apps to which you have enabled Self-service access.</span></span> <span data-ttu-id="08267-176">Zakelijke goedkeurders er ook een melding in hun [Toegangspaneel toepassing](https://myapps.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="08267-176">Business approvers also see a notification in their [Application Access Panel](https://myapps.microsoft.com/).</span></span> <span data-ttu-id="08267-177">U kunt een melding wanneer een gebruiker heeft toegang tot een toepassing die hun goedkeuring vereist aangevraagd e-mail inschakelen.</span><span class="sxs-lookup"><span data-stu-id="08267-177">You can enable an email notifying them when a user has requested access to an application that requires their approval.</span></span> 

<span data-ttu-id="08267-178">Deze goedkeuringen ondersteuning voor één goedkeuringswerkstromen, wat betekent dat als u meerdere goedkeurders opgeeft, kan een enkele fiatteur goedkeurder toegang tot de toepassing.</span><span class="sxs-lookup"><span data-stu-id="08267-178">These approvals support single approval workflows only, meaning that if you specify multiple approvers, any single approver may approver access to the application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="08267-179">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="08267-179">Next steps</span></span>
[<span data-ttu-id="08267-180">Geef één aanmelding bij uw apps met toepassingsproxy</span><span class="sxs-lookup"><span data-stu-id="08267-180">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
