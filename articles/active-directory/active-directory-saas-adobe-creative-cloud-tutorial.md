---
title: 'Zelfstudie: Azure Active Directory-integratie met Adobe Creative Cloud | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Adobe Creative Cloud.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9ba1171e-56b1-4475-b308-58637d35e5a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 3d13608612c77236346b0e98551d7fc427d602e1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adobe-creative-cloud"></a><span data-ttu-id="daa78-103">Zelfstudie: Azure Active Directory-integratie met Adobe Creative Cloud</span><span class="sxs-lookup"><span data-stu-id="daa78-103">Tutorial: Azure Active Directory integration with Adobe Creative Cloud</span></span>

<span data-ttu-id="daa78-104">In deze zelfstudie leert u hoe Adobe Creative Cloud integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="daa78-104">In this tutorial, you learn how to integrate Adobe Creative Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="daa78-105">Adobe Creative Cloud integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="daa78-105">Integrating Adobe Creative Cloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="daa78-106">U kunt beheren in Azure AD die toegang tot Adobe Creative Cloud heeft</span><span class="sxs-lookup"><span data-stu-id="daa78-106">You can control in Azure AD who has access to Adobe Creative Cloud</span></span>
- <span data-ttu-id="daa78-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Adobe Creative Cloud (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="daa78-107">You can enable your users to automatically get signed-on to Adobe Creative Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="daa78-108">U kunt uw accounts op één centrale locatie - en de Azure Management portal beheren</span><span class="sxs-lookup"><span data-stu-id="daa78-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="daa78-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="daa78-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="daa78-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="daa78-110">Prerequisites</span></span>

<span data-ttu-id="daa78-111">Voor het configureren van Azure AD-integratie met Adobe Creative Cloud, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="daa78-111">To configure Azure AD integration with Adobe Creative Cloud, you need the following items:</span></span>

