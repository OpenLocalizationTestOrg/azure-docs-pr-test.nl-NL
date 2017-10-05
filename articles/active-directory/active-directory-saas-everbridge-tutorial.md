---
title: 'Zelfstudie: Azure Active Directory-integratie met EverBridge | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en EverBridge.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 58d7cd22-98c0-4606-9ce5-8bdb22ee8b3e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: f5a97fc8df978dd55a73ae53516a82f884c14bec
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-everbridge"></a><span data-ttu-id="4ca94-103">Zelfstudie: Azure Active Directory-integratie met EverBridge</span><span class="sxs-lookup"><span data-stu-id="4ca94-103">Tutorial: Azure Active Directory integration with EverBridge</span></span>

<span data-ttu-id="4ca94-104">In deze zelfstudie leert u hoe EverBridge integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4ca94-104">In this tutorial, you learn how to integrate EverBridge with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4ca94-105">EverBridge integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="4ca94-105">Integrating EverBridge with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4ca94-106">U kunt beheren in Azure AD die toegang tot EverBridge heeft</span><span class="sxs-lookup"><span data-stu-id="4ca94-106">You can control in Azure AD who has access to EverBridge</span></span>
- <span data-ttu-id="4ca94-107">U kunt uw gebruikers automatisch ophalen aangemeld bij EverBridge (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="4ca94-107">You can enable your users to automatically get signed-on to EverBridge (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4ca94-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="4ca94-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="4ca94-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4ca94-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4ca94-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="4ca94-110">Prerequisites</span></span>

<span data-ttu-id="4ca94-111">Voor het configureren van Azure AD-integratie met EverBridge, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="4ca94-111">To configure Azure AD integration with EverBridge, you need the following items:</span></span>

- <span data-ttu-id="4ca94-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="4ca94-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4ca94-113">Een EverBridge eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="4ca94-113">An EverBridge single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4ca94-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="4ca94-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4ca94-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="4ca94-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4ca94-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="4ca94-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4ca94-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4ca94-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4ca94-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="4ca94-118">Scenario description</span></span>
<span data-ttu-id="4ca94-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="4ca94-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4ca94-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="4ca94-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4ca94-121">EverBridge uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="4ca94-121">Adding EverBridge from the gallery</span></span>
2. <span data-ttu-id="4ca94-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="4ca94-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-everbridge-from-the-gallery"></a><span data-ttu-id="4ca94-123">EverBridge uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="4ca94-123">Adding EverBridge from the gallery</span></span>
<span data-ttu-id="4ca94-124">Voor het configureren van de integratie van EverBridge in Azure AD, moet u EverBridge uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="4ca94-124">To configure the integration of EverBridge into Azure AD, you need to add EverBridge from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4ca94-125">**Als u wilt toevoegen EverBridge uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="4ca94-125">**To add EverBridge from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4ca94-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="4ca94-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4ca94-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="4ca94-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4ca94-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="4ca94-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="4ca94-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4ca94-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="4ca94-133">Typ in het zoekvak **EverBridge**.</span><span class="sxs-lookup"><span data-stu-id="4ca94-133">In the search box, type **EverBridge**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_search.png)

5. <span data-ttu-id="4ca94-135">Selecteer in het deelvenster resultaten **EverBridge**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="4ca94-135">In the results panel, select **EverBridge**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4ca94-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="4ca94-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4ca94-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met EverBridge op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="4ca94-138">In this section, you configure and test Azure AD single sign-on with EverBridge based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4ca94-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in EverBridge is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4ca94-139">For single sign-on to work, Azure AD needs to know what the counterpart user in EverBridge is to a user in Azure AD.</span></span> <span data-ttu-id="4ca94-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in EverBridge tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="4ca94-140">In other words, a link relationship between an Azure AD user and the related user in EverBridge needs to be established.</span></span>

<span data-ttu-id="4ca94-141">Wijs in EverBridge, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="4ca94-141">In EverBridge, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="4ca94-142">Om te configureren en testen van Azure AD eenmalige aanmelding met EverBridge, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="4ca94-142">To configure and test Azure AD single sign-on with EverBridge, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4ca94-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="4ca94-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4ca94-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4ca94-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4ca94-145">**[Maken van een testgebruiker EverBridge](#creating-an-everbridge-test-user)**  - EverBridge die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="4ca94-145">**[Creating an EverBridge test user](#creating-an-everbridge-test-user)** - to have a counterpart of Britta Simon in EverBridge that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="4ca94-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="4ca94-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4ca94-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="4ca94-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4ca94-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="4ca94-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4ca94-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing EverBridge configureren.</span><span class="sxs-lookup"><span data-stu-id="4ca94-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your EverBridge application.</span></span>

<span data-ttu-id="4ca94-150">**Voor het configureren van Azure AD eenmalige aanmelding met EverBridge, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="4ca94-150">**To configure Azure AD single sign-on with EverBridge, perform the following steps:**</span></span>

1. <span data-ttu-id="4ca94-151">In de Azure-portal op de **EverBridge** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="4ca94-151">In the Azure portal, on the **EverBridge** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="4ca94-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="4ca94-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_samlbase.png)

3. <span data-ttu-id="4ca94-155">Op de **EverBridge domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="4ca94-155">On the **EverBridge Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_url.png)

    <span data-ttu-id="4ca94-157">a.</span><span class="sxs-lookup"><span data-stu-id="4ca94-157">a.</span></span> <span data-ttu-id="4ca94-158">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://sso.everbridge.net/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="4ca94-158">In the **Identifier** textbox, type a URL using the following pattern: `https://sso.everbridge.net/<companyname>`</span></span>

    <span data-ttu-id="4ca94-159">b.</span><span class="sxs-lookup"><span data-stu-id="4ca94-159">b.</span></span> <span data-ttu-id="4ca94-160">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://manager.everbridge.net/saml/SSO/<companyname>/alias/defaultAlias`</span><span class="sxs-lookup"><span data-stu-id="4ca94-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://manager.everbridge.net/saml/SSO/<companyname>/alias/defaultAlias`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4ca94-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="4ca94-161">These values are not real.</span></span> <span data-ttu-id="4ca94-162">Deze waarden bijwerken met de werkelijke id en de antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="4ca94-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="4ca94-163">Neem contact op met [EverBridge ondersteuningsteam](mailto:support@everbridge.com) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="4ca94-163">Contact [EverBridge support team](mailto:support@everbridge.com) to get these values.</span></span>
 
4. <span data-ttu-id="4ca94-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="4ca94-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_certificate.png) 

