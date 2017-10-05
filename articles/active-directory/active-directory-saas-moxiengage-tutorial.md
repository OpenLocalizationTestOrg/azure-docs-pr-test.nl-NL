---
title: 'Zelfstudie: Azure Active Directory-integratie met Moxi benaderen | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Moxi benaderen.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1135a879-8f00-43b0-ac8a-831593d9586d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jeedes
ms.openlocfilehash: 25b5e377d8d0d504860ab9a8c4dac49c9ca5b104
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-moxi-engage"></a><span data-ttu-id="82ea3-103">Zelfstudie: Azure Active Directory-integratie met Moxi benaderen</span><span class="sxs-lookup"><span data-stu-id="82ea3-103">Tutorial: Azure Active Directory integration with Moxi Engage</span></span>

<span data-ttu-id="82ea3-104">In deze zelfstudie leert u hoe Moxi benaderen integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="82ea3-104">In this tutorial, you learn how to integrate Moxi Engage with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="82ea3-105">Moxi benaderen integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="82ea3-105">Integrating Moxi Engage with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="82ea3-106">U kunt beheren in Azure AD die toegang tot Moxi benaderen heeft</span><span class="sxs-lookup"><span data-stu-id="82ea3-106">You can control in Azure AD who has access to Moxi Engage</span></span>
- <span data-ttu-id="82ea3-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Moxi benaderen (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="82ea3-107">You can enable your users to automatically get signed-on to Moxi Engage (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="82ea3-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="82ea3-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="82ea3-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="82ea3-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="82ea3-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="82ea3-110">Prerequisites</span></span>

<span data-ttu-id="82ea3-111">Voor het configureren van Azure AD-integratie met Moxi benaderen, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="82ea3-111">To configure Azure AD integration with Moxi Engage, you need the following items:</span></span>

- <span data-ttu-id="82ea3-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="82ea3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="82ea3-113">Een Moxi benaderen eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="82ea3-113">A Moxi Engage single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="82ea3-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="82ea3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="82ea3-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="82ea3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="82ea3-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="82ea3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="82ea3-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="82ea3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="82ea3-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="82ea3-118">Scenario description</span></span>
<span data-ttu-id="82ea3-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="82ea3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="82ea3-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="82ea3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="82ea3-121">Toe te voegen Moxi benaderen uit de galerie</span><span class="sxs-lookup"><span data-stu-id="82ea3-121">Adding Moxi Engage from the gallery</span></span>
2. <span data-ttu-id="82ea3-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="82ea3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-moxi-engage-from-the-gallery"></a><span data-ttu-id="82ea3-123">Toe te voegen Moxi benaderen uit de galerie</span><span class="sxs-lookup"><span data-stu-id="82ea3-123">Adding Moxi Engage from the gallery</span></span>
<span data-ttu-id="82ea3-124">Voor het configureren van de integratie van Moxi benaderen in Azure AD, moet u Moxi benaderen toevoegen uit de galerie aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="82ea3-124">To configure the integration of Moxi Engage into Azure AD, you need to add Moxi Engage from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="82ea3-125">**Als u wilt toevoegen Moxi benaderen uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="82ea3-125">**To add Moxi Engage from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="82ea3-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="82ea3-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="82ea3-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="82ea3-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="82ea3-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="82ea3-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="82ea3-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="82ea3-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="82ea3-133">Typ in het zoekvak **Moxi benaderen**.</span><span class="sxs-lookup"><span data-stu-id="82ea3-133">In the search box, type **Moxi Engage**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-moxiengage-tutorial/tutorial_moxiengage_search.png)

