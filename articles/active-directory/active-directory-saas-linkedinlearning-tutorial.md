---
title: 'Zelfstudie: Azure Active Directory-integratie met LinkedIn Learning | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en LinkedIn daarvan te leren.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d5857070-bf79-4bd3-9a2a-4c1919a74946
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: jeedes
ms.openlocfilehash: 6ad28cb3adaa63ddc3d3769a650d26ca6a7e2695
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-learning"></a><span data-ttu-id="ba54d-103">Zelfstudie: Azure Active Directory-integratie met LinkedIn Learning</span><span class="sxs-lookup"><span data-stu-id="ba54d-103">Tutorial: Azure Active Directory integration with LinkedIn Learning</span></span>

<span data-ttu-id="ba54d-104">In deze zelfstudie leert u hoe LinkedIn Learning integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ba54d-104">In this tutorial, you learn how to integrate LinkedIn Learning with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ba54d-105">LinkedIn Learning integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="ba54d-105">Integrating LinkedIn Learning with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ba54d-106">U kunt beheren in Azure AD die toegang tot LinkedIn Learning heeft</span><span class="sxs-lookup"><span data-stu-id="ba54d-106">You can control in Azure AD who has access to LinkedIn Learning</span></span>
- <span data-ttu-id="ba54d-107">U kunt uw gebruikers automatisch ophalen aangemeld bij LinkedIn Learning (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="ba54d-107">You can enable your users to automatically get signed-on to LinkedIn Learning (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ba54d-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="ba54d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ba54d-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ba54d-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ba54d-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ba54d-110">Prerequisites</span></span>

<span data-ttu-id="ba54d-111">Voor het configureren van Azure AD-integratie met LinkedIn Learning, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="ba54d-111">To configure Azure AD integration with LinkedIn Learning, you need the following items:</span></span>

- <span data-ttu-id="ba54d-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="ba54d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ba54d-113">Een LinkedIn Learning eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="ba54d-113">A LinkedIn Learning single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ba54d-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="ba54d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ba54d-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="ba54d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ba54d-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="ba54d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ba54d-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ba54d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ba54d-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="ba54d-118">Scenario description</span></span>
<span data-ttu-id="ba54d-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="ba54d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ba54d-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="ba54d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ba54d-121">LinkedIn Learning uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="ba54d-121">Adding LinkedIn Learning from the gallery</span></span>
2. <span data-ttu-id="ba54d-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ba54d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-learning-from-the-gallery"></a><span data-ttu-id="ba54d-123">LinkedIn Learning uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="ba54d-123">Adding LinkedIn Learning from the gallery</span></span>
<span data-ttu-id="ba54d-124">Voor het configureren van de integratie van LinkedIn Learning in Azure AD, moet u LinkedIn Learning uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="ba54d-124">To configure the integration of LinkedIn Learning into Azure AD, you need to add LinkedIn Learning from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ba54d-125">**Als u wilt toevoegen LinkedIn Learning uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="ba54d-125">**To add LinkedIn Learning from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ba54d-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="ba54d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ba54d-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ba54d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ba54d-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ba54d-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="ba54d-131">Klik op **toevoegen** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ba54d-131">Click **Add** button on the top of the dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="ba54d-133">Typ in het zoekvak **LinkedIn Learning**.</span><span class="sxs-lookup"><span data-stu-id="ba54d-133">In the search box, type **LinkedIn Learning**.</span></span> <span data-ttu-id="ba54d-134">Klik in het deelvenster met resultaten, op **LinkedIn Learning** de toepassing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="ba54d-134">From results panel, click **LinkedIn Learning** to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_000.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ba54d-136">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ba54d-136">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ba54d-137">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met LinkedIn Learning op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="ba54d-137">In this section, you configure and test Azure AD single sign-on with LinkedIn Learning based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ba54d-138">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in LinkedIn Learning in Azure AD voor een gebruiker is.</span><span class="sxs-lookup"><span data-stu-id="ba54d-138">For single sign-on to work, Azure AD needs to know what the counterpart user in LinkedIn Learning is to a user in Azure AD.</span></span> <span data-ttu-id="ba54d-139">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in LinkedIn Learning tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="ba54d-139">In other words, a link relationship between an Azure AD user and the related user in LinkedIn Learning needs to be established.</span></span>

<span data-ttu-id="ba54d-140">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** LinkedIn weten.</span><span class="sxs-lookup"><span data-stu-id="ba54d-140">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in LinkedIn Learning.</span></span>

<span data-ttu-id="ba54d-141">Om te configureren en testen van Azure AD eenmalige aanmelding met LinkedIn Learning, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="ba54d-141">To configure and test Azure AD single sign-on with LinkedIn Learning, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ba54d-142">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ba54d-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ba54d-143">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ba54d-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ba54d-144">**[Maken van een testgebruiker LinkedIn Learning](#creating-a-linkedin-learning-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ba54d-144">**[Creating a LinkedIn Learning test user](#creating-a-linkedin-learning-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="ba54d-145">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="ba54d-145">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ba54d-146">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="ba54d-146">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ba54d-147">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="ba54d-147">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ba54d-148">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw toepassing LinkedIn Learning.</span><span class="sxs-lookup"><span data-stu-id="ba54d-148">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LinkedIn Learning application.</span></span>

<span data-ttu-id="ba54d-149">**Voor het configureren van Azure AD eenmalige aanmelding met LinkedIn Learning, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="ba54d-149">**To configure Azure AD single sign-on with LinkedIn Learning, perform the following steps:**</span></span>

1. <span data-ttu-id="ba54d-150">In de Azure-portal op de **LinkedIn Learning** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="ba54d-150">In the Azure portal, on the **LinkedIn Learning** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="ba54d-152">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="ba54d-152">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedin_01.png)

3. <span data-ttu-id="ba54d-154">In een ander browservenster aanmelding in uw tenant, LinkedIn Learning als beheerder.</span><span class="sxs-lookup"><span data-stu-id="ba54d-154">In a different web browser window, sign-on to your LinkedIn Learning tenant as an administrator.</span></span>

4. <span data-ttu-id="ba54d-155">In **Accountcentrum**, klikt u op **globale instellingen** onder **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="ba54d-155">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="ba54d-156">Schakel ook **Learning - standaard** uit de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="ba54d-156">Also, select **Learning - Default** from the dropdown list.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_01.png)

5. <span data-ttu-id="ba54d-158">Klik op **of Klik hier om te laden en afzonderlijke velden van het formulier kopiëren** en kopieer **entiteit-Id** en **Url Assertion Consumer Access (ACS)**</span><span class="sxs-lookup"><span data-stu-id="ba54d-158">Click **OR Click Here to load and copy individual fields from the form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_03.png)

