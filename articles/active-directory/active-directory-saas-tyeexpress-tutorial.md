---
title: 'Zelfstudie: Azure Active Directory-integratie met T & E Express | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en T & E Express.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: B42374E5-2559-4309-8EF2-820BEE7EBB0C
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: jeedes
ms.openlocfilehash: 869e5284c71904fcc817ceee0f39d94fab1bc6f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-te-express"></a><span data-ttu-id="9298c-103">Zelfstudie: Azure Active Directory-integratie met T & E Express</span><span class="sxs-lookup"><span data-stu-id="9298c-103">Tutorial: Azure Active Directory integration with T&E Express</span></span>

<span data-ttu-id="9298c-104">In deze zelfstudie leert u hoe d & E Express integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9298c-104">In this tutorial, you learn how to integrate T&E Express with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9298c-105">D & E Express integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="9298c-105">Integrating T&E Express with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9298c-106">U kunt beheren in Azure AD die toegang tot de d & E Express heeft</span><span class="sxs-lookup"><span data-stu-id="9298c-106">You can control in Azure AD who has access to T&E Express</span></span>
- <span data-ttu-id="9298c-107">U kunt uw gebruikers automatisch ophalen aangemeld bij d & E Express (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="9298c-107">You can enable your users to automatically get signed-on to T&E Express (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9298c-108">U kunt uw accounts op één centrale locatie - en de Azure Management portal beheren</span><span class="sxs-lookup"><span data-stu-id="9298c-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="9298c-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9298c-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9298c-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="9298c-110">Prerequisites</span></span>

<span data-ttu-id="9298c-111">Voor het configureren van Azure AD-integratie met T & E Express, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="9298c-111">To configure Azure AD integration with T&E Express, you need the following items:</span></span>

- <span data-ttu-id="9298c-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="9298c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9298c-113">Een d & E Express eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="9298c-113">A T&E Express single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9298c-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="9298c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9298c-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="9298c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9298c-116">U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="9298c-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="9298c-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9298c-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9298c-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="9298c-118">Scenario description</span></span>
<span data-ttu-id="9298c-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="9298c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9298c-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="9298c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9298c-121">D & E Express uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="9298c-121">Adding T&E Express from the gallery</span></span>
2. <span data-ttu-id="9298c-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="9298c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-te-express-from-the-gallery"></a><span data-ttu-id="9298c-123">D & E Express uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="9298c-123">Adding T&E Express from the gallery</span></span>
<span data-ttu-id="9298c-124">Voor het configureren van de integratie van d & E Express in Azure AD, moet u d & E Express uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="9298c-124">To configure the integration of T&E Express into Azure AD, you need to add T&E Express from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9298c-125">**Als u wilt toevoegen d & E Express uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="9298c-125">**To add T&E Express from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9298c-126">In de  **[Azure Management Portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="9298c-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9298c-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="9298c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9298c-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="9298c-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="9298c-131">Klik op **toevoegen** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9298c-131">Click **Add** button on the top of the dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="9298c-133">Typ in het zoekvak **d & E Express**.</span><span class="sxs-lookup"><span data-stu-id="9298c-133">In the search box, type **T&E Express**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_search.png)

5. <span data-ttu-id="9298c-135">Selecteer in het deelvenster resultaten **d & E Express**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="9298c-135">In the results panel, select **T&E Express**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9298c-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="9298c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9298c-138">In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met T & E Express op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="9298c-138">In this section, you configure and test Azure AD single sign-on with T&E Express based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9298c-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in d & E Express is aan een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9298c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in T&E Express is to a user in Azure AD.</span></span> <span data-ttu-id="9298c-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in de T & E Express worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="9298c-140">In other words, a link relationship between an Azure AD user and the related user in T&E Express needs to be established.</span></span>

<span data-ttu-id="9298c-141">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in d & E Express.</span><span class="sxs-lookup"><span data-stu-id="9298c-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in T&E Express.</span></span>

<span data-ttu-id="9298c-142">Om te configureren en testen van Azure AD eenmalige aanmelding met T & E Express, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="9298c-142">To configure and test Azure AD single sign-on with T&E Express, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9298c-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="9298c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9298c-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9298c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9298c-145">**[Maken van een testgebruiker d & E Express](#creating-a-te-express-test-user)**  : een equivalent van Britta Simon in d & E Express die is gekoppeld aan de Azure AD-representatie van haar hebben.</span><span class="sxs-lookup"><span data-stu-id="9298c-145">**[Creating a T&E Express test user](#creating-a-te-express-test-user)** - to have a counterpart of Britta Simon in T&E Express that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="9298c-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="9298c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9298c-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="9298c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9298c-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="9298c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9298c-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure-beheerportal en eenmalige aanmelding configureren in uw toepassing d & E Express.</span><span class="sxs-lookup"><span data-stu-id="9298c-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your T&E Express application.</span></span>

<span data-ttu-id="9298c-150">**Voor het configureren van Azure AD eenmalige aanmelding met T & E Express, de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="9298c-150">**To configure Azure AD single sign-on with T&E Express, perform the following steps:**</span></span>

1. <span data-ttu-id="9298c-151">In de Azure-beheerportal op de **d & E Express** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="9298c-151">In the Azure Management portal, on the **T&E Express** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="9298c-153">Op de **eenmalige aanmelding** dialoogvenster als **modus** Selecteer **op basis van SAML aanmelding** eenmalige aanmelding inschakelen op.</span><span class="sxs-lookup"><span data-stu-id="9298c-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_samlbase.png)

3. <span data-ttu-id="9298c-155">Op de **T & E Express domein en URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="9298c-155">On the **T&E Express Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_url.png)

    <span data-ttu-id="9298c-157">a.</span><span class="sxs-lookup"><span data-stu-id="9298c-157">a.</span></span> <span data-ttu-id="9298c-158">In de **id** textbox, typ de waarde als:`https://<domain>.tyeexpress.com`</span><span class="sxs-lookup"><span data-stu-id="9298c-158">In the **Identifier** textbox, type the value as: `https://<domain>.tyeexpress.com`</span></span>

    <span data-ttu-id="9298c-159">b.</span><span class="sxs-lookup"><span data-stu-id="9298c-159">b.</span></span> <span data-ttu-id="9298c-160">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://<domain>.tyeexpress.com/authorize/samlConsume.aspx`</span><span class="sxs-lookup"><span data-stu-id="9298c-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<domain>.tyeexpress.com/authorize/samlConsume.aspx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9298c-161">Houd er rekening mee dat deze niet de werkelijke waarden zijn.</span><span class="sxs-lookup"><span data-stu-id="9298c-161">Please note that these are not the real values.</span></span> <span data-ttu-id="9298c-162">U hebt deze waarden bijwerken met de werkelijke id en de antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="9298c-162">You have to update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="9298c-163">Hier raden we u voor het gebruik van de unieke waarde van een tekenreeks in de id.</span><span class="sxs-lookup"><span data-stu-id="9298c-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="9298c-164">Neem contact op met [d & E Express ondersteuningsteam](http://www.tyeexpress.com/contacto.aspx) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="9298c-164">Contact [T&E Express support team](http://www.tyeexpress.com/contacto.aspx) to get these values.</span></span>

5. <span data-ttu-id="9298c-165">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het XML-bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="9298c-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_certificate.png) 

6. <span data-ttu-id="9298c-167">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="9298c-167">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="9298c-169">Eenmalige aanmelding configureren op **d & E snelle** side, meld u aan bij de d & E express toepassing zonder eenmalige SAML over het gebruik van beheerdersreferenties.</span><span class="sxs-lookup"><span data-stu-id="9298c-169">To configure single sign-on on **T&E Express** side, login to the T&E express application without SAML single sign on using admin credentials.</span></span>

9. <span data-ttu-id="9298c-170">Onder de **Admin** tabblad, klikt u op **SAML domein** naar de instellingenpagina SAML openen.</span><span class="sxs-lookup"><span data-stu-id="9298c-170">Under the **Admin** Tab, Click on **SAML domain** to Open the SAML settings page.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tyeexpress-tutorial/tye-SAML.png)

10. <span data-ttu-id="9298c-172">Selecteer de **Activar(Activate)** optie van **Nee** naar **SI(Yes)**.</span><span class="sxs-lookup"><span data-stu-id="9298c-172">Select the **Activar(Activate)** option from **No** to **SI(Yes)**.</span></span> <span data-ttu-id="9298c-173">In de **identiteit Provider metagegevens** textbox, plakt u de metagegevens-XML, die u hebt donwloaded vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="9298c-173">In the **Identity Provider Metadata** textbox, paste the metadata XML which you have donwloaded from Azure portal.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tyeexpress-tutorial/tyeAdmin.png)

