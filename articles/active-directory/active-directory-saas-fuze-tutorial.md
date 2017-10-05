---
title: 'Zelfstudie: Azure Active Directory-integratie met Fuze | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Fuze.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9780b4bf-1fd1-48c1-9ceb-f750225ae08a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: jeedes
ms.openlocfilehash: c7f7b095aac6202a7ec5248ee2bbb109615287a7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-fuze"></a><span data-ttu-id="d673f-103">Zelfstudie: Azure Active Directory-integratie met Fuze</span><span class="sxs-lookup"><span data-stu-id="d673f-103">Tutorial: Azure Active Directory integration with Fuze</span></span>

<span data-ttu-id="d673f-104">In deze zelfstudie leert u hoe Fuze integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d673f-104">In this tutorial, you learn how to integrate Fuze with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d673f-105">Fuze integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="d673f-105">Integrating Fuze with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d673f-106">U kunt beheren in Azure AD die toegang tot Fuze heeft</span><span class="sxs-lookup"><span data-stu-id="d673f-106">You can control in Azure AD who has access to Fuze</span></span>
- <span data-ttu-id="d673f-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Fuze (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="d673f-107">You can enable your users to automatically get signed-on to Fuze (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d673f-108">U kunt uw accounts op één centrale locatie - en de Azure Management portal beheren</span><span class="sxs-lookup"><span data-stu-id="d673f-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="d673f-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d673f-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d673f-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="d673f-110">Prerequisites</span></span>

<span data-ttu-id="d673f-111">Voor het configureren van Azure AD-integratie met Fuze, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="d673f-111">To configure Azure AD integration with Fuze, you need the following items:</span></span>

- <span data-ttu-id="d673f-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="d673f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d673f-113">Een Fuze eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="d673f-113">A Fuze single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="d673f-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="d673f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="d673f-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="d673f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d673f-116">U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="d673f-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="d673f-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d673f-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="d673f-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="d673f-118">Scenario description</span></span>
<span data-ttu-id="d673f-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="d673f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d673f-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="d673f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d673f-121">Fuze uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="d673f-121">Adding Fuze from the gallery</span></span>
2. <span data-ttu-id="d673f-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="d673f-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-fuze-from-the-gallery"></a><span data-ttu-id="d673f-123">Fuze uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="d673f-123">Adding Fuze from the gallery</span></span>
<span data-ttu-id="d673f-124">Voor het configureren van de integratie van Fuze in Azure AD, moet u Fuze uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="d673f-124">To configure the integration of Fuze into Azure AD, you need to add Fuze from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d673f-125">**Als u wilt toevoegen Fuze uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="d673f-125">**To add Fuze from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d673f-126">In de  **[Azure Management Portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="d673f-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d673f-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="d673f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d673f-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="d673f-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="d673f-131">Klik op **toevoegen** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d673f-131">Click **Add** button on the top of the dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="d673f-133">Typ in het zoekvak **Fuze**.</span><span class="sxs-lookup"><span data-stu-id="d673f-133">In the search box, type **Fuze**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_000.png)

5. <span data-ttu-id="d673f-135">Selecteer in het deelvenster resultaten **Fuze**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="d673f-135">In the results panel, select **Fuze**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d673f-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="d673f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d673f-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Fuze op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="d673f-138">In this section, you configure and test Azure AD single sign-on with Fuze based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d673f-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Fuze is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d673f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Fuze is to a user in Azure AD.</span></span> <span data-ttu-id="d673f-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Fuze tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="d673f-140">In other words, a link relationship between an Azure AD user and the related user in Fuze needs to be established.</span></span>

<span data-ttu-id="d673f-141">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in Fuze.</span><span class="sxs-lookup"><span data-stu-id="d673f-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Fuze.</span></span>

<span data-ttu-id="d673f-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Fuze, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="d673f-142">To configure and test Azure AD single sign-on with Fuze, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d673f-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d673f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d673f-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d673f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d673f-145">**[Maken van een testgebruiker Fuze](#creating-a-fuze-test-user)**  - Fuze die is gekoppeld aan de Azure AD-representatie van haar van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="d673f-145">**[Creating a Fuze test user](#creating-a-fuze-test-user)** - to have a counterpart of Britta Simon in Fuze that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="d673f-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="d673f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d673f-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="d673f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d673f-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="d673f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d673f-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure-beheerportal en eenmalige aanmelding in uw toepassing Fuze configureren.</span><span class="sxs-lookup"><span data-stu-id="d673f-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Fuze application.</span></span>

<span data-ttu-id="d673f-150">**Voor het configureren van Azure AD eenmalige aanmelding met Fuze, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="d673f-150">**To configure Azure AD single sign-on with Fuze, perform the following steps:**</span></span>

1. <span data-ttu-id="d673f-151">In de Azure-beheerportal op de **Fuze** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="d673f-151">In the Azure Management portal, on the **Fuze** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="d673f-153">Op de **eenmalige aanmelding** dialoogvenster als **modus** Selecteer **op basis van SAML aanmelding** eenmalige aanmelding inschakelen op.</span><span class="sxs-lookup"><span data-stu-id="d673f-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_01.png)

3. <span data-ttu-id="d673f-155">Op de **Fuze domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="d673f-155">On the **Fuze Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_020.png)
    
    <span data-ttu-id="d673f-157">In de **aanmelden URL** textbox, typ de eenmalige aanmelding URL als:`https://www.thinkingphones.com/jetspeed/portal/`</span><span class="sxs-lookup"><span data-stu-id="d673f-157">In the **Sign on URL** textbox, type the Sign-on URL as: `https://www.thinkingphones.com/jetspeed/portal/`</span></span>

