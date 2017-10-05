---
title: 'Zelfstudie: Azure Active Directory-integratie met LinkedIn Lookup | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en LinkedIn opzoeken.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a2757a39-1ead-4a3e-91e4-270be3055683
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: e296431866a8611b30e72f286884890adf0f7e50
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-lookup"></a><span data-ttu-id="c0d4b-103">Zelfstudie: Azure Active Directory-integratie met LinkedIn Lookup</span><span class="sxs-lookup"><span data-stu-id="c0d4b-103">Tutorial: Azure Active Directory integration with LinkedIn Lookup</span></span>

<span data-ttu-id="c0d4b-104">In deze zelfstudie leert u hoe LinkedIn om Lookup te integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c0d4b-104">In this tutorial, you learn how to integrate LinkedIn Lookup with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c0d4b-105">LinkedIn Lookup integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="c0d4b-105">Integrating LinkedIn Lookup with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c0d4b-106">U kunt beheren in Azure AD die toegang tot LinkedIn Lookup heeft</span><span class="sxs-lookup"><span data-stu-id="c0d4b-106">You can control in Azure AD who has access to LinkedIn Lookup</span></span>
- <span data-ttu-id="c0d4b-107">U kunt uw gebruikers automatisch ophalen aangemeld bij LinkedIn Lookup (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="c0d4b-107">You can enable your users to automatically get signed-on to LinkedIn Lookup (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c0d4b-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="c0d4b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c0d4b-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c0d4b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c0d4b-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="c0d4b-110">Prerequisites</span></span>

<span data-ttu-id="c0d4b-111">Voor het configureren van Azure AD-integratie met LinkedIn opzoeken, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="c0d4b-111">To configure Azure AD integration with LinkedIn Lookup, you need the following items:</span></span>

- <span data-ttu-id="c0d4b-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="c0d4b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c0d4b-113">Een LinkedIn Lookup eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="c0d4b-113">An LinkedIn Lookup single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c0d4b-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c0d4b-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="c0d4b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c0d4b-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c0d4b-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c0d4b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c0d4b-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="c0d4b-118">Scenario description</span></span>
<span data-ttu-id="c0d4b-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c0d4b-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="c0d4b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c0d4b-121">LinkedIn Lookup uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="c0d4b-121">Adding LinkedIn Lookup from the gallery</span></span>
2. <span data-ttu-id="c0d4b-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="c0d4b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-lookup-from-the-gallery"></a><span data-ttu-id="c0d4b-123">LinkedIn Lookup uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="c0d4b-123">Adding LinkedIn Lookup from the gallery</span></span>
<span data-ttu-id="c0d4b-124">Voor het configureren van de integratie van LinkedIn zoeken in Azure AD, moet u LinkedIn Lookup uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-124">To configure the integration of LinkedIn Lookup into Azure AD, you need to add LinkedIn Lookup from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c0d4b-125">**Als u wilt toevoegen LinkedIn Lookup uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="c0d4b-125">**To add LinkedIn Lookup from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c0d4b-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c0d4b-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c0d4b-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="c0d4b-131">Klik op **nieuwe toepassing** knop boven aan het dialoogvenster nieuwe toepassing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-131">Click **New application** button on the top of the dialog to add new application.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="c0d4b-133">Typ in het zoekvak **LinkedIn Lookup**.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-133">In the search box, type **LinkedIn Lookup**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_search.png)

5. <span data-ttu-id="c0d4b-135">Selecteer in het deelvenster resultaten **LinkedIn Lookup**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-135">In the results panel, select **LinkedIn Lookup**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c0d4b-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="c0d4b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c0d4b-138">In deze sectie maakt u configureert en test eenmalige aanmelding Azure AD met LinkedIn opzoeken op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-138">In this section, you configure and test Azure AD single sign-on with LinkedIn Lookup based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c0d4b-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in LinkedIn Lookup is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LinkedIn Lookup is to a user in Azure AD.</span></span> <span data-ttu-id="c0d4b-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in de zoekactie LinkedIn tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-140">In other words, a link relationship between an Azure AD user and the related user in LinkedIn Lookup needs to be established.</span></span>

<span data-ttu-id="c0d4b-141">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in LinkedIn opzoeken.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in LinkedIn Lookup.</span></span>

<span data-ttu-id="c0d4b-142">Als u wilt configureren en testen Azure AD eenmalige aanmelding met LinkedIn opzoeken, moet u voltooien van de volgende elementen:</span><span class="sxs-lookup"><span data-stu-id="c0d4b-142">To configure and test Azure AD single sign-on with LinkedIn Lookup, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c0d4b-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c0d4b-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c0d4b-145">**[Maken van een testgebruiker LinkedIn Lookup](#creating-an-linkedin-lookup-test-user)**  - LinkedIn Lookup die is gekoppeld aan de Azure AD-weergave van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-145">**[Creating an LinkedIn Lookup test user](#creating-an-linkedin-lookup-test-user)** - to have a counterpart of Britta Simon in LinkedIn Lookup that is linked to the Azure AD representation.</span></span>
4. <span data-ttu-id="c0d4b-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c0d4b-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c0d4b-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="c0d4b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c0d4b-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing LinkedIn Lookup configureren.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LinkedIn Lookup application.</span></span>

<span data-ttu-id="c0d4b-150">**Voor het configureren van Azure AD eenmalige aanmelding met LinkedIn opzoeken, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="c0d4b-150">**To configure Azure AD single sign-on with LinkedIn Lookup, perform the following steps:**</span></span>

1. <span data-ttu-id="c0d4b-151">In de Azure-portal op de **LinkedIn Lookup** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-151">In the Azure portal, on the **LinkedIn Lookup** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="c0d4b-153">Op de **eenmalige aanmelding** dialoogvenster in **modus** Selecteer **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-153">On the **Single sign-on** dialog, in **Mode** select **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_samlbase.png)

3. <span data-ttu-id="c0d4b-155">In een ander browservenster aanmelding bij uw **LinkedIn Lookup** website als beheerder.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-155">In a different web browser window, sign-on to your **LinkedIn Lookup** website as an administrator.</span></span>

4. <span data-ttu-id="c0d4b-156">In **Accountcentrum**, klikt u op **globale instellingen** onder **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-156">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="c0d4b-157">Schakel ook **Lookup** uit de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-157">Also, select **Lookup** from the dropdown list.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_LinkedIn_admin_011.png)

