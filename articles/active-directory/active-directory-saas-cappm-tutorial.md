---
title: 'Zelfstudie: Azure Active Directory-integratie met CA PPM | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en CA-pagina's per minuut.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ca9d5e71-e429-4891-8d10-3498e7210e89
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 4ca9268c26f681fcc96955b6161fe4a119b2dcf4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ca-ppm"></a><span data-ttu-id="eb429-103">Zelfstudie: Azure Active Directory-integratie met CA PPM</span><span class="sxs-lookup"><span data-stu-id="eb429-103">Tutorial: Azure Active Directory integration with CA PPM</span></span>

<span data-ttu-id="eb429-104">In deze zelfstudie leert u hoe CA PPM integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="eb429-104">In this tutorial, you learn how to integrate CA PPM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="eb429-105">CA PPM integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="eb429-105">Integrating CA PPM with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="eb429-106">U kunt beheren in Azure AD die toegang tot de CA-pagina's per minuut heeft</span><span class="sxs-lookup"><span data-stu-id="eb429-106">You can control in Azure AD who has access to CA PPM</span></span>
- <span data-ttu-id="eb429-107">U kunt uw gebruikers automatisch ophalen aangemeld bij CA PPM (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="eb429-107">You can enable your users to automatically get signed-on to CA PPM (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="eb429-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="eb429-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="eb429-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="eb429-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eb429-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="eb429-110">Prerequisites</span></span>

<span data-ttu-id="eb429-111">Voor het configureren van Azure AD-integratie met CA PPM, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="eb429-111">To configure Azure AD integration with CA PPM, you need the following items:</span></span>

- <span data-ttu-id="eb429-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="eb429-112">An Azure AD subscription</span></span>
- <span data-ttu-id="eb429-113">Een CA PPM eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="eb429-113">A CA PPM single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="eb429-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="eb429-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="eb429-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="eb429-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="eb429-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="eb429-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="eb429-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="eb429-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="eb429-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="eb429-118">Scenario description</span></span>
<span data-ttu-id="eb429-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="eb429-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="eb429-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="eb429-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="eb429-121">CA PPM uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="eb429-121">Adding CA PPM from the gallery</span></span>
2. <span data-ttu-id="eb429-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="eb429-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ca-ppm-from-the-gallery"></a><span data-ttu-id="eb429-123">CA PPM uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="eb429-123">Adding CA PPM from the gallery</span></span>
<span data-ttu-id="eb429-124">Voor het configureren van de integratie van CA-pagina's per minuut in Azure AD, moet u CA PPM uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="eb429-124">To configure the integration of CA PPM into Azure AD, you need to add CA PPM from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="eb429-125">**Als u wilt toevoegen CA PPM uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="eb429-125">**To add CA PPM from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="eb429-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="eb429-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="eb429-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="eb429-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="eb429-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="eb429-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="eb429-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="eb429-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="eb429-133">Typ in het zoekvak **CA PPM**.</span><span class="sxs-lookup"><span data-stu-id="eb429-133">In the search box, type **CA PPM**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_search.png)

5. <span data-ttu-id="eb429-135">Selecteer in het deelvenster resultaten **CA PPM**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="eb429-135">In the results panel, select **CA PPM**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="eb429-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="eb429-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="eb429-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met CA PPM op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="eb429-138">In this section, you configure and test Azure AD single sign-on with CA PPM based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="eb429-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent CA ppm is aan een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eb429-139">For single sign-on to work, Azure AD needs to know what the counterpart user in CA PPM is to a user in Azure AD.</span></span> <span data-ttu-id="eb429-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker CA ppm tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="eb429-140">In other words, a link relationship between an Azure AD user and the related user in CA PPM needs to be established.</span></span>

<span data-ttu-id="eb429-141">Ppm CA, wijs de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="eb429-141">In CA PPM, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="eb429-142">Om te configureren en testen van Azure AD eenmalige aanmelding met CA PPM, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="eb429-142">To configure and test Azure AD single sign-on with CA PPM, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="eb429-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="eb429-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="eb429-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="eb429-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="eb429-145">**[Maken van een CA PPM testgebruiker](#creating-a-ca-ppm-test-user)**  - hebben een equivalent van Britta Simon CA ppm die is gekoppeld aan de Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="eb429-145">**[Creating a CA PPM test user](#creating-a-ca-ppm-test-user)** - to have a counterpart of Britta Simon in CA PPM that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="eb429-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="eb429-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="eb429-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="eb429-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="eb429-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="eb429-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="eb429-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw CA PPM-toepassing.</span><span class="sxs-lookup"><span data-stu-id="eb429-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your CA PPM application.</span></span>

<span data-ttu-id="eb429-150">**Voor het configureren van Azure AD eenmalige aanmelding met CA PPM, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="eb429-150">**To configure Azure AD single sign-on with CA PPM, perform the following steps:**</span></span>

1. <span data-ttu-id="eb429-151">In de Azure-portal op de **CA PPM** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="eb429-151">In the Azure portal, on the **CA PPM** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="eb429-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="eb429-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_samlbase.png)

3. <span data-ttu-id="eb429-155">Op de **CA PPM domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="eb429-155">On the **CA PPM Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_url.png)

    <span data-ttu-id="eb429-157">a.</span><span class="sxs-lookup"><span data-stu-id="eb429-157">a.</span></span> <span data-ttu-id="eb429-158">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://ca.ondemand.saml.20.post.<companyname>`</span><span class="sxs-lookup"><span data-stu-id="eb429-158">In the **Identifier** textbox, type a URL using the following pattern: `https://ca.ondemand.saml.20.post.<companyname>`</span></span>
    
    <span data-ttu-id="eb429-159">b.</span><span class="sxs-lookup"><span data-stu-id="eb429-159">b.</span></span> <span data-ttu-id="eb429-160">In de **antwoord-URL** textbox type als:`https://fedsso.ondemand.ca.com/affwebservices/public/saml2assertionconsumer`</span><span class="sxs-lookup"><span data-stu-id="eb429-160">In the **Reply URL** textbox, type as: `https://fedsso.ondemand.ca.com/affwebservices/public/saml2assertionconsumer`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="eb429-161">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="eb429-161">This value is not real.</span></span> <span data-ttu-id="eb429-162">Deze waarde door de werkelijke ID bijwerken.</span><span class="sxs-lookup"><span data-stu-id="eb429-162">Update this value with the actual Identifier.</span></span> <span data-ttu-id="eb429-163">Neem contact op met [CA PPM-ondersteuningsteam](mailto:catechnicalsupport@ca.com) deze waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="eb429-163">Contact [CA PPM support team](mailto:catechnicalsupport@ca.com) to get this value.</span></span>
 
4. <span data-ttu-id="eb429-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="eb429-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_certificate.png) 

