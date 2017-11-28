---
title: 'Zelfstudie: ZenDesk configureren voor het automatisch gebruikers inrichten met Azure Active Directory | Microsoft Docs'
description: Meer informatie over hoe tooconfigure Azure Active Directory tooautomatically leveren en intrekken gebruikersaccounts tooZenDesk.
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
ms.openlocfilehash: 200e8790ec1755f5cf927274ceb38527dd993f3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-zendesk-for-automatic-user-provisioning"></a><span data-ttu-id="78abb-103">Zelfstudie: ZenDesk configureren voor het automatisch gebruikers inrichten</span><span class="sxs-lookup"><span data-stu-id="78abb-103">Tutorial: Configuring ZenDesk for Automatic User Provisioning</span></span>


<span data-ttu-id="78abb-104">Hallo-doel van deze zelfstudie is tooshow u stappen die u moet tooperform in de ZenDesk- en Azure AD tooautomatically leveren en intrekken gebruikersaccounts vanuit Azure AD tooZenDesk Hallo.</span><span class="sxs-lookup"><span data-stu-id="78abb-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in ZenDesk and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooZenDesk.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="78abb-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="78abb-105">Prerequisites</span></span>

<span data-ttu-id="78abb-106">Hallo scenario beschreven in deze zelfstudie wordt ervan uitgegaan dat u al hebt Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="78abb-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="78abb-107">Een Azure Active directory-tenant</span><span class="sxs-lookup"><span data-stu-id="78abb-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="78abb-108">Een tenant ZenDesk Hello [enterpriseplan](https://www.zendesk.com/product/pricing/) of beter ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="78abb-108">A ZenDesk tenant with hello [Enterprise plan](https://www.zendesk.com/product/pricing/) or better enabled</span></span> 
*   <span data-ttu-id="78abb-109">Een gebruikersaccount in de ZenDesk met beheerdersmachtigingen</span><span class="sxs-lookup"><span data-stu-id="78abb-109">A user account in ZenDesk with Admin permissions</span></span> 

> [!NOTE]
> <span data-ttu-id="78abb-110">Hello Azure AD integratie inrichting is afhankelijk van Hallo [ZenDesk REST-API](https://developer.zendesk.com/rest_api/docs/core/introduction#the-api), die beschikbaar tooZenDesk teams op Hallo essentiële plan of hoger is.</span><span class="sxs-lookup"><span data-stu-id="78abb-110">hello Azure AD provisioning integration relies on hello [ZenDesk REST API](https://developer.zendesk.com/rest_api/docs/core/introduction#the-api), which is available tooZenDesk teams on hello Essential plan or better.</span></span>

## <a name="assigning-users-toozendesk"></a><span data-ttu-id="78abb-111">Gebruikers tooZenDesk toewijzen</span><span class="sxs-lookup"><span data-stu-id="78abb-111">Assigning users tooZenDesk</span></span>

<span data-ttu-id="78abb-112">Azure Active Directory gebruikt een concept 'toewijzingen' toodetermine welke gebruikers toegang tooselected apps krijgen genoemd.</span><span class="sxs-lookup"><span data-stu-id="78abb-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="78abb-113">In de context van de Hallo van automatische gebruikers account inrichten, worden alleen Hallo-gebruikers en groepen die '' tooan toepassing in Azure AD toegewezen zijn gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="78abb-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD are synchronized.</span></span> 

<span data-ttu-id="78abb-114">Voordat u configureren en inschakelen van Hallo-service inricht, moet u toodecide welke gebruikers en/of groepen in Azure AD vertegenwoordigen Hallo-gebruikers die toegang moeten hebben tot tooyour ZenDesk-app.</span><span class="sxs-lookup"><span data-stu-id="78abb-114">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour ZenDesk app.</span></span> <span data-ttu-id="78abb-115">Als besloten, kunt u deze gebruikers tooyour ZenDesk-app kunt toewijzen door hier Hallo-instructies te volgen:</span><span class="sxs-lookup"><span data-stu-id="78abb-115">Once decided, you can assign these users tooyour ZenDesk app by following hello instructions here:</span></span>

[<span data-ttu-id="78abb-116">Toewijzen van een gebruiker of groep tooan enterprise-app</span><span class="sxs-lookup"><span data-stu-id="78abb-116">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toozendesk"></a><span data-ttu-id="78abb-117">Belangrijke tips voor het toewijzen van gebruikers tooZenDesk</span><span class="sxs-lookup"><span data-stu-id="78abb-117">Important tips for assigning users tooZenDesk</span></span>

*   <span data-ttu-id="78abb-118">Het is raadzaam om één tooZenDesk tootest Hallo inrichting configuratie door Azure AD-gebruiker is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="78abb-118">It is recommended that a single Azure AD user is assigned tooZenDesk tootest hello provisioning configuration.</span></span> <span data-ttu-id="78abb-119">Extra gebruikers en/of groepen kunnen later worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="78abb-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="78abb-120">Wanneer u een gebruiker tooZenDesk toewijst, moet u beide Hallo **gebruiker** functie of een andere geldige toepassingsspecifieke-rol (indien beschikbaar) in het dialoogvenster voor Hallo-toewijzing.</span><span class="sxs-lookup"><span data-stu-id="78abb-120">When assigning a user tooZenDesk, you must select either hello **User** role, or another valid application-specific role (if available) in hello assignment dialog.</span></span> <span data-ttu-id="78abb-121">Hallo **standaardtoegang** rol werkt niet voor het inrichten en deze gebruikers worden overgeslagen.</span><span class="sxs-lookup"><span data-stu-id="78abb-121">hello **Default Access** role does not work for provisioning, and these users are skipped.</span></span>

> [!NOTE]
> <span data-ttu-id="78abb-122">Als een extra functie Hallo-service inricht eventuele aangepaste rollen gedefinieerd in de Zendesk leest en importeert ze in Azure AD waarin ze kunnen worden geselecteerd in het dialoogvenster voor Hallo rol selecteren.</span><span class="sxs-lookup"><span data-stu-id="78abb-122">As an added feature, hello provisioning service reads any custom roles defined in Zendesk, and imports them into Azure AD where they can be selected in hello Select Role dialog.</span></span> <span data-ttu-id="78abb-123">Deze rollen zijn zichtbaar in hello Azure-portal nadat Hallo-service inricht is ingeschakeld en een synchronisatiecyclus is voltooid.</span><span class="sxs-lookup"><span data-stu-id="78abb-123">These roles will be visible in hello Azure portal after hello provisioning service is enabled and one synchronization cycle has completed.</span></span>

## <a name="configuring-user-provisioning-toozendesk"></a><span data-ttu-id="78abb-124">Gebruikers inrichten tooZenDesk configureren</span><span class="sxs-lookup"><span data-stu-id="78abb-124">Configuring user provisioning tooZenDesk</span></span> 

<span data-ttu-id="78abb-125">In deze sectie helpt u bij het verbinden van uw Azure AD-tooZenDesk gebruikersaccount inrichten API en Hallo service toocreate inrichting configureren, bijwerken en uitschakelen van toegewezen gebruikersaccounts in de ZenDesk op basis van gebruikers en groepen toewijzen in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="78abb-125">This section guides you through connecting your Azure AD tooZenDesk's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in ZenDesk based on user and group assignment in Azure AD.</span></span>

> [!TIP] 
> <span data-ttu-id="78abb-126">U kunt ook tooenabled op basis van SAML eenmalige aanmelding voor ZenDesk, in het Hallo-instructies te volgen [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="78abb-126">You may also choose tooenabled SAML-based Single Sign-On for ZenDesk, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="78abb-127">Eenmalige aanmelding kan worden geconfigureerd onafhankelijk van automatische inrichting, hoewel deze twee functies aanvulling van elkaar.</span><span class="sxs-lookup"><span data-stu-id="78abb-127">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-toozendesk-in-azure-ad"></a><span data-ttu-id="78abb-128">Automatische gebruikersaccount tooZenDesk ingericht in Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="78abb-128">Configure automatic user account provisioning tooZenDesk in Azure AD</span></span>


1. <span data-ttu-id="78abb-129">In Hallo [Azure-portal](https://portal.azure.com), bladeren toohello **Azure Active Directory > zakelijke Apps > alle toepassingen** sectie.</span><span class="sxs-lookup"><span data-stu-id="78abb-129">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="78abb-130">Als u ZenDesk al hebt geconfigureerd voor eenmalige aanmelding, zoekt u uw exemplaar van ZenDesk met Hallo zoekveld opgegeven.</span><span class="sxs-lookup"><span data-stu-id="78abb-130">If you have already configured ZenDesk for single sign-on, search for your instance of ZenDesk using hello search field.</span></span> <span data-ttu-id="78abb-131">Selecteer anders **toevoegen** en zoek naar **ZenDesk** in Hallo-toepassingsgalerie.</span><span class="sxs-lookup"><span data-stu-id="78abb-131">Otherwise, select **Add** and search for **ZenDesk** in hello application gallery.</span></span> <span data-ttu-id="78abb-132">Selecteer ZenDesk in zoekresultaten hello, en voeg deze tooyour lijst met toepassingen.</span><span class="sxs-lookup"><span data-stu-id="78abb-132">Select ZenDesk from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="78abb-133">Selecteer uw ZenDesk-exemplaar en vervolgens Hallo **inrichten** tabblad.</span><span class="sxs-lookup"><span data-stu-id="78abb-133">Select your instance of ZenDesk, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="78abb-134">Set Hallo **modus inrichting** te**automatische**.</span><span class="sxs-lookup"><span data-stu-id="78abb-134">Set hello **Provisioning Mode** too**Automatic**.</span></span>

    ![ZenDesk-inrichting](./media/active-directory-saas-zendesk-provisioning-tutorial/ZenDesk1.png)

5. <span data-ttu-id="78abb-136">Onder Hallo **beheerdersreferenties** sectie, invoer Hallo **Admin Username & tokenkey & domein** die worden gegenereerd door uw ZenDesk-account (Hallo token vindt u onder uw account: **Admin**   >  **API** > **instellingen**).</span><span class="sxs-lookup"><span data-stu-id="78abb-136">Under hello **Admin Credentials** section, input hello **Admin Username&tokenkey&Domain** generated by your ZenDesk's account (you can find hello token under your account: **Admin** > **API** > **Settings**).</span></span> 

    ![ZenDesk-inrichting](./media/active-directory-saas-zendesk-provisioning-tutorial/ZenDesk2.png)

6. <span data-ttu-id="78abb-138">Klik in hello Azure-portal, op **testverbinding** tooensure Azure AD tooyour ZenDesk-app kunt verbinden.</span><span class="sxs-lookup"><span data-stu-id="78abb-138">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour ZenDesk app.</span></span> <span data-ttu-id="78abb-139">Als Hallo verbinding mislukt, zorg ervoor dat uw ZenDesk-account beheerdersmachtigingen heeft en probeer het opnieuw stap 5.</span><span class="sxs-lookup"><span data-stu-id="78abb-139">If hello connection fails, ensure your ZenDesk account has Admin permissions and try step 5 again.</span></span>

7. <span data-ttu-id="78abb-140">Voer e-mailadres van een persoon of groep die inrichting fout meldingen in Hallo ontvangen moet Hallo **e-mailmelding** veld en controleer Hallo selectievakje ' een e-mailmelding verzenden wanneer een fout optreedt."</span><span class="sxs-lookup"><span data-stu-id="78abb-140">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox "Send an email notification when a failure occurs."</span></span>

8. <span data-ttu-id="78abb-141">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="78abb-141">Click **Save**.</span></span> 

9. <span data-ttu-id="78abb-142">Selecteer onder Hallo toewijzingen sectie, **synchroniseren Azure Active Directory: gebruikers tooZenDesk**.</span><span class="sxs-lookup"><span data-stu-id="78abb-142">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooZenDesk**.</span></span>

10. <span data-ttu-id="78abb-143">In Hallo **kenmerktoewijzingen** sectie, bekijkt hello gebruikerskenmerken die worden gesynchroniseerd vanuit Azure AD-tooZenDesk.</span><span class="sxs-lookup"><span data-stu-id="78abb-143">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooZenDesk.</span></span> <span data-ttu-id="78abb-144">kenmerken die zijn geselecteerd als Hallo **overeenkomend** eigenschappen zijn gebruikte toomatch Hallo gebruikersaccounts in de ZenDesk voor update-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="78abb-144">hello attributes selected as **Matching** properties are used toomatch hello user accounts in ZenDesk for update operations.</span></span> <span data-ttu-id="78abb-145">Selecteer Hallo knop toocommit wijzigingen zijn opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="78abb-145">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="78abb-146">tooenable Hallo inrichting Azure AD-service voor ZenDesk, wijziging Hallo **inrichting Status** te**op** in Hallo **instellingen** sectie</span><span class="sxs-lookup"><span data-stu-id="78abb-146">tooenable hello Azure AD provisioning service for ZenDesk, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

12. <span data-ttu-id="78abb-147">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="78abb-147">Click **Save**.</span></span> 

<span data-ttu-id="78abb-148">Deze bewerking begint Hallo initiële synchronisatie van gebruikers en/of groepen die zijn toegewezen tooZenDesk in Hallo gebruikers en groepen sectie.</span><span class="sxs-lookup"><span data-stu-id="78abb-148">This operation starts hello initial synchronization of any users and/or groups assigned tooZenDesk in hello Users and Groups section.</span></span> <span data-ttu-id="78abb-149">de initiële synchronisatie Hallo duurt langer tooperform dan het volgende wordt gesynchroniseerd, die ongeveer 20 minuten optreden, zolang het Hallo-service wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="78abb-149">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="78abb-150">U kunt Hallo **synchronisatiedetails** sectie toomonitor uitgevoerd en volgt u koppelingen tooprovisioning activiteitsrapporten, waarin alle bewerkingen die worden uitgevoerd door het Hallo-service inricht.</span><span class="sxs-lookup"><span data-stu-id="78abb-150">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service.</span></span>

<span data-ttu-id="78abb-151">Zie voor meer informatie over hoe tooread hello Azure AD-inrichting registreert, [rapportage over automatische account gebruikersaanvragen](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="78abb-151">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="78abb-152">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="78abb-152">Additional resources</span></span>

* [<span data-ttu-id="78abb-153">Het beheren van gebruikers account inrichten voor zakelijke Apps</span><span class="sxs-lookup"><span data-stu-id="78abb-153">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="78abb-154">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="78abb-154">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="78abb-155">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="78abb-155">Next steps</span></span>

* [<span data-ttu-id="78abb-156">Informatie over hoe tooreview registreert en het ophalen van rapporten over het inrichten van activiteit</span><span class="sxs-lookup"><span data-stu-id="78abb-156">Learn how tooreview logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
