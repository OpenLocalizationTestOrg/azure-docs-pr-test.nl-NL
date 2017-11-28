---
title: 'Zelfstudie: Azure Active Directory-integratie met Lecorpio | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Lecorpio.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/02/2017
ms.author: jeedes
ms.openlocfilehash: 35c94e2d9d8a938971f85ea732a74a7e1655545e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lecorpio"></a><span data-ttu-id="b43a2-103">Zelfstudie: Azure Active Directory-integratie met Lecorpio</span><span class="sxs-lookup"><span data-stu-id="b43a2-103">Tutorial: Azure Active Directory integration with Lecorpio</span></span>

<span data-ttu-id="b43a2-104">In deze zelfstudie leert u hoe Lecorpio integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b43a2-104">In this tutorial, you learn how to integrate Lecorpio with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b43a2-105">Lecorpio integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="b43a2-105">Integrating Lecorpio with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b43a2-106">U kunt beheren in Azure AD die toegang tot Lecorpio heeft</span><span class="sxs-lookup"><span data-stu-id="b43a2-106">You can control in Azure AD who has access to Lecorpio</span></span>
- <span data-ttu-id="b43a2-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Lecorpio (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="b43a2-107">You can enable your users to automatically get signed-on to Lecorpio (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b43a2-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="b43a2-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b43a2-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b43a2-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b43a2-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="b43a2-110">Prerequisites</span></span>

<span data-ttu-id="b43a2-111">Voor het configureren van Azure AD-integratie met Lecorpio, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="b43a2-111">To configure Azure AD integration with Lecorpio, you need the following items:</span></span>

- <span data-ttu-id="b43a2-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="b43a2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b43a2-113">Een Lecorpio eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="b43a2-113">A Lecorpio single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b43a2-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="b43a2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b43a2-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="b43a2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b43a2-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="b43a2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b43a2-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b43a2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b43a2-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="b43a2-118">Scenario description</span></span>
<span data-ttu-id="b43a2-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="b43a2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b43a2-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="b43a2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b43a2-121">Lecorpio uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="b43a2-121">Adding Lecorpio from the gallery</span></span>
2. <span data-ttu-id="b43a2-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b43a2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lecorpio-from-the-gallery"></a><span data-ttu-id="b43a2-123">Lecorpio uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="b43a2-123">Adding Lecorpio from the gallery</span></span>
<span data-ttu-id="b43a2-124">Voor het configureren van de integratie van Lecorpio in Azure AD, moet u Lecorpio uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="b43a2-124">To configure the integration of Lecorpio into Azure AD, you need to add Lecorpio from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b43a2-125">**Als u wilt toevoegen Lecorpio uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b43a2-125">**To add Lecorpio from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b43a2-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="b43a2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b43a2-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b43a2-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b43a2-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b43a2-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="b43a2-131">Klik op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b43a2-131">Click **New application** button on the top of the dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="b43a2-133">Typ in het zoekvak **Lecorpio**.</span><span class="sxs-lookup"><span data-stu-id="b43a2-133">In the search box, type **Lecorpio**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_search.png)

5. <span data-ttu-id="b43a2-135">Selecteer in het deelvenster resultaten **Lecorpio**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="b43a2-135">In the results panel, select **Lecorpio**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b43a2-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b43a2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b43a2-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Lecorpio op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="b43a2-138">In this section, you configure and test Azure AD single sign-on with Lecorpio based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b43a2-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Lecorpio is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b43a2-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Lecorpio is to a user in Azure AD.</span></span> <span data-ttu-id="b43a2-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Lecorpio tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="b43a2-140">In other words, a link relationship between an Azure AD user and the related user in Lecorpio needs to be established.</span></span>

<span data-ttu-id="b43a2-141">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in Lecorpio.</span><span class="sxs-lookup"><span data-stu-id="b43a2-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Lecorpio.</span></span>

<span data-ttu-id="b43a2-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Lecorpio, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="b43a2-142">To configure and test Azure AD single sign-on with Lecorpio, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b43a2-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b43a2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b43a2-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b43a2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b43a2-145">**[Maken van een testgebruiker Lecorpio](#creating-a-lecorpio-test-user)**  - Lecorpio die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="b43a2-145">**[Creating a Lecorpio test user](#creating-a-lecorpio-test-user)** - to have a counterpart of Britta Simon in Lecorpio that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b43a2-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="b43a2-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b43a2-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="b43a2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b43a2-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="b43a2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b43a2-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Lecorpio configureren.</span><span class="sxs-lookup"><span data-stu-id="b43a2-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Lecorpio application.</span></span>

<span data-ttu-id="b43a2-150">**Voor het configureren van Azure AD eenmalige aanmelding met Lecorpio, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b43a2-150">**To configure Azure AD single sign-on with Lecorpio, perform the following steps:**</span></span>

1. <span data-ttu-id="b43a2-151">In de Azure-portal op de **Lecorpio** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="b43a2-151">In the Azure portal, on the **Lecorpio** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="b43a2-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="b43a2-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_samlbase.png)

