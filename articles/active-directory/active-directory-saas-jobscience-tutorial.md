---
title: 'Zelfstudie: Azure Active Directory-integratie met Jobscience | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Jobscience.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 77282dcc-bbe2-4728-953d-adb4ab6a713b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 66bec35a8f17482433dbf02827b90620d1cff378
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jobscience"></a><span data-ttu-id="bac5d-103">Zelfstudie: Azure Active Directory-integratie met Jobscience</span><span class="sxs-lookup"><span data-stu-id="bac5d-103">Tutorial: Azure Active Directory integration with Jobscience</span></span>

<span data-ttu-id="bac5d-104">In deze zelfstudie leert u hoe Jobscience integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bac5d-104">In this tutorial, you learn how to integrate Jobscience with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bac5d-105">Jobscience integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="bac5d-105">Integrating Jobscience with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="bac5d-106">U kunt beheren in Azure AD die toegang tot Jobscience heeft</span><span class="sxs-lookup"><span data-stu-id="bac5d-106">You can control in Azure AD who has access to Jobscience</span></span>
- <span data-ttu-id="bac5d-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Jobscience (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="bac5d-107">You can enable your users to automatically get signed-on to Jobscience (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bac5d-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="bac5d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="bac5d-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bac5d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bac5d-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="bac5d-110">Prerequisites</span></span>

<span data-ttu-id="bac5d-111">Voor het configureren van Azure AD-integratie met Jobscience, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="bac5d-111">To configure Azure AD integration with Jobscience, you need the following items:</span></span>

- <span data-ttu-id="bac5d-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="bac5d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bac5d-113">Een Jobscience eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="bac5d-113">A Jobscience single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bac5d-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="bac5d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bac5d-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="bac5d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bac5d-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="bac5d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bac5d-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand hier downloaden: [proefversie aanbieding](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bac5d-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bac5d-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="bac5d-118">Scenario description</span></span>
<span data-ttu-id="bac5d-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="bac5d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bac5d-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="bac5d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bac5d-121">Jobscience uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="bac5d-121">Adding Jobscience from the gallery</span></span>
2. <span data-ttu-id="bac5d-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="bac5d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jobscience-from-the-gallery"></a><span data-ttu-id="bac5d-123">Jobscience uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="bac5d-123">Adding Jobscience from the gallery</span></span>
<span data-ttu-id="bac5d-124">Voor het configureren van de integratie van Jobscience in Azure AD, moet u Jobscience uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="bac5d-124">To configure the integration of Jobscience into Azure AD, you need to add Jobscience from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="bac5d-125">**Als u wilt toevoegen Jobscience uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="bac5d-125">**To add Jobscience from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="bac5d-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="bac5d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="bac5d-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="bac5d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="bac5d-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="bac5d-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="bac5d-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="bac5d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="bac5d-133">Typ in het zoekvak **Jobscience**.</span><span class="sxs-lookup"><span data-stu-id="bac5d-133">In the search box, type **Jobscience**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_search.png)

5. <span data-ttu-id="bac5d-135">Selecteer in het deelvenster resultaten **Jobscience**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="bac5d-135">In the results panel, select **Jobscience**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bac5d-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="bac5d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bac5d-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Jobscience op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="bac5d-138">In this section, you configure and test Azure AD single sign-on with Jobscience based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="bac5d-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Jobscience is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bac5d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Jobscience is to a user in Azure AD.</span></span> <span data-ttu-id="bac5d-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Jobscience tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="bac5d-140">In other words, a link relationship between an Azure AD user and the related user in Jobscience needs to be established.</span></span>

<span data-ttu-id="bac5d-141">Wijs in Jobscience, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="bac5d-141">In Jobscience, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="bac5d-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Jobscience, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="bac5d-142">To configure and test Azure AD single sign-on with Jobscience, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="bac5d-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="bac5d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="bac5d-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bac5d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bac5d-145">**[Maken van een testgebruiker Jobscience](#creating-a-jobscience-test-user)**  - Jobscience die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="bac5d-145">**[Creating a Jobscience test user](#creating-a-jobscience-test-user)** - to have a counterpart of Britta Simon in Jobscience that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="bac5d-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="bac5d-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bac5d-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="bac5d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bac5d-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="bac5d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bac5d-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Jobscience configureren.</span><span class="sxs-lookup"><span data-stu-id="bac5d-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Jobscience application.</span></span>

