---
title: 'Zelfstudie: Azure Active Directory-integratie met werkplek door Facebook | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en werkplek met Facebook.
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
ms.openlocfilehash: 551ec353a5ec1da936373587688c299a6f4acca7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-workplace-by-facebook-for-user-provisioning"></a><span data-ttu-id="4cd53-103">Zelfstudie: Werkplek door Facebook configureren voor gebruikers inrichten</span><span class="sxs-lookup"><span data-stu-id="4cd53-103">Tutorial: Configuring Workplace by Facebook for User Provisioning</span></span>

<span data-ttu-id="4cd53-104">Hallo-doel van deze zelfstudie is tooshow Hallo van stappen die u moet tooperform op werkplek door Facebook en Azure AD tooautomatically leveren en intrekken gebruikersaccounts vanuit Azure AD-tooWorkplace met Facebook.</span><span class="sxs-lookup"><span data-stu-id="4cd53-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Workplace by Facebook and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooWorkplace by Facebook.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4cd53-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="4cd53-105">Prerequisites</span></span>

<span data-ttu-id="4cd53-106">Azure AD-integratie met werkplek door Facebook tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="4cd53-106">tooconfigure Azure AD integration with Workplace by Facebook, you need hello following items:</span></span>

- <span data-ttu-id="4cd53-107">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="4cd53-107">An Azure AD subscription</span></span>
- <span data-ttu-id="4cd53-108">Een werkplek door Facebook-eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="4cd53-108">A Workplace by Facebook single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4cd53-109">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="4cd53-109">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4cd53-110">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="4cd53-110">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4cd53-111">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="4cd53-111">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4cd53-112">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4cd53-112">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="assigning-users-tooworkplace-by-facebook"></a><span data-ttu-id="4cd53-113">Toewijzen van gebruikers tooWorkplace door Facebook</span><span class="sxs-lookup"><span data-stu-id="4cd53-113">Assigning users tooWorkplace by Facebook</span></span>

<span data-ttu-id="4cd53-114">Azure Active Directory gebruikt een concept 'toewijzingen' toodetermine welke gebruikers toegang tooselected apps krijgen genoemd.</span><span class="sxs-lookup"><span data-stu-id="4cd53-114">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="4cd53-115">In de context van de Hallo van automatische gebruikers account inrichten, alleen Hallo-gebruikers en groepen die '' tooan toepassing in Azure AD toegewezen zijn gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="4cd53-115">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="4cd53-116">Voordat u configureren en inschakelen van Hallo-service inricht, moet u toodecide welke gebruikers en/of groepen in Azure AD vertegenwoordigen Hallo-gebruikers die toegang moeten hebben tot tooyour werkplek door Facebook-app.</span><span class="sxs-lookup"><span data-stu-id="4cd53-116">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Workplace by Facebook app.</span></span> <span data-ttu-id="4cd53-117">Als besloten, kunt u deze gebruikers tooyour werkplek door Facebook-app kunt toewijzen door hier Hallo-instructies te volgen:</span><span class="sxs-lookup"><span data-stu-id="4cd53-117">Once decided, you can assign these users tooyour Workplace by Facebook app by following hello instructions here:</span></span>

