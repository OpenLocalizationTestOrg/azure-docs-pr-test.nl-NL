---
title: 'Zelfstudie: Azure Active Directory-integratie met LinkedInSalesNavigator | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en LinkedInSalesNavigator.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7a9fa8f3-d611-4ffe-8d50-04e9586b24da
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: ef26a16e79d9c9b0654634960b57dc59827b2c24
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-sales-navigator"></a><span data-ttu-id="b73d5-103">Zelfstudie: Azure Active Directory-integratie met LinkedIn verkoop Navigator</span><span class="sxs-lookup"><span data-stu-id="b73d5-103">Tutorial: Azure Active Directory integration with LinkedIn Sales Navigator</span></span>

<span data-ttu-id="b73d5-104">In deze zelfstudie leert u hoe LinkedIn verkoop Navigator integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b73d5-104">In this tutorial, you learn how to integrate LinkedIn Sales Navigator with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b73d5-105">LinkedIn verkoop Navigator integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="b73d5-105">Integrating LinkedIn Sales Navigator with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b73d5-106">U kunt beheren in Azure AD die toegang tot LinkedIn verkoop Navigator heeft</span><span class="sxs-lookup"><span data-stu-id="b73d5-106">You can control in Azure AD who has access to LinkedIn Sales Navigator</span></span>
- <span data-ttu-id="b73d5-107">U kunt uw gebruikers automatisch ophalen aangemeld bij LinkedIn verkoop Navigator (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="b73d5-107">You can enable your users to automatically get signed-on to LinkedIn Sales Navigator (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b73d5-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="b73d5-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b73d5-109">Als u meer gedetailleerde informatie over de integratie van de SaaS-app met Azure AD, bladert u [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b73d5-109">If you want to know more details about SaaS app integration with Azure AD, browse [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b73d5-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="b73d5-110">Prerequisites</span></span>

<span data-ttu-id="b73d5-111">Voor het configureren van Azure AD-integratie met LinkedIn verkoop Navigator, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="b73d5-111">To configure Azure AD integration with LinkedIn Sales Navigator, you need the following items:</span></span>

- <span data-ttu-id="b73d5-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="b73d5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b73d5-113">Een LinkedIn verkoop Navigator eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="b73d5-113">A LinkedIn Sales Navigator single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b73d5-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="b73d5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b73d5-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="b73d5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b73d5-116">Vermijd het gebruik van uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="b73d5-116">Avoid using your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b73d5-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b73d5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b73d5-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="b73d5-118">Scenario description</span></span>
<span data-ttu-id="b73d5-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="b73d5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b73d5-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="b73d5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b73d5-121">LinkedIn verkoop Navigator uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="b73d5-121">Adding LinkedIn Sales Navigator from the gallery</span></span>
2. <span data-ttu-id="b73d5-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b73d5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-sales-navigator-from-the-gallery"></a><span data-ttu-id="b73d5-123">LinkedIn verkoop Navigator uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="b73d5-123">Adding LinkedIn Sales Navigator from the gallery</span></span>
<span data-ttu-id="b73d5-124">Voor het configureren van de integratie van LinkedIn verkoop Navigator in Azure AD, moet u LinkedIn verkoop Navigator uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="b73d5-124">To configure the integration of LinkedIn Sales Navigator into Azure AD, you need to add LinkedIn Sales Navigator from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b73d5-125">**Als u wilt toevoegen LinkedIn verkoop Navigator uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b73d5-125">**To add LinkedIn Sales Navigator from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b73d5-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="b73d5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b73d5-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b73d5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b73d5-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b73d5-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="b73d5-131">Klik op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b73d5-131">Click **New application** button on the top of the dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="b73d5-133">Typ in het zoekvak **LinkedIn verkoop Navigator**.</span><span class="sxs-lookup"><span data-stu-id="b73d5-133">In the search box, type **LinkedIn Sales Navigator**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_search.png)

5. <span data-ttu-id="b73d5-135">Selecteer in het deelvenster resultaten **LinkedIn verkoop Navigator**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="b73d5-135">In the results panel, select **LinkedIn Sales Navigator**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b73d5-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b73d5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b73d5-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met LinkedIn verkoop Navigator op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="b73d5-138">In this section, you configure and test Azure AD single sign-on with LinkedIn Sales Navigator based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b73d5-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in LinkedIn verkoop Navigator is aan een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b73d5-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LinkedIn Sales Navigator is to a user in Azure AD.</span></span> <span data-ttu-id="b73d5-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in LinkedIn verkoop Navigator tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="b73d5-140">In other words, a link relationship between an Azure AD user and the related user in LinkedIn Sales Navigator needs to be established.</span></span>

<span data-ttu-id="b73d5-141">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in LinkedIn verkoop Navigator.</span><span class="sxs-lookup"><span data-stu-id="b73d5-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in LinkedIn Sales Navigator.</span></span>

<span data-ttu-id="b73d5-142">Om te configureren en testen van Azure AD eenmalige aanmelding met LinkedIn verkoop Navigator, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="b73d5-142">To configure and test Azure AD single sign-on with LinkedIn Sales Navigator, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b73d5-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b73d5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b73d5-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b73d5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b73d5-145">**[Maken van een testgebruiker LinkedIn verkoop Navigator](#creating-a-linkedin-sales-navigator-test-user)**  - LinkedIn verkoop Navigator die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="b73d5-145">**[Creating a LinkedIn Sales Navigator test user](#creating-a-linkedin-sales-navigator-test-user)** - to have a counterpart of Britta Simon in LinkedIn Sales Navigator that is linked to the Azure AD representation of the user.</span></span>
4. <span data-ttu-id="b73d5-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="b73d5-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b73d5-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="b73d5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b73d5-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="b73d5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b73d5-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw toepassing LinkedIn verkoop Navigator.</span><span class="sxs-lookup"><span data-stu-id="b73d5-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LinkedIn Sales Navigator application.</span></span>

<span data-ttu-id="b73d5-150">**Voor het configureren van Azure AD eenmalige aanmelding met LinkedIn verkoop Navigator, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b73d5-150">**To configure Azure AD single sign-on with LinkedIn Sales Navigator, perform the following steps:**</span></span>

1. <span data-ttu-id="b73d5-151">In de Azure-portal op de **LinkedIn verkoop Navigator** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="b73d5-151">In the Azure portal, on the **LinkedIn Sales Navigator** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="b73d5-153">Op de **eenmalige aanmelding** dialoogvenster in **modus** Selecteer **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="b73d5-153">On the **Single sign-on** dialog, in **Mode** select **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_samlbase.png)

3. <span data-ttu-id="b73d5-155">In een ander browservenster aanmelding bij uw **LinkedIn verkoop Navigator** website als beheerder.</span><span class="sxs-lookup"><span data-stu-id="b73d5-155">In a different web browser window, sign-on to your **LinkedIn Sales Navigator** website as an administrator.</span></span>

4. <span data-ttu-id="b73d5-156">In **Accountcentrum**, klikt u op **globale instellingen** onder **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="b73d5-156">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="b73d5-157">Schakel ook **verkoop Navigator** uit de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="b73d5-157">Also, select **Sales Navigator** from the dropdown list.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_admin_01.png)

