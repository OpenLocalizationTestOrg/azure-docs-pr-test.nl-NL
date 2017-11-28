---
title: 'Zelfstudie: Azure Active Directory-integratie met Hightail | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Hightail.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e15206ac-74b0-46e4-9329-892c7d242ec0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: ba55f9b62d274aa3eb91723c62b53f54de0891b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hightail"></a><span data-ttu-id="e696e-103">Zelfstudie: Azure Active Directory-integratie met Hightail</span><span class="sxs-lookup"><span data-stu-id="e696e-103">Tutorial: Azure Active Directory integration with Hightail</span></span>

<span data-ttu-id="e696e-104">In deze zelfstudie leert u hoe Hightail integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e696e-104">In this tutorial, you learn how to integrate Hightail with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e696e-105">Hightail integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="e696e-105">Integrating Hightail with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e696e-106">U kunt beheren in Azure AD die toegang tot Hightail heeft</span><span class="sxs-lookup"><span data-stu-id="e696e-106">You can control in Azure AD who has access to Hightail</span></span>
- <span data-ttu-id="e696e-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Hightail (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="e696e-107">You can enable your users to automatically get signed-on to Hightail (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e696e-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="e696e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e696e-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e696e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e696e-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="e696e-110">Prerequisites</span></span>

<span data-ttu-id="e696e-111">Voor het configureren van Azure AD-integratie met Hightail, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="e696e-111">To configure Azure AD integration with Hightail, you need the following items:</span></span>

- <span data-ttu-id="e696e-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="e696e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e696e-113">Een Hightail eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="e696e-113">A Hightail single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e696e-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="e696e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e696e-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="e696e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e696e-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="e696e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e696e-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e696e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e696e-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="e696e-118">Scenario description</span></span>
<span data-ttu-id="e696e-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="e696e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e696e-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="e696e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e696e-121">Hightail uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="e696e-121">Adding Hightail from the gallery</span></span>
2. <span data-ttu-id="e696e-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="e696e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hightail-from-the-gallery"></a><span data-ttu-id="e696e-123">Hightail uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="e696e-123">Adding Hightail from the gallery</span></span>
<span data-ttu-id="e696e-124">Voor het configureren van de integratie van Hightail in Azure AD, moet u Hightail uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="e696e-124">To configure the integration of Hightail into Azure AD, you need to add Hightail from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e696e-125">**Als u wilt toevoegen Hightail uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="e696e-125">**To add Hightail from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e696e-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="e696e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e696e-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="e696e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e696e-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="e696e-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="e696e-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e696e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="e696e-133">Typ in het zoekvak **Hightail**.</span><span class="sxs-lookup"><span data-stu-id="e696e-133">In the search box, type **Hightail**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_search.png)

5. <span data-ttu-id="e696e-135">Selecteer in het deelvenster resultaten **Hightail**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="e696e-135">In the results panel, select **Hightail**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e696e-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="e696e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e696e-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Hightail op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="e696e-138">In this section, you configure and test Azure AD single sign-on with Hightail based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e696e-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Hightail is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e696e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Hightail is to a user in Azure AD.</span></span> <span data-ttu-id="e696e-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Hightail tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="e696e-140">In other words, a link relationship between an Azure AD user and the related user in Hightail needs to be established.</span></span>

<span data-ttu-id="e696e-141">Wijs in Hightail, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="e696e-141">In Hightail, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e696e-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Hightail, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="e696e-142">To configure and test Azure AD single sign-on with Hightail, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e696e-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e696e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e696e-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e696e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e696e-145">**[Maken van een testgebruiker Hightail](#creating-a-hightail-test-user)**  - Hightail die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="e696e-145">**[Creating a Hightail test user](#creating-a-hightail-test-user)** - to have a counterpart of Britta Simon in Hightail that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e696e-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="e696e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e696e-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="e696e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e696e-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="e696e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e696e-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Hightail configureren.</span><span class="sxs-lookup"><span data-stu-id="e696e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Hightail application.</span></span>

