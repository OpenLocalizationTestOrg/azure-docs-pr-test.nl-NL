---
title: 'Zelfstudie: GitHub configureren voor het automatisch gebruikers inrichten met Azure Active Directory | Microsoft Docs'
description: Meer informatie over hoe tooconfigure Azure Active Directory tooautomatically leveren en intrekken gebruikersaccounts tooGitHub.
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: stevenpo
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: asmalser-msft
ms.openlocfilehash: c1f0f7a42e4f8a94db3f409cd463e13bb1bc13bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-github-for-automatic-user-provisioning"></a><span data-ttu-id="8c1f5-103">Zelfstudie: GitHub configureren voor het automatisch gebruikers inrichten</span><span class="sxs-lookup"><span data-stu-id="8c1f5-103">Tutorial: Configuring GitHub for Automatic User Provisioning</span></span>


<span data-ttu-id="8c1f5-104">Hallo-doel van deze zelfstudie is tooshow u stappen die u moet tooperform in GitHub en Azure AD tooautomatically leveren en intrekken gebruikersaccounts vanuit Azure AD tooGitHub Hallo.</span><span class="sxs-lookup"><span data-stu-id="8c1f5-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in GitHub and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooGitHub.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="8c1f5-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="8c1f5-105">Prerequisites</span></span>

