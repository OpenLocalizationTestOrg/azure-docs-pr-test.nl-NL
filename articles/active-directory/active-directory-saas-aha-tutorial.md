---
title: 'Zelfstudie: Azure Active Directory-integratie met Aha! | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Aha!.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ad955d3d-896a-41bb-800d-68e8cb5ff48d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 7723864b2e1ab2d5b69d86f0fa18416b9d3f9aa3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-aha"></a><span data-ttu-id="1a121-104">Zelfstudie: Azure Active Directory-integratie met Aha!</span><span class="sxs-lookup"><span data-stu-id="1a121-104">Tutorial: Azure Active Directory integration with Aha!</span></span>

<span data-ttu-id="1a121-105">In deze zelfstudie leert u hoe integreren Aha!</span><span class="sxs-lookup"><span data-stu-id="1a121-105">In this tutorial, you learn how to integrate Aha!</span></span> <span data-ttu-id="1a121-106">met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1a121-106">with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1a121-107">Integratie van Aha!</span><span class="sxs-lookup"><span data-stu-id="1a121-107">Integrating Aha!</span></span> <span data-ttu-id="1a121-108">met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="1a121-108">with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1a121-109">U kunt beheren in Azure AD die toegang tot Aha heeft!</span><span class="sxs-lookup"><span data-stu-id="1a121-109">You can control in Azure AD who has access to Aha!</span></span>
- <span data-ttu-id="1a121-110">U kunt uw gebruikers automatisch ophalen aangemeld bij Aha inschakelen!</span><span class="sxs-lookup"><span data-stu-id="1a121-110">You can enable your users to automatically get signed-on to Aha!</span></span> <span data-ttu-id="1a121-111">(Single Sign-On) met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="1a121-111">(Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1a121-112">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="1a121-112">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1a121-113">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1a121-113">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1a121-114">Vereisten</span><span class="sxs-lookup"><span data-stu-id="1a121-114">Prerequisites</span></span>

<span data-ttu-id="1a121-115">Configureren van Azure AD-integratie met Aha!, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="1a121-115">To configure Azure AD integration with Aha!, you need the following items:</span></span>

- <span data-ttu-id="1a121-116">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="1a121-116">An Azure AD subscription</span></span>
- <span data-ttu-id="1a121-117">Een Aha!</span><span class="sxs-lookup"><span data-stu-id="1a121-117">An Aha!</span></span> <span data-ttu-id="1a121-118">eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="1a121-118">single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1a121-119">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="1a121-119">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1a121-120">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="1a121-120">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1a121-121">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="1a121-121">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1a121-122">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1a121-122">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1a121-123">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="1a121-123">Scenario description</span></span>
<span data-ttu-id="1a121-124">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="1a121-124">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1a121-125">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="1a121-125">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1a121-126">Toe te voegen Aha!</span><span class="sxs-lookup"><span data-stu-id="1a121-126">Adding Aha!</span></span> <span data-ttu-id="1a121-127">in de galerie</span><span class="sxs-lookup"><span data-stu-id="1a121-127">from the gallery</span></span>
2. <span data-ttu-id="1a121-128">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="1a121-128">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-aha-from-the-gallery"></a><span data-ttu-id="1a121-129">Toe te voegen Aha!</span><span class="sxs-lookup"><span data-stu-id="1a121-129">Adding Aha!</span></span> <span data-ttu-id="1a121-130">in de galerie</span><span class="sxs-lookup"><span data-stu-id="1a121-130">from the gallery</span></span>
<span data-ttu-id="1a121-131">Voor het configureren van de integratie van Aha!</span><span class="sxs-lookup"><span data-stu-id="1a121-131">To configure the integration of Aha!</span></span> <span data-ttu-id="1a121-132">met Azure AD moet u toevoegen Aha!</span><span class="sxs-lookup"><span data-stu-id="1a121-132">into Azure AD, you need to add Aha!</span></span> <span data-ttu-id="1a121-133">in de galerie aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="1a121-133">from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1a121-134">**Om toe te voegen Aha! in de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="1a121-134">**To add Aha! from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1a121-135">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="1a121-135">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1a121-137">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="1a121-137">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1a121-138">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="1a121-138">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="1a121-140">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1a121-140">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="1a121-142">Typ in het zoekvak **Aha!**.</span><span class="sxs-lookup"><span data-stu-id="1a121-142">In the search box, type **Aha!**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-aha-tutorial/tutorial_aha_search.png)

5. <span data-ttu-id="1a121-144">Selecteer in het deelvenster resultaten **Aha!**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="1a121-144">In the results panel, select **Aha!**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-aha-tutorial/tutorial_aha_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1a121-146">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="1a121-146">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1a121-147">In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met Aha!</span><span class="sxs-lookup"><span data-stu-id="1a121-147">In this section, you configure and test Azure AD single sign-on with Aha!</span></span> <span data-ttu-id="1a121-148">op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="1a121-148">based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1a121-149">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de equivalente gebruiker in Aha!</span><span class="sxs-lookup"><span data-stu-id="1a121-149">For single sign-on to work, Azure AD needs to know what the counterpart user in Aha!</span></span> <span data-ttu-id="1a121-150">is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1a121-150">is to a user in Azure AD.</span></span> <span data-ttu-id="1a121-151">Met andere woorden, een relatie koppeling tussen een Azure AD-gebruiker en de betreffende gebruiker in Aha!</span><span class="sxs-lookup"><span data-stu-id="1a121-151">In other words, a link relationship between an Azure AD user and the related user in Aha!</span></span> <span data-ttu-id="1a121-152">moet worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1a121-152">needs to be established.</span></span>

<span data-ttu-id="1a121-153">In Aha!, wijs de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="1a121-153">In Aha!, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1a121-154">Configureren en testen Azure AD eenmalige aanmelding met Aha!, u moet voltooien van de volgende elementen:</span><span class="sxs-lookup"><span data-stu-id="1a121-154">To configure and test Azure AD single sign-on with Aha!, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1a121-155">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1a121-155">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1a121-156">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1a121-156">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1a121-157">**[Maken van een Aha! testgebruiker](#creating-an-aha-test-user)**  - met een exemplaar van Britta Simon Aha!</span><span class="sxs-lookup"><span data-stu-id="1a121-157">**[Creating an Aha! test user](#creating-an-aha-test-user)** - to have a counterpart of Britta Simon in Aha!</span></span> <span data-ttu-id="1a121-158">dat is gekoppeld aan de Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="1a121-158">that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1a121-159">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="1a121-159">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1a121-160">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="1a121-160">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1a121-161">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="1a121-161">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1a121-162">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw Aha!</span><span class="sxs-lookup"><span data-stu-id="1a121-162">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Aha!</span></span> <span data-ttu-id="1a121-163">de toepassing.</span><span class="sxs-lookup"><span data-stu-id="1a121-163">application.</span></span>

<span data-ttu-id="1a121-164">**Eenmalige aanmelding Azure AD configureren met Aha!, de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="1a121-164">**To configure Azure AD single sign-on with Aha!, perform the following steps:**</span></span>

1. <span data-ttu-id="1a121-165">In de Azure-portal op de **Aha!**</span><span class="sxs-lookup"><span data-stu-id="1a121-165">In the Azure portal, on the **Aha!**</span></span> <span data-ttu-id="1a121-166">pagina van de integratie van toepassing, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="1a121-166">application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="1a121-168">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="1a121-168">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-aha-tutorial/tutorial_aha_samlbase.png)

3. <span data-ttu-id="1a121-170">Op de **Aha! Domein- en URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="1a121-170">On the **Aha! Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-aha-tutorial/tutorial_aha_url.png)

    <span data-ttu-id="1a121-172">a.</span><span class="sxs-lookup"><span data-stu-id="1a121-172">a.</span></span> <span data-ttu-id="1a121-173">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<companyname>.aha.io/session/new`</span><span class="sxs-lookup"><span data-stu-id="1a121-173">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.aha.io/session/new`</span></span>

    <span data-ttu-id="1a121-174">b.</span><span class="sxs-lookup"><span data-stu-id="1a121-174">b.</span></span> <span data-ttu-id="1a121-175">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<companyname>.aha.io`</span><span class="sxs-lookup"><span data-stu-id="1a121-175">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.aha.io`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1a121-176">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="1a121-176">These values are not real.</span></span> <span data-ttu-id="1a121-177">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="1a121-177">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="1a121-178">Neem contact op met [Aha! Client-ondersteuningsteam](https://www.aha.io/company/contact) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="1a121-178">Contact [Aha! Client support team](https://www.aha.io/company/contact) to get these values.</span></span> 
 
