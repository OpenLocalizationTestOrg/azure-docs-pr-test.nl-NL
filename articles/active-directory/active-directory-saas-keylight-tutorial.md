---
title: 'Zelfstudie: Azure Active Directory-integratie met LockPath Keylight | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en LockPath Keylight.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 234a32f1-9f56-4650-9e31-7b38ad734b1a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: e64a966f24411818abc4cc4ab29a428b5577d012
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lockpath-keylight"></a><span data-ttu-id="e09a4-103">Zelfstudie: Azure Active Directory-integratie met LockPath Keylight</span><span class="sxs-lookup"><span data-stu-id="e09a4-103">Tutorial: Azure Active Directory integration with LockPath Keylight</span></span>

<span data-ttu-id="e09a4-104">In deze zelfstudie leert u hoe LockPath Keylight integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e09a4-104">In this tutorial, you learn how to integrate LockPath Keylight with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e09a4-105">LockPath Keylight integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="e09a4-105">Integrating LockPath Keylight with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e09a4-106">U kunt beheren in Azure AD die toegang tot LockPath Keylight heeft</span><span class="sxs-lookup"><span data-stu-id="e09a4-106">You can control in Azure AD who has access to LockPath Keylight</span></span>
- <span data-ttu-id="e09a4-107">U kunt uw gebruikers automatisch ophalen aangemeld bij LockPath Keylight (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="e09a4-107">You can enable your users to automatically get signed-on to LockPath Keylight (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e09a4-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="e09a4-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e09a4-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e09a4-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e09a4-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="e09a4-110">Prerequisites</span></span>

<span data-ttu-id="e09a4-111">Voor het configureren van Azure AD-integratie met LockPath Keylight, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="e09a4-111">To configure Azure AD integration with LockPath Keylight, you need the following items:</span></span>

- <span data-ttu-id="e09a4-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="e09a4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e09a4-113">Een LockPath Keylight eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="e09a4-113">A LockPath Keylight single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e09a4-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="e09a4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e09a4-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="e09a4-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e09a4-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="e09a4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e09a4-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e09a4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e09a4-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="e09a4-118">Scenario description</span></span>
<span data-ttu-id="e09a4-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="e09a4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e09a4-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="e09a4-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e09a4-121">LockPath Keylight uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="e09a4-121">Adding LockPath Keylight from the gallery</span></span>
2. <span data-ttu-id="e09a4-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="e09a4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lockpath-keylight-from-the-gallery"></a><span data-ttu-id="e09a4-123">LockPath Keylight uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="e09a4-123">Adding LockPath Keylight from the gallery</span></span>
<span data-ttu-id="e09a4-124">Voor het configureren van de integratie van LockPath Keylight in Azure AD, moet u LockPath Keylight uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="e09a4-124">To configure the integration of LockPath Keylight into Azure AD, you need to add LockPath Keylight from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e09a4-125">**Als u wilt toevoegen LockPath Keylight uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="e09a4-125">**To add LockPath Keylight from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e09a4-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="e09a4-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e09a4-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="e09a4-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e09a4-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="e09a4-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="e09a4-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e09a4-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="e09a4-133">Typ in het zoekvak **LockPath Keylight**.</span><span class="sxs-lookup"><span data-stu-id="e09a4-133">In the search box, type **LockPath Keylight**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_search.png)

5. <span data-ttu-id="e09a4-135">Selecteer in het deelvenster resultaten **LockPath Keylight**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="e09a4-135">In the results panel, select **LockPath Keylight**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e09a4-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="e09a4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e09a4-138">In deze sectie kunt u configureren en test eenmalige aanmelding Azure AD met LockPath Keylight op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="e09a4-138">In this section, you configure and test Azure AD single sign-on with LockPath Keylight based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e09a4-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in LockPath Keylight is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e09a4-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LockPath Keylight is to a user in Azure AD.</span></span> <span data-ttu-id="e09a4-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in LockPath Keylight tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="e09a4-140">In other words, a link relationship between an Azure AD user and the related user in LockPath Keylight needs to be established.</span></span>

<span data-ttu-id="e09a4-141">Wijs in LockPath Keylight, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="e09a4-141">In LockPath Keylight, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e09a4-142">Om te configureren en testen van Azure AD eenmalige aanmelding met LockPath Keylight, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="e09a4-142">To configure and test Azure AD single sign-on with LockPath Keylight, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e09a4-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e09a4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e09a4-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e09a4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e09a4-145">**[Maken van een testgebruiker LockPath Keylight](#creating-a-lockpath-keylight-test-user)**  - LockPath Keylight die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="e09a4-145">**[Creating a LockPath Keylight test user](#creating-a-lockpath-keylight-test-user)** - to have a counterpart of Britta Simon in LockPath Keylight that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e09a4-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="e09a4-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e09a4-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="e09a4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e09a4-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="e09a4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e09a4-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing LockPath Keylight configureren.</span><span class="sxs-lookup"><span data-stu-id="e09a4-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LockPath Keylight application.</span></span>

<span data-ttu-id="e09a4-150">**Voor het configureren van Azure AD eenmalige aanmelding met LockPath Keylight, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="e09a4-150">**To configure Azure AD single sign-on with LockPath Keylight, perform the following steps:**</span></span>

1. <span data-ttu-id="e09a4-151">In de Azure-portal op de **LockPath Keylight** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="e09a4-151">In the Azure portal, on the **LockPath Keylight** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="e09a4-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="e09a4-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_samlbase.png)

3. <span data-ttu-id="e09a4-155">Op de **LockPath Keylight domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="e09a4-155">On the **LockPath Keylight Domain and URLs** section, perform the following steps::</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_url.png)

    <span data-ttu-id="e09a4-157">a.</span><span class="sxs-lookup"><span data-stu-id="e09a4-157">a.</span></span> <span data-ttu-id="e09a4-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<company name>.keylightgrc.com/`</span><span class="sxs-lookup"><span data-stu-id="e09a4-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.keylightgrc.com/`</span></span>

    <span data-ttu-id="e09a4-159">b.</span><span class="sxs-lookup"><span data-stu-id="e09a4-159">b.</span></span> <span data-ttu-id="e09a4-160">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<company name>.keylightgrc.com`</span><span class="sxs-lookup"><span data-stu-id="e09a4-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.keylightgrc.com`</span></span>

    <span data-ttu-id="e09a4-161">c.</span><span class="sxs-lookup"><span data-stu-id="e09a4-161">c.</span></span> <span data-ttu-id="e09a4-162">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://<company name>.keylightgrc.com/Login.aspx`</span><span class="sxs-lookup"><span data-stu-id="e09a4-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.keylightgrc.com/Login.aspx`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="e09a4-163">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="e09a4-163">These values are not real.</span></span> <span data-ttu-id="e09a4-164">Deze waarden bijwerken met de werkelijke id, antwoord-URL en aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="e09a4-164">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="e09a4-165">Neem contact op met [LockPath Keylight Client ondersteuningsteam](https://www.lockpath.com/contact/) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="e09a4-165">Contact [LockPath Keylight Client support team](https://www.lockpath.com/contact/) to get these values.</span></span> 

4. <span data-ttu-id="e09a4-166">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Raw)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="e09a4-166">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_certificate.png) 

