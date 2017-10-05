---
title: 'Zelfstudie: Azure Active Directory-integratie met itslearning | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en itslearning.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 60587ba3-1396-4b8a-9ac1-e22a98e5e0ac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 32c8a8dff533f726784fb52b9496c2cb50ecfde7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-itslearning"></a><span data-ttu-id="88b96-103">Zelfstudie: Azure Active Directory-integratie met itslearning</span><span class="sxs-lookup"><span data-stu-id="88b96-103">Tutorial: Azure Active Directory integration with itslearning</span></span>

<span data-ttu-id="88b96-104">In deze zelfstudie leert u hoe itslearning integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="88b96-104">In this tutorial, you learn how to integrate itslearning with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="88b96-105">Itslearning integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="88b96-105">Integrating itslearning with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="88b96-106">U kunt beheren in Azure AD die toegang tot itslearning heeft</span><span class="sxs-lookup"><span data-stu-id="88b96-106">You can control in Azure AD who has access to itslearning</span></span>
- <span data-ttu-id="88b96-107">U kunt uw gebruikers automatisch ophalen aangemeld bij itslearning (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="88b96-107">You can enable your users to automatically get signed-on to itslearning (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="88b96-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="88b96-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="88b96-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="88b96-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="88b96-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="88b96-110">Prerequisites</span></span>

<span data-ttu-id="88b96-111">Voor het configureren van Azure AD-integratie met itslearning, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="88b96-111">To configure Azure AD integration with itslearning, you need the following items:</span></span>

- <span data-ttu-id="88b96-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="88b96-112">An Azure AD subscription</span></span>
- <span data-ttu-id="88b96-113">Een itslearning eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="88b96-113">An itslearning single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="88b96-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="88b96-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="88b96-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="88b96-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="88b96-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="88b96-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="88b96-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="88b96-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="88b96-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="88b96-118">Scenario description</span></span>
<span data-ttu-id="88b96-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="88b96-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="88b96-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="88b96-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="88b96-121">Itslearning uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="88b96-121">Adding itslearning from the gallery</span></span>
2. <span data-ttu-id="88b96-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="88b96-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-itslearning-from-the-gallery"></a><span data-ttu-id="88b96-123">Itslearning uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="88b96-123">Adding itslearning from the gallery</span></span>
<span data-ttu-id="88b96-124">Voor het configureren van de integratie van itslearning in Azure AD, moet u itslearning uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="88b96-124">To configure the integration of itslearning into Azure AD, you need to add itslearning from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="88b96-125">**Als u wilt toevoegen itslearning uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="88b96-125">**To add itslearning from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="88b96-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="88b96-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="88b96-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="88b96-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="88b96-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="88b96-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="88b96-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="88b96-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="88b96-133">Typ in het zoekvak **itslearning**.</span><span class="sxs-lookup"><span data-stu-id="88b96-133">In the search box, type **itslearning**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-itslearning-tutorial/tutorial_itslearning_search.png)

5. <span data-ttu-id="88b96-135">Selecteer in het deelvenster resultaten **itslearning**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="88b96-135">In the results panel, select **itslearning**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-itslearning-tutorial/tutorial_itslearning_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="88b96-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="88b96-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="88b96-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met itslearning op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="88b96-138">In this section, you configure and test Azure AD single sign-on with itslearning based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="88b96-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in itslearning is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="88b96-139">For single sign-on to work, Azure AD needs to know what the counterpart user in itslearning is to a user in Azure AD.</span></span> <span data-ttu-id="88b96-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in itslearning tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="88b96-140">In other words, a link relationship between an Azure AD user and the related user in itslearning needs to be established.</span></span>

<span data-ttu-id="88b96-141">Wijs in itslearning, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="88b96-141">In itslearning, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="88b96-142">Om te configureren en testen van Azure AD eenmalige aanmelding met itslearning, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="88b96-142">To configure and test Azure AD single sign-on with itslearning, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="88b96-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="88b96-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="88b96-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="88b96-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="88b96-145">**[Maken van een testgebruiker itslearning](#creating-an-itslearning-test-user)**  - hebben een equivalent van Britta Simon in itslearning die is gekoppeld aan de Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="88b96-145">**[Creating an itslearning test user](#creating-an-itslearning-test-user)** - to have a counterpart of Britta Simon in itslearning that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="88b96-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="88b96-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="88b96-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="88b96-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="88b96-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="88b96-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="88b96-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing itslearning configureren.</span><span class="sxs-lookup"><span data-stu-id="88b96-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your itslearning application.</span></span>

<span data-ttu-id="88b96-150">**Voor het configureren van Azure AD eenmalige aanmelding met itslearning, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="88b96-150">**To configure Azure AD single sign-on with itslearning, perform the following steps:**</span></span>

1. <span data-ttu-id="88b96-151">In de Azure-portal op de **itslearning** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="88b96-151">In the Azure portal, on the **itslearning** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="88b96-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="88b96-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-itslearning-tutorial/tutorial_itslearning_samlbase.png)

3. <span data-ttu-id="88b96-155">Op de **itslearning domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="88b96-155">On the **itslearning Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-itslearning-tutorial/tutorial_itslearning_url.png)

    <span data-ttu-id="88b96-157">a.</span><span class="sxs-lookup"><span data-stu-id="88b96-157">a.</span></span> <span data-ttu-id="88b96-158">In de **aanmeldings-URL** textbox, typ een URL als:</span><span class="sxs-lookup"><span data-stu-id="88b96-158">In the **Sign-on URL** textbox, type a URL as:</span></span>
    | |
    |--| 
    | `https://www.itslearning.com/index.aspx`|
    | `https://us1.itslearning.com/index.aspx`|

    <span data-ttu-id="88b96-159">b.</span><span class="sxs-lookup"><span data-stu-id="88b96-159">b.</span></span> <span data-ttu-id="88b96-160">In de **id** textbox, typ een URL als:`urn:mace:saml2v2.no:services:com.itslearning`</span><span class="sxs-lookup"><span data-stu-id="88b96-160">In the **Identifier** textbox, type a URL as: `urn:mace:saml2v2.no:services:com.itslearning`</span></span>

