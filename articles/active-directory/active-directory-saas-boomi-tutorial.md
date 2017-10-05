---
title: 'Zelfstudie: Azure Active Directory-integratie met Boomi | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Boomi.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8e05afa9-2eda-4975-a0cc-6d408065860f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 1121d22beddf73fd2109a4b410422f76dd37478e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-boomi"></a><span data-ttu-id="734d9-103">Zelfstudie: Azure Active Directory-integratie met Boomi</span><span class="sxs-lookup"><span data-stu-id="734d9-103">Tutorial: Azure Active Directory integration with Boomi</span></span>

<span data-ttu-id="734d9-104">In deze zelfstudie leert u hoe Boomi integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="734d9-104">In this tutorial, you learn how to integrate Boomi with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="734d9-105">Boomi integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="734d9-105">Integrating Boomi with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="734d9-106">U kunt beheren in Azure AD die toegang tot Boomi heeft</span><span class="sxs-lookup"><span data-stu-id="734d9-106">You can control in Azure AD who has access to Boomi</span></span>
- <span data-ttu-id="734d9-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Boomi (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="734d9-107">You can enable your users to automatically get signed-on to Boomi (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="734d9-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="734d9-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="734d9-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="734d9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="734d9-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="734d9-110">Prerequisites</span></span>

<span data-ttu-id="734d9-111">Voor het configureren van Azure AD-integratie met Boomi, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="734d9-111">To configure Azure AD integration with Boomi, you need the following items:</span></span>

- <span data-ttu-id="734d9-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="734d9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="734d9-113">Een Boomi eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="734d9-113">A Boomi single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="734d9-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="734d9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="734d9-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="734d9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="734d9-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="734d9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="734d9-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="734d9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="734d9-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="734d9-118">Scenario description</span></span>
<span data-ttu-id="734d9-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="734d9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="734d9-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="734d9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="734d9-121">Boomi uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="734d9-121">Adding Boomi from the gallery</span></span>
2. <span data-ttu-id="734d9-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="734d9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-boomi-from-the-gallery"></a><span data-ttu-id="734d9-123">Boomi uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="734d9-123">Adding Boomi from the gallery</span></span>
<span data-ttu-id="734d9-124">Voor het configureren van de integratie van Boomi in Azure AD, moet u Boomi uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="734d9-124">To configure the integration of Boomi into Azure AD, you need to add Boomi from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="734d9-125">**Als u wilt toevoegen Boomi uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="734d9-125">**To add Boomi from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="734d9-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="734d9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="734d9-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="734d9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="734d9-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="734d9-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="734d9-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="734d9-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="734d9-133">Typ in het zoekvak **Boomi**.</span><span class="sxs-lookup"><span data-stu-id="734d9-133">In the search box, type **Boomi**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_search.png)

5. <span data-ttu-id="734d9-135">Selecteer in het deelvenster resultaten **Boomi**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="734d9-135">In the results panel, select **Boomi**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="734d9-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="734d9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="734d9-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Boomi op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="734d9-138">In this section, you configure and test Azure AD single sign-on with Boomi based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="734d9-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Boomi is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="734d9-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Boomi is to a user in Azure AD.</span></span> <span data-ttu-id="734d9-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Boomi tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="734d9-140">In other words, a link relationship between an Azure AD user and the related user in Boomi needs to be established.</span></span>

<span data-ttu-id="734d9-141">Wijs in Boomi, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="734d9-141">In Boomi, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="734d9-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Boomi, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="734d9-142">To configure and test Azure AD single sign-on with Boomi, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="734d9-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="734d9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="734d9-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="734d9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="734d9-145">**[Maken van een testgebruiker Boomi](#creating-a-boomi-test-user)**  - Boomi die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="734d9-145">**[Creating a Boomi test user](#creating-a-boomi-test-user)** - to have a counterpart of Britta Simon in Boomi that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="734d9-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="734d9-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="734d9-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="734d9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="734d9-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="734d9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="734d9-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Boomi configureren.</span><span class="sxs-lookup"><span data-stu-id="734d9-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Boomi application.</span></span>

