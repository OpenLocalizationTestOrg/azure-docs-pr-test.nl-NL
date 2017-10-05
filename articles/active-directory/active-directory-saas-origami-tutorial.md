---
title: 'Zelfstudie: Azure Active Directory-integratie met Origami | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Origami.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a28bb0ba-b564-46ba-accc-e587699295d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 3420409b72ff032e64ac59365083dd141dfc3c1b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-origami"></a><span data-ttu-id="5fe51-103">Zelfstudie: Azure Active Directory-integratie met Origami</span><span class="sxs-lookup"><span data-stu-id="5fe51-103">Tutorial: Azure Active Directory integration with Origami</span></span>

<span data-ttu-id="5fe51-104">In deze zelfstudie leert u hoe Origami integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5fe51-104">In this tutorial, you learn how to integrate Origami with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5fe51-105">Origami integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="5fe51-105">Integrating Origami with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5fe51-106">U kunt beheren in Azure AD die toegang tot Origami heeft</span><span class="sxs-lookup"><span data-stu-id="5fe51-106">You can control in Azure AD who has access to Origami</span></span>
- <span data-ttu-id="5fe51-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Origami (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="5fe51-107">You can enable your users to automatically get signed-on to Origami (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5fe51-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="5fe51-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="5fe51-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5fe51-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5fe51-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="5fe51-110">Prerequisites</span></span>

<span data-ttu-id="5fe51-111">Voor het configureren van Azure AD-integratie met Origami, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="5fe51-111">To configure Azure AD integration with Origami, you need the following items:</span></span>

- <span data-ttu-id="5fe51-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="5fe51-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5fe51-113">Een Origami eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="5fe51-113">An Origami single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5fe51-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="5fe51-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5fe51-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="5fe51-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5fe51-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="5fe51-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5fe51-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5fe51-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5fe51-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="5fe51-118">Scenario description</span></span>
<span data-ttu-id="5fe51-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="5fe51-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5fe51-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="5fe51-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5fe51-121">Origami uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="5fe51-121">Adding Origami from the gallery</span></span>
2. <span data-ttu-id="5fe51-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="5fe51-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-origami-from-the-gallery"></a><span data-ttu-id="5fe51-123">Origami uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="5fe51-123">Adding Origami from the gallery</span></span>
<span data-ttu-id="5fe51-124">Voor het configureren van de integratie van Origami in Azure AD, moet u Origami uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="5fe51-124">To configure the integration of Origami into Azure AD, you need to add Origami from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5fe51-125">**Als u wilt toevoegen Origami uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="5fe51-125">**To add Origami from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5fe51-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="5fe51-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5fe51-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="5fe51-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5fe51-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="5fe51-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="5fe51-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="5fe51-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="5fe51-133">Typ in het zoekvak **Origami**.</span><span class="sxs-lookup"><span data-stu-id="5fe51-133">In the search box, type **Origami**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-origami-tutorial/tutorial_origami_search.png)

5. <span data-ttu-id="5fe51-135">Selecteer in het deelvenster resultaten **Origami**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="5fe51-135">In the results panel, select **Origami**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-origami-tutorial/tutorial_origami_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5fe51-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="5fe51-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5fe51-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Origami op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="5fe51-138">In this section, you configure and test Azure AD single sign-on with Origami based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5fe51-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Origami is aan een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5fe51-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Origami is to a user in Azure AD.</span></span> <span data-ttu-id="5fe51-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Origami tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="5fe51-140">In other words, a link relationship between an Azure AD user and the related user in Origami needs to be established.</span></span>

<span data-ttu-id="5fe51-141">Wijs in Origami, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="5fe51-141">In Origami, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="5fe51-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Origami, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="5fe51-142">To configure and test Azure AD single sign-on with Origami, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5fe51-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="5fe51-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5fe51-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5fe51-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5fe51-145">**[Maken van een testgebruiker Origami](#creating-an-origami-test-user)**  - Origami die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="5fe51-145">**[Creating an Origami test user](#creating-an-origami-test-user)** - to have a counterpart of Britta Simon in Origami that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5fe51-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="5fe51-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5fe51-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="5fe51-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5fe51-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="5fe51-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5fe51-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Origami configureren.</span><span class="sxs-lookup"><span data-stu-id="5fe51-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Origami application.</span></span>

