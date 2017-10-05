---
title: 'Zelfstudie: Azure Active Directory-integratie met Yardi eLearning | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Yardi eLearning.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7ea58b54-ec5b-4576-8586-814b11d0f4fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: e7b36b692ad2a8bc3a3f5203d93882af96fd2109
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-yardi-elearning"></a><span data-ttu-id="b97dc-103">Zelfstudie: Azure Active Directory-integratie met Yardi eLearning</span><span class="sxs-lookup"><span data-stu-id="b97dc-103">Tutorial: Azure Active Directory integration with Yardi eLearning</span></span>

<span data-ttu-id="b97dc-104">In deze zelfstudie leert u hoe Yardi eLearning integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b97dc-104">In this tutorial, you learn how to integrate Yardi eLearning with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b97dc-105">Integratie van Yardi biedt eLearning met Azure AD de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="b97dc-105">Integrating Yardi eLearning with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b97dc-106">U kunt beheren in Azure AD die toegang tot Yardi eLearning heeft</span><span class="sxs-lookup"><span data-stu-id="b97dc-106">You can control in Azure AD who has access to Yardi eLearning</span></span>
- <span data-ttu-id="b97dc-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Yardi eLearning (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="b97dc-107">You can enable your users to automatically get signed-on to Yardi eLearning (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b97dc-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="b97dc-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b97dc-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b97dc-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b97dc-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="b97dc-110">Prerequisites</span></span>

<span data-ttu-id="b97dc-111">Voor het configureren van Azure AD-integratie met Yardi eLearning, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="b97dc-111">To configure Azure AD integration with Yardi eLearning, you need the following items:</span></span>

- <span data-ttu-id="b97dc-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="b97dc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b97dc-113">Een Yardi eLearning eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="b97dc-113">A Yardi eLearning single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b97dc-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="b97dc-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b97dc-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="b97dc-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b97dc-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="b97dc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b97dc-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b97dc-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b97dc-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="b97dc-118">Scenario description</span></span>
<span data-ttu-id="b97dc-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="b97dc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b97dc-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="b97dc-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b97dc-121">Yardi eLearning uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="b97dc-121">Adding Yardi eLearning from the gallery</span></span>
2. <span data-ttu-id="b97dc-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b97dc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-yardi-elearning-from-the-gallery"></a><span data-ttu-id="b97dc-123">Yardi eLearning uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="b97dc-123">Adding Yardi eLearning from the gallery</span></span>
<span data-ttu-id="b97dc-124">Voor het configureren van de integratie van Yardi eLearning in Azure AD, moet u Yardi eLearning uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="b97dc-124">To configure the integration of Yardi eLearning into Azure AD, you need to add Yardi eLearning from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b97dc-125">**Als u wilt toevoegen Yardi eLearning uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b97dc-125">**To add Yardi eLearning from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b97dc-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="b97dc-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b97dc-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b97dc-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b97dc-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b97dc-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="b97dc-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b97dc-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="b97dc-133">Typ in het zoekvak **Yardi eLearning**.</span><span class="sxs-lookup"><span data-stu-id="b97dc-133">In the search box, type **Yardi eLearning**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-yardielearning-tutorial/tutorial_yardielearning_search.png)

5. <span data-ttu-id="b97dc-135">Selecteer in het deelvenster resultaten **Yardi eLearning**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="b97dc-135">In the results panel, select **Yardi eLearning**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-yardielearning-tutorial/tutorial_yardielearning_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b97dc-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b97dc-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b97dc-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Yardi eLearning op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="b97dc-138">In this section, you configure and test Azure AD single sign-on with Yardi eLearning based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b97dc-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Yardi eLearning is aan een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b97dc-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Yardi eLearning is to a user in Azure AD.</span></span> <span data-ttu-id="b97dc-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Yardi eLearning tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="b97dc-140">In other words, a link relationship between an Azure AD user and the related user in Yardi eLearning needs to be established.</span></span>

