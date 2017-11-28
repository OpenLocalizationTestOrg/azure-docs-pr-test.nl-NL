---
title: 'Zelfstudie: Azure Active Directory-integratie met Synergi | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Synergi.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 73c970e1-f1ba-420b-b225-414fdf93b140
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: jeedes
ms.openlocfilehash: dedbe96fbb26bc34c4d7e213892b318f0e6fef12
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-synergi"></a><span data-ttu-id="25eca-103">Zelfstudie: Azure Active Directory-integratie met Synergi</span><span class="sxs-lookup"><span data-stu-id="25eca-103">Tutorial: Azure Active Directory integration with Synergi</span></span>

<span data-ttu-id="25eca-104">In deze zelfstudie leert u hoe Synergi integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="25eca-104">In this tutorial, you learn how to integrate Synergi with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="25eca-105">Synergi integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="25eca-105">Integrating Synergi with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="25eca-106">U kunt beheren in Azure AD die toegang tot Synergi heeft.</span><span class="sxs-lookup"><span data-stu-id="25eca-106">You can control in Azure AD who has access to Synergi.</span></span>
- <span data-ttu-id="25eca-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Synergi (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="25eca-107">You can enable your users to automatically get signed-on to Synergi (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="25eca-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="25eca-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="25eca-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="25eca-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="25eca-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="25eca-110">Prerequisites</span></span>

<span data-ttu-id="25eca-111">Voor het configureren van Azure AD-integratie met Synergi, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="25eca-111">To configure Azure AD integration with Synergi, you need the following items:</span></span>

- <span data-ttu-id="25eca-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="25eca-112">An Azure AD subscription</span></span>
- <span data-ttu-id="25eca-113">Een Synergi eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="25eca-113">A Synergi single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="25eca-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="25eca-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="25eca-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="25eca-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="25eca-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="25eca-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="25eca-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="25eca-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="25eca-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="25eca-118">Scenario description</span></span>
<span data-ttu-id="25eca-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="25eca-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="25eca-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="25eca-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="25eca-121">Synergi uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="25eca-121">Adding Synergi from the gallery</span></span>
2. <span data-ttu-id="25eca-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="25eca-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-synergi-from-the-gallery"></a><span data-ttu-id="25eca-123">Synergi uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="25eca-123">Adding Synergi from the gallery</span></span>
<span data-ttu-id="25eca-124">Voor het configureren van de integratie van Synergi in Azure AD, moet u Synergi uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="25eca-124">To configure the integration of Synergi into Azure AD, you need to add Synergi from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="25eca-125">**Als u wilt toevoegen Synergi uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="25eca-125">**To add Synergi from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="25eca-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="25eca-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![De Azure Active Directory-knop][1]

2. <span data-ttu-id="25eca-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="25eca-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="25eca-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="25eca-129">Then go to **All applications**.</span></span>

    ![De blade Enterprise-toepassingen][2]
    
3. <span data-ttu-id="25eca-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="25eca-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![De knop Nieuw toepassing][3]

