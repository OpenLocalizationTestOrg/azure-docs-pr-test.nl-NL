---
title: 'Zelfstudie: Azure Active Directory-integratie met Wikispaces | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Wikispaces.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 665b95aa-f7f5-4406-9e2a-6fc299a1599c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: d01543955bdf6a274571f67eafdff5f637863d5c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wikispaces"></a><span data-ttu-id="bccaf-103">Zelfstudie: Azure Active Directory-integratie met Wikispaces</span><span class="sxs-lookup"><span data-stu-id="bccaf-103">Tutorial: Azure Active Directory integration with Wikispaces</span></span>

<span data-ttu-id="bccaf-104">In deze zelfstudie leert u hoe Wikispaces integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bccaf-104">In this tutorial, you learn how to integrate Wikispaces with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bccaf-105">Wikispaces integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="bccaf-105">Integrating Wikispaces with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="bccaf-106">U kunt beheren in Azure AD die toegang tot Wikispaces heeft</span><span class="sxs-lookup"><span data-stu-id="bccaf-106">You can control in Azure AD who has access to Wikispaces</span></span>
- <span data-ttu-id="bccaf-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Wikispaces (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="bccaf-107">You can enable your users to automatically get signed-on to Wikispaces (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bccaf-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="bccaf-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="bccaf-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bccaf-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bccaf-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="bccaf-110">Prerequisites</span></span>

<span data-ttu-id="bccaf-111">Voor het configureren van Azure AD-integratie met Wikispaces, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="bccaf-111">To configure Azure AD integration with Wikispaces, you need the following items:</span></span>

- <span data-ttu-id="bccaf-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="bccaf-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bccaf-113">Een Wikispaces eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="bccaf-113">A Wikispaces single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bccaf-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="bccaf-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bccaf-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="bccaf-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bccaf-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="bccaf-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bccaf-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bccaf-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bccaf-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="bccaf-118">Scenario description</span></span>
<span data-ttu-id="bccaf-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="bccaf-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bccaf-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="bccaf-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bccaf-121">Wikispaces uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="bccaf-121">Adding Wikispaces from the gallery</span></span>
2. <span data-ttu-id="bccaf-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="bccaf-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-wikispaces-from-the-gallery"></a><span data-ttu-id="bccaf-123">Wikispaces uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="bccaf-123">Adding Wikispaces from the gallery</span></span>
<span data-ttu-id="bccaf-124">Voor het configureren van de integratie van Wikispaces in Azure AD, moet u Wikispaces uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="bccaf-124">To configure the integration of Wikispaces into Azure AD, you need to add Wikispaces from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="bccaf-125">**Als u wilt toevoegen Wikispaces uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="bccaf-125">**To add Wikispaces from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="bccaf-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="bccaf-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="bccaf-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="bccaf-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="bccaf-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="bccaf-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="bccaf-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="bccaf-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="bccaf-133">Typ in het zoekvak **Wikispaces**.</span><span class="sxs-lookup"><span data-stu-id="bccaf-133">In the search box, type **Wikispaces**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_search.png)

5. <span data-ttu-id="bccaf-135">Selecteer in het deelvenster resultaten **Wikispaces**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="bccaf-135">In the results panel, select **Wikispaces**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bccaf-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="bccaf-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bccaf-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Wikispaces op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="bccaf-138">In this section, you configure and test Azure AD single sign-on with Wikispaces based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="bccaf-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Wikispaces is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bccaf-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Wikispaces is to a user in Azure AD.</span></span> <span data-ttu-id="bccaf-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Wikispaces tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="bccaf-140">In other words, a link relationship between an Azure AD user and the related user in Wikispaces needs to be established.</span></span>

<span data-ttu-id="bccaf-141">Wijs in Wikispaces, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="bccaf-141">In Wikispaces, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="bccaf-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Wikispaces, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="bccaf-142">To configure and test Azure AD single sign-on with Wikispaces, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="bccaf-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="bccaf-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="bccaf-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bccaf-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bccaf-145">**[Maken van een testgebruiker Wikispaces](#creating-a-wikispaces-test-user)**  - Wikispaces die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="bccaf-145">**[Creating a Wikispaces test user](#creating-a-wikispaces-test-user)** - to have a counterpart of Britta Simon in Wikispaces that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="bccaf-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="bccaf-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bccaf-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="bccaf-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bccaf-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="bccaf-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bccaf-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Wikispaces configureren.</span><span class="sxs-lookup"><span data-stu-id="bccaf-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Wikispaces application.</span></span>

<span data-ttu-id="bccaf-150">**Voor het configureren van Azure AD eenmalige aanmelding met Wikispaces, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="bccaf-150">**To configure Azure AD single sign-on with Wikispaces, perform the following steps:**</span></span>

