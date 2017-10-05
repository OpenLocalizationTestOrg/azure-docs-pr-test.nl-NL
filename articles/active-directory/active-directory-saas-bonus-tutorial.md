---
title: 'Zelfstudie: Azure Active Directory-integratie met Bonusly | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Bonusly.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 29fea32a-fa20-47b2-9e24-26feb47b0ae6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 29a88b2efdb9f0f33f7933bc654a5a0fdf589c5a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bonusly"></a><span data-ttu-id="3e68b-103">Zelfstudie: Azure Active Directory-integratie met Bonusly</span><span class="sxs-lookup"><span data-stu-id="3e68b-103">Tutorial: Azure Active Directory integration with Bonusly</span></span>

<span data-ttu-id="3e68b-104">In deze zelfstudie leert u hoe Bonusly integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3e68b-104">In this tutorial, you learn how to integrate Bonusly with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3e68b-105">Bonusly integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="3e68b-105">Integrating Bonusly with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3e68b-106">U kunt beheren in Azure AD die toegang tot Bonusly heeft</span><span class="sxs-lookup"><span data-stu-id="3e68b-106">You can control in Azure AD who has access to Bonusly</span></span>
- <span data-ttu-id="3e68b-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Bonusly (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="3e68b-107">You can enable your users to automatically get signed-on to Bonusly (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3e68b-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="3e68b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3e68b-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3e68b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3e68b-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="3e68b-110">Prerequisites</span></span>

<span data-ttu-id="3e68b-111">Voor het configureren van Azure AD-integratie met Bonusly, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="3e68b-111">To configure Azure AD integration with Bonusly, you need the following items:</span></span>

- <span data-ttu-id="3e68b-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="3e68b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3e68b-113">Een Bonusly eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="3e68b-113">A Bonusly single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3e68b-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="3e68b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3e68b-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="3e68b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3e68b-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="3e68b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3e68b-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3e68b-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3e68b-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="3e68b-118">Scenario description</span></span>
<span data-ttu-id="3e68b-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="3e68b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3e68b-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="3e68b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3e68b-121">Bonusly uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="3e68b-121">Adding Bonusly from the gallery</span></span>
2. <span data-ttu-id="3e68b-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="3e68b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bonusly-from-the-gallery"></a><span data-ttu-id="3e68b-123">Bonusly uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="3e68b-123">Adding Bonusly from the gallery</span></span>
<span data-ttu-id="3e68b-124">Voor het configureren van de integratie van Bonusly in Azure AD, moet u Bonusly uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="3e68b-124">To configure the integration of Bonusly into Azure AD, you need to add Bonusly from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3e68b-125">**Als u wilt toevoegen Bonusly uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="3e68b-125">**To add Bonusly from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3e68b-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="3e68b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![De Azure Active Directory-knop][1]

2. <span data-ttu-id="3e68b-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="3e68b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3e68b-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="3e68b-129">Then go to **All applications**.</span></span>

    ![De blade Enterprise-toepassingen][2]
    
3. <span data-ttu-id="3e68b-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3e68b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![De knop Nieuw toepassing][3]

