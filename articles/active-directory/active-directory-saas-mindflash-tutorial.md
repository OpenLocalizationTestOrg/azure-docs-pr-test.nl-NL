---
title: 'Zelfstudie: Azure Active Directory-integratie met Mindflash | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Mindflash.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bdf91993-aaaa-4598-89b7-77ef8ca065d5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 90de7b6a82d88f9407a35fbfebe8a652928d76cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mindflash"></a><span data-ttu-id="495d6-103">Zelfstudie: Azure Active Directory-integratie met Mindflash</span><span class="sxs-lookup"><span data-stu-id="495d6-103">Tutorial: Azure Active Directory integration with Mindflash</span></span>

<span data-ttu-id="495d6-104">In deze zelfstudie leert u hoe Mindflash integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="495d6-104">In this tutorial, you learn how to integrate Mindflash with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="495d6-105">Mindflash integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="495d6-105">Integrating Mindflash with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="495d6-106">U kunt beheren in Azure AD die toegang tot Mindflash heeft</span><span class="sxs-lookup"><span data-stu-id="495d6-106">You can control in Azure AD who has access to Mindflash</span></span>
- <span data-ttu-id="495d6-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Mindflash (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="495d6-107">You can enable your users to automatically get signed-on to Mindflash (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="495d6-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="495d6-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="495d6-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="495d6-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="495d6-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="495d6-110">Prerequisites</span></span>

<span data-ttu-id="495d6-111">Voor het configureren van Azure AD-integratie met Mindflash, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="495d6-111">To configure Azure AD integration with Mindflash, you need the following items:</span></span>

- <span data-ttu-id="495d6-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="495d6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="495d6-113">Een Mindflash eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="495d6-113">A Mindflash single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="495d6-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="495d6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="495d6-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="495d6-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="495d6-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="495d6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="495d6-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="495d6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="495d6-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="495d6-118">Scenario description</span></span>
<span data-ttu-id="495d6-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="495d6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="495d6-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="495d6-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="495d6-121">Mindflash uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="495d6-121">Adding Mindflash from the gallery</span></span>
2. <span data-ttu-id="495d6-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="495d6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mindflash-from-the-gallery"></a><span data-ttu-id="495d6-123">Mindflash uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="495d6-123">Adding Mindflash from the gallery</span></span>
<span data-ttu-id="495d6-124">Voor het configureren van de integratie van Mindflash in Azure AD, moet u Mindflash uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="495d6-124">To configure the integration of Mindflash into Azure AD, you need to add Mindflash from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="495d6-125">**Als u wilt toevoegen Mindflash uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="495d6-125">**To add Mindflash from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="495d6-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="495d6-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="495d6-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="495d6-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="495d6-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="495d6-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="495d6-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="495d6-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="495d6-133">Typ in het zoekvak **Mindflash**.</span><span class="sxs-lookup"><span data-stu-id="495d6-133">In the search box, type **Mindflash**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_search.png)

5. <span data-ttu-id="495d6-135">Selecteer in het deelvenster resultaten **Mindflash**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="495d6-135">In the results panel, select **Mindflash**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="495d6-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="495d6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="495d6-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Mindflash op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="495d6-138">In this section, you configure and test Azure AD single sign-on with Mindflash based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="495d6-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Mindflash is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="495d6-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Mindflash is to a user in Azure AD.</span></span> <span data-ttu-id="495d6-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Mindflash tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="495d6-140">In other words, a link relationship between an Azure AD user and the related user in Mindflash needs to be established.</span></span>

<span data-ttu-id="495d6-141">Wijs in Mindflash, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="495d6-141">In Mindflash, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="495d6-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Mindflash, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="495d6-142">To configure and test Azure AD single sign-on with Mindflash, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="495d6-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="495d6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="495d6-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="495d6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="495d6-145">**[Maken van een testgebruiker Mindflash](#creating-a-mindflash-test-user)**  - Mindflash die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="495d6-145">**[Creating a Mindflash test user](#creating-a-mindflash-test-user)** - to have a counterpart of Britta Simon in Mindflash that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="495d6-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="495d6-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="495d6-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="495d6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="495d6-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="495d6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="495d6-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Mindflash configureren.</span><span class="sxs-lookup"><span data-stu-id="495d6-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Mindflash application.</span></span>

<span data-ttu-id="495d6-150">**Voor het configureren van Azure AD eenmalige aanmelding met Mindflash, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="495d6-150">**To configure Azure AD single sign-on with Mindflash, perform the following steps:**</span></span>

