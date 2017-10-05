---
title: 'Zelfstudie: Azure Active Directory-integratie met DocuSign | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en DocuSign.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a691288b-84c1-40fb-84bd-5b06878865f0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: 29c99fdf39d366df90abc070f7b836320935035c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-docusign"></a><span data-ttu-id="788d6-103">Zelfstudie: Azure Active Directory-integratie met DocuSign</span><span class="sxs-lookup"><span data-stu-id="788d6-103">Tutorial: Azure Active Directory integration with DocuSign</span></span>

<span data-ttu-id="788d6-104">In deze zelfstudie leert u hoe DocuSign integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="788d6-104">In this tutorial, you learn how to integrate DocuSign with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="788d6-105">DocuSign integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="788d6-105">Integrating DocuSign with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="788d6-106">U kunt beheren in Azure AD die toegang tot DocuSign heeft</span><span class="sxs-lookup"><span data-stu-id="788d6-106">You can control in Azure AD who has access to DocuSign</span></span>
- <span data-ttu-id="788d6-107">U kunt uw gebruikers automatisch ophalen aangemeld bij DocuSign (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="788d6-107">You can enable your users to automatically get signed-on to DocuSign (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="788d6-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="788d6-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="788d6-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="788d6-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="788d6-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="788d6-110">Prerequisites</span></span>

<span data-ttu-id="788d6-111">Voor het configureren van Azure AD-integratie met DocuSign, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="788d6-111">To configure Azure AD integration with DocuSign, you need the following items:</span></span>

- <span data-ttu-id="788d6-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="788d6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="788d6-113">Een DocuSign eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="788d6-113">A DocuSign single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="788d6-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="788d6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="788d6-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="788d6-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="788d6-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="788d6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="788d6-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="788d6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="788d6-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="788d6-118">Scenario description</span></span>
<span data-ttu-id="788d6-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="788d6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="788d6-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="788d6-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="788d6-121">DocuSign uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="788d6-121">Adding DocuSign from the gallery</span></span>
2. <span data-ttu-id="788d6-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="788d6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-docusign-from-the-gallery"></a><span data-ttu-id="788d6-123">DocuSign uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="788d6-123">Adding DocuSign from the gallery</span></span>
<span data-ttu-id="788d6-124">Voor het configureren van de integratie van DocuSign in Azure AD, moet u DocuSign uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="788d6-124">To configure the integration of DocuSign into Azure AD, you need to add DocuSign from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="788d6-125">**Als u wilt toevoegen DocuSign uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="788d6-125">**To add DocuSign from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="788d6-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="788d6-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="788d6-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="788d6-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="788d6-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="788d6-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="788d6-131">Klik op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="788d6-131">Click **New application** button on the top of the dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="788d6-133">Typ in het zoekvak **DocuSign**.</span><span class="sxs-lookup"><span data-stu-id="788d6-133">In the search box, type **DocuSign**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_search.png)

5. <span data-ttu-id="788d6-135">Selecteer in het deelvenster resultaten **DocuSign**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="788d6-135">In the results panel, select **DocuSign**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="788d6-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="788d6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="788d6-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met DocuSign op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="788d6-138">In this section, you configure and test Azure AD single sign-on with DocuSign based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="788d6-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in DocuSign is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="788d6-139">For single sign-on to work, Azure AD needs to know what the counterpart user in DocuSign is to a user in Azure AD.</span></span> <span data-ttu-id="788d6-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in DocuSign tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="788d6-140">In other words, a link relationship between an Azure AD user and the related user in DocuSign needs to be established.</span></span>

<span data-ttu-id="788d6-141">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in DocuSign.</span><span class="sxs-lookup"><span data-stu-id="788d6-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in DocuSign.</span></span>

<span data-ttu-id="788d6-142">Om te configureren en testen van Azure AD eenmalige aanmelding met DocuSign, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="788d6-142">To configure and test Azure AD single sign-on with DocuSign, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="788d6-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="788d6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="788d6-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="788d6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="788d6-145">**[Maken van een testgebruiker DocuSign](#creating-a-docusign-test-user)**  - DocuSign die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="788d6-145">**[Creating a DocuSign test user](#creating-a-docusign-test-user)** - to have a counterpart of Britta Simon in DocuSign that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="788d6-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="788d6-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="788d6-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="788d6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="788d6-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="788d6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="788d6-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing DocuSign configureren.</span><span class="sxs-lookup"><span data-stu-id="788d6-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your DocuSign application.</span></span>

<span data-ttu-id="788d6-150">**Voor het configureren van Azure AD eenmalige aanmelding met DocuSign, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="788d6-150">**To configure Azure AD single sign-on with DocuSign, perform the following steps:**</span></span>

1. <span data-ttu-id="788d6-151">In de Azure-portal op de **DocuSign** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="788d6-151">In the Azure portal, on the **DocuSign** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="788d6-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="788d6-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_samlbase.png)

3. <span data-ttu-id="788d6-155">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base 64)** en sla het bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="788d6-155">On the **SAML Signing Certificate** section, click **Certificate(Base 64)** and then save certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_certificate.png) 

