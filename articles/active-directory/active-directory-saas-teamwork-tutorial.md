---
title: 'Zelfstudie: Azure Active Directory-integratie met werken als een team | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en werken als een team.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 03760032-3d76-4b47-ab84-241f72fbd561
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: jeedes
ms.openlocfilehash: edd2f9446515531f1147a8abf99295b618b89b25
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamwork"></a><span data-ttu-id="a1e57-103">Zelfstudie: Azure Active Directory-integratie met werken als een team</span><span class="sxs-lookup"><span data-stu-id="a1e57-103">Tutorial: Azure Active Directory integration with Teamwork</span></span>

<span data-ttu-id="a1e57-104">In deze zelfstudie leert u hoe werken als een team integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a1e57-104">In this tutorial, you learn how to integrate Teamwork with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a1e57-105">Werken als een team integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="a1e57-105">Integrating Teamwork with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a1e57-106">U kunt beheren in Azure AD die toegang tot werken als een team heeft</span><span class="sxs-lookup"><span data-stu-id="a1e57-106">You can control in Azure AD who has access to Teamwork</span></span>
- <span data-ttu-id="a1e57-107">U kunt uw gebruikers automatisch ophalen aangemeld bij werken als een team (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="a1e57-107">You can enable your users to automatically get signed-on to Teamwork (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a1e57-108">U kunt uw accounts op één centrale locatie - en de Azure Management portal beheren</span><span class="sxs-lookup"><span data-stu-id="a1e57-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="a1e57-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a1e57-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a1e57-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a1e57-110">Prerequisites</span></span>

<span data-ttu-id="a1e57-111">Om Azure AD-integratie met werken als een team configureert, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="a1e57-111">To configure Azure AD integration with Teamwork, you need the following items:</span></span>

- <span data-ttu-id="a1e57-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="a1e57-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a1e57-113">Een werken als een team eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="a1e57-113">A Teamwork single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="a1e57-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="a1e57-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="a1e57-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="a1e57-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a1e57-116">U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="a1e57-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="a1e57-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a1e57-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="a1e57-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="a1e57-118">Scenario description</span></span>
<span data-ttu-id="a1e57-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="a1e57-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a1e57-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="a1e57-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a1e57-121">Werken als een team uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="a1e57-121">Adding Teamwork from the gallery</span></span>
2. <span data-ttu-id="a1e57-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="a1e57-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-teamwork-from-the-gallery"></a><span data-ttu-id="a1e57-123">Werken als een team uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="a1e57-123">Adding Teamwork from the gallery</span></span>
<span data-ttu-id="a1e57-124">Voor het configureren van de integratie van werken als een team in Azure AD, moet u werken als een team uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="a1e57-124">To configure the integration of Teamwork into Azure AD, you need to add Teamwork from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a1e57-125">**Als u wilt werken als een team uit de galerie toevoegen, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="a1e57-125">**To add Teamwork from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a1e57-126">In de  **[Azure Management Portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="a1e57-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a1e57-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a1e57-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a1e57-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a1e57-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="a1e57-131">Klik op **toevoegen** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a1e57-131">Click **Add** button on the top of the dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="a1e57-133">Typ in het zoekvak **werken als een team**.</span><span class="sxs-lookup"><span data-stu-id="a1e57-133">In the search box, type **Teamwork**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_001.png)

5. <span data-ttu-id="a1e57-135">Selecteer in het deelvenster resultaten **werken als een team**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="a1e57-135">In the results panel, select **Teamwork**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a1e57-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="a1e57-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a1e57-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met werken als een team op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="a1e57-138">In this section, you configure and test Azure AD single sign-on with Teamwork based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a1e57-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in werken als een team is aan een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a1e57-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Teamwork is to a user in Azure AD.</span></span> <span data-ttu-id="a1e57-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in werken als een team tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="a1e57-140">In other words, a link relationship between an Azure AD user and the related user in Teamwork needs to be established.</span></span>

<span data-ttu-id="a1e57-141">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in werken als een team.</span><span class="sxs-lookup"><span data-stu-id="a1e57-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Teamwork.</span></span>

<span data-ttu-id="a1e57-142">Om te configureren en testen van Azure AD eenmalige aanmelding met werken als een team, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="a1e57-142">To configure and test Azure AD single sign-on with Teamwork, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a1e57-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a1e57-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a1e57-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a1e57-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a1e57-145">**[Maken van een testgebruiker werken als een team](#creating-a-teamwork-test-user)**  - werken als een team dat is gekoppeld aan de Azure AD-representatie van haar van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="a1e57-145">**[Creating a Teamwork test user](#creating-a-teamwork-test-user)** - to have a counterpart of Britta Simon in Teamwork that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="a1e57-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="a1e57-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a1e57-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="a1e57-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a1e57-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="a1e57-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a1e57-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure-beheerportal en eenmalige aanmelding configureren in uw toepassing werken als een team.</span><span class="sxs-lookup"><span data-stu-id="a1e57-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Teamwork application.</span></span>

<span data-ttu-id="a1e57-150">**Om eenmalige aanmelding Azure AD met werken als een team configureert, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="a1e57-150">**To configure Azure AD single sign-on with Teamwork, perform the following steps:**</span></span>

1. <span data-ttu-id="a1e57-151">In de Azure-beheerportal op de **werken als een team** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="a1e57-151">In the Azure Management portal, on the **Teamwork** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="a1e57-153">Op de **eenmalige aanmelding** dialoogvenster als **modus** Selecteer **op basis van SAML aanmelding** eenmalige aanmelding inschakelen op.</span><span class="sxs-lookup"><span data-stu-id="a1e57-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_01.png)

3. <span data-ttu-id="a1e57-155">Op de **werken als een team domein en de URL's** sectie in het **aanmelding op URL** textbox, typ een URL met het volgende patroon volgen:`https://<company name>.teamwork.com`</span><span class="sxs-lookup"><span data-stu-id="a1e57-155">On the **Teamwork Domain and URLs** section, in the **Sign On URL** textbox, type a URL using the following pattern: `https://<company name>.teamwork.com`</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_02.png)

    > [!NOTE] 
    > <span data-ttu-id="a1e57-157">Houd er rekening mee dat dit geen de feitelijke waarde is.</span><span class="sxs-lookup"><span data-stu-id="a1e57-157">Please note that this is not the real value.</span></span> <span data-ttu-id="a1e57-158">U moet deze waarde met de werkelijke aanmelding op de URL bijwerken.</span><span class="sxs-lookup"><span data-stu-id="a1e57-158">You have to update this value with the actual Sign On URL.</span></span> <span data-ttu-id="a1e57-159">Neem contact op met [werken als een team ondersteuningsteam](mailto:support@teamwork.com) deze waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="a1e57-159">Contact [Teamwork support team](mailto:support@teamwork.com) to get this value.</span></span> 

4. <span data-ttu-id="a1e57-160">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **nieuw certificaat maken**.</span><span class="sxs-lookup"><span data-stu-id="a1e57-160">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_03.png)   

5. <span data-ttu-id="a1e57-162">Op de **nieuw certificaat maken** dialoogvenster, klikt u op het pictogram van de kalender en selecteer een **vervaldatum**.</span><span class="sxs-lookup"><span data-stu-id="a1e57-162">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="a1e57-163">Klik vervolgens op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="a1e57-163">Then click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamwork-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="a1e57-165">Op de **SAML-certificaat voor ondertekening van** sectie **nieuwe certificaat activeren** en klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="a1e57-165">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_04.png)