5. <span data-ttu-id="c0d4b-159">Klik op **of Klik hier om te laden en afzonderlijke velden van het formulier kopiëren** en kopieer **entiteit-Id** en **Url Assertion Consumer Access (ACS)**</span><span class="sxs-lookup"><span data-stu-id="c0d4b-159">Click **OR Click Here to load and copy individual fields from the form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_LinkedIn_admin_032.png)

6. <span data-ttu-id="c0d4b-161">Op de Azure-portal onder **LinkedIn Lookup domein en de URL's** sectie, voert u de volgende stappen uit als u wilt configureren, de toepassing in **IDP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="c0d4b-161">On Azure portal, under **LinkedIn Lookup Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_url.png)

    <span data-ttu-id="c0d4b-163">a.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-163">a.</span></span> <span data-ttu-id="c0d4b-164">In de **id** textbox, voer de **entiteit-ID** gekopieerd uit LinkedIn-Portal</span><span class="sxs-lookup"><span data-stu-id="c0d4b-164">In the **Identifier** textbox, enter the **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="c0d4b-165">b.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-165">b.</span></span> <span data-ttu-id="c0d4b-166">In de **antwoord-URL** textbox, voer de **Assertion Consumer Access (ACS) Url** gekopieerd uit LinkedIn-Portal</span><span class="sxs-lookup"><span data-stu-id="c0d4b-166">In the **Reply URL** textbox, enter the **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="c0d4b-167">Controleer **weergeven geavanceerde instellingen voor URL**, als u wilt configureren van de toepassing in **SP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="c0d4b-167">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_url1.png)

    <span data-ttu-id="c0d4b-169">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://www.linkedIn.com/checkpoint/enterprise/login/<AccountId>?application=lookup`</span><span class="sxs-lookup"><span data-stu-id="c0d4b-169">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://www.linkedIn.com/checkpoint/enterprise/login/<AccountId>?application=lookup`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="c0d4b-170">Dit is geen echte waarde.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-170">This is not real value.</span></span> <span data-ttu-id="c0d4b-171">De gebruiker heeft deze waarden bijwerken met de werkelijke URL voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-171">The user has to update these values with the actual Sign-On URL.</span></span> <span data-ttu-id="c0d4b-172">Neem contact op met [LinkedIn Lookup Client ondersteuningsteam](https://business.LinkedIn.com/lookup) deze waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-172">Contact [LinkedIn Lookup Client support team](https://business.LinkedIn.com/lookup) to get this value.</span></span>

