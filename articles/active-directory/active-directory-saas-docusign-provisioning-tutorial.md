---
title: 'Zelfstudie: Azure Active Directory-integratie met DocuSign | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en DocuSign.
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
ms.openlocfilehash: 3b509ffa934949200277ae431761d2accd4a02d6
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-configuring-docusign-for-user-provisioning"></a><span data-ttu-id="97313-103">Zelfstudie: DocuSign configureren voor gebruikers inrichten</span><span class="sxs-lookup"><span data-stu-id="97313-103">Tutorial: Configuring DocuSign for User Provisioning</span></span>

<span data-ttu-id="97313-104">Het doel van deze zelfstudie is zodat u de stappen die u uitvoeren in DocuSign en Azure AD wilt om automatisch in te richten en inrichten van gebruikersaccounts vanuit Azure AD naar DocuSign ongedaan.</span><span class="sxs-lookup"><span data-stu-id="97313-104">The objective of this tutorial is to show you the steps you need to perform in DocuSign and Azure AD to automatically provision and de-provision user accounts from Azure AD to DocuSign.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="97313-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="97313-105">Prerequisites</span></span>

<span data-ttu-id="97313-106">Het scenario in deze zelfstudie wordt ervan uitgegaan dat u al de volgende items hebt:</span><span class="sxs-lookup"><span data-stu-id="97313-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="97313-107">Een Azure Active directory-tenant.</span><span class="sxs-lookup"><span data-stu-id="97313-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="97313-108">Een DocuSign eenmalige aanmelding ingeschakeld abonnement.</span><span class="sxs-lookup"><span data-stu-id="97313-108">A DocuSign single sign-on enabled subscription.</span></span>
*   <span data-ttu-id="97313-109">Een gebruikersaccount in DocuSign met beheerdersmachtigingen Team.</span><span class="sxs-lookup"><span data-stu-id="97313-109">A user account in DocuSign with Team Admin permissions.</span></span>

## <a name="assigning-users-to-docusign"></a><span data-ttu-id="97313-110">Gebruikers toewijzen aan DocuSign</span><span class="sxs-lookup"><span data-stu-id="97313-110">Assigning users to DocuSign</span></span>

<span data-ttu-id="97313-111">Azure Active Directory gebruikt een concept 'toewijzingen' genoemd om te bepalen welke gebruikers krijgen toegang tot geselecteerde apps.</span><span class="sxs-lookup"><span data-stu-id="97313-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="97313-112">In de context van automatische gebruikers account inrichten, worden alleen de gebruikers en groepen die '' tot een toepassing in Azure AD toegewezen zijn gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="97313-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD are synchronized.</span></span>

<span data-ttu-id="97313-113">Voordat u configureren en inschakelen van de inrichting service, moet u om te bepalen welke gebruikers en/of groepen in Azure AD vertegenwoordigen de gebruikers die toegang tot uw app DocuSign nodig hebben.</span><span class="sxs-lookup"><span data-stu-id="97313-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your DocuSign app.</span></span> <span data-ttu-id="97313-114">Als besloten, kunt u deze gebruikers toewijzen aan uw app DocuSign door de volgende instructies te volgen:</span><span class="sxs-lookup"><span data-stu-id="97313-114">Once decided, you can assign these users to your DocuSign app by following the instructions here:</span></span>

