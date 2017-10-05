---
title: 'Zelfstudie: Azure Active Directory-integratie met Salesforce | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Salesforce.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2d7d420-dc91-41b8-a6b3-59579e043b35
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 639e40ca7e406a1726033e9f5c5363c289087589
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce"></a><span data-ttu-id="08cfe-103">Zelfstudie: Azure Active Directory-integratie met Salesforce</span><span class="sxs-lookup"><span data-stu-id="08cfe-103">Tutorial: Azure Active Directory integration with Salesforce</span></span>

<span data-ttu-id="08cfe-104">In deze zelfstudie leert u hoe Salesforce integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="08cfe-104">In this tutorial, you learn how to integrate Salesforce with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="08cfe-105">Salesforce integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="08cfe-105">Integrating Salesforce with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="08cfe-106">U kunt beheren in Azure AD die toegang tot de Salesforce heeft</span><span class="sxs-lookup"><span data-stu-id="08cfe-106">You can control in Azure AD who has access to Salesforce</span></span>
- <span data-ttu-id="08cfe-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Salesforce (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="08cfe-107">You can enable your users to automatically get signed-on to Salesforce (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="08cfe-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="08cfe-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="08cfe-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="08cfe-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="08cfe-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="08cfe-110">Prerequisites</span></span>

<span data-ttu-id="08cfe-111">Voor het configureren van Azure AD-integratie met Salesforce, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="08cfe-111">To configure Azure AD integration with Salesforce, you need the following items:</span></span>

- <span data-ttu-id="08cfe-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="08cfe-112">An Azure AD subscription</span></span>
- <span data-ttu-id="08cfe-113">Een Salesforce eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="08cfe-113">A Salesforce single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="08cfe-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="08cfe-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="08cfe-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="08cfe-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="08cfe-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="08cfe-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="08cfe-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="08cfe-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="08cfe-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="08cfe-118">Scenario description</span></span>
<span data-ttu-id="08cfe-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="08cfe-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="08cfe-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="08cfe-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="08cfe-121">Salesforce uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="08cfe-121">Adding Salesforce from the gallery</span></span>
2. <span data-ttu-id="08cfe-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="08cfe-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-salesforce-from-the-gallery"></a><span data-ttu-id="08cfe-123">Salesforce uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="08cfe-123">Adding Salesforce from the gallery</span></span>
<span data-ttu-id="08cfe-124">Voor het configureren van de integratie van Salesforce in Azure AD, moet u Salesforce uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="08cfe-124">To configure the integration of Salesforce into Azure AD, you need to add Salesforce from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="08cfe-125">**Als u wilt toevoegen Salesforce uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="08cfe-125">**To add Salesforce from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="08cfe-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="08cfe-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="08cfe-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="08cfe-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="08cfe-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="08cfe-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="08cfe-131">Klik op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="08cfe-131">Click **New application** button on the top of the dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="08cfe-133">Typ in het zoekvak **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="08cfe-133">In the search box, type **Salesforce**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_search.png)

5. <span data-ttu-id="08cfe-135">Selecteer in het deelvenster resultaten **Salesforce**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="08cfe-135">In the results panel, select **Salesforce**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="08cfe-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="08cfe-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="08cfe-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Salesforce op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="08cfe-138">In this section, you configure and test Azure AD single sign-on with Salesforce based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="08cfe-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Salesforce is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="08cfe-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Salesforce is to a user in Azure AD.</span></span> <span data-ttu-id="08cfe-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Salesforce tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="08cfe-140">In other words, a link relationship between an Azure AD user and the related user in Salesforce needs to be established.</span></span>

<span data-ttu-id="08cfe-141">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in Salesforce.</span><span class="sxs-lookup"><span data-stu-id="08cfe-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Salesforce.</span></span>

<span data-ttu-id="08cfe-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Salesforce, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="08cfe-142">To configure and test Azure AD single sign-on with Salesforce, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="08cfe-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="08cfe-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="08cfe-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="08cfe-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="08cfe-145">**[Maken van een testgebruiker Salesforce](#creating-a-salesforce-test-user)**  - Salesforce die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="08cfe-145">**[Creating a Salesforce test user](#creating-a-salesforce-test-user)** - to have a counterpart of Britta Simon in Salesforce that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="08cfe-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="08cfe-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="08cfe-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="08cfe-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="08cfe-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="08cfe-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="08cfe-149">In deze sectie maakt u Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw Salesforce-toepassing.</span><span class="sxs-lookup"><span data-stu-id="08cfe-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Salesforce application.</span></span>