6. <span data-ttu-id="ba54d-160">Op de Azure-portal onder **LinkedIn Learning domein en de URL's**, voer de volgende stappen uit als u wilt configureren van SSO in **IdP geïnitieerd** modus</span><span class="sxs-lookup"><span data-stu-id="ba54d-160">On Azure portal, under **LinkedIn Learning Domain and URLs**, perform the following steps if you want to configure SSO in **IdP Initiated** mode</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_signon_01.png)

    <span data-ttu-id="ba54d-162">a.</span><span class="sxs-lookup"><span data-stu-id="ba54d-162">a.</span></span> <span data-ttu-id="ba54d-163">In de **id** textbox, voer de **entiteit-ID** gekopieerd uit LinkedIn-Portal</span><span class="sxs-lookup"><span data-stu-id="ba54d-163">In the **Identifier** textbox, enter the **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="ba54d-164">b.</span><span class="sxs-lookup"><span data-stu-id="ba54d-164">b.</span></span> <span data-ttu-id="ba54d-165">In de **antwoord-URL** textbox, voer de **Assertion Consumer Access (ACS) Url** gekopieerd uit LinkedIn-Portal</span><span class="sxs-lookup"><span data-stu-id="ba54d-165">In the **Reply URL** textbox, enter the **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="ba54d-166">Als u wilt configureren van SSO in **SP geïnitieerd**, klikt u op geavanceerde URL weergeven instelling optie in de configuratiesectie en de aanmeldings-URL configureren met het volgende patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="ba54d-166">If you want to configure SSO in **SP Initiated**, then click Show Advanced URL setting option in the configuration section and configure the sign-on URL with the following pattern:</span></span>

    `https://www.linkedin.com/checkpoint/enterprise/login/<AccountId>?application=learning&applicationInstanceId=<InstanceId>`

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_signon_02.png)   
    
