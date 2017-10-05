---
title: 'Zelfstudie: Azure Active Directory-integratie met mensen | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en personen.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7c9b6202-11dd-4bb6-a679-8fb0a7a0ef4e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: caa287a2ed8774965ef722685e4e950336e5e0ea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-people"></a><span data-ttu-id="f1de5-103">Zelfstudie: Azure Active Directory-integratie met mensen</span><span class="sxs-lookup"><span data-stu-id="f1de5-103">Tutorial: Azure Active Directory integration with People</span></span>

<span data-ttu-id="f1de5-104">In deze zelfstudie leert u hoe mensen integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f1de5-104">In this tutorial, you learn how to integrate People with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f1de5-105">Mensen integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="f1de5-105">Integrating People with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f1de5-106">U kunt beheren in Azure AD die toegang tot personen heeft</span><span class="sxs-lookup"><span data-stu-id="f1de5-106">You can control in Azure AD who has access to People</span></span>
- <span data-ttu-id="f1de5-107">U kunt uw gebruikers automatisch ophalen aangemelde naar mensen (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="f1de5-107">You can enable your users to automatically get signed-on to People (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f1de5-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="f1de5-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f1de5-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f1de5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f1de5-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f1de5-110">Prerequisites</span></span>

<span data-ttu-id="f1de5-111">Voor het configureren van Azure AD-integratie met mensen, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="f1de5-111">To configure Azure AD integration with People, you need the following items:</span></span>

- <span data-ttu-id="f1de5-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="f1de5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f1de5-113">Een mensen eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="f1de5-113">A People single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f1de5-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="f1de5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f1de5-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="f1de5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f1de5-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="f1de5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f1de5-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f1de5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f1de5-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="f1de5-118">Scenario description</span></span>
<span data-ttu-id="f1de5-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="f1de5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f1de5-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="f1de5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f1de5-121">Toevoegen van personen uit de galerie</span><span class="sxs-lookup"><span data-stu-id="f1de5-121">Adding People from the gallery</span></span>
2. <span data-ttu-id="f1de5-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f1de5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-people-from-the-gallery"></a><span data-ttu-id="f1de5-123">Toevoegen van personen uit de galerie</span><span class="sxs-lookup"><span data-stu-id="f1de5-123">Adding People from the gallery</span></span>
<span data-ttu-id="f1de5-124">Voor het configureren van de integratie van mensen in Azure AD, moet u mensen uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="f1de5-124">To configure the integration of People into Azure AD, you need to add People from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f1de5-125">**Als u wilt mensen uit de galerie toevoegen, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="f1de5-125">**To add People from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f1de5-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="f1de5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f1de5-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f1de5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f1de5-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f1de5-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="f1de5-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f1de5-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="f1de5-133">Typ in het zoekvak **mensen**.</span><span class="sxs-lookup"><span data-stu-id="f1de5-133">In the search box, type **People**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-people-tutorial/tutorial_people_search.png)

5. <span data-ttu-id="f1de5-135">Selecteer in het deelvenster resultaten **mensen**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="f1de5-135">In the results panel, select **People**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-people-tutorial/tutorial_people_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f1de5-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f1de5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f1de5-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met personen op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="f1de5-138">In this section, you configure and test Azure AD single sign-on with People based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f1de5-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in mensen in Azure AD voor een gebruiker is.</span><span class="sxs-lookup"><span data-stu-id="f1de5-139">For single sign-on to work, Azure AD needs to know what the counterpart user in People is to a user in Azure AD.</span></span> <span data-ttu-id="f1de5-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in mensen tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="f1de5-140">In other words, a link relationship between an Azure AD user and the related user in People needs to be established.</span></span>

<span data-ttu-id="f1de5-141">Wijs in personen, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="f1de5-141">In People, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f1de5-142">Om te configureren en testen van Azure AD eenmalige aanmelding met mensen, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="f1de5-142">To configure and test Azure AD single sign-on with People, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f1de5-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f1de5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f1de5-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f1de5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f1de5-145">**[Maken van een testgebruiker mensen](#creating-a-people-test-user)**  - mensen die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="f1de5-145">**[Creating a People test user](#creating-a-people-test-user)** - to have a counterpart of Britta Simon in People that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f1de5-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="f1de5-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f1de5-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="f1de5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f1de5-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="f1de5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f1de5-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw toepassing personen.</span><span class="sxs-lookup"><span data-stu-id="f1de5-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your People application.</span></span>

<span data-ttu-id="f1de5-150">**Voor het configureren van Azure AD eenmalige aanmelding met mensen, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="f1de5-150">**To configure Azure AD single sign-on with People, perform the following steps:**</span></span>

1. <span data-ttu-id="f1de5-151">In de Azure-portal op de **mensen** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="f1de5-151">In the Azure portal, on the **People** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="f1de5-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="f1de5-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-people-tutorial/tutorial_people_samlbase.png)

3. <span data-ttu-id="f1de5-155">Op de **mensen domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="f1de5-155">On the **People Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-people-tutorial/tutorial_people_url.png)

    <span data-ttu-id="f1de5-157">a.</span><span class="sxs-lookup"><span data-stu-id="f1de5-157">a.</span></span> <span data-ttu-id="f1de5-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<company name>.peoplehr.com/`</span><span class="sxs-lookup"><span data-stu-id="f1de5-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.peoplehr.com/`</span></span>

    <span data-ttu-id="f1de5-159">b.</span><span class="sxs-lookup"><span data-stu-id="f1de5-159">b.</span></span> <span data-ttu-id="f1de5-160">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://www.peoplehr.com`</span><span class="sxs-lookup"><span data-stu-id="f1de5-160">In the **Identifier** textbox, type a URL using the following pattern: `https://www.peoplehr.com`</span></span>

    <span data-ttu-id="f1de5-161">c.</span><span class="sxs-lookup"><span data-stu-id="f1de5-161">c.</span></span> <span data-ttu-id="f1de5-162">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://<company name>.peoplehr.net/Pages/Saml/ConsumeAzureAD.aspx`</span><span class="sxs-lookup"><span data-stu-id="f1de5-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.peoplehr.net/Pages/Saml/ConsumeAzureAD.aspx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f1de5-163">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="f1de5-163">These values are not real.</span></span> <span data-ttu-id="f1de5-164">Deze waarden bijwerken met de werkelijke id, antwoord-URL en aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="f1de5-164">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="f1de5-165">Neem contact op met [mensen Client ondersteuningsteam](mailto:customerservices@peoplehr.com) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="f1de5-165">Contact [People Client support team](mailto:customerservices@peoplehr.com) to get these values.</span></span>

5. <span data-ttu-id="f1de5-166">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="f1de5-166">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-people-tutorial/tutorial_people_certificate.png) 

