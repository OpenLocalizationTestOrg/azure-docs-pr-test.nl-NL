---
title: 'Zelfstudie: LinkedIn bevoegdheden configureren voor het automatisch gebruikers inrichten met Azure Active Directory | Microsoft Docs'
description: Informatie over het configureren van Azure Active Directory voor het automatisch inrichten en gebruikersaccounts wilt uitbreiden LinkedIn ongedaan in te richten.
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
ms.date: 04/15/2017
ms.author: asmalser-msft
ms.openlocfilehash: 526666301aad1e5284c621024649d9cd52c92d18
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-linkedin-elevate-for-automatic-user-provisioning"></a><span data-ttu-id="0e11e-103">Zelfstudie: Configureren LinkedIn uitbreiden automatisch gebruikers inrichten</span><span class="sxs-lookup"><span data-stu-id="0e11e-103">Tutorial: Configuring LinkedIn Elevate for Automatic User Provisioning</span></span>


<span data-ttu-id="0e11e-104">Het doel van deze zelfstudie is zodat u de stappen die u uitvoeren in LinkedIn uitbreiden en Azure AD wilt om automatisch inrichten en gebruikersaccounts vanuit Azure AD wilt uitbreiden LinkedIn ongedaan in te richten.</span><span class="sxs-lookup"><span data-stu-id="0e11e-104">The objective of this tutorial is to show you the steps you need to perform in LinkedIn Elevate and Azure AD to automatically provision and de-provision user accounts from Azure AD to LinkedIn Elevate.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="0e11e-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="0e11e-105">Prerequisites</span></span>

<span data-ttu-id="0e11e-106">Het scenario in deze zelfstudie wordt ervan uitgegaan dat u al de volgende items hebt:</span><span class="sxs-lookup"><span data-stu-id="0e11e-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="0e11e-107">Een Azure Active Directory-tenant</span><span class="sxs-lookup"><span data-stu-id="0e11e-107">An Azure Active Directory tenant</span></span>
*   <span data-ttu-id="0e11e-108">Een tenant LinkedIn uitbreiden</span><span class="sxs-lookup"><span data-stu-id="0e11e-108">A LinkedIn Elevate tenant</span></span> 
*   <span data-ttu-id="0e11e-109">Een administrator-account in LinkedIn worden de bevoegdheden met toegang tot het LinkedIn-Accountcentrum</span><span class="sxs-lookup"><span data-stu-id="0e11e-109">An administrator account in LinkedIn Elevate with access to the LinkedIn Account Center</span></span>