5. <span data-ttu-id="e09a4-168">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="e09a4-168">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-keylight-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="e09a4-170">Op de **LockPath Keylight configuratie** sectie, klikt u op **configureren LockPath Keylight** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="e09a4-170">On the **LockPath Keylight Configuration** section, click **Configure LockPath Keylight** to open **Configure sign-on** window.</span></span> <span data-ttu-id="e09a4-171">Kopieer de **Sign-Out URL's en SAML Single Sign-On Service** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="e09a4-171">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_configure.png) 

7. <span data-ttu-id="e09a4-173">Om SSO in LockPath Keylight, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="e09a4-173">To enable SSO in LockPath Keylight, perform the following steps:</span></span>
   
    <span data-ttu-id="e09a4-174">a.</span><span class="sxs-lookup"><span data-stu-id="e09a4-174">a.</span></span> <span data-ttu-id="e09a4-175">Aanmelding bij je account LockPath Keylight als administrator.</span><span class="sxs-lookup"><span data-stu-id="e09a4-175">Sign-on to your LockPath Keylight account as administrator.</span></span>
    
    <span data-ttu-id="e09a4-176">b.</span><span class="sxs-lookup"><span data-stu-id="e09a4-176">b.</span></span> <span data-ttu-id="e09a4-177">Klik in het menu bovenaan op **persoon**, en selecteer **Keylight Setup**.</span><span class="sxs-lookup"><span data-stu-id="e09a4-177">In the menu on the top, click **Person**, and select **Keylight Setup**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-keylight-tutorial/401.png) 

    <span data-ttu-id="e09a4-179">c.</span><span class="sxs-lookup"><span data-stu-id="e09a4-179">c.</span></span> <span data-ttu-id="e09a4-180">Klik in de structuurweergave links **SAML**.</span><span class="sxs-lookup"><span data-stu-id="e09a4-180">In the treeview on the left, click **SAML**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-keylight-tutorial/402.png) 

    <span data-ttu-id="e09a4-182">d.</span><span class="sxs-lookup"><span data-stu-id="e09a4-182">d.</span></span> <span data-ttu-id="e09a4-183">Op de **SAML instellingen** dialoogvenster, klikt u op **bewerken**.</span><span class="sxs-lookup"><span data-stu-id="e09a4-183">On the **SAML Settings** dialog, click **Edit**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-keylight-tutorial/404.png) 

