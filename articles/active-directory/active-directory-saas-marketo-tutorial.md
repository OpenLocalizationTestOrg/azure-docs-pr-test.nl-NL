---
title: 'Zelfstudie: Azure Active Directory-integratie met Marketo | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Marketo.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b88c45f5-d288-4717-835c-ca965add8735
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: e146fd5a8075bc9c7ba049b25e5f301fc2645ed9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-marketo"></a><span data-ttu-id="f3023-103">Zelfstudie: Azure Active Directory-integratie met Marketo</span><span class="sxs-lookup"><span data-stu-id="f3023-103">Tutorial: Azure Active Directory integration with Marketo</span></span>

<span data-ttu-id="f3023-104">In deze zelfstudie leert u hoe Marketo integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f3023-104">In this tutorial, you learn how to integrate Marketo with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f3023-105">Marketo integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="f3023-105">Integrating Marketo with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f3023-106">U kunt beheren in Azure AD die toegang tot de Marketo heeft</span><span class="sxs-lookup"><span data-stu-id="f3023-106">You can control in Azure AD who has access to Marketo</span></span>
- <span data-ttu-id="f3023-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Marketo (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="f3023-107">You can enable your users to automatically get signed-on to Marketo (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f3023-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="f3023-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f3023-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f3023-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f3023-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f3023-110">Prerequisites</span></span>

<span data-ttu-id="f3023-111">Voor het configureren van Azure AD-integratie met Marketo, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="f3023-111">To configure Azure AD integration with Marketo, you need the following items:</span></span>

- <span data-ttu-id="f3023-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="f3023-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f3023-113">Een Marketo-eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="f3023-113">A Marketo single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f3023-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="f3023-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f3023-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="f3023-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f3023-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="f3023-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f3023-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f3023-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f3023-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="f3023-118">Scenario description</span></span>
<span data-ttu-id="f3023-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="f3023-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f3023-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="f3023-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f3023-121">Marketo uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="f3023-121">Adding Marketo from the gallery</span></span>
2. <span data-ttu-id="f3023-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f3023-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-marketo-from-the-gallery"></a><span data-ttu-id="f3023-123">Marketo uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="f3023-123">Adding Marketo from the gallery</span></span>
<span data-ttu-id="f3023-124">Voor het configureren van de integratie van Marketo in Azure AD, moet u Marketo uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="f3023-124">To configure the integration of Marketo into Azure AD, you need to add Marketo from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f3023-125">**Als u wilt toevoegen Marketo uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="f3023-125">**To add Marketo from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f3023-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="f3023-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f3023-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f3023-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f3023-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f3023-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="f3023-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f3023-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="f3023-133">Typ in het zoekvak **Marketo**.</span><span class="sxs-lookup"><span data-stu-id="f3023-133">In the search box, type **Marketo**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_search.png)

5. <span data-ttu-id="f3023-135">Selecteer in het deelvenster resultaten **Marketo**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="f3023-135">In the results panel, select **Marketo**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f3023-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f3023-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f3023-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Marketo op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="f3023-138">In this section, you configure and test Azure AD single sign-on with Marketo based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f3023-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Marketo is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f3023-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Marketo is to a user in Azure AD.</span></span> <span data-ttu-id="f3023-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante Marketo-gebruiker worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f3023-140">In other words, a link relationship between an Azure AD user and the related user in Marketo needs to be established.</span></span>

<span data-ttu-id="f3023-141">Wijs in Marketo, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="f3023-141">In Marketo, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f3023-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Marketo, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="f3023-142">To configure and test Azure AD single sign-on with Marketo, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f3023-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f3023-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f3023-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f3023-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f3023-145">**[Maken van een testgebruiker Marketo](#creating-a-marketo-test-user)**  - Marketo die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="f3023-145">**[Creating a Marketo test user](#creating-a-marketo-test-user)** - to have a counterpart of Britta Simon in Marketo that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f3023-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="f3023-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f3023-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="f3023-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f3023-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="f3023-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f3023-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw toepassing Marketo.</span><span class="sxs-lookup"><span data-stu-id="f3023-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Marketo application.</span></span>

<span data-ttu-id="f3023-150">**Voor het configureren van Azure AD eenmalige aanmelding met Marketo, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="f3023-150">**To configure Azure AD single sign-on with Marketo, perform the following steps:**</span></span>

1. <span data-ttu-id="f3023-151">In de Azure-portal op de **Marketo** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="f3023-151">In the Azure portal, on the **Marketo** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="f3023-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="f3023-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_samlbase.png)

