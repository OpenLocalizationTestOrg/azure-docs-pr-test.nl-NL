---
title: aaaManaging groepen in Azure Active Directory | Microsoft Docs
description: Hoe toocreate en beheren van groepen toomanage Azure gebruikers met Azure Active Directory.
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d1f5451c-3807-423c-8bac-2822d27b893f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/24/2017
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 9bee224655639740b3dd99983892b30c3c537aa0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-groups-in-azure-active-directory"></a><span data-ttu-id="e12e9-103">Groepen beheren in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e12e9-103">Managing groups in Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e12e9-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="e12e9-104">Azure portal</span></span>](active-directory-groups-create-azure-portal.md)
> * [<span data-ttu-id="e12e9-105">Klassieke Azure Portal</span><span class="sxs-lookup"><span data-stu-id="e12e9-105">Azure classic portal</span></span>](active-directory-accessmanagement-manage-groups.md)
> * [<span data-ttu-id="e12e9-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e12e9-106">PowerShell</span></span>](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

<span data-ttu-id="e12e9-107">Een van de functies Hallo van Gebruikersbeheer van Azure Active Directory (Azure AD) is Hallo mogelijkheid toocreate groepen gebruikers.</span><span class="sxs-lookup"><span data-stu-id="e12e9-107">One of hello features of Azure Active Directory (Azure AD) user management is hello ability toocreate groups of users.</span></span> <span data-ttu-id="e12e9-108">U een groep tooperform beheertaken, zoals het toewijzen van licenties of machtigingen tooa aantal gebruikers tegelijk gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e12e9-108">You use a group tooperform management tasks such as assigning licenses or permissions tooa number of users at once.</span></span> <span data-ttu-id="e12e9-109">Bovendien kunt u groepen tooassign toegangsmachtigingen voor</span><span class="sxs-lookup"><span data-stu-id="e12e9-109">You can also use groups tooassign access permission to</span></span>

* <span data-ttu-id="e12e9-110">Resources zoals objecten in de directory Hallo</span><span class="sxs-lookup"><span data-stu-id="e12e9-110">Resources such as objects in hello directory</span></span>
* <span data-ttu-id="e12e9-111">Bronnen extern toohello directory zoals SaaS-toepassingen, Azure-services, SharePoint-sites of lokale bronnen</span><span class="sxs-lookup"><span data-stu-id="e12e9-111">Resources external toohello directory such as SaaS applications, Azure services, SharePoint sites, or on-premises resources</span></span>

<span data-ttu-id="e12e9-112">Bovendien kan een resource-eigenaar ook toegang tooa resource tooan Azure AD-groep eigendom van iemand anders toewijzen.</span><span class="sxs-lookup"><span data-stu-id="e12e9-112">In addition, a resource owner can also assign access tooa resource tooan Azure AD group owned by someone else.</span></span> <span data-ttu-id="e12e9-113">Deze toewijzing hebben Hallo leden van die groep toegang toohello resource.</span><span class="sxs-lookup"><span data-stu-id="e12e9-113">This assignment grants hello members of that group access toohello resource.</span></span> <span data-ttu-id="e12e9-114">Hallo-eigenaar van Hallo groep beheert vervolgens lidmaatschap van groep Hallo.</span><span class="sxs-lookup"><span data-stu-id="e12e9-114">Then, hello owner of hello group manages membership in hello group.</span></span> <span data-ttu-id="e12e9-115">Effectief Hallo resource eigenaar gemachtigden toohello eigenaar van Hallo Hallo machtiging tooassign gebruikers tootheir groepsbron.</span><span class="sxs-lookup"><span data-stu-id="e12e9-115">Effectively, hello resource owner delegates toohello owner of hello group hello permission tooassign users tootheir resource.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e12e9-116">Microsoft raadt aan dat u Azure AD beheren met Hallo [Azure AD-beheercentrum](https://aad.portal.azure.com) in Hallo hello Azure-portal in plaats van de klassieke Azure-portal waarnaar wordt verwezen in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="e12e9-116">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> <span data-ttu-id="e12e9-117">Zie voor hoe toomanage in hello Azure AD-beheercentrum groepen, [een groep maken en leden toevoegen in Azure Active Directory](active-directory-groups-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e12e9-117">For how toomanage groups in hello Azure AD admin center, see [Create a group and add members in Azure Active Directory](active-directory-groups-create-azure-portal.md).</span></span>

## <a name="how-do-i-create-a-group"></a><span data-ttu-id="e12e9-118">Hoe maak ik een groep?</span><span class="sxs-lookup"><span data-stu-id="e12e9-118">How do I create a group?</span></span>
<span data-ttu-id="e12e9-119">Afhankelijk van Hallo services toowhich die uw organisatie is geabonneerd, kunt u een groep met behulp van een van de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="e12e9-119">Depending on hello services toowhich your organization has subscribed, you can create a group using one of hello following:</span></span>

* <span data-ttu-id="e12e9-120">Hallo klassieke Azure-portal</span><span class="sxs-lookup"><span data-stu-id="e12e9-120">hello Azure classic portal</span></span>
* <span data-ttu-id="e12e9-121">Hallo Office 365-accountportal</span><span class="sxs-lookup"><span data-stu-id="e12e9-121">hello Office 365 account portal</span></span>
* <span data-ttu-id="e12e9-122">Hallo Windows Intune-accountportal</span><span class="sxs-lookup"><span data-stu-id="e12e9-122">hello Windows Intune account portal</span></span>

<span data-ttu-id="e12e9-123">We beschrijven taken zoals uitgevoerd in de klassieke Azure-portal Hallo.</span><span class="sxs-lookup"><span data-stu-id="e12e9-123">We'll describe tasks as performed in hello Azure classic portal.</span></span> <span data-ttu-id="e12e9-124">Zie voor meer informatie over het gebruik van niet-Azure-portals toomanage uw Azure AD-directory [beheer van uw Azure AD-directory](active-directory-administer.md).</span><span class="sxs-lookup"><span data-stu-id="e12e9-124">For more information about using non-Azure portals toomanage your Azure AD directory, see [Administering your Azure AD directory](active-directory-administer.md).</span></span>

1. <span data-ttu-id="e12e9-125">In Hallo [klassieke Azure-portal](https://manage.windowsazure.com), selecteer **Active Directory**, en selecteer vervolgens de naam Hallo van Hallo directory voor uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="e12e9-125">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then select hello name of hello directory for your organization.</span></span>
2. <span data-ttu-id="e12e9-126">Selecteer Hallo **groepen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="e12e9-126">Select hello **Groups** tab.</span></span>
3. <span data-ttu-id="e12e9-127">Selecteer **Groep toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="e12e9-127">Select **Add Group**.</span></span>
4. <span data-ttu-id="e12e9-128">In Hallo **groep toevoegen** venster Geef Hallo naam en beschrijving van een groep Hallo.</span><span class="sxs-lookup"><span data-stu-id="e12e9-128">In hello **Add Group** window, specify hello name and hello description of a group.</span></span>

## <a name="how-do-i-add-or-remove-individual-users-in-a-security-group"></a><span data-ttu-id="e12e9-129">Hoe kan ik afzonderlijke gebruikers in een beveiligingsgroep toevoegen of verwijderen?</span><span class="sxs-lookup"><span data-stu-id="e12e9-129">How do I add or remove individual users in a security group?</span></span>
<span data-ttu-id="e12e9-130">**een afzonderlijke gebruiker tooa groep tooadd**</span><span class="sxs-lookup"><span data-stu-id="e12e9-130">**tooadd an individual user tooa group**</span></span>

1. <span data-ttu-id="e12e9-131">In Hallo [klassieke Azure-portal](https://manage.windowsazure.com), selecteer **Active Directory**, en selecteer vervolgens de naam Hallo van Hallo directory voor uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="e12e9-131">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then select hello name of hello directory for your organization.</span></span>
2. <span data-ttu-id="e12e9-132">Selecteer Hallo **groepen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="e12e9-132">Select hello **Groups** tab.</span></span>
3. <span data-ttu-id="e12e9-133">Hallo groep toowhich u tooadd leden wilt openen.</span><span class="sxs-lookup"><span data-stu-id="e12e9-133">Open hello group toowhich you want tooadd members.</span></span> <span data-ttu-id="e12e9-134">Open Hallo **leden** tabblad Hallo groep geselecteerd als deze nog niet weergeven.</span><span class="sxs-lookup"><span data-stu-id="e12e9-134">Open hello **Members** tab of hello selected group if it not already displaying.</span></span>
4. <span data-ttu-id="e12e9-135">Selecteer **Leden toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="e12e9-135">Select **Add Members**.</span></span>
5. <span data-ttu-id="e12e9-136">Op Hallo **leden toevoegen** pagina, selecteer Hallo-naam van het Hallo-gebruiker of groep dat u tooadd wilt gebruiken als een lid van deze groep.</span><span class="sxs-lookup"><span data-stu-id="e12e9-136">On hello **Add Members** page, select hello name of hello user or a group that you want tooadd as a member of this group.</span></span> <span data-ttu-id="e12e9-137">Controleer of deze naam is toegevoegd toohello **geselecteerde** deelvenster.</span><span class="sxs-lookup"><span data-stu-id="e12e9-137">Make sure that this name is added toohello **Selected** pane.</span></span>

<span data-ttu-id="e12e9-138">**tooremove een afzonderlijke gebruiker uit een groep**</span><span class="sxs-lookup"><span data-stu-id="e12e9-138">**tooremove an individual user from a group**</span></span>

1. <span data-ttu-id="e12e9-139">In Hallo [klassieke Azure-portal](https://manage.windowsazure.com), selecteer **Active Directory**, en selecteer vervolgens de naam Hallo van Hallo directory voor uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="e12e9-139">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then select hello name of hello directory for your organization.</span></span>
2. <span data-ttu-id="e12e9-140">Selecteer Hallo **groepen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="e12e9-140">Select hello **Groups** tab.</span></span>
3. <span data-ttu-id="e12e9-141">Hallo-groep waaruit u tooremove leden wilt openen.</span><span class="sxs-lookup"><span data-stu-id="e12e9-141">Open hello group from which you want tooremove members.</span></span>
4. <span data-ttu-id="e12e9-142">Selecteer Hallo **leden** tabblad, selecteer Hallo-naam van Hallo lid dat u tooremove uit deze groep wilt en klik vervolgens op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="e12e9-142">Select hello **Members** tab, select hello name of hello member that you want tooremove from this group, and then click **Remove**.</span></span>
5. <span data-ttu-id="e12e9-143">Hallo een opdrachtprompt wilt bevestigen dat u tooremove dit lid uit Hallo-groep.</span><span class="sxs-lookup"><span data-stu-id="e12e9-143">Confirm at hello prompt that you want tooremove this member from hello group.</span></span>

## <a name="how-can-i-manage-hello-membership-of-a-group-dynamically"></a><span data-ttu-id="e12e9-144">Hoe kan ik Hallo lidmaatschap van een groep dynamisch beheren?</span><span class="sxs-lookup"><span data-stu-id="e12e9-144">How can I manage hello membership of a group dynamically?</span></span>
<span data-ttu-id="e12e9-145">In Azure AD, kunt u heel eenvoudig een eenvoudige regel toodetermine welke gebruikers toobe lid van Hallo groep zijn instellen.</span><span class="sxs-lookup"><span data-stu-id="e12e9-145">In Azure AD, you can very easily set up a simple rule toodetermine which users are toobe members of hello group.</span></span> <span data-ttu-id="e12e9-146">Een eenvoudige regel is een regel die slechts één vergelijking maakt.</span><span class="sxs-lookup"><span data-stu-id="e12e9-146">A simple rule is one that makes only a single comparison.</span></span> <span data-ttu-id="e12e9-147">Bijvoorbeeld, als een groep is toegewezen tooa SaaS-toepassing, kunt u instellen van een regel tooadd gebruikers die de functienaam 'Vertegenwoordiger'.</span><span class="sxs-lookup"><span data-stu-id="e12e9-147">For example, if a group is assigned tooa SaaS application, you can set up a rule tooadd users who have a job title of "Sales Rep."</span></span> <span data-ttu-id="e12e9-148">Deze regel verleent toegang vervolgens toothis SaaS-toepassing tooall gebruikers met die functienaam in uw directory.</span><span class="sxs-lookup"><span data-stu-id="e12e9-148">This rule then grants access toothis SaaS application tooall users with that job title in your directory.</span></span>

<span data-ttu-id="e12e9-149">Wanneer Hallo system evalueert. kenmerken van een wijziging van de gebruiker, worden alle regels voor dynamische groepen in een directory toosee als Hallo kenmerkwijziging van Hallo gebruiker zou een groep toegevoegd of verwijderd.</span><span class="sxs-lookup"><span data-stu-id="e12e9-149">When any attributes of a user change, hello system evaluates all dynamic group rules in a directory toosee if hello attribute change of hello user would trigger any group adds or removes.</span></span> <span data-ttu-id="e12e9-150">Als een gebruiker voldoet aan een regel voor een groep, worden ze toegevoegd als een lid toothat-groep.</span><span class="sxs-lookup"><span data-stu-id="e12e9-150">If a user satisfies a rule on a group, they are added as a member toothat group.</span></span> <span data-ttu-id="e12e9-151">Als ze voldoen aan het niet langer Hallo-regel van een groep die ze lid van zijn, worden ze verwijderd als een leden van die groep.</span><span class="sxs-lookup"><span data-stu-id="e12e9-151">If they no longer satisfy hello rule of a group they are a member of, they are removed as a members from that group.</span></span>

> [!NOTE]
> <span data-ttu-id="e12e9-152">U kunt een regel instellen voor dynamisch lidmaatschap voor beveiligingsgroepen of Office 365-groepen.</span><span class="sxs-lookup"><span data-stu-id="e12e9-152">You can set up a rule for dynamic membership on security groups or Office 365 groups.</span></span> <span data-ttu-id="e12e9-153">Genest groepslidmaatschap worden momenteel niet ondersteund voor toewijzing op basis van een groep tooapplications.</span><span class="sxs-lookup"><span data-stu-id="e12e9-153">Nested group memberships aren't currently supported for group-based assignment tooapplications.</span></span>
>
> <span data-ttu-id="e12e9-154">Dynamisch lidmaatschap voor groepen moet een Azure AD Premium-licentie toobe toegewezen aan</span><span class="sxs-lookup"><span data-stu-id="e12e9-154">Dynamic memberships for groups require an Azure AD Premium license toobe assigned to</span></span>
>
> * <span data-ttu-id="e12e9-155">Hallo beheerder van Hallo-regel voor een groep</span><span class="sxs-lookup"><span data-stu-id="e12e9-155">hello administrator who manages hello rule on a group</span></span>
> * <span data-ttu-id="e12e9-156">Alle leden van de groep Hallo</span><span class="sxs-lookup"><span data-stu-id="e12e9-156">All members of hello group</span></span>
>
>

<span data-ttu-id="e12e9-157">**tooenable dynamisch lidmaatschap voor een groep**</span><span class="sxs-lookup"><span data-stu-id="e12e9-157">**tooenable dynamic membership for a group**</span></span>

1. <span data-ttu-id="e12e9-158">In Hallo [klassieke Azure-portal](https://manage.windowsazure.com), selecteer **Active Directory**, en selecteer vervolgens de naam Hallo van Hallo directory voor uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="e12e9-158">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then select hello name of hello directory for your organization.</span></span>
2. <span data-ttu-id="e12e9-159">Selecteer Hallo **groepen** tabblad en gewenste tooedit open Hallo-groep.</span><span class="sxs-lookup"><span data-stu-id="e12e9-159">Select hello **Groups** tab, and open hello group you want tooedit.</span></span>
3. <span data-ttu-id="e12e9-160">Selecteer Hallo **configureren** tabblad en stel vervolgens **dynamische lidmaatschappen inschakelen** te**Ja**.</span><span class="sxs-lookup"><span data-stu-id="e12e9-160">Select hello **Configure** tab, and then set **Enable Dynamic Memberships** too**Yes**.</span></span>
4. <span data-ttu-id="e12e9-161">Een eenvoudige regel voor Hallo groep toocontrol instellen hoe dynamisch lidmaatschap werkt voor deze groep.</span><span class="sxs-lookup"><span data-stu-id="e12e9-161">Set up a simple single rule for hello group toocontrol how dynamic membership for this group functions.</span></span> <span data-ttu-id="e12e9-162">Zorg ervoor dat Hallo **gebruikers toevoegen waarbij** optie is geselecteerd en selecteer vervolgens een gebruikerseigenschap in Hallo lijst (bijvoorbeeld afdeling, functietitel, enz.)</span><span class="sxs-lookup"><span data-stu-id="e12e9-162">Make sure hello **Add users where** option is selected, and then select a user property from hello list (for example, department, jobTitle, etc.),</span></span>
5. <span data-ttu-id="e12e9-163">Selecteer vervolgens een voorwaarde (niet gelijk aan, gelijk aan, begint niet met, begint met, bevat niet, bevat, geen overeenkomst, overeenkomst).</span><span class="sxs-lookup"><span data-stu-id="e12e9-163">Next, select a condition (Not Equals, Equals, Not Starts With, Starts With, Not Contains, Contains, Not Match, Match).</span></span>
6. <span data-ttu-id="e12e9-164">Geef een vergelijkingswaarde voor gebruikerseigenschap Hallo geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="e12e9-164">Specify a comparison value for hello selected user property.</span></span>

<span data-ttu-id="e12e9-165">toolearn over het toocreate *geavanceerde* regels (regels met meerdere vergelijkingen) voor dynamisch groepslidmaatschap, Zie [met behulp van kenmerken toocreate geavanceerde regels](active-directory-accessmanagement-groups-with-advanced-rules.md).</span><span class="sxs-lookup"><span data-stu-id="e12e9-165">toolearn about how toocreate *advanced* rules (rules that can contain multiple comparisons) for dynamic group membership, see [Using attributes toocreate advanced rules](active-directory-accessmanagement-groups-with-advanced-rules.md).</span></span>

## <a name="additional-information"></a><span data-ttu-id="e12e9-166">Aanvullende informatie</span><span class="sxs-lookup"><span data-stu-id="e12e9-166">Additional information</span></span>
<span data-ttu-id="e12e9-167">Deze artikelen bevatten aanvullende informatie over Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e12e9-167">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="e12e9-168">Tooresources toegang beheren met Azure Active Directory-groepen</span><span class="sxs-lookup"><span data-stu-id="e12e9-168">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* <span data-ttu-id="e12e9-169">[Azure Active Directory cmdlets for configuring group settings](active-directory-accessmanagement-groups-settings-cmdlets.md) (Azure Active Directory-cmdlets voor het configureren van groepsinstellingen)</span><span class="sxs-lookup"><span data-stu-id="e12e9-169">[Azure Active Directory cmdlets for configuring group settings](active-directory-accessmanagement-groups-settings-cmdlets.md)</span></span>
* <span data-ttu-id="e12e9-170">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)</span><span class="sxs-lookup"><span data-stu-id="e12e9-170">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md)</span></span>
* <span data-ttu-id="e12e9-171">[What is Azure Active Directory?](active-directory-whatis.md) (Wat is Azure Active Directory?)</span><span class="sxs-lookup"><span data-stu-id="e12e9-171">[What is Azure Active Directory?](active-directory-whatis.md)</span></span>
* [<span data-ttu-id="e12e9-172">Uw on-premises identiteiten integreren met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e12e9-172">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
