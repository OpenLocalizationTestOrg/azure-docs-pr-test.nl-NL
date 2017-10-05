---
title: 'Zelfstudie: Azure Active Directory-integratie met handel | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en handel.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 78ec1766-4f79-4f16-9a66-d5584c4b6151
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: d3aba4aab8ded8749db2bf8197f57a6763008c60
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-greenhouse"></a><span data-ttu-id="ce406-103">Zelfstudie: Azure Active Directory-integratie met handel</span><span class="sxs-lookup"><span data-stu-id="ce406-103">Tutorial: Azure Active Directory integration with Greenhouse</span></span>

<span data-ttu-id="ce406-104">In deze zelfstudie leert u hoe handel integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ce406-104">In this tutorial, you learn how to integrate Greenhouse with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ce406-105">Handel integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="ce406-105">Integrating Greenhouse with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ce406-106">U kunt beheren in Azure AD die toegang tot de handel heeft.</span><span class="sxs-lookup"><span data-stu-id="ce406-106">You can control in Azure AD who has access to Greenhouse.</span></span>
- <span data-ttu-id="ce406-107">U kunt uw gebruikers automatisch ophalen aangemeld bij handel (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="ce406-107">You can enable your users to automatically get signed-on to Greenhouse (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="ce406-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="ce406-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="ce406-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ce406-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ce406-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ce406-110">Prerequisites</span></span>

<span data-ttu-id="ce406-111">Voor het configureren van Azure AD-integratie met handel, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="ce406-111">To configure Azure AD integration with Greenhouse, you need the following items:</span></span>

- <span data-ttu-id="ce406-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="ce406-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ce406-113">Een handel eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="ce406-113">A Greenhouse single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ce406-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="ce406-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ce406-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="ce406-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ce406-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="ce406-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ce406-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ce406-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ce406-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="ce406-118">Scenario description</span></span>
<span data-ttu-id="ce406-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="ce406-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ce406-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="ce406-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ce406-121">Handel uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="ce406-121">Adding Greenhouse from the gallery</span></span>
2. <span data-ttu-id="ce406-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ce406-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-greenhouse-from-the-gallery"></a><span data-ttu-id="ce406-123">Handel uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="ce406-123">Adding Greenhouse from the gallery</span></span>
<span data-ttu-id="ce406-124">Voor het configureren van de integratie van handel in Azure AD, moet u handel uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="ce406-124">To configure the integration of Greenhouse into Azure AD, you need to add Greenhouse from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ce406-125">**Als u wilt toevoegen handel uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="ce406-125">**To add Greenhouse from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ce406-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="ce406-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![De Azure Active Directory-knop][1]

2. <span data-ttu-id="ce406-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ce406-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ce406-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ce406-129">Then go to **All applications**.</span></span>

    ![De blade Enterprise-toepassingen][2]
    
3. <span data-ttu-id="ce406-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ce406-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![De knop Nieuw toepassing][3]

4. <span data-ttu-id="ce406-133">Typ in het zoekvak **handel**, selecteer **handel** van resultaat deelvenster klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="ce406-133">In the search box, type **Greenhouse**, select **Greenhouse** from result panel then click **Add** button to add the application.</span></span>

    ![Handel in de lijst met resultaten](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="ce406-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="ce406-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="ce406-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met handel op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="ce406-136">In this section, you configure and test Azure AD single sign-on with Greenhouse based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ce406-137">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in de handel in Azure AD voor een gebruiker is.</span><span class="sxs-lookup"><span data-stu-id="ce406-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Greenhouse is to a user in Azure AD.</span></span> <span data-ttu-id="ce406-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in de handel tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="ce406-138">In other words, a link relationship between an Azure AD user and the related user in Greenhouse needs to be established.</span></span>

<span data-ttu-id="ce406-139">In de handel, wijs de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="ce406-139">In Greenhouse, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ce406-140">Om te configureren en testen van Azure AD eenmalige aanmelding met handel, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="ce406-140">To configure and test Azure AD single sign-on with Greenhouse, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ce406-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ce406-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ce406-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ce406-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ce406-143">**[Maak een testgebruiker handel](#create-a-greenhouse-test-user)**  - handel die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="ce406-143">**[Create a Greenhouse test user](#create-a-greenhouse-test-user)** - to have a counterpart of Britta Simon in Greenhouse that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ce406-144">**[Toewijzen van de Azure AD-testgebruiker](#assign-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="ce406-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ce406-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="ce406-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="ce406-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="ce406-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="ce406-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing handel configureren.</span><span class="sxs-lookup"><span data-stu-id="ce406-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Greenhouse application.</span></span>

<span data-ttu-id="ce406-148">**Voor het configureren van Azure AD eenmalige aanmelding met handel, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="ce406-148">**To configure Azure AD single sign-on with Greenhouse, perform the following steps:**</span></span>

1. <span data-ttu-id="ce406-149">In de Azure-portal op de **handel** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="ce406-149">In the Azure portal, on the **Greenhouse** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="ce406-151">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="ce406-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_samlbase.png)

3. <span data-ttu-id="ce406-153">Op de **handel domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="ce406-153">On the **Greenhouse Domain and URLs** section, perform the following steps:</span></span>

    ![Handel domein en de URL's van eenmalige aanmelding informatie](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_url.png)

    <span data-ttu-id="ce406-155">a.</span><span class="sxs-lookup"><span data-stu-id="ce406-155">a.</span></span> <span data-ttu-id="ce406-156">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<companyname>.greenhouse.io`</span><span class="sxs-lookup"><span data-stu-id="ce406-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.greenhouse.io`</span></span>

    <span data-ttu-id="ce406-157">b.</span><span class="sxs-lookup"><span data-stu-id="ce406-157">b.</span></span> <span data-ttu-id="ce406-158">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<companyname>.greenhouse.io`</span><span class="sxs-lookup"><span data-stu-id="ce406-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.greenhouse.io`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ce406-159">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="ce406-159">These values are not real.</span></span> <span data-ttu-id="ce406-160">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="ce406-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="ce406-161">Neem contact op met [handel Client ondersteuningsteam](https://www.greenhouse.io/contact) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="ce406-161">Contact [Greenhouse Client support team](https://www.greenhouse.io/contact) to get these values.</span></span> 
 


4. <span data-ttu-id="ce406-162">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="ce406-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![De downloadkoppeling certificaat](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_certificate.png) 

5. <span data-ttu-id="ce406-164">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="ce406-164">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-greenhouse-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ce406-166">Eenmalige aanmelding configureren op **handel** zijde, moet u de gedownloade verzenden **Metadata XML** naar [handel ondersteuningsteam](http://www.greenhouse.io/contact).</span><span class="sxs-lookup"><span data-stu-id="ce406-166">To configure single sign-on on **Greenhouse** side, you need to send the downloaded **Metadata XML** to [Greenhouse support team](http://www.greenhouse.io/contact).</span></span>

> [!TIP]
> <span data-ttu-id="ce406-167">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="ce406-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ce406-168">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="ce406-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ce406-169">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ce406-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="ce406-170">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="ce406-170">Create an Azure AD test user</span></span>

<span data-ttu-id="ce406-171">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="ce406-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="ce406-173">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="ce406-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ce406-174">Klik in de Azure-portal in het linkerdeelvenster op het **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="ce406-174">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![De Azure Active Directory-knop](./media/active-directory-saas-greenhouse-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="ce406-176">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="ce406-176">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !['Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-greenhouse-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="ce406-178">Openen van de **gebruiker** in het dialoogvenster klikt u op **toevoegen** boven aan de **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ce406-178">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![De knop toevoegen](./media/active-directory-saas-greenhouse-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="ce406-180">In de **gebruiker** dialoogvenster vak, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="ce406-180">In the **User** dialog box, perform the following steps:</span></span>

    ![Het dialoogvenster gebruiker](./media/active-directory-saas-greenhouse-tutorial/create_aaduser_04.png)

    <span data-ttu-id="ce406-182">a.</span><span class="sxs-lookup"><span data-stu-id="ce406-182">a.</span></span> <span data-ttu-id="ce406-183">In de **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ce406-183">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ce406-184">b.</span><span class="sxs-lookup"><span data-stu-id="ce406-184">b.</span></span> <span data-ttu-id="ce406-185">In de **gebruikersnaam** typt u het e-mailadres van gebruiker Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ce406-185">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="ce406-186">c.</span><span class="sxs-lookup"><span data-stu-id="ce406-186">c.</span></span> <span data-ttu-id="ce406-187">Selecteer de **wachtwoord weergeven** selectievakje, en noteer de waarde die wordt weergegeven in de **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="ce406-187">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="ce406-188">d.</span><span class="sxs-lookup"><span data-stu-id="ce406-188">d.</span></span> <span data-ttu-id="ce406-189">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="ce406-189">Click **Create**.</span></span>
 
### <a name="create-a-greenhouse-test-user"></a><span data-ttu-id="ce406-190">Een testgebruiker handel maken</span><span class="sxs-lookup"><span data-stu-id="ce406-190">Create a Greenhouse test user</span></span>

<span data-ttu-id="ce406-191">Zodat gebruikers van Azure AD aan te melden bij handel moeten ze worden ingericht in de handel.</span><span class="sxs-lookup"><span data-stu-id="ce406-191">In order to enable Azure AD users to log into Greenhouse, they must be provisioned into Greenhouse.</span></span> <span data-ttu-id="ce406-192">In het geval van handel is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="ce406-192">In the case of Greenhouse, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="ce406-193">U kunt andere handel gebruiker account hulpmiddelen voor het maken of API's die is geleverd door handel aan inrichten AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="ce406-193">You can use any other Greenhouse user account creation tools or APIs provided by Greenhouse to provision AAD user accounts.</span></span> 

<span data-ttu-id="ce406-194">**Voor het inrichten van een gebruikersaccount, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="ce406-194">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="ce406-195">Meld u aan bij uw **handel** bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="ce406-195">Log in to your **Greenhouse** company site as an administrator.</span></span>

2. <span data-ttu-id="ce406-196">Klik in het menu bovenaan op **configureren**, en klik vervolgens op **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="ce406-196">In the menu on the top, click **Configure**, and then click **Users**.</span></span>
   
   <span data-ttu-id="ce406-197">![Gebruikers](./media/active-directory-saas-greenhouse-tutorial/ic790791.png "gebruikers")</span><span class="sxs-lookup"><span data-stu-id="ce406-197">![Users](./media/active-directory-saas-greenhouse-tutorial/ic790791.png "Users")</span></span>

3. <span data-ttu-id="ce406-198">Klik op **nieuwe gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="ce406-198">Click **New Users**.</span></span>
   
   <span data-ttu-id="ce406-199">![Nieuwe gebruiker](./media/active-directory-saas-greenhouse-tutorial/ic790792.png "nieuwe gebruiker")</span><span class="sxs-lookup"><span data-stu-id="ce406-199">![New User](./media/active-directory-saas-greenhouse-tutorial/ic790792.png "New User")</span></span>

4. <span data-ttu-id="ce406-200">In de **nieuwe gebruiker toevoegen** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="ce406-200">In the **Add New User** section, perform the following steps:</span></span>
   
   <span data-ttu-id="ce406-201">![Nieuwe gebruiker toevoegen](./media/active-directory-saas-greenhouse-tutorial/ic790793.png "nieuwe gebruiker toevoegen")</span><span class="sxs-lookup"><span data-stu-id="ce406-201">![Add New User](./media/active-directory-saas-greenhouse-tutorial/ic790793.png "Add New User")</span></span>

   <span data-ttu-id="ce406-202">a.</span><span class="sxs-lookup"><span data-stu-id="ce406-202">a.</span></span> <span data-ttu-id="ce406-203">In de **e-mails van de gebruiker invoeren** textbox, typ de e-mailadres van een geldige Azure Active Directory-account dat u inrichten wilt.</span><span class="sxs-lookup"><span data-stu-id="ce406-203">In the **Enter user emails** textbox, type the email address of a valid Azure Active Directory account you want to provision.</span></span>

   <span data-ttu-id="ce406-204">b.</span><span class="sxs-lookup"><span data-stu-id="ce406-204">b.</span></span> <span data-ttu-id="ce406-205">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="ce406-205">Click **Save**.</span></span>    
   
      >[!NOTE]
      ><span data-ttu-id="ce406-206">De houders van Azure Active Directory-account ontvangt een e-mailbericht met inbegrip van een koppeling om te bevestigen van het account voordat deze geactiveerd wordt.</span><span class="sxs-lookup"><span data-stu-id="ce406-206">The Azure Active Directory account holders will receive an email including a link to confirm the account before it becomes active.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="ce406-207">De Azure AD-testgebruiker toewijzen</span><span class="sxs-lookup"><span data-stu-id="ce406-207">Assign the Azure AD test user</span></span>

<span data-ttu-id="ce406-208">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan handel.</span><span class="sxs-lookup"><span data-stu-id="ce406-208">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Greenhouse.</span></span>

![Toewijzen van de gebruikersrol][200] 

<span data-ttu-id="ce406-210">**Britta Simon om aan te wijzen handel, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="ce406-210">**To assign Britta Simon to Greenhouse, perform the following steps:**</span></span>

1. <span data-ttu-id="ce406-211">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ce406-211">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="ce406-213">Selecteer in de lijst met toepassingen **handel**.</span><span class="sxs-lookup"><span data-stu-id="ce406-213">In the applications list, select **Greenhouse**.</span></span>

    ![De koppeling handel in de lijst met toepassingen](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_app.png)  

3. <span data-ttu-id="ce406-215">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="ce406-215">In the menu on the left, click **Users and groups**.</span></span>

    ![De koppeling 'Gebruikers en groepen'][202]

4. <span data-ttu-id="ce406-217">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="ce406-217">Click **Add** button.</span></span> <span data-ttu-id="ce406-218">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ce406-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Het deelvenster toewijzing toevoegen][203]

5. <span data-ttu-id="ce406-220">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="ce406-220">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ce406-221">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ce406-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ce406-222">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ce406-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="ce406-223">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ce406-223">Test single sign-on</span></span>

<span data-ttu-id="ce406-224">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="ce406-224">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ce406-225">Als u op de tegel handel in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing handel.</span><span class="sxs-lookup"><span data-stu-id="ce406-225">When you click the Greenhouse tile in the Access Panel, you should get automatically signed-on to your Greenhouse application.</span></span>
<span data-ttu-id="ce406-226">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ce406-226">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ce406-227">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="ce406-227">Additional resources</span></span>

* [<span data-ttu-id="ce406-228">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ce406-228">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ce406-229">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ce406-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_203.png

