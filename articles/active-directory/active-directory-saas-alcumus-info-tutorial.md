---
title: 'Zelfstudie: Azure Active Directory-integratie met Alcumus Info Exchange | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Alcumus Info Exchange.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d26034b8-f0d5-4f65-aa56-0fc168ceec8c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: jeedes
ms.openlocfilehash: 1f67682111de0bea1b18fd97d739492661ebbfd9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-alcumus-info-exchange"></a><span data-ttu-id="7b78a-103">Zelfstudie: Azure Active Directory-integratie met Exchange-Alcumus Info</span><span class="sxs-lookup"><span data-stu-id="7b78a-103">Tutorial: Azure Active Directory integration with Alcumus Info Exchange</span></span>

<span data-ttu-id="7b78a-104">In deze zelfstudie leert u hoe Alcumus Info Exchange integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7b78a-104">In this tutorial, you learn how to integrate Alcumus Info Exchange with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7b78a-105">Alcumus Info Exchange integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="7b78a-105">Integrating Alcumus Info Exchange with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7b78a-106">U kunt beheren in Azure AD die toegang tot Alcumus Info Exchange heeft</span><span class="sxs-lookup"><span data-stu-id="7b78a-106">You can control in Azure AD who has access to Alcumus Info Exchange</span></span>
- <span data-ttu-id="7b78a-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Alcumus Info Exchange (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="7b78a-107">You can enable your users to automatically get signed-on to Alcumus Info Exchange (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7b78a-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="7b78a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7b78a-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7b78a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7b78a-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="7b78a-110">Prerequisites</span></span>

<span data-ttu-id="7b78a-111">Voor het configureren van Azure AD-integratie met Alcumus Info Exchange, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="7b78a-111">To configure Azure AD integration with Alcumus Info Exchange, you need the following items:</span></span>

- <span data-ttu-id="7b78a-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="7b78a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7b78a-113">Een Alcumus Info Exchange eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="7b78a-113">An Alcumus Info Exchange single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7b78a-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="7b78a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7b78a-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="7b78a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7b78a-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="7b78a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7b78a-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7b78a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7b78a-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="7b78a-118">Scenario description</span></span>
<span data-ttu-id="7b78a-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="7b78a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7b78a-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="7b78a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7b78a-121">Alcumus Info Exchange vanuit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="7b78a-121">Adding Alcumus Info Exchange from the gallery</span></span>
2. <span data-ttu-id="7b78a-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="7b78a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-alcumus-info-exchange-from-the-gallery"></a><span data-ttu-id="7b78a-123">Alcumus Info Exchange vanuit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="7b78a-123">Adding Alcumus Info Exchange from the gallery</span></span>
<span data-ttu-id="7b78a-124">Voor het configureren van de integratie van Alcumus Info Exchange in Azure AD, moet u Alcumus Info Exchange vanuit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="7b78a-124">To configure the integration of Alcumus Info Exchange into Azure AD, you need to add Alcumus Info Exchange from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7b78a-125">**Als u wilt toevoegen Alcumus Info Exchange vanuit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="7b78a-125">**To add Alcumus Info Exchange from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7b78a-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="7b78a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7b78a-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="7b78a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7b78a-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="7b78a-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="7b78a-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7b78a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="7b78a-133">Typ in het zoekvak **Alcumus Info Exchange**.</span><span class="sxs-lookup"><span data-stu-id="7b78a-133">In the search box, type **Alcumus Info Exchange**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-alcumus-info-tutorial/tutorial_alcumusinfoexchange_search.png)

5. <span data-ttu-id="7b78a-135">Selecteer in het deelvenster resultaten **Alcumus Info Exchange**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="7b78a-135">In the results panel, select **Alcumus Info Exchange**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-alcumus-info-tutorial/tutorial_alcumusinfoexchange_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7b78a-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="7b78a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7b78a-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Alcumus Info Exchange op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="7b78a-138">In this section, you configure and test Azure AD single sign-on with Alcumus Info Exchange based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7b78a-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Alcumus Info Exchange is aan een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7b78a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Alcumus Info Exchange is to a user in Azure AD.</span></span> <span data-ttu-id="7b78a-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Alcumus Info Exchange tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="7b78a-140">In other words, a link relationship between an Azure AD user and the related user in Alcumus Info Exchange needs to be established.</span></span>