<span data-ttu-id="08cfe-150">**Voor het configureren van Azure AD eenmalige aanmelding met Salesforce, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="08cfe-150">**To configure Azure AD single sign-on with Salesforce, perform the following steps:**</span></span>

1. <span data-ttu-id="08cfe-151">In de Azure-portal op de **Salesforce** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="08cfe-151">In the Azure portal, on the **Salesforce** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="08cfe-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="08cfe-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_samlbase.png)

3. <span data-ttu-id="08cfe-155">Op de **Salesforce-domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="08cfe-155">On the **Salesforce Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_url.png)

    <span data-ttu-id="08cfe-157">In de **aanmeldings-URL** textbox, typ de waarde met het volgende patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="08cfe-157">In the **Sign-on URL** textbox, type the value using the following pattern:</span></span> 
   * <span data-ttu-id="08cfe-158">Account voor de onderneming:`https://<subdomain>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="08cfe-158">Enterprise account: `https://<subdomain>.my.salesforce.com`</span></span>
   * <span data-ttu-id="08cfe-159">Developer-account:`https://<subdomain>-dev-ed.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="08cfe-159">Developer account: `https://<subdomain>-dev-ed.my.salesforce.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="08cfe-160">Deze waarden zijn niet de werkelijke.</span><span class="sxs-lookup"><span data-stu-id="08cfe-160">These values are not the real.</span></span> <span data-ttu-id="08cfe-161">Deze waarden bijwerken met de werkelijke URL voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="08cfe-161">Update these values with the actual Sign-on URL.</span></span> <span data-ttu-id="08cfe-162">Neem contact op met [Salesforce Client ondersteuningsteam](https://help.salesforce.com/support) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="08cfe-162">Contact [Salesforce Client support team](https://help.salesforce.com/support) to get these values.</span></span> 
 
4. <span data-ttu-id="08cfe-163">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="08cfe-163">On the **SAML Signing Certificate** section, click **Certificate** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_certificate.png) 

5. <span data-ttu-id="08cfe-165">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="08cfe-165">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforce-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="08cfe-167">Op de **Salesforce configuratie** sectie, klikt u op **configureren Salesforce** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="08cfe-167">On the **Salesforce Configuration** section, click **Configure Salesforce** to open **Configure sign-on** window.</span></span> <span data-ttu-id="08cfe-168">Kopieer de **SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="08cfe-168">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span> 

    <span data-ttu-id="08cfe-169">![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="08cfe-169">![Configure Single Sign-On](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_configure.png) 
<CS></span></span>
7.  <span data-ttu-id="08cfe-170">Open een nieuw tabblad in de browser en meld u aan op uw Salesforce-beheerdersaccount.</span><span class="sxs-lookup"><span data-stu-id="08cfe-170">Open a new tab in your browser and log in to your Salesforce administrator account.</span></span>

8.  <span data-ttu-id="08cfe-171">Onder de **beheerder** navigatiedeelvenster, klikt u op **beveiligingsmechanismen** uitbreiden van de bijbehorende sectie.</span><span class="sxs-lookup"><span data-stu-id="08cfe-171">Under the **Administrator** navigation pane, click **Security Controls** to expand the related section.</span></span> <span data-ttu-id="08cfe-172">Klik vervolgens op **instellingen voor eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="08cfe-172">Then click **Single Sign-On Settings**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso.png)

9.  <span data-ttu-id="08cfe-174">Op de **instellingen voor eenmalige aanmelding** pagina, klikt u op de **bewerken** knop.</span><span class="sxs-lookup"><span data-stu-id="08cfe-174">On the **Single Sign-On Settings** page, click the **Edit** button.</span></span>
    <span data-ttu-id="08cfe-175">![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-edit.png)</span><span class="sxs-lookup"><span data-stu-id="08cfe-175">![Configure Single Sign-On](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-edit.png)</span></span>

      > [!NOTE]
      > <span data-ttu-id="08cfe-176">Als u nog geen Single Sign-On-instellingen voor uw Salesforce-account inschakelen, moet u mogelijk contact opnemen met [Salesforce Client ondersteuningsteam](https://help.salesforce.com/support).</span><span class="sxs-lookup"><span data-stu-id="08cfe-176">If you are unable to enable Single Sign-On settings for your Salesforce account, you may need to contact [Salesforce Client support team](https://help.salesforce.com/support).</span></span> 

10. <span data-ttu-id="08cfe-177">Selecteer **SAML ingeschakeld**, en klik vervolgens op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="08cfe-177">Select **SAML Enabled**, and then click **Save**.</span></span>

      ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforce-tutorial/sf-enable-saml.png)