<span data-ttu-id="b97dc-141">Wijs in Yardi eLearning, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="b97dc-141">In Yardi eLearning, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b97dc-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Yardi eLearning, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="b97dc-142">To configure and test Azure AD single sign-on with Yardi eLearning, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b97dc-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b97dc-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b97dc-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b97dc-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b97dc-145">**[Maken van een gebruiker Yardi eLearning test](#creating-a-yardi-elearning-test-user)**  - hebben een equivalent van Britta Simon in Yardi eLearning die is gekoppeld aan de Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="b97dc-145">**[Creating a Yardi eLearning test user](#creating-a-yardi-elearning-test-user)** - to have a counterpart of Britta Simon in Yardi eLearning that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b97dc-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="b97dc-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b97dc-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="b97dc-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b97dc-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="b97dc-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b97dc-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw Yardi eLearning-toepassing.</span><span class="sxs-lookup"><span data-stu-id="b97dc-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Yardi eLearning application.</span></span>

<span data-ttu-id="b97dc-150">**Voor het configureren van Azure AD eenmalige aanmelding met Yardi eLearning, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b97dc-150">**To configure Azure AD single sign-on with Yardi eLearning, perform the following steps:**</span></span>

1. <span data-ttu-id="b97dc-151">In de Azure-portal op de **Yardi eLearning** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="b97dc-151">In the Azure portal, on the **Yardi eLearning** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="b97dc-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="b97dc-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-yardielearning-tutorial/tutorial_yardielearning_samlbase.png)

3. <span data-ttu-id="b97dc-155">Op de **Yardi eLearning domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="b97dc-155">On the **Yardi eLearning Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-yardielearning-tutorial/tutorial_yardielearning_url.png)

    <span data-ttu-id="b97dc-157">a.</span><span class="sxs-lookup"><span data-stu-id="b97dc-157">a.</span></span> <span data-ttu-id="b97dc-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<companyname>.yardielearning.com/login`</span><span class="sxs-lookup"><span data-stu-id="b97dc-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.yardielearning.com/login`</span></span>

    <span data-ttu-id="b97dc-159">b.</span><span class="sxs-lookup"><span data-stu-id="b97dc-159">b.</span></span> <span data-ttu-id="b97dc-160">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<companyname>.yardielearning.com/trust`</span><span class="sxs-lookup"><span data-stu-id="b97dc-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.yardielearning.com/trust`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b97dc-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="b97dc-161">These values are not real.</span></span> <span data-ttu-id="b97dc-162">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="b97dc-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="b97dc-163">Neem contact op met [Yardi eLearning Client ondersteuningsteam](mailto:elearning@yardi.com) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="b97dc-163">Contact [Yardi eLearning Client support team](mailto:elearning@yardi.com) to get these values.</span></span> 
 
4. <span data-ttu-id="b97dc-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="b97dc-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-yardielearning-tutorial/tutorial_yardielearning_certificate.png) 

5. <span data-ttu-id="b97dc-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="b97dc-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-yardielearning-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="b97dc-168">Eenmalige aanmelding configureren op **Yardi eLearning** zijde, moet u de gedownloade verzenden **Metadata XML** naar [Yardi eLearning ondersteuningsteam](mailto:elearning@yardi.com).</span><span class="sxs-lookup"><span data-stu-id="b97dc-168">To configure single sign-on on **Yardi eLearning** side, you need to send the downloaded **Metadata XML** to [Yardi eLearning support team](mailto:elearning@yardi.com).</span></span> 

> [!TIP]
> <span data-ttu-id="b97dc-169">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="b97dc-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b97dc-170">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="b97dc-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b97dc-171">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b97dc-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b97dc-172">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="b97dc-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="b97dc-173">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="b97dc-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="b97dc-175">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b97dc-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b97dc-176">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="b97dc-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-yardielearning-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b97dc-178">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="b97dc-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-yardielearning-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b97dc-180">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b97dc-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-yardielearning-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b97dc-182">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="b97dc-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-yardielearning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b97dc-184">a.</span><span class="sxs-lookup"><span data-stu-id="b97dc-184">a.</span></span> <span data-ttu-id="b97dc-185">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b97dc-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b97dc-186">b.</span><span class="sxs-lookup"><span data-stu-id="b97dc-186">b.</span></span> <span data-ttu-id="b97dc-187">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b97dc-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b97dc-188">c.</span><span class="sxs-lookup"><span data-stu-id="b97dc-188">c.</span></span> <span data-ttu-id="b97dc-189">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="b97dc-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b97dc-190">d.</span><span class="sxs-lookup"><span data-stu-id="b97dc-190">d.</span></span> <span data-ttu-id="b97dc-191">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="b97dc-191">Click **Create**.</span></span>
 
