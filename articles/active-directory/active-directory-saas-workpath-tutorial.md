---
title: 'Zelfstudie: Azure Active Directory-integratie met Workpath | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Workpath.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 320b0daf-14be-4813-b59b-25a6a5070690
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: f4efa56d2c0374a977c1e46dad64b596cc9c3ea8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workpath"></a><span data-ttu-id="3e19e-103">Zelfstudie: Azure Active Directory-integratie met Workpath</span><span class="sxs-lookup"><span data-stu-id="3e19e-103">Tutorial: Azure Active Directory integration with Workpath</span></span>

<span data-ttu-id="3e19e-104">In deze zelfstudie leert u hoe Workpath integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3e19e-104">In this tutorial, you learn how to integrate Workpath with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3e19e-105">Workpath integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="3e19e-105">Integrating Workpath with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3e19e-106">U kunt beheren in Azure AD die toegang tot Workpath heeft</span><span class="sxs-lookup"><span data-stu-id="3e19e-106">You can control in Azure AD who has access to Workpath</span></span>
- <span data-ttu-id="3e19e-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Workpath (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="3e19e-107">You can enable your users to automatically get signed-on to Workpath (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3e19e-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="3e19e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3e19e-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3e19e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3e19e-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="3e19e-110">Prerequisites</span></span>

<span data-ttu-id="3e19e-111">Voor het configureren van Azure AD-integratie met Workpath, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="3e19e-111">To configure Azure AD integration with Workpath, you need the following items:</span></span>

- <span data-ttu-id="3e19e-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="3e19e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3e19e-113">Een Workpath eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="3e19e-113">A Workpath single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3e19e-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="3e19e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3e19e-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="3e19e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3e19e-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="3e19e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3e19e-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3e19e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3e19e-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="3e19e-118">Scenario description</span></span>
<span data-ttu-id="3e19e-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="3e19e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3e19e-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="3e19e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3e19e-121">Workpath uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="3e19e-121">Adding Workpath from the gallery</span></span>
2. <span data-ttu-id="3e19e-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="3e19e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workpath-from-the-gallery"></a><span data-ttu-id="3e19e-123">Workpath uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="3e19e-123">Adding Workpath from the gallery</span></span>
<span data-ttu-id="3e19e-124">Voor het configureren van de integratie van Workpath in Azure AD, moet u Workpath uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="3e19e-124">To configure the integration of Workpath into Azure AD, you need to add Workpath from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3e19e-125">**Als u wilt toevoegen Workpath uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="3e19e-125">**To add Workpath from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3e19e-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="3e19e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3e19e-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="3e19e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3e19e-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="3e19e-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="3e19e-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3e19e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="3e19e-133">Typ in het zoekvak **Workpath**.</span><span class="sxs-lookup"><span data-stu-id="3e19e-133">In the search box, type **Workpath**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_search.png)

5. <span data-ttu-id="3e19e-135">Selecteer in het deelvenster resultaten **Workpath**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="3e19e-135">In the results panel, select **Workpath**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3e19e-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="3e19e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3e19e-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Workpath op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="3e19e-138">In this section, you configure and test Azure AD single sign-on with Workpath based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3e19e-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Workpath is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3e19e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Workpath is to a user in Azure AD.</span></span> <span data-ttu-id="3e19e-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Workpath tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="3e19e-140">In other words, a link relationship between an Azure AD user and the related user in Workpath needs to be established.</span></span>

<span data-ttu-id="3e19e-141">Wijs in Workpath, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="3e19e-141">In Workpath, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3e19e-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Workpath, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="3e19e-142">To configure and test Azure AD single sign-on with Workpath, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3e19e-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3e19e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3e19e-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3e19e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3e19e-145">**[Maken van een testgebruiker Workpath](#creating-a-workpath-test-user)**  - Workpath die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="3e19e-145">**[Creating a Workpath test user](#creating-a-workpath-test-user)** - to have a counterpart of Britta Simon in Workpath that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3e19e-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="3e19e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3e19e-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="3e19e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3e19e-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="3e19e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3e19e-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Workpath configureren.</span><span class="sxs-lookup"><span data-stu-id="3e19e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Workpath application.</span></span>

<span data-ttu-id="3e19e-150">**Voor het configureren van Azure AD eenmalige aanmelding met Workpath, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="3e19e-150">**To configure Azure AD single sign-on with Workpath, perform the following steps:**</span></span>

1. <span data-ttu-id="3e19e-151">In de Azure-portal op de **Workpath** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="3e19e-151">In the Azure portal, on the **Workpath** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="3e19e-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="3e19e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_samlbase.png)

