---
title: 'Zelfstudie: Azure Active Directory-integratie met Jive | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Jive.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6fbfdbe7-d66c-4305-9fea-76d6a6a92830
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: b1c0d0bc2d79427c055f577fe5f9d30d10f1bbdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-jive-for-user-provisioning"></a><span data-ttu-id="cd982-103">Zelfstudie: Jive configureren voor gebruikers inrichten</span><span class="sxs-lookup"><span data-stu-id="cd982-103">Tutorial: Configuring Jive for User Provisioning</span></span>

<span data-ttu-id="cd982-104">Hallo-doel van deze zelfstudie is tooshow u stappen die u moet tooperform in Jive en Azure AD tooautomatically leveren en intrekken gebruikersaccounts vanuit Azure AD tooJive Hallo.</span><span class="sxs-lookup"><span data-stu-id="cd982-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Jive and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooJive.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cd982-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="cd982-105">Prerequisites</span></span>

<span data-ttu-id="cd982-106">Hallo scenario beschreven in deze zelfstudie wordt ervan uitgegaan dat u al hebt Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="cd982-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="cd982-107">Een Azure Active directory-tenant.</span><span class="sxs-lookup"><span data-stu-id="cd982-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="cd982-108">Een Jive eenmalige aanmelding ingeschakeld abonnement.</span><span class="sxs-lookup"><span data-stu-id="cd982-108">A Jive single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="cd982-109">Een gebruikersaccount in Jive met beheerdersmachtigingen Team.</span><span class="sxs-lookup"><span data-stu-id="cd982-109">A user account in Jive with Team Admin permissions.</span></span>

## <a name="assigning-users-toojive"></a><span data-ttu-id="cd982-110">Gebruikers tooJive toewijzen</span><span class="sxs-lookup"><span data-stu-id="cd982-110">Assigning users tooJive</span></span>

<span data-ttu-id="cd982-111">Azure Active Directory gebruikt een concept 'toewijzingen' toodetermine welke gebruikers toegang tooselected apps krijgen genoemd.</span><span class="sxs-lookup"><span data-stu-id="cd982-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="cd982-112">In de context van de Hallo van automatische gebruikers account inrichten, alleen Hallo-gebruikers en groepen die '' tooan toepassing in Azure AD toegewezen zijn gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="cd982-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="cd982-113">Voordat u configureren en inschakelen van Hallo-service inricht, moet u toodecide welke gebruikers en/of groepen in Azure AD Hallo-gebruikers die toegang moeten hebben tot tooyour Jive app vertegenwoordigen.</span><span class="sxs-lookup"><span data-stu-id="cd982-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Jive app.</span></span> <span data-ttu-id="cd982-114">Als besloten, kunt u deze app-gebruikers tooyour Jive toewijzen door hier Hallo-instructies te volgen:</span><span class="sxs-lookup"><span data-stu-id="cd982-114">Once decided, you can assign these users tooyour Jive app by following hello instructions here:</span></span>