8. <span data-ttu-id="ba54d-168">Uw toepassing LinkedIn Learning verwacht de SAML-asserties in een specifieke indeling waarvoor u aangepaste kenmerktoewijzingen toevoegen aan uw configuratie van SAML-token kenmerken.</span><span class="sxs-lookup"><span data-stu-id="ba54d-168">Your LinkedIn Learning application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="ba54d-169">De volgende Schermafbeelding toont een voorbeeld voor deze.</span><span class="sxs-lookup"><span data-stu-id="ba54d-169">The following screenshot shows an example for this.</span></span> <span data-ttu-id="ba54d-170">De standaardwaarde van **gebruikers-id** is **user.userprincipalname** maar LinkedIn Learning verwacht dit met het e-mailadres van de gebruiker worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="ba54d-170">The default value of **User Identifier** is **user.userprincipalname** but LinkedIn Learning expects this to be mapped with the user's email address.</span></span> <span data-ttu-id="ba54d-171">Die u kunt **user.mail** kenmerk uit de lijst of gebruik de juiste kenmerkwaarde op basis van de organisatieconfiguratie van uw.</span><span class="sxs-lookup"><span data-stu-id="ba54d-171">For that you can use **user.mail** attribute from the list or use the appropriate attribute value based on your organization configuration.</span></span> 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinlearning-tutorial/updateusermail.png)
    
9. <span data-ttu-id="ba54d-173">In **gebruikerskenmerken** sectie, klikt u op **weergeven en bewerken van alle andere gebruikerskenmerken** en kenmerken instellen.</span><span class="sxs-lookup"><span data-stu-id="ba54d-173">In **User Attributes** section, click **View and edit all other user attributes** and set the attributes.</span></span> <span data-ttu-id="ba54d-174">De gebruiker moet vier claims met de naam toe te voegen **e**, **afdeling**, **firstname**, en **lastname** en de waarde moet worden toegewezen met **user.mail**, **user.department**, **user.givenname**, en **user.surname** respectievelijk</span><span class="sxs-lookup"><span data-stu-id="ba54d-174">The user needs to add four claims named **email**, **department**, **firstname**, and **lastname** and the value is to be mapped with **user.mail**, **user.department**, **user.givenname**, and **user.surname** respectively</span></span>

    | <span data-ttu-id="ba54d-175">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="ba54d-175">Attribute Name</span></span> | <span data-ttu-id="ba54d-176">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="ba54d-176">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="ba54d-177">E-mail</span><span class="sxs-lookup"><span data-stu-id="ba54d-177">email</span></span>| <span data-ttu-id="ba54d-178">User.mail</span><span class="sxs-lookup"><span data-stu-id="ba54d-178">user.mail</span></span> |    
    | <span data-ttu-id="ba54d-179">Afdeling</span><span class="sxs-lookup"><span data-stu-id="ba54d-179">department</span></span>| <span data-ttu-id="ba54d-180">User.Department</span><span class="sxs-lookup"><span data-stu-id="ba54d-180">user.department</span></span> |
    | <span data-ttu-id="ba54d-181">Voornaam</span><span class="sxs-lookup"><span data-stu-id="ba54d-181">firstname</span></span>| <span data-ttu-id="ba54d-182">User.givenName</span><span class="sxs-lookup"><span data-stu-id="ba54d-182">user.givenname</span></span> |
    | <span data-ttu-id="ba54d-183">Achternaam</span><span class="sxs-lookup"><span data-stu-id="ba54d-183">lastname</span></span>| <span data-ttu-id="ba54d-184">User.surname</span><span class="sxs-lookup"><span data-stu-id="ba54d-184">user.surname</span></span> |
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-linkedinlearning-tutorial/userattribute.png)
    
    <span data-ttu-id="ba54d-186">a.</span><span class="sxs-lookup"><span data-stu-id="ba54d-186">a.</span></span> <span data-ttu-id="ba54d-187">Klik op **kenmerk toevoegen** om het dialoogvenster kenmerk te openen.</span><span class="sxs-lookup"><span data-stu-id="ba54d-187">Click **Add Attribute** to open the attribute dialog.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-linkedinLearning-tutorial/tutorial_attribute_04.png)

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-linkedinLearning-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="ba54d-190">b.</span><span class="sxs-lookup"><span data-stu-id="ba54d-190">b.</span></span> <span data-ttu-id="ba54d-191">In de **naam** textbox, typ de naam van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="ba54d-191">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="ba54d-192">c.</span><span class="sxs-lookup"><span data-stu-id="ba54d-192">c.</span></span> <span data-ttu-id="ba54d-193">Van de **waarde** typt u de waarde van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="ba54d-193">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="ba54d-194">d.</span><span class="sxs-lookup"><span data-stu-id="ba54d-194">d.</span></span> <span data-ttu-id="ba54d-195">Klik op **Ok**</span><span class="sxs-lookup"><span data-stu-id="ba54d-195">Click **Ok**</span></span>