4. <span data-ttu-id="1a121-179">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="1a121-179">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-aha-tutorial/tutorial_aha_certificate.png) 

5. <span data-ttu-id="1a121-181">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="1a121-181">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-aha-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1a121-183">In een ander browservenster, meld u aan bij uw Aha!</span><span class="sxs-lookup"><span data-stu-id="1a121-183">In a different web browser window, log in to your Aha!</span></span> <span data-ttu-id="1a121-184">bedrijf-site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="1a121-184">company site as an administrator.</span></span>

7. <span data-ttu-id="1a121-185">Klik in het menu bovenaan op **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="1a121-185">In the menu on the top, click **Settings**.</span></span>

    <span data-ttu-id="1a121-186">![Instellingen](./media/active-directory-saas-aha-tutorial/IC798950.png "instellingen")</span><span class="sxs-lookup"><span data-stu-id="1a121-186">![Settings](./media/active-directory-saas-aha-tutorial/IC798950.png "Settings")</span></span>

8. <span data-ttu-id="1a121-187">Klik op **Account**.</span><span class="sxs-lookup"><span data-stu-id="1a121-187">Click **Account**.</span></span>
   
    <span data-ttu-id="1a121-188">![Profiel](./media/active-directory-saas-aha-tutorial/IC798951.png "profiel")</span><span class="sxs-lookup"><span data-stu-id="1a121-188">![Profile](./media/active-directory-saas-aha-tutorial/IC798951.png "Profile")</span></span>