<span data-ttu-id="5fe51-150">**Voor het configureren van Azure AD eenmalige aanmelding met Origami, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="5fe51-150">**To configure Azure AD single sign-on with Origami, perform the following steps:**</span></span>

1. <span data-ttu-id="5fe51-151">In de Azure-portal op de **Origami** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="5fe51-151">In the Azure portal, on the **Origami** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="5fe51-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="5fe51-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-origami-tutorial/tutorial_origami_samlbase.png)

3. <span data-ttu-id="5fe51-155">Op de **Origami domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="5fe51-155">On the **Origami Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-origami-tutorial/tutorial_origami_url.png)

    <span data-ttu-id="5fe51-157">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://live.origamirisk.com/origami/account/login?account=<companyname>`</span><span class="sxs-lookup"><span data-stu-id="5fe51-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://live.origamirisk.com/origami/account/login?account=<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5fe51-158">De waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="5fe51-158">The value is not real.</span></span> <span data-ttu-id="5fe51-159">Werk de waarde met de werkelijke URL voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="5fe51-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="5fe51-160">Neem contact op met [Origami Client ondersteuningsteam](https://wordpress.org/support/theme/origami) de waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="5fe51-160">Contact [Origami Client support team](https://wordpress.org/support/theme/origami) to get the value.</span></span> 
 
4. <span data-ttu-id="5fe51-161">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="5fe51-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-origami-tutorial/tutorial_origami_certificate.png) 

5. <span data-ttu-id="5fe51-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="5fe51-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-origami-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5fe51-165">Op de **Origami configuratie** sectie, klikt u op **Origami configureren** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="5fe51-165">On the **Origami Configuration** section, click **Configure Origami** to open **Configure sign-on** window.</span></span> <span data-ttu-id="5fe51-166">Kopieer de **Sign-Out URL's, en SAML Single Sign-On Service** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="5fe51-166">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-origami-tutorial/tutorial_origami_configure.png) 

7. <span data-ttu-id="5fe51-168">Aanmelden bij de Origami-account met beheerdersrechten.</span><span class="sxs-lookup"><span data-stu-id="5fe51-168">Log in to the Origami account with Admin rights.</span></span>

8. <span data-ttu-id="5fe51-169">Klik in het menu bovenaan op **Admin**.</span><span class="sxs-lookup"><span data-stu-id="5fe51-169">In the menu on the top, click **Admin**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-origami-tutorial/tutorial_origami_51.png)

