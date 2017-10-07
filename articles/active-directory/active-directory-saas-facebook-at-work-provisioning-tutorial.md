---
title: 'Zelfstudie: Werkplek door Facebook configureren voor gebruikers inrichten | Microsoft Docs'
description: Meer informatie over hoe tooautomatically leveren en intrekken gebruikersaccounts vanuit Azure AD-tooWorkplace met Facebook.
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
ms.openlocfilehash: 33d294dbc8f441b29138408b3c9ca41f2141f8af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configure-workplace-by-facebook-for-user-provisioning"></a><span data-ttu-id="9a603-103">Zelfstudie: Werkplek door Facebook configureren voor gebruikers inrichten</span><span class="sxs-lookup"><span data-stu-id="9a603-103">Tutorial: Configure Workplace by Facebook for user provisioning</span></span>

<span data-ttu-id="9a603-104">Deze zelfstudie ziet u stappen nodig tooautomatically leveren en intrekken gebruikersaccounts van Azure Active Directory (Azure AD) tooWorkplace door Facebook Hallo.</span><span class="sxs-lookup"><span data-stu-id="9a603-104">This tutorial shows you hello steps necessary tooautomatically provision and de-provision user accounts from Azure Active Directory (Azure AD) tooWorkplace by Facebook.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9a603-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="9a603-105">Prerequisites</span></span>

<span data-ttu-id="9a603-106">tooconfigure Azure AD-integratie met werkplek door Facebook, moet u de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="9a603-106">tooconfigure Azure AD integration with Workplace by Facebook, you need hello following:</span></span>

- <span data-ttu-id="9a603-107">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="9a603-107">An Azure AD subscription</span></span>
- <span data-ttu-id="9a603-108">Een werkplek door Facebook eenmalige aanmelding (SSO) abonnement ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="9a603-108">A Workplace by Facebook single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="9a603-109">tootest hello stappen in deze zelfstudie volgt u deze aanbevelingen:</span><span class="sxs-lookup"><span data-stu-id="9a603-109">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="9a603-110">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="9a603-110">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9a603-111">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een [één maand proefabonnement](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9a603-111">If you don't have an Azure AD trial environment, you can get a [one-month trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="assign-users-tooworkplace-by-facebook"></a><span data-ttu-id="9a603-112">Toewijzen van gebruikers tooWorkplace door Facebook</span><span class="sxs-lookup"><span data-stu-id="9a603-112">Assign users tooWorkplace by Facebook</span></span>

<span data-ttu-id="9a603-113">Azure AD maakt gebruik van een concept 'toewijzingen' toodetermine welke gebruikers toegang tooselected apps krijgen genoemd.</span><span class="sxs-lookup"><span data-stu-id="9a603-113">Azure AD uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="9a603-114">In de context van de Hallo van automatische gebruikers account inrichten, worden alleen Hallo-gebruikers en groepen die zijn toegewezen aan de tooan toepassing in Azure AD gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="9a603-114">In hello context of automatic user account provisioning, only hello users and groups that have been assigned tooan application in Azure AD are synchronized.</span></span>