<span data-ttu-id="734d9-150">**Voor het configureren van Azure AD eenmalige aanmelding met Boomi, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="734d9-150">**To configure Azure AD single sign-on with Boomi, perform the following steps:**</span></span>

1. <span data-ttu-id="734d9-151">In de Azure-portal op de **Boomi** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="734d9-151">In the Azure portal, on the **Boomi** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="734d9-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="734d9-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_samlbase.png)

3. <span data-ttu-id="734d9-155">Op de **Boomi domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="734d9-155">On the **Boomi Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_url.png)

    <span data-ttu-id="734d9-157">a.</span><span class="sxs-lookup"><span data-stu-id="734d9-157">a.</span></span> <span data-ttu-id="734d9-158">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://platform.boomi.com/sso/<accountname>/saml`</span><span class="sxs-lookup"><span data-stu-id="734d9-158">In the **Identifier** textbox, type a URL using the following pattern: `https://platform.boomi.com/sso/<accountname>/saml`</span></span>

    <span data-ttu-id="734d9-159">b.</span><span class="sxs-lookup"><span data-stu-id="734d9-159">b.</span></span> <span data-ttu-id="734d9-160">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://platform.boomi.com/sso/<accountname>/saml`</span><span class="sxs-lookup"><span data-stu-id="734d9-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://platform.boomi.com/sso/<accountname>/saml`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="734d9-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="734d9-161">These values are not real.</span></span> <span data-ttu-id="734d9-162">Deze waarden bijwerken met de werkelijke id en de antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="734d9-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="734d9-163">Neem contact op met [Boomi ondersteuningsteam](https://boomi.com/company/contact/) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="734d9-163">Contact [Boomi support team](https://boomi.com/company/contact/) to get these values.</span></span>

4. <span data-ttu-id="734d9-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="734d9-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_certificate.png)

4. <span data-ttu-id="734d9-166">De SAML-asserties verwacht Boomi toepassing in een specifieke indeling.</span><span class="sxs-lookup"><span data-stu-id="734d9-166">Boomi application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="734d9-167">Configureer de volgende claims voor deze toepassing.</span><span class="sxs-lookup"><span data-stu-id="734d9-167">Please configure the following claims for this application.</span></span> <span data-ttu-id="734d9-168">U kunt beheren de waarden van deze kenmerken van de '**gebruikerskenmerken**' sectie op de pagina van de toepassing-integratie.</span><span class="sxs-lookup"><span data-stu-id="734d9-168">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="734d9-169">De volgende Schermafbeelding toont een voorbeeld voor deze.</span><span class="sxs-lookup"><span data-stu-id="734d9-169">The following screenshot shows an example for this.</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-boomi-tutorial/tutorial_attribute.png)

5. <span data-ttu-id="734d9-171">In de **gebruikerskenmerken** sectie op de **eenmalige aanmelding** dialoogvenster uitvoeren voor elke rij in de onderstaande tabel wordt weergegeven op de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="734d9-171">In the **User Attributes** section on the **Single sign-on** dialog, for each row shown in the table below, perform the following steps:</span></span>

    | <span data-ttu-id="734d9-172">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="734d9-172">Attribute Name</span></span> | <span data-ttu-id="734d9-173">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="734d9-173">Attribute Value</span></span> |
    | -------------- | --------------- |
    | <span data-ttu-id="734d9-174">FEDERATION_ID</span><span class="sxs-lookup"><span data-stu-id="734d9-174">FEDERATION_ID</span></span> | <span data-ttu-id="734d9-175">User.mail</span><span class="sxs-lookup"><span data-stu-id="734d9-175">user.mail</span></span> |
    
    <span data-ttu-id="734d9-176">a.</span><span class="sxs-lookup"><span data-stu-id="734d9-176">a.</span></span> <span data-ttu-id="734d9-177">Klik op **toevoegen kenmerk** openen de **kenmerk toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="734d9-177">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-boomi-tutorial/tutorial_attribute_04.png)
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-boomi-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="734d9-180">b.</span><span class="sxs-lookup"><span data-stu-id="734d9-180">b.</span></span> <span data-ttu-id="734d9-181">In de **naam** textbox, typ de naam van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="734d9-181">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="734d9-182">c.</span><span class="sxs-lookup"><span data-stu-id="734d9-182">c.</span></span> <span data-ttu-id="734d9-183">Van de **waarde** typt u de waarde van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="734d9-183">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="734d9-184">d.</span><span class="sxs-lookup"><span data-stu-id="734d9-184">d.</span></span> <span data-ttu-id="734d9-185">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="734d9-185">Click **Ok**.</span></span>