3. <span data-ttu-id="3e19e-155">Op de **Workpath domein en de URL's** sectie als u wilt configureren van de toepassing in **IDP** geïnitieerd modus de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="3e19e-155">On the **Workpath Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_url.png)

    <span data-ttu-id="3e19e-157">a.</span><span class="sxs-lookup"><span data-stu-id="3e19e-157">a.</span></span> <span data-ttu-id="3e19e-158">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://api.workpath.com/v1/saml/metadata/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="3e19e-158">In the **Identifier** textbox, type a URL using the following pattern: `https://api.workpath.com/v1/saml/metadata/<instancename>`</span></span>

    <span data-ttu-id="3e19e-159">b.</span><span class="sxs-lookup"><span data-stu-id="3e19e-159">b.</span></span> <span data-ttu-id="3e19e-160">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://api.workpath.com/v1/saml/assert/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="3e19e-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://api.workpath.com/v1/saml/assert/<instancename>`</span></span>

4. <span data-ttu-id="3e19e-161">Controleer **weergeven geavanceerde instellingen voor URL**.</span><span class="sxs-lookup"><span data-stu-id="3e19e-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="3e19e-162">Als u wilt configureren van de toepassing in **SP** geïnitieerd modus, voer de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="3e19e-162">If you wish to configure the application in **SP** initiated mode, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_url1.png)

    <span data-ttu-id="3e19e-164">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<subdomain>.workpath.com/ `</span><span class="sxs-lookup"><span data-stu-id="3e19e-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.workpath.com/ `</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3e19e-165">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="3e19e-165">These values are not real.</span></span> <span data-ttu-id="3e19e-166">Deze waarden bijwerken met de werkelijke aanmeldings-URL, -id en antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="3e19e-166">Update these values with the actual Sign-on URL, Identifier and Reply URL.</span></span> <span data-ttu-id="3e19e-167">Neem contact op met [Workpath ondersteuningsteam](https://help.workpath.com) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="3e19e-167">Contact [Workpath support team](https://help.workpath.com) to get these values.</span></span>

5. <span data-ttu-id="3e19e-168">De SAML-asserties verwacht Workpath toepassing in een specifieke indeling.</span><span class="sxs-lookup"><span data-stu-id="3e19e-168">Workpath application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="3e19e-169">Configureer de volgende claims voor deze toepassing.</span><span class="sxs-lookup"><span data-stu-id="3e19e-169">Configure the following claims for this application.</span></span> <span data-ttu-id="3e19e-170">U kunt beheren de waarden van deze kenmerken van de '**gebruikerskenmerken**' sectie op de pagina van de toepassing-integratie.</span><span class="sxs-lookup"><span data-stu-id="3e19e-170">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="3e19e-171">De volgende Schermafbeelding toont een voorbeeld voor deze configuratie.</span><span class="sxs-lookup"><span data-stu-id="3e19e-171">The following screenshot shows an example for this configuration.</span></span> 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_attributes.png)
    
6. <span data-ttu-id="3e19e-173">In de **gebruikerskenmerken** sectie op de **eenmalige aanmelding** dialoogvenster SAML-token kenmerk configureren zoals wordt weergegeven in de afbeelding en de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="3e19e-173">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="3e19e-174">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="3e19e-174">Attribute Name</span></span> | <span data-ttu-id="3e19e-175">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="3e19e-175">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="3e19e-176">Voornaam</span><span class="sxs-lookup"><span data-stu-id="3e19e-176">first_name</span></span> | <span data-ttu-id="3e19e-177">User.givenName</span><span class="sxs-lookup"><span data-stu-id="3e19e-177">user.givenname</span></span> |
    | <span data-ttu-id="3e19e-178">Achternaam</span><span class="sxs-lookup"><span data-stu-id="3e19e-178">last_name</span></span> | <span data-ttu-id="3e19e-179">User.surname</span><span class="sxs-lookup"><span data-stu-id="3e19e-179">user.surname</span></span> |
    
    <span data-ttu-id="3e19e-180">a.</span><span class="sxs-lookup"><span data-stu-id="3e19e-180">a.</span></span> <span data-ttu-id="3e19e-181">Klik op **toevoegen kenmerk** openen de **kenmerk toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3e19e-181">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-workpath-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="3e19e-183">b.</span><span class="sxs-lookup"><span data-stu-id="3e19e-183">b.</span></span> <span data-ttu-id="3e19e-184">In de **naam** textbox, typ de naam van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="3e19e-184">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-workpath-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="3e19e-186">c.</span><span class="sxs-lookup"><span data-stu-id="3e19e-186">c.</span></span> <span data-ttu-id="3e19e-187">Van de **waarde** typt u de waarde van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="3e19e-187">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="3e19e-188">d.</span><span class="sxs-lookup"><span data-stu-id="3e19e-188">d.</span></span> <span data-ttu-id="3e19e-189">Laat de **Namespace** textbox leeg.</span><span class="sxs-lookup"><span data-stu-id="3e19e-189">Leave the **Namespace** textbox blank.</span></span>
    
    <span data-ttu-id="3e19e-190">e.</span><span class="sxs-lookup"><span data-stu-id="3e19e-190">e.</span></span> <span data-ttu-id="3e19e-191">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="3e19e-191">Click **Ok**.</span></span>
    

