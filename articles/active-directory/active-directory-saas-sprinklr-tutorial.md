---
title: 'Zelfstudie: Azure Active Directory-integratie met Sprinklr | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Sprinklr.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b33938a1-25a5-484c-8e75-7dc6de2d534d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 6e1622cd55e3b0e8063604ac9dc0cb0673fa9753
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sprinklr"></a><span data-ttu-id="2234b-103">Zelfstudie: Azure Active Directory-integratie met Sprinklr</span><span class="sxs-lookup"><span data-stu-id="2234b-103">Tutorial: Azure Active Directory integration with Sprinklr</span></span>

<span data-ttu-id="2234b-104">In deze zelfstudie leert u hoe Sprinklr integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2234b-104">In this tutorial, you learn how to integrate Sprinklr with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2234b-105">Sprinklr integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="2234b-105">Integrating Sprinklr with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2234b-106">U kunt beheren in Azure AD die toegang tot Sprinklr heeft</span><span class="sxs-lookup"><span data-stu-id="2234b-106">You can control in Azure AD who has access to Sprinklr</span></span>
- <span data-ttu-id="2234b-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Sprinklr (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="2234b-107">You can enable your users to automatically get signed-on to Sprinklr (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2234b-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="2234b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="2234b-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2234b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2234b-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="2234b-110">Prerequisites</span></span>

<span data-ttu-id="2234b-111">Voor het configureren van Azure AD-integratie met Sprinklr, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="2234b-111">To configure Azure AD integration with Sprinklr, you need the following items:</span></span>

- <span data-ttu-id="2234b-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="2234b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2234b-113">Een Sprinklr eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="2234b-113">A Sprinklr single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2234b-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="2234b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2234b-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="2234b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2234b-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="2234b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2234b-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2234b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2234b-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="2234b-118">Scenario description</span></span>
<span data-ttu-id="2234b-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="2234b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2234b-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="2234b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2234b-121">Sprinklr uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="2234b-121">Adding Sprinklr from the gallery</span></span>
2. <span data-ttu-id="2234b-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="2234b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sprinklr-from-the-gallery"></a><span data-ttu-id="2234b-123">Sprinklr uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="2234b-123">Adding Sprinklr from the gallery</span></span>
<span data-ttu-id="2234b-124">Voor het configureren van de integratie van Sprinklr in Azure AD, moet u Sprinklr uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="2234b-124">To configure the integration of Sprinklr into Azure AD, you need to add Sprinklr from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2234b-125">**Als u wilt toevoegen Sprinklr uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="2234b-125">**To add Sprinklr from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2234b-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="2234b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2234b-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="2234b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2234b-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="2234b-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="2234b-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2234b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="2234b-133">Typ in het zoekvak **Sprinklr**.</span><span class="sxs-lookup"><span data-stu-id="2234b-133">In the search box, type **Sprinklr**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_search.png)

5. <span data-ttu-id="2234b-135">Selecteer in het deelvenster resultaten **Sprinklr**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="2234b-135">In the results panel, select **Sprinklr**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2234b-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="2234b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2234b-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Sprinklr op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="2234b-138">In this section, you configure and test Azure AD single sign-on with Sprinklr based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="2234b-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Sprinklr is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2234b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Sprinklr is to a user in Azure AD.</span></span> <span data-ttu-id="2234b-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Sprinklr tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="2234b-140">In other words, a link relationship between an Azure AD user and the related user in Sprinklr needs to be established.</span></span>

<span data-ttu-id="2234b-141">Wijs in Sprinklr, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="2234b-141">In Sprinklr, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="2234b-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Sprinklr, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="2234b-142">To configure and test Azure AD single sign-on with Sprinklr, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2234b-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2234b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2234b-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2234b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2234b-145">**[Maken van een testgebruiker Sprinklr](#creating-a-sprinklr-test-user)**  - Sprinklr die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="2234b-145">**[Creating a Sprinklr test user](#creating-a-sprinklr-test-user)** - to have a counterpart of Britta Simon in Sprinklr that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="2234b-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="2234b-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2234b-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="2234b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2234b-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="2234b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2234b-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Sprinklr configureren.</span><span class="sxs-lookup"><span data-stu-id="2234b-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Sprinklr application.</span></span>

<span data-ttu-id="2234b-150">**Voor het configureren van Azure AD eenmalige aanmelding met Sprinklr, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="2234b-150">**To configure Azure AD single sign-on with Sprinklr, perform the following steps:**</span></span>

1. <span data-ttu-id="2234b-151">In de Azure-portal op de **Sprinklr** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="2234b-151">In the Azure portal, on the **Sprinklr** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="2234b-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="2234b-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_samlbase.png)

