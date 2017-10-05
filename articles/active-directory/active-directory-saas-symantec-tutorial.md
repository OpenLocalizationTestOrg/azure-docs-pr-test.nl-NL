---
title: 'Zelfstudie: Azure Active Directory-integratie met Symantec Web Security Service (WSS) | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Symantec Web Security Service (WSS).
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d6e4d893-1f14-4522-ac20-0c73b18c72a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 61576d3a915d209e7355e04432e586dcf66e7c5a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-symantec-web-security-service-wss"></a><span data-ttu-id="56077-103">Zelfstudie: Azure Active Directory-integratie met Symantec Web Security Service (WSS)</span><span class="sxs-lookup"><span data-stu-id="56077-103">Tutorial: Azure Active Directory integration with Symantec Web Security Service (WSS)</span></span>

<span data-ttu-id="56077-104">In deze zelfstudie leert u het integreren van uw account Symantec Web Security Service (WSS) aan uw account voor Azure Active Directory (Azure AD), zodat WSS kunnen verifiëren van een eindgebruiker ingericht in de Azure AD dat gebruikmaakt van SAML-verificatie en afdwingen van de gebruiker of groep niveau beleidsregels.</span><span class="sxs-lookup"><span data-stu-id="56077-104">In this tutorial, you will learn how to integrate your Symantec Web Security Service (WSS) account with your Azure Active Directory (Azure AD) account so that WSS can authenticate an end user provisioned in the Azure AD using SAML authentication and enforce user or group level policy rules.</span></span>

<span data-ttu-id="56077-105">Symantec Web Security Service (WSS) integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="56077-105">Integrating Symantec Web Security Service (WSS) with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="56077-106">Alle gebruikers en groepen die worden gebruikt door uw WSS-account van uw Azure AD-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="56077-106">Manage all of the end users and groups used by your WSS account from your Azure AD portal.</span></span> 

- <span data-ttu-id="56077-107">De gebruikers om zich te authentiseren in WSS met hun Azure AD-referenties toestaan.</span><span class="sxs-lookup"><span data-stu-id="56077-107">Allow the end users to authenticate themselves in WSS using their Azure AD credentials.</span></span>

- <span data-ttu-id="56077-108">Schakel het afdwingen van de gebruiker en groep niveau beleidsregels die zijn gedefinieerd in uw WSS-account.</span><span class="sxs-lookup"><span data-stu-id="56077-108">Enable the enforcement of user and group level policy rules defined in your WSS account.</span></span>

<span data-ttu-id="56077-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="56077-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="56077-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="56077-110">Prerequisites</span></span>

<span data-ttu-id="56077-111">Voor het configureren van Azure AD-integratie met Symantec Web Security Service (WSS), moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="56077-111">To configure Azure AD integration with Symantec Web Security Service (WSS), you need the following items:</span></span>

- <span data-ttu-id="56077-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="56077-112">An Azure AD subscription</span></span>
- <span data-ttu-id="56077-113">Een account Symantec Web Security Service (WSS)</span><span class="sxs-lookup"><span data-stu-id="56077-113">A Symantec Web Security Service (WSS) account</span></span>

> [!NOTE]
> <span data-ttu-id="56077-114">Test de stappen in deze zelfstudie, raden we niet met een WSS-account dat momenteel wordt gebruikt voor productie-doel.</span><span class="sxs-lookup"><span data-stu-id="56077-114">To test the steps in this tutorial, we do not recommend using a WSS account that is currently being used for production purpose.</span></span>

