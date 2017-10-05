---
title: 'Zelfstudie: Azure Active Directory-integratie met 15Five | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en 15Five.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2fb301c2-7d7a-4046-8ee1-7dc9e7684806
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: ea36774747a0fcfa4ace1aefb2d46dba815d92c4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-15five"></a><span data-ttu-id="05e45-103">Zelfstudie: Azure Active Directory-integratie met 15Five</span><span class="sxs-lookup"><span data-stu-id="05e45-103">Tutorial: Azure Active Directory integration with 15Five</span></span>

<span data-ttu-id="05e45-104">In deze zelfstudie leert u hoe 15Five integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="05e45-104">In this tutorial, you learn how to integrate 15Five with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="05e45-105">15Five integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="05e45-105">Integrating 15Five with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="05e45-106">U kunt beheren in Azure AD die toegang tot 15Five heeft</span><span class="sxs-lookup"><span data-stu-id="05e45-106">You can control in Azure AD who has access to 15Five</span></span>
- <span data-ttu-id="05e45-107">U kunt uw gebruikers automatisch ophalen aangemeld bij 15Five inschakelen (Single Sign-On) met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="05e45-107">You can enable your users to automatically get signed-on to 15Five (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="05e45-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="05e45-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="05e45-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="05e45-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="05e45-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="05e45-110">Prerequisites</span></span>

<span data-ttu-id="05e45-111">Voor het configureren van Azure AD-integratie met 15Five, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="05e45-111">To configure Azure AD integration with 15Five, you need the following items:</span></span>

- <span data-ttu-id="05e45-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="05e45-112">An Azure AD subscription</span></span>
- <span data-ttu-id="05e45-113">Een 15Five eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="05e45-113">A 15Five single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="05e45-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="05e45-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="05e45-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="05e45-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="05e45-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="05e45-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="05e45-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="05e45-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="05e45-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="05e45-118">Scenario description</span></span>
<span data-ttu-id="05e45-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="05e45-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="05e45-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="05e45-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="05e45-121">15Five uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="05e45-121">Adding 15Five from the gallery</span></span>
2. <span data-ttu-id="05e45-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="05e45-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-15five-from-the-gallery"></a><span data-ttu-id="05e45-123">15Five uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="05e45-123">Adding 15Five from the gallery</span></span>
<span data-ttu-id="05e45-124">Voor het configureren van de integratie van 15Five in Azure AD, moet u 15Five uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="05e45-124">To configure the integration of 15Five into Azure AD, you need to add 15Five from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="05e45-125">**Als u wilt toevoegen 15Five uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="05e45-125">**To add 15Five from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="05e45-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="05e45-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="05e45-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="05e45-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="05e45-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="05e45-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="05e45-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="05e45-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="05e45-133">Typ in het zoekvak **15Five**.</span><span class="sxs-lookup"><span data-stu-id="05e45-133">In the search box, type **15Five**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-15five-tutorial/tutorial_15five_search.png)

5. <span data-ttu-id="05e45-135">Selecteer in het deelvenster resultaten **15Five**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="05e45-135">In the results panel, select **15Five**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-15five-tutorial/tutorial_15five_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="05e45-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="05e45-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="05e45-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met 15Five op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="05e45-138">In this section, you configure and test Azure AD single sign-on with 15Five based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="05e45-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in 15Five is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="05e45-139">For single sign-on to work, Azure AD needs to know what the counterpart user in 15Five is to a user in Azure AD.</span></span> <span data-ttu-id="05e45-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in 15Five tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="05e45-140">In other words, a link relationship between an Azure AD user and the related user in 15Five needs to be established.</span></span>

<span data-ttu-id="05e45-141">Wijs in 15Five, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="05e45-141">In 15Five, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="05e45-142">Om te configureren en testen van Azure AD eenmalige aanmelding met 15Five, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="05e45-142">To configure and test Azure AD single sign-on with 15Five, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="05e45-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="05e45-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="05e45-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="05e45-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="05e45-145">**[Maken van een testgebruiker 15Five](#creating-a-15five-test-user)**  - hebben een equivalent van Britta Simon in 15Five die is gekoppeld aan de Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="05e45-145">**[Creating a 15Five test user](#creating-a-15five-test-user)** - to have a counterpart of Britta Simon in 15Five that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="05e45-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="05e45-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="05e45-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="05e45-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="05e45-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="05e45-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="05e45-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing 15Five configureren.</span><span class="sxs-lookup"><span data-stu-id="05e45-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your 15Five application.</span></span>

<span data-ttu-id="05e45-150">**Voor het configureren van Azure AD eenmalige aanmelding met 15Five, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="05e45-150">**To configure Azure AD single sign-on with 15Five, perform the following steps:**</span></span>

1. <span data-ttu-id="05e45-151">In de Azure-portal op de **15Five** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="05e45-151">In the Azure portal, on the **15Five** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="05e45-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="05e45-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-15five-tutorial/tutorial_15five_samlbase.png)