3. <span data-ttu-id="f3023-155">Op de **Marketo-domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="f3023-155">On the **Marketo Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_url.png)

    <span data-ttu-id="f3023-157">a.</span><span class="sxs-lookup"><span data-stu-id="f3023-157">a.</span></span> <span data-ttu-id="f3023-158">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://saml.marketo.com/sp`</span><span class="sxs-lookup"><span data-stu-id="f3023-158">In the **Identifier** textbox, type a URL using the following pattern: `https://saml.marketo.com/sp`</span></span>

    <span data-ttu-id="f3023-159">b.</span><span class="sxs-lookup"><span data-stu-id="f3023-159">b.</span></span> <span data-ttu-id="f3023-160">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://login.marketo.com/saml/assertion/\<munchkinid\>`</span><span class="sxs-lookup"><span data-stu-id="f3023-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://login.marketo.com/saml/assertion/\<munchkinid\>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f3023-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="f3023-161">These values are not real.</span></span> <span data-ttu-id="f3023-162">Deze waarden bijwerken met de werkelijke id en de antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="f3023-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="f3023-163">Neem contact op met [Marketo-ondersteuningsteam](http://investors.marketo.com/contactus.cfm) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="f3023-163">Contact [Marketo support team](http://investors.marketo.com/contactus.cfm) to get these values.</span></span>
 
4. <span data-ttu-id="f3023-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="f3023-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_certificate.png) 

5. <span data-ttu-id="f3023-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="f3023-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f3023-168">Op de **Marketo configuratie** sectie, klikt u op **configureren Marketo** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="f3023-168">On the **Marketo Configuration** section, click **Configure Marketo** to open **Configure sign-on** window.</span></span> <span data-ttu-id="f3023-169">Kopieer de **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="f3023-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_configure.png) 

7. <span data-ttu-id="f3023-171">Meld u aan met beheerdersreferenties Marketo bij om Munchkin-Id van uw toepassing, en volgende acties uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="f3023-171">To get Munchkin Id of your application, log in to Marketo using admin credentials and perform following actions:</span></span>
   
    <span data-ttu-id="f3023-172">a.</span><span class="sxs-lookup"><span data-stu-id="f3023-172">a.</span></span> <span data-ttu-id="f3023-173">Aanmelden bij Marketo-app met beheerdersreferenties.</span><span class="sxs-lookup"><span data-stu-id="f3023-173">Log in to Marketo app using admin credentials.</span></span>
   
    <span data-ttu-id="f3023-174">b.</span><span class="sxs-lookup"><span data-stu-id="f3023-174">b.</span></span> <span data-ttu-id="f3023-175">Klik op de **Admin** knop op het bovenste navigatiedeelvenster.</span><span class="sxs-lookup"><span data-stu-id="f3023-175">Click the **Admin** button on the top navigation pane.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="f3023-177">c.</span><span class="sxs-lookup"><span data-stu-id="f3023-177">c.</span></span> <span data-ttu-id="f3023-178">Navigeer naar het menu integratie en klik op de **Munchkin koppeling**.</span><span class="sxs-lookup"><span data-stu-id="f3023-178">Navigate to the Integration menu and click the **Munchkin link**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_11.png)
   
    <span data-ttu-id="f3023-180">d.</span><span class="sxs-lookup"><span data-stu-id="f3023-180">d.</span></span> <span data-ttu-id="f3023-181">Kopieer de weergegeven op het scherm Munchkin-Id en volledige uw antwoord-URL in de Azure AD-configuratiewizard.</span><span class="sxs-lookup"><span data-stu-id="f3023-181">Copy the Munchkin Id shown on the screen and complete your Reply URL in the Azure AD configuration wizard.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_12.png) 

