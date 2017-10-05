---
title: 'Zelfstudie: Azure Active Directory-integratie met Inkling | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Inkling.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 64c7ee45-ee8a-42f7-bf04-fd0e00833ea9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: jeedes
ms.openlocfilehash: 7b0639c6515298731f88346c2e4ca82664653a2b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-inkling"></a><span data-ttu-id="348a0-103">Zelfstudie: Azure Active Directory-integratie met Inkling</span><span class="sxs-lookup"><span data-stu-id="348a0-103">Tutorial: Azure Active Directory integration with Inkling</span></span>

<span data-ttu-id="348a0-104">In deze zelfstudie leert u hoe Inkling integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="348a0-104">In this tutorial, you learn how to integrate Inkling with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="348a0-105">Inkling integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="348a0-105">Integrating Inkling with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="348a0-106">U kunt beheren in Azure AD die toegang tot Inkling heeft</span><span class="sxs-lookup"><span data-stu-id="348a0-106">You can control in Azure AD who has access to Inkling</span></span>
- <span data-ttu-id="348a0-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Inkling (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="348a0-107">You can enable your users to automatically get signed-on to Inkling (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="348a0-108">U kunt uw accounts op één centrale locatie - en de Azure Management portal beheren</span><span class="sxs-lookup"><span data-stu-id="348a0-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="348a0-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="348a0-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="348a0-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="348a0-110">Prerequisites</span></span>

<span data-ttu-id="348a0-111">Voor het configureren van Azure AD-integratie met Inkling, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="348a0-111">To configure Azure AD integration with Inkling, you need the following items:</span></span>