8. <span data-ttu-id="c0d4b-173">Uw **LinkedIn Lookup** toepassing de SAML-asserties verwacht in een specifieke indeling.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-173">Your **LinkedIn Lookup** application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="c0d4b-174">De gebruiker heeft het aangepaste kenmerktoewijzingen toevoegen aan de configuratie van de SAML-token kenmerken.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-174">The user has to add custom attribute mappings to the SAML token attributes configuration.</span></span> <span data-ttu-id="c0d4b-175">De volgende Schermafbeelding toont een voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-175">The following screenshot shows an example.</span></span> <span data-ttu-id="c0d4b-176">De standaardwaarde van **gebruikers-id** is **user.userprincipalname** maar LinkedIn Lookup verwacht dit met het e-mailadres van de gebruiker worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-176">The default value of **User Identifier** is **user.userprincipalname** but LinkedIn Lookup expects this to be mapped with the user's email address.</span></span> <span data-ttu-id="c0d4b-177">U kunt **user.mail** kenmerk uit de lijst of gebruik de juiste kenmerkwaarde op basis van de organisatieconfiguratie van uw.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-177">You can use **user.mail** attribute from the list or use the appropriate attribute value based on your organization configuration.</span></span> 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-LinkedInlookup-tutorial/updateusermail.png)
    
