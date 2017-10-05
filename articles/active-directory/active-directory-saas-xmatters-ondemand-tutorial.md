---
title: 'Zelfstudie: Azure Active Directory-integratie met xMatters OnDemand | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en xMatters OnDemand.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ca0633db-4f95-432e-b3db-0168193b5ce9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 9bfcb44ed19f167872b3cd9119e2dbdd35c82604
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-xmatters-ondemand"></a><span data-ttu-id="6cd5e-103">Zelfstudie: Azure Active Directory-integratie met xMatters OnDemand</span><span class="sxs-lookup"><span data-stu-id="6cd5e-103">Tutorial: Azure Active Directory integration with xMatters OnDemand</span></span>

<span data-ttu-id="6cd5e-104">In deze zelfstudie leert u hoe xMatters OnDemand integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6cd5e-104">In this tutorial, you learn how to integrate xMatters OnDemand with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6cd5e-105">XMatters OnDemand integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="6cd5e-105">Integrating xMatters OnDemand with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6cd5e-106">U kunt beheren in Azure AD die toegang tot xMatters OnDemand heeft</span><span class="sxs-lookup"><span data-stu-id="6cd5e-106">You can control in Azure AD who has access to xMatters OnDemand</span></span>
- <span data-ttu-id="6cd5e-107">U kunt uw gebruikers automatisch ophalen aangemeld bij xMatters OnDemand (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="6cd5e-107">You can enable your users to automatically get signed-on to xMatters OnDemand (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6cd5e-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="6cd5e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="6cd5e-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6cd5e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6cd5e-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="6cd5e-110">Prerequisites</span></span>

<span data-ttu-id="6cd5e-111">Voor het configureren van Azure AD-integratie met xMatters OnDemand, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="6cd5e-111">To configure Azure AD integration with xMatters OnDemand, you need the following items:</span></span>

- <span data-ttu-id="6cd5e-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="6cd5e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6cd5e-113">Een xMatters eenmalige aanmelding OnDemand abonnement ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="6cd5e-113">A xMatters OnDemand single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6cd5e-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6cd5e-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="6cd5e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6cd5e-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6cd5e-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6cd5e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6cd5e-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="6cd5e-118">Scenario description</span></span>
<span data-ttu-id="6cd5e-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6cd5e-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="6cd5e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6cd5e-121">XMatters OnDemand uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="6cd5e-121">Adding xMatters OnDemand from the gallery</span></span>
2. <span data-ttu-id="6cd5e-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="6cd5e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-xmatters-ondemand-from-the-gallery"></a><span data-ttu-id="6cd5e-123">XMatters OnDemand uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="6cd5e-123">Adding xMatters OnDemand from the gallery</span></span>
<span data-ttu-id="6cd5e-124">Voor het configureren van de integratie van xMatters OnDemand in Azure AD, moet u xMatters OnDemand uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-124">To configure the integration of xMatters OnDemand into Azure AD, you need to add xMatters OnDemand from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6cd5e-125">**Als u wilt toevoegen xMatters OnDemand uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="6cd5e-125">**To add xMatters OnDemand from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6cd5e-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6cd5e-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6cd5e-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="6cd5e-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="6cd5e-133">Typ in het zoekvak **xMatters OnDemand**.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-133">In the search box, type **xMatters OnDemand**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_search.png)

5. <span data-ttu-id="6cd5e-135">Selecteer in het deelvenster resultaten **xMatters OnDemand**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-135">In the results panel, select **xMatters OnDemand**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6cd5e-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="6cd5e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6cd5e-138">In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met xMatters die OnDemand op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-138">In this section, you configure and test Azure AD single sign-on with xMatters OnDemand based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6cd5e-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de equivalente gebruiker in xMatters OnDemand aan een gebruiker in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in xMatters OnDemand is to a user in Azure AD.</span></span> <span data-ttu-id="6cd5e-140">Met andere woorden, een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in xMatters OnDemand moet tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-140">In other words, a link relationship between an Azure AD user and the related user in xMatters OnDemand needs to be established.</span></span>

<span data-ttu-id="6cd5e-141">Wijs in xMatters OnDemand, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-141">In xMatters OnDemand, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="6cd5e-142">Om te configureren en testen van Azure AD eenmalige aanmelding met xMatters OnDemand, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="6cd5e-142">To configure and test Azure AD single sign-on with xMatters OnDemand, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6cd5e-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6cd5e-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6cd5e-145">**[Maken van een gebruiker xMatters OnDemand test](#creating-a-xmatters-ondemand-test-user)**  - hebben een equivalent van Britta Simon in xMatters OnDemand die is gekoppeld aan de Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-145">**[Creating a xMatters OnDemand test user](#creating-a-xmatters-ondemand-test-user)** - to have a counterpart of Britta Simon in xMatters OnDemand that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="6cd5e-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6cd5e-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6cd5e-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="6cd5e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6cd5e-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw xMatters OnDemand-toepassing.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your xMatters OnDemand application.</span></span>

<span data-ttu-id="6cd5e-150">**Voor het configureren van Azure AD eenmalige aanmelding met xMatters OnDemand, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="6cd5e-150">**To configure Azure AD single sign-on with xMatters OnDemand, perform the following steps:**</span></span>

1. <span data-ttu-id="6cd5e-151">In de Azure-portal op de **xMatters OnDemand** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-151">In the Azure portal, on the **xMatters OnDemand** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="6cd5e-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_samlbase.png)

3. <span data-ttu-id="6cd5e-155">Op de **xMatters OnDemand domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="6cd5e-155">On the **xMatters OnDemand Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_url.png)
    
    <span data-ttu-id="6cd5e-157">a.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-157">a.</span></span> <span data-ttu-id="6cd5e-158">In de **id** textbox, typ een URL met het volgende patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="6cd5e-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>   
    | |
    |--|
    | `https://<companyname>.au1.xmatters.com.au/`|
    | `https://<companyname>.cs1.xmatters.com/`|
    | `https://<companyname>.xmatters.com/`|
    | `https://www.xmatters.com`|
    | `https://<companyname>.xmatters.com.au/`|

    <span data-ttu-id="6cd5e-159">b.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-159">b.</span></span> <span data-ttu-id="6cd5e-160">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="6cd5e-160">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.au1.xmatters.com.au`|
    | `https://<companyname>.xmatters.com/sp/<instancename>`|
    | `https://<companyname>.cs1.xmatters.com/sp/<instancename>`|
    | `https://<companyname>.au1.xmatters.com.au/<instancename>`|

    > [!NOTE] 
    > <span data-ttu-id="6cd5e-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-161">These values are not real.</span></span> <span data-ttu-id="6cd5e-162">Deze waarden bijwerken met de werkelijke id en de antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="6cd5e-163">Neem contact op met [xMatters OnDemand ondersteuningsteam](https://www.xmatters.com/company/contact-us/) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-163">Contact [xMatters OnDemand support team](https://www.xmatters.com/company/contact-us/) to get these values.</span></span>

4. <span data-ttu-id="6cd5e-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het certificaatbestand lokaal als **c:\\XMatters OnDemand.cer**.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file locally as **c:\\XMatters OnDemand.cer**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_certificate.png)
    
    > [!IMPORTANT]
    > <span data-ttu-id="6cd5e-166">U moet voor het doorsturen van het certificaat naar de [ondersteuningsteam voor OnDemand xMatters](https://www.xmatters.com/company/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="6cd5e-166">You need to forward the certificate to the [xMatters OnDemand support team](https://www.xmatters.com/company/contact-us/).</span></span> <span data-ttu-id="6cd5e-167">Het certificaat moet worden geüpload door het ondersteuningsteam xMatters voordat u de configuratie voor eenmalige aanmelding kunt voltooien.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-167">The certificate needs to be uploaded by the xMatters support team before you can finalize the single sign-on configuration.</span></span> 

5. <span data-ttu-id="6cd5e-168">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-168">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6cd5e-170">Op de **xMatters OnDemand configuratie** sectie, klikt u op **xMatters OnDemand configureren** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-170">On the **xMatters OnDemand Configuration** section, click **Configure xMatters OnDemand** to open **Configure sign-on** window.</span></span> <span data-ttu-id="6cd5e-171">Kopieer de **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="6cd5e-171">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_configure.png) 

7. <span data-ttu-id="6cd5e-173">In een ander browservenster, meld u aan bij uw bedrijf XMatters OnDemand site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-173">In a different web browser window, log in to your XMatters OnDemand company site as an administrator.</span></span>

8. <span data-ttu-id="6cd5e-174">Klik in de werkbalk bovenaan op **Admin**, en klik vervolgens op **bedrijfsgegevens** in de navigatiebalk aan de linkerkant.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-174">In the toolbar on the top, click **Admin**, and then click **Company Details** in the navigation bar on the left side.</span></span>
   
    <span data-ttu-id="6cd5e-175">![Beheerder](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776795.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="6cd5e-175">![Admin](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776795.png "Admin")</span></span>

9. <span data-ttu-id="6cd5e-176">Op de **SAML-configuratie** pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="6cd5e-176">On the **SAML Configuration** page, perform the following steps:</span></span>
   
    <span data-ttu-id="6cd5e-177">![De SAML-configuratie](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776796.png "SAML-configuratie")</span><span class="sxs-lookup"><span data-stu-id="6cd5e-177">![SAML configuration](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776796.png "SAML configuration")</span></span>
   
    <span data-ttu-id="6cd5e-178">a.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-178">a.</span></span> <span data-ttu-id="6cd5e-179">Selecteer **SAML inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-179">Select **Enable SAML**.</span></span>
   
    <span data-ttu-id="6cd5e-180">b.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-180">b.</span></span> <span data-ttu-id="6cd5e-181">Plakken **SAML entiteit-ID**, die u hebt gekopieerd vanuit de Azure-portal in de **identiteit Provider-ID** textbox.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-181">Paste **SAML Entity ID**, which you have copied from the Azure portal into the **Identity Provider ID** textbox.</span></span>
   
    <span data-ttu-id="6cd5e-182">c.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-182">c.</span></span> <span data-ttu-id="6cd5e-183">Plakken **SAML Single Sign-On Service-URL**, die u hebt gekopieerd vanuit de Azure-portal in de **eenmalige aanmelding op URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-183">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal into the **Single Sign On URL** textbox.</span></span>
   
    <span data-ttu-id="6cd5e-184">d.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-184">d.</span></span> <span data-ttu-id="6cd5e-185">Plakken **Sign-Out URL**, die u hebt gekopieerd vanuit de Azure-portal in de **-URL met eenmalige afmelding** textbox.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-185">Paste **Sign-Out URL**, which you have copied from the Azure portal into the **Single Logout URL** textbox.</span></span>
   
    <span data-ttu-id="6cd5e-186">e.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-186">e.</span></span> <span data-ttu-id="6cd5e-187">Klik op de pagina Bedrijfsgegevens aan de bovenkant op **wijzigingen opslaan**.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-187">On the Company Details page, at the top, click **Save Changes**.</span></span>
    
    <span data-ttu-id="6cd5e-188">![Details voor de bedrijfsportal](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776797.png "details voor de bedrijfsportal")</span><span class="sxs-lookup"><span data-stu-id="6cd5e-188">![Company details](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776797.png "Company details")</span></span>

> [!TIP]
> <span data-ttu-id="6cd5e-189">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="6cd5e-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6cd5e-190">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6cd5e-191">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6cd5e-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6cd5e-192">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="6cd5e-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="6cd5e-193">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="6cd5e-195">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="6cd5e-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6cd5e-196">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6cd5e-198">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6cd5e-200">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6cd5e-202">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="6cd5e-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6cd5e-204">a.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-204">a.</span></span> <span data-ttu-id="6cd5e-205">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6cd5e-206">b.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-206">b.</span></span> <span data-ttu-id="6cd5e-207">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6cd5e-208">c.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-208">c.</span></span> <span data-ttu-id="6cd5e-209">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6cd5e-210">d.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-210">d.</span></span> <span data-ttu-id="6cd5e-211">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-211">Click **Create**.</span></span>
 
### <a name="creating-a-xmatters-ondemand-test-user"></a><span data-ttu-id="6cd5e-212">Maken van een gebruiker xMatters OnDemand testen</span><span class="sxs-lookup"><span data-stu-id="6cd5e-212">Creating a xMatters OnDemand test user</span></span>

<span data-ttu-id="6cd5e-213">Om Azure AD-gebruikers zich aanmelden bij XMatters OnDemand inschakelt, moeten ze worden ingericht in XMatters OnDemand.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-213">In order to enable Azure AD users to log in to XMatters OnDemand, they must be provisioned into XMatters OnDemand.</span></span> <span data-ttu-id="6cd5e-214">In het geval van XMatters OnDemand is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-214">In the case of XMatters OnDemand, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-accounts-perform-the-following-steps"></a><span data-ttu-id="6cd5e-215">Voor het inrichten van een gebruikersaccount, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="6cd5e-215">To provision a user accounts, perform the following steps:</span></span>
1. <span data-ttu-id="6cd5e-216">Meld u aan bij uw **XMatters OnDemand** tenant.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-216">Log in to your **XMatters OnDemand** tenant.</span></span>

2.  <span data-ttu-id="6cd5e-217">Klik op **gebruikers** tabblad.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-217">Click **Users** tab.</span></span> <span data-ttu-id="6cd5e-218">en klik vervolgens op **gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-218">and then click **Add User**.</span></span>
  
    <span data-ttu-id="6cd5e-219">![Gebruikers](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781048.png "gebruikers")</span><span class="sxs-lookup"><span data-stu-id="6cd5e-219">![Users](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781048.png "Users")</span></span>

3. <span data-ttu-id="6cd5e-220">In de **toevoegen van een gebruiker** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="6cd5e-220">In the **Add a User** section, perform the following steps:</span></span>
   
    <span data-ttu-id="6cd5e-221">![Een gebruiker toevoegen](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781049.png "een gebruiker toevoegen")</span><span class="sxs-lookup"><span data-stu-id="6cd5e-221">![Add a User](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781049.png "Add a User")</span></span>

    <span data-ttu-id="6cd5e-222">a.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-222">a.</span></span> <span data-ttu-id="6cd5e-223">Selecteer **Active**.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-223">Select **Active**.</span></span>

    <span data-ttu-id="6cd5e-224">b.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-224">b.</span></span> <span data-ttu-id="6cd5e-225">In de **gebruikers-ID** textbox type de gebruikers-id van gebruiker, zoals Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-225">In the **User ID** textbox, type the user id of user like Brittasimon@contoso.com.</span></span>
   
    <span data-ttu-id="6cd5e-226">c.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-226">c.</span></span> <span data-ttu-id="6cd5e-227">In de **voornaam** textbox type voornaam van de gebruiker zoals Britta.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-227">In the **First Name** textbox, type first name of the user like Britta.</span></span>

    <span data-ttu-id="6cd5e-228">d.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-228">d.</span></span> <span data-ttu-id="6cd5e-229">In de **achternaam** textbox achternaam van de gebruiker zoals Simon type.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-229">In the **Last Name** textbox, type last name of the user like Simon.</span></span>
    
    <span data-ttu-id="6cd5e-230">e.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-230">e.</span></span> <span data-ttu-id="6cd5e-231">In de **Site** textbox, voer de geldige site van een geldig Azure AD-account die u inrichten wilt.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-231">In the **Site** textbox, Enter the valid site of a valid Azure AD account you want to provision.</span></span>
    
    <span data-ttu-id="6cd5e-232">f.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-232">f.</span></span> <span data-ttu-id="6cd5e-233">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-233">Click **Save**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="6cd5e-234">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="6cd5e-234">Assigning the Azure AD test user</span></span>

<span data-ttu-id="6cd5e-235">In deze sectie schakelt u Britta Simon Azure eenmalige aanmelding gebruiken door het verlenen van toegang tot xMatters OnDemand.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-235">In this section, you enable Britta Simon to use Azure single sign-on by granting access to xMatters OnDemand.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="6cd5e-237">**Britta Simon om aan te wijzen xMatters OnDemand, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="6cd5e-237">**To assign Britta Simon to xMatters OnDemand, perform the following steps:**</span></span>

1. <span data-ttu-id="6cd5e-238">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-238">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="6cd5e-240">Selecteer in de lijst met toepassingen **xMatters OnDemand**.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-240">In the applications list, select **xMatters OnDemand**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_app.png) 

3. <span data-ttu-id="6cd5e-242">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-242">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="6cd5e-244">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-244">Click **Add** button.</span></span> <span data-ttu-id="6cd5e-245">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="6cd5e-247">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-247">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6cd5e-248">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6cd5e-249">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6cd5e-250">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="6cd5e-250">Testing single sign-on</span></span>

<span data-ttu-id="6cd5e-251">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-251">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="6cd5e-252">Als u op de xMatters OnDemand-tegel in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw xMatters OnDemand-toepassing.</span><span class="sxs-lookup"><span data-stu-id="6cd5e-252">When you click the xMatters OnDemand tile in the Access Panel, you should get automatically signed-on to your xMatters OnDemand application.</span></span>
<span data-ttu-id="6cd5e-253">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6cd5e-253">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6cd5e-254">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="6cd5e-254">Additional resources</span></span>

* [<span data-ttu-id="6cd5e-255">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6cd5e-255">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6cd5e-256">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6cd5e-256">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_203.png