8. <span data-ttu-id="e09a4-185">Op de **SAML-instellingen bewerken** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="e09a4-185">On the **Edit SAML Settings** dialog page, perform the following steps:</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-keylight-tutorial/405.png) 
   
    <span data-ttu-id="e09a4-187">a.</span><span class="sxs-lookup"><span data-stu-id="e09a4-187">a.</span></span> <span data-ttu-id="e09a4-188">Stel **SAML-verificatie** naar **Active**.</span><span class="sxs-lookup"><span data-stu-id="e09a4-188">Set **SAML authentication** to **Active**.</span></span>

    <span data-ttu-id="e09a4-189">b.</span><span class="sxs-lookup"><span data-stu-id="e09a4-189">b.</span></span> <span data-ttu-id="e09a4-190">Plak de **SAML Single Sign-On Service-URL** waarde die u hebt gekopieerd vanuit de Azure-portal in de **identiteit Provider aanmeldings-URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="e09a4-190">Paste the **SAML Single Sign-On Service URL** value which you have copied from the Azure portal into the **Identity Provider Login URL** textbox.</span></span>

    <span data-ttu-id="e09a4-191">c.</span><span class="sxs-lookup"><span data-stu-id="e09a4-191">c.</span></span> <span data-ttu-id="e09a4-192">Plak de **Service-URL met eenmalige Sign-Out** waarde die u hebt gekopieerd vanuit de Azure-portal in de **identiteit Provider afmelding URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="e09a4-192">Paste the **Single Sign-Out Service URL** value which you have copied from the Azure portal into the **Identity Provider Logout URL** textbox.</span></span>

    <span data-ttu-id="e09a4-193">d.</span><span class="sxs-lookup"><span data-stu-id="e09a4-193">d.</span></span> <span data-ttu-id="e09a4-194">Klik op **bestand kiezen** uw gedownloade LockPath Keylight certificaat selecteren en klik vervolgens op **Open** om het certificaat te uploaden.</span><span class="sxs-lookup"><span data-stu-id="e09a4-194">Click **Choose File** to select your downloaded LockPath Keylight certificate, and then click **Open** to upload the certificate.</span></span>

    <span data-ttu-id="e09a4-195">e.</span><span class="sxs-lookup"><span data-stu-id="e09a4-195">e.</span></span> <span data-ttu-id="e09a4-196">Ingesteld **SAML-gebruikersnaam locatie** naar **NameIdentifier-element van het onderwerp overzicht**.</span><span class="sxs-lookup"><span data-stu-id="e09a4-196">Set **SAML User Id location** to **NameIdentifier element of the subject statement**.</span></span>
    
    <span data-ttu-id="e09a4-197">f.</span><span class="sxs-lookup"><span data-stu-id="e09a4-197">f.</span></span> <span data-ttu-id="e09a4-198">Geef de **Keylight serviceprovider** met het volgende patroon volgen: **https://&lt;NaamBedrijf&gt;. keylightgrc.com**.</span><span class="sxs-lookup"><span data-stu-id="e09a4-198">Provide the **Keylight Service Provider** using the following pattern: **https://&lt;CompanyName&gt;.keylightgrc.com**.</span></span>
    
    <span data-ttu-id="e09a4-199">g.</span><span class="sxs-lookup"><span data-stu-id="e09a4-199">g.</span></span> <span data-ttu-id="e09a4-200">Stel **automatisch inrichten gebruikers** naar **Active**.</span><span class="sxs-lookup"><span data-stu-id="e09a4-200">Set **Auto-provision users** to **Active**.</span></span>

    <span data-ttu-id="e09a4-201">h.</span><span class="sxs-lookup"><span data-stu-id="e09a4-201">h.</span></span> <span data-ttu-id="e09a4-202">Stel **automatisch inrichten accounttype** naar **volledige gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="e09a4-202">Set **Auto-provision account type** to **Full User**.</span></span>

    <span data-ttu-id="e09a4-203">ik.</span><span class="sxs-lookup"><span data-stu-id="e09a4-203">i.</span></span> <span data-ttu-id="e09a4-204">Stel **automatisch inrichten beveiligingsrol**, selecteer **standaardgebruiker met SAML**.</span><span class="sxs-lookup"><span data-stu-id="e09a4-204">Set **Auto-provision security role**, select **Standard User with SAML**.</span></span>
    
    <span data-ttu-id="e09a4-205">j.</span><span class="sxs-lookup"><span data-stu-id="e09a4-205">j.</span></span> <span data-ttu-id="e09a4-206">Stel **automatisch inrichten beveiliging config**, selecteer **standaardconfiguratie van de gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="e09a4-206">Set **Auto-provision security config**, select **Standard User Configuration**.</span></span>
     
    <span data-ttu-id="e09a4-207">k.</span><span class="sxs-lookup"><span data-stu-id="e09a4-207">k.</span></span> <span data-ttu-id="e09a4-208">In de **e kenmerk** textbox type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="e09a4-208">In the **Email attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
    
    <span data-ttu-id="e09a4-209">l.</span><span class="sxs-lookup"><span data-stu-id="e09a4-209">l.</span></span> <span data-ttu-id="e09a4-210">In de **voornaam kenmerk** textbox type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span><span class="sxs-lookup"><span data-stu-id="e09a4-210">In the **First name attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>
    
    <span data-ttu-id="e09a4-211">m.</span><span class="sxs-lookup"><span data-stu-id="e09a4-211">m.</span></span> <span data-ttu-id="e09a4-212">In de **laatste naamkenmerk** textbox type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span><span class="sxs-lookup"><span data-stu-id="e09a4-212">In the **Last name attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>
    
    <span data-ttu-id="e09a4-213">n.</span><span class="sxs-lookup"><span data-stu-id="e09a4-213">n.</span></span> <span data-ttu-id="e09a4-214">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="e09a4-214">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="e09a4-215">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="e09a4-215">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e09a4-216">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="e09a4-216">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e09a4-217">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e09a4-217">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e09a4-218">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="e09a4-218">Creating an Azure AD test user</span></span>
