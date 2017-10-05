---
title: "Zelfstudie: Azure Active Directory-integratie met één Zscaler | Microsoft Docs"
description: "Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en één Zscaler."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f352e00d-68d3-4a77-bb92-717d055da56f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 7d655c482a16c991a819eec84c84556d2f288a75
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-one"></a><span data-ttu-id="d17d3-103">Zelfstudie: Azure Active Directory-integratie met één Zscaler</span><span class="sxs-lookup"><span data-stu-id="d17d3-103">Tutorial: Azure Active Directory integration with Zscaler One</span></span>

<span data-ttu-id="d17d3-104">In deze zelfstudie leert u hoe een Zscaler integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d17d3-104">In this tutorial, you learn how to integrate Zscaler One with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d17d3-105">Een Zscaler integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="d17d3-105">Integrating Zscaler One with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d17d3-106">U kunt beheren in Azure AD die toegang tot één Zscaler heeft</span><span class="sxs-lookup"><span data-stu-id="d17d3-106">You can control in Azure AD who has access to Zscaler One</span></span>
- <span data-ttu-id="d17d3-107">U kunt uw gebruikers automatisch ophalen aangemeld bij een Zscaler (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="d17d3-107">You can enable your users to automatically get signed-on to Zscaler One (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d17d3-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="d17d3-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d17d3-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d17d3-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d17d3-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="d17d3-110">Prerequisites</span></span>

<span data-ttu-id="d17d3-111">Voor het configureren van Azure AD-integratie met één Zscaler, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="d17d3-111">To configure Azure AD integration with Zscaler One, you need the following items:</span></span>

- <span data-ttu-id="d17d3-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="d17d3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d17d3-113">Een Zscaler een eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="d17d3-113">A Zscaler One single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d17d3-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="d17d3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d17d3-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="d17d3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d17d3-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="d17d3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d17d3-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand hier downloaden: [proefversie aanbieding](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d17d3-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d17d3-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="d17d3-118">Scenario description</span></span>
<span data-ttu-id="d17d3-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="d17d3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d17d3-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="d17d3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d17d3-121">Toevoegen van een Zscaler uit de galerie</span><span class="sxs-lookup"><span data-stu-id="d17d3-121">Adding Zscaler One from the gallery</span></span>
2. <span data-ttu-id="d17d3-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="d17d3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zscaler-one-from-the-gallery"></a><span data-ttu-id="d17d3-123">Toevoegen van een Zscaler uit de galerie</span><span class="sxs-lookup"><span data-stu-id="d17d3-123">Adding Zscaler One from the gallery</span></span>
<span data-ttu-id="d17d3-124">Voor het configureren van de integratie van één Zscaler in Azure AD, moet u één Zscaler uit de galerie toevoegt aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="d17d3-124">To configure the integration of Zscaler One into Azure AD, you need to add Zscaler One from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d17d3-125">**Als u wilt toevoegen één Zscaler uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="d17d3-125">**To add Zscaler One from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d17d3-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="d17d3-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d17d3-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="d17d3-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d17d3-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="d17d3-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="d17d3-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d17d3-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="d17d3-133">Typ in het zoekvak **Zscaler één**.</span><span class="sxs-lookup"><span data-stu-id="d17d3-133">In the search box, type **Zscaler One**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zscaler-one-tutorial/tutorial_zscalerone_search.png)

5. <span data-ttu-id="d17d3-135">Selecteer in het deelvenster resultaten **Zscaler één**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="d17d3-135">In the results panel, select **Zscaler One**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zscaler-one-tutorial/tutorial_zscalerone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d17d3-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="d17d3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d17d3-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Zscaler één, op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="d17d3-138">In this section, you configure and test Azure AD single sign-on with Zscaler One based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d17d3-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in één Zscaler is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d17d3-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Zscaler One is to a user in Azure AD.</span></span> <span data-ttu-id="d17d3-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in één Zscaler tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="d17d3-140">In other words, a link relationship between an Azure AD user and the related user in Zscaler One needs to be established.</span></span>

<span data-ttu-id="d17d3-141">In één Zscaler, wijs de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="d17d3-141">In Zscaler One, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d17d3-142">Om te configureren en testen van Azure AD eenmalige aanmelding met een Zscaler, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="d17d3-142">To configure and test Azure AD single sign-on with Zscaler One, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d17d3-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d17d3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d17d3-144">**[Proxy-instellingen configureren](#configuring-proxy-settings)**  : als u wilt de proxy-instellingen in Internet Explorer configureren</span><span class="sxs-lookup"><span data-stu-id="d17d3-144">**[Configuring proxy settings](#configuring-proxy-settings)** - to configure the proxy settings in Internet Explorer</span></span>
3. <span data-ttu-id="d17d3-145">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d17d3-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="d17d3-146">**[Maken van een Zscaler een testgebruiker](#creating-a-zscaler-one-test-user)**  - bevatten een equivalent van Britta Simon Zscaler één die is gekoppeld aan de Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="d17d3-146">**[Creating a Zscaler One test user](#creating-a-zscaler-one-test-user)** - to have a counterpart of Britta Simon in Zscaler One that is linked to the Azure AD representation of user.</span></span>
5. <span data-ttu-id="d17d3-147">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="d17d3-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
6. <span data-ttu-id="d17d3-148">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="d17d3-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d17d3-149">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="d17d3-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d17d3-150">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw Zscaler één toepassing.</span><span class="sxs-lookup"><span data-stu-id="d17d3-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zscaler One application.</span></span>

<span data-ttu-id="d17d3-151">**Voor het configureren van Azure AD eenmalige aanmelding met een Zscaler, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="d17d3-151">**To configure Azure AD single sign-on with Zscaler One, perform the following steps:**</span></span>

1. <span data-ttu-id="d17d3-152">In de Azure-portal op de **Zscaler één** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="d17d3-152">In the Azure portal, on the **Zscaler One** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="d17d3-154">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="d17d3-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zscaler-one-tutorial/tutorial_zscalerone_samlbase.png)

3. <span data-ttu-id="d17d3-156">Op de **Zscaler één domein en URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="d17d3-156">On the **Zscaler One Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zscaler-one-tutorial/tutorial_zscalerone_url.png)

    <span data-ttu-id="d17d3-158">Typ in het tekstvak aanmeldings-URL de URL die wordt gebruikt door uw gebruikers eenmalige aanmelding voor uw Zscaler één toepassing.</span><span class="sxs-lookup"><span data-stu-id="d17d3-158">In the Sign-on URL textbox, type the URL used by your users to sign-on to your Zscaler One application.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d17d3-159">U moet deze waarde bijwerken met de werkelijke URL voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="d17d3-159">You have to update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="d17d3-160">Neem contact op met [Zscaler één Client ondersteuningsteam](https://www.zscaler.com/company/contact) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="d17d3-160">Contact [Zscaler One Client support team](https://www.zscaler.com/company/contact) to get these values.</span></span>

4. <span data-ttu-id="d17d3-161">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="d17d3-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zscaler-one-tutorial/tutorial_zscalerone_certificate.png) 

5. <span data-ttu-id="d17d3-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="d17d3-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d17d3-165">Op de **Zscaler één configuratie** sectie, klikt u op **configureren met één Zscaler** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="d17d3-165">On the **Zscaler One Configuration** section, click **Configure Zscaler One** to open **Configure sign-on** window.</span></span> <span data-ttu-id="d17d3-166">Kopieer de **SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="d17d3-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zscaler-one-tutorial/tutorial_zscalerone_configure.png) 

7. <span data-ttu-id="d17d3-168">In een ander browservenster, meld u aan bij uw site met één Zscaler bedrijf als beheerder.</span><span class="sxs-lookup"><span data-stu-id="d17d3-168">In a different web browser window, log in to your Zscaler One company site as an administrator.</span></span>

8. <span data-ttu-id="d17d3-169">Klik in het menu bovenaan op **beheer**.</span><span class="sxs-lookup"><span data-stu-id="d17d3-169">In the menu on the top, click **Administration**.</span></span>
   
    <span data-ttu-id="d17d3-170">![Beheer](./media/active-directory-saas-zscaler-one-tutorial/ic800206.png "beheer")</span><span class="sxs-lookup"><span data-stu-id="d17d3-170">![Administration](./media/active-directory-saas-zscaler-one-tutorial/ic800206.png "Administration")</span></span>

9. <span data-ttu-id="d17d3-171">Onder **beheerders beheren en rollen**, klikt u op **gebruikers beheren & verificatie**.</span><span class="sxs-lookup"><span data-stu-id="d17d3-171">Under **Manage Administrators & Roles**, click **Manage Users & Authentication**.</span></span>   
            
    <span data-ttu-id="d17d3-172">![Gebruikers & verificatie beheren](./media/active-directory-saas-zscaler-one-tutorial/ic800207.png "gebruikers & verificatie beheren")</span><span class="sxs-lookup"><span data-stu-id="d17d3-172">![Manage Users & Authentication](./media/active-directory-saas-zscaler-one-tutorial/ic800207.png "Manage Users & Authentication")</span></span>

10. <span data-ttu-id="d17d3-173">In de **verificatie-opties kiezen voor uw organisatie** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="d17d3-173">In the **Choose Authentication Options for your Organization** section, perform the following steps:</span></span>   
                
    <span data-ttu-id="d17d3-174">![Verificatie](./media/active-directory-saas-zscaler-one-tutorial/ic800208.png "verificatie")</span><span class="sxs-lookup"><span data-stu-id="d17d3-174">![Authentication](./media/active-directory-saas-zscaler-one-tutorial/ic800208.png "Authentication")</span></span>
   
    <span data-ttu-id="d17d3-175">a.</span><span class="sxs-lookup"><span data-stu-id="d17d3-175">a.</span></span> <span data-ttu-id="d17d3-176">Selecteer **verificatie met eenmalige aanmelding SAML**.</span><span class="sxs-lookup"><span data-stu-id="d17d3-176">Select **Authenticate using SAML Single Sign-On**.</span></span>

    <span data-ttu-id="d17d3-177">b.</span><span class="sxs-lookup"><span data-stu-id="d17d3-177">b.</span></span> <span data-ttu-id="d17d3-178">Klik op **één SAML aanmelding Parameters configureren**.</span><span class="sxs-lookup"><span data-stu-id="d17d3-178">Click **Configure SAML Single Sign-On Parameters**.</span></span>

11. <span data-ttu-id="d17d3-179">Op de **configureren SAML Single Sign-On Parameters** dialoogvenster pagina de volgende stappen uit en klik vervolgens op **gedaan**</span><span class="sxs-lookup"><span data-stu-id="d17d3-179">On the **Configure SAML Single Sign-On Parameters** dialog page, perform the following steps, and then click **Done**</span></span>

    <span data-ttu-id="d17d3-180">![Eenmalige aanmelding](./media/active-directory-saas-zscaler-one-tutorial/ic800209.png "eenmalige aanmelding")</span><span class="sxs-lookup"><span data-stu-id="d17d3-180">![Single Sign-On](./media/active-directory-saas-zscaler-one-tutorial/ic800209.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="d17d3-181">a.</span><span class="sxs-lookup"><span data-stu-id="d17d3-181">a.</span></span> <span data-ttu-id="d17d3-182">Plak de **SAML Single Sign-On Service-URL** waarde, die u hebt gekopieerd vanuit de Azure-portal in de **URL van de SAML-Portal waarmee gebruikers worden verzonden voor verificatie** textbox.</span><span class="sxs-lookup"><span data-stu-id="d17d3-182">Paste the **SAML Single Sign-On Service URL** value, which you have copied from the Azure portal into the **URL of the SAML Portal to which users are sent for authentication** textbox.</span></span>
    
    <span data-ttu-id="d17d3-183">b.</span><span class="sxs-lookup"><span data-stu-id="d17d3-183">b.</span></span> <span data-ttu-id="d17d3-184">In de **kenmerk met naam van de aanmelding** textbox type **NameID**.</span><span class="sxs-lookup"><span data-stu-id="d17d3-184">In the **Attribute containing Login Name** textbox, type **NameID**.</span></span>
    
    <span data-ttu-id="d17d3-185">c.</span><span class="sxs-lookup"><span data-stu-id="d17d3-185">c.</span></span> <span data-ttu-id="d17d3-186">Als u wilt uw gedownloade certificaat uploaden, klikt u op **Zscaler pem**.</span><span class="sxs-lookup"><span data-stu-id="d17d3-186">To upload your downloaded certificate, click **Zscaler pem**.</span></span>
    
    <span data-ttu-id="d17d3-187">d.</span><span class="sxs-lookup"><span data-stu-id="d17d3-187">d.</span></span> <span data-ttu-id="d17d3-188">Selecteer **SAML automatische inrichting inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="d17d3-188">Select **Enable SAML Auto-Provisioning**.</span></span>

12. <span data-ttu-id="d17d3-189">Op de **gebruikersverificatie configureren** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="d17d3-189">On the **Configure User Authentication** dialog page, perform the following steps:</span></span>

    <span data-ttu-id="d17d3-190">![Beheer](./media/active-directory-saas-zscaler-one-tutorial/ic800210.png "beheer")</span><span class="sxs-lookup"><span data-stu-id="d17d3-190">![Administration](./media/active-directory-saas-zscaler-one-tutorial/ic800210.png "Administration")</span></span>
    
    <span data-ttu-id="d17d3-191">a.</span><span class="sxs-lookup"><span data-stu-id="d17d3-191">a.</span></span> <span data-ttu-id="d17d3-192">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="d17d3-192">Click **Save**.</span></span>

    <span data-ttu-id="d17d3-193">b.</span><span class="sxs-lookup"><span data-stu-id="d17d3-193">b.</span></span> <span data-ttu-id="d17d3-194">Klik op **nu activeren**.</span><span class="sxs-lookup"><span data-stu-id="d17d3-194">Click **Activate Now**.</span></span>

## <a name="configuring-proxy-settings"></a><span data-ttu-id="d17d3-195">Proxy-instellingen configureren</span><span class="sxs-lookup"><span data-stu-id="d17d3-195">Configuring proxy settings</span></span>
### <a name="to-configure-the-proxy-settings-in-internet-explorer"></a><span data-ttu-id="d17d3-196">De proxy-instellingen in Internet Explorer configureren</span><span class="sxs-lookup"><span data-stu-id="d17d3-196">To configure the proxy settings in Internet Explorer</span></span>

1. <span data-ttu-id="d17d3-197">Start **Internet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="d17d3-197">Start **Internet Explorer**.</span></span>

2. <span data-ttu-id="d17d3-198">Selecteer **Internetopties** van de **extra** menu voor open de **Internetopties** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d17d3-198">Select **Internet options** from the **Tools** menu for open the **Internet Options** dialog.</span></span>   
    
     <span data-ttu-id="d17d3-199">![Internetopties](./media/active-directory-saas-zscaler-one-tutorial/ic769492.png "Internetopties")</span><span class="sxs-lookup"><span data-stu-id="d17d3-199">![Internet Options](./media/active-directory-saas-zscaler-one-tutorial/ic769492.png "Internet Options")</span></span>

3. <span data-ttu-id="d17d3-200">Klik op de **verbindingen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="d17d3-200">Click the **Connections** tab.</span></span>   
  
     <span data-ttu-id="d17d3-201">![Verbindingen](./media/active-directory-saas-zscaler-one-tutorial/ic769493.png "verbindingen")</span><span class="sxs-lookup"><span data-stu-id="d17d3-201">![Connections](./media/active-directory-saas-zscaler-one-tutorial/ic769493.png "Connections")</span></span>

4. <span data-ttu-id="d17d3-202">Klik op **LAN-instellingen** openen de **LAN-instellingen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d17d3-202">Click **LAN settings** to open the **LAN Settings** dialog.</span></span>

5. <span data-ttu-id="d17d3-203">Voer de volgende stappen uit in de sectie Proxy-server:</span><span class="sxs-lookup"><span data-stu-id="d17d3-203">In the Proxy server section, perform the following steps:</span></span>   
   
    <span data-ttu-id="d17d3-204">![Proxyserver](./media/active-directory-saas-zscaler-one-tutorial/ic769494.png "proxyserver")</span><span class="sxs-lookup"><span data-stu-id="d17d3-204">![Proxy server](./media/active-directory-saas-zscaler-one-tutorial/ic769494.png "Proxy server")</span></span>

    <span data-ttu-id="d17d3-205">a.</span><span class="sxs-lookup"><span data-stu-id="d17d3-205">a.</span></span> <span data-ttu-id="d17d3-206">Selecteer **een proxyserver gebruiken voor uw LAN**.</span><span class="sxs-lookup"><span data-stu-id="d17d3-206">Select **Use a proxy server for your LAN**.</span></span>

    <span data-ttu-id="d17d3-207">b.</span><span class="sxs-lookup"><span data-stu-id="d17d3-207">b.</span></span> <span data-ttu-id="d17d3-208">Typ in het tekstvak adres **gateway.zscalerone.net**.</span><span class="sxs-lookup"><span data-stu-id="d17d3-208">In the Address textbox, type **gateway.zscalerone.net**.</span></span>

    <span data-ttu-id="d17d3-209">c.</span><span class="sxs-lookup"><span data-stu-id="d17d3-209">c.</span></span> <span data-ttu-id="d17d3-210">Typ in het tekstvak poort **80**.</span><span class="sxs-lookup"><span data-stu-id="d17d3-210">In the Port textbox, type **80**.</span></span>

    <span data-ttu-id="d17d3-211">d.</span><span class="sxs-lookup"><span data-stu-id="d17d3-211">d.</span></span> <span data-ttu-id="d17d3-212">Selecteer **proxyserver niet gebruiken voor lokale adressen**.</span><span class="sxs-lookup"><span data-stu-id="d17d3-212">Select **Bypass proxy server for local addresses**.</span></span>

    <span data-ttu-id="d17d3-213">e.</span><span class="sxs-lookup"><span data-stu-id="d17d3-213">e.</span></span> <span data-ttu-id="d17d3-214">Klik op **OK** sluiten de **Local Area Network (LAN)-instellingen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d17d3-214">Click **OK** to close the **Local Area Network (LAN) Settings** dialog.</span></span>

6. <span data-ttu-id="d17d3-215">Klik op **OK** sluiten de **Internetopties** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d17d3-215">Click **OK** to close the **Internet Options** dialog.</span></span>

> [!TIP]
> <span data-ttu-id="d17d3-216">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="d17d3-216">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d17d3-217">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="d17d3-217">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d17d3-218">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d17d3-218">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d17d3-219">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="d17d3-219">Creating an Azure AD test user</span></span>
<span data-ttu-id="d17d3-220">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="d17d3-220">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="d17d3-222">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="d17d3-222">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d17d3-223">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="d17d3-223">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zscaler-one-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d17d3-225">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="d17d3-225">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zscaler-one-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d17d3-227">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d17d3-227">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zscaler-one-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d17d3-229">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="d17d3-229">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zscaler-one-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d17d3-231">a.</span><span class="sxs-lookup"><span data-stu-id="d17d3-231">a.</span></span> <span data-ttu-id="d17d3-232">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d17d3-232">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d17d3-233">b.</span><span class="sxs-lookup"><span data-stu-id="d17d3-233">b.</span></span> <span data-ttu-id="d17d3-234">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d17d3-234">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d17d3-235">c.</span><span class="sxs-lookup"><span data-stu-id="d17d3-235">c.</span></span> <span data-ttu-id="d17d3-236">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="d17d3-236">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d17d3-237">d.</span><span class="sxs-lookup"><span data-stu-id="d17d3-237">d.</span></span> <span data-ttu-id="d17d3-238">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="d17d3-238">Click **Create**.</span></span>
 
### <a name="creating-a-zscaler-one-test-user"></a><span data-ttu-id="d17d3-239">Een Zscaler een testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="d17d3-239">Creating a Zscaler One test user</span></span>

<span data-ttu-id="d17d3-240">Om Azure AD-gebruikers zich aanmelden bij een Zscaler, moeten ze worden ingericht aan één Zscaler.</span><span class="sxs-lookup"><span data-stu-id="d17d3-240">To enable Azure AD users to log in to Zscaler One, they must be provisioned to Zscaler One.</span></span> <span data-ttu-id="d17d3-241">In het geval van een Zscaler is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="d17d3-241">In the case of Zscaler One, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="d17d3-242">Als u wilt configureren voor gebruikers inrichten, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="d17d3-242">To configure user provisioning, perform the following steps:</span></span>

1. <span data-ttu-id="d17d3-243">Meld u aan bij uw **Zscaler één** tenant.</span><span class="sxs-lookup"><span data-stu-id="d17d3-243">Log in to your **Zscaler One** tenant.</span></span>

2. <span data-ttu-id="d17d3-244">Klik op **beheer**.</span><span class="sxs-lookup"><span data-stu-id="d17d3-244">Click **Administration**.</span></span>   
   
    <span data-ttu-id="d17d3-245">![Beheer](./media/active-directory-saas-zscaler-one-tutorial/ic781035.png "beheer")</span><span class="sxs-lookup"><span data-stu-id="d17d3-245">![Administration](./media/active-directory-saas-zscaler-one-tutorial/ic781035.png "Administration")</span></span>

3. <span data-ttu-id="d17d3-246">Klik op **Gebruikersbeheer**.</span><span class="sxs-lookup"><span data-stu-id="d17d3-246">Click **User Management**.</span></span>   
        
     <span data-ttu-id="d17d3-247">![Voeg](./media/active-directory-saas-zscaler-one-tutorial/ic781036.png "toevoegen")</span><span class="sxs-lookup"><span data-stu-id="d17d3-247">![Add](./media/active-directory-saas-zscaler-one-tutorial/ic781036.png "Add")</span></span>

4. <span data-ttu-id="d17d3-248">In de **gebruikers** tabblad **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="d17d3-248">In the **Users** tab, click **Add**.</span></span>
      
    <span data-ttu-id="d17d3-249">![Voeg](./media/active-directory-saas-zscaler-one-tutorial/ic781037.png "toevoegen")</span><span class="sxs-lookup"><span data-stu-id="d17d3-249">![Add](./media/active-directory-saas-zscaler-one-tutorial/ic781037.png "Add")</span></span>

5. <span data-ttu-id="d17d3-250">Voer de volgende stappen uit in de sectie gebruiker toevoegen:</span><span class="sxs-lookup"><span data-stu-id="d17d3-250">In the Add User section, perform the following steps:</span></span>
        
    <span data-ttu-id="d17d3-251">![Gebruiker toevoegen](./media/active-directory-saas-zscaler-one-tutorial/ic781038.png "gebruiker toevoegen")</span><span class="sxs-lookup"><span data-stu-id="d17d3-251">![Add User](./media/active-directory-saas-zscaler-one-tutorial/ic781038.png "Add User")</span></span>
   
    <span data-ttu-id="d17d3-252">a.</span><span class="sxs-lookup"><span data-stu-id="d17d3-252">a.</span></span> <span data-ttu-id="d17d3-253">Typ de **UserID**, **weergavenaam gebruiker**, **wachtwoord**, **wachtwoord bevestigen**, en selecteer vervolgens **groepen** en de **afdeling** van een geldig Azure AD-account die u inrichten wilt.</span><span class="sxs-lookup"><span data-stu-id="d17d3-253">Type the **UserID**, **User Display Name**, **Password**, **Confirm Password**, and then select **Groups** and the **Department** of a valid Azure AD account you want to provision.</span></span>

    <span data-ttu-id="d17d3-254">b.</span><span class="sxs-lookup"><span data-stu-id="d17d3-254">b.</span></span> <span data-ttu-id="d17d3-255">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="d17d3-255">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="d17d3-256">U kunt geen andere Zscaler één hulpmiddelen voor het account maken gebruiker of API's die worden geleverd door een Zscaler voor het inrichten van Azure AD-gebruikersaccounts gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d17d3-256">You can use any other Zscaler One user account creation tools or APIs provided by Zscaler One to provision Azure AD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d17d3-257">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="d17d3-257">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d17d3-258">In deze sectie maakt inschakelen u Britta Simon gebruikt Azure eenmalige aanmelding toegang te verlenen aan één Zscaler.</span><span class="sxs-lookup"><span data-stu-id="d17d3-258">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zscaler One.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="d17d3-260">**Als u wilt toewijzen Britta Simon aan één Zscaler, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="d17d3-260">**To assign Britta Simon to Zscaler One, perform the following steps:**</span></span>

1. <span data-ttu-id="d17d3-261">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="d17d3-261">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="d17d3-263">Selecteer in de lijst met toepassingen **Zscaler één**.</span><span class="sxs-lookup"><span data-stu-id="d17d3-263">In the applications list, select **Zscaler One**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zscaler-one-tutorial/tutorial_zscalerone_app.png) 

3. <span data-ttu-id="d17d3-265">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="d17d3-265">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="d17d3-267">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="d17d3-267">Click **Add** button.</span></span> <span data-ttu-id="d17d3-268">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d17d3-268">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="d17d3-270">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="d17d3-270">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d17d3-271">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d17d3-271">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d17d3-272">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d17d3-272">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d17d3-273">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="d17d3-273">Testing single sign-on</span></span>

<span data-ttu-id="d17d3-274">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="d17d3-274">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d17d3-275">Als u op de Zscaler een tegel in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw Zscaler één toepassing.</span><span class="sxs-lookup"><span data-stu-id="d17d3-275">When you click the Zscaler One tile in the Access Panel, you should get automatically signed-on to your Zscaler One application.</span></span>
<span data-ttu-id="d17d3-276">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d17d3-276">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d17d3-277">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="d17d3-277">Additional resources</span></span>

* [<span data-ttu-id="d17d3-278">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d17d3-278">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d17d3-279">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d17d3-279">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_203.png

