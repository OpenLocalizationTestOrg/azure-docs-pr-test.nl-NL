---
title: 'Zelfstudie: LinkedIn Lookup configureren voor het automatisch gebruikers inrichten met Azure Active Directory | Microsoft Docs'
description: Meer informatie over hoe tooconfigure Azure Active Directory tooautomatically leveren en intrekken gebruikersaccounts tooLinkedIn opzoeken.
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
ms.date: 04/15/2017
ms.author: asmalser-msft
ms.openlocfilehash: 3e41abb8af00715f70e5a14d9d26ff600c10f492
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-linkedin-lookup-for-automatic-user-provisioning"></a><span data-ttu-id="8ed73-103">Zelfstudie: LinkedIn Lookup configureren voor het automatisch gebruikers inrichten</span><span class="sxs-lookup"><span data-stu-id="8ed73-103">Tutorial: Configuring LinkedIn Lookup for Automatic User Provisioning</span></span>


<span data-ttu-id="8ed73-104">Hallo-doel van deze zelfstudie is tooshow u stappen die u moet tooperform in LinkedIn opzoeken en Azure AD tooautomatically leveren en intrekken gebruikersaccounts vanuit Azure AD tooLinkedIn Lookup Hallo.</span><span class="sxs-lookup"><span data-stu-id="8ed73-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in LinkedIn Lookup and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooLinkedIn Lookup.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="8ed73-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="8ed73-105">Prerequisites</span></span>

<span data-ttu-id="8ed73-106">Hallo scenario beschreven in deze zelfstudie wordt ervan uitgegaan dat u al hebt Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="8ed73-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="8ed73-107">Een Azure Active Directory-tenant</span><span class="sxs-lookup"><span data-stu-id="8ed73-107">An Azure Active Directory tenant</span></span>
*   <span data-ttu-id="8ed73-108">Een tenant LinkedIn Lookup</span><span class="sxs-lookup"><span data-stu-id="8ed73-108">A LinkedIn Lookup tenant</span></span> 
*   <span data-ttu-id="8ed73-109">Een administrator-account in LinkedIn Lookup met toegang toohello LinkedIn Account Center</span><span class="sxs-lookup"><span data-stu-id="8ed73-109">An administrator account in LinkedIn Lookup with access toohello LinkedIn Account Center</span></span>