<span data-ttu-id="7b78a-141">Wijs in Alcumus Info Exchange de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="7b78a-141">In Alcumus Info Exchange, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="7b78a-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Alcumus Info Exchange, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="7b78a-142">To configure and test Azure AD single sign-on with Alcumus Info Exchange, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7b78a-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7b78a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7b78a-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7b78a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7b78a-145">**[Maken van een testgebruiker Alcumus Info Exchange](#creating-an-alcumus-info-exchange-test-user)**  - Alcumus Info Exchange die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="7b78a-145">**[Creating an Alcumus Info Exchange test user](#creating-an-alcumus-info-exchange-test-user)** - to have a counterpart of Britta Simon in Alcumus Info Exchange that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7b78a-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="7b78a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7b78a-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="7b78a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7b78a-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="7b78a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7b78a-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw toepassing Alcumus Info Exchange.</span><span class="sxs-lookup"><span data-stu-id="7b78a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Alcumus Info Exchange application.</span></span>

<span data-ttu-id="7b78a-150">**Voor het configureren van Azure AD eenmalige aanmelding met Alcumus Info Exchange, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="7b78a-150">**To configure Azure AD single sign-on with Alcumus Info Exchange, perform the following steps:**</span></span>

1. <span data-ttu-id="7b78a-151">In de Azure-portal op de **Alcumus Info Exchange** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="7b78a-151">In the Azure portal, on the **Alcumus Info Exchange** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="7b78a-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="7b78a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-alcumus-info-tutorial/tutorial_alcumusinfoexchange_samlbase.png)

3. <span data-ttu-id="7b78a-155">Op de **Alcumus Info Exchange domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="7b78a-155">On the **Alcumus Info Exchange Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-alcumus-info-tutorial/tutorial_alcumusinfoexchange_url.png)

    <span data-ttu-id="7b78a-157">a.</span><span class="sxs-lookup"><span data-stu-id="7b78a-157">a.</span></span> <span data-ttu-id="7b78a-158">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<subdomain>.info-exchange.com`</span><span class="sxs-lookup"><span data-stu-id="7b78a-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.info-exchange.com`</span></span>

    <span data-ttu-id="7b78a-159">b.</span><span class="sxs-lookup"><span data-stu-id="7b78a-159">b.</span></span> <span data-ttu-id="7b78a-160">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://<subdomain>.info-exchange.com/Auth/`</span><span class="sxs-lookup"><span data-stu-id="7b78a-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.info-exchange.com/Auth/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7b78a-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="7b78a-161">These values are not real.</span></span> <span data-ttu-id="7b78a-162">Deze waarden bijwerken met de werkelijke id en de antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="7b78a-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="7b78a-163">Neem contact op met [Alcumus Info Exchange ondersteuningsteam](mailto:helpdesk@alcumusgroup.com) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="7b78a-163">Contact [Alcumus Info Exchange support team](mailto:helpdesk@alcumusgroup.com) to get these values.</span></span>
 
4. <span data-ttu-id="7b78a-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="7b78a-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-alcumus-info-tutorial/tutorial_alcumusinfoexchange_certificate.png) 

5. <span data-ttu-id="7b78a-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="7b78a-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7b78a-168">Eenmalige aanmelding configureren op **Alcumus Info Exchange** zijde, moet u de gedownloade verzenden **Metadata XML** naar [Alcumus Info Exchange ondersteuningsteam](mailto:helpdesk@alcumusgroup.com).</span><span class="sxs-lookup"><span data-stu-id="7b78a-168">To configure single sign-on on **Alcumus Info Exchange** side, you need to send the downloaded **Metadata XML** to [Alcumus Info Exchange support team](mailto:helpdesk@alcumusgroup.com).</span></span>