### <a name="creating-a-yardi-elearning-test-user"></a><span data-ttu-id="b97dc-192">Maken van een gebruiker Yardi eLearning testen</span><span class="sxs-lookup"><span data-stu-id="b97dc-192">Creating a Yardi eLearning test user</span></span>

<span data-ttu-id="b97dc-193">Het doel van deze sectie is het maken van een gebruiker Britta Simon in Yardi eLearning genoemd.</span><span class="sxs-lookup"><span data-stu-id="b97dc-193">The objective of this section is to create a user called Britta Simon in Yardi eLearning.</span></span> <span data-ttu-id="b97dc-194">Yardi eLearning ondersteunt just-in-time-inrichting, dit is standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="b97dc-194">Yardi eLearning supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="b97dc-195">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="b97dc-195">There is no action item for you in this section.</span></span> <span data-ttu-id="b97dc-196">Een nieuwe gebruiker is gemaakt tijdens een poging tot toegang tot Yardi eLearning als deze nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="b97dc-196">A new user is created during an attempt to access Yardi eLearning if it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="b97dc-197">Als u een gebruiker handmatig maken wilt, moet u contact op met de [Yardi eLearning ondersteuningsteam](mailto:elearning@yardi.com).</span><span class="sxs-lookup"><span data-stu-id="b97dc-197">If you need to create a user manually, you need to contact the [Yardi eLearning support team](mailto:elearning@yardi.com).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b97dc-198">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="b97dc-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b97dc-199">In deze sectie schakelt u Britta Simon Azure eenmalige aanmelding gebruiken door het verlenen van toegang tot Yardi eLearning.</span><span class="sxs-lookup"><span data-stu-id="b97dc-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Yardi eLearning.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="b97dc-201">**Britta Simon om aan te wijzen Yardi eLearning, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b97dc-201">**To assign Britta Simon to Yardi eLearning, perform the following steps:**</span></span>

1. <span data-ttu-id="b97dc-202">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b97dc-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="b97dc-204">Selecteer in de lijst met toepassingen **Yardi eLearning**.</span><span class="sxs-lookup"><span data-stu-id="b97dc-204">In the applications list, select **Yardi eLearning**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-yardielearning-tutorial/tutorial_yardielearning_app.png) 

3. <span data-ttu-id="b97dc-206">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="b97dc-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="b97dc-208">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="b97dc-208">Click **Add** button.</span></span> <span data-ttu-id="b97dc-209">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b97dc-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="b97dc-211">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="b97dc-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b97dc-212">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b97dc-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b97dc-213">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b97dc-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b97dc-214">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b97dc-214">Testing single sign-on</span></span>

<span data-ttu-id="b97dc-215">Het doel van deze sectie is het testen van uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="b97dc-215">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b97dc-216">Als u op de tegel Yardi eLearning in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw Yardi eLearning-toepassing.</span><span class="sxs-lookup"><span data-stu-id="b97dc-216">When you click the Yardi eLearning tile in the Access Panel, you should get automatically signed-on to your Yardi eLearning application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b97dc-217">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="b97dc-217">Additional resources</span></span>

* [<span data-ttu-id="b97dc-218">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b97dc-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b97dc-219">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b97dc-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-yardielearning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-yardielearning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-yardielearning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-yardielearning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-yardielearning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-yardielearning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-yardielearning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-yardielearning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-yardielearning-tutorial/tutorial_general_203.png

