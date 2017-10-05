---
title: 'Zelfstudie: Azure Active Directory-integratie met Capriza Platform | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Capriza Platform.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 48d92247-f00a-47b9-8d4e-137028d9e200
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 668c094d5330be1c5f71d51d2e76170dc69d1bce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-capriza-platform"></a><span data-ttu-id="446d7-103">Zelfstudie: Azure Active Directory-integratie met Capriza Platform</span><span class="sxs-lookup"><span data-stu-id="446d7-103">Tutorial: Azure Active Directory integration with Capriza Platform</span></span>

<span data-ttu-id="446d7-104">In deze zelfstudie leert u hoe Capriza Platform integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="446d7-104">In this tutorial, you learn how to integrate Capriza Platform with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="446d7-105">Capriza Platform integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="446d7-105">Integrating Capriza Platform with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="446d7-106">U kunt beheren in Azure AD die toegang tot Capriza Platform heeft</span><span class="sxs-lookup"><span data-stu-id="446d7-106">You can control in Azure AD who has access to Capriza Platform</span></span>
- <span data-ttu-id="446d7-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Capriza Platform (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="446d7-107">You can enable your users to automatically get signed-on to Capriza Platform (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="446d7-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="446d7-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="446d7-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="446d7-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="446d7-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="446d7-110">Prerequisites</span></span>

<span data-ttu-id="446d7-111">Voor het configureren van Azure AD-integratie met Capriza Platform, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="446d7-111">To configure Azure AD integration with Capriza Platform, you need the following items:</span></span>

- <span data-ttu-id="446d7-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="446d7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="446d7-113">Een Capriza Platform eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="446d7-113">A Capriza Platform single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="446d7-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="446d7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="446d7-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="446d7-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="446d7-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="446d7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="446d7-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="446d7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="446d7-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="446d7-118">Scenario description</span></span>
<span data-ttu-id="446d7-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="446d7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="446d7-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="446d7-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="446d7-121">Capriza Platform uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="446d7-121">Adding Capriza Platform from the gallery</span></span>
2. <span data-ttu-id="446d7-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="446d7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-capriza-platform-from-the-gallery"></a><span data-ttu-id="446d7-123">Capriza Platform uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="446d7-123">Adding Capriza Platform from the gallery</span></span>
<span data-ttu-id="446d7-124">Voor het configureren van de integratie van Capriza Platform in Azure AD, moet u Capriza Platform uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="446d7-124">To configure the integration of Capriza Platform into Azure AD, you need to add Capriza Platform from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="446d7-125">**Als u wilt toevoegen Capriza Platform uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="446d7-125">**To add Capriza Platform from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="446d7-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="446d7-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="446d7-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="446d7-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="446d7-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="446d7-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="446d7-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="446d7-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="446d7-133">Typ in het zoekvak **Capriza Platform**.</span><span class="sxs-lookup"><span data-stu-id="446d7-133">In the search box, type **Capriza Platform**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_search.png)

5. <span data-ttu-id="446d7-135">Selecteer in het deelvenster resultaten **Capriza Platform**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="446d7-135">In the results panel, select **Capriza Platform**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="446d7-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="446d7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="446d7-138">In deze sectie kunt u configureren en test eenmalige aanmelding Azure AD met Capriza Platform op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="446d7-138">In this section, you configure and test Azure AD single sign-on with Capriza Platform based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="446d7-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Capriza Platform is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="446d7-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Capriza Platform is to a user in Azure AD.</span></span> <span data-ttu-id="446d7-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Capriza Platform tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="446d7-140">In other words, a link relationship between an Azure AD user and the related user in Capriza Platform needs to be established.</span></span>

<span data-ttu-id="446d7-141">Wijs in Capriza Platform, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="446d7-141">In Capriza Platform, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="446d7-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Capriza Platform, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="446d7-142">To configure and test Azure AD single sign-on with Capriza Platform, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="446d7-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="446d7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="446d7-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="446d7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="446d7-145">**[Maken van een testgebruiker Capriza Platform](#creating-a-capriza-platform-test-user)**  - Capriza-Platform die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="446d7-145">**[Creating a Capriza Platform test user](#creating-a-capriza-platform-test-user)** - to have a counterpart of Britta Simon in Capriza Platform that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="446d7-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="446d7-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="446d7-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="446d7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="446d7-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="446d7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="446d7-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Capriza Platform configureren.</span><span class="sxs-lookup"><span data-stu-id="446d7-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Capriza Platform application.</span></span>

<span data-ttu-id="446d7-150">**Voor het configureren van Azure AD eenmalige aanmelding met Capriza Platform, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="446d7-150">**To configure Azure AD single sign-on with Capriza Platform, perform the following steps:**</span></span>

1. <span data-ttu-id="446d7-151">In de Azure-portal op de **Capriza Platform** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="446d7-151">In the Azure portal, on the **Capriza Platform** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="446d7-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="446d7-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_samlbase.png)