11. <span data-ttu-id="08cfe-179">Uw SAML eenmalige aanmelding om instellingen te configureren, klikt u op **nieuw**.</span><span class="sxs-lookup"><span data-stu-id="08cfe-179">To configure your SAML single sign-on settings, click **New**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-new.png)

12. <span data-ttu-id="08cfe-181">Op de **SAML Single Sign-On instelling bewerken** maken de volgende configuraties:</span><span class="sxs-lookup"><span data-stu-id="08cfe-181">On the **SAML Single Sign-On Setting Edit** page, make the following configurations:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforce-tutorial/sf-saml-config.png)

    <span data-ttu-id="08cfe-183">a.</span><span class="sxs-lookup"><span data-stu-id="08cfe-183">a.</span></span> <span data-ttu-id="08cfe-184">Voor de **naam** veld, typ een beschrijvende naam voor deze configuratie.</span><span class="sxs-lookup"><span data-stu-id="08cfe-184">For the **Name** field, type in a friendly name for this configuration.</span></span> <span data-ttu-id="08cfe-185">Om een waarde voor **naam** automatisch invullen de **API-naam** textbox.</span><span class="sxs-lookup"><span data-stu-id="08cfe-185">Providing a value for **Name** automatically populate the **API Name** textbox.</span></span>

    <span data-ttu-id="08cfe-186">b.</span><span class="sxs-lookup"><span data-stu-id="08cfe-186">b.</span></span> <span data-ttu-id="08cfe-187">Plakken **SMAL entiteit-ID** waarde in de **verlener** veld in Salesforce.</span><span class="sxs-lookup"><span data-stu-id="08cfe-187">Paste **SMAL Entity ID** value into the **Issuer** field in Salesforce.</span></span>

    <span data-ttu-id="08cfe-188">c.</span><span class="sxs-lookup"><span data-stu-id="08cfe-188">c.</span></span> <span data-ttu-id="08cfe-189">In de **tekstvak voor de entiteit-Id**, typ de naam van uw Salesforce-domein met het volgende patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="08cfe-189">In the **Entity Id textbox**, type your Salesforce domain name using the following pattern:</span></span>
      
      * <span data-ttu-id="08cfe-190">Account voor de onderneming:`https://<subdomain>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="08cfe-190">Enterprise account: `https://<subdomain>.my.salesforce.com`</span></span>
      * <span data-ttu-id="08cfe-191">Developer-account:`https://<subdomain>-dev-ed.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="08cfe-191">Developer account: `https://<subdomain>-dev-ed.my.salesforce.com`</span></span>
      
    <span data-ttu-id="08cfe-192">d.</span><span class="sxs-lookup"><span data-stu-id="08cfe-192">d.</span></span> <span data-ttu-id="08cfe-193">Klik op **Bladeren** of **bestand kiezen** openen de **te uploaden bestand kiezen** dialoogvenster uw Salesforce-certificaat selecteren en klik vervolgens op **openen** om het certificaat te uploaden.</span><span class="sxs-lookup"><span data-stu-id="08cfe-193">Click **Browse** or **Choose File** to open the **Choose File to Upload** dialog, select your Salesforce certificate, and then click **Open** to upload the certificate.</span></span>

    <span data-ttu-id="08cfe-194">e.</span><span class="sxs-lookup"><span data-stu-id="08cfe-194">e.</span></span> <span data-ttu-id="08cfe-195">Voor **SAML identiteitstype**, selecteer **verklaring van de gebruiker salesforce.com gebruikersnaam bevat**.</span><span class="sxs-lookup"><span data-stu-id="08cfe-195">For **SAML Identity Type**, select **Assertion contains User's salesforce.com username**.</span></span>

    <span data-ttu-id="08cfe-196">f.</span><span class="sxs-lookup"><span data-stu-id="08cfe-196">f.</span></span> <span data-ttu-id="08cfe-197">Voor **SAML identiteit locatie**, selecteer **identiteit is in het element NameIdentifier van het onderwerp overzicht**</span><span class="sxs-lookup"><span data-stu-id="08cfe-197">For **SAML Identity Location**, select **Identity is in the NameIdentifier element of the Subject statement**</span></span>

    <span data-ttu-id="08cfe-198">g.</span><span class="sxs-lookup"><span data-stu-id="08cfe-198">g.</span></span> <span data-ttu-id="08cfe-199">Plakken **Single Sign-On Service-URL** in de **identiteit Provider aanmeldings-URL** veld in Salesforce.</span><span class="sxs-lookup"><span data-stu-id="08cfe-199">Paste **Single Sign-On Service URL** into the **Identity Provider Login URL** field in Salesforce.</span></span>
    
    <span data-ttu-id="08cfe-200">h.</span><span class="sxs-lookup"><span data-stu-id="08cfe-200">h.</span></span> <span data-ttu-id="08cfe-201">Voor **Provider geïnitieerd aanvragen servicebinding**, selecteer **HTTP-omleiding**.</span><span class="sxs-lookup"><span data-stu-id="08cfe-201">For **Service Provider Initiated Request Binding**, select **HTTP Redirect**.</span></span>
    
    <span data-ttu-id="08cfe-202">ik.</span><span class="sxs-lookup"><span data-stu-id="08cfe-202">i.</span></span> <span data-ttu-id="08cfe-203">Tot slot op **opslaan** instellingen toe te passen uw SAML eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="08cfe-203">Finally, click **Save** to apply your SAML single sign-on settings.</span></span>