[<span data-ttu-id="97313-115">Een gebruiker of groep toewijzen aan een enterprise-app</span><span class="sxs-lookup"><span data-stu-id="97313-115">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-docusign"></a><span data-ttu-id="97313-116">Belangrijke tips voor het toewijzen van gebruikers aan DocuSign</span><span class="sxs-lookup"><span data-stu-id="97313-116">Important tips for assigning users to DocuSign</span></span>

*   <span data-ttu-id="97313-117">Het is raadzaam om één Azure AD-gebruiker is toegewezen aan DocuSign voor het testen van de configuratie van de inrichting.</span><span class="sxs-lookup"><span data-stu-id="97313-117">It is recommended that a single Azure AD user is assigned to DocuSign to test the provisioning configuration.</span></span> <span data-ttu-id="97313-118">Extra gebruikers en/of groepen kunnen later worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="97313-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="97313-119">Wanneer een gebruiker aan DocuSign toewijzen, moet u een geldige gebruikersrol selecteren.</span><span class="sxs-lookup"><span data-stu-id="97313-119">When assigning a user to DocuSign, you must select a valid user role.</span></span> <span data-ttu-id="97313-120">De rol 'Default toegang' werkt niet voor het inrichten.</span><span class="sxs-lookup"><span data-stu-id="97313-120">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="97313-121">Gebruikersinrichting inschakelen</span><span class="sxs-lookup"><span data-stu-id="97313-121">Enable User Provisioning</span></span>

<span data-ttu-id="97313-122">Deze sectie helpt u bij het verbinding maken met uw Azure AD DocuSign van gebruikersaccount inrichten API en configureren van de inrichting service te maken, bijwerken en uitschakelen van toegewezen gebruikersaccounts in DocuSign op basis van gebruikers en groepen toewijzen in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="97313-122">This section guides you through connecting your Azure AD to DocuSign's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in DocuSign based on user and group assignment in Azure AD.</span></span>

> [!Tip]
> <span data-ttu-id="97313-123">U kunt ook op basis van SAML eenmalige aanmelding is ingeschakeld voor DocuSign, vindt u de instructies te volgen in [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="97313-123">You may also choose to enabled SAML-based Single Sign-On for DocuSign, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="97313-124">Eenmalige aanmelding kan worden geconfigureerd onafhankelijk van automatische inrichting, hoewel deze twee functies aanvulling van elkaar.</span><span class="sxs-lookup"><span data-stu-id="97313-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-user-account-provisioning"></a><span data-ttu-id="97313-125">Configureren voor het inrichten van het account:</span><span class="sxs-lookup"><span data-stu-id="97313-125">To configure user account provisioning:</span></span>

<span data-ttu-id="97313-126">Het doel van deze sectie is het inschakelen van de gebruiker het inrichten van Active Directory-gebruikersaccounts met DocuSign overzicht.</span><span class="sxs-lookup"><span data-stu-id="97313-126">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to DocuSign.</span></span>

1. <span data-ttu-id="97313-127">In de [Azure-portal](https://portal.azure.com), blader naar de **Azure Active Directory > zakelijke Apps > alle toepassingen** sectie.</span><span class="sxs-lookup"><span data-stu-id="97313-127">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="97313-128">Als u al DocuSign voor eenmalige aanmelding hebt geconfigureerd, kunt u zoeken naar uw exemplaar van DocuSign met behulp van het zoekveld.</span><span class="sxs-lookup"><span data-stu-id="97313-128">If you have already configured DocuSign for single sign-on, search for your instance of DocuSign using the search field.</span></span> <span data-ttu-id="97313-129">Selecteer anders **toevoegen** en zoek naar **DocuSign** in de galerie met toepassingen.</span><span class="sxs-lookup"><span data-stu-id="97313-129">Otherwise, select **Add** and search for **DocuSign** in the application gallery.</span></span> <span data-ttu-id="97313-130">DocuSign selecteert in de zoekresultaten en toe te voegen aan uw lijst met toepassingen.</span><span class="sxs-lookup"><span data-stu-id="97313-130">Select DocuSign from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="97313-131">Selecteer uw exemplaar van DocuSign en selecteer vervolgens de **inrichten** tabblad.</span><span class="sxs-lookup"><span data-stu-id="97313-131">Select your instance of DocuSign, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="97313-132">Stel de **Inrichtingsmodus** naar **automatische**.</span><span class="sxs-lookup"><span data-stu-id="97313-132">Set the **Provisioning Mode** to **Automatic**.</span></span> 

    ![Inrichting](./media/active-directory-saas-docusign-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="97313-134">Onder de **beheerdersreferenties** sectie, bieden de volgende configuratie-instellingen:</span><span class="sxs-lookup"><span data-stu-id="97313-134">Under the **Admin Credentials** section, provide the following configuration settings:</span></span>
   
    <span data-ttu-id="97313-135">a.</span><span class="sxs-lookup"><span data-stu-id="97313-135">a.</span></span> <span data-ttu-id="97313-136">In de **Beheerdersgebruikersnaam** textbox type een DocuSign accountnaam met de **systeembeheerder** profiel in DocuSign.com toegewezen.</span><span class="sxs-lookup"><span data-stu-id="97313-136">In the **Admin User Name** textbox, type a DocuSign account name that has the **System Administrator** profile in DocuSign.com assigned.</span></span>
   
    <span data-ttu-id="97313-137">b.</span><span class="sxs-lookup"><span data-stu-id="97313-137">b.</span></span> <span data-ttu-id="97313-138">In de **beheerderswachtwoord** textbox, typt u het wachtwoord voor dit account.</span><span class="sxs-lookup"><span data-stu-id="97313-138">In the **Admin Password** textbox, type the password for this account.</span></span>

6. <span data-ttu-id="97313-139">Klik in de Azure-portal op **testverbinding** om te controleren of Azure AD, kan verbinding maken met uw app DocuSign.</span><span class="sxs-lookup"><span data-stu-id="97313-139">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your DocuSign app.</span></span>

7. <span data-ttu-id="97313-140">In de **e-mailmelding** en voer het e-mailadres van een persoon of groep die u moet inrichting fout meldingen ontvangen en schakel het selectievakje in.</span><span class="sxs-lookup"><span data-stu-id="97313-140">In the **Notification Email** field, enter the email address of a person or group who should receive provisioning error notifications, and check the checkbox.</span></span>

8. <span data-ttu-id="97313-141">Klik op **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="97313-141">Click **Save.**</span></span>

9. <span data-ttu-id="97313-142">Selecteer onder de sectie toewijzingen **synchroniseren Azure Active Directory-gebruikers DocuSign.**</span><span class="sxs-lookup"><span data-stu-id="97313-142">Under the Mappings section, select **Synchronize Azure Active Directory Users to DocuSign.**</span></span>

10. <span data-ttu-id="97313-143">In de **kenmerktoewijzingen** sectie, moet u de kenmerken van de gebruiker is gesynchroniseerd vanuit Azure AD DocuSign controleren.</span><span class="sxs-lookup"><span data-stu-id="97313-143">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to DocuSign.</span></span> <span data-ttu-id="97313-144">De kenmerken die zijn geselecteerd als **overeenkomend** eigenschappen overeenkomen met de gebruikersaccounts in DocuSign voor update-bewerkingen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="97313-144">The attributes selected as **Matching** properties are used to match the user accounts in DocuSign for update operations.</span></span> <span data-ttu-id="97313-145">Selecteer de knop Opslaan eventuele wijzigingen doorvoeren.</span><span class="sxs-lookup"><span data-stu-id="97313-145">Select the Save button to commit any changes.</span></span>

11. <span data-ttu-id="97313-146">Om de Azure AD-service voor DocuSign inricht, wijzigen de **inrichting Status** naar **op** in de sectie instellingen</span><span class="sxs-lookup"><span data-stu-id="97313-146">To enable the Azure AD provisioning service for DocuSign, change the **Provisioning Status** to **On** in the Settings section</span></span>

12. <span data-ttu-id="97313-147">Klik op **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="97313-147">Click **Save.**</span></span>

<span data-ttu-id="97313-148">De initiële synchronisatie van gebruikers en/of groepen die zijn toegewezen aan DocuSign in de sectie gebruikers en groepen wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="97313-148">It starts the initial synchronization of any users and/or groups assigned to DocuSign in the Users and Groups section.</span></span> <span data-ttu-id="97313-149">De eerste synchronisatie langer duren om uit te voeren dan het volgende wordt gesynchroniseerd, die ongeveer 20 minuten optreden als de service wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="97313-149">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="97313-150">U kunt de **synchronisatiedetails** sectie voortgang en volg de koppelingen voor het inrichten van de activiteitsrapporten, waarin alle acties die worden uitgevoerd door de inrichting service op uw app DocuSign beschrijven.</span><span class="sxs-lookup"><span data-stu-id="97313-150">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your DocuSign app.</span></span>

<span data-ttu-id="97313-151">U kunt nu een testaccount maken.</span><span class="sxs-lookup"><span data-stu-id="97313-151">You can now create a test account.</span></span> <span data-ttu-id="97313-152">Wacht 20 minuten duren om te verifiëren dat het account is gesynchroniseerd voor DocuSign.</span><span class="sxs-lookup"><span data-stu-id="97313-152">Wait for up to 20 minutes to verify that the account has been synchronized to DocuSign.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="97313-153">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="97313-153">Additional resources</span></span>

* [<span data-ttu-id="97313-154">Het beheren van gebruikers account inrichten voor zakelijke Apps</span><span class="sxs-lookup"><span data-stu-id="97313-154">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="97313-155">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="97313-155">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="97313-156">Eenmalige aanmelding configureren</span><span class="sxs-lookup"><span data-stu-id="97313-156">Configure Single Sign-on</span></span>](active-directory-saas-docusign-tutorial.md)