10. <span data-ttu-id="ba54d-196">Voer de volgende stappen uit op de **naam** kenmerk -</span><span class="sxs-lookup"><span data-stu-id="ba54d-196">Perform the following steps on the **name** attribute-</span></span>

    <span data-ttu-id="ba54d-197">a.</span><span class="sxs-lookup"><span data-stu-id="ba54d-197">a.</span></span> <span data-ttu-id="ba54d-198">Klik op het kenmerk openen de **kenmerk bewerken** venster.</span><span class="sxs-lookup"><span data-stu-id="ba54d-198">Click on the attribute to open the **Edit Attribute** window.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinLearning-tutorial/url_update.png)

    <span data-ttu-id="ba54d-200">b.</span><span class="sxs-lookup"><span data-stu-id="ba54d-200">b.</span></span> <span data-ttu-id="ba54d-201">Verwijder de URL-waarde van de **naamruimte**.</span><span class="sxs-lookup"><span data-stu-id="ba54d-201">Delete the URL value from the **namespace**.</span></span>
    
    <span data-ttu-id="ba54d-202">c.</span><span class="sxs-lookup"><span data-stu-id="ba54d-202">c.</span></span> <span data-ttu-id="ba54d-203">Klik op **Ok** om op te slaan van de instelling.</span><span class="sxs-lookup"><span data-stu-id="ba54d-203">Click **Ok** to save the setting.</span></span>

11. <span data-ttu-id="ba54d-204">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het XML-bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="ba54d-204">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_certificate.png) 

12. <span data-ttu-id="ba54d-206">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="ba54d-206">Click **Save**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_400.png)

13. <span data-ttu-id="ba54d-208">Ga naar **LinkedIn beheerdersinstellingen** sectie.</span><span class="sxs-lookup"><span data-stu-id="ba54d-208">Go to **LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="ba54d-209">Het XML-bestand dat u hebt gedownload van de Azure-portal door te klikken op de optie uploaden XML-bestand uploaden.</span><span class="sxs-lookup"><span data-stu-id="ba54d-209">Upload the XML file you downloaded from the Azure portal by clicking the Upload XML file option.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_metadata_03.png)