13. <span data-ttu-id="08cfe-204">Klik op het linkernavigatiedeelvenster in Salesforce **domeinbeheer** Vouw de bijbehorende sectie en klik vervolgens op **mijn domein**.</span><span class="sxs-lookup"><span data-stu-id="08cfe-204">On the left navigation pane in Salesforce, click **Domain Management** to expand the related section, and then click **My Domain**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforce-tutorial/sf-my-domain.png)

14. <span data-ttu-id="08cfe-206">Schuif omlaag naar de **verificatieconfiguratie** uit en klik op de **bewerken** knop.</span><span class="sxs-lookup"><span data-stu-id="08cfe-206">Scroll down to the **Authentication Configuration** section, and click the **Edit** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforce-tutorial/sf-edit-auth-config.png)

15. <span data-ttu-id="08cfe-208">In de **verificatieservice** sectie, selecteert u de beschrijvende naam van uw configuratie SAML SSO en klik vervolgens op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="08cfe-208">In the **Authentication Service** section, select the friendly name of your SAML SSO configuration, and then click **Save**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforce-tutorial/sf-auth-config.png)

    > [!NOTE]
    > <span data-ttu-id="08cfe-210">Als meer dan één authentication-service is ingeschakeld, worden gebruikers gevraagd om te selecteren welke verificatieservice die ze aanmelden willen tijdens de initialisatie van eenmalige aanmelding met uw Salesforce-omgeving.</span><span class="sxs-lookup"><span data-stu-id="08cfe-210">If more than one authentication service is selected, users are prompted to select which authentication service they like to sign in with while initiating single sign-on to your Salesforce environment.</span></span> <span data-ttu-id="08cfe-211">Als u niet dat dit wilt gebeurt, dan u moet **laat alle andere verificatieservices uitgeschakeld**.</span><span class="sxs-lookup"><span data-stu-id="08cfe-211">If you don’t want it to happen, then you should **leave all other authentication services unchecked**.</span></span>