3. <span data-ttu-id="b43a2-155">Op de **Lecorpio domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="b43a2-155">On the **Lecorpio Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_url.png)

    <span data-ttu-id="b43a2-157">a.</span><span class="sxs-lookup"><span data-stu-id="b43a2-157">a.</span></span> <span data-ttu-id="b43a2-158">In de **aanmeldings-URL** textbox, typ de waarde met het volgende patroon volgen:`https://<instance name>.lecorpio.com/<customer name>`</span><span class="sxs-lookup"><span data-stu-id="b43a2-158">In the **Sign-on URL** textbox, type the value using the following pattern: `https://<instance name>.lecorpio.com/<customer name>`</span></span>

    <span data-ttu-id="b43a2-159">b.</span><span class="sxs-lookup"><span data-stu-id="b43a2-159">b.</span></span> <span data-ttu-id="b43a2-160">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<instance name>.lecorpio.com/<customer name>`</span><span class="sxs-lookup"><span data-stu-id="b43a2-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<instance name>.lecorpio.com/<customer name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b43a2-161">Deze waarden zijn niet de werkelijke.</span><span class="sxs-lookup"><span data-stu-id="b43a2-161">These values are not the real.</span></span> <span data-ttu-id="b43a2-162">Deze waarden bijwerken met de werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="b43a2-162">Update these values with the actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="b43a2-163">Hier raden we u voor het gebruik van de unieke waarde van een tekenreeks in de id.</span><span class="sxs-lookup"><span data-stu-id="b43a2-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="b43a2-164">Neem contact op met [Lecorpio Client ondersteuningsteam](mailto:info@lecorpio.com) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="b43a2-164">Contact [Lecorpio Client support team](mailto:info@lecorpio.com) to get these values.</span></span> 
 
4. <span data-ttu-id="b43a2-165">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="b43a2-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_certificate.png) 

5. <span data-ttu-id="b43a2-167">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="b43a2-167">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lecorpio-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b43a2-169">Eenmalige aanmelding configureren op **Lecorpio** zijde, moet u de gedownloade verzenden **Metadata XML** naar [Lecorpio ondersteuningsteam](mailto:info@lecorpio.com).</span><span class="sxs-lookup"><span data-stu-id="b43a2-169">To configure single sign-on on **Lecorpio** side, you need to send the downloaded **Metadata XML** to [Lecorpio support team](mailto:info@lecorpio.com).</span></span>

> [!TIP]
> <span data-ttu-id="b43a2-170">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="b43a2-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b43a2-171">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="b43a2-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b43a2-172">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b43a2-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b43a2-173">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="b43a2-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="b43a2-174">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="b43a2-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="b43a2-176">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b43a2-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b43a2-177">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="b43a2-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lecorpio-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b43a2-179">Ga naar **gebruikers en groepen** en klik op **alle gebruikers** om de lijst met gebruikers weer te geven.</span><span class="sxs-lookup"><span data-stu-id="b43a2-179">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lecorpio-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b43a2-181">Aan de bovenkant van het dialoogvenster, klikt u op **toevoegen** openen de **gebruiker** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b43a2-181">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lecorpio-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b43a2-183">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="b43a2-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lecorpio-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b43a2-185">a.</span><span class="sxs-lookup"><span data-stu-id="b43a2-185">a.</span></span> <span data-ttu-id="b43a2-186">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b43a2-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b43a2-187">b.</span><span class="sxs-lookup"><span data-stu-id="b43a2-187">b.</span></span> <span data-ttu-id="b43a2-188">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b43a2-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b43a2-189">c.</span><span class="sxs-lookup"><span data-stu-id="b43a2-189">c.</span></span> <span data-ttu-id="b43a2-190">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="b43a2-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b43a2-191">d.</span><span class="sxs-lookup"><span data-stu-id="b43a2-191">d.</span></span> <span data-ttu-id="b43a2-192">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="b43a2-192">Click **Create**.</span></span>
 
### <a name="creating-a-lecorpio-test-user"></a><span data-ttu-id="b43a2-193">Een testgebruiker Lecorpio maken</span><span class="sxs-lookup"><span data-stu-id="b43a2-193">Creating a Lecorpio test user</span></span>

<span data-ttu-id="b43a2-194">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in Lecorpio maken.</span><span class="sxs-lookup"><span data-stu-id="b43a2-194">In this section, you create a user called Britta Simon in Lecorpio.</span></span> 

<span data-ttu-id="b43a2-195">Neem contact op met [Lecorpio Client ondersteuningsteam](mailto:info@lecorpio.com) de gebruikers in de toepassing Lecorpio toevoegen.</span><span class="sxs-lookup"><span data-stu-id="b43a2-195">Contact [Lecorpio Client support team](mailto:info@lecorpio.com) to add the users in the Lecorpio application.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b43a2-196">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="b43a2-196">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b43a2-197">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Lecorpio.</span><span class="sxs-lookup"><span data-stu-id="b43a2-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Lecorpio.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="b43a2-199">**Britta Simon om aan te wijzen Lecorpio, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b43a2-199">**To assign Britta Simon to Lecorpio, perform the following steps:**</span></span>

1. <span data-ttu-id="b43a2-200">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b43a2-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="b43a2-202">Selecteer in de lijst met toepassingen **Lecorpio**.</span><span class="sxs-lookup"><span data-stu-id="b43a2-202">In the applications list, select **Lecorpio**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_app.png) 

3. <span data-ttu-id="b43a2-204">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="b43a2-204">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="b43a2-206">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="b43a2-206">Click **Add** button.</span></span> <span data-ttu-id="b43a2-207">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b43a2-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="b43a2-209">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="b43a2-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b43a2-210">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b43a2-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b43a2-211">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b43a2-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b43a2-212">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b43a2-212">Testing single sign-on</span></span>

<span data-ttu-id="b43a2-213">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="b43a2-213">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b43a2-214">Als u op de tegel Lecorpio in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Lecorpio.</span><span class="sxs-lookup"><span data-stu-id="b43a2-214">When you click the Lecorpio tile in the Access Panel, you should get automatically signed-on to your Lecorpio application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b43a2-215">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="b43a2-215">Additional resources</span></span>

* [<span data-ttu-id="b43a2-216">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b43a2-216">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b43a2-217">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b43a2-217">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_203.png

