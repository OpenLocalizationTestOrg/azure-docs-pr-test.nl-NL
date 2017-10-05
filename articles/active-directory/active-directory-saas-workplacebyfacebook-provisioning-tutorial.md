---
title: 'Zelfstudie: Azure Active Directory-integratie met werkplek door Facebook | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en werkplek met Facebook.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6341e67e-8ce6-42dc-a4ea-7295904a53ef
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 9b22679c304248ed7ba7a6bd9eaf82b64f7143cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-workplace-by-facebook-for-user-provisioning"></a><span data-ttu-id="a3f20-103">Zelfstudie: Werkplek door Facebook configureren voor gebruikers inrichten</span><span class="sxs-lookup"><span data-stu-id="a3f20-103">Tutorial: Configuring Workplace by Facebook for User Provisioning</span></span>

<span data-ttu-id="a3f20-104">Het doel van deze zelfstudie is zodat u de stappen die u moet uitvoeren op de werkplek door Facebook en Azure AD automatisch inrichten en inrichten van gebruikersaccounts vanuit Azure AD aan werkplek door Facebook ongedaan.</span><span class="sxs-lookup"><span data-stu-id="a3f20-104">The objective of this tutorial is to show you the steps you need to perform in Workplace by Facebook and Azure AD to automatically provision and de-provision user accounts from Azure AD to Workplace by Facebook.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a3f20-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a3f20-105">Prerequisites</span></span>

<span data-ttu-id="a3f20-106">Voor het configureren van Azure AD-integratie met werkplek door Facebook, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="a3f20-106">To configure Azure AD integration with Workplace by Facebook, you need the following items:</span></span>

- <span data-ttu-id="a3f20-107">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="a3f20-107">An Azure AD subscription</span></span>
- <span data-ttu-id="a3f20-108">Een werkplek door Facebook-eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="a3f20-108">A Workplace by Facebook single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a3f20-109">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="a3f20-109">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a3f20-110">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="a3f20-110">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a3f20-111">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="a3f20-111">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a3f20-112">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a3f20-112">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="assigning-users-to-workplace-by-facebook"></a><span data-ttu-id="a3f20-113">Gebruikers toewijzen aan een werkplek door Facebook</span><span class="sxs-lookup"><span data-stu-id="a3f20-113">Assigning users to Workplace by Facebook</span></span>

<span data-ttu-id="a3f20-114">Azure Active Directory gebruikt een concept 'toewijzingen' genoemd om te bepalen welke gebruikers krijgen toegang tot geselecteerde apps.</span><span class="sxs-lookup"><span data-stu-id="a3f20-114">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="a3f20-115">In de context van automatische gebruikers account inrichten, alleen de gebruikers en groepen die '' tot een toepassing in Azure AD toegewezen zijn gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="a3f20-115">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="a3f20-116">Voordat u configureren en inschakelen van de inrichting service, moet u bepalen welke gebruikers en/of groepen in Azure AD vertegenwoordigen de gebruikers die toegang nodig tot uw werkplek door Facebook-app.</span><span class="sxs-lookup"><span data-stu-id="a3f20-116">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Workplace by Facebook app.</span></span> <span data-ttu-id="a3f20-117">Als besloten, kunt u deze gebruikers toewijzen aan uw werkplek met Facebook-app door de volgende instructies te volgen:</span><span class="sxs-lookup"><span data-stu-id="a3f20-117">Once decided, you can assign these users to your Workplace by Facebook app by following the instructions here:</span></span>

