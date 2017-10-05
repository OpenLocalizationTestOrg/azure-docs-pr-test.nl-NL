---
title: 'Zelfstudie: Azure Active Directory-integratie met JobScore | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en JobScore.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 30f51b32-e55c-4c66-96e8-50a2f9c2194a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: f6ed2d362f7b027bfdc38ba2fdaa03948ff5632c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jobscore"></a><span data-ttu-id="458ff-103">Zelfstudie: Azure Active Directory-integratie met JobScore</span><span class="sxs-lookup"><span data-stu-id="458ff-103">Tutorial: Azure Active Directory integration with JobScore</span></span>

<span data-ttu-id="458ff-104">In deze zelfstudie leert u hoe JobScore integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="458ff-104">In this tutorial, you learn how to integrate JobScore with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="458ff-105">JobScore integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="458ff-105">Integrating JobScore with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="458ff-106">U kunt beheren in Azure AD die toegang tot JobScore heeft</span><span class="sxs-lookup"><span data-stu-id="458ff-106">You can control in Azure AD who has access to JobScore</span></span>
- <span data-ttu-id="458ff-107">U kunt uw gebruikers automatisch ophalen aangemeld bij JobScore (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="458ff-107">You can enable your users to automatically get signed-on to JobScore (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="458ff-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="458ff-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="458ff-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="458ff-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="458ff-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="458ff-110">Prerequisites</span></span>

<span data-ttu-id="458ff-111">Voor het configureren van Azure AD-integratie met JobScore, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="458ff-111">To configure Azure AD integration with JobScore, you need the following items:</span></span>

- <span data-ttu-id="458ff-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="458ff-112">An Azure AD subscription</span></span>
- <span data-ttu-id="458ff-113">Een JobScore eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="458ff-113">A JobScore single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="458ff-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="458ff-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="458ff-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="458ff-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="458ff-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="458ff-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="458ff-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="458ff-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="458ff-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="458ff-118">Scenario description</span></span>
<span data-ttu-id="458ff-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="458ff-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="458ff-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="458ff-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="458ff-121">JobScore uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="458ff-121">Adding JobScore from the gallery</span></span>
2. <span data-ttu-id="458ff-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="458ff-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jobscore-from-the-gallery"></a><span data-ttu-id="458ff-123">JobScore uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="458ff-123">Adding JobScore from the gallery</span></span>
<span data-ttu-id="458ff-124">Voor het configureren van de integratie van JobScore in Azure AD, moet u JobScore uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="458ff-124">To configure the integration of JobScore into Azure AD, you need to add JobScore from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="458ff-125">**Als u wilt toevoegen JobScore uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="458ff-125">**To add JobScore from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="458ff-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="458ff-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="458ff-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="458ff-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="458ff-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="458ff-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="458ff-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="458ff-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="458ff-133">Typ in het zoekvak **JobScore**.</span><span class="sxs-lookup"><span data-stu-id="458ff-133">In the search box, type **JobScore**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_search.png)

5. <span data-ttu-id="458ff-135">Selecteer in het deelvenster resultaten **JobScore**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="458ff-135">In the results panel, select **JobScore**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="458ff-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="458ff-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="458ff-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met JobScore op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="458ff-138">In this section, you configure and test Azure AD single sign-on with JobScore based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="458ff-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in JobScore is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="458ff-139">For single sign-on to work, Azure AD needs to know what the counterpart user in JobScore is to a user in Azure AD.</span></span> <span data-ttu-id="458ff-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in JobScore tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="458ff-140">In other words, a link relationship between an Azure AD user and the related user in JobScore needs to be established.</span></span>

<span data-ttu-id="458ff-141">Wijs in JobScore, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="458ff-141">In JobScore, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="458ff-142">Om te configureren en testen van Azure AD eenmalige aanmelding met JobScore, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="458ff-142">To configure and test Azure AD single sign-on with JobScore, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="458ff-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="458ff-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="458ff-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="458ff-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="458ff-145">**[Maken van een testgebruiker JobScore](#creating-a-jobscore-test-user)**  - JobScore die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="458ff-145">**[Creating a JobScore test user](#creating-a-jobscore-test-user)** - to have a counterpart of Britta Simon in JobScore that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="458ff-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="458ff-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="458ff-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="458ff-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="458ff-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="458ff-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="458ff-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing JobScore configureren.</span><span class="sxs-lookup"><span data-stu-id="458ff-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your JobScore application.</span></span>

<span data-ttu-id="458ff-150">**Voor het configureren van Azure AD eenmalige aanmelding met JobScore, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="458ff-150">**To configure Azure AD single sign-on with JobScore, perform the following steps:**</span></span>

1. <span data-ttu-id="458ff-151">In de Azure-portal op de **JobScore** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="458ff-151">In the Azure portal, on the **JobScore** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="458ff-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="458ff-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_samlbase.png)

3. <span data-ttu-id="458ff-155">Op de **JobScore domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="458ff-155">On the **JobScore Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_url.png)

    <span data-ttu-id="458ff-157">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://hire.jobscore.com/auth/adfs/<company name>`</span><span class="sxs-lookup"><span data-stu-id="458ff-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://hire.jobscore.com/auth/adfs/<company name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="458ff-158">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="458ff-158">This value is not real.</span></span> <span data-ttu-id="458ff-159">Deze waarde bijwerken met de werkelijke URL voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="458ff-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="458ff-160">Neem contact op met [JobScore Client ondersteuningsteam](mailto:support@jobscore.com) deze waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="458ff-160">Contact [JobScore Client support team](mailto:support@jobscore.com) to get this value.</span></span> 
 