<span data-ttu-id="8c1f5-106">Hallo scenario beschreven in deze zelfstudie wordt ervan uitgegaan dat u al hebt Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="8c1f5-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="8c1f5-107">Een Azure Active directory-tenant</span><span class="sxs-lookup"><span data-stu-id="8c1f5-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="8c1f5-108">Een tenant Github Hello [bedrijfsplan](https://help.github.com/articles/organization-billing-plans/#business-plan) of beter ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="8c1f5-108">A Github tenant with hello [Business plan](https://help.github.com/articles/organization-billing-plans/#business-plan) or better enabled</span></span> 
*   <span data-ttu-id="8c1f5-109">Een gebruikersaccount in GitHub met beheerdersmachtigingen</span><span class="sxs-lookup"><span data-stu-id="8c1f5-109">A user account in GitHub with Admin permissions</span></span> 

> [!NOTE]
> <span data-ttu-id="8c1f5-110">Hello Azure AD integratie inrichting is afhankelijk van Hallo [GitHub SCIM API](https://developer.github.com/v3/scim/), die beschikbaar tooGithub teams op Hallo bedrijfsplan of hoger is.</span><span class="sxs-lookup"><span data-stu-id="8c1f5-110">hello Azure AD provisioning integration relies on hello [GitHub SCIM API](https://developer.github.com/v3/scim/), which is available tooGithub teams on hello Business plan or better.</span></span>

## <a name="assigning-users-toogithub"></a><span data-ttu-id="8c1f5-111">Gebruikers tooGitHub toewijzen</span><span class="sxs-lookup"><span data-stu-id="8c1f5-111">Assigning users tooGitHub</span></span>

<span data-ttu-id="8c1f5-112">Azure Active Directory gebruikt een concept 'toewijzingen' toodetermine welke gebruikers toegang tooselected apps krijgen genoemd.</span><span class="sxs-lookup"><span data-stu-id="8c1f5-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="8c1f5-113">In de context van de Hallo van automatische gebruikers account inrichten, alleen Hallo-gebruikers en groepen die '' tooan toepassing in Azure AD toegewezen zijn gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="8c1f5-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span> 

<span data-ttu-id="8c1f5-114">Voordat u configureren en inschakelen van Hallo-service inricht, moet u toodecide welke gebruikers en/of groepen in Azure AD vertegenwoordigen Hallo-gebruikers die toegang moeten hebben tot tooyour GitHub-app.</span><span class="sxs-lookup"><span data-stu-id="8c1f5-114">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour GitHub app.</span></span> <span data-ttu-id="8c1f5-115">Als besloten, kunt u deze app-gebruikers tooyour GitHub toewijzen door hier Hallo-instructies te volgen:</span><span class="sxs-lookup"><span data-stu-id="8c1f5-115">Once decided, you can assign these users tooyour GitHub app by following hello instructions here:</span></span>

[<span data-ttu-id="8c1f5-116">Toewijzen van een gebruiker of groep tooan enterprise-app</span><span class="sxs-lookup"><span data-stu-id="8c1f5-116">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toogithub"></a><span data-ttu-id="8c1f5-117">Belangrijke tips voor het toewijzen van gebruikers tooGitHub</span><span class="sxs-lookup"><span data-stu-id="8c1f5-117">Important tips for assigning users tooGitHub</span></span>

*   <span data-ttu-id="8c1f5-118">Het is raadzaam om één tooGitHub tootest Hallo inrichting configuratie door Azure AD-gebruiker is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="8c1f5-118">It is recommended that a single Azure AD user is assigned tooGitHub tootest hello provisioning configuration.</span></span> <span data-ttu-id="8c1f5-119">Extra gebruikers en/of groepen kunnen later worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="8c1f5-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="8c1f5-120">Wanneer u een gebruiker tooGitHub toewijst, moet u beide Hallo **gebruiker** functie of een andere geldige toepassingsspecifieke-rol (indien beschikbaar) in het dialoogvenster voor Hallo-toewijzing.</span><span class="sxs-lookup"><span data-stu-id="8c1f5-120">When assigning a user tooGitHub, you must select either hello **User** role, or another valid application-specific role (if available) in hello assignment dialog.</span></span> <span data-ttu-id="8c1f5-121">Hallo **standaardtoegang** rol werkt niet voor het inrichten en deze gebruikers worden overgeslagen.</span><span class="sxs-lookup"><span data-stu-id="8c1f5-121">hello **Default Access** role does not work for provisioning, and these users are skipped.</span></span>


## <a name="configuring-user-provisioning-toogithub"></a><span data-ttu-id="8c1f5-122">Gebruikers inrichten tooGitHub configureren</span><span class="sxs-lookup"><span data-stu-id="8c1f5-122">Configuring user provisioning tooGitHub</span></span> 

<span data-ttu-id="8c1f5-123">In deze sectie helpt u bij het verbinden van uw Azure AD-tooGitHub gebruikersaccount inrichten API en Hallo service toocreate inrichting configureren, bijwerken en uitschakelen van toegewezen gebruikersaccounts in GitHub op basis van gebruikers en groepen toewijzen in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8c1f5-123">This section guides you through connecting your Azure AD tooGitHub's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in GitHub based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="8c1f5-124">U kunt ook tooenabled op basis van SAML eenmalige aanmelding voor GitHub, in het Hallo-instructies te volgen [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8c1f5-124">You may also choose tooenabled SAML-based Single Sign-On for GitHub, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="8c1f5-125">Eenmalige aanmelding kan worden geconfigureerd onafhankelijk van automatische inrichting, hoewel deze twee functies aanvulling van elkaar.</span><span class="sxs-lookup"><span data-stu-id="8c1f5-125">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-toogithub-in-azure-ad"></a><span data-ttu-id="8c1f5-126">Automatische gebruikersaccount tooGitHub ingericht in Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="8c1f5-126">Configure automatic user account provisioning tooGitHub in Azure AD</span></span>


1. <span data-ttu-id="8c1f5-127">In Hallo [Azure-portal](https://portal.azure.com), bladeren toohello **Azure Active Directory > zakelijke Apps > alle toepassingen** sectie.</span><span class="sxs-lookup"><span data-stu-id="8c1f5-127">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="8c1f5-128">Als u al GitHub hebt geconfigureerd voor eenmalige aanmelding, zoeken naar uw exemplaar van GitHub met Hallo zoekveld opgegeven.</span><span class="sxs-lookup"><span data-stu-id="8c1f5-128">If you have already configured GitHub for single sign-on, search for your instance of GitHub using hello search field.</span></span> <span data-ttu-id="8c1f5-129">Selecteer anders **toevoegen** en zoek naar **GitHub** in Hallo-toepassingsgalerie.</span><span class="sxs-lookup"><span data-stu-id="8c1f5-129">Otherwise, select **Add** and search for **GitHub** in hello application gallery.</span></span> <span data-ttu-id="8c1f5-130">Selecteer GitHub in zoekresultaten hello, en voeg deze tooyour lijst met toepassingen.</span><span class="sxs-lookup"><span data-stu-id="8c1f5-130">Select GitHub from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="8c1f5-131">Selecteer uw exemplaar van GitHub en vervolgens Hallo **inrichten** tabblad.</span><span class="sxs-lookup"><span data-stu-id="8c1f5-131">Select your instance of GitHub, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="8c1f5-132">Set Hallo **modus inrichting** te**automatische**.</span><span class="sxs-lookup"><span data-stu-id="8c1f5-132">Set hello **Provisioning Mode** too**Automatic**.</span></span>

    ![Het inrichten van GitHub](./media/active-directory-saas-github-provisioning-tutorial/GitHub1.png)

5. <span data-ttu-id="8c1f5-134">Onder Hallo **beheerdersreferenties** sectie, klikt u op **autoriseren**.</span><span class="sxs-lookup"><span data-stu-id="8c1f5-134">Under hello **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="8c1f5-135">Deze bewerking wordt een dialoogvenster met GitHub autorisatie in een nieuw browservenster geopend.</span><span class="sxs-lookup"><span data-stu-id="8c1f5-135">This operation opens a GitHub authorization dialog in a new browser window.</span></span> 

6. <span data-ttu-id="8c1f5-136">In nieuw venster hello, je aanmelden bij uw beheerdersaccount met GitHub.</span><span class="sxs-lookup"><span data-stu-id="8c1f5-136">In hello new window, sign into GitHub using your Admin account.</span></span> <span data-ttu-id="8c1f5-137">Selecteer in de resulterende autorisatie dialoogvenster Hallo Hallo GitHub team dat u wilt tooenable voor inrichting en selecteer vervolgens **autoriseren**.</span><span class="sxs-lookup"><span data-stu-id="8c1f5-137">In hello resulting authorization dialog, select hello GitHub team that you want tooenable provisioning for, and then select **Authorize**.</span></span> <span data-ttu-id="8c1f5-138">Voltooid door terug te gaan toohello Azure portal toocomplete hello configuratie inrichten.</span><span class="sxs-lookup"><span data-stu-id="8c1f5-138">Once completed, return toohello Azure portal toocomplete hello provisioning configuration.</span></span>

    ![Dialoogvenster autorisatie](./media/active-directory-saas-github-provisioning-tutorial/GitHub2.png)

7. <span data-ttu-id="8c1f5-140">Invoer in hello Azure-portal, **Tenant-URL** en klik op **testverbinding** tooensure Azure AD tooyour GitHub-app kunt verbinden.</span><span class="sxs-lookup"><span data-stu-id="8c1f5-140">In hello Azure portal, input **Tenant URL** and click **Test Connection** tooensure Azure AD can connect tooyour GitHub app.</span></span> <span data-ttu-id="8c1f5-141">Als Hallo verbinding mislukt, zorg ervoor dat uw GitHub-account beheerdersmachtigingen heeft en **Tenant-URl** is opgegeven correct en probeer het vervolgens opnieuw 'Autoriseren' stap Hallo (u kunt vormen **Tenant-URL** door regel: 'https : //api.github.com/scim/v2/organizations/ + < Organizations_name > ', kunt u uw organisaties vinden onder uw GitHub-account: **instellingen** > **organisaties**).</span><span class="sxs-lookup"><span data-stu-id="8c1f5-141">If hello connection fails, ensure your GitHub account has Admin permissions and **Tenant URl** is inputted correctly, then try hello "Authorize" step again (you can constitute **Tenant URL** by rule: "https://api.github.com/scim/v2/organizations/ + <Organizations_name>", you can find your organizations under your GitHub account: **Settings** > **Organizations**).</span></span>

    ![Dialoogvenster autorisatie](./media/active-directory-saas-github-provisioning-tutorial/GitHub3.png)

8. <span data-ttu-id="8c1f5-143">Voer e-mailadres van een persoon of groep die inrichting fout meldingen in Hallo ontvangen moet Hallo **e-mailmelding** veld en controleer Hallo selectievakje ' een e-mailmelding verzenden wanneer een fout optreedt."</span><span class="sxs-lookup"><span data-stu-id="8c1f5-143">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox "Send an email notification when a failure occurs."</span></span>

9. <span data-ttu-id="8c1f5-144">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="8c1f5-144">Click **Save**.</span></span> 

10. <span data-ttu-id="8c1f5-145">Selecteer onder Hallo toewijzingen sectie, **synchroniseren Azure Active Directory: gebruikers tooGitHub**.</span><span class="sxs-lookup"><span data-stu-id="8c1f5-145">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooGitHub**.</span></span>

11. <span data-ttu-id="8c1f5-146">In Hallo **kenmerktoewijzingen** sectie, bekijkt hello gebruikerskenmerken die worden gesynchroniseerd vanuit Azure AD-tooGitHub.</span><span class="sxs-lookup"><span data-stu-id="8c1f5-146">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooGitHub.</span></span> <span data-ttu-id="8c1f5-147">kenmerken die zijn geselecteerd als Hallo **overeenkomend** eigenschappen zijn gebruikte toomatch Hallo gebruikersaccounts in GitHub voor update-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="8c1f5-147">hello attributes selected as **Matching** properties are used toomatch hello user accounts in GitHub for update operations.</span></span> <span data-ttu-id="8c1f5-148">Selecteer Hallo knop toocommit wijzigingen zijn opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="8c1f5-148">Select hello Save button toocommit any changes.</span></span>

12. <span data-ttu-id="8c1f5-149">tooenable Hallo inrichting Azure AD-service voor GitHub, wijziging Hallo **inrichting Status** te**op** in Hallo **instellingen** sectie</span><span class="sxs-lookup"><span data-stu-id="8c1f5-149">tooenable hello Azure AD provisioning service for GitHub, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

13. <span data-ttu-id="8c1f5-150">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="8c1f5-150">Click **Save**.</span></span> 

<span data-ttu-id="8c1f5-151">Deze bewerking begint Hallo initiële synchronisatie van gebruikers en/of groepen die zijn toegewezen tooGitHub in Hallo gebruikers en groepen sectie.</span><span class="sxs-lookup"><span data-stu-id="8c1f5-151">This operation starts hello initial synchronization of any users and/or groups assigned tooGitHub in hello Users and Groups section.</span></span> <span data-ttu-id="8c1f5-152">de initiële synchronisatie Hallo duurt langer tooperform dan het volgende wordt gesynchroniseerd, die ongeveer 20 minuten optreden, zolang het Hallo-service wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8c1f5-152">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="8c1f5-153">U kunt Hallo **synchronisatiedetails** sectie toomonitor uitgevoerd en volgt u koppelingen tooprovisioning activiteitsrapporten, waarin alle bewerkingen die worden uitgevoerd door het Hallo-service inricht.</span><span class="sxs-lookup"><span data-stu-id="8c1f5-153">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service.</span></span>

<span data-ttu-id="8c1f5-154">Zie voor meer informatie over hoe tooread hello Azure AD-inrichting registreert, [rapportage over automatische account gebruikersaanvragen](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="8c1f5-154">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="8c1f5-155">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="8c1f5-155">Additional resources</span></span>

* [<span data-ttu-id="8c1f5-156">Het beheren van gebruikers account inrichten voor zakelijke Apps</span><span class="sxs-lookup"><span data-stu-id="8c1f5-156">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="8c1f5-157">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8c1f5-157">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="8c1f5-158">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8c1f5-158">Next steps</span></span>

* [<span data-ttu-id="8c1f5-159">Informatie over hoe tooreview registreert en het ophalen van rapporten over het inrichten van activiteit</span><span class="sxs-lookup"><span data-stu-id="8c1f5-159">Learn how tooreview logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