11. <span data-ttu-id="9298c-175">Klik op de **Guardar(Save)** knop de instellingen op te slaan.</span><span class="sxs-lookup"><span data-stu-id="9298c-175">Click on the **Guardar(Save)** button to save the settings.</span></span> 


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9298c-176">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="9298c-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="9298c-177">Het doel van deze sectie is het een testgebruiker maken in Azure Management portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="9298c-177">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="9298c-179">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="9298c-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9298c-180">In de **Azure Management portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="9298c-180">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9298c-182">Ga naar **gebruikers en groepen** en klik op **alle gebruikers** om de lijst met gebruikers weer te geven.</span><span class="sxs-lookup"><span data-stu-id="9298c-182">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9298c-184">Klik aan de bovenkant van het dialoogvenster **toevoegen** openen de **gebruiker** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9298c-184">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9298c-186">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="9298c-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9298c-188">a.</span><span class="sxs-lookup"><span data-stu-id="9298c-188">a.</span></span> <span data-ttu-id="9298c-189">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9298c-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9298c-190">b.</span><span class="sxs-lookup"><span data-stu-id="9298c-190">b.</span></span> <span data-ttu-id="9298c-191">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9298c-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9298c-192">c.</span><span class="sxs-lookup"><span data-stu-id="9298c-192">c.</span></span> <span data-ttu-id="9298c-193">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="9298c-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9298c-194">d.</span><span class="sxs-lookup"><span data-stu-id="9298c-194">d.</span></span> <span data-ttu-id="9298c-195">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="9298c-195">Click **Create**.</span></span>
 