<span data-ttu-id="9a603-115">Voordat u configureren en inschakelen van Hallo inrichting van de service, besluit welke gebruikers en groepen in Azure AD vertegenwoordigen Hallo-gebruikers die toegang moeten hebben tot tooyour werkplek door Facebook-app.</span><span class="sxs-lookup"><span data-stu-id="9a603-115">Before configuring and enabling hello provisioning service, decide what users and groups in Azure AD represent hello users who need access tooyour Workplace by Facebook app.</span></span> <span data-ttu-id="9a603-116">Vervolgens kunt u deze gebruikers tooyour werkplek door Facebook-app door de volgende instructies in Hallo [toewijzen van een gebruiker of groep tooan enterprise app](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="9a603-116">You can then assign these users tooyour Workplace by Facebook app by following hello instructions in [Assign a user or group tooan enterprise app](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal).</span></span>

>[!IMPORTANT]
>*   <span data-ttu-id="9a603-117">Test Hallo configuratie inrichten door toe te wijzen één tooWorkplace voor Azure AD-gebruiker met Facebook.</span><span class="sxs-lookup"><span data-stu-id="9a603-117">Test hello provisioning configuration by assigning a single Azure AD user tooWorkplace by Facebook.</span></span> <span data-ttu-id="9a603-118">Later extra gebruikers en groepen toewijzen.</span><span class="sxs-lookup"><span data-stu-id="9a603-118">Assign additional users and groups later.</span></span>
>*   <span data-ttu-id="9a603-119">Wanneer u een gebruiker tooWorkplace door Facebook toewijst, moet u een geldige gebruikersrol selecteren.</span><span class="sxs-lookup"><span data-stu-id="9a603-119">When you assign a user tooWorkplace by Facebook, you must select a valid user role.</span></span> <span data-ttu-id="9a603-120">Hallo standaard toegangsfunctie werkt niet voor het inrichten.</span><span class="sxs-lookup"><span data-stu-id="9a603-120">hello Default Access role does not work for provisioning.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="9a603-121">Geautomatiseerde gebruikersinrichting inschakelen</span><span class="sxs-lookup"><span data-stu-id="9a603-121">Enable automated user provisioning</span></span>

<span data-ttu-id="9a603-122">In deze sectie helpt u bij het verbinden van uw Azure AD toohello gebruikersaccount inrichten API werkplek met Facebook.</span><span class="sxs-lookup"><span data-stu-id="9a603-122">This section guides you through connecting your Azure AD toohello user account provisioning API of Workplace by Facebook.</span></span> <span data-ttu-id="9a603-123">U leert ook hoe tooconfigure Hallo inrichting service toocreate bijwerken en uitschakelen van toegewezen gebruikersaccounts in werkplek met Facebook.</span><span class="sxs-lookup"><span data-stu-id="9a603-123">You also learn how tooconfigure hello provisioning service toocreate, update, and disable assigned user accounts in Workplace by Facebook.</span></span> <span data-ttu-id="9a603-124">Dit is gebaseerd op de gebruiker en groepstoewijzing in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9a603-124">This is based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="9a603-125">U kunt ook tooenabled SAML gebaseerde SSO voor werkplek door Facebook, door Hallo instructies vindt u in Hallo [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9a603-125">You can also choose tooenabled SAML-based SSO for Workplace by Facebook, by following hello instructions provided in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="9a603-126">Eenmalige aanmelding kan worden geconfigureerd onafhankelijk van automatische inrichting, hoewel deze twee functies elkaar aanvullen.</span><span class="sxs-lookup"><span data-stu-id="9a603-126">SSO can be configured independently of automatic provisioning, though these two features complement each other.</span></span>

### <a name="configure-user-account-provisioning-tooworkplace-by-facebook-in-azure-ad"></a><span data-ttu-id="9a603-127">Gebruikersaccount tooWorkplace door Facebook-inrichting in Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="9a603-127">Configure user account provisioning tooWorkplace by Facebook in Azure AD</span></span>

<span data-ttu-id="9a603-128">Azure AD ondersteunt Hallo mogelijkheid tooautomatically synchroniseren accountdetails Hallo van toegewezen gebruikers tooWorkplace met Facebook.</span><span class="sxs-lookup"><span data-stu-id="9a603-128">Azure AD supports hello ability tooautomatically synchronize hello account details of assigned users tooWorkplace by Facebook.</span></span> <span data-ttu-id="9a603-129">Deze automatische synchronisatie kunt werkplek door Facebook tooget Hallo gegevens tooauthorize gebruikers om toegang te krijgen, voordat moet ze toosign in voor Hallo eerst geprobeerd.</span><span class="sxs-lookup"><span data-stu-id="9a603-129">This automatic synchronization enables Workplace by Facebook tooget hello data it needs tooauthorize users for access, before them attempting toosign in for hello first time.</span></span> <span data-ttu-id="9a603-130">Het ook inricht ongedaan gebruikers van werkplek door Facebook wanneer toegang in Azure AD is ingetrokken.</span><span class="sxs-lookup"><span data-stu-id="9a603-130">It also de-provisions users from Workplace by Facebook when access has been revoked in Azure AD.</span></span>

1. <span data-ttu-id="9a603-131">In Hallo [Azure-portal](https://portal.azure.com), selecteer **Azure Active Directory** > **zakelijke Apps** > **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="9a603-131">In hello [Azure portal](https://portal.azure.com), select **Azure Active Directory** > **Enterprise Apps** > **All applications**.</span></span>

2. <span data-ttu-id="9a603-132">Als u werkplek door Facebook al hebt geconfigureerd voor eenmalige aanmelding, zoekt u uw exemplaar van de werkplek door Facebook met behulp van Hallo zoekveld opgegeven.</span><span class="sxs-lookup"><span data-stu-id="9a603-132">If you have already configured Workplace by Facebook for SSO, search for your instance of Workplace by Facebook by using hello search field.</span></span> <span data-ttu-id="9a603-133">Selecteer anders **toevoegen** en zoek naar **werkplek door Facebook** in Hallo-toepassingsgalerie.</span><span class="sxs-lookup"><span data-stu-id="9a603-133">Otherwise, select **Add** and search for **Workplace by Facebook** in hello application gallery.</span></span> <span data-ttu-id="9a603-134">Selecteer **werkplek door Facebook** van Hallo zoekresultaten en toe te voegen tooyour lijst met toepassingen.</span><span class="sxs-lookup"><span data-stu-id="9a603-134">Select **Workplace by Facebook** from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="9a603-135">Selecteer uw exemplaar van de werkplek door Facebook, en selecteer vervolgens Hallo **inrichten** tabblad.</span><span class="sxs-lookup"><span data-stu-id="9a603-135">Select your instance of Workplace by Facebook, and then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="9a603-136">Stel **modus inrichting** te**automatische**.</span><span class="sxs-lookup"><span data-stu-id="9a603-136">Set **Provisioning Mode** too**Automatic**.</span></span> 

    ![Schermopname van werkplek door Facebook opties voor apparaatinrichting](./media/active-directory-saas-facebook-at-work-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="9a603-138">Onder Hallo **beheerdersreferenties** sectie, voert u Hallo **geheim Token** en Hallo **Tenant-URL** van uw werkplek door Facebook-beheerder.</span><span class="sxs-lookup"><span data-stu-id="9a603-138">Under hello **Admin Credentials** section, enter hello **Secret Token** and hello **Tenant URL** of your Workplace by Facebook administrator.</span></span>

6. <span data-ttu-id="9a603-139">Selecteer in de Azure-portal hello, **testverbinding** tooensure Azure AD verbinding tooyour werkplek door Facebook-app kunt maken.</span><span class="sxs-lookup"><span data-stu-id="9a603-139">In hello Azure portal, select **Test Connection** tooensure Azure AD can connect tooyour Workplace by Facebook app.</span></span> <span data-ttu-id="9a603-140">Als Hallo verbinding mislukt, zorg ervoor dat uw werkplek door Facebook-account Team beheerdersmachtigingen.</span><span class="sxs-lookup"><span data-stu-id="9a603-140">If hello connection fails, ensure that your Workplace by Facebook account has Team Admin permissions.</span></span>

7. <span data-ttu-id="9a603-141">Voer e-mailadres van een persoon of groep die inrichting fout meldingen in Hallo ontvangen moet Hallo **e-mailmelding** veld en schakel het selectievakje Hallo.</span><span class="sxs-lookup"><span data-stu-id="9a603-141">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello check box.</span></span>

8. <span data-ttu-id="9a603-142">Selecteer **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="9a603-142">Select **Save**.</span></span>

9. <span data-ttu-id="9a603-143">Selecteer onder Hallo toewijzingen sectie, **synchroniseren Azure Active Directory: gebruikers tooWorkplace door Facebook**.</span><span class="sxs-lookup"><span data-stu-id="9a603-143">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooWorkplace by Facebook**.</span></span>

10. <span data-ttu-id="9a603-144">In Hallo **kenmerktoewijzingen** sectie, bekijkt hello gebruikerskenmerken die worden gesynchroniseerd vanuit Azure AD-tooWorkplace met Facebook.</span><span class="sxs-lookup"><span data-stu-id="9a603-144">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooWorkplace by Facebook.</span></span> <span data-ttu-id="9a603-145">kenmerken die zijn geselecteerd als Hallo **overeenkomend** eigenschappen zijn gebruikte toomatch Hallo gebruikersaccounts op de werkplek door Facebook voor update-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="9a603-145">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Workplace by Facebook for update operations.</span></span> <span data-ttu-id="9a603-146">wijzigen, selecteert u toocommit **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="9a603-146">toocommit any changes, select **Save**.</span></span>

11. <span data-ttu-id="9a603-147">tooenable hello Azure AD provisioning-service voor werkplek door Facebook, in Hallo **instellingen** sectie, wijzigt u Hallo **inrichting Status** te**op**.</span><span class="sxs-lookup"><span data-stu-id="9a603-147">tooenable hello Azure AD provisioning service for Workplace by Facebook, in hello **Settings** section, change hello **Provisioning Status** too**On**.</span></span>

12. <span data-ttu-id="9a603-148">Selecteer **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="9a603-148">Select **Save**.</span></span>

<span data-ttu-id="9a603-149">Voor meer informatie over het tooconfigure automatische inrichting, Zie [Hallo Facebook documentatie](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers).</span><span class="sxs-lookup"><span data-stu-id="9a603-149">For more information on how tooconfigure automatic provisioning, see [hello Facebook documentation](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers).</span></span>

<span data-ttu-id="9a603-150">U kunt nu een testaccount maken.</span><span class="sxs-lookup"><span data-stu-id="9a603-150">You can now create a test account.</span></span> <span data-ttu-id="9a603-151">Wacht tot up too20 minuten tooverify die Hallo-account is gesynchroniseerd tooWorkplace met Facebook.</span><span class="sxs-lookup"><span data-stu-id="9a603-151">Wait for up too20 minutes tooverify that hello account has been synchronized tooWorkplace by Facebook.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9a603-152">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="9a603-152">Additional resources</span></span>

* [<span data-ttu-id="9a603-153">Het beheren van gebruikers account inrichten voor zakelijke apps</span><span class="sxs-lookup"><span data-stu-id="9a603-153">Managing user account provisioning for enterprise apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9a603-154">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9a603-154">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="9a603-155">Eenmalige aanmelding configureren</span><span class="sxs-lookup"><span data-stu-id="9a603-155">Configure single sign-on</span></span>](active-directory-saas-facebook-at-work-tutorial.md)