9. <span data-ttu-id="5fe51-171">Op de pagina van het dialoogvenster Single Sign in Setup de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="5fe51-171">On the Single Sign On Setup dialog page, perform the following steps:</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-origami-tutorial/tutorial_origami_531.png)

    <span data-ttu-id="5fe51-173">a.</span><span class="sxs-lookup"><span data-stu-id="5fe51-173">a.</span></span> <span data-ttu-id="5fe51-174">Selecteer **eenmalige aanmelding inschakelen op**.</span><span class="sxs-lookup"><span data-stu-id="5fe51-174">Select **Enable Single Sign On**.</span></span>

    <span data-ttu-id="5fe51-175">b.</span><span class="sxs-lookup"><span data-stu-id="5fe51-175">b.</span></span> <span data-ttu-id="5fe51-176">In de **van de identiteitsprovider aanmelden pagina-URL** textbox, plak de waarde van **SAML Single Sign-On Service-URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="5fe51-176">In the **Identity Provider's Sign-in Page URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="5fe51-177">c.</span><span class="sxs-lookup"><span data-stu-id="5fe51-177">c.</span></span> <span data-ttu-id="5fe51-178">In de **Sign-out pagina-URL van de identiteitsprovider** textbox, plak de waarde van **Sign-Out URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="5fe51-178">In the **Identity Provider's Sign-out Page URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="5fe51-179">d.</span><span class="sxs-lookup"><span data-stu-id="5fe51-179">d.</span></span> <span data-ttu-id="5fe51-180">Klik op **Bladeren** voor het uploaden van het certificaat dat u hebt gedownload vanuit de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="5fe51-180">Click **Browse** to upload the certificate you have downloaded from the Azure portal.</span></span>

    <span data-ttu-id="5fe51-181">e.</span><span class="sxs-lookup"><span data-stu-id="5fe51-181">e.</span></span> <span data-ttu-id="5fe51-182">Klik op **wijzigingen opslaan**.</span><span class="sxs-lookup"><span data-stu-id="5fe51-182">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="5fe51-183">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="5fe51-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5fe51-184">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="5fe51-184">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5fe51-185">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5fe51-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5fe51-186">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="5fe51-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="5fe51-187">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="5fe51-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="5fe51-189">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="5fe51-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5fe51-190">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="5fe51-190">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-origami-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5fe51-192">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="5fe51-192">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-origami-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5fe51-194">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="5fe51-194">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-origami-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5fe51-196">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="5fe51-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-origami-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5fe51-198">a.</span><span class="sxs-lookup"><span data-stu-id="5fe51-198">a.</span></span> <span data-ttu-id="5fe51-199">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5fe51-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5fe51-200">b.</span><span class="sxs-lookup"><span data-stu-id="5fe51-200">b.</span></span> <span data-ttu-id="5fe51-201">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5fe51-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5fe51-202">c.</span><span class="sxs-lookup"><span data-stu-id="5fe51-202">c.</span></span> <span data-ttu-id="5fe51-203">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="5fe51-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5fe51-204">d.</span><span class="sxs-lookup"><span data-stu-id="5fe51-204">d.</span></span> <span data-ttu-id="5fe51-205">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="5fe51-205">Click **Create**.</span></span>
 
### <a name="creating-an-origami-test-user"></a><span data-ttu-id="5fe51-206">Een testgebruiker Origami maken</span><span class="sxs-lookup"><span data-stu-id="5fe51-206">Creating an Origami test user</span></span>

<span data-ttu-id="5fe51-207">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in Origami maken.</span><span class="sxs-lookup"><span data-stu-id="5fe51-207">In this section, you create a user called Britta Simon in Origami.</span></span> 

1. <span data-ttu-id="5fe51-208">Aanmelden bij de Origami-account met beheerdersrechten.</span><span class="sxs-lookup"><span data-stu-id="5fe51-208">Log in to the Origami account with Admin rights.</span></span>

2. <span data-ttu-id="5fe51-209">Klik in het menu bovenaan op **Admin**.</span><span class="sxs-lookup"><span data-stu-id="5fe51-209">In the menu on the top, click **Admin**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-origami-tutorial/tutorial_origami_51.png)

3. <span data-ttu-id="5fe51-211">Op de **gebruikers en beveiliging** dialoogvenster, klikt u op **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="5fe51-211">On the **Users and Security** dialog, click **Users**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-origami-tutorial/tutorial_origami_54.png)

4. <span data-ttu-id="5fe51-213">Klik op **nieuwe gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="5fe51-213">Click **Add New User**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-origami-tutorial/tutorial_origami_55.png)

