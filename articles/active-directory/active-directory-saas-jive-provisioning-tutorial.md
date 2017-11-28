---
title: 'Zelfstudie: Azure Active Directory-integratie met Jive | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Jive.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6fbfdbe7-d66c-4305-9fea-76d6a6a92830
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 957b152fdd40d08a867e788b0cb9f7d57ed481e4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-jive-for-user-provisioning"></a><span data-ttu-id="14000-103">Zelfstudie: Jive configureren voor gebruikers inrichten</span><span class="sxs-lookup"><span data-stu-id="14000-103">Tutorial: Configuring Jive for User Provisioning</span></span>

<span data-ttu-id="14000-104">Het doel van deze zelfstudie is zodat u de stappen die u wilt uitvoeren in Jive en Azure AD aan automatisch leveren en intrekken gebruikersaccounts vanuit Azure AD te Jive.</span><span class="sxs-lookup"><span data-stu-id="14000-104">The objective of this tutorial is to show you the steps you need to perform in Jive and Azure AD to automatically provision and de-provision user accounts from Azure AD to Jive.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="14000-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="14000-105">Prerequisites</span></span>

<span data-ttu-id="14000-106">Het scenario in deze zelfstudie wordt ervan uitgegaan dat u al de volgende items hebt:</span><span class="sxs-lookup"><span data-stu-id="14000-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="14000-107">Een Azure Active directory-tenant.</span><span class="sxs-lookup"><span data-stu-id="14000-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="14000-108">Een Jive eenmalige aanmelding ingeschakeld abonnement.</span><span class="sxs-lookup"><span data-stu-id="14000-108">A Jive single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="14000-109">Een gebruikersaccount in Jive met beheerdersmachtigingen Team.</span><span class="sxs-lookup"><span data-stu-id="14000-109">A user account in Jive with Team Admin permissions.</span></span>

## <a name="assigning-users-to-jive"></a><span data-ttu-id="14000-110">Gebruikers toewijzen aan Jive</span><span class="sxs-lookup"><span data-stu-id="14000-110">Assigning users to Jive</span></span>

<span data-ttu-id="14000-111">Azure Active Directory gebruikt een concept 'toewijzingen' genoemd om te bepalen welke gebruikers krijgen toegang tot geselecteerde apps.</span><span class="sxs-lookup"><span data-stu-id="14000-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="14000-112">In de context van automatische gebruikers account inrichten, alleen de gebruikers en groepen die '' tot een toepassing in Azure AD toegewezen zijn gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="14000-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="14000-113">Voordat u configureren en inschakelen van de inrichting service, moet u om te bepalen welke gebruikers en/of groepen in Azure AD vertegenwoordigen de gebruikers die toegang tot uw app Jive nodig hebben.</span><span class="sxs-lookup"><span data-stu-id="14000-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Jive app.</span></span> <span data-ttu-id="14000-114">Als besloten, kunt u deze gebruikers toewijzen aan uw app Jive door de volgende instructies te volgen:</span><span class="sxs-lookup"><span data-stu-id="14000-114">Once decided, you can assign these users to your Jive app by following the instructions here:</span></span>

