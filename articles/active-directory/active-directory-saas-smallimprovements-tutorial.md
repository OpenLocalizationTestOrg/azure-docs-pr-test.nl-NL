---
title: 'Zelfstudie: Azure Active Directory-integratie met kleine verbeteringen | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory- en kleine verbeteringen.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 59c8a112-41e1-4337-9ef3-3d7029780d61
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 49a8cd3acfc6df15ef6a51171c8421162bc94efc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-small-improvements"></a><span data-ttu-id="a0882-103">Zelfstudie: Azure Active Directory-integratie met kleine verbeteringen</span><span class="sxs-lookup"><span data-stu-id="a0882-103">Tutorial: Azure Active Directory integration with Small Improvements</span></span>

<span data-ttu-id="a0882-104">In deze zelfstudie leert u hoe kleine verbeteringen integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a0882-104">In this tutorial, you learn how to integrate Small Improvements with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a0882-105">Kleine verbeteringen integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="a0882-105">Integrating Small Improvements with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a0882-106">U kunt beheren in Azure AD die toegang tot kleine verbeteringen heeft</span><span class="sxs-lookup"><span data-stu-id="a0882-106">You can control in Azure AD who has access to Small Improvements</span></span>
- <span data-ttu-id="a0882-107">U kunt uw gebruikers automatisch ophalen aangemeld bij kleine verbeteringen (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="a0882-107">You can enable your users to automatically get signed-on to Small Improvements (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a0882-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="a0882-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a0882-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a0882-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a0882-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a0882-110">Prerequisites</span></span>

<span data-ttu-id="a0882-111">Voor het configureren van Azure AD-integratie met kleine verbeteringen, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="a0882-111">To configure Azure AD integration with Small Improvements, you need the following items:</span></span>

- <span data-ttu-id="a0882-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="a0882-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a0882-113">Een kleine verbeteringen eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="a0882-113">A Small Improvements single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a0882-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="a0882-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a0882-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="a0882-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a0882-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="a0882-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a0882-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u hier een proefversie van één maand krijgen [proefversie aanbieding](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a0882-117">If you don't have an Azure AD trial environment, you can get a one-month trial here [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a0882-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="a0882-118">Scenario description</span></span>
<span data-ttu-id="a0882-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="a0882-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a0882-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="a0882-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a0882-121">Kleine verbeteringen in de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="a0882-121">Adding Small Improvements from the gallery</span></span>
2. <span data-ttu-id="a0882-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="a0882-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-small-improvements-from-the-gallery"></a><span data-ttu-id="a0882-123">Kleine verbeteringen in de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="a0882-123">Adding Small Improvements from the gallery</span></span>
<span data-ttu-id="a0882-124">Voor het configureren van de integratie van kleine verbeteringen in Azure AD, moet u kleine verbeteringen in de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="a0882-124">To configure the integration of Small Improvements into Azure AD, you need to add Small Improvements from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a0882-125">**Als u wilt toevoegen kleine verbeteringen in de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="a0882-125">**To add Small Improvements from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a0882-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="a0882-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a0882-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a0882-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a0882-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a0882-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="a0882-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a0882-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="a0882-133">Typ in het zoekvak **kleine verbeteringen**.</span><span class="sxs-lookup"><span data-stu-id="a0882-133">In the search box, type **Small Improvements**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_search.png)

5. <span data-ttu-id="a0882-135">Selecteer in het deelvenster resultaten **kleine verbeteringen**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="a0882-135">In the results panel, select **Small Improvements**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a0882-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="a0882-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a0882-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met kleine verbeteringen op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="a0882-138">In this section, you configure and test Azure AD single sign-on with Small Improvements based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a0882-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in kleine verbeteringen in Azure AD voor een gebruiker is.</span><span class="sxs-lookup"><span data-stu-id="a0882-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Small Improvements is to a user in Azure AD.</span></span> <span data-ttu-id="a0882-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in kleine verbeteringen tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="a0882-140">In other words, a link relationship between an Azure AD user and the related user in Small Improvements needs to be established.</span></span>

<span data-ttu-id="a0882-141">Wijs in kleine verbeteringen, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="a0882-141">In Small Improvements, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a0882-142">Om te configureren en testen van Azure AD eenmalige aanmelding met kleine verbeteringen, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="a0882-142">To configure and test Azure AD single sign-on with Small Improvements, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a0882-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a0882-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a0882-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a0882-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a0882-145">**[Maken van een testgebruiker kleine verbeteringen](#creating-a-small-improvements-test-user)**  - hebben een equivalent van Britta Simon in kleine verbeteringen die is gekoppeld aan de Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="a0882-145">**[Creating a Small Improvements test user](#creating-a-small-improvements-test-user)** - to have a counterpart of Britta Simon in Small Improvements that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a0882-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="a0882-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a0882-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="a0882-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a0882-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="a0882-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a0882-149">In deze sectie maakt u Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw toepassing kleine verbeteringen.</span><span class="sxs-lookup"><span data-stu-id="a0882-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Small Improvements application.</span></span>

<span data-ttu-id="a0882-150">**Voor het configureren van Azure AD eenmalige aanmelding met kleine verbeteringen, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="a0882-150">**To configure Azure AD single sign-on with Small Improvements, perform the following steps:**</span></span>

1. <span data-ttu-id="a0882-151">In de Azure-portal op de **kleine verbeteringen** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="a0882-151">In the Azure portal, on the **Small Improvements** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="a0882-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="a0882-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_samlbase.png)

3. <span data-ttu-id="a0882-155">Op de **kleine verbeteringen domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="a0882-155">On the **Small Improvements Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_url.png)

    <span data-ttu-id="a0882-157">a.</span><span class="sxs-lookup"><span data-stu-id="a0882-157">a.</span></span> <span data-ttu-id="a0882-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<subdomain>.small-improvements.com`</span><span class="sxs-lookup"><span data-stu-id="a0882-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.small-improvements.com`</span></span>

    <span data-ttu-id="a0882-159">b.</span><span class="sxs-lookup"><span data-stu-id="a0882-159">b.</span></span> <span data-ttu-id="a0882-160">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<subdomain>.small-improvements.com`</span><span class="sxs-lookup"><span data-stu-id="a0882-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.small-improvements.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a0882-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="a0882-161">These values are not real.</span></span> <span data-ttu-id="a0882-162">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="a0882-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="a0882-163">Neem contact op met [kleine verbeteringen Client ondersteuningsteam](mailto:support@small-improvements.com) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="a0882-163">Contact [Small Improvements Client support team](mailto:support@small-improvements.com) to get these values.</span></span> 
 
4. <span data-ttu-id="a0882-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="a0882-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_certificate.png) 

5. <span data-ttu-id="a0882-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="a0882-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a0882-168">Op de **kleine verbeteringen configuratie** sectie, klikt u op **kleine verbeteringen configureren** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="a0882-168">On the **Small Improvements Configuration** section, click **Configure Small Improvements** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a0882-169">Kopieer de **SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="a0882-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_configure.png) 

7. <span data-ttu-id="a0882-171">In een ander browservenster zich aanmelden bij uw bedrijf kleine verbeteringen site als een beheerder.</span><span class="sxs-lookup"><span data-stu-id="a0882-171">In another browser window, sign on to your Small Improvements company site as an administrator.</span></span>

8. <span data-ttu-id="a0882-172">Klik op de pagina hoofddashboard **beheer** knop aan de linkerkant.</span><span class="sxs-lookup"><span data-stu-id="a0882-172">From the main dashboard page, click **Administration** button on the left.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_06.png) 

