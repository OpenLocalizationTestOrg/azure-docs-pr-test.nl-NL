---
title: 'Zelfstudie: Slack configureren voor het automatisch gebruikers inrichten met Azure Active Directory | Microsoft Docs'
description: Meer informatie over hoe tooconfigure Azure Active Directory tooautomatically leveren en intrekken gebruikersaccounts tooSlack.
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: sakula
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: asmalser-msft
ms.reviewer: asmalser
ms.openlocfilehash: d0a565bbe0bd7e229b9dd99b1ebbaf67d93a2206
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-slack-for-automatic-user-provisioning"></a><span data-ttu-id="bec3e-103">Zelfstudie: Slack configureren voor het automatisch gebruikers inrichten</span><span class="sxs-lookup"><span data-stu-id="bec3e-103">Tutorial: Configuring Slack for Automatic User Provisioning</span></span>


<span data-ttu-id="bec3e-104">Hallo doel van deze zelfstudie is tooshow Hallo van stappen die u moet tooperform in Slack en Azure AD tooautomatically leveren en intrekken gebruikersaccounts vanuit Azure AD-tooSlack.</span><span class="sxs-lookup"><span data-stu-id="bec3e-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Slack and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooSlack.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="bec3e-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="bec3e-105">Prerequisites</span></span>