3. <span data-ttu-id="446d7-155">Op de **Capriza Platform domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="446d7-155">On the **Capriza Platform Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_url.png)

    <span data-ttu-id="446d7-157">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<companyname>.capriza.com/<tenantid>`</span><span class="sxs-lookup"><span data-stu-id="446d7-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.capriza.com/<tenantid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="446d7-158">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="446d7-158">This value is not real.</span></span> <span data-ttu-id="446d7-159">Deze waarde bijwerken met de werkelijke URL voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="446d7-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="446d7-160">Neem contact op met [Capriza Platform Client ondersteuningsteam](mailTo:support@capriza.com) deze waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="446d7-160">Contact [Capriza Platform Client support team](mailTo:support@capriza.com) to get this value.</span></span> 

4. <span data-ttu-id="446d7-161">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="446d7-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_certificate.png) 

5. <span data-ttu-id="446d7-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="446d7-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-capriza-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="446d7-165">Op de **Capriza platformconfiguratie** sectie, klikt u op **Capriza Platform configureren** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="446d7-165">On the **Capriza Platform Configuration** section, click **Configure Capriza Platform** to open **Configure sign-on** window.</span></span> <span data-ttu-id="446d7-166">Kopieer de **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="446d7-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_configure.png) 

7. <span data-ttu-id="446d7-168">Eenmalige aanmelding configureren op **Capriza Platform** zijde, moet u de gedownloade verzenden **certificaat**, **Sign-Out URL**, **SAML entiteit-ID** en **SAML Single Sign-On Service-URL** naar [Capriza Platform ondersteuningsteam](mailTo:support@capriza.com).</span><span class="sxs-lookup"><span data-stu-id="446d7-168">To configure single sign-on on **Capriza Platform** side, you need to send the downloaded **Certificate**, **Sign-Out URL**, **SAML Entity ID** and **SAML Single Sign-On Service URL** to [Capriza Platform support team](mailTo:support@capriza.com).</span></span> <span data-ttu-id="446d7-169">Ze deze instelling zodat de SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="446d7-169">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="446d7-170">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="446d7-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="446d7-171">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="446d7-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="446d7-172">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="446d7-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="446d7-173">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="446d7-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="446d7-174">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="446d7-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="446d7-176">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="446d7-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="446d7-177">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="446d7-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-capriza-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="446d7-179">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="446d7-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-capriza-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="446d7-181">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="446d7-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-capriza-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="446d7-183">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="446d7-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-capriza-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="446d7-185">a.</span><span class="sxs-lookup"><span data-stu-id="446d7-185">a.</span></span> <span data-ttu-id="446d7-186">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="446d7-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="446d7-187">b.</span><span class="sxs-lookup"><span data-stu-id="446d7-187">b.</span></span> <span data-ttu-id="446d7-188">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="446d7-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="446d7-189">c.</span><span class="sxs-lookup"><span data-stu-id="446d7-189">c.</span></span> <span data-ttu-id="446d7-190">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="446d7-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="446d7-191">d.</span><span class="sxs-lookup"><span data-stu-id="446d7-191">d.</span></span> <span data-ttu-id="446d7-192">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="446d7-192">Click **Create**.</span></span>
 
### <a name="creating-a-capriza-platform-test-user"></a><span data-ttu-id="446d7-193">Maken van een testgebruiker Capriza Platform</span><span class="sxs-lookup"><span data-stu-id="446d7-193">Creating a Capriza Platform test user</span></span>

<span data-ttu-id="446d7-194">Het doel van deze sectie is het maken van een gebruiker Britta Simon in Capriza genoemd.</span><span class="sxs-lookup"><span data-stu-id="446d7-194">The objective of this section is to create a user called Britta Simon in Capriza.</span></span> <span data-ttu-id="446d7-195">Capriza ondersteunt just-in-time-inrichting, dit is standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="446d7-195">Capriza supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="446d7-196">**Zorg dat de domeinnaam van uw is geconfigureerd met Capriza voor gebruikers inrichten. Na die alleen de just in time gebruikersaanvragen werkt.**</span><span class="sxs-lookup"><span data-stu-id="446d7-196">**Please make sure that your domain name is configured with Capriza for user provisioning. After that only the just-in-time user provisioning will work.**</span></span>

<span data-ttu-id="446d7-197">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="446d7-197">There is no action item for you in this section.</span></span> <span data-ttu-id="446d7-198">Een nieuwe gebruiker wordt gemaakt tijdens een poging tot toegang tot Capriza als deze nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="446d7-198">A new user will be created during an attempt to access Capriza if it doesn't exist yet.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="446d7-199">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="446d7-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="446d7-200">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Capriza Platform.</span><span class="sxs-lookup"><span data-stu-id="446d7-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Capriza Platform.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="446d7-202">**Britta Simon om aan te wijzen Capriza Platform, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="446d7-202">**To assign Britta Simon to Capriza Platform, perform the following steps:**</span></span>

1. <span data-ttu-id="446d7-203">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="446d7-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="446d7-205">Selecteer in de lijst met toepassingen **Capriza Platform**.</span><span class="sxs-lookup"><span data-stu-id="446d7-205">In the applications list, select **Capriza Platform**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_app.png) 

3. <span data-ttu-id="446d7-207">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="446d7-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="446d7-209">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="446d7-209">Click **Add** button.</span></span> <span data-ttu-id="446d7-210">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="446d7-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="446d7-212">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="446d7-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="446d7-213">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="446d7-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="446d7-214">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="446d7-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="446d7-215">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="446d7-215">Testing single sign-on</span></span>

<span data-ttu-id="446d7-216">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="446d7-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="446d7-217">Als u op de tegel Capriza Platform in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Capriza.</span><span class="sxs-lookup"><span data-stu-id="446d7-217">When you click the Capriza Platform tile in the Access Panel, you should get automatically signed-on to your Capriza application.</span></span> <span data-ttu-id="446d7-218">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="446d7-218">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="446d7-219">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="446d7-219">Additional resources</span></span>

* [<span data-ttu-id="446d7-220">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="446d7-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="446d7-221">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="446d7-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_203.png