5. <span data-ttu-id="5fe51-215">Voer de volgende stappen uit in het dialoogvenster Nieuwe gebruiker toevoegen:</span><span class="sxs-lookup"><span data-stu-id="5fe51-215">On the Add New User dialog, perform the following steps:</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-origami-tutorial/tutorial_origami_56.png)

    <span data-ttu-id="5fe51-217">a.</span><span class="sxs-lookup"><span data-stu-id="5fe51-217">a.</span></span> <span data-ttu-id="5fe51-218">In de **gebruikersnaam** textbox, voer het e-mailadres van de gebruiker zoals  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="5fe51-218">In the **User Name** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="5fe51-219">b.</span><span class="sxs-lookup"><span data-stu-id="5fe51-219">b.</span></span> <span data-ttu-id="5fe51-220">In de **wachtwoord** textbox, typ een wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="5fe51-220">In the **Password** textbox, type a password.</span></span>

    <span data-ttu-id="5fe51-221">c.</span><span class="sxs-lookup"><span data-stu-id="5fe51-221">c.</span></span> <span data-ttu-id="5fe51-222">In de **wachtwoord bevestigen** textbox Typ nogmaals het wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="5fe51-222">In the **Confirm Password** textbox, type the password again.</span></span>

    <span data-ttu-id="5fe51-223">d.</span><span class="sxs-lookup"><span data-stu-id="5fe51-223">d.</span></span> <span data-ttu-id="5fe51-224">In de **voornaam** textbox, voer de voornaam van de gebruiker zoals **Britta**.</span><span class="sxs-lookup"><span data-stu-id="5fe51-224">In the **First Name** textbox, enter the first name of user like **Britta**.</span></span>

    <span data-ttu-id="5fe51-225">e.</span><span class="sxs-lookup"><span data-stu-id="5fe51-225">e.</span></span> <span data-ttu-id="5fe51-226">In de **achternaam** textbox, geef de achternaam van de gebruiker zoals **Simon**.</span><span class="sxs-lookup"><span data-stu-id="5fe51-226">In the **Last Name** textbox, enter the last name of user like **Simon**.</span></span>

    <span data-ttu-id="5fe51-227">f.</span><span class="sxs-lookup"><span data-stu-id="5fe51-227">f.</span></span> <span data-ttu-id="5fe51-228">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="5fe51-228">Click **Save**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-origami-tutorial/tutorial_origami_57.png)

6. <span data-ttu-id="5fe51-230">Wijs **gebruikersrollen** en **clienttoegang** aan de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="5fe51-230">Assign **User Roles** and **Client Access** to the user.</span></span> 
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-origami-tutorial/tutorial_origami_58.png)

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5fe51-232">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="5fe51-232">Assigning the Azure AD test user</span></span>

<span data-ttu-id="5fe51-233">In deze sectie maakt inschakelen u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Origami.</span><span class="sxs-lookup"><span data-stu-id="5fe51-233">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Origami.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="5fe51-235">**Britta Simon om aan te wijzen Origami, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="5fe51-235">**To assign Britta Simon to Origami, perform the following steps:**</span></span>

1. <span data-ttu-id="5fe51-236">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="5fe51-236">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="5fe51-238">Selecteer in de lijst met toepassingen **Origami**.</span><span class="sxs-lookup"><span data-stu-id="5fe51-238">In the applications list, select **Origami**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-origami-tutorial/tutorial_origami_app.png) 

3. <span data-ttu-id="5fe51-240">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="5fe51-240">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="5fe51-242">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="5fe51-242">Click **Add** button.</span></span> <span data-ttu-id="5fe51-243">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="5fe51-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="5fe51-245">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="5fe51-245">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5fe51-246">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="5fe51-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5fe51-247">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="5fe51-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5fe51-248">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="5fe51-248">Testing single sign-on</span></span>

<span data-ttu-id="5fe51-249">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="5fe51-249">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="5fe51-250">Als u op de tegel Origami in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Origami.</span><span class="sxs-lookup"><span data-stu-id="5fe51-250">When you click the Origami tile in the Access Panel, you should get automatically signed-on to your Origami application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5fe51-251">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="5fe51-251">Additional resources</span></span>

* [<span data-ttu-id="5fe51-252">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5fe51-252">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5fe51-253">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5fe51-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-origami-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-origami-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-origami-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-origami-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-origami-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-origami-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-origami-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-origami-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-origami-tutorial/tutorial_general_203.png

