---
title: 'Zelfstudie: Azure Active Directory-integratie met Concur | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Concur.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: df47f55f-a894-4e01-a82e-0dbf55fc8af1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 13ba364af26a5ce0f1d2b51aaa0f84a4c353b107
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-concur-for-user-provisioning"></a><span data-ttu-id="efe14-103">Zelfstudie: Configureren voor gebruikers inrichten instemming</span><span class="sxs-lookup"><span data-stu-id="efe14-103">Tutorial: Configuring Concur for User Provisioning</span></span>

<span data-ttu-id="efe14-104">Hallo-doel van deze zelfstudie is tooshow u stappen die u moet tooperform in Concur en Azure AD tooautomatically leveren en intrekken gebruikersaccounts vanuit Azure AD tooConcur Hallo.</span><span class="sxs-lookup"><span data-stu-id="efe14-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Concur and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooConcur.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="efe14-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="efe14-105">Prerequisites</span></span>

<span data-ttu-id="efe14-106">Hallo scenario beschreven in deze zelfstudie wordt ervan uitgegaan dat u al hebt Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="efe14-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="efe14-107">Een Azure Active directory-tenant.</span><span class="sxs-lookup"><span data-stu-id="efe14-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="efe14-108">Een Concur eenmalige aanmelding ingeschakeld abonnement.</span><span class="sxs-lookup"><span data-stu-id="efe14-108">A Concur single sign-on enabled subscription.</span></span>
*   <span data-ttu-id="efe14-109">Een gebruikersaccount in Concur met beheerdersmachtigingen Team.</span><span class="sxs-lookup"><span data-stu-id="efe14-109">A user account in Concur with Team Admin permissions.</span></span>

## <a name="assigning-users-tooconcur"></a><span data-ttu-id="efe14-110">Gebruikers tooConcur toewijzen</span><span class="sxs-lookup"><span data-stu-id="efe14-110">Assigning users tooConcur</span></span>

<span data-ttu-id="efe14-111">Azure Active Directory gebruikt een concept 'toewijzingen' toodetermine welke gebruikers toegang tooselected apps krijgen genoemd.</span><span class="sxs-lookup"><span data-stu-id="efe14-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="efe14-112">In de context van de Hallo van automatische gebruikers account inrichten, alleen Hallo-gebruikers en groepen die '' tooan toepassing in Azure AD toegewezen zijn gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="efe14-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="efe14-113">Voordat u configureren en inschakelen van Hallo-service inricht, moet u toodecide welke gebruikers en/of groepen in Azure AD vertegenwoordigen Hallo-gebruikers die toegang moeten hebben tot tooyour Concur app.</span><span class="sxs-lookup"><span data-stu-id="efe14-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Concur app.</span></span> <span data-ttu-id="efe14-114">Als besloten, kunt u deze app-gebruikers tooyour Concur toewijzen door hier Hallo-instructies te volgen:</span><span class="sxs-lookup"><span data-stu-id="efe14-114">Once decided, you can assign these users tooyour Concur app by following hello instructions here:</span></span>