> [!NOTE]
> <span data-ttu-id="8ed73-110">Azure Active Directory is geïntegreerd met LinkedIn Lookup met Hallo [SCIM](http://www.simplecloud.info/) protocol.</span><span class="sxs-lookup"><span data-stu-id="8ed73-110">Azure Active Directory integrates with LinkedIn Lookup using hello [SCIM](http://www.simplecloud.info/) protocol.</span></span>

## <a name="assigning-users-toolinkedin-lookup"></a><span data-ttu-id="8ed73-111">Toewijzen van gebruikers tooLinkedIn Lookup</span><span class="sxs-lookup"><span data-stu-id="8ed73-111">Assigning users tooLinkedIn Lookup</span></span>

<span data-ttu-id="8ed73-112">Azure Active Directory gebruikt een concept 'toewijzingen' toodetermine welke gebruikers toegang tooselected apps krijgen genoemd.</span><span class="sxs-lookup"><span data-stu-id="8ed73-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="8ed73-113">In de context van de Hallo van automatische gebruikers account inrichten, worden alleen Hallo-gebruikers en groepen die '' tooan toepassing in Azure AD toegewezen zijn gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="8ed73-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD will be synchronized.</span></span> 

<span data-ttu-id="8ed73-114">Voordat u configureren en inschakelen van Hallo-service inricht, moet u toodecide welke gebruikers en/of groepen in Azure AD Hallo-gebruikers die toegang moeten hebben tot tooLinkedIn Lookup vertegenwoordigen.</span><span class="sxs-lookup"><span data-stu-id="8ed73-114">Before configuring and enabling hello provisioning service, you will need toodecide what users and/or groups in Azure AD represent hello users who need access tooLinkedIn Lookup.</span></span> <span data-ttu-id="8ed73-115">Als besloten, kunt u deze gebruikers tooLinkedIn Lookup toewijzen door hier Hallo-instructies te volgen:</span><span class="sxs-lookup"><span data-stu-id="8ed73-115">Once decided, you can assign these users tooLinkedIn Lookup by following hello instructions here:</span></span>

[<span data-ttu-id="8ed73-116">Toewijzen van een gebruiker of groep tooan enterprise-app</span><span class="sxs-lookup"><span data-stu-id="8ed73-116">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toolinkedin-lookup"></a><span data-ttu-id="8ed73-117">Belangrijke tips voor het toewijzen van gebruikers tooLinkedIn Lookup</span><span class="sxs-lookup"><span data-stu-id="8ed73-117">Important tips for assigning users tooLinkedIn Lookup</span></span>

*   <span data-ttu-id="8ed73-118">Het is raadzaam om één Azure AD-gebruiker tooLinkedIn Lookup tootest Hallo inrichting configuratie worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="8ed73-118">It is recommended that a single Azure AD user be assigned tooLinkedIn Lookup tootest hello provisioning configuration.</span></span> <span data-ttu-id="8ed73-119">Extra gebruikers en/of groepen kunnen later worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="8ed73-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="8ed73-120">Bij het toewijzen van een gebruiker tooLinkedIn opzoeken, moet u Hallo **gebruiker** rol in het dialoogvenster voor Hallo-toewijzing.</span><span class="sxs-lookup"><span data-stu-id="8ed73-120">When assigning a user tooLinkedIn Lookup, you must select hello **User** role in hello assignment dialog.</span></span> <span data-ttu-id="8ed73-121">Hallo 'Default toegang' rol werkt niet voor het inrichten.</span><span class="sxs-lookup"><span data-stu-id="8ed73-121">hello "Default Access" role does not work for provisioning.</span></span>


## <a name="configuring-user-provisioning-toolinkedin-lookup"></a><span data-ttu-id="8ed73-122">Gebruikers inrichten tooLinkedIn Lookup configureren</span><span class="sxs-lookup"><span data-stu-id="8ed73-122">Configuring user provisioning tooLinkedIn Lookup</span></span>

<span data-ttu-id="8ed73-123">Deze sectie helpt u bij het verbinding maken met uw Azure AD tooLinkedIn Lookup SCIM-gebruikersaccount inrichten API en Hallo service toocreate inrichting configureren, bijwerken en uitschakelen van de toegewezen gebruiker accounts in LinkedIn opzoeken op basis van gebruikers en groepen toewijzing in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8ed73-123">This section guides you through connecting your Azure AD tooLinkedIn Lookup's SCIM user account provisioning API, and configuring hello provisioning service toocreate, update and disable assigned user accounts in LinkedIn Lookup based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="8ed73-124">U kunt ook tooenabled op basis van SAML eenmalige aanmelding voor het opzoeken van LinkedIn, in het Hallo-instructies te volgen [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8ed73-124">You may also choose tooenabled SAML-based Single Sign-On for LinkedIn Lookup, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="8ed73-125">Eenmalige aanmelding kan worden geconfigureerd onafhankelijk van automatische inrichting, hoewel deze twee functies elkaar aanvullen.</span><span class="sxs-lookup"><span data-stu-id="8ed73-125">Single sign-on can be configured independently of automatic provisioning, though these two features complement each other.</span></span>


### <a name="tooconfigure-automatic-user-account-provisioning-toolinkedin-lookup-in-azure-ad"></a><span data-ttu-id="8ed73-126">tooconfigure automatische gebruikersaccount tooLinkedIn Lookup ingericht in Azure AD:</span><span class="sxs-lookup"><span data-stu-id="8ed73-126">tooconfigure automatic user account provisioning tooLinkedIn Lookup in Azure AD:</span></span>


<span data-ttu-id="8ed73-127">de eerste stap Hallo tooretrieve is uw toegangstoken LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="8ed73-127">hello first step is tooretrieve your LinkedIn access token.</span></span> <span data-ttu-id="8ed73-128">Als u een ondernemingsadministrator bent, kunt u zelf een toegangstoken inrichten.</span><span class="sxs-lookup"><span data-stu-id="8ed73-128">If you are an Enterprise administrator, you can self-provision an access token.</span></span> <span data-ttu-id="8ed73-129">Ga te in uw accountcentrum**instellingen &gt; globale instellingen** en open Hallo **SCIM Setup** Configuratiescherm.</span><span class="sxs-lookup"><span data-stu-id="8ed73-129">In your account center, go too**Settings &gt; Global Settings** and open hello **SCIM Setup** panel.</span></span>

> [!NOTE]
> <span data-ttu-id="8ed73-130">Als u Hallo-accountcentrum rechtstreeks in plaats van via een koppeling opent, kunt u met behulp van de volgende stappen uit Hallo bereiken.</span><span class="sxs-lookup"><span data-stu-id="8ed73-130">If you are accessing hello account center directly rather than through a link, you can reach it using hello following steps.</span></span>

1)  <span data-ttu-id="8ed73-131">Meld u aan tooAccount Center.</span><span class="sxs-lookup"><span data-stu-id="8ed73-131">Sign in tooAccount Center.</span></span>

2)  <span data-ttu-id="8ed73-132">Selecteer **Admin &gt; beheerdersinstellingen** .</span><span class="sxs-lookup"><span data-stu-id="8ed73-132">Select **Admin &gt; Admin Settings** .</span></span>

