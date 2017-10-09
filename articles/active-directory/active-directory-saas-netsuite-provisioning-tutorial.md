---
title: 'Zelfstudie: Azure Active Directory-integratie met Netsuite | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Netsuite.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8a6d3994-ee33-4a6f-b0a2-9d0389467f16
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 5bb2989c1296b9f2abc9e8c84855731adc484aab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-netsuite-for-automatic-user-provisioning"></a><span data-ttu-id="58e41-103">Zelfstudie: Netsuite configureren voor het automatisch gebruikers inrichten</span><span class="sxs-lookup"><span data-stu-id="58e41-103">Tutorial: Configuring Netsuite for Automatic User Provisioning</span></span>

<span data-ttu-id="58e41-104">Hallo-doel van deze zelfstudie is tooshow u stappen die u moet tooperform in Netsuite en Azure AD tooautomatically leveren en intrekken gebruikersaccounts vanuit Azure AD tooNetsuite Hallo.</span><span class="sxs-lookup"><span data-stu-id="58e41-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Netsuite and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooNetsuite.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="58e41-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="58e41-105">Prerequisites</span></span>

<span data-ttu-id="58e41-106">Hallo scenario beschreven in deze zelfstudie wordt ervan uitgegaan dat u al hebt Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="58e41-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="58e41-107">Een Azure Active directory-tenant.</span><span class="sxs-lookup"><span data-stu-id="58e41-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="58e41-108">Een Netsuite eenmalige aanmelding ingeschakeld abonnement.</span><span class="sxs-lookup"><span data-stu-id="58e41-108">A Netsuite single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="58e41-109">Een gebruikersaccount in Netsuite met beheerdersmachtigingen Team.</span><span class="sxs-lookup"><span data-stu-id="58e41-109">A user account in Netsuite with Team Admin permissions.</span></span>

## <a name="assigning-users-toonetsuite"></a><span data-ttu-id="58e41-110">Gebruikers tooNetsuite toewijzen</span><span class="sxs-lookup"><span data-stu-id="58e41-110">Assigning users tooNetsuite</span></span>

<span data-ttu-id="58e41-111">Azure Active Directory gebruikt een concept 'toewijzingen' toodetermine welke gebruikers toegang tooselected apps krijgen genoemd.</span><span class="sxs-lookup"><span data-stu-id="58e41-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="58e41-112">In de context van de Hallo van automatische gebruikers account inrichten, worden alleen Hallo-gebruikers en groepen die '' tooan toepassing in Azure AD toegewezen zijn gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="58e41-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD are synchronized.</span></span>

<span data-ttu-id="58e41-113">Voordat u configureren en inschakelen van Hallo-service inricht, moet u toodecide welke gebruikers en/of groepen in Azure AD vertegenwoordigen Hallo-gebruikers die toegang moeten hebben tot tooyour Netsuite app.</span><span class="sxs-lookup"><span data-stu-id="58e41-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Netsuite app.</span></span> <span data-ttu-id="58e41-114">Als besloten, kunt u deze app-gebruikers tooyour Netsuite toewijzen door hier Hallo-instructies te volgen:</span><span class="sxs-lookup"><span data-stu-id="58e41-114">Once decided, you can assign these users tooyour Netsuite app by following hello instructions here:</span></span>