9. <span data-ttu-id="c0d4b-179">In **gebruikerskenmerken** sectie, klikt u op **weergeven en bewerken van alle andere gebruikerskenmerken** en kenmerken instellen.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-179">In **User Attributes** section, click **View and edit all other user attributes** and set the attributes.</span></span> <span data-ttu-id="c0d4b-180">De gebruiker moet vier claims met de naam toe te voegen **e**, **afdeling**, **firstname**, en **lastname** en de waarde moet worden toegewezen met **user.mail**, **user.department**, **user.givenname**, en **user.surname** respectievelijk</span><span class="sxs-lookup"><span data-stu-id="c0d4b-180">The user needs to add four claims named **email**,  **department**, **firstname**, and **lastname** and the value is to be mapped with **user.mail**, **user.department**, **user.givenname**, and **user.surname** respectively</span></span>

    | <span data-ttu-id="c0d4b-181">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="c0d4b-181">Attribute Name</span></span> | <span data-ttu-id="c0d4b-182">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="c0d4b-182">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="c0d4b-183">E-mail</span><span class="sxs-lookup"><span data-stu-id="c0d4b-183">email</span></span>| <span data-ttu-id="c0d4b-184">User.mail</span><span class="sxs-lookup"><span data-stu-id="c0d4b-184">user.mail</span></span> |    
    | <span data-ttu-id="c0d4b-185">Afdeling</span><span class="sxs-lookup"><span data-stu-id="c0d4b-185">department</span></span>| <span data-ttu-id="c0d4b-186">User.Department</span><span class="sxs-lookup"><span data-stu-id="c0d4b-186">user.department</span></span> |
    | <span data-ttu-id="c0d4b-187">Voornaam</span><span class="sxs-lookup"><span data-stu-id="c0d4b-187">firstname</span></span>| <span data-ttu-id="c0d4b-188">User.givenName</span><span class="sxs-lookup"><span data-stu-id="c0d4b-188">user.givenname</span></span> |
    | <span data-ttu-id="c0d4b-189">Achternaam</span><span class="sxs-lookup"><span data-stu-id="c0d4b-189">lastname</span></span>| <span data-ttu-id="c0d4b-190">User.surname</span><span class="sxs-lookup"><span data-stu-id="c0d4b-190">user.surname</span></span> |

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-LinkedInlookup-tutorial/userattribute.png)

    <span data-ttu-id="c0d4b-192">a.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-192">a.</span></span> <span data-ttu-id="c0d4b-193">Klik op **kenmerk toevoegen** openen de **kenmerk toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-193">Click **Add Attribute** to open the **Add Attribute** dialog.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-LinkedInlookup-tutorial/4.png)
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-LinkedInlookup-tutorial/5.png)
   
    <span data-ttu-id="c0d4b-196">b.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-196">b.</span></span> <span data-ttu-id="c0d4b-197">In de **naam** textbox, typ de naam van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-197">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="c0d4b-198">c.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-198">c.</span></span> <span data-ttu-id="c0d4b-199">Van de **waarde** typt u de waarde van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-199">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="c0d4b-200">d.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-200">d.</span></span> <span data-ttu-id="c0d4b-201">Klik op **Ok**</span><span class="sxs-lookup"><span data-stu-id="c0d4b-201">Click **Ok**</span></span>

10. <span data-ttu-id="c0d4b-202">Voer de volgende stappen uit op de **naam** kenmerk -</span><span class="sxs-lookup"><span data-stu-id="c0d4b-202">Perform the following steps on the **name** attribute-</span></span>

    <span data-ttu-id="c0d4b-203">a.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-203">a.</span></span> <span data-ttu-id="c0d4b-204">Klik op het kenmerk openen de **kenmerk bewerken** venster.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-204">Click on the attribute to open the **Edit Attribute** window.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-LinkedInlookup-tutorial/url_update.png)

    <span data-ttu-id="c0d4b-206">b.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-206">b.</span></span> <span data-ttu-id="c0d4b-207">Verwijder de URL-waarde van de **naamruimte**.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-207">Delete the URL value from the **namespace**.</span></span>
    
    <span data-ttu-id="c0d4b-208">c.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-208">c.</span></span> <span data-ttu-id="c0d4b-209">Klik op **Ok** om op te slaan van de instelling.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-209">Click **Ok** to save the setting.</span></span>

10. <span data-ttu-id="c0d4b-210">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het XML-bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-210">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_certificate.png) 

11. <span data-ttu-id="c0d4b-212">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-212">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_400.png)

12. <span data-ttu-id="c0d4b-214">Ga naar **LinkedIn beheerdersinstellingen** sectie.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-214">Go to **LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="c0d4b-215">Uploaden van het XML-bestand dat u hebt gedownload van de Azure-portal door te klikken op de **uploaden XML-bestand** optie.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-215">Upload the XML file you downloaded from the Azure portal by clicking the **Upload XML file** option.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedIn_metadata_03.png)

13. <span data-ttu-id="c0d4b-217">Klik op **op** eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-217">Click **On** to enable SSO.</span></span> <span data-ttu-id="c0d4b-218">Status SSO wordt gewijzigd van **niet verbonden** naar **verbonden**</span><span class="sxs-lookup"><span data-stu-id="c0d4b-218">SSO status changes from **Not Connected** to **Connected**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedIn_admin_05.png)