<span data-ttu-id="bac5d-150">**Voor het configureren van Azure AD eenmalige aanmelding met Jobscience, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="bac5d-150">**To configure Azure AD single sign-on with Jobscience, perform the following steps:**</span></span>

1. <span data-ttu-id="bac5d-151">In de Azure-portal op de **Jobscience** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="bac5d-151">In the Azure portal, on the **Jobscience** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="bac5d-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="bac5d-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_samlbase.png)

3. <span data-ttu-id="bac5d-155">Op de **Jobscience domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="bac5d-155">On the **Jobscience Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_url.png)

    <span data-ttu-id="bac5d-157">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`http://<company name>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="bac5d-157">In the **Sign-on URL** textbox, type a URL using the following pattern:  `http://<company name>.my.salesforce.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="bac5d-158">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="bac5d-158">This value is not real.</span></span> <span data-ttu-id="bac5d-159">Deze waarde bijwerken met de werkelijke URL voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="bac5d-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="bac5d-160">Deze waarde krijgen door [Jobscience Client ondersteuningsteam](https://www.jobscience.com/support) of van het profiel voor eenmalige aanmelding wordt u maken die later in de zelfstudie wordt uitgelegd.</span><span class="sxs-lookup"><span data-stu-id="bac5d-160">Get this value by [Jobscience Client support team](https://www.jobscience.com/support) or from the SSO profile you will create which is explained later in the tutorial.</span></span> 
 
4. <span data-ttu-id="bac5d-161">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="bac5d-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_certificate.png) 

5. <span data-ttu-id="bac5d-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="bac5d-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jobscience-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="bac5d-165">Op de **Jobscience configuratie** sectie, klikt u op **configureren Jobscience** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="bac5d-165">On the **Jobscience Configuration** section, click **Configure Jobscience** to open **Configure sign-on** window.</span></span> <span data-ttu-id="bac5d-166">Kopieer de **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="bac5d-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_configure.png) 

7. <span data-ttu-id="bac5d-168">Meld u aan bij uw bedrijf Jobscience site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="bac5d-168">Log in to your Jobscience company site as an administrator.</span></span>

8. <span data-ttu-id="bac5d-169">Ga naar **Setup**.</span><span class="sxs-lookup"><span data-stu-id="bac5d-169">Go to **Setup**.</span></span>
   
   <span data-ttu-id="bac5d-170">![Setup](./media/active-directory-saas-jobscience-tutorial/IC784358.png "Setup")</span><span class="sxs-lookup"><span data-stu-id="bac5d-170">![Setup](./media/active-directory-saas-jobscience-tutorial/IC784358.png "Setup")</span></span>

9. <span data-ttu-id="bac5d-171">In het navigatiedeelvenster links in de **beheren** sectie, klikt u op **domeinbeheer** Vouw de bijbehorende sectie en klik vervolgens op **mijn domein** openen van de **Mijn domein** pagina.</span><span class="sxs-lookup"><span data-stu-id="bac5d-171">On the left navigation pane, in the **Administer** section, click **Domain Management** to expand the related section, and then click **My Domain** to open the **My Domain** page.</span></span> 
   
   <span data-ttu-id="bac5d-172">![Mijn domein](./media/active-directory-saas-jobscience-tutorial/ic767825.png "mijn domein")</span><span class="sxs-lookup"><span data-stu-id="bac5d-172">![My Domain](./media/active-directory-saas-jobscience-tutorial/ic767825.png "My Domain")</span></span>

