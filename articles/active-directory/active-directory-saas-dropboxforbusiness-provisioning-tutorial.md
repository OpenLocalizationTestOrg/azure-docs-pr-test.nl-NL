---
title: 'Zelfstudie: Azure Active Directory-integratie met Dropbox voor bedrijven | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Dropbox voor bedrijven.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0f3a42e4-6897-4234-af84-b47c148ec3e1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 0fb01eab4f7c6c4516eac64a4343e46ea221f98d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-dropbox-for-business-for-automatic-user-provisioning"></a><span data-ttu-id="1b331-103">Zelfstudie: Dropbox voor bedrijven configureren voor het automatisch gebruikers inrichten</span><span class="sxs-lookup"><span data-stu-id="1b331-103">Tutorial: Configuring Dropbox for Business for Automatic User Provisioning</span></span>

<span data-ttu-id="1b331-104">Hallo-doel van deze zelfstudie is tooshow u stappen die u tooperform in Dropbox voor bedrijven en Azure AD tooautomatically leveren en intrekken gebruikersaccounts vanuit Azure AD-tooDropbox voor bedrijven moet Hallo.</span><span class="sxs-lookup"><span data-stu-id="1b331-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Dropbox for Business and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooDropbox for Business.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1b331-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="1b331-105">Prerequisites</span></span>

<span data-ttu-id="1b331-106">Hallo scenario beschreven in deze zelfstudie wordt ervan uitgegaan dat u al hebt Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="1b331-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="1b331-107">Een Azure Active directory-tenant.</span><span class="sxs-lookup"><span data-stu-id="1b331-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="1b331-108">Een Dropbox voor bedrijven-eenmalige aanmelding ingeschakeld abonnement.</span><span class="sxs-lookup"><span data-stu-id="1b331-108">A Dropbox for Business single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="1b331-109">Een gebruikersaccount in Dropbox voor bedrijven met beheerdersmachtigingen Team.</span><span class="sxs-lookup"><span data-stu-id="1b331-109">A user account in Dropbox for Business with Team Admin permissions.</span></span>

## <a name="assigning-users-toodropbox-for-business"></a><span data-ttu-id="1b331-110">Gebruikers tooDropbox toewijzen voor bedrijven</span><span class="sxs-lookup"><span data-stu-id="1b331-110">Assigning users tooDropbox for Business</span></span>

<span data-ttu-id="1b331-111">Azure Active Directory gebruikt een concept 'toewijzingen' toodetermine welke gebruikers toegang tooselected apps krijgen genoemd.</span><span class="sxs-lookup"><span data-stu-id="1b331-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="1b331-112">In de context van de Hallo van automatische gebruikers account inrichten, alleen Hallo-gebruikers en groepen die '' tooan toepassing in Azure AD toegewezen zijn gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="1b331-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="1b331-113">Voordat u configureren en inschakelen van Hallo-service inricht, moet u toodecide welke gebruikers en/of groepen in Azure AD vertegenwoordigen Hallo-gebruikers die toegang moeten hebben tot tooyour Dropbox voor bedrijven-app.</span><span class="sxs-lookup"><span data-stu-id="1b331-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Dropbox for Business app.</span></span> <span data-ttu-id="1b331-114">Als besloten, kunt u deze gebruikers tooyour Dropbox voor bedrijven-app kunt toewijzen door hier Hallo-instructies te volgen:</span><span class="sxs-lookup"><span data-stu-id="1b331-114">Once decided, you can assign these users tooyour Dropbox for Business app by following hello instructions here:</span></span>