4. <span data-ttu-id="88b96-161">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="88b96-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-itslearning-tutorial/tutorial_itslearning_certificate.png) 

5. <span data-ttu-id="88b96-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="88b96-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-itslearning-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="88b96-165">Eenmalige aanmelding configureren op **itslearning** zijde, moet u de gedownloade verzenden **Metadata XML** naar [itslearning ondersteuningsteam](mailto:support@itslearning.com).</span><span class="sxs-lookup"><span data-stu-id="88b96-165">To configure single sign-on on **itslearning** side, you need to send the downloaded **Metadata XML** to [itslearning support team](mailto:support@itslearning.com).</span></span> <span data-ttu-id="88b96-166">Ze deze instelling zodat de SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="88b96-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="88b96-167">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="88b96-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="88b96-168">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="88b96-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="88b96-169">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="88b96-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="88b96-170">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="88b96-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="88b96-171">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="88b96-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="88b96-173">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="88b96-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="88b96-174">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="88b96-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-itslearning-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="88b96-176">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="88b96-176">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-itslearning-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="88b96-178">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="88b96-178">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-itslearning-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="88b96-180">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="88b96-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-itslearning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="88b96-182">a.</span><span class="sxs-lookup"><span data-stu-id="88b96-182">a.</span></span> <span data-ttu-id="88b96-183">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="88b96-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="88b96-184">b.</span><span class="sxs-lookup"><span data-stu-id="88b96-184">b.</span></span> <span data-ttu-id="88b96-185">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="88b96-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="88b96-186">c.</span><span class="sxs-lookup"><span data-stu-id="88b96-186">c.</span></span> <span data-ttu-id="88b96-187">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="88b96-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="88b96-188">d.</span><span class="sxs-lookup"><span data-stu-id="88b96-188">d.</span></span> <span data-ttu-id="88b96-189">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="88b96-189">Click **Create**.</span></span>
 
### <a name="creating-an-itslearning-test-user"></a><span data-ttu-id="88b96-190">Een testgebruiker itslearning maken</span><span class="sxs-lookup"><span data-stu-id="88b96-190">Creating an itslearning test user</span></span>

<span data-ttu-id="88b96-191">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in itslearning maken.</span><span class="sxs-lookup"><span data-stu-id="88b96-191">In this section, you create a user called Britta Simon in itslearning.</span></span> <span data-ttu-id="88b96-192">Werken met [itslearning Client ondersteuningsteam](mailto:support@itslearning.com) de gebruikers van het platform itslearning toevoegen.</span><span class="sxs-lookup"><span data-stu-id="88b96-192">Work with [itslearning Client support team](mailto:support@itslearning.com) to add the users in the itslearning platform.</span></span> <span data-ttu-id="88b96-193">Gebruikers moeten worden gemaakt en worden geactiveerd voordat u eenmalige aanmelding gebruiken.</span><span class="sxs-lookup"><span data-stu-id="88b96-193">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="88b96-194">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="88b96-194">Assigning the Azure AD test user</span></span>

<span data-ttu-id="88b96-195">In deze sectie schakelt u Britta Simon Azure eenmalige aanmelding gebruiken door het verlenen van toegang tot itslearning.</span><span class="sxs-lookup"><span data-stu-id="88b96-195">In this section, you enable Britta Simon to use Azure single sign-on by granting access to itslearning.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="88b96-197">**Britta Simon om aan te wijzen itslearning, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="88b96-197">**To assign Britta Simon to itslearning, perform the following steps:**</span></span>

1. <span data-ttu-id="88b96-198">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="88b96-198">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="88b96-200">Selecteer in de lijst met toepassingen **itslearning**.</span><span class="sxs-lookup"><span data-stu-id="88b96-200">In the applications list, select **itslearning**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-itslearning-tutorial/tutorial_itslearning_app.png) 

3. <span data-ttu-id="88b96-202">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="88b96-202">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="88b96-204">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="88b96-204">Click **Add** button.</span></span> <span data-ttu-id="88b96-205">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="88b96-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="88b96-207">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="88b96-207">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="88b96-208">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="88b96-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="88b96-209">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="88b96-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="88b96-210">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="88b96-210">Testing single sign-on</span></span>

<span data-ttu-id="88b96-211">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="88b96-211">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="88b96-212">Als u op de tegel itslearning in het deelvenster toegang, krijgt u de aanmeldingspagina van itslearning toepassing.</span><span class="sxs-lookup"><span data-stu-id="88b96-212">When you click the itslearning tile in the Access Panel, you should get login page of itslearning application.</span></span> <span data-ttu-id="88b96-213">Klik op **aanmelden met Windows Azure ACS1** voor geslaagde aanmelding in de toepassing.</span><span class="sxs-lookup"><span data-stu-id="88b96-213">Click **Log in with Windows Azure ACS1** for successful login into the application.</span></span>

  ![Aanmelden](./media/active-directory-saas-itslearning-tutorial/login.png)

<span data-ttu-id="88b96-215">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="88b96-215">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="88b96-216">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="88b96-216">Additional resources</span></span>

* [<span data-ttu-id="88b96-217">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="88b96-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="88b96-218">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="88b96-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_203.png

