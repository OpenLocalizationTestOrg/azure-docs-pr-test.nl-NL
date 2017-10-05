---
title: 'Zelfstudie: Azure Active Directory-integratie met Derhoud Jones Factiva | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Derhoud Jones Factiva.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b36e97e8-37a6-4096-a894-530427ee1331
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/11/2017
ms.author: jeedes
ms.openlocfilehash: dab48c24ff25fd68df1ee540bb8f0929e7e81bcb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-dow-jones-factiva"></a><span data-ttu-id="16f2d-103">Zelfstudie: Azure Active Directory-integratie met Derhoud Jones Factiva</span><span class="sxs-lookup"><span data-stu-id="16f2d-103">Tutorial: Azure Active Directory integration with Dow Jones Factiva</span></span>

<span data-ttu-id="16f2d-104">In deze zelfstudie leert u hoe Derhoud Jones Factiva integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="16f2d-104">In this tutorial, you learn how to integrate Dow Jones Factiva with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="16f2d-105">Derhoud Jones Factiva integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="16f2d-105">Integrating Dow Jones Factiva with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="16f2d-106">U kunt beheren in Azure AD die toegang tot Derhoud Jones Factiva heeft</span><span class="sxs-lookup"><span data-stu-id="16f2d-106">You can control in Azure AD who has access to Dow Jones Factiva</span></span>
- <span data-ttu-id="16f2d-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Derhoud Jones Factiva (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="16f2d-107">You can enable your users to automatically get signed-on to Dow Jones Factiva (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="16f2d-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="16f2d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="16f2d-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="16f2d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="16f2d-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="16f2d-110">Prerequisites</span></span>

<span data-ttu-id="16f2d-111">Voor het configureren van Azure AD-integratie met Derhoud Jones Factiva, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="16f2d-111">To configure Azure AD integration with Dow Jones Factiva, you need the following items:</span></span>

- <span data-ttu-id="16f2d-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="16f2d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="16f2d-113">Een Derhoud Jones Factiva eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="16f2d-113">A Dow Jones Factiva single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="16f2d-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="16f2d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="16f2d-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="16f2d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="16f2d-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="16f2d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="16f2d-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="16f2d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="16f2d-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="16f2d-118">Scenario description</span></span>
<span data-ttu-id="16f2d-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="16f2d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="16f2d-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="16f2d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="16f2d-121">Derhoud Jones Factiva uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="16f2d-121">Adding Dow Jones Factiva from the gallery</span></span>
2. <span data-ttu-id="16f2d-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="16f2d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-dow-jones-factiva-from-the-gallery"></a><span data-ttu-id="16f2d-123">Derhoud Jones Factiva uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="16f2d-123">Adding Dow Jones Factiva from the gallery</span></span>
<span data-ttu-id="16f2d-124">Voor het configureren van de integratie van Derhoud Jones Factiva in Azure AD, moet u Derhoud Jones Factiva uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="16f2d-124">To configure the integration of Dow Jones Factiva into Azure AD, you need to add Dow Jones Factiva from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="16f2d-125">**Als u wilt toevoegen Derhoud Jones Factiva uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="16f2d-125">**To add Dow Jones Factiva from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="16f2d-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="16f2d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="16f2d-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="16f2d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="16f2d-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="16f2d-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="16f2d-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="16f2d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="16f2d-133">Typ in het zoekvak **Derhoud Jones Factiva**.</span><span class="sxs-lookup"><span data-stu-id="16f2d-133">In the search box, type **Dow Jones Factiva**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_dowjonesfactiva_search.png)

5. <span data-ttu-id="16f2d-135">Selecteer in het deelvenster resultaten **Derhoud Jones Factiva**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="16f2d-135">In the results panel, select **Dow Jones Factiva**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_dowjonesfactiva_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="16f2d-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="16f2d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="16f2d-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Derhoud Jones Factiva op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="16f2d-138">In this section, you configure and test Azure AD single sign-on with Dow Jones Factiva based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="16f2d-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Derhoud Jones Factiva is aan een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="16f2d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Dow Jones Factiva is to a user in Azure AD.</span></span> <span data-ttu-id="16f2d-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Derhoud Jones Factiva tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="16f2d-140">In other words, a link relationship between an Azure AD user and the related user in Dow Jones Factiva needs to be established.</span></span>

<span data-ttu-id="16f2d-141">Wijs in Derhoud Jones Factiva, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="16f2d-141">In Dow Jones Factiva, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="16f2d-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Derhoud Jones Factiva, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="16f2d-142">To configure and test Azure AD single sign-on with Dow Jones Factiva, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="16f2d-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="16f2d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="16f2d-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="16f2d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="16f2d-145">**[Maken van een testgebruiker Derhoud Jones Factiva](#creating-a-dow-jones-factiva-test-user)**  - Derhoud Jones Factiva die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="16f2d-145">**[Creating a Dow Jones Factiva test user](#creating-a-dow-jones-factiva-test-user)** - to have a counterpart of Britta Simon in Dow Jones Factiva that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="16f2d-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="16f2d-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="16f2d-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="16f2d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="16f2d-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="16f2d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="16f2d-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Derhoud Jones Factiva configureren.</span><span class="sxs-lookup"><span data-stu-id="16f2d-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Dow Jones Factiva application.</span></span>

<span data-ttu-id="16f2d-150">**Voor het configureren van Azure AD eenmalige aanmelding met Derhoud Jones Factiva, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="16f2d-150">**To configure Azure AD single sign-on with Dow Jones Factiva, perform the following steps:**</span></span>

