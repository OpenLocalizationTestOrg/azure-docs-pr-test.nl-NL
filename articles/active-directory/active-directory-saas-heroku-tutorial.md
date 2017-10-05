---
title: 'Zelfstudie: Azure Active Directory-integratie met Heroku | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Heroku.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d7d72ec6-4a60-4524-8634-26d8fbbcc833
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: d30605e4757b484f327a784b73f939b62ef59373
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-heroku"></a><span data-ttu-id="396f4-103">Zelfstudie: Azure Active Directory-integratie met Heroku</span><span class="sxs-lookup"><span data-stu-id="396f4-103">Tutorial: Azure Active Directory integration with Heroku</span></span>

<span data-ttu-id="396f4-104">In deze zelfstudie leert u hoe Heroku integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="396f4-104">In this tutorial, you learn how to integrate Heroku with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="396f4-105">Heroku integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="396f4-105">Integrating Heroku with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="396f4-106">U kunt beheren in Azure AD die toegang tot Heroku heeft</span><span class="sxs-lookup"><span data-stu-id="396f4-106">You can control in Azure AD who has access to Heroku</span></span>
- <span data-ttu-id="396f4-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Heroku (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="396f4-107">You can enable your users to automatically get signed-on to Heroku (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="396f4-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="396f4-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="396f4-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="396f4-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="396f4-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="396f4-110">Prerequisites</span></span>

<span data-ttu-id="396f4-111">Voor het configureren van Azure AD-integratie met Heroku, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="396f4-111">To configure Azure AD integration with Heroku, you need the following items:</span></span>

- <span data-ttu-id="396f4-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="396f4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="396f4-113">Een Heroku eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="396f4-113">A Heroku single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="396f4-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="396f4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="396f4-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="396f4-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="396f4-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="396f4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="396f4-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="396f4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="396f4-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="396f4-118">Scenario description</span></span>
<span data-ttu-id="396f4-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="396f4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="396f4-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="396f4-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="396f4-121">Heroku uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="396f4-121">Adding Heroku from the gallery</span></span>
2. <span data-ttu-id="396f4-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="396f4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-heroku-from-the-gallery"></a><span data-ttu-id="396f4-123">Heroku uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="396f4-123">Adding Heroku from the gallery</span></span>
<span data-ttu-id="396f4-124">Voor het configureren van de integratie van Heroku in Azure AD, moet u Heroku uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="396f4-124">To configure the integration of Heroku into Azure AD, you need to add Heroku from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="396f4-125">**Als u wilt toevoegen Heroku uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="396f4-125">**To add Heroku from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="396f4-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="396f4-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="396f4-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="396f4-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="396f4-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="396f4-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="396f4-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="396f4-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="396f4-133">Typ in het zoekvak **Heroku**.</span><span class="sxs-lookup"><span data-stu-id="396f4-133">In the search box, type **Heroku**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_search.png)

5. <span data-ttu-id="396f4-135">Selecteer in het deelvenster resultaten **Heroku**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="396f4-135">In the results panel, select **Heroku**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="396f4-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="396f4-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="396f4-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Heroku op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="396f4-138">In this section, you configure and test Azure AD single sign-on with Heroku based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="396f4-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Heroku is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="396f4-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Heroku is to a user in Azure AD.</span></span> <span data-ttu-id="396f4-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Heroku tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="396f4-140">In other words, a link relationship between an Azure AD user and the related user in Heroku needs to be established.</span></span>

<span data-ttu-id="396f4-141">Wijs in Heroku, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="396f4-141">In Heroku, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="396f4-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Heroku, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="396f4-142">To configure and test Azure AD single sign-on with Heroku, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="396f4-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="396f4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="396f4-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="396f4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="396f4-145">**[Maken van een testgebruiker Heroku](#creating-a-heroku-test-user)**  - Heroku die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="396f4-145">**[Creating a Heroku test user](#creating-a-heroku-test-user)** - to have a counterpart of Britta Simon in Heroku that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="396f4-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="396f4-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="396f4-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="396f4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="396f4-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="396f4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="396f4-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Heroku configureren.</span><span class="sxs-lookup"><span data-stu-id="396f4-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Heroku application.</span></span>

<span data-ttu-id="396f4-150">**Voor het configureren van Azure AD eenmalige aanmelding met Heroku, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="396f4-150">**To configure Azure AD single sign-on with Heroku, perform the following steps:**</span></span>