8. <span data-ttu-id="f3023-183">Volg de eenmalige aanmelding configureren in de toepassing de onderstaande stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f3023-183">To configure the SSO in the application, follow the below steps:</span></span>
   
    <span data-ttu-id="f3023-184">a.</span><span class="sxs-lookup"><span data-stu-id="f3023-184">a.</span></span> <span data-ttu-id="f3023-185">Aanmelden bij Marketo-app met beheerdersreferenties.</span><span class="sxs-lookup"><span data-stu-id="f3023-185">Log in to Marketo app using admin credentials.</span></span>
   
    <span data-ttu-id="f3023-186">b.</span><span class="sxs-lookup"><span data-stu-id="f3023-186">b.</span></span> <span data-ttu-id="f3023-187">Klik op de **Admin** knop op het bovenste navigatiedeelvenster.</span><span class="sxs-lookup"><span data-stu-id="f3023-187">Click the **Admin** button on the top navigation pane.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="f3023-189">c.</span><span class="sxs-lookup"><span data-stu-id="f3023-189">c.</span></span> <span data-ttu-id="f3023-190">Navigeer naar het menu integratie en klik op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="f3023-190">Navigate to the Integration menu and click **Single Sign On**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_07.png) 
   
    <span data-ttu-id="f3023-192">d.</span><span class="sxs-lookup"><span data-stu-id="f3023-192">d.</span></span> <span data-ttu-id="f3023-193">Als de SAML-instellingen, klikt u op **bewerken** knop.</span><span class="sxs-lookup"><span data-stu-id="f3023-193">To enable the SAML Settings, click **Edit** button.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_08.png) 
   
    <span data-ttu-id="f3023-195">e.</span><span class="sxs-lookup"><span data-stu-id="f3023-195">e.</span></span> <span data-ttu-id="f3023-196">**Ingeschakeld** Single Sign-On-instellingen.</span><span class="sxs-lookup"><span data-stu-id="f3023-196">**Enabled** Single Sign-On settings.</span></span>
   
    <span data-ttu-id="f3023-197">f.</span><span class="sxs-lookup"><span data-stu-id="f3023-197">f.</span></span> <span data-ttu-id="f3023-198">Plak de **SAML entiteit-ID**, in de **uitgever-ID** textbox.</span><span class="sxs-lookup"><span data-stu-id="f3023-198">Paste the **SAML Entity ID**, in the **Issuer ID** textbox.</span></span>
   
    <span data-ttu-id="f3023-199">g.</span><span class="sxs-lookup"><span data-stu-id="f3023-199">g.</span></span> <span data-ttu-id="f3023-200">In de **entiteit-ID** textbox, voert u de URL als `http://saml.marketo.com/sp`.</span><span class="sxs-lookup"><span data-stu-id="f3023-200">In the **Entity ID** textbox, enter the URL as `http://saml.marketo.com/sp`.</span></span>
   
    <span data-ttu-id="f3023-201">h.</span><span class="sxs-lookup"><span data-stu-id="f3023-201">h.</span></span> <span data-ttu-id="f3023-202">Selecteer de locatie van de gebruiker-ID als **naam-ID-element**.</span><span class="sxs-lookup"><span data-stu-id="f3023-202">Select the User ID Location as **Name Identifier element**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_09.png)
   
    > [!NOTE]
    > <span data-ttu-id="f3023-204">Als uw gebruikers-id geen UPN-naam en wijzig de waarde in het tabblad kenmerk is.</span><span class="sxs-lookup"><span data-stu-id="f3023-204">If your User Identifier is not UPN value then change the value in the Attribute tab.</span></span>
   
    <span data-ttu-id="f3023-205">ik.</span><span class="sxs-lookup"><span data-stu-id="f3023-205">i.</span></span> <span data-ttu-id="f3023-206">Upload het certificaat dat u hebt gedownload van Azure AD-configuratiewizard.</span><span class="sxs-lookup"><span data-stu-id="f3023-206">Upload the certificate, which you have downloaded from Azure AD configuration wizard.</span></span> <span data-ttu-id="f3023-207">**Sla** de instellingen.</span><span class="sxs-lookup"><span data-stu-id="f3023-207">**Save** the settings.</span></span>
   
    <span data-ttu-id="f3023-208">j.</span><span class="sxs-lookup"><span data-stu-id="f3023-208">j.</span></span> <span data-ttu-id="f3023-209">Bewerk de instellingen voor pagina's omleiden.</span><span class="sxs-lookup"><span data-stu-id="f3023-209">Edit the Redirect Pages settings.</span></span>
   
    <span data-ttu-id="f3023-210">k.</span><span class="sxs-lookup"><span data-stu-id="f3023-210">k.</span></span> <span data-ttu-id="f3023-211">Plak de **SAML Single Sign-On Service-URL** in de **aanmeldings-URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="f3023-211">Paste the **SAML Single Sign-On Service URL** in the **Login URL** textbox.</span></span>
   
    <span data-ttu-id="f3023-212">l.</span><span class="sxs-lookup"><span data-stu-id="f3023-212">l.</span></span> <span data-ttu-id="f3023-213">Plak de **Sign-Out URL** in de **afmelding URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="f3023-213">Paste the **Sign-Out URL** in the **Logout URL** textbox.</span></span>
   
    <span data-ttu-id="f3023-214">m.</span><span class="sxs-lookup"><span data-stu-id="f3023-214">m.</span></span> <span data-ttu-id="f3023-215">In de **Error URL**, Kopieer uw **Marketo exemplaar-URL** en klik op **opslaan** knop instellingen op te slaan.</span><span class="sxs-lookup"><span data-stu-id="f3023-215">In the **Error URL**, copy your **Marketo instance URL** and click **Save** button to save settings.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_10.png)