9. <span data-ttu-id="1a121-189">Klik op **beveiligings- en eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="1a121-189">Click **Security and single sign-on**.</span></span>
   
    <span data-ttu-id="1a121-190">![Beveiliging en eenmalige aanmelding](./media/active-directory-saas-aha-tutorial/IC798952.png "beveiligings- en eenmalige aanmelding")</span><span class="sxs-lookup"><span data-stu-id="1a121-190">![Security and single sign-on](./media/active-directory-saas-aha-tutorial/IC798952.png "Security and single sign-on")</span></span>

10. <span data-ttu-id="1a121-191">In **Single Sign-On** sectie als **identiteitsprovider**, selecteer **SAML2.0**.</span><span class="sxs-lookup"><span data-stu-id="1a121-191">In **Single Sign-On** section, as **Identity Provider**, select **SAML2.0**.</span></span>
   
    <span data-ttu-id="1a121-192">![Beveiliging en eenmalige aanmelding](./media/active-directory-saas-aha-tutorial/IC798953.png "beveiligings- en eenmalige aanmelding")</span><span class="sxs-lookup"><span data-stu-id="1a121-192">![Security and single sign-on](./media/active-directory-saas-aha-tutorial/IC798953.png "Security and single sign-on")</span></span>

11. <span data-ttu-id="1a121-193">Op de **Single Sign-On** configuratie pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="1a121-193">On the **Single Sign-On** configuration page, perform the following steps:</span></span>
    
    <span data-ttu-id="1a121-194">![Eenmalige aanmelding](./media/active-directory-saas-aha-tutorial/IC798954.png "eenmalige aanmelding")</span><span class="sxs-lookup"><span data-stu-id="1a121-194">![Single Sign-On](./media/active-directory-saas-aha-tutorial/IC798954.png "Single Sign-On")</span></span>
    
       <span data-ttu-id="1a121-195">a.</span><span class="sxs-lookup"><span data-stu-id="1a121-195">a.</span></span> <span data-ttu-id="1a121-196">In de **naam** textbox, typ een naam voor uw configuratie.</span><span class="sxs-lookup"><span data-stu-id="1a121-196">In the **Name** textbox, type a name for your configuration.</span></span>

       <span data-ttu-id="1a121-197">b.</span><span class="sxs-lookup"><span data-stu-id="1a121-197">b.</span></span> <span data-ttu-id="1a121-198">Voor **configureren met behulp van**, selecteer **metagegevensbestand**.</span><span class="sxs-lookup"><span data-stu-id="1a121-198">For **Configure using**, select **Metadata File**.</span></span>
   
       <span data-ttu-id="1a121-199">c.</span><span class="sxs-lookup"><span data-stu-id="1a121-199">c.</span></span> <span data-ttu-id="1a121-200">Als u wilt uw van het gedownloade metagegevensbestand uploadt, klikt u op **Bladeren**.</span><span class="sxs-lookup"><span data-stu-id="1a121-200">To upload your downloaded metadata file, click **Browse**.</span></span>
   
       <span data-ttu-id="1a121-201">d.</span><span class="sxs-lookup"><span data-stu-id="1a121-201">d.</span></span> <span data-ttu-id="1a121-202">Klik op **Update**.</span><span class="sxs-lookup"><span data-stu-id="1a121-202">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="1a121-203">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="1a121-203">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1a121-204">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="1a121-204">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1a121-205">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1a121-205">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1a121-206">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="1a121-206">Creating an Azure AD test user</span></span>