4. <span data-ttu-id="788d6-157">Op de **DocuSign configuratie** sectie van de Azure-portal klikt u op **DocuSign configureren** om configureren aanmelding venster te openen.</span><span class="sxs-lookup"><span data-stu-id="788d6-157">On the **DocuSign Configuration** section of Azure portal, Click **Configure DocuSign** to open Configure sign-on window.</span></span> <span data-ttu-id="788d6-158">Kopieer de **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="788d6-158">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_configure.png)

5. <span data-ttu-id="788d6-160">In een ander browservenster, meld u aan bij uw **DocuSign-beheerportal** als beheerder.</span><span class="sxs-lookup"><span data-stu-id="788d6-160">In a different web browser window, login to your **DocuSign admin portal** as an administrator.</span></span>

6. <span data-ttu-id="788d6-161">Klik in het navigatiemenu aan de linkerkant op **domeinen**.</span><span class="sxs-lookup"><span data-stu-id="788d6-161">In the navigation menu on the left, click **Domains**.</span></span>
   
    ![Eenmalige aanmelding configureren][51]

7. <span data-ttu-id="788d6-163">Klik in het rechterdeelvenster op **Claim domein**.</span><span class="sxs-lookup"><span data-stu-id="788d6-163">On the right pane, click **Claim Domain**.</span></span>
   
    ![Eenmalige aanmelding configureren][52]

8. <span data-ttu-id="788d6-165">Op de **claimen van een domein** dialoogvenster in de **domeinnaam** textbox, typt u het domein van uw bedrijf en klik vervolgens op **Claim**.</span><span class="sxs-lookup"><span data-stu-id="788d6-165">On the **Claim a domain** dialog, in the **Domain Name** textbox, type your company domain, and then click **Claim**.</span></span> <span data-ttu-id="788d6-166">Zorg ervoor dat u het domein verifiëren en de status actief is.</span><span class="sxs-lookup"><span data-stu-id="788d6-166">Make sure that you verify the domain and the status is active.</span></span>
   
    ![Eenmalige aanmelding configureren][53]

9. <span data-ttu-id="788d6-168">Klik in het menu aan de linkerkant op **id-Providers**</span><span class="sxs-lookup"><span data-stu-id="788d6-168">In menu on the left side, click **Identity Providers**</span></span>  
   
    ![Eenmalige aanmelding configureren][54]
10. <span data-ttu-id="788d6-170">Klik in het rechterdeelvenster **identiteitsprovider toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="788d6-170">In the right pane, click **Add Identity Provider**.</span></span> 
   
    ![Eenmalige aanmelding configureren][55]