9. <span data-ttu-id="f3023-217">Als u wilt inschakelen voor gebruikers met SSO, moet u de volgende acties uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="f3023-217">To enable the SSO for users, complete the following actions:</span></span>
   
    <span data-ttu-id="f3023-218">a.</span><span class="sxs-lookup"><span data-stu-id="f3023-218">a.</span></span> <span data-ttu-id="f3023-219">Aanmelden bij Marketo-app met beheerdersreferenties.</span><span class="sxs-lookup"><span data-stu-id="f3023-219">Log in to Marketo app using admin credentials.</span></span>
   
    <span data-ttu-id="f3023-220">b.</span><span class="sxs-lookup"><span data-stu-id="f3023-220">b.</span></span> <span data-ttu-id="f3023-221">Klik op de **Admin** knop op het bovenste navigatiedeelvenster.</span><span class="sxs-lookup"><span data-stu-id="f3023-221">Click the **Admin** button on the top navigation pane.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="f3023-223">c.</span><span class="sxs-lookup"><span data-stu-id="f3023-223">c.</span></span> <span data-ttu-id="f3023-224">Navigeer naar de **beveiliging** en klik op **aanmeldingsinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="f3023-224">Navigate to the **Security** menu and click **Login Settings**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_13.png)
   
    <span data-ttu-id="f3023-226">d.</span><span class="sxs-lookup"><span data-stu-id="f3023-226">d.</span></span> <span data-ttu-id="f3023-227">Controleer de **vereisen SSO** optie en **opslaan** de instellingen.</span><span class="sxs-lookup"><span data-stu-id="f3023-227">Check the **Require SSO** option and **Save** the settings.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_14.png)

> [!TIP]
> <span data-ttu-id="f3023-229">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="f3023-229">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f3023-230">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="f3023-230">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f3023-231">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f3023-231">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f3023-232">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="f3023-232">Creating an Azure AD test user</span></span>
<span data-ttu-id="f3023-233">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="f3023-233">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="f3023-235">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="f3023-235">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f3023-236">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="f3023-236">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-marketo-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f3023-238">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="f3023-238">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-marketo-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f3023-240">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f3023-240">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-marketo-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f3023-242">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="f3023-242">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-marketo-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f3023-244">a.</span><span class="sxs-lookup"><span data-stu-id="f3023-244">a.</span></span> <span data-ttu-id="f3023-245">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f3023-245">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f3023-246">b.</span><span class="sxs-lookup"><span data-stu-id="f3023-246">b.</span></span> <span data-ttu-id="f3023-247">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f3023-247">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f3023-248">c.</span><span class="sxs-lookup"><span data-stu-id="f3023-248">c.</span></span> <span data-ttu-id="f3023-249">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="f3023-249">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f3023-250">d.</span><span class="sxs-lookup"><span data-stu-id="f3023-250">d.</span></span> <span data-ttu-id="f3023-251">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="f3023-251">Click **Create**.</span></span>
 
### <a name="creating-a-marketo-test-user"></a><span data-ttu-id="f3023-252">Een testgebruiker Marketo maken</span><span class="sxs-lookup"><span data-stu-id="f3023-252">Creating a Marketo test user</span></span>

<span data-ttu-id="f3023-253">In deze sectie maakt maken u een gebruiker Britta Simon aangeroepen in Marketo.</span><span class="sxs-lookup"><span data-stu-id="f3023-253">In this section, you create a user called Britta Simon in Marketo.</span></span> <span data-ttu-id="f3023-254">Volg deze stappen voor het maken van een gebruiker in Marketo-platform.</span><span class="sxs-lookup"><span data-stu-id="f3023-254">follow these steps to create a user in Marketo platform.</span></span>

1. <span data-ttu-id="f3023-255">Aanmelden bij Marketo-app met beheerdersreferenties.</span><span class="sxs-lookup"><span data-stu-id="f3023-255">Log in to Marketo app using admin credentials.</span></span>

2. <span data-ttu-id="f3023-256">Klik op de **Admin** knop op het bovenste navigatiedeelvenster.</span><span class="sxs-lookup"><span data-stu-id="f3023-256">Click the **Admin** button on the top navigation pane.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 