<CE>    
> [!TIP]
> <span data-ttu-id="08cfe-212">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="08cfe-212">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="08cfe-213">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="08cfe-213">After adding this app from the **Active Directory > Enterprise Applications** section, simply click **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="08cfe-214">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="08cfe-214">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="08cfe-215">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="08cfe-215">Creating an Azure AD test user</span></span>
<span data-ttu-id="08cfe-216">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="08cfe-216">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="08cfe-218">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="08cfe-218">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="08cfe-219">In het navigatiedeelvenster links in de **Azure-portal**, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="08cfe-219">On the left navigation pane in the **Azure portal**, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-salesforce-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="08cfe-221">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="08cfe-221">To display the list of users, Go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-salesforce-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="08cfe-223">Aan de bovenkant van het dialoogvenster, klikt u op **toevoegen** openen de **gebruiker** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="08cfe-223">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-salesforce-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="08cfe-225">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="08cfe-225">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-salesforce-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="08cfe-227">a.</span><span class="sxs-lookup"><span data-stu-id="08cfe-227">a.</span></span> <span data-ttu-id="08cfe-228">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="08cfe-228">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="08cfe-229">b.</span><span class="sxs-lookup"><span data-stu-id="08cfe-229">b.</span></span> <span data-ttu-id="08cfe-230">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="08cfe-230">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="08cfe-231">c.</span><span class="sxs-lookup"><span data-stu-id="08cfe-231">c.</span></span> <span data-ttu-id="08cfe-232">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="08cfe-232">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="08cfe-233">d.</span><span class="sxs-lookup"><span data-stu-id="08cfe-233">d.</span></span> <span data-ttu-id="08cfe-234">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="08cfe-234">Click **Create**.</span></span>
 
### <a name="creating-a-salesforce-test-user"></a><span data-ttu-id="08cfe-235">Een testgebruiker Salesforce maken</span><span class="sxs-lookup"><span data-stu-id="08cfe-235">Creating a Salesforce test user</span></span>

<span data-ttu-id="08cfe-236">In deze sectie wordt een gebruiker met de naam Britta Simon gemaakt in Salesforce.</span><span class="sxs-lookup"><span data-stu-id="08cfe-236">In this section, a user called Britta Simon is created in Salesforce.</span></span> <span data-ttu-id="08cfe-237">SalesForce ondersteunt just-in-time-inrichting, die standaard is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="08cfe-237">Salesforce supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="08cfe-238">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="08cfe-238">There is no action item for you in this section.</span></span> <span data-ttu-id="08cfe-239">Als een gebruiker in Salesforce nog niet bestaat, wordt een nieuw gemaakt wanneer u probeert te krijgen tot Salesforce.</span><span class="sxs-lookup"><span data-stu-id="08cfe-239">If a user doesn't already exist in Salesforce, a new one is created when you attempt to access Salesforce.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="08cfe-240">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="08cfe-240">Assigning the Azure AD test user</span></span>

<span data-ttu-id="08cfe-241">In deze sectie maakt inschakelen u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Salesforce.</span><span class="sxs-lookup"><span data-stu-id="08cfe-241">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Salesforce.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="08cfe-243">**Britta Simon om aan te wijzen Salesforce, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="08cfe-243">**To assign Britta Simon to Salesforce, perform the following steps:**</span></span>

1. <span data-ttu-id="08cfe-244">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="08cfe-244">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="08cfe-246">Selecteer in de lijst met toepassingen **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="08cfe-246">In the applications list, select **Salesforce**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_app.png) 

3. <span data-ttu-id="08cfe-248">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="08cfe-248">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="08cfe-250">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="08cfe-250">Click **Add** button.</span></span> <span data-ttu-id="08cfe-251">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="08cfe-251">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="08cfe-253">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="08cfe-253">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="08cfe-254">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="08cfe-254">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="08cfe-255">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="08cfe-255">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="08cfe-256">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="08cfe-256">Testing single sign-on</span></span>

<span data-ttu-id="08cfe-257">Als u wilt testen van uw instellingen voor eenmalige aanmelding, opent u het toegangsvenster op [https://myapps.microsoft.com](https://myapps.microsoft.com/), meldt u zich bij de testaccount en klikt u op **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="08cfe-257">To test your single sign-on settings, open the Access Panel at [https://myapps.microsoft.com](https://myapps.microsoft.com/), then sign into the test account, and click **Salesforce**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="08cfe-258">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="08cfe-258">Additional resources</span></span>

* [<span data-ttu-id="08cfe-259">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="08cfe-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="08cfe-260">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="08cfe-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="08cfe-261">Gebruikers inrichten configureren</span><span class="sxs-lookup"><span data-stu-id="08cfe-261">Configure User Provisioning</span></span>](active-directory-saas-salesforce-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_203.png