10. <span data-ttu-id="bac5d-173">Om te controleren of uw domein correct is ingesteld, zorg ervoor dat deze wordt '**stap 4 geïmplementeerd naar gebruikers**' en bekijk uw '**mijn domeininstellingen**'.</span><span class="sxs-lookup"><span data-stu-id="bac5d-173">To verify that your domain has been set up correctly, make sure that it is in “**Step 4 Deployed to Users**” and review your “**My Domain Settings**”.</span></span>

    <span data-ttu-id="bac5d-174">![Domein geïmplementeerd voor gebruiker](./media/active-directory-saas-jobscience-tutorial/ic784377.png "domein geïmplementeerd voor gebruiker")</span><span class="sxs-lookup"><span data-stu-id="bac5d-174">![Domain Deployed to User](./media/active-directory-saas-jobscience-tutorial/ic784377.png "Domain Deployed to User")</span></span>

11. <span data-ttu-id="bac5d-175">Klik op de site van het bedrijf Jobscience **beveiligingsmechanismen**, en klik vervolgens op **instellingen voor eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="bac5d-175">On the Jobscience company site, click **Security Controls**, and then click **Single Sign-On Settings**.</span></span>
    
    <span data-ttu-id="bac5d-176">![Beveiligingsmechanismen](./media/active-directory-saas-jobscience-tutorial/ic784364.png "beveiligingsmechanismen")</span><span class="sxs-lookup"><span data-stu-id="bac5d-176">![Security Controls](./media/active-directory-saas-jobscience-tutorial/ic784364.png "Security Controls")</span></span>

12. <span data-ttu-id="bac5d-177">In de **instellingen voor eenmalige aanmelding** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="bac5d-177">In the **Single Sign-On Settings** section, perform the following steps:</span></span>
    
    <span data-ttu-id="bac5d-178">![Eenmalige aanmelding instellingen](./media/active-directory-saas-jobscience-tutorial/ic781026.png "eenmalige aanmelding-instellingen")</span><span class="sxs-lookup"><span data-stu-id="bac5d-178">![Single Sign-On Settings](./media/active-directory-saas-jobscience-tutorial/ic781026.png "Single Sign-On Settings")</span></span>
    
    <span data-ttu-id="bac5d-179">a.</span><span class="sxs-lookup"><span data-stu-id="bac5d-179">a.</span></span> <span data-ttu-id="bac5d-180">Selecteer **SAML ingeschakeld**.</span><span class="sxs-lookup"><span data-stu-id="bac5d-180">Select **SAML Enabled**.</span></span>

    <span data-ttu-id="bac5d-181">b.</span><span class="sxs-lookup"><span data-stu-id="bac5d-181">b.</span></span> <span data-ttu-id="bac5d-182">Klik op **Nieuw**.</span><span class="sxs-lookup"><span data-stu-id="bac5d-182">Click **New**.</span></span>