6. <span data-ttu-id="734d9-186">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="734d9-186">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-boomi-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="734d9-188">Op de **Boomi configuratie** sectie, klikt u op **configureren Boomi** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="734d9-188">On the **Boomi Configuration** section, click **Configure Boomi** to open **Configure sign-on** window.</span></span> <span data-ttu-id="734d9-189">Kopieer de **SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="734d9-189">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_configure.png) 

8. <span data-ttu-id="734d9-191">In een ander browservenster, meld u bij uw bedrijf Boomi site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="734d9-191">In a different web browser window, log into your Boomi company site as an administrator.</span></span> 

9. <span data-ttu-id="734d9-192">Navigeer naar **bedrijfsnaam** en Ga naar **instellen**.</span><span class="sxs-lookup"><span data-stu-id="734d9-192">Navigate to **Company Name** and go to **Set up**.</span></span>

10. <span data-ttu-id="734d9-193">Klik op de **SSO opties** tabblad en Voer onderstaande stappen te volgen.</span><span class="sxs-lookup"><span data-stu-id="734d9-193">Click the **SSO Options** tab and perform below steps.</span></span>

    ![App-zijde eenmalige aanmelding configureren](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_11.png)

    <span data-ttu-id="734d9-195">a.</span><span class="sxs-lookup"><span data-stu-id="734d9-195">a.</span></span> <span data-ttu-id="734d9-196">Controleer **inschakelen SAML Single Sign-On** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="734d9-196">Check **Enable SAML Single Sign-On** checkbox.</span></span>

    <span data-ttu-id="734d9-197">b.</span><span class="sxs-lookup"><span data-stu-id="734d9-197">b.</span></span> <span data-ttu-id="734d9-198">Klik op **importeren** voor het uploaden van het gedownloade certificaat uit Azure AD **Provider identiteitscertificaat**.</span><span class="sxs-lookup"><span data-stu-id="734d9-198">Click **Import** to upload the downloaded certificate from Azure AD to **Identity Provider Certificate**.</span></span>
    
    <span data-ttu-id="734d9-199">c.</span><span class="sxs-lookup"><span data-stu-id="734d9-199">c.</span></span> <span data-ttu-id="734d9-200">In de **identiteit Provider aanmeldings-URL** textbox, plaatst u de waarde van **SAML Single Sign-On Service-URL** van het venster voor configuratie van Azure AD-toepassing.</span><span class="sxs-lookup"><span data-stu-id="734d9-200">In the **Identity Provider Login URL** textbox, put the value of **SAML Single Sign-On Service URL** from Azure AD application configuration window.</span></span>

    <span data-ttu-id="734d9-201">d.</span><span class="sxs-lookup"><span data-stu-id="734d9-201">d.</span></span> <span data-ttu-id="734d9-202">Als **Federation Id locatie**, selecteer **Federation-Id wordt FEDERATION_ID kenmerk element** keuzerondje.</span><span class="sxs-lookup"><span data-stu-id="734d9-202">As **Federation Id Location**, select **Federation Id is in FEDERATION_ID Attribute element** radio button.</span></span> 

    <span data-ttu-id="734d9-203">e.</span><span class="sxs-lookup"><span data-stu-id="734d9-203">e.</span></span> <span data-ttu-id="734d9-204">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="734d9-204">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="734d9-205">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="734d9-205">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="734d9-206">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="734d9-206">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="734d9-207">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="734d9-207">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="734d9-208">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="734d9-208">Creating an Azure AD test user</span></span>