<span data-ttu-id="e09a4-219">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="e09a4-219">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="e09a4-221">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="e09a4-221">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e09a4-222">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="e09a4-222">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-keylight-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e09a4-224">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="e09a4-224">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-keylight-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e09a4-226">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e09a4-226">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-keylight-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e09a4-228">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="e09a4-228">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-keylight-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e09a4-230">a.</span><span class="sxs-lookup"><span data-stu-id="e09a4-230">a.</span></span> <span data-ttu-id="e09a4-231">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e09a4-231">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e09a4-232">b.</span><span class="sxs-lookup"><span data-stu-id="e09a4-232">b.</span></span> <span data-ttu-id="e09a4-233">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e09a4-233">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e09a4-234">c.</span><span class="sxs-lookup"><span data-stu-id="e09a4-234">c.</span></span> <span data-ttu-id="e09a4-235">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="e09a4-235">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e09a4-236">d.</span><span class="sxs-lookup"><span data-stu-id="e09a4-236">d.</span></span> <span data-ttu-id="e09a4-237">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="e09a4-237">Click **Create**.</span></span>
 
### <a name="creating-a-lockpath-keylight-test-user"></a><span data-ttu-id="e09a4-238">Een testgebruiker LockPath Keylight maken</span><span class="sxs-lookup"><span data-stu-id="e09a4-238">Creating a LockPath Keylight test user</span></span>