9. <span data-ttu-id="a0882-174">Klik op de **SAML SSO** knop van **integraties** sectie.</span><span class="sxs-lookup"><span data-stu-id="a0882-174">Click the **SAML SSO** button from **Integrations** section.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_07.png) 

10. <span data-ttu-id="a0882-176">Voer de volgende stappen uit op de installatiepagina van eenmalige aanmelding:</span><span class="sxs-lookup"><span data-stu-id="a0882-176">On the SSO Setup page, perform the following steps:</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_08.png)  

    <span data-ttu-id="a0882-178">a.</span><span class="sxs-lookup"><span data-stu-id="a0882-178">a.</span></span> <span data-ttu-id="a0882-179">In de **HTTP-eindpunt** textbox, plak de waarde van **SAML Single Sign-On Service-URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="a0882-179">In the **HTTP Endpoint** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="a0882-180">b.</span><span class="sxs-lookup"><span data-stu-id="a0882-180">b.</span></span> <span data-ttu-id="a0882-181">Open uw gedownloade certificaat in Kladblok, Kopieer de inhoud en plakt u deze in de **x509 certificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="a0882-181">Open your downloaded certificate in Notepad, copy the content, and then paste it into the **x509 Certificate** textbox.</span></span> 

    <span data-ttu-id="a0882-182">c.</span><span class="sxs-lookup"><span data-stu-id="a0882-182">c.</span></span> <span data-ttu-id="a0882-183">Als u wilt dat eenmalige aanmelding en aanmelding formulier verificatieoptie beschikbaar voor gebruikers hebt, controleert u de **toegang via aanmelding en wachtwoord te inschakelen** optie.</span><span class="sxs-lookup"><span data-stu-id="a0882-183">If you wish to have SSO and Login form authentication option available for users, then check the **Enable access via login/password too** option.</span></span>  

    <span data-ttu-id="a0882-184">d.</span><span class="sxs-lookup"><span data-stu-id="a0882-184">d.</span></span> <span data-ttu-id="a0882-185">Voer de juiste waarde als naam voor de knop SSO aanmelden in de **SAML vragen** textbox.</span><span class="sxs-lookup"><span data-stu-id="a0882-185">Enter the appropriate value to Name the SSO Login button in the **SAML Prompt** textbox.</span></span>  

    <span data-ttu-id="a0882-186">e.</span><span class="sxs-lookup"><span data-stu-id="a0882-186">e.</span></span> <span data-ttu-id="a0882-187">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="a0882-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="a0882-188">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="a0882-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a0882-189">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="a0882-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a0882-190">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a0882-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a0882-191">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="a0882-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="a0882-192">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="a0882-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="a0882-194">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="a0882-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a0882-195">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="a0882-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-smallimprovements-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a0882-197">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="a0882-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-smallimprovements-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a0882-199">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a0882-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-smallimprovements-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a0882-201">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="a0882-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-smallimprovements-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a0882-203">a.</span><span class="sxs-lookup"><span data-stu-id="a0882-203">a.</span></span> <span data-ttu-id="a0882-204">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a0882-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a0882-205">b.</span><span class="sxs-lookup"><span data-stu-id="a0882-205">b.</span></span> <span data-ttu-id="a0882-206">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a0882-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a0882-207">c.</span><span class="sxs-lookup"><span data-stu-id="a0882-207">c.</span></span> <span data-ttu-id="a0882-208">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="a0882-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a0882-209">d.</span><span class="sxs-lookup"><span data-stu-id="a0882-209">d.</span></span> <span data-ttu-id="a0882-210">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="a0882-210">Click **Create**.</span></span>
 