11. <span data-ttu-id="788d6-172">Op de **identiteit Providerinstellingen** pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="788d6-172">On the **Identity Provider Settings** page, perform the following steps:</span></span>
   
    ![Eenmalige aanmelding configureren][56]

    <span data-ttu-id="788d6-174">a.</span><span class="sxs-lookup"><span data-stu-id="788d6-174">a.</span></span> <span data-ttu-id="788d6-175">In de **naam** textbox, typ een unieke naam voor uw configuratie.</span><span class="sxs-lookup"><span data-stu-id="788d6-175">In the **Name** textbox, type a unique name for your configuration.</span></span> <span data-ttu-id="788d6-176">Gebruik geen spaties.</span><span class="sxs-lookup"><span data-stu-id="788d6-176">Do not use spaces.</span></span>

    <span data-ttu-id="788d6-177">b.</span><span class="sxs-lookup"><span data-stu-id="788d6-177">b.</span></span> <span data-ttu-id="788d6-178">Plakken **SAML entiteit-ID** in de **identiteit Provider verlener** textbox.</span><span class="sxs-lookup"><span data-stu-id="788d6-178">Paste **SAML Entity ID** into the **Identity Provider Issuer** textbox.</span></span>

    <span data-ttu-id="788d6-179">c.</span><span class="sxs-lookup"><span data-stu-id="788d6-179">c.</span></span> <span data-ttu-id="788d6-180">Plakken **SAML Single Sign-On Service-URL** in de **identiteit Provider aanmeldings-URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="788d6-180">Paste **SAML Single Sign-On Service URL** into the **Identity Provider Login URL** textbox.</span></span>

    <span data-ttu-id="788d6-181">d.</span><span class="sxs-lookup"><span data-stu-id="788d6-181">d.</span></span> <span data-ttu-id="788d6-182">Plakken **Sign-Out URL** in de **identiteit Provider afmelding URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="788d6-182">Paste **Sign-Out URL** into the **Identity Provider Logout URL** textbox.</span></span>

    <span data-ttu-id="788d6-183">e.</span><span class="sxs-lookup"><span data-stu-id="788d6-183">e.</span></span> <span data-ttu-id="788d6-184">Selecteer **AuthN aanvraag ondertekenen**.</span><span class="sxs-lookup"><span data-stu-id="788d6-184">Select **Sign AuthN Request**.</span></span>

    <span data-ttu-id="788d6-185">f.</span><span class="sxs-lookup"><span data-stu-id="788d6-185">f.</span></span> <span data-ttu-id="788d6-186">Als **aanvraag verzenden AuthN door**, selecteer **POST**.</span><span class="sxs-lookup"><span data-stu-id="788d6-186">As **Send AuthN request by**, select **POST**.</span></span>

    <span data-ttu-id="788d6-187">g.</span><span class="sxs-lookup"><span data-stu-id="788d6-187">g.</span></span> <span data-ttu-id="788d6-188">Als **afmelding Verzendaanvraag door**, selecteer **ophalen**.</span><span class="sxs-lookup"><span data-stu-id="788d6-188">As **Send logout request by**, select **GET**.</span></span>

12. <span data-ttu-id="788d6-189">In de **toewijzing van aangepast kenmerk** sectie, kiest u het veld dat u wilt koppelen aan Azure AD Claim.</span><span class="sxs-lookup"><span data-stu-id="788d6-189">In the **Custom Attribute Mapping** section, choose the field you want to map with Azure AD Claim.</span></span> <span data-ttu-id="788d6-190">In dit voorbeeld wordt de **emailaddress** claim is toegewezen door de waarde van **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="788d6-190">In this example, the **emailaddress** claim is mapped with the value of **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span> <span data-ttu-id="788d6-191">Het is de standaardnaam van de claim uit Azure AD voor e-mailbericht claim.</span><span class="sxs-lookup"><span data-stu-id="788d6-191">It is the default claim name from Azure AD for email claim.</span></span> 
   
    > [!NOTE]
    > <span data-ttu-id="788d6-192">Gebruik het juiste **gebruikers-id** toewijzen van de gebruiker van Azure AD DocuSign gebruiker toewijzen.</span><span class="sxs-lookup"><span data-stu-id="788d6-192">Use the appropriate **User identifier** to map the user from Azure AD to DocuSign user mapping.</span></span> <span data-ttu-id="788d6-193">Selecteer het juiste veld en voer de juiste waarde op basis van de instellingen van uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="788d6-193">Select the proper Field and enter the appropriate value based on your organization settings.</span></span>
          
    ![Eenmalige aanmelding configureren][57]