<span data-ttu-id="bec3e-106">Hallo scenario beschreven in deze zelfstudie wordt ervan uitgegaan dat u al hebt Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="bec3e-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="bec3e-107">Een Azure Active Active directory-tenant</span><span class="sxs-lookup"><span data-stu-id="bec3e-107">An Azure Active Active directory tenant</span></span>
*   <span data-ttu-id="bec3e-108">Een Slack-tenant met Hallo [Plus plan](https://aadsyncfabric.slack.com/pricing) of beter ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="bec3e-108">A Slack tenant with hello [Plus plan](https://aadsyncfabric.slack.com/pricing) or better enabled</span></span> 
*   <span data-ttu-id="bec3e-109">Een gebruikersaccount in Slack met beheerdersmachtigingen Team</span><span class="sxs-lookup"><span data-stu-id="bec3e-109">A user account in Slack with Team Admin permissions</span></span> 

<span data-ttu-id="bec3e-110">Opmerking: hello Azure AD integratie inrichting is afhankelijk van Hallo [Slack SCIM API](https://api.slack.com/scim) die teams op Hallo Plus-abonnement of een betere tooSlack beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="bec3e-110">Note: hello Azure AD provisioning integration relies on hello [Slack SCIM API](https://api.slack.com/scim) which is available tooSlack teams on hello Plus plan or better.</span></span>

## <a name="assigning-users-tooslack"></a><span data-ttu-id="bec3e-111">Gebruikers tooSlack toewijzen</span><span class="sxs-lookup"><span data-stu-id="bec3e-111">Assigning users tooSlack</span></span>

<span data-ttu-id="bec3e-112">Azure Active Directory gebruikt een concept 'toewijzingen' toodetermine welke gebruikers toegang tooselected apps krijgen genoemd.</span><span class="sxs-lookup"><span data-stu-id="bec3e-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="bec3e-113">In de context van de Hallo van automatische gebruikers account inrichten, worden alleen Hallo-gebruikers en groepen die '' tooan toepassing in Azure AD toegewezen zijn gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="bec3e-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD will be synchronized.</span></span> 

<span data-ttu-id="bec3e-114">Voordat u configureren en inschakelen van Hallo-service inricht, moet u toodecide welke gebruikers en/of groepen in Azure AD vertegenwoordigen Hallo-gebruikers die toegang moeten hebben tot tooyour toegestane app.</span><span class="sxs-lookup"><span data-stu-id="bec3e-114">Before configuring and enabling hello provisioning service, you will need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Slack app.</span></span> <span data-ttu-id="bec3e-115">Als besloten, kunt u deze gebruikers tooyour toegestane app toewijzen door hier Hallo-instructies te volgen:</span><span class="sxs-lookup"><span data-stu-id="bec3e-115">Once decided, you can assign these users tooyour Slack app by following hello instructions here:</span></span>

[<span data-ttu-id="bec3e-116">Toewijzen van een gebruiker of groep tooan enterprise-app</span><span class="sxs-lookup"><span data-stu-id="bec3e-116">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-tooslack"></a><span data-ttu-id="bec3e-117">Belangrijke tips voor het toewijzen van gebruikers tooSlack</span><span class="sxs-lookup"><span data-stu-id="bec3e-117">Important tips for assigning users tooSlack</span></span>

*   <span data-ttu-id="bec3e-118">Het is raadzaam om één Azure AD-gebruiker tooSlack tootest Hallo inrichting configuratie worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="bec3e-118">It is recommended that a single Azure AD user be assigned tooSlack tootest hello provisioning configuration.</span></span> <span data-ttu-id="bec3e-119">Extra gebruikers en/of groepen kunnen later worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="bec3e-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="bec3e-120">Wanneer u een gebruiker tooSlack toewijst, moet u Hallo **gebruiker** of 'Groep'-rol in het dialoogvenster voor Hallo-toewijzing.</span><span class="sxs-lookup"><span data-stu-id="bec3e-120">When assigning a user tooSlack, you must select hello **User** or "Group" role in hello assignment dialog.</span></span> <span data-ttu-id="bec3e-121">Hallo 'Default toegang' rol werkt niet voor het inrichten.</span><span class="sxs-lookup"><span data-stu-id="bec3e-121">hello "Default Access" role does not work for provisioning.</span></span>


## <a name="configuring-user-provisioning-tooslack"></a><span data-ttu-id="bec3e-122">Gebruikers inrichten tooSlack configureren</span><span class="sxs-lookup"><span data-stu-id="bec3e-122">Configuring user provisioning tooSlack</span></span> 

<span data-ttu-id="bec3e-123">Deze sectie helpt u bij het verbinden van uw Azure AD-tooSlack gebruikersaccount inrichten API en Hallo service toocreate inrichting configureren, bijwerken en uitschakelen van toegewezen gebruikersaccounts in Slack op basis van gebruikers en groepen toewijzen in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bec3e-123">This section guides you through connecting your Azure AD tooSlack's user account provisioning API, and configuring hello provisioning service toocreate, update and disable assigned user accounts in Slack based on user and group assignment in Azure AD.</span></span>

<span data-ttu-id="bec3e-124">**Tip:** u kunt ook tooenabled op basis van SAML eenmalige aanmelding voor de vertraging Hallo instructies vindt u in (Azure-portal) [https://portal.azure.com].</span><span class="sxs-lookup"><span data-stu-id="bec3e-124">**Tip:** You may also choose tooenabled SAML-based Single Sign-On for Slack, following hello instructions provided in (Azure portal)[https://portal.azure.com].</span></span> <span data-ttu-id="bec3e-125">Eenmalige aanmelding kan worden geconfigureerd onafhankelijk van automatische inrichting, hoewel deze twee functies aanvulling van elkaar.</span><span class="sxs-lookup"><span data-stu-id="bec3e-125">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="tooconfigure-automatic-user-account-provisioning-tooslack-in-azure-ad"></a><span data-ttu-id="bec3e-126">tooconfigure automatische gebruikersaccount tooSlack ingericht in Azure AD:</span><span class="sxs-lookup"><span data-stu-id="bec3e-126">tooconfigure automatic user account provisioning tooSlack in Azure AD:</span></span>


1)  <span data-ttu-id="bec3e-127">In Hallo [Azure-portal](https://portal.azure.com), bladeren toohello **Azure Active Directory > zakelijke Apps > alle toepassingen** sectie.</span><span class="sxs-lookup"><span data-stu-id="bec3e-127">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2) <span data-ttu-id="bec3e-128">Als u toegestane vertraging voor eenmalige aanmelding al hebt geconfigureerd, kunt u zoeken naar uw exemplaar van Hallo zoekveld met Slack.</span><span class="sxs-lookup"><span data-stu-id="bec3e-128">If you have already configured Slack for single sign-on, search for your instance of Slack using hello search field.</span></span> <span data-ttu-id="bec3e-129">Selecteer anders **toevoegen** en zoek naar **Slack** in Hallo-toepassingsgalerie.</span><span class="sxs-lookup"><span data-stu-id="bec3e-129">Otherwise, select **Add** and search for **Slack** in hello application gallery.</span></span> <span data-ttu-id="bec3e-130">Selecteer Slack in zoekresultaten hello, en voeg deze tooyour lijst met toepassingen.</span><span class="sxs-lookup"><span data-stu-id="bec3e-130">Select Slack from hello search results, and add it tooyour list of applications.</span></span>

3)  <span data-ttu-id="bec3e-131">Selecteer uw exemplaar van Slack en vervolgens Hallo **inrichten** tabblad.</span><span class="sxs-lookup"><span data-stu-id="bec3e-131">Select your instance of Slack, then select hello **Provisioning** tab.</span></span>

4)  <span data-ttu-id="bec3e-132">Set Hallo **modus inrichting** te**automatische**.</span><span class="sxs-lookup"><span data-stu-id="bec3e-132">Set hello **Provisioning Mode** too**Automatic**.</span></span>

![Vertraging inrichten](./media/active-directory-saas-slack-provisioning-tutorial/Slack1.PNG)

5)  <span data-ttu-id="bec3e-134">Onder Hallo **beheerdersreferenties** sectie, klikt u op **autoriseren**.</span><span class="sxs-lookup"><span data-stu-id="bec3e-134">Under hello **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="bec3e-135">Hiermee opent u een dialoogvenster toegestane autorisatie in een nieuw browservenster.</span><span class="sxs-lookup"><span data-stu-id="bec3e-135">This opens a Slack authorization dialog in a new browser window.</span></span> 

6) <span data-ttu-id="bec3e-136">In nieuw venster hello, meld u aan in Slack met uw Team Admin-account.</span><span class="sxs-lookup"><span data-stu-id="bec3e-136">In hello new window, sign into Slack using your Team Admin account.</span></span> <span data-ttu-id="bec3e-137">in het resulterende autorisatie dialoogvenster Hallo Hallo Selecteer toegestane team dat u wilt tooenable voor inrichting en selecteer vervolgens **autoriseren**.</span><span class="sxs-lookup"><span data-stu-id="bec3e-137">in hello resulting authorization dialog, select hello Slack team that you want tooenable provisioning for, and then select **Authorize**.</span></span> <span data-ttu-id="bec3e-138">Voltooid door terug te gaan toohello Azure portal toocomplete hello configuratie inrichten.</span><span class="sxs-lookup"><span data-stu-id="bec3e-138">Once completed, return toohello Azure portal toocomplete hello provisioning configuration.</span></span>