5. <span data-ttu-id="82ea3-135">Selecteer in het deelvenster resultaten **Moxi benaderen**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="82ea3-135">In the results panel, select **Moxi Engage**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-moxiengage-tutorial/tutorial_moxiengage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="82ea3-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="82ea3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="82ea3-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Moxi benaderen op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="82ea3-138">In this section, you configure and test Azure AD single sign-on with Moxi Engage based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="82ea3-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Moxi benaderen is aan een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="82ea3-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Moxi Engage is to a user in Azure AD.</span></span> <span data-ttu-id="82ea3-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Moxi benaderen tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="82ea3-140">In other words, a link relationship between an Azure AD user and the related user in Moxi Engage needs to be established.</span></span>

<span data-ttu-id="82ea3-141">Wijs in het Moxi benaderen, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="82ea3-141">In Moxi Engage, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="82ea3-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Moxi benaderen, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="82ea3-142">To configure and test Azure AD single sign-on with Moxi Engage, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="82ea3-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="82ea3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="82ea3-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="82ea3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="82ea3-145">**[Maken van een testgebruiker Moxi benaderen](#creating-a-moxi-engage-test-user)**  - Moxi benaderen die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="82ea3-145">**[Creating a Moxi Engage test user](#creating-a-moxi-engage-test-user)** - to have a counterpart of Britta Simon in Moxi Engage that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="82ea3-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="82ea3-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="82ea3-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="82ea3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="82ea3-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="82ea3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="82ea3-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw toepassing Moxi benaderen.</span><span class="sxs-lookup"><span data-stu-id="82ea3-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Moxi Engage application.</span></span>

<span data-ttu-id="82ea3-150">**Voor het configureren van Azure AD eenmalige aanmelding met Moxi benaderen, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="82ea3-150">**To configure Azure AD single sign-on with Moxi Engage, perform the following steps:**</span></span>

1. <span data-ttu-id="82ea3-151">In de Azure-portal op de **Moxi benaderen** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="82ea3-151">In the Azure portal, on the **Moxi Engage** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="82ea3-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="82ea3-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-moxiengage-tutorial/tutorial_moxiengage_samlbase.png)

3. <span data-ttu-id="82ea3-155">Op de **Moxi benaderen domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="82ea3-155">On the **Moxi Engage Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-moxiengage-tutorial/tutorial_moxiengage_url.png)

    <span data-ttu-id="82ea3-157">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://svc.<moxiworks-integration-domain>/service/v1/auth/inbound/saml/aad`</span><span class="sxs-lookup"><span data-stu-id="82ea3-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://svc.<moxiworks-integration-domain>/service/v1/auth/inbound/saml/aad`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="82ea3-158">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="82ea3-158">This value is not real.</span></span> <span data-ttu-id="82ea3-159">Deze waarde bijwerken met de werkelijke URL voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="82ea3-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="82ea3-160">Neem contact op met [Moxi benaderen Client ondersteuningsteam](mailto:support@moxiworks.com) deze waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="82ea3-160">Contact [Moxi Engage Client support team](mailto:support@moxiworks.com) to get this value.</span></span> 
 
4. <span data-ttu-id="82ea3-161">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="82ea3-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-moxiengage-tutorial/tutorial_moxiengage_certificate.png) 

5. <span data-ttu-id="82ea3-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="82ea3-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-moxiengage-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="82ea3-165">Eenmalige aanmelding configureren op **Moxi benaderen** zijde, moet u de gedownloade verzenden **Metadata XML** naar [ondersteuningsteam Moxi benaderen](mailto:support@moxiworks.com).</span><span class="sxs-lookup"><span data-stu-id="82ea3-165">To configure single sign-on on **Moxi Engage** side, you need to send the downloaded **Metadata XML** to [Moxi Engage support team](mailto:support@moxiworks.com).</span></span> <span data-ttu-id="82ea3-166">Ze deze instelling zodat de SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="82ea3-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="82ea3-167">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="82ea3-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="82ea3-168">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="82ea3-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="82ea3-169">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="82ea3-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="82ea3-170">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="82ea3-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="82ea3-171">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="82ea3-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="82ea3-173">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="82ea3-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="82ea3-174">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="82ea3-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-moxiengage-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="82ea3-176">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="82ea3-176">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-moxiengage-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="82ea3-178">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="82ea3-178">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-moxiengage-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="82ea3-180">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="82ea3-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-moxiengage-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="82ea3-182">a.</span><span class="sxs-lookup"><span data-stu-id="82ea3-182">a.</span></span> <span data-ttu-id="82ea3-183">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="82ea3-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="82ea3-184">b.</span><span class="sxs-lookup"><span data-stu-id="82ea3-184">b.</span></span> <span data-ttu-id="82ea3-185">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="82ea3-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="82ea3-186">c.</span><span class="sxs-lookup"><span data-stu-id="82ea3-186">c.</span></span> <span data-ttu-id="82ea3-187">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="82ea3-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="82ea3-188">d.</span><span class="sxs-lookup"><span data-stu-id="82ea3-188">d.</span></span> <span data-ttu-id="82ea3-189">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="82ea3-189">Click **Create**.</span></span>
 
