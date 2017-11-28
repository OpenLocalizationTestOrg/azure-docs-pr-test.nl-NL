---
title: 'Zelfstudie: Azure Active Directory-integratie met ZIVVER | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en ZIVVER.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 64cb7ea0-df6c-4963-84d8-6f435980e2de
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: d27c773baaae64922fc8ad2c8f65bab177769f67
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zivver"></a><span data-ttu-id="9d763-103">Zelfstudie: Azure Active Directory-integratie met ZIVVER</span><span class="sxs-lookup"><span data-stu-id="9d763-103">Tutorial: Azure Active Directory integration with ZIVVER</span></span>

<span data-ttu-id="9d763-104">In deze zelfstudie leert u hoe ZIVVER integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9d763-104">In this tutorial, you learn how to integrate ZIVVER with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9d763-105">ZIVVER integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="9d763-105">Integrating ZIVVER with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9d763-106">U kunt beheren in Azure AD die toegang tot ZIVVER heeft.</span><span class="sxs-lookup"><span data-stu-id="9d763-106">You can control in Azure AD who has access to ZIVVER.</span></span>
- <span data-ttu-id="9d763-107">U kunt uw gebruikers automatisch ophalen aangemeld bij ZIVVER (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="9d763-107">You can enable your users to automatically get signed-on to ZIVVER (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="9d763-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="9d763-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="9d763-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9d763-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9d763-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="9d763-110">Prerequisites</span></span>

<span data-ttu-id="9d763-111">Voor het configureren van Azure AD-integratie met ZIVVER, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="9d763-111">To configure Azure AD integration with ZIVVER, you need the following items:</span></span>

- <span data-ttu-id="9d763-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="9d763-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9d763-113">Een ZIVVER eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="9d763-113">A ZIVVER single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9d763-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="9d763-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9d763-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="9d763-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9d763-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="9d763-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9d763-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9d763-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9d763-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="9d763-118">Scenario description</span></span>
<span data-ttu-id="9d763-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="9d763-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9d763-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="9d763-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9d763-121">ZIVVER uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="9d763-121">Adding ZIVVER from the gallery</span></span>
2. <span data-ttu-id="9d763-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="9d763-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zivver-from-the-gallery"></a><span data-ttu-id="9d763-123">ZIVVER uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="9d763-123">Adding ZIVVER from the gallery</span></span>
<span data-ttu-id="9d763-124">Voor het configureren van de integratie van ZIVVER in Azure AD, moet u ZIVVER uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="9d763-124">To configure the integration of ZIVVER into Azure AD, you need to add ZIVVER from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9d763-125">**Als u wilt toevoegen ZIVVER uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="9d763-125">**To add ZIVVER from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9d763-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="9d763-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![De Azure Active Directory-knop][1]

2. <span data-ttu-id="9d763-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="9d763-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9d763-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="9d763-129">Then go to **All applications**.</span></span>

    ![De blade Enterprise-toepassingen][2]
    
3. <span data-ttu-id="9d763-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9d763-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![De knop Nieuw toepassing][3]

4. <span data-ttu-id="9d763-133">Typ in het zoekvak **ZIVVER**, selecteer **ZIVVER** van resultaat deelvenster klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="9d763-133">In the search box, type **ZIVVER**, select **ZIVVER** from result panel then click **Add** button to add the application.</span></span>

    ![ZIVVER in de lijst met resultaten](./media/active-directory-saas-zivver-tutorial/tutorial_zivver_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="9d763-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="9d763-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="9d763-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met ZIVVER op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="9d763-136">In this section, you configure and test Azure AD single sign-on with ZIVVER based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9d763-137">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in ZIVVER is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9d763-137">For single sign-on to work, Azure AD needs to know what the counterpart user in ZIVVER is to a user in Azure AD.</span></span> <span data-ttu-id="9d763-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in ZIVVER tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="9d763-138">In other words, a link relationship between an Azure AD user and the related user in ZIVVER needs to be established.</span></span>

<span data-ttu-id="9d763-139">Wijs in ZIVVER, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="9d763-139">In ZIVVER, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="9d763-140">Om te configureren en testen van Azure AD eenmalige aanmelding met ZIVVER, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="9d763-140">To configure and test Azure AD single sign-on with ZIVVER, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9d763-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="9d763-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9d763-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9d763-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9d763-143">**[Maak een testgebruiker ZIVVER](#create-a-zivver-test-user)**  - ZIVVER die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="9d763-143">**[Create a ZIVVER test user](#create-a-zivver-test-user)** - to have a counterpart of Britta Simon in ZIVVER that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9d763-144">**[Toewijzen van de Azure AD-testgebruiker](#assign-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="9d763-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9d763-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="9d763-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="9d763-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="9d763-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="9d763-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing ZIVVER configureren.</span><span class="sxs-lookup"><span data-stu-id="9d763-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ZIVVER application.</span></span>

<span data-ttu-id="9d763-148">**Voor het configureren van Azure AD eenmalige aanmelding met ZIVVER, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="9d763-148">**To configure Azure AD single sign-on with ZIVVER, perform the following steps:**</span></span>

1. <span data-ttu-id="9d763-149">In de Azure-portal op de **ZIVVER** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="9d763-149">In the Azure portal, on the **ZIVVER** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="9d763-151">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="9d763-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-zivver-tutorial/tutorial_zivver_samlbase.png)

3. <span data-ttu-id="9d763-153">Op de **ZIVVER domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="9d763-153">On the **ZIVVER Domain and URLs** section, perform the following steps:</span></span>

    ![URL's en ZIVVER domein eenmalige aanmelding informatie](./media/active-directory-saas-zivver-tutorial/tutorial_zivver_url.png)

    <span data-ttu-id="9d763-155">In de **id** textbox, typ de URL:`https://app.zivver.com/SAML/Zivver`</span><span class="sxs-lookup"><span data-stu-id="9d763-155">In the **Identifier** textbox, type the URL: `https://app.zivver.com/SAML/Zivver`</span></span>

4. <span data-ttu-id="9d763-156">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="9d763-156">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![De downloadkoppeling certificaat](./media/active-directory-saas-zivver-tutorial/tutorial_zivver_certificate.png) 

5. <span data-ttu-id="9d763-158">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="9d763-158">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-zivver-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9d763-160">Eenmalige aanmelding configureren op **ZIVVER** zijde, moet u de gedownloade verzenden **Metadata XML** naar [ZIVVER ondersteuningsteam](https://support.zivver.com).</span><span class="sxs-lookup"><span data-stu-id="9d763-160">To configure single sign-on on **ZIVVER** side, you need to send the downloaded **Metadata XML** to [ZIVVER support team](https://support.zivver.com).</span></span> <span data-ttu-id="9d763-161">Ze deze instelling zodat de SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="9d763-161">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="9d763-162">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="9d763-162">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9d763-163">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="9d763-163">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9d763-164">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9d763-164">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="9d763-165">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="9d763-165">Create an Azure AD test user</span></span>

<span data-ttu-id="9d763-166">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="9d763-166">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="9d763-168">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="9d763-168">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9d763-169">Klik in de Azure-portal in het linkerdeelvenster op het **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="9d763-169">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![De Azure Active Directory-knop](./media/active-directory-saas-zivver-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="9d763-171">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="9d763-171">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !['Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-zivver-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="9d763-173">Openen van de **gebruiker** in het dialoogvenster klikt u op **toevoegen** boven aan de **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9d763-173">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![De knop toevoegen](./media/active-directory-saas-zivver-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="9d763-175">In de **gebruiker** dialoogvenster vak, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="9d763-175">In the **User** dialog box, perform the following steps:</span></span>

    ![Het dialoogvenster gebruiker](./media/active-directory-saas-zivver-tutorial/create_aaduser_04.png)

    <span data-ttu-id="9d763-177">a.</span><span class="sxs-lookup"><span data-stu-id="9d763-177">a.</span></span> <span data-ttu-id="9d763-178">In de **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9d763-178">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9d763-179">b.</span><span class="sxs-lookup"><span data-stu-id="9d763-179">b.</span></span> <span data-ttu-id="9d763-180">In de **gebruikersnaam** typt u het e-mailadres van gebruiker Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9d763-180">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="9d763-181">c.</span><span class="sxs-lookup"><span data-stu-id="9d763-181">c.</span></span> <span data-ttu-id="9d763-182">Selecteer de **wachtwoord weergeven** selectievakje, en noteer de waarde die wordt weergegeven in de **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="9d763-182">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="9d763-183">d.</span><span class="sxs-lookup"><span data-stu-id="9d763-183">d.</span></span> <span data-ttu-id="9d763-184">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="9d763-184">Click **Create**.</span></span>
  
### <a name="create-a-zivver-test-user"></a><span data-ttu-id="9d763-185">Een testgebruiker ZIVVER maken</span><span class="sxs-lookup"><span data-stu-id="9d763-185">Create a ZIVVER test user</span></span>

<span data-ttu-id="9d763-186">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in ZIVVER maken.</span><span class="sxs-lookup"><span data-stu-id="9d763-186">In this section, you create a user called Britta Simon in ZIVVER.</span></span> <span data-ttu-id="9d763-187">Werken met [ZIVVER ondersteuningsteam](https://support.zivver.com) de gebruikers van het platform ZIVVER toevoegen.</span><span class="sxs-lookup"><span data-stu-id="9d763-187">Work with [ZIVVER support team](https://support.zivver.com) to add the users in the ZIVVER platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="9d763-188">De Azure AD-testgebruiker toewijzen</span><span class="sxs-lookup"><span data-stu-id="9d763-188">Assign the Azure AD test user</span></span>

<span data-ttu-id="9d763-189">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan ZIVVER.</span><span class="sxs-lookup"><span data-stu-id="9d763-189">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ZIVVER.</span></span>

![Toewijzen van de gebruikersrol][200] 

<span data-ttu-id="9d763-191">**Britta Simon om aan te wijzen ZIVVER, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="9d763-191">**To assign Britta Simon to ZIVVER, perform the following steps:**</span></span>

1. <span data-ttu-id="9d763-192">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="9d763-192">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="9d763-194">Selecteer in de lijst met toepassingen **ZIVVER**.</span><span class="sxs-lookup"><span data-stu-id="9d763-194">In the applications list, select **ZIVVER**.</span></span>

    ![De koppeling ZIVVER in de lijst met toepassingen](./media/active-directory-saas-zivver-tutorial/tutorial_zivver_app.png)  

3. <span data-ttu-id="9d763-196">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="9d763-196">In the menu on the left, click **Users and groups**.</span></span>

    ![De koppeling 'Gebruikers en groepen'][202]

4. <span data-ttu-id="9d763-198">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="9d763-198">Click **Add** button.</span></span> <span data-ttu-id="9d763-199">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9d763-199">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Het deelvenster toewijzing toevoegen][203]

5. <span data-ttu-id="9d763-201">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="9d763-201">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9d763-202">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9d763-202">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9d763-203">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9d763-203">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="9d763-204">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="9d763-204">Test single sign-on</span></span>

<span data-ttu-id="9d763-205">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="9d763-205">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="9d763-206">Als u op de tegel ZIVVER in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing ZIVVER.</span><span class="sxs-lookup"><span data-stu-id="9d763-206">When you click the ZIVVER tile in the Access Panel, you should get automatically signed-on to your ZIVVER application.</span></span>
<span data-ttu-id="9d763-207">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9d763-207">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="9d763-208">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="9d763-208">Additional resources</span></span>

* [<span data-ttu-id="9d763-209">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9d763-209">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9d763-210">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9d763-210">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_203.png