3. <span data-ttu-id="2234b-155">Op de **Sprinklr domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="2234b-155">On the **Sprinklr Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_url.png)

    <span data-ttu-id="2234b-157">a.</span><span class="sxs-lookup"><span data-stu-id="2234b-157">a.</span></span> <span data-ttu-id="2234b-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<subdomain>.sprinklr.com`</span><span class="sxs-lookup"><span data-stu-id="2234b-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.sprinklr.com`</span></span>

    <span data-ttu-id="2234b-159">b.</span><span class="sxs-lookup"><span data-stu-id="2234b-159">b.</span></span> <span data-ttu-id="2234b-160">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<subdomain>.sprinklr.com`</span><span class="sxs-lookup"><span data-stu-id="2234b-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.sprinklr.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2234b-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="2234b-161">These values are not real.</span></span> <span data-ttu-id="2234b-162">Werk de waarde met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="2234b-162">Update the value with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="2234b-163">Neem contact op met [Sprinklr Client ondersteuningsteam](https://www.sprinklr.com/contact-us/) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="2234b-163">Contact [Sprinklr Client support team](https://www.sprinklr.com/contact-us/) to get these values.</span></span> 
 
4. <span data-ttu-id="2234b-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="2234b-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_certificate.png) 

5. <span data-ttu-id="2234b-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="2234b-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sprinklr-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2234b-168">Op de **Sprinklr configuratie** sectie, klikt u op **configureren Sprinklr** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="2234b-168">On the **Sprinklr Configuration** section, click **Configure Sprinklr** to open **Configure sign-on** window.</span></span> <span data-ttu-id="2234b-169">Kopieer de **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="2234b-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

7. <span data-ttu-id="2234b-170">In een ander browservenster, meld u aan bij uw bedrijf Sprinklr site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="2234b-170">In a different web browser window, log in to your Sprinklr company site as an administrator.</span></span>

