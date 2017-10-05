---
title: 'Zelfstudie: Azure Active Directory-integratie met 23 Video | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en 23 Video.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5e73dd1d-3995-4a73-b9cf-1b2318d49cb3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: jeedes
ms.openlocfilehash: ffcd665506c21e25c84367af5b6a3afb8e319af7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-23-video"></a><span data-ttu-id="34899-103">Zelfstudie: Azure Active Directory-integratie met 23 Video</span><span class="sxs-lookup"><span data-stu-id="34899-103">Tutorial: Azure Active Directory integration with 23 Video</span></span>

<span data-ttu-id="34899-104">In deze zelfstudie leert u hoe 23 Video integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="34899-104">In this tutorial, you learn how to integrate 23 Video with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="34899-105">Integratie van 23 biedt Video met Azure AD de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="34899-105">Integrating 23 Video with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="34899-106">U kunt beheren in Azure AD die toegang tot 23 Video heeft</span><span class="sxs-lookup"><span data-stu-id="34899-106">You can control in Azure AD who has access to 23 Video</span></span>
- <span data-ttu-id="34899-107">U kunt uw gebruikers automatisch ophalen aangemeld bij 23 Video (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="34899-107">You can enable your users to automatically get signed-on to 23 Video (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="34899-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="34899-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="34899-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="34899-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="34899-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="34899-110">Prerequisites</span></span>

<span data-ttu-id="34899-111">Voor het configureren van Azure AD-integratie met 23 Video, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="34899-111">To configure Azure AD integration with 23 Video, you need the following items:</span></span>

- <span data-ttu-id="34899-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="34899-112">An Azure AD subscription</span></span>
- <span data-ttu-id="34899-113">Een 23 Video eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="34899-113">A 23 Video single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="34899-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="34899-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="34899-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="34899-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="34899-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="34899-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="34899-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="34899-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="34899-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="34899-118">Scenario description</span></span>
<span data-ttu-id="34899-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="34899-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="34899-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="34899-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="34899-121">23 Video toevoegen uit de galerie</span><span class="sxs-lookup"><span data-stu-id="34899-121">Adding 23 Video from the gallery</span></span>
2. <span data-ttu-id="34899-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="34899-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-23-video-from-the-gallery"></a><span data-ttu-id="34899-123">23 Video toevoegen uit de galerie</span><span class="sxs-lookup"><span data-stu-id="34899-123">Adding 23 Video from the gallery</span></span>
<span data-ttu-id="34899-124">Voor het configureren van de integratie van 23 Video in Azure AD, moet u 23 Video uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="34899-124">To configure the integration of 23 Video into Azure AD, you need to add 23 Video from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="34899-125">**Als u wilt toevoegen 23 Video uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="34899-125">**To add 23 Video from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="34899-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="34899-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="34899-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="34899-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="34899-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="34899-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="34899-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="34899-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="34899-133">Typ in het zoekvak **23 Video**.</span><span class="sxs-lookup"><span data-stu-id="34899-133">In the search box, type **23 Video**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-23video-tutorial/tutorial_23video_search.png)

5. <span data-ttu-id="34899-135">Selecteer in het deelvenster resultaten **23 Video**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="34899-135">In the results panel, select **23 Video**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-23video-tutorial/tutorial_23video_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="34899-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="34899-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="34899-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met 23 Video op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="34899-138">In this section, you configure and test Azure AD single sign-on with 23 Video based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="34899-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in 23 Video is aan een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="34899-139">For single sign-on to work, Azure AD needs to know what the counterpart user in 23 Video is to a user in Azure AD.</span></span> <span data-ttu-id="34899-140">Met andere woorden, een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in 23 Video moet tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="34899-140">In other words, a link relationship between an Azure AD user and the related user in 23 Video needs to be established.</span></span>

<span data-ttu-id="34899-141">Wijs in 23 Video de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="34899-141">In 23 Video, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="34899-142">Om te configureren en testen van Azure AD eenmalige aanmelding met 23 Video, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="34899-142">To configure and test Azure AD single sign-on with 23 Video, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="34899-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="34899-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="34899-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="34899-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="34899-145">**[Maken van een 23 Video testgebruiker](#creating-a-23-video-test-user)**  : 23 Video die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="34899-145">**[Creating a 23 Video test user](#creating-a-23-video-test-user)** - to have a counterpart of Britta Simon in 23 Video that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="34899-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="34899-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="34899-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="34899-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="34899-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="34899-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="34899-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw 23 Video-toepassing.</span><span class="sxs-lookup"><span data-stu-id="34899-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your 23 Video application.</span></span>

<span data-ttu-id="34899-150">**Voor het configureren van Azure AD eenmalige aanmelding met 23 Video, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="34899-150">**To configure Azure AD single sign-on with 23 Video, perform the following steps:**</span></span>

1. <span data-ttu-id="34899-151">In de Azure-portal op de **23 Video** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="34899-151">In the Azure portal, on the **23 Video** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="34899-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="34899-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-23video-tutorial/tutorial_23video_samlbase.png)

3. <span data-ttu-id="34899-155">Op de **23 URL's en Video domein** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="34899-155">On the **23 Video Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-23video-tutorial/tutorial_23video_url.png)

    <span data-ttu-id="34899-157">a.</span><span class="sxs-lookup"><span data-stu-id="34899-157">a.</span></span> <span data-ttu-id="34899-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<subdomain>.23video.com`</span><span class="sxs-lookup"><span data-stu-id="34899-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.23video.com`</span></span>

    <span data-ttu-id="34899-159">b.</span><span class="sxs-lookup"><span data-stu-id="34899-159">b.</span></span> <span data-ttu-id="34899-160">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://www.23video.com/saml/trust/<uniqueid>`</span><span class="sxs-lookup"><span data-stu-id="34899-160">In the **Identifier** textbox, type a URL using the following pattern: `https://www.23video.com/saml/trust/<uniqueid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="34899-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="34899-161">These values are not real.</span></span> <span data-ttu-id="34899-162">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="34899-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="34899-163">Neem contact op met [23 Video Client ondersteuningsteam](mailto:support@23company.com) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="34899-163">Contact [23 Video Client support team](mailto:support@23company.com) to get these values.</span></span> 
 
4. <span data-ttu-id="34899-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="34899-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-23video-tutorial/tutorial_23video_certificate.png) 

5. <span data-ttu-id="34899-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="34899-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-23video-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="34899-168">Op de **23 videoconfiguratie** sectie, klikt u op **configureren 23 Video** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="34899-168">On the **23 Video Configuration** section, click **Configure 23 Video** to open **Configure sign-on** window.</span></span> <span data-ttu-id="34899-169">Kopieer de **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="34899-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-23video-tutorial/tutorial_23video_configure.png) 

7. <span data-ttu-id="34899-171">Eenmalige aanmelding configureren op **23 Video** zijde, moet u de gedownloade verzenden **certificaat (Base64)**, **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** naar [23 Video ondersteuningsteam](mailto:support@23company.com).</span><span class="sxs-lookup"><span data-stu-id="34899-171">To configure single sign-on on **23 Video** side, you need to send the downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [23 Video support team](mailto:support@23company.com).</span></span> 


> [!TIP]
> <span data-ttu-id="34899-172">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="34899-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="34899-173">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="34899-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="34899-174">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="34899-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="34899-175">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="34899-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="34899-176">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="34899-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="34899-178">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="34899-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="34899-179">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="34899-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-23video-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="34899-181">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="34899-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-23video-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="34899-183">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="34899-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-23video-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="34899-185">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="34899-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-23video-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="34899-187">a.</span><span class="sxs-lookup"><span data-stu-id="34899-187">a.</span></span> <span data-ttu-id="34899-188">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="34899-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="34899-189">b.</span><span class="sxs-lookup"><span data-stu-id="34899-189">b.</span></span> <span data-ttu-id="34899-190">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="34899-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="34899-191">c.</span><span class="sxs-lookup"><span data-stu-id="34899-191">c.</span></span> <span data-ttu-id="34899-192">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="34899-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="34899-193">d.</span><span class="sxs-lookup"><span data-stu-id="34899-193">d.</span></span> <span data-ttu-id="34899-194">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="34899-194">Click **Create**.</span></span>
 
### <a name="creating-a-23-video-test-user"></a><span data-ttu-id="34899-195">Een 23 Video testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="34899-195">Creating a 23 Video test user</span></span>

<span data-ttu-id="34899-196">Het doel van deze sectie is het maken van een gebruiker Britta Simon aangeroepen in 23 Video.</span><span class="sxs-lookup"><span data-stu-id="34899-196">The objective of this section is to create a user called Britta Simon in 23 Video.</span></span>

<span data-ttu-id="34899-197">**Als u wilt een gebruiker Britta Simon aangeroepen in 23 Video maakt, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="34899-197">**To create a user called Britta Simon in 23 Video, perform the following steps:**</span></span>

1. <span data-ttu-id="34899-198">Meld u op met uw 23 Video bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="34899-198">Sign on to your 23 Video company site as administrator.</span></span>

2. <span data-ttu-id="34899-199">Ga naar **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="34899-199">Go to **Settings**.</span></span>
 
3. <span data-ttu-id="34899-200">In **gebruikers** sectie, klikt u op **configureren**.</span><span class="sxs-lookup"><span data-stu-id="34899-200">In **Users** section, click **Configure**.</span></span>
   
    ![Gebruiker toewijzen][400]

4. <span data-ttu-id="34899-202">Klik op **een nieuwe gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="34899-202">Click **Add a new user**.</span></span> 
   
    ![Gebruiker toewijzen][401]

5. <span data-ttu-id="34899-204">In de **iemand uitnodigen voor deelname aan deze site** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="34899-204">In the **Invite someone to join this site** section, perform the following steps:</span></span>
   
    ![Gebruiker toewijzen][402]

    <span data-ttu-id="34899-206">a.</span><span class="sxs-lookup"><span data-stu-id="34899-206">a.</span></span> <span data-ttu-id="34899-207">In de **e-mailadressen** textbox Britta Simon van e-mailadres typt in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="34899-207">In the **E-mail addresses** textbox, type Britta Simon's email address in Azure AD.</span></span>  
 
    <span data-ttu-id="34899-208">b.</span><span class="sxs-lookup"><span data-stu-id="34899-208">b.</span></span> <span data-ttu-id="34899-209">Klik op **toevoegen van de gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="34899-209">Click **Add the user**.</span></span>   

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="34899-210">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="34899-210">Assigning the Azure AD test user</span></span>

<span data-ttu-id="34899-211">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan 23 Video.</span><span class="sxs-lookup"><span data-stu-id="34899-211">In this section, you enable Britta Simon to use Azure single sign-on by granting access to 23 Video.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="34899-213">**Britta Simon om aan te wijzen 23 Video, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="34899-213">**To assign Britta Simon to 23 Video, perform the following steps:**</span></span>

1. <span data-ttu-id="34899-214">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="34899-214">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="34899-216">Selecteer in de lijst met toepassingen **23 Video**.</span><span class="sxs-lookup"><span data-stu-id="34899-216">In the applications list, select **23 Video**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-23video-tutorial/tutorial_23video_app.png) 

3. <span data-ttu-id="34899-218">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="34899-218">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="34899-220">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="34899-220">Click **Add** button.</span></span> <span data-ttu-id="34899-221">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="34899-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="34899-223">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="34899-223">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="34899-224">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="34899-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="34899-225">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="34899-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="34899-226">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="34899-226">Testing single sign-on</span></span>

<span data-ttu-id="34899-227">Het doel van deze sectie is het testen van uw Azure AD SSO-configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="34899-227">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="34899-228">Als u op de 23 Video-tegel in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw 23 Video-toepassing.</span><span class="sxs-lookup"><span data-stu-id="34899-228">When you click the 23 Video tile in the Access Panel, you should get automatically signed-on to your 23 Video application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="34899-229">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="34899-229">Additional resources</span></span>

* [<span data-ttu-id="34899-230">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="34899-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="34899-231">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="34899-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-23video-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-23video-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-23video-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-23video-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-23video-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-23video-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-23video-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-23video-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-23video-tutorial/tutorial_general_203.png

[400]: ./media/active-directory-saas-23video-tutorial/tutorial_23video_10.png
[401]: ./media/active-directory-saas-23video-tutorial/tutorial_23video_11.png
[402]: ./media/active-directory-saas-23video-tutorial/tutorial_23video_12.png