### <a name="creating-a-small-improvements-test-user"></a><span data-ttu-id="a0882-211">Een kleine verbeteringen testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="a0882-211">Creating a Small Improvements test user</span></span>

<span data-ttu-id="a0882-212">Om Azure AD-gebruikers zich aanmelden bij kleine verbeteringen, moeten ze worden ingericht in kleine verbeteringen.</span><span class="sxs-lookup"><span data-stu-id="a0882-212">To enable Azure AD users to log in to Small Improvements, they must be provisioned into Small Improvements.</span></span> <span data-ttu-id="a0882-213">In het geval van kleine verbeteringen is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="a0882-213">In the case of Small Improvements, provisioning is a manual task.</span></span>

<span data-ttu-id="a0882-214">**Voor het inrichten van een gebruikersaccount, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="a0882-214">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="a0882-215">Aanmelding bij uw bedrijf kleine verbeteringen site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="a0882-215">Sign-on to your Small Improvements company site as an administrator.</span></span>

2. <span data-ttu-id="a0882-216">Vanaf de startpagina, gaat u naar het menu van de linkerkant, klik op **beheer**.</span><span class="sxs-lookup"><span data-stu-id="a0882-216">From the Home page, go to the menu on the left, click **Administration**.</span></span>

3. <span data-ttu-id="a0882-217">Klik op de **gebruikerslijst** knop uit de sectie beheer van gebruikers.</span><span class="sxs-lookup"><span data-stu-id="a0882-217">Click the **User Directory** button from User Management section.</span></span> 
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_10.png) 