1. <span data-ttu-id="495d6-151">In de Azure-portal op de **Mindflash** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="495d6-151">In the Azure portal, on the **Mindflash** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="495d6-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="495d6-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_samlbase.png)

3. <span data-ttu-id="495d6-155">Op de **Mindflash domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="495d6-155">On the **Mindflash Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_url.png)

    <span data-ttu-id="495d6-157">a.</span><span class="sxs-lookup"><span data-stu-id="495d6-157">a.</span></span> <span data-ttu-id="495d6-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<companyname>.mindflash.com`</span><span class="sxs-lookup"><span data-stu-id="495d6-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.mindflash.com`</span></span>

    <span data-ttu-id="495d6-159">b.</span><span class="sxs-lookup"><span data-stu-id="495d6-159">b.</span></span> <span data-ttu-id="495d6-160">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<companyname>.mindflash.com`</span><span class="sxs-lookup"><span data-stu-id="495d6-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.mindflash.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="495d6-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="495d6-161">These values are not real.</span></span> <span data-ttu-id="495d6-162">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="495d6-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="495d6-163">Neem contact op met [Mindflash Client ondersteuningsteam](https://www.mindflash.com/contact/) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="495d6-163">Contact [Mindflash Client support team](https://www.mindflash.com/contact/) to get these values.</span></span> 
 


4. <span data-ttu-id="495d6-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="495d6-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_certificate.png) 