> [!TIP]
> <span data-ttu-id="7b78a-169">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="7b78a-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7b78a-170">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="7b78a-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7b78a-171">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7b78a-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7b78a-172">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="7b78a-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="7b78a-173">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="7b78a-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="7b78a-175">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="7b78a-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7b78a-176">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="7b78a-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-alcumus-info-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7b78a-178">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="7b78a-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-alcumus-info-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7b78a-180">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7b78a-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-alcumus-info-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7b78a-182">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="7b78a-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-alcumus-info-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7b78a-184">a.</span><span class="sxs-lookup"><span data-stu-id="7b78a-184">a.</span></span> <span data-ttu-id="7b78a-185">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7b78a-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7b78a-186">b.</span><span class="sxs-lookup"><span data-stu-id="7b78a-186">b.</span></span> <span data-ttu-id="7b78a-187">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7b78a-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7b78a-188">c.</span><span class="sxs-lookup"><span data-stu-id="7b78a-188">c.</span></span> <span data-ttu-id="7b78a-189">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="7b78a-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7b78a-190">d.</span><span class="sxs-lookup"><span data-stu-id="7b78a-190">d.</span></span> <span data-ttu-id="7b78a-191">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="7b78a-191">Click **Create**.</span></span>
 
### <a name="creating-an-alcumus-info-exchange-test-user"></a><span data-ttu-id="7b78a-192">Maken van een testgebruiker Alcumus Info Exchange</span><span class="sxs-lookup"><span data-stu-id="7b78a-192">Creating an Alcumus Info Exchange test user</span></span>

<span data-ttu-id="7b78a-193">Het doel van deze sectie is het maken van een gebruiker Britta Simon aangeroepen in Alcumus Info Exchange.</span><span class="sxs-lookup"><span data-stu-id="7b78a-193">The objective of this section is to create a user called Britta Simon in Alcumus Info Exchange.</span></span>

<span data-ttu-id="7b78a-194">Voor het maken van een gebruiker met de naam van Britta Simon Alcumus Info Exchange Neem contact op met de [Alcumus Info Exchange ondersteuningsteam](mailto:helpdesk@alcumusgroup.com).</span><span class="sxs-lookup"><span data-stu-id="7b78a-194">To create a user called Britta Simon in Alcumus Info Exchange, Contact the [Alcumus Info Exchange support team](mailto:helpdesk@alcumusgroup.com).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7b78a-195">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="7b78a-195">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7b78a-196">In deze sectie schakelt u Britta Simon Azure eenmalige aanmelding toegang verleent tot Alcumus Info Exchange gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7b78a-196">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Alcumus Info Exchange.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="7b78a-198">**Britta Simon om aan te wijzen Alcumus Info Exchange, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="7b78a-198">**To assign Britta Simon to Alcumus Info Exchange, perform the following steps:**</span></span>

1. <span data-ttu-id="7b78a-199">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="7b78a-199">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="7b78a-201">Selecteer in de lijst met toepassingen **Alcumus Info Exchange**.</span><span class="sxs-lookup"><span data-stu-id="7b78a-201">In the applications list, select **Alcumus Info Exchange**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-alcumus-info-tutorial/tutorial_alcumusinfoexchange_app.png) 

3. <span data-ttu-id="7b78a-203">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="7b78a-203">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="7b78a-205">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="7b78a-205">Click **Add** button.</span></span> <span data-ttu-id="7b78a-206">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7b78a-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="7b78a-208">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="7b78a-208">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7b78a-209">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7b78a-209">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7b78a-210">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7b78a-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7b78a-211">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="7b78a-211">Testing single sign-on</span></span>

<span data-ttu-id="7b78a-212">Het doel van deze sectie is het testen van uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="7b78a-212">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="7b78a-213">Als u op de tegel Alcumus Info Exchange in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw Alcumus Info Exchange-toepassing.</span><span class="sxs-lookup"><span data-stu-id="7b78a-213">When you click the Alcumus Info Exchange tile in the Access Panel, you should get automatically signed-on to your Alcumus Info Exchange application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7b78a-214">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="7b78a-214">Additional resources</span></span>

* [<span data-ttu-id="7b78a-215">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7b78a-215">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7b78a-216">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7b78a-216">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_203.png