- <span data-ttu-id="daa78-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="daa78-112">An Azure AD subscription</span></span>
- <span data-ttu-id="daa78-113">Een Adobe Creative Cloud eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="daa78-113">A Adobe Creative Cloud single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="daa78-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="daa78-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="daa78-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="daa78-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="daa78-116">U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="daa78-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="daa78-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="daa78-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="daa78-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="daa78-118">Scenario description</span></span>
<span data-ttu-id="daa78-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="daa78-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="daa78-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="daa78-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="daa78-121">Adobe Creative Cloud uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="daa78-121">Adding Adobe Creative Cloud from the gallery</span></span>
2. <span data-ttu-id="daa78-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="daa78-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adobe-creative-cloud-from-the-gallery"></a><span data-ttu-id="daa78-123">Adobe Creative Cloud uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="daa78-123">Adding Adobe Creative Cloud from the gallery</span></span>
<span data-ttu-id="daa78-124">Voor het configureren van de integratie van Adobe Creative Cloud met Azure AD, moet u Adobe Creative Cloud uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="daa78-124">To configure the integration of Adobe Creative Cloud into Azure AD, you need to add Adobe Creative Cloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="daa78-125">**Als u wilt toevoegen Adobe Creative Cloud uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="daa78-125">**To add Adobe Creative Cloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="daa78-126">In de  **[Azure Management Portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="daa78-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="daa78-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="daa78-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="daa78-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="daa78-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="daa78-131">Klik op **toevoegen** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="daa78-131">Click **Add** button on the top of the dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="daa78-133">Typ in het zoekvak **Adobe Creative Cloud**.</span><span class="sxs-lookup"><span data-stu-id="daa78-133">In the search box, type **Adobe Creative Cloud**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_000.png)

5. <span data-ttu-id="daa78-135">Selecteer in het deelvenster resultaten **Adobe Creative Cloud**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="daa78-135">In the results panel, select **Adobe Creative Cloud**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_0001.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="daa78-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="daa78-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="daa78-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Adobe Creative Cloud op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="daa78-138">In this section, you configure and test Azure AD single sign-on with Adobe Creative Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="daa78-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Adobe Creative Cloud is aan een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="daa78-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Adobe Creative Cloud is to a user in Azure AD.</span></span> <span data-ttu-id="daa78-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Adobe Creative Cloud worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="daa78-140">In other words, a link relationship between an Azure AD user and the related user in Adobe Creative Cloud needs to be established.</span></span>

<span data-ttu-id="daa78-141">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in Adobe Creative Cloud.</span><span class="sxs-lookup"><span data-stu-id="daa78-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Adobe Creative Cloud.</span></span>

<span data-ttu-id="daa78-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Adobe Creative Cloud, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="daa78-142">To configure and test Azure AD single sign-on with Adobe Creative Cloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="daa78-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="daa78-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="daa78-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="daa78-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="daa78-145">**[Maken van een testgebruiker Adobe Creative Cloud](#creating-an-adobe-creative-cloud-test-user)**  : een equivalent van Britta Simon in Adobe Creative Cloud die is gekoppeld aan de Azure AD-representatie van haar hebben.</span><span class="sxs-lookup"><span data-stu-id="daa78-145">**[Creating an Adobe Creative Cloud test user](#creating-an-adobe-creative-cloud-test-user)** - to have a counterpart of Britta Simon in Adobe Creative Cloud that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="daa78-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="daa78-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="daa78-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="daa78-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="daa78-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="daa78-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="daa78-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure-beheerportal en eenmalige aanmelding configureren in uw toepassing Adobe Creative Cloud.</span><span class="sxs-lookup"><span data-stu-id="daa78-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Adobe Creative Cloud application.</span></span>

<span data-ttu-id="daa78-150">**Om eenmalige aanmelding Azure AD met Adobe Creative Cloud configureert, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="daa78-150">**To configure Azure AD single sign-on with Adobe Creative Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="daa78-151">In de Azure-beheerportal op de **Adobe Creative Cloud** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="daa78-151">In the Azure Management portal, on the **Adobe Creative Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="daa78-153">Op de **eenmalige aanmelding** dialoogvenster als **modus** Selecteer **op basis van SAML aanmelding** eenmalige aanmelding inschakelen op.</span><span class="sxs-lookup"><span data-stu-id="daa78-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_01.png)

3. <span data-ttu-id="daa78-155">Op de **Adobe Creative Cloud-domein en de URL's** sectie, voert u de volgende stappen uit als u wilt configureren, de toepassing in **IDP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="daa78-155">On the **Adobe Creative Cloud Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url1.png)

    <span data-ttu-id="daa78-157">a.</span><span class="sxs-lookup"><span data-stu-id="daa78-157">a.</span></span> <span data-ttu-id="daa78-158">In de **id** textbox, typ de waarde als:`https://www.okta.com/saml2/service-provider/<token>`</span><span class="sxs-lookup"><span data-stu-id="daa78-158">In the **Identifier** textbox, type the value as: `https://www.okta.com/saml2/service-provider/<token>`</span></span>

    <span data-ttu-id="daa78-159">b.</span><span class="sxs-lookup"><span data-stu-id="daa78-159">b.</span></span> <span data-ttu-id="daa78-160">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://<company name>.okta.com/auth/saml20/accauthlinktest`</span><span class="sxs-lookup"><span data-stu-id="daa78-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.okta.com/auth/saml20/accauthlinktest`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="daa78-161">Houd er rekening mee dat deze niet de werkelijke waarden zijn.</span><span class="sxs-lookup"><span data-stu-id="daa78-161">Please note that these are not the real values.</span></span> <span data-ttu-id="daa78-162">U hebt deze waarden bijwerken met de werkelijke id en de antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="daa78-162">You have to update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="daa78-163">Hier raden we u voor het gebruik van de unieke waarde van een tekenreeks in de id.</span><span class="sxs-lookup"><span data-stu-id="daa78-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="daa78-164">Als u een gebruiker handmatig maken wilt, moet u contact op met het ondersteuningsteam van Adobe Creative Cloud.</span><span class="sxs-lookup"><span data-stu-id="daa78-164">If you need to create an user manually, you need to contact the Adobe Creative Cloud support team.</span></span>

4. <span data-ttu-id="daa78-165">Op de **Adobe Creative Cloud-domein en de URL's** sectie, voert u de volgende stappen uit als u wilt configureren, de toepassing in **SP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="daa78-165">On the **Adobe Creative Cloud Domain and URLs** section, perform the following steps if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url2.png)

    <span data-ttu-id="daa78-167">a.</span><span class="sxs-lookup"><span data-stu-id="daa78-167">a.</span></span> <span data-ttu-id="daa78-168">Klik op de **weergeven geavanceerde instellingen voor URL** optie</span><span class="sxs-lookup"><span data-stu-id="daa78-168">Click on the **Show advanced URL settings** option</span></span>

    <span data-ttu-id="daa78-169">b.</span><span class="sxs-lookup"><span data-stu-id="daa78-169">b.</span></span> <span data-ttu-id="daa78-170">In de **aanmeldings-URL** textbox, typ de waarde als:`https://adobe.com`</span><span class="sxs-lookup"><span data-stu-id="daa78-170">In the **Sign-on URL** textbox, type the value as: `https://adobe.com`</span></span>

5. <span data-ttu-id="daa78-171">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="daa78-171">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_05.png) 

