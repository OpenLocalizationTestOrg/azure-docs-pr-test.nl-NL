---
title: 'Zelfstudie: Azure Active Directory-integratie met eDigitalResearch | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en eDigitalResearch.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: c6b66ea0-16ba-45b4-b550-e81c56262b1f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: f877a1dd844c40c913f3121e5288952653c312cd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-edigitalresearch"></a><span data-ttu-id="9669c-103">Zelfstudie: Azure Active Directory-integratie met eDigitalResearch</span><span class="sxs-lookup"><span data-stu-id="9669c-103">Tutorial: Azure Active Directory integration with eDigitalResearch</span></span>

<span data-ttu-id="9669c-104">In deze zelfstudie leert u hoe eDigitalResearch integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9669c-104">In this tutorial, you learn how to integrate eDigitalResearch with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9669c-105">EDigitalResearch integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="9669c-105">Integrating eDigitalResearch with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9669c-106">U kunt beheren in Azure AD die toegang tot eDigitalResearch heeft.</span><span class="sxs-lookup"><span data-stu-id="9669c-106">You can control in Azure AD who has access to eDigitalResearch.</span></span>
- <span data-ttu-id="9669c-107">U kunt uw gebruikers automatisch ophalen aangemeld bij eDigitalResearch (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="9669c-107">You can enable your users to automatically get signed-on to eDigitalResearch (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="9669c-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="9669c-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="9669c-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9669c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9669c-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="9669c-110">Prerequisites</span></span>

<span data-ttu-id="9669c-111">Voor het configureren van Azure AD-integratie met eDigitalResearch, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="9669c-111">To configure Azure AD integration with eDigitalResearch, you need the following items:</span></span>

- <span data-ttu-id="9669c-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="9669c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9669c-113">Een eDigitalResearch eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="9669c-113">A eDigitalResearch single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9669c-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="9669c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9669c-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="9669c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9669c-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="9669c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9669c-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9669c-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9669c-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="9669c-118">Scenario description</span></span>
<span data-ttu-id="9669c-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="9669c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9669c-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="9669c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9669c-121">EDigitalResearch uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="9669c-121">Adding eDigitalResearch from the gallery</span></span>
2. <span data-ttu-id="9669c-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="9669c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-edigitalresearch-from-the-gallery"></a><span data-ttu-id="9669c-123">EDigitalResearch uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="9669c-123">Adding eDigitalResearch from the gallery</span></span>
<span data-ttu-id="9669c-124">Voor het configureren van de integratie van eDigitalResearch in Azure AD, moet u eDigitalResearch uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="9669c-124">To configure the integration of eDigitalResearch into Azure AD, you need to add eDigitalResearch from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9669c-125">**Als u wilt toevoegen eDigitalResearch uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="9669c-125">**To add eDigitalResearch from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9669c-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="9669c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![De Azure Active Directory-knop][1]

2. <span data-ttu-id="9669c-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="9669c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9669c-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="9669c-129">Then go to **All applications**.</span></span>

    ![De blade Enterprise-toepassingen][2]
    
3. <span data-ttu-id="9669c-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9669c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![De knop Nieuw toepassing][3]

4. <span data-ttu-id="9669c-133">Typ in het zoekvak **eDigitalResearch**, selecteer **eDigitalResearch** van resultaat deelvenster klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="9669c-133">In the search box, type **eDigitalResearch**, select **eDigitalResearch** from result panel then click **Add** button to add the application.</span></span>

    ![eDigitalResearch in de lijst met resultaten](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="9669c-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="9669c-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="9669c-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met eDigitalResearch op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="9669c-136">In this section, you configure and test Azure AD single sign-on with eDigitalResearch based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9669c-137">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in eDigitalResearch is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9669c-137">For single sign-on to work, Azure AD needs to know what the counterpart user in eDigitalResearch is to a user in Azure AD.</span></span> <span data-ttu-id="9669c-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in eDigitalResearch tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="9669c-138">In other words, a link relationship between an Azure AD user and the related user in eDigitalResearch needs to be established.</span></span>

<span data-ttu-id="9669c-139">Wijs in eDigitalResearch, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="9669c-139">In eDigitalResearch, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="9669c-140">Om te configureren en testen van Azure AD eenmalige aanmelding met eDigitalResearch, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="9669c-140">To configure and test Azure AD single sign-on with eDigitalResearch, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9669c-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="9669c-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9669c-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9669c-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9669c-143">**[Maak een testgebruiker eDigitalResearch](#create-a-edigitalresearch-test-user)**  - hebben een equivalent van Britta Simon in eDigitalResearch die is gekoppeld aan de Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="9669c-143">**[Create a eDigitalResearch test user](#create-a-edigitalresearch-test-user)** - to have a counterpart of Britta Simon in eDigitalResearch that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9669c-144">**[Toewijzen van de Azure AD-testgebruiker](#assign-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="9669c-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9669c-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="9669c-145">**[Test single sign-on](#test-single-sign-on)**  to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="9669c-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="9669c-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="9669c-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing eDigitalResearch configureren.</span><span class="sxs-lookup"><span data-stu-id="9669c-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your eDigitalResearch application.</span></span>

<span data-ttu-id="9669c-148">**Voor het configureren van Azure AD eenmalige aanmelding met eDigitalResearch, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="9669c-148">**To configure Azure AD single sign-on with eDigitalResearch, perform the following steps:**</span></span>

1. <span data-ttu-id="9669c-149">In de Azure-portal op de **eDigitalResearch** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="9669c-149">In the Azure portal, on the **eDigitalResearch** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="9669c-151">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="9669c-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_samlbase.png)

3. <span data-ttu-id="9669c-153">Op de **eDigitalResearch domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="9669c-153">On the **eDigitalResearch Domain and URLs** section, perform the following steps:</span></span>

    ![eDigitalResearch domein en de URL's eenmalige aanmelding informatie](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_url.png)

    <span data-ttu-id="9669c-155">a.</span><span class="sxs-lookup"><span data-stu-id="9669c-155">a.</span></span> <span data-ttu-id="9669c-156">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<company-name>.edigitalresearch.com`</span><span class="sxs-lookup"><span data-stu-id="9669c-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<company-name>.edigitalresearch.com`</span></span>

    <span data-ttu-id="9669c-157">b.</span><span class="sxs-lookup"><span data-stu-id="9669c-157">b.</span></span> <span data-ttu-id="9669c-158">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://<company-name>.edigitalresearch.com/login/consume`</span><span class="sxs-lookup"><span data-stu-id="9669c-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company-name>.edigitalresearch.com/login/consume`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9669c-159">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="9669c-159">These values are not real.</span></span> <span data-ttu-id="9669c-160">Deze waarden bijwerken met de werkelijke id en de antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="9669c-160">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="9669c-161">Neem contact op met [eDigitalResearch ondersteuningsteam](http://www.maruedr.com/contact) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="9669c-161">Contact [eDigitalResearch support team](http://www.maruedr.com/contact) to get these values.</span></span>
 


4. <span data-ttu-id="9669c-162">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat Base(64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="9669c-162">On the **SAML Signing Certificate** section, click **Certificate Base(64)** and then save the certificate file on your computer.</span></span>

    <span data-ttu-id="9669c-163">!</span><span class="sxs-lookup"><span data-stu-id="9669c-163">!</span></span>![De downloadkoppeling certificaat](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_certificate.png) 

5. <span data-ttu-id="9669c-165">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="9669c-165">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9669c-167">Op de **eDigitalResearch configuratie** sectie, klikt u op **configureren eDigitalResearch** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="9669c-167">On the **eDigitalResearch Configuration** section, click **Configure eDigitalResearch** to open **Configure sign-on** window.</span></span> <span data-ttu-id="9669c-168">Kopieer de **Sign-Out-URL, SAML entiteit-ID** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="9669c-168">Copy the **Sign-Out URL, SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![eDigitalResearch configuratie](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_configure.png) 

7. <span data-ttu-id="9669c-170">Eenmalige aanmelding configureren op **eDigitalResearch** zijde, moet u de gedownloade verzenden **certificaatbestand (Base64)**, **SAML entiteit-ID**, en **afmelden URL** naar [eDigitalResearch ondersteuningsteam](http://www.maruedr.com/contact).</span><span class="sxs-lookup"><span data-stu-id="9669c-170">To configure single sign-on on **eDigitalResearch** side, you need to send the downloaded **Certificate (Base64) File**, **SAML Entity ID**, and **Sign-Out URL** to [eDigitalResearch support team](http://www.maruedr.com/contact).</span></span> <span data-ttu-id="9669c-171">Ze deze instelling zodat de SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="9669c-171">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="9669c-172">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="9669c-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9669c-173">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="9669c-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9669c-174">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9669c-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="9669c-175">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="9669c-175">Create an Azure AD test user</span></span>

<span data-ttu-id="9669c-176">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="9669c-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="9669c-178">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="9669c-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9669c-179">Klik in de Azure-portal in het linkerdeelvenster op het **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="9669c-179">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![De Azure Active Directory-knop](./media/active-directory-saas-edigitalresearch-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="9669c-181">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="9669c-181">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !['Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-edigitalresearch-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="9669c-183">Openen van de **gebruiker** in het dialoogvenster klikt u op **toevoegen** boven aan de **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9669c-183">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![De knop toevoegen](./media/active-directory-saas-edigitalresearch-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="9669c-185">In de **gebruiker** dialoogvenster vak, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="9669c-185">In the **User** dialog box, perform the following steps:</span></span>

    ![Het dialoogvenster gebruiker](./media/active-directory-saas-edigitalresearch-tutorial/create_aaduser_04.png)

    <span data-ttu-id="9669c-187">a.</span><span class="sxs-lookup"><span data-stu-id="9669c-187">a.</span></span> <span data-ttu-id="9669c-188">In de **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9669c-188">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9669c-189">b.</span><span class="sxs-lookup"><span data-stu-id="9669c-189">b.</span></span> <span data-ttu-id="9669c-190">In de **gebruikersnaam** typt u het e-mailadres van gebruiker Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9669c-190">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="9669c-191">c.</span><span class="sxs-lookup"><span data-stu-id="9669c-191">c.</span></span> <span data-ttu-id="9669c-192">Selecteer de **wachtwoord weergeven** selectievakje, en noteer de waarde die wordt weergegeven in de **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="9669c-192">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="9669c-193">d.</span><span class="sxs-lookup"><span data-stu-id="9669c-193">d.</span></span> <span data-ttu-id="9669c-194">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="9669c-194">Click **Create**.</span></span>
  
### <a name="create-a-edigitalresearch-test-user"></a><span data-ttu-id="9669c-195">Een testgebruiker eDigitalResearch maken</span><span class="sxs-lookup"><span data-stu-id="9669c-195">Create a eDigitalResearch test user</span></span>

<span data-ttu-id="9669c-196">Het doel van deze sectie is het maken van een gebruiker Britta Simon in eDigitalResearch genoemd.</span><span class="sxs-lookup"><span data-stu-id="9669c-196">The objective of this section is to create a user called Britta Simon in eDigitalResearch.</span></span> 

<span data-ttu-id="9669c-197">Werken met de [eDigitalResearch ondersteuningsteam](http://www.maruedr.com/contact) om op te halen van gebruikers die zijn gemaakt.</span><span class="sxs-lookup"><span data-stu-id="9669c-197">Work with the [eDigitalResearch support team](http://www.maruedr.com/contact) to get users created.</span></span>     
    
 > [!NOTE]
 > <span data-ttu-id="9669c-198">De houder van Azure Active Directory-account ontvangt een e-mailbericht en volgt een koppeling om hun account te bevestigen voordat deze geactiveerd wordt.</span><span class="sxs-lookup"><span data-stu-id="9669c-198">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="9669c-199">De Azure AD-testgebruiker toewijzen</span><span class="sxs-lookup"><span data-stu-id="9669c-199">Assign the Azure AD test user</span></span>

<span data-ttu-id="9669c-200">In deze sectie schakelt u Britta Simon Azure eenmalige aanmelding gebruiken door het verlenen van toegang tot eDigitalResearch.</span><span class="sxs-lookup"><span data-stu-id="9669c-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to eDigitalResearch.</span></span>

![Toewijzen van de gebruikersrol][200] 

<span data-ttu-id="9669c-202">**Britta Simon om aan te wijzen eDigitalResearch, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="9669c-202">**To assign Britta Simon to eDigitalResearch, perform the following steps:**</span></span>

1. <span data-ttu-id="9669c-203">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="9669c-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="9669c-205">Selecteer in de lijst met toepassingen **eDigitalResearch**.</span><span class="sxs-lookup"><span data-stu-id="9669c-205">In the applications list, select **eDigitalResearch**.</span></span>

    ![De koppeling eDigitalResearch in de lijst met toepassingen](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_app.png)  

3. <span data-ttu-id="9669c-207">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="9669c-207">In the menu on the left, click **Users and groups**.</span></span>

    ![De koppeling 'Gebruikers en groepen'][202]

4. <span data-ttu-id="9669c-209">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="9669c-209">Click **Add** button.</span></span> <span data-ttu-id="9669c-210">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9669c-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Het deelvenster toewijzing toevoegen][203]

5. <span data-ttu-id="9669c-212">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="9669c-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9669c-213">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9669c-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9669c-214">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9669c-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="9669c-215">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="9669c-215">Test single sign-on</span></span>

<span data-ttu-id="9669c-216">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="9669c-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="9669c-217">Als u op de tegel eDigitalResearch in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing eDigitalResearch.</span><span class="sxs-lookup"><span data-stu-id="9669c-217">When you click the eDigitalResearch tile in the Access Panel, you should get automatically signed-on to your eDigitalResearch application.</span></span>
<span data-ttu-id="9669c-218">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9669c-218">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="9669c-219">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="9669c-219">Additional resources</span></span>

* [<span data-ttu-id="9669c-220">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9669c-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9669c-221">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9669c-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_203.png