<span data-ttu-id="56077-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="56077-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="56077-116">Gebruik niet uw WSS-account dat momenteel wordt gebruikt voor productie-doel voor deze test als dat nodig is.</span><span class="sxs-lookup"><span data-stu-id="56077-116">Do not use your WSS account that is currently being used for production purpose for this test unless it is necessary.</span></span>
- <span data-ttu-id="56077-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="56077-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="56077-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="56077-118">Scenario description</span></span>
<span data-ttu-id="56077-119">In deze zelfstudie configureert u uw Azure AD om in te schakelen eenmalige aanmelding voor WSS met behulp van de referenties van de gebruiker gedefinieerd in uw Azure AD-account.</span><span class="sxs-lookup"><span data-stu-id="56077-119">In this tutorial, you will configure your Azure AD to enable single sign-on to WSS using the end user credentials defined in your Azure AD account.</span></span>
<span data-ttu-id="56077-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="56077-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="56077-121">De app Symantec Web Security Service (WSS) toevoegen uit de galerie</span><span class="sxs-lookup"><span data-stu-id="56077-121">Adding the Symantec Web Security Service (WSS) app from the gallery</span></span>
2. <span data-ttu-id="56077-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="56077-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-symantec-web-security-service-wss-from-the-gallery"></a><span data-ttu-id="56077-123">Symantec Web Security Service (WSS) uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="56077-123">Adding Symantec Web Security Service (WSS) from the gallery</span></span>
<span data-ttu-id="56077-124">Voor het configureren van de integratie van Symantec Web Security Service (WSS) in Azure AD, moet u Symantec Web Security Service (WSS) uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="56077-124">To configure the integration of Symantec Web Security Service (WSS) into Azure AD, you need to add Symantec Web Security Service (WSS) from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="56077-125">**Als u wilt toevoegen Symantec Web Security Service (WSS) uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="56077-125">**To add Symantec Web Security Service (WSS) from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="56077-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="56077-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![De Azure Active Directory-knop][1]

2. <span data-ttu-id="56077-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="56077-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="56077-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="56077-129">Then go to **All applications**.</span></span>

    ![De blade Enterprise-toepassingen][2]
    
3. <span data-ttu-id="56077-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="56077-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![De knop Nieuw toepassing][3]