6. <span data-ttu-id="f1de5-168">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="f1de5-168">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-people-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="f1de5-170">Als u eenmalige aanmelding voor uw toepassing is geconfigureerd, moet u eenmalige aanmelding voor uw tenant mensen als beheerder.</span><span class="sxs-lookup"><span data-stu-id="f1de5-170">To get SSO configured for your application, you need to sign-on to your People tenant as an administrator.</span></span>
   
8. <span data-ttu-id="f1de5-171">Klik in het menu aan de linkerkant op **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="f1de5-171">In the menu on the left side, click **Settings**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-people-tutorial/tutorial_people_001.png)

9. <span data-ttu-id="f1de5-173">Klik op **bedrijf**.</span><span class="sxs-lookup"><span data-stu-id="f1de5-173">Click **Company**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-people-tutorial/tutorial_people_002.png)

10. <span data-ttu-id="f1de5-175">Op de **uploaden 'Eenmalige aanmelding' SAML meta-gegevensbestand**, klikt u op **Bladeren** het gedownloade metagegevensbestand te uploaden.</span><span class="sxs-lookup"><span data-stu-id="f1de5-175">On the **Upload 'Single Sign On' SAML meta-data file**, click **Browse** to upload the downloaded metadata file.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-people-tutorial/tutorial_people_003.png)

