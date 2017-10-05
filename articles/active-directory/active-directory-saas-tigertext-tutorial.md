---
title: 'Zelfstudie: Azure Active Directory-integratie met TigerText Secure Messenger | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en TigerText Secure Messenger.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 03f1e128-5bcb-4e49-b6a3-fe22eedc6d5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.openlocfilehash: e101e5fc84b032b66dd0636bab8bff128791f77c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tigertext-secure-messenger"></a><span data-ttu-id="1560a-103">Zelfstudie: Azure Active Directory-integratie met TigerText Secure Messenger</span><span class="sxs-lookup"><span data-stu-id="1560a-103">Tutorial: Azure Active Directory integration with TigerText Secure Messenger</span></span>

<span data-ttu-id="1560a-104">In deze zelfstudie leert u hoe TigerText Secure Messenger integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1560a-104">In this tutorial, you learn how to integrate TigerText Secure Messenger with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1560a-105">TigerText Secure Messenger integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="1560a-105">Integrating TigerText Secure Messenger with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1560a-106">U kunt beheren in Azure AD die toegang tot TigerText Secure Messenger heeft</span><span class="sxs-lookup"><span data-stu-id="1560a-106">You can control in Azure AD who has access to TigerText Secure Messenger</span></span>
- <span data-ttu-id="1560a-107">U kunt uw gebruikers automatisch ophalen aangemeld bij TigerText Secure Messenger (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="1560a-107">You can enable your users to automatically get signed-on to TigerText Secure Messenger (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1560a-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="1560a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1560a-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1560a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1560a-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="1560a-110">Prerequisites</span></span>

<span data-ttu-id="1560a-111">Voor het configureren van Azure AD-integratie met TigerText Secure Messenger, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="1560a-111">To configure Azure AD integration with TigerText Secure Messenger, you need the following items:</span></span>

- <span data-ttu-id="1560a-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="1560a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1560a-113">Een TigerText Secure Messenger eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="1560a-113">A TigerText Secure Messenger single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1560a-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="1560a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1560a-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="1560a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1560a-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="1560a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1560a-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1560a-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1560a-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="1560a-118">Scenario description</span></span>
<span data-ttu-id="1560a-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="1560a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1560a-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="1560a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1560a-121">TigerText Secure Messenger uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="1560a-121">Add TigerText Secure Messenger from the gallery</span></span>
2. <span data-ttu-id="1560a-122">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="1560a-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-tigertext-secure-messenger-from-the-gallery"></a><span data-ttu-id="1560a-123">TigerText Secure Messenger uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="1560a-123">Add TigerText Secure Messenger from the gallery</span></span>
<span data-ttu-id="1560a-124">Voor het configureren van de integratie van TigerText Secure Messenger in Azure AD, moet u TigerText Secure Messenger uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="1560a-124">To configure the integration of TigerText Secure Messenger into Azure AD, you need to add TigerText Secure Messenger from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1560a-125">**Als u wilt toevoegen TigerText Secure Messenger uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="1560a-125">**To add TigerText Secure Messenger from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1560a-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="1560a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1560a-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="1560a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1560a-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="1560a-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="1560a-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1560a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="1560a-133">Typ in het zoekvak **TigerText Secure Messenger**, selecteer **TigerText Secure Messenger** van resultaat deelvenster klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="1560a-133">In the search box, type **TigerText Secure Messenger**, select **TigerText Secure Messenger** from result panel then click **Add** button to add the application.</span></span>

    ![Uit de galerie toevoegen](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="1560a-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="1560a-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="1560a-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met TigerText Secure Messenger op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="1560a-136">In this section, you configure and test Azure AD single sign-on with TigerText Secure Messenger based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1560a-137">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in TigerText Secure Messenger is aan een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1560a-137">For single sign-on to work, Azure AD needs to know what the counterpart user in TigerText Secure Messenger is to a user in Azure AD.</span></span> <span data-ttu-id="1560a-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante TigerText Secure Messenger-gebruiker worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1560a-138">In other words, a link relationship between an Azure AD user and the related user in TigerText Secure Messenger needs to be established.</span></span>

<span data-ttu-id="1560a-139">Wijs in TigerText Secure Messenger, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="1560a-139">In TigerText Secure Messenger, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1560a-140">Om te configureren en testen van Azure AD eenmalige aanmelding met TigerText Secure Messenger, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="1560a-140">To configure and test Azure AD single sign-on with TigerText Secure Messenger, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1560a-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1560a-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1560a-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1560a-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1560a-143">**[Maak een testgebruiker TigerText Secure Messenger](#create-a-tigertext-secure-messenger-test-user)**  - TigerText Secure Messenger die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="1560a-143">**[Create a TigerText Secure Messenger test user](#create-a-tigertext-secure-messenger-test-user)** - to have a counterpart of Britta Simon in TigerText Secure Messenger that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1560a-144">**[Toewijzen van de Azure AD-testgebruiker](#assign-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="1560a-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1560a-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="1560a-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="1560a-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="1560a-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="1560a-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw toepassing TigerText Secure Messenger.</span><span class="sxs-lookup"><span data-stu-id="1560a-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TigerText Secure Messenger application.</span></span>

<span data-ttu-id="1560a-148">**Voor het configureren van Azure AD eenmalige aanmelding met TigerText Secure Messenger, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="1560a-148">**To configure Azure AD single sign-on with TigerText Secure Messenger, perform the following steps:**</span></span>

1. <span data-ttu-id="1560a-149">In de Azure-portal op de **TigerText Secure Messenger** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="1560a-149">In the Azure portal, on the **TigerText Secure Messenger** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="1560a-151">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="1560a-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Op basis van SAML eenmalige aanmelding](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_samlbase.png)

3. <span data-ttu-id="1560a-153">Op de **TigerText Secure Messenger domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="1560a-153">On the **TigerText Secure Messenger Domain and URLs** section, perform the following steps:</span></span>

    ![Sectie TigerText Secure Messenger domein en URL 's](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_url.png)

    <span data-ttu-id="1560a-155">a.</span><span class="sxs-lookup"><span data-stu-id="1560a-155">a.</span></span> <span data-ttu-id="1560a-156">In de **aanmeldings-URL** textbox, typ de URL als:`https://home.tigertext.com`</span><span class="sxs-lookup"><span data-stu-id="1560a-156">In the **Sign-on URL** textbox, type URL as: `https://home.tigertext.com`</span></span>

    <span data-ttu-id="1560a-157">b.</span><span class="sxs-lookup"><span data-stu-id="1560a-157">b.</span></span> <span data-ttu-id="1560a-158">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://saml-lb.tigertext.me/v1/organization/<instance Id>`</span><span class="sxs-lookup"><span data-stu-id="1560a-158">In the **Identifier** textbox, type a URL using the following pattern: `https://saml-lb.tigertext.me/v1/organization/<instance Id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1560a-159">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="1560a-159">This value is not real.</span></span> <span data-ttu-id="1560a-160">Deze waarde door de werkelijke ID bijwerken.</span><span class="sxs-lookup"><span data-stu-id="1560a-160">Update this value with the actual Identifier.</span></span> <span data-ttu-id="1560a-161">Neem contact op met [TigerText Secure Messenger-Client-ondersteuningsteam](mailTo:prosupport@tigertext.com) deze waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="1560a-161">Contact [TigerText Secure Messenger Client support team](mailTo:prosupport@tigertext.com) to get this value.</span></span> 
 
4. <span data-ttu-id="1560a-162">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="1560a-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Certificaat voor ondertekening van SAML-sectie](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_certificate.png) 

5. <span data-ttu-id="1560a-164">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="1560a-164">Click **Save** button.</span></span>

    ![De knop Opslaan](./media/active-directory-saas-tigertext-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1560a-166">Als u eenmalige aanmelding configureren voor uw toepassing, neem contact op met [TigerText Secure Messenger ondersteuningsteam](mailTo:prosupport@tigertext.com) en geeft u de **gedownloade metagegevens**.</span><span class="sxs-lookup"><span data-stu-id="1560a-166">To get single sign-on configured for your application, contact [TigerText Secure Messenger support team](mailTo:prosupport@tigertext.com) and provide them the **Downloaded metadata**.</span></span>

> [!TIP]
> <span data-ttu-id="1560a-167">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="1560a-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1560a-168">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="1560a-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1560a-169">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1560a-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="1560a-170">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="1560a-170">Create an Azure AD test user</span></span>
<span data-ttu-id="1560a-171">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="1560a-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="1560a-173">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="1560a-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1560a-174">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="1560a-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tigertext-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1560a-176">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="1560a-176">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Gebruikers en groepen -> alle gebruikers](./media/active-directory-saas-tigertext-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1560a-178">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1560a-178">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Knop toevoegen](./media/active-directory-saas-tigertext-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1560a-180">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="1560a-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Gebruikersdialoogvenster](./media/active-directory-saas-tigertext-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1560a-182">a.</span><span class="sxs-lookup"><span data-stu-id="1560a-182">a.</span></span> <span data-ttu-id="1560a-183">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1560a-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1560a-184">b.</span><span class="sxs-lookup"><span data-stu-id="1560a-184">b.</span></span> <span data-ttu-id="1560a-185">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1560a-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1560a-186">c.</span><span class="sxs-lookup"><span data-stu-id="1560a-186">c.</span></span> <span data-ttu-id="1560a-187">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="1560a-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1560a-188">d.</span><span class="sxs-lookup"><span data-stu-id="1560a-188">d.</span></span> <span data-ttu-id="1560a-189">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="1560a-189">Click **Create**.</span></span>
 
### <a name="create-a-tigertext-secure-messenger-test-user"></a><span data-ttu-id="1560a-190">Een testgebruiker TigerText Secure Messenger maken</span><span class="sxs-lookup"><span data-stu-id="1560a-190">Create a TigerText Secure Messenger test user</span></span>

<span data-ttu-id="1560a-191">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in TigerText maken.</span><span class="sxs-lookup"><span data-stu-id="1560a-191">In this section, you create a user called Britta Simon in TigerText.</span></span> <span data-ttu-id="1560a-192">Neem bereiken [TigerText Secure Messenger-Client-ondersteuningsteam](mailTo:prosupport@tigertext.com) de gebruikers van het platform TigerText toevoegen.</span><span class="sxs-lookup"><span data-stu-id="1560a-192">Please reach out to [TigerText Secure Messenger Client support team](mailTo:prosupport@tigertext.com) to add the users in the TigerText platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="1560a-193">De Azure AD-testgebruiker toewijzen</span><span class="sxs-lookup"><span data-stu-id="1560a-193">Assign the Azure AD test user</span></span>

<span data-ttu-id="1560a-194">In deze sectie maakt inschakelen u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan TigerText Secure Messenger.</span><span class="sxs-lookup"><span data-stu-id="1560a-194">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TigerText Secure Messenger.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="1560a-196">**Britta Simon om aan te wijzen TigerText Secure Messenger, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="1560a-196">**To assign Britta Simon to TigerText Secure Messenger, perform the following steps:**</span></span>

1. <span data-ttu-id="1560a-197">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="1560a-197">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="1560a-199">Selecteer in de lijst met toepassingen **TigerText Secure Messenger**.</span><span class="sxs-lookup"><span data-stu-id="1560a-199">In the applications list, select **TigerText Secure Messenger**.</span></span>

    ![TigerText Secure Messenger in lijst met Apps](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_app.png) 

3. <span data-ttu-id="1560a-201">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="1560a-201">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="1560a-203">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="1560a-203">Click **Add** button.</span></span> <span data-ttu-id="1560a-204">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1560a-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="1560a-206">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="1560a-206">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1560a-207">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1560a-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1560a-208">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1560a-208">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="1560a-209">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="1560a-209">Test single sign-on</span></span>

<span data-ttu-id="1560a-210">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="1560a-210">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1560a-211">Als u op de tegel TigerText in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing TigerText.</span><span class="sxs-lookup"><span data-stu-id="1560a-211">When you click the TigerText tile in the Access Panel, you should get automatically signed-on to your TigerText application.</span></span> <span data-ttu-id="1560a-212">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1560a-212">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1560a-213">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="1560a-213">Additional resources</span></span>

* [<span data-ttu-id="1560a-214">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1560a-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1560a-215">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1560a-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_203.png