<span data-ttu-id="e696e-150">**Voor het configureren van Azure AD eenmalige aanmelding met Hightail, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="e696e-150">**To configure Azure AD single sign-on with Hightail, perform the following steps:**</span></span>

1. <span data-ttu-id="e696e-151">In de Azure-portal op de **Hightail** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="e696e-151">In the Azure portal, on the **Hightail** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="e696e-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="e696e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_samlbase.png)

3. <span data-ttu-id="e696e-155">Op de **Hightail domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="e696e-155">On the **Hightail Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_url.png)

     <span data-ttu-id="e696e-157">In de **antwoord-URL** textbox, typ de URL als:`https://www.hightail.com/samlLogin?phi_action=app/samlLogin&subAction=handleSamlResponse`</span><span class="sxs-lookup"><span data-stu-id="e696e-157">In the **Reply URL** textbox, type the URL as: `https://www.hightail.com/samlLogin?phi_action=app/samlLogin&subAction=handleSamlResponse`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e696e-158">De voorgaande waarde is geen echte waarde.</span><span class="sxs-lookup"><span data-stu-id="e696e-158">The preceding value is not real value.</span></span> <span data-ttu-id="e696e-159">U kunt de waarde wordt bijgewerkt met de werkelijke antwoord-URL, die verderop in de zelfstudie wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="e696e-159">You will update the value with the actual Reply URL, which is explained later in the tutorial.</span></span>
 
4. <span data-ttu-id="e696e-160">Op de **Hightail domein en de URL's** sectie als u wilt configureren van de toepassing in **SP geïnitieerd modus**, voer de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="e696e-160">On the **Hightail Domain and URLs** section, If you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_url1.png)

    <span data-ttu-id="e696e-162">a.</span><span class="sxs-lookup"><span data-stu-id="e696e-162">a.</span></span> <span data-ttu-id="e696e-163">Klik op de **weergeven geavanceerde instellingen voor URL**.</span><span class="sxs-lookup"><span data-stu-id="e696e-163">Click the **Show advanced URL settings**.</span></span>

    <span data-ttu-id="e696e-164">b.</span><span class="sxs-lookup"><span data-stu-id="e696e-164">b.</span></span> <span data-ttu-id="e696e-165">In de **aanmelding op URL** textbox, typ de URL als:`https://www.hightail.com/loginSSO`</span><span class="sxs-lookup"><span data-stu-id="e696e-165">In the **Sign On URL** textbox, type the URL as: `https://www.hightail.com/loginSSO`</span></span>

4. <span data-ttu-id="e696e-166">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="e696e-166">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_certificate.png) 

5. <span data-ttu-id="e696e-168">Hightail toepassing de SAML-asserties verwacht in een specifieke indeling.</span><span class="sxs-lookup"><span data-stu-id="e696e-168">Hightail application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="e696e-169">Configureer de volgende claims voor deze toepassing.</span><span class="sxs-lookup"><span data-stu-id="e696e-169">Please configure the following claims for this application.</span></span> <span data-ttu-id="e696e-170">U kunt de waarden van deze kenmerken van beheren de **'Atrribute'** tabblad van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="e696e-170">You can manage the values of these attributes from the **"Atrribute"** tab of the application.</span></span> <span data-ttu-id="e696e-171">De volgende Schermafbeelding toont een voorbeeld voor deze.</span><span class="sxs-lookup"><span data-stu-id="e696e-171">The following screenshot shows an example for this.</span></span> 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_attribute.png) 