1. <span data-ttu-id="bccaf-151">In de Azure-portal op de **Wikispaces** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="bccaf-151">In the Azure portal, on the **Wikispaces** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="bccaf-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="bccaf-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_samlbase.png)

3. <span data-ttu-id="bccaf-155">Op de **Wikispaces domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="bccaf-155">On the **Wikispaces Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_url.png)

    <span data-ttu-id="bccaf-157">a.</span><span class="sxs-lookup"><span data-stu-id="bccaf-157">a.</span></span> <span data-ttu-id="bccaf-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<companyname>.wikispaces.net`</span><span class="sxs-lookup"><span data-stu-id="bccaf-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.wikispaces.net`</span></span>

    <span data-ttu-id="bccaf-159">b.</span><span class="sxs-lookup"><span data-stu-id="bccaf-159">b.</span></span> <span data-ttu-id="bccaf-160">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://session.wikispaces.net/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="bccaf-160">In the **Identifier** textbox, type a URL using the following pattern: `https://session.wikispaces.net/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="bccaf-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="bccaf-161">These values are not real.</span></span> <span data-ttu-id="bccaf-162">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="bccaf-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="bccaf-163">Neem contact op met [Wikispaces Client ondersteuningsteam](https://www.wikispaces.com/site/help) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="bccaf-163">Contact [Wikispaces Client support team](https://www.wikispaces.com/site/help) to get these values.</span></span> 

4. <span data-ttu-id="bccaf-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="bccaf-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_certificate.png) 