> [!NOTE]
> <span data-ttu-id="0e11e-110">Azure Active Directory is geïntegreerd met het gebruik van de bevoegdheden LinkedIn de [SCIM](http://www.simplecloud.info/) protocol.</span><span class="sxs-lookup"><span data-stu-id="0e11e-110">Azure Active Directory integrates with LinkedIn Elevate using the [SCIM](http://www.simplecloud.info/) protocol.</span></span>

## <a name="assigning-users-to-linkedin-elevate"></a><span data-ttu-id="0e11e-111">Gebruikers toewijzen aan LinkedIn uitbreiden</span><span class="sxs-lookup"><span data-stu-id="0e11e-111">Assigning users to LinkedIn Elevate</span></span>

<span data-ttu-id="0e11e-112">Azure Active Directory gebruikt een concept 'toewijzingen' genoemd om te bepalen welke gebruikers krijgen toegang tot geselecteerde apps.</span><span class="sxs-lookup"><span data-stu-id="0e11e-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="0e11e-113">In de context van automatische gebruikers account inrichten, worden alleen de gebruikers en groepen die '' tot een toepassing in Azure AD toegewezen zijn gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="0e11e-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD will be synchronized.</span></span> 

<span data-ttu-id="0e11e-114">Voordat u configureren en inschakelen van de inrichting service, moet u bepalen welke gebruikers en/of groepen in Azure AD vertegenwoordigen de gebruikers die toegang nodig tot LinkedIn uitbreiden.</span><span class="sxs-lookup"><span data-stu-id="0e11e-114">Before configuring and enabling the provisioning service, you will need to decide what users and/or groups in Azure AD represent the users who need access to LinkedIn Elevate.</span></span> <span data-ttu-id="0e11e-115">Als besloten, kunt u deze gebruikers toewijzen aan LinkedIn verhogen door de volgende instructies te volgen:</span><span class="sxs-lookup"><span data-stu-id="0e11e-115">Once decided, you can assign these users to LinkedIn Elevate by following the instructions here:</span></span>

[<span data-ttu-id="0e11e-116">Een gebruiker of groep toewijzen aan een enterprise-app</span><span class="sxs-lookup"><span data-stu-id="0e11e-116">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-to-linkedin-elevate"></a><span data-ttu-id="0e11e-117">Belangrijke tips voor het toewijzen van gebruikers wilt LinkedIn uitbreiden</span><span class="sxs-lookup"><span data-stu-id="0e11e-117">Important tips for assigning users to LinkedIn Elevate</span></span>

*   <span data-ttu-id="0e11e-118">Het is raadzaam om één Azure AD-gebruiker worden toegewezen aan het LinkedIn bevoegdheden voor het testen van de configuratie van de inrichting.</span><span class="sxs-lookup"><span data-stu-id="0e11e-118">It is recommended that a single Azure AD user be assigned to LinkedIn Elevate to test the provisioning configuration.</span></span> <span data-ttu-id="0e11e-119">Extra gebruikers en/of groepen kunnen later worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="0e11e-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="0e11e-120">Bij het toewijzen van een gebruiker wilt LinkedIn uitbreiden, moet u de **gebruiker** rol in het dialoogvenster toewijzing.</span><span class="sxs-lookup"><span data-stu-id="0e11e-120">When assigning a user to LinkedIn Elevate, you must select the **User** role in the assignment dialog.</span></span> <span data-ttu-id="0e11e-121">De rol 'Default toegang' werkt niet voor het inrichten.</span><span class="sxs-lookup"><span data-stu-id="0e11e-121">The "Default Access" role does not work for provisioning.</span></span>


## <a name="configuring-user-provisioning-to-linkedin-elevate"></a><span data-ttu-id="0e11e-122">Configuratie van gebruikers inrichten wilt LinkedIn uitbreiden</span><span class="sxs-lookup"><span data-stu-id="0e11e-122">Configuring user provisioning to LinkedIn Elevate</span></span>

<span data-ttu-id="0e11e-123">Deze sectie helpt u bij het verbinding maken met uw Azure AD LinkedIn worden de bevoegdheden van SCIM gebruikersaccount inrichten API en de inrichting service maken, bijwerken en uitschakelen configureren toegewezen gebruikersaccounts in LinkedIn worden de bevoegdheden op basis van gebruiker en groepstoewijzing in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0e11e-123">This section guides you through connecting your Azure AD to LinkedIn Elevate's SCIM user account provisioning API, and configuring the provisioning service to create, update and disable assigned user accounts in LinkedIn Elevate based on user and group assignment in Azure AD.</span></span>

<span data-ttu-id="0e11e-124">**Tip:** u kunt ook op basis van SAML eenmalige aanmelding is ingeschakeld voor het LinkedIn bevoegdheden, volgt de instructies in [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0e11e-124">**Tip:** You may also choose to enabled SAML-based Single Sign-On for LinkedIn Elevate, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="0e11e-125">Eenmalige aanmelding kan worden geconfigureerd onafhankelijk van automatische inrichting, hoewel deze twee functies elkaar aanvullen.</span><span class="sxs-lookup"><span data-stu-id="0e11e-125">Single sign-on can be configured independently of automatic provisioning, though these two features complement each other.</span></span>


### <a name="to-configure-automatic-user-account-provisioning-to-linkedin-elevate-in-azure-ad"></a><span data-ttu-id="0e11e-126">Voor het configureren van automatische account gebruikersaanvragen wilt LinkedIn uitbreiden in Azure AD:</span><span class="sxs-lookup"><span data-stu-id="0e11e-126">To configure automatic user account provisioning to LinkedIn Elevate in Azure AD:</span></span>


<span data-ttu-id="0e11e-127">De eerste stap is om op te halen van uw toegangstoken LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="0e11e-127">The first step is to retrieve your LinkedIn access token.</span></span> <span data-ttu-id="0e11e-128">Als u een ondernemingsadministrator bent, kunt u zelf een toegangstoken inrichten.</span><span class="sxs-lookup"><span data-stu-id="0e11e-128">If you are an Enterprise administrator, you can self-provision an access token.</span></span> <span data-ttu-id="0e11e-129">Ga in uw accountcentrum naar **instellingen &gt; globale instellingen** en open de **SCIM Setup** Configuratiescherm.</span><span class="sxs-lookup"><span data-stu-id="0e11e-129">In your account center, go to **Settings &gt; Global Settings** and open the **SCIM Setup** panel.</span></span>

> [!NOTE]
> <span data-ttu-id="0e11e-130">Als u het account center rechtstreeks in plaats van via een koppeling opent, kunt u met behulp van de volgende stappen kunt bereiken.</span><span class="sxs-lookup"><span data-stu-id="0e11e-130">If you are accessing the account center directly rather than through a link, you can reach it using the following steps.</span></span>

1)  <span data-ttu-id="0e11e-131">Aanmelden bij de Center-Account.</span><span class="sxs-lookup"><span data-stu-id="0e11e-131">Sign in to Account Center.</span></span>

2)  <span data-ttu-id="0e11e-132">Selecteer **Admin &gt; beheerdersinstellingen** .</span><span class="sxs-lookup"><span data-stu-id="0e11e-132">Select **Admin &gt; Admin Settings** .</span></span>

3)  <span data-ttu-id="0e11e-133">Klik op **integraties geavanceerde** op de links zijbalk.</span><span class="sxs-lookup"><span data-stu-id="0e11e-133">Click **Advanced Integrations** on the left sidebar.</span></span> <span data-ttu-id="0e11e-134">U omgeleid naar de account center.</span><span class="sxs-lookup"><span data-stu-id="0e11e-134">You are directed to the account center.</span></span>