5. <span data-ttu-id="eb429-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="eb429-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cappm-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="eb429-168">Op de **CA PPM-configuratie** sectie, klikt u op **configureren CA PPM** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="eb429-168">On the **CA PPM Configuration** section, click **Configure CA PPM** to open **Configure sign-on** window.</span></span> <span data-ttu-id="eb429-169">Kopieer de **SAML entiteit-ID** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="eb429-169">Copy the **SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_configure.png) 

7. <span data-ttu-id="eb429-171">Eenmalige aanmelding configureren op **CA PPM** zijde, moet u de gedownloade verzenden **Certificate(Base64)** en **SAML entiteit-ID** naar [CA PPM-ondersteuningsteam](mailto:catechnicalsupport@ca.com).</span><span class="sxs-lookup"><span data-stu-id="eb429-171">To configure single sign-on on **CA PPM** side, you need to send the downloaded **Certificate(Base64)** and **SAML Entity ID** to [CA PPM support team](mailto:catechnicalsupport@ca.com).</span></span>

> [!TIP]
> <span data-ttu-id="eb429-172">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="eb429-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="eb429-173">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="eb429-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="eb429-174">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="eb429-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="eb429-175">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="eb429-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="eb429-176">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="eb429-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="eb429-178">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="eb429-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="eb429-179">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="eb429-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cappm-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="eb429-181">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="eb429-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cappm-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="eb429-183">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="eb429-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cappm-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="eb429-185">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="eb429-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cappm-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="eb429-187">a.</span><span class="sxs-lookup"><span data-stu-id="eb429-187">a.</span></span> <span data-ttu-id="eb429-188">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="eb429-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="eb429-189">b.</span><span class="sxs-lookup"><span data-stu-id="eb429-189">b.</span></span> <span data-ttu-id="eb429-190">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="eb429-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="eb429-191">c.</span><span class="sxs-lookup"><span data-stu-id="eb429-191">c.</span></span> <span data-ttu-id="eb429-192">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="eb429-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="eb429-193">d.</span><span class="sxs-lookup"><span data-stu-id="eb429-193">d.</span></span> <span data-ttu-id="eb429-194">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="eb429-194">Click **Create**.</span></span>
 
### <a name="creating-a-ca-ppm-test-user"></a><span data-ttu-id="eb429-195">Maken van een CA PPM testgebruiker</span><span class="sxs-lookup"><span data-stu-id="eb429-195">Creating a CA PPM test user</span></span>

<span data-ttu-id="eb429-196">In deze sectie maakt maken u een gebruiker met de naam van Britta Simon CA ppm.</span><span class="sxs-lookup"><span data-stu-id="eb429-196">In this section, you create a user called Britta Simon in CA PPM.</span></span> <span data-ttu-id="eb429-197">Werken met [CA PPM-ondersteuningsteam](mailto:catechnicalsupport@ca.com) toevoegen van de gebruikers in het CA-PPM-platform.</span><span class="sxs-lookup"><span data-stu-id="eb429-197">Work with [CA PPM support team](mailto:catechnicalsupport@ca.com) to add the users in the CA PPM platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="eb429-198">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb429-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="eb429-199">In deze sectie schakelt u Britta Simon Azure eenmalige aanmelding gebruiken door het verlenen van toegang tot CA PPM.</span><span class="sxs-lookup"><span data-stu-id="eb429-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to CA PPM.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="eb429-201">**Als u wilt toewijzen Britta Simon CA ppm, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="eb429-201">**To assign Britta Simon to CA PPM, perform the following steps:**</span></span>

1. <span data-ttu-id="eb429-202">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="eb429-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="eb429-204">Selecteer in de lijst met toepassingen **CA PPM**.</span><span class="sxs-lookup"><span data-stu-id="eb429-204">In the applications list, select **CA PPM**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_app.png) 

3. <span data-ttu-id="eb429-206">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="eb429-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="eb429-208">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="eb429-208">Click **Add** button.</span></span> <span data-ttu-id="eb429-209">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="eb429-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="eb429-211">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="eb429-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="eb429-212">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="eb429-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="eb429-213">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="eb429-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="eb429-214">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="eb429-214">Testing single sign-on</span></span>

<span data-ttu-id="eb429-215">In deze sectie kunt u uw Azure AD SSO-configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="eb429-215">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="eb429-216">Als u op de CA PPM-tegel in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw CA PPM-toepassing.</span><span class="sxs-lookup"><span data-stu-id="eb429-216">When you click the CA PPM tile in the Access Panel, you should get automatically signed-on to your CA PPM application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="eb429-217">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="eb429-217">Additional resources</span></span>

* [<span data-ttu-id="eb429-218">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="eb429-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="eb429-219">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="eb429-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_203.png