<span data-ttu-id="734d9-209">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="734d9-209">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="734d9-211">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="734d9-211">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="734d9-212">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="734d9-212">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-boomi-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="734d9-214">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="734d9-214">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-boomi-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="734d9-216">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="734d9-216">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-boomi-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="734d9-218">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="734d9-218">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-boomi-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="734d9-220">a.</span><span class="sxs-lookup"><span data-stu-id="734d9-220">a.</span></span> <span data-ttu-id="734d9-221">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="734d9-221">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="734d9-222">b.</span><span class="sxs-lookup"><span data-stu-id="734d9-222">b.</span></span> <span data-ttu-id="734d9-223">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="734d9-223">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="734d9-224">c.</span><span class="sxs-lookup"><span data-stu-id="734d9-224">c.</span></span> <span data-ttu-id="734d9-225">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="734d9-225">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="734d9-226">d.</span><span class="sxs-lookup"><span data-stu-id="734d9-226">d.</span></span> <span data-ttu-id="734d9-227">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="734d9-227">Click **Create**.</span></span>
 
### <a name="creating-a-boomi-test-user"></a><span data-ttu-id="734d9-228">Een testgebruiker Boomi maken</span><span class="sxs-lookup"><span data-stu-id="734d9-228">Creating a Boomi test user</span></span>

<span data-ttu-id="734d9-229">Om Azure AD-gebruikers zich aanmelden bij Boomi inschakelt, moeten ze worden ingericht in Boomi.</span><span class="sxs-lookup"><span data-stu-id="734d9-229">In order to enable Azure AD users to log in to Boomi, they must be provisioned into Boomi.</span></span> <span data-ttu-id="734d9-230">In het geval van Boomi is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="734d9-230">In the case of Boomi, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-account-perform-the-following-steps"></a><span data-ttu-id="734d9-231">Voor het inrichten van een gebruikersaccount, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="734d9-231">To provision a user account, perform the following steps:</span></span>

1. <span data-ttu-id="734d9-232">Meld u aan bij uw bedrijf Boomi site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="734d9-232">Log in to your Boomi company site as an administrator.</span></span>

2. <span data-ttu-id="734d9-233">Na het aanmelden, gaat u naar **Gebruikersbeheer** en Ga naar **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="734d9-233">After logging in, navigate to **User Management** and go to **Users**.</span></span>

    <span data-ttu-id="734d9-234">![Gebruikers](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_001.png "gebruikers")</span><span class="sxs-lookup"><span data-stu-id="734d9-234">![Users](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_001.png "Users")</span></span>