![Dialoogvenster autorisatie](./media/active-directory-saas-slack-provisioning-tutorial/Slack3.PNG)

7) <span data-ttu-id="bec3e-140">Klik in hello Azure-portal, op **testverbinding** tooensure Azure AD tooyour toegestane app kunt verbinden.</span><span class="sxs-lookup"><span data-stu-id="bec3e-140">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Slack app.</span></span> <span data-ttu-id="bec3e-141">Als Hallo verbinding mislukt, zorg ervoor dat uw toegestane account Team beheerdersmachtigingen heeft en probeer het Hallo 'Autoriseren' stap opnieuw.</span><span class="sxs-lookup"><span data-stu-id="bec3e-141">If hello connection fails, ensure your Slack account has Team Admin permissions and try hello "Authorize" step again.</span></span>

8) <span data-ttu-id="bec3e-142">Voer e-mailadres van een persoon of groep die inrichting fout meldingen in Hallo ontvangen moet Hallo **e-mailmelding** veld en controleer de onderstaande Hallo selectievakje.</span><span class="sxs-lookup"><span data-stu-id="bec3e-142">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox below.</span></span>

9) <span data-ttu-id="bec3e-143">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="bec3e-143">Click **Save**.</span></span> 

10) <span data-ttu-id="bec3e-144">Selecteer onder Hallo toewijzingen sectie, **synchroniseren Azure Active Directory: gebruikers tooSlack**.</span><span class="sxs-lookup"><span data-stu-id="bec3e-144">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooSlack**.</span></span>

