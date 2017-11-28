---
title: 'Zelfstudie: Azure Active Directory-integratie met Skillport | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Skillport.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4df349b2-a73f-4b88-a077-ec0fbfc26527
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: jeedes
ms.openlocfilehash: 668fc5ae4f964bd776904c3a9dbc2b203689d50c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-skillport"></a><span data-ttu-id="06ea8-103">Zelfstudie: Azure Active Directory-integratie met Skillport</span><span class="sxs-lookup"><span data-stu-id="06ea8-103">Tutorial: Azure Active Directory integration with Skillport</span></span>

<span data-ttu-id="06ea8-104">In deze zelfstudie leert u hoe Skillport integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="06ea8-104">In this tutorial, you learn how to integrate Skillport with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="06ea8-105">Skillport integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="06ea8-105">Integrating Skillport with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="06ea8-106">U kunt beheren in Azure AD die toegang tot Skillport heeft</span><span class="sxs-lookup"><span data-stu-id="06ea8-106">You can control in Azure AD who has access to Skillport</span></span>
- <span data-ttu-id="06ea8-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Skillport (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="06ea8-107">You can enable your users to automatically get signed-on to Skillport (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="06ea8-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="06ea8-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="06ea8-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="06ea8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="06ea8-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="06ea8-110">Prerequisites</span></span>

<span data-ttu-id="06ea8-111">Voor het configureren van Azure AD-integratie met Skillport, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="06ea8-111">To configure Azure AD integration with Skillport, you need the following items:</span></span>

- <span data-ttu-id="06ea8-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="06ea8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="06ea8-113">Een Skillport eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="06ea8-113">A Skillport single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="06ea8-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="06ea8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="06ea8-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="06ea8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="06ea8-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="06ea8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="06ea8-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="06ea8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="06ea8-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="06ea8-118">Scenario description</span></span>
<span data-ttu-id="06ea8-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="06ea8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="06ea8-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="06ea8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="06ea8-121">Skillport uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="06ea8-121">Adding Skillport from the gallery</span></span>
2. <span data-ttu-id="06ea8-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="06ea8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-skillport-from-the-gallery"></a><span data-ttu-id="06ea8-123">Skillport uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="06ea8-123">Adding Skillport from the gallery</span></span>
<span data-ttu-id="06ea8-124">Voor het configureren van de integratie van Skillport in Azure AD, moet u Skillport uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="06ea8-124">To configure the integration of Skillport into Azure AD, you need to add Skillport from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="06ea8-125">**Als u wilt toevoegen Skillport uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="06ea8-125">**To add Skillport from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="06ea8-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="06ea8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="06ea8-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="06ea8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="06ea8-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="06ea8-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="06ea8-131">Klik op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="06ea8-131">Click **New Application** button on the top of the dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="06ea8-133">Typ in het zoekvak **Skillport**.</span><span class="sxs-lookup"><span data-stu-id="06ea8-133">In the search box, type **Skillport**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_search.png)

5. <span data-ttu-id="06ea8-135">Selecteer in het deelvenster resultaten **Skillport**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="06ea8-135">In the results panel, select **Skillport**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="06ea8-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="06ea8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="06ea8-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Skillport op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="06ea8-138">In this section, you configure and test Azure AD single sign-on with Skillport based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="06ea8-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Skillport is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="06ea8-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Skillport is to a user in Azure AD.</span></span> <span data-ttu-id="06ea8-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Skillport tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="06ea8-140">In other words, a link relationship between an Azure AD user and the related user in Skillport needs to be established.</span></span>

<span data-ttu-id="06ea8-141">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in Skillport.</span><span class="sxs-lookup"><span data-stu-id="06ea8-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Skillport.</span></span>

<span data-ttu-id="06ea8-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Skillport, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="06ea8-142">To configure and test Azure AD single sign-on with Skillport, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="06ea8-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="06ea8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="06ea8-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="06ea8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="06ea8-145">**[Maken van een testgebruiker Skillport](#creating-a-skillport-test-user)**  - Skillport die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="06ea8-145">**[Creating a Skillport test user](#creating-a-skillport-test-user)** - to have a counterpart of Britta Simon in Skillport that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="06ea8-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="06ea8-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="06ea8-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="06ea8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="06ea8-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="06ea8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="06ea8-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Skillport configureren.</span><span class="sxs-lookup"><span data-stu-id="06ea8-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Skillport application.</span></span>