14. <span data-ttu-id="ba54d-211">Klik op **op** eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="ba54d-211">Click **On** to enable SSO.</span></span> <span data-ttu-id="ba54d-212">Status SSO wordt gewijzigd van **niet verbonden** naar **verbonden**</span><span class="sxs-lookup"><span data-stu-id="ba54d-212">SSO status changes from **Not Connected** to **Connected**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_05.png)

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ba54d-214">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="ba54d-214">Creating an Azure AD test user</span></span>
<span data-ttu-id="ba54d-215">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="ba54d-215">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="ba54d-217">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="ba54d-217">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ba54d-218">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="ba54d-218">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ba54d-220">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="ba54d-220">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ba54d-222">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ba54d-222">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ba54d-224">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="ba54d-224">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ba54d-226">a.</span><span class="sxs-lookup"><span data-stu-id="ba54d-226">a.</span></span> <span data-ttu-id="ba54d-227">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ba54d-227">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ba54d-228">b.</span><span class="sxs-lookup"><span data-stu-id="ba54d-228">b.</span></span> <span data-ttu-id="ba54d-229">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ba54d-229">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ba54d-230">c.</span><span class="sxs-lookup"><span data-stu-id="ba54d-230">c.</span></span> <span data-ttu-id="ba54d-231">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="ba54d-231">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ba54d-232">d.</span><span class="sxs-lookup"><span data-stu-id="ba54d-232">d.</span></span> <span data-ttu-id="ba54d-233">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="ba54d-233">Click **Create**.</span></span> 

### <a name="creating-a-linkedin-learning-test-user"></a><span data-ttu-id="ba54d-234">Een testgebruiker LinkedIn Learning maken</span><span class="sxs-lookup"><span data-stu-id="ba54d-234">Creating a LinkedIn Learning test user</span></span>

<span data-ttu-id="ba54d-235">Gekoppelde Learning toepassing ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="ba54d-235">Linked Learning Application supports.</span></span> <span data-ttu-id="ba54d-236">Alleen bij tijd gebruikers inrichten en na verificatie zijn gebruikers in de toepassing automatisch gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ba54d-236">Just in time user provisioning and after authentication users are created in the application automatically.</span></span> <span data-ttu-id="ba54d-237">Op de beheerder van het tabblad instellingen op de portal spiegelen LinkedIn Learning de switch **automatisch toewijzen van licenties** actief voor het inschakelen van Just in time-inrichting en dit wordt ook een licentie toewijzen aan de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="ba54d-237">On the admin settings page on the LinkedIn Learning portal flip the switch **Automatically Assign licenses** to active to enable Just in time provisioning and this will also assign a license to the user.</span></span>
   
   ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-linkedinLearning-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ba54d-239">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="ba54d-239">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ba54d-240">In deze sectie maakt inschakelen u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan LinkedIn Learning.</span><span class="sxs-lookup"><span data-stu-id="ba54d-240">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LinkedIn Learning.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="ba54d-242">**Britta Simon om aan te wijzen LinkedIn Learning, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="ba54d-242">**To assign Britta Simon to LinkedIn Learning, perform the following steps:**</span></span>

1. <span data-ttu-id="ba54d-243">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ba54d-243">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="ba54d-245">Selecteer in de lijst met toepassingen **LinkedIn Learning**.</span><span class="sxs-lookup"><span data-stu-id="ba54d-245">In the applications list, select **LinkedIn Learning**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_0001.png) 

3. <span data-ttu-id="ba54d-247">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="ba54d-247">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="ba54d-249">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="ba54d-249">Click **Add** button.</span></span> <span data-ttu-id="ba54d-250">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ba54d-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="ba54d-252">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="ba54d-252">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ba54d-253">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ba54d-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ba54d-254">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ba54d-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ba54d-255">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ba54d-255">Testing single sign-on</span></span>

<span data-ttu-id="ba54d-256">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="ba54d-256">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ba54d-257">Wanneer u klikt op de tegel LinkedIn Learning in het deelvenster toegang, krijgt u de pagina Azure eenmalige aanmelding en op na geslaagde aanmelding, krijgt u in uw toepassing LinkedIn Learning.</span><span class="sxs-lookup"><span data-stu-id="ba54d-257">When you click the LinkedIn Learning tile in the Access Panel, you should get the Azure Sign-on page and on after successful sign-on, you should get into your LinkedIn Learning application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ba54d-258">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="ba54d-258">Additional resources</span></span>

* [<span data-ttu-id="ba54d-259">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ba54d-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ba54d-260">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ba54d-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_203.png