4)  <span data-ttu-id="0e11e-135">Klik op **+ toevoegen nieuwe SCIM configuratie** en volg de procedure door in elk veld te vullen.</span><span class="sxs-lookup"><span data-stu-id="0e11e-135">Click **+ Add new SCIM configuration** and follow the procedure by filling in each field.</span></span>

> <span data-ttu-id="0e11e-136">Wanneer autoassign licenties niet is ingeschakeld, betekent dit dat alleen de gegevens van de gebruiker is gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="0e11e-136">When auto­assign licenses is not enabled, it means that only user data is synced.</span></span>

![De inrichting van LinkedIn bevoegdheden](./media/active-directory-saas-linkedin-elevate-provisioning-tutorial/linkedin_elevate1.PNG)

> <span data-ttu-id="0e11e-138">Wanneer autolicense toewijzing is ingeschakeld, moet u het toepassingsexemplaar en licentietype.</span><span class="sxs-lookup"><span data-stu-id="0e11e-138">When auto­license assignment is enabled, you need to note the application instance and license type.</span></span> <span data-ttu-id="0e11e-139">Licenties zijn toegewezen op een eerst komt, eerst basis fungeren totdat alle licenties worden gehaald.</span><span class="sxs-lookup"><span data-stu-id="0e11e-139">Licenses are assigned on a first come, first serve basis until all the licenses are taken.</span></span>