> [!TIP]
> <span data-ttu-id="f1de5-177">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="f1de5-177">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f1de5-178">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="f1de5-178">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f1de5-179">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f1de5-179">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f1de5-180">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="f1de5-180">Creating an Azure AD test user</span></span>
<span data-ttu-id="f1de5-181">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="f1de5-181">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="f1de5-183">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="f1de5-183">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f1de5-184">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="f1de5-184">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-people-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f1de5-186">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="f1de5-186">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-people-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f1de5-188">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f1de5-188">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-people-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f1de5-190">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="f1de5-190">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-people-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f1de5-192">a.</span><span class="sxs-lookup"><span data-stu-id="f1de5-192">a.</span></span> <span data-ttu-id="f1de5-193">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f1de5-193">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f1de5-194">b.</span><span class="sxs-lookup"><span data-stu-id="f1de5-194">b.</span></span> <span data-ttu-id="f1de5-195">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f1de5-195">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f1de5-196">c.</span><span class="sxs-lookup"><span data-stu-id="f1de5-196">c.</span></span> <span data-ttu-id="f1de5-197">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="f1de5-197">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f1de5-198">d.</span><span class="sxs-lookup"><span data-stu-id="f1de5-198">d.</span></span> <span data-ttu-id="f1de5-199">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="f1de5-199">Click **Create**.</span></span>
 
### <a name="creating-a-people-test-user"></a><span data-ttu-id="f1de5-200">Maken van een testgebruiker personen</span><span class="sxs-lookup"><span data-stu-id="f1de5-200">Creating a People test user</span></span>

<span data-ttu-id="f1de5-201">In deze sectie maakt u Britta Simon aangeroepen in mensen van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="f1de5-201">In this section, you create a user called Britta Simon in People.</span></span> <span data-ttu-id="f1de5-202">Werken met [mensen Client ondersteuningsteam](mailto:customerservices@peoplehr.com) om toe te voegen de gebruikers van het platform personen.</span><span class="sxs-lookup"><span data-stu-id="f1de5-202">Work with [People Client support team](mailto:customerservices@peoplehr.com) to add the users in the People platform.</span></span> <span data-ttu-id="f1de5-203">Gebruikers moeten worden gemaakt en worden geactiveerd voordat u eenmalige aanmelding gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f1de5-203">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f1de5-204">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="f1de5-204">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f1de5-205">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan mensen.</span><span class="sxs-lookup"><span data-stu-id="f1de5-205">In this section, you enable Britta Simon to use Azure single sign-on by granting access to People.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="f1de5-207">**Als u wilt toewijzen Britta Simon naar mensen, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="f1de5-207">**To assign Britta Simon to People, perform the following steps:**</span></span>

1. <span data-ttu-id="f1de5-208">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f1de5-208">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="f1de5-210">Selecteer in de lijst met toepassingen **mensen**.</span><span class="sxs-lookup"><span data-stu-id="f1de5-210">In the applications list, select **People**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-people-tutorial/tutorial_people_app.png) 

3. <span data-ttu-id="f1de5-212">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="f1de5-212">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="f1de5-214">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="f1de5-214">Click **Add** button.</span></span> <span data-ttu-id="f1de5-215">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f1de5-215">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="f1de5-217">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="f1de5-217">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f1de5-218">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f1de5-218">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f1de5-219">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f1de5-219">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f1de5-220">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f1de5-220">Testing single sign-on</span></span>

<span data-ttu-id="f1de5-221">Het doel van deze sectie is het testen van uw Azure AD SSO-configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="f1de5-221">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="f1de5-222">Als u op de tegel mensen in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing personen.</span><span class="sxs-lookup"><span data-stu-id="f1de5-222">When you click the People tile in the Access Panel, you should get automatically signed-on to your People application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f1de5-223">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="f1de5-223">Additional resources</span></span>

* [<span data-ttu-id="f1de5-224">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f1de5-224">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f1de5-225">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f1de5-225">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-people-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-people-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-people-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-people-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-people-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-people-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-people-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-people-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-people-tutorial/tutorial_general_203.png