3. <span data-ttu-id="05e45-155">Op de **15Five domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="05e45-155">On the **15Five Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-15five-tutorial/tutorial_15five_url.png)

    <span data-ttu-id="05e45-157">a.</span><span class="sxs-lookup"><span data-stu-id="05e45-157">a.</span></span> <span data-ttu-id="05e45-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<companyname>.15five.com`</span><span class="sxs-lookup"><span data-stu-id="05e45-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.15five.com`</span></span>

    <span data-ttu-id="05e45-159">b.</span><span class="sxs-lookup"><span data-stu-id="05e45-159">b.</span></span> <span data-ttu-id="05e45-160">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<companyname>.15five.com/saml2/metadata/`</span><span class="sxs-lookup"><span data-stu-id="05e45-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.15five.com/saml2/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="05e45-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="05e45-161">These values are not real.</span></span> <span data-ttu-id="05e45-162">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="05e45-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="05e45-163">Neem contact op met [15Five Client ondersteuningsteam](https://www.15five.com/contact/) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="05e45-163">Contact [15Five Client support team](https://www.15five.com/contact/) to get these values.</span></span> 
 
4. <span data-ttu-id="05e45-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="05e45-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-15five-tutorial/tutorial_15five_certificate.png) 

5. <span data-ttu-id="05e45-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="05e45-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-15five-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="05e45-168">Eenmalige aanmelding configureren op **15Five** zijde, moet u de gedownloade verzenden **Metadata XML** naar [15Five ondersteuningsteam](https://www.15five.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="05e45-168">To configure single sign-on on **15Five** side, you need to send the downloaded **Metadata XML** to [15Five support team](https://www.15five.com/contact/).</span></span>

> [!TIP]
> <span data-ttu-id="05e45-169">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="05e45-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="05e45-170">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="05e45-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="05e45-171">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="05e45-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="05e45-172">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="05e45-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="05e45-173">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="05e45-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="05e45-175">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="05e45-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="05e45-176">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="05e45-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-15five-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="05e45-178">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="05e45-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-15five-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="05e45-180">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="05e45-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-15five-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="05e45-182">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="05e45-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-15five-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="05e45-184">a.</span><span class="sxs-lookup"><span data-stu-id="05e45-184">a.</span></span> <span data-ttu-id="05e45-185">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="05e45-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="05e45-186">b.</span><span class="sxs-lookup"><span data-stu-id="05e45-186">b.</span></span> <span data-ttu-id="05e45-187">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="05e45-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="05e45-188">c.</span><span class="sxs-lookup"><span data-stu-id="05e45-188">c.</span></span> <span data-ttu-id="05e45-189">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="05e45-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="05e45-190">d.</span><span class="sxs-lookup"><span data-stu-id="05e45-190">d.</span></span> <span data-ttu-id="05e45-191">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="05e45-191">Click **Create**.</span></span>
 
### <a name="creating-a-15five-test-user"></a><span data-ttu-id="05e45-192">Een testgebruiker 15Five maken</span><span class="sxs-lookup"><span data-stu-id="05e45-192">Creating a 15Five test user</span></span>

<span data-ttu-id="05e45-193">Om Azure AD-gebruikers zich aanmelden bij 15Five, moeten ze worden ingericht in 15Five.</span><span class="sxs-lookup"><span data-stu-id="05e45-193">To enable Azure AD users to log in to 15Five, they must be provisioned into 15Five.</span></span> <span data-ttu-id="05e45-194">Wanneer 15Five, inrichting is een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="05e45-194">When 15Five, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="05e45-195">Als u wilt configureren voor gebruikers inrichten, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="05e45-195">To configure user provisioning, perform the following steps:</span></span>
1. <span data-ttu-id="05e45-196">Meld u aan bij uw **15Five** bedrijf site als administrator.</span><span class="sxs-lookup"><span data-stu-id="05e45-196">Log in to your **15Five** company site as administrator.</span></span>

2. <span data-ttu-id="05e45-197">Ga naar **bedrijf beheren**.</span><span class="sxs-lookup"><span data-stu-id="05e45-197">Go to **Manage Company**.</span></span>
   
    <span data-ttu-id="05e45-198">![Bedrijf beheren](./media/active-directory-saas-15five-tutorial/IC784675.png "bedrijf beheren")</span><span class="sxs-lookup"><span data-stu-id="05e45-198">![Manage Company](./media/active-directory-saas-15five-tutorial/IC784675.png "Manage Company")</span></span>

3. <span data-ttu-id="05e45-199">Ga naar **mensen \> personen toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="05e45-199">Go to **People \> Add People**.</span></span>
   
    <span data-ttu-id="05e45-200">![Mensen](./media/active-directory-saas-15five-tutorial/IC784676.png "personen")</span><span class="sxs-lookup"><span data-stu-id="05e45-200">![People](./media/active-directory-saas-15five-tutorial/IC784676.png "People")</span></span>

4. <span data-ttu-id="05e45-201">Voer de volgende stappen uit in de sectie nieuwe persoon toevoegen:</span><span class="sxs-lookup"><span data-stu-id="05e45-201">In the Add New Person section, perform the following steps:</span></span>
   
    <span data-ttu-id="05e45-202">![Toevoegen van nieuwe persoon](./media/active-directory-saas-15five-tutorial/IC784677.png "nieuwe persoon toevoegen")</span><span class="sxs-lookup"><span data-stu-id="05e45-202">![Add New Person](./media/active-directory-saas-15five-tutorial/IC784677.png "Add New Person")</span></span>
   
    <span data-ttu-id="05e45-203">a.</span><span class="sxs-lookup"><span data-stu-id="05e45-203">a.</span></span> <span data-ttu-id="05e45-204">Typ de **voornaam**, **achternaam**, **titel**, **e-mailadres** van een geldige Azure Active Directory-account dat u inrichten wilt in de verwante tekstvakken.</span><span class="sxs-lookup"><span data-stu-id="05e45-204">Type the **First Name**, **Last Name**, **Title**, **Email address** of a valid Azure Active Directory account you want to provision into the related textboxes.</span></span>

    <span data-ttu-id="05e45-205">b.</span><span class="sxs-lookup"><span data-stu-id="05e45-205">b.</span></span> <span data-ttu-id="05e45-206">Klik op **Gereed**.</span><span class="sxs-lookup"><span data-stu-id="05e45-206">Click **Done**.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="05e45-207">De accounthouder Azure AD ontvangt een e-mailbericht met inbegrip van een koppeling om te bevestigen van het account voordat deze geactiveerd wordt.</span><span class="sxs-lookup"><span data-stu-id="05e45-207">The Azure AD account holder receives an email including a link to confirm the account before it becomes active.</span></span>
   
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="05e45-208">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="05e45-208">Assigning the Azure AD test user</span></span>

<span data-ttu-id="05e45-209">In deze sectie schakelt u Britta Simon Azure eenmalige aanmelding gebruiken door het verlenen van toegang tot 15Five.</span><span class="sxs-lookup"><span data-stu-id="05e45-209">In this section, you enable Britta Simon to use Azure single sign-on by granting access to 15Five.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="05e45-211">**Britta Simon om aan te wijzen 15Five, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="05e45-211">**To assign Britta Simon to 15Five, perform the following steps:**</span></span>

1. <span data-ttu-id="05e45-212">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="05e45-212">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="05e45-214">Selecteer in de lijst met toepassingen **15Five**.</span><span class="sxs-lookup"><span data-stu-id="05e45-214">In the applications list, select **15Five**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-15five-tutorial/tutorial_15five_app.png) 

3. <span data-ttu-id="05e45-216">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="05e45-216">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="05e45-218">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="05e45-218">Click **Add** button.</span></span> <span data-ttu-id="05e45-219">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="05e45-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="05e45-221">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="05e45-221">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="05e45-222">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="05e45-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="05e45-223">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="05e45-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="05e45-224">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="05e45-224">Testing single sign-on</span></span>

<span data-ttu-id="05e45-225">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="05e45-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="05e45-226">Als u op de tegel 15Five in het deelvenster toegang, krijgt u de aanmeldingspagina van 15Five toepassing.</span><span class="sxs-lookup"><span data-stu-id="05e45-226">When you click the 15Five tile in the Access Panel, you should get login page of 15Five application.</span></span>
<span data-ttu-id="05e45-227">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="05e45-227">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="05e45-228">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="05e45-228">Additional resources</span></span>

* [<span data-ttu-id="05e45-229">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="05e45-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="05e45-230">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="05e45-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-15five-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-15five-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-15five-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-15five-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-15five-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-15five-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-15five-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-15five-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-15five-tutorial/tutorial_general_203.png