4. <span data-ttu-id="25eca-133">Typ in het zoekvak **Synergi**, selecteer **Synergi** van resultaat deelvenster klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="25eca-133">In the search box, type **Synergi**, select **Synergi** from result panel then click **Add** button to add the application.</span></span>

    ![Synergi in de lijst met resultaten](./media/active-directory-saas-synergi-tutorial/tutorial_synergi_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="25eca-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="25eca-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="25eca-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met Synergi op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="25eca-136">In this section, you configure and test Azure AD single sign-on with Synergi based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="25eca-137">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Synergi is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="25eca-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Synergi is to a user in Azure AD.</span></span> <span data-ttu-id="25eca-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Synergi tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="25eca-138">In other words, a link relationship between an Azure AD user and the related user in Synergi needs to be established.</span></span>

<span data-ttu-id="25eca-139">Wijs in Synergi, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="25eca-139">In Synergi, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="25eca-140">Om te configureren en testen van Azure AD eenmalige aanmelding met Synergi, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="25eca-140">To configure and test Azure AD single sign-on with Synergi, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="25eca-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="25eca-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="25eca-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="25eca-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="25eca-143">**[Maak een testgebruiker Synergi](#create-a-synergi-test-user)**  - Synergi die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="25eca-143">**[Create a Synergi test user](#create-a-synergi-test-user)** - to have a counterpart of Britta Simon in Synergi that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="25eca-144">**[Toewijzen van de Azure AD-testgebruiker](#assign-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="25eca-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="25eca-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="25eca-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="25eca-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="25eca-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="25eca-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Synergi configureren.</span><span class="sxs-lookup"><span data-stu-id="25eca-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Synergi application.</span></span>

<span data-ttu-id="25eca-148">**Voor het configureren van Azure AD eenmalige aanmelding met Synergi, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="25eca-148">**To configure Azure AD single sign-on with Synergi, perform the following steps:**</span></span>

1. <span data-ttu-id="25eca-149">In de Azure-portal op de **Synergi** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="25eca-149">In the Azure portal, on the **Synergi** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="25eca-151">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="25eca-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-synergi-tutorial/tutorial_synergi_samlbase.png)

3. <span data-ttu-id="25eca-153">Op de **Synergi domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="25eca-153">On the **Synergi Domain and URLs** section, perform the following steps:</span></span>

    ![URL's en Synergi domein eenmalige aanmelding informatie](./media/active-directory-saas-synergi-tutorial/tutorial_synergi_url.png)

    <span data-ttu-id="25eca-155">a.</span><span class="sxs-lookup"><span data-stu-id="25eca-155">a.</span></span> <span data-ttu-id="25eca-156">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<company name>.irmsecurity.com`</span><span class="sxs-lookup"><span data-stu-id="25eca-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.irmsecurity.com`</span></span>

    <span data-ttu-id="25eca-157">b.</span><span class="sxs-lookup"><span data-stu-id="25eca-157">b.</span></span> <span data-ttu-id="25eca-158">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://<company name>.irmsecurity.com/sso/<organization id>`</span><span class="sxs-lookup"><span data-stu-id="25eca-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.irmsecurity.com/sso/<organization id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="25eca-159">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="25eca-159">These values are not real.</span></span> <span data-ttu-id="25eca-160">Deze waarden bijwerken met de werkelijke id en de antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="25eca-160">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="25eca-161">Neem contact op met [Synergi ondersteuningsteam](https://www.irmsecurity.com/contact/) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="25eca-161">Contact [Synergi support team](https://www.irmsecurity.com/contact/) to get these values.</span></span>

4. <span data-ttu-id="25eca-162">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="25eca-162">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![De downloadkoppeling certificaat](./media/active-directory-saas-synergi-tutorial/tutorial_synergi_certificate.png) 

5. <span data-ttu-id="25eca-164">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="25eca-164">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-synergi-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="25eca-166">Op de **Synergi configuratie** sectie, klikt u op **configureren Synergi** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="25eca-166">On the **Synergi Configuration** section, click **Configure Synergi** to open **Configure sign-on** window.</span></span> <span data-ttu-id="25eca-167">Kopieer de **Sign-Out URL en SAML entiteit-ID** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="25eca-167">Copy the **Sign-Out URL and SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Synergi configuratie](./media/active-directory-saas-synergi-tutorial/tutorial_synergi_configure.png) 

7. <span data-ttu-id="25eca-169">Eenmalige aanmelding configureren op **Synergi** zijde, moet u de gedownloade verzenden **Certificate(Base64), Sign-Out-URL en de entiteit-ID SAML** naar [Synergi ondersteuningsteam](https://www.irmsecurity.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="25eca-169">To configure single sign-on on **Synergi** side, you need to send the downloaded **Certificate(Base64), Sign-Out URL, and SAML Entity ID** to [Synergi support team](https://www.irmsecurity.com/contact/).</span></span>

> [!TIP]
> <span data-ttu-id="25eca-170">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="25eca-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="25eca-171">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="25eca-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="25eca-172">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="25eca-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="25eca-173">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="25eca-173">Create an Azure AD test user</span></span>

<span data-ttu-id="25eca-174">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="25eca-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="25eca-176">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="25eca-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="25eca-177">Klik in de Azure-portal in het linkerdeelvenster op het **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="25eca-177">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![De Azure Active Directory-knop](./media/active-directory-saas-synergi-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="25eca-179">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="25eca-179">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !['Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-synergi-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="25eca-181">Openen van de **gebruiker** in het dialoogvenster klikt u op **toevoegen** boven aan de **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="25eca-181">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![De knop toevoegen](./media/active-directory-saas-synergi-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="25eca-183">In de **gebruiker** dialoogvenster vak, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="25eca-183">In the **User** dialog box, perform the following steps:</span></span>

    ![Het dialoogvenster gebruiker](./media/active-directory-saas-synergi-tutorial/create_aaduser_04.png)

    <span data-ttu-id="25eca-185">a.</span><span class="sxs-lookup"><span data-stu-id="25eca-185">a.</span></span> <span data-ttu-id="25eca-186">In de **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="25eca-186">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="25eca-187">b.</span><span class="sxs-lookup"><span data-stu-id="25eca-187">b.</span></span> <span data-ttu-id="25eca-188">In de **gebruikersnaam** typt u het e-mailadres van gebruiker Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="25eca-188">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="25eca-189">c.</span><span class="sxs-lookup"><span data-stu-id="25eca-189">c.</span></span> <span data-ttu-id="25eca-190">Selecteer de **wachtwoord weergeven** selectievakje, en noteer de waarde die wordt weergegeven in de **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="25eca-190">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="25eca-191">d.</span><span class="sxs-lookup"><span data-stu-id="25eca-191">d.</span></span> <span data-ttu-id="25eca-192">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="25eca-192">Click **Create**.</span></span>
  
### <a name="create-a-synergi-test-user"></a><span data-ttu-id="25eca-193">Een testgebruiker Synergi maken</span><span class="sxs-lookup"><span data-stu-id="25eca-193">Create a Synergi test user</span></span>

<span data-ttu-id="25eca-194">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in Synergi maken.</span><span class="sxs-lookup"><span data-stu-id="25eca-194">In this section, you create a user called Britta Simon in Synergi.</span></span> <span data-ttu-id="25eca-195">Werken met [Synergi ondersteuningsteam](https://www.irmsecurity.com/contact/) de gebruikers van het platform Synergi toevoegen.</span><span class="sxs-lookup"><span data-stu-id="25eca-195">Work with [Synergi support team](https://www.irmsecurity.com/contact/) to add the users in the Synergi platform.</span></span> <span data-ttu-id="25eca-196">Gebruikers moeten worden gemaakt en worden geactiveerd voordat u eenmalige aanmelding gebruiken.</span><span class="sxs-lookup"><span data-stu-id="25eca-196">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="25eca-197">De Azure AD-testgebruiker toewijzen</span><span class="sxs-lookup"><span data-stu-id="25eca-197">Assign the Azure AD test user</span></span>

<span data-ttu-id="25eca-198">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Synergi.</span><span class="sxs-lookup"><span data-stu-id="25eca-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Synergi.</span></span>

![Toewijzen van de gebruikersrol][200] 

<span data-ttu-id="25eca-200">**Britta Simon om aan te wijzen Synergi, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="25eca-200">**To assign Britta Simon to Synergi, perform the following steps:**</span></span>

1. <span data-ttu-id="25eca-201">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="25eca-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="25eca-203">Selecteer in de lijst met toepassingen **Synergi**.</span><span class="sxs-lookup"><span data-stu-id="25eca-203">In the applications list, select **Synergi**.</span></span>

    ![De koppeling Synergi in de lijst met toepassingen](./media/active-directory-saas-synergi-tutorial/tutorial_synergi_app.png)  

3. <span data-ttu-id="25eca-205">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="25eca-205">In the menu on the left, click **Users and groups**.</span></span>

    ![De koppeling 'Gebruikers en groepen'][202]

4. <span data-ttu-id="25eca-207">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="25eca-207">Click **Add** button.</span></span> <span data-ttu-id="25eca-208">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="25eca-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Het deelvenster toewijzing toevoegen][203]

5. <span data-ttu-id="25eca-210">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="25eca-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="25eca-211">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="25eca-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="25eca-212">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="25eca-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="25eca-213">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="25eca-213">Test single sign-on</span></span>

<span data-ttu-id="25eca-214">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="25eca-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="25eca-215">Als u op de tegel Synergi in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Synergi.</span><span class="sxs-lookup"><span data-stu-id="25eca-215">When you click the Synergi tile in the Access Panel, you should get automatically signed-on to your Synergi application.</span></span>
<span data-ttu-id="25eca-216">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="25eca-216">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="25eca-217">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="25eca-217">Additional resources</span></span>

* [<span data-ttu-id="25eca-218">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="25eca-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="25eca-219">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="25eca-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-synergi-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-synergi-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-synergi-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-synergi-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-synergi-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-synergi-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-synergi-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-synergi-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-synergi-tutorial/tutorial_general_203.png

