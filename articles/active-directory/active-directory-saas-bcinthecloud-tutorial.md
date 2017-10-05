---
title: 'Zelfstudie: Azure Active Directory-integratie met BC in de Cloud | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en BC in de Cloud.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7dc40d2c-6349-40cb-b304-b098bd03a66c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/1/2017
ms.author: jeedes
ms.openlocfilehash: ebc95d600eca1027331cd92cfe481d0c3ee833a5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bc-in-the-cloud"></a><span data-ttu-id="ee30f-103">Zelfstudie: Azure Active Directory-integratie met BC in de Cloud</span><span class="sxs-lookup"><span data-stu-id="ee30f-103">Tutorial: Azure Active Directory integration with BC in the Cloud</span></span>

<span data-ttu-id="ee30f-104">In deze zelfstudie leert u hoe BC integreren in de Cloud met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ee30f-104">In this tutorial, you learn how to integrate BC in the Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ee30f-105">BC integreren in de Cloud met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="ee30f-105">Integrating BC in the Cloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ee30f-106">U kunt beheren in Azure AD die toegang tot BC in de Cloud heeft</span><span class="sxs-lookup"><span data-stu-id="ee30f-106">You can control in Azure AD who has access to BC in the Cloud</span></span>
- <span data-ttu-id="ee30f-107">U kunt uw gebruikers automatisch ophalen aangemeld bij BC in de Cloud (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="ee30f-107">You can enable your users to automatically get signed-on to BC in the Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ee30f-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="ee30f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ee30f-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ee30f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ee30f-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ee30f-110">Prerequisites</span></span>

<span data-ttu-id="ee30f-111">Voor het configureren van Azure AD-integratie met BC in de Cloud, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="ee30f-111">To configure Azure AD integration with BC in the Cloud, you need the following items:</span></span>

- <span data-ttu-id="ee30f-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="ee30f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ee30f-113">Een BC in de Cloud eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="ee30f-113">A BC in the Cloud single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ee30f-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="ee30f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ee30f-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="ee30f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ee30f-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="ee30f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ee30f-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ee30f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ee30f-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="ee30f-118">Scenario description</span></span>
<span data-ttu-id="ee30f-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="ee30f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ee30f-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="ee30f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ee30f-121">BC toe te voegen in de Cloud uit de galerie</span><span class="sxs-lookup"><span data-stu-id="ee30f-121">Adding BC in the Cloud from the gallery</span></span>
2. <span data-ttu-id="ee30f-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ee30f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bc-in-the-cloud-from-the-gallery"></a><span data-ttu-id="ee30f-123">BC toe te voegen in de Cloud uit de galerie</span><span class="sxs-lookup"><span data-stu-id="ee30f-123">Adding BC in the Cloud from the gallery</span></span>
<span data-ttu-id="ee30f-124">Voor het configureren van de integratie van BC in de Cloud met Azure AD, moet u BC in de Cloud uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="ee30f-124">To configure the integration of BC in the Cloud into Azure AD, you need to add BC in the Cloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ee30f-125">**Als u wilt toevoegen BC in de Cloud uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="ee30f-125">**To add BC in the Cloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ee30f-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="ee30f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ee30f-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ee30f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ee30f-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ee30f-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="ee30f-131">Om de nieuwe toepassing toevoegen, klikt u op **toevoegen** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ee30f-131">To add new application, click **Add** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="ee30f-133">Typ in het zoekvak **BC in de Cloud**.</span><span class="sxs-lookup"><span data-stu-id="ee30f-133">In the search box, type **BC in the Cloud**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_search.png)

5. <span data-ttu-id="ee30f-135">Selecteer in het deelvenster resultaten **BC in de Cloud**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="ee30f-135">In the results panel, select **BC in the Cloud**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ee30f-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ee30f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ee30f-138">In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met BC in de Cloud op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="ee30f-138">In this section, you configure and test Azure AD single sign-on with BC in the Cloud based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ee30f-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker van het bijbehorende equivalent in BC in de Cloud is aan een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ee30f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BC in the Cloud is to a user in Azure AD.</span></span> <span data-ttu-id="ee30f-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in BC in de Cloud worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ee30f-140">In other words, a link relationship between an Azure AD user and the related user in BC in the Cloud needs to be established.</span></span>

<span data-ttu-id="ee30f-141">Wijs in BC in de Cloud, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="ee30f-141">In BC in the Cloud, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ee30f-142">Om te configureren en testen van Azure AD eenmalige aanmelding met BC in de Cloud, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="ee30f-142">To configure and test Azure AD single sign-on with BC in the Cloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ee30f-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ee30f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ee30f-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ee30f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ee30f-145">**[Maken van een BC in de Cloud testgebruiker](#creating-a-bc-in-the-cloud-test-user)**  - bevatten een equivalent van Britta Simon BC in de Cloud die is gekoppeld aan de Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="ee30f-145">**[Creating a BC in the Cloud test user](#creating-a-bc-in-the-cloud-test-user)** - to have a counterpart of Britta Simon in BC in the Cloud that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ee30f-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="ee30f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ee30f-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="ee30f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ee30f-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="ee30f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ee30f-149">In deze sectie maakt u Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw BC in de Cloud-toepassing.</span><span class="sxs-lookup"><span data-stu-id="ee30f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BC in the Cloud application.</span></span>

<span data-ttu-id="ee30f-150">**Voor het configureren van Azure AD eenmalige aanmelding met BC in de Cloud, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="ee30f-150">**To configure Azure AD single sign-on with BC in the Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="ee30f-151">In de Azure-portal op de **BC in de Cloud** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="ee30f-151">In the Azure portal, on the **BC in the Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="ee30f-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="ee30f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_samlbase.png)

3. <span data-ttu-id="ee30f-155">Op de **BC in de Cloud-domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="ee30f-155">On the **BC in the Cloud Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_url.png)

    <span data-ttu-id="ee30f-157">a.</span><span class="sxs-lookup"><span data-stu-id="ee30f-157">a.</span></span> <span data-ttu-id="ee30f-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://app.bcinthecloud.com/router/loginSaml/<customerid>`</span><span class="sxs-lookup"><span data-stu-id="ee30f-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://app.bcinthecloud.com/router/loginSaml/<customerid>`</span></span>

    <span data-ttu-id="ee30f-159">b.</span><span class="sxs-lookup"><span data-stu-id="ee30f-159">b.</span></span> <span data-ttu-id="ee30f-160">In de **id** textbox, typ een URL als:`https://app.bcinthecloud.com`</span><span class="sxs-lookup"><span data-stu-id="ee30f-160">In the **Identifier** textbox, type a URL as: `https://app.bcinthecloud.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ee30f-161">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="ee30f-161">This value is not real.</span></span> <span data-ttu-id="ee30f-162">Deze waarde bijwerken met de werkelijke URL voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="ee30f-162">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="ee30f-163">Neem contact op met [BC in de Cloud-Client ondersteuningsteam](https://www.bcinthecloud.com/supportcenter/) deze waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="ee30f-163">Contact [BC in the Cloud Client support team](https://www.bcinthecloud.com/supportcenter/) to get this value.</span></span> 
 
4. <span data-ttu-id="ee30f-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="ee30f-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_certificate.png) 

5. <span data-ttu-id="ee30f-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="ee30f-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ee30f-168">Eenmalige aanmelding configureren op **BC in de Cloud** zijde, moet u de gedownloade verzenden **Metadata XML** naar [BC in de Cloud ondersteuningsteam](https://www.bcinthecloud.com/supportcenter/).</span><span class="sxs-lookup"><span data-stu-id="ee30f-168">To configure single sign-on on **BC in the Cloud** side, you need to send the downloaded **Metadata XML** to [BC in the Cloud support team](https://www.bcinthecloud.com/supportcenter/).</span></span>

> [!TIP]
> <span data-ttu-id="ee30f-169">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="ee30f-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ee30f-170">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="ee30f-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ee30f-171">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ee30f-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ee30f-172">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="ee30f-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="ee30f-173">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="ee30f-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="ee30f-175">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="ee30f-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ee30f-176">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="ee30f-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bcinthecloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ee30f-178">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="ee30f-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bcinthecloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ee30f-180">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ee30f-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bcinthecloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ee30f-182">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="ee30f-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bcinthecloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ee30f-184">a.</span><span class="sxs-lookup"><span data-stu-id="ee30f-184">a.</span></span> <span data-ttu-id="ee30f-185">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ee30f-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ee30f-186">b.</span><span class="sxs-lookup"><span data-stu-id="ee30f-186">b.</span></span> <span data-ttu-id="ee30f-187">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ee30f-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ee30f-188">c.</span><span class="sxs-lookup"><span data-stu-id="ee30f-188">c.</span></span> <span data-ttu-id="ee30f-189">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="ee30f-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ee30f-190">d.</span><span class="sxs-lookup"><span data-stu-id="ee30f-190">d.</span></span> <span data-ttu-id="ee30f-191">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="ee30f-191">Click **Create**.</span></span>
 
### <a name="creating-a-bc-in-the-cloud-test-user"></a><span data-ttu-id="ee30f-192">Maken van een BC in de Cloud testgebruiker</span><span class="sxs-lookup"><span data-stu-id="ee30f-192">Creating a BC in the Cloud test user</span></span>

<span data-ttu-id="ee30f-193">In deze sectie maakt u een gebruiker Britta Simon in BC aangeroepen in de Cloud.</span><span class="sxs-lookup"><span data-stu-id="ee30f-193">In this section, you create a user called Britta Simon in BC in the Cloud.</span></span> <span data-ttu-id="ee30f-194">Werken met [BC in de Cloud-Client ondersteuningsteam](https://www.bcinthecloud.com/supportcenter/) de gebruikers in de BC in de Cloud-toepassing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="ee30f-194">Work with [BC in the Cloud Client support team](https://www.bcinthecloud.com/supportcenter/) to add the users in the BC in the Cloud application.</span></span> <span data-ttu-id="ee30f-195">Gebruikers moeten worden gemaakt en worden geactiveerd voordat u eenmalige aanmelding gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ee30f-195">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ee30f-196">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="ee30f-196">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ee30f-197">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan BC in de Cloud.</span><span class="sxs-lookup"><span data-stu-id="ee30f-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BC in the Cloud.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="ee30f-199">**Britta Simon om aan te wijzen BC in de Cloud, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="ee30f-199">**To assign Britta Simon to BC in the Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="ee30f-200">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ee30f-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="ee30f-202">Selecteer in de lijst met toepassingen **BC in de Cloud**.</span><span class="sxs-lookup"><span data-stu-id="ee30f-202">In the applications list, select **BC in the Cloud**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_app.png) 

3. <span data-ttu-id="ee30f-204">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="ee30f-204">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="ee30f-206">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="ee30f-206">Click **Add** button.</span></span> <span data-ttu-id="ee30f-207">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ee30f-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="ee30f-209">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="ee30f-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ee30f-210">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ee30f-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ee30f-211">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ee30f-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ee30f-212">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ee30f-212">Testing single sign-on</span></span>

<span data-ttu-id="ee30f-213">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="ee30f-213">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

 <span data-ttu-id="ee30f-214">Als u op de BC in de Cloud-tegel in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw BC in de Cloud-toepassing.</span><span class="sxs-lookup"><span data-stu-id="ee30f-214">When you click the BC in the Cloud tile in the Access Panel, you should get automatically signed-on to your BC in the Cloud application.</span></span> <span data-ttu-id="ee30f-215">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ee30f-215">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ee30f-216">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="ee30f-216">Additional resources</span></span>

* [<span data-ttu-id="ee30f-217">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ee30f-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ee30f-218">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ee30f-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_203.png

