---
title: 'Zelfstudie: Azure Active Directory-integratie met DocuSign | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en DocuSign.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 294cd6b8-74d7-44bc-92bc-020ccd13ff12
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: 8562a8f9e05fb72d3331507b7da5c6afee38f9b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-docusign-for-user-provisioning"></a><span data-ttu-id="69757-103">Zelfstudie: DocuSign configureren voor gebruikers inrichten</span><span class="sxs-lookup"><span data-stu-id="69757-103">Tutorial: Configuring DocuSign for User Provisioning</span></span>

<span data-ttu-id="69757-104">Hallo-doel van deze zelfstudie is tooshow u stappen die u moet tooperform in DocuSign en Azure AD tooautomatically leveren en intrekken gebruikersaccounts vanuit Azure AD tooDocuSign Hallo.</span><span class="sxs-lookup"><span data-stu-id="69757-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in DocuSign and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooDocuSign.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="69757-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="69757-105">Prerequisites</span></span>

<span data-ttu-id="69757-106">Hallo scenario beschreven in deze zelfstudie wordt ervan uitgegaan dat u al hebt Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="69757-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="69757-107">Een Azure Active directory-tenant.</span><span class="sxs-lookup"><span data-stu-id="69757-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="69757-108">Een DocuSign eenmalige aanmelding ingeschakeld abonnement.</span><span class="sxs-lookup"><span data-stu-id="69757-108">A DocuSign single sign-on enabled subscription.</span></span>
*   <span data-ttu-id="69757-109">Een gebruikersaccount in DocuSign met beheerdersmachtigingen Team.</span><span class="sxs-lookup"><span data-stu-id="69757-109">A user account in DocuSign with Team Admin permissions.</span></span>

## <a name="assigning-users-toodocusign"></a><span data-ttu-id="69757-110">Gebruikers tooDocuSign toewijzen</span><span class="sxs-lookup"><span data-stu-id="69757-110">Assigning users tooDocuSign</span></span>

<span data-ttu-id="69757-111">Azure Active Directory gebruikt een concept 'toewijzingen' toodetermine welke gebruikers toegang tooselected apps krijgen genoemd.</span><span class="sxs-lookup"><span data-stu-id="69757-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="69757-112">In de context van de Hallo van automatische gebruikers account inrichten, worden alleen Hallo-gebruikers en groepen die '' tooan toepassing in Azure AD toegewezen zijn gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="69757-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD are synchronized.</span></span>

<span data-ttu-id="69757-113">Voordat u configureren en inschakelen van Hallo-service inricht, moet u toodecide welke gebruikers en/of groepen in Azure AD vertegenwoordigen Hallo-gebruikers die toegang moeten hebben tot tooyour DocuSign app.</span><span class="sxs-lookup"><span data-stu-id="69757-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour DocuSign app.</span></span> <span data-ttu-id="69757-114">Als besloten, kunt u deze app-gebruikers tooyour DocuSign toewijzen door hier Hallo-instructies te volgen:</span><span class="sxs-lookup"><span data-stu-id="69757-114">Once decided, you can assign these users tooyour DocuSign app by following hello instructions here:</span></span>

