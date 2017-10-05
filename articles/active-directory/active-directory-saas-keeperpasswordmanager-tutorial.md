---
title: 'Zelfstudie: Azure Active Directory-integratie met wachtwoordbeheer houder & digitale kluis | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en houder wachtwoordbeheer & digitale kluis.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e1a98f6a-2dae-4734-bdbf-4fba742a61d2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 36504a281756b980e3348e7f892ba08821873b52
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-keeper-password-manager--digital-vault"></a><span data-ttu-id="28e71-103">Zelfstudie: Azure Active Directory-integratie met wachtwoordbeheer houder & digitale kluis</span><span class="sxs-lookup"><span data-stu-id="28e71-103">Tutorial: Azure Active Directory integration with Keeper Password Manager & Digital Vault</span></span>

<span data-ttu-id="28e71-104">In deze zelfstudie leert u hoe houder wachtwoordbeheer & digitale kluis integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="28e71-104">In this tutorial, you learn how to integrate Keeper Password Manager & Digital Vault with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="28e71-105">Wachtwoordbeheer houder & digitale kluis integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="28e71-105">Integrating Keeper Password Manager & Digital Vault with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="28e71-106">U kunt beheren in Azure AD die toegang tot de houder wachtwoordbeheer & digitale kluis heeft</span><span class="sxs-lookup"><span data-stu-id="28e71-106">You can control in Azure AD who has access to Keeper Password Manager & Digital Vault</span></span>
- <span data-ttu-id="28e71-107">U kunt uw gebruikers automatisch ophalen aangemeld bij houder wachtwoordbeheer & digitale kluis (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="28e71-107">You can enable your users to automatically get signed-on to Keeper Password Manager & Digital Vault (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="28e71-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="28e71-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="28e71-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="28e71-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="28e71-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="28e71-110">Prerequisites</span></span>

<span data-ttu-id="28e71-111">Voor het configureren van Azure AD-integratie met wachtwoordbeheer houder & digitale kluis, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="28e71-111">To configure Azure AD integration with Keeper Password Manager & Digital Vault, you need the following items:</span></span>

- <span data-ttu-id="28e71-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="28e71-112">An Azure AD subscription</span></span>
- <span data-ttu-id="28e71-113">Een houder wachtwoordbeheer & digitale kluis eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="28e71-113">A Keeper Password Manager & Digital Vault single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="28e71-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="28e71-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="28e71-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="28e71-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="28e71-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="28e71-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="28e71-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="28e71-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="28e71-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="28e71-118">Scenario description</span></span>
<span data-ttu-id="28e71-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="28e71-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="28e71-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="28e71-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="28e71-121">Wachtwoordbeheer houder & digitale kluis uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="28e71-121">Adding Keeper Password Manager & Digital Vault from the gallery</span></span>
2. <span data-ttu-id="28e71-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="28e71-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-keeper-password-manager--digital-vault-from-the-gallery"></a><span data-ttu-id="28e71-123">Wachtwoordbeheer houder & digitale kluis uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="28e71-123">Adding Keeper Password Manager & Digital Vault from the gallery</span></span>
<span data-ttu-id="28e71-124">Voor het configureren van de integratie van houder wachtwoordbeheer & digitale kluis in Azure AD, moet u wachtwoordbeheer houder & digitale kluis uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="28e71-124">To configure the integration of Keeper Password Manager & Digital Vault into Azure AD, you need to add Keeper Password Manager & Digital Vault from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="28e71-125">**Als u wilt toevoegen houder wachtwoordbeheer & digitale kluis uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="28e71-125">**To add Keeper Password Manager & Digital Vault from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="28e71-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="28e71-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="28e71-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="28e71-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="28e71-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="28e71-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="28e71-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="28e71-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="28e71-133">Typ in het zoekvak **houder wachtwoordbeheer & digitale kluis**.</span><span class="sxs-lookup"><span data-stu-id="28e71-133">In the search box, type **Keeper Password Manager & Digital Vault**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_search.png)

5. <span data-ttu-id="28e71-135">Selecteer in het deelvenster resultaten **houder wachtwoordbeheer & digitale kluis**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="28e71-135">In the results panel, select **Keeper Password Manager & Digital Vault**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="28e71-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="28e71-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="28e71-138">In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met wachtwoordbeheer houder & digitale kluis op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="28e71-138">In this section, you configure and test Azure AD single sign-on with Keeper Password Manager & Digital Vault based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="28e71-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in houder wachtwoordbeheer & digitale kluis in Azure AD voor een gebruiker is.</span><span class="sxs-lookup"><span data-stu-id="28e71-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Keeper Password Manager & Digital Vault is to a user in Azure AD.</span></span> <span data-ttu-id="28e71-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in de houder wachtwoordbeheer & digitale kluis tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="28e71-140">In other words, a link relationship between an Azure AD user and the related user in Keeper Password Manager & Digital Vault needs to be established.</span></span>

<span data-ttu-id="28e71-141">Wijs in houder wachtwoordbeheer & digitale kluis, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="28e71-141">In Keeper Password Manager & Digital Vault, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="28e71-142">Om te configureren en testen van Azure AD eenmalige aanmelding met wachtwoordbeheer houder & digitale kluis, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="28e71-142">To configure and test Azure AD single sign-on with Keeper Password Manager & Digital Vault, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="28e71-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="28e71-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="28e71-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="28e71-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="28e71-145">**[Maken van een testgebruiker houder wachtwoordbeheer & digitale kluis](#creating-a-keeperpasswordmanager-test-user)**  - hebben een equivalent van Britta Simon in houder wachtwoordbeheer & digitale kluis die is gekoppeld aan de Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="28e71-145">**[Creating a Keeper Password Manager & Digital Vault test user](#creating-a-keeperpasswordmanager-test-user)** - to have a counterpart of Britta Simon in Keeper Password Manager & Digital Vault that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="28e71-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="28e71-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="28e71-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="28e71-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="28e71-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="28e71-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="28e71-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw toepassing houder wachtwoordbeheer & digitale kluis.</span><span class="sxs-lookup"><span data-stu-id="28e71-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Keeper Password Manager & Digital Vault application.</span></span>

<span data-ttu-id="28e71-150">**Voor het configureren van Azure AD eenmalige aanmelding met wachtwoordbeheer houder & digitale kluis, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="28e71-150">**To configure Azure AD single sign-on with Keeper Password Manager & Digital Vault, perform the following steps:**</span></span>

1. <span data-ttu-id="28e71-151">In de Azure-portal op de **houder wachtwoordbeheer & digitale kluis** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="28e71-151">In the Azure portal, on the **Keeper Password Manager & Digital Vault** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="28e71-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="28e71-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_samlbase.png)

3. <span data-ttu-id="28e71-155">Op de **houder wachtwoordbeheer & digitale kluis domein en URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="28e71-155">On the **Keeper Password Manager & Digital Vault Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_url.png)

    <span data-ttu-id="28e71-157">a.</span><span class="sxs-lookup"><span data-stu-id="28e71-157">a.</span></span> <span data-ttu-id="28e71-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://{SSO CONNECT SERVER}/sso-connect/saml/login`</span><span class="sxs-lookup"><span data-stu-id="28e71-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://{SSO CONNECT SERVER}/sso-connect/saml/login`</span></span>

    <span data-ttu-id="28e71-159">b.</span><span class="sxs-lookup"><span data-stu-id="28e71-159">b.</span></span> <span data-ttu-id="28e71-160">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://{SSO CONNECT SERVER}/sso-connect/saml/sso`</span><span class="sxs-lookup"><span data-stu-id="28e71-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://{SSO CONNECT SERVER}/sso-connect/saml/sso`</span></span>

    <span data-ttu-id="28e71-161">c.</span><span class="sxs-lookup"><span data-stu-id="28e71-161">c.</span></span> <span data-ttu-id="28e71-162">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://{SSO CONNECT SERVER}/sso-connect`</span><span class="sxs-lookup"><span data-stu-id="28e71-162">In the **Identifier** textbox, type a URL using the following pattern: `https://{SSO CONNECT SERVER}/sso-connect`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="28e71-163">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="28e71-163">These values are not real.</span></span> <span data-ttu-id="28e71-164">Deze waarden bijwerken met de werkelijke antwoord-URL en de aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="28e71-164">Update these values with the actual Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="28e71-165">Neem contact op met [houder wachtwoordbeheer & digitale kluis Client ondersteuningsteam](https://keepersecurity.com/contact.html) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="28e71-165">Contact [Keeper Password Manager & Digital Vault Client support team](https://keepersecurity.com/contact.html) to get these values.</span></span> 