4. <span data-ttu-id="56077-133">Typ in het zoekvak **Symantec Web Security Service (WSS)**, selecteer **Symantec Web Security Service (WSS)** van resultaat deelvenster klik vervolgens op **toevoegen** om toe te voegen de de toepassing.</span><span class="sxs-lookup"><span data-stu-id="56077-133">In the search box, type **Symantec Web Security Service (WSS)**, select **Symantec Web Security Service (WSS)** from result panel then click **Add** button to add the application.</span></span>

    ![Symantec Web Security Service (WSS) in de lijst met resultaten](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="56077-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="56077-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="56077-136">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Symantec Web Security Service (WSS) hebt op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="56077-136">In this section, you configure and test Azure AD single sign-on with Symantec Web Security Service (WSS) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="56077-137">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Symantec Web Security Service (WSS) is aan een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="56077-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Symantec Web Security Service (WSS) is to a user in Azure AD.</span></span> <span data-ttu-id="56077-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Symantec Web Security Service (WSS) tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="56077-138">In other words, a link relationship between an Azure AD user and the related user in Symantec Web Security Service (WSS) needs to be established.</span></span>

<span data-ttu-id="56077-139">In Symantec Web Security Service (WSS), wijs de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="56077-139">In Symantec Web Security Service (WSS), assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="56077-140">Om te configureren en testen van Azure AD eenmalige aanmelding met Symantec Web Security Service (WSS), moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="56077-140">To configure and test Azure AD single sign-on with Symantec Web Security Service (WSS), you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="56077-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="56077-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="56077-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="56077-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="56077-143">**[Maak een testgebruiker Symantec Web Security Service (WSS)](#create-a-symantec-web-security-service-wss-test-user)**  - hebben een equivalent van Britta Simon in Symantec Web Security Service (WSS) die is gekoppeld aan de Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="56077-143">**[Create a Symantec Web Security Service (WSS) test user](#create-a-symantec-web-security-service-wss-test-user)** - to have a counterpart of Britta Simon in Symantec Web Security Service (WSS) that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="56077-144">**[Toewijzen van de Azure AD-testgebruiker](#assign-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="56077-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="56077-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="56077-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="56077-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="56077-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="56077-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw toepassing Symantec Web Security Service (WSS).</span><span class="sxs-lookup"><span data-stu-id="56077-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Symantec Web Security Service (WSS) application.</span></span>

<span data-ttu-id="56077-148">**Voor het configureren van Azure AD eenmalige aanmelding met Symantec Web Security Service (WSS), moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="56077-148">**To configure Azure AD single sign-on with Symantec Web Security Service (WSS), perform the following steps:**</span></span>

1. <span data-ttu-id="56077-149">In de Azure-portal op de **Symantec Web Security Service (WSS)** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="56077-149">In the Azure portal, on the **Symantec Web Security Service (WSS)** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="56077-151">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="56077-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_samlbase.png)

3. <span data-ttu-id="56077-153">Op de **Symantec Web Service (WSS) beveiligingsdomein en URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="56077-153">On the **Symantec Web Security Service (WSS) Domain and URLs** section, perform the following steps:</span></span>

    ![Symantec Web Security Service (WSS)-domein en de URL's van eenmalige aanmelding informatie](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_url.png)

    <span data-ttu-id="56077-155">a.</span><span class="sxs-lookup"><span data-stu-id="56077-155">a.</span></span> <span data-ttu-id="56077-156">In de **id** textbox, typ de URL:`https://saml.threatpulse.net:8443/saml/saml_realm`</span><span class="sxs-lookup"><span data-stu-id="56077-156">In the **Identifier** textbox, type the URL: `https://saml.threatpulse.net:8443/saml/saml_realm`</span></span>

    <span data-ttu-id="56077-157">b.</span><span class="sxs-lookup"><span data-stu-id="56077-157">b.</span></span> <span data-ttu-id="56077-158">In de **antwoord-URL** textbox, typ de URL:`https://saml.threatpulse.net:8443/saml/saml_realm/bcsamlpost`</span><span class="sxs-lookup"><span data-stu-id="56077-158">In the **Reply URL** textbox, type the URL: `https://saml.threatpulse.net:8443/saml/saml_realm/bcsamlpost`</span></span>

    > [!NOTE]
    > <span data-ttu-id="56077-159">Neem contact op met de [Symantec Web Security Service (WSS) Client ondersteuningsteam](https://www.symantec.com/contact-us) als de waarden voor de **id** en **antwoord-URL** zijn voor een bepaalde reden niet werkt.</span><span class="sxs-lookup"><span data-stu-id="56077-159">Please contact the [Symantec Web Security Service (WSS) Client support team](https://www.symantec.com/contact-us) if the values for the **Identifier** and **Reply URL** are not working for some reason.</span></span>

4. <span data-ttu-id="56077-160">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="56077-160">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![De downloadkoppeling certificaat](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_certificate.png) 

5. <span data-ttu-id="56077-162">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="56077-162">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-symantec-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="56077-164">Raadpleeg de onlinedocumentatie WSS voor het configureren van eenmalige aanmelding aan de kant van Symantec Web Security Service (WSS).</span><span class="sxs-lookup"><span data-stu-id="56077-164">To configure single sign-on on the Symantec Web Security Service (WSS) side, refer to the WSS online documentation.</span></span> <span data-ttu-id="56077-165">De gedownloade **Metadata XML** bestand moet worden geïmporteerd in de WSS-portal.</span><span class="sxs-lookup"><span data-stu-id="56077-165">The downloaded **Metadata XML** file will need to be imported into the WSS portal.</span></span> <span data-ttu-id="56077-166">Neem contact op met de [Symantec Web Security Service (WSS) ondersteuningsteam](https://www.symantec.com/contact-us) als u hulp nodig hebt bij de configuratie op de WSS-portal.</span><span class="sxs-lookup"><span data-stu-id="56077-166">Contact the [Symantec Web Security Service (WSS) support team](https://www.symantec.com/contact-us) if you need assistance with the configuration on the WSS portal.</span></span>

> [!TIP]
> <span data-ttu-id="56077-167">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="56077-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="56077-168">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="56077-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="56077-169">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="56077-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="56077-170">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="56077-170">Create an Azure AD test user</span></span>

<span data-ttu-id="56077-171">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="56077-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="56077-173">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="56077-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="56077-174">Klik in de Azure-portal in het linkerdeelvenster op het **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="56077-174">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![De Azure Active Directory-knop](./media/active-directory-saas-symantec-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="56077-176">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="56077-176">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !['Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-symantec-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="56077-178">Openen van de **gebruiker** in het dialoogvenster klikt u op **toevoegen** boven aan de **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="56077-178">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![De knop toevoegen](./media/active-directory-saas-symantec-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="56077-180">In de **gebruiker** dialoogvenster vak, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="56077-180">In the **User** dialog box, perform the following steps:</span></span>

    ![Het dialoogvenster gebruiker](./media/active-directory-saas-symantec-tutorial/create_aaduser_04.png)

    <span data-ttu-id="56077-182">a.</span><span class="sxs-lookup"><span data-stu-id="56077-182">a.</span></span> <span data-ttu-id="56077-183">In de **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="56077-183">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="56077-184">b.</span><span class="sxs-lookup"><span data-stu-id="56077-184">b.</span></span> <span data-ttu-id="56077-185">In de **gebruikersnaam** typt u het e-mailadres van gebruiker Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="56077-185">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="56077-186">c.</span><span class="sxs-lookup"><span data-stu-id="56077-186">c.</span></span> <span data-ttu-id="56077-187">Selecteer de **wachtwoord weergeven** selectievakje, en noteer de waarde die wordt weergegeven in de **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="56077-187">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="56077-188">d.</span><span class="sxs-lookup"><span data-stu-id="56077-188">d.</span></span> <span data-ttu-id="56077-189">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="56077-189">Click **Create**.</span></span>
 
### <a name="create-a-symantec-web-security-service-wss-test-user"></a><span data-ttu-id="56077-190">Maak een testgebruiker Symantec Web Security Service (WSS)</span><span class="sxs-lookup"><span data-stu-id="56077-190">Create a Symantec Web Security Service (WSS) test user</span></span>

<span data-ttu-id="56077-191">In deze sectie maakt u een gebruiker met de naam Britta Simon in Symantec Web Security Service (WSS).</span><span class="sxs-lookup"><span data-stu-id="56077-191">In this section, you create a user called Britta Simon in Symantec Web Security Service (WSS).</span></span> <span data-ttu-id="56077-192">De bijbehorende end gebruikersnaam kan handmatig worden gemaakt in de WSS-portal of u kunt wachten op de gebruikers/groepen ingericht in de Azure AD moeten worden gesynchroniseerd naar de portal WSS na een paar minuten (~ 15 minuten).</span><span class="sxs-lookup"><span data-stu-id="56077-192">The corresponding end username can be manually created in the WSS portal or you can wait for the users/groups provisioned in the Azure AD to be synchronized to the WSS portal after a few minutes (~15 minutes).</span></span> <span data-ttu-id="56077-193">Gebruikers moeten worden gemaakt en worden geactiveerd voordat u eenmalige aanmelding gebruiken.</span><span class="sxs-lookup"><span data-stu-id="56077-193">Users must be created and activated before you use single sign-on.</span></span> <span data-ttu-id="56077-194">Het openbare IP-adres van de eindgebruiker-machine die wordt gebruikt om te bladeren websites moet ook worden ingericht in de portal Symantec Web Security Service (WSS).</span><span class="sxs-lookup"><span data-stu-id="56077-194">The public IP address of the end user machine, which will be used to browse websites also need to be provisioned in the Symantec Web Security Service (WSS) portal.</span></span>

> [!NOTE]
> <span data-ttu-id="56077-195">Neem [Klik hier](http://www.bing.com/search?q=my+ip+address&qs=AS&pq=my+ip+a&sc=8-7&cvid=29A720C95C78488CA3F9A6BA0B3F98C5&FORM=QBLH&sp=1) ophalen van de computer het openbare IP-adres.</span><span class="sxs-lookup"><span data-stu-id="56077-195">Please [click here](http://www.bing.com/search?q=my+ip+address&qs=AS&pq=my+ip+a&sc=8-7&cvid=29A720C95C78488CA3F9A6BA0B3F98C5&FORM=QBLH&sp=1) to get your machine's public IPaddress.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="56077-196">De Azure AD-testgebruiker toewijzen</span><span class="sxs-lookup"><span data-stu-id="56077-196">Assign the Azure AD test user</span></span>

<span data-ttu-id="56077-197">In deze sectie schakelt u Britta Simon Azure eenmalige aanmelding toegang verleent aan Symantec Web Security Service (WSS) gebruiken.</span><span class="sxs-lookup"><span data-stu-id="56077-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Symantec Web Security Service (WSS).</span></span>

![Toewijzen van de gebruikersrol][200] 

<span data-ttu-id="56077-199">**Als u wilt toewijzen Britta Simon naar Symantec Web Security Service (WSS), moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="56077-199">**To assign Britta Simon to Symantec Web Security Service (WSS), perform the following steps:**</span></span>

1. <span data-ttu-id="56077-200">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="56077-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="56077-202">Selecteer in de lijst met toepassingen **Symantec Web Security Service (WSS)**.</span><span class="sxs-lookup"><span data-stu-id="56077-202">In the applications list, select **Symantec Web Security Service (WSS)**.</span></span>

    ![De koppeling Symantec Web Security Service (WSS) in de lijst met toepassingen](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_app.png)  

3. <span data-ttu-id="56077-204">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="56077-204">In the menu on the left, click **Users and groups**.</span></span>

    ![De koppeling 'Gebruikers en groepen'][202]

4. <span data-ttu-id="56077-206">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="56077-206">Click **Add** button.</span></span> <span data-ttu-id="56077-207">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="56077-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Het deelvenster toewijzing toevoegen][203]

5. <span data-ttu-id="56077-209">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="56077-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="56077-210">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="56077-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="56077-211">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="56077-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="56077-212">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="56077-212">Test single sign-on</span></span>

<span data-ttu-id="56077-213">In deze sectie test u de functionaliteit voor eenmalige aanmelding nu dat u uw WSS-account voor het gebruik van uw Azure AD voor SAML-verificatie hebt geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="56077-213">In this section, you'll test the single sign-on functionality now that you've configured your WSS account to use your Azure AD for SAML authentication.</span></span>

<span data-ttu-id="56077-214">Nadat u hebt uw webbrowser om proxy het verkeer naar WSS, geconfigureerd wanneer u uw webbrowser Open en probeert om te bladeren naar een site en vervolgens wordt u omgeleid naar de pagina voor Azure.</span><span class="sxs-lookup"><span data-stu-id="56077-214">After you have configured your web browser to proxy traffic to WSS, when you open your web browser and try to browse to a site then you'll be redirected to the Azure sign-on page.</span></span> <span data-ttu-id="56077-215">Geef de referenties van de eindgebruiker test die is ingericht in de Azure AD (dat wil zeggen, BrittaSimon) en het wachtwoord dat is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="56077-215">Enter the credentials of the test end user that has been provisioned in the Azure AD (that is, BrittaSimon) and associated password.</span></span> <span data-ttu-id="56077-216">Eenmaal is geverifieerd, kunt u zult kunnen bladeren naar de website die u hebt gekozen.</span><span class="sxs-lookup"><span data-stu-id="56077-216">Once authenticated, you'll be able to browse to the website that you chose.</span></span> <span data-ttu-id="56077-217">U moet een beleidsregel maken aan de kant WSS BrittaSimon van bladeren naar een bepaalde site, en vervolgens u de pagina WSS-blok ziet wanneer u probeert om te bladeren naar die site als gebruiker BrittaSimon blokkeren.</span><span class="sxs-lookup"><span data-stu-id="56077-217">Should you create a policy rule on the WSS side to block BrittaSimon from browsing to a particular site then you should see the WSS block page when you attempt to browse to that site as user BrittaSimon.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="56077-218">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="56077-218">Additional resources</span></span>

* [<span data-ttu-id="56077-219">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="56077-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="56077-220">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="56077-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_203.png