[<span data-ttu-id="69757-115">Toewijzen van een gebruiker of groep tooan enterprise-app</span><span class="sxs-lookup"><span data-stu-id="69757-115">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toodocusign"></a><span data-ttu-id="69757-116">Belangrijke tips voor het toewijzen van gebruikers tooDocuSign</span><span class="sxs-lookup"><span data-stu-id="69757-116">Important tips for assigning users tooDocuSign</span></span>

*   <span data-ttu-id="69757-117">Het is raadzaam om één tooDocuSign tootest Hallo inrichting configuratie door Azure AD-gebruiker is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="69757-117">It is recommended that a single Azure AD user is assigned tooDocuSign tootest hello provisioning configuration.</span></span> <span data-ttu-id="69757-118">Extra gebruikers en/of groepen kunnen later worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="69757-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="69757-119">Wanneer u een gebruiker tooDocuSign toewijst, moet u een geldige gebruikersrol.</span><span class="sxs-lookup"><span data-stu-id="69757-119">When assigning a user tooDocuSign, you must select a valid user role.</span></span> <span data-ttu-id="69757-120">Hallo 'Default toegang' rol werkt niet voor het inrichten.</span><span class="sxs-lookup"><span data-stu-id="69757-120">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="69757-121">Gebruikersinrichting inschakelen</span><span class="sxs-lookup"><span data-stu-id="69757-121">Enable User Provisioning</span></span>

<span data-ttu-id="69757-122">Deze sectie helpt u bij het verbinden van uw Azure AD-tooDocuSign gebruikersaccount inrichten API en Hallo service toocreate inrichting configureren, bijwerken en uitschakelen toegewezen gebruikersaccounts in DocuSign op basis van gebruikers en groepen toewijzen in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="69757-122">This section guides you through connecting your Azure AD tooDocuSign's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in DocuSign based on user and group assignment in Azure AD.</span></span>

> [!Tip]
> <span data-ttu-id="69757-123">U kunt ook tooenabled op basis van SAML eenmalige aanmelding voor DocuSign, in het Hallo-instructies te volgen [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="69757-123">You may also choose tooenabled SAML-based Single Sign-On for DocuSign, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="69757-124">Eenmalige aanmelding kan worden geconfigureerd onafhankelijk van automatische inrichting, hoewel deze twee functies aanvulling van elkaar.</span><span class="sxs-lookup"><span data-stu-id="69757-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-user-account-provisioning"></a><span data-ttu-id="69757-125">tooconfigure account gebruikersaanvragen:</span><span class="sxs-lookup"><span data-stu-id="69757-125">tooconfigure user account provisioning:</span></span>

<span data-ttu-id="69757-126">Hallo-doel van deze sectie is het toooutline hoe tooDocuSign tooenable gebruikers inrichten van Active Directory-gebruiker accounts.</span><span class="sxs-lookup"><span data-stu-id="69757-126">hello objective of this section is toooutline how tooenable user provisioning of Active Directory user accounts tooDocuSign.</span></span>

1. <span data-ttu-id="69757-127">In Hallo [Azure-portal](https://portal.azure.com), bladeren toohello **Azure Active Directory > zakelijke Apps > alle toepassingen** sectie.</span><span class="sxs-lookup"><span data-stu-id="69757-127">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="69757-128">Als u DocuSign al hebt geconfigureerd voor eenmalige aanmelding, zoekt u uw exemplaar van DocuSign met Hallo zoekveld opgegeven.</span><span class="sxs-lookup"><span data-stu-id="69757-128">If you have already configured DocuSign for single sign-on, search for your instance of DocuSign using hello search field.</span></span> <span data-ttu-id="69757-129">Selecteer anders **toevoegen** en zoek naar **DocuSign** in Hallo-toepassingsgalerie.</span><span class="sxs-lookup"><span data-stu-id="69757-129">Otherwise, select **Add** and search for **DocuSign** in hello application gallery.</span></span> <span data-ttu-id="69757-130">Selecteer DocuSign in zoekresultaten hello, en voeg deze tooyour lijst met toepassingen.</span><span class="sxs-lookup"><span data-stu-id="69757-130">Select DocuSign from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="69757-131">Selecteer uw exemplaar van DocuSign en vervolgens Hallo **inrichten** tabblad.</span><span class="sxs-lookup"><span data-stu-id="69757-131">Select your instance of DocuSign, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="69757-132">Set Hallo **modus inrichting** te**automatische**.</span><span class="sxs-lookup"><span data-stu-id="69757-132">Set hello **Provisioning Mode** too**Automatic**.</span></span> 

    ![Inrichting](./media/active-directory-saas-docusign-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="69757-134">Onder Hallo **beheerdersreferenties** sectie, bieden Hallo na configuratie-instellingen:</span><span class="sxs-lookup"><span data-stu-id="69757-134">Under hello **Admin Credentials** section, provide hello following configuration settings:</span></span>
   
    <span data-ttu-id="69757-135">a.</span><span class="sxs-lookup"><span data-stu-id="69757-135">a.</span></span> <span data-ttu-id="69757-136">In Hallo **Beheerdersgebruikersnaam** textbox type een DocuSign accountnaam die heeft Hallo **systeembeheerder** profiel in DocuSign.com toegewezen.</span><span class="sxs-lookup"><span data-stu-id="69757-136">In hello **Admin User Name** textbox, type a DocuSign account name that has hello **System Administrator** profile in DocuSign.com assigned.</span></span>
   
    <span data-ttu-id="69757-137">b.</span><span class="sxs-lookup"><span data-stu-id="69757-137">b.</span></span> <span data-ttu-id="69757-138">In Hallo **beheerderswachtwoord** textbox Hallo een wachtwoord op voor dit account.</span><span class="sxs-lookup"><span data-stu-id="69757-138">In hello **Admin Password** textbox, type hello password for this account.</span></span>

6. <span data-ttu-id="69757-139">Klik in hello Azure-portal, op **testverbinding** tooensure Azure AD tooyour DocuSign app kunt verbinden.</span><span class="sxs-lookup"><span data-stu-id="69757-139">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour DocuSign app.</span></span>

7. <span data-ttu-id="69757-140">In Hallo **e-mailmelding** Voer Hallo e-mailadres van een persoon of groep die moet inrichting fout meldingen ontvangen en Hallo selectievakje.</span><span class="sxs-lookup"><span data-stu-id="69757-140">In hello **Notification Email** field, enter hello email address of a person or group who should receive provisioning error notifications, and check hello checkbox.</span></span>

8. <span data-ttu-id="69757-141">Klik op **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="69757-141">Click **Save.**</span></span>

9. <span data-ttu-id="69757-142">Selecteer onder Hallo toewijzingen sectie, **tooDocuSign synchroniseren Azure Active Directory-gebruikers.**</span><span class="sxs-lookup"><span data-stu-id="69757-142">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooDocuSign.**</span></span>

10. <span data-ttu-id="69757-143">In Hallo **kenmerktoewijzingen** sectie, bekijkt hello gebruikerskenmerken die worden gesynchroniseerd vanuit Azure AD-tooDocuSign.</span><span class="sxs-lookup"><span data-stu-id="69757-143">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooDocuSign.</span></span> <span data-ttu-id="69757-144">kenmerken die zijn geselecteerd als Hallo **overeenkomend** eigenschappen zijn gebruikte toomatch Hallo gebruikersaccounts in DocuSign voor update-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="69757-144">hello attributes selected as **Matching** properties are used toomatch hello user accounts in DocuSign for update operations.</span></span> <span data-ttu-id="69757-145">Selecteer Hallo knop toocommit wijzigingen zijn opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="69757-145">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="69757-146">tooenable Hallo inrichting Azure AD-service voor DocuSign, wijziging Hallo **inrichting Status** te**op** in Hallo Zoekinstellingen</span><span class="sxs-lookup"><span data-stu-id="69757-146">tooenable hello Azure AD provisioning service for DocuSign, change hello **Provisioning Status** too**On** in hello Settings section</span></span>

12. <span data-ttu-id="69757-147">Klik op **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="69757-147">Click **Save.**</span></span>

<span data-ttu-id="69757-148">Hallo initiële synchronisatie van gebruikers en/of groepen die zijn toegewezen tooDocuSign in Hallo gebruikers en groepen sectie begint.</span><span class="sxs-lookup"><span data-stu-id="69757-148">It starts hello initial synchronization of any users and/or groups assigned tooDocuSign in hello Users and Groups section.</span></span> <span data-ttu-id="69757-149">de initiële synchronisatie Hallo duurt langer tooperform dan het volgende wordt gesynchroniseerd, die ongeveer 20 minuten optreden, zolang het Hallo-service wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="69757-149">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="69757-150">U kunt Hallo **synchronisatiedetails** sectie toomonitor uitgevoerd en volgt u koppelingen tooprovisioning activiteitsrapporten, waarin alle bewerkingen die worden uitgevoerd door het Hallo-service op uw app DocuSign inrichting beschrijven.</span><span class="sxs-lookup"><span data-stu-id="69757-150">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your DocuSign app.</span></span>

<span data-ttu-id="69757-151">U kunt nu een testaccount maken.</span><span class="sxs-lookup"><span data-stu-id="69757-151">You can now create a test account.</span></span> <span data-ttu-id="69757-152">Wacht tot up too20 minuten tooverify die Hallo-account is gesynchroniseerd tooDocuSign.</span><span class="sxs-lookup"><span data-stu-id="69757-152">Wait for up too20 minutes tooverify that hello account has been synchronized tooDocuSign.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="69757-153">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="69757-153">Additional resources</span></span>

* [<span data-ttu-id="69757-154">Het beheren van gebruikers account inrichten voor zakelijke Apps</span><span class="sxs-lookup"><span data-stu-id="69757-154">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="69757-155">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="69757-155">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="69757-156">Eenmalige aanmelding configureren</span><span class="sxs-lookup"><span data-stu-id="69757-156">Configure Single Sign-on</span></span>](active-directory-saas-docusign-tutorial.md)