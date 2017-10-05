---
title: 'Zelfstudie: Slack configureren voor het automatisch gebruikers inrichten met Azure Active Directory | Microsoft Docs'
description: Informatie over het configureren van Azure Active Directory automatisch leveren en intrekken accounts van gebruikers met Slack.
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: sakula
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: asmalser-msft
ms.reviewer: asmalser
ms.openlocfilehash: 3cb49a4abb26c34a938c963c4cf326b5ccd490de
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-configuring-slack-for-automatic-user-provisioning"></a><span data-ttu-id="f3a15-103">Zelfstudie: Slack configureren voor het automatisch gebruikers inrichten</span><span class="sxs-lookup"><span data-stu-id="f3a15-103">Tutorial: Configuring Slack for Automatic User Provisioning</span></span>


<span data-ttu-id="f3a15-104">Het doel van deze zelfstudie is zodat u de stappen die u wilt uitvoeren in Slack en Azure AD aan automatisch leveren en intrekken gebruikersaccounts vanuit Azure AD met Slack.</span><span class="sxs-lookup"><span data-stu-id="f3a15-104">The objective of this tutorial is to show you the steps you need to perform in Slack and Azure AD to automatically provision and de-provision user accounts from Azure AD to Slack.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="f3a15-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f3a15-105">Prerequisites</span></span>