11) <span data-ttu-id="bec3e-145">In Hallo **kenmerktoewijzingen** sectie, bekijkt hello gebruikerskenmerken die worden gesynchroniseerd vanuit Azure AD-tooSlack.</span><span class="sxs-lookup"><span data-stu-id="bec3e-145">In hello **Attribute Mappings** section, review hello user attributes that will be synchronized from Azure AD tooSlack.</span></span> <span data-ttu-id="bec3e-146">Let op: kenmerken die zijn geselecteerd als Hallo **overeenkomend** eigenschappen worden gebruikte toomatch Hallo gebruikersaccounts in Slack voor update-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="bec3e-146">Note that hello attributes selected as **Matching** properties will be used toomatch hello user accounts in Slack for update operations.</span></span> <span data-ttu-id="bec3e-147">Selecteer Hallo knop toocommit wijzigingen zijn opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="bec3e-147">Select hello Save button toocommit any changes.</span></span>

12) <span data-ttu-id="bec3e-148">tooenable Hallo inrichting Azure AD-service voor vertraging wijziging Hallo **inrichting Status** te**op** in Hallo **instellingen** sectie</span><span class="sxs-lookup"><span data-stu-id="bec3e-148">tooenable hello Azure AD provisioning service for Slack, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

13) <span data-ttu-id="bec3e-149">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="bec3e-149">Click **Save**.</span></span> 

<span data-ttu-id="bec3e-150">Hiermee start u de initiële synchronisatie Hallo van gebruikers en/of groepen die zijn toegewezen tooSlack in Hallo gebruikers en groepen sectie.</span><span class="sxs-lookup"><span data-stu-id="bec3e-150">This will start hello initial synchronization of any users and/or groups assigned tooSlack in hello Users and Groups section.</span></span> <span data-ttu-id="bec3e-151">Houd er rekening mee dat de initiële synchronisatie Hallo langer tooperform dan het volgende wordt gesynchroniseerd, die ongeveer elke 10 minuten optreden duurt, zolang het Hallo-service wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="bec3e-151">Note that hello initial sync will take longer tooperform than subsequent syncs, which occur approximately every 10 minutes as long as hello service is running.</span></span> <span data-ttu-id="bec3e-152">U kunt Hallo **synchronisatiedetails** sectie toomonitor uitgevoerd en volgt u koppelingen tooprovisioning activiteitsrapporten, waarin alle bewerkingen die worden uitgevoerd door het Hallo-service op uw toegestane app inrichten.</span><span class="sxs-lookup"><span data-stu-id="bec3e-152">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Slack app.</span></span>

## <a name="optional-configuring-group-object-provisioning-tooslack"></a><span data-ttu-id="bec3e-153">[Optioneel] Groepsobject tooSlack inrichting configureren</span><span class="sxs-lookup"><span data-stu-id="bec3e-153">[Optional] Configuring group object provisioning tooSlack</span></span> 

