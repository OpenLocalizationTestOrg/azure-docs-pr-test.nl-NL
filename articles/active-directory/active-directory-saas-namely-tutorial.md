---
title: 'Zelfstudie: Azure Active Directory-integratie met namelijk | Microsoft Docs'
description: Meer informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en namelijk.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9541d5c4-4c82-4b5b-b01a-6a3f75a2b7a1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 1d7e8fbcfc757853ab909bbb05522f3dc387715d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-namely"></a><span data-ttu-id="a0c78-103">Zelfstudie: Azure Active Directory-integratie met namelijk</span><span class="sxs-lookup"><span data-stu-id="a0c78-103">Tutorial: Azure Active Directory integration with Namely</span></span>

<span data-ttu-id="a0c78-104">In deze zelfstudie leert u hoe namelijk integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a0c78-104">In this tutorial, you learn how to integrate Namely with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a0c78-105">Namelijk integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="a0c78-105">Integrating Namely with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a0c78-106">U kunt beheren in Azure AD die toegang heeft tot namelijk</span><span class="sxs-lookup"><span data-stu-id="a0c78-106">You can control in Azure AD who has access to Namely</span></span>
- <span data-ttu-id="a0c78-107">U kunt uw gebruikers automatisch aangemeld bij namelijk inschakelen (Single Sign-On) met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="a0c78-107">You can enable your users to automatically get signed-on to Namely (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a0c78-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="a0c78-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a0c78-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a0c78-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a0c78-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a0c78-110">Prerequisites</span></span>

<span data-ttu-id="a0c78-111">Voor het configureren van Azure AD-integratie met name als u de volgende items nodig:</span><span class="sxs-lookup"><span data-stu-id="a0c78-111">To configure Azure AD integration with Namely, you need the following items:</span></span>

- <span data-ttu-id="a0c78-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="a0c78-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a0c78-113">Een namelijk eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="a0c78-113">A Namely single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a0c78-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="a0c78-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a0c78-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="a0c78-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a0c78-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="a0c78-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a0c78-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a0c78-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a0c78-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="a0c78-118">Scenario description</span></span>
<span data-ttu-id="a0c78-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="a0c78-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a0c78-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="a0c78-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a0c78-121">Namelijk uit de galerie toe te voegen</span><span class="sxs-lookup"><span data-stu-id="a0c78-121">Adding Namely from the gallery</span></span>
2. <span data-ttu-id="a0c78-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="a0c78-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-namely-from-the-gallery"></a><span data-ttu-id="a0c78-123">Namelijk uit de galerie toe te voegen</span><span class="sxs-lookup"><span data-stu-id="a0c78-123">Adding Namely from the gallery</span></span>
<span data-ttu-id="a0c78-124">Voor het configureren van de integratie van namelijk in Azure AD, moet u namelijk uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="a0c78-124">To configure the integration of Namely into Azure AD, you need to add Namely from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a0c78-125">**Als u wilt weten uit de galerie toevoegt, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="a0c78-125">**To add Namely from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a0c78-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="a0c78-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a0c78-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a0c78-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a0c78-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a0c78-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="a0c78-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a0c78-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="a0c78-133">Typ in het zoekvak **namelijk**.</span><span class="sxs-lookup"><span data-stu-id="a0c78-133">In the search box, type **Namely**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-namely-tutorial/tutorial_namely_search.png)

5. <span data-ttu-id="a0c78-135">Selecteer in het deelvenster resultaten **namelijk**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="a0c78-135">In the results panel, select **Namely**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-namely-tutorial/tutorial_namely_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a0c78-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="a0c78-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a0c78-138">In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met namelijk op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="a0c78-138">In this section, you configure and test Azure AD single sign-on with Namely based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a0c78-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in namelijk is aan een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a0c78-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Namely is to a user in Azure AD.</span></span> <span data-ttu-id="a0c78-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in namelijk tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="a0c78-140">In other words, a link relationship between an Azure AD user and the related user in Namely needs to be established.</span></span>

<span data-ttu-id="a0c78-141">Dat wil zeggen Wijs in de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="a0c78-141">In Namely, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a0c78-142">Als u wilt configureren en testen van Azure AD moet eenmalige aanmelding met namelijk, u voltooien van de volgende elementen:</span><span class="sxs-lookup"><span data-stu-id="a0c78-142">To configure and test Azure AD single sign-on with Namely, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a0c78-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a0c78-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a0c78-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a0c78-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a0c78-145">**[Maken van een namelijk testgebruiker](#creating-a-namely-test-user)**  - hebben een equivalent van Britta Simon in namelijk dat is gekoppeld aan de Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="a0c78-145">**[Creating a Namely test user](#creating-a-namely-test-user)** - to have a counterpart of Britta Simon in Namely that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a0c78-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="a0c78-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a0c78-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="a0c78-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a0c78-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="a0c78-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a0c78-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing namelijk configureren.</span><span class="sxs-lookup"><span data-stu-id="a0c78-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Namely application.</span></span>

<span data-ttu-id="a0c78-150">**Voor het configureren van Azure AD eenmalige aanmelding met name de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="a0c78-150">**To configure Azure AD single sign-on with Namely, perform the following steps:**</span></span>

1. <span data-ttu-id="a0c78-151">In de Azure-portal op de **namelijk** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="a0c78-151">In the Azure portal, on the **Namely** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="a0c78-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="a0c78-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-namely-tutorial/tutorial_namely_samlbase.png)

3. <span data-ttu-id="a0c78-155">Op de **namelijk domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="a0c78-155">On the **Namely Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-namely-tutorial/tutorial_namely_url.png)

    <span data-ttu-id="a0c78-157">a.</span><span class="sxs-lookup"><span data-stu-id="a0c78-157">a.</span></span> <span data-ttu-id="a0c78-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<subdomain>.namely.com`</span><span class="sxs-lookup"><span data-stu-id="a0c78-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.namely.com`</span></span>

    <span data-ttu-id="a0c78-159">b.</span><span class="sxs-lookup"><span data-stu-id="a0c78-159">b.</span></span> <span data-ttu-id="a0c78-160">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<subdomain>.namely.com/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="a0c78-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.namely.com/saml/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a0c78-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="a0c78-161">These values are not real.</span></span> <span data-ttu-id="a0c78-162">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="a0c78-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="a0c78-163">Neem contact op met [namelijk Client ondersteuningsteam](https://www.namely.com/contact/) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="a0c78-163">Contact [Namely Client support team](https://www.namely.com/contact/) to get these values.</span></span> 
 
4. <span data-ttu-id="a0c78-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="a0c78-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-namely-tutorial/tutorial_namely_certificate.png) 

5. <span data-ttu-id="a0c78-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="a0c78-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-namely-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a0c78-168">Op de **namelijk configuratie** sectie, klikt u op **namelijk configureren** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="a0c78-168">On the **Namely Configuration** section, click **Configure Namely** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a0c78-169">Kopieer de **SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="a0c78-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-namely-tutorial/tutorial_namely_configure.png) 

7. <span data-ttu-id="a0c78-171">In een ander browservenster geopend Meld u aan bij uw namelijk bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="a0c78-171">In another browser window, sign on to your Namely company site as an administrator.</span></span>

8. <span data-ttu-id="a0c78-172">Klik in de werkbalk bovenaan op **bedrijf**.</span><span class="sxs-lookup"><span data-stu-id="a0c78-172">In the toolbar on the top, click **Company**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-namely-tutorial/tutorial_namely_06.png) 

9. <span data-ttu-id="a0c78-174">Klik op het tabblad **Settings**.</span><span class="sxs-lookup"><span data-stu-id="a0c78-174">Click the **Settings** tab.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-namely-tutorial/tutorial_namely_07.png) 

10. <span data-ttu-id="a0c78-176">Klik op **SAML**.</span><span class="sxs-lookup"><span data-stu-id="a0c78-176">Click **SAML**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-namely-tutorial/tutorial_namely_08.png) 

11. <span data-ttu-id="a0c78-178">Op de **SAML instellingen** pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="a0c78-178">On the **SAML Settings** page, perform the following steps:</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-namely-tutorial/tutorial_namely_09.png)
 
    <span data-ttu-id="a0c78-180">a.</span><span class="sxs-lookup"><span data-stu-id="a0c78-180">a.</span></span> <span data-ttu-id="a0c78-181">Klik op **SAML inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="a0c78-181">Click **Enable SAML**.</span></span> 

    <span data-ttu-id="a0c78-182">b.</span><span class="sxs-lookup"><span data-stu-id="a0c78-182">b.</span></span> <span data-ttu-id="a0c78-183">In de **identiteit provider SSO url** textbox, plak de waarde van **SAML Single Sign-On Service-URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="a0c78-183">In the **Identity provider SSO url** textbox,  paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="a0c78-184">c.</span><span class="sxs-lookup"><span data-stu-id="a0c78-184">c.</span></span> <span data-ttu-id="a0c78-185">Open uw gedownloade certificaat in Kladblok, Kopieer de inhoud en plakt u deze in de **provider identiteitscertificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="a0c78-185">Open your downloaded certificate in Notepad, copy the content, and then paste it into the **Identity provider certificate** textbox.</span></span>
     
    <span data-ttu-id="a0c78-186">d.</span><span class="sxs-lookup"><span data-stu-id="a0c78-186">d.</span></span> <span data-ttu-id="a0c78-187">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="a0c78-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="a0c78-188">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="a0c78-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a0c78-189">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="a0c78-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a0c78-190">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a0c78-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a0c78-191">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="a0c78-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="a0c78-192">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="a0c78-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="a0c78-194">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="a0c78-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a0c78-195">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="a0c78-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-namely-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a0c78-197">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="a0c78-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-namely-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a0c78-199">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a0c78-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-namely-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a0c78-201">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="a0c78-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-namely-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a0c78-203">a.</span><span class="sxs-lookup"><span data-stu-id="a0c78-203">a.</span></span> <span data-ttu-id="a0c78-204">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a0c78-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a0c78-205">b.</span><span class="sxs-lookup"><span data-stu-id="a0c78-205">b.</span></span> <span data-ttu-id="a0c78-206">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a0c78-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a0c78-207">c.</span><span class="sxs-lookup"><span data-stu-id="a0c78-207">c.</span></span> <span data-ttu-id="a0c78-208">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="a0c78-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a0c78-209">d.</span><span class="sxs-lookup"><span data-stu-id="a0c78-209">d.</span></span> <span data-ttu-id="a0c78-210">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="a0c78-210">Click **Create**.</span></span>
 
### <a name="creating-a-namely-test-user"></a><span data-ttu-id="a0c78-211">Maken van een namelijk testgebruiker</span><span class="sxs-lookup"><span data-stu-id="a0c78-211">Creating a Namely test user</span></span>

<span data-ttu-id="a0c78-212">Het doel van deze sectie is het maken van een gebruiker Britta Simon namelijk aangeroepen in.</span><span class="sxs-lookup"><span data-stu-id="a0c78-212">The objective of this section is to create a user called Britta Simon in Namely.</span></span>

<span data-ttu-id="a0c78-213">**Voor het maken van een gebruiker Britta Simon namelijk aangeroepen in de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="a0c78-213">**To create a user called Britta Simon in Namely, perform the following steps:**</span></span>

1. <span data-ttu-id="a0c78-214">Aanmelding bij uw namelijk bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="a0c78-214">Sign-on to your Namely company site as an administrator.</span></span>

2. <span data-ttu-id="a0c78-215">Klik in de werkbalk bovenaan op **mensen**.</span><span class="sxs-lookup"><span data-stu-id="a0c78-215">In the toolbar on the top, click **People**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-namely-tutorial/tutorial_namely_10.png) 

3. <span data-ttu-id="a0c78-217">Klik op de **Directory** tabblad.</span><span class="sxs-lookup"><span data-stu-id="a0c78-217">Click the **Directory** tab.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-namely-tutorial/tutorial_namely_11.png) 

4. <span data-ttu-id="a0c78-219">Klik op **toevoegen van nieuwe persoon**.</span><span class="sxs-lookup"><span data-stu-id="a0c78-219">Click **Add New Person**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-namely-tutorial/tutorial_namely_12.png)

5. <span data-ttu-id="a0c78-221">Op de **nieuwe persoon toevoegen** dialoogvenster de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="a0c78-221">On the **Add New Person** dialog, perform the following steps:</span></span>

    <span data-ttu-id="a0c78-222">a.</span><span class="sxs-lookup"><span data-stu-id="a0c78-222">a.</span></span> <span data-ttu-id="a0c78-223">In de **voornaam** textbox type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="a0c78-223">In the **First name** textbox, type **Britta**.</span></span>

    <span data-ttu-id="a0c78-224">b.</span><span class="sxs-lookup"><span data-stu-id="a0c78-224">b.</span></span> <span data-ttu-id="a0c78-225">In de **achternaam** textbox type **Simon**.</span><span class="sxs-lookup"><span data-stu-id="a0c78-225">In the **Last name** textbox, type **Simon**.</span></span>

    <span data-ttu-id="a0c78-226">c.</span><span class="sxs-lookup"><span data-stu-id="a0c78-226">c.</span></span> <span data-ttu-id="a0c78-227">In de **e** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a0c78-227">In the **Email** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a0c78-228">d.</span><span class="sxs-lookup"><span data-stu-id="a0c78-228">d.</span></span> <span data-ttu-id="a0c78-229">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="a0c78-229">Click **Save**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a0c78-230">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="a0c78-230">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a0c78-231">In deze sectie maakt inschakelen u Britta Simon Azure eenmalige aanmelding gebruiken door het verlenen van toegang tot namelijk.</span><span class="sxs-lookup"><span data-stu-id="a0c78-231">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Namely.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="a0c78-233">**Toewijzen Britta Simon wil zeggen, de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="a0c78-233">**To assign Britta Simon to Namely, perform the following steps:**</span></span>

1. <span data-ttu-id="a0c78-234">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a0c78-234">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="a0c78-236">Selecteer in de lijst met toepassingen **namelijk**.</span><span class="sxs-lookup"><span data-stu-id="a0c78-236">In the applications list, select **Namely**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-namely-tutorial/tutorial_namely_app.png) 

3. <span data-ttu-id="a0c78-238">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="a0c78-238">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="a0c78-240">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="a0c78-240">Click **Add** button.</span></span> <span data-ttu-id="a0c78-241">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a0c78-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="a0c78-243">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="a0c78-243">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a0c78-244">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a0c78-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a0c78-245">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a0c78-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a0c78-246">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="a0c78-246">Testing single sign-on</span></span>

<span data-ttu-id="a0c78-247">Het doel van deze sectie is het testen van uw Azure AD SSO-configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="a0c78-247">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="a0c78-248">Wanneer u klikt op de namelijk-tegel in het toegangsvenster, u moet ophalen automatisch aangemeld bij uw toepassing namelijk</span><span class="sxs-lookup"><span data-stu-id="a0c78-248">When you click the Namely tile in the Access Panel, you should get automatically signed-on to your Namely application</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a0c78-249">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="a0c78-249">Additional resources</span></span>

* [<span data-ttu-id="a0c78-250">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a0c78-250">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a0c78-251">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a0c78-251">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-namely-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-namely-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-namely-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-namely-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-namely-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-namely-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-namely-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-namely-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-namely-tutorial/tutorial_general_203.png