5. <span data-ttu-id="495d6-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="495d6-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mindflash-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="495d6-168">Eenmalige aanmelding configureren op **Mindflash** zijde, moet u de gedownloade verzenden **Metadata XML** naar [Mindflash ondersteuningsteam](https://www.mindflash.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="495d6-168">To configure single sign-on on **Mindflash** side, you need to send the downloaded **Metadata XML** to [Mindflash support team](https://www.mindflash.com/contact/).</span></span>

> [!TIP]
> <span data-ttu-id="495d6-169">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="495d6-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="495d6-170">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="495d6-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="495d6-171">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="495d6-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="495d6-172">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="495d6-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="495d6-173">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="495d6-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="495d6-175">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="495d6-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="495d6-176">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="495d6-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mindflash-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="495d6-178">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="495d6-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mindflash-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="495d6-180">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="495d6-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mindflash-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="495d6-182">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="495d6-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mindflash-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="495d6-184">a.</span><span class="sxs-lookup"><span data-stu-id="495d6-184">a.</span></span> <span data-ttu-id="495d6-185">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="495d6-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="495d6-186">b.</span><span class="sxs-lookup"><span data-stu-id="495d6-186">b.</span></span> <span data-ttu-id="495d6-187">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="495d6-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="495d6-188">c.</span><span class="sxs-lookup"><span data-stu-id="495d6-188">c.</span></span> <span data-ttu-id="495d6-189">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="495d6-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="495d6-190">d.</span><span class="sxs-lookup"><span data-stu-id="495d6-190">d.</span></span> <span data-ttu-id="495d6-191">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="495d6-191">Click **Create**.</span></span>
 
### <a name="creating-a-mindflash-test-user"></a><span data-ttu-id="495d6-192">Een testgebruiker Mindflash maken</span><span class="sxs-lookup"><span data-stu-id="495d6-192">Creating a Mindflash test user</span></span>

<span data-ttu-id="495d6-193">Om in te schakelen gebruikers van Azure AD aan te melden bij Mindflash, moeten ze worden ingericht in Mindflash.</span><span class="sxs-lookup"><span data-stu-id="495d6-193">In order to enable Azure AD users to log into Mindflash, they must be provisioned into Mindflash.</span></span> <span data-ttu-id="495d6-194">In het geval van Mindflash is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="495d6-194">In the case of Mindflash, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-accounts-perform-the-following-steps"></a><span data-ttu-id="495d6-195">Voor het inrichten van een gebruikersaccount, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="495d6-195">To provision a user accounts, perform the following steps:</span></span>

1. <span data-ttu-id="495d6-196">Meld u aan bij uw **Mindflash** bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="495d6-196">Log in to your **Mindflash** company site as an administrator.</span></span>

2. <span data-ttu-id="495d6-197">Ga naar **gebruikers beheren**.</span><span class="sxs-lookup"><span data-stu-id="495d6-197">Go to **Manage Users**.</span></span>
   
    <span data-ttu-id="495d6-198">![Gebruikers beheren](./media/active-directory-saas-mindflash-tutorial/ic787140.png "gebruikers beheren")</span><span class="sxs-lookup"><span data-stu-id="495d6-198">![Manage Users](./media/active-directory-saas-mindflash-tutorial/ic787140.png "Manage Users")</span></span>

3. <span data-ttu-id="495d6-199">Klik op de **gebruikers toevoegen**, en klik vervolgens op **nieuw**.</span><span class="sxs-lookup"><span data-stu-id="495d6-199">Click the **Add Users**, and then click **New**.</span></span>

4. <span data-ttu-id="495d6-200">In de **nieuwe gebruikers toevoegen** sectie, voert u de volgende stappen van een geldig Azure AD-account die u inrichten wilt:</span><span class="sxs-lookup"><span data-stu-id="495d6-200">In the **Add New Users** section, perform the following steps of a valid Azure AD account you want to provision:</span></span>
   
    <span data-ttu-id="495d6-201">![Nieuwe gebruikers toevoegen](./media/active-directory-saas-mindflash-tutorial/ic787141.png "nieuwe gebruikers toevoegen")</span><span class="sxs-lookup"><span data-stu-id="495d6-201">![Add New Users](./media/active-directory-saas-mindflash-tutorial/ic787141.png "Add New Users")</span></span>
   
    <span data-ttu-id="495d6-202">a.</span><span class="sxs-lookup"><span data-stu-id="495d6-202">a.</span></span> <span data-ttu-id="495d6-203">In de **voornaam** textbox type **voornaam** van de gebruiker als **Britta**.</span><span class="sxs-lookup"><span data-stu-id="495d6-203">In the **First name** textbox, type **First name** of the user as **Britta**.</span></span>

    <span data-ttu-id="495d6-204">b.</span><span class="sxs-lookup"><span data-stu-id="495d6-204">b.</span></span> <span data-ttu-id="495d6-205">In de **achternaam** textbox type **achternaam** van de gebruiker als **Simon**.</span><span class="sxs-lookup"><span data-stu-id="495d6-205">In the **Last name** textbox, type **Last name** of the user as **Simon**.</span></span>
    
    <span data-ttu-id="495d6-206">c.</span><span class="sxs-lookup"><span data-stu-id="495d6-206">c.</span></span> <span data-ttu-id="495d6-207">In de **e** textbox type **e-mailadres** van de gebruiker als  **BrittaSimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="495d6-207">In the **Email** textbox, type **Email Address** of the user as **BrittaSimon@contoso.com**.</span></span>

    <span data-ttu-id="495d6-208">b.</span><span class="sxs-lookup"><span data-stu-id="495d6-208">b.</span></span> <span data-ttu-id="495d6-209">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="495d6-209">Click **Add**.</span></span>

>[!NOTE]
><span data-ttu-id="495d6-210">U kunt andere Mindflash gebruiker account hulpmiddelen voor het maken of API's die is geleverd door Mindflash aan inrichten AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="495d6-210">You can use any other Mindflash user account creation tools or APIs provided by Mindflash to provision AAD user accounts.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="495d6-211">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="495d6-211">Assigning the Azure AD test user</span></span>

<span data-ttu-id="495d6-212">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Mindflash.</span><span class="sxs-lookup"><span data-stu-id="495d6-212">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Mindflash.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="495d6-214">**Britta Simon om aan te wijzen Mindflash, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="495d6-214">**To assign Britta Simon to Mindflash, perform the following steps:**</span></span>

1. <span data-ttu-id="495d6-215">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="495d6-215">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="495d6-217">Selecteer in de lijst met toepassingen **Mindflash**.</span><span class="sxs-lookup"><span data-stu-id="495d6-217">In the applications list, select **Mindflash**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_app.png) 

3. <span data-ttu-id="495d6-219">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="495d6-219">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="495d6-221">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="495d6-221">Click **Add** button.</span></span> <span data-ttu-id="495d6-222">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="495d6-222">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="495d6-224">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="495d6-224">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="495d6-225">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="495d6-225">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="495d6-226">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="495d6-226">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="495d6-227">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="495d6-227">Testing single sign-on</span></span>

<span data-ttu-id="495d6-228">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="495d6-228">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="495d6-229">Als u op de tegel Mindflash in het deelvenster toegang, krijgt u de aanmeldingspagina van Mindflash toepassing.</span><span class="sxs-lookup"><span data-stu-id="495d6-229">When you click the Mindflash tile in the Access Panel, you should get login page of Mindflash application.</span></span>
<span data-ttu-id="495d6-230">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="495d6-230">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="495d6-231">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="495d6-231">Additional resources</span></span>

* [<span data-ttu-id="495d6-232">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="495d6-232">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="495d6-233">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="495d6-233">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_203.png