[<span data-ttu-id="58e41-115">Toewijzen van een gebruiker of groep tooan enterprise-app</span><span class="sxs-lookup"><span data-stu-id="58e41-115">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toonetsuite"></a><span data-ttu-id="58e41-116">Belangrijke tips voor het toewijzen van gebruikers tooNetsuite</span><span class="sxs-lookup"><span data-stu-id="58e41-116">Important tips for assigning users tooNetsuite</span></span>

*   <span data-ttu-id="58e41-117">Het is raadzaam om één tooNetsuite tootest Hallo inrichting configuratie door Azure AD-gebruiker is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="58e41-117">It is recommended that a single Azure AD user is assigned tooNetsuite tootest hello provisioning configuration.</span></span> <span data-ttu-id="58e41-118">Extra gebruikers en/of groepen kunnen later worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="58e41-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="58e41-119">Wanneer u een gebruiker tooNetsuite toewijst, moet u een geldige gebruikersrol.</span><span class="sxs-lookup"><span data-stu-id="58e41-119">When assigning a user tooNetsuite, you must select a valid user role.</span></span> <span data-ttu-id="58e41-120">Hallo 'Default toegang' rol werkt niet voor het inrichten.</span><span class="sxs-lookup"><span data-stu-id="58e41-120">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="58e41-121">Gebruikersinrichting inschakelen</span><span class="sxs-lookup"><span data-stu-id="58e41-121">Enable User Provisioning</span></span>

<span data-ttu-id="58e41-122">Deze sectie helpt u bij het verbinden van uw Azure AD-tooNetsuite gebruikersaccount inrichten API en Hallo service toocreate inrichting configureren, bijwerken en uitschakelen toegewezen gebruikersaccounts in Netsuite op basis van gebruikers en groepen toewijzen in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="58e41-122">This section guides you through connecting your Azure AD tooNetsuite's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Netsuite based on user and group assignment in Azure AD.</span></span>

> [!TIP] 
> <span data-ttu-id="58e41-123">U kunt ook tooenabled op basis van SAML eenmalige aanmelding voor Netsuite, in het Hallo-instructies te volgen [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="58e41-123">You may also choose tooenabled SAML-based Single Sign-On for Netsuite, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="58e41-124">Eenmalige aanmelding kan worden geconfigureerd onafhankelijk van automatische inrichting, hoewel deze twee functies aanvulling van elkaar.</span><span class="sxs-lookup"><span data-stu-id="58e41-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-user-account-provisioning"></a><span data-ttu-id="58e41-125">tooconfigure account gebruikersaanvragen:</span><span class="sxs-lookup"><span data-stu-id="58e41-125">tooconfigure user account provisioning:</span></span>

<span data-ttu-id="58e41-126">Hallo-doel van deze sectie is het toooutline hoe tooNetsuite tooenable gebruikers inrichten van Active Directory-gebruiker accounts.</span><span class="sxs-lookup"><span data-stu-id="58e41-126">hello objective of this section is toooutline how tooenable user provisioning of Active Directory user accounts tooNetsuite.</span></span>

1. <span data-ttu-id="58e41-127">In Hallo [Azure-portal](https://portal.azure.com), bladeren toohello **Azure Active Directory > zakelijke Apps > alle toepassingen** sectie.</span><span class="sxs-lookup"><span data-stu-id="58e41-127">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="58e41-128">Als u Netsuite al hebt geconfigureerd voor eenmalige aanmelding, zoekt u uw exemplaar van Netsuite met Hallo zoekveld opgegeven.</span><span class="sxs-lookup"><span data-stu-id="58e41-128">If you have already configured Netsuite for single sign-on, search for your instance of Netsuite using hello search field.</span></span> <span data-ttu-id="58e41-129">Selecteer anders **toevoegen** en zoek naar **Netsuite** in Hallo-toepassingsgalerie.</span><span class="sxs-lookup"><span data-stu-id="58e41-129">Otherwise, select **Add** and search for **Netsuite** in hello application gallery.</span></span> <span data-ttu-id="58e41-130">Selecteer Netsuite in zoekresultaten hello, en voeg deze tooyour lijst met toepassingen.</span><span class="sxs-lookup"><span data-stu-id="58e41-130">Select Netsuite from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="58e41-131">Selecteer uw exemplaar van Netsuite en vervolgens Hallo **inrichten** tabblad.</span><span class="sxs-lookup"><span data-stu-id="58e41-131">Select your instance of Netsuite, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="58e41-132">Set Hallo **modus inrichting** te**automatische**.</span><span class="sxs-lookup"><span data-stu-id="58e41-132">Set hello **Provisioning Mode** too**Automatic**.</span></span> 

    ![Inrichting](./media/active-directory-saas-netsuite-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="58e41-134">Onder Hallo **beheerdersreferenties** sectie, bieden Hallo na configuratie-instellingen:</span><span class="sxs-lookup"><span data-stu-id="58e41-134">Under hello **Admin Credentials** section, provide hello following configuration settings:</span></span>
   
    <span data-ttu-id="58e41-135">a.</span><span class="sxs-lookup"><span data-stu-id="58e41-135">a.</span></span> <span data-ttu-id="58e41-136">In Hallo **Beheerdersgebruikersnaam** textbox type een Netsuite accountnaam die heeft Hallo **systeembeheerder** profiel in Netsuite.com toegewezen.</span><span class="sxs-lookup"><span data-stu-id="58e41-136">In hello **Admin User Name** textbox, type a Netsuite account name that has hello **System Administrator** profile in Netsuite.com assigned.</span></span>
   
    <span data-ttu-id="58e41-137">b.</span><span class="sxs-lookup"><span data-stu-id="58e41-137">b.</span></span> <span data-ttu-id="58e41-138">In Hallo **beheerderswachtwoord** textbox Hallo een wachtwoord op voor dit account.</span><span class="sxs-lookup"><span data-stu-id="58e41-138">In hello **Admin Password** textbox, type hello password for this account.</span></span>
      
6. <span data-ttu-id="58e41-139">Klik in hello Azure-portal, op **testverbinding** tooensure Azure AD tooyour Netsuite app kunt verbinden.</span><span class="sxs-lookup"><span data-stu-id="58e41-139">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Netsuite app.</span></span>

7. <span data-ttu-id="58e41-140">In Hallo **e-mailmelding** Voer Hallo e-mailadres van een persoon of groep die moet inrichting fout meldingen ontvangen en Hallo selectievakje.</span><span class="sxs-lookup"><span data-stu-id="58e41-140">In hello **Notification Email** field, enter hello email address of a person or group who should receive provisioning error notifications, and check hello checkbox.</span></span>

8. <span data-ttu-id="58e41-141">Klik op **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="58e41-141">Click **Save.**</span></span>

9. <span data-ttu-id="58e41-142">Selecteer onder Hallo toewijzingen sectie, **tooNetsuite synchroniseren Azure Active Directory-gebruikers.**</span><span class="sxs-lookup"><span data-stu-id="58e41-142">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooNetsuite.**</span></span>

10. <span data-ttu-id="58e41-143">In Hallo **kenmerktoewijzingen** sectie, bekijkt hello gebruikerskenmerken die worden gesynchroniseerd vanuit Azure AD-tooNetsuite.</span><span class="sxs-lookup"><span data-stu-id="58e41-143">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooNetsuite.</span></span> <span data-ttu-id="58e41-144">Let op: kenmerken die zijn geselecteerd als Hallo **overeenkomend** eigenschappen zijn gebruikte toomatch Hallo gebruikersaccounts in Netsuite voor update-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="58e41-144">Note that hello attributes selected as **Matching** properties are used toomatch hello user accounts in Netsuite for update operations.</span></span> <span data-ttu-id="58e41-145">Selecteer Hallo knop toocommit wijzigingen zijn opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="58e41-145">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="58e41-146">tooenable Hallo inrichting Azure AD-service voor Netsuite, wijziging Hallo **inrichting Status** te**op** in Hallo Zoekinstellingen</span><span class="sxs-lookup"><span data-stu-id="58e41-146">tooenable hello Azure AD provisioning service for Netsuite, change hello **Provisioning Status** too**On** in hello Settings section</span></span>

12. <span data-ttu-id="58e41-147">Klik op **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="58e41-147">Click **Save.**</span></span>

<span data-ttu-id="58e41-148">Hallo initiële synchronisatie van gebruikers en/of groepen die zijn toegewezen tooNetsuite in Hallo gebruikers en groepen sectie begint.</span><span class="sxs-lookup"><span data-stu-id="58e41-148">It starts hello initial synchronization of any users and/or groups assigned tooNetsuite in hello Users and Groups section.</span></span> <span data-ttu-id="58e41-149">Houd er rekening mee dat de initiële synchronisatie Hallo langer tooperform dan het volgende wordt gesynchroniseerd, die ongeveer 20 minuten optreden duurt, zolang het Hallo-service wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="58e41-149">Note that hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="58e41-150">U kunt Hallo **synchronisatiedetails** sectie toomonitor uitgevoerd en volgt u koppelingen tooprovisioning activiteitsrapporten, waarin alle bewerkingen die worden uitgevoerd door het Hallo-service op uw app Netsuite inrichting beschrijven.</span><span class="sxs-lookup"><span data-stu-id="58e41-150">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Netsuite app.</span></span>

<span data-ttu-id="58e41-151">U kunt nu een testaccount maken.</span><span class="sxs-lookup"><span data-stu-id="58e41-151">You can now create a test account.</span></span> <span data-ttu-id="58e41-152">Wacht tot up too20 minuten tooverify die Hallo-account is gesynchroniseerd tooNetsuite.</span><span class="sxs-lookup"><span data-stu-id="58e41-152">Wait for up too20 minutes tooverify that hello account has been synchronized tooNetsuite.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="58e41-153">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="58e41-153">Additional resources</span></span>

* [<span data-ttu-id="58e41-154">Het beheren van gebruikers account inrichten voor zakelijke Apps</span><span class="sxs-lookup"><span data-stu-id="58e41-154">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="58e41-155">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="58e41-155">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="58e41-156">Eenmalige aanmelding configureren</span><span class="sxs-lookup"><span data-stu-id="58e41-156">Configure Single Sign-on</span></span>](active-directory-saas-netsuite-tutorial.md)