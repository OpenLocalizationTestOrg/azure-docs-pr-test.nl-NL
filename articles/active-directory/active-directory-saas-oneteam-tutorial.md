---
title: 'Zelfstudie: Azure Active Directory-integratie met Oneteam | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Oneteam.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2e94916c-64ae-4e1a-a8b5-bc6ef7d28c29
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: c4381ca3166bd75bda1179b9a67b2224ba58ae68
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-oneteam"></a><span data-ttu-id="7d6aa-103">Zelfstudie: Azure Active Directory-integratie met Oneteam</span><span class="sxs-lookup"><span data-stu-id="7d6aa-103">Tutorial: Azure Active Directory integration with Oneteam</span></span>

<span data-ttu-id="7d6aa-104">In deze zelfstudie leert u hoe Oneteam integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7d6aa-104">In this tutorial, you learn how to integrate Oneteam with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7d6aa-105">Oneteam integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="7d6aa-105">Integrating Oneteam with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7d6aa-106">U kunt beheren in Azure AD die toegang tot Oneteam heeft</span><span class="sxs-lookup"><span data-stu-id="7d6aa-106">You can control in Azure AD who has access to Oneteam</span></span>
- <span data-ttu-id="7d6aa-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Oneteam (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="7d6aa-107">You can enable your users to automatically get signed-on to Oneteam (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7d6aa-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="7d6aa-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7d6aa-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7d6aa-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7d6aa-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="7d6aa-110">Prerequisites</span></span>

<span data-ttu-id="7d6aa-111">Voor het configureren van Azure AD-integratie met Oneteam, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="7d6aa-111">To configure Azure AD integration with Oneteam, you need the following items:</span></span>

- <span data-ttu-id="7d6aa-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="7d6aa-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7d6aa-113">Een Oneteam eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="7d6aa-113">A Oneteam single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7d6aa-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="7d6aa-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7d6aa-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="7d6aa-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7d6aa-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="7d6aa-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7d6aa-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7d6aa-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7d6aa-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="7d6aa-118">Scenario description</span></span>
<span data-ttu-id="7d6aa-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="7d6aa-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7d6aa-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="7d6aa-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7d6aa-121">Oneteam uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="7d6aa-121">Adding Oneteam from the gallery</span></span>
2. <span data-ttu-id="7d6aa-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="7d6aa-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-oneteam-from-the-gallery"></a><span data-ttu-id="7d6aa-123">Oneteam uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="7d6aa-123">Adding Oneteam from the gallery</span></span>
<span data-ttu-id="7d6aa-124">Voor het configureren van de integratie van Oneteam in Azure AD, moet u Oneteam uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="7d6aa-124">To configure the integration of Oneteam into Azure AD, you need to add Oneteam from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7d6aa-125">**Als u wilt toevoegen Oneteam uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="7d6aa-125">**To add Oneteam from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7d6aa-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="7d6aa-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7d6aa-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="7d6aa-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7d6aa-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="7d6aa-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="7d6aa-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7d6aa-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="7d6aa-133">Typ in het zoekvak **Oneteam**.</span><span class="sxs-lookup"><span data-stu-id="7d6aa-133">In the search box, type **Oneteam**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_search.png)

5. <span data-ttu-id="7d6aa-135">Selecteer in het deelvenster resultaten **Oneteam**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="7d6aa-135">In the results panel, select **Oneteam**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7d6aa-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="7d6aa-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7d6aa-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Oneteam op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="7d6aa-138">In this section, you configure and test Azure AD single sign-on with Oneteam based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7d6aa-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Oneteam is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7d6aa-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Oneteam is to a user in Azure AD.</span></span> <span data-ttu-id="7d6aa-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Oneteam tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="7d6aa-140">In other words, a link relationship between an Azure AD user and the related user in Oneteam needs to be established.</span></span>