8. <span data-ttu-id="2234b-171">Ga naar **beheer \> instellingen**.</span><span class="sxs-lookup"><span data-stu-id="2234b-171">Go to **Administration \> Settings**.</span></span>
   
    <span data-ttu-id="2234b-172">![Beheer](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "beheer")</span><span class="sxs-lookup"><span data-stu-id="2234b-172">![Administration](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Administration")</span></span>

9. <span data-ttu-id="2234b-173">Ga naar **beheren Partner \> eenmalige** op in het linkerdeelvenster.</span><span class="sxs-lookup"><span data-stu-id="2234b-173">Go to **Manage Partner \> Single Sign** on from the left pane.</span></span>
   
    <span data-ttu-id="2234b-174">![Partner beheren](./media/active-directory-saas-sprinklr-tutorial/ic782908.png "Partner beheren")</span><span class="sxs-lookup"><span data-stu-id="2234b-174">![Manage Partner](./media/active-directory-saas-sprinklr-tutorial/ic782908.png "Manage Partner")</span></span>

10. <span data-ttu-id="2234b-175">Klik op **+ toevoegen voor eenmalige aanmeldingen**.</span><span class="sxs-lookup"><span data-stu-id="2234b-175">Click **+Add Single Sign Ons**.</span></span>
   
    <span data-ttu-id="2234b-176">![Eenmalige aanmeldingen](./media/active-directory-saas-sprinklr-tutorial/ic782909.png "eenmalige aanmeldingen")</span><span class="sxs-lookup"><span data-stu-id="2234b-176">![Single Sign-Ons](./media/active-directory-saas-sprinklr-tutorial/ic782909.png "Single Sign-Ons")</span></span>

11. <span data-ttu-id="2234b-177">Op de **voor eenmalige aanmelding** pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="2234b-177">On the **Single Sign on** page, perform the following steps:</span></span>
   
    <span data-ttu-id="2234b-178">![Eenmalige aanmeldingen](./media/active-directory-saas-sprinklr-tutorial/ic782910.png "eenmalige aanmeldingen")</span><span class="sxs-lookup"><span data-stu-id="2234b-178">![Single Sign-Ons](./media/active-directory-saas-sprinklr-tutorial/ic782910.png "Single Sign-Ons")</span></span>

    <span data-ttu-id="2234b-179">a.</span><span class="sxs-lookup"><span data-stu-id="2234b-179">a.</span></span> <span data-ttu-id="2234b-180">In de **naam** textbox, typ een naam voor uw configuratie (bijvoorbeeld: *WAADSSOTest*).</span><span class="sxs-lookup"><span data-stu-id="2234b-180">In the **Name** textbox, type a name for your configuration (for example: *WAADSSOTest*).</span></span>

    <span data-ttu-id="2234b-181">b.</span><span class="sxs-lookup"><span data-stu-id="2234b-181">b.</span></span> <span data-ttu-id="2234b-182">Selecteer **ingeschakeld**.</span><span class="sxs-lookup"><span data-stu-id="2234b-182">Select **Enabled**.</span></span>

    <span data-ttu-id="2234b-183">c.</span><span class="sxs-lookup"><span data-stu-id="2234b-183">c.</span></span> <span data-ttu-id="2234b-184">Selecteer **nieuw certificaat voor eenmalige aanmelding gebruiken**.</span><span class="sxs-lookup"><span data-stu-id="2234b-184">Select **Use new SSO Certificate**.</span></span>
             
    <span data-ttu-id="2234b-185">e.</span><span class="sxs-lookup"><span data-stu-id="2234b-185">e.</span></span> <span data-ttu-id="2234b-186">Open uw base-64 gecodeerde certificaat in Kladblok, Kopieer de inhoud ervan naar het Klembord en plakt u deze naar de **Provider identiteitscertificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="2234b-186">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Identity Provider Certificate** textbox.</span></span>

    <span data-ttu-id="2234b-187">f.</span><span class="sxs-lookup"><span data-stu-id="2234b-187">f.</span></span> <span data-ttu-id="2234b-188">Plak de **SAML entiteit-ID** waarde die u hebt gekopieerd vanuit Azure Portal naar de **entiteit-Id** textbox.</span><span class="sxs-lookup"><span data-stu-id="2234b-188">Paste the **SAML Entity ID** value which you have copied from Azure Portal into the **Entity Id** textbox.</span></span>

    <span data-ttu-id="2234b-189">g.</span><span class="sxs-lookup"><span data-stu-id="2234b-189">g.</span></span> <span data-ttu-id="2234b-190">Plak de **SAML Single Sign-On Service-URL** waarde die u hebt gekopieerd vanuit Azure Portal naar de **identiteit Provider aanmeldings-URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="2234b-190">Paste the **SAML Single Sign-On Service URL** value which you have copied from Azure Portal into the **Identity Provider Login URL** textbox.</span></span>

    <span data-ttu-id="2234b-191">h.</span><span class="sxs-lookup"><span data-stu-id="2234b-191">h.</span></span> <span data-ttu-id="2234b-192">Plak de **Sign-Out URL** waarde die u hebt gekopieerd vanuit Azure Portal naar de **identiteit Provider afmelding URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="2234b-192">Paste the **Sign-Out URL** value which you have copied from Azure Portal into the **Identity Provider Logout URL** textbox.</span></span>
     
    <span data-ttu-id="2234b-193">ik.</span><span class="sxs-lookup"><span data-stu-id="2234b-193">i.</span></span> <span data-ttu-id="2234b-194">Als **SAML-ID gebruikerstype**, selecteer **Assertion gebruiker bevat ' s sprinklr.com gebruikersnaam**.</span><span class="sxs-lookup"><span data-stu-id="2234b-194">As **SAML User ID Type**, select **Assertion contains User”s sprinklr.com username**.</span></span>

    <span data-ttu-id="2234b-195">j.</span><span class="sxs-lookup"><span data-stu-id="2234b-195">j.</span></span> <span data-ttu-id="2234b-196">Als **SAML-ID gebruikerslocatie**, selecteer **gebruikers-ID is in het element met naam-id van het onderwerp overzicht**.</span><span class="sxs-lookup"><span data-stu-id="2234b-196">As **SAML User ID Location**, select **User ID is in the Name Identifier element of the Subject statement**.</span></span>

    <span data-ttu-id="2234b-197">k.</span><span class="sxs-lookup"><span data-stu-id="2234b-197">k.</span></span> <span data-ttu-id="2234b-198">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="2234b-198">Click **Save**.</span></span>
       
    <span data-ttu-id="2234b-199">![SAML](./media/active-directory-saas-sprinklr-tutorial/ic782911.png "SAML")</span><span class="sxs-lookup"><span data-stu-id="2234b-199">![SAML](./media/active-directory-saas-sprinklr-tutorial/ic782911.png "SAML")</span></span>

> [!TIP]
> <span data-ttu-id="2234b-200">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="2234b-200">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="2234b-201">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="2234b-201">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="2234b-202">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2234b-202">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2234b-203">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="2234b-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="2234b-204">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="2234b-204">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="2234b-206">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="2234b-206">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2234b-207">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="2234b-207">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2234b-209">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="2234b-209">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2234b-211">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2234b-211">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2234b-213">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="2234b-213">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2234b-215">a.</span><span class="sxs-lookup"><span data-stu-id="2234b-215">a.</span></span> <span data-ttu-id="2234b-216">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2234b-216">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2234b-217">b.</span><span class="sxs-lookup"><span data-stu-id="2234b-217">b.</span></span> <span data-ttu-id="2234b-218">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2234b-218">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2234b-219">c.</span><span class="sxs-lookup"><span data-stu-id="2234b-219">c.</span></span> <span data-ttu-id="2234b-220">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="2234b-220">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="2234b-221">d.</span><span class="sxs-lookup"><span data-stu-id="2234b-221">d.</span></span> <span data-ttu-id="2234b-222">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="2234b-222">Click **Create**.</span></span>
 
### <a name="creating-a-sprinklr-test-user"></a><span data-ttu-id="2234b-223">Een testgebruiker Sprinklr maken</span><span class="sxs-lookup"><span data-stu-id="2234b-223">Creating a Sprinklr test user</span></span>

1. <span data-ttu-id="2234b-224">Meld u aan bij uw bedrijf Sprinklr site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="2234b-224">Log in to your Sprinklr company site as an administrator.</span></span>

2. <span data-ttu-id="2234b-225">Ga naar **beheer \> instellingen**.</span><span class="sxs-lookup"><span data-stu-id="2234b-225">Go to **Administration \> Settings**.</span></span>
   
    <span data-ttu-id="2234b-226">![Beheer](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "beheer")</span><span class="sxs-lookup"><span data-stu-id="2234b-226">![Administration](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Administration")</span></span>

3. <span data-ttu-id="2234b-227">Ga naar **Client beheren \> gebruikers** in het linkerdeelvenster.</span><span class="sxs-lookup"><span data-stu-id="2234b-227">Go to **Manage Client \> Users** from the left pane.</span></span>
   
    <span data-ttu-id="2234b-228">![Instellingen](./media/active-directory-saas-sprinklr-tutorial/ic782914.png "instellingen")</span><span class="sxs-lookup"><span data-stu-id="2234b-228">![Settings](./media/active-directory-saas-sprinklr-tutorial/ic782914.png "Settings")</span></span>

4. <span data-ttu-id="2234b-229">Klik op **gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="2234b-229">Click **Add User**.</span></span>
   
    <span data-ttu-id="2234b-230">![Instellingen](./media/active-directory-saas-sprinklr-tutorial/ic782915.png "instellingen")</span><span class="sxs-lookup"><span data-stu-id="2234b-230">![Settings](./media/active-directory-saas-sprinklr-tutorial/ic782915.png "Settings")</span></span>

5. <span data-ttu-id="2234b-231">Op de **bewerken gebruiker** dialoogvenster de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="2234b-231">On the **Edit user** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="2234b-232">![Gebruiker bewerken](./media/active-directory-saas-sprinklr-tutorial/ic782916.png "gebruiker bewerken")</span><span class="sxs-lookup"><span data-stu-id="2234b-232">![Edit user](./media/active-directory-saas-sprinklr-tutorial/ic782916.png "Edit user")</span></span> 

    <span data-ttu-id="2234b-233">a.</span><span class="sxs-lookup"><span data-stu-id="2234b-233">a.</span></span> <span data-ttu-id="2234b-234">In de **e**, **voornaam** en **achternaam** tekstvakken, typt u de gegevens van een Azure AD-gebruikersaccount dat u inrichten wilt.</span><span class="sxs-lookup"><span data-stu-id="2234b-234">In the **Email**, **First Name** and **Last Name** textboxes, type the information of an Azure AD user account you want to provision.</span></span>

    <span data-ttu-id="2234b-235">b.</span><span class="sxs-lookup"><span data-stu-id="2234b-235">b.</span></span> <span data-ttu-id="2234b-236">Selecteer **wachtwoord uitgeschakeld**.</span><span class="sxs-lookup"><span data-stu-id="2234b-236">Select **Password Disabled**.</span></span>

    <span data-ttu-id="2234b-237">c.</span><span class="sxs-lookup"><span data-stu-id="2234b-237">c.</span></span> <span data-ttu-id="2234b-238">Selecteer **taal**.</span><span class="sxs-lookup"><span data-stu-id="2234b-238">Select **Language**.</span></span>

    <span data-ttu-id="2234b-239">d.</span><span class="sxs-lookup"><span data-stu-id="2234b-239">d.</span></span> <span data-ttu-id="2234b-240">Selecteer **gebruikerstype**.</span><span class="sxs-lookup"><span data-stu-id="2234b-240">Select **User Type**.</span></span>

    <span data-ttu-id="2234b-241">e.</span><span class="sxs-lookup"><span data-stu-id="2234b-241">e.</span></span> <span data-ttu-id="2234b-242">Klik op **Update**.</span><span class="sxs-lookup"><span data-stu-id="2234b-242">Click **Update**.</span></span>
   
     >[!IMPORTANT]
     ><span data-ttu-id="2234b-243">**Wachtwoord uitgeschakeld** zodat een gebruiker zich aanmelden via een id-provider moet worden geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="2234b-243">**Password Disabled** must be selected to enable a user to log in via an Identity provider.</span></span> 
     
6. <span data-ttu-id="2234b-244">Ga naar **rol**, en voer de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="2234b-244">Go to **Role**, and then perform the following steps:</span></span>
   
    <span data-ttu-id="2234b-245">![Rollen partner](./media/active-directory-saas-sprinklr-tutorial/ic782917.png "Partner rollen")</span><span class="sxs-lookup"><span data-stu-id="2234b-245">![Partner Roles](./media/active-directory-saas-sprinklr-tutorial/ic782917.png "Partner Roles")</span></span>

    <span data-ttu-id="2234b-246">a.</span><span class="sxs-lookup"><span data-stu-id="2234b-246">a.</span></span> <span data-ttu-id="2234b-247">Van de **Global** selecteert **alle\_machtigingen**.</span><span class="sxs-lookup"><span data-stu-id="2234b-247">From the **Global** list, select **ALL\_Permissions**.</span></span>  

    <span data-ttu-id="2234b-248">b.</span><span class="sxs-lookup"><span data-stu-id="2234b-248">b.</span></span> <span data-ttu-id="2234b-249">Klik op **Update**.</span><span class="sxs-lookup"><span data-stu-id="2234b-249">Click **Update**.</span></span>

>[!NOTE]
><span data-ttu-id="2234b-250">U kunt andere Sprinklr gebruiker account hulpmiddelen voor het maken of API's die is geleverd door Sprinklr voor het inrichten van Azure AD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="2234b-250">You can use any other Sprinklr user account creation tools or APIs provided by Sprinklr to provision Azure AD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="2234b-251">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="2234b-251">Assigning the Azure AD test user</span></span>

<span data-ttu-id="2234b-252">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Sprinklr.</span><span class="sxs-lookup"><span data-stu-id="2234b-252">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Sprinklr.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="2234b-254">**Britta Simon om aan te wijzen Sprinklr, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="2234b-254">**To assign Britta Simon to Sprinklr, perform the following steps:**</span></span>

1. <span data-ttu-id="2234b-255">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="2234b-255">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="2234b-257">Selecteer in de lijst met toepassingen **Sprinklr**.</span><span class="sxs-lookup"><span data-stu-id="2234b-257">In the applications list, select **Sprinklr**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_app.png) 

3. <span data-ttu-id="2234b-259">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="2234b-259">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="2234b-261">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="2234b-261">Click **Add** button.</span></span> <span data-ttu-id="2234b-262">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2234b-262">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="2234b-264">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="2234b-264">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="2234b-265">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2234b-265">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2234b-266">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2234b-266">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2234b-267">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="2234b-267">Testing single sign-on</span></span>

<span data-ttu-id="2234b-268">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="2234b-268">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="2234b-269">Als u op de tegel Sprinklr in het deelvenster toegang, krijgt u automatisch aangemeld bij uw toepassing Sprinklr Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2234b-269">When you click the Sprinklr tile in the Access Panel, you should get automatically signed-on to your Sprinklr application For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="2234b-270">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="2234b-270">Additional resources</span></span>

* [<span data-ttu-id="2234b-271">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2234b-271">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2234b-272">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2234b-272">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_203.png