4. <span data-ttu-id="a0882-219">Klik op **gebruikers toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="a0882-219">Click **Add users**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_11.png) 

5. <span data-ttu-id="a0882-221">Op de **gebruikers toevoegen** dialoogvenster de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="a0882-221">On the **Add Users** dialog, perform the following steps:</span></span> 

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_12.png)
    
    <span data-ttu-id="a0882-223">a.</span><span class="sxs-lookup"><span data-stu-id="a0882-223">a.</span></span> <span data-ttu-id="a0882-224">Voer de **voornaam** van gebruiker zoals **Britta**.</span><span class="sxs-lookup"><span data-stu-id="a0882-224">Enter the **first name** of user like **Britta**.</span></span>

    <span data-ttu-id="a0882-225">b.</span><span class="sxs-lookup"><span data-stu-id="a0882-225">b.</span></span> <span data-ttu-id="a0882-226">Voer de **achternaam** van gebruiker zoals **Simon**.</span><span class="sxs-lookup"><span data-stu-id="a0882-226">Enter the **Last name** of user like **Simon**.</span></span>

    <span data-ttu-id="a0882-227">c.</span><span class="sxs-lookup"><span data-stu-id="a0882-227">c.</span></span> <span data-ttu-id="a0882-228">Voer de **e** van gebruiker zoals  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="a0882-228">Enter the **Email** of user like **brittasimon@contoso.com**.</span></span> 

    <span data-ttu-id="a0882-229">d.</span><span class="sxs-lookup"><span data-stu-id="a0882-229">d.</span></span> <span data-ttu-id="a0882-230">U kunt er ook voor kiezen om in te voeren van het persoonlijke bericht in de **e-mailmelding verzenden** vak.</span><span class="sxs-lookup"><span data-stu-id="a0882-230">You can also choose to enter the personal message in the **Send notification email** box.</span></span> <span data-ttu-id="a0882-231">Als u niet verzenden van de melding wilt, schakelt u dit selectievakje in.</span><span class="sxs-lookup"><span data-stu-id="a0882-231">If you do not wish to send the notification, then uncheck this checkbox.</span></span>

    <span data-ttu-id="a0882-232">e.</span><span class="sxs-lookup"><span data-stu-id="a0882-232">e.</span></span> <span data-ttu-id="a0882-233">Klik op **gebruikers maken**.</span><span class="sxs-lookup"><span data-stu-id="a0882-233">Click **Create Users**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a0882-234">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="a0882-234">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a0882-235">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan kleine verbeteringen.</span><span class="sxs-lookup"><span data-stu-id="a0882-235">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Small Improvements.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="a0882-237">**Britta Simon om aan te wijzen kleine verbeteringen, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="a0882-237">**To assign Britta Simon to Small Improvements, perform the following steps:**</span></span>

1. <span data-ttu-id="a0882-238">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a0882-238">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="a0882-240">Selecteer in de lijst met toepassingen **kleine verbeteringen**.</span><span class="sxs-lookup"><span data-stu-id="a0882-240">In the applications list, select **Small Improvements**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_app.png) 

3. <span data-ttu-id="a0882-242">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="a0882-242">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="a0882-244">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="a0882-244">Click **Add** button.</span></span> <span data-ttu-id="a0882-245">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a0882-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="a0882-247">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="a0882-247">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a0882-248">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a0882-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a0882-249">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a0882-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a0882-250">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="a0882-250">Testing single sign-on</span></span>

<span data-ttu-id="a0882-251">Het doel van deze sectie is het testen van uw Azure AD SSO-configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="a0882-251">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="a0882-252">Als u op de tegel kleine verbeteringen in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing kleine verbeteringen.</span><span class="sxs-lookup"><span data-stu-id="a0882-252">When you click the Small Improvements tile in the Access Panel, you should get automatically signed-on to your Small Improvements application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a0882-253">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="a0882-253">Additional resources</span></span>

* [<span data-ttu-id="a0882-254">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a0882-254">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a0882-255">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a0882-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_203.png