<span data-ttu-id="f3a15-106">Het scenario in deze zelfstudie wordt ervan uitgegaan dat u al de volgende items hebt:</span><span class="sxs-lookup"><span data-stu-id="f3a15-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="f3a15-107">Een Azure Active Active directory-tenant</span><span class="sxs-lookup"><span data-stu-id="f3a15-107">An Azure Active Active directory tenant</span></span>
*   <span data-ttu-id="f3a15-108">Een Slack-tenant met de [Plus plan](https://aadsyncfabric.slack.com/pricing) of beter ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="f3a15-108">A Slack tenant with the [Plus plan](https://aadsyncfabric.slack.com/pricing) or better enabled</span></span> 
*   <span data-ttu-id="f3a15-109">Een gebruikersaccount in Slack met beheerdersmachtigingen Team</span><span class="sxs-lookup"><span data-stu-id="f3a15-109">A user account in Slack with Team Admin permissions</span></span> 

<span data-ttu-id="f3a15-110">Opmerking: De Azure AD integratie inrichting is afhankelijk van de [Slack SCIM API](https://api.slack.com/scim) die voor toegestane teams beschikbaar is op het plusteken plannen of sneller.</span><span class="sxs-lookup"><span data-stu-id="f3a15-110">Note: The Azure AD provisioning integration relies on the [Slack SCIM API](https://api.slack.com/scim) which is available to Slack teams on the Plus plan or better.</span></span>

## <a name="assigning-users-to-slack"></a><span data-ttu-id="f3a15-111">Toewijzen van gebruikers met Slack</span><span class="sxs-lookup"><span data-stu-id="f3a15-111">Assigning users to Slack</span></span>

<span data-ttu-id="f3a15-112">Azure Active Directory gebruikt een concept 'toewijzingen' genoemd om te bepalen welke gebruikers krijgen toegang tot geselecteerde apps.</span><span class="sxs-lookup"><span data-stu-id="f3a15-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="f3a15-113">In de context van automatische gebruikers account inrichten, worden alleen de gebruikers en groepen die '' tot een toepassing in Azure AD toegewezen zijn gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="f3a15-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD will be synchronized.</span></span> 

<span data-ttu-id="f3a15-114">Voordat u configureren en inschakelen van de inrichting service, moet u bepalen welke gebruikers en/of groepen in Azure AD de gebruikers die toegang nodig tot de toegestane app vertegenwoordigen.</span><span class="sxs-lookup"><span data-stu-id="f3a15-114">Before configuring and enabling the provisioning service, you will need to decide what users and/or groups in Azure AD represent the users who need access to your Slack app.</span></span> <span data-ttu-id="f3a15-115">Als besloten, kunt u deze gebruikers toewijzen aan uw toegestane app door de volgende instructies te volgen:</span><span class="sxs-lookup"><span data-stu-id="f3a15-115">Once decided, you can assign these users to your Slack app by following the instructions here:</span></span>

[<span data-ttu-id="f3a15-116">Een gebruiker of groep toewijzen aan een enterprise-app</span><span class="sxs-lookup"><span data-stu-id="f3a15-116">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-to-slack"></a><span data-ttu-id="f3a15-117">Belangrijke tips voor het toewijzen van gebruikers met Slack</span><span class="sxs-lookup"><span data-stu-id="f3a15-117">Important tips for assigning users to Slack</span></span>

*   <span data-ttu-id="f3a15-118">Het is raadzaam om één Azure AD-gebruiker worden toegewezen aan de vertraging voor het testen van de configuratie van de inrichting.</span><span class="sxs-lookup"><span data-stu-id="f3a15-118">It is recommended that a single Azure AD user be assigned to Slack to test the provisioning configuration.</span></span> <span data-ttu-id="f3a15-119">Extra gebruikers en/of groepen kunnen later worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="f3a15-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="f3a15-120">Bij het toewijzen van een gebruiker met Slack, moet u de **gebruiker** of 'Groep'-rol in het dialoogvenster toewijzing.</span><span class="sxs-lookup"><span data-stu-id="f3a15-120">When assigning a user to Slack, you must select the **User** or "Group" role in the assignment dialog.</span></span> <span data-ttu-id="f3a15-121">De rol 'Default toegang' werkt niet voor het inrichten.</span><span class="sxs-lookup"><span data-stu-id="f3a15-121">The "Default Access" role does not work for provisioning.</span></span>


## <a name="configuring-user-provisioning-to-slack"></a><span data-ttu-id="f3a15-122">Gebruikers inrichten met Slack configureren</span><span class="sxs-lookup"><span data-stu-id="f3a15-122">Configuring user provisioning to Slack</span></span> 

<span data-ttu-id="f3a15-123">Deze sectie helpt u bij uw Azure AD verbinden met Slack van gebruikersaccount inrichten API en de inrichting service maken, bijwerken en uitschakelen configureren toegewezen gebruikersaccounts in Slack op basis van gebruiker en groepstoewijzing in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f3a15-123">This section guides you through connecting your Azure AD to Slack's user account provisioning API, and configuring the provisioning service to create, update and disable assigned user accounts in Slack based on user and group assignment in Azure AD.</span></span>

<span data-ttu-id="f3a15-124">**Tip:** u kunt ook ingeschakeld op basis van SAML eenmalige aanmelding voor de vertraging, volgt de instructies in (Azure-portal) [https://portal.azure.com].</span><span class="sxs-lookup"><span data-stu-id="f3a15-124">**Tip:** You may also choose to enabled SAML-based Single Sign-On for Slack, following the instructions provided in (Azure portal)[https://portal.azure.com].</span></span> <span data-ttu-id="f3a15-125">Eenmalige aanmelding kan worden geconfigureerd onafhankelijk van automatische inrichting, hoewel deze twee functies aanvulling van elkaar.</span><span class="sxs-lookup"><span data-stu-id="f3a15-125">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="to-configure-automatic-user-account-provisioning-to-slack-in-azure-ad"></a><span data-ttu-id="f3a15-126">Voor het configureren van automatische gebruikers account inrichten met Slack in Azure AD:</span><span class="sxs-lookup"><span data-stu-id="f3a15-126">To configure automatic user account provisioning to Slack in Azure AD:</span></span>


1)  <span data-ttu-id="f3a15-127">In de [Azure-portal](https://portal.azure.com), blader naar de **Azure Active Directory > zakelijke Apps > alle toepassingen** sectie.</span><span class="sxs-lookup"><span data-stu-id="f3a15-127">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2) <span data-ttu-id="f3a15-128">Als u al vertraging voor eenmalige aanmelding hebt geconfigureerd, kunt u zoeken naar uw exemplaar van het zoekveld met Slack.</span><span class="sxs-lookup"><span data-stu-id="f3a15-128">If you have already configured Slack for single sign-on, search for your instance of Slack using the search field.</span></span> <span data-ttu-id="f3a15-129">Selecteer anders **toevoegen** en zoek naar **Slack** in de galerie met toepassingen.</span><span class="sxs-lookup"><span data-stu-id="f3a15-129">Otherwise, select **Add** and search for **Slack** in the application gallery.</span></span> <span data-ttu-id="f3a15-130">Vertraging in de zoekresultaten te selecteren en toe te voegen aan uw lijst met toepassingen.</span><span class="sxs-lookup"><span data-stu-id="f3a15-130">Select Slack from the search results, and add it to your list of applications.</span></span>

3)  <span data-ttu-id="f3a15-131">Selecteer uw exemplaar van Slack en selecteer vervolgens de **inrichten** tabblad.</span><span class="sxs-lookup"><span data-stu-id="f3a15-131">Select your instance of Slack, then select the **Provisioning** tab.</span></span>

4)  <span data-ttu-id="f3a15-132">Stel de **Inrichtingsmodus** naar **automatische**.</span><span class="sxs-lookup"><span data-stu-id="f3a15-132">Set the **Provisioning Mode** to **Automatic**.</span></span>

![Vertraging inrichten](./media/active-directory-saas-slack-provisioning-tutorial/Slack1.PNG)

5)  <span data-ttu-id="f3a15-134">Onder de **beheerdersreferenties** sectie, klikt u op **autoriseren**.</span><span class="sxs-lookup"><span data-stu-id="f3a15-134">Under the **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="f3a15-135">Hiermee opent u een dialoogvenster toegestane autorisatie in een nieuw browservenster.</span><span class="sxs-lookup"><span data-stu-id="f3a15-135">This opens a Slack authorization dialog in a new browser window.</span></span> 

6) <span data-ttu-id="f3a15-136">Aanmelden bij uw Team beheerdersaccount met Slack in het nieuwe venster.</span><span class="sxs-lookup"><span data-stu-id="f3a15-136">In the new window, sign into Slack using your Team Admin account.</span></span> <span data-ttu-id="f3a15-137">Selecteer in het dialoogvenster resulterende autorisatie het toegestane team dat u inschakelen wilt voor inrichting, en selecteer vervolgens **autoriseren**.</span><span class="sxs-lookup"><span data-stu-id="f3a15-137">in the resulting authorization dialog, select the Slack team that you want to enable provisioning for, and then select **Authorize**.</span></span> <span data-ttu-id="f3a15-138">Als voltooid, terug naar de Azure-portal om het inrichtingsproces configuratie te voltooien.</span><span class="sxs-lookup"><span data-stu-id="f3a15-138">Once completed, return to the Azure portal to complete the provisioning configuration.</span></span>

