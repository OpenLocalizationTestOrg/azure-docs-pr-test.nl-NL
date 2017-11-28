---
title: 'Zelfstudie: Azure Active Directory-integratie met MobileXpense | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en MobileXpense.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e649fc4e-3e15-4948-b977-00bfe9f7db13
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/25/2017
ms.author: jeedes
ms.openlocfilehash: 030a1fc9f36d6fcfa607552d85ce232e36eaa64b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mobilexpense"></a><span data-ttu-id="980eb-103">Zelfstudie: Azure Active Directory-integratie met MobileXpense</span><span class="sxs-lookup"><span data-stu-id="980eb-103">Tutorial: Azure Active Directory integration with MobileXpense</span></span>

<span data-ttu-id="980eb-104">In deze zelfstudie leert u hoe MobileXpense integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="980eb-104">In this tutorial, you learn how to integrate MobileXpense with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="980eb-105">MobileXpense integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="980eb-105">Integrating MobileXpense with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="980eb-106">U kunt beheren in Azure AD die toegang tot MobileXpense heeft</span><span class="sxs-lookup"><span data-stu-id="980eb-106">You can control in Azure AD who has access to MobileXpense</span></span>
- <span data-ttu-id="980eb-107">U kunt uw gebruikers automatisch ophalen aangemeld bij MobileXpense (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="980eb-107">You can enable your users to automatically get signed-on to MobileXpense (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="980eb-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="980eb-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="980eb-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="980eb-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="980eb-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="980eb-110">Prerequisites</span></span>

<span data-ttu-id="980eb-111">Voor het configureren van Azure AD-integratie met MobileXpense, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="980eb-111">To configure Azure AD integration with MobileXpense, you need the following items:</span></span>

- <span data-ttu-id="980eb-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="980eb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="980eb-113">Een MobileXpense eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="980eb-113">A MobileXpense single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="980eb-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="980eb-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="980eb-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="980eb-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="980eb-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="980eb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="980eb-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="980eb-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="980eb-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="980eb-118">Scenario description</span></span>
<span data-ttu-id="980eb-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="980eb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="980eb-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="980eb-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="980eb-121">MobileXpense uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="980eb-121">Adding MobileXpense from the gallery</span></span>
2. <span data-ttu-id="980eb-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="980eb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mobilexpense-from-the-gallery"></a><span data-ttu-id="980eb-123">MobileXpense uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="980eb-123">Adding MobileXpense from the gallery</span></span>
<span data-ttu-id="980eb-124">Voor het configureren van de integratie van MobileXpense in Azure AD, moet u MobileXpense uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="980eb-124">To configure the integration of MobileXpense into Azure AD, you need to add MobileXpense from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="980eb-125">**Als u wilt toevoegen MobileXpense uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="980eb-125">**To add MobileXpense from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="980eb-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="980eb-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="980eb-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="980eb-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="980eb-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="980eb-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="980eb-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="980eb-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="980eb-133">Typ in het zoekvak **MobileXpense**.</span><span class="sxs-lookup"><span data-stu-id="980eb-133">In the search box, type **MobileXpense**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_search.png)

5. <span data-ttu-id="980eb-135">Selecteer in het deelvenster resultaten **MobileXpense**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="980eb-135">In the results panel, select **MobileXpense**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="980eb-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="980eb-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="980eb-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met MobileXpense op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="980eb-138">In this section, you configure and test Azure AD single sign-on with MobileXpense based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="980eb-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in MobileXpense is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="980eb-139">For single sign-on to work, Azure AD needs to know what the counterpart user in MobileXpense is to a user in Azure AD.</span></span> <span data-ttu-id="980eb-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in MobileXpense tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="980eb-140">In other words, a link relationship between an Azure AD user and the related user in MobileXpense needs to be established.</span></span>

<span data-ttu-id="980eb-141">Wijs in MobileXpense, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="980eb-141">In MobileXpense, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="980eb-142">Om te configureren en testen van Azure AD eenmalige aanmelding met MobileXpense, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="980eb-142">To configure and test Azure AD single sign-on with MobileXpense, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="980eb-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="980eb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="980eb-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="980eb-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="980eb-145">**[Maken van een testgebruiker MobileXpense](#creating-a-mobilexpense-test-user)**  - MobileXpense die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="980eb-145">**[Creating a MobileXpense test user](#creating-a-mobilexpense-test-user)** - to have a counterpart of Britta Simon in MobileXpense that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="980eb-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="980eb-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="980eb-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="980eb-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="980eb-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="980eb-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="980eb-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing MobileXpense configureren.</span><span class="sxs-lookup"><span data-stu-id="980eb-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your MobileXpense application.</span></span>

<span data-ttu-id="980eb-150">**Voor het configureren van Azure AD eenmalige aanmelding met MobileXpense, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="980eb-150">**To configure Azure AD single sign-on with MobileXpense, perform the following steps:**</span></span>

1. <span data-ttu-id="980eb-151">In de Azure-portal op de **MobileXpense** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="980eb-151">In the Azure portal, on the **MobileXpense** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="980eb-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="980eb-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_samlbase.png)

3. <span data-ttu-id="980eb-155">Op de **MobileXpense domein en de URL's** sectie als u wilt configureren van de toepassing in **IDP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="980eb-155">On the **MobileXpense Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_url11.png)

    <span data-ttu-id="980eb-157">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://<sub domain>.mobilexpense.com/SSO/SAML20/SAML/AssertionConsumerService.aspx`</span><span class="sxs-lookup"><span data-stu-id="980eb-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<sub domain>.mobilexpense.com/SSO/SAML20/SAML/AssertionConsumerService.aspx`</span></span>

4. <span data-ttu-id="980eb-158">Controleer **weergeven geavanceerde instellingen voor URL**, als u wilt configureren van de toepassing in **SP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="980eb-158">Check **Show advanced URL settings**, If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_url22.png)

