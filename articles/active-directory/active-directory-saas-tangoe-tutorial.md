---
title: 'Zelfstudie: Azure Active Directory-integratie met Tangoe opdracht Premium Mobile | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Tangoe opdracht Premium Mobile.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 2b0b544c-9c2c-49cd-862b-ec2ee9330126
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 595541e7248a7486e58123927389c552af0e50f7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tangoe-command-premium-mobile"></a><span data-ttu-id="c099d-103">Zelfstudie: Azure Active Directory-integratie met Tangoe opdracht Premium Mobile</span><span class="sxs-lookup"><span data-stu-id="c099d-103">Tutorial: Azure Active Directory integration with Tangoe Command Premium Mobile</span></span>

<span data-ttu-id="c099d-104">In deze zelfstudie leert u hoe Tangoe opdracht Premium Mobile integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c099d-104">In this tutorial, you learn how to integrate Tangoe Command Premium Mobile with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c099d-105">Tangoe opdracht Premium Mobile integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="c099d-105">Integrating Tangoe Command Premium Mobile with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c099d-106">U kunt beheren in Azure AD die toegang tot Tangoe opdracht Premium Mobile heeft</span><span class="sxs-lookup"><span data-stu-id="c099d-106">You can control in Azure AD who has access to Tangoe Command Premium Mobile</span></span>
- <span data-ttu-id="c099d-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Tangoe opdracht Premium Mobile (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="c099d-107">You can enable your users to automatically get signed-on to Tangoe Command Premium Mobile (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c099d-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="c099d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c099d-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c099d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c099d-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="c099d-110">Prerequisites</span></span>

<span data-ttu-id="c099d-111">Voor het configureren van Azure AD-integratie met Tangoe opdracht Premium Mobile, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="c099d-111">To configure Azure AD integration with Tangoe Command Premium Mobile, you need the following items:</span></span>