[<span data-ttu-id="cd982-115">Toewijzen van een gebruiker of groep tooan enterprise-app</span><span class="sxs-lookup"><span data-stu-id="cd982-115">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toojive"></a><span data-ttu-id="cd982-116">Belangrijke tips voor het toewijzen van gebruikers tooJive</span><span class="sxs-lookup"><span data-stu-id="cd982-116">Important tips for assigning users tooJive</span></span>

*   <span data-ttu-id="cd982-117">Het is raadzaam om één Azure AD-gebruiker tooJive tootest Hallo inrichting configuratie worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="cd982-117">It is recommended that a single Azure AD user be assigned tooJive tootest hello provisioning configuration.</span></span> <span data-ttu-id="cd982-118">Extra gebruikers en/of groepen kunnen later worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="cd982-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="cd982-119">Wanneer u een gebruiker tooJive toewijst, moet u een geldige gebruikersrol.</span><span class="sxs-lookup"><span data-stu-id="cd982-119">When assigning a user tooJive, you must select a valid user role.</span></span> <span data-ttu-id="cd982-120">Hallo 'Default toegang' rol werkt niet voor het inrichten.</span><span class="sxs-lookup"><span data-stu-id="cd982-120">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="cd982-121">Gebruikersinrichting inschakelen</span><span class="sxs-lookup"><span data-stu-id="cd982-121">Enable User Provisioning</span></span>

<span data-ttu-id="cd982-122">Deze sectie helpt u bij het verbinden van uw Azure AD-tooJive gebruikersaccount inrichten API en Hallo service toocreate inrichting configureren, bijwerken en uitschakelen toegewezen gebruikersaccounts in Jive op basis van gebruikers en groepen toewijzen in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cd982-122">This section guides you through connecting your Azure AD tooJive's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Jive based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="cd982-123">U kunt ook tooenabled op basis van SAML eenmalige aanmelding voor Jive, in het Hallo-instructies te volgen [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="cd982-123">You may also choose tooenabled SAML-based Single Sign-On for Jive, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="cd982-124">Eenmalige aanmelding kan worden geconfigureerd onafhankelijk van automatische inrichting, hoewel deze twee functies aanvulling van elkaar.</span><span class="sxs-lookup"><span data-stu-id="cd982-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-user-account-provisioning"></a><span data-ttu-id="cd982-125">tooconfigure account gebruikersaanvragen:</span><span class="sxs-lookup"><span data-stu-id="cd982-125">tooconfigure user account provisioning:</span></span>

<span data-ttu-id="cd982-126">Hallo-doel van deze sectie is het toooutline hoe tooJive tooenable gebruikers inrichten van Active Directory-gebruiker accounts.</span><span class="sxs-lookup"><span data-stu-id="cd982-126">hello objective of this section is toooutline how tooenable user provisioning of Active Directory user accounts tooJive.</span></span>
<span data-ttu-id="cd982-127">Als onderdeel van deze procedure bent u vereiste tooprovide het beveiligingstoken van een gebruiker moet u toorequest van Jive.com.</span><span class="sxs-lookup"><span data-stu-id="cd982-127">As part of this procedure, you are required tooprovide a user security token you need toorequest from Jive.com.</span></span>

1. <span data-ttu-id="cd982-128">In Hallo [Azure-portal](https://portal.azure.com), bladeren toohello **Azure Active Directory > zakelijke Apps > alle toepassingen** sectie.</span><span class="sxs-lookup"><span data-stu-id="cd982-128">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="cd982-129">Als u Jive al hebt geconfigureerd voor eenmalige aanmelding, zoekt u uw exemplaar van Jive met Hallo zoekveld opgegeven.</span><span class="sxs-lookup"><span data-stu-id="cd982-129">If you have already configured Jive for single sign-on, search for your instance of Jive using hello search field.</span></span> <span data-ttu-id="cd982-130">Selecteer anders **toevoegen** en zoek naar **Jive** in Hallo-toepassingsgalerie.</span><span class="sxs-lookup"><span data-stu-id="cd982-130">Otherwise, select **Add** and search for **Jive** in hello application gallery.</span></span> <span data-ttu-id="cd982-131">Selecteer Jive in zoekresultaten hello, en voeg deze tooyour lijst met toepassingen.</span><span class="sxs-lookup"><span data-stu-id="cd982-131">Select Jive from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="cd982-132">Selecteer uw exemplaar van Jive en vervolgens Hallo **inrichten** tabblad.</span><span class="sxs-lookup"><span data-stu-id="cd982-132">Select your instance of Jive, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="cd982-133">Set Hallo **modus inrichting** te**automatische**.</span><span class="sxs-lookup"><span data-stu-id="cd982-133">Set hello **Provisioning Mode** too**Automatic**.</span></span> 

    ![Inrichting](./media/active-directory-saas-jive-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="cd982-135">Onder Hallo **beheerdersreferenties** sectie, bieden Hallo na configuratie-instellingen:</span><span class="sxs-lookup"><span data-stu-id="cd982-135">Under hello **Admin Credentials** section, provide hello following configuration settings:</span></span>
   
    <span data-ttu-id="cd982-136">a.</span><span class="sxs-lookup"><span data-stu-id="cd982-136">a.</span></span> <span data-ttu-id="cd982-137">In Hallo **Jive Beheerdersgebruikersnaam** textbox type een Jive accountnaam die heeft Hallo **systeembeheerder** profiel in Jive.com toegewezen.</span><span class="sxs-lookup"><span data-stu-id="cd982-137">In hello **Jive Admin User Name** textbox, type a Jive account name that has hello **System Administrator** profile in Jive.com assigned.</span></span>
   
    <span data-ttu-id="cd982-138">b.</span><span class="sxs-lookup"><span data-stu-id="cd982-138">b.</span></span> <span data-ttu-id="cd982-139">In Hallo **Jive beheerderswachtwoord** textbox Hallo een wachtwoord op voor dit account.</span><span class="sxs-lookup"><span data-stu-id="cd982-139">In hello **Jive Admin Password** textbox, type hello password for this account.</span></span>
   
    <span data-ttu-id="cd982-140">c.</span><span class="sxs-lookup"><span data-stu-id="cd982-140">c.</span></span> <span data-ttu-id="cd982-141">In Hallo **Jive Tenant-URL** textbox type Hallo Jive tenant-URL.</span><span class="sxs-lookup"><span data-stu-id="cd982-141">In hello **Jive Tenant URL** textbox, type hello Jive tenant URL.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="cd982-142">Hallo Jive tenant-URL is de URL die wordt gebruikt door uw organisatie toolog in tooJive.</span><span class="sxs-lookup"><span data-stu-id="cd982-142">hello Jive tenant URL is URL that is used by your organization toolog in tooJive.</span></span>  
      > <span data-ttu-id="cd982-143">Normaal gesproken Hallo-URL heeft Hallo volgende indeling: **www.\< organisatie\>. jive.com**.</span><span class="sxs-lookup"><span data-stu-id="cd982-143">Typically, hello URL has hello following format: **www.\<organization\>.jive.com**.</span></span>          

6. <span data-ttu-id="cd982-144">Klik in hello Azure-portal, op **testverbinding** tooensure Azure AD tooyour Jive app kunt verbinden.</span><span class="sxs-lookup"><span data-stu-id="cd982-144">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Jive app.</span></span>

7. <span data-ttu-id="cd982-145">Voer e-mailadres van een persoon of groep die inrichting fout meldingen in Hallo ontvangen moet Hallo **e-mailmelding** veld en controleer de onderstaande Hallo selectievakje.</span><span class="sxs-lookup"><span data-stu-id="cd982-145">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox below.</span></span>

8. <span data-ttu-id="cd982-146">Klik op **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="cd982-146">Click **Save.**</span></span>

9. <span data-ttu-id="cd982-147">Selecteer onder Hallo toewijzingen sectie, **tooJive synchroniseren Azure Active Directory-gebruikers.**</span><span class="sxs-lookup"><span data-stu-id="cd982-147">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooJive.**</span></span>

10. <span data-ttu-id="cd982-148">In Hallo **kenmerktoewijzingen** sectie, bekijkt hello gebruikerskenmerken die worden gesynchroniseerd vanuit Azure AD-tooJive.</span><span class="sxs-lookup"><span data-stu-id="cd982-148">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooJive.</span></span> <span data-ttu-id="cd982-149">kenmerken die zijn geselecteerd als Hallo **overeenkomend** eigenschappen zijn gebruikte toomatch Hallo gebruikersaccounts in Jive voor update-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="cd982-149">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Jive for update operations.</span></span> <span data-ttu-id="cd982-150">Selecteer Hallo knop toocommit wijzigingen zijn opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="cd982-150">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="cd982-151">tooenable Hallo inrichting Azure AD-service voor Jive, wijziging Hallo **inrichting Status** te**op** in Hallo Zoekinstellingen</span><span class="sxs-lookup"><span data-stu-id="cd982-151">tooenable hello Azure AD provisioning service for Jive, change hello **Provisioning Status** too**On** in hello Settings section</span></span>

12. <span data-ttu-id="cd982-152">Klik op **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="cd982-152">Click **Save.**</span></span>

<span data-ttu-id="cd982-153">Hallo initiële synchronisatie van gebruikers en/of groepen die zijn toegewezen tooJive in Hallo gebruikers en groepen sectie begint.</span><span class="sxs-lookup"><span data-stu-id="cd982-153">It starts hello initial synchronization of any users and/or groups assigned tooJive in hello Users and Groups section.</span></span> <span data-ttu-id="cd982-154">de initiële synchronisatie Hallo duurt langer tooperform dan het volgende wordt gesynchroniseerd, die ongeveer 20 minuten optreden, zolang het Hallo-service wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="cd982-154">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="cd982-155">U kunt Hallo **synchronisatiedetails** sectie toomonitor uitgevoerd en volgt u koppelingen tooprovisioning activiteitsrapporten, waarin alle bewerkingen die worden uitgevoerd door het Hallo-service op uw app Jive inrichting beschrijven.</span><span class="sxs-lookup"><span data-stu-id="cd982-155">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Jive app.</span></span>

<span data-ttu-id="cd982-156">U kunt nu een testaccount maken.</span><span class="sxs-lookup"><span data-stu-id="cd982-156">You can now create a test account.</span></span> <span data-ttu-id="cd982-157">Wacht tot up too20 minuten tooverify die Hallo-account is gesynchroniseerd tooJive.</span><span class="sxs-lookup"><span data-stu-id="cd982-157">Wait for up too20 minutes tooverify that hello account has been synchronized tooJive.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cd982-158">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="cd982-158">Additional resources</span></span>

* [<span data-ttu-id="cd982-159">Het beheren van gebruikers account inrichten voor zakelijke Apps</span><span class="sxs-lookup"><span data-stu-id="cd982-159">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cd982-160">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cd982-160">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="cd982-161">Eenmalige aanmelding configureren</span><span class="sxs-lookup"><span data-stu-id="cd982-161">Configure Single Sign-on</span></span>](active-directory-saas-jive-tutorial.md)