4. <span data-ttu-id="3e68b-133">Typ in het zoekvak **Bonusly**, selecteer **Bonusly** van resultaat deelvenster klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="3e68b-133">In the search box, type **Bonusly**, select **Bonusly** from result panel then click **Add** button to add the application.</span></span>

    ![Bonusly in de lijst met resultaten](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="3e68b-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="3e68b-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="3e68b-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met Bonusly op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="3e68b-136">In this section, you configure and test Azure AD single sign-on with Bonusly based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3e68b-137">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Bonusly is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3e68b-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Bonusly is to a user in Azure AD.</span></span> <span data-ttu-id="3e68b-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Bonusly tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="3e68b-138">In other words, a link relationship between an Azure AD user and the related user in Bonusly needs to be established.</span></span>

<span data-ttu-id="3e68b-139">Wijs in Bonusly, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="3e68b-139">In Bonusly, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3e68b-140">Om te configureren en testen van Azure AD eenmalige aanmelding met Bonusly, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="3e68b-140">To configure and test Azure AD single sign-on with Bonusly, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3e68b-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3e68b-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3e68b-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3e68b-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3e68b-143">**[Maak een Bonusly testgebruiker](#create-a-bonusly-test-user)**  - Bonusly die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="3e68b-143">**[Create a Bonusly test user](#create-a-bonusly-test-user)** - to have a counterpart of Britta Simon in Bonusly that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3e68b-144">**[Toewijzen van de Azure AD-testgebruiker](#assign-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="3e68b-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3e68b-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="3e68b-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="3e68b-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="3e68b-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="3e68b-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Bonusly configureren.</span><span class="sxs-lookup"><span data-stu-id="3e68b-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Bonusly application.</span></span>

<span data-ttu-id="3e68b-148">**Voor het configureren van Azure AD eenmalige aanmelding met Bonusly, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="3e68b-148">**To configure Azure AD single sign-on with Bonusly, perform the following steps:**</span></span>

1. <span data-ttu-id="3e68b-149">In de Azure-portal op de **Bonusly** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="3e68b-149">In the Azure portal, on the **Bonusly** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="3e68b-151">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="3e68b-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_samlbase.png)

3. <span data-ttu-id="3e68b-153">Op de **Bonusly domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="3e68b-153">On the **Bonusly Domain and URLs** section, perform the following steps:</span></span>

    ![Bonusly domein en de URL's van eenmalige aanmelding informatie](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_url.png)

    <span data-ttu-id="3e68b-155">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://Bonus.ly/saml/<tenant-name>`</span><span class="sxs-lookup"><span data-stu-id="3e68b-155">In the **Reply URL** textbox, type a URL using the following pattern: `https://Bonus.ly/saml/<tenant-name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3e68b-156">De waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="3e68b-156">The value is not real.</span></span> <span data-ttu-id="3e68b-157">Werk de waarde met de werkelijke antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="3e68b-157">Update the value with the actual Reply URL.</span></span> <span data-ttu-id="3e68b-158">Neem contact op met [Bonusly ondersteuningsteam](https://Bonusly/contact) de waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="3e68b-158">Contact [Bonusly support team](https://Bonusly/contact) to get the value.</span></span>
 
4. <span data-ttu-id="3e68b-159">Op de **SAML-certificaat voor ondertekening van** sectie, Kopieer de **VINGERAFDRUK** waarde van het certificaat.</span><span class="sxs-lookup"><span data-stu-id="3e68b-159">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value from the certificate.</span></span>

    ![De downloadkoppeling certificaat](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_certificate.png) 

5. <span data-ttu-id="3e68b-161">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="3e68b-161">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-bonus-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3e68b-163">Op de **Bonusly configuratie** sectie, klikt u op **Bonusly configureren** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="3e68b-163">On the **Bonusly Configuration** section, click **Configure Bonusly** to open **Configure sign-on** window.</span></span> <span data-ttu-id="3e68b-164">Kopieer de **SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="3e68b-164">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Bonusly configuratie](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_configure.png) 

7. <span data-ttu-id="3e68b-166">In een ander browservenster, meld u aan bij uw **Bonusly** tenant.</span><span class="sxs-lookup"><span data-stu-id="3e68b-166">In a different browser window, log in to your **Bonusly** tenant.</span></span>

8. <span data-ttu-id="3e68b-167">Klik in de werkbalk bovenaan op **instellingen**, en selecteer vervolgens **integraties en apps**.</span><span class="sxs-lookup"><span data-stu-id="3e68b-167">In the toolbar on the top, click **Settings**, and then select **Integrations and apps**.</span></span>
   
    <span data-ttu-id="3e68b-168">![Bonusly sociale sectie](./media/active-directory-saas-bonus-tutorial/ic773686.png "Bonusly")</span><span class="sxs-lookup"><span data-stu-id="3e68b-168">![Bonusly Social Section](./media/active-directory-saas-bonus-tutorial/ic773686.png "Bonusly")</span></span>
9. <span data-ttu-id="3e68b-169">Onder **Single Sign-On**, selecteer **SAML**.</span><span class="sxs-lookup"><span data-stu-id="3e68b-169">Under **Single Sign-On**, select **SAML**.</span></span>

10. <span data-ttu-id="3e68b-170">Op de **SAML** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="3e68b-170">On the **SAML** dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="3e68b-171">![Bonusly Saml dialoogvenster pagina](./media/active-directory-saas-bonus-tutorial/ic773687.png "Bonusly")</span><span class="sxs-lookup"><span data-stu-id="3e68b-171">![Bonusly Saml Dialog page](./media/active-directory-saas-bonus-tutorial/ic773687.png "Bonusly")</span></span>
   
    <span data-ttu-id="3e68b-172">a.</span><span class="sxs-lookup"><span data-stu-id="3e68b-172">a.</span></span> <span data-ttu-id="3e68b-173">In de **doel-URL voor eenmalige aanmelding IdP** textbox, plak de waarde van **SAML Single Sign-On Service-URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="3e68b-173">In the **IdP SSO target URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="3e68b-174">b.</span><span class="sxs-lookup"><span data-stu-id="3e68b-174">b.</span></span> <span data-ttu-id="3e68b-175">In de **IdP verlener** textbox, plak de waarde van **SAML entiteit-ID**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="3e68b-175">In the **IdP Issuer** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="3e68b-176">c.</span><span class="sxs-lookup"><span data-stu-id="3e68b-176">c.</span></span> <span data-ttu-id="3e68b-177">In de **IdP aanmeldings-URL** textbox, plak de waarde van **SAML Single Sign-On Service-URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="3e68b-177">In the **IdP Login URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="3e68b-178">d.</span><span class="sxs-lookup"><span data-stu-id="3e68b-178">d.</span></span> <span data-ttu-id="3e68b-179">Plak de **vingerafdruk** waarde opgehaald uit Azure-portal in de **Cert vingerafdruk** textbox.</span><span class="sxs-lookup"><span data-stu-id="3e68b-179">Paste the **Thumbprint** value copied from Azure portal into the **Cert Fingerprint** textbox.</span></span>
   
11. <span data-ttu-id="3e68b-180">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="3e68b-180">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="3e68b-181">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="3e68b-181">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3e68b-182">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="3e68b-182">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3e68b-183">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3e68b-183">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="3e68b-184">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="3e68b-184">Create an Azure AD test user</span></span>
<span data-ttu-id="3e68b-185">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="3e68b-185">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="3e68b-187">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="3e68b-187">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3e68b-188">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="3e68b-188">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![De Azure Active Directory-knop](./media/active-directory-saas-bonus-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3e68b-190">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="3e68b-190">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    !['Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-bonus-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3e68b-192">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3e68b-192">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![De knop toevoegen](./media/active-directory-saas-bonus-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3e68b-194">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="3e68b-194">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Het dialoogvenster gebruiker](./media/active-directory-saas-bonus-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3e68b-196">a.</span><span class="sxs-lookup"><span data-stu-id="3e68b-196">a.</span></span> <span data-ttu-id="3e68b-197">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3e68b-197">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3e68b-198">b.</span><span class="sxs-lookup"><span data-stu-id="3e68b-198">b.</span></span> <span data-ttu-id="3e68b-199">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3e68b-199">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3e68b-200">c.</span><span class="sxs-lookup"><span data-stu-id="3e68b-200">c.</span></span> <span data-ttu-id="3e68b-201">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="3e68b-201">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3e68b-202">d.</span><span class="sxs-lookup"><span data-stu-id="3e68b-202">d.</span></span> <span data-ttu-id="3e68b-203">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="3e68b-203">Click **Create**.</span></span>
 
### <a name="create-a-bonusly-test-user"></a><span data-ttu-id="3e68b-204">Een Bonusly testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="3e68b-204">Create a Bonusly test user</span></span>

<span data-ttu-id="3e68b-205">Om Azure AD-gebruikers zich aanmelden bij Bonusly inschakelt, moeten ze worden ingericht in Bonusly.</span><span class="sxs-lookup"><span data-stu-id="3e68b-205">In order to enable Azure AD users to log in to Bonusly, they must be provisioned into Bonusly.</span></span> <span data-ttu-id="3e68b-206">In het geval van Bonusly is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="3e68b-206">In the case of Bonusly, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="3e68b-207">U kunt een andere gebruiker Bonusly account hulpmiddelen voor het maken of API's die is geleverd door Bonusly aan inrichten AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="3e68b-207">You can use any other Bonusly user account creation tools or APIs provided by Bonusly to provision AAD user accounts.</span></span>
>  

<span data-ttu-id="3e68b-208">**Als u wilt configureren voor gebruikers inrichten, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="3e68b-208">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="3e68b-209">In een browservenster geopend, moet u zich aanmelden bij uw Bonusly tenant.</span><span class="sxs-lookup"><span data-stu-id="3e68b-209">In a web browser window, log in to your Bonusly tenant.</span></span>

2. <span data-ttu-id="3e68b-210">Klik op **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="3e68b-210">Click **Settings**.</span></span>
 
    <span data-ttu-id="3e68b-211">![Instellingen](./media/active-directory-saas-bonus-tutorial/ic781041.png "instellingen")</span><span class="sxs-lookup"><span data-stu-id="3e68b-211">![Settings](./media/active-directory-saas-bonus-tutorial/ic781041.png "Settings")</span></span>

3. <span data-ttu-id="3e68b-212">Klik op de **gebruikers en bonussen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="3e68b-212">Click the **Users and bonuses** tab.</span></span>
   
    <span data-ttu-id="3e68b-213">![Gebruikers en bonussen](./media/active-directory-saas-bonus-tutorial/ic781042.png "gebruikers en bonussen")</span><span class="sxs-lookup"><span data-stu-id="3e68b-213">![Users and bonuses](./media/active-directory-saas-bonus-tutorial/ic781042.png "Users and bonuses")</span></span>

4. <span data-ttu-id="3e68b-214">Klik op **gebruikers beheren**.</span><span class="sxs-lookup"><span data-stu-id="3e68b-214">Click **Manage Users**.</span></span>
   
    <span data-ttu-id="3e68b-215">![Gebruikers beheren](./media/active-directory-saas-bonus-tutorial/ic781043.png "gebruikers beheren")</span><span class="sxs-lookup"><span data-stu-id="3e68b-215">![Manage Users](./media/active-directory-saas-bonus-tutorial/ic781043.png "Manage Users")</span></span>

5. <span data-ttu-id="3e68b-216">Klik op **gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="3e68b-216">Click **Add User**.</span></span>
   
    <span data-ttu-id="3e68b-217">![Gebruiker toevoegen](./media/active-directory-saas-bonus-tutorial/ic781044.png "gebruiker toevoegen")</span><span class="sxs-lookup"><span data-stu-id="3e68b-217">![Add User](./media/active-directory-saas-bonus-tutorial/ic781044.png "Add User")</span></span>

6. <span data-ttu-id="3e68b-218">Op de **gebruiker toevoegen** dialoogvenster de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="3e68b-218">On the **Add User** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="3e68b-219">![Gebruiker toevoegen](./media/active-directory-saas-bonus-tutorial/ic781045.png "gebruiker toevoegen")</span><span class="sxs-lookup"><span data-stu-id="3e68b-219">![Add User](./media/active-directory-saas-bonus-tutorial/ic781045.png "Add User")</span></span>  

    <span data-ttu-id="3e68b-220">a.</span><span class="sxs-lookup"><span data-stu-id="3e68b-220">a.</span></span> <span data-ttu-id="3e68b-221">In de **voornaam** textbox, voer de voornaam van de gebruiker zoals **Britta**.</span><span class="sxs-lookup"><span data-stu-id="3e68b-221">In the **First name** textbox, enter the first name of user like **Britta**.</span></span>

    <span data-ttu-id="3e68b-222">b.</span><span class="sxs-lookup"><span data-stu-id="3e68b-222">b.</span></span> <span data-ttu-id="3e68b-223">In de **achternaam** textbox, geef de achternaam van de gebruiker zoals **Simon**.</span><span class="sxs-lookup"><span data-stu-id="3e68b-223">In the **Last name** textbox, enter the last name of user like **Simon**.</span></span>
 
    <span data-ttu-id="3e68b-224">c.</span><span class="sxs-lookup"><span data-stu-id="3e68b-224">c.</span></span> <span data-ttu-id="3e68b-225">In de **e** textbox, voer het e-mailadres van de gebruiker zoals  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="3e68b-225">In the **Email** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="3e68b-226">d.</span><span class="sxs-lookup"><span data-stu-id="3e68b-226">d.</span></span> <span data-ttu-id="3e68b-227">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="3e68b-227">Click **Save**.</span></span>
   
     >[!NOTE]
     ><span data-ttu-id="3e68b-228">De accounthouder Azure AD ontvangt een e-mailbericht een koppeling om te bevestigen van het account bevat voordat deze geactiveerd wordt.</span><span class="sxs-lookup"><span data-stu-id="3e68b-228">The Azure AD account holder receives an email that includes a link to confirm the account before it becomes active.</span></span>
     >  

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="3e68b-229">De Azure AD-testgebruiker toewijzen</span><span class="sxs-lookup"><span data-stu-id="3e68b-229">Assign the Azure AD test user</span></span>

<span data-ttu-id="3e68b-230">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Bonusly.</span><span class="sxs-lookup"><span data-stu-id="3e68b-230">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Bonusly.</span></span>

![Toewijzen van de gebruikersrol][200] 

<span data-ttu-id="3e68b-232">**Britta Simon om aan te wijzen Bonusly, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="3e68b-232">**To assign Britta Simon to Bonusly, perform the following steps:**</span></span>

1. <span data-ttu-id="3e68b-233">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="3e68b-233">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="3e68b-235">Selecteer in de lijst met toepassingen **Bonusly**.</span><span class="sxs-lookup"><span data-stu-id="3e68b-235">In the applications list, select **Bonusly**.</span></span>

    ![De Bonusly koppelen in de lijst met toepassingen](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_app.png) 

3. <span data-ttu-id="3e68b-237">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="3e68b-237">In the menu on the left, click **Users and groups**.</span></span>

    ![De koppeling 'Gebruikers en groepen'][202] 

4. <span data-ttu-id="3e68b-239">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="3e68b-239">Click **Add** button.</span></span> <span data-ttu-id="3e68b-240">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3e68b-240">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Het deelvenster toewijzing toevoegen][203]

5. <span data-ttu-id="3e68b-242">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="3e68b-242">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3e68b-243">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3e68b-243">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3e68b-244">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3e68b-244">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="3e68b-245">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="3e68b-245">Test single sign-on</span></span>

<span data-ttu-id="3e68b-246">Het doel van deze sectie is het testen van uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="3e68b-246">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3e68b-247">Wanneer u klikt op de tegel Bonusly in het deelvenster toegang u moet ophalen automatisch aangemeld bij uw Bonusly toepassing.</span><span class="sxs-lookup"><span data-stu-id="3e68b-247">When you click the Bonusly tile in the Access Panel, you should get automatically signed-on to your Bonusly application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3e68b-248">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="3e68b-248">Additional resources</span></span>

* [<span data-ttu-id="3e68b-249">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3e68b-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3e68b-250">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3e68b-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_203.png