[<span data-ttu-id="a3f20-118">Een gebruiker of groep toewijzen aan een enterprise-app</span><span class="sxs-lookup"><span data-stu-id="a3f20-118">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-workplace-by-facebook"></a><span data-ttu-id="a3f20-119">Belangrijke tips voor het toewijzen van gebruikers aan de werkplek door Facebook</span><span class="sxs-lookup"><span data-stu-id="a3f20-119">Important tips for assigning users to Workplace by Facebook</span></span>

*   <span data-ttu-id="a3f20-120">Het is raadzaam om één Azure AD-gebruiker is toegewezen aan een werkplek door Facebook voor het testen van de configuratie van de inrichting.</span><span class="sxs-lookup"><span data-stu-id="a3f20-120">It is recommended that a single Azure AD user is assigned to Workplace by Facebook to test the provisioning configuration.</span></span> <span data-ttu-id="a3f20-121">Extra gebruikers en/of groepen kunnen later worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="a3f20-121">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="a3f20-122">Wanneer een gebruiker toewijzen aan een werkplek door Facebook, moet u een geldige gebruikersrol selecteren.</span><span class="sxs-lookup"><span data-stu-id="a3f20-122">When assigning a user to Workplace by Facebook, you must select a valid user role.</span></span> <span data-ttu-id="a3f20-123">De rol 'Default toegang' werkt niet voor het inrichten.</span><span class="sxs-lookup"><span data-stu-id="a3f20-123">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="a3f20-124">Gebruikersinrichting inschakelen</span><span class="sxs-lookup"><span data-stu-id="a3f20-124">Enable User Provisioning</span></span>

<span data-ttu-id="a3f20-125">Deze sectie helpt u bij uw Azure AD verbinden met werkplek door Facebook van gebruikersaccount API-inrichting, en configureren van de inrichting service te maken, bijwerken en uitschakelen van toegewezen gebruikersaccounts in werkplek door Facebook op basis van gebruikers en groepen toewijzing in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a3f20-125">This section guides you through connecting your Azure AD to Workplace by Facebook's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Workplace by Facebook based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="a3f20-126">U kunt ook op basis van SAML eenmalige aanmelding is ingeschakeld voor werkplek door Facebook, vindt u de instructies te volgen in [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a3f20-126">You may also choose to enabled SAML-based Single Sign-On for Workplace by Facebook, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="a3f20-127">Eenmalige aanmelding kan worden geconfigureerd onafhankelijk van automatische inrichting, hoewel deze twee functies aanvulling van elkaar.</span><span class="sxs-lookup"><span data-stu-id="a3f20-127">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-user-account-provisioning-to-workplace-by-facebook-in-azure-ad"></a><span data-ttu-id="a3f20-128">Voor het configureren van account gebruikersaanvragen werkplek door Facebook in Azure AD:</span><span class="sxs-lookup"><span data-stu-id="a3f20-128">To configure user account provisioning to Workplace by Facebook in Azure AD:</span></span>

<span data-ttu-id="a3f20-129">Het doel van deze sectie is het overzicht van Active Directory-gebruikersaccounts aan werkplek door Facebook-inrichting inschakelen.</span><span class="sxs-lookup"><span data-stu-id="a3f20-129">The objective of this section is to outline how to enable provisioning of Active Directory user accounts to Workplace by Facebook.</span></span>

<span data-ttu-id="a3f20-130">Azure AD biedt ondersteuning voor de mogelijkheid om automatisch te synchroniseren de accountdetails van toegewezen gebruikers aan een werkplek met Facebook.</span><span class="sxs-lookup"><span data-stu-id="a3f20-130">Azure AD supports the ability to automatically synchronize the account details of assigned users to Workplace by Facebook.</span></span> <span data-ttu-id="a3f20-131">Deze automatische synchronisatie kunt werkplek met Facebook om op te halen van de vereiste gegevens voor het autoriseren van gebruikers om toegang te krijgen, vóór u wilt zich aanmelden voor de eerste keer.</span><span class="sxs-lookup"><span data-stu-id="a3f20-131">This automatic synchronization enables Workplace by Facebook to get the data it needs to authorize users for access, before them attempting to sign in for the first time.</span></span> <span data-ttu-id="a3f20-132">Het ook inricht ongedaan gebruikers van werkplek door Facebook wanneer toegang in Azure AD is ingetrokken.</span><span class="sxs-lookup"><span data-stu-id="a3f20-132">It also de-provisions users from Workplace by Facebook when access has been revoked in Azure AD.</span></span>

1. <span data-ttu-id="a3f20-133">In de [Azure-portal](https://portal.azure.com), blader naar de **Azure Active Directory** > **zakelijke Apps** > **alle toepassingen** sectie.</span><span class="sxs-lookup"><span data-stu-id="a3f20-133">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory** > **Enterprise Apps** > **All applications** section.</span></span>

2. <span data-ttu-id="a3f20-134">Als u werkplek door Facebook al hebt geconfigureerd voor eenmalige aanmelding, zoekt u uw exemplaar van de werkplek door het zoekveld met Facebook.</span><span class="sxs-lookup"><span data-stu-id="a3f20-134">If you have already configured Workplace by Facebook for single sign-on, search for your instance of Workplace by Facebook using the search field.</span></span> <span data-ttu-id="a3f20-135">Selecteer anders **toevoegen** en zoek naar **werkplek door Facebook** in de galerie met toepassingen.</span><span class="sxs-lookup"><span data-stu-id="a3f20-135">Otherwise, select **Add** and search for **Workplace by Facebook** in the application gallery.</span></span> <span data-ttu-id="a3f20-136">Werkplek door Facebook selecteert in de zoekresultaten en toe te voegen aan uw lijst met toepassingen.</span><span class="sxs-lookup"><span data-stu-id="a3f20-136">Select Workplace by Facebook from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="a3f20-137">Selecteer uw werkplek door Facebook-exemplaar en selecteer vervolgens de **inrichten** tabblad.</span><span class="sxs-lookup"><span data-stu-id="a3f20-137">Select your instance of Workplace by Facebook, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="a3f20-138">Stel de **Inrichtingsmodus** naar **automatische**.</span><span class="sxs-lookup"><span data-stu-id="a3f20-138">Set the **Provisioning Mode** to **Automatic**.</span></span> 

    ![Inrichting](./media/active-directory-saas-workplacebyfacebook-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="a3f20-140">Onder de **beheerdersreferenties** sectie, voert u het geheim Token en de Tenant-URL van uw werkplek door Facebook-beheerder.</span><span class="sxs-lookup"><span data-stu-id="a3f20-140">Under the **Admin Credentials** section, enter the Secret Token and the Tenant URL of your Workplace by Facebook administrator.</span></span>

6. <span data-ttu-id="a3f20-141">Klik in de Azure-portal op **testverbinding** om te controleren of Azure AD verbinding kunt maken met uw werkplek met Facebook-app.</span><span class="sxs-lookup"><span data-stu-id="a3f20-141">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Workplace by Facebook app.</span></span> <span data-ttu-id="a3f20-142">Als de verbinding is mislukt, zorg ervoor dat uw werkplek door Facebook-account Team beheerdersmachtigingen heeft.</span><span class="sxs-lookup"><span data-stu-id="a3f20-142">If the connection fails, ensure your Workplace by Facebook account has Team Admin permissions.</span></span>

7. <span data-ttu-id="a3f20-143">Voer het e-mailadres van een persoon of groep die in inrichting fout meldingen moet ontvangen de **e-mailmelding** veld en schakel het selectievakje in.</span><span class="sxs-lookup"><span data-stu-id="a3f20-143">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox.</span></span>

8. <span data-ttu-id="a3f20-144">Klik op **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="a3f20-144">Click **Save.**</span></span>

9. <span data-ttu-id="a3f20-145">Selecteer onder de sectie toewijzingen **synchroniseren Azure Active Directory: gebruikers aan een werkplek met Facebook.**</span><span class="sxs-lookup"><span data-stu-id="a3f20-145">Under the Mappings section, select **Synchronize Azure Active Directory Users to Workplace by Facebook.**</span></span>

10. <span data-ttu-id="a3f20-146">In de **kenmerktoewijzingen** sectie, controleert u de kenmerken van de gebruiker die zijn gesynchroniseerd vanuit Azure AD aan werkplek Facebook.</span><span class="sxs-lookup"><span data-stu-id="a3f20-146">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Workplace by Facebook.</span></span> <span data-ttu-id="a3f20-147">De kenmerken die zijn geselecteerd als **overeenkomend** eigenschappen worden gebruikt voor het overeenkomen met de gebruikersaccounts in werkplek door Facebook voor update-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="a3f20-147">The attributes selected as **Matching** properties are used to match the user accounts in Workplace by Facebook for update operations.</span></span> <span data-ttu-id="a3f20-148">Selecteer de knop Opslaan eventuele wijzigingen doorvoeren.</span><span class="sxs-lookup"><span data-stu-id="a3f20-148">Select the Save button to commit any changes.</span></span>

11. <span data-ttu-id="a3f20-149">Om de Azure AD-service voor werkplek door Facebook inricht, wijzigen de **inrichting Status** naar **op** in de **instellingen** sectie</span><span class="sxs-lookup"><span data-stu-id="a3f20-149">To enable the Azure AD provisioning service for Workplace by Facebook, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

12. <span data-ttu-id="a3f20-150">Klik op **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="a3f20-150">Click **Save.**</span></span>

<span data-ttu-id="a3f20-151">Zie voor meer informatie over het configureren van automatische inrichting [https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers)</span><span class="sxs-lookup"><span data-stu-id="a3f20-151">For more information on how to configure automatic provisioning, see [https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers)</span></span>

<span data-ttu-id="a3f20-152">U kunt nu een testaccount maken.</span><span class="sxs-lookup"><span data-stu-id="a3f20-152">You can now create a test account.</span></span> <span data-ttu-id="a3f20-153">Wacht 20 minuten duren om te verifiëren dat het account is gesynchroniseerd met werkplek met Facebook.</span><span class="sxs-lookup"><span data-stu-id="a3f20-153">Wait for up to 20 minutes to verify that the account has been synchronized to Workplace by Facebook.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a3f20-154">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="a3f20-154">Additional resources</span></span>

* [<span data-ttu-id="a3f20-155">Het beheren van gebruikers account inrichten voor zakelijke Apps</span><span class="sxs-lookup"><span data-stu-id="a3f20-155">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a3f20-156">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a3f20-156">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="a3f20-157">Eenmalige aanmelding configureren</span><span class="sxs-lookup"><span data-stu-id="a3f20-157">Configure Single Sign-on</span></span>](active-directory-saas-workplacebyfacebook-tutorial.md)