<span data-ttu-id="1a121-207">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="1a121-207">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="1a121-209">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="1a121-209">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1a121-210">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="1a121-210">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-aha-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1a121-212">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="1a121-212">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-aha-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1a121-214">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1a121-214">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-aha-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1a121-216">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="1a121-216">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-aha-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1a121-218">a.</span><span class="sxs-lookup"><span data-stu-id="1a121-218">a.</span></span> <span data-ttu-id="1a121-219">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1a121-219">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1a121-220">b.</span><span class="sxs-lookup"><span data-stu-id="1a121-220">b.</span></span> <span data-ttu-id="1a121-221">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1a121-221">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1a121-222">c.</span><span class="sxs-lookup"><span data-stu-id="1a121-222">c.</span></span> <span data-ttu-id="1a121-223">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="1a121-223">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1a121-224">d.</span><span class="sxs-lookup"><span data-stu-id="1a121-224">d.</span></span> <span data-ttu-id="1a121-225">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="1a121-225">Click **Create**.</span></span>
 
### <a name="creating-an-aha-test-user"></a><span data-ttu-id="1a121-226">Maken van een Aha!</span><span class="sxs-lookup"><span data-stu-id="1a121-226">Creating an Aha!</span></span> <span data-ttu-id="1a121-227">testgebruiker</span><span class="sxs-lookup"><span data-stu-id="1a121-227">test user</span></span>

<span data-ttu-id="1a121-228">Inschakelen van Azure AD-gebruikers zich aanmelden bij Aha!, deze moeten worden ingericht in Aha!.</span><span class="sxs-lookup"><span data-stu-id="1a121-228">To enable Azure AD users to log in to Aha!, they must be provisioned into Aha!.</span></span>  

<span data-ttu-id="1a121-229">In het geval van Aha!, wordt een geautomatiseerde taak ingericht.</span><span class="sxs-lookup"><span data-stu-id="1a121-229">In the case of Aha!, provisioning is an automated task.</span></span> <span data-ttu-id="1a121-230">Er is geen actie-item voor u.</span><span class="sxs-lookup"><span data-stu-id="1a121-230">There is no action item for you.</span></span>

<span data-ttu-id="1a121-231">Gebruikers worden automatisch gemaakt indien nodig tijdens de eerste eenmalige aanmelding poging.</span><span class="sxs-lookup"><span data-stu-id="1a121-231">Users are automatically created if necessary during the first single sign-on attempt.</span></span>

>[!NOTE]
><span data-ttu-id="1a121-232">U kunt andere Aha!</span><span class="sxs-lookup"><span data-stu-id="1a121-232">You can use any other Aha!</span></span> <span data-ttu-id="1a121-233">hulpmiddelen voor het maken van account of API's die worden geleverd door Aha!</span><span class="sxs-lookup"><span data-stu-id="1a121-233">user account creation tools or APIs provided by Aha!</span></span> <span data-ttu-id="1a121-234">voor het inrichten van AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="1a121-234">to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1a121-235">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="1a121-235">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1a121-236">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Aha!.</span><span class="sxs-lookup"><span data-stu-id="1a121-236">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Aha!.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="1a121-238">**Britta Simon toewijzen aan Aha!, de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="1a121-238">**To assign Britta Simon to Aha!, perform the following steps:**</span></span>

1. <span data-ttu-id="1a121-239">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="1a121-239">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="1a121-241">Selecteer in de lijst met toepassingen **Aha!**.</span><span class="sxs-lookup"><span data-stu-id="1a121-241">In the applications list, select **Aha!**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-aha-tutorial/tutorial_aha_app.png) 

3. <span data-ttu-id="1a121-243">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="1a121-243">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="1a121-245">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="1a121-245">Click **Add** button.</span></span> <span data-ttu-id="1a121-246">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1a121-246">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="1a121-248">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="1a121-248">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1a121-249">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1a121-249">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1a121-250">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1a121-250">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1a121-251">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="1a121-251">Testing single sign-on</span></span>

<span data-ttu-id="1a121-252">Als u testen van uw instellingen voor eenmalige aanmelding wilt, opent u het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="1a121-252">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="1a121-253">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1a121-253">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1a121-254">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="1a121-254">Additional resources</span></span>

* [<span data-ttu-id="1a121-255">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1a121-255">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1a121-256">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1a121-256">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-aha-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-aha-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-aha-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-aha-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-aha-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-aha-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-aha-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-aha-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-aha-tutorial/tutorial_general_203.png