4. <span data-ttu-id="458ff-161">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="458ff-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_certificate.png) 

5. <span data-ttu-id="458ff-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="458ff-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jobscore-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="458ff-165">Eenmalige aanmelding configureren op **JobScore** zijde, moet u de gedownloade verzenden **Metadata XML** naar [JobScore ondersteuningsteam](mailto:support@jobscore.com).</span><span class="sxs-lookup"><span data-stu-id="458ff-165">To configure single sign-on on **JobScore** side, you need to send the downloaded **Metadata XML** to [JobScore support team](mailto:support@jobscore.com).</span></span> 

> [!TIP]
> <span data-ttu-id="458ff-166">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="458ff-166">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="458ff-167">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="458ff-167">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="458ff-168">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="458ff-168">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="458ff-169">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="458ff-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="458ff-170">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="458ff-170">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="458ff-172">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="458ff-172">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="458ff-173">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="458ff-173">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jobscore-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="458ff-175">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="458ff-175">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jobscore-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="458ff-177">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="458ff-177">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jobscore-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="458ff-179">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="458ff-179">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jobscore-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="458ff-181">a.</span><span class="sxs-lookup"><span data-stu-id="458ff-181">a.</span></span> <span data-ttu-id="458ff-182">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="458ff-182">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="458ff-183">b.</span><span class="sxs-lookup"><span data-stu-id="458ff-183">b.</span></span> <span data-ttu-id="458ff-184">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="458ff-184">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="458ff-185">c.</span><span class="sxs-lookup"><span data-stu-id="458ff-185">c.</span></span> <span data-ttu-id="458ff-186">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="458ff-186">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="458ff-187">d.</span><span class="sxs-lookup"><span data-stu-id="458ff-187">d.</span></span> <span data-ttu-id="458ff-188">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="458ff-188">Click **Create**.</span></span>
 
### <a name="creating-a-jobscore-test-user"></a><span data-ttu-id="458ff-189">Een testgebruiker JobScore maken</span><span class="sxs-lookup"><span data-stu-id="458ff-189">Creating a JobScore test user</span></span>

<span data-ttu-id="458ff-190">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in JobScore maken.</span><span class="sxs-lookup"><span data-stu-id="458ff-190">In this section, you create a user called Britta Simon in JobScore.</span></span> <span data-ttu-id="458ff-191">Werken met [JobScore ondersteuningsteam](mailto:support@jobscore.com) de gebruikers van het platform JobScore toevoegen.</span><span class="sxs-lookup"><span data-stu-id="458ff-191">Work with [JobScore support team](mailto:support@jobscore.com) to add the users in the JobScore platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="458ff-192">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="458ff-192">Assigning the Azure AD test user</span></span>

<span data-ttu-id="458ff-193">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan JobScore.</span><span class="sxs-lookup"><span data-stu-id="458ff-193">In this section, you enable Britta Simon to use Azure single sign-on by granting access to JobScore.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="458ff-195">**Britta Simon om aan te wijzen JobScore, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="458ff-195">**To assign Britta Simon to JobScore, perform the following steps:**</span></span>

1. <span data-ttu-id="458ff-196">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="458ff-196">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="458ff-198">Selecteer in de lijst met toepassingen **JobScore**.</span><span class="sxs-lookup"><span data-stu-id="458ff-198">In the applications list, select **JobScore**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_app.png) 

3. <span data-ttu-id="458ff-200">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="458ff-200">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="458ff-202">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="458ff-202">Click **Add** button.</span></span> <span data-ttu-id="458ff-203">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="458ff-203">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="458ff-205">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="458ff-205">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="458ff-206">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="458ff-206">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="458ff-207">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="458ff-207">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="458ff-208">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="458ff-208">Testing single sign-on</span></span>

<span data-ttu-id="458ff-209">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="458ff-209">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="458ff-210">Als u op de tegel JobScore in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing JobScore.</span><span class="sxs-lookup"><span data-stu-id="458ff-210">When you click the JobScore tile in the Access Panel, you should get automatically signed-on to your JobScore application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="458ff-211">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="458ff-211">Additional resources</span></span>

* [<span data-ttu-id="458ff-212">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="458ff-212">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="458ff-213">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="458ff-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_203.png

