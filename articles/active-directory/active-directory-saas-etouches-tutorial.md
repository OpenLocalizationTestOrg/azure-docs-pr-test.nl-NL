---
title: 'Zelfstudie: Azure Active Directory-integratie met etouches | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en etouches.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 76cccaa8-859c-4c16-9d1d-8a6496fc7520
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 3cd9e9d6aae924369065ca492b1f6380c0ddc5fe
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-etouches"></a><span data-ttu-id="1aeed-103">Zelfstudie: Azure Active Directory-integratie met etouches</span><span class="sxs-lookup"><span data-stu-id="1aeed-103">Tutorial: Azure Active Directory integration with etouches</span></span>

<span data-ttu-id="1aeed-104">In deze zelfstudie leert u hoe etouches integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1aeed-104">In this tutorial, you learn how to integrate etouches with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1aeed-105">Etouches integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="1aeed-105">Integrating etouches with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1aeed-106">U kunt beheren in Azure AD die toegang tot etouches heeft</span><span class="sxs-lookup"><span data-stu-id="1aeed-106">You can control in Azure AD who has access to etouches</span></span>
- <span data-ttu-id="1aeed-107">U kunt uw gebruikers automatisch ophalen aangemeld bij etouches (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="1aeed-107">You can enable your users to automatically get signed-on to etouches (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1aeed-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="1aeed-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1aeed-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1aeed-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1aeed-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="1aeed-110">Prerequisites</span></span>

<span data-ttu-id="1aeed-111">Voor het configureren van Azure AD-integratie met etouches, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="1aeed-111">To configure Azure AD integration with etouches, you need the following items:</span></span>

- <span data-ttu-id="1aeed-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="1aeed-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1aeed-113">Een etouches eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="1aeed-113">An etouches single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1aeed-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="1aeed-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1aeed-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="1aeed-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1aeed-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="1aeed-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1aeed-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1aeed-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1aeed-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="1aeed-118">Scenario description</span></span>
<span data-ttu-id="1aeed-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="1aeed-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1aeed-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="1aeed-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1aeed-121">Etouches uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="1aeed-121">Adding etouches from the gallery</span></span>
2. <span data-ttu-id="1aeed-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="1aeed-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-etouches-from-the-gallery"></a><span data-ttu-id="1aeed-123">Etouches uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="1aeed-123">Adding etouches from the gallery</span></span>
<span data-ttu-id="1aeed-124">Voor het configureren van de integratie van etouches in Azure AD, moet u etouches uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="1aeed-124">To configure the integration of etouches into Azure AD, you need to add etouches from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1aeed-125">**Als u wilt toevoegen etouches uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="1aeed-125">**To add etouches from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1aeed-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="1aeed-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![De Azure Active Directory-knop][1]

2. <span data-ttu-id="1aeed-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="1aeed-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1aeed-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="1aeed-129">Then go to **All applications**.</span></span>

    ![De blade Enterprise-toepassingen][2]
    
3. <span data-ttu-id="1aeed-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1aeed-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![De knop Nieuw toepassing][3]

4. <span data-ttu-id="1aeed-133">Typ in het zoekvak **etouches**, selecteer **etouches** van resultaat deelvenster klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="1aeed-133">In the search box, type **etouches**, select **etouches** from result panel then click **Add** button to add the application.</span></span>

    ![etouches in de lijst met resultaten](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="1aeed-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="1aeed-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="1aeed-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met etouches op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="1aeed-136">In this section, you configure and test Azure AD single sign-on with etouches based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1aeed-137">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in etouches is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1aeed-137">For single sign-on to work, Azure AD needs to know what the counterpart user in etouches is to a user in Azure AD.</span></span> <span data-ttu-id="1aeed-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in etouches tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="1aeed-138">In other words, a link relationship between an Azure AD user and the related user in etouches needs to be established.</span></span>

<span data-ttu-id="1aeed-139">Wijs in etouches, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="1aeed-139">In etouches, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1aeed-140">Om te configureren en testen van Azure AD eenmalige aanmelding met etouches, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="1aeed-140">To configure and test Azure AD single sign-on with etouches, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1aeed-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1aeed-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1aeed-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1aeed-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1aeed-143">**[Maken van een testgebruiker etouches](#create-an-etouches-test-user)**  - hebben een equivalent van Britta Simon in etouches die is gekoppeld aan de Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="1aeed-143">**[Create an etouches test user](#create-an-etouches-test-user)** - to have a counterpart of Britta Simon in etouches that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1aeed-144">**[Toewijzen van de Azure AD-testgebruiker](#assign-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="1aeed-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1aeed-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="1aeed-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="1aeed-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="1aeed-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="1aeed-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing etouches configureren.</span><span class="sxs-lookup"><span data-stu-id="1aeed-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your etouches application.</span></span>

<span data-ttu-id="1aeed-148">**Voor het configureren van Azure AD eenmalige aanmelding met etouches, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="1aeed-148">**To configure Azure AD single sign-on with etouches, perform the following steps:**</span></span>

1. <span data-ttu-id="1aeed-149">In de Azure-portal op de **etouches** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="1aeed-149">In the Azure portal, on the **etouches** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="1aeed-151">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="1aeed-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_samlbase.png)

3. <span data-ttu-id="1aeed-153">Op de **etouches domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="1aeed-153">On the **etouches Domain and URLs** section, perform the following steps:</span></span>

    ![etouches domein en de URL's eenmalige aanmelding informatie](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_url.png)

    <span data-ttu-id="1aeed-155">a.</span><span class="sxs-lookup"><span data-stu-id="1aeed-155">a.</span></span> <span data-ttu-id="1aeed-156">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://www.eiseverywhere.com/saml/accounts/?sso&accountid=<ACCOUNTID>`</span><span class="sxs-lookup"><span data-stu-id="1aeed-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://www.eiseverywhere.com/saml/accounts/?sso&accountid=<ACCOUNTID>`</span></span>

    <span data-ttu-id="1aeed-157">b.</span><span class="sxs-lookup"><span data-stu-id="1aeed-157">b.</span></span> <span data-ttu-id="1aeed-158">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://www.eiseverywhere.com/<instance name>`</span><span class="sxs-lookup"><span data-stu-id="1aeed-158">In the **Identifier** textbox, type a URL using the following pattern: `https://www.eiseverywhere.com/<instance name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1aeed-159">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="1aeed-159">These values are not real.</span></span> <span data-ttu-id="1aeed-160">U bijwerken de waarde met de werkelijke aanmelding URL en de id, die verderop in de zelfstudie wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="1aeed-160">You update the value with the actual Sign on URL and Identifier, which is explained later in the tutorial.</span></span>
    > 

4. <span data-ttu-id="1aeed-161">de SAML-asserties verwacht etouches toepassing in een specifieke indeling.</span><span class="sxs-lookup"><span data-stu-id="1aeed-161">etouches application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="1aeed-162">Configureer de volgende claims voor deze toepassing.</span><span class="sxs-lookup"><span data-stu-id="1aeed-162">Configure the following claims for this application.</span></span> <span data-ttu-id="1aeed-163">U kunt de waarden van deze kenmerken van beheren de **gebruikerskenmerk** van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="1aeed-163">You can manage the values of these attributes from the **User Attribute** of the application.</span></span> <span data-ttu-id="1aeed-164">De volgende Schermafbeelding toont een voorbeeld voor deze.</span><span class="sxs-lookup"><span data-stu-id="1aeed-164">The following screenshot shows an example for this.</span></span> 

    ![Gebruikerskenmerk](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_attribute.png) 

5. <span data-ttu-id="1aeed-166">In de **gebruikerskenmerken** sectie op de **eenmalige aanmelding** dialoogvenster SAML-token kenmerk configureren zoals wordt weergegeven in de afbeelding en de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="1aeed-166">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="1aeed-167">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="1aeed-167">Attribute Name</span></span> | <span data-ttu-id="1aeed-168">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="1aeed-168">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="1aeed-169">E-mail</span><span class="sxs-lookup"><span data-stu-id="1aeed-169">Email</span></span> | <span data-ttu-id="1aeed-170">User.mail</span><span class="sxs-lookup"><span data-stu-id="1aeed-170">user.mail</span></span> |    
    
    <span data-ttu-id="1aeed-171">a.</span><span class="sxs-lookup"><span data-stu-id="1aeed-171">a.</span></span> <span data-ttu-id="1aeed-172">Klik op **toevoegen kenmerk** openen de **kenmerk toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1aeed-172">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Kenmerk toevoegen](./media/active-directory-saas-etouches-tutorial/tutorial_attribute_04.png)

    ![Dialoogvenster kenmerk toevoegen](./media/active-directory-saas-etouches-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="1aeed-175">b.</span><span class="sxs-lookup"><span data-stu-id="1aeed-175">b.</span></span> <span data-ttu-id="1aeed-176">In de **naam** textbox, typ de naam van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="1aeed-176">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="1aeed-177">c.</span><span class="sxs-lookup"><span data-stu-id="1aeed-177">c.</span></span> <span data-ttu-id="1aeed-178">Van de **waarde** typt u de waarde van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="1aeed-178">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="1aeed-179">d.</span><span class="sxs-lookup"><span data-stu-id="1aeed-179">d.</span></span> <span data-ttu-id="1aeed-180">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="1aeed-180">Click **Ok**.</span></span> 

6. <span data-ttu-id="1aeed-181">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="1aeed-181">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![De downloadkoppeling certificaat](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_certificate.png) 

7. <span data-ttu-id="1aeed-183">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="1aeed-183">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-etouches-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="1aeed-185">Als u eenmalige aanmelding voor uw toepassing is geconfigureerd, moet u de volgende stappen uitvoeren in de toepassing etouches:</span><span class="sxs-lookup"><span data-stu-id="1aeed-185">To get SSO configured for your application, perform the following steps in the etouches application:</span></span> 

    ![etouches configuratie](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_06.png) 

    <span data-ttu-id="1aeed-187">a.</span><span class="sxs-lookup"><span data-stu-id="1aeed-187">a.</span></span> <span data-ttu-id="1aeed-188">Meld u aan bij **etouches** toepassing met behulp van de Administrator-rechten.</span><span class="sxs-lookup"><span data-stu-id="1aeed-188">Login to **etouches** application using the Admin rights.</span></span>
   
    <span data-ttu-id="1aeed-189">b.</span><span class="sxs-lookup"><span data-stu-id="1aeed-189">b.</span></span> <span data-ttu-id="1aeed-190">Ga naar de **SAML** configuratie.</span><span class="sxs-lookup"><span data-stu-id="1aeed-190">Go to the **SAML** Configuration.</span></span>

    <span data-ttu-id="1aeed-191">c.</span><span class="sxs-lookup"><span data-stu-id="1aeed-191">c.</span></span> <span data-ttu-id="1aeed-192">In de **algemene instellingen** sectie, opent u het gedownloade certificaat vanuit Azure-portal in Kladblok, Kopieer de inhoud en plak deze in het tekstvak IDP-metagegevens.</span><span class="sxs-lookup"><span data-stu-id="1aeed-192">In the **General Settings** section, open your downloaded certificate from Azure portal in notepad, copy the content, and then paste it into the IDP metadata textbox.</span></span> 

    <span data-ttu-id="1aeed-193">d.</span><span class="sxs-lookup"><span data-stu-id="1aeed-193">d.</span></span> <span data-ttu-id="1aeed-194">Klik op de **opslaan & blijven** knop.</span><span class="sxs-lookup"><span data-stu-id="1aeed-194">Click on the **Save & Stay** button.</span></span>
  
    <span data-ttu-id="1aeed-195">e.</span><span class="sxs-lookup"><span data-stu-id="1aeed-195">e.</span></span> <span data-ttu-id="1aeed-196">Klik op de **updatemetagegevens** knop in de sectie SAML-metagegevens.</span><span class="sxs-lookup"><span data-stu-id="1aeed-196">Click on the **Update Metadata** button in the SAML Metadata section.</span></span> 

    <span data-ttu-id="1aeed-197">f.</span><span class="sxs-lookup"><span data-stu-id="1aeed-197">f.</span></span> <span data-ttu-id="1aeed-198">Hiermee opent u de pagina en SSO worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="1aeed-198">This opens the page and perform SSO.</span></span> <span data-ttu-id="1aeed-199">Zodra de eenmalige aanmelding werkt kunt u de gebruikersnaam instellen.</span><span class="sxs-lookup"><span data-stu-id="1aeed-199">Once the SSO is working then you can set up the username.</span></span>

    <span data-ttu-id="1aeed-200">g.</span><span class="sxs-lookup"><span data-stu-id="1aeed-200">g.</span></span> <span data-ttu-id="1aeed-201">Selecteer in het veld Username de **emailaddress** zoals weergegeven in de onderstaande afbeelding.</span><span class="sxs-lookup"><span data-stu-id="1aeed-201">In the Username field, select the **emailaddress** as shown in the image below.</span></span> 

    <span data-ttu-id="1aeed-202">h.</span><span class="sxs-lookup"><span data-stu-id="1aeed-202">h.</span></span> <span data-ttu-id="1aeed-203">Kopieer de **SP entiteit-ID** waarde en plak deze in de **id** textbox in **etouches domein en de URL's** sectie op Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="1aeed-203">Copy the **SP entity ID** value and paste it into the **Identifier**  textbox, which is in **etouches Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="1aeed-204">ik.</span><span class="sxs-lookup"><span data-stu-id="1aeed-204">i.</span></span> <span data-ttu-id="1aeed-205">Kopiëren de **SSO URL / ACS** waarde en plak deze in de **aanmelden URL** textbox in **etouches domein en de URL's** sectie op Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="1aeed-205">Copy the **SSO URL / ACS** value and paste it into the **Sign on URL** textbox, which is in **etouches Domain and URLs** section on Azure portal.</span></span>
   
> [!TIP]
> <span data-ttu-id="1aeed-206">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="1aeed-206">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1aeed-207">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="1aeed-207">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1aeed-208">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1aeed-208">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="1aeed-209">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="1aeed-209">Create an Azure AD test user</span></span>
<span data-ttu-id="1aeed-210">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="1aeed-210">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="1aeed-212">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="1aeed-212">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1aeed-213">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="1aeed-213">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![De Azure Active Directory-knop](./media/active-directory-saas-etouches-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1aeed-215">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="1aeed-215">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    !['Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-etouches-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1aeed-217">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1aeed-217">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![De knop toevoegen](./media/active-directory-saas-etouches-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1aeed-219">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="1aeed-219">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Het dialoogvenster gebruiker](./media/active-directory-saas-etouches-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1aeed-221">a.</span><span class="sxs-lookup"><span data-stu-id="1aeed-221">a.</span></span> <span data-ttu-id="1aeed-222">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1aeed-222">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1aeed-223">b.</span><span class="sxs-lookup"><span data-stu-id="1aeed-223">b.</span></span> <span data-ttu-id="1aeed-224">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1aeed-224">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1aeed-225">c.</span><span class="sxs-lookup"><span data-stu-id="1aeed-225">c.</span></span> <span data-ttu-id="1aeed-226">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="1aeed-226">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1aeed-227">d.</span><span class="sxs-lookup"><span data-stu-id="1aeed-227">d.</span></span> <span data-ttu-id="1aeed-228">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="1aeed-228">Click **Create**.</span></span>
 
### <a name="create-an-etouches-test-user"></a><span data-ttu-id="1aeed-229">Een testgebruiker etouches maken</span><span class="sxs-lookup"><span data-stu-id="1aeed-229">Create an etouches test user</span></span>

<span data-ttu-id="1aeed-230">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in etouches maken.</span><span class="sxs-lookup"><span data-stu-id="1aeed-230">In this section, you create a user called Britta Simon in etouches.</span></span> <span data-ttu-id="1aeed-231">Werken met [etouches Client ondersteuningsteam](https://www.etouches.com/event-software/support/customer-support/) de gebruikers van het platform etouches toevoegen.</span><span class="sxs-lookup"><span data-stu-id="1aeed-231">Work with [etouches Client support team](https://www.etouches.com/event-software/support/customer-support/) to add the users in the etouches platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="1aeed-232">De Azure AD-testgebruiker toewijzen</span><span class="sxs-lookup"><span data-stu-id="1aeed-232">Assign the Azure AD test user</span></span>

<span data-ttu-id="1aeed-233">In deze sectie schakelt u Britta Simon Azure eenmalige aanmelding gebruiken door het verlenen van toegang tot etouches.</span><span class="sxs-lookup"><span data-stu-id="1aeed-233">In this section, you enable Britta Simon to use Azure single sign-on by granting access to etouches.</span></span>

![Toewijzen van de gebruikersrol][200] 

<span data-ttu-id="1aeed-235">**Britta Simon om aan te wijzen etouches, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="1aeed-235">**To assign Britta Simon to etouches, perform the following steps:**</span></span>

1. <span data-ttu-id="1aeed-236">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="1aeed-236">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="1aeed-238">Selecteer in de lijst met toepassingen **etouches**.</span><span class="sxs-lookup"><span data-stu-id="1aeed-238">In the applications list, select **etouches**.</span></span>

    ![De koppeling etouches in de lijst met toepassingen](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_app.png) 

3. <span data-ttu-id="1aeed-240">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="1aeed-240">In the menu on the left, click **Users and groups**.</span></span>

    ![De koppeling 'Gebruikers en groepen'][202] 

4. <span data-ttu-id="1aeed-242">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="1aeed-242">Click **Add** button.</span></span> <span data-ttu-id="1aeed-243">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1aeed-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Het deelvenster toewijzing toevoegen][203]

5. <span data-ttu-id="1aeed-245">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="1aeed-245">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1aeed-246">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1aeed-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1aeed-247">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1aeed-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="1aeed-248">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="1aeed-248">Test single sign-on</span></span>


<span data-ttu-id="1aeed-249">Het doel van deze sectie is het testen van uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="1aeed-249">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1aeed-250">Als u op de tegel etouches in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing etouches.</span><span class="sxs-lookup"><span data-stu-id="1aeed-250">When you click the etouches tile in the Access Panel, you should get automatically signed-on to your etouches application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1aeed-251">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="1aeed-251">Additional resources</span></span>

* [<span data-ttu-id="1aeed-252">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1aeed-252">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1aeed-253">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1aeed-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_203.png

