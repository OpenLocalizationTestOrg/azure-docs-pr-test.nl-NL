---
title: 'Zelfstudie: Azure Active Directory-integratie met QuickHelp | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en QuickHelp.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 655c9ad3-2076-4e2c-8e47-9ed3bf04be56
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: jeedes
ms.openlocfilehash: 1c72b0ddee636090129dab7a5c7ec6ffd452434a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-quickhelp"></a><span data-ttu-id="9a085-103">Zelfstudie: Azure Active Directory-integratie met QuickHelp</span><span class="sxs-lookup"><span data-stu-id="9a085-103">Tutorial: Azure Active Directory integration with QuickHelp</span></span>

<span data-ttu-id="9a085-104">In deze zelfstudie leert u hoe QuickHelp integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9a085-104">In this tutorial, you learn how to integrate QuickHelp with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9a085-105">QuickHelp integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="9a085-105">Integrating QuickHelp with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9a085-106">U kunt beheren in Azure AD die toegang tot QuickHelp heeft</span><span class="sxs-lookup"><span data-stu-id="9a085-106">You can control in Azure AD who has access to QuickHelp</span></span>
- <span data-ttu-id="9a085-107">U kunt uw gebruikers automatisch ophalen aangemeld bij QuickHelp (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="9a085-107">You can enable your users to automatically get signed-on to QuickHelp (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9a085-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="9a085-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9a085-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9a085-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9a085-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="9a085-110">Prerequisites</span></span>

<span data-ttu-id="9a085-111">Voor het configureren van Azure AD-integratie met QuickHelp, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="9a085-111">To configure Azure AD integration with QuickHelp, you need the following items:</span></span>

- <span data-ttu-id="9a085-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="9a085-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9a085-113">Een QuickHelp eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="9a085-113">A QuickHelp single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9a085-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="9a085-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9a085-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="9a085-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9a085-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="9a085-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9a085-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9a085-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9a085-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="9a085-118">Scenario description</span></span>
<span data-ttu-id="9a085-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="9a085-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9a085-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="9a085-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9a085-121">QuickHelp uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="9a085-121">Adding QuickHelp from the gallery</span></span>
2. <span data-ttu-id="9a085-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="9a085-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-quickhelp-from-the-gallery"></a><span data-ttu-id="9a085-123">QuickHelp uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="9a085-123">Adding QuickHelp from the gallery</span></span>
<span data-ttu-id="9a085-124">Voor het configureren van de integratie van QuickHelp in Azure AD, moet u QuickHelp uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="9a085-124">To configure the integration of QuickHelp into Azure AD, you need to add QuickHelp from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9a085-125">**Als u wilt toevoegen QuickHelp uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="9a085-125">**To add QuickHelp from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9a085-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="9a085-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9a085-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="9a085-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9a085-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="9a085-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="9a085-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9a085-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="9a085-133">Typ in het zoekvak **QuickHelp**.</span><span class="sxs-lookup"><span data-stu-id="9a085-133">In the search box, type **QuickHelp**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_search.png)

5. <span data-ttu-id="9a085-135">Selecteer in het deelvenster resultaten **QuickHelp**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="9a085-135">In the results panel, select **QuickHelp**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9a085-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="9a085-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9a085-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met QuickHelp op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="9a085-138">In this section, you configure and test Azure AD single sign-on with QuickHelp based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9a085-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in QuickHelp is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9a085-139">For single sign-on to work, Azure AD needs to know what the counterpart user in QuickHelp is to a user in Azure AD.</span></span> <span data-ttu-id="9a085-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in QuickHelp tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="9a085-140">In other words, a link relationship between an Azure AD user and the related user in QuickHelp needs to be established.</span></span>

<span data-ttu-id="9a085-141">Wijs in QuickHelp, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="9a085-141">In QuickHelp, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="9a085-142">Om te configureren en testen van Azure AD eenmalige aanmelding met QuickHelp, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="9a085-142">To configure and test Azure AD single sign-on with QuickHelp, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9a085-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="9a085-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9a085-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9a085-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9a085-145">**[Maken van een testgebruiker QuickHelp](#creating-a-quickhelp-test-user)**  - QuickHelp die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="9a085-145">**[Creating a QuickHelp test user](#creating-a-quickhelp-test-user)** - to have a counterpart of Britta Simon in QuickHelp that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9a085-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="9a085-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9a085-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="9a085-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9a085-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="9a085-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9a085-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing QuickHelp configureren.</span><span class="sxs-lookup"><span data-stu-id="9a085-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your QuickHelp application.</span></span>

<span data-ttu-id="9a085-150">**Voor het configureren van Azure AD eenmalige aanmelding met QuickHelp, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="9a085-150">**To configure Azure AD single sign-on with QuickHelp, perform the following steps:**</span></span>

1. <span data-ttu-id="9a085-151">In de Azure-portal op de **QuickHelp** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="9a085-151">In the Azure portal, on the **QuickHelp** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="9a085-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="9a085-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_samlbase.png)

3. <span data-ttu-id="9a085-155">Op de **QuickHelp domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="9a085-155">On the **QuickHelp Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_url.png)

    <span data-ttu-id="9a085-157">a.</span><span class="sxs-lookup"><span data-stu-id="9a085-157">a.</span></span> <span data-ttu-id="9a085-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://quickhelp.com/<instancename>/#/Login`</span><span class="sxs-lookup"><span data-stu-id="9a085-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://quickhelp.com/<instancename>/#/Login`</span></span>

    <span data-ttu-id="9a085-159">b.</span><span class="sxs-lookup"><span data-stu-id="9a085-159">b.</span></span> <span data-ttu-id="9a085-160">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<subdomain>.quickhelp.com`</span><span class="sxs-lookup"><span data-stu-id="9a085-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.quickhelp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9a085-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="9a085-161">These values are not real.</span></span> <span data-ttu-id="9a085-162">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="9a085-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="9a085-163">Neem contact op met [QuickHelp Client ondersteuningsteam](https://support.quickhelp.com/) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="9a085-163">Contact [QuickHelp Client support team](https://support.quickhelp.com/) to get these values.</span></span> 
 
4. <span data-ttu-id="9a085-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="9a085-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_certificate.png) 

5. <span data-ttu-id="9a085-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="9a085-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-quickhelp-tutorial/tutorial_general_400.png) 

6. <span data-ttu-id="9a085-168">Aanmelding bij uw bedrijf QuickHelp site als administrator.</span><span class="sxs-lookup"><span data-stu-id="9a085-168">Sign-on to your QuickHelp company site as administrator.</span></span>

7. <span data-ttu-id="9a085-169">Klik in het menu bovenaan op **Admin**.</span><span class="sxs-lookup"><span data-stu-id="9a085-169">In the menu on the top, click **Admin**.</span></span>
   
    ![Eenmalige aanmelding configureren][21]

8. <span data-ttu-id="9a085-171">In de **QuickHelp Admin** menu, klikt u op **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="9a085-171">In the **QuickHelp Admin** menu, click **Settings**.</span></span>
   
    ![Eenmalige aanmelding configureren][22]

9. <span data-ttu-id="9a085-173">Klik op **verificatie-instellingen**.</span><span class="sxs-lookup"><span data-stu-id="9a085-173">Click **Authentication Settings**.</span></span>

10. <span data-ttu-id="9a085-174">Op de **verificatie-instellingen** pagina, voert u de volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9a085-174">On the **Authentication Settings** page, perform the following steps</span></span>
   
    ![Eenmalige aanmelding configureren][23]
   
    <span data-ttu-id="9a085-176">a.</span><span class="sxs-lookup"><span data-stu-id="9a085-176">a.</span></span> <span data-ttu-id="9a085-177">Als **SSO Type**, selecteer **WSFederation**.</span><span class="sxs-lookup"><span data-stu-id="9a085-177">As **SSO Type**, select **WSFederation**.</span></span>
   
    <span data-ttu-id="9a085-178">b.</span><span class="sxs-lookup"><span data-stu-id="9a085-178">b.</span></span> <span data-ttu-id="9a085-179">Als u wilt uw gedownloade Azure metagegevensbestand uploadt, klikt u op **Bladeren**, Ga naar het bestand, klikt u vervolgens op eindigen **metagegevens uploaden**.</span><span class="sxs-lookup"><span data-stu-id="9a085-179">To upload your downloaded Azure metadata file, click **Browse**, navigate to the file, end then click **Upload Metadata**.</span></span>
   
    <span data-ttu-id="9a085-180">c.</span><span class="sxs-lookup"><span data-stu-id="9a085-180">c.</span></span> <span data-ttu-id="9a085-181">In de **e** textbox type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="9a085-181">In the **Email** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
   
    <span data-ttu-id="9a085-182">d.</span><span class="sxs-lookup"><span data-stu-id="9a085-182">d.</span></span> <span data-ttu-id="9a085-183">In de **voornaam** textbox `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span><span class="sxs-lookup"><span data-stu-id="9a085-183">In the **First Name** textbox, `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>
   
    <span data-ttu-id="9a085-184">e.</span><span class="sxs-lookup"><span data-stu-id="9a085-184">e.</span></span> <span data-ttu-id="9a085-185">In de **achternaam** textbox `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span><span class="sxs-lookup"><span data-stu-id="9a085-185">In the **Last Name** textbox, `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>
   
    <span data-ttu-id="9a085-186">f.</span><span class="sxs-lookup"><span data-stu-id="9a085-186">f.</span></span> <span data-ttu-id="9a085-187">In de **actiebalk**, klikt u op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="9a085-187">In the **Action Bar**, click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="9a085-188">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="9a085-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9a085-189">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="9a085-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9a085-190">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9a085-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9a085-191">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="9a085-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="9a085-192">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="9a085-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="9a085-194">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="9a085-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9a085-195">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="9a085-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9a085-197">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="9a085-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9a085-199">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9a085-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9a085-201">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="9a085-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9a085-203">a.</span><span class="sxs-lookup"><span data-stu-id="9a085-203">a.</span></span> <span data-ttu-id="9a085-204">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9a085-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9a085-205">b.</span><span class="sxs-lookup"><span data-stu-id="9a085-205">b.</span></span> <span data-ttu-id="9a085-206">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9a085-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9a085-207">c.</span><span class="sxs-lookup"><span data-stu-id="9a085-207">c.</span></span> <span data-ttu-id="9a085-208">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="9a085-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9a085-209">d.</span><span class="sxs-lookup"><span data-stu-id="9a085-209">d.</span></span> <span data-ttu-id="9a085-210">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="9a085-210">Click **Create**.</span></span>
 
### <a name="creating-a-quickhelp-test-user"></a><span data-ttu-id="9a085-211">Een testgebruiker QuickHelp maken</span><span class="sxs-lookup"><span data-stu-id="9a085-211">Creating a QuickHelp test user</span></span>

<span data-ttu-id="9a085-212">Het doel van deze sectie is het maken van een gebruiker Britta Simon in QuickHelp genoemd.</span><span class="sxs-lookup"><span data-stu-id="9a085-212">The objective of this section is to create a user called Britta Simon in QuickHelp.</span></span>
<span data-ttu-id="9a085-213">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker van het bijbehorende equivalent in QuickHelp aan een gebruiker in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="9a085-213">For single sign-on to work, Azure AD needs to know what the counterpart user in QuickHelp to a user in Azure AD is.</span></span> <span data-ttu-id="9a085-214">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in QuickHelp tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="9a085-214">In other words, a link relationship between an Azure AD user and the related user in QuickHelp needs to be established.</span></span>

<span data-ttu-id="9a085-215">QuickHelp ondersteuning biedt voor just-in-time-inrichting.</span><span class="sxs-lookup"><span data-stu-id="9a085-215">QuickHelp supports just-in-time provisioning.</span></span> <span data-ttu-id="9a085-216">Dit betekent, indien nodig, een gebruikersaccount wordt automatisch gemaakt in QuickHelp en het account is gekoppeld aan de Azure AD-account.</span><span class="sxs-lookup"><span data-stu-id="9a085-216">This means, if necessary, a user account is automatically created in QuickHelp and the account is linked to the Azure AD account.</span></span>

<span data-ttu-id="9a085-217">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="9a085-217">There is no action item for you in this section.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9a085-218">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="9a085-218">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9a085-219">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan QuickHelp.</span><span class="sxs-lookup"><span data-stu-id="9a085-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to QuickHelp.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="9a085-221">**Britta Simon om aan te wijzen QuickHelp, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="9a085-221">**To assign Britta Simon to QuickHelp, perform the following steps:**</span></span>

1. <span data-ttu-id="9a085-222">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="9a085-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="9a085-224">Selecteer in de lijst met toepassingen **QuickHelp**.</span><span class="sxs-lookup"><span data-stu-id="9a085-224">In the applications list, select **QuickHelp**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_app.png) 

3. <span data-ttu-id="9a085-226">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="9a085-226">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="9a085-228">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="9a085-228">Click **Add** button.</span></span> <span data-ttu-id="9a085-229">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9a085-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="9a085-231">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="9a085-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9a085-232">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9a085-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9a085-233">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9a085-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9a085-234">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="9a085-234">Testing single sign-on</span></span>

<span data-ttu-id="9a085-235">Het doel van deze sectie is het testen van uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="9a085-235">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  

<span data-ttu-id="9a085-236">Als u op de tegel QuickHelp in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing QuickHelp.</span><span class="sxs-lookup"><span data-stu-id="9a085-236">When you click the QuickHelp tile in the Access Panel, you should get automatically signed-on to your QuickHelp application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="9a085-237">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="9a085-237">Additional resources</span></span>

* [<span data-ttu-id="9a085-238">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9a085-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9a085-239">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9a085-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_203.png
[21]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_05.png
[22]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_06.png
[23]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_07.png