[<span data-ttu-id="efe14-115">Toewijzen van een gebruiker of groep tooan enterprise-app</span><span class="sxs-lookup"><span data-stu-id="efe14-115">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-tooconcur"></a><span data-ttu-id="efe14-116">Belangrijke tips voor het toewijzen van gebruikers tooConcur</span><span class="sxs-lookup"><span data-stu-id="efe14-116">Important tips for assigning users tooConcur</span></span>

*   <span data-ttu-id="efe14-117">Het is raadzaam om één Azure AD-gebruiker tooConcur tootest Hallo inrichting configuratie worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="efe14-117">It is recommended that a single Azure AD user be assigned tooConcur tootest hello provisioning configuration.</span></span> <span data-ttu-id="efe14-118">Extra gebruikers en/of groepen kunnen later worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="efe14-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="efe14-119">Wanneer u een gebruiker tooConcur toewijst, moet u een geldige gebruikersrol.</span><span class="sxs-lookup"><span data-stu-id="efe14-119">When assigning a user tooConcur, you must select a valid user role.</span></span> <span data-ttu-id="efe14-120">Hallo 'Default toegang' rol werkt niet voor het inrichten.</span><span class="sxs-lookup"><span data-stu-id="efe14-120">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="efe14-121">Gebruikersinrichting inschakelen</span><span class="sxs-lookup"><span data-stu-id="efe14-121">Enable user provisioning</span></span>

<span data-ttu-id="efe14-122">Deze sectie helpt u bij het verbinden van uw Azure AD-tooConcur gebruikersaccount inrichten API en Hallo service toocreate inrichting configureren, bijwerken en uitschakelen toegewezen gebruikersaccounts in Concur op basis van gebruikers en groepen toewijzen in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="efe14-122">This section guides you through connecting your Azure AD tooConcur's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Concur based on user and group assignment in Azure AD.</span></span>

> [!Tip] 
> <span data-ttu-id="efe14-123">U kunt ook tooenabled op basis van SAML eenmalige aanmelding voor Concur, in het Hallo-instructies te volgen [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="efe14-123">You may also choose tooenabled SAML-based Single Sign-On for Concur, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="efe14-124">Eenmalige aanmelding kan worden geconfigureerd onafhankelijk van automatische inrichting, hoewel deze twee functies aanvulling van elkaar.</span><span class="sxs-lookup"><span data-stu-id="efe14-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-user-account-provisioning"></a><span data-ttu-id="efe14-125">tooconfigure account gebruikersaanvragen:</span><span class="sxs-lookup"><span data-stu-id="efe14-125">tooconfigure user account provisioning:</span></span>

<span data-ttu-id="efe14-126">Hallo-doel van deze sectie is het toooutline hoe tooConcur tooenable het inrichten van Active Directory-gebruiker accounts.</span><span class="sxs-lookup"><span data-stu-id="efe14-126">hello objective of this section is toooutline how tooenable provisioning of Active Directory user accounts tooConcur.</span></span>

<span data-ttu-id="efe14-127">tooenable toepassingen in de Service onkosten Hallo, er is de juiste instelling toobe en het gebruik van een profiel voor een Web-servicebeheerder.</span><span class="sxs-lookup"><span data-stu-id="efe14-127">tooenable apps in hello Expense Service, there has toobe proper setup and use of a Web Service Admin profile.</span></span> <span data-ttu-id="efe14-128">Voeg niet Hallo WS Admin rol tooyour bestaande beheerdersprofiel dat u voor T & en beheerfuncties gebruikt.</span><span class="sxs-lookup"><span data-stu-id="efe14-128">Don't add hello WS Admin role tooyour existing administrator profile that you use for T&E administrative functions.</span></span>

<span data-ttu-id="efe14-129">Instemming adviseurs of Hallo client beheerder moet een afzonderlijke Service webbeheerder-profiel maken en Hallo Client administrator moet dit profiel gebruiken voor Hallo Web Services-beheerder functies (bijvoorbeeld inschakelen apps).</span><span class="sxs-lookup"><span data-stu-id="efe14-129">Concur Consultants or hello client administrator must create a distinct Web Service Administrator profile and hello Client administrator must use this profile for hello Web Services Administrator functions (for example, enabling apps).</span></span> <span data-ttu-id="efe14-130">Deze profielen moeten gescheiden worden gehouden van Hallo client dagelijkse d & E admin beheerdersprofiel (Hallo T & E admin profiel mag geen Hallo WSAdmin rol toegewezen).</span><span class="sxs-lookup"><span data-stu-id="efe14-130">These profiles must be kept separate from hello client administrator's daily T&E admin profile (hello T&E admin profile should not have hello WSAdmin role assigned).</span></span>

<span data-ttu-id="efe14-131">Wanneer u Hallo profiel toobe gebruikt voor het inschakelen van Hallo-app maakt, aangaan Hallo client beheerder Hallo gebruiker profiel velden.</span><span class="sxs-lookup"><span data-stu-id="efe14-131">When you create hello profile toobe used for enabling hello app, enter hello client administrator's name into hello user profile fields.</span></span> <span data-ttu-id="efe14-132">Hiermee wijst eigendom toohello profiel toe.</span><span class="sxs-lookup"><span data-stu-id="efe14-132">This assigns ownership toohello profile.</span></span> <span data-ttu-id="efe14-133">Zodra een of meer profielen is gemaakt, Hallo-client moet aanmelden met dit profiel tooclick Hallo '*inschakelen*' knop voor een App-Partner in het Hallo-webservices menu.</span><span class="sxs-lookup"><span data-stu-id="efe14-133">Once one or more profiles is created, hello client must log in with this profile tooclick hello "*Enable*" button for a Partner App within hello Web Services menu.</span></span>

<span data-ttu-id="efe14-134">Voor Hallo redenen te volgen, moet deze actie niet met Hallo profiel die ze voor normale T & en beheer gebruiken worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="efe14-134">For hello following reasons, this action should not be done with hello profile they use for normal T&E administration.</span></span>

* <span data-ttu-id="efe14-135">Hallo client heeft toobe Hallo die klikt op '*Ja*' hello dialoog venster dat wordt weergegeven nadat een app is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="efe14-135">hello client has toobe hello one that clicks "*Yes*" on hello dialogue window that is displayed after an app is enabled.</span></span> <span data-ttu-id="efe14-136">Klikt u op bevestigt Hallo-client is bereid voor Hallo Partner toepassing tooaccess hun gegevens, zodat u of Hallo Partner kan niet klikt u op dat Ja knop.</span><span class="sxs-lookup"><span data-stu-id="efe14-136">This click acknowledges hello client is willing for hello Partner application tooaccess their data, so you or hello Partner cannot click that Yes button.</span></span>

* <span data-ttu-id="efe14-137">Als de beheerder van een client die een app met Hallo T & E admin profiel heeft ingeschakeld achterlaat Hallo bedrijf (waardoor Hallo-profiel wordt uitgeschakeld), alle apps ingeschakeld met behulp van dit profiel werkt niet totdat het Hallo-app met een andere actieve WS-beheer is ingeschakeld profiel.</span><span class="sxs-lookup"><span data-stu-id="efe14-137">If a client administrator that has enabled an app using hello T&E admin profile leaves hello company (resulting in hello profile being inactivated), any apps enabled using that profile does not function until hello app is enabled with another active WS Admin profile.</span></span> <span data-ttu-id="efe14-138">Dit is de reden waarom u gewoonlijk toocreate distinct WS Admin profielen.</span><span class="sxs-lookup"><span data-stu-id="efe14-138">This is why you are supposed toocreate distinct WS Admin profiles.</span></span>

* <span data-ttu-id="efe14-139">Als een beheerder Hallo bedrijf verlaat, gekoppelde Hallo naam toohello WS-beheerder kan profiel gewijzigde toohello vervanging beheerder zijn indien gewenst zonder enige impact op Hallo ingeschakeld app omdat dit profiel niet hoeft deactiveren.</span><span class="sxs-lookup"><span data-stu-id="efe14-139">If an administrator leaves hello company, hello name associated toohello WS Admin profile can be changed toohello replacement administrator if desired without impacting hello enabled app because that profile does not need inactivated.</span></span>

<span data-ttu-id="efe14-140">**tooconfigure gebruikers inrichten, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="efe14-140">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="efe14-141">Meld u aan tooyour **Concur** tenant.</span><span class="sxs-lookup"><span data-stu-id="efe14-141">Log on tooyour **Concur** tenant.</span></span>

2. <span data-ttu-id="efe14-142">Van Hallo **beheer** selecteert u **webservices**.</span><span class="sxs-lookup"><span data-stu-id="efe14-142">From hello **Administration** menu, select **Web Services**.</span></span>
   
    <span data-ttu-id="efe14-143">![Concur tenant](./media/active-directory-saas-concur-provisioning-tutorial/IC721729.png "Concur tenant")</span><span class="sxs-lookup"><span data-stu-id="efe14-143">![Concur tenant](./media/active-directory-saas-concur-provisioning-tutorial/IC721729.png "Concur tenant")</span></span>

3. <span data-ttu-id="efe14-144">Op de linkerkant van Hallo Hallo **webservices** deelvenster **partnertoepassing inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="efe14-144">On hello left side, from hello **Web Services** pane, select **Enable Partner Application**.</span></span>
   
    <span data-ttu-id="efe14-145">![Partnertoepassing inschakelen](./media/active-directory-saas-concur-provisioning-tutorial/ic721730.png "partnertoepassing inschakelen")</span><span class="sxs-lookup"><span data-stu-id="efe14-145">![Enable Partner Application](./media/active-directory-saas-concur-provisioning-tutorial/ic721730.png "Enable Partner Application")</span></span>

4. <span data-ttu-id="efe14-146">Van Hallo **toepassing inschakelen** selecteert **Azure Active Directory**, en klik vervolgens op **inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="efe14-146">From hello **Enable Application** list, select **Azure Active Directory**, and then click **Enable**.</span></span>
   
    <span data-ttu-id="efe14-147">![Microsoft Azure Active Directory](./media/active-directory-saas-concur-provisioning-tutorial/ic721731.png "Microsoft Azure Active Directory")</span><span class="sxs-lookup"><span data-stu-id="efe14-147">![Microsoft Azure Active Directory](./media/active-directory-saas-concur-provisioning-tutorial/ic721731.png "Microsoft Azure Active Directory")</span></span>

5. <span data-ttu-id="efe14-148">Klik op **Ja** tooclose hello **bevestigen actie** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="efe14-148">Click **Yes** tooclose hello **Confirm Action** dialog.</span></span>
   
    <span data-ttu-id="efe14-149">![Bevestig de actie](./media/active-directory-saas-concur-provisioning-tutorial/ic721732.png "Bevestig de actie")</span><span class="sxs-lookup"><span data-stu-id="efe14-149">![Confirm Action](./media/active-directory-saas-concur-provisioning-tutorial/ic721732.png "Confirm Action")</span></span>

6. <span data-ttu-id="efe14-150">In Hallo [Azure-portal](https://portal.azure.com), bladeren toohello **Azure Active Directory > zakelijke Apps > alle toepassingen** sectie.</span><span class="sxs-lookup"><span data-stu-id="efe14-150">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

7. <span data-ttu-id="efe14-151">Als u Concur al hebt geconfigureerd voor eenmalige aanmelding, zoekt u uw exemplaar van Concur met Hallo zoekveld opgegeven.</span><span class="sxs-lookup"><span data-stu-id="efe14-151">If you have already configured Concur for single sign-on, search for your instance of Concur using hello search field.</span></span> <span data-ttu-id="efe14-152">Selecteer anders **toevoegen** en zoek naar **Concur** in Hallo-toepassingsgalerie.</span><span class="sxs-lookup"><span data-stu-id="efe14-152">Otherwise, select **Add** and search for **Concur** in hello application gallery.</span></span> <span data-ttu-id="efe14-153">Selecteer Concur in zoekresultaten hello, en voeg deze tooyour lijst met toepassingen.</span><span class="sxs-lookup"><span data-stu-id="efe14-153">Select Concur from hello search results, and add it tooyour list of applications.</span></span>

8. <span data-ttu-id="efe14-154">Selecteer uw exemplaar van Concur en vervolgens Hallo **inrichten** tabblad.</span><span class="sxs-lookup"><span data-stu-id="efe14-154">Select your instance of Concur, then select hello **Provisioning** tab.</span></span>

9. <span data-ttu-id="efe14-155">Set Hallo **modus inrichting** te**automatische**.</span><span class="sxs-lookup"><span data-stu-id="efe14-155">Set hello **Provisioning Mode** too**Automatic**.</span></span> 
 
    ![Inrichting](./media/active-directory-saas-concur-provisioning-tutorial/provisioning.png)

10. <span data-ttu-id="efe14-157">Onder Hallo **beheerdersreferenties** sectie, voert u Hallo **gebruikersnaam** en Hallo **wachtwoord** van uw beheerder Concur.</span><span class="sxs-lookup"><span data-stu-id="efe14-157">Under hello **Admin Credentials** section, enter hello **user name** and hello **password** of your Concur administrator.</span></span>

11. <span data-ttu-id="efe14-158">Klik in hello Azure-portal, op **testverbinding** tooensure Azure AD tooyour Concur app kunt verbinden.</span><span class="sxs-lookup"><span data-stu-id="efe14-158">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Concur app.</span></span> <span data-ttu-id="efe14-159">Als Hallo verbinding mislukt, Controleer of uw account Concur Team beheerder machtigingen.</span><span class="sxs-lookup"><span data-stu-id="efe14-159">If hello connection fails, ensure your Concur account has Team Admin permissions.</span></span>

12. <span data-ttu-id="efe14-160">Voer e-mailadres van een persoon of groep die inrichting fout meldingen in Hallo ontvangen moet Hallo **e-mailmelding** veld en Hallo selectievakje.</span><span class="sxs-lookup"><span data-stu-id="efe14-160">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox.</span></span>

13. <span data-ttu-id="efe14-161">Klik op **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="efe14-161">Click **Save.**</span></span>

14. <span data-ttu-id="efe14-162">Selecteer onder Hallo toewijzingen sectie, **tooConcur synchroniseren Azure Active Directory-gebruikers.**</span><span class="sxs-lookup"><span data-stu-id="efe14-162">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooConcur.**</span></span>

15. <span data-ttu-id="efe14-163">In Hallo **kenmerktoewijzingen** sectie, bekijkt hello gebruikerskenmerken die worden gesynchroniseerd vanuit Azure AD-tooConcur.</span><span class="sxs-lookup"><span data-stu-id="efe14-163">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooConcur.</span></span> <span data-ttu-id="efe14-164">kenmerken die zijn geselecteerd als Hallo **overeenkomend** eigenschappen zijn gebruikte toomatch Hallo gebruikersaccounts in Concur voor update-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="efe14-164">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Concur for update operations.</span></span> <span data-ttu-id="efe14-165">Selecteer Hallo knop toocommit wijzigingen zijn opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="efe14-165">Select hello Save button toocommit any changes.</span></span>

16. <span data-ttu-id="efe14-166">tooenable Hallo inrichting Azure AD-service voor Concur, wijziging Hallo **inrichting Status** te**op** in Hallo **instellingen** sectie</span><span class="sxs-lookup"><span data-stu-id="efe14-166">tooenable hello Azure AD provisioning service for Concur, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

17. <span data-ttu-id="efe14-167">Klik op **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="efe14-167">Click **Save.**</span></span>

<span data-ttu-id="efe14-168">U kunt nu een testaccount maken.</span><span class="sxs-lookup"><span data-stu-id="efe14-168">You can now create a test account.</span></span> <span data-ttu-id="efe14-169">Wacht tot up too20 minuten tooverify die Hallo-account is gesynchroniseerd tooConcur.</span><span class="sxs-lookup"><span data-stu-id="efe14-169">Wait for up too20 minutes tooverify that hello account has been synchronized tooConcur.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="efe14-170">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="efe14-170">Additional resources</span></span>

* [<span data-ttu-id="efe14-171">Het beheren van gebruikers account inrichten voor zakelijke Apps</span><span class="sxs-lookup"><span data-stu-id="efe14-171">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="efe14-172">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="efe14-172">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="efe14-173">Eenmalige aanmelding configureren</span><span class="sxs-lookup"><span data-stu-id="efe14-173">Configure Single Sign-on</span></span>](active-directory-saas-concur-tutorial.md)