<span data-ttu-id="7d6aa-141">Wijs in Oneteam, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="7d6aa-141">In Oneteam, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="7d6aa-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Oneteam, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="7d6aa-142">To configure and test Azure AD single sign-on with Oneteam, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7d6aa-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7d6aa-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7d6aa-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7d6aa-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7d6aa-145">**[Maken van een testgebruiker Oneteam](#creating-a-oneteam-test-user)**  - Oneteam die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="7d6aa-145">**[Creating a Oneteam test user](#creating-a-oneteam-test-user)** - to have a counterpart of Britta Simon in Oneteam that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7d6aa-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="7d6aa-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7d6aa-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="7d6aa-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7d6aa-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="7d6aa-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7d6aa-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Oneteam configureren.</span><span class="sxs-lookup"><span data-stu-id="7d6aa-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Oneteam application.</span></span>

<span data-ttu-id="7d6aa-150">**Voor het configureren van Azure AD eenmalige aanmelding met Oneteam, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="7d6aa-150">**To configure Azure AD single sign-on with Oneteam, perform the following steps:**</span></span>

1. <span data-ttu-id="7d6aa-151">In de Azure-portal op de **Oneteam** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="7d6aa-151">In the Azure portal, on the **Oneteam** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="7d6aa-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="7d6aa-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_samlbase.png)

3. <span data-ttu-id="7d6aa-155">Op de **Oneteam domein en de URL's** sectie als u wilt configureren van de toepassing in **IDP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="7d6aa-155">On the **Oneteam Domain and URLs** section, if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_url.png)

    <span data-ttu-id="7d6aa-157">a.</span><span class="sxs-lookup"><span data-stu-id="7d6aa-157">a.</span></span> <span data-ttu-id="7d6aa-158">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://api.one-team.io/teams/<team name>`</span><span class="sxs-lookup"><span data-stu-id="7d6aa-158">In the **Identifier** textbox, type a URL using the following pattern: `https://api.one-team.io/teams/<team name>`</span></span>

    <span data-ttu-id="7d6aa-159">b.</span><span class="sxs-lookup"><span data-stu-id="7d6aa-159">b.</span></span> <span data-ttu-id="7d6aa-160">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://api.one-team.io/teams/<team name>/auth/saml/callback`</span><span class="sxs-lookup"><span data-stu-id="7d6aa-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://api.one-team.io/teams/<team name>/auth/saml/callback`</span></span>

