---
title: 'Zelfstudie: Samanage configureren voor het automatisch gebruikers inrichten met Azure Active Directory | Microsoft Docs'
description: Meer informatie over hoe tooconfigure Azure Active Directory tooautomatically leveren en intrekken gebruikersaccounts tooSamanage.
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
ms.openlocfilehash: 6cb36d2cc6ce33da4f8ebba65d138bfd4f2aca9b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-samanage-for-automatic-user-provisioning"></a><span data-ttu-id="41de1-103">Zelfstudie: Samanage configureren voor het automatisch gebruikers inrichten</span><span class="sxs-lookup"><span data-stu-id="41de1-103">Tutorial: Configuring Samanage for Automatic User Provisioning</span></span>


<span data-ttu-id="41de1-104">Hallo-doel van deze zelfstudie is tooshow u stappen die u moet tooperform in Samanage en Azure AD tooautomatically leveren en intrekken gebruikersaccounts vanuit Azure AD tooSamanage Hallo.</span><span class="sxs-lookup"><span data-stu-id="41de1-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Samanage and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooSamanage.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="41de1-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="41de1-105">Prerequisites</span></span>

<span data-ttu-id="41de1-106">Hallo scenario beschreven in deze zelfstudie wordt ervan uitgegaan dat u al hebt Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="41de1-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="41de1-107">Een Azure Active directory-tenant</span><span class="sxs-lookup"><span data-stu-id="41de1-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="41de1-108">Een tenant Samanage Hello [Professional plan](https://www.samanage.com/pricing/) of beter ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="41de1-108">A Samanage tenant with hello [Professional plan](https://www.samanage.com/pricing/) or better enabled</span></span> 
*   <span data-ttu-id="41de1-109">Een gebruikersaccount in Samanage met beheerdersmachtigingen</span><span class="sxs-lookup"><span data-stu-id="41de1-109">A user account in Samanage with Admin permissions</span></span> 

> [!NOTE]
> <span data-ttu-id="41de1-110">Hello Azure AD integratie inrichting is afhankelijk van Hallo [Samanage REST-API](https://www.samanage.com/api/), namelijk beschikbaar tooSamanage teams op Hallo Professional plannen of voor een betere.</span><span class="sxs-lookup"><span data-stu-id="41de1-110">hello Azure AD provisioning integration relies on hello [Samanage REST API](https://www.samanage.com/api/), which is available tooSamanage teams on hello Professional plan or better.</span></span>

## <a name="assigning-users-toosamanage"></a><span data-ttu-id="41de1-111">Gebruikers tooSamanage toewijzen</span><span class="sxs-lookup"><span data-stu-id="41de1-111">Assigning users tooSamanage</span></span>

<span data-ttu-id="41de1-112">Azure Active Directory gebruikt een concept 'toewijzingen' toodetermine welke gebruikers toegang tooselected apps krijgen genoemd.</span><span class="sxs-lookup"><span data-stu-id="41de1-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="41de1-113">In de context van de Hallo van automatische gebruikers account inrichten, alleen Hallo-gebruikers en groepen die '' tooan toepassing in Azure AD toegewezen zijn gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="41de1-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span> 

<span data-ttu-id="41de1-114">Voordat u configureren en inschakelen van Hallo-service inricht, moet u toodecide welke gebruikers en/of groepen in Azure AD vertegenwoordigen Hallo-gebruikers die toegang moeten hebben tot tooyour Samanage app.</span><span class="sxs-lookup"><span data-stu-id="41de1-114">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Samanage app.</span></span> <span data-ttu-id="41de1-115">Als besloten, kunt u deze app-gebruikers tooyour Samanage toewijzen door hier Hallo-instructies te volgen:</span><span class="sxs-lookup"><span data-stu-id="41de1-115">Once decided, you can assign these users tooyour Samanage app by following hello instructions here:</span></span>

[<span data-ttu-id="41de1-116">Toewijzen van een gebruiker of groep tooan enterprise-app</span><span class="sxs-lookup"><span data-stu-id="41de1-116">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toosamanage"></a><span data-ttu-id="41de1-117">Belangrijke tips voor het toewijzen van gebruikers tooSamanage</span><span class="sxs-lookup"><span data-stu-id="41de1-117">Important tips for assigning users tooSamanage</span></span>

*   <span data-ttu-id="41de1-118">Het is raadzaam om één tooSamanage tootest Hallo inrichting configuratie door Azure AD-gebruiker is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="41de1-118">It is recommended that a single Azure AD user is assigned tooSamanage tootest hello provisioning configuration.</span></span> <span data-ttu-id="41de1-119">Extra gebruikers en/of groepen kunnen later worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="41de1-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="41de1-120">Wanneer u een gebruiker tooSamanage toewijst, moet u beide Hallo **gebruiker** functie of een andere geldige toepassingsspecifieke-rol (indien beschikbaar) in het dialoogvenster voor Hallo-toewijzing.</span><span class="sxs-lookup"><span data-stu-id="41de1-120">When assigning a user tooSamanage, you must select either hello **User** role, or another valid application-specific role (if available) in hello assignment dialog.</span></span> <span data-ttu-id="41de1-121">Hallo **standaardtoegang** rol werkt niet voor het inrichten en deze gebruikers worden overgeslagen.</span><span class="sxs-lookup"><span data-stu-id="41de1-121">hello **Default Access** role does not work for provisioning, and these users are skipped.</span></span>

> [!NOTE]
> <span data-ttu-id="41de1-122">Als een extra functie Hallo-service inricht eventuele aangepaste rollen gedefinieerd in Samanage leest en importeert ze in Azure AD waarin ze kunnen worden geselecteerd in het dialoogvenster voor Hallo rol selecteren.</span><span class="sxs-lookup"><span data-stu-id="41de1-122">As an added feature, hello provisioning service reads any custom roles defined in Samanage, and imports them into Azure AD where they can be selected in hello Select Role dialog.</span></span> <span data-ttu-id="41de1-123">Deze rollen zijn zichtbaar in hello Azure-portal nadat Hallo-service inricht is ingeschakeld en een synchronisatiecyclus is voltooid.</span><span class="sxs-lookup"><span data-stu-id="41de1-123">These roles will be visible in hello Azure portal after hello provisioning service is enabled and one synchronization cycle has completed.</span></span>

## <a name="configuring-user-provisioning-toosamanage"></a><span data-ttu-id="41de1-124">Gebruikers inrichten tooSamanage configureren</span><span class="sxs-lookup"><span data-stu-id="41de1-124">Configuring user provisioning tooSamanage</span></span> 

<span data-ttu-id="41de1-125">Deze sectie helpt u bij het verbinden van uw Azure AD-tooSamanage gebruikersaccount inrichten API en Hallo service toocreate inrichting configureren, bijwerken en uitschakelen toegewezen gebruikersaccounts in Samanage op basis van gebruikers en groepen toewijzen in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="41de1-125">This section guides you through connecting your Azure AD tooSamanage's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Samanage based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="41de1-126">U kunt ook tooenabled op basis van SAML eenmalige aanmelding voor Samanage, in het Hallo-instructies te volgen [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="41de1-126">You may also choose tooenabled SAML-based Single Sign-On for Samanage, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="41de1-127">Eenmalige aanmelding kan worden geconfigureerd onafhankelijk van automatische inrichting, hoewel deze twee functies aanvulling van elkaar.</span><span class="sxs-lookup"><span data-stu-id="41de1-127">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-toosamanage-in-azure-ad"></a><span data-ttu-id="41de1-128">Automatische gebruikersaccount tooSamanage ingericht in Azure AD configureren:</span><span class="sxs-lookup"><span data-stu-id="41de1-128">Configure automatic user account provisioning tooSamanage in Azure AD:</span></span>


1. <span data-ttu-id="41de1-129">In Hallo [Azure-portal](https://portal.azure.com), bladeren toohello **Azure Active Directory > zakelijke Apps > alle toepassingen** sectie.</span><span class="sxs-lookup"><span data-stu-id="41de1-129">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="41de1-130">Als u Samanage al hebt geconfigureerd voor eenmalige aanmelding, zoekt u uw exemplaar van Samanage met Hallo zoekveld opgegeven.</span><span class="sxs-lookup"><span data-stu-id="41de1-130">If you have already configured Samanage for single sign-on, search for your instance of Samanage using hello search field.</span></span> <span data-ttu-id="41de1-131">Selecteer anders **toevoegen** en zoek naar **Samanage** in Hallo-toepassingsgalerie.</span><span class="sxs-lookup"><span data-stu-id="41de1-131">Otherwise, select **Add** and search for **Samanage** in hello application gallery.</span></span> <span data-ttu-id="41de1-132">Selecteer Samanage in zoekresultaten hello, en voeg deze tooyour lijst met toepassingen.</span><span class="sxs-lookup"><span data-stu-id="41de1-132">Select Samanage from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="41de1-133">Selecteer uw exemplaar van Samanage en vervolgens Hallo **inrichten** tabblad.</span><span class="sxs-lookup"><span data-stu-id="41de1-133">Select your instance of Samanage, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="41de1-134">Set Hallo **modus inrichting** te**automatische**.</span><span class="sxs-lookup"><span data-stu-id="41de1-134">Set hello **Provisioning Mode** too**Automatic**.</span></span>

    ![Samanage inrichten](./media/active-directory-saas-samanage-provisioning-tutorial/Samanage1.png)

5. <span data-ttu-id="41de1-136">Onder Hallo **beheerdersreferenties** sectie, invoer Hallo **Admin Username & beheerderswachtwoord** van uw Samanage-account.</span><span class="sxs-lookup"><span data-stu-id="41de1-136">Under hello **Admin Credentials** section, input hello **Admin Username&Admin Password** of your Samanage's account.</span></span> 

6. <span data-ttu-id="41de1-137">Klik in hello Azure-portal, op **testverbinding** tooensure Azure AD tooyour Samanage app kunt verbinden.</span><span class="sxs-lookup"><span data-stu-id="41de1-137">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Samanage app.</span></span> <span data-ttu-id="41de1-138">Als Hallo verbinding mislukt, zorg ervoor dat uw account Samanage beheerdersmachtigingen heeft en probeer het opnieuw stap 5.</span><span class="sxs-lookup"><span data-stu-id="41de1-138">If hello connection fails, ensure your Samanage account has Admin permissions and try step 5 again.</span></span>

7. <span data-ttu-id="41de1-139">Voer e-mailadres van een persoon of groep die inrichting fout meldingen in Hallo ontvangen moet Hallo **e-mailmelding** veld en controleer Hallo selectievakje ' een e-mailmelding verzenden wanneer een fout optreedt."</span><span class="sxs-lookup"><span data-stu-id="41de1-139">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox "Send an email notification when a failure occurs."</span></span>

8. <span data-ttu-id="41de1-140">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="41de1-140">Click **Save**.</span></span> 

9. <span data-ttu-id="41de1-141">Selecteer onder Hallo toewijzingen sectie, **synchroniseren Azure Active Directory: gebruikers tooSamanage**.</span><span class="sxs-lookup"><span data-stu-id="41de1-141">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooSamanage**.</span></span>

10. <span data-ttu-id="41de1-142">In Hallo **kenmerktoewijzingen** sectie, bekijkt hello gebruikerskenmerken die worden gesynchroniseerd vanuit Azure AD-tooSamanage.</span><span class="sxs-lookup"><span data-stu-id="41de1-142">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooSamanage.</span></span> <span data-ttu-id="41de1-143">kenmerken die zijn geselecteerd als Hallo **overeenkomend** eigenschappen zijn gebruikte toomatch Hallo gebruikersaccounts in Samanage voor update-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="41de1-143">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Samanage for update operations.</span></span> <span data-ttu-id="41de1-144">Selecteer Hallo knop toocommit wijzigingen zijn opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="41de1-144">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="41de1-145">tooenable Hallo inrichting Azure AD-service voor Samanage, wijziging Hallo **inrichting Status** te**op** in Hallo **instellingen** sectie</span><span class="sxs-lookup"><span data-stu-id="41de1-145">tooenable hello Azure AD provisioning service for Samanage, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

12. <span data-ttu-id="41de1-146">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="41de1-146">Click **Save**.</span></span> 

<span data-ttu-id="41de1-147">Deze bewerking begint Hallo initiële synchronisatie van gebruikers en/of groepen die zijn toegewezen tooSamanage in Hallo gebruikers en groepen sectie.</span><span class="sxs-lookup"><span data-stu-id="41de1-147">This operation starts hello initial synchronization of any users and/or groups assigned tooSamanage in hello Users and Groups section.</span></span> <span data-ttu-id="41de1-148">de initiële synchronisatie Hallo duurt langer tooperform dan het volgende wordt gesynchroniseerd, die ongeveer 20 minuten optreden, zolang het Hallo-service wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="41de1-148">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="41de1-149">U kunt Hallo **synchronisatiedetails** sectie toomonitor uitgevoerd en volgt u koppelingen tooprovisioning activiteitsrapporten, waarin alle bewerkingen die worden uitgevoerd door het Hallo-service inricht.</span><span class="sxs-lookup"><span data-stu-id="41de1-149">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service.</span></span>

<span data-ttu-id="41de1-150">Zie voor meer informatie over hoe tooread hello Azure AD-inrichting registreert, [rapportage over automatische account gebruikersaanvragen](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="41de1-150">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="41de1-151">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="41de1-151">Additional resources</span></span>

* [<span data-ttu-id="41de1-152">Het beheren van gebruikers account inrichten voor zakelijke Apps</span><span class="sxs-lookup"><span data-stu-id="41de1-152">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="41de1-153">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="41de1-153">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="41de1-154">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="41de1-154">Next steps</span></span>

* [<span data-ttu-id="41de1-155">Informatie over hoe tooreview registreert en het ophalen van rapporten over het inrichten van activiteit</span><span class="sxs-lookup"><span data-stu-id="41de1-155">Learn how tooreview logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