7. <span data-ttu-id="3e19e-192">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="3e19e-192">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_certificate.png) 

8. <span data-ttu-id="3e19e-194">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="3e19e-194">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-workpath-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="3e19e-196">Op de **Workpath configuratie** sectie, klikt u op **configureren Workpath** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="3e19e-196">On the **Workpath Configuration** section, click **Configure Workpath** to open **Configure sign-on** window.</span></span> <span data-ttu-id="3e19e-197">Kopieer de **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="3e19e-197">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_configure.png) 

10. <span data-ttu-id="3e19e-199">Eenmalige aanmelding configureren op **Workpath** zijde, moet u de gedownloade verzenden **Metadata XML**, **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** naar [Workpath ondersteuningsteam](https://help.workpath.com).</span><span class="sxs-lookup"><span data-stu-id="3e19e-199">To configure single sign-on on **Workpath** side, you need to send the downloaded **Metadata XML**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Workpath support team](https://help.workpath.com).</span></span> 

> [!TIP]
> <span data-ttu-id="3e19e-200">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="3e19e-200">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3e19e-201">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="3e19e-201">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3e19e-202">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3e19e-202">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3e19e-203">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="3e19e-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="3e19e-204">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="3e19e-204">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="3e19e-206">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="3e19e-206">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3e19e-207">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="3e19e-207">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-workpath-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3e19e-209">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="3e19e-209">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-workpath-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3e19e-211">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3e19e-211">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-workpath-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3e19e-213">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="3e19e-213">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-workpath-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3e19e-215">a.</span><span class="sxs-lookup"><span data-stu-id="3e19e-215">a.</span></span> <span data-ttu-id="3e19e-216">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3e19e-216">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3e19e-217">b.</span><span class="sxs-lookup"><span data-stu-id="3e19e-217">b.</span></span> <span data-ttu-id="3e19e-218">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3e19e-218">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3e19e-219">c.</span><span class="sxs-lookup"><span data-stu-id="3e19e-219">c.</span></span> <span data-ttu-id="3e19e-220">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="3e19e-220">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3e19e-221">d.</span><span class="sxs-lookup"><span data-stu-id="3e19e-221">d.</span></span> <span data-ttu-id="3e19e-222">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="3e19e-222">Click **Create**.</span></span>
 
### <a name="creating-a-workpath-test-user"></a><span data-ttu-id="3e19e-223">Een testgebruiker Workpath maken</span><span class="sxs-lookup"><span data-stu-id="3e19e-223">Creating a Workpath test user</span></span>

<span data-ttu-id="3e19e-224">Workpath ondersteunt Just in time gebruikers inrichten.</span><span class="sxs-lookup"><span data-stu-id="3e19e-224">Workpath supports Just in time user provisioning.</span></span> <span data-ttu-id="3e19e-225">Na verificatie gebruikers in de toepassing automatisch gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3e19e-225">After authentication users are created in the application automatically.</span></span> 


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3e19e-226">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="3e19e-226">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3e19e-227">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Workpath.</span><span class="sxs-lookup"><span data-stu-id="3e19e-227">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Workpath.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="3e19e-229">**Britta Simon om aan te wijzen Workpath, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="3e19e-229">**To assign Britta Simon to Workpath, perform the following steps:**</span></span>

1. <span data-ttu-id="3e19e-230">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="3e19e-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="3e19e-232">Selecteer in de lijst met toepassingen **Workpath**.</span><span class="sxs-lookup"><span data-stu-id="3e19e-232">In the applications list, select **Workpath**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_app.png) 

3. <span data-ttu-id="3e19e-234">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="3e19e-234">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="3e19e-236">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="3e19e-236">Click **Add** button.</span></span> <span data-ttu-id="3e19e-237">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3e19e-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="3e19e-239">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="3e19e-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3e19e-240">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3e19e-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3e19e-241">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3e19e-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3e19e-242">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="3e19e-242">Testing single sign-on</span></span>

<span data-ttu-id="3e19e-243">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="3e19e-243">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3e19e-244">Als u op de tegel Workpath in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Workpath.</span><span class="sxs-lookup"><span data-stu-id="3e19e-244">When you click the Workpath tile in the Access Panel, you should get automatically signed-on to your Workpath application.</span></span>
<span data-ttu-id="3e19e-245">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3e19e-245">For more information about the Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3e19e-246">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="3e19e-246">Additional resources</span></span>

* [<span data-ttu-id="3e19e-247">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3e19e-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3e19e-248">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3e19e-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_203.png