### <a name="creating-a-te-express-test-user"></a><span data-ttu-id="9298c-196">Maken van een testgebruiker d & E Express</span><span class="sxs-lookup"><span data-stu-id="9298c-196">Creating a T&E Express test user</span></span>

<span data-ttu-id="9298c-197">Om in te schakelen gebruikers van Azure AD aan te melden bij de d & E Express, moeten ze worden ingericht in d & E Express.</span><span class="sxs-lookup"><span data-stu-id="9298c-197">In order to enable Azure AD users to log into T&E Express, they must be provisioned into T&E Express.</span></span>  
<span data-ttu-id="9298c-198">In geval van een T & E Express is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="9298c-198">In case of T&E Express, provisioning is a manual task.</span></span>

<span data-ttu-id="9298c-199">**Voor het inrichten van een gebruikersaccount, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="9298c-199">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="9298c-200">Meld u aan bij uw bedrijf d & E Express site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="9298c-200">Log in to your T&E Express company site as an administrator.</span></span>

2. <span data-ttu-id="9298c-201">Klik op gebruikers kunnen de gebruikers basispagina openen onder Admin-tag.</span><span class="sxs-lookup"><span data-stu-id="9298c-201">Under Admin tag, click on Users to open the Users master page.</span></span>

    ![Werknemer toevoegen](./media/active-directory-saas-tyeexpress-tutorial/tye-adminusers.png)

3. <span data-ttu-id="9298c-203">Klik op de startpagina op  **+**  de gebruikers toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="9298c-203">On the home page, click on **+** to add the users.</span></span>

    ![Werknemer toevoegen](./media/active-directory-saas-tyeexpress-tutorial/tye-usershome.png)

4. <span data-ttu-id="9298c-205">Voer de verplichte details zoals gevraagd in de vorm en klikt u op de knop voor het opslaan de details op te slaan.</span><span class="sxs-lookup"><span data-stu-id="9298c-205">Enter all the mandatory details as asked in the form and click the save button to save the details.</span></span>

    ![Werknemer toevoegen](./media/active-directory-saas-tyeexpress-tutorial/tye-usersadd.png)

    ![Werknemer toevoegen](./media/active-directory-saas-tyeexpress-tutorial/tye-userssave.png)


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9298c-208">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="9298c-208">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9298c-209">In deze sectie maakt inschakelen u Britta Simon Azure eenmalige aanmelding gebruiken door haar toegang verlenen aan d & E Express.</span><span class="sxs-lookup"><span data-stu-id="9298c-209">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to T&E Express.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="9298c-211">**Britta Simon om aan te wijzen d & E Express, de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="9298c-211">**To assign Britta Simon to T&E Express, perform the following steps:**</span></span>

1. <span data-ttu-id="9298c-212">In de Azure-beheerportal, opent u de weergave toepassingen en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="9298c-212">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="9298c-214">Selecteer in de lijst met toepassingen **d & E Express**.</span><span class="sxs-lookup"><span data-stu-id="9298c-214">In the applications list, select **T&E Express**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_app.png) 

3. <span data-ttu-id="9298c-216">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="9298c-216">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="9298c-218">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="9298c-218">Click **Add** button.</span></span> <span data-ttu-id="9298c-219">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9298c-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="9298c-221">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="9298c-221">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9298c-222">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9298c-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9298c-223">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9298c-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9298c-224">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="9298c-224">Testing single sign-on</span></span>

<span data-ttu-id="9298c-225">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="9298c-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="9298c-226">Als u op de tegel d & E Express in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing d & E Express.</span><span class="sxs-lookup"><span data-stu-id="9298c-226">When you click the T&E Express tile in the Access Panel, you should get automatically signed-on to your T&E Express application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9298c-227">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="9298c-227">Additional resources</span></span>

* [<span data-ttu-id="9298c-228">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9298c-228">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9298c-229">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9298c-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_203.png