13. <span data-ttu-id="bac5d-183">Op de **SAML Single Sign-On instelling bewerken** dialoogvenster de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="bac5d-183">On the **SAML Single Sign-On Setting Edit** dialog, perform the following steps:</span></span>
    
    <span data-ttu-id="bac5d-184">![Afzonderlijke SAML aanmelding instelling](./media/active-directory-saas-jobscience-tutorial/ic784365.png "SAML Single Sign-On-instelling")</span><span class="sxs-lookup"><span data-stu-id="bac5d-184">![SAML Single Sign-On Setting](./media/active-directory-saas-jobscience-tutorial/ic784365.png "SAML Single Sign-On Setting")</span></span>
    
    <span data-ttu-id="bac5d-185">a.</span><span class="sxs-lookup"><span data-stu-id="bac5d-185">a.</span></span> <span data-ttu-id="bac5d-186">In de **naam** textbox, typ een naam voor uw configuratie.</span><span class="sxs-lookup"><span data-stu-id="bac5d-186">In the **Name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="bac5d-187">b.</span><span class="sxs-lookup"><span data-stu-id="bac5d-187">b.</span></span> <span data-ttu-id="bac5d-188">In **verlener** textbox, plak de waarde van **SAML entiteit-ID**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="bac5d-188">In **Issuer** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="bac5d-189">c.</span><span class="sxs-lookup"><span data-stu-id="bac5d-189">c.</span></span> <span data-ttu-id="bac5d-190">In de **entiteit-Id** textbox type`https://salesforce-jobscience.com`</span><span class="sxs-lookup"><span data-stu-id="bac5d-190">In the **Entity Id** textbox, type `https://salesforce-jobscience.com`</span></span>

    <span data-ttu-id="bac5d-191">d.</span><span class="sxs-lookup"><span data-stu-id="bac5d-191">d.</span></span> <span data-ttu-id="bac5d-192">Klik op **Bladeren** om uw Azure AD-certificaat te uploaden.</span><span class="sxs-lookup"><span data-stu-id="bac5d-192">Click **Browse** to upload your Azure AD certificate.</span></span>

    <span data-ttu-id="bac5d-193">e.</span><span class="sxs-lookup"><span data-stu-id="bac5d-193">e.</span></span> <span data-ttu-id="bac5d-194">Als **SAML identiteitstype**, selecteer **Assertion bevat de Federation-ID van het gebruikersobject**.</span><span class="sxs-lookup"><span data-stu-id="bac5d-194">As **SAML Identity Type**, select **Assertion contains the Federation ID from the User object**.</span></span>

    <span data-ttu-id="bac5d-195">f.</span><span class="sxs-lookup"><span data-stu-id="bac5d-195">f.</span></span> <span data-ttu-id="bac5d-196">Als **SAML identiteit locatie**, selecteer **identiteit is in het element NameIdentfier van het onderwerp overzicht**.</span><span class="sxs-lookup"><span data-stu-id="bac5d-196">As **SAML Identity Location**, select **Identity is in the NameIdentfier element of the Subject statement**.</span></span>

    <span data-ttu-id="bac5d-197">g.</span><span class="sxs-lookup"><span data-stu-id="bac5d-197">g.</span></span> <span data-ttu-id="bac5d-198">In **identiteit Provider aanmeldings-URL** textbox, plak de waarde van **SAML Single Sign-On Service-URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="bac5d-198">In **Identity Provider Login URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="bac5d-199">h.</span><span class="sxs-lookup"><span data-stu-id="bac5d-199">h.</span></span> <span data-ttu-id="bac5d-200">In **identiteit Provider afmelding URL** textbox, plak de waarde van **Sign-Out URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="bac5d-200">In **Identity Provider Logout URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="bac5d-201">ik.</span><span class="sxs-lookup"><span data-stu-id="bac5d-201">i.</span></span> <span data-ttu-id="bac5d-202">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="bac5d-202">Click **Save**.</span></span>

14. <span data-ttu-id="bac5d-203">In het navigatiedeelvenster links in de **beheren** sectie, klikt u op **domeinbeheer** Vouw de bijbehorende sectie en klik vervolgens op **mijn domein** openen van de **Mijn domein** pagina.</span><span class="sxs-lookup"><span data-stu-id="bac5d-203">On the left navigation pane, in the **Administer** section, click **Domain Management** to expand the related section, and then click **My Domain** to open the **My Domain** page.</span></span> 
    
    <span data-ttu-id="bac5d-204">![Mijn domein](./media/active-directory-saas-jobscience-tutorial/ic767825.png "mijn domein")</span><span class="sxs-lookup"><span data-stu-id="bac5d-204">![My Domain](./media/active-directory-saas-jobscience-tutorial/ic767825.png "My Domain")</span></span>

15. <span data-ttu-id="bac5d-205">Op de **mijn domein** pagina in de **aanmelding pagina huisstijl** sectie, klikt u op **bewerken**.</span><span class="sxs-lookup"><span data-stu-id="bac5d-205">On the **My Domain** page, in the **Login Page Branding** section, click **Edit**.</span></span>
    
    <span data-ttu-id="bac5d-206">![Aanmeldingspagina huisstijl](./media/active-directory-saas-jobscience-tutorial/ic767826.png "aanmeldingspagina huisstijl")</span><span class="sxs-lookup"><span data-stu-id="bac5d-206">![Login Page Branding](./media/active-directory-saas-jobscience-tutorial/ic767826.png "Login Page Branding")</span></span>