![De inrichting van LinkedIn bevoegdheden](./media/active-directory-saas-linkedin-elevate-provisioning-tutorial/linkedin_elevate2.PNG)

5)  <span data-ttu-id="0e11e-141">Klik op **Generate token**.</span><span class="sxs-lookup"><span data-stu-id="0e11e-141">Click **Generate token**.</span></span> <span data-ttu-id="0e11e-142">U ziet uw access token weergegeven onder de **toegangstoken** veld.</span><span class="sxs-lookup"><span data-stu-id="0e11e-142">You should see your access token display under the **Access token** field.</span></span>

6)  <span data-ttu-id="0e11e-143">Sla uw toegangstoken op het Klembord of de computer voordat u de pagina verlaat.</span><span class="sxs-lookup"><span data-stu-id="0e11e-143">Save your access token to your clipboard or computer before leaving the page.</span></span>

7) <span data-ttu-id="0e11e-144">Vervolgens moet u zich aanmeldt bij de [Azure-portal](https://portal.azure.com), en blader naar de **Azure Active Directory > zakelijke Apps > alle toepassingen** sectie.</span><span class="sxs-lookup"><span data-stu-id="0e11e-144">Next, sign in to the [Azure portal](https://portal.azure.com), and browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

8) <span data-ttu-id="0e11e-145">Als u al hebt geconfigureerd LinkedIn bevoegdheden voor eenmalige aanmelding, zoekt u uw exemplaar van het LinkedIn worden de bevoegdheden met het zoekveld.</span><span class="sxs-lookup"><span data-stu-id="0e11e-145">If you have already configured LinkedIn Elevate for single sign-on, search for your instance of LinkedIn Elevate using the search field.</span></span> <span data-ttu-id="0e11e-146">Selecteer anders **toevoegen** en zoek naar **LinkedIn bevoegdheden** in de galerie met toepassingen.</span><span class="sxs-lookup"><span data-stu-id="0e11e-146">Otherwise, select **Add** and search for **LinkedIn Elevate** in the application gallery.</span></span> <span data-ttu-id="0e11e-147">Selecteer LinkedIn worden de bevoegdheden van de zoekresultaten en toe te voegen aan uw lijst met toepassingen.</span><span class="sxs-lookup"><span data-stu-id="0e11e-147">Select LinkedIn Elevate from the search results, and add it to your list of applications.</span></span>

9)  <span data-ttu-id="0e11e-148">Selecteer uw exemplaar van de bevoegdheden LinkedIn en selecteer vervolgens de **inrichten** tabblad.</span><span class="sxs-lookup"><span data-stu-id="0e11e-148">Select your instance of LinkedIn Elevate, then select the **Provisioning** tab.</span></span>

10) <span data-ttu-id="0e11e-149">Stel de **Inrichtingsmodus** naar **automatische**.</span><span class="sxs-lookup"><span data-stu-id="0e11e-149">Set the **Provisioning Mode** to **Automatic**.</span></span>

![De inrichting van LinkedIn bevoegdheden](./media/active-directory-saas-linkedin-elevate-provisioning-tutorial/linkedin_elevate3.PNG)

11)  <span data-ttu-id="0e11e-151">Vul de volgende velden onder **beheerdersreferenties** :</span><span class="sxs-lookup"><span data-stu-id="0e11e-151">Fill in the following fields under **Admin Credentials** :</span></span>

* <span data-ttu-id="0e11e-152">In de **Tenant-URL** Voer https://api.linkedin.com.</span><span class="sxs-lookup"><span data-stu-id="0e11e-152">In the **Tenant URL** field, enter https://api.linkedin.com.</span></span>

* <span data-ttu-id="0e11e-153">In de **geheim Token** veld, voer het toegangstoken dat u in stap 1 hebt gemaakt en klik op **testverbinding** .</span><span class="sxs-lookup"><span data-stu-id="0e11e-153">In the **Secret Token** field, enter the access token you generated in step 1 and click **Test Connection** .</span></span>