5. <span data-ttu-id="b73d5-159">Klik op **of Klik hier om te laden en afzonderlijke velden van het formulier kopiëren** en kopieer **entiteit-Id** en **Assertion Consumer Access (ACS) Url**.</span><span class="sxs-lookup"><span data-stu-id="b73d5-159">Click **OR Click Here to load and copy individual fields from the form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_admin_031.png)

6. <span data-ttu-id="b73d5-161">Op de Azure-portal onder **LinkedIn verkoop Navigator domein en de URL's** sectie, voert u de volgende stappen uit als u wilt configureren, de toepassing in **IDP** modus gestart.</span><span class="sxs-lookup"><span data-stu-id="b73d5-161">On Azure portal, under **LinkedIn Sales Navigator Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_url1.png)

    <span data-ttu-id="b73d5-163">a.</span><span class="sxs-lookup"><span data-stu-id="b73d5-163">a.</span></span> <span data-ttu-id="b73d5-164">In de **id** textbox, voer de **entiteit-ID** gekopieerd uit LinkedIn-Portal</span><span class="sxs-lookup"><span data-stu-id="b73d5-164">In the **Identifier** textbox, enter the **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="b73d5-165">b.</span><span class="sxs-lookup"><span data-stu-id="b73d5-165">b.</span></span> <span data-ttu-id="b73d5-166">In de **antwoord-URL** textbox, voer de **Assertion Consumer Access (ACS) Url** gekopieerd uit LinkedIn-Portal</span><span class="sxs-lookup"><span data-stu-id="b73d5-166">In the **Reply URL** textbox, enter the **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="b73d5-167">Controleer **weergeven geavanceerde instellingen voor URL**, als u wilt configureren van de toepassing in **SP** modus gestart.</span><span class="sxs-lookup"><span data-stu-id="b73d5-167">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_url2.png)

    <span data-ttu-id="b73d5-169">In de **aanmeldings-URL** textbox, typ de waarde met het volgende patroon volgen:`https://www.linkedin.com/checkpoint/enterprise/login/<account id>?application=salesNavigator`</span><span class="sxs-lookup"><span data-stu-id="b73d5-169">In the **Sign-on URL** textbox, type the value using the following pattern: `https://www.linkedin.com/checkpoint/enterprise/login/<account id>?application=salesNavigator`</span></span>

