---
title: 'Zelfstudie: Azure Active Directory-integratie met RealtimeBoard | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en RealtimeBoard.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: a37fc1c0-4bae-4173-989b-00de53a0076f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: jeedes
ms.openlocfilehash: d3ba8cb1f7e1d4332f7912848e8b6902d9acf909
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-realtimeboard"></a><span data-ttu-id="fcc0c-103">Zelfstudie: Azure Active Directory-integratie met RealtimeBoard</span><span class="sxs-lookup"><span data-stu-id="fcc0c-103">Tutorial: Azure Active Directory integration with RealtimeBoard</span></span>

<span data-ttu-id="fcc0c-104">In deze zelfstudie leert u hoe RealtimeBoard integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fcc0c-104">In this tutorial, you learn how to integrate RealtimeBoard with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fcc0c-105">RealtimeBoard integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="fcc0c-105">Integrating RealtimeBoard with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="fcc0c-106">U kunt beheren in Azure AD die toegang tot RealtimeBoard heeft.</span><span class="sxs-lookup"><span data-stu-id="fcc0c-106">You can control in Azure AD who has access to RealtimeBoard.</span></span>
- <span data-ttu-id="fcc0c-107">U kunt uw gebruikers automatisch ophalen aangemeld bij RealtimeBoard (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="fcc0c-107">You can enable your users to automatically get signed-on to RealtimeBoard (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="fcc0c-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="fcc0c-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="fcc0c-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fcc0c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fcc0c-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="fcc0c-110">Prerequisites</span></span>

<span data-ttu-id="fcc0c-111">Voor het configureren van Azure AD-integratie met RealtimeBoard, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="fcc0c-111">To configure Azure AD integration with RealtimeBoard, you need the following items:</span></span>

- <span data-ttu-id="fcc0c-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="fcc0c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fcc0c-113">Een RealtimeBoard eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="fcc0c-113">A RealtimeBoard single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fcc0c-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="fcc0c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fcc0c-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="fcc0c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fcc0c-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="fcc0c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fcc0c-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fcc0c-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fcc0c-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="fcc0c-118">Scenario description</span></span>
<span data-ttu-id="fcc0c-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="fcc0c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fcc0c-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="fcc0c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fcc0c-121">RealtimeBoard uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="fcc0c-121">Adding RealtimeBoard from the gallery</span></span>
2. <span data-ttu-id="fcc0c-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="fcc0c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-realtimeboard-from-the-gallery"></a><span data-ttu-id="fcc0c-123">RealtimeBoard uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="fcc0c-123">Adding RealtimeBoard from the gallery</span></span>
<span data-ttu-id="fcc0c-124">Voor het configureren van de integratie van RealtimeBoard in Azure AD, moet u RealtimeBoard uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="fcc0c-124">To configure the integration of RealtimeBoard into Azure AD, you need to add RealtimeBoard from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="fcc0c-125">**Als u wilt toevoegen RealtimeBoard uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="fcc0c-125">**To add RealtimeBoard from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="fcc0c-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="fcc0c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![De Azure Active Directory-knop][1]

2. <span data-ttu-id="fcc0c-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="fcc0c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="fcc0c-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="fcc0c-129">Then go to **All applications**.</span></span>

    ![De blade Enterprise-toepassingen][2]
    
3. <span data-ttu-id="fcc0c-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="fcc0c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![De knop Nieuw toepassing][3]

4. <span data-ttu-id="fcc0c-133">Typ in het zoekvak **RealtimeBoard**, selecteer **RealtimeBoard** van resultaat deelvenster klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="fcc0c-133">In the search box, type **RealtimeBoard**, select **RealtimeBoard** from result panel then click **Add** button to add the application.</span></span>

    ![RealtimeBoard in de lijst met resultaten](./media/active-directory-saas-realtimeboard-tutorial/tutorial_realtimeboard_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="fcc0c-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="fcc0c-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="fcc0c-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met RealtimeBoard op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="fcc0c-136">In this section, you configure and test Azure AD single sign-on with RealtimeBoard based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="fcc0c-137">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in RealtimeBoard is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fcc0c-137">For single sign-on to work, Azure AD needs to know what the counterpart user in RealtimeBoard is to a user in Azure AD.</span></span> <span data-ttu-id="fcc0c-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in RealtimeBoard tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="fcc0c-138">In other words, a link relationship between an Azure AD user and the related user in RealtimeBoard needs to be established.</span></span>

<span data-ttu-id="fcc0c-139">Wijs in RealtimeBoard, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="fcc0c-139">In RealtimeBoard, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="fcc0c-140">Om te configureren en testen van Azure AD eenmalige aanmelding met RealtimeBoard, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="fcc0c-140">To configure and test Azure AD single sign-on with RealtimeBoard, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="fcc0c-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="fcc0c-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="fcc0c-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fcc0c-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fcc0c-143">**[Maak een testgebruiker RealtimeBoard](#create-a-realtimeboard-test-user)**  - RealtimeBoard die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="fcc0c-143">**[Create a RealtimeBoard test user](#create-a-realtimeboard-test-user)** - to have a counterpart of Britta Simon in RealtimeBoard that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="fcc0c-144">**[Toewijzen van de Azure AD-testgebruiker](#assign-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="fcc0c-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fcc0c-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="fcc0c-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="fcc0c-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="fcc0c-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="fcc0c-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing RealtimeBoard configureren.</span><span class="sxs-lookup"><span data-stu-id="fcc0c-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your RealtimeBoard application.</span></span>

<span data-ttu-id="fcc0c-148">**Voor het configureren van Azure AD eenmalige aanmelding met RealtimeBoard, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="fcc0c-148">**To configure Azure AD single sign-on with RealtimeBoard, perform the following steps:**</span></span>

1. <span data-ttu-id="fcc0c-149">In de Azure-portal op de **RealtimeBoard** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="fcc0c-149">In the Azure portal, on the **RealtimeBoard** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="fcc0c-151">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="fcc0c-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-realtimeboard-tutorial/tutorial_realtimeboard_samlbase.png)

3. <span data-ttu-id="fcc0c-153">Op de **RealtimeBoard domein en de URL's** sectie als u wilt configureren van de toepassing in **IDP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="fcc0c-153">On the **RealtimeBoard Domain and URLs** section, if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![URL's en RealtimeBoard domein eenmalige aanmelding informatie](./media/active-directory-saas-realtimeboard-tutorial/tutorial_realtimeboard_url.png)

    <span data-ttu-id="fcc0c-155">In de **id** textbox, typ een URL als:`https://realtimeboard.com/`</span><span class="sxs-lookup"><span data-stu-id="fcc0c-155">In the **Identifier** textbox, type a URL as: `https://realtimeboard.com/`</span></span>

4. <span data-ttu-id="fcc0c-156">Controleer **weergeven geavanceerde instellingen voor URL**, als u wilt configureren van de toepassing in **SP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="fcc0c-156">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-realtimeboard-tutorial/tutorial_realtimeboard_url2.png)

    <span data-ttu-id="fcc0c-158">In de **aanmeldings-URL** textbox, typ een URL als:`https://realtimeboard.com/sso/saml`</span><span class="sxs-lookup"><span data-stu-id="fcc0c-158">In the **Sign-on URL** textbox, type a URL as: `https://realtimeboard.com/sso/saml`</span></span>

5. <span data-ttu-id="fcc0c-159">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="fcc0c-159">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![De downloadkoppeling certificaat](./media/active-directory-saas-realtimeboard-tutorial/tutorial_realtimeboard_certificate.png) 

6. <span data-ttu-id="fcc0c-161">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="fcc0c-161">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="fcc0c-163">Eenmalige aanmelding configureren op **RealtimeBoard** zijde, moet u de gedownloade verzenden **Metadata XML** naar [RealtimeBoard ondersteuningsteam](mailto:support@realtimeboard.com).</span><span class="sxs-lookup"><span data-stu-id="fcc0c-163">To configure single sign-on on **RealtimeBoard** side, you need to send the downloaded **Metadata XML** to [RealtimeBoard support team](mailto:support@realtimeboard.com).</span></span> <span data-ttu-id="fcc0c-164">Ze deze instelling zodat de SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="fcc0c-164">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="fcc0c-165">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="fcc0c-165">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="fcc0c-166">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="fcc0c-166">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="fcc0c-167">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fcc0c-167">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="fcc0c-168">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="fcc0c-168">Create an Azure AD test user</span></span>

<span data-ttu-id="fcc0c-169">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="fcc0c-169">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="fcc0c-171">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="fcc0c-171">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="fcc0c-172">Klik in de Azure-portal in het linkerdeelvenster op het **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="fcc0c-172">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![De Azure Active Directory-knop](./media/active-directory-saas-realtimeboard-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="fcc0c-174">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="fcc0c-174">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !['Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-realtimeboard-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="fcc0c-176">Openen van de **gebruiker** in het dialoogvenster klikt u op **toevoegen** boven aan de **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="fcc0c-176">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![De knop toevoegen](./media/active-directory-saas-realtimeboard-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="fcc0c-178">In de **gebruiker** dialoogvenster vak, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="fcc0c-178">In the **User** dialog box, perform the following steps:</span></span>

    ![Het dialoogvenster gebruiker](./media/active-directory-saas-realtimeboard-tutorial/create_aaduser_04.png)

    <span data-ttu-id="fcc0c-180">a.</span><span class="sxs-lookup"><span data-stu-id="fcc0c-180">a.</span></span> <span data-ttu-id="fcc0c-181">In de **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fcc0c-181">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fcc0c-182">b.</span><span class="sxs-lookup"><span data-stu-id="fcc0c-182">b.</span></span> <span data-ttu-id="fcc0c-183">In de **gebruikersnaam** typt u het e-mailadres van gebruiker Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fcc0c-183">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="fcc0c-184">c.</span><span class="sxs-lookup"><span data-stu-id="fcc0c-184">c.</span></span> <span data-ttu-id="fcc0c-185">Selecteer de **wachtwoord weergeven** selectievakje, en noteer de waarde die wordt weergegeven in de **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="fcc0c-185">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="fcc0c-186">d.</span><span class="sxs-lookup"><span data-stu-id="fcc0c-186">d.</span></span> <span data-ttu-id="fcc0c-187">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="fcc0c-187">Click **Create**.</span></span>
 
### <a name="create-a-realtimeboard-test-user"></a><span data-ttu-id="fcc0c-188">Een testgebruiker RealtimeBoard maken</span><span class="sxs-lookup"><span data-stu-id="fcc0c-188">Create a RealtimeBoard test user</span></span>

<span data-ttu-id="fcc0c-189">Het doel van deze sectie is het maken van een gebruiker Britta Simon in RealtimeBoard genoemd.</span><span class="sxs-lookup"><span data-stu-id="fcc0c-189">The objective of this section is to create a user called Britta Simon in RealtimeBoard.</span></span> <span data-ttu-id="fcc0c-190">RealtimeBoard ondersteunt just-in-time-inrichting, dit is standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="fcc0c-190">RealtimeBoard supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="fcc0c-191">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="fcc0c-191">There is no action item for you in this section.</span></span> <span data-ttu-id="fcc0c-192">Als een gebruiker in RealtimeBoard nog niet bestaat, wordt een nieuw gemaakt wanneer u probeert te krijgen tot RealtimeBoard.</span><span class="sxs-lookup"><span data-stu-id="fcc0c-192">If a user doesn't already exist in RealtimeBoard, a new one is created when you attempt to access RealtimeBoard.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="fcc0c-193">De Azure AD-testgebruiker toewijzen</span><span class="sxs-lookup"><span data-stu-id="fcc0c-193">Assign the Azure AD test user</span></span>

<span data-ttu-id="fcc0c-194">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan RealtimeBoard.</span><span class="sxs-lookup"><span data-stu-id="fcc0c-194">In this section, you enable Britta Simon to use Azure single sign-on by granting access to RealtimeBoard.</span></span>

![Toewijzen van de gebruikersrol][200] 

<span data-ttu-id="fcc0c-196">**Britta Simon om aan te wijzen RealtimeBoard, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="fcc0c-196">**To assign Britta Simon to RealtimeBoard, perform the following steps:**</span></span>

1. <span data-ttu-id="fcc0c-197">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="fcc0c-197">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="fcc0c-199">Selecteer in de lijst met toepassingen **RealtimeBoard**.</span><span class="sxs-lookup"><span data-stu-id="fcc0c-199">In the applications list, select **RealtimeBoard**.</span></span>

    ![De koppeling RealtimeBoard in de lijst met toepassingen](./media/active-directory-saas-realtimeboard-tutorial/tutorial_realtimeboard_app.png)  

3. <span data-ttu-id="fcc0c-201">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="fcc0c-201">In the menu on the left, click **Users and groups**.</span></span>

    ![De koppeling 'Gebruikers en groepen'][202]

4. <span data-ttu-id="fcc0c-203">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="fcc0c-203">Click **Add** button.</span></span> <span data-ttu-id="fcc0c-204">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="fcc0c-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Het deelvenster toewijzing toevoegen][203]

5. <span data-ttu-id="fcc0c-206">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="fcc0c-206">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="fcc0c-207">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="fcc0c-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fcc0c-208">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="fcc0c-208">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="fcc0c-209">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="fcc0c-209">Test single sign-on</span></span>

<span data-ttu-id="fcc0c-210">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="fcc0c-210">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="fcc0c-211">Als u op de tegel RealtimeBoard in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing RealtimeBoard.</span><span class="sxs-lookup"><span data-stu-id="fcc0c-211">When you click the RealtimeBoard tile in the Access Panel, you should get automatically signed-on to your RealtimeBoard application.</span></span>
<span data-ttu-id="fcc0c-212">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="fcc0c-212">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="fcc0c-213">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="fcc0c-213">Additional resources</span></span>

* [<span data-ttu-id="fcc0c-214">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fcc0c-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fcc0c-215">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="fcc0c-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_203.png