- <span data-ttu-id="348a0-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="348a0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="348a0-113">Een Inkling eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="348a0-113">An Inkling single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="348a0-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="348a0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="348a0-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="348a0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="348a0-116">U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="348a0-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="348a0-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="348a0-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="348a0-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="348a0-118">Scenario description</span></span>
<span data-ttu-id="348a0-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="348a0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="348a0-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="348a0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="348a0-121">Inkling uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="348a0-121">Adding Inkling from the gallery</span></span>
2. <span data-ttu-id="348a0-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="348a0-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-inkling-from-the-gallery"></a><span data-ttu-id="348a0-123">Inkling uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="348a0-123">Adding Inkling from the gallery</span></span>
<span data-ttu-id="348a0-124">Voor het configureren van de integratie van Inkling in Azure AD, moet u Inkling uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="348a0-124">To configure the integration of Inkling into Azure AD, you need to add Inkling from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="348a0-125">**Als u wilt toevoegen Inkling uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="348a0-125">**To add Inkling from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="348a0-126">In de  **[Azure Management Portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="348a0-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="348a0-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="348a0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="348a0-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="348a0-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="348a0-131">Klik op **toevoegen** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="348a0-131">Click **Add** button on the top of the dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="348a0-133">Typ in het zoekvak **Inkling**.</span><span class="sxs-lookup"><span data-stu-id="348a0-133">In the search box, type **Inkling**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_001.png)

5. <span data-ttu-id="348a0-135">Selecteer in het deelvenster resultaten **Inkling**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="348a0-135">In the results panel, select **Inkling**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="348a0-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="348a0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="348a0-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Inkling op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="348a0-138">In this section, you configure and test Azure AD single sign-on with Inkling based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="348a0-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Inkling is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="348a0-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Inkling is to a user in Azure AD.</span></span> <span data-ttu-id="348a0-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Inkling tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="348a0-140">In other words, a link relationship between an Azure AD user and the related user in Inkling needs to be established.</span></span>

<span data-ttu-id="348a0-141">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in Inkling.</span><span class="sxs-lookup"><span data-stu-id="348a0-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Inkling.</span></span>

<span data-ttu-id="348a0-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Inkling, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="348a0-142">To configure and test Azure AD single sign-on with Inkling, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="348a0-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="348a0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="348a0-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="348a0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="348a0-145">**[Maken van een testgebruiker Inkling](#creating-an-inkling-test-user)**  - Inkling die is gekoppeld aan de Azure AD-representatie van haar van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="348a0-145">**[Creating an Inkling test user](#creating-an-inkling-test-user)** - to have a counterpart of Britta Simon in Inkling that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="348a0-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="348a0-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="348a0-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="348a0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="348a0-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="348a0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="348a0-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure-beheerportal en eenmalige aanmelding in uw toepassing Inkling configureren.</span><span class="sxs-lookup"><span data-stu-id="348a0-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Inkling application.</span></span>

<span data-ttu-id="348a0-150">**Voor het configureren van Azure AD eenmalige aanmelding met Inkling, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="348a0-150">**To configure Azure AD single sign-on with Inkling, perform the following steps:**</span></span>

1. <span data-ttu-id="348a0-151">In de Azure-beheerportal op de **Inkling** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="348a0-151">In the Azure Management portal, on the **Inkling** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="348a0-153">Op de **eenmalige aanmelding** dialoogvenster als **modus** Selecteer **op basis van SAML aanmelding** eenmalige aanmelding inschakelen op.</span><span class="sxs-lookup"><span data-stu-id="348a0-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-inkling-tutorial/tutorial_general_300.png)
    
3. <span data-ttu-id="348a0-155">Op de **Inkling domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="348a0-155">On the **Inkling Domain and URLs** section, perform the following steps:</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_01.png)

    <span data-ttu-id="348a0-157">a.</span><span class="sxs-lookup"><span data-stu-id="348a0-157">a.</span></span> <span data-ttu-id="348a0-158">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://api.inkling.com/saml/v2/metadata/<user-id>`</span><span class="sxs-lookup"><span data-stu-id="348a0-158">In the **Identifier** textbox, type a URL using the following pattern: `https://api.inkling.com/saml/v2/metadata/<user-id>`</span></span>

    <span data-ttu-id="348a0-159">b.</span><span class="sxs-lookup"><span data-stu-id="348a0-159">b.</span></span> <span data-ttu-id="348a0-160">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://api.inkling.com/saml/v2/acs/<user-id>`</span><span class="sxs-lookup"><span data-stu-id="348a0-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://api.inkling.com/saml/v2/acs/<user-id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="348a0-161">Houd er rekening mee dat deze niet de werkelijke waarden zijn.</span><span class="sxs-lookup"><span data-stu-id="348a0-161">Please note that these are not the real values.</span></span> <span data-ttu-id="348a0-162">U hebt deze waarden bijwerken met de werkelijke id en de antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="348a0-162">You have to update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="348a0-163">Neem contact op met [Inkling ondersteuningsteam](mailto:press@inkling.com) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="348a0-163">Contact [Inkling support team](mailto:press@inkling.com) to get these values.</span></span>

4. <span data-ttu-id="348a0-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **nieuw certificaat maken**.</span><span class="sxs-lookup"><span data-stu-id="348a0-164">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-inkling-tutorial/tutorial_general_400.png)    

5. <span data-ttu-id="348a0-166">Op de **nieuw certificaat maken** dialoogvenster, klikt u op het pictogram van de kalender en selecteer een **vervaldatum**.</span><span class="sxs-lookup"><span data-stu-id="348a0-166">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="348a0-167">Klik vervolgens op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="348a0-167">Then click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-inkling-tutorial/tutorial_general_500.png)

6. <span data-ttu-id="348a0-169">Op de **SAML-certificaat voor ondertekening van** sectie **nieuwe certificaat activeren** en klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="348a0-169">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_02.png)

7. <span data-ttu-id="348a0-171">In het pop-upvenster **rollovercertificaat** venster, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="348a0-171">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-inkling-tutorial/tutorial_general_600.png)

8. <span data-ttu-id="348a0-173">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="348a0-173">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_03.png) 