### <a name="creating-a-moxi-engage-test-user"></a><span data-ttu-id="82ea3-190">Maken van een testgebruiker Moxi benaderen</span><span class="sxs-lookup"><span data-stu-id="82ea3-190">Creating a Moxi Engage test user</span></span>

<span data-ttu-id="82ea3-191">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in het benaderen van Moxi maken.</span><span class="sxs-lookup"><span data-stu-id="82ea3-191">In this section, you create a user called Britta Simon in Moxi Engage.</span></span> <span data-ttu-id="82ea3-192">Werken met [ondersteuningsteam Moxi benaderen](mailto:support@moxiworks.com) om toe te voegen de gebruikers van het platform Moxi benaderen.</span><span class="sxs-lookup"><span data-stu-id="82ea3-192">Work with [Moxi Engage support team](mailto:support@moxiworks.com) to add the users in the Moxi Engage platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="82ea3-193">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="82ea3-193">Assigning the Azure AD test user</span></span>

<span data-ttu-id="82ea3-194">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen Moxi benaderen.</span><span class="sxs-lookup"><span data-stu-id="82ea3-194">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Moxi Engage.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="82ea3-196">**Als u wilt toewijzen Britta Simon Moxi bezighouden, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="82ea3-196">**To assign Britta Simon to Moxi Engage, perform the following steps:**</span></span>

1. <span data-ttu-id="82ea3-197">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="82ea3-197">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="82ea3-199">Selecteer in de lijst met toepassingen **Moxi benaderen**.</span><span class="sxs-lookup"><span data-stu-id="82ea3-199">In the applications list, select **Moxi Engage**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-moxiengage-tutorial/tutorial_moxiengage_app.png) 

3. <span data-ttu-id="82ea3-201">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="82ea3-201">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="82ea3-203">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="82ea3-203">Click **Add** button.</span></span> <span data-ttu-id="82ea3-204">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="82ea3-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="82ea3-206">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="82ea3-206">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="82ea3-207">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="82ea3-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="82ea3-208">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="82ea3-208">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="82ea3-209">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="82ea3-209">Testing single sign-on</span></span>

<span data-ttu-id="82ea3-210">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="82ea3-210">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="82ea3-211">Als u op de tegel Moxi benaderen in het deelvenster toegang, krijgt u automatische aanmelding bij de toepassing Moxi benaderen.</span><span class="sxs-lookup"><span data-stu-id="82ea3-211">When you click the Moxi Engage tile in the Access Panel, you should get automatic login to Moxi Engage application.</span></span>
<span data-ttu-id="82ea3-212">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="82ea3-212">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="82ea3-213">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="82ea3-213">Additional resources</span></span>

* [<span data-ttu-id="82ea3-214">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="82ea3-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="82ea3-215">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="82ea3-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-moxiengage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-moxiengage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-moxiengage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-moxiengage-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-moxiengage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-moxiengage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-moxiengage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-moxiengage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-moxiengage-tutorial/tutorial_general_203.png

