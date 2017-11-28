---
title: 'Zelfstudie: Azure Active Directory-integratie met Citrix GoToMeeting | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Citrix GoToMeeting.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0f59fedb-2cf8-48d2-a5fb-222ed943ff78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 3c6eed5309dfa384c292b0cf63f8aa58988add81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-citrix-gotomeeting-for-automatic-user-provisioning"></a><span data-ttu-id="6da36-103">Zelfstudie: Citrix GoToMeeting configureren voor het automatisch gebruikers inrichten</span><span class="sxs-lookup"><span data-stu-id="6da36-103">Tutorial: Configuring Citrix GoToMeeting for Automatic User Provisioning</span></span>

<span data-ttu-id="6da36-104">Hallo-doel van deze zelfstudie is tooshow u stappen die u moet tooperform in Citrix GoToMeeting en Azure AD tooautomatically leveren en intrekken gebruikersaccounts vanuit Azure AD-tooCitrix GoToMeeting Hallo.</span><span class="sxs-lookup"><span data-stu-id="6da36-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Citrix GoToMeeting and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooCitrix GoToMeeting.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6da36-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="6da36-105">Prerequisites</span></span>

<span data-ttu-id="6da36-106">Hallo scenario beschreven in deze zelfstudie wordt ervan uitgegaan dat u al hebt Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="6da36-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="6da36-107">Een Azure Active directory-tenant.</span><span class="sxs-lookup"><span data-stu-id="6da36-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="6da36-108">Een Citrix GoToMeeting eenmalige aanmelding ingeschakeld abonnement.</span><span class="sxs-lookup"><span data-stu-id="6da36-108">A Citrix GoToMeeting single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="6da36-109">Een gebruikersaccount in Citrix GoToMeeting met beheerdersmachtigingen Team.</span><span class="sxs-lookup"><span data-stu-id="6da36-109">A user account in Citrix GoToMeeting with Team Admin permissions.</span></span>

## <a name="assigning-users-toocitrix-gotomeeting"></a><span data-ttu-id="6da36-110">Gebruikers tooCitrix GoToMeeting toewijzen</span><span class="sxs-lookup"><span data-stu-id="6da36-110">Assigning users tooCitrix GoToMeeting</span></span>

<span data-ttu-id="6da36-111">Azure Active Directory gebruikt een concept 'toewijzingen' toodetermine welke gebruikers toegang tooselected apps krijgen genoemd.</span><span class="sxs-lookup"><span data-stu-id="6da36-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="6da36-112">In de context van de Hallo van automatische gebruikers account inrichten, alleen Hallo-gebruikers en groepen die '' tooan toepassing in Azure AD toegewezen zijn gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="6da36-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="6da36-113">Voordat u configureren en inschakelen van Hallo-service inricht, moet u toodecide welke gebruikers en/of groepen in Azure AD Hallo-gebruikers die toegang moeten hebben tot tooyour Citrix GoToMeeting app vertegenwoordigen.</span><span class="sxs-lookup"><span data-stu-id="6da36-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Citrix GoToMeeting app.</span></span> <span data-ttu-id="6da36-114">Als besloten, kunt u deze gebruikers tooyour Citrix GoToMeeting app toewijzen door hier Hallo-instructies te volgen:</span><span class="sxs-lookup"><span data-stu-id="6da36-114">Once decided, you can assign these users tooyour Citrix GoToMeeting app by following hello instructions here:</span></span>