4. <span data-ttu-id="28e71-166">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="28e71-166">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_certificate.png) 

5. <span data-ttu-id="28e71-168">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="28e71-168">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="28e71-170">Op de **houder wachtwoordbeheer & digitale kluis configuratie** sectie, klikt u op **houder wachtwoordbeheer configureren & digitale kluis** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="28e71-170">On the **Keeper Password Manager & Digital Vault Configuration** section, click **Configure Keeper Password Manager & Digital Vault** to open **Configure sign-on** window.</span></span> <span data-ttu-id="28e71-171">Kopieer de **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="28e71-171">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_configure.png) 

7. <span data-ttu-id="28e71-173">Eenmalige aanmelding configureren op **houder wachtwoordbeheer & digitale kluis configuratie** zijde, volg de richtlijnen gegeven op [houder Support Guide](https://keepersecurity.com/assets/pdf/SettingupAzurewithKeeperSSOConnect.pdf)</span><span class="sxs-lookup"><span data-stu-id="28e71-173">To configure single sign-on on **Keeper Password Manager & Digital Vault Configuration** side, follow the guidelines given at [Keeper Support Guide](https://keepersecurity.com/assets/pdf/SettingupAzurewithKeeperSSOConnect.pdf)</span></span>

> [!TIP]
> <span data-ttu-id="28e71-174">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="28e71-174">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="28e71-175">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="28e71-175">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="28e71-176">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="28e71-176">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="28e71-177">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="28e71-177">Creating an Azure AD test user</span></span>
<span data-ttu-id="28e71-178">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="28e71-178">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="28e71-180">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="28e71-180">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="28e71-181">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="28e71-181">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-keeperpasswordmanager-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="28e71-183">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="28e71-183">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-keeperpasswordmanager-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="28e71-185">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="28e71-185">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-keeperpasswordmanager-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="28e71-187">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="28e71-187">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-keeperpasswordmanager-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="28e71-189">a.</span><span class="sxs-lookup"><span data-stu-id="28e71-189">a.</span></span> <span data-ttu-id="28e71-190">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="28e71-190">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="28e71-191">b.</span><span class="sxs-lookup"><span data-stu-id="28e71-191">b.</span></span> <span data-ttu-id="28e71-192">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="28e71-192">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="28e71-193">c.</span><span class="sxs-lookup"><span data-stu-id="28e71-193">c.</span></span> <span data-ttu-id="28e71-194">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="28e71-194">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="28e71-195">d.</span><span class="sxs-lookup"><span data-stu-id="28e71-195">d.</span></span> <span data-ttu-id="28e71-196">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="28e71-196">Click **Create**.</span></span>
 
### <a name="creating-a-keeper-password-manager--digital-vault-test-user"></a><span data-ttu-id="28e71-197">Een testgebruiker houder wachtwoordbeheer & digitale kluis maken</span><span class="sxs-lookup"><span data-stu-id="28e71-197">Creating a Keeper Password Manager & Digital Vault test user</span></span>

<span data-ttu-id="28e71-198">Om Azure AD-gebruikers zich aanmelden bij de houder wachtwoordbeheer & digitale kluis, moeten ze worden ingericht in houder wachtwoordbeheer & digitale kluis.</span><span class="sxs-lookup"><span data-stu-id="28e71-198">To enable Azure AD users to log in to Keeper Password Manager & Digital Vault, they must be provisioned into Keeper Password Manager & Digital Vault.</span></span> <span data-ttu-id="28e71-199">Toepassing ondersteunt Just in tijd gebruikers inrichten en na verificatie gebruikers wordt in de toepassing automatisch gemaakt.</span><span class="sxs-lookup"><span data-stu-id="28e71-199">Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span></span> <span data-ttu-id="28e71-200">U kunt contact opnemen met [houder ondersteuning](https://keepersecurity.com/contact.html), als u wilt gebruikers handmatig instellen.</span><span class="sxs-lookup"><span data-stu-id="28e71-200">You can contact [Keeper Support](https://keepersecurity.com/contact.html), if you want to setup users manually.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="28e71-201">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="28e71-201">Assigning the Azure AD test user</span></span>

<span data-ttu-id="28e71-202">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan houder wachtwoordbeheer & digitale kluis.</span><span class="sxs-lookup"><span data-stu-id="28e71-202">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Keeper Password Manager & Digital Vault.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="28e71-204">**Britta Simon om aan te wijzen houder wachtwoordbeheer & digitale kluis, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="28e71-204">**To assign Britta Simon to Keeper Password Manager & Digital Vault, perform the following steps:**</span></span>

1. <span data-ttu-id="28e71-205">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="28e71-205">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="28e71-207">Selecteer in de lijst met toepassingen **houder wachtwoordbeheer & digitale kluis**.</span><span class="sxs-lookup"><span data-stu-id="28e71-207">In the applications list, select **Keeper Password Manager & Digital Vault**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_app.png) 

3. <span data-ttu-id="28e71-209">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="28e71-209">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="28e71-211">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="28e71-211">Click **Add** button.</span></span> <span data-ttu-id="28e71-212">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="28e71-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="28e71-214">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="28e71-214">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="28e71-215">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="28e71-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="28e71-216">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="28e71-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="28e71-217">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="28e71-217">Testing single sign-on</span></span>

<span data-ttu-id="28e71-218">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="28e71-218">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="28e71-219">Als u op de tegel houder wachtwoordbeheer & digitale kluis in het deelvenster toegang, krijgt u de aanmeldingspagina van houder wachtwoordbeheer & digitale kluis toepassing.</span><span class="sxs-lookup"><span data-stu-id="28e71-219">When you click the Keeper Password Manager & Digital Vault tile in the Access Panel, you should get login page of Keeper Password Manager & Digital Vault application.</span></span> <span data-ttu-id="28e71-220">Op de geslaagde verificatie, moet u in de toepassing ophalen.</span><span class="sxs-lookup"><span data-stu-id="28e71-220">Upon successful authentication, you should get into the application.</span></span> <span data-ttu-id="28e71-221">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="28e71-221">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="28e71-222">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="28e71-222">Additional resources</span></span>

* [<span data-ttu-id="28e71-223">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="28e71-223">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="28e71-224">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="28e71-224">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_203.png