8. <span data-ttu-id="b73d5-170">Uw **LinkedIn verkoop Navigator** toepassing de SAML-asserties in een specifieke indeling waarvoor u aangepaste kenmerktoewijzingen toevoegen aan uw configuratie van SAML-token kenmerken verwacht.</span><span class="sxs-lookup"><span data-stu-id="b73d5-170">Your **LinkedIn Sales Navigator** application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="b73d5-171">De volgende Schermafbeelding toont een voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="b73d5-171">The following screenshot shows an example.</span></span> <span data-ttu-id="b73d5-172">De standaardwaarde van **gebruikers-id** is **user.userprincipalname** maar LinkedIn verkoop Navigator verwacht met e-mailadres van de gebruiker worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="b73d5-172">The default value of **User Identifier** is **user.userprincipalname** but LinkedIn Sales Navigator expects it to be mapped with the user's email address.</span></span> <span data-ttu-id="b73d5-173">U kunt **user.mail** kenmerk uit de lijst of gebruik de juiste kenmerkwaarde op basis van de organisatieconfiguratie van uw.</span><span class="sxs-lookup"><span data-stu-id="b73d5-173">You can use **user.mail** attribute from the list or use the appropriate attribute value based on your organization configuration.</span></span> 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinsalesnavigator-tutorial/updateusermail.png)
    
9. <span data-ttu-id="b73d5-175">In **gebruikerskenmerken** sectie, klikt u op **weergeven en bewerken van alle andere gebruikerskenmerken** en kenmerken instellen.</span><span class="sxs-lookup"><span data-stu-id="b73d5-175">In **User Attributes** section, click **View and edit all other user attributes** and set the attributes.</span></span> <span data-ttu-id="b73d5-176">De gebruiker moet vier claims met de naam toe te voegen **e**, **afdeling**, **firstname**, en **lastname** en de waarde moet worden toegewezen met **user.mail**, **user.department**, **user.givenname**, en **user.surname** respectievelijk</span><span class="sxs-lookup"><span data-stu-id="b73d5-176">The user needs to add four claims named **email**, **department**, **firstname**, and **lastname** and the value is to be mapped with **user.mail**, **user.department**, **user.givenname**, and **user.surname** respectively</span></span>

    | <span data-ttu-id="b73d5-177">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="b73d5-177">Attribute Name</span></span> | <span data-ttu-id="b73d5-178">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="b73d5-178">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="b73d5-179">E-mail</span><span class="sxs-lookup"><span data-stu-id="b73d5-179">email</span></span>| <span data-ttu-id="b73d5-180">User.mail</span><span class="sxs-lookup"><span data-stu-id="b73d5-180">user.mail</span></span> |
    | <span data-ttu-id="b73d5-181">Afdeling</span><span class="sxs-lookup"><span data-stu-id="b73d5-181">department</span></span>| <span data-ttu-id="b73d5-182">User.Department</span><span class="sxs-lookup"><span data-stu-id="b73d5-182">user.department</span></span> |
    | <span data-ttu-id="b73d5-183">Voornaam</span><span class="sxs-lookup"><span data-stu-id="b73d5-183">firstname</span></span>| <span data-ttu-id="b73d5-184">User.givenName</span><span class="sxs-lookup"><span data-stu-id="b73d5-184">user.givenname</span></span> |
    | <span data-ttu-id="b73d5-185">Achternaam</span><span class="sxs-lookup"><span data-stu-id="b73d5-185">lastname</span></span>| <span data-ttu-id="b73d5-186">User.surname</span><span class="sxs-lookup"><span data-stu-id="b73d5-186">user.surname</span></span> |
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-linkedinsalesnavigator-tutorial/userattribute.png)
    
    <span data-ttu-id="b73d5-188">a.</span><span class="sxs-lookup"><span data-stu-id="b73d5-188">a.</span></span> <span data-ttu-id="b73d5-189">Klik op **kenmerk toevoegen** om het dialoogvenster kenmerk te openen.</span><span class="sxs-lookup"><span data-stu-id="b73d5-189">Click on **Add Attribute** to open the attribute dialog.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_attribute_04.png)
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_attribute_05.png)
   
    <span data-ttu-id="b73d5-192">b.</span><span class="sxs-lookup"><span data-stu-id="b73d5-192">b.</span></span> <span data-ttu-id="b73d5-193">In de **naam** textbox, typ de naam van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="b73d5-193">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="b73d5-194">c.</span><span class="sxs-lookup"><span data-stu-id="b73d5-194">c.</span></span> <span data-ttu-id="b73d5-195">Van de **waarde** typt u de waarde van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="b73d5-195">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="b73d5-196">d.</span><span class="sxs-lookup"><span data-stu-id="b73d5-196">d.</span></span> <span data-ttu-id="b73d5-197">Klik op **Ok**</span><span class="sxs-lookup"><span data-stu-id="b73d5-197">Click **Ok**</span></span>

