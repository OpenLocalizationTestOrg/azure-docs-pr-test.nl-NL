---
title: 'Zelfstudie: Google Apps configureren voor het automatisch gebruikers inrichten in Azure | Microsoft Docs'
description: Meer informatie over hoe tooautomatically leveren en intrekken gebruikersaccounts vanuit Azure AD tooGoogle Apps.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6dbd50b5-589f-4132-b9eb-a53a318a64e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: d1fa8449bd6013d1627b3552aaa19db1c0f4f46f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-google-apps-for-automatic-user-provisioning"></a><span data-ttu-id="ff66d-103">Zelfstudie: Google Apps configureren voor het automatisch gebruikers inrichten</span><span class="sxs-lookup"><span data-stu-id="ff66d-103">Tutorial: Configuring Google Apps for automatic user provisioning</span></span>

<span data-ttu-id="ff66d-104">Hallo-doel van deze zelfstudie is tooshow Hallo van stappen u moet tooperform in Google Apps en Azure AD tooautomatically inrichten en ongedaan inrichten gebruikersaccounts vanuit Azure AD tooGoogle Apps.</span><span class="sxs-lookup"><span data-stu-id="ff66d-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Google Apps and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooGoogle Apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ff66d-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ff66d-105">Prerequisites</span></span>

<span data-ttu-id="ff66d-106">Hallo scenario beschreven in deze zelfstudie wordt ervan uitgegaan dat u al hebt Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="ff66d-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="ff66d-107">Een Azure Active directory-tenant.</span><span class="sxs-lookup"><span data-stu-id="ff66d-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="ff66d-108">U moet een geldige tenant voor Google Apps voor werk- of Google Apps voor onderwijs hebben.</span><span class="sxs-lookup"><span data-stu-id="ff66d-108">You must have a valid tenant for Google Apps for Work or Google Apps for Education.</span></span> <span data-ttu-id="ff66d-109">U kunt een gratis proefaccount voor de service.</span><span class="sxs-lookup"><span data-stu-id="ff66d-109">You may use a free trial account for either service.</span></span>
*   <span data-ttu-id="ff66d-110">Een gebruikersaccount in Google Apps met beheerdersmachtigingen Team.</span><span class="sxs-lookup"><span data-stu-id="ff66d-110">A user account in Google Apps with Team Admin permissions.</span></span>

## <a name="assigning-users-toogoogle-apps"></a><span data-ttu-id="ff66d-111">Toewijzen van gebruikers tooGoogle Apps</span><span class="sxs-lookup"><span data-stu-id="ff66d-111">Assigning users tooGoogle Apps</span></span>

<span data-ttu-id="ff66d-112">Azure Active Directory gebruikt een concept 'toewijzingen' toodetermine welke gebruikers toegang tooselected apps krijgen genoemd.</span><span class="sxs-lookup"><span data-stu-id="ff66d-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="ff66d-113">In de context van de Hallo van automatische gebruikers account inrichten, alleen Hallo-gebruikers en groepen die '' tooan toepassing in Azure AD toegewezen zijn gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="ff66d-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="ff66d-114">Voordat u configureren en inschakelen van Hallo-service inricht, moet u toodecide welke gebruikers en/of groepen in Azure AD Hallo-gebruikers die toegang moeten hebben tot tooyour Google Apps app vertegenwoordigen.</span><span class="sxs-lookup"><span data-stu-id="ff66d-114">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Google Apps app.</span></span> <span data-ttu-id="ff66d-115">Als u besloten, kunt u deze app-gebruikers tooyour Google Apps toewijzen door hier Hallo-instructies te volgen: [toewijzen van een gebruiker of groep tooan enterprise-app](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)</span><span class="sxs-lookup"><span data-stu-id="ff66d-115">Once decided, you can assign these users tooyour Google Apps app by following hello instructions here: [Assign a user or group tooan enterprise app](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)</span></span>

