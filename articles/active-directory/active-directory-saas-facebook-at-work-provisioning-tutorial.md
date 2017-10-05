---
title: 'Zelfstudie: Werkplek door Facebook configureren voor gebruikers inrichten | Microsoft Docs'
description: Informatie over het automatisch inrichten en de gebruikersaccounts van Azure AD aan werkplek door Facebook ongedaan in te richten.
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
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: a347eedbf5511dc83e1bc7721667441cfb87cb59
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-configure-workplace-by-facebook-for-user-provisioning"></a><span data-ttu-id="a2e37-103">Zelfstudie: Werkplek door Facebook configureren voor gebruikers inrichten</span><span class="sxs-lookup"><span data-stu-id="a2e37-103">Tutorial: Configure Workplace by Facebook for user provisioning</span></span>

<span data-ttu-id="a2e37-104">Deze zelfstudie ziet u de stappen nodig zijn voor automatisch leveren en intrekken gebruikersaccounts van Azure Active Directory (Azure AD) aan een werkplek met Facebook.</span><span class="sxs-lookup"><span data-stu-id="a2e37-104">This tutorial shows you the steps necessary to automatically provision and de-provision user accounts from Azure Active Directory (Azure AD) to Workplace by Facebook.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a2e37-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a2e37-105">Prerequisites</span></span>

<span data-ttu-id="a2e37-106">Voor het configureren van Azure AD-integratie met werkplek door Facebook, moet u het volgende:</span><span class="sxs-lookup"><span data-stu-id="a2e37-106">To configure Azure AD integration with Workplace by Facebook, you need the following:</span></span>

- <span data-ttu-id="a2e37-107">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="a2e37-107">An Azure AD subscription</span></span>
- <span data-ttu-id="a2e37-108">Een werkplek door Facebook eenmalige aanmelding (SSO) abonnement ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="a2e37-108">A Workplace by Facebook single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="a2e37-109">Test de stappen in deze zelfstudie, volgt u deze aanbevelingen:</span><span class="sxs-lookup"><span data-stu-id="a2e37-109">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="a2e37-110">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="a2e37-110">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a2e37-111">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een [één maand proefabonnement](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a2e37-111">If you don't have an Azure AD trial environment, you can get a [one-month trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="assign-users-to-workplace-by-facebook"></a><span data-ttu-id="a2e37-112">Gebruikers toewijzen aan de werkplek door Facebook</span><span class="sxs-lookup"><span data-stu-id="a2e37-112">Assign users to Workplace by Facebook</span></span>

<span data-ttu-id="a2e37-113">Azure AD gebruikt een concept 'toewijzingen' genoemd om te bepalen welke gebruikers krijgen toegang tot geselecteerde apps.</span><span class="sxs-lookup"><span data-stu-id="a2e37-113">Azure AD uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="a2e37-114">In de context van automatische gebruikers account inrichten, worden alleen de gebruikers en groepen die zijn toegewezen aan een toepassing in Azure AD gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="a2e37-114">In the context of automatic user account provisioning, only the users and groups that have been assigned to an application in Azure AD are synchronized.</span></span>