1. <span data-ttu-id="16f2d-151">In de Azure-portal op de **Derhoud Jones Factiva** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="16f2d-151">In the Azure portal, on the **Dow Jones Factiva** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="16f2d-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="16f2d-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_dowjonesfactiva_samlbase.png)

3. <span data-ttu-id="16f2d-155">Op de **Derhoud Jones Factiva domein en de URL's** sectie, de gebruiker heeft geen alle stappen uitvoeren als de app al vooraf is geïntegreerd met Azure.</span><span class="sxs-lookup"><span data-stu-id="16f2d-155">On the **Dow Jones Factiva Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_dowjonesfactiva_url.png)

4. <span data-ttu-id="16f2d-157">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="16f2d-157">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_dowjonesfactiva_certificate.png) 

5. <span data-ttu-id="16f2d-159">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="16f2d-159">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="16f2d-161">Eenmalige aanmelding configureren op **Derhoud Jones Factiva** zijde, moet u de gedownloade verzenden **Metadata XML** naar [Derhoud Jones Factiva ondersteuningsteam](https://www.dowjones.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="16f2d-161">To configure single sign-on on **Dow Jones Factiva** side, you need to send the downloaded **Metadata XML** to [Dow Jones Factiva support team](https://www.dowjones.com/contact/).</span></span> <span data-ttu-id="16f2d-162">Ze deze instelling zodat de SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="16f2d-162">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="16f2d-163">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="16f2d-163">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="16f2d-164">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="16f2d-164">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="16f2d-165">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="16f2d-165">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="16f2d-166">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="16f2d-166">Creating an Azure AD test user</span></span>
<span data-ttu-id="16f2d-167">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="16f2d-167">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="16f2d-169">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="16f2d-169">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="16f2d-170">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="16f2d-170">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-dowjones-factiva-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="16f2d-172">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="16f2d-172">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-dowjones-factiva-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="16f2d-174">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="16f2d-174">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-dowjones-factiva-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="16f2d-176">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="16f2d-176">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-dowjones-factiva-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="16f2d-178">a.</span><span class="sxs-lookup"><span data-stu-id="16f2d-178">a.</span></span> <span data-ttu-id="16f2d-179">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="16f2d-179">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="16f2d-180">b.</span><span class="sxs-lookup"><span data-stu-id="16f2d-180">b.</span></span> <span data-ttu-id="16f2d-181">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="16f2d-181">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="16f2d-182">c.</span><span class="sxs-lookup"><span data-stu-id="16f2d-182">c.</span></span> <span data-ttu-id="16f2d-183">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="16f2d-183">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="16f2d-184">d.</span><span class="sxs-lookup"><span data-stu-id="16f2d-184">d.</span></span> <span data-ttu-id="16f2d-185">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="16f2d-185">Click **Create**.</span></span>
 
### <a name="creating-a-dow-jones-factiva-test-user"></a><span data-ttu-id="16f2d-186">Een testgebruiker Derhoud Jones Factiva maken</span><span class="sxs-lookup"><span data-stu-id="16f2d-186">Creating a Dow Jones Factiva test user</span></span>

<span data-ttu-id="16f2d-187">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in Derhoud Jones Factiva maken.</span><span class="sxs-lookup"><span data-stu-id="16f2d-187">In this section, you create a user called Britta Simon in Dow Jones Factiva.</span></span> <span data-ttu-id="16f2d-188">Neem contact op met Derhoud [Jones Factiva ondersteuningsteam](https://www.dowjones.com/contact/) de gebruikers van het platform Derhoud Jones Factiva toevoegen.</span><span class="sxs-lookup"><span data-stu-id="16f2d-188">Please work with Dow [Jones Factiva support team](https://www.dowjones.com/contact/) to add the users in the Dow Jones Factiva platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="16f2d-189">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="16f2d-189">Assigning the Azure AD test user</span></span>

<span data-ttu-id="16f2d-190">In deze sectie maakt inschakelen u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Derhoud Jones Factiva.</span><span class="sxs-lookup"><span data-stu-id="16f2d-190">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Dow Jones Factiva.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="16f2d-192">**Britta Simon om aan te wijzen Derhoud Jones Factiva, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="16f2d-192">**To assign Britta Simon to Dow Jones Factiva, perform the following steps:**</span></span>

1. <span data-ttu-id="16f2d-193">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="16f2d-193">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="16f2d-195">Selecteer in de lijst met toepassingen **Derhoud Jones Factiva**.</span><span class="sxs-lookup"><span data-stu-id="16f2d-195">In the applications list, select **Dow Jones Factiva**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_dowjonesfactiva_app.png) 

3. <span data-ttu-id="16f2d-197">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="16f2d-197">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="16f2d-199">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="16f2d-199">Click **Add** button.</span></span> <span data-ttu-id="16f2d-200">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="16f2d-200">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="16f2d-202">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="16f2d-202">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="16f2d-203">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="16f2d-203">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="16f2d-204">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="16f2d-204">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="16f2d-205">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="16f2d-205">Testing single sign-on</span></span>

<span data-ttu-id="16f2d-206">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="16f2d-206">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="16f2d-207">Als u op de tegel Derhoud Jones Factiva in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Derhoud Jones Factiva.</span><span class="sxs-lookup"><span data-stu-id="16f2d-207">When you click the Dow Jones Factiva tile in the Access Panel, you should get automatically signed-on to your Dow Jones Factiva application.</span></span>
<span data-ttu-id="16f2d-208">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="16f2d-208">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="16f2d-209">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="16f2d-209">Additional resources</span></span>

* [<span data-ttu-id="16f2d-210">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="16f2d-210">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="16f2d-211">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="16f2d-211">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_203.png