13. <span data-ttu-id="788d6-195">In de **Provider identiteitscertificaat** sectie, klikt u op **certificaat toevoegen**, en vervolgens het certificaat dat u hebt gedownload van Azure AD-portal uploaden.</span><span class="sxs-lookup"><span data-stu-id="788d6-195">In the **Identity Provider Certificate** section, click **Add Certificate**, and then upload the certificate you have downloaded from Azure AD portal.</span></span>   
   
    ![Eenmalige aanmelding configureren][58]

14. <span data-ttu-id="788d6-197">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="788d6-197">Click **Save**.</span></span>

15. <span data-ttu-id="788d6-198">In de **identiteitsproviders** sectie, klikt u op **acties**, en klik vervolgens op **eindpunten**.</span><span class="sxs-lookup"><span data-stu-id="788d6-198">In the **Identity Providers** section, click **Actions**, and then click **Endpoints**.</span></span>   
   
    ![Eenmalige aanmelding configureren][59]
 
16. <span data-ttu-id="788d6-200">In de **SAML 2.0-eindpunten weergeven** sectie op **DocuSign-beheerportal**, voer de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="788d6-200">In the **View SAML 2.0 Endpoints** section on **DocuSign admin portal**, perform the following steps:</span></span>
   
    ![Eenmalige aanmelding configureren][60]
   
    <span data-ttu-id="788d6-202">a.</span><span class="sxs-lookup"><span data-stu-id="788d6-202">a.</span></span> <span data-ttu-id="788d6-203">Kopiëren de **URL-Service Provider verlener**, en plak in het **id** textbox op **DocuSign domein en de URL's** sectie van de Azure portal, het patroon volgen: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/login/sp/<uniqueID>`.</span><span class="sxs-lookup"><span data-stu-id="788d6-203">Copy the **Service Provider Issuer URL**, and then paste into the **Identifier** textbox on **DocuSign Domain and URLs** section of the Azure portal following the pattern: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/login/sp/<uniqueID>`.</span></span>
   
    <span data-ttu-id="788d6-204">b.</span><span class="sxs-lookup"><span data-stu-id="788d6-204">b.</span></span> <span data-ttu-id="788d6-205">Kopiëren de **aanmeldings-URL voor Service Provider**, en plak in het **aanmelding op URL** textbox op **DocuSign domein en de URL's** sectie van de Azure portal, het patroon volgen: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/`.</span><span class="sxs-lookup"><span data-stu-id="788d6-205">Copy the **Service Provider Login URL**, and then paste into the **Sign On URL** textbox on **DocuSign Domain and URLs** section of the Azure portal following the pattern: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/`.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_url.png)
      
    <span data-ttu-id="788d6-207">c.</span><span class="sxs-lookup"><span data-stu-id="788d6-207">c.</span></span>  <span data-ttu-id="788d6-208">Klik op **sluiten**</span><span class="sxs-lookup"><span data-stu-id="788d6-208">Click **Close**</span></span>
    
17. <span data-ttu-id="788d6-209">Klik op de Azure-portal op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="788d6-209">On the Azure portal, click **Save**.</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-docusign-tutorial/tutorial_general_400.png)