4.  <span data-ttu-id="d673f-158">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="d673f-158">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-fuze-tutorial/tutorial_general_400.png)

5. <span data-ttu-id="d673f-160">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het XML-bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="d673f-160">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the xml file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_05.png) 

6. <span data-ttu-id="d673f-162">Eenmalige aanmelding configureren op **Fuze** zijde, moet u de gedownloade verzenden **Metadata XML** naar [Fuze ondersteuningsteam](https://www.fuze.com/support).</span><span class="sxs-lookup"><span data-stu-id="d673f-162">To configure single sign-on on **Fuze** side, you need to send the downloaded **Metadata XML** to [Fuze support team](https://www.fuze.com/support).</span></span> <span data-ttu-id="d673f-163">Ze zullen dit instellen om de SAML SSO-verbinding juist is ingesteld op beide zijden.</span><span class="sxs-lookup"><span data-stu-id="d673f-163">They will set this up in order to have the SAML SSO connection set properly on both sides.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d673f-164">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="d673f-164">Creating an Azure AD test user</span></span>
<span data-ttu-id="d673f-165">Het doel van deze sectie is het een testgebruiker maken in Azure Management portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="d673f-165">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="d673f-167">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="d673f-167">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d673f-168">In de **Azure Management portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="d673f-168">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-fuze-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d673f-170">Ga naar **gebruikers en groepen** en klik op **alle gebruikers** om de lijst met gebruikers weer te geven.</span><span class="sxs-lookup"><span data-stu-id="d673f-170">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-fuze-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d673f-172">Klik aan de bovenkant van het dialoogvenster **toevoegen** openen de **gebruiker** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d673f-172">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-fuze-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d673f-174">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="d673f-174">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-fuze-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d673f-176">a.</span><span class="sxs-lookup"><span data-stu-id="d673f-176">a.</span></span> <span data-ttu-id="d673f-177">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d673f-177">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d673f-178">b.</span><span class="sxs-lookup"><span data-stu-id="d673f-178">b.</span></span> <span data-ttu-id="d673f-179">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d673f-179">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d673f-180">c.</span><span class="sxs-lookup"><span data-stu-id="d673f-180">c.</span></span> <span data-ttu-id="d673f-181">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="d673f-181">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d673f-182">d.</span><span class="sxs-lookup"><span data-stu-id="d673f-182">d.</span></span> <span data-ttu-id="d673f-183">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="d673f-183">Click **Create**.</span></span> 


### <a name="creating-a-fuze-test-user"></a><span data-ttu-id="d673f-184">Een testgebruiker Fuze maken</span><span class="sxs-lookup"><span data-stu-id="d673f-184">Creating a Fuze test user</span></span>

<span data-ttu-id="d673f-185">Fuze toepassing ondersteunt volledige Just in tijd gebruiker inrichten, zodat gebruikers automatisch gemaakt wordt wanneer ze aanmelden.</span><span class="sxs-lookup"><span data-stu-id="d673f-185">Fuze application supports full Just in time user provision, so users will get created automatically when they sign-in.</span></span> <span data-ttu-id="d673f-186">Voor alle andere informatie contact op met Fuze [ondersteunen](https://www.fuze.com/support).</span><span class="sxs-lookup"><span data-stu-id="d673f-186">For any other clarification, please contact Fuze [support](https://www.fuze.com/support).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d673f-187">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="d673f-187">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d673f-188">In deze sectie schakelt u Britta Simon Azure eenmalige aanmelding gebruiken door haar toegang verlenen aan Fuze.</span><span class="sxs-lookup"><span data-stu-id="d673f-188">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Fuze.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="d673f-190">**Britta Simon om aan te wijzen Fuze, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="d673f-190">**To assign Britta Simon to Fuze, perform the following steps:**</span></span>

1. <span data-ttu-id="d673f-191">In de Azure-beheerportal, opent u de weergave toepassingen en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="d673f-191">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="d673f-193">Selecteer in de lijst met toepassingen **Fuze**.</span><span class="sxs-lookup"><span data-stu-id="d673f-193">In the applications list, select **Fuze**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_50.png) 

3. <span data-ttu-id="d673f-195">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="d673f-195">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="d673f-197">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="d673f-197">Click **Add** button.</span></span> <span data-ttu-id="d673f-198">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d673f-198">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="d673f-200">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="d673f-200">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d673f-201">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d673f-201">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d673f-202">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d673f-202">Click **Assign** button on **Add Assignment** dialog.</span></span>
    

### <a name="testing-single-sign-on"></a><span data-ttu-id="d673f-203">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="d673f-203">Testing single sign-on</span></span>

<span data-ttu-id="d673f-204">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="d673f-204">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d673f-205">Als u op de tegel Fuze in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Fuze.</span><span class="sxs-lookup"><span data-stu-id="d673f-205">When you click the Fuze tile in the Access Panel, you should get automatically signed-on to your Fuze application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="d673f-206">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="d673f-206">Additional resources</span></span>

* [<span data-ttu-id="d673f-207">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d673f-207">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d673f-208">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d673f-208">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_203.png