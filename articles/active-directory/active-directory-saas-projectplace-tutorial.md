---
title: 'Zelfstudie: Azure Active Directory-integratie met Projectplace | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Projectplace.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 298059ca-b652-4577-916a-c31393d53d7a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: bb9dd10c887cb0e42e544066d9b0dcfa554e10ce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-projectplace"></a><span data-ttu-id="b54be-103">Zelfstudie: Azure Active Directory-integratie met Projectplace</span><span class="sxs-lookup"><span data-stu-id="b54be-103">Tutorial: Azure Active Directory integration with Projectplace</span></span>

<span data-ttu-id="b54be-104">In deze zelfstudie leert u hoe Projectplace integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b54be-104">In this tutorial, you learn how to integrate Projectplace with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b54be-105">Projectplace integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="b54be-105">Integrating Projectplace with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b54be-106">U kunt beheren in Azure AD die toegang tot Projectplace heeft</span><span class="sxs-lookup"><span data-stu-id="b54be-106">You can control in Azure AD who has access to Projectplace</span></span>
- <span data-ttu-id="b54be-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Projectplace (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="b54be-107">You can enable your users to automatically get signed-on to Projectplace (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b54be-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="b54be-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b54be-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b54be-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b54be-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="b54be-110">Prerequisites</span></span>

<span data-ttu-id="b54be-111">Voor het configureren van Azure AD-integratie met Projectplace, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="b54be-111">To configure Azure AD integration with Projectplace, you need the following items:</span></span>

- <span data-ttu-id="b54be-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="b54be-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b54be-113">Een Projectplace eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="b54be-113">A Projectplace single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b54be-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="b54be-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b54be-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="b54be-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b54be-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="b54be-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b54be-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b54be-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b54be-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="b54be-118">Scenario description</span></span>
<span data-ttu-id="b54be-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="b54be-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b54be-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="b54be-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b54be-121">Projectplace uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="b54be-121">Adding Projectplace from the gallery</span></span>
2. <span data-ttu-id="b54be-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b54be-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-projectplace-from-the-gallery"></a><span data-ttu-id="b54be-123">Projectplace uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="b54be-123">Adding Projectplace from the gallery</span></span>
<span data-ttu-id="b54be-124">Voor het configureren van de integratie van Projectplace in Azure AD, moet u Projectplace uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="b54be-124">To configure the integration of Projectplace into Azure AD, you need to add Projectplace from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b54be-125">**Als u wilt toevoegen Projectplace uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b54be-125">**To add Projectplace from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b54be-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="b54be-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b54be-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b54be-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b54be-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b54be-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="b54be-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b54be-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="b54be-133">Typ in het zoekvak **Projectplace**.</span><span class="sxs-lookup"><span data-stu-id="b54be-133">In the search box, type **Projectplace**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_search.png)

5. <span data-ttu-id="b54be-135">Selecteer in het deelvenster resultaten **Projectplace**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="b54be-135">In the results panel, select **Projectplace**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b54be-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b54be-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b54be-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Projectplace op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="b54be-138">In this section, you configure and test Azure AD single sign-on with Projectplace based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b54be-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Projectplace is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b54be-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Projectplace is to a user in Azure AD.</span></span> <span data-ttu-id="b54be-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante Projectplace-gebruiker worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b54be-140">In other words, a link relationship between an Azure AD user and the related user in Projectplace needs to be established.</span></span>

<span data-ttu-id="b54be-141">Wijs in Projectplace, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="b54be-141">In Projectplace, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b54be-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Projectplace, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="b54be-142">To configure and test Azure AD single sign-on with Projectplace, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b54be-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b54be-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b54be-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b54be-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b54be-145">**[Maken van een testgebruiker Projectplace](#creating-a-projectplace-test-user)**  - Projectplace die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="b54be-145">**[Creating a Projectplace test user](#creating-a-projectplace-test-user)** - to have a counterpart of Britta Simon in Projectplace that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b54be-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="b54be-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b54be-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="b54be-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b54be-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="b54be-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b54be-149">In deze sectie maakt u Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw Projectplace-toepassing.</span><span class="sxs-lookup"><span data-stu-id="b54be-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Projectplace application.</span></span>

<span data-ttu-id="b54be-150">**Voor het configureren van Azure AD eenmalige aanmelding met Projectplace, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b54be-150">**To configure Azure AD single sign-on with Projectplace, perform the following steps:**</span></span>

