---
title: 'Zelfstudie: Azure Active Directory-integratie met vak | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en vak.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1c959595-6e57-4954-9c0d-67ba03ee212b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 9f061f3f5a0a4825854b893150ceccc8951487de
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-box-for-automatic-user-provisioning"></a><span data-ttu-id="d9b6b-103">Zelfstudie: Vak configureren voor het automatisch gebruikers inrichten</span><span class="sxs-lookup"><span data-stu-id="d9b6b-103">Tutorial: Configuring Box for Automatic User Provisioning</span></span>

<span data-ttu-id="d9b6b-104">Het doel van deze zelfstudie is het ziet u de stappen die u wilt uitvoeren in het vak en Azure AD aan automatisch leveren en intrekken gebruikersaccounts vanuit Azure AD aan vak.</span><span class="sxs-lookup"><span data-stu-id="d9b6b-104">The objective of this tutorial is to show the steps you need to perform in Box and Azure AD to automatically provision and de-provision user accounts from Azure AD to Box.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d9b6b-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="d9b6b-105">Prerequisites</span></span>

<span data-ttu-id="d9b6b-106">Het scenario in deze zelfstudie wordt ervan uitgegaan dat u al de volgende items hebt:</span><span class="sxs-lookup"><span data-stu-id="d9b6b-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="d9b6b-107">Een Azure Active directory-tenant.</span><span class="sxs-lookup"><span data-stu-id="d9b6b-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="d9b6b-108">Een selectievakje eenmalige aanmelding ingeschakeld abonnement.</span><span class="sxs-lookup"><span data-stu-id="d9b6b-108">A Box single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="d9b6b-109">Een gebruikersaccount in het vak met beheerdersmachtigingen Team.</span><span class="sxs-lookup"><span data-stu-id="d9b6b-109">A user account in Box with Team Admin permissions.</span></span>

## <a name="assigning-users-to-box"></a><span data-ttu-id="d9b6b-110">Gebruikers toewijzen aan vak</span><span class="sxs-lookup"><span data-stu-id="d9b6b-110">Assigning users to Box</span></span> 

<span data-ttu-id="d9b6b-111">Azure Active Directory gebruikt een concept 'toewijzingen' genoemd om te bepalen welke gebruikers krijgen toegang tot geselecteerde apps.</span><span class="sxs-lookup"><span data-stu-id="d9b6b-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="d9b6b-112">In de context van automatische gebruikers account inrichten, alleen de gebruikers en groepen die '' tot een toepassing in Azure AD toegewezen zijn gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="d9b6b-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="d9b6b-113">Voordat u configureren en inschakelen van de inrichting service, moet u bepalen welke gebruikers en/of groepen in Azure AD vertegenwoordigen de gebruikers die toegang nodig tot de Box-app.</span><span class="sxs-lookup"><span data-stu-id="d9b6b-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Box app.</span></span> <span data-ttu-id="d9b6b-114">Als besloten, kunt u deze gebruikers toewijzen aan uw app vak door de volgende instructies te volgen:</span><span class="sxs-lookup"><span data-stu-id="d9b6b-114">Once decided, you can assign these users to your Box app by following the instructions here:</span></span>