5. <span data-ttu-id="4ca94-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="4ca94-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-everbridge-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4ca94-168">Op de **EverBridge configuratie** sectie, klikt u op **configureren EverBridge** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="4ca94-168">On the **EverBridge Configuration** section, click **Configure EverBridge** to open **Configure sign-on** window.</span></span> <span data-ttu-id="4ca94-169">Kopieer de **SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="4ca94-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_configure.png) 

6. <span data-ttu-id="4ca94-171">Als u eenmalige aanmelding voor uw toepassing is geconfigureerd, moet u eenmalige aanmelding voor uw tenant Everbridge als beheerder.</span><span class="sxs-lookup"><span data-stu-id="4ca94-171">To get SSO configured for your application, you need to sign-on to your Everbridge tenant as an administrator.</span></span>

7. <span data-ttu-id="4ca94-172">Klik in het menu bovenaan op de **instellingen** tabblad en selecteer **Single Sign-On** onder **beveiliging**.</span><span class="sxs-lookup"><span data-stu-id="4ca94-172">In the menu on the top, click the **Settings** tab and select **Single Sign-On** under **Security**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_002.png)
   
    <span data-ttu-id="4ca94-174">a.</span><span class="sxs-lookup"><span data-stu-id="4ca94-174">a.</span></span> <span data-ttu-id="4ca94-175">In de **naam** textbox, typ de naam van de id-Provider (bijvoorbeeld: naam van uw bedrijf).</span><span class="sxs-lookup"><span data-stu-id="4ca94-175">In the **Name** textbox, type the name of Identifier Provider (for example: your company name).</span></span>
   
    <span data-ttu-id="4ca94-176">b.</span><span class="sxs-lookup"><span data-stu-id="4ca94-176">b.</span></span> <span data-ttu-id="4ca94-177">In de **API-naam** textbox, typ de naam van de API.</span><span class="sxs-lookup"><span data-stu-id="4ca94-177">In the **API Name** textbox, type the name of API.</span></span>
   
    <span data-ttu-id="4ca94-178">c.</span><span class="sxs-lookup"><span data-stu-id="4ca94-178">c.</span></span> <span data-ttu-id="4ca94-179">Klik op **bestand kiezen** knop voor het uploaden van het bestand met metagegevens die u hebt gedownload van Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="4ca94-179">Click **Choose File** button to upload the metadata file which you downloaded from Azure portal.</span></span>
   
    <span data-ttu-id="4ca94-180">d.</span><span class="sxs-lookup"><span data-stu-id="4ca94-180">d.</span></span> <span data-ttu-id="4ca94-181">Selecteer in de locatie van de identiteit SAML **identiteit is in het element NameIdentifier van het onderwerp overzicht**.</span><span class="sxs-lookup"><span data-stu-id="4ca94-181">In the SAML Identity Location, select **Identity is in the NameIdentifier element of the Subject statement**.</span></span>
   
    <span data-ttu-id="4ca94-182">e.</span><span class="sxs-lookup"><span data-stu-id="4ca94-182">e.</span></span> <span data-ttu-id="4ca94-183">In de **identiteit Provider aanmeldings-URL** textbox, plak de waarde van SAML SSO-URL van Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4ca94-183">In the **Identity Provider Login URL** textbox, paste the value of SAML SSO URL from Azure AD.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_003.png)
   
    <span data-ttu-id="4ca94-185">f.</span><span class="sxs-lookup"><span data-stu-id="4ca94-185">f.</span></span> <span data-ttu-id="4ca94-186">Selecteer in de Service Provider geïnitieerd aanvragen Binding, **HTTP-omleiding**.</span><span class="sxs-lookup"><span data-stu-id="4ca94-186">In the Service Provider Initiated Request Binding, select **HTTP Redirect**.</span></span>

    <span data-ttu-id="4ca94-187">g.</span><span class="sxs-lookup"><span data-stu-id="4ca94-187">g.</span></span> <span data-ttu-id="4ca94-188">Klik op **opslaan**</span><span class="sxs-lookup"><span data-stu-id="4ca94-188">Click **Save**</span></span>

