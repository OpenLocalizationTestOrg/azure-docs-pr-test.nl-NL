---
title: 'Zelfstudie: Azure Active Directory-integratie met BGS Online | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding van Azure Active Directory en BGS Online.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4fd6b29b-1b46-4fd1-9f5e-16b1c9d892cd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: d1abd3f8e2980e03fc092613183a261880fbce38
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bgs-online"></a><span data-ttu-id="062cc-103">Zelfstudie: Azure Active Directory-integratie met BGS Online</span><span class="sxs-lookup"><span data-stu-id="062cc-103">Tutorial: Azure Active Directory integration with BGS Online</span></span>

<span data-ttu-id="062cc-104">In deze zelfstudie leert u hoe BGS Online integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="062cc-104">In this tutorial, you learn how to integrate BGS Online with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="062cc-105">Online BGS integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="062cc-105">Integrating BGS Online with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="062cc-106">U kunt beheren in Azure AD die toegang tot BGS Online heeft</span><span class="sxs-lookup"><span data-stu-id="062cc-106">You can control in Azure AD who has access to BGS Online</span></span>
- <span data-ttu-id="062cc-107">U kunt uw gebruikers automatisch ophalen aangemeld bij BGS Online (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="062cc-107">You can enable your users to automatically get signed-on to BGS Online (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="062cc-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="062cc-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="062cc-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="062cc-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="062cc-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="062cc-110">Prerequisites</span></span>

<span data-ttu-id="062cc-111">Voor het configureren van Azure AD-integratie met BGS Online, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="062cc-111">To configure Azure AD integration with BGS Online, you need the following items:</span></span>

- <span data-ttu-id="062cc-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="062cc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="062cc-113">Een BGS Online eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="062cc-113">A BGS Online single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="062cc-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="062cc-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="062cc-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="062cc-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="062cc-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="062cc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="062cc-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="062cc-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="062cc-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="062cc-118">Scenario description</span></span>
<span data-ttu-id="062cc-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="062cc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="062cc-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="062cc-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="062cc-121">Toevoegen van Online BGS uit de galerie</span><span class="sxs-lookup"><span data-stu-id="062cc-121">Adding BGS Online from the gallery</span></span>
2. <span data-ttu-id="062cc-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="062cc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bgs-online-from-the-gallery"></a><span data-ttu-id="062cc-123">Toevoegen van Online BGS uit de galerie</span><span class="sxs-lookup"><span data-stu-id="062cc-123">Adding BGS Online from the gallery</span></span>
<span data-ttu-id="062cc-124">Voor het configureren van de integratie van BGS Online in Azure AD, moet u BGS Online uit de galerie toevoegt aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="062cc-124">To configure the integration of BGS Online into Azure AD, you need to add BGS Online from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="062cc-125">**Als u wilt toevoegen in de galerie BGS Online, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="062cc-125">**To add BGS Online from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="062cc-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="062cc-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="062cc-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="062cc-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="062cc-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="062cc-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="062cc-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="062cc-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="062cc-133">Typ in het zoekvak **BGS Online**.</span><span class="sxs-lookup"><span data-stu-id="062cc-133">In the search box, type **BGS Online**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_search.png)

5. <span data-ttu-id="062cc-135">Selecteer in het deelvenster resultaten **BGS Online**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="062cc-135">In the results panel, select **BGS Online**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="062cc-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="062cc-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="062cc-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met BGS Online op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="062cc-138">In this section, you configure and test Azure AD single sign-on with BGS Online based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="062cc-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in BGS Online is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="062cc-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BGS Online is to a user in Azure AD.</span></span> <span data-ttu-id="062cc-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker BGS online worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="062cc-140">In other words, a link relationship between an Azure AD user and the related user in BGS Online needs to be established.</span></span>

<span data-ttu-id="062cc-141">In Online BGS, wijs de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="062cc-141">In BGS Online, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="062cc-142">Om te configureren en testen van Azure AD eenmalige aanmelding met BGS Online, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="062cc-142">To configure and test Azure AD single sign-on with BGS Online, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="062cc-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="062cc-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="062cc-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="062cc-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="062cc-145">**[Maken van een Online BGS testgebruiker](#creating-a-bgs-online-test-user)**  - bevatten een equivalent van Britta Simon BGS Online die is gekoppeld aan de Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="062cc-145">**[Creating a BGS Online test user](#creating-a-bgs-online-test-user)** - to have a counterpart of Britta Simon in BGS Online that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="062cc-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="062cc-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="062cc-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="062cc-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="062cc-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="062cc-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="062cc-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing BGS Online configureren.</span><span class="sxs-lookup"><span data-stu-id="062cc-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BGS Online application.</span></span>

<span data-ttu-id="062cc-150">**Voor het configureren van Azure AD eenmalige aanmelding met BGS Online, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="062cc-150">**To configure Azure AD single sign-on with BGS Online, perform the following steps:**</span></span>

1. <span data-ttu-id="062cc-151">In de Azure-portal op de **BGS Online** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="062cc-151">In the Azure portal, on the **BGS Online** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="062cc-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="062cc-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_samlbase.png)

3. <span data-ttu-id="062cc-155">Op de **BGS Online domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="062cc-155">On the **BGS Online Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_url.png)

    <span data-ttu-id="062cc-157">a.</span><span class="sxs-lookup"><span data-stu-id="062cc-157">a.</span></span> <span data-ttu-id="062cc-158">In de **id** textbox, typ een URL met het volgende patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="062cc-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>

    <span data-ttu-id="062cc-159">Gebruik dit patroon voor productie-omgeving.`https://<company name>.millwardbrown.report`</span><span class="sxs-lookup"><span data-stu-id="062cc-159">For production environment, use this pattern `https://<company name>.millwardbrown.report`</span></span> 

    <span data-ttu-id="062cc-160">Gebruik dit patroon voor de testomgeving`https://millwardbrown.marketingtracker.nl/mt5/`</span><span class="sxs-lookup"><span data-stu-id="062cc-160">For test environment, use this pattern `https://millwardbrown.marketingtracker.nl/mt5/`</span></span>

    <span data-ttu-id="062cc-161">b.</span><span class="sxs-lookup"><span data-stu-id="062cc-161">b.</span></span> <span data-ttu-id="062cc-162">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="062cc-162">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>
    
    <span data-ttu-id="062cc-163">Gebruik dit patroon voor productie-omgeving.`https://<company name>.millwardbrown.report/sso/saml/AssertionConsumerService.aspx`</span><span class="sxs-lookup"><span data-stu-id="062cc-163">For production environment, use this pattern `https://<company name>.millwardbrown.report/sso/saml/AssertionConsumerService.aspx`</span></span> 
      
    <span data-ttu-id="062cc-164">Gebruik dit patroon voor de testomgeving`https://millwardbrown.marketingtracker.nl/mt5/sso/saml/AssertionConsumerService.aspx`</span><span class="sxs-lookup"><span data-stu-id="062cc-164">For test environment, use this pattern `https://millwardbrown.marketingtracker.nl/mt5/sso/saml/AssertionConsumerService.aspx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="062cc-165">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="062cc-165">These values are not real.</span></span> <span data-ttu-id="062cc-166">Deze waarden bijwerken met de werkelijke id en de antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="062cc-166">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="062cc-167">Neem contact op met [BGS Online ondersteuningsteam](mailTo:bgsdashboardteam@millwardbrown.com) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="062cc-167">Contact [BGS Online support team](mailTo:bgsdashboardteam@millwardbrown.com) to get these values.</span></span>
 

4. <span data-ttu-id="062cc-168">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="062cc-168">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_certificate.png) 

5. <span data-ttu-id="062cc-170">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="062cc-170">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bgsonline-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="062cc-172">Op de **BGS Online configuratie** sectie, klikt u op **BGS Online configureren** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="062cc-172">On the **BGS Online Configuration** section, click **Configure BGS Online** to open **Configure sign-on** window.</span></span> <span data-ttu-id="062cc-173">Kopieer de **SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="062cc-173">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_configure.png) 

7. <span data-ttu-id="062cc-175">Eenmalige aanmelding configureren op **BGS Online** zijde, moet u de gedownloade verzenden **Metadata XML** en **SAML Single Sign-On Service-URL** naar [BGS Online ondersteuningsteam](mailto:bgsdashboardteam@millwardbrown.com).</span><span class="sxs-lookup"><span data-stu-id="062cc-175">To configure single sign-on on **BGS Online** side, you need to send the downloaded **Metadata XML** and **SAML Single Sign-On Service URL** to [BGS Online support team](mailto:bgsdashboardteam@millwardbrown.com).</span></span> 


> [!TIP]
> <span data-ttu-id="062cc-176">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="062cc-176">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="062cc-177">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="062cc-177">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="062cc-178">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="062cc-178">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="062cc-179">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="062cc-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="062cc-180">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="062cc-180">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="062cc-182">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="062cc-182">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="062cc-183">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="062cc-183">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bgsonline-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="062cc-185">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="062cc-185">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bgsonline-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="062cc-187">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="062cc-187">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bgsonline-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="062cc-189">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="062cc-189">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bgsonline-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="062cc-191">a.</span><span class="sxs-lookup"><span data-stu-id="062cc-191">a.</span></span> <span data-ttu-id="062cc-192">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="062cc-192">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="062cc-193">b.</span><span class="sxs-lookup"><span data-stu-id="062cc-193">b.</span></span> <span data-ttu-id="062cc-194">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="062cc-194">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="062cc-195">c.</span><span class="sxs-lookup"><span data-stu-id="062cc-195">c.</span></span> <span data-ttu-id="062cc-196">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="062cc-196">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="062cc-197">d.</span><span class="sxs-lookup"><span data-stu-id="062cc-197">d.</span></span> <span data-ttu-id="062cc-198">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="062cc-198">Click **Create**.</span></span>
 
### <a name="creating-a-bgs-online-test-user"></a><span data-ttu-id="062cc-199">Maken van een Online BGS testgebruiker</span><span class="sxs-lookup"><span data-stu-id="062cc-199">Creating a BGS Online test user</span></span>

<span data-ttu-id="062cc-200">In deze sectie maakt maken u een gebruiker die is aangeroepen terwijl Britta Simon BGS Online.</span><span class="sxs-lookup"><span data-stu-id="062cc-200">In this section, you create a user called Britta Simon in BGS Online.</span></span> <span data-ttu-id="062cc-201">Werken met [BGS Online ondersteuningsteam](mailto:bgsdashboardteam@millwardbrown.com) toevoegen van de gebruikers in het Online BGS platform.</span><span class="sxs-lookup"><span data-stu-id="062cc-201">Work with [BGS Online support team](mailto:bgsdashboardteam@millwardbrown.com) to add the users in the BGS Online platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="062cc-202">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="062cc-202">Assigning the Azure AD test user</span></span>

<span data-ttu-id="062cc-203">In deze sectie maakt inschakelen u Britta Simon gebruiken Azure eenmalige aanmelding toegang verleent tot BGS Online.</span><span class="sxs-lookup"><span data-stu-id="062cc-203">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BGS Online.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="062cc-205">**Britta Simon om aan te wijzen BGS Online, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="062cc-205">**To assign Britta Simon to BGS Online, perform the following steps:**</span></span>

1. <span data-ttu-id="062cc-206">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="062cc-206">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="062cc-208">Selecteer in de lijst met toepassingen **BGS Online**.</span><span class="sxs-lookup"><span data-stu-id="062cc-208">In the applications list, select **BGS Online**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_app.png) 

3. <span data-ttu-id="062cc-210">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="062cc-210">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="062cc-212">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="062cc-212">Click **Add** button.</span></span> <span data-ttu-id="062cc-213">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="062cc-213">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="062cc-215">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="062cc-215">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="062cc-216">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="062cc-216">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="062cc-217">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="062cc-217">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="062cc-218">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="062cc-218">Testing single sign-on</span></span>

<span data-ttu-id="062cc-219">In deze sectie kunt u uw Azure AD SSO-configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="062cc-219">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="062cc-220">Als u op de tegel BGS Online in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw BGS Online-toepassing.</span><span class="sxs-lookup"><span data-stu-id="062cc-220">When you click the BGS Online tile in the Access Panel, you should get automatically signed-on to your BGS Online application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="062cc-221">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="062cc-221">Additional resources</span></span>

* [<span data-ttu-id="062cc-222">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="062cc-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="062cc-223">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="062cc-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_203.png