> [!IMPORTANT]
>*   <span data-ttu-id="ff66d-116">Het is raadzaam om één Azure AD-gebruiker tooGoogle Apps tootest Hallo inrichting configuratie worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="ff66d-116">It is recommended that a single Azure AD user be assigned tooGoogle Apps tootest hello provisioning configuration.</span></span> <span data-ttu-id="ff66d-117">Extra gebruikers en/of groepen kunnen later worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="ff66d-117">Additional users and/or groups may be assigned later.</span></span>
>*   <span data-ttu-id="ff66d-118">Wanneer u een gebruiker tooGoogle Apps toewijst, moet u Hallo gebruiker of rol van 'Groep' in het dialoogvenster voor Hallo-toewijzing.</span><span class="sxs-lookup"><span data-stu-id="ff66d-118">When assigning a user tooGoogle Apps, you must select hello User or "Group" role in hello assignment dialog.</span></span> <span data-ttu-id="ff66d-119">Hallo 'Default toegang' rol werkt niet voor het inrichten.</span><span class="sxs-lookup"><span data-stu-id="ff66d-119">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="ff66d-120">Geautomatiseerde gebruikersinrichting inschakelen</span><span class="sxs-lookup"><span data-stu-id="ff66d-120">Enable automated user provisioning</span></span>

<span data-ttu-id="ff66d-121">Deze sectie helpt u bij het verbinden van uw Azure AD tooGoogle-Apps gebruikersaccount inrichten API en Hallo service toocreate inrichting configureren, bijwerken en uitschakelen van toegewezen gebruikersaccounts in Google Apps op basis van gebruikers en groepen toewijzen in Azure AD .</span><span class="sxs-lookup"><span data-stu-id="ff66d-121">This section guides you through connecting your Azure AD tooGoogle Apps's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Google Apps based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="ff66d-122">U kunt ook tooenabled op basis van SAML eenmalige aanmelding voor Google Apps, in het Hallo-instructies te volgen [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ff66d-122">You may also choose tooenabled SAML-based Single Sign-On for Google Apps, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="ff66d-123">Eenmalige aanmelding kan worden geconfigureerd onafhankelijk van automatische inrichting, hoewel deze twee functies aanvulling van elkaar.</span><span class="sxs-lookup"><span data-stu-id="ff66d-123">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="configure-automatic-user-account-provisioning"></a><span data-ttu-id="ff66d-124">Automatisch gebruikers inrichten van account configureren</span><span class="sxs-lookup"><span data-stu-id="ff66d-124">Configure automatic user account provisioning</span></span>