3. <span data-ttu-id="734d9-235">Klik op  **+**  pictogram en de **toevoegen/onderhouden gebruikersrollen** dialoogvenster wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="734d9-235">Click **+**  icon and the **Add/Maintain User Roles** dialog opens.</span></span>

    <span data-ttu-id="734d9-236">![Gebruikers](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_002.png "gebruikers")</span><span class="sxs-lookup"><span data-stu-id="734d9-236">![Users](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_002.png "Users")</span></span>

    <span data-ttu-id="734d9-237">![Gebruikers](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_003.png "gebruikers")</span><span class="sxs-lookup"><span data-stu-id="734d9-237">![Users](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_003.png "Users")</span></span>

    <span data-ttu-id="734d9-238">a.</span><span class="sxs-lookup"><span data-stu-id="734d9-238">a.</span></span> <span data-ttu-id="734d9-239">In de **e-mailadres gebruiker** textbox, typ het e-mailadres van gebruiker, zoals BrittaSimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="734d9-239">In the **User e-mail address** textbox, type the email of user like BrittaSimon@contoso.com.</span></span>
    
    <span data-ttu-id="734d9-240">b.</span><span class="sxs-lookup"><span data-stu-id="734d9-240">b.</span></span> <span data-ttu-id="734d9-241">In de **voornaam** textbox, de eerste naam van gebruiker zoals Britta.</span><span class="sxs-lookup"><span data-stu-id="734d9-241">In the **First name** textbox, type the First name of user like Britta.</span></span>

    <span data-ttu-id="734d9-242">c.</span><span class="sxs-lookup"><span data-stu-id="734d9-242">c.</span></span> <span data-ttu-id="734d9-243">In de **achternaam** textbox, typt u de achternaam van de gebruiker zoals Simon.</span><span class="sxs-lookup"><span data-stu-id="734d9-243">In the **Last name** textbox, type the Last name of user like Simon.</span></span>
    
    <span data-ttu-id="734d9-244">d.</span><span class="sxs-lookup"><span data-stu-id="734d9-244">d.</span></span> <span data-ttu-id="734d9-245">Voer de gebruiker **Federatie-ID**.</span><span class="sxs-lookup"><span data-stu-id="734d9-245">Enter the user's **Federation ID**.</span></span> <span data-ttu-id="734d9-246">Elke gebruiker moet een Federation-ID die een unieke identificatie van de gebruiker binnen het account hebben.</span><span class="sxs-lookup"><span data-stu-id="734d9-246">Each user must have a Federation ID that uniquely identifies the user within the account.</span></span>
    
    <span data-ttu-id="734d9-247">e.</span><span class="sxs-lookup"><span data-stu-id="734d9-247">e.</span></span> <span data-ttu-id="734d9-248">Wijs de **standaardgebruiker** rol aan de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="734d9-248">Assign the **Standard User** role to the user.</span></span> <span data-ttu-id="734d9-249">Wijs de rol beheerder niet toe omdat die hem normale lucht toegang als één aanmelding toegang wilt geven.</span><span class="sxs-lookup"><span data-stu-id="734d9-249">Do not assign the Administrator role because that would give him normal Atmosphere access as well as single sign-on access.</span></span>
    
    <span data-ttu-id="734d9-250">f.</span><span class="sxs-lookup"><span data-stu-id="734d9-250">f.</span></span> <span data-ttu-id="734d9-251">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="734d9-251">Click **OK**.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="734d9-252">De gebruiker ontvangt een e-mailmelding Welkom met een wachtwoord dat kan worden gebruikt voor aanmelding bij het account AtomSphere omdat het wachtwoord wordt beheerd via de id-provider niet.</span><span class="sxs-lookup"><span data-stu-id="734d9-252">The user will not receive a welcome notification email containing a password that can be used to log in to the AtomSphere account because his password is managed through the identity provider.</span></span> <span data-ttu-id="734d9-253">U kunt andere Boomi gebruiker account hulpmiddelen voor het maken of API's die is geleverd door Boomi aan inrichten AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="734d9-253">You may use any other Boomi user account creation tools or APIs provided by Boomi to provision AAD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="734d9-254">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="734d9-254">Assigning the Azure AD test user</span></span>

<span data-ttu-id="734d9-255">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Boomi.</span><span class="sxs-lookup"><span data-stu-id="734d9-255">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Boomi.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="734d9-257">**Britta Simon om aan te wijzen Boomi, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="734d9-257">**To assign Britta Simon to Boomi, perform the following steps:**</span></span>

1. <span data-ttu-id="734d9-258">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="734d9-258">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="734d9-260">Selecteer in de lijst met toepassingen **Boomi**.</span><span class="sxs-lookup"><span data-stu-id="734d9-260">In the applications list, select **Boomi**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_app.png) 

3. <span data-ttu-id="734d9-262">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="734d9-262">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="734d9-264">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="734d9-264">Click **Add** button.</span></span> <span data-ttu-id="734d9-265">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="734d9-265">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="734d9-267">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="734d9-267">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="734d9-268">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="734d9-268">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="734d9-269">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="734d9-269">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="734d9-270">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="734d9-270">Testing single sign-on</span></span>

<span data-ttu-id="734d9-271">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="734d9-271">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="734d9-272">Als u op de tegel Boomi in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Boomi.</span><span class="sxs-lookup"><span data-stu-id="734d9-272">When you click the Boomi tile in the Access Panel, you should get automatically signed-on to your Boomi application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="734d9-273">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="734d9-273">Additional resources</span></span>

* [<span data-ttu-id="734d9-274">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="734d9-274">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="734d9-275">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="734d9-275">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_203.png