[<span data-ttu-id="d9b6b-115">Een gebruiker of groep toewijzen aan een enterprise-app</span><span class="sxs-lookup"><span data-stu-id="d9b6b-115">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

## <a name="assign-users-and-groups"></a><span data-ttu-id="d9b6b-116">Gebruikers en groepen toewijzen</span><span class="sxs-lookup"><span data-stu-id="d9b6b-116">Assign users and groups</span></span>
<span data-ttu-id="d9b6b-117">De **vak > gebruikers en groepen** tabblad in de Azure portal kunt u opgeven welke gebruikers en groepen toegang moeten worden verleend aan vak.</span><span class="sxs-lookup"><span data-stu-id="d9b6b-117">The **Box > Users and Groups** tab in the Azure portal allows you to specify which users and groups should be granted access to Box.</span></span> <span data-ttu-id="d9b6b-118">Toewijzing van een gebruiker of groep zorgt ervoor dat de volgende taken uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="d9b6b-118">Assignment of a user or group causes the following things to occur:</span></span>

* <span data-ttu-id="d9b6b-119">Azure AD kan de toegewezen gebruiker (via een rechtstreekse toewijzing toe of groepslidmaatschap) om het selectievakje te verifiëren.</span><span class="sxs-lookup"><span data-stu-id="d9b6b-119">Azure AD permits the assigned user (either by direct assignment or group membership) to authenticate to Box.</span></span> <span data-ttu-id="d9b6b-120">Als een gebruiker niet is toegewezen, Azure AD staat niet toe dat ze aan te melden bij vak en retourneert een fout op de aanmeldingspagina van Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d9b6b-120">If a user is not assigned, then Azure AD does not permit them to sign in to Box and returns an error on the Azure AD sign-in page.</span></span>
* <span data-ttu-id="d9b6b-121">Een app-tegel voor Box wordt toegevoegd aan de gebruiker [toepassingsstartprogramma](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users).</span><span class="sxs-lookup"><span data-stu-id="d9b6b-121">An app tile for Box is added to the user's [application launcher](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users).</span></span>
* <span data-ttu-id="d9b6b-122">Als automatische inrichting is ingeschakeld, worden klikt u vervolgens de toegewezen gebruikers en/of groepen toegevoegd aan de inrichting wachtrij automatisch worden ingericht.</span><span class="sxs-lookup"><span data-stu-id="d9b6b-122">If automatic provisioning is enabled, then the assigned users and/or groups are added to the provisioning queue to be automatically provisioned.</span></span>
  
  * <span data-ttu-id="d9b6b-123">Als alleen gebruikersobjecten zijn geconfigureerd om te worden ingericht, vervolgens alle rechtstreeks toegewezen gebruikers in de inrichting wachtrij zijn geplaatst en alle gebruikers die lid van een toegewezen groepen zijn in de inrichting wachtrij zijn geplaatst.</span><span class="sxs-lookup"><span data-stu-id="d9b6b-123">If only user objects were configured to be provisioned, then all directly assigned users are placed in the provisioning queue, and all users that are members of any assigned groups are placed in the provisioning queue.</span></span> 
  * <span data-ttu-id="d9b6b-124">Als groepsobjecten zijn geconfigureerd om te worden ingericht, zijn alle toegewezen groepsobjecten ingericht op het selectievakje en alle gebruikers die lid zijn van die groepen.</span><span class="sxs-lookup"><span data-stu-id="d9b6b-124">If group objects were configured to be provisioned, then all assigned group objects are provisioned to Box, and all users that are members of those groups.</span></span> <span data-ttu-id="d9b6b-125">De groeps- en -lidmaatschappen blijven behouden bij het vak wordt geschreven.</span><span class="sxs-lookup"><span data-stu-id="d9b6b-125">The group and user memberships are preserved upon being written to Box.</span></span>

<span data-ttu-id="d9b6b-126">U kunt de **kenmerken > Single Sign-On** tabblad configureren welke gebruikerskenmerken (of de claims), worden aangeboden aan vak tijdens de verificatie op basis van SAML en de **kenmerken > inrichten** tab naar configureren hoe de gebruikers- en groepskenmerken wordt overgebracht van Azure AD naar vak tijdens het inrichten van bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="d9b6b-126">You can use the **Attributes > Single Sign-On** tab to configure which user attributes (or claims) are presented to Box during SAML-based authentication, and the **Attributes > Provisioning** tab to configure how user and group attributes flow from Azure AD to Box during provisioning operations.</span></span>

### <a name="important-tips-for-assigning-users-to-box"></a><span data-ttu-id="d9b6b-127">Belangrijke tips voor het toewijzen van gebruikers aan vak</span><span class="sxs-lookup"><span data-stu-id="d9b6b-127">Important tips for assigning users to Box</span></span> 

*   <span data-ttu-id="d9b6b-128">Het is raadzaam om één Azure AD-gebruiker is toegewezen aan het selectievakje voor het testen van de configuratie van de inrichting.</span><span class="sxs-lookup"><span data-stu-id="d9b6b-128">It is recommended that a single Azure AD user assigned to Box to test the provisioning configuration.</span></span> <span data-ttu-id="d9b6b-129">Extra gebruikers en/of groepen kunnen later worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="d9b6b-129">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="d9b6b-130">Wanneer een gebruiker toewijzen aan vak, moet u een geldige gebruikersrol selecteren.</span><span class="sxs-lookup"><span data-stu-id="d9b6b-130">When assigning a user to box, you must select a valid user role.</span></span> <span data-ttu-id="d9b6b-131">De rol 'Default toegang' werkt niet voor het inrichten.</span><span class="sxs-lookup"><span data-stu-id="d9b6b-131">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="d9b6b-132">Geautomatiseerde Gebruikersinrichting inschakelen</span><span class="sxs-lookup"><span data-stu-id="d9b6b-132">Enable Automated User Provisioning</span></span>

<span data-ttu-id="d9b6b-133">Deze sectie helpt bij het verbinding maken met uw Azure AD gebruikersaccount van het vak API-inrichting en configureren van de inrichting service te maken, bijwerken en uitschakelen van toegewezen gebruikersaccounts in vak op basis van gebruikers en groepen toewijzen in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d9b6b-133">This section guides through connecting your Azure AD to Box's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Box based on user and group assignment in Azure AD.</span></span>

<span data-ttu-id="d9b6b-134">Als automatische inrichting is ingeschakeld, worden klikt u vervolgens de toegewezen gebruikers en/of groepen toegevoegd aan de inrichting wachtrij automatisch worden ingericht.</span><span class="sxs-lookup"><span data-stu-id="d9b6b-134">If automatic provisioning is enabled, then the assigned users and/or groups are added to the provisioning queue to be automatically provisioned.</span></span>
    
 * <span data-ttu-id="d9b6b-135">Als er slechts gebruikersobjecten zijn geconfigureerd om te worden ingericht, en vervolgens rechtstreeks toegewezen gebruikers in de inrichting wachtrij zijn geplaatst en alle gebruikers die lid van een toegewezen groepen zijn in de inrichting wachtrij worden geplaatst.</span><span class="sxs-lookup"><span data-stu-id="d9b6b-135">If only user objects are configured to be provisioned, then directly assigned users are placed in the provisioning queue, and all users that are members of any assigned groups are placed in the provisioning queue.</span></span> 
    
 * <span data-ttu-id="d9b6b-136">Als groepsobjecten zijn geconfigureerd om te worden ingericht, zijn alle toegewezen groepsobjecten ingericht op het selectievakje en alle gebruikers die lid zijn van die groepen.</span><span class="sxs-lookup"><span data-stu-id="d9b6b-136">If group objects were configured to be provisioned, then all assigned group objects are provisioned to Box, and all users that are members of those groups.</span></span> <span data-ttu-id="d9b6b-137">De groeps- en -lidmaatschappen blijven behouden bij het vak wordt geschreven.</span><span class="sxs-lookup"><span data-stu-id="d9b6b-137">The group and user memberships are preserved upon being written to Box.</span></span>

> [!TIP] 
> <span data-ttu-id="d9b6b-138">U kunt ook op basis van SAML eenmalige aanmelding voor het selectievakje is ingeschakeld, vindt u de instructies te volgen in [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d9b6b-138">You may also choose to enabled SAML-based Single Sign-On for Box, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="d9b6b-139">Eenmalige aanmelding kan worden geconfigureerd onafhankelijk van automatische inrichting, hoewel deze twee functies aanvulling van elkaar.</span><span class="sxs-lookup"><span data-stu-id="d9b6b-139">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-automatic-user-account-provisioning"></a><span data-ttu-id="d9b6b-140">Voor het configureren van automatische account gebruikersaanvragen:</span><span class="sxs-lookup"><span data-stu-id="d9b6b-140">To configure automatic user account provisioning:</span></span>

<span data-ttu-id="d9b6b-141">Het doel van deze sectie is het inschakelen van de inrichting van Active Directory-gebruikersaccounts aan vak overzicht.</span><span class="sxs-lookup"><span data-stu-id="d9b6b-141">The objective of this section is to outline how to enable provisioning of Active Directory user accounts to Box.</span></span>

1. <span data-ttu-id="d9b6b-142">In de [Azure-portal](https://portal.azure.com), blader naar de **Azure Active Directory > zakelijke Apps > alle toepassingen** sectie.</span><span class="sxs-lookup"><span data-stu-id="d9b6b-142">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="d9b6b-143">Als u het selectievakje al hebt geconfigureerd voor eenmalige aanmelding, zoeken naar uw exemplaar van het kiezen van het zoekveld.</span><span class="sxs-lookup"><span data-stu-id="d9b6b-143">If you have already configured Box for single sign-on, search for your instance of Box using the search field.</span></span> <span data-ttu-id="d9b6b-144">Selecteer anders **toevoegen** en zoek naar **vak** in de galerie met toepassingen.</span><span class="sxs-lookup"><span data-stu-id="d9b6b-144">Otherwise, select **Add** and search for **Box** in the application gallery.</span></span> <span data-ttu-id="d9b6b-145">Schakel in in de zoekresultaten en toe te voegen aan uw lijst met toepassingen.</span><span class="sxs-lookup"><span data-stu-id="d9b6b-145">Select Box from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="d9b6b-146">Selecteer uw exemplaar van het vak en selecteer vervolgens de **inrichten** tabblad.</span><span class="sxs-lookup"><span data-stu-id="d9b6b-146">Select your instance of Box, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="d9b6b-147">Stel de **Inrichtingsmodus** naar **automatische**.</span><span class="sxs-lookup"><span data-stu-id="d9b6b-147">Set the **Provisioning Mode** to **Automatic**.</span></span> 

    ![Inrichting](./media/active-directory-saas-box-userprovisioning-tutorial/provisioning.png)

5. <span data-ttu-id="d9b6b-149">Onder de **beheerdersreferenties** sectie, klikt u op **autoriseren** een dialoogvenster voor aanmelding openen in een nieuw browservenster.</span><span class="sxs-lookup"><span data-stu-id="d9b6b-149">Under the **Admin Credentials** section, click **Authorize** to open a Box login dialog in a new browser window.</span></span>

6. <span data-ttu-id="d9b6b-150">Op de **aanmelden om toegang te verlenen aan vak** pagina, geef de vereiste referenties op en klik vervolgens op **autoriseren**.</span><span class="sxs-lookup"><span data-stu-id="d9b6b-150">On the **Login to grant access to Box** page, provide the required credentials, and then click **Authorize**.</span></span> 
   
    <span data-ttu-id="d9b6b-151">![Schakel Automatische gebruikersaanvragen](./media/active-directory-saas-box-userprovisioning-tutorial/IC769546.png "automatische gebruikersinrichting inschakelen")</span><span class="sxs-lookup"><span data-stu-id="d9b6b-151">![Enable automatic user provisioning](./media/active-directory-saas-box-userprovisioning-tutorial/IC769546.png "Enable automatic user provisioning")</span></span>

7. <span data-ttu-id="d9b6b-152">Klik op **toegang verlenen aan vak** voor het autoriseren van deze bewerking en terug te keren naar de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d9b6b-152">Click **Grant access to Box** to authorize this operation and to return to the Azure portal.</span></span> 
   
    <span data-ttu-id="d9b6b-153">![Schakel Automatische gebruikersaanvragen](./media/active-directory-saas-box-userprovisioning-tutorial/IC769549.png "automatische gebruikersinrichting inschakelen")</span><span class="sxs-lookup"><span data-stu-id="d9b6b-153">![Enable automatic user provisioning](./media/active-directory-saas-box-userprovisioning-tutorial/IC769549.png "Enable automatic user provisioning")</span></span>

8. <span data-ttu-id="d9b6b-154">Klik in de Azure-portal op **testverbinding** om te controleren of Azure AD, kan verbinding maken met uw app vak.</span><span class="sxs-lookup"><span data-stu-id="d9b6b-154">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Box app.</span></span> <span data-ttu-id="d9b6b-155">Als de verbinding is mislukt, zorg je account vak Team beheerdersmachtigingen heeft en probeer de **'Autoriseren'** stap opnieuw.</span><span class="sxs-lookup"><span data-stu-id="d9b6b-155">If the connection fails, ensure your Box account has Team Admin permissions and try the **"Authorize"** step again.</span></span>

9. <span data-ttu-id="d9b6b-156">Voer het e-mailadres van een persoon of groep die in inrichting fout meldingen moet ontvangen de **e-mailmelding** veld en schakel het selectievakje in.</span><span class="sxs-lookup"><span data-stu-id="d9b6b-156">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox.</span></span>

10. <span data-ttu-id="d9b6b-157">Klik op **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="d9b6b-157">Click **Save.**</span></span>

11. <span data-ttu-id="d9b6b-158">Selecteer onder de sectie toewijzingen **synchroniseren Azure Active Directory: gebruikers aan vak.**</span><span class="sxs-lookup"><span data-stu-id="d9b6b-158">Under the Mappings section, select **Synchronize Azure Active Directory Users to Box.**</span></span>

12. <span data-ttu-id="d9b6b-159">In de **kenmerktoewijzingen** sectie, controleert u de kenmerken van de gebruiker die zijn gesynchroniseerd vanuit Azure AD aan vak.</span><span class="sxs-lookup"><span data-stu-id="d9b6b-159">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Box.</span></span> <span data-ttu-id="d9b6b-160">De kenmerken die zijn geselecteerd als **overeenkomend** eigenschappen overeenkomen met de gebruikersaccounts in vak voor update-bewerkingen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d9b6b-160">The attributes selected as **Matching** properties are used to match the user accounts in Box for update operations.</span></span> <span data-ttu-id="d9b6b-161">Selecteer de knop Opslaan eventuele wijzigingen doorvoeren.</span><span class="sxs-lookup"><span data-stu-id="d9b6b-161">Select the Save button to commit any changes.</span></span>

13. <span data-ttu-id="d9b6b-162">Om de Azure AD-service voor Box inricht, wijzigen de **inrichting Status** naar **op** in de sectie instellingen</span><span class="sxs-lookup"><span data-stu-id="d9b6b-162">To enable the Azure AD provisioning service for Box, change the **Provisioning Status** to **On** in the Settings section</span></span>

14. <span data-ttu-id="d9b6b-163">Klik op **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="d9b6b-163">Click **Save.**</span></span>

<span data-ttu-id="d9b6b-164">De initiële synchronisatie van gebruikers en/of groepen die zijn toegewezen aan het vak in de sectie gebruikers en groepen worden gestart.</span><span class="sxs-lookup"><span data-stu-id="d9b6b-164">That starts the initial synchronization of any users and/or groups assigned to Box in the Users and Groups section.</span></span> <span data-ttu-id="d9b6b-165">De eerste synchronisatie langer duren om uit te voeren dan het volgende wordt gesynchroniseerd, die ongeveer 20 minuten optreden als de service wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d9b6b-165">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="d9b6b-166">U kunt de **synchronisatiedetails** sectie voortgang en volg de koppelingen voor het inrichten van de activiteitsrapporten, waarin alle acties die worden uitgevoerd door de inrichting service op de Box-app.</span><span class="sxs-lookup"><span data-stu-id="d9b6b-166">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Box app.</span></span>

<span data-ttu-id="d9b6b-167">U kunt nu een testaccount maken.</span><span class="sxs-lookup"><span data-stu-id="d9b6b-167">You can now create a test account.</span></span> <span data-ttu-id="d9b6b-168">Wacht 20 minuten duren om te verifiëren dat het account is gesynchroniseerd naar vak.</span><span class="sxs-lookup"><span data-stu-id="d9b6b-168">Wait for up to 20 minutes to verify that the account has been synchronized to box.</span></span>

<span data-ttu-id="d9b6b-169">In uw tenant vak gesynchroniseerde gebruikers worden vermeld in **beheerde gebruikers** in de **beheerconsole**.</span><span class="sxs-lookup"><span data-stu-id="d9b6b-169">In your Box tenant, synchronized users are listed under **Managed Users** in the **Admin Console**.</span></span>

<span data-ttu-id="d9b6b-170">![Integratiestatus](./media/active-directory-saas-box-userprovisioning-tutorial/IC769556.png "integratie-status")</span><span class="sxs-lookup"><span data-stu-id="d9b6b-170">![Integration status](./media/active-directory-saas-box-userprovisioning-tutorial/IC769556.png "Integration status")</span></span>


## <a name="additional-resources"></a><span data-ttu-id="d9b6b-171">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="d9b6b-171">Additional resources</span></span>

* [<span data-ttu-id="d9b6b-172">Het beheren van gebruikers account inrichten voor zakelijke Apps</span><span class="sxs-lookup"><span data-stu-id="d9b6b-172">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d9b6b-173">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d9b6b-173">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="d9b6b-174">Eenmalige aanmelding configureren</span><span class="sxs-lookup"><span data-stu-id="d9b6b-174">Configure Single Sign-on</span></span>](active-directory-saas-box-tutorial.md)