10. <span data-ttu-id="b73d5-198">Voer de volgende stappen uit op de **naam** kenmerk -</span><span class="sxs-lookup"><span data-stu-id="b73d5-198">Perform the following steps on the **name** attribute-</span></span>

    <span data-ttu-id="b73d5-199">a.</span><span class="sxs-lookup"><span data-stu-id="b73d5-199">a.</span></span> <span data-ttu-id="b73d5-200">Klik op het kenmerk openen de **kenmerk bewerken** venster.</span><span class="sxs-lookup"><span data-stu-id="b73d5-200">Click on the attribute to open the **Edit Attribute** window.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinsalesnavigator-tutorial/url_update.png)

    <span data-ttu-id="b73d5-202">b.</span><span class="sxs-lookup"><span data-stu-id="b73d5-202">b.</span></span> <span data-ttu-id="b73d5-203">Verwijder de URL-waarde van de **naamruimte**.</span><span class="sxs-lookup"><span data-stu-id="b73d5-203">Delete the URL value from the **namespace**.</span></span>
    
    <span data-ttu-id="b73d5-204">c.</span><span class="sxs-lookup"><span data-stu-id="b73d5-204">c.</span></span> <span data-ttu-id="b73d5-205">Klik op **Ok** om op te slaan van de instelling.</span><span class="sxs-lookup"><span data-stu-id="b73d5-205">Click **Ok** to save the setting.</span></span>

11. <span data-ttu-id="b73d5-206">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het XML-bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="b73d5-206">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_certificate.png) 

12. <span data-ttu-id="b73d5-208">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="b73d5-208">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_400.png)

13. <span data-ttu-id="b73d5-210">Ga naar **LinkedIn beheerdersinstellingen** sectie.</span><span class="sxs-lookup"><span data-stu-id="b73d5-210">Go to **LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="b73d5-211">Klik op **uploaden XML-bestand** voor het uploaden van de Metadata-XML-bestand dat u hebt gedownload vanuit de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="b73d5-211">Click **Upload XML file** to upload the Metadata XML file that you have downloaded from the Azure portal.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_metadata_03.png)

14. <span data-ttu-id="b73d5-213">Klik op **op** eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="b73d5-213">Click **On** to enable SSO.</span></span> <span data-ttu-id="b73d5-214">Status SSO wordt gewijzigd van **niet verbonden** naar **verbonden**</span><span class="sxs-lookup"><span data-stu-id="b73d5-214">SSO status changes from **Not Connected** to **Connected**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_admin_05.png)