1. <span data-ttu-id="396f4-151">In de Azure-portal op de **Heroku** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="396f4-151">In the Azure portal, on the **Heroku** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="396f4-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="396f4-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_samlbase.png)

3. <span data-ttu-id="396f4-155">Op de **Heroku domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="396f4-155">On the **Heroku Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_url.png)

    <span data-ttu-id="396f4-157">a.</span><span class="sxs-lookup"><span data-stu-id="396f4-157">a.</span></span> <span data-ttu-id="396f4-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="396f4-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>    
    `https://sso.heroku.com/saml/<company-name>/init`

    <span data-ttu-id="396f4-159">b.</span><span class="sxs-lookup"><span data-stu-id="396f4-159">b.</span></span> <span data-ttu-id="396f4-160">In de **identificatie-URL** textbox, typ een URL met het volgende patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="396f4-160">In the **Identifier URL** textbox, type a URL using the following pattern:</span></span>            
    `https://sso.heroku.com/saml/<company-name>`

    > [!NOTE]
    ><span data-ttu-id="396f4-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="396f4-161">These values are not real.</span></span> <span data-ttu-id="396f4-162">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="396f4-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="396f4-163">U kunt deze waarden ophalen van Heroku-team in latere secties van dit artikel wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="396f4-163">You get these values from Heroku team, which is described in later sections of this article.</span></span> 
        
4. <span data-ttu-id="396f4-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="396f4-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_certificate.png) 

5. <span data-ttu-id="396f4-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="396f4-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-heroku-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="396f4-168">Om SSO in Heroku, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="396f4-168">To enable SSO in Heroku, perform the following steps:</span></span>
   
    <span data-ttu-id="396f4-169">a.</span><span class="sxs-lookup"><span data-stu-id="396f4-169">a.</span></span> <span data-ttu-id="396f4-170">Meld u aan bij de account Heroku als beheerder.</span><span class="sxs-lookup"><span data-stu-id="396f4-170">Log in to the Heroku account as an administrator.</span></span>

    <span data-ttu-id="396f4-171">b.</span><span class="sxs-lookup"><span data-stu-id="396f4-171">b.</span></span> <span data-ttu-id="396f4-172">Klik op het tabblad **Settings**.</span><span class="sxs-lookup"><span data-stu-id="396f4-172">Click the **Settings** tab.</span></span>

    <span data-ttu-id="396f4-173">c.</span><span class="sxs-lookup"><span data-stu-id="396f4-173">c.</span></span> <span data-ttu-id="396f4-174">Op de **eenmalige aanmelding op de pagina**, klikt u op **metagegevens uploaden**.</span><span class="sxs-lookup"><span data-stu-id="396f4-174">On the **Single Sign On Page**, click **Upload Metadata**.</span></span>

    <span data-ttu-id="396f4-175">d.</span><span class="sxs-lookup"><span data-stu-id="396f4-175">d.</span></span> <span data-ttu-id="396f4-176">Upload het metagegevensbestand, dat u hebt gedownload vanuit de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="396f4-176">Upload the metadata file, which you have downloaded from the Azure portal.</span></span>

    <span data-ttu-id="396f4-177">e.</span><span class="sxs-lookup"><span data-stu-id="396f4-177">e.</span></span> <span data-ttu-id="396f4-178">Als de installatie geslaagd is, beheerders bevestigen en de URL van de SSO-aanmelding voor eindgebruikers wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="396f4-178">When the setup is successful, administrators see a confirmation dialog and the URL of the SSO Login for end users is displayed.</span></span> 

    <span data-ttu-id="396f4-179">f.</span><span class="sxs-lookup"><span data-stu-id="396f4-179">f.</span></span> <span data-ttu-id="396f4-180">Kopieer de **Heroku aanmeldings-URL** en **Heroku entiteit-ID** waarden en Ga terug naar **Heroku domein en de URL's** sectie in Azure-portal en plak deze waarden in de **aanmeldings-Url** en **id** tekstvakken respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="396f4-180">Copy the **Heroku Login URL** and **Heroku Entity ID** values and go back to **Heroku Domain and URLs** section in Azure portal and paste these values into the **Sign-On Url** and **Identifier** textboxes respectively.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_52.png) 
    
8. <span data-ttu-id="396f4-182">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="396f4-182">Click **Next**.</span></span>