[<span data-ttu-id="1b331-115">Toewijzen van een gebruiker of groep tooan enterprise-app</span><span class="sxs-lookup"><span data-stu-id="1b331-115">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toodropbox-for-business"></a><span data-ttu-id="1b331-116">Belangrijke tips voor het toewijzen van gebruikers tooDropbox voor bedrijven</span><span class="sxs-lookup"><span data-stu-id="1b331-116">Important tips for assigning users tooDropbox for Business</span></span>

*   <span data-ttu-id="1b331-117">Het is raadzaam om één tooDropbox voor bedrijven tootest Hallo configuratie inrichten door Azure AD-gebruiker is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="1b331-117">It is recommended that a single Azure AD user is assigned tooDropbox for Business tootest hello provisioning configuration.</span></span> <span data-ttu-id="1b331-118">Extra gebruikers en/of groepen kunnen later worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="1b331-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="1b331-119">Wanneer een gebruiker tooDropbox toewijzen voor bedrijven, moet u een geldige gebruikersrol selecteren.</span><span class="sxs-lookup"><span data-stu-id="1b331-119">When assigning a user tooDropbox for Business, you must select a valid user role.</span></span> <span data-ttu-id="1b331-120">Hallo 'Default toegang' rol werkt niet voor het inrichten van...</span><span class="sxs-lookup"><span data-stu-id="1b331-120">hello "Default Access" role does not work for provisioning..</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="1b331-121">Geautomatiseerde Gebruikersinrichting inschakelen</span><span class="sxs-lookup"><span data-stu-id="1b331-121">Enable Automated User Provisioning</span></span>

<span data-ttu-id="1b331-122">Deze sectie helpt u bij het verbinden van uw Azure AD-tooDropbox voor bedrijven van gebruikersaccount inrichten API en Hallo service toocreate inrichting configureren, bijwerken en uitschakelen van toegewezen gebruikersaccounts in Dropbox voor bedrijven op basis van gebruikers en groepen toewijzing in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1b331-122">This section guides you through connecting your Azure AD tooDropbox for Business's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Dropbox for Business based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="1b331-123">U kunt ook tooenabled op basis van SAML eenmalige aanmelding voor Dropbox voor bedrijven, in het Hallo-instructies te volgen [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1b331-123">You may also choose tooenabled SAML-based Single Sign-On for Dropbox for Business, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="1b331-124">Eenmalige aanmelding kan worden geconfigureerd onafhankelijk van automatische inrichting, hoewel deze twee functies aanvulling van elkaar.</span><span class="sxs-lookup"><span data-stu-id="1b331-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-automatic-user-account-provisioning"></a><span data-ttu-id="1b331-125">tooconfigure automatische account gebruikersaanvragen:</span><span class="sxs-lookup"><span data-stu-id="1b331-125">tooconfigure automatic user account provisioning:</span></span>

1. <span data-ttu-id="1b331-126">In Hallo [Azure-portal](https://portal.azure.com), bladeren toohello **Azure Active Directory > zakelijke Apps > alle toepassingen** sectie.</span><span class="sxs-lookup"><span data-stu-id="1b331-126">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="1b331-127">Als u al Dropbox voor bedrijven hebt geconfigureerd voor eenmalige aanmelding, zoeken naar uw exemplaar van Dropbox voor bedrijven met Hallo zoekveld opgegeven.</span><span class="sxs-lookup"><span data-stu-id="1b331-127">If you have already configured Dropbox for Business for single sign-on, search for your instance of Dropbox for Business using hello search field.</span></span> <span data-ttu-id="1b331-128">Selecteer anders **toevoegen** en zoek naar **Dropbox voor bedrijven** in Hallo-toepassingsgalerie.</span><span class="sxs-lookup"><span data-stu-id="1b331-128">Otherwise, select **Add** and search for **Dropbox for Business** in hello application gallery.</span></span> <span data-ttu-id="1b331-129">Selecteer Dropbox voor bedrijven in zoekresultaten hello, en voeg deze tooyour lijst met toepassingen.</span><span class="sxs-lookup"><span data-stu-id="1b331-129">Select Dropbox for Business from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="1b331-130">Selecteer uw exemplaar van Dropbox voor bedrijven en vervolgens Hallo **inrichten** tabblad.</span><span class="sxs-lookup"><span data-stu-id="1b331-130">Select your instance of Dropbox for Business, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="1b331-131">Set Hallo **modus inrichting** te**automatische**.</span><span class="sxs-lookup"><span data-stu-id="1b331-131">Set hello **Provisioning Mode** too**Automatic**.</span></span> 

    ![Inrichting](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="1b331-133">Onder Hallo **beheerdersreferenties** sectie, klikt u op **autoriseren**.</span><span class="sxs-lookup"><span data-stu-id="1b331-133">Under hello **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="1b331-134">Er wordt een Dropbox voor zakelijke aanmeldingsdialoogvenster geopend in een nieuw browservenster.</span><span class="sxs-lookup"><span data-stu-id="1b331-134">It opens a Dropbox for Business login dialog in a new browser window.</span></span>

6. <span data-ttu-id="1b331-135">Op Hallo **aanmelden tooDropbox toolink met Azure AD** dialoogvenster Aanmelden tooyour Dropbox voor bedrijven-tenant.</span><span class="sxs-lookup"><span data-stu-id="1b331-135">On hello **Sign-in tooDropbox toolink with Azure AD** dialog, sign in tooyour Dropbox for Business tenant.</span></span>

     <span data-ttu-id="1b331-136">![Gebruikers inrichten](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769518.png "gebruikers inrichten")</span><span class="sxs-lookup"><span data-stu-id="1b331-136">![User provisioning](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769518.png "User provisioning")</span></span>

7. <span data-ttu-id="1b331-137">Bevestig dat u toogive Azure Active Directory machtiging toomake wijzigingen tooyour Dropbox voor bedrijven-tenant wilt.</span><span class="sxs-lookup"><span data-stu-id="1b331-137">Confirm that you would like toogive Azure Active Directory permission toomake changes tooyour Dropbox for Business tenant.</span></span> <span data-ttu-id="1b331-138">Klik op **toestaan**.</span><span class="sxs-lookup"><span data-stu-id="1b331-138">Click **Allow**.</span></span>
    
      <span data-ttu-id="1b331-139">![Gebruikers inrichten](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769519.png "gebruikers inrichten")</span><span class="sxs-lookup"><span data-stu-id="1b331-139">![User provisioning](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769519.png "User provisioning")</span></span>

8. <span data-ttu-id="1b331-140">Klik in hello Azure-portal, op **testverbinding** tooensure Azure AD verbinding kan maken van tooyour Dropbox voor bedrijven-app.</span><span class="sxs-lookup"><span data-stu-id="1b331-140">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Dropbox for Business app.</span></span> <span data-ttu-id="1b331-141">Als Hallo verbinding mislukt, zorg ervoor dat uw Dropbox voor bedrijven-account Team beheerdersmachtigingen heeft en probeer het Hallo **'Autoriseren'** stap opnieuw.</span><span class="sxs-lookup"><span data-stu-id="1b331-141">If hello connection fails, ensure your Dropbox for Business account has Team Admin permissions and try hello **"Authorize"** step again.</span></span>

9. <span data-ttu-id="1b331-142">Voer e-mailadres van een persoon of groep die inrichting fout meldingen in Hallo ontvangen moet Hallo **e-mailmelding** veld en Hallo selectievakje.</span><span class="sxs-lookup"><span data-stu-id="1b331-142">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox.</span></span>

10. <span data-ttu-id="1b331-143">Klik op **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="1b331-143">Click **Save.**</span></span>

11. <span data-ttu-id="1b331-144">Selecteer onder Hallo toewijzingen sectie, **tooDropbox voor bedrijven synchroniseren Azure Active Directory-gebruikers.**</span><span class="sxs-lookup"><span data-stu-id="1b331-144">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooDropbox for Business.**</span></span>

12. <span data-ttu-id="1b331-145">In Hallo **kenmerktoewijzingen** sectie, bekijkt hello gebruikerskenmerken die worden gesynchroniseerd vanuit Azure AD-tooDropbox voor bedrijven.</span><span class="sxs-lookup"><span data-stu-id="1b331-145">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooDropbox for Business.</span></span> <span data-ttu-id="1b331-146">kenmerken die zijn geselecteerd als Hallo **overeenkomend** eigenschappen zijn gebruikte toomatch Hallo gebruikersaccounts in Dropbox voor bedrijven voor update-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="1b331-146">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Dropbox for Business for update operations.</span></span> <span data-ttu-id="1b331-147">Selecteer Hallo knop toocommit wijzigingen zijn opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="1b331-147">Select hello Save button toocommit any changes.</span></span>

13. <span data-ttu-id="1b331-148">tooenable Hallo inrichting Azure AD-service voor Dropbox voor bedrijven, wijziging Hallo **inrichting Status** te**op** in Hallo Zoekinstellingen</span><span class="sxs-lookup"><span data-stu-id="1b331-148">tooenable hello Azure AD provisioning service for Dropbox for Business, change hello **Provisioning Status** too**On** in hello Settings section</span></span>

14. <span data-ttu-id="1b331-149">Klik op **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="1b331-149">Click **Save.**</span></span>

<span data-ttu-id="1b331-150">Hallo initiële synchronisatie van gebruikers en/of groepen die zijn toegewezen tooDropbox voor bedrijven in Hallo gebruikers en groepen sectie begint.</span><span class="sxs-lookup"><span data-stu-id="1b331-150">It starts hello initial synchronization of any users and/or groups assigned tooDropbox for Business in hello Users and Groups section.</span></span> <span data-ttu-id="1b331-151">de initiële synchronisatie Hallo duurt langer tooperform dan het volgende wordt gesynchroniseerd, die ongeveer 20 minuten optreden, zolang het Hallo-service wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="1b331-151">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="1b331-152">U kunt Hallo **synchronisatiedetails** sectie toomonitor uitgevoerd en volgt u koppelingen tooprovisioning activiteitsrapporten, waarin alle acties die worden uitgevoerd door hello voor bedrijven-app op uw Dropbox-service inricht.</span><span class="sxs-lookup"><span data-stu-id="1b331-152">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Dropbox for Business app.</span></span>

<span data-ttu-id="1b331-153">U kunt nu een testaccount maken.</span><span class="sxs-lookup"><span data-stu-id="1b331-153">You can now create a test account.</span></span> <span data-ttu-id="1b331-154">Wacht tot up too20 minuten tooverify die Hallo-account is gesynchroniseerd tooDropbox voor bedrijven.</span><span class="sxs-lookup"><span data-stu-id="1b331-154">Wait for up too20 minutes tooverify that hello account has been synchronized tooDropbox for Business.</span></span>

<span data-ttu-id="1b331-155">Een is voltooid gebruikersaanvragen cyclus wordt aangegeven door de bijbehorende status.</span><span class="sxs-lookup"><span data-stu-id="1b331-155">A successfully completed user provisioning cycle is indicated by a related status.</span></span>

<span data-ttu-id="1b331-156">![Gebruikers toewijzen](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/IC769523.png "gebruikers toewijzen")</span><span class="sxs-lookup"><span data-stu-id="1b331-156">![Assign users](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/IC769523.png "Assign users")</span></span>


## <a name="additional-resources"></a><span data-ttu-id="1b331-157">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="1b331-157">Additional resources</span></span>

* [<span data-ttu-id="1b331-158">Het beheren van gebruikers account inrichten voor zakelijke Apps</span><span class="sxs-lookup"><span data-stu-id="1b331-158">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1b331-159">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1b331-159">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="1b331-160">Eenmalige aanmelding configureren</span><span class="sxs-lookup"><span data-stu-id="1b331-160">Configure Single Sign-on</span></span>](active-directory-saas-dropboxforbusiness-tutorial.md)