1. <span data-ttu-id="b54be-151">In de Azure-portal op de **Projectplace** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="b54be-151">In the Azure portal, on the **Projectplace** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="b54be-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="b54be-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_samlbase.png)

3. <span data-ttu-id="b54be-155">Op de **Projectplace-domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="b54be-155">On the **Projectplace Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_url.png)

    <span data-ttu-id="b54be-157">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<company>.projectplace.com`</span><span class="sxs-lookup"><span data-stu-id="b54be-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company>.projectplace.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b54be-158">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="b54be-158">This value is not real.</span></span> <span data-ttu-id="b54be-159">Deze waarde bijwerken met de werkelijke URL voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="b54be-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="b54be-160">Neem contact op met [Projectplace-Client-ondersteuningsteam](https://success.planview.com/Projectplace/Support) deze waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="b54be-160">Contact [Projectplace Client support team](https://success.planview.com/Projectplace/Support) to get this value.</span></span> 
 
4. <span data-ttu-id="b54be-161">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="b54be-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_certificate.png) 

5. <span data-ttu-id="b54be-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="b54be-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-projectplace-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="b54be-165">Eenmalige aanmelding configureren op **Projectplace** zijde, moet u de gedownloade verzenden **Metadata XML** naar [Projectplace-ondersteuningsteam](https://success.planview.com/Projectplace/Support).</span><span class="sxs-lookup"><span data-stu-id="b54be-165">To configure single sign-on on **Projectplace** side, you need to send the downloaded **Metadata XML** to [Projectplace support team](https://success.planview.com/Projectplace/Support).</span></span> <span data-ttu-id="b54be-166">Ze deze instelling zodat de SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="b54be-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

>[!NOTE]
><span data-ttu-id="b54be-167">De configuratie voor eenmalige aanmelding moet worden uitgevoerd door de [Projectplace-ondersteuningsteam](https://success.planview.com/Projectplace/Support).</span><span class="sxs-lookup"><span data-stu-id="b54be-167">The single sign-on configuration has to be performed by the [Projectplace support team](https://success.planview.com/Projectplace/Support).</span></span> <span data-ttu-id="b54be-168">U ontvangt een melding zodra de configuratie is voltooid.</span><span class="sxs-lookup"><span data-stu-id="b54be-168">You will get a notification as soon as the configuration has been completed.</span></span>

> [!TIP]
> <span data-ttu-id="b54be-169">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="b54be-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b54be-170">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="b54be-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b54be-171">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b54be-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b54be-172">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="b54be-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="b54be-173">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="b54be-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="b54be-175">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b54be-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b54be-176">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="b54be-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-projectplace-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b54be-178">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="b54be-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-projectplace-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b54be-180">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b54be-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-projectplace-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b54be-182">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="b54be-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-projectplace-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b54be-184">a.</span><span class="sxs-lookup"><span data-stu-id="b54be-184">a.</span></span> <span data-ttu-id="b54be-185">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b54be-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b54be-186">b.</span><span class="sxs-lookup"><span data-stu-id="b54be-186">b.</span></span> <span data-ttu-id="b54be-187">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b54be-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b54be-188">c.</span><span class="sxs-lookup"><span data-stu-id="b54be-188">c.</span></span> <span data-ttu-id="b54be-189">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="b54be-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b54be-190">d.</span><span class="sxs-lookup"><span data-stu-id="b54be-190">d.</span></span> <span data-ttu-id="b54be-191">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="b54be-191">Click **Create**.</span></span>
 
### <a name="creating-a-projectplace-test-user"></a><span data-ttu-id="b54be-192">Een testgebruiker Projectplace maken</span><span class="sxs-lookup"><span data-stu-id="b54be-192">Creating a Projectplace test user</span></span>

<span data-ttu-id="b54be-193">Om in te schakelen gebruikers van Azure AD aan te melden bij Projectplace, moeten ze worden ingericht in Projectplace.</span><span class="sxs-lookup"><span data-stu-id="b54be-193">In order to enable Azure AD users to log into Projectplace, they must be provisioned into Projectplace.</span></span> <span data-ttu-id="b54be-194">In het geval van Projectplace is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="b54be-194">In the case of Projectplace, provisioning is a manual task.</span></span>

<span data-ttu-id="b54be-195">**Voor het inrichten van een gebruikersaccount, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b54be-195">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="b54be-196">Meld u aan bij uw **Projectplace** bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="b54be-196">Log in to your **Projectplace** company site as an administrator.</span></span>

2. <span data-ttu-id="b54be-197">Ga naar **mensen**, en klik vervolgens op **leden**.</span><span class="sxs-lookup"><span data-stu-id="b54be-197">Go to **People**, and then click **Members**.</span></span>
   
    <span data-ttu-id="b54be-198">![Mensen](./media/active-directory-saas-projectplace-tutorial/ic790228.png "personen")</span><span class="sxs-lookup"><span data-stu-id="b54be-198">![People](./media/active-directory-saas-projectplace-tutorial/ic790228.png "People")</span></span>

3. <span data-ttu-id="b54be-199">Klik op **lid toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b54be-199">Click **Add Member**.</span></span>
   
    <span data-ttu-id="b54be-200">![Toevoegen van leden](./media/active-directory-saas-projectplace-tutorial/ic790232.png "leden toevoegen")</span><span class="sxs-lookup"><span data-stu-id="b54be-200">![Add Members](./media/active-directory-saas-projectplace-tutorial/ic790232.png "Add Members")</span></span>

4. <span data-ttu-id="b54be-201">In de **lid toevoegen** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="b54be-201">In the **Add Member** section, perform the following steps:</span></span>
   
    <span data-ttu-id="b54be-202">![Nieuwe leden](./media/active-directory-saas-projectplace-tutorial/ic790233.png "nieuwe leden")</span><span class="sxs-lookup"><span data-stu-id="b54be-202">![New Members](./media/active-directory-saas-projectplace-tutorial/ic790233.png "New Members")</span></span>
   
    <span data-ttu-id="b54be-203">a.</span><span class="sxs-lookup"><span data-stu-id="b54be-203">a.</span></span> <span data-ttu-id="b54be-204">In de **nieuwe leden** textbox, typ de e-mailadres van een geldige AAD-account dat u inrichten in de bijbehorende tekstvakken wilt.</span><span class="sxs-lookup"><span data-stu-id="b54be-204">In the **New Members** textbox, type the email address of a valid AAD account you want to provision into the related textboxes.</span></span>
   
    <span data-ttu-id="b54be-205">b.</span><span class="sxs-lookup"><span data-stu-id="b54be-205">b.</span></span> <span data-ttu-id="b54be-206">Klik op **verzenden**.</span><span class="sxs-lookup"><span data-stu-id="b54be-206">Click **Send**.</span></span>

   <span data-ttu-id="b54be-207">Een e-mailbericht met inbegrip van een koppeling om te bevestigen van het account voordat deze actief is verzonden naar de houder van Azure Active Directory-account.</span><span class="sxs-lookup"><span data-stu-id="b54be-207">An email including a link to confirm the account before it becomes active is sent to the Azure Active Directory account holder.</span></span>

>[!NOTE]
><span data-ttu-id="b54be-208">U kunt andere Projectplace gebruiker account hulpmiddelen voor het maken of API's die is geleverd door Projectplace aan inrichten AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="b54be-208">You can use any other Projectplace user account creation tools or APIs provided by Projectplace to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b54be-209">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="b54be-209">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b54be-210">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Projectplace.</span><span class="sxs-lookup"><span data-stu-id="b54be-210">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Projectplace.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="b54be-212">**Britta Simon om aan te wijzen Projectplace, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b54be-212">**To assign Britta Simon to Projectplace, perform the following steps:**</span></span>

1. <span data-ttu-id="b54be-213">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b54be-213">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="b54be-215">Selecteer in de lijst met toepassingen **Projectplace**.</span><span class="sxs-lookup"><span data-stu-id="b54be-215">In the applications list, select **Projectplace**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_app.png) 

3. <span data-ttu-id="b54be-217">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="b54be-217">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="b54be-219">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="b54be-219">Click **Add** button.</span></span> <span data-ttu-id="b54be-220">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b54be-220">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="b54be-222">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="b54be-222">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b54be-223">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b54be-223">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b54be-224">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b54be-224">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b54be-225">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b54be-225">Testing single sign-on</span></span>

<span data-ttu-id="b54be-226">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="b54be-226">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b54be-227">Als u op de Projectplace-tegel in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw Projectplace-toepassing.</span><span class="sxs-lookup"><span data-stu-id="b54be-227">When you click the Projectplace tile in the Access Panel, you should get automatically signed-on to your Projectplace application.</span></span>
<span data-ttu-id="b54be-228">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b54be-228">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b54be-229">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="b54be-229">Additional resources</span></span>

* [<span data-ttu-id="b54be-230">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b54be-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b54be-231">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b54be-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_203.png