6. <span data-ttu-id="e696e-173">In de **gebruikerskenmerken** sectie op de **eenmalige aanmelding** dialoogvenster SAML-token kenmerk configureren zoals wordt weergegeven in de afbeelding en de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="e696e-173">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="e696e-174">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="e696e-174">Attribute Name</span></span> | <span data-ttu-id="e696e-175">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="e696e-175">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="e696e-176">Voornaam</span><span class="sxs-lookup"><span data-stu-id="e696e-176">FirstName</span></span> | <span data-ttu-id="e696e-177">User.givenName</span><span class="sxs-lookup"><span data-stu-id="e696e-177">user.givenname</span></span> |
    | <span data-ttu-id="e696e-178">Achternaam</span><span class="sxs-lookup"><span data-stu-id="e696e-178">LastName</span></span> | <span data-ttu-id="e696e-179">User.surname</span><span class="sxs-lookup"><span data-stu-id="e696e-179">user.surname</span></span> |
    | <span data-ttu-id="e696e-180">E-mail</span><span class="sxs-lookup"><span data-stu-id="e696e-180">Email</span></span> | <span data-ttu-id="e696e-181">User.mail</span><span class="sxs-lookup"><span data-stu-id="e696e-181">user.mail</span></span> |    
    | <span data-ttu-id="e696e-182">UserIdentity</span><span class="sxs-lookup"><span data-stu-id="e696e-182">UserIdentity</span></span> | <span data-ttu-id="e696e-183">User.mail</span><span class="sxs-lookup"><span data-stu-id="e696e-183">user.mail</span></span> |
    
    <span data-ttu-id="e696e-184">a.</span><span class="sxs-lookup"><span data-stu-id="e696e-184">a.</span></span> <span data-ttu-id="e696e-185">Klik op **toevoegen kenmerk** openen de **kenmerk toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e696e-185">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hightail-tutorial/tutorial_officespace_04.png)

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hightail-tutorial/tutorial_officespace_05.png)

    <span data-ttu-id="e696e-188">b.</span><span class="sxs-lookup"><span data-stu-id="e696e-188">b.</span></span> <span data-ttu-id="e696e-189">In de **naam** textbox, typ de naam van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="e696e-189">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="e696e-190">c.</span><span class="sxs-lookup"><span data-stu-id="e696e-190">c.</span></span> <span data-ttu-id="e696e-191">Van de **waarde** typt u de waarde van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="e696e-191">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="e696e-192">d.</span><span class="sxs-lookup"><span data-stu-id="e696e-192">d.</span></span> <span data-ttu-id="e696e-193">Laat de **Namespace** leeg.</span><span class="sxs-lookup"><span data-stu-id="e696e-193">Leave the **Namespace** blank.</span></span>
    
    <span data-ttu-id="e696e-194">e.</span><span class="sxs-lookup"><span data-stu-id="e696e-194">e.</span></span> <span data-ttu-id="e696e-195">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="e696e-195">Click **Ok**.</span></span>

7. <span data-ttu-id="e696e-196">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="e696e-196">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hightail-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="e696e-198">Op de **Hightail configuratie** sectie, klikt u op **configureren Hightail** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="e696e-198">On the **Hightail Configuration** section, click **Configure Hightail** to open **Configure sign-on** window.</span></span> <span data-ttu-id="e696e-199">Kopieer de **SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="e696e-199">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_configure.png) 

    >[!NOTE] 
    ><span data-ttu-id="e696e-201">Voordat u configureert de eenmalige aanmelding op Hightail app, neemt u witte lijst uw e-maildomein met Hightail team, zodat alle gebruikers die dit domein functionaliteit voor eenmalige aanmelding kunnen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e696e-201">Before configuring the Single Sign On at Hightail app, please white list your email domain with Hightail team so that all the users who are using this domain can use Single Sign On functionality.</span></span>