- <span data-ttu-id="c099d-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="c099d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c099d-113">Een Tangoe opdracht Premium Mobile eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="c099d-113">A Tangoe Command Premium Mobile single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c099d-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="c099d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c099d-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="c099d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c099d-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="c099d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c099d-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c099d-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c099d-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="c099d-118">Scenario description</span></span>
<span data-ttu-id="c099d-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="c099d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c099d-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="c099d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c099d-121">Tangoe opdracht Premium Mobile uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="c099d-121">Add Tangoe Command Premium Mobile from the gallery</span></span>
2. <span data-ttu-id="c099d-122">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="c099d-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-tangoe-command-premium-mobile-from-the-gallery"></a><span data-ttu-id="c099d-123">Tangoe opdracht Premium Mobile uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="c099d-123">Add Tangoe Command Premium Mobile from the gallery</span></span>
<span data-ttu-id="c099d-124">Voor het configureren van de integratie van Tangoe opdracht Premium Mobile in Azure AD, moet u Tangoe opdracht Premium Mobile uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="c099d-124">To configure the integration of Tangoe Command Premium Mobile into Azure AD, you need to add Tangoe Command Premium Mobile from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c099d-125">**Als u wilt toevoegen Tangoe opdracht Premium Mobile uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="c099d-125">**To add Tangoe Command Premium Mobile from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c099d-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="c099d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c099d-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c099d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c099d-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c099d-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="c099d-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c099d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="c099d-133">Typ in het zoekvak **Tangoe opdracht Premium Mobile**, selecteer **Tangoe opdracht Premium Mobile** van resultaat deelvenster klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="c099d-133">In the search box, type **Tangoe Command Premium Mobile**, select **Tangoe Command Premium Mobile** from result panel then click **Add** button to add the application.</span></span>

    ![<span data-ttu-id="c099d-134">Tangoe opdracht Premium Mobile uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="c099d-134">Add Tangoe Command Premium Mobile from gallery</span></span> ](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="c099d-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="c099d-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="c099d-136">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Tangoe opdracht Premium Mobile op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="c099d-136">In this section, you configure and test Azure AD single sign-on with Tangoe Command Premium Mobile based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c099d-137">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Tangoe opdracht Premium Mobile is aan een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c099d-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Tangoe Command Premium Mobile is to a user in Azure AD.</span></span> <span data-ttu-id="c099d-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Tangoe opdracht Premium Mobile tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="c099d-138">In other words, a link relationship between an Azure AD user and the related user in Tangoe Command Premium Mobile needs to be established.</span></span>

<span data-ttu-id="c099d-139">Wijs in Tangoe opdracht Premium Mobile, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="c099d-139">In Tangoe Command Premium Mobile, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c099d-140">Om te configureren en testen van Azure AD eenmalige aanmelding met Tangoe opdracht Premium Mobile, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="c099d-140">To configure and test Azure AD single sign-on with Tangoe Command Premium Mobile, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c099d-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c099d-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c099d-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c099d-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c099d-143">**[Maak een testgebruiker Tangoe opdracht Premium Mobile](#create-a-tangoe-command-premium-mobile-test-user)**  - Tangoe opdracht Premium Mobile die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="c099d-143">**[Create a Tangoe Command Premium Mobile test user](#create-a-tangoe-command-premium-mobile-test-user)** - to have a counterpart of Britta Simon in Tangoe Command Premium Mobile that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c099d-144">**[Toewijzen van de Azure AD-testgebruiker](#assign-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="c099d-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c099d-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="c099d-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="c099d-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="c099d-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="c099d-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw toepassing Tangoe opdracht Premium Mobile.</span><span class="sxs-lookup"><span data-stu-id="c099d-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Tangoe Command Premium Mobile application.</span></span>

<span data-ttu-id="c099d-148">**Voor het configureren van Azure AD eenmalige aanmelding met Tangoe opdracht Premium Mobile, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="c099d-148">**To configure Azure AD single sign-on with Tangoe Command Premium Mobile, perform the following steps:**</span></span>

1. <span data-ttu-id="c099d-149">In de Azure-portal op de **Tangoe opdracht Premium Mobile** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="c099d-149">In the Azure portal, on the **Tangoe Command Premium Mobile** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="c099d-151">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="c099d-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Op basis van SAML eenmalige aanmelding](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_samlbase.png)

3. <span data-ttu-id="c099d-153">Op de **Tangoe opdracht Premium Mobile domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="c099d-153">On the **Tangoe Command Premium Mobile Domain and URLs** section, perform the following steps:</span></span>

    ![URL's en mobiele Tangoe opdracht Premium-domein](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_url.png)

    <span data-ttu-id="c099d-155">a.</span><span class="sxs-lookup"><span data-stu-id="c099d-155">a.</span></span> <span data-ttu-id="c099d-156">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://sso.tangoe.com/sp/startSSO.ping?PartnerIdpId=<tenant issuer>&TARGET=<target page url>`</span><span class="sxs-lookup"><span data-stu-id="c099d-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://sso.tangoe.com/sp/startSSO.ping?PartnerIdpId=<tenant issuer>&TARGET=<target page url>`</span></span>

    <span data-ttu-id="c099d-157">b.</span><span class="sxs-lookup"><span data-stu-id="c099d-157">b.</span></span> <span data-ttu-id="c099d-158">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://sso.tangoe.com/sp/ACS.saml2`</span><span class="sxs-lookup"><span data-stu-id="c099d-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://sso.tangoe.com/sp/ACS.saml2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c099d-159">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="c099d-159">These values are not real.</span></span> <span data-ttu-id="c099d-160">Deze waarden bijwerken met de werkelijke antwoord-URL en de aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="c099d-160">Update these values with the actual  Reply URL and Sign-On URL.</span></span> <span data-ttu-id="c099d-161">Neem contact op met [Tangoe opdracht Premium Mobile Client ondersteuningsteam](https://www.tangoe.com/contact-2/) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="c099d-161">Contact [Tangoe Command Premium Mobile Client support team](https://www.tangoe.com/contact-2/) to get these values.</span></span> 

4. <span data-ttu-id="c099d-162">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="c099d-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Certificaat voor ondertekening van SAML-sectie](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_certificate.png) 

5. <span data-ttu-id="c099d-164">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="c099d-164">Click **Save** button.</span></span>

    ![knop Opslaan](./media/active-directory-saas-tangoe-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="c099d-166">Op de **Tangoe Premium mobiele configuratie** sectie, klikt u op **configureren Tangoe opdracht Premium Mobile** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="c099d-166">On the **Tangoe Command Premium Mobile Configuration** section, click **Configure Tangoe Command Premium Mobile** to open **Configure sign-on** window.</span></span> <span data-ttu-id="c099d-167">Kopieer de **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="c099d-167">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuratiesectie Tangoe opdracht Premium Mobile](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_configure.png) 

7. <span data-ttu-id="c099d-169">Als u eenmalige aanmelding die zijn geconfigureerd voor uw toepassing, neem contact op met uw [Tangoe opdracht Premium Mobile Client ondersteuningsteam](https://www.tangoe.com/contact-2/) en biedt het volgende:</span><span class="sxs-lookup"><span data-stu-id="c099d-169">To get SSO configured for your application, contact your [Tangoe Command Premium Mobile Client support team](https://www.tangoe.com/contact-2/) and provide the following:</span></span>

   - <span data-ttu-id="c099d-170">Het metagegevensbestand van de gedownloade</span><span class="sxs-lookup"><span data-stu-id="c099d-170">The downloaded metadata file</span></span>
   - <span data-ttu-id="c099d-171">De **SAML entiteit-ID**</span><span class="sxs-lookup"><span data-stu-id="c099d-171">The **SAML Entity ID**</span></span>
   - <span data-ttu-id="c099d-172">De **URL voor SAML-Service voor eenmalige aanmelding**</span><span class="sxs-lookup"><span data-stu-id="c099d-172">The **SAML Single Sign-On Service URL**</span></span>
   - <span data-ttu-id="c099d-173">De **afmelden URL**</span><span class="sxs-lookup"><span data-stu-id="c099d-173">The **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="c099d-174">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="c099d-174">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c099d-175">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="c099d-175">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c099d-176">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c099d-176">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="c099d-177">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="c099d-177">Create an Azure AD test user</span></span>
<span data-ttu-id="c099d-178">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="c099d-178">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="c099d-180">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="c099d-180">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c099d-181">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="c099d-181">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tangoe-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c099d-183">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="c099d-183">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Gebruikers en groepen -> alle gebruikers](./media/active-directory-saas-tangoe-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c099d-185">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c099d-185">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Gebruiker toevoegen](./media/active-directory-saas-tangoe-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c099d-187">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="c099d-187">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Dialoogvenster op de gebruikerspagina](./media/active-directory-saas-tangoe-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c099d-189">a.</span><span class="sxs-lookup"><span data-stu-id="c099d-189">a.</span></span> <span data-ttu-id="c099d-190">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c099d-190">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c099d-191">b.</span><span class="sxs-lookup"><span data-stu-id="c099d-191">b.</span></span> <span data-ttu-id="c099d-192">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c099d-192">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c099d-193">c.</span><span class="sxs-lookup"><span data-stu-id="c099d-193">c.</span></span> <span data-ttu-id="c099d-194">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="c099d-194">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c099d-195">d.</span><span class="sxs-lookup"><span data-stu-id="c099d-195">d.</span></span> <span data-ttu-id="c099d-196">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="c099d-196">Click **Create**.</span></span>
 
### <a name="create-a-tangoe-command-premium-mobile-test-user"></a><span data-ttu-id="c099d-197">Maak een testgebruiker Tangoe opdracht Premium Mobile</span><span class="sxs-lookup"><span data-stu-id="c099d-197">Create a Tangoe Command Premium Mobile test user</span></span>

<span data-ttu-id="c099d-198">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in Tangoe opdracht Premium Mobile maken.</span><span class="sxs-lookup"><span data-stu-id="c099d-198">In this section, you create a user called Britta Simon in Tangoe Command Premium Mobile.</span></span> 

<span data-ttu-id="c099d-199">Tangoe opdracht Premium mobiele App moet de gebruikers moeten worden ingericht in de toepassing voordat u eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="c099d-199">Tangoe Command Premium Mobile application needs all the users to be provisioned in the application before doing Single Sign On.</span></span> <span data-ttu-id="c099d-200">Dus neem werk met de [Tangoe opdracht Premium Mobile Client ondersteuningsteam](https://www.tangoe.com/contact-2/) voor het inrichten van al deze gebruikers in de toepassing.</span><span class="sxs-lookup"><span data-stu-id="c099d-200">So please work with the [Tangoe Command Premium Mobile Client support team](https://www.tangoe.com/contact-2/) to provision all these users into the application.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="c099d-201">De Azure AD-testgebruiker toewijzen</span><span class="sxs-lookup"><span data-stu-id="c099d-201">Assign the Azure AD test user</span></span>

<span data-ttu-id="c099d-202">In deze sectie maakt inschakelen u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Tangoe opdracht Premium Mobile.</span><span class="sxs-lookup"><span data-stu-id="c099d-202">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Tangoe Command Premium Mobile.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="c099d-204">**Als u wilt toewijzen Britta Simon Tangoe opdracht Premium Mobile, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="c099d-204">**To assign Britta Simon to Tangoe Command Premium Mobile, perform the following steps:**</span></span>

1. <span data-ttu-id="c099d-205">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c099d-205">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="c099d-207">Selecteer in de lijst met toepassingen **Tangoe opdracht Premium Mobile**.</span><span class="sxs-lookup"><span data-stu-id="c099d-207">In the applications list, select **Tangoe Command Premium Mobile**.</span></span>

    ![Tangoe opdracht Premium Mobile in lijst met Apps](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_app.png) 

3. <span data-ttu-id="c099d-209">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="c099d-209">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="c099d-211">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="c099d-211">Click **Add** button.</span></span> <span data-ttu-id="c099d-212">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c099d-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="c099d-214">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="c099d-214">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c099d-215">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c099d-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c099d-216">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c099d-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="c099d-217">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="c099d-217">Test single sign-on</span></span>

<span data-ttu-id="c099d-218">In deze sectie kunt u uw Azure AD SSO-configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="c099d-218">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="c099d-219">Als u op de tegel Tangoe opdracht Premium Mobile in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Tangoe opdracht Premium Mobile.</span><span class="sxs-lookup"><span data-stu-id="c099d-219">When you click the Tangoe Command Premium Mobile tile in the Access Panel, you should get automatically signed-on to your Tangoe Command Premium Mobile application.</span></span> <span data-ttu-id="c099d-220">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c099d-220">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c099d-221">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="c099d-221">Additional resources</span></span>

* [<span data-ttu-id="c099d-222">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c099d-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c099d-223">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c099d-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_203.png

