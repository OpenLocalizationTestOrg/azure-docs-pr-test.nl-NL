---
title: 'Zelfstudie: ThousandEyes configureren voor het automatisch gebruikers inrichten met Azure Active Directory | Microsoft Docs'
description: Meer informatie over hoe tooconfigure Azure Active Directory tooautomatically leveren en intrekken gebruikersaccounts tooThousandEyes.
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
ms.openlocfilehash: f31883ab685d0ffcd9a830aa4a7d43c056f5f4cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-thousandeyes-for-automatic-user-provisioning"></a><span data-ttu-id="d0e51-103">Zelfstudie: ThousandEyes configureren voor het automatisch gebruikers inrichten</span><span class="sxs-lookup"><span data-stu-id="d0e51-103">Tutorial: Configuring ThousandEyes for Automatic User Provisioning</span></span>


<span data-ttu-id="d0e51-104">Hallo-doel van deze zelfstudie is tooshow Hallo van stappen u moet tooperform in ThousandEyes en Azure AD tooautomatically inrichten en ongedaan inrichten gebruikersaccounts vanuit Azure AD-tooThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="d0e51-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in ThousandEyes and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooThousandEyes.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="d0e51-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="d0e51-105">Prerequisites</span></span>

<span data-ttu-id="d0e51-106">Hallo scenario beschreven in deze zelfstudie wordt ervan uitgegaan dat u al hebt Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="d0e51-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="d0e51-107">Een Azure Active directory-tenant</span><span class="sxs-lookup"><span data-stu-id="d0e51-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="d0e51-108">Een tenant ThousandEyes Hello [standaardplan](https://www.thousandeyes.com/pricing) of beter ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="d0e51-108">A ThousandEyes tenant with hello [Standard plan](https://www.thousandeyes.com/pricing) or better enabled</span></span> 
*   <span data-ttu-id="d0e51-109">Een gebruikersaccount in ThousandEyes met beheerdersmachtigingen</span><span class="sxs-lookup"><span data-stu-id="d0e51-109">A user account in ThousandEyes with Admin permissions</span></span> 

> [!NOTE]
> <span data-ttu-id="d0e51-110">Hello Azure AD integratie inrichting is afhankelijk van Hallo [ThousandEyes SCIM API](https://success.thousandeyes.com/PublicArticlePage?articleIdParam=kA044000000CnWrCAK), die beschikbaar tooThousandEyes teams op Hallo standaard-plan of hoger is.</span><span class="sxs-lookup"><span data-stu-id="d0e51-110">hello Azure AD provisioning integration relies on hello [ThousandEyes SCIM API](https://success.thousandeyes.com/PublicArticlePage?articleIdParam=kA044000000CnWrCAK), which is available tooThousandEyes teams on hello Standard plan or better.</span></span>

## <a name="assigning-users-toothousandeyes"></a><span data-ttu-id="d0e51-111">Gebruikers tooThousandEyes toewijzen</span><span class="sxs-lookup"><span data-stu-id="d0e51-111">Assigning users tooThousandEyes</span></span>

<span data-ttu-id="d0e51-112">Azure Active Directory gebruikt een concept 'toewijzingen' toodetermine welke gebruikers toegang tooselected apps krijgen genoemd.</span><span class="sxs-lookup"><span data-stu-id="d0e51-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="d0e51-113">In de context van de Hallo van automatische gebruikers account inrichten, alleen Hallo-gebruikers en groepen die '' tooan toepassing in Azure AD toegewezen zijn gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="d0e51-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span> 

<span data-ttu-id="d0e51-114">Voordat u configureren en inschakelen van Hallo-service inricht, moet u toodecide welke gebruikers en/of groepen in Azure AD vertegenwoordigen Hallo-gebruikers die toegang moeten hebben tot tooyour ThousandEyes app.</span><span class="sxs-lookup"><span data-stu-id="d0e51-114">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour ThousandEyes app.</span></span> <span data-ttu-id="d0e51-115">Als besloten, kunt u deze app-gebruikers tooyour ThousandEyes toewijzen door hier Hallo-instructies te volgen:</span><span class="sxs-lookup"><span data-stu-id="d0e51-115">Once decided, you can assign these users tooyour ThousandEyes app by following hello instructions here:</span></span>

[<span data-ttu-id="d0e51-116">Toewijzen van een gebruiker of groep tooan enterprise-app</span><span class="sxs-lookup"><span data-stu-id="d0e51-116">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toothousandeyes"></a><span data-ttu-id="d0e51-117">Belangrijke tips voor het toewijzen van gebruikers tooThousandEyes</span><span class="sxs-lookup"><span data-stu-id="d0e51-117">Important tips for assigning users tooThousandEyes</span></span>

*   <span data-ttu-id="d0e51-118">Het is raadzaam om één tooThousandEyes tootest Hallo inrichting configuratie door Azure AD-gebruiker is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="d0e51-118">It is recommended that a single Azure AD user is assigned tooThousandEyes tootest hello provisioning configuration.</span></span> <span data-ttu-id="d0e51-119">Extra gebruikers en/of groepen kunnen later worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="d0e51-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="d0e51-120">Wanneer u een gebruiker tooThousandEyes toewijst, moet u beide Hallo **gebruiker** functie of een andere geldige toepassingsspecifieke-rol (indien beschikbaar) in het dialoogvenster voor Hallo-toewijzing.</span><span class="sxs-lookup"><span data-stu-id="d0e51-120">When assigning a user tooThousandEyes, you must select either hello **User** role, or another valid application-specific role (if available) in hello assignment dialog.</span></span> <span data-ttu-id="d0e51-121">Hallo **standaardtoegang** rol werkt niet voor het inrichten en deze gebruikers worden overgeslagen.</span><span class="sxs-lookup"><span data-stu-id="d0e51-121">hello **Default Access** role does not work for provisioning, and these users are skipped.</span></span>


## <a name="configuring-user-provisioning-toothousandeyes"></a><span data-ttu-id="d0e51-122">Gebruikers inrichten tooThousandEyes configureren</span><span class="sxs-lookup"><span data-stu-id="d0e51-122">Configuring user provisioning tooThousandEyes</span></span> 

<span data-ttu-id="d0e51-123">In deze sectie helpt u bij het verbinden van uw Azure AD-tooThousandEyes gebruikersaccount inrichten API en Hallo service toocreate inrichting configureren, bijwerken en toegewezen gebruikersaccounts in op basis van gebruiker en groep-toewijzing in ThousandEyes uitschakelen Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d0e51-123">This section guides you through connecting your Azure AD tooThousandEyes's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in ThousandEyes based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="d0e51-124">U kunt ook tooenabled op basis van SAML eenmalige aanmelding voor ThousandEyes, in het Hallo-instructies te volgen [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d0e51-124">You may also choose tooenabled SAML-based Single Sign-On for ThousandEyes, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="d0e51-125">Eenmalige aanmelding kan worden geconfigureerd onafhankelijk van automatische inrichting, hoewel deze twee functies aanvulling van elkaar.</span><span class="sxs-lookup"><span data-stu-id="d0e51-125">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-toothousandeyes-in-azure-ad"></a><span data-ttu-id="d0e51-126">Automatische gebruikersaccount tooThousandEyes ingericht in Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="d0e51-126">Configure automatic user account provisioning tooThousandEyes in Azure AD</span></span>


1. <span data-ttu-id="d0e51-127">In Hallo [Azure-portal](https://portal.azure.com), bladeren toohello **Azure Active Directory > zakelijke Apps > alle toepassingen** sectie.</span><span class="sxs-lookup"><span data-stu-id="d0e51-127">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="d0e51-128">Als u ThousandEyes al hebt geconfigureerd voor eenmalige aanmelding, zoekt u uw exemplaar van ThousandEyes met Hallo zoekveld opgegeven.</span><span class="sxs-lookup"><span data-stu-id="d0e51-128">If you have already configured ThousandEyes for single sign-on, search for your instance of ThousandEyes using hello search field.</span></span> <span data-ttu-id="d0e51-129">Selecteer anders **toevoegen** en zoek naar **ThousandEyes** in Hallo-toepassingsgalerie.</span><span class="sxs-lookup"><span data-stu-id="d0e51-129">Otherwise, select **Add** and search for **ThousandEyes** in hello application gallery.</span></span> <span data-ttu-id="d0e51-130">Selecteer ThousandEyes in zoekresultaten hello, en voeg deze tooyour lijst met toepassingen.</span><span class="sxs-lookup"><span data-stu-id="d0e51-130">Select ThousandEyes from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="d0e51-131">Selecteer uw exemplaar van ThousandEyes en vervolgens Hallo **inrichten** tabblad.</span><span class="sxs-lookup"><span data-stu-id="d0e51-131">Select your instance of ThousandEyes, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="d0e51-132">Set Hallo **modus inrichting** te**automatische**.</span><span class="sxs-lookup"><span data-stu-id="d0e51-132">Set hello **Provisioning Mode** too**Automatic**.</span></span>

    ![ThousandEyes inrichten](./media/active-directory-saas-thousandeyes-provisioning-tutorial/ThousandEyes1.png)

5. <span data-ttu-id="d0e51-134">Onder Hallo **beheerdersreferenties** sectie, invoer Hallo **geheim Token** die worden gegenereerd door uw ThousandEyes account (Hallo token vindt u onder uw account ThousandEyes: **beveiliging & Verificatie**).</span><span class="sxs-lookup"><span data-stu-id="d0e51-134">Under hello **Admin Credentials** section, input hello **Secret Token** generated by your ThousandEyes's account (you can find hello token under your ThousandEyes account: **Security & Authentication**).</span></span> 

    ![ThousandEyes inrichten](./media/active-directory-saas-thousandeyes-provisioning-tutorial/ThousandEyes2.png)

6. <span data-ttu-id="d0e51-136">Klik in hello Azure-portal, op **testverbinding** tooensure Azure AD tooyour ThousandEyes app kunt verbinden.</span><span class="sxs-lookup"><span data-stu-id="d0e51-136">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour ThousandEyes app.</span></span> <span data-ttu-id="d0e51-137">Als Hallo verbinding mislukt, zorg ervoor dat uw account ThousandEyes beheerdersmachtigingen heeft en probeer het opnieuw stap 5.</span><span class="sxs-lookup"><span data-stu-id="d0e51-137">If hello connection fails, ensure your ThousandEyes account has Admin permissions and try step 5 again.</span></span>

7. <span data-ttu-id="d0e51-138">Voer e-mailadres van een persoon of groep die inrichting fout meldingen in Hallo ontvangen moet Hallo **e-mailmelding** veld en controleer Hallo selectievakje ' een e-mailmelding verzenden wanneer een fout optreedt."</span><span class="sxs-lookup"><span data-stu-id="d0e51-138">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox "Send an email notification when a failure occurs."</span></span>

8. <span data-ttu-id="d0e51-139">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="d0e51-139">Click **Save**.</span></span> 

9. <span data-ttu-id="d0e51-140">Selecteer onder Hallo toewijzingen sectie, **synchroniseren Azure Active Directory: gebruikers tooThousandEyes**.</span><span class="sxs-lookup"><span data-stu-id="d0e51-140">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooThousandEyes**.</span></span>

10. <span data-ttu-id="d0e51-141">In Hallo **kenmerktoewijzingen** sectie, bekijkt hello gebruikerskenmerken die worden gesynchroniseerd vanuit Azure AD-tooThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="d0e51-141">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooThousandEyes.</span></span> <span data-ttu-id="d0e51-142">kenmerken die zijn geselecteerd als Hallo **overeenkomend** eigenschappen zijn gebruikte toomatch Hallo gebruikersaccounts in ThousandEyes voor update-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="d0e51-142">hello attributes selected as **Matching** properties are used toomatch hello user accounts in ThousandEyes for update operations.</span></span> <span data-ttu-id="d0e51-143">Selecteer Hallo knop toocommit wijzigingen zijn opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="d0e51-143">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="d0e51-144">tooenable Hallo inrichting Azure AD-service voor ThousandEyes, wijziging Hallo **inrichting Status** te**op** in Hallo **instellingen** sectie</span><span class="sxs-lookup"><span data-stu-id="d0e51-144">tooenable hello Azure AD provisioning service for ThousandEyes, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

12. <span data-ttu-id="d0e51-145">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="d0e51-145">Click **Save**.</span></span> 

<span data-ttu-id="d0e51-146">Deze bewerking begint Hallo initiële synchronisatie van gebruikers en/of groepen die zijn toegewezen tooThousandEyes in Hallo gebruikers en groepen sectie.</span><span class="sxs-lookup"><span data-stu-id="d0e51-146">This operation starts hello initial synchronization of any users and/or groups assigned tooThousandEyes in hello Users and Groups section.</span></span> <span data-ttu-id="d0e51-147">de initiële synchronisatie Hallo duurt langer tooperform dan het volgende wordt gesynchroniseerd, die ongeveer 20 minuten optreden, zolang het Hallo-service wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d0e51-147">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="d0e51-148">U kunt Hallo **synchronisatiedetails** sectie toomonitor uitgevoerd en volgt u koppelingen tooprovisioning activiteitsrapporten, waarin alle bewerkingen die worden uitgevoerd door het Hallo-service inricht.</span><span class="sxs-lookup"><span data-stu-id="d0e51-148">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service.</span></span>

<span data-ttu-id="d0e51-149">Zie voor meer informatie over hoe tooread hello Azure AD-inrichting registreert, [rapportage over automatische account gebruikersaanvragen](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="d0e51-149">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="d0e51-150">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="d0e51-150">Additional resources</span></span>

* [<span data-ttu-id="d0e51-151">Het beheren van gebruikers account inrichten voor zakelijke Apps</span><span class="sxs-lookup"><span data-stu-id="d0e51-151">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="d0e51-152">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d0e51-152">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="d0e51-153">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d0e51-153">Next steps</span></span>

* [<span data-ttu-id="d0e51-154">Informatie over hoe tooreview registreert en het ophalen van rapporten over het inrichten van activiteit</span><span class="sxs-lookup"><span data-stu-id="d0e51-154">Learn how tooreview logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