9. <span data-ttu-id="e696e-202">Als u eenmalige aanmelding voor uw toepassing is geconfigureerd, moet u eenmalige aanmelding voor uw tenant Hightail als beheerder.</span><span class="sxs-lookup"><span data-stu-id="e696e-202">To get SSO configured for your application, you need to sign-on to your Hightail tenant as an administrator.</span></span>
   
    <span data-ttu-id="e696e-203">a.</span><span class="sxs-lookup"><span data-stu-id="e696e-203">a.</span></span> <span data-ttu-id="e696e-204">Klik in het menu bovenaan op de **Account** tabblad en selecteer **SAML configureren**.</span><span class="sxs-lookup"><span data-stu-id="e696e-204">In the menu on the top, click the **Account** tab and select **Configure SAML**.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_001.png) 

    <span data-ttu-id="e696e-206">b.</span><span class="sxs-lookup"><span data-stu-id="e696e-206">b.</span></span> <span data-ttu-id="e696e-207">Schakel het selectievakje van **SAML-verificatie inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="e696e-207">Select the checkbox of **Enable SAML Authentication**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_002.png) 

    <span data-ttu-id="e696e-209">c.</span><span class="sxs-lookup"><span data-stu-id="e696e-209">c.</span></span> <span data-ttu-id="e696e-210">De base-64 gecodeerde certificaat openen in Kladblok van Azure portal hebt gedownload, Kopieer de inhoud ervan naar het Klembord en plakt u deze naar de **handtekeningcertificaat van SAML-Token** textbox.</span><span class="sxs-lookup"><span data-stu-id="e696e-210">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **SAML Token Signing Certificate** textbox.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_003.png) 

    <span data-ttu-id="e696e-212">d.</span><span class="sxs-lookup"><span data-stu-id="e696e-212">d.</span></span> <span data-ttu-id="e696e-213">In de **SAML-instantie (id-Provider)** textbox, plak de waarde van **SAML Single Sign-On Service-URL** gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="e696e-213">In the **SAML Authority (Identity Provider)** textbox, paste the value of **SAML Single Sign-On Service URL** copied from Azure portal.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_004.png)

    <span data-ttu-id="e696e-215">e.</span><span class="sxs-lookup"><span data-stu-id="e696e-215">e.</span></span> <span data-ttu-id="e696e-216">Als u wilt configureren van de toepassing in **IDP geïnitieerd modus** Selecteer **'Identiteitsprovider (IdP) geïnitieerd aanmelden'**.</span><span class="sxs-lookup"><span data-stu-id="e696e-216">If you wish to configure the application in **IDP initiated mode** select **"Identity Provider (IdP) initiated log in"**.</span></span> <span data-ttu-id="e696e-217">Als **SP geïnitieerd modus** Selecteer **'Serviceprovider (SP) geïnitieerd aanmelden'**.</span><span class="sxs-lookup"><span data-stu-id="e696e-217">If **SP initiated mode** select **"Service Provider (SP) initiated log in"**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_006.png)

    <span data-ttu-id="e696e-219">f.</span><span class="sxs-lookup"><span data-stu-id="e696e-219">f.</span></span> <span data-ttu-id="e696e-220">Kopieer de URL van de consument SAML voor uw exemplaar en plak deze in **antwoord-URL** textbox in **Hightail domein en de URL's** sectie op Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="e696e-220">Copy the SAML consumer URL for your instance and paste it in **Reply URL** textbox in **Hightail Domain and URLs** section on Azure portal.</span></span>
    
    <span data-ttu-id="e696e-221">g.</span><span class="sxs-lookup"><span data-stu-id="e696e-221">g.</span></span> <span data-ttu-id="e696e-222">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="e696e-222">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="e696e-223">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="e696e-223">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e696e-224">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="e696e-224">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e696e-225">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e696e-225">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e696e-226">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="e696e-226">Creating an Azure AD test user</span></span>