> [!TIP]
> <span data-ttu-id="c0d4b-220">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="c0d4b-220">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c0d4b-221">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-221">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c0d4b-222">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c0d4b-222">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c0d4b-223">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="c0d4b-223">Creating an Azure AD test user</span></span>
<span data-ttu-id="c0d4b-224">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-224">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="c0d4b-226">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="c0d4b-226">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c0d4b-227">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-227">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c0d4b-229">Ga naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-229">Go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c0d4b-231">Klik op **toevoegen** openen de **gebruiker** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-231">Click **Add** to open the **User** dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c0d4b-233">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="c0d4b-233">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c0d4b-235">a.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-235">a.</span></span> <span data-ttu-id="c0d4b-236">In de **naam** textbox type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-236">In the **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="c0d4b-237">b.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-237">b.</span></span> <span data-ttu-id="c0d4b-238">In de **gebruikersnaam** textbox type de **e-mailadres** van Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-238">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="c0d4b-239">c.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-239">c.</span></span> <span data-ttu-id="c0d4b-240">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-240">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c0d4b-241">d.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-241">d.</span></span> <span data-ttu-id="c0d4b-242">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-242">Click **Create**.</span></span>
 
### <a name="creating-an-linkedin-lookup-test-user"></a><span data-ttu-id="c0d4b-243">Maken van een testgebruiker LinkedIn Lookup</span><span class="sxs-lookup"><span data-stu-id="c0d4b-243">Creating an LinkedIn Lookup test user</span></span>

<span data-ttu-id="c0d4b-244">Gekoppelde Lookup toepassing ondersteunt Just in Time (Just in time) gebruikers inrichten en na verificatie gebruikers automatisch in de toepassing gemaakt worden.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-244">Linked Lookup Application supports Just in Time (JIT) user provisioning and after authentication users are created in the application automatically.</span></span> <span data-ttu-id="c0d4b-245">Activeren **automatisch toewijzen van licenties** een licentie toewijzen aan de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-245">Activate **Automatically assign licenses** to assign a license to the user.</span></span>
   
   ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedin_admin_license.png)

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c0d4b-247">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0d4b-247">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c0d4b-248">In deze sectie maakt inschakelen u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan LinkedIn-Lookup.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-248">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LinkedIn Lookup.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="c0d4b-250">**Als u wilt toewijzen Britta Simon LinkedIn opzoeken, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="c0d4b-250">**To assign Britta Simon to LinkedIn Lookup, perform the following steps:**</span></span>

1. <span data-ttu-id="c0d4b-251">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-251">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="c0d4b-253">Selecteer in de lijst met toepassingen **LinkedIn Lookup**.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-253">In the applications list, select **LinkedIn Lookup**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_app.png) 

3. <span data-ttu-id="c0d4b-255">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-255">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="c0d4b-257">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-257">Click **Add** button.</span></span> <span data-ttu-id="c0d4b-258">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-258">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="c0d4b-260">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-260">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c0d4b-261">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-261">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c0d4b-262">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-262">Click **Assign** button on **Add Assignment** dialog.</span></span>

    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c0d4b-263">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="c0d4b-263">Testing single sign-on</span></span>

<span data-ttu-id="c0d4b-264">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-264">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c0d4b-265">Als u op de tegel LinkedIn opzoeken in het deelvenster toegang, moet u naar organisatie pagina waar u de details van uw persoonlijke LinkedIn moet worden omgeleid.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-265">When you click the LinkedIn Lookup tile in the Access Panel, you should be redirected to Organizational page where you have to provide your personal LinkedIn account details.</span></span> <span data-ttu-id="c0d4b-266">Uw persoonlijke account aan uw LinkedIn business-account worden gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="c0d4b-266">It links your personal account with your LinkedIn business account.</span></span> 

<span data-ttu-id="c0d4b-267">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c0d4b-267">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c0d4b-268">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="c0d4b-268">Additional resources</span></span>

* [<span data-ttu-id="c0d4b-269">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c0d4b-269">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c0d4b-270">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c0d4b-270">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_203.png