3)  <span data-ttu-id="8ed73-133">Klik op **integraties geavanceerde** op Hallo links zijbalk.</span><span class="sxs-lookup"><span data-stu-id="8ed73-133">Click **Advanced Integrations** on hello left sidebar.</span></span> <span data-ttu-id="8ed73-134">U bent gerichte toohello-accountcentrum.</span><span class="sxs-lookup"><span data-stu-id="8ed73-134">You are directed toohello account center.</span></span>

4)  <span data-ttu-id="8ed73-135">Klik op **+ toevoegen nieuwe SCIM configuratie** en volg de procedure Hallo door in elk veld te vullen.</span><span class="sxs-lookup"><span data-stu-id="8ed73-135">Click **+ Add new SCIM configuration** and follow hello procedure by filling in each field.</span></span>

> <span data-ttu-id="8ed73-136">Wanneer autoassign licenties niet is ingeschakeld, betekent dit dat alleen de gegevens van de gebruiker is gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="8ed73-136">When auto­assign licenses is not enabled, it means that only user data is synced.</span></span>

![LinkedIn Lookup inrichten](./media/active-directory-saas-linkedinlookup-provisioning-tutorial/linkedin_1.PNG)

> <span data-ttu-id="8ed73-138">Wanneer autolicense toewijzing is ingeschakeld, moet u het toepassingsexemplaar toonote en licentietype.</span><span class="sxs-lookup"><span data-stu-id="8ed73-138">When auto­license assignment is enabled, you need toonote the application instance and license type.</span></span> <span data-ttu-id="8ed73-139">Licenties zijn toegewezen op een eerst komt, eerst basis fungeren totdat alle Hallo-licenties worden gehaald.</span><span class="sxs-lookup"><span data-stu-id="8ed73-139">Licenses are assigned on a first come, first serve basis until all hello licenses are taken.</span></span>

![LinkedIn Lookup inrichten](./media/active-directory-saas-linkedinlookup-provisioning-tutorial/linkedin_2.PNG)

5)  <span data-ttu-id="8ed73-141">Klik op **Generate token**.</span><span class="sxs-lookup"><span data-stu-id="8ed73-141">Click **Generate token**.</span></span> <span data-ttu-id="8ed73-142">U ziet uw toegang tot token weergeven onder Hallo **toegangstoken** veld.</span><span class="sxs-lookup"><span data-stu-id="8ed73-142">You should see your access token display under hello **Access token** field.</span></span>

6)  <span data-ttu-id="8ed73-143">Sla de toegang tot token tooyour Klembord of de computer voordat u Hallo pagina verlaat.</span><span class="sxs-lookup"><span data-stu-id="8ed73-143">Save your access token tooyour clipboard or computer before leaving hello page.</span></span>

7) <span data-ttu-id="8ed73-144">Meld je vervolgens in toohello [Azure-portal](https://portal.azure.com), en blader toohello **Azure Active Directory > zakelijke Apps > alle toepassingen** sectie.</span><span class="sxs-lookup"><span data-stu-id="8ed73-144">Next, sign in toohello [Azure portal](https://portal.azure.com), and browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

8) <span data-ttu-id="8ed73-145">Als u LinkedIn Lookup voor eenmalige aanmelding al hebt geconfigureerd, kunt u zoeken naar uw exemplaar van LinkedIn zoeken met behulp van Hallo zoekveld opgegeven.</span><span class="sxs-lookup"><span data-stu-id="8ed73-145">If you have already configured LinkedIn Lookup for single sign-on, search for your instance of LinkedIn Lookup using hello search field.</span></span> <span data-ttu-id="8ed73-146">Selecteer anders **toevoegen** en zoek naar **LinkedIn Lookup** in Hallo-toepassingsgalerie.</span><span class="sxs-lookup"><span data-stu-id="8ed73-146">Otherwise, select **Add** and search for **LinkedIn Lookup** in hello application gallery.</span></span> <span data-ttu-id="8ed73-147">Selecteer LinkedIn opzoeken in zoekresultaten hello, en voeg deze tooyour lijst met toepassingen.</span><span class="sxs-lookup"><span data-stu-id="8ed73-147">Select LinkedIn Lookup from hello search results, and add it tooyour list of applications.</span></span>

9)  <span data-ttu-id="8ed73-148">Selecteer uw exemplaar van LinkedIn zoeken en vervolgens Hallo **inrichten** tabblad.</span><span class="sxs-lookup"><span data-stu-id="8ed73-148">Select your instance of LinkedIn Lookup, then select hello **Provisioning** tab.</span></span>

10) <span data-ttu-id="8ed73-149">Set Hallo **modus inrichting** te**automatische**.</span><span class="sxs-lookup"><span data-stu-id="8ed73-149">Set hello **Provisioning Mode** too**Automatic**.</span></span>

![LinkedIn Lookup inrichten](./media/active-directory-saas-linkedinlookup-provisioning-tutorial/linkedin_3.PNG)