![Dialoogvenster autorisatie](./media/active-directory-saas-slack-provisioning-tutorial/Slack3.PNG)

7) <span data-ttu-id="f3a15-140">Klik in de Azure-portal op **testverbinding** om te controleren of Azure AD, kan verbinding maken met uw toegestane app.</span><span class="sxs-lookup"><span data-stu-id="f3a15-140">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Slack app.</span></span> <span data-ttu-id="f3a15-141">Als de verbinding is mislukt, controleert dat uw toegestane account Team beheerder machtigingen heeft en probeer het opnieuw de stap 'Autoriseren'.</span><span class="sxs-lookup"><span data-stu-id="f3a15-141">If the connection fails, ensure your Slack account has Team Admin permissions and try the "Authorize" step again.</span></span>

8) <span data-ttu-id="f3a15-142">Voer het e-mailadres van een persoon of groep die in inrichting fout meldingen moet ontvangen de **e-mailmelding** veld en schakel het selectievakje hieronder in.</span><span class="sxs-lookup"><span data-stu-id="f3a15-142">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox below.</span></span>

9) <span data-ttu-id="f3a15-143">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="f3a15-143">Click **Save**.</span></span> 

10) <span data-ttu-id="f3a15-144">Selecteer onder de sectie toewijzingen **synchroniseren Azure Active Directory-gebruikers met Slack**.</span><span class="sxs-lookup"><span data-stu-id="f3a15-144">Under the Mappings section, select **Synchronize Azure Active Directory Users to Slack**.</span></span>

11) <span data-ttu-id="f3a15-145">In de **kenmerktoewijzingen** sectie, controleert u de kenmerken van de gebruiker die met Slack van Azure AD worden gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="f3a15-145">In the **Attribute Mappings** section, review the user attributes that will be synchronized from Azure AD to Slack.</span></span> <span data-ttu-id="f3a15-146">Let op de kenmerken die zijn geselecteerd als **overeenkomend** eigenschappen overeenkomen met de gebruikersaccounts in Slack voor update-bewerkingen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f3a15-146">Note that the attributes selected as **Matching** properties will be used to match the user accounts in Slack for update operations.</span></span> <span data-ttu-id="f3a15-147">Selecteer de knop Opslaan eventuele wijzigingen doorvoeren.</span><span class="sxs-lookup"><span data-stu-id="f3a15-147">Select the Save button to commit any changes.</span></span>

12) <span data-ttu-id="f3a15-148">Om de Azure AD-service voor Slack inricht, wijzigen de **inrichting Status** naar **op** in de **instellingen** sectie</span><span class="sxs-lookup"><span data-stu-id="f3a15-148">To enable the Azure AD provisioning service for Slack, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

13) <span data-ttu-id="f3a15-149">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="f3a15-149">Click **Save**.</span></span> 

<span data-ttu-id="f3a15-150">Hiermee start u de initiële synchronisatie van gebruikers en/of groepen die zijn toegewezen aan de vertraging in de sectie gebruikers en groepen.</span><span class="sxs-lookup"><span data-stu-id="f3a15-150">This will start the initial synchronization of any users and/or groups assigned to Slack in the Users and Groups section.</span></span> <span data-ttu-id="f3a15-151">Houd er rekening mee dat de eerste synchronisatie langer dan het volgende wordt gesynchroniseerd, die ongeveer elke 10 minuten optreden duurt als de service wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f3a15-151">Note that the initial sync will take longer to perform than subsequent syncs, which occur approximately every 10 minutes as long as the service is running.</span></span> <span data-ttu-id="f3a15-152">U kunt de **synchronisatiedetails** sectie voortgang en volg de koppelingen voor het inrichten van de activiteitsrapporten, waarin alle acties die worden uitgevoerd door de inrichting service op uw toegestane app te beschrijven.</span><span class="sxs-lookup"><span data-stu-id="f3a15-152">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Slack app.</span></span>