16. <span data-ttu-id="bac5d-207">Op de **aanmelding pagina huisstijl** pagina in de **verificatieservice** sectie, de naam van uw **SAML SSO instellingen** wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="bac5d-207">On the **Login Page Branding** page, in the **Authentication Service** section, the name of your **SAML SSO Settings** is displayed.</span></span> <span data-ttu-id="bac5d-208">Selecteer deze en klik vervolgens op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="bac5d-208">Select it, and then click **Save**.</span></span>
    
    <span data-ttu-id="bac5d-209">![Aanmeldingspagina huisstijl](./media/active-directory-saas-jobscience-tutorial/ic784366.png "aanmeldingspagina huisstijl")</span><span class="sxs-lookup"><span data-stu-id="bac5d-209">![Login Page Branding](./media/active-directory-saas-jobscience-tutorial/ic784366.png "Login Page Branding")</span></span>

17. <span data-ttu-id="bac5d-210">Gestart om op te halen van de Serviceprovider voor eenmalige aanmeldings-URL wordt geklikt op de **instellingen voor eenmalige aanmelding** in de **beveiligingsmechanismen** sectie menu.</span><span class="sxs-lookup"><span data-stu-id="bac5d-210">To get the SP initiated Single Sign on Login URL click on the **Single Sign On settings** in the **Security Controls** menu section.</span></span>

    <span data-ttu-id="bac5d-211">![Beveiligingsmechanismen](./media/active-directory-saas-jobscience-tutorial/ic784368.png "beveiligingsmechanismen")</span><span class="sxs-lookup"><span data-stu-id="bac5d-211">![Security Controls](./media/active-directory-saas-jobscience-tutorial/ic784368.png "Security Controls")</span></span>
    
    <span data-ttu-id="bac5d-212">Klik op de SSO-profiel dat u hebt gemaakt in de bovenstaande stap.</span><span class="sxs-lookup"><span data-stu-id="bac5d-212">Click the SSO profile you have created in the step above.</span></span> <span data-ttu-id="bac5d-213">Deze pagina bevat de eenmalige aanmelding op de URL voor uw bedrijf (bijvoorbeeld [https://companyname.my.salesforce.com?so=companyid](https://companyname.my.salesforce.com?so=companyid).</span><span class="sxs-lookup"><span data-stu-id="bac5d-213">This page shows the Single Sign on URL for your company (for example, [https://companyname.my.salesforce.com?so=companyid](https://companyname.my.salesforce.com?so=companyid).</span></span>    

> [!TIP]
> <span data-ttu-id="bac5d-214">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="bac5d-214">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="bac5d-215">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="bac5d-215">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="bac5d-216">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bac5d-216">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bac5d-217">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="bac5d-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="bac5d-218">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="bac5d-218">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="bac5d-220">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="bac5d-220">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="bac5d-221">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="bac5d-221">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jobscience-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bac5d-223">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="bac5d-223">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jobscience-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bac5d-225">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="bac5d-225">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jobscience-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bac5d-227">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="bac5d-227">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jobscience-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bac5d-229">a.</span><span class="sxs-lookup"><span data-stu-id="bac5d-229">a.</span></span> <span data-ttu-id="bac5d-230">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bac5d-230">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bac5d-231">b.</span><span class="sxs-lookup"><span data-stu-id="bac5d-231">b.</span></span> <span data-ttu-id="bac5d-232">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="bac5d-232">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bac5d-233">c.</span><span class="sxs-lookup"><span data-stu-id="bac5d-233">c.</span></span> <span data-ttu-id="bac5d-234">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="bac5d-234">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="bac5d-235">d.</span><span class="sxs-lookup"><span data-stu-id="bac5d-235">d.</span></span> <span data-ttu-id="bac5d-236">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="bac5d-236">Click **Create**.</span></span>
 
### <a name="creating-a-jobscience-test-user"></a><span data-ttu-id="bac5d-237">Een testgebruiker Jobscience maken</span><span class="sxs-lookup"><span data-stu-id="bac5d-237">Creating a Jobscience test user</span></span>

<span data-ttu-id="bac5d-238">Om Azure AD-gebruikers zich aanmelden bij Jobscience inschakelt, moeten ze worden ingericht in Jobscience.</span><span class="sxs-lookup"><span data-stu-id="bac5d-238">In order to enable Azure AD users to log in to Jobscience, they must be provisioned into Jobscience.</span></span> <span data-ttu-id="bac5d-239">In het geval van Jobscience is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="bac5d-239">In the case of Jobscience, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="bac5d-240">U kunt andere Jobscience gebruiker account hulpmiddelen voor het maken of API's geleverd door Jobscience om in te richten Azure Active Directory-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="bac5d-240">You can use any other Jobscience user account creation tools or APIs provided by Jobscience to provision Azure Active Directory user accounts.</span></span>
>  
        
<span data-ttu-id="bac5d-241">**Als u wilt configureren voor gebruikers inrichten, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="bac5d-241">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="bac5d-242">Meld u aan bij uw **Jobscience** bedrijf site als administrator.</span><span class="sxs-lookup"><span data-stu-id="bac5d-242">Log in to your **Jobscience** company site as administrator.</span></span>

2. <span data-ttu-id="bac5d-243">Ga naar instellingen.</span><span class="sxs-lookup"><span data-stu-id="bac5d-243">Go to Setup.</span></span>
   
   <span data-ttu-id="bac5d-244">![Setup](./media/active-directory-saas-jobscience-tutorial/ic784358.png "Setup")</span><span class="sxs-lookup"><span data-stu-id="bac5d-244">![Setup](./media/active-directory-saas-jobscience-tutorial/ic784358.png "Setup")</span></span>
3. <span data-ttu-id="bac5d-245">Ga naar **gebruikers beheren \> gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="bac5d-245">Go to **Manage Users \> Users**.</span></span>
   
   <span data-ttu-id="bac5d-246">![Gebruikers](./media/active-directory-saas-jobscience-tutorial/ic784369.png "gebruikers")</span><span class="sxs-lookup"><span data-stu-id="bac5d-246">![Users](./media/active-directory-saas-jobscience-tutorial/ic784369.png "Users")</span></span>
4. <span data-ttu-id="bac5d-247">Klik op **nieuwe gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="bac5d-247">Click **New User**.</span></span>
   
   <span data-ttu-id="bac5d-248">![Alle gebruikers](./media/active-directory-saas-jobscience-tutorial/ic784370.png "alle gebruikers")</span><span class="sxs-lookup"><span data-stu-id="bac5d-248">![All Users](./media/active-directory-saas-jobscience-tutorial/ic784370.png "All Users")</span></span>
5. <span data-ttu-id="bac5d-249">Op de **-gebruiker bewerken** dialoogvenster de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="bac5d-249">On the **Edit User** dialog, perform the following steps:</span></span>
   
   <span data-ttu-id="bac5d-250">![Gebruiker bewerken](./media/active-directory-saas-jobscience-tutorial/ic784371.png "gebruiker bewerken")</span><span class="sxs-lookup"><span data-stu-id="bac5d-250">![User Edit](./media/active-directory-saas-jobscience-tutorial/ic784371.png "User Edit")</span></span>
   
   <span data-ttu-id="bac5d-251">a.</span><span class="sxs-lookup"><span data-stu-id="bac5d-251">a.</span></span> <span data-ttu-id="bac5d-252">In de **voornaam** textbox, typ een naam van de eerste van de gebruiker zoals Britta.</span><span class="sxs-lookup"><span data-stu-id="bac5d-252">In the **First Name** textbox, type a first name of the user like Britta.</span></span>
   
   <span data-ttu-id="bac5d-253">b.</span><span class="sxs-lookup"><span data-stu-id="bac5d-253">b.</span></span> <span data-ttu-id="bac5d-254">In de **achternaam** textbox, typt u de achternaam van de gebruiker zoals Simon.</span><span class="sxs-lookup"><span data-stu-id="bac5d-254">In the **Last Name** textbox, type a last name of the user like Simon.</span></span>
   
   <span data-ttu-id="bac5d-255">c.</span><span class="sxs-lookup"><span data-stu-id="bac5d-255">c.</span></span> <span data-ttu-id="bac5d-256">In de **Alias** textbox, typt u een aliasnaam van de gebruiker zoals brittas.</span><span class="sxs-lookup"><span data-stu-id="bac5d-256">In the **Alias** textbox, type an alias name of the user like brittas.</span></span>

   <span data-ttu-id="bac5d-257">d.</span><span class="sxs-lookup"><span data-stu-id="bac5d-257">d.</span></span> <span data-ttu-id="bac5d-258">In de **e** textbox, typ het e-mailadres van gebruiker, zoals Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="bac5d-258">In the **Email** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>

   <span data-ttu-id="bac5d-259">e.</span><span class="sxs-lookup"><span data-stu-id="bac5d-259">e.</span></span> <span data-ttu-id="bac5d-260">In de **gebruikersnaam** textbox, typ een naam van gebruiker, zoals Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="bac5d-260">In the **User Name** textbox, type a user name of user like Brittasimon@contoso.com.</span></span>

   <span data-ttu-id="bac5d-261">f.</span><span class="sxs-lookup"><span data-stu-id="bac5d-261">f.</span></span> <span data-ttu-id="bac5d-262">In de **bijnaam** textbox, typ een naam nick van gebruiker zoals Simon.</span><span class="sxs-lookup"><span data-stu-id="bac5d-262">In the **Nick Name** textbox, type a nick name of user like Simon.</span></span>

   <span data-ttu-id="bac5d-263">g.</span><span class="sxs-lookup"><span data-stu-id="bac5d-263">g.</span></span> <span data-ttu-id="bac5d-264">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="bac5d-264">Click **Save**.</span></span>

    
> [!NOTE]
> <span data-ttu-id="bac5d-265">De houder van Azure Active Directory-account ontvangt een e-mailbericht en volgt een koppeling om hun account te bevestigen voordat deze geactiveerd wordt.</span><span class="sxs-lookup"><span data-stu-id="bac5d-265">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="bac5d-266">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="bac5d-266">Assigning the Azure AD test user</span></span>

<span data-ttu-id="bac5d-267">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Jobscience.</span><span class="sxs-lookup"><span data-stu-id="bac5d-267">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Jobscience.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="bac5d-269">**Britta Simon om aan te wijzen Jobscience, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="bac5d-269">**To assign Britta Simon to Jobscience, perform the following steps:**</span></span>

1. <span data-ttu-id="bac5d-270">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="bac5d-270">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="bac5d-272">Selecteer in de lijst met toepassingen **Jobscience**.</span><span class="sxs-lookup"><span data-stu-id="bac5d-272">In the applications list, select **Jobscience**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_app.png) 

3. <span data-ttu-id="bac5d-274">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="bac5d-274">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="bac5d-276">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="bac5d-276">Click **Add** button.</span></span> <span data-ttu-id="bac5d-277">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="bac5d-277">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="bac5d-279">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="bac5d-279">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="bac5d-280">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="bac5d-280">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bac5d-281">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="bac5d-281">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bac5d-282">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="bac5d-282">Testing single sign-on</span></span>

<span data-ttu-id="bac5d-283">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="bac5d-283">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="bac5d-284">Als u op de tegel Jobscience in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Jobscience.</span><span class="sxs-lookup"><span data-stu-id="bac5d-284">When you click the Jobscience tile in the Access Panel, you should get automatically signed-on to your Jobscience application.</span></span>
<span data-ttu-id="bac5d-285">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bac5d-285">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bac5d-286">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="bac5d-286">Additional resources</span></span>

* [<span data-ttu-id="bac5d-287">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bac5d-287">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bac5d-288">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bac5d-288">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_203.png