<span data-ttu-id="e09a4-239">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in LockPath Keylight maken.</span><span class="sxs-lookup"><span data-stu-id="e09a4-239">In this section, you create a user called Britta Simon in LockPath Keylight.</span></span> <span data-ttu-id="e09a4-240">LockPath Keylight ondersteunt just-in-time-inrichting, die standaard is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="e09a4-240">LockPath Keylight supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="e09a4-241">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="e09a4-241">There is no action item for you in this section.</span></span> <span data-ttu-id="e09a4-242">Een nieuwe gebruiker wordt gemaakt bij het openen van LockPath Keylight als de gebruiker nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="e09a4-242">A new user is created when accessing LockPath Keylight if the user doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="e09a4-243">Als u een gebruiker handmatig maken wilt, moet u contact op met de [LockPath Keylight Client ondersteuningsteam](https://www.lockpath.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="e09a4-243">If you need to create a user manually, you need to contact the [LockPath Keylight Client support team](https://www.lockpath.com/contact/).</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e09a4-244">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="e09a4-244">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e09a4-245">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan LockPath Keylight.</span><span class="sxs-lookup"><span data-stu-id="e09a4-245">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LockPath Keylight.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="e09a4-247">**Britta Simon om aan te wijzen LockPath Keylight, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="e09a4-247">**To assign Britta Simon to LockPath Keylight, perform the following steps:**</span></span>

1. <span data-ttu-id="e09a4-248">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="e09a4-248">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="e09a4-250">Selecteer in de lijst met toepassingen **LockPath Keylight**.</span><span class="sxs-lookup"><span data-stu-id="e09a4-250">In the applications list, select **LockPath Keylight**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_app.png) 

3. <span data-ttu-id="e09a4-252">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="e09a4-252">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="e09a4-254">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="e09a4-254">Click **Add** button.</span></span> <span data-ttu-id="e09a4-255">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e09a4-255">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="e09a4-257">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="e09a4-257">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e09a4-258">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e09a4-258">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e09a4-259">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e09a4-259">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e09a4-260">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="e09a4-260">Testing single sign-on</span></span>

<span data-ttu-id="e09a4-261">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="e09a4-261">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e09a4-262">Als u op de tegel LockPath Keylight in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing LockPath Keylight.</span><span class="sxs-lookup"><span data-stu-id="e09a4-262">When you click the LockPath Keylight tile in the Access Panel, you should get automatically signed-on to your LockPath Keylight application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="e09a4-263">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="e09a4-263">Additional resources</span></span>

* [<span data-ttu-id="e09a4-264">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e09a4-264">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e09a4-265">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e09a4-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_203.png

