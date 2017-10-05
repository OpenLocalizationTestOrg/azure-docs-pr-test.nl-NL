---
title: 'Zelfstudie: Azure Active Directory-integratie met Novatus | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Novatus.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2f13779-bdb7-4408-9738-be67ed3de4e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/02/2017
ms.author: jeedes
ms.openlocfilehash: ec67e96309a8877e6fb65b30da1501e4f34a9ee4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-novatus"></a><span data-ttu-id="fa891-103">Zelfstudie: Azure Active Directory-integratie met Novatus</span><span class="sxs-lookup"><span data-stu-id="fa891-103">Tutorial: Azure Active Directory integration with Novatus</span></span>

<span data-ttu-id="fa891-104">In deze zelfstudie leert u hoe Novatus integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fa891-104">In this tutorial, you learn how to integrate Novatus with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fa891-105">Novatus integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="fa891-105">Integrating Novatus with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="fa891-106">U kunt beheren in Azure AD die toegang tot Novatus heeft</span><span class="sxs-lookup"><span data-stu-id="fa891-106">You can control in Azure AD who has access to Novatus</span></span>
- <span data-ttu-id="fa891-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Novatus (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="fa891-107">You can enable your users to automatically get signed-on to Novatus (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fa891-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="fa891-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="fa891-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fa891-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fa891-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="fa891-110">Prerequisites</span></span>

<span data-ttu-id="fa891-111">Voor het configureren van Azure AD-integratie met Novatus, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="fa891-111">To configure Azure AD integration with Novatus, you need the following items:</span></span>

- <span data-ttu-id="fa891-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="fa891-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fa891-113">Een Novatus eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="fa891-113">A Novatus single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fa891-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="fa891-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fa891-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="fa891-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fa891-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="fa891-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fa891-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fa891-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fa891-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="fa891-118">Scenario description</span></span>
<span data-ttu-id="fa891-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="fa891-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fa891-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="fa891-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fa891-121">Novatus uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="fa891-121">Adding Novatus from the gallery</span></span>
2. <span data-ttu-id="fa891-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="fa891-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-novatus-from-the-gallery"></a><span data-ttu-id="fa891-123">Novatus uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="fa891-123">Adding Novatus from the gallery</span></span>
<span data-ttu-id="fa891-124">Voor het configureren van de integratie van Novatus in Azure AD, moet u Novatus uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="fa891-124">To configure the integration of Novatus into Azure AD, you need to add Novatus from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="fa891-125">**Als u wilt toevoegen Novatus uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="fa891-125">**To add Novatus from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="fa891-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="fa891-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="fa891-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="fa891-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="fa891-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="fa891-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="fa891-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="fa891-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="fa891-133">Typ in het zoekvak **Novatus**.</span><span class="sxs-lookup"><span data-stu-id="fa891-133">In the search box, type **Novatus**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_search.png)

5. <span data-ttu-id="fa891-135">Selecteer in het deelvenster resultaten **Novatus**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="fa891-135">In the results panel, select **Novatus**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="fa891-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="fa891-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="fa891-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Novatus op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="fa891-138">In this section, you configure and test Azure AD single sign-on with Novatus based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="fa891-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Novatus is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fa891-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Novatus is to a user in Azure AD.</span></span> <span data-ttu-id="fa891-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Novatus tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="fa891-140">In other words, a link relationship between an Azure AD user and the related user in Novatus needs to be established.</span></span>

<span data-ttu-id="fa891-141">Wijs in Novatus, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="fa891-141">In Novatus, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="fa891-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Novatus, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="fa891-142">To configure and test Azure AD single sign-on with Novatus, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="fa891-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="fa891-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="fa891-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fa891-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fa891-145">**[Maken van een testgebruiker Novatus](#creating-a-novatus-test-user)**  - Novatus die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="fa891-145">**[Creating a Novatus test user](#creating-a-novatus-test-user)** - to have a counterpart of Britta Simon in Novatus that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="fa891-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="fa891-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fa891-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="fa891-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="fa891-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="fa891-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="fa891-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Novatus configureren.</span><span class="sxs-lookup"><span data-stu-id="fa891-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Novatus application.</span></span>

<span data-ttu-id="fa891-150">**Voor het configureren van Azure AD eenmalige aanmelding met Novatus, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="fa891-150">**To configure Azure AD single sign-on with Novatus, perform the following steps:**</span></span>

1. <span data-ttu-id="fa891-151">In de Azure-portal op de **Novatus** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="fa891-151">In the Azure portal, on the **Novatus** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="fa891-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="fa891-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_samlbase.png)

3. <span data-ttu-id="fa891-155">Op de **Novatus domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="fa891-155">On the **Novatus Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_url.png)

     <span data-ttu-id="fa891-157">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://sso.novatuscontracts.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="fa891-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://sso.novatuscontracts.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="fa891-158">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="fa891-158">This value is not real.</span></span> <span data-ttu-id="fa891-159">Deze waarde bijwerken met de werkelijke URL voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="fa891-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="fa891-160">Neem contact op met [Novatus Client ondersteuningsteam](mailto:jvinci@novatusinc.com) deze waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="fa891-160">Contact [Novatus Client support team](mailto:jvinci@novatusinc.com) to get this value.</span></span> 
 


4. <span data-ttu-id="fa891-161">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="fa891-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_certificate.png) 

5. <span data-ttu-id="fa891-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="fa891-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-novatus-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="fa891-165">Op de **Novatus configuratie** sectie, klikt u op **configureren Novatus** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="fa891-165">On the **Novatus Configuration** section, click **Configure Novatus** to open **Configure sign-on** window.</span></span> <span data-ttu-id="fa891-166">Kopieer de **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="fa891-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_configure.png) 

7. <span data-ttu-id="fa891-168">Als u eenmalige aanmelding die zijn geconfigureerd voor uw toepassing, neem contact op met uw [Novatus ondersteuningsteam](mailto:jvinci@novatusinc.com).</span><span class="sxs-lookup"><span data-stu-id="fa891-168">To get SSO configured for your application, contact your [Novatus support team](mailto:jvinci@novatusinc.com).</span></span> <span data-ttu-id="fa891-169">Koppel de **certificaat gedownload** bestand voor uw e-mail en -share de **metagegevens-URL's** (**Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL**) met Novatus team voor het instellen van eenmalige aanmelding op hun kant.</span><span class="sxs-lookup"><span data-stu-id="fa891-169">Attach the **downloaded certificate** file to your mail and share the **metadata urls** (**Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL**) with Novatus team to set up SSO on their side.</span></span>

> [!TIP]
> <span data-ttu-id="fa891-170">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="fa891-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="fa891-171">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="fa891-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="fa891-172">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fa891-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="fa891-173">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="fa891-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="fa891-174">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="fa891-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="fa891-176">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="fa891-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="fa891-177">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="fa891-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-novatus-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="fa891-179">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="fa891-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-novatus-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fa891-181">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="fa891-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-novatus-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fa891-183">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="fa891-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-novatus-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fa891-185">a.</span><span class="sxs-lookup"><span data-stu-id="fa891-185">a.</span></span> <span data-ttu-id="fa891-186">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fa891-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fa891-187">b.</span><span class="sxs-lookup"><span data-stu-id="fa891-187">b.</span></span> <span data-ttu-id="fa891-188">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="fa891-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="fa891-189">c.</span><span class="sxs-lookup"><span data-stu-id="fa891-189">c.</span></span> <span data-ttu-id="fa891-190">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="fa891-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="fa891-191">d.</span><span class="sxs-lookup"><span data-stu-id="fa891-191">d.</span></span> <span data-ttu-id="fa891-192">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="fa891-192">Click **Create**.</span></span>
 
### <a name="creating-a-novatus-test-user"></a><span data-ttu-id="fa891-193">Een testgebruiker Novatus maken</span><span class="sxs-lookup"><span data-stu-id="fa891-193">Creating a Novatus test user</span></span>

<span data-ttu-id="fa891-194">Het doel van deze sectie is het maken van een gebruiker Britta Simon in Novatus genoemd.</span><span class="sxs-lookup"><span data-stu-id="fa891-194">The objective of this section is to create a user called Britta Simon in Novatus.</span></span> <span data-ttu-id="fa891-195">Novatus ondersteunt just-in-time-inrichting, dit is standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="fa891-195">Novatus supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="fa891-196">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="fa891-196">There is no action item for you in this section.</span></span> <span data-ttu-id="fa891-197">Een nieuwe gebruiker wordt gemaakt tijdens een poging tot toegang tot Novatus als deze nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="fa891-197">A new user will be created during an attempt to access Novatus if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="fa891-198">Als u een gebruiker handmatig maken wilt, moet u contact op met de [Novatus ondersteuningsteam](mailto:jvinci@novatusinc.com).</span><span class="sxs-lookup"><span data-stu-id="fa891-198">If you need to create an user manually, you need to contact the [Novatus support team](mailto:jvinci@novatusinc.com).</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="fa891-199">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="fa891-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="fa891-200">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Novatus.</span><span class="sxs-lookup"><span data-stu-id="fa891-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Novatus.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="fa891-202">**Britta Simon om aan te wijzen Novatus, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="fa891-202">**To assign Britta Simon to Novatus, perform the following steps:**</span></span>

1. <span data-ttu-id="fa891-203">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="fa891-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="fa891-205">Selecteer in de lijst met toepassingen **Novatus**.</span><span class="sxs-lookup"><span data-stu-id="fa891-205">In the applications list, select **Novatus**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_app.png) 

3. <span data-ttu-id="fa891-207">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="fa891-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="fa891-209">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="fa891-209">Click **Add** button.</span></span> <span data-ttu-id="fa891-210">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="fa891-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="fa891-212">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="fa891-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="fa891-213">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="fa891-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fa891-214">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="fa891-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="fa891-215">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="fa891-215">Testing single sign-on</span></span>

<span data-ttu-id="fa891-216">Het doel van deze sectie is het testen van uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="fa891-216">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="fa891-217">Als u op de tegel Novatus in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Novatus.</span><span class="sxs-lookup"><span data-stu-id="fa891-217">When you click the Novatus tile in the Access Panel, you should get automatically signed-on to your Novatus application.</span></span> <span data-ttu-id="fa891-218">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="fa891-218">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fa891-219">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="fa891-219">Additional resources</span></span>

* [<span data-ttu-id="fa891-220">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fa891-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fa891-221">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="fa891-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_203.png