3. <span data-ttu-id="f3023-258">Navigeer naar de **beveiliging** en klik op **gebruikers en rollen**</span><span class="sxs-lookup"><span data-stu-id="f3023-258">Navigate to the **Security** menu and click **Users & Roles**</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_19.png)  

4. <span data-ttu-id="f3023-260">Klik op de **nieuwe gebruikers uitnodigen** koppeling op het tabblad gebruikers</span><span class="sxs-lookup"><span data-stu-id="f3023-260">Click the **Invite New User** link on the Users tab</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_15.png) 

5. <span data-ttu-id="f3023-262">Vul de volgende informatie in de wizard nieuwe gebruikers uitnodigen</span><span class="sxs-lookup"><span data-stu-id="f3023-262">In the Invite New User wizard fill the following information</span></span>
   
    <span data-ttu-id="f3023-263">a.</span><span class="sxs-lookup"><span data-stu-id="f3023-263">a.</span></span> <span data-ttu-id="f3023-264">Voer de gebruiker **e** adres in het tekstvak</span><span class="sxs-lookup"><span data-stu-id="f3023-264">Enter the user **Email** address in the textbox</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_16.png)
   
    <span data-ttu-id="f3023-266">b.</span><span class="sxs-lookup"><span data-stu-id="f3023-266">b.</span></span> <span data-ttu-id="f3023-267">Voer de **voornaam** in het tekstvak</span><span class="sxs-lookup"><span data-stu-id="f3023-267">Enter the **First Name** in the textbox</span></span>
   
    <span data-ttu-id="f3023-268">c.</span><span class="sxs-lookup"><span data-stu-id="f3023-268">c.</span></span> <span data-ttu-id="f3023-269">Voer de **achternaam** in het tekstvak</span><span class="sxs-lookup"><span data-stu-id="f3023-269">Enter the **Last Name**  in the textbox</span></span>
   
    <span data-ttu-id="f3023-270">d.</span><span class="sxs-lookup"><span data-stu-id="f3023-270">d.</span></span> <span data-ttu-id="f3023-271">Klik op **Volgende**</span><span class="sxs-lookup"><span data-stu-id="f3023-271">Click **Next**</span></span>

6. <span data-ttu-id="f3023-272">In de **machtigingen** tabblad de **userRoles** en klik op **volgende**</span><span class="sxs-lookup"><span data-stu-id="f3023-272">In the **Permissions** tab, select the **userRoles** and click **Next**</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_17.png)
7. <span data-ttu-id="f3023-274">Klik op de **verzenden** knop de uitnodiging gebruiker te verzenden</span><span class="sxs-lookup"><span data-stu-id="f3023-274">Click the **Send** button to send the user invitation</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_18.png)

8. <span data-ttu-id="f3023-276">Gebruiker e-mailmelding ontvangt en klik op de koppeling en wijzig het wachtwoord om het account te activeren.</span><span class="sxs-lookup"><span data-stu-id="f3023-276">User receives the email notification and has to click the link and change the password to activate the account.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f3023-277">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="f3023-277">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f3023-278">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Marketo.</span><span class="sxs-lookup"><span data-stu-id="f3023-278">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Marketo.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="f3023-280">**Britta Simon om aan te wijzen Marketo, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="f3023-280">**To assign Britta Simon to Marketo, perform the following steps:**</span></span>

1. <span data-ttu-id="f3023-281">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f3023-281">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="f3023-283">Selecteer in de lijst met toepassingen **Marketo**.</span><span class="sxs-lookup"><span data-stu-id="f3023-283">In the applications list, select **Marketo**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_app.png) 

3. <span data-ttu-id="f3023-285">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="f3023-285">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="f3023-287">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="f3023-287">Click **Add** button.</span></span> <span data-ttu-id="f3023-288">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f3023-288">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="f3023-290">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="f3023-290">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f3023-291">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f3023-291">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f3023-292">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f3023-292">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f3023-293">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f3023-293">Testing single sign-on</span></span>

<span data-ttu-id="f3023-294">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="f3023-294">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f3023-295">Als u op de Marketo-tegel in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Marketo.</span><span class="sxs-lookup"><span data-stu-id="f3023-295">When you click the Marketo tile in the Access Panel, you should get automatically signed-on to your Marketo application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f3023-296">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="f3023-296">Additional resources</span></span>

* [<span data-ttu-id="f3023-297">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f3023-297">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f3023-298">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f3023-298">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_203.png