> [!TIP]
> <span data-ttu-id="4ca94-189">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="4ca94-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="4ca94-190">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="4ca94-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="4ca94-191">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4ca94-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4ca94-192">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="4ca94-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="4ca94-193">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="4ca94-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="4ca94-195">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="4ca94-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4ca94-196">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="4ca94-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-everbridge-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4ca94-198">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="4ca94-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-everbridge-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4ca94-200">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4ca94-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-everbridge-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4ca94-202">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="4ca94-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-everbridge-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4ca94-204">a.</span><span class="sxs-lookup"><span data-stu-id="4ca94-204">a.</span></span> <span data-ttu-id="4ca94-205">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4ca94-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4ca94-206">b.</span><span class="sxs-lookup"><span data-stu-id="4ca94-206">b.</span></span> <span data-ttu-id="4ca94-207">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4ca94-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4ca94-208">c.</span><span class="sxs-lookup"><span data-stu-id="4ca94-208">c.</span></span> <span data-ttu-id="4ca94-209">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="4ca94-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="4ca94-210">d.</span><span class="sxs-lookup"><span data-stu-id="4ca94-210">d.</span></span> <span data-ttu-id="4ca94-211">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="4ca94-211">Click **Create**.</span></span>
 
### <a name="creating-an-everbridge-test-user"></a><span data-ttu-id="4ca94-212">Een testgebruiker EverBridge maken</span><span class="sxs-lookup"><span data-stu-id="4ca94-212">Creating an EverBridge test user</span></span>

<span data-ttu-id="4ca94-213">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in Everbridge maken.</span><span class="sxs-lookup"><span data-stu-id="4ca94-213">In this section, you create a user called Britta Simon in Everbridge.</span></span> <span data-ttu-id="4ca94-214">Werken met [EverBridge ondersteuningsteam](mailto:support@everbridge.com) de gebruikers van het platform Everbridge toevoegen.</span><span class="sxs-lookup"><span data-stu-id="4ca94-214">Work with [EverBridge support team](mailto:support@everbridge.com) to add the users in the Everbridge platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="4ca94-215">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="4ca94-215">Assigning the Azure AD test user</span></span>

<span data-ttu-id="4ca94-216">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan EverBridge.</span><span class="sxs-lookup"><span data-stu-id="4ca94-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to EverBridge.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="4ca94-218">**Britta Simon om aan te wijzen EverBridge, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="4ca94-218">**To assign Britta Simon to EverBridge, perform the following steps:**</span></span>

1. <span data-ttu-id="4ca94-219">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="4ca94-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="4ca94-221">Selecteer in de lijst met toepassingen **EverBridge**.</span><span class="sxs-lookup"><span data-stu-id="4ca94-221">In the applications list, select **EverBridge**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_app.png) 

3. <span data-ttu-id="4ca94-223">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="4ca94-223">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="4ca94-225">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="4ca94-225">Click **Add** button.</span></span> <span data-ttu-id="4ca94-226">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4ca94-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="4ca94-228">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="4ca94-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="4ca94-229">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4ca94-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4ca94-230">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4ca94-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4ca94-231">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="4ca94-231">Testing single sign-on</span></span>

<span data-ttu-id="4ca94-232">Het doel van deze sectie is het testen van uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="4ca94-232">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="4ca94-233">Als u op de tegel Everbridge in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Everbridge.</span><span class="sxs-lookup"><span data-stu-id="4ca94-233">When you click the Everbridge tile in the Access Panel, you should get automatically signed-on to your Everbridge application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4ca94-234">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="4ca94-234">Additional resources</span></span>

* [<span data-ttu-id="4ca94-235">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4ca94-235">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4ca94-236">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4ca94-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_203.png

