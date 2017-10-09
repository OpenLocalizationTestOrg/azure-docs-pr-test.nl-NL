---
title: 'Zelfstudie: LucidChart configureren voor het automatisch gebruikers inrichten met Azure Active Directory | Microsoft Docs'
description: Meer informatie over hoe tooconfigure Azure Active Directory tooautomatically leveren en intrekken gebruikersaccounts tooLucidChart.
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
ms.openlocfilehash: d3af45141731215f2edc8942ad21b016468c1e38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-lucidchart-for-automatic-user-provisioning"></a><span data-ttu-id="c9902-103">Zelfstudie: LucidChart configureren voor het automatisch gebruikers inrichten</span><span class="sxs-lookup"><span data-stu-id="c9902-103">Tutorial: Configuring LucidChart for Automatic User Provisioning</span></span>


<span data-ttu-id="c9902-104">Hallo-doel van deze zelfstudie is tooshow u stappen die u moet tooperform in LucidChart en Azure AD tooautomatically leveren en intrekken gebruikersaccounts vanuit Azure AD tooLucidChart Hallo.</span><span class="sxs-lookup"><span data-stu-id="c9902-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in LucidChart and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooLucidChart.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="c9902-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="c9902-105">Prerequisites</span></span>

<span data-ttu-id="c9902-106">Hallo scenario beschreven in deze zelfstudie wordt ervan uitgegaan dat u al hebt Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="c9902-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="c9902-107">Een Azure Active directory-tenant</span><span class="sxs-lookup"><span data-stu-id="c9902-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="c9902-108">Een tenant LucidChart Hello [enterpriseplan](https://www.lucidchart.com/user/117598685#/subscriptionLevel) of beter ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="c9902-108">A LucidChart tenant with hello [Enterprise plan](https://www.lucidchart.com/user/117598685#/subscriptionLevel) or better enabled</span></span> 
*   <span data-ttu-id="c9902-109">Een gebruikersaccount in LucidChart met beheerdersmachtigingen</span><span class="sxs-lookup"><span data-stu-id="c9902-109">A user account in LucidChart with Admin permissions</span></span> 

## <a name="assigning-users-toolucidchart"></a><span data-ttu-id="c9902-110">Gebruikers tooLucidChart toewijzen</span><span class="sxs-lookup"><span data-stu-id="c9902-110">Assigning users tooLucidChart</span></span>

<span data-ttu-id="c9902-111">Azure Active Directory gebruikt een concept 'toewijzingen' toodetermine welke gebruikers toegang tooselected apps krijgen genoemd.</span><span class="sxs-lookup"><span data-stu-id="c9902-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="c9902-112">In de context van de Hallo van automatische gebruikers account inrichten, alleen Hallo-gebruikers en groepen die '' tooan toepassing in Azure AD toegewezen zijn gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="c9902-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span> 

<span data-ttu-id="c9902-113">Voordat u configureren en inschakelen van Hallo-service inricht, moet u toodecide welke gebruikers en/of groepen in Azure AD vertegenwoordigen Hallo-gebruikers die toegang moeten hebben tot tooyour LucidChart app.</span><span class="sxs-lookup"><span data-stu-id="c9902-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour LucidChart app.</span></span> <span data-ttu-id="c9902-114">Als besloten, kunt u deze app-gebruikers tooyour LucidChart toewijzen door hier Hallo-instructies te volgen:</span><span class="sxs-lookup"><span data-stu-id="c9902-114">Once decided, you can assign these users tooyour LucidChart app by following hello instructions here:</span></span>

[<span data-ttu-id="c9902-115">Toewijzen van een gebruiker of groep tooan enterprise-app</span><span class="sxs-lookup"><span data-stu-id="c9902-115">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toolucidchart"></a><span data-ttu-id="c9902-116">Belangrijke tips voor het toewijzen van gebruikers tooLucidChart</span><span class="sxs-lookup"><span data-stu-id="c9902-116">Important tips for assigning users tooLucidChart</span></span>

*   <span data-ttu-id="c9902-117">Het is raadzaam om één tooLucidChart tootest Hallo inrichting configuratie door Azure AD-gebruiker is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="c9902-117">It is recommended that a single Azure AD user is assigned tooLucidChart tootest hello provisioning configuration.</span></span> <span data-ttu-id="c9902-118">Extra gebruikers en/of groepen kunnen later worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="c9902-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="c9902-119">Wanneer u een gebruiker tooLucidChart toewijst, moet u beide Hallo **gebruiker** functie of een andere geldige toepassingsspecifieke-rol (indien beschikbaar) in het dialoogvenster voor Hallo-toewijzing.</span><span class="sxs-lookup"><span data-stu-id="c9902-119">When assigning a user tooLucidChart, you must select either hello **User** role, or another valid application-specific role (if available) in hello assignment dialog.</span></span> <span data-ttu-id="c9902-120">Hallo **standaardtoegang** rol werkt niet voor het inrichten en deze gebruikers worden overgeslagen.</span><span class="sxs-lookup"><span data-stu-id="c9902-120">hello **Default Access** role does not work for provisioning, and these users are skipped.</span></span>


## <a name="configuring-user-provisioning-toolucidchart"></a><span data-ttu-id="c9902-121">Gebruikers inrichten tooLucidChart configureren</span><span class="sxs-lookup"><span data-stu-id="c9902-121">Configuring user provisioning tooLucidChart</span></span> 

<span data-ttu-id="c9902-122">Deze sectie helpt u bij het verbinden van uw Azure AD-tooLucidChart gebruikersaccount inrichten API en Hallo service toocreate inrichting configureren, bijwerken en uitschakelen van toegewezen gebruikersaccounts in LucidChart op basis van gebruikers en groepen toewijzen in Azure AD .</span><span class="sxs-lookup"><span data-stu-id="c9902-122">This section guides you through connecting your Azure AD tooLucidChart's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in LucidChart based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="c9902-123">U kunt ook tooenabled op basis van SAML eenmalige aanmelding voor LucidChart, in het Hallo-instructies te volgen [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c9902-123">You may also choose tooenabled SAML-based Single Sign-On for LucidChart, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="c9902-124">Eenmalige aanmelding kan worden geconfigureerd onafhankelijk van automatische inrichting, hoewel deze twee functies aanvulling van elkaar.</span><span class="sxs-lookup"><span data-stu-id="c9902-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-toolucidchart-in-azure-ad"></a><span data-ttu-id="c9902-125">Automatische gebruikersaccount tooLucidChart ingericht in Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="c9902-125">Configure automatic user account provisioning tooLucidChart in Azure AD</span></span>


1. <span data-ttu-id="c9902-126">In Hallo [Azure-portal](https://portal.azure.com), bladeren toohello **Azure Active Directory > zakelijke Apps > alle toepassingen** sectie.</span><span class="sxs-lookup"><span data-stu-id="c9902-126">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="c9902-127">Als u LucidChart al hebt geconfigureerd voor eenmalige aanmelding, zoekt u uw exemplaar van LucidChart met Hallo zoekveld opgegeven.</span><span class="sxs-lookup"><span data-stu-id="c9902-127">If you have already configured LucidChart for single sign-on, search for your instance of LucidChart using hello search field.</span></span> <span data-ttu-id="c9902-128">Selecteer anders **toevoegen** en zoek naar **LucidChart** in Hallo-toepassingsgalerie.</span><span class="sxs-lookup"><span data-stu-id="c9902-128">Otherwise, select **Add** and search for **LucidChart** in hello application gallery.</span></span> <span data-ttu-id="c9902-129">Selecteer LucidChart in zoekresultaten hello, en voeg deze tooyour lijst met toepassingen.</span><span class="sxs-lookup"><span data-stu-id="c9902-129">Select LucidChart from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="c9902-130">Selecteer uw exemplaar van LucidChart en vervolgens Hallo **inrichten** tabblad.</span><span class="sxs-lookup"><span data-stu-id="c9902-130">Select your instance of LucidChart, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="c9902-131">Set Hallo **modus inrichting** te**automatische**.</span><span class="sxs-lookup"><span data-stu-id="c9902-131">Set hello **Provisioning Mode** too**Automatic**.</span></span>

    ![LucidChart inrichten](./media/active-directory-saas-lucidchart-provisioning-tutorial/LucidChart1.png)

5. <span data-ttu-id="c9902-133">Onder Hallo **beheerdersreferenties** sectie, invoer Hallo **geheim Token** die worden gegenereerd door uw LucidChart account (Hallo token vindt u onder uw account: **Team**  >  **App-integratie** > **SCIM**).</span><span class="sxs-lookup"><span data-stu-id="c9902-133">Under hello **Admin Credentials** section, input hello **Secret Token** generated by your LucidChart's account (you can find hello token under your account: **Team** > **App Integration** > **SCIM**).</span></span> 

    ![LucidChart inrichten](./media/active-directory-saas-lucidchart-provisioning-tutorial/LucidChart2.png)

6. <span data-ttu-id="c9902-135">Klik in hello Azure-portal, op **testverbinding** tooensure Azure AD tooyour LucidChart app kunt verbinden.</span><span class="sxs-lookup"><span data-stu-id="c9902-135">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour LucidChart app.</span></span> <span data-ttu-id="c9902-136">Als Hallo verbinding mislukt, zorg ervoor dat uw account LucidChart beheerdersmachtigingen heeft en probeer het opnieuw stap 5.</span><span class="sxs-lookup"><span data-stu-id="c9902-136">If hello connection fails, ensure your LucidChart account has Admin permissions and try step 5 again.</span></span>

7. <span data-ttu-id="c9902-137">Voer e-mailadres van een persoon of groep die inrichting fout meldingen in Hallo ontvangen moet Hallo **e-mailmelding** veld en controleer Hallo selectievakje ' een e-mailmelding verzenden wanneer een fout optreedt."</span><span class="sxs-lookup"><span data-stu-id="c9902-137">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox "Send an email notification when a failure occurs."</span></span>

8. <span data-ttu-id="c9902-138">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="c9902-138">Click **Save**.</span></span> 

9. <span data-ttu-id="c9902-139">Selecteer onder Hallo toewijzingen sectie, **synchroniseren Azure Active Directory: gebruikers tooLucidChart**.</span><span class="sxs-lookup"><span data-stu-id="c9902-139">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooLucidChart**.</span></span>

10. <span data-ttu-id="c9902-140">In Hallo **kenmerktoewijzingen** sectie, bekijkt hello gebruikerskenmerken die worden gesynchroniseerd vanuit Azure AD-tooLucidChart.</span><span class="sxs-lookup"><span data-stu-id="c9902-140">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooLucidChart.</span></span> <span data-ttu-id="c9902-141">kenmerken die zijn geselecteerd als Hallo **overeenkomend** eigenschappen zijn gebruikte toomatch Hallo gebruikersaccounts in LucidChart voor update-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="c9902-141">hello attributes selected as **Matching** properties are used toomatch hello user accounts in LucidChart for update operations.</span></span> <span data-ttu-id="c9902-142">Selecteer Hallo knop toocommit wijzigingen zijn opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="c9902-142">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="c9902-143">tooenable Hallo inrichting Azure AD-service voor LucidChart, wijziging Hallo **inrichting Status** te**op** in Hallo **instellingen** sectie</span><span class="sxs-lookup"><span data-stu-id="c9902-143">tooenable hello Azure AD provisioning service for LucidChart, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

12. <span data-ttu-id="c9902-144">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="c9902-144">Click **Save**.</span></span> 

<span data-ttu-id="c9902-145">Deze bewerking begint Hallo initiële synchronisatie van gebruikers en/of groepen die zijn toegewezen tooLucidChart in Hallo gebruikers en groepen sectie.</span><span class="sxs-lookup"><span data-stu-id="c9902-145">This operation starts hello initial synchronization of any users and/or groups assigned tooLucidChart in hello Users and Groups section.</span></span> <span data-ttu-id="c9902-146">de initiële synchronisatie Hallo duurt langer tooperform dan het volgende wordt gesynchroniseerd, die ongeveer 20 minuten optreden, zolang het Hallo-service wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c9902-146">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="c9902-147">U kunt Hallo **synchronisatiedetails** sectie toomonitor uitgevoerd en volgt u koppelingen tooprovisioning activiteitsrapporten, waarin alle bewerkingen die worden uitgevoerd door het Hallo-service inricht.</span><span class="sxs-lookup"><span data-stu-id="c9902-147">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service.</span></span>

<span data-ttu-id="c9902-148">Zie voor meer informatie over hoe tooread hello Azure AD-inrichting registreert, [rapportage over automatische account gebruikersaanvragen](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="c9902-148">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="c9902-149">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="c9902-149">Additional resources</span></span>

* [<span data-ttu-id="c9902-150">Het beheren van gebruikers account inrichten voor zakelijke Apps</span><span class="sxs-lookup"><span data-stu-id="c9902-150">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="c9902-151">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c9902-151">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="c9902-152">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c9902-152">Next steps</span></span>

* [<span data-ttu-id="c9902-153">Informatie over hoe tooreview registreert en het ophalen van rapporten over het inrichten van activiteit</span><span class="sxs-lookup"><span data-stu-id="c9902-153">Learn how tooreview logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