6. <span data-ttu-id="daa78-173">Op de **Adobe Creative Cloudconfiguratie** sectie, klikt u op **Adobe Creative Cloud configureren** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="daa78-173">On the **Adobe Creative Cloud Configuration** section, click **Configure Adobe Creative Cloud** to open **Configure sign-on** window.</span></span> <span data-ttu-id="daa78-174">Kopieer de **SAML entiteit-Id** en **SAML SSO Service URL** van naslag-sectie.</span><span class="sxs-lookup"><span data-stu-id="daa78-174">Please copy the **SAML Entity Id** and **SAML SSO Service URL** from Quick Reference section.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_06.png) 

7. <span data-ttu-id="daa78-176">In een ander browservenster aanmelding bij uw cloudtenant van Adobe Creative als beheerder.</span><span class="sxs-lookup"><span data-stu-id="daa78-176">In a different web browser window, sign-on to your Adobe Creative Cloud tenant as an administrator.</span></span>

8.  <span data-ttu-id="daa78-177">Ga naar **identiteit** in het navigatiedeelvenster links en klikt u op uw domein.</span><span class="sxs-lookup"><span data-stu-id="daa78-177">Go to **Identity** on the left navigation pane and click your domain.</span></span> <span data-ttu-id="daa78-178">Voer de volgende stappen uit op **eenmalige aanmelding op configuratie vereist** sectie.</span><span class="sxs-lookup"><span data-stu-id="daa78-178">Then perform the following steps on **Single Sign On Configuration Required** section.</span></span>

    <span data-ttu-id="daa78-179">![Instellingen](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_001.png "instellingen")</span><span class="sxs-lookup"><span data-stu-id="daa78-179">![Settings](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_001.png "Settings")</span></span>

9. <span data-ttu-id="daa78-180">Klik op **Bladeren** voor het uploaden van het gedownloade certificaat uit Azure AD **IDP certificaat**.</span><span class="sxs-lookup"><span data-stu-id="daa78-180">Click **Browse** to upload the downloaded certificate from Azure AD to **IDP Certificate**.</span></span>

10. <span data-ttu-id="daa78-181">In de **IDP verlener** textbox, plaatst u de waarde van **SAML entiteit-Id** die u hebt gekopieerd uit **eenmalige aanmelding configureren** sectie in Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="daa78-181">In the **IDP issuer** textbox, put the value of **SAML Entity Id** which you copied from **Configure sign-on** section in Azure portal.</span></span>

11. <span data-ttu-id="daa78-182">In de **IDP aanmeldings-URL** textbox, plaatst u de waarde van **SAML SSO Service URL** die u hebt gekopieerd uit **eenmalige aanmelding configureren** sectie in Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="daa78-182">In the **IDP Login URL** textbox, put the value of **SAML SSO Service URL** which you copied from **Configure sign-on** section in Azure portal.</span></span>

12. <span data-ttu-id="daa78-183">Selecteer **HTTP - omleiding** als **IDP Binding**.</span><span class="sxs-lookup"><span data-stu-id="daa78-183">Select **HTTP - Redirect** as **IDP Binding**.</span></span>

13. <span data-ttu-id="daa78-184">Selecteer **e-mailadres** als **aanmelding gebruikersinstelling**.</span><span class="sxs-lookup"><span data-stu-id="daa78-184">Select **Email Address** as **User Login Setting**.</span></span>
 