9. <span data-ttu-id="348a0-175">Als u eenmalige aanmelding die zijn geconfigureerd voor uw toepassing, neem contact op met [Inkling ondersteuningsteam](mailto:press@inkling.com) en bieden ze gedownload met **metagegevens**.</span><span class="sxs-lookup"><span data-stu-id="348a0-175">To get SSO configured for your application, contact [Inkling support team](mailto:press@inkling.com) and provide them with downloaded **metadata**.</span></span> 


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="348a0-176">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="348a0-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="348a0-177">Het doel van deze sectie is het een testgebruiker maken in Azure Management portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="348a0-177">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="348a0-179">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="348a0-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="348a0-180">In de **Azure Management portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="348a0-180">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-inkling-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="348a0-182">Ga naar **gebruikers en groepen** en klik op **alle gebruikers** om de lijst met gebruikers weer te geven.</span><span class="sxs-lookup"><span data-stu-id="348a0-182">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-inkling-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="348a0-184">Klik aan de bovenkant van het dialoogvenster **toevoegen** openen de **gebruiker** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="348a0-184">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-inkling-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="348a0-186">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="348a0-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-inkling-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="348a0-188">a.</span><span class="sxs-lookup"><span data-stu-id="348a0-188">a.</span></span> <span data-ttu-id="348a0-189">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="348a0-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="348a0-190">b.</span><span class="sxs-lookup"><span data-stu-id="348a0-190">b.</span></span> <span data-ttu-id="348a0-191">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="348a0-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="348a0-192">c.</span><span class="sxs-lookup"><span data-stu-id="348a0-192">c.</span></span> <span data-ttu-id="348a0-193">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="348a0-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="348a0-194">d.</span><span class="sxs-lookup"><span data-stu-id="348a0-194">d.</span></span> <span data-ttu-id="348a0-195">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="348a0-195">Click **Create**.</span></span> 



### <a name="creating-an-inkling-test-user"></a><span data-ttu-id="348a0-196">Een testgebruiker Inkling maken</span><span class="sxs-lookup"><span data-stu-id="348a0-196">Creating an Inkling test user</span></span>

<span data-ttu-id="348a0-197">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in Inkling maken.</span><span class="sxs-lookup"><span data-stu-id="348a0-197">In this section, you create a user called Britta Simon in Inkling.</span></span> <span data-ttu-id="348a0-198">Neem contact op met [Inkling ondersteuningsteam](mailto:press@inkling.com) de gebruikers van het platform Inkling toevoegen.</span><span class="sxs-lookup"><span data-stu-id="348a0-198">Please work with [Inkling support team](mailto:press@inkling.com) to add the users in the Inkling platform.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="348a0-199">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="348a0-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="348a0-200">In deze sectie schakelt u Britta Simon Azure eenmalige aanmelding gebruiken door haar toegang verlenen aan Inkling.</span><span class="sxs-lookup"><span data-stu-id="348a0-200">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Inkling.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="348a0-202">**Britta Simon om aan te wijzen Inkling, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="348a0-202">**To assign Britta Simon to Inkling, perform the following steps:**</span></span>

1. <span data-ttu-id="348a0-203">In de Azure-beheerportal, opent u de weergave toepassingen en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="348a0-203">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="348a0-205">Selecteer in de lijst met toepassingen **Inkling**.</span><span class="sxs-lookup"><span data-stu-id="348a0-205">In the applications list, select **Inkling**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_50.png) 

3. <span data-ttu-id="348a0-207">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="348a0-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="348a0-209">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="348a0-209">Click **Add** button.</span></span> <span data-ttu-id="348a0-210">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="348a0-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="348a0-212">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="348a0-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="348a0-213">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="348a0-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="348a0-214">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="348a0-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="348a0-215">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="348a0-215">Testing single sign-on</span></span>

<span data-ttu-id="348a0-216">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="348a0-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="348a0-217">Als u op de tegel Inkling in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Inkling.</span><span class="sxs-lookup"><span data-stu-id="348a0-217">When you click the Inkling tile in the Access Panel, you should get automatically signed-on to your Inkling application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="348a0-218">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="348a0-218">Additional resources</span></span>

* [<span data-ttu-id="348a0-219">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="348a0-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="348a0-220">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="348a0-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_203.png