<span data-ttu-id="06ea8-150">**Voor het configureren van Azure AD eenmalige aanmelding met Skillport, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="06ea8-150">**To configure Azure AD single sign-on with Skillport, perform the following steps:**</span></span>

1. <span data-ttu-id="06ea8-151">In de Azure-portal op de **Skillport** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="06ea8-151">In the Azure  portal, on the **Skillport** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="06ea8-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="06ea8-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_samlbase.png)

3. <span data-ttu-id="06ea8-155">Op de **Skillport domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="06ea8-155">On the **Skillport Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_url.png)

    <span data-ttu-id="06ea8-157">a.</span><span class="sxs-lookup"><span data-stu-id="06ea8-157">a.</span></span> <span data-ttu-id="06ea8-158">In de **aanmeldings-URL** textbox, typ een URL met de volgende patronen:</span><span class="sxs-lookup"><span data-stu-id="06ea8-158">In the **Sign-on URL** textbox, type a URL using the following patterns:</span></span>
      
      <span data-ttu-id="06ea8-159">EU Datacenter:`https://<subdomain>.skillport.eu`</span><span class="sxs-lookup"><span data-stu-id="06ea8-159">EU Datacenter: `https://<subdomain>.skillport.eu`</span></span>
   
      <span data-ttu-id="06ea8-160">VS Datacenter:`https://<subdomain>.skillport.com`</span><span class="sxs-lookup"><span data-stu-id="06ea8-160">US Datacenter: `https://<subdomain>.skillport.com`</span></span>
   
    <span data-ttu-id="06ea8-161">b.</span><span class="sxs-lookup"><span data-stu-id="06ea8-161">b.</span></span> <span data-ttu-id="06ea8-162">In de **antwoord-URL** textbox, typ een URL met de volgende patronen:</span><span class="sxs-lookup"><span data-stu-id="06ea8-162">In the **Reply URL** textbox, type a URL using the following patterns:</span></span>
    
      <span data-ttu-id="06ea8-163">EU Datacenter:`https://<subdomain>.skillport.eu/adfs/ls/`</span><span class="sxs-lookup"><span data-stu-id="06ea8-163">EU Datacenter: `https://<subdomain>.skillport.eu/adfs/ls/`</span></span>
    
      <span data-ttu-id="06ea8-164">VS Datacenter:`https://<subdomain>.skillport.com/sp/ACS.saml2`</span><span class="sxs-lookup"><span data-stu-id="06ea8-164">US Datacenter: `https://<subdomain>.skillport.com/sp/ACS.saml2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="06ea8-165">Deze waarden zijn niet de werkelijke.</span><span class="sxs-lookup"><span data-stu-id="06ea8-165">These values are not the real.</span></span> <span data-ttu-id="06ea8-166">Deze waarden bijwerken met de werkelijke antwoord-URL en de aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="06ea8-166">Update these values with the actual Reply URL and Sign-On URL.</span></span> <span data-ttu-id="06ea8-167">Neem contact op met [Skillport Client ondersteuningsteam](https://www.skillsoft.com/contact.asp) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="06ea8-167">Contact [Skillport Client support team](https://www.skillsoft.com/contact.asp) to get these values.</span></span>
 
4. <span data-ttu-id="06ea8-168">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het XML-bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="06ea8-168">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_certificate.png) 

5. <span data-ttu-id="06ea8-170">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="06ea8-170">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-skillport-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="06ea8-172">Eenmalige aanmelding configureren op **Skillport** zijde, moet u de gedownloade verzenden **Metadata XML** naar [Skillport ondersteuningsteam](https://www.skillsoft.com/contact.asp).</span><span class="sxs-lookup"><span data-stu-id="06ea8-172">To configure single sign-on on **Skillport** side, you need to send the downloaded **Metadata XML** to [Skillport support team](https://www.skillsoft.com/contact.asp).</span></span> <span data-ttu-id="06ea8-173">Ze stelt het de SAML SSO-verbinding juist is ingesteld op beide zijden.</span><span class="sxs-lookup"><span data-stu-id="06ea8-173">They will set it up to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="06ea8-174">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="06ea8-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="06ea8-175">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="06ea8-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="06ea8-177">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="06ea8-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="06ea8-178">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="06ea8-178">In the **Azure  portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-skillport-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="06ea8-180">Ga naar **gebruikers en groepen** en klik op **alle gebruikers** om de lijst met gebruikers weer te geven.</span><span class="sxs-lookup"><span data-stu-id="06ea8-180">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-skillport-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="06ea8-182">Aan de bovenkant van het dialoogvenster, klikt u op **toevoegen** openen de **gebruiker** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="06ea8-182">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-skillport-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="06ea8-184">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="06ea8-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-skillport-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="06ea8-186">a.</span><span class="sxs-lookup"><span data-stu-id="06ea8-186">a.</span></span> <span data-ttu-id="06ea8-187">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="06ea8-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="06ea8-188">b.</span><span class="sxs-lookup"><span data-stu-id="06ea8-188">b.</span></span> <span data-ttu-id="06ea8-189">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="06ea8-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="06ea8-190">c.</span><span class="sxs-lookup"><span data-stu-id="06ea8-190">c.</span></span> <span data-ttu-id="06ea8-191">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="06ea8-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="06ea8-192">d.</span><span class="sxs-lookup"><span data-stu-id="06ea8-192">d.</span></span> <span data-ttu-id="06ea8-193">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="06ea8-193">Click **Create**.</span></span>
 
### <a name="creating-a-skillport-test-user"></a><span data-ttu-id="06ea8-194">Een testgebruiker Skillport maken</span><span class="sxs-lookup"><span data-stu-id="06ea8-194">Creating a Skillport test user</span></span>

<span data-ttu-id="06ea8-195">Om te kunnen Skillport testgebruiker maken, moet u contact opnemen met [Skillport ondersteuningsteam](https://www.skillsoft.com/contact.asp) als ze meerdere bedrijfsscenario's volgens de vereisten van de eindgebruiker hebben.</span><span class="sxs-lookup"><span data-stu-id="06ea8-195">In order to create Skillport test user, you need to contact [Skillport support team](https://www.skillsoft.com/contact.asp) as they have multiple business scenarios according to the requirement of end user.</span></span> <span data-ttu-id="06ea8-196">Ze zullen deze na overleg met de gebruikers configureren.</span><span class="sxs-lookup"><span data-stu-id="06ea8-196">They will configure it after discussion with the users.</span></span>  

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="06ea8-197">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="06ea8-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="06ea8-198">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Skillport.</span><span class="sxs-lookup"><span data-stu-id="06ea8-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Skillport.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="06ea8-200">**Britta Simon om aan te wijzen Skillport, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="06ea8-200">**To assign Britta Simon to Skillport, perform the following steps:**</span></span>

1. <span data-ttu-id="06ea8-201">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="06ea8-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="06ea8-203">Selecteer in de lijst met toepassingen **Skillport**.</span><span class="sxs-lookup"><span data-stu-id="06ea8-203">In the applications list, select **Skillport**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_app.png) 

3. <span data-ttu-id="06ea8-205">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="06ea8-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="06ea8-207">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="06ea8-207">Click **Add** button.</span></span> <span data-ttu-id="06ea8-208">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="06ea8-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="06ea8-210">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="06ea8-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="06ea8-211">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="06ea8-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="06ea8-212">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="06ea8-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="06ea8-213">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="06ea8-213">Testing single sign-on</span></span>

<span data-ttu-id="06ea8-214">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="06ea8-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="06ea8-215">Als u op de tegel Skillport in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Skillport.</span><span class="sxs-lookup"><span data-stu-id="06ea8-215">When you click the Skillport tile in the Access Panel, you should get automatically signed-on to your Skillport application.</span></span>
<span data-ttu-id="06ea8-216">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="06ea8-216">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="06ea8-217">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="06ea8-217">Additional resources</span></span>

* [<span data-ttu-id="06ea8-218">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="06ea8-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="06ea8-219">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="06ea8-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_203.png