<span data-ttu-id="bec3e-154">Desgewenst kunt u Hallo inrichting van groepsobjecten van Azure AD-tooSlack inschakelen.</span><span class="sxs-lookup"><span data-stu-id="bec3e-154">Optionally, you can enable hello provisioning of group objects from Azure AD tooSlack.</span></span> <span data-ttu-id="bec3e-155">Dit verschilt van het 'groepen gebruikers toe te wijzen', in Hallo werkelijke groepsobject bovendien tooits leden van Azure AD-tooSlack worden gerepliceerd.</span><span class="sxs-lookup"><span data-stu-id="bec3e-155">This is different from "assigning groups of users", in that hello actual group object in addition tooits members will be replicated from Azure AD tooSlack.</span></span> <span data-ttu-id="bec3e-156">Als u een groep met de naam 'Mijn groep' in Azure AD hebt, wordt bijvoorbeeld een identitical groep met de naam 'Mijn groep' gemaakt binnen de toegestane vertraging.</span><span class="sxs-lookup"><span data-stu-id="bec3e-156">For example, if you have a group named "My Group" in Azure AD, an identitical group named "My Group" will be created inside Slack.</span></span>

### <a name="tooenable-provisioning-of-group-objects"></a><span data-ttu-id="bec3e-157">tooenable inrichting van groepsobjecten:</span><span class="sxs-lookup"><span data-stu-id="bec3e-157">tooenable provisioning of group objects:</span></span>

1) <span data-ttu-id="bec3e-158">Selecteer onder Hallo toewijzingen sectie, **synchroniseren Azure Active Directory-groepen tooSlack**.</span><span class="sxs-lookup"><span data-stu-id="bec3e-158">Under hello Mappings section, select **Synchronize Azure Active Directory Groups tooSlack**.</span></span>

2) <span data-ttu-id="bec3e-159">Hallo kenmerk toewijzing blade ingesteld tooYes ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="bec3e-159">In hello Attribute Mapping blade, set Enabled tooYes.</span></span>

3) <span data-ttu-id="bec3e-160">In Hallo **kenmerktoewijzingen** sectie, bekijkt hello Groepkenmerken die wordt gesynchroniseerd vanaf de Azure AD-tooSlack.</span><span class="sxs-lookup"><span data-stu-id="bec3e-160">In hello **Attribute Mappings** section, review hello group attributes that will be synchronized from Azure AD tooSlack.</span></span> <span data-ttu-id="bec3e-161">Let op: kenmerken die zijn geselecteerd als Hallo **overeenkomend** eigenschappen worden gebruikte toomatch Hallo groepen in Slack voor update-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="bec3e-161">Note that hello attributes selected as **Matching** properties will be used toomatch hello groups in Slack for update operations.</span></span> 

4) <span data-ttu-id="bec3e-162">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="bec3e-162">Click **Save**.</span></span>

<span data-ttu-id="bec3e-163">Deze leiden tot een groep objecten die zijn toegewezen tooSlack in Hallo **gebruikers en groepen** sectie volledig wordt gesynchroniseerd vanuit Azure AD-tooSlack.</span><span class="sxs-lookup"><span data-stu-id="bec3e-163">This result in any group objects assigned tooSlack in hello **Users and Groups** section being fully synchronized from Azure AD tooSlack.</span></span> <span data-ttu-id="bec3e-164">U kunt Hallo **synchronisatiedetails** sectie toomonitor uitgevoerd en volgt u koppelingen tooprovisioning activiteitsrapporten, waarin alle bewerkingen die worden uitgevoerd door het Hallo-service op uw toegestane app inrichten.</span><span class="sxs-lookup"><span data-stu-id="bec3e-164">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Slack app.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="bec3e-165">Aanvullende resources</span><span class="sxs-lookup"><span data-stu-id="bec3e-165">Additional Resources</span></span>

* [<span data-ttu-id="bec3e-166">Het beheren van gebruikers account inrichten voor zakelijke Apps</span><span class="sxs-lookup"><span data-stu-id="bec3e-166">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="bec3e-167">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bec3e-167">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