[<span data-ttu-id="14000-115">Een gebruiker of groep toewijzen aan een enterprise-app</span><span class="sxs-lookup"><span data-stu-id="14000-115">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-jive"></a><span data-ttu-id="14000-116">Belangrijke tips voor het toewijzen van gebruikers aan Jive</span><span class="sxs-lookup"><span data-stu-id="14000-116">Important tips for assigning users to Jive</span></span>

*   <span data-ttu-id="14000-117">Het is raadzaam om één Azure AD-gebruiker worden toegewezen aan Jive voor het testen van de configuratie van de inrichting.</span><span class="sxs-lookup"><span data-stu-id="14000-117">It is recommended that a single Azure AD user be assigned to Jive to test the provisioning configuration.</span></span> <span data-ttu-id="14000-118">Extra gebruikers en/of groepen kunnen later worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="14000-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="14000-119">Wanneer een gebruiker aan Jive toewijzen, moet u een geldige gebruikersrol selecteren.</span><span class="sxs-lookup"><span data-stu-id="14000-119">When assigning a user to Jive, you must select a valid user role.</span></span> <span data-ttu-id="14000-120">De rol 'Default toegang' werkt niet voor het inrichten.</span><span class="sxs-lookup"><span data-stu-id="14000-120">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="14000-121">Gebruikersinrichting inschakelen</span><span class="sxs-lookup"><span data-stu-id="14000-121">Enable User Provisioning</span></span>

<span data-ttu-id="14000-122">Deze sectie helpt u bij het verbinding maken met uw Azure AD Jive van gebruikersaccount inrichten API en configureren van de inrichting service te maken, bijwerken en uitschakelen van toegewezen gebruikersaccounts in Jive op basis van gebruikers en groepen toewijzen in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="14000-122">This section guides you through connecting your Azure AD to Jive's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Jive based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="14000-123">U kunt ook op basis van SAML Single Sign-On for Jive is ingeschakeld, vindt u de instructies te volgen in [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="14000-123">You may also choose to enabled SAML-based Single Sign-On for Jive, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="14000-124">Eenmalige aanmelding kan worden geconfigureerd onafhankelijk van automatische inrichting, hoewel deze twee functies aanvulling van elkaar.</span><span class="sxs-lookup"><span data-stu-id="14000-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-user-account-provisioning"></a><span data-ttu-id="14000-125">Configureren voor het inrichten van het account:</span><span class="sxs-lookup"><span data-stu-id="14000-125">To configure user account provisioning:</span></span>

<span data-ttu-id="14000-126">Het doel van deze sectie is het inschakelen van de gebruiker het inrichten van Active Directory-gebruikersaccounts met Jive overzicht.</span><span class="sxs-lookup"><span data-stu-id="14000-126">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to Jive.</span></span>
<span data-ttu-id="14000-127">Als onderdeel van deze procedure moet zijn u vereist voor het beveiligingstoken van een gebruiker moet u aanvragen via Jive.com.</span><span class="sxs-lookup"><span data-stu-id="14000-127">As part of this procedure, you are required to provide a user security token you need to request from Jive.com.</span></span>

1. <span data-ttu-id="14000-128">In de [Azure-portal](https://portal.azure.com), blader naar de **Azure Active Directory > zakelijke Apps > alle toepassingen** sectie.</span><span class="sxs-lookup"><span data-stu-id="14000-128">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="14000-129">Als u al Jive voor eenmalige aanmelding hebt geconfigureerd, kunt u zoeken naar uw exemplaar van Jive met behulp van het zoekveld.</span><span class="sxs-lookup"><span data-stu-id="14000-129">If you have already configured Jive for single sign-on, search for your instance of Jive using the search field.</span></span> <span data-ttu-id="14000-130">Selecteer anders **toevoegen** en zoek naar **Jive** in de galerie met toepassingen.</span><span class="sxs-lookup"><span data-stu-id="14000-130">Otherwise, select **Add** and search for **Jive** in the application gallery.</span></span> <span data-ttu-id="14000-131">Jive selecteert in de zoekresultaten en toe te voegen aan uw lijst met toepassingen.</span><span class="sxs-lookup"><span data-stu-id="14000-131">Select Jive from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="14000-132">Selecteer uw exemplaar van Jive en selecteer vervolgens de **inrichten** tabblad.</span><span class="sxs-lookup"><span data-stu-id="14000-132">Select your instance of Jive, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="14000-133">Stel de **Inrichtingsmodus** naar **automatische**.</span><span class="sxs-lookup"><span data-stu-id="14000-133">Set the **Provisioning Mode** to **Automatic**.</span></span> 

    ![Inrichting](./media/active-directory-saas-jive-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="14000-135">Onder de **beheerdersreferenties** sectie, bieden de volgende configuratie-instellingen:</span><span class="sxs-lookup"><span data-stu-id="14000-135">Under the **Admin Credentials** section, provide the following configuration settings:</span></span>
   
    <span data-ttu-id="14000-136">a.</span><span class="sxs-lookup"><span data-stu-id="14000-136">a.</span></span> <span data-ttu-id="14000-137">In de **Jive Beheerdersgebruikersnaam** textbox type een Jive accountnaam met de **systeembeheerder** profiel in Jive.com toegewezen.</span><span class="sxs-lookup"><span data-stu-id="14000-137">In the **Jive Admin User Name** textbox, type a Jive account name that has the **System Administrator** profile in Jive.com assigned.</span></span>
   
    <span data-ttu-id="14000-138">b.</span><span class="sxs-lookup"><span data-stu-id="14000-138">b.</span></span> <span data-ttu-id="14000-139">In de **Jive beheerderswachtwoord** textbox, typt u het wachtwoord voor dit account.</span><span class="sxs-lookup"><span data-stu-id="14000-139">In the **Jive Admin Password** textbox, type the password for this account.</span></span>
   
    <span data-ttu-id="14000-140">c.</span><span class="sxs-lookup"><span data-stu-id="14000-140">c.</span></span> <span data-ttu-id="14000-141">In de **Jive Tenant-URL** textbox, typ de URL van de tenant Jive.</span><span class="sxs-lookup"><span data-stu-id="14000-141">In the **Jive Tenant URL** textbox, type the Jive tenant URL.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="14000-142">De URL van de tenant Jive is de URL die wordt gebruikt door uw organisatie zich aanmelden bij Jive.</span><span class="sxs-lookup"><span data-stu-id="14000-142">The Jive tenant URL is URL that is used by your organization to log in to Jive.</span></span>  
      > <span data-ttu-id="14000-143">Normaal gesproken de URL heeft de volgende indeling: **www.\< organisatie\>. jive.com**.</span><span class="sxs-lookup"><span data-stu-id="14000-143">Typically, the URL has the following format: **www.\<organization\>.jive.com**.</span></span>          

6. <span data-ttu-id="14000-144">Klik in de Azure-portal op **testverbinding** om te controleren of Azure AD, kan verbinding maken met uw app Jive.</span><span class="sxs-lookup"><span data-stu-id="14000-144">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Jive app.</span></span>

7. <span data-ttu-id="14000-145">Voer het e-mailadres van een persoon of groep die in inrichting fout meldingen moet ontvangen de **e-mailmelding** veld en schakel het selectievakje hieronder in.</span><span class="sxs-lookup"><span data-stu-id="14000-145">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox below.</span></span>

8. <span data-ttu-id="14000-146">Klik op **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="14000-146">Click **Save.**</span></span>

9. <span data-ttu-id="14000-147">Selecteer onder de sectie toewijzingen **synchroniseren Azure Active Directory-gebruikers Jive.**</span><span class="sxs-lookup"><span data-stu-id="14000-147">Under the Mappings section, select **Synchronize Azure Active Directory Users to Jive.**</span></span>

10. <span data-ttu-id="14000-148">In de **kenmerktoewijzingen** sectie, moet u de kenmerken van de gebruiker is gesynchroniseerd vanuit Azure AD Jive controleren.</span><span class="sxs-lookup"><span data-stu-id="14000-148">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Jive.</span></span> <span data-ttu-id="14000-149">De kenmerken die zijn geselecteerd als **overeenkomend** eigenschappen overeenkomen met de gebruikersaccounts in Jive voor update-bewerkingen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="14000-149">The attributes selected as **Matching** properties are used to match the user accounts in Jive for update operations.</span></span> <span data-ttu-id="14000-150">Selecteer de knop Opslaan eventuele wijzigingen doorvoeren.</span><span class="sxs-lookup"><span data-stu-id="14000-150">Select the Save button to commit any changes.</span></span>

11. <span data-ttu-id="14000-151">Om de Azure AD-service voor Jive inricht, wijzigen de **inrichting Status** naar **op** in de sectie instellingen</span><span class="sxs-lookup"><span data-stu-id="14000-151">To enable the Azure AD provisioning service for Jive, change the **Provisioning Status** to **On** in the Settings section</span></span>

12. <span data-ttu-id="14000-152">Klik op **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="14000-152">Click **Save.**</span></span>

<span data-ttu-id="14000-153">De initiële synchronisatie van gebruikers en/of groepen die zijn toegewezen aan Jive in de sectie gebruikers en groepen wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="14000-153">It starts the initial synchronization of any users and/or groups assigned to Jive in the Users and Groups section.</span></span> <span data-ttu-id="14000-154">De eerste synchronisatie langer duren om uit te voeren dan het volgende wordt gesynchroniseerd, die ongeveer 20 minuten optreden als de service wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="14000-154">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="14000-155">U kunt de **synchronisatiedetails** sectie voortgang en volg de koppelingen voor het inrichten van de activiteitsrapporten, waarin alle acties die worden uitgevoerd door de inrichting service op uw app Jive beschrijven.</span><span class="sxs-lookup"><span data-stu-id="14000-155">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Jive app.</span></span>

<span data-ttu-id="14000-156">U kunt nu een testaccount maken.</span><span class="sxs-lookup"><span data-stu-id="14000-156">You can now create a test account.</span></span> <span data-ttu-id="14000-157">Wacht 20 minuten duren om te verifiëren dat het account is gesynchroniseerd voor Jive.</span><span class="sxs-lookup"><span data-stu-id="14000-157">Wait for up to 20 minutes to verify that the account has been synchronized to Jive.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="14000-158">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="14000-158">Additional resources</span></span>

* [<span data-ttu-id="14000-159">Het beheren van gebruikers account inrichten voor zakelijke Apps</span><span class="sxs-lookup"><span data-stu-id="14000-159">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="14000-160">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="14000-160">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="14000-161">Eenmalige aanmelding configureren</span><span class="sxs-lookup"><span data-stu-id="14000-161">Configure Single Sign-on</span></span>](active-directory-saas-jive-tutorial.md)