4. <span data-ttu-id="7d6aa-161">Controleer **weergeven geavanceerde instellingen voor URL**, als u wilt configureren van de toepassing in **SP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="7d6aa-161">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_url1.png)

    <span data-ttu-id="7d6aa-163">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<team name>.one-team.io/`</span><span class="sxs-lookup"><span data-stu-id="7d6aa-163">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<team name>.one-team.io/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="7d6aa-164">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="7d6aa-164">These values are not real.</span></span> <span data-ttu-id="7d6aa-165">Deze waarden bijwerken met de werkelijke id, antwoord-URL en aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="7d6aa-165">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="7d6aa-166">Neem contact op met [Oneteam Client ondersteuningsteam](https://support.one-team.com/hc/requests/new) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="7d6aa-166">Contact [Oneteam Client support team](https://support.one-team.com/hc/requests/new) to get these values.</span></span> 



5. <span data-ttu-id="7d6aa-167">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="7d6aa-167">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_certificate.png) 

6. <span data-ttu-id="7d6aa-169">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="7d6aa-169">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-oneteam-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="7d6aa-171">Als u eenmalige aanmelding voor uw toepassing is geconfigureerd, kunt u de ondersteuningsticket met verhogen [Oneteam ondersteuningsteam](https://support.one-team.com/hc/requests/new) en geeft u de gedownloade **metagegevens**.</span><span class="sxs-lookup"><span data-stu-id="7d6aa-171">To get SSO configured for your application, you can raise the support ticket with [Oneteam support team](https://support.one-team.com/hc/requests/new) and provide them the downloaded **Metadata**.</span></span> 

> [!TIP]
> <span data-ttu-id="7d6aa-172">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="7d6aa-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7d6aa-173">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="7d6aa-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7d6aa-174">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7d6aa-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7d6aa-175">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="7d6aa-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="7d6aa-176">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="7d6aa-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="7d6aa-178">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="7d6aa-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7d6aa-179">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="7d6aa-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-oneteam-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7d6aa-181">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="7d6aa-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-oneteam-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7d6aa-183">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7d6aa-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-oneteam-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7d6aa-185">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="7d6aa-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-oneteam-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7d6aa-187">a.</span><span class="sxs-lookup"><span data-stu-id="7d6aa-187">a.</span></span> <span data-ttu-id="7d6aa-188">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7d6aa-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7d6aa-189">b.</span><span class="sxs-lookup"><span data-stu-id="7d6aa-189">b.</span></span> <span data-ttu-id="7d6aa-190">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7d6aa-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7d6aa-191">c.</span><span class="sxs-lookup"><span data-stu-id="7d6aa-191">c.</span></span> <span data-ttu-id="7d6aa-192">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="7d6aa-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7d6aa-193">d.</span><span class="sxs-lookup"><span data-stu-id="7d6aa-193">d.</span></span> <span data-ttu-id="7d6aa-194">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="7d6aa-194">Click **Create**.</span></span>
 
### <a name="creating-a-oneteam-test-user"></a><span data-ttu-id="7d6aa-195">Een testgebruiker Oneteam maken</span><span class="sxs-lookup"><span data-stu-id="7d6aa-195">Creating a Oneteam test user</span></span>

<span data-ttu-id="7d6aa-196">Het doel van deze sectie is het maken van een gebruiker Britta Simon in Oneteam genoemd.</span><span class="sxs-lookup"><span data-stu-id="7d6aa-196">The objective of this section is to create a user called Britta Simon in Oneteam.</span></span> <span data-ttu-id="7d6aa-197">Oneteam ondersteunt just-in-time-inrichting, dit is standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="7d6aa-197">Oneteam supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="7d6aa-198">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="7d6aa-198">There is no action item for you in this section.</span></span> <span data-ttu-id="7d6aa-199">Een nieuwe gebruiker wordt gemaakt tijdens een poging tot toegang tot Oneteam, als deze nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="7d6aa-199">A new user will be created during an attempt to access Oneteam, if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="7d6aa-200">Als u een gebruiker handmatig maken moet, kunt u de ondersteuningsticket met verhogen [Oneteam ondersteuningsteam](https://support.one-team.com/hc/requests/new).</span><span class="sxs-lookup"><span data-stu-id="7d6aa-200">If you need to create an user manually, you can raise the support ticket with [Oneteam support team](https://support.one-team.com/hc/requests/new).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7d6aa-201">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="7d6aa-201">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7d6aa-202">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Oneteam.</span><span class="sxs-lookup"><span data-stu-id="7d6aa-202">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Oneteam.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="7d6aa-204">**Britta Simon om aan te wijzen Oneteam, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="7d6aa-204">**To assign Britta Simon to Oneteam, perform the following steps:**</span></span>

1. <span data-ttu-id="7d6aa-205">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="7d6aa-205">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="7d6aa-207">Selecteer in de lijst met toepassingen **Oneteam**.</span><span class="sxs-lookup"><span data-stu-id="7d6aa-207">In the applications list, select **Oneteam**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_app.png) 

3. <span data-ttu-id="7d6aa-209">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="7d6aa-209">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="7d6aa-211">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="7d6aa-211">Click **Add** button.</span></span> <span data-ttu-id="7d6aa-212">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7d6aa-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="7d6aa-214">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="7d6aa-214">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7d6aa-215">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7d6aa-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7d6aa-216">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7d6aa-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7d6aa-217">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="7d6aa-217">Testing single sign-on</span></span>

<span data-ttu-id="7d6aa-218">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="7d6aa-218">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="7d6aa-219">Als u op de tegel Oneteam in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Oneteam.</span><span class="sxs-lookup"><span data-stu-id="7d6aa-219">When you click the Oneteam tile in the Access Panel, you should get automatically signed-on to your Oneteam application.</span></span>
<span data-ttu-id="7d6aa-220">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7d6aa-220">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7d6aa-221">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="7d6aa-221">Additional resources</span></span>

* [<span data-ttu-id="7d6aa-222">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7d6aa-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7d6aa-223">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7d6aa-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_203.png