[<span data-ttu-id="6da36-115">Toewijzen van een gebruiker of groep tooan enterprise-app</span><span class="sxs-lookup"><span data-stu-id="6da36-115">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toocitrix-gotomeeting"></a><span data-ttu-id="6da36-116">Belangrijke tips voor het toewijzen van gebruikers tooCitrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="6da36-116">Important tips for assigning users tooCitrix GoToMeeting</span></span>

*   <span data-ttu-id="6da36-117">Het is raadzaam om één tooCitrix GoToMeeting tootest Hallo configuratie inrichten door Azure AD-gebruiker is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="6da36-117">It is recommended that a single Azure AD user is assigned tooCitrix GoToMeeting tootest hello provisioning configuration.</span></span> <span data-ttu-id="6da36-118">Extra gebruikers en/of groepen kunnen later worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="6da36-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="6da36-119">Wanneer u een gebruiker tooCitrix GoToMeeting toewijst, moet u een geldige gebruikersrol selecteren.</span><span class="sxs-lookup"><span data-stu-id="6da36-119">When assigning a user tooCitrix GoToMeeting, you must select a valid user role.</span></span> <span data-ttu-id="6da36-120">Hallo 'Default toegang' rol werkt niet voor het inrichten.</span><span class="sxs-lookup"><span data-stu-id="6da36-120">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="6da36-121">Geautomatiseerde Gebruikersinrichting inschakelen</span><span class="sxs-lookup"><span data-stu-id="6da36-121">Enable Automated User Provisioning</span></span>

<span data-ttu-id="6da36-122">Deze sectie helpt u bij het verbinden van uw Azure AD tooCitrix GoToMeeting gebruikersaccount inrichten API en Hallo service toocreate inrichting configureren, bijwerken en uitschakelen van de toegewezen gebruiker accounts in Citrix GoToMeeting op basis van gebruikers en groepen toewijzing in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6da36-122">This section guides you through connecting your Azure AD tooCitrix GoToMeeting's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Citrix GoToMeeting based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="6da36-123">U kunt ook tooenabled op basis van SAML eenmalige aanmelding voor Citrix GoToMeeting, in het Hallo-instructies te volgen [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6da36-123">You may also choose tooenabled SAML-based Single Sign-On for Citrix GoToMeeting, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="6da36-124">Eenmalige aanmelding kan worden geconfigureerd onafhankelijk van automatische inrichting, hoewel deze twee functies aanvulling van elkaar.</span><span class="sxs-lookup"><span data-stu-id="6da36-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-automatic-user-account-provisioning"></a><span data-ttu-id="6da36-125">tooconfigure automatische account gebruikersaanvragen:</span><span class="sxs-lookup"><span data-stu-id="6da36-125">tooconfigure automatic user account provisioning:</span></span>

1. <span data-ttu-id="6da36-126">In Hallo [Azure-portal](https://portal.azure.com), bladeren toohello **Azure Active Directory > zakelijke Apps > alle toepassingen** sectie.</span><span class="sxs-lookup"><span data-stu-id="6da36-126">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="6da36-127">Als u Citrix GoToMeeting al hebt geconfigureerd voor eenmalige aanmelding, zoekt u uw exemplaar van Citrix GoToMeeting met Hallo zoekveld opgegeven.</span><span class="sxs-lookup"><span data-stu-id="6da36-127">If you have already configured Citrix GoToMeeting for single sign-on, search for your instance of Citrix GoToMeeting using hello search field.</span></span> <span data-ttu-id="6da36-128">Selecteer anders **toevoegen** en zoek naar **Citrix GoToMeeting** in Hallo-toepassingsgalerie.</span><span class="sxs-lookup"><span data-stu-id="6da36-128">Otherwise, select **Add** and search for **Citrix GoToMeeting** in hello application gallery.</span></span> <span data-ttu-id="6da36-129">Citrix GoToMeeting selecteert in de zoekresultaten hello, en voeg deze tooyour lijst met toepassingen.</span><span class="sxs-lookup"><span data-stu-id="6da36-129">Select Citrix GoToMeeting from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="6da36-130">Selecteer uw exemplaar van Citrix GoToMeeting en vervolgens Hallo **inrichten** tabblad.</span><span class="sxs-lookup"><span data-stu-id="6da36-130">Select your instance of Citrix GoToMeeting, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="6da36-131">Set Hallo **inrichten** modus te**automatische**.</span><span class="sxs-lookup"><span data-stu-id="6da36-131">Set hello **Provisioning** Mode too**Automatic**.</span></span> 

    ![Inrichting](./media/active-directory-saas-citrixgotomeeting-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="6da36-133">Voer onder Hallo beheerdersreferenties sectie, Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="6da36-133">Under hello Admin Credentials section, perform hello following steps:</span></span>
   
    <span data-ttu-id="6da36-134">a.</span><span class="sxs-lookup"><span data-stu-id="6da36-134">a.</span></span> <span data-ttu-id="6da36-135">In Hallo **Citrix GoToMeeting Beheerdersgebruikersnaam** textbox, typ de gebruikersnaam van een beheerder Hallo.</span><span class="sxs-lookup"><span data-stu-id="6da36-135">In hello **Citrix GoToMeeting Admin User Name** textbox, type hello user name of an administrator.</span></span>

    <span data-ttu-id="6da36-136">b.</span><span class="sxs-lookup"><span data-stu-id="6da36-136">b.</span></span> <span data-ttu-id="6da36-137">In Hallo **Citrix GoToMeeting beheerderswachtwoord** textbox Hallo beheerderswachtwoord.</span><span class="sxs-lookup"><span data-stu-id="6da36-137">In hello **Citrix GoToMeeting Admin Password** textbox, hello administrator's password.</span></span>

6. <span data-ttu-id="6da36-138">In hello Azure-portal, klikt u op **testverbinding** tooensure Azure AD verbinding tooyour Citrix GoToMeeting app kunt maken.</span><span class="sxs-lookup"><span data-stu-id="6da36-138">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Citrix GoToMeeting app.</span></span> <span data-ttu-id="6da36-139">Als Hallo verbinding mislukt, zorg ervoor dat uw account Citrix GoToMeeting Team beheerdersmachtigingen heeft en probeer het Hallo **'Beheerdersreferenties'** stap opnieuw.</span><span class="sxs-lookup"><span data-stu-id="6da36-139">If hello connection fails, ensure your Citrix GoToMeeting account has Team Admin permissions and try hello **"Admin Credentials"** step again.</span></span>

7. <span data-ttu-id="6da36-140">Voer e-mailadres van een persoon of groep die inrichting fout meldingen in Hallo ontvangen moet Hallo **e-mailmelding** veld en Hallo selectievakje.</span><span class="sxs-lookup"><span data-stu-id="6da36-140">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox.</span></span>

8. <span data-ttu-id="6da36-141">Klik op **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="6da36-141">Click **Save.**</span></span>

9. <span data-ttu-id="6da36-142">Selecteer onder Hallo toewijzingen sectie, **synchroniseren Azure Active Directory: gebruikers tooCitrix GoToMeeting.**</span><span class="sxs-lookup"><span data-stu-id="6da36-142">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooCitrix GoToMeeting.**</span></span>

10. <span data-ttu-id="6da36-143">In Hallo **kenmerktoewijzingen** sectie, bekijkt hello gebruikerskenmerken die worden gesynchroniseerd vanuit Azure AD-tooCitrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="6da36-143">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooCitrix GoToMeeting.</span></span> <span data-ttu-id="6da36-144">kenmerken die zijn geselecteerd als Hallo **overeenkomend** eigenschappen zijn gebruikte toomatch Hallo gebruikersaccounts in Citrix GoToMeeting voor update-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="6da36-144">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Citrix GoToMeeting for update operations.</span></span> <span data-ttu-id="6da36-145">Selecteer Hallo knop toocommit wijzigingen zijn opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="6da36-145">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="6da36-146">tooenable Hallo inrichting Azure AD-service voor Citrix GoToMeeting, wijziging Hallo **inrichting Status** te**op** in Hallo Zoekinstellingen</span><span class="sxs-lookup"><span data-stu-id="6da36-146">tooenable hello Azure AD provisioning service for Citrix GoToMeeting, change hello **Provisioning Status** too**On** in hello Settings section</span></span>

12. <span data-ttu-id="6da36-147">Klik op **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="6da36-147">Click **Save.**</span></span>

<span data-ttu-id="6da36-148">Deze begint de initiële synchronisatie Hallo van alle gebruikers en/of groepen tooCitrix GoToMeeting in de sectie gebruikers en groepen Hallo toegewezen.</span><span class="sxs-lookup"><span data-stu-id="6da36-148">It starts hello initial synchronization of any users and/or groups assigned tooCitrix GoToMeeting in hello Users and Groups section.</span></span> <span data-ttu-id="6da36-149">de initiële synchronisatie Hallo duurt langer tooperform dan het volgende wordt gesynchroniseerd, die ongeveer 20 minuten optreden, zolang het Hallo-service wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="6da36-149">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="6da36-150">U kunt Hallo **synchronisatiedetails** sectie toomonitor uitgevoerd en volgt u koppelingen tooprovisioning activiteitsrapporten, waarin alle bewerkingen die worden uitgevoerd door het Hallo-service op uw app Citrix GoToMeeting inrichting beschrijven.</span><span class="sxs-lookup"><span data-stu-id="6da36-150">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Citrix GoToMeeting app.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6da36-151">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="6da36-151">Additional resources</span></span>

* [<span data-ttu-id="6da36-152">Het beheren van gebruikers account inrichten voor zakelijke Apps</span><span class="sxs-lookup"><span data-stu-id="6da36-152">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6da36-153">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6da36-153">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="6da36-154">Eenmalige aanmelding configureren</span><span class="sxs-lookup"><span data-stu-id="6da36-154">Configure Single Sign-on</span></span>](active-directory-saas-citrix-gotomeeting-tutorial.md)