14. <span data-ttu-id="daa78-185">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="daa78-185">Click **Save** button.</span></span>

15. <span data-ttu-id="daa78-186">Het dashboard biedt nu de XML **'Metagegevens downloaden'** bestand.</span><span class="sxs-lookup"><span data-stu-id="daa78-186">The dashboard will now present the XML **"Download Metadata"** file.</span></span> <span data-ttu-id="daa78-187">Het bevat van Adobe EntityDescriptor URL's en AssertionConsumerService.</span><span class="sxs-lookup"><span data-stu-id="daa78-187">It contains Adobe’s EntityDescriptor URL and AssertionConsumerService URL.</span></span> <span data-ttu-id="daa78-188">Open het bestand en configureer deze in de Azure AD-toepassing.</span><span class="sxs-lookup"><span data-stu-id="daa78-188">Please open the file and configure them in the Azure AD application.</span></span>

    ![App-zijde eenmalige aanmelding configureren](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_002.png)

    ![App-zijde eenmalige aanmelding configureren](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_003.png)

    <span data-ttu-id="daa78-191">a.</span><span class="sxs-lookup"><span data-stu-id="daa78-191">a.</span></span> <span data-ttu-id="daa78-192">Gebruik de waarde van de EntityDescriptor Adobe geleverd, kunt u voor **id** op de **App-instellingen configureren** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="daa78-192">Use the EntityDescriptor value Adobe provided you for **Identifier** on the **Configure App Settings** dialog.</span></span>

    <span data-ttu-id="daa78-193">b.</span><span class="sxs-lookup"><span data-stu-id="daa78-193">b.</span></span> <span data-ttu-id="daa78-194">Gebruik de waarde van de AssertionConsumerService Adobe geleverd, kunt u voor **antwoord-URL** op de **App-instellingen configureren** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="daa78-194">Use the AssertionConsumerService value Adobe provided you for **Reply URL** on the **Configure App Settings** dialog.</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="daa78-195">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="daa78-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="daa78-196">Het doel van deze sectie is het een testgebruiker maken in Azure Management portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="daa78-196">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="daa78-198">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="daa78-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="daa78-199">In de **Azure Management portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="daa78-199">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="daa78-201">Ga naar **gebruikers en groepen** en klik op **alle gebruikers** om de lijst met gebruikers weer te geven.</span><span class="sxs-lookup"><span data-stu-id="daa78-201">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="daa78-203">Klik aan de bovenkant van het dialoogvenster **toevoegen** openen de **gebruiker** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="daa78-203">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="daa78-205">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="daa78-205">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="daa78-207">a.</span><span class="sxs-lookup"><span data-stu-id="daa78-207">a.</span></span> <span data-ttu-id="daa78-208">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="daa78-208">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="daa78-209">b.</span><span class="sxs-lookup"><span data-stu-id="daa78-209">b.</span></span> <span data-ttu-id="daa78-210">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="daa78-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="daa78-211">c.</span><span class="sxs-lookup"><span data-stu-id="daa78-211">c.</span></span> <span data-ttu-id="daa78-212">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="daa78-212">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="daa78-213">d.</span><span class="sxs-lookup"><span data-stu-id="daa78-213">d.</span></span> <span data-ttu-id="daa78-214">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="daa78-214">Click **Create**.</span></span> 

### <a name="creating-an-adobe-creative-cloud-test-user"></a><span data-ttu-id="daa78-215">Een testgebruiker Adobe Creative Cloud maken</span><span class="sxs-lookup"><span data-stu-id="daa78-215">Creating an Adobe Creative Cloud test user</span></span>

<span data-ttu-id="daa78-216">Om in te schakelen gebruikers van Azure AD aan te melden bij Adobe Creative Cloud, moeten ze worden ingericht in Adobe Creative Cloud.</span><span class="sxs-lookup"><span data-stu-id="daa78-216">In order to enable Azure AD users to log into Adobe Creative Cloud, they must be provisioned into Adobe Creative Cloud.</span></span>  
<span data-ttu-id="daa78-217">In het geval van Adobe Creative Cloud is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="daa78-217">In the case of Adobe Creative Cloud, provisioning is a manual task.</span></span>