<span data-ttu-id="e696e-227">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="e696e-227">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="e696e-229">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="e696e-229">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e696e-230">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="e696e-230">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hightail-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e696e-232">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="e696e-232">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hightail-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e696e-234">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e696e-234">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hightail-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e696e-236">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="e696e-236">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hightail-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e696e-238">a.</span><span class="sxs-lookup"><span data-stu-id="e696e-238">a.</span></span> <span data-ttu-id="e696e-239">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e696e-239">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e696e-240">b.</span><span class="sxs-lookup"><span data-stu-id="e696e-240">b.</span></span> <span data-ttu-id="e696e-241">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e696e-241">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e696e-242">c.</span><span class="sxs-lookup"><span data-stu-id="e696e-242">c.</span></span> <span data-ttu-id="e696e-243">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="e696e-243">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e696e-244">d.</span><span class="sxs-lookup"><span data-stu-id="e696e-244">d.</span></span> <span data-ttu-id="e696e-245">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="e696e-245">Click **Create**.</span></span>
 
### <a name="creating-a-hightail-test-user"></a><span data-ttu-id="e696e-246">Een testgebruiker Hightail maken</span><span class="sxs-lookup"><span data-stu-id="e696e-246">Creating a Hightail test user</span></span>

<span data-ttu-id="e696e-247">Het doel van deze sectie is het maken van een gebruiker Britta Simon in Hightail genoemd.</span><span class="sxs-lookup"><span data-stu-id="e696e-247">The objective of this section is to create a user called Britta Simon in Hightail.</span></span> 

<span data-ttu-id="e696e-248">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="e696e-248">There is no action item for you in this section.</span></span> <span data-ttu-id="e696e-249">Hightail ondersteunt just in time gebruikers inrichten op basis van de aangepaste claims.</span><span class="sxs-lookup"><span data-stu-id="e696e-249">Hightail supports just-in-time user provisioning based on the custom claims.</span></span> <span data-ttu-id="e696e-250">Als u de aangepaste claims hebt geconfigureerd, zoals wordt weergegeven in de sectie  **[eenmalige aanmelding configureren Azure AD](#configuring-azure-ad-single-sign-on)**  , een gebruiker is gemaakt in de toepassing nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="e696e-250">If you have configured the custom claims as shown in the section **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** above, a user is automatically created in the application it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="e696e-251">Als u een gebruiker handmatig maken wilt, moet u contact op met de [Hightail ondersteuningsteam](mailto:support@hightail.com).</span><span class="sxs-lookup"><span data-stu-id="e696e-251">If you need to create a user manually, you need to contact the [Hightail support team](mailto:support@hightail.com).</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e696e-252">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="e696e-252">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e696e-253">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Hightail.</span><span class="sxs-lookup"><span data-stu-id="e696e-253">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Hightail.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="e696e-255">**Britta Simon om aan te wijzen Hightail, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="e696e-255">**To assign Britta Simon to Hightail, perform the following steps:**</span></span>

1. <span data-ttu-id="e696e-256">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="e696e-256">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="e696e-258">Selecteer in de lijst met toepassingen **Hightail**.</span><span class="sxs-lookup"><span data-stu-id="e696e-258">In the applications list, select **Hightail**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_app.png) 

3. <span data-ttu-id="e696e-260">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="e696e-260">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="e696e-262">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="e696e-262">Click **Add** button.</span></span> <span data-ttu-id="e696e-263">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e696e-263">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="e696e-265">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="e696e-265">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e696e-266">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e696e-266">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e696e-267">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e696e-267">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e696e-268">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="e696e-268">Testing single sign-on</span></span>

<span data-ttu-id="e696e-269">Het doel van deze sectie is het testen van uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="e696e-269">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e696e-270">Als u op de tegel Hightail in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Hightail.</span><span class="sxs-lookup"><span data-stu-id="e696e-270">When you click the Hightail tile in the Access Panel, you should get automatically signed-on to your Hightail application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="e696e-271">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="e696e-271">Additional resources</span></span>

* [<span data-ttu-id="e696e-272">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e696e-272">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e696e-273">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e696e-273">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_203.png