## <a name="optional-configuring-group-object-provisioning-to-slack"></a><span data-ttu-id="f3a15-153">[Optioneel] Groep object inrichten met Slack configureren</span><span class="sxs-lookup"><span data-stu-id="f3a15-153">[Optional] Configuring group object provisioning to Slack</span></span> 

<span data-ttu-id="f3a15-154">Desgewenst kunt u de inrichting van groepsobjecten van Azure AD met Slack inschakelen.</span><span class="sxs-lookup"><span data-stu-id="f3a15-154">Optionally, you can enable the provisioning of group objects from Azure AD to Slack.</span></span> <span data-ttu-id="f3a15-155">Dit is anders dan 'groepen gebruikers toe te wijzen', in dat de werkelijke groep object naast de leden ervan gerepliceerd van Azure AD met Slack.</span><span class="sxs-lookup"><span data-stu-id="f3a15-155">This is different from "assigning groups of users", in that the actual group object in addition to its members will be replicated from Azure AD to Slack.</span></span> <span data-ttu-id="f3a15-156">Als u een groep met de naam 'Mijn groep' in Azure AD hebt, wordt bijvoorbeeld een identitical groep met de naam 'Mijn groep' gemaakt binnen de toegestane vertraging.</span><span class="sxs-lookup"><span data-stu-id="f3a15-156">For example, if you have a group named "My Group" in Azure AD, an identitical group named "My Group" will be created inside Slack.</span></span>

### <a name="to-enable-provisioning-of-group-objects"></a><span data-ttu-id="f3a15-157">Inschakelen voor het inrichten van groepsobjecten:</span><span class="sxs-lookup"><span data-stu-id="f3a15-157">To enable provisioning of group objects:</span></span>

1) <span data-ttu-id="f3a15-158">Selecteer onder de sectie toewijzingen **synchroniseren Azure Active Directory-groepen met Slack**.</span><span class="sxs-lookup"><span data-stu-id="f3a15-158">Under the Mappings section, select **Synchronize Azure Active Directory Groups to Slack**.</span></span>

2) <span data-ttu-id="f3a15-159">Stel op de blade kenmerk toewijzing Enabled in op Ja.</span><span class="sxs-lookup"><span data-stu-id="f3a15-159">In the Attribute Mapping blade, set Enabled to Yes.</span></span>

3) <span data-ttu-id="f3a15-160">In de **kenmerktoewijzingen** sectie, moet u de kenmerken die worden gesynchroniseerd vanuit Azure AD met Slack controleren.</span><span class="sxs-lookup"><span data-stu-id="f3a15-160">In the **Attribute Mappings** section, review the group attributes that will be synchronized from Azure AD to Slack.</span></span> <span data-ttu-id="f3a15-161">Let op de kenmerken die zijn geselecteerd als **overeenkomend** eigenschappen overeenkomen met de groepen in Slack voor update-bewerkingen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f3a15-161">Note that the attributes selected as **Matching** properties will be used to match the groups in Slack for update operations.</span></span> 

4) <span data-ttu-id="f3a15-162">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="f3a15-162">Click **Save**.</span></span>

<span data-ttu-id="f3a15-163">Deze leiden tot een groepsobjecten worden toegewezen aan de vertraging in de **gebruikers en groepen** sectie volledig van Azure AD worden gesynchroniseerd met vertraging.</span><span class="sxs-lookup"><span data-stu-id="f3a15-163">This result in any group objects assigned to Slack in the **Users and Groups** section being fully synchronized from Azure AD to Slack.</span></span> <span data-ttu-id="f3a15-164">U kunt de **synchronisatiedetails** sectie voortgang en volg de koppelingen voor het inrichten van de activiteitsrapporten, waarin alle acties die worden uitgevoerd door de inrichting service op uw toegestane app te beschrijven.</span><span class="sxs-lookup"><span data-stu-id="f3a15-164">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Slack app.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="f3a15-165">Aanvullende resources</span><span class="sxs-lookup"><span data-stu-id="f3a15-165">Additional Resources</span></span>

* [<span data-ttu-id="f3a15-166">Het beheren van gebruikers account inrichten voor zakelijke Apps</span><span class="sxs-lookup"><span data-stu-id="f3a15-166">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="f3a15-167">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f3a15-167">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