<span data-ttu-id="a2e37-115">Voordat u configureren en inschakelen van de inrichting service, bepalen welke gebruikers en groepen in Azure AD vertegenwoordigen de gebruikers die toegang nodig tot uw werkplek door Facebook-app.</span><span class="sxs-lookup"><span data-stu-id="a2e37-115">Before configuring and enabling the provisioning service, decide what users and groups in Azure AD represent the users who need access to your Workplace by Facebook app.</span></span> <span data-ttu-id="a2e37-116">U kunt vervolgens deze gebruikers toewijzen aan uw werkplek door Facebook-app door de instructies in [een gebruiker of groep toewijzen aan een app enterprise](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="a2e37-116">You can then assign these users to your Workplace by Facebook app by following the instructions in [Assign a user or group to an enterprise app](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal).</span></span>

>[!IMPORTANT]
>*   <span data-ttu-id="a2e37-117">De configuratie van de inrichting testen door het toewijzen van één Azure AD-gebruiker aan een werkplek met Facebook.</span><span class="sxs-lookup"><span data-stu-id="a2e37-117">Test the provisioning configuration by assigning a single Azure AD user to Workplace by Facebook.</span></span> <span data-ttu-id="a2e37-118">Later extra gebruikers en groepen toewijzen.</span><span class="sxs-lookup"><span data-stu-id="a2e37-118">Assign additional users and groups later.</span></span>
>*   <span data-ttu-id="a2e37-119">Wanneer u een gebruiker aan een werkplek door Facebook toewijzen, moet u een geldige gebruikersrol selecteren.</span><span class="sxs-lookup"><span data-stu-id="a2e37-119">When you assign a user to Workplace by Facebook, you must select a valid user role.</span></span> <span data-ttu-id="a2e37-120">De functie standaardtoegang werkt niet voor het inrichten.</span><span class="sxs-lookup"><span data-stu-id="a2e37-120">The Default Access role does not work for provisioning.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="a2e37-121">Geautomatiseerde gebruikersinrichting inschakelen</span><span class="sxs-lookup"><span data-stu-id="a2e37-121">Enable automated user provisioning</span></span>

<span data-ttu-id="a2e37-122">Deze sectie helpt u bij uw Azure AD verbinden met het gebruikersaccount inrichten API werkplek met Facebook.</span><span class="sxs-lookup"><span data-stu-id="a2e37-122">This section guides you through connecting your Azure AD to the user account provisioning API of Workplace by Facebook.</span></span> <span data-ttu-id="a2e37-123">U leert ook hoe u de inrichting service te maken, bijwerken en uitschakelen van toegewezen gebruikersaccounts in werkplek door Facebook configureren.</span><span class="sxs-lookup"><span data-stu-id="a2e37-123">You also learn how to configure the provisioning service to create, update, and disable assigned user accounts in Workplace by Facebook.</span></span> <span data-ttu-id="a2e37-124">Dit is gebaseerd op de gebruiker en groepstoewijzing in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a2e37-124">This is based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="a2e37-125">U kunt ook ingeschakeld SAML gebaseerde SSO voor werkplek door Facebook, door de instructies die is opgegeven in de [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a2e37-125">You can also choose to enabled SAML-based SSO for Workplace by Facebook, by following the instructions provided in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="a2e37-126">Eenmalige aanmelding kan worden geconfigureerd onafhankelijk van automatische inrichting, hoewel deze twee functies elkaar aanvullen.</span><span class="sxs-lookup"><span data-stu-id="a2e37-126">SSO can be configured independently of automatic provisioning, though these two features complement each other.</span></span>

### <a name="configure-user-account-provisioning-to-workplace-by-facebook-in-azure-ad"></a><span data-ttu-id="a2e37-127">Gebruikersaccount inrichten werkplek door Facebook in Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="a2e37-127">Configure user account provisioning to Workplace by Facebook in Azure AD</span></span>

<span data-ttu-id="a2e37-128">Azure AD biedt ondersteuning voor de mogelijkheid om automatisch te synchroniseren de accountdetails van toegewezen gebruikers aan een werkplek met Facebook.</span><span class="sxs-lookup"><span data-stu-id="a2e37-128">Azure AD supports the ability to automatically synchronize the account details of assigned users to Workplace by Facebook.</span></span> <span data-ttu-id="a2e37-129">Deze automatische synchronisatie kunt werkplek met Facebook om op te halen van de vereiste gegevens voor het autoriseren van gebruikers om toegang te krijgen, vóór u wilt zich aanmelden voor de eerste keer.</span><span class="sxs-lookup"><span data-stu-id="a2e37-129">This automatic synchronization enables Workplace by Facebook to get the data it needs to authorize users for access, before them attempting to sign in for the first time.</span></span> <span data-ttu-id="a2e37-130">Het ook inricht ongedaan gebruikers van werkplek door Facebook wanneer toegang in Azure AD is ingetrokken.</span><span class="sxs-lookup"><span data-stu-id="a2e37-130">It also de-provisions users from Workplace by Facebook when access has been revoked in Azure AD.</span></span>

1. <span data-ttu-id="a2e37-131">In de [Azure-portal](https://portal.azure.com), selecteer **Azure Active Directory** > **zakelijke Apps** > **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a2e37-131">In the [Azure portal](https://portal.azure.com), select **Azure Active Directory** > **Enterprise Apps** > **All applications**.</span></span>

2. <span data-ttu-id="a2e37-132">Als u werkplek door Facebook al hebt geconfigureerd voor eenmalige aanmelding, kunt u zoeken naar uw werkplek door Facebook-exemplaar met behulp van het zoekveld.</span><span class="sxs-lookup"><span data-stu-id="a2e37-132">If you have already configured Workplace by Facebook for SSO, search for your instance of Workplace by Facebook by using the search field.</span></span> <span data-ttu-id="a2e37-133">Selecteer anders **toevoegen** en zoek naar **werkplek door Facebook** in de galerie met toepassingen.</span><span class="sxs-lookup"><span data-stu-id="a2e37-133">Otherwise, select **Add** and search for **Workplace by Facebook** in the application gallery.</span></span> <span data-ttu-id="a2e37-134">Selecteer **werkplek door Facebook** uit de lijst met zoekresultaten en toe te voegen aan de lijst met toepassingen.</span><span class="sxs-lookup"><span data-stu-id="a2e37-134">Select **Workplace by Facebook** from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="a2e37-135">Selecteer uw exemplaar van de werkplek door Facebook, en selecteer vervolgens de **inrichten** tabblad.</span><span class="sxs-lookup"><span data-stu-id="a2e37-135">Select your instance of Workplace by Facebook, and then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="a2e37-136">Stel **Inrichtingsmodus** naar **automatische**.</span><span class="sxs-lookup"><span data-stu-id="a2e37-136">Set **Provisioning Mode** to **Automatic**.</span></span> 

    ![Schermopname van werkplek door Facebook opties voor apparaatinrichting](./media/active-directory-saas-facebook-at-work-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="a2e37-138">Onder de **beheerdersreferenties** sectie, voert u de **geheim Token** en de **Tenant-URL** van uw werkplek door Facebook-beheerder.</span><span class="sxs-lookup"><span data-stu-id="a2e37-138">Under the **Admin Credentials** section, enter the **Secret Token** and the **Tenant URL** of your Workplace by Facebook administrator.</span></span>

6. <span data-ttu-id="a2e37-139">Selecteer in de Azure-portal **testverbinding** om te controleren of Azure AD verbinding kunt maken met uw werkplek met Facebook-app.</span><span class="sxs-lookup"><span data-stu-id="a2e37-139">In the Azure portal, select **Test Connection** to ensure Azure AD can connect to your Workplace by Facebook app.</span></span> <span data-ttu-id="a2e37-140">Als de verbinding is mislukt, zorg ervoor dat uw werkplek door Facebook-account Team beheerdersmachtigingen.</span><span class="sxs-lookup"><span data-stu-id="a2e37-140">If the connection fails, ensure that your Workplace by Facebook account has Team Admin permissions.</span></span>

7. <span data-ttu-id="a2e37-141">Voer het e-mailadres van een persoon of groep die in inrichting fout meldingen moet ontvangen de **e-mailmelding** veld en schakel het selectievakje in.</span><span class="sxs-lookup"><span data-stu-id="a2e37-141">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the check box.</span></span>

8. <span data-ttu-id="a2e37-142">Selecteer **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="a2e37-142">Select **Save**.</span></span>

9. <span data-ttu-id="a2e37-143">Selecteer onder de sectie toewijzingen **synchroniseren Azure Active Directory: gebruikers aan een werkplek door Facebook**.</span><span class="sxs-lookup"><span data-stu-id="a2e37-143">Under the Mappings section, select **Synchronize Azure Active Directory Users to Workplace by Facebook**.</span></span>

10. <span data-ttu-id="a2e37-144">In de **kenmerktoewijzingen** sectie, controleert u de kenmerken van de gebruiker die zijn gesynchroniseerd vanuit Azure AD aan werkplek Facebook.</span><span class="sxs-lookup"><span data-stu-id="a2e37-144">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Workplace by Facebook.</span></span> <span data-ttu-id="a2e37-145">De kenmerken die zijn geselecteerd als **overeenkomend** eigenschappen worden gebruikt voor het overeenkomen met de gebruikersaccounts in werkplek door Facebook voor update-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="a2e37-145">The attributes selected as **Matching** properties are used to match the user accounts in Workplace by Facebook for update operations.</span></span> <span data-ttu-id="a2e37-146">Selecteer om eventuele wijzigingen doorvoert, **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="a2e37-146">To commit any changes, select **Save**.</span></span>

11. <span data-ttu-id="a2e37-147">Inschakelen van de Azure AD-service voor werkplek door Facebook, inrichten in de **instellingen** sectie, wijzigt u de **inrichting Status** naar **op**.</span><span class="sxs-lookup"><span data-stu-id="a2e37-147">To enable the Azure AD provisioning service for Workplace by Facebook, in the **Settings** section, change the **Provisioning Status** to **On**.</span></span>

12. <span data-ttu-id="a2e37-148">Selecteer **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="a2e37-148">Select **Save**.</span></span>

<span data-ttu-id="a2e37-149">Zie voor meer informatie over het configureren van automatische inrichting [de Facebook-documentatie](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers).</span><span class="sxs-lookup"><span data-stu-id="a2e37-149">For more information on how to configure automatic provisioning, see [the Facebook documentation](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers).</span></span>

<span data-ttu-id="a2e37-150">U kunt nu een testaccount maken.</span><span class="sxs-lookup"><span data-stu-id="a2e37-150">You can now create a test account.</span></span> <span data-ttu-id="a2e37-151">Wacht 20 minuten duren om te verifiëren dat het account is gesynchroniseerd met werkplek met Facebook.</span><span class="sxs-lookup"><span data-stu-id="a2e37-151">Wait for up to 20 minutes to verify that the account has been synchronized to Workplace by Facebook.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a2e37-152">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="a2e37-152">Additional resources</span></span>

* [<span data-ttu-id="a2e37-153">Het beheren van gebruikers account inrichten voor zakelijke apps</span><span class="sxs-lookup"><span data-stu-id="a2e37-153">Managing user account provisioning for enterprise apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a2e37-154">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a2e37-154">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="a2e37-155">Eenmalige aanmelding configureren</span><span class="sxs-lookup"><span data-stu-id="a2e37-155">Configure single sign-on</span></span>](active-directory-saas-facebook-at-work-tutorial.md)