> [!NOTE]
> <span data-ttu-id="ff66d-125">Een andere geschikte optie voor het automatiseren van gebruikers inrichten tooGoogle Apps is toouse [Google Apps Directory Sync (GADS)](https://support.google.com/a/answer/106368?hl=en) die voorziet in uw lokale Active Directory identiteiten tooGoogle Apps.</span><span class="sxs-lookup"><span data-stu-id="ff66d-125">Another viable option for automating user provisioning tooGoogle Apps is toouse [Google Apps Directory Sync (GADS)](https://support.google.com/a/answer/106368?hl=en) which provisions your on-premises Active Directory identities tooGoogle Apps.</span></span> <span data-ttu-id="ff66d-126">Daarentegen richt Hallo-oplossing in deze zelfstudie uw Azure Active Directory (cloud) gebruikers en groepen met e-mailfunctionaliteit tooGoogle Apps.</span><span class="sxs-lookup"><span data-stu-id="ff66d-126">In contrast, hello solution in this tutorial provisions your Azure Active Directory (cloud) users and mail-enabled groups tooGoogle Apps.</span></span> 

1. <span data-ttu-id="ff66d-127">Meld u aan bij Hallo [Google Apps-beheerconsole](http://admin.google.com/) met behulp van uw beheerdersaccount en klik op **beveiliging**.</span><span class="sxs-lookup"><span data-stu-id="ff66d-127">Sign into hello [Google Apps Admin Console](http://admin.google.com/) using your administrator account, and click **Security**.</span></span> <span data-ttu-id="ff66d-128">Als er geen Hallo-koppeling, kan het verborgen onder Hallo **meer besturingselementen** menu Hallo onder welkomstscherm aan.</span><span class="sxs-lookup"><span data-stu-id="ff66d-128">If you don't see hello link, it may be hidden under hello **More Controls** menu at hello bottom of hello screen.</span></span>
   
    ![Klik op 'Security' (Beveiliging).][10]

2. <span data-ttu-id="ff66d-130">Op Hallo **beveiliging** pagina, klikt u op **API Reference**.</span><span class="sxs-lookup"><span data-stu-id="ff66d-130">On hello **Security** page, click **API Reference**.</span></span>
   
    ![Klik op API-verwijzing.][15]

3. <span data-ttu-id="ff66d-132">Selecteer **inschakelen API-toegang**.</span><span class="sxs-lookup"><span data-stu-id="ff66d-132">Select **Enable API access**.</span></span>
   
    ![Klik op API-verwijzing.][16]

    > [!IMPORTANT]
    > <span data-ttu-id="ff66d-134">Voor elke gebruiker die u van plan tooprovision tooGoogle Apps, hun gebruikersnaam in Azure Active Directory bent *moet* worden gebonden tooa aangepast domein.</span><span class="sxs-lookup"><span data-stu-id="ff66d-134">For every user that you intend tooprovision tooGoogle Apps, their username in Azure Active Directory *must* be tied tooa custom domain.</span></span> <span data-ttu-id="ff66d-135">Bijvoorbeeld, de gebruikersnamen die lijken op bob@contoso.onmicrosoft.com wordt niet geaccepteerd door Google Apps, terwijl bob@contoso.com wordt geaccepteerd.</span><span class="sxs-lookup"><span data-stu-id="ff66d-135">For example, usernames that look like bob@contoso.onmicrosoft.com is not accepted by Google Apps, whereas bob@contoso.com is accepted.</span></span> <span data-ttu-id="ff66d-136">U kunt het domein van een bestaande gebruiker wijzigen door de eigenschappen bewerken in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ff66d-136">You can change an existing user's domain by editing their properties in Azure AD.</span></span> <span data-ttu-id="ff66d-137">Instructies voor hoe tooset een aangepast domein voor zowel de Azure Active Directory en de Google Apps zijn opgenomen in volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="ff66d-137">Instructions for how tooset a custom domain for both Azure Active Directory and Google Apps are included in following steps.</span></span>
      
4. <span data-ttu-id="ff66d-138">Als u een aangepast domein naam tooyour Azure Active Directory nog niet hebt toegevoegd, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ff66d-138">If you haven't added a custom domain name tooyour Azure Active Directory yet, then follow hello following steps:</span></span>
  
    <span data-ttu-id="ff66d-139">a.</span><span class="sxs-lookup"><span data-stu-id="ff66d-139">a.</span></span> <span data-ttu-id="ff66d-140">In Hallo [Azure-portal](https://portal.azure.com), op Hallo navigatiedeelvenster links, klikt u op **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ff66d-140">In hello [Azure portal](https://portal.azure.com), on hello left navigation pane, click **Active Directory**.</span></span> <span data-ttu-id="ff66d-141">In de maplijsten hello, selecteer uw directory.</span><span class="sxs-lookup"><span data-stu-id="ff66d-141">In hello directory list, select your directory.</span></span> 

    <span data-ttu-id="ff66d-142">b.</span><span class="sxs-lookup"><span data-stu-id="ff66d-142">b.</span></span> <span data-ttu-id="ff66d-143">Klik op **domeinen naam** op Hallo navigatiedeelvenster links en klik vervolgens op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="ff66d-143">Click **Domains name** on hello left navigation pane, and then click **Add**.</span></span>
     
     ![Domein](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_1.png)

     ![domein toevoegen](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_2.png)

    <span data-ttu-id="ff66d-146">c.</span><span class="sxs-lookup"><span data-stu-id="ff66d-146">c.</span></span> <span data-ttu-id="ff66d-147">Typ de naam van uw domein in Hallo **domeinnaam** veld.</span><span class="sxs-lookup"><span data-stu-id="ff66d-147">Type your domain name into hello **Domain name** field.</span></span> <span data-ttu-id="ff66d-148">Deze domeinnaam moet Hallo dezelfde domeinnaam die u van plan toouse voor Google Apps bent.</span><span class="sxs-lookup"><span data-stu-id="ff66d-148">This domain name should be hello same domain name that you intend toouse for Google Apps.</span></span> <span data-ttu-id="ff66d-149">Wanneer u klaar bent, klikt u op Hallo **domein toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="ff66d-149">When ready, click hello **Add Domain** button.</span></span>
     
     ![Domeinnaam](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_3.png)

    <span data-ttu-id="ff66d-151">d.</span><span class="sxs-lookup"><span data-stu-id="ff66d-151">d.</span></span> <span data-ttu-id="ff66d-152">Klik op **volgende** toogo toohello verificatie pagina.</span><span class="sxs-lookup"><span data-stu-id="ff66d-152">Click **Next** toogo toohello verification page.</span></span> <span data-ttu-id="ff66d-153">tooverify eigenaar van dit domein, moet u Hallo-domein-DNS-records volgens toohello-waarden die op deze pagina bewerken.</span><span class="sxs-lookup"><span data-stu-id="ff66d-153">tooverify that you own this domain, you must edit hello domain's DNS records according toohello values provided on this page.</span></span> <span data-ttu-id="ff66d-154">U kunt met behulp van tooverify **MX-records** of **TXT-records**, afhankelijk van wat u selecteren voor Hallo **recordtype** optie.</span><span class="sxs-lookup"><span data-stu-id="ff66d-154">You may choose tooverify using either **MX records** or **TXT records**, depending on what you select for hello **Record Type** option.</span></span> <span data-ttu-id="ff66d-155">Raadpleeg voor meer uitgebreide instructies over hoe tooverify domeinnaam met Azure AD, [toevoegen van uw eigen domein naam tooAzure AD](https://go.microsoft.com/fwLink/?LinkID=278919&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="ff66d-155">For more comprehensive instructions on how tooverify domain name with Azure AD, refer [Add your own domain name tooAzure AD](https://go.microsoft.com/fwLink/?LinkID=278919&clcid=0x409).</span></span>
     
     ![Domein](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_4.png)

    <span data-ttu-id="ff66d-157">e.</span><span class="sxs-lookup"><span data-stu-id="ff66d-157">e.</span></span> <span data-ttu-id="ff66d-158">Herhaal de vorige stappen voor alle Hallo domeinen die u van plan tooadd tooyour directory bent Hallo.</span><span class="sxs-lookup"><span data-stu-id="ff66d-158">Repeat hello preceding steps for all hello domains that you intend tooadd tooyour directory.</span></span>

5. <span data-ttu-id="ff66d-159">Nu dat u uw domeinen met Azure AD hebt gecontroleerd, moet u nu controleren ze opnieuw met Google Apps.</span><span class="sxs-lookup"><span data-stu-id="ff66d-159">Now that you have verified all your domains with Azure AD, you must now verify them again with Google Apps.</span></span> <span data-ttu-id="ff66d-160">Voer voor elk domein dat al is niet geregistreerd bij Google Apps, Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ff66d-160">For each domain that isn't already registered with Google Apps, perform hello following steps:</span></span>
   
    <span data-ttu-id="ff66d-161">a.</span><span class="sxs-lookup"><span data-stu-id="ff66d-161">a.</span></span> <span data-ttu-id="ff66d-162">In Hallo [Google Apps-beheerconsole](http://admin.google.com/), klikt u op **domeinen**.</span><span class="sxs-lookup"><span data-stu-id="ff66d-162">In hello [Google Apps Admin Console](http://admin.google.com/), click **Domains**.</span></span>
     
     ![Klik op domeinen][20]

    <span data-ttu-id="ff66d-164">b.</span><span class="sxs-lookup"><span data-stu-id="ff66d-164">b.</span></span> <span data-ttu-id="ff66d-165">Klik op **toevoegen van een domein of de domeinalias van een**.</span><span class="sxs-lookup"><span data-stu-id="ff66d-165">Click **Add a domain or a domain alias**.</span></span>
     
     ![Een nieuw domein toevoegen][21]

    <span data-ttu-id="ff66d-167">c.</span><span class="sxs-lookup"><span data-stu-id="ff66d-167">c.</span></span> <span data-ttu-id="ff66d-168">Selecteer **toevoegen van een ander domein**, en typt u de naam van het Hallo van Hallo-domein dat u tooadd wilt.</span><span class="sxs-lookup"><span data-stu-id="ff66d-168">Select **Add another domain**, and type in hello name of hello domain that you would like tooadd.</span></span>
     
     ![Typ de domeinnaam van uw][22]

    <span data-ttu-id="ff66d-170">d.</span><span class="sxs-lookup"><span data-stu-id="ff66d-170">d.</span></span> <span data-ttu-id="ff66d-171">Klik op **doorgaan en verifiëren dat dit domein**.</span><span class="sxs-lookup"><span data-stu-id="ff66d-171">Click **Continue and verify domain ownership**.</span></span> <span data-ttu-id="ff66d-172">Volg Hallo stappen tooverify dat u Hallo domeinnaam bezit.</span><span class="sxs-lookup"><span data-stu-id="ff66d-172">Then follow hello steps tooverify that you own hello domain name.</span></span> <span data-ttu-id="ff66d-173">Voor uitgebreide instructies over hoe tooverify uw domein met Google Apps zien.</span><span class="sxs-lookup"><span data-stu-id="ff66d-173">For comprehensive instructions on how tooverify your domain with Google Apps, see.</span></span> <span data-ttu-id="ff66d-174">[Controleer of uw site-eigendom met Google Apps](https://support.google.com/webmasters/answer/35179).</span><span class="sxs-lookup"><span data-stu-id="ff66d-174">[Verify your site ownership with Google Apps](https://support.google.com/webmasters/answer/35179).</span></span>

    <span data-ttu-id="ff66d-175">e.</span><span class="sxs-lookup"><span data-stu-id="ff66d-175">e.</span></span> <span data-ttu-id="ff66d-176">Herhaal de vorige stappen voor aanvullende domeinen die u van plan tooadd tooGoogle Apps bent Hallo.</span><span class="sxs-lookup"><span data-stu-id="ff66d-176">Repeat hello preceding steps for any additional domains that you intend tooadd tooGoogle Apps.</span></span>
     
     > [!WARNING]
     > <span data-ttu-id="ff66d-177">Als u de primaire domeincontroller Hallo voor uw tenant Google Apps wijzigen, en als u al hebt geconfigureerd eenmalige aanmelding met Azure AD, hebt u toorepeat stap #3 onder [twee stap: Schakel eenmalige aanmelding](#step-two-enable-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="ff66d-177">If you change hello primary domain for your Google Apps tenant, and if you have already configured single sign-on with Azure AD, then you have toorepeat step #3 under [Step Two: Enable Single Sign-On](#step-two-enable-single-sign-on).</span></span>
       
6. <span data-ttu-id="ff66d-178">In Hallo [Google Apps-beheerconsole](http://admin.google.com/), klikt u op **beheerdersrollen**.</span><span class="sxs-lookup"><span data-stu-id="ff66d-178">In hello [Google Apps Admin Console](http://admin.google.com/), click **Admin Roles**.</span></span>
   
     ![Klik op Google Apps][26]

7. <span data-ttu-id="ff66d-180">Bepalen welke admin account u wilt dat toouse toomanage gebruikers inrichten.</span><span class="sxs-lookup"><span data-stu-id="ff66d-180">Determine which admin account you would like toouse toomanage user provisioning.</span></span> <span data-ttu-id="ff66d-181">Voor Hallo **beheerrol** bewerken van dat account Hallo **bevoegdheden** voor die rol.</span><span class="sxs-lookup"><span data-stu-id="ff66d-181">For hello **admin role** of that account, edit hello **Privileges** for that role.</span></span> <span data-ttu-id="ff66d-182">Zorg ervoor dat deze alle Hallo **API beheerdersbevoegdheden** ingeschakeld zodat dit account kan worden gebruikt voor het inrichten.</span><span class="sxs-lookup"><span data-stu-id="ff66d-182">Make sure it has all hello **Admin API Privileges** enabled so that this account can be used for provisioning.</span></span>
   
     ![Klik op Google Apps][27]
   
    > [!NOTE]
    > <span data-ttu-id="ff66d-184">Als u een productie-omgeving configureert, is de beste Hallo toocreate een beheerdersaccount te gebruiken in Google Apps specifiek voor deze stap.</span><span class="sxs-lookup"><span data-stu-id="ff66d-184">If you are configuring a production environment, hello best practice is toocreate an admin account in Google Apps specifically for this step.</span></span> <span data-ttu-id="ff66d-185">Deze accounts moeten een beheerdersrol gekoppeld met de benodigde API-bevoegdheden Hallo hebben.</span><span class="sxs-lookup"><span data-stu-id="ff66d-185">These accounts must have an admin role associated with it that has hello necessary API privileges.</span></span>
     
8. <span data-ttu-id="ff66d-186">In Hallo [Azure-portal](https://portal.azure.com), bladeren toohello **Azure Active Directory > zakelijke Apps > alle toepassingen** sectie.</span><span class="sxs-lookup"><span data-stu-id="ff66d-186">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

9. <span data-ttu-id="ff66d-187">Als u Google Apps al hebt geconfigureerd voor eenmalige aanmelding, zoekt u uw exemplaar van Google Apps met behulp van Hallo zoekveld opgegeven.</span><span class="sxs-lookup"><span data-stu-id="ff66d-187">If you have already configured Google Apps for single sign-on, search for your instance of Google Apps using hello search field.</span></span> <span data-ttu-id="ff66d-188">Selecteer anders **toevoegen** en zoek naar **Google Apps** in Hallo-toepassingsgalerie.</span><span class="sxs-lookup"><span data-stu-id="ff66d-188">Otherwise, select **Add** and search for **Google Apps** in hello application gallery.</span></span> <span data-ttu-id="ff66d-189">Hallo zoekresultaten van Google Apps selecteren, en voeg deze tooyour lijst met toepassingen.</span><span class="sxs-lookup"><span data-stu-id="ff66d-189">Select Google Apps from hello search results, and add it tooyour list of applications.</span></span>

10. <span data-ttu-id="ff66d-190">Selecteer uw exemplaar van Google Apps en vervolgens Hallo **inrichten** tabblad.</span><span class="sxs-lookup"><span data-stu-id="ff66d-190">Select your instance of Google Apps, then select hello **Provisioning** tab.</span></span>

11. <span data-ttu-id="ff66d-191">Set Hallo **modus inrichting** te**automatische**.</span><span class="sxs-lookup"><span data-stu-id="ff66d-191">Set hello **Provisioning Mode** too**Automatic**.</span></span> 

     ![Inrichting](./media/active-directory-saas-google-apps-provisioning-tutorial/provisioning.png)

12. <span data-ttu-id="ff66d-193">Onder Hallo **beheerdersreferenties** sectie, klikt u op **autoriseren**.</span><span class="sxs-lookup"><span data-stu-id="ff66d-193">Under hello **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="ff66d-194">Een dialoogvenster met Google Apps autorisatie in een nieuw browservenster geopend.</span><span class="sxs-lookup"><span data-stu-id="ff66d-194">It opens a Google Apps authorization dialog in a new browser window.</span></span>

13. <span data-ttu-id="ff66d-195">Bevestig dat u wilt toogive Azure Active Directory toomake wijzigingen in de machtigingen die voor de tenantsleutel tooyour Google Apps.</span><span class="sxs-lookup"><span data-stu-id="ff66d-195">Confirm that you would like toogive Azure Active Directory permission toomake changes tooyour Google Apps tenant.</span></span> <span data-ttu-id="ff66d-196">Klik op **accepteren**.</span><span class="sxs-lookup"><span data-stu-id="ff66d-196">Click **Accept**.</span></span>
    
     ![Controleer de machtigingen.][28]

14. <span data-ttu-id="ff66d-198">Klik in hello Azure-portal, op **testverbinding** tooensure Azure AD tooyour Google Apps-app kunt verbinden.</span><span class="sxs-lookup"><span data-stu-id="ff66d-198">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Google Apps app.</span></span> <span data-ttu-id="ff66d-199">Als Hallo verbinding mislukt, zorg ervoor dat uw Google Apps-account Team beheerdersmachtigingen heeft en probeer het Hallo **'Autoriseren'** stap opnieuw.</span><span class="sxs-lookup"><span data-stu-id="ff66d-199">If hello connection fails, ensure your Google Apps account has Team Admin permissions and try hello **"Authorize"** step again.</span></span>

15. <span data-ttu-id="ff66d-200">Voer e-mailadres van een persoon of groep die inrichting fout meldingen in Hallo ontvangen moet Hallo **e-mailmelding** veld en Hallo selectievakje.</span><span class="sxs-lookup"><span data-stu-id="ff66d-200">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox.</span></span>

16. <span data-ttu-id="ff66d-201">Klik op **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="ff66d-201">Click **Save.**</span></span>

17. <span data-ttu-id="ff66d-202">Selecteer onder Hallo toewijzingen sectie, **tooGoogle synchroniseren Azure Active Directory-gebruikers Apps.**</span><span class="sxs-lookup"><span data-stu-id="ff66d-202">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooGoogle Apps.**</span></span>

18. <span data-ttu-id="ff66d-203">In Hallo **kenmerktoewijzingen** sectie, bekijkt hello gebruikerskenmerken die worden gesynchroniseerd vanuit Azure AD tooGoogle Apps.</span><span class="sxs-lookup"><span data-stu-id="ff66d-203">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooGoogle Apps.</span></span> <span data-ttu-id="ff66d-204">kenmerken die zijn geselecteerd als Hallo **overeenkomend** eigenschappen zijn gebruikte toomatch Hallo gebruikersaccounts in Google Apps voor update-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="ff66d-204">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Google Apps for update operations.</span></span> <span data-ttu-id="ff66d-205">Selecteer Hallo knop toocommit wijzigingen zijn opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="ff66d-205">Select hello Save button toocommit any changes.</span></span>

19. <span data-ttu-id="ff66d-206">tooenable Hallo inrichting Azure AD-service voor Google Apps, wijziging Hallo **inrichting Status** te**op** in Hallo Zoekinstellingen</span><span class="sxs-lookup"><span data-stu-id="ff66d-206">tooenable hello Azure AD provisioning service for Google Apps, change hello **Provisioning Status** too**On** in hello Settings section</span></span>

20. <span data-ttu-id="ff66d-207">Klik op **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="ff66d-207">Click **Save.**</span></span>

<span data-ttu-id="ff66d-208">Deze begint de initiële synchronisatie Hallo van alle gebruikers en/of groepen tooGoogle Apps in de sectie gebruikers en groepen Hallo toegewezen.</span><span class="sxs-lookup"><span data-stu-id="ff66d-208">It starts hello initial synchronization of any users and/or groups assigned tooGoogle Apps in hello Users and Groups section.</span></span> <span data-ttu-id="ff66d-209">de initiële synchronisatie Hallo duurt langer tooperform dan het volgende wordt gesynchroniseerd, die ongeveer 20 minuten optreden, zolang het Hallo-service wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ff66d-209">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="ff66d-210">U kunt Hallo **synchronisatiedetails** sectie toomonitor uitgevoerd en volgt u koppelingen tooprovisioning activiteitsrapporten, waarin alle bewerkingen die worden uitgevoerd door het Hallo-service op uw app in Google Apps inrichten.</span><span class="sxs-lookup"><span data-stu-id="ff66d-210">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Google Apps app.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ff66d-211">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="ff66d-211">Additional resources</span></span>

* [<span data-ttu-id="ff66d-212">Het beheren van gebruikers account inrichten voor zakelijke Apps</span><span class="sxs-lookup"><span data-stu-id="ff66d-212">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ff66d-213">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ff66d-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="ff66d-214">Eenmalige aanmelding configureren</span><span class="sxs-lookup"><span data-stu-id="ff66d-214">Configure Single Sign-on</span></span>](active-directory-saas-google-apps-tutorial.md)



<!--Image references-->

[10]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-security.png
[15]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-api.png
[16]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-api-enabled.png
[20]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-domains.png
[21]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-add-domain.png
[22]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-add-another.png
[24]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-provisioning.png
[25]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-provisioning-auth.png
[26]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-admin.png
[27]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-admin-privileges.png
[28]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-auth.png