<span data-ttu-id="980eb-160">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<sub domain>.mobilexpense.com/<customername>`</span><span class="sxs-lookup"><span data-stu-id="980eb-160">In the **Sign-on URL** textbox, type a URL using the following pattern:: `https://<sub domain>.mobilexpense.com/<customername>`</span></span>

> [!NOTE] 
> <span data-ttu-id="980eb-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="980eb-161">These values are not real.</span></span> <span data-ttu-id="980eb-162">Deze waarden bijwerken met de werkelijke antwoord-URL en de aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="980eb-162">Update these values with the actual Reply URL and Sign-On URL.</span></span> <span data-ttu-id="980eb-163">Neem contact op met [MobileXpense Client ondersteuningsteam](http://www.mobilexpense.net/contact) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="980eb-163">Contact [MobileXpense Client support team](http://www.mobilexpense.net/contact) to get these values.</span></span> 

5. <span data-ttu-id="980eb-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="980eb-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_certificate.png) 

6. <span data-ttu-id="980eb-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="980eb-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="980eb-168">Eenmalige aanmelding configureren op **MobileXpense** zijde, moet u de gedownloade verzenden **Metadata XML** naar [MobileXpense ondersteuningsteam](http://www.mobilexpense.net/contact).</span><span class="sxs-lookup"><span data-stu-id="980eb-168">To configure single sign-on on **MobileXpense** side, you need to send the downloaded **Metadata XML** to [MobileXpense support team](http://www.mobilexpense.net/contact).</span></span>

> [!TIP]
> <span data-ttu-id="980eb-169">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="980eb-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="980eb-170">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="980eb-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="980eb-171">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="980eb-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="980eb-172">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="980eb-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="980eb-173">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="980eb-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="980eb-175">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="980eb-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="980eb-176">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="980eb-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mobilexpense-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="980eb-178">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="980eb-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mobilexpense-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="980eb-180">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="980eb-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mobilexpense-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="980eb-182">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="980eb-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mobilexpense-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="980eb-184">a.</span><span class="sxs-lookup"><span data-stu-id="980eb-184">a.</span></span> <span data-ttu-id="980eb-185">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="980eb-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="980eb-186">b.</span><span class="sxs-lookup"><span data-stu-id="980eb-186">b.</span></span> <span data-ttu-id="980eb-187">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="980eb-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="980eb-188">c.</span><span class="sxs-lookup"><span data-stu-id="980eb-188">c.</span></span> <span data-ttu-id="980eb-189">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="980eb-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="980eb-190">d.</span><span class="sxs-lookup"><span data-stu-id="980eb-190">d.</span></span> <span data-ttu-id="980eb-191">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="980eb-191">Click **Create**.</span></span>
 
### <a name="creating-a-mobilexpense-test-user"></a><span data-ttu-id="980eb-192">Een testgebruiker MobileXpense maken</span><span class="sxs-lookup"><span data-stu-id="980eb-192">Creating a MobileXpense test user</span></span>

<span data-ttu-id="980eb-193">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in MobileXpense maken.</span><span class="sxs-lookup"><span data-stu-id="980eb-193">In this section, you create a user called Britta Simon in MobileXpense.</span></span> <span data-ttu-id="980eb-194">werken met [MobileXpense ondersteuningsteam](http://www.mobilexpense.net/contact) de gebruikers van het platform MobileXpense toevoegen.</span><span class="sxs-lookup"><span data-stu-id="980eb-194">work with [MobileXpense support team](http://www.mobilexpense.net/contact) to add the users in the MobileXpense platform.</span></span> <span data-ttu-id="980eb-195">Gebruikers moeten worden gemaakt en worden geactiveerd voordat u eenmalige aanmelding gebruiken.</span><span class="sxs-lookup"><span data-stu-id="980eb-195">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="980eb-196">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="980eb-196">Assigning the Azure AD test user</span></span>

<span data-ttu-id="980eb-197">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan MobileXpense.</span><span class="sxs-lookup"><span data-stu-id="980eb-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to MobileXpense.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="980eb-199">**Britta Simon om aan te wijzen MobileXpense, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="980eb-199">**To assign Britta Simon to MobileXpense, perform the following steps:**</span></span>

1. <span data-ttu-id="980eb-200">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="980eb-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="980eb-202">Selecteer in de lijst met toepassingen **MobileXpense**.</span><span class="sxs-lookup"><span data-stu-id="980eb-202">In the applications list, select **MobileXpense**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_app.png) 

3. <span data-ttu-id="980eb-204">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="980eb-204">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="980eb-206">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="980eb-206">Click **Add** button.</span></span> <span data-ttu-id="980eb-207">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="980eb-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="980eb-209">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="980eb-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="980eb-210">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="980eb-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="980eb-211">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="980eb-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="980eb-212">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="980eb-212">Testing single sign-on</span></span>

<span data-ttu-id="980eb-213">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="980eb-213">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="980eb-214">Als u op de tegel MobileXpense in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing MobileXpense.</span><span class="sxs-lookup"><span data-stu-id="980eb-214">When you click the MobileXpense tile in the Access Panel, you should get automatically signed-on to your MobileXpense application.</span></span>
<span data-ttu-id="980eb-215">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="980eb-215">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="980eb-216">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="980eb-216">Additional resources</span></span>

* [<span data-ttu-id="980eb-217">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="980eb-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="980eb-218">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="980eb-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_203.png