7. <span data-ttu-id="a1e57-167">In het pop-upvenster **rollovercertificaat** venster, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="a1e57-167">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamwork-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="a1e57-169">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="a1e57-169">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_05.png) 

9. <span data-ttu-id="a1e57-171">Als u eenmalige aanmelding die zijn geconfigureerd voor uw toepassing, neem contact op met [werken als een team ondersteuningsteam](mailto:support@teamwork.com) en geeft u de gedownloade **metagegevens**.</span><span class="sxs-lookup"><span data-stu-id="a1e57-171">To get SSO configured for your application, contact [Teamwork support team](mailto:support@teamwork.com) and provide them with the downloaded **metadata**.</span></span>
  

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a1e57-172">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="a1e57-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="a1e57-173">Het doel van deze sectie is het een testgebruiker maken in Azure Management portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="a1e57-173">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="a1e57-175">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="a1e57-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a1e57-176">In de **Azure Management portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="a1e57-176">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-teamwork-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a1e57-178">Ga naar **gebruikers en groepen** en klik op **alle gebruikers** om de lijst met gebruikers weer te geven.</span><span class="sxs-lookup"><span data-stu-id="a1e57-178">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-teamwork-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a1e57-180">Klik aan de bovenkant van het dialoogvenster **toevoegen** openen de **gebruiker** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a1e57-180">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-teamwork-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a1e57-182">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="a1e57-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-teamwork-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a1e57-184">a.</span><span class="sxs-lookup"><span data-stu-id="a1e57-184">a.</span></span> <span data-ttu-id="a1e57-185">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a1e57-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a1e57-186">b.</span><span class="sxs-lookup"><span data-stu-id="a1e57-186">b.</span></span> <span data-ttu-id="a1e57-187">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a1e57-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a1e57-188">c.</span><span class="sxs-lookup"><span data-stu-id="a1e57-188">c.</span></span> <span data-ttu-id="a1e57-189">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="a1e57-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a1e57-190">d.</span><span class="sxs-lookup"><span data-stu-id="a1e57-190">d.</span></span> <span data-ttu-id="a1e57-191">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="a1e57-191">Click **Create**.</span></span> 