> [!TIP]
> <span data-ttu-id="b73d5-216">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="b73d5-216">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b73d5-217">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="b73d5-217">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b73d5-218">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b73d5-218">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b73d5-219">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="b73d5-219">Creating an Azure AD test user</span></span>
<span data-ttu-id="b73d5-220">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="b73d5-220">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="b73d5-222">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b73d5-222">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b73d5-223">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="b73d5-223">In the **Azure  portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b73d5-225">Ga naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="b73d5-225">Go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b73d5-227">Klik aan de bovenkant van het dialoogvenster **toevoegen** openen de **gebruiker** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b73d5-227">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b73d5-229">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="b73d5-229">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b73d5-231">a.</span><span class="sxs-lookup"><span data-stu-id="b73d5-231">a.</span></span> <span data-ttu-id="b73d5-232">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b73d5-232">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b73d5-233">b.</span><span class="sxs-lookup"><span data-stu-id="b73d5-233">b.</span></span> <span data-ttu-id="b73d5-234">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b73d5-234">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b73d5-235">c.</span><span class="sxs-lookup"><span data-stu-id="b73d5-235">c.</span></span> <span data-ttu-id="b73d5-236">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="b73d5-236">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b73d5-237">d.</span><span class="sxs-lookup"><span data-stu-id="b73d5-237">d.</span></span> <span data-ttu-id="b73d5-238">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="b73d5-238">Click **Create**.</span></span>
 
### <a name="creating-a-linkedin-sales-navigator-test-user"></a><span data-ttu-id="b73d5-239">Een testgebruiker LinkedIn verkoop Navigator maken</span><span class="sxs-lookup"><span data-stu-id="b73d5-239">Creating a LinkedIn Sales Navigator test user</span></span>

<span data-ttu-id="b73d5-240">Toepassing van de Navigator gekoppelde verkoop ondersteunt Just in Time (Just in time) gebruikers inrichten en na verificatie gebruikers automatisch in de toepassing gemaakt worden.</span><span class="sxs-lookup"><span data-stu-id="b73d5-240">Linked Sales Navigator Application supports Just in Time (JIT) user provisioning and after authentication users are created in the application automatically.</span></span> <span data-ttu-id="b73d5-241">Activeren **automatisch toewijzen van licenties** een licentie toewijzen aan de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="b73d5-241">Activate **Automatically assign licenses** to assign a license to the user.</span></span>
   
   ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-linkedinsalesnavigator-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b73d5-243">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="b73d5-243">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b73d5-244">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang te verlenen aan LinkedIn verkoop Navigator.</span><span class="sxs-lookup"><span data-stu-id="b73d5-244">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LinkedIn Sales Navigator.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="b73d5-246">**Britta Simon om aan te wijzen LinkedIn verkoop Navigator, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b73d5-246">**To assign Britta Simon to LinkedIn Sales Navigator, perform the following steps:**</span></span>

1. <span data-ttu-id="b73d5-247">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b73d5-247">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="b73d5-249">Selecteer in de lijst met toepassingen **LinkedIn verkoop Navigator**.</span><span class="sxs-lookup"><span data-stu-id="b73d5-249">In the applications list, select **LinkedIn Sales Navigator**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_app.png) 

3. <span data-ttu-id="b73d5-251">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="b73d5-251">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="b73d5-253">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="b73d5-253">Click **Add** button.</span></span> <span data-ttu-id="b73d5-254">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b73d5-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="b73d5-256">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="b73d5-256">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b73d5-257">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b73d5-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b73d5-258">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b73d5-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b73d5-259">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b73d5-259">Testing single sign-on</span></span>

<span data-ttu-id="b73d5-260">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="b73d5-260">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b73d5-261">Als u op de tegel LinkedIn verkoop Navigator in het deelvenster toegang, moet u naar organisatie pagina waar u de details van uw persoonlijke LinkedIn moet worden omgeleid.</span><span class="sxs-lookup"><span data-stu-id="b73d5-261">When you click the LinkedIn Sales Navigator tile in the Access Panel, you should be redirected to Organizational page where you have to provide your personal LinkedIn account details.</span></span> <span data-ttu-id="b73d5-262">Uw persoonlijke account aan uw LinkedIn business-account worden gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="b73d5-262">It links your personal account with your LinkedIn business account.</span></span> <span data-ttu-id="b73d5-263">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="b73d5-263">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b73d5-264">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="b73d5-264">Additional resources</span></span>

* [<span data-ttu-id="b73d5-265">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b73d5-265">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b73d5-266">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b73d5-266">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_203.png