* <span data-ttu-id="0e11e-154">U ziet een melding met succes de upperright-zijde van de portal.</span><span class="sxs-lookup"><span data-stu-id="0e11e-154">You should see a success notification on the upper­right side of   your portal.</span></span>

12) <span data-ttu-id="0e11e-155">Voer het e-mailadres van een persoon of groep die in inrichting fout meldingen moet ontvangen de **e-mailmelding** veld en schakel het selectievakje hieronder in.</span><span class="sxs-lookup"><span data-stu-id="0e11e-155">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox below.</span></span>

13) <span data-ttu-id="0e11e-156">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="0e11e-156">Click **Save**.</span></span> 

14) <span data-ttu-id="0e11e-157">In de **kenmerktoewijzingen** sectie, controleert u de gebruikers- en groepskenmerken die worden gesynchroniseerd vanuit Azure AD wilt LinkedIn uitbreiden.</span><span class="sxs-lookup"><span data-stu-id="0e11e-157">In the **Attribute Mappings** section, review the user and group attributes that will be synchronized from Azure AD to LinkedIn Elevate.</span></span> <span data-ttu-id="0e11e-158">Let op de kenmerken die zijn geselecteerd als **overeenkomend** eigenschappen overeenkomen met de gebruikersaccounts en groepen in het LinkedIn bevoegdheden voor update-bewerkingen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="0e11e-158">Note that the attributes selected as **Matching** properties will be used to match the user accounts and groups in LinkedIn Elevate for update operations.</span></span> <span data-ttu-id="0e11e-159">Selecteer de knop Opslaan eventuele wijzigingen doorvoeren.</span><span class="sxs-lookup"><span data-stu-id="0e11e-159">Select the Save button to commit any changes.</span></span>

![De inrichting van LinkedIn bevoegdheden](./media/active-directory-saas-linkedin-elevate-provisioning-tutorial/linkedin_elevate4.PNG)

15) <span data-ttu-id="0e11e-161">Om de Azure AD-service voor het uitbreiden van LinkedIn inricht, wijzigen de **inrichting Status** naar **op** in de **instellingen** sectie</span><span class="sxs-lookup"><span data-stu-id="0e11e-161">To enable the Azure AD provisioning service for LinkedIn Elevate, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

16) <span data-ttu-id="0e11e-162">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="0e11e-162">Click **Save**.</span></span> 

<span data-ttu-id="0e11e-163">Hiermee start u de initiële synchronisatie van gebruikers en/of groepen die zijn toegewezen aan het LinkedIn uitbreiden in de sectie gebruikers en groepen.</span><span class="sxs-lookup"><span data-stu-id="0e11e-163">This will start the initial synchronization of any users and/or groups assigned to LinkedIn Elevate in the Users and Groups section.</span></span> <span data-ttu-id="0e11e-164">Houd er rekening mee dat de eerste synchronisatie langer dan het volgende wordt gesynchroniseerd, die ongeveer 20 minuten optreden duurt als de service wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="0e11e-164">Note that the initial sync will take longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="0e11e-165">U kunt de **synchronisatiedetails** sectie voortgang en volg de koppelingen voor het inrichten van de activiteitsrapporten, waarin alle acties die worden uitgevoerd door de inrichting service op uw app LinkedIn bevoegdheden beschreven.</span><span class="sxs-lookup"><span data-stu-id="0e11e-165">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your LinkedIn Elevate app.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="0e11e-166">Aanvullende resources</span><span class="sxs-lookup"><span data-stu-id="0e11e-166">Additional Resources</span></span>

* [<span data-ttu-id="0e11e-167">Het beheren van gebruikers account inrichten voor zakelijke Apps</span><span class="sxs-lookup"><span data-stu-id="0e11e-167">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="0e11e-168">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0e11e-168">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