> [!TIP]
> <span data-ttu-id="788d6-211">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="788d6-211">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="788d6-212">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="788d6-212">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="788d6-213">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="788d6-213">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="788d6-214">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="788d6-214">Creating an Azure AD test user</span></span>
<span data-ttu-id="788d6-215">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="788d6-215">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="788d6-217">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="788d6-217">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="788d6-218">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="788d6-218">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-docusign-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="788d6-220">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="788d6-220">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-docusign-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="788d6-222">Aan de bovenkant van het dialoogvenster, klikt u op **toevoegen** openen de **gebruiker** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="788d6-222">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-docusign-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="788d6-224">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="788d6-224">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-docusign-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="788d6-226">a.</span><span class="sxs-lookup"><span data-stu-id="788d6-226">a.</span></span> <span data-ttu-id="788d6-227">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="788d6-227">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="788d6-228">b.</span><span class="sxs-lookup"><span data-stu-id="788d6-228">b.</span></span> <span data-ttu-id="788d6-229">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="788d6-229">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="788d6-230">c.</span><span class="sxs-lookup"><span data-stu-id="788d6-230">c.</span></span> <span data-ttu-id="788d6-231">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="788d6-231">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="788d6-232">d.</span><span class="sxs-lookup"><span data-stu-id="788d6-232">d.</span></span> <span data-ttu-id="788d6-233">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="788d6-233">Click **Create**.</span></span>
 
### <a name="creating-a-docusign-test-user"></a><span data-ttu-id="788d6-234">Een testgebruiker DocuSign maken</span><span class="sxs-lookup"><span data-stu-id="788d6-234">Creating a DocuSign test user</span></span>

<span data-ttu-id="788d6-235">Toepassing ondersteunt **Just in time gebruikersaanvragen** en na verificatie gebruikers automatisch in de toepassing gemaakt worden.</span><span class="sxs-lookup"><span data-stu-id="788d6-235">Application supports **Just in time user provisioning** and after authentication users are created in the application automatically.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="788d6-236">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="788d6-236">Assigning the Azure AD test user</span></span>

<span data-ttu-id="788d6-237">In deze sectie schakelt u Britta Simon Azure eenmalige aanmelding gebruiken door haar toegang verlenen aan DocuSign.</span><span class="sxs-lookup"><span data-stu-id="788d6-237">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to DocuSign.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="788d6-239">**Britta Simon om aan te wijzen DocuSign, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="788d6-239">**To assign Britta Simon to DocuSign, perform the following steps:**</span></span>

1. <span data-ttu-id="788d6-240">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="788d6-240">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="788d6-242">Selecteer in de lijst met toepassingen **DocuSign**.</span><span class="sxs-lookup"><span data-stu-id="788d6-242">In the applications list, select **DocuSign**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_app.png) 

3. <span data-ttu-id="788d6-244">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="788d6-244">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="788d6-246">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="788d6-246">Click **Add** button.</span></span> <span data-ttu-id="788d6-247">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="788d6-247">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="788d6-249">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="788d6-249">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="788d6-250">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="788d6-250">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="788d6-251">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="788d6-251">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="788d6-252">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="788d6-252">Testing single sign-on</span></span>

<span data-ttu-id="788d6-253">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="788d6-253">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="788d6-254">Als u op de tegel DocuSign in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing DocuSign.</span><span class="sxs-lookup"><span data-stu-id="788d6-254">When you click the DocuSign tile in the Access Panel, you should get automatically signed-on to your DocuSign application.</span></span>
<span data-ttu-id="788d6-255">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="788d6-255">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="788d6-256">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="788d6-256">Additional resources</span></span>

* [<span data-ttu-id="788d6-257">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="788d6-257">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="788d6-258">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="788d6-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="788d6-259">Gebruikers inrichten configureren</span><span class="sxs-lookup"><span data-stu-id="788d6-259">Configure User Provisioning</span></span>](active-directory-saas-docusign-provisioning-tutorial.md)


<!--Image references-->

[1]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_04.png
[51]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_21.png
[52]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_22.png
[53]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_23.png
[54]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_19.png
[55]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_20.png
[56]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_24.png
[57]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_25.png
[58]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_26.png
[59]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_27.png
[60]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_28.png
[61]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_29.png
[100]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_203.png