<span data-ttu-id="daa78-218">**Voor het inrichten van een gebruikersaccount, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="daa78-218">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="daa78-219">Meld u aan bij uw bedrijf Adobe Creative Cloud site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="daa78-219">Log in to your Adobe Creative Cloud company site as an administrator.</span></span>

2. <span data-ttu-id="daa78-220">Klik op **mensen**.</span><span class="sxs-lookup"><span data-stu-id="daa78-220">Click **People**.</span></span>

    <span data-ttu-id="daa78-221">![Mensen](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_001.png "personen")</span><span class="sxs-lookup"><span data-stu-id="daa78-221">![People](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_001.png "People")</span></span>

3. <span data-ttu-id="daa78-222">Klik op **gebruiker uitnodigen**.</span><span class="sxs-lookup"><span data-stu-id="daa78-222">Click **Invite User**.</span></span>

    <span data-ttu-id="daa78-223">![Gebruikers uitnodigen](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_002.png "gebruikers uitnodigen")</span><span class="sxs-lookup"><span data-stu-id="daa78-223">![Invite Users](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_002.png "Invite Users")</span></span>

4. <span data-ttu-id="daa78-224">Op de **personen uitnodigen** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="daa78-224">On the **Invite People** dialog page, perform the following steps:</span></span>

    <span data-ttu-id="daa78-225">![Personen uitnodigen](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_003.png "personen uitnodigen")</span><span class="sxs-lookup"><span data-stu-id="daa78-225">![Invite People](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_003.png "Invite People")</span></span>

    <span data-ttu-id="daa78-226">a.</span><span class="sxs-lookup"><span data-stu-id="daa78-226">a.</span></span> <span data-ttu-id="daa78-227">In de **e** textbox, typ de e-mailadres van Britta Simon account.</span><span class="sxs-lookup"><span data-stu-id="daa78-227">In the **Email** textbox, type the email address of Britta Simon account.</span></span>
    
    <span data-ttu-id="daa78-228">b.</span><span class="sxs-lookup"><span data-stu-id="daa78-228">b.</span></span> <span data-ttu-id="daa78-229">Klik op **uitnodigen**.</span><span class="sxs-lookup"><span data-stu-id="daa78-229">Click **Invite**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="daa78-230">De accounthouder Azure Active Directory wordt een e-mailbericht ontvangen en Ga als volgt een koppeling om hun account te bevestigen voordat deze geactiveerd wordt.</span><span class="sxs-lookup"><span data-stu-id="daa78-230">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="daa78-231">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="daa78-231">Assigning the Azure AD test user</span></span>

<span data-ttu-id="daa78-232">In deze sectie maakt inschakelen u Britta Simon Azure eenmalige aanmelding gebruiken door haar toegang verlenen aan Adobe Creative Cloud.</span><span class="sxs-lookup"><span data-stu-id="daa78-232">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Adobe Creative Cloud.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="daa78-234">**Britta Simon om aan te wijzen Adobe Creative Cloud, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="daa78-234">**To assign Britta Simon to Adobe Creative Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="daa78-235">In de Azure-beheerportal, opent u de weergave toepassingen en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="daa78-235">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="daa78-237">Selecteer in de lijst met toepassingen **Adobe Creative Cloud**.</span><span class="sxs-lookup"><span data-stu-id="daa78-237">In the applications list, select **Adobe Creative Cloud**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_50.png) 

3. <span data-ttu-id="daa78-239">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="daa78-239">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="daa78-241">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="daa78-241">Click **Add** button.</span></span> <span data-ttu-id="daa78-242">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="daa78-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="daa78-244">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="daa78-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="daa78-245">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="daa78-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="daa78-246">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="daa78-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="daa78-247">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="daa78-247">Testing single sign-on</span></span>

<span data-ttu-id="daa78-248">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="daa78-248">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="daa78-249">Als u op de tegel Adobe Creative Cloud in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Adobe Creative Cloud.</span><span class="sxs-lookup"><span data-stu-id="daa78-249">When you click the Adobe Creative Cloud tile in the Access Panel, you should get automatically signed-on to your Adobe Creative Cloud application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="daa78-250">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="daa78-250">Additional resources</span></span>

* [<span data-ttu-id="daa78-251">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="daa78-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="daa78-252">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="daa78-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_203.png