### <a name="creating-a-teamwork-test-user"></a><span data-ttu-id="a1e57-192">Een testgebruiker werken als een team maken</span><span class="sxs-lookup"><span data-stu-id="a1e57-192">Creating a Teamwork test user</span></span>

<span data-ttu-id="a1e57-193">In deze sectie maakt maken u een gebruiker Britta Simon aangeroepen in werken als een team.</span><span class="sxs-lookup"><span data-stu-id="a1e57-193">In this section, you create a user called Britta Simon in Teamwork.</span></span> <span data-ttu-id="a1e57-194">Neem contact op met [werken als een team ondersteuningsteam](mailto:support@teamwork.com) om toe te voegen de gebruikers van het platform werken als een team.</span><span class="sxs-lookup"><span data-stu-id="a1e57-194">Please work with [Teamwork support team](mailto:support@teamwork.com) to add the users in the Teamwork platform.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a1e57-195">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="a1e57-195">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a1e57-196">In deze sectie schakelt u Britta Simon Azure eenmalige aanmelding gebruiken door haar toegang te verlenen om te werken als een team.</span><span class="sxs-lookup"><span data-stu-id="a1e57-196">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Teamwork.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="a1e57-198">**Britta Simon om aan te wijzen werken als een team, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="a1e57-198">**To assign Britta Simon to Teamwork, perform the following steps:**</span></span>

1. <span data-ttu-id="a1e57-199">In de Azure-beheerportal, opent u de weergave toepassingen en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a1e57-199">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="a1e57-201">Selecteer in de lijst met toepassingen **werken als een team**.</span><span class="sxs-lookup"><span data-stu-id="a1e57-201">In the applications list, select **Teamwork**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_50.png) 

3. <span data-ttu-id="a1e57-203">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="a1e57-203">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="a1e57-205">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="a1e57-205">Click **Add** button.</span></span> <span data-ttu-id="a1e57-206">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a1e57-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="a1e57-208">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="a1e57-208">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a1e57-209">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a1e57-209">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a1e57-210">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a1e57-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="a1e57-211">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="a1e57-211">Testing single sign-on</span></span>

<span data-ttu-id="a1e57-212">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="a1e57-212">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a1e57-213">Als u op de tegel werken als een team in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing werken als een team.</span><span class="sxs-lookup"><span data-stu-id="a1e57-213">When you click the Teamwork tile in the Access Panel, you should get automatically signed-on to your Teamwork application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="a1e57-214">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="a1e57-214">Additional resources</span></span>

* [<span data-ttu-id="a1e57-215">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a1e57-215">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a1e57-216">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a1e57-216">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_203.png