[<span data-ttu-id="4cd53-118">Toewijzen van een gebruiker of groep tooan enterprise-app</span><span class="sxs-lookup"><span data-stu-id="4cd53-118">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-tooworkplace-by-facebook"></a><span data-ttu-id="4cd53-119">Belangrijke tips voor het toewijzen van gebruikers tooWorkplace door Facebook</span><span class="sxs-lookup"><span data-stu-id="4cd53-119">Important tips for assigning users tooWorkplace by Facebook</span></span>

*   <span data-ttu-id="4cd53-120">Het is raadzaam om één Azure AD-gebruiker tooWorkplace door Facebook tootest Hallo configuratie inrichting is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="4cd53-120">It is recommended that a single Azure AD user is assigned tooWorkplace by Facebook tootest hello provisioning configuration.</span></span> <span data-ttu-id="4cd53-121">Extra gebruikers en/of groepen kunnen later worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="4cd53-121">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="4cd53-122">U moet een geldige gebruikersrol selecteren bij het toewijzen van een gebruiker tooWorkplace met Facebook.</span><span class="sxs-lookup"><span data-stu-id="4cd53-122">When assigning a user tooWorkplace by Facebook, you must select a valid user role.</span></span> <span data-ttu-id="4cd53-123">Hallo 'Default toegang' rol werkt niet voor het inrichten.</span><span class="sxs-lookup"><span data-stu-id="4cd53-123">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="4cd53-124">Gebruikersinrichting inschakelen</span><span class="sxs-lookup"><span data-stu-id="4cd53-124">Enable User Provisioning</span></span>

<span data-ttu-id="4cd53-125">Deze sectie helpt u bij het verbinden van uw Azure AD-tooWorkplace door Facebook van gebruikersaccount inrichten API en Hallo service toocreate inrichting configureren, bijwerken en uitschakelen van toegewezen gebruikersaccounts in werkplek door Facebook op basis van gebruikers en groepen toewijzing in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4cd53-125">This section guides you through connecting your Azure AD tooWorkplace by Facebook's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Workplace by Facebook based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="4cd53-126">U kunt ook tooenabled op basis van SAML eenmalige aanmelding voor werkplek door Facebook, in het Hallo-instructies te volgen [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4cd53-126">You may also choose tooenabled SAML-based Single Sign-On for Workplace by Facebook, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="4cd53-127">Eenmalige aanmelding kan worden geconfigureerd onafhankelijk van automatische inrichting, hoewel deze twee functies aanvulling van elkaar.</span><span class="sxs-lookup"><span data-stu-id="4cd53-127">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-user-account-provisioning-tooworkplace-by-facebook-in-azure-ad"></a><span data-ttu-id="4cd53-128">tooconfigure gebruikersaccount tooWorkplace door Facebook-inrichting in Azure AD:</span><span class="sxs-lookup"><span data-stu-id="4cd53-128">tooconfigure user account provisioning tooWorkplace by Facebook in Azure AD:</span></span>

<span data-ttu-id="4cd53-129">Hallo-doel van deze sectie is het toooutline hoe tooenable inrichting van Active Directory-gebruiker tooWorkplace door Facebook-accounts.</span><span class="sxs-lookup"><span data-stu-id="4cd53-129">hello objective of this section is toooutline how tooenable provisioning of Active Directory user accounts tooWorkplace by Facebook.</span></span>

<span data-ttu-id="4cd53-130">Azure AD ondersteunt Hallo mogelijkheid tooautomatically synchroniseren accountdetails Hallo van toegewezen gebruikers tooWorkplace met Facebook.</span><span class="sxs-lookup"><span data-stu-id="4cd53-130">Azure AD supports hello ability tooautomatically synchronize hello account details of assigned users tooWorkplace by Facebook.</span></span> <span data-ttu-id="4cd53-131">Deze automatische synchronisatie kunt werkplek door Facebook tooget Hallo gegevens tooauthorize gebruikers om toegang te krijgen, voordat moet ze toosign in voor Hallo eerst geprobeerd.</span><span class="sxs-lookup"><span data-stu-id="4cd53-131">This automatic synchronization enables Workplace by Facebook tooget hello data it needs tooauthorize users for access, before them attempting toosign in for hello first time.</span></span> <span data-ttu-id="4cd53-132">Het ook inricht ongedaan gebruikers van werkplek door Facebook wanneer toegang in Azure AD is ingetrokken.</span><span class="sxs-lookup"><span data-stu-id="4cd53-132">It also de-provisions users from Workplace by Facebook when access has been revoked in Azure AD.</span></span>

1. <span data-ttu-id="4cd53-133">In Hallo [Azure-portal](https://portal.azure.com), bladeren toohello **Azure Active Directory** > **zakelijke Apps** > **alle toepassingen** sectie.</span><span class="sxs-lookup"><span data-stu-id="4cd53-133">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory** > **Enterprise Apps** > **All applications** section.</span></span>

2. <span data-ttu-id="4cd53-134">Als u werkplek door Facebook al hebt geconfigureerd voor eenmalige aanmelding, zoekt u uw exemplaar van de werkplek door Hallo zoekveld met Facebook.</span><span class="sxs-lookup"><span data-stu-id="4cd53-134">If you have already configured Workplace by Facebook for single sign-on, search for your instance of Workplace by Facebook using hello search field.</span></span> <span data-ttu-id="4cd53-135">Selecteer anders **toevoegen** en zoek naar **werkplek door Facebook** in Hallo-toepassingsgalerie.</span><span class="sxs-lookup"><span data-stu-id="4cd53-135">Otherwise, select **Add** and search for **Workplace by Facebook** in hello application gallery.</span></span> <span data-ttu-id="4cd53-136">Selecteer werkplek door Facebook in zoekresultaten hello, en voeg deze tooyour lijst met toepassingen.</span><span class="sxs-lookup"><span data-stu-id="4cd53-136">Select Workplace by Facebook from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="4cd53-137">Selecteer uw exemplaar van de werkplek door Facebook en vervolgens Hallo **inrichten** tabblad.</span><span class="sxs-lookup"><span data-stu-id="4cd53-137">Select your instance of Workplace by Facebook, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="4cd53-138">Set Hallo **modus inrichting** te**automatische**.</span><span class="sxs-lookup"><span data-stu-id="4cd53-138">Set hello **Provisioning Mode** too**Automatic**.</span></span> 

    ![Inrichting](./media/active-directory-saas-workplacebyfacebook-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="4cd53-140">Onder Hallo **beheerdersreferenties** sectie, voert u Hallo geheim Token en Hallo Tenant-URL van uw werkplek door Facebook-beheerder.</span><span class="sxs-lookup"><span data-stu-id="4cd53-140">Under hello **Admin Credentials** section, enter hello Secret Token and hello Tenant URL of your Workplace by Facebook administrator.</span></span>

6. <span data-ttu-id="4cd53-141">Klik in hello Azure-portal, op **testverbinding** tooensure Azure AD verbinding kan maken van tooyour werkplek door Facebook-app.</span><span class="sxs-lookup"><span data-stu-id="4cd53-141">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Workplace by Facebook app.</span></span> <span data-ttu-id="4cd53-142">Als Hallo verbinding mislukt, zorg ervoor dat uw werkplek door Facebook-account Team beheerdersmachtigingen heeft.</span><span class="sxs-lookup"><span data-stu-id="4cd53-142">If hello connection fails, ensure your Workplace by Facebook account has Team Admin permissions.</span></span>

7. <span data-ttu-id="4cd53-143">Voer e-mailadres van een persoon of groep die inrichting fout meldingen in Hallo ontvangen moet Hallo **e-mailmelding** veld en Hallo selectievakje.</span><span class="sxs-lookup"><span data-stu-id="4cd53-143">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox.</span></span>

8. <span data-ttu-id="4cd53-144">Klik op **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="4cd53-144">Click **Save.**</span></span>

9. <span data-ttu-id="4cd53-145">Selecteer onder Hallo toewijzingen sectie, **tooWorkplace synchroniseren Azure Active Directory-gebruikers met Facebook.**</span><span class="sxs-lookup"><span data-stu-id="4cd53-145">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooWorkplace by Facebook.**</span></span>

10. <span data-ttu-id="4cd53-146">In Hallo **kenmerktoewijzingen** sectie, bekijkt hello gebruikerskenmerken die worden gesynchroniseerd vanuit Azure AD-tooWorkplace met Facebook.</span><span class="sxs-lookup"><span data-stu-id="4cd53-146">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooWorkplace by Facebook.</span></span> <span data-ttu-id="4cd53-147">kenmerken die zijn geselecteerd als Hallo **overeenkomend** eigenschappen zijn gebruikte toomatch Hallo gebruikersaccounts op de werkplek door Facebook voor update-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="4cd53-147">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Workplace by Facebook for update operations.</span></span> <span data-ttu-id="4cd53-148">Selecteer Hallo knop toocommit wijzigingen zijn opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="4cd53-148">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="4cd53-149">tooenable Hallo inrichting Azure AD-service voor werkplek door Facebook, wijziging Hallo **inrichting Status** te**op** in Hallo **instellingen** sectie</span><span class="sxs-lookup"><span data-stu-id="4cd53-149">tooenable hello Azure AD provisioning service for Workplace by Facebook, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

12. <span data-ttu-id="4cd53-150">Klik op **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="4cd53-150">Click **Save.**</span></span>

<span data-ttu-id="4cd53-151">Voor meer informatie over het tooconfigure automatische inrichting, Zie [https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers)</span><span class="sxs-lookup"><span data-stu-id="4cd53-151">For more information on how tooconfigure automatic provisioning, see [https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers)</span></span>

<span data-ttu-id="4cd53-152">U kunt nu een testaccount maken.</span><span class="sxs-lookup"><span data-stu-id="4cd53-152">You can now create a test account.</span></span> <span data-ttu-id="4cd53-153">Wacht tot up too20 minuten tooverify die Hallo-account is gesynchroniseerd tooWorkplace met Facebook.</span><span class="sxs-lookup"><span data-stu-id="4cd53-153">Wait for up too20 minutes tooverify that hello account has been synchronized tooWorkplace by Facebook.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4cd53-154">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="4cd53-154">Additional resources</span></span>

* [<span data-ttu-id="4cd53-155">Het beheren van gebruikers account inrichten voor zakelijke Apps</span><span class="sxs-lookup"><span data-stu-id="4cd53-155">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4cd53-156">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4cd53-156">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="4cd53-157">Eenmalige aanmelding configureren</span><span class="sxs-lookup"><span data-stu-id="4cd53-157">Configure Single Sign-on</span></span>](active-directory-saas-workplacebyfacebook-tutorial.md)

