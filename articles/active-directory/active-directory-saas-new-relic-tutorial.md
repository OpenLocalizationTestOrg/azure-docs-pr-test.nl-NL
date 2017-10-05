---
title: 'Zelfstudie: Azure Active Directory-integratie met New Relic | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en de New Relic.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3186b9a8-f4d8-45e2-ad82-6275f95e7aa6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: jeedes
ms.openlocfilehash: 605e85c23a849f70fcc0237361d7a891f716ca3a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-new-relic"></a><span data-ttu-id="baa93-103">Zelfstudie: Azure Active Directory-integratie met New Relic</span><span class="sxs-lookup"><span data-stu-id="baa93-103">Tutorial: Azure Active Directory integration with New Relic</span></span>

<span data-ttu-id="baa93-104">In deze zelfstudie leert u hoe New Relic integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="baa93-104">In this tutorial, you learn how to integrate New Relic with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="baa93-105">New Relic integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="baa93-105">Integrating New Relic with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="baa93-106">U kunt beheren in Azure AD die toegang tot de New Relic heeft</span><span class="sxs-lookup"><span data-stu-id="baa93-106">You can control in Azure AD who has access to New Relic</span></span>
- <span data-ttu-id="baa93-107">U kunt uw gebruikers automatisch ophalen aangemeld bij New Relic (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="baa93-107">You can enable your users to automatically get signed-on to New Relic (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="baa93-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="baa93-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="baa93-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="baa93-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="baa93-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="baa93-110">Prerequisites</span></span>

<span data-ttu-id="baa93-111">Voor het configureren van Azure AD-integratie met New Relic, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="baa93-111">To configure Azure AD integration with New Relic, you need the following items:</span></span>

- <span data-ttu-id="baa93-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="baa93-112">An Azure AD subscription</span></span>
- <span data-ttu-id="baa93-113">Een New Relic eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="baa93-113">A New Relic single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="baa93-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="baa93-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="baa93-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="baa93-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="baa93-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="baa93-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="baa93-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="baa93-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="baa93-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="baa93-118">Scenario description</span></span>
<span data-ttu-id="baa93-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="baa93-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="baa93-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="baa93-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="baa93-121">New Relic uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="baa93-121">Adding New Relic from the gallery</span></span>
2. <span data-ttu-id="baa93-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="baa93-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-new-relic-from-the-gallery"></a><span data-ttu-id="baa93-123">New Relic uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="baa93-123">Adding New Relic from the gallery</span></span>
<span data-ttu-id="baa93-124">Voor het configureren van de integratie van New Relic in Azure AD, moet u New Relic uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="baa93-124">To configure the integration of New Relic into Azure AD, you need to add New Relic from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="baa93-125">**Als u wilt toevoegen New Relic uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="baa93-125">**To add New Relic from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="baa93-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="baa93-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="baa93-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="baa93-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="baa93-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="baa93-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="baa93-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="baa93-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="baa93-133">Typ in het zoekvak **New Relic**.</span><span class="sxs-lookup"><span data-stu-id="baa93-133">In the search box, type **New Relic**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_search.png)

5. <span data-ttu-id="baa93-135">Selecteer in het deelvenster resultaten **New Relic**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="baa93-135">In the results panel, select **New Relic**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="baa93-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="baa93-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="baa93-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met New Relic op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="baa93-138">In this section, you configure and test Azure AD single sign-on with New Relic based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="baa93-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in New Relic in Azure AD voor een gebruiker is.</span><span class="sxs-lookup"><span data-stu-id="baa93-139">For single sign-on to work, Azure AD needs to know what the counterpart user in New Relic is to a user in Azure AD.</span></span> <span data-ttu-id="baa93-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante New Relic-gebruiker worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="baa93-140">In other words, a link relationship between an Azure AD user and the related user in New Relic needs to be established.</span></span>

<span data-ttu-id="baa93-141">Wijs in New Relic de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="baa93-141">In New Relic, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="baa93-142">Om te configureren en testen van Azure AD eenmalige aanmelding met New Relic, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="baa93-142">To configure and test Azure AD single sign-on with New Relic, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="baa93-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="baa93-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="baa93-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="baa93-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="baa93-145">**[Maken van een New Relic-testgebruiker](#creating-a-new-relic-test-user)**  - New Relic die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="baa93-145">**[Creating a New Relic test user](#creating-a-new-relic-test-user)** - to have a counterpart of Britta Simon in New Relic that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="baa93-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="baa93-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="baa93-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="baa93-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="baa93-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="baa93-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="baa93-149">In deze sectie maakt u Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw toepassing New Relic.</span><span class="sxs-lookup"><span data-stu-id="baa93-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your New Relic application.</span></span>

<span data-ttu-id="baa93-150">**Voor het configureren van Azure AD eenmalige aanmelding met New Relic, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="baa93-150">**To configure Azure AD single sign-on with New Relic, perform the following steps:**</span></span>

1. <span data-ttu-id="baa93-151">In de Azure-portal op de **New Relic** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="baa93-151">In the Azure portal, on the **New Relic** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="baa93-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="baa93-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_samlbase.png)

3. <span data-ttu-id="baa93-155">Op de **nieuwe Relic domein en URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="baa93-155">On the **New Relic Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_url.png)

    <span data-ttu-id="baa93-157">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<subdomain>.newrelic.com`</span><span class="sxs-lookup"><span data-stu-id="baa93-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.newrelic.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="baa93-158">De waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="baa93-158">The value is not real.</span></span> <span data-ttu-id="baa93-159">Werk de waarde met de werkelijke URL voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="baa93-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="baa93-160">Neem contact op met [nieuwe Relic Client ondersteuningsteam](https://support.newrelic.com/) de waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="baa93-160">Contact [New Relic Client support team](https://support.newrelic.com/) to get the value.</span></span> 
 
4. <span data-ttu-id="baa93-161">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="baa93-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_certificate.png) 

5. <span data-ttu-id="baa93-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="baa93-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-new-relic-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="baa93-165">Op de **nieuwe Relic configuratie** sectie, klikt u op **New Relic configureren** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="baa93-165">On the **New Relic Configuration** section, click **Configure New Relic** to open **Configure sign-on** window.</span></span> <span data-ttu-id="baa93-166">Kopieer de **Sign-Out URL's, en SAML Single Sign-On Service** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="baa93-166">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_configure.png) 

7. <span data-ttu-id="baa93-168">In een ander browservenster, meld u aan bij uw **New Relic** bedrijf site als administrator.</span><span class="sxs-lookup"><span data-stu-id="baa93-168">In a different web browser window, sign on to your **New Relic** company site as administrator.</span></span>

8. <span data-ttu-id="baa93-169">Klik in het menu bovenaan op **Accountinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="baa93-169">In the menu on the top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="baa93-170">![Instellingen account](./media/active-directory-saas-new-relic-tutorial/ic797036.png "Accountinstellingen")</span><span class="sxs-lookup"><span data-stu-id="baa93-170">![Account Settings](./media/active-directory-saas-new-relic-tutorial/ic797036.png "Account Settings")</span></span>

9. <span data-ttu-id="baa93-171">Klik op de **beveiligings- en** tabblad en klik vervolgens op de **eenmalige aanmelding** tabblad.</span><span class="sxs-lookup"><span data-stu-id="baa93-171">Click the **Security and authentication** tab, and then click the **Single sign on** tab.</span></span>
   
    <span data-ttu-id="baa93-172">![Eenmalige aanmelding](./media/active-directory-saas-new-relic-tutorial/ic797037.png "eenmalige aanmelding")</span><span class="sxs-lookup"><span data-stu-id="baa93-172">![Single Sign-On](./media/active-directory-saas-new-relic-tutorial/ic797037.png "Single Sign-On")</span></span>

10. <span data-ttu-id="baa93-173">Voer de volgende stappen uit op de pagina van het dialoogvenster SAML:</span><span class="sxs-lookup"><span data-stu-id="baa93-173">On the SAML dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="baa93-174">![SAML](./media/active-directory-saas-new-relic-tutorial/ic797038.png "SAML")</span><span class="sxs-lookup"><span data-stu-id="baa93-174">![SAML](./media/active-directory-saas-new-relic-tutorial/ic797038.png "SAML")</span></span>
   
   <span data-ttu-id="baa93-175">a.</span><span class="sxs-lookup"><span data-stu-id="baa93-175">a.</span></span> <span data-ttu-id="baa93-176">Klik op **bestand kiezen** om uw gedownloade Azure Active Directory-certificaat te uploaden.</span><span class="sxs-lookup"><span data-stu-id="baa93-176">Click **Choose File** to upload your downloaded Azure Active Directory certificate.</span></span>

   <span data-ttu-id="baa93-177">b.</span><span class="sxs-lookup"><span data-stu-id="baa93-177">b.</span></span> <span data-ttu-id="baa93-178">In de **externe aanmeldings-URL** textbox, plak de waarde van **SAML Single Sign-On Service-URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="baa93-178">In the **Remote login URL** textbox,  paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="baa93-179">c.</span><span class="sxs-lookup"><span data-stu-id="baa93-179">c.</span></span> <span data-ttu-id="baa93-180">In de **afmelding aanvoer URL** textbox, plak de waarde van **Sign-Out URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="baa93-180">In the **Logout landing URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

   <span data-ttu-id="baa93-181">d.</span><span class="sxs-lookup"><span data-stu-id="baa93-181">d.</span></span> <span data-ttu-id="baa93-182">Klik op **wijzigingen opslaan**.</span><span class="sxs-lookup"><span data-stu-id="baa93-182">Click **Save my changes**.</span></span>

> [!TIP]
> <span data-ttu-id="baa93-183">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="baa93-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="baa93-184">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="baa93-184">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="baa93-185">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="baa93-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="baa93-186">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="baa93-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="baa93-187">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="baa93-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="baa93-189">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="baa93-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="baa93-190">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="baa93-190">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-new-relic-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="baa93-192">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="baa93-192">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-new-relic-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="baa93-194">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="baa93-194">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-new-relic-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="baa93-196">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="baa93-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-new-relic-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="baa93-198">a.</span><span class="sxs-lookup"><span data-stu-id="baa93-198">a.</span></span> <span data-ttu-id="baa93-199">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="baa93-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="baa93-200">b.</span><span class="sxs-lookup"><span data-stu-id="baa93-200">b.</span></span> <span data-ttu-id="baa93-201">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="baa93-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="baa93-202">c.</span><span class="sxs-lookup"><span data-stu-id="baa93-202">c.</span></span> <span data-ttu-id="baa93-203">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="baa93-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="baa93-204">d.</span><span class="sxs-lookup"><span data-stu-id="baa93-204">d.</span></span> <span data-ttu-id="baa93-205">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="baa93-205">Click **Create**.</span></span>
 
### <a name="creating-a-new-relic-test-user"></a><span data-ttu-id="baa93-206">De gebruiker van een New Relic-test maken</span><span class="sxs-lookup"><span data-stu-id="baa93-206">Creating a New Relic test user</span></span>

<span data-ttu-id="baa93-207">Om Azure Active Directory-gebruikers zich aanmelden bij de New Relic inschakelt, moeten ze worden ingericht in New Relic.</span><span class="sxs-lookup"><span data-stu-id="baa93-207">In order to enable Azure Active Directory users to log in to New Relic, they must be provisioned into New Relic.</span></span> <span data-ttu-id="baa93-208">In het geval van New Relic is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="baa93-208">In the case of New Relic, provisioning is a manual task.</span></span>

<span data-ttu-id="baa93-209">**Voor het inrichten van een New Relic-gebruikersaccount, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="baa93-209">**To provision a user account to New Relic, perform the following steps:**</span></span>

1. <span data-ttu-id="baa93-210">Meld u aan bij uw **New Relic** bedrijf site als administrator.</span><span class="sxs-lookup"><span data-stu-id="baa93-210">Log in to your **New Relic** company site as administrator.</span></span>

2. <span data-ttu-id="baa93-211">Klik in het menu bovenaan op **Accountinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="baa93-211">In the menu on the top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="baa93-212">![Instellingen account](./media/active-directory-saas-new-relic-tutorial/ic797040.png "Accountinstellingen")</span><span class="sxs-lookup"><span data-stu-id="baa93-212">![Account Settings](./media/active-directory-saas-new-relic-tutorial/ic797040.png "Account Settings")</span></span>

3. <span data-ttu-id="baa93-213">In de **Account** deelvenster aan de linkerkant te klikken op **samenvatting**, en klik vervolgens op **gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="baa93-213">In the **Account** pane on the left side, click **Summary**, and then click **Add user**.</span></span>
   
    <span data-ttu-id="baa93-214">![Instellingen account](./media/active-directory-saas-new-relic-tutorial/ic797041.png "Accountinstellingen")</span><span class="sxs-lookup"><span data-stu-id="baa93-214">![Account Settings](./media/active-directory-saas-new-relic-tutorial/ic797041.png "Account Settings")</span></span>

4. <span data-ttu-id="baa93-215">Op de **actieve gebruikers** dialoogvenster de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="baa93-215">On the **Active users** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="baa93-216">![Actieve gebruikers](./media/active-directory-saas-new-relic-tutorial/ic797042.png "actieve gebruikers")</span><span class="sxs-lookup"><span data-stu-id="baa93-216">![Active Users](./media/active-directory-saas-new-relic-tutorial/ic797042.png "Active Users")</span></span>
   
    <span data-ttu-id="baa93-217">a.</span><span class="sxs-lookup"><span data-stu-id="baa93-217">a.</span></span> <span data-ttu-id="baa93-218">In de **e** textbox, typ de e-mailadres van een geldige Azure Active Directory-gebruiker die u inrichten wilt.</span><span class="sxs-lookup"><span data-stu-id="baa93-218">In the **Email** textbox, type the email address of a valid Azure Active Directory user you want to provision.</span></span>

    <span data-ttu-id="baa93-219">b.</span><span class="sxs-lookup"><span data-stu-id="baa93-219">b.</span></span> <span data-ttu-id="baa93-220">Als **rol** Selecteer **gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="baa93-220">As **Role** select **User**.</span></span>

    <span data-ttu-id="baa93-221">c.</span><span class="sxs-lookup"><span data-stu-id="baa93-221">c.</span></span> <span data-ttu-id="baa93-222">Klik op **deze gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="baa93-222">Click **Add this user**.</span></span>

>[!NOTE]
><span data-ttu-id="baa93-223">U kunt andere New Relic gebruiker account hulpmiddelen voor het maken of API's die door New Relic inrichten AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="baa93-223">You can use any other New Relic user account creation tools or APIs provided by New Relic to provision AAD user accounts.</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="baa93-224">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="baa93-224">Assigning the Azure AD test user</span></span>

<span data-ttu-id="baa93-225">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan New Relic.</span><span class="sxs-lookup"><span data-stu-id="baa93-225">In this section, you enable Britta Simon to use Azure single sign-on by granting access to New Relic.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="baa93-227">**Britta Simon om aan te wijzen New Relic, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="baa93-227">**To assign Britta Simon to New Relic, perform the following steps:**</span></span>

1. <span data-ttu-id="baa93-228">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="baa93-228">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="baa93-230">Selecteer in de lijst met toepassingen **New Relic**.</span><span class="sxs-lookup"><span data-stu-id="baa93-230">In the applications list, select **New Relic**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_app.png) 

3. <span data-ttu-id="baa93-232">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="baa93-232">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="baa93-234">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="baa93-234">Click **Add** button.</span></span> <span data-ttu-id="baa93-235">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="baa93-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="baa93-237">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="baa93-237">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="baa93-238">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="baa93-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="baa93-239">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="baa93-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="baa93-240">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="baa93-240">Testing single sign-on</span></span>

<span data-ttu-id="baa93-241">Het doel van deze sectie is het testen van uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="baa93-241">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="baa93-242">Als u op de New Relic-tegel in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw New Relic-toepassing.</span><span class="sxs-lookup"><span data-stu-id="baa93-242">When you click the New Relic tile in the Access Panel, you should get automatically signed-on to your New Relic application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="baa93-243">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="baa93-243">Additional resources</span></span>

* [<span data-ttu-id="baa93-244">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="baa93-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="baa93-245">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="baa93-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_203.png