5. <span data-ttu-id="bccaf-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="bccaf-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-wikispaces-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="bccaf-168">Eenmalige aanmelding configureren op **Wikispaces** zijde, moet u de gedownloade verzenden **Metadata XML** naar [Wikispaces ondersteuningsteam](https://www.wikispaces.com/site/help).</span><span class="sxs-lookup"><span data-stu-id="bccaf-168">To configure single sign-on on **Wikispaces** side, you need to send the downloaded **Metadata XML** to [Wikispaces support team](https://www.wikispaces.com/site/help).</span></span> <span data-ttu-id="bccaf-169">U ontvangt een melding zodra de configuratie is voltooid.</span><span class="sxs-lookup"><span data-stu-id="bccaf-169">You will get a notification as soon as the configuration has been completed.</span></span>

> [!TIP]
> <span data-ttu-id="bccaf-170">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="bccaf-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="bccaf-171">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="bccaf-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="bccaf-172">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bccaf-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bccaf-173">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="bccaf-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="bccaf-174">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="bccaf-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="bccaf-176">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="bccaf-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="bccaf-177">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="bccaf-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-wikispaces-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bccaf-179">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="bccaf-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-wikispaces-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bccaf-181">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="bccaf-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-wikispaces-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bccaf-183">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="bccaf-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-wikispaces-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bccaf-185">a.</span><span class="sxs-lookup"><span data-stu-id="bccaf-185">a.</span></span> <span data-ttu-id="bccaf-186">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bccaf-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bccaf-187">b.</span><span class="sxs-lookup"><span data-stu-id="bccaf-187">b.</span></span> <span data-ttu-id="bccaf-188">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="bccaf-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bccaf-189">c.</span><span class="sxs-lookup"><span data-stu-id="bccaf-189">c.</span></span> <span data-ttu-id="bccaf-190">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="bccaf-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="bccaf-191">d.</span><span class="sxs-lookup"><span data-stu-id="bccaf-191">d.</span></span> <span data-ttu-id="bccaf-192">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="bccaf-192">Click **Create**.</span></span>
 
### <a name="creating-a-wikispaces-test-user"></a><span data-ttu-id="bccaf-193">Een testgebruiker Wikispaces maken</span><span class="sxs-lookup"><span data-stu-id="bccaf-193">Creating a Wikispaces test user</span></span>

<span data-ttu-id="bccaf-194">Om Azure AD-gebruikers zich aanmelden bij Wikispaces inschakelt, moeten ze worden ingericht in Wikispaces.</span><span class="sxs-lookup"><span data-stu-id="bccaf-194">In order to enable Azure AD users to log in to Wikispaces, they must be provisioned into Wikispaces.</span></span> <span data-ttu-id="bccaf-195">In het geval van Wikispaces is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="bccaf-195">In the case of Wikispaces, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-accounts-perform-the-following-steps"></a><span data-ttu-id="bccaf-196">Voor het inrichten van een gebruikersaccount, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="bccaf-196">To provision a user accounts, perform the following steps:</span></span>
1. <span data-ttu-id="bccaf-197">Meld u aan bij uw **Wikispaces** bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="bccaf-197">Log in to your **Wikispaces** company site as an administrator.</span></span>

2. <span data-ttu-id="bccaf-198">Ga naar **leden**.</span><span class="sxs-lookup"><span data-stu-id="bccaf-198">Go to **Members**.</span></span>
   
    <span data-ttu-id="bccaf-199">![Leden](./media/active-directory-saas-wikispaces-tutorial/ic787193.png "leden")</span><span class="sxs-lookup"><span data-stu-id="bccaf-199">![Members](./media/active-directory-saas-wikispaces-tutorial/ic787193.png "Members")</span></span>

3. <span data-ttu-id="bccaf-200">Klik op de **personen uitnodigen**.</span><span class="sxs-lookup"><span data-stu-id="bccaf-200">Click the **Invite People**.</span></span>
   
    <span data-ttu-id="bccaf-201">![Personen uitnodigen](./media/active-directory-saas-wikispaces-tutorial/ic787194.png "personen uitnodigen")</span><span class="sxs-lookup"><span data-stu-id="bccaf-201">![Invite People](./media/active-directory-saas-wikispaces-tutorial/ic787194.png "Invite People")</span></span>

4. <span data-ttu-id="bccaf-202">In de **personen uitnodigen** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="bccaf-202">In the **Invite People** section, perform the following steps:</span></span>
   
    <span data-ttu-id="bccaf-203">![Personen uitnodigen](./media/active-directory-saas-wikispaces-tutorial/ic787208.png "personen uitnodigen")</span><span class="sxs-lookup"><span data-stu-id="bccaf-203">![Invite People](./media/active-directory-saas-wikispaces-tutorial/ic787208.png "Invite People")</span></span>
   
    <span data-ttu-id="bccaf-204">a.</span><span class="sxs-lookup"><span data-stu-id="bccaf-204">a.</span></span> <span data-ttu-id="bccaf-205">Typ de **gebruikersnamen of e-mailadres** van een geldige AAD-account dat u inrichten in de bijbehorende tekstvakken wilt.</span><span class="sxs-lookup"><span data-stu-id="bccaf-205">Type the **Usernames or Email Address** of a valid AAD account you want to provision into the related textboxes.</span></span>
   
    <span data-ttu-id="bccaf-206">b.</span><span class="sxs-lookup"><span data-stu-id="bccaf-206">b.</span></span> <span data-ttu-id="bccaf-207">Klik op **verzenden**.</span><span class="sxs-lookup"><span data-stu-id="bccaf-207">Click **Send**.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="bccaf-208">De houder van Azure Active Directory-account ontvangt een e-mailbericht met inbegrip van een koppeling om te bevestigen van het account voordat deze geactiveerd wordt.</span><span class="sxs-lookup"><span data-stu-id="bccaf-208">The Azure Active Directory account holder receives an email including a link to confirm the account before it becomes active.</span></span>
    
> [!NOTE]
> <span data-ttu-id="bccaf-209">U kunt andere Wikispaces gebruiker account hulpmiddelen voor het maken of API's die is geleverd door Wikispaces aan inrichten AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="bccaf-209">You can use any other Wikispaces user account creation tools or APIs provided by Wikispaces to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="bccaf-210">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="bccaf-210">Assigning the Azure AD test user</span></span>

<span data-ttu-id="bccaf-211">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Wikispaces.</span><span class="sxs-lookup"><span data-stu-id="bccaf-211">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Wikispaces.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="bccaf-213">**Britta Simon om aan te wijzen Wikispaces, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="bccaf-213">**To assign Britta Simon to Wikispaces, perform the following steps:**</span></span>

1. <span data-ttu-id="bccaf-214">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="bccaf-214">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="bccaf-216">Selecteer in de lijst met toepassingen **Wikispaces**.</span><span class="sxs-lookup"><span data-stu-id="bccaf-216">In the applications list, select **Wikispaces**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_app.png) 

3. <span data-ttu-id="bccaf-218">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="bccaf-218">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="bccaf-220">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="bccaf-220">Click **Add** button.</span></span> <span data-ttu-id="bccaf-221">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="bccaf-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="bccaf-223">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="bccaf-223">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="bccaf-224">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="bccaf-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bccaf-225">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="bccaf-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bccaf-226">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="bccaf-226">Testing single sign-on</span></span>

<span data-ttu-id="bccaf-227">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="bccaf-227">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="bccaf-228">Als u op de tegel Wikispaces in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Wikispaces.</span><span class="sxs-lookup"><span data-stu-id="bccaf-228">When you click the Wikispaces tile in the Access Panel, you should get automatically signed-on to your Wikispaces application.</span></span>
<span data-ttu-id="bccaf-229">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bccaf-229">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bccaf-230">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="bccaf-230">Additional resources</span></span>

* [<span data-ttu-id="bccaf-231">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bccaf-231">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bccaf-232">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bccaf-232">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_203.png