11)  <span data-ttu-id="8ed73-151">Hallo volgen onder velden invullen **beheerdersreferenties** :</span><span class="sxs-lookup"><span data-stu-id="8ed73-151">Fill in hello following fields under **Admin Credentials** :</span></span>

* <span data-ttu-id="8ed73-152">In Hallo **Tenant-URL** Voer https://api.linkedin.com.</span><span class="sxs-lookup"><span data-stu-id="8ed73-152">In hello **Tenant URL** field, enter https://api.linkedin.com.</span></span>

* <span data-ttu-id="8ed73-153">In Hallo **geheim Token** veld Hallo-toegangstoken die u in stap 1 hebt gegenereerd en op **testverbinding** .</span><span class="sxs-lookup"><span data-stu-id="8ed73-153">In hello **Secret Token** field, enter hello access token you generated in step 1 and click **Test Connection** .</span></span>

* <span data-ttu-id="8ed73-154">U ziet een melding geslaagd Hallo upperright zijde van de portal.</span><span class="sxs-lookup"><span data-stu-id="8ed73-154">You should see a success notification on hello upper­right side of   your portal.</span></span>

12) <span data-ttu-id="8ed73-155">Voer e-mailadres van een persoon of groep die inrichting fout meldingen in Hallo ontvangen moet Hallo **e-mailmelding** veld en controleer de onderstaande Hallo selectievakje.</span><span class="sxs-lookup"><span data-stu-id="8ed73-155">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox below.</span></span>

13) <span data-ttu-id="8ed73-156">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="8ed73-156">Click **Save**.</span></span> 

14) <span data-ttu-id="8ed73-157">In Hallo **kenmerktoewijzingen** sectie, bekijkt hello gebruikers- en groepskenmerken die wordt gesynchroniseerd vanaf de Azure AD tooLinkedIn opzoeken.</span><span class="sxs-lookup"><span data-stu-id="8ed73-157">In hello **Attribute Mappings** section, review hello user and group attributes that will be synchronized from Azure AD tooLinkedIn Lookup.</span></span> <span data-ttu-id="8ed73-158">Let op: kenmerken die zijn geselecteerd als Hallo **overeenkomend** eigenschappen worden gebruikte toomatch Hallo gebruikersaccounts en groepen in LinkedIn Lookup voor update-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="8ed73-158">Note that hello attributes selected as **Matching** properties will be used toomatch hello user accounts and groups in LinkedIn Lookup for update operations.</span></span> <span data-ttu-id="8ed73-159">Selecteer Hallo knop toocommit wijzigingen zijn opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="8ed73-159">Select hello Save button toocommit any changes.</span></span>

![LinkedIn Lookup inrichten](./media/active-directory-saas-linkedinlookup-provisioning-tutorial/linkedin_4.PNG)

15) <span data-ttu-id="8ed73-161">tooenable Hallo inrichting Azure AD-service voor het opzoeken van LinkedIn, wijziging Hallo **inrichting Status** te**op** in Hallo **instellingen** sectie</span><span class="sxs-lookup"><span data-stu-id="8ed73-161">tooenable hello Azure AD provisioning service for LinkedIn Lookup, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

16) <span data-ttu-id="8ed73-162">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="8ed73-162">Click **Save**.</span></span> 

<span data-ttu-id="8ed73-163">Hiermee start u de initiële synchronisatie Hallo van alle gebruikers en/of groepen tooLinkedIn opzoeken in de sectie gebruikers en groepen Hallo toegewezen.</span><span class="sxs-lookup"><span data-stu-id="8ed73-163">This will start hello initial synchronization of any users and/or groups assigned tooLinkedIn Lookup in hello Users and Groups section.</span></span> <span data-ttu-id="8ed73-164">Houd er rekening mee dat de initiële synchronisatie Hallo langer tooperform dan het volgende wordt gesynchroniseerd, die ongeveer 20 minuten optreden duurt, zolang het Hallo-service wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8ed73-164">Note that hello initial sync will take longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="8ed73-165">U kunt Hallo **synchronisatiedetails** sectie toomonitor uitgevoerd en volgt u koppelingen tooprovisioning activiteitsrapporten, waarin alle bewerkingen die worden uitgevoerd door het Hallo-service op uw app LinkedIn Lookup inrichting beschrijven.</span><span class="sxs-lookup"><span data-stu-id="8ed73-165">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your LinkedIn Lookup app.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="8ed73-166">Aanvullende resources</span><span class="sxs-lookup"><span data-stu-id="8ed73-166">Additional Resources</span></span>

* [<span data-ttu-id="8ed73-167">Het beheren van gebruikers account inrichten voor zakelijke Apps</span><span class="sxs-lookup"><span data-stu-id="8ed73-167">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="8ed73-168">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8ed73-168">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