> [!TIP]
> <span data-ttu-id="396f4-183">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="396f4-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="396f4-184">Na het toevoegen van deze app uit de **Active Directory-bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie aan de onderkant.</span><span class="sxs-lookup"><span data-stu-id="396f4-184">After adding this app from the **Active Directory Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="396f4-185">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="396f4-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="396f4-186">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="396f4-186">Creating an Azure AD test user</span></span>

<span data-ttu-id="396f4-187">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="396f4-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="396f4-189">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="396f4-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="396f4-190">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="396f4-190">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-heroku-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="396f4-192">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="396f4-192">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-heroku-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="396f4-194">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="396f4-194">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-heroku-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="396f4-196">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="396f4-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-heroku-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="396f4-198">a.</span><span class="sxs-lookup"><span data-stu-id="396f4-198">a.</span></span> <span data-ttu-id="396f4-199">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="396f4-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="396f4-200">b.</span><span class="sxs-lookup"><span data-stu-id="396f4-200">b.</span></span> <span data-ttu-id="396f4-201">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="396f4-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="396f4-202">c.</span><span class="sxs-lookup"><span data-stu-id="396f4-202">c.</span></span> <span data-ttu-id="396f4-203">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="396f4-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="396f4-204">d.</span><span class="sxs-lookup"><span data-stu-id="396f4-204">d.</span></span> <span data-ttu-id="396f4-205">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="396f4-205">Click **Create**.</span></span>
 
### <a name="creating-a-heroku-test-user"></a><span data-ttu-id="396f4-206">Een testgebruiker Heroku maken</span><span class="sxs-lookup"><span data-stu-id="396f4-206">Creating a Heroku test user</span></span>

<span data-ttu-id="396f4-207">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in Heroku maken.</span><span class="sxs-lookup"><span data-stu-id="396f4-207">In this section, you create a user called Britta Simon in Heroku.</span></span> <span data-ttu-id="396f4-208">Heroku ondersteunt just-in-time-inrichting, die standaard is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="396f4-208">Heroku supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="396f4-209">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="396f4-209">There is no action item for you in this section.</span></span> <span data-ttu-id="396f4-210">Een nieuwe gebruiker wordt gemaakt bij het openen van Heroku als de gebruiker nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="396f4-210">A new user is created when accessing Heroku if the user doesn't exist yet.</span></span> <span data-ttu-id="396f4-211">Nadat het account is ingericht, wordt de gebruiker ontvangt een bevestigingsmail en moet Klik op de koppeling bevestiging.</span><span class="sxs-lookup"><span data-stu-id="396f4-211">After the account is provisioned, the end user receives a verification email and needs to click the acknowledgement link.</span></span>

>[!NOTE]
><span data-ttu-id="396f4-212">Als u een gebruiker handmatig maken wilt, moet u contact op met de [Heroku Client ondersteuningsteam](https://www.heroku.com/support).</span><span class="sxs-lookup"><span data-stu-id="396f4-212">If you need to create a user manually, you need to contact the [Heroku Client support team](https://www.heroku.com/support).</span></span>
>  

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="396f4-213">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="396f4-213">Assigning the Azure AD test user</span></span>

<span data-ttu-id="396f4-214">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Heroku.</span><span class="sxs-lookup"><span data-stu-id="396f4-214">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Heroku.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="396f4-216">**Britta Simon om aan te wijzen Heroku, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="396f4-216">**To assign Britta Simon to Heroku, perform the following steps:**</span></span>

1. <span data-ttu-id="396f4-217">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="396f4-217">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="396f4-219">Selecteer in de lijst met toepassingen **Heroku**.</span><span class="sxs-lookup"><span data-stu-id="396f4-219">In the applications list, select **Heroku**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_app.png) 

3. <span data-ttu-id="396f4-221">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="396f4-221">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="396f4-223">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="396f4-223">Click **Add** button.</span></span> <span data-ttu-id="396f4-224">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="396f4-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="396f4-226">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="396f4-226">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="396f4-227">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="396f4-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="396f4-228">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="396f4-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="396f4-229">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="396f4-229">Testing single sign-on</span></span>

<span data-ttu-id="396f4-230">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="396f4-230">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="396f4-231">Als u op de tegel Heroku in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Heroku.</span><span class="sxs-lookup"><span data-stu-id="396f4-231">When you click the Heroku tile in the Access Panel, you should get automatically signed-on to your Heroku application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="396f4-232">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="396f4-232">Additional resources</span></span>

* [<span data-ttu-id="396f4-233">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="396f4-233">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="396f4-234">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="396f4-234">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_203.png
