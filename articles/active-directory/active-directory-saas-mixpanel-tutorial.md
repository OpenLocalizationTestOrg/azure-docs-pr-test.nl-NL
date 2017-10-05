---
title: 'Zelfstudie: Azure Active Directory-integratie met Mixpanel | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Mixpanel.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a2df26ef-d441-44ac-a9f3-b37bf9709bcb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 3dd11b3477de1329c1c8e45a6dbf212b1635fd95
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mixpanel"></a><span data-ttu-id="ec779-103">Zelfstudie: Azure Active Directory-integratie met Mixpanel</span><span class="sxs-lookup"><span data-stu-id="ec779-103">Tutorial: Azure Active Directory integration with Mixpanel</span></span>

<span data-ttu-id="ec779-104">In deze zelfstudie leert u hoe Mixpanel integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ec779-104">In this tutorial, you learn how to integrate Mixpanel with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ec779-105">Mixpanel integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="ec779-105">Integrating Mixpanel with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ec779-106">U kunt beheren in Azure AD die toegang tot Mixpanel heeft</span><span class="sxs-lookup"><span data-stu-id="ec779-106">You can control in Azure AD who has access to Mixpanel</span></span>
- <span data-ttu-id="ec779-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Mixpanel (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="ec779-107">You can enable your users to automatically get signed-on to Mixpanel (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ec779-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="ec779-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ec779-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ec779-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ec779-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ec779-110">Prerequisites</span></span>

<span data-ttu-id="ec779-111">Voor het configureren van Azure AD-integratie met Mixpanel, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="ec779-111">To configure Azure AD integration with Mixpanel, you need the following items:</span></span>

- <span data-ttu-id="ec779-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="ec779-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ec779-113">Een Mixpanel eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="ec779-113">A Mixpanel single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ec779-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="ec779-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ec779-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="ec779-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ec779-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="ec779-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ec779-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ec779-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ec779-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="ec779-118">Scenario description</span></span>
<span data-ttu-id="ec779-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="ec779-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ec779-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="ec779-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ec779-121">Mixpanel uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="ec779-121">Adding Mixpanel from the gallery</span></span>
2. <span data-ttu-id="ec779-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ec779-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mixpanel-from-the-gallery"></a><span data-ttu-id="ec779-123">Mixpanel uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="ec779-123">Adding Mixpanel from the gallery</span></span>
<span data-ttu-id="ec779-124">Voor het configureren van de integratie van Mixpanel in Azure AD, moet u Mixpanel uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="ec779-124">To configure the integration of Mixpanel into Azure AD, you need to add Mixpanel from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ec779-125">**Als u wilt toevoegen Mixpanel uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="ec779-125">**To add Mixpanel from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ec779-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="ec779-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ec779-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ec779-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ec779-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ec779-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="ec779-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ec779-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="ec779-133">Typ in het zoekvak **Mixpanel**.</span><span class="sxs-lookup"><span data-stu-id="ec779-133">In the search box, type **Mixpanel**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_search.png)

5. <span data-ttu-id="ec779-135">Selecteer in het deelvenster resultaten **Mixpanel**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="ec779-135">In the results panel, select **Mixpanel**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ec779-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ec779-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ec779-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Mixpanel op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="ec779-138">In this section, you configure and test Azure AD single sign-on with Mixpanel based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ec779-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Mixpanel is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ec779-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Mixpanel is to a user in Azure AD.</span></span> <span data-ttu-id="ec779-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Mixpanel tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="ec779-140">In other words, a link relationship between an Azure AD user and the related user in Mixpanel needs to be established.</span></span>

<span data-ttu-id="ec779-141">Wijs in Mixpanel, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="ec779-141">In Mixpanel, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ec779-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Mixpanel, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="ec779-142">To configure and test Azure AD single sign-on with Mixpanel, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ec779-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ec779-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ec779-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ec779-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ec779-145">**[Maken van een testgebruiker Mixpanel](#creating-a-mixpanel-test-user)**  - Mixpanel die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="ec779-145">**[Creating a Mixpanel test user](#creating-a-mixpanel-test-user)** - to have a counterpart of Britta Simon in Mixpanel that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ec779-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="ec779-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ec779-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="ec779-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ec779-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="ec779-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ec779-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Mixpanel configureren.</span><span class="sxs-lookup"><span data-stu-id="ec779-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Mixpanel application.</span></span>

<span data-ttu-id="ec779-150">**Voor het configureren van Azure AD eenmalige aanmelding met Mixpanel, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="ec779-150">**To configure Azure AD single sign-on with Mixpanel, perform the following steps:**</span></span>

1. <span data-ttu-id="ec779-151">In de Azure-portal op de **Mixpanel** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="ec779-151">In the Azure portal, on the **Mixpanel** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="ec779-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="ec779-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_samlbase.png)

3. <span data-ttu-id="ec779-155">Op de **Mixpanel domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="ec779-155">On the **Mixpanel Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_url.png)

     <span data-ttu-id="ec779-157">In de **aanmeldings-URL** textbox, typ een URL als:`https://mixpanel.com/login/`</span><span class="sxs-lookup"><span data-stu-id="ec779-157">In the **Sign-on URL** textbox, type a URL as: `https://mixpanel.com/login/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ec779-158">Registreer op [https://mixpanel.com/register/](https://mixpanel.com/register/) voor het instellen van de aanmeldingsgegevens en neem contact op met de [Mixpanel ondersteuningsteam](mailto:support@mixpanel.com) SSO-instellingen voor uw tenant inschakelen.</span><span class="sxs-lookup"><span data-stu-id="ec779-158">Please register at [https://mixpanel.com/register/](https://mixpanel.com/register/) to set up your login credentials and  contact the [Mixpanel support team](mailto:support@mixpanel.com) to enable SSO settings for your tenant.</span></span> <span data-ttu-id="ec779-159">Ook kunt u uw aanmelding op URL-waarde indien nodig ophalen uit het ondersteuningsteam Mixpanel.</span><span class="sxs-lookup"><span data-stu-id="ec779-159">You can also get your Sign On URL value if necessary from your Mixpanel support team.</span></span> 
 
4. <span data-ttu-id="ec779-160">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="ec779-160">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_certificate.png) 

5. <span data-ttu-id="ec779-162">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="ec779-162">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mixpanel-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ec779-164">Op de **Mixpanel configuratie** sectie, klikt u op **configureren Mixpanel** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="ec779-164">On the **Mixpanel Configuration** section, click **Configure Mixpanel** to open **Configure sign-on** window.</span></span> <span data-ttu-id="ec779-165">Kopieer de **SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="ec779-165">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_configure.png) 

7. <span data-ttu-id="ec779-167">In een ander browservenster eenmalige aanmelding voor uw toepassing Mixpanel als beheerder.</span><span class="sxs-lookup"><span data-stu-id="ec779-167">In a different browser window, sign-on to your Mixpanel application as an administrator.</span></span>

8. <span data-ttu-id="ec779-168">Aan de onderkant van de pagina, klikt u op het kleine **stemmen** pictogram in de linkerhoek.</span><span class="sxs-lookup"><span data-stu-id="ec779-168">On bottom of the page, click the little **gear** icon in the left corner.</span></span> 
   
    ![Mixpanel voor eenmalige aanmelding](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_06.png) 

9. <span data-ttu-id="ec779-170">Klik op de **toegangsbeveiliging** tabblad en klik vervolgens op **instellingen wijzigen**.</span><span class="sxs-lookup"><span data-stu-id="ec779-170">Click the **Access security** tab, and then click **Change settings**.</span></span>
   
    ![Mixpanel instellingen](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_08.png) 

10. <span data-ttu-id="ec779-172">Op de **wijzigen van uw certificaat** dialoogvenster pagina, klikt u op **bestand kiezen** uw gedownloade certificaat uploaden en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="ec779-172">On the **Change your certificate** dialog page, click **Choose file** to upload your downloaded certificate, and then click **NEXT**.</span></span>
   
    ![Mixpanel instellingen](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_09.png) 

11.  <span data-ttu-id="ec779-174">In het tekstvak voor de URL van verificatie op de **wijzigen van de URL voor webverificatie** dialoogvenster pagina, plak de waarde van **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="ec779-174">In the authentication URL textbox on the **Change your authentication  URL** dialog page, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal, and then click **NEXT**.</span></span>
   
   ![Mixpanel instellingen](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_10.png) 

12. <span data-ttu-id="ec779-176">Klik op **Gereed**.</span><span class="sxs-lookup"><span data-stu-id="ec779-176">Click **Done**.</span></span>

> [!TIP]
> <span data-ttu-id="ec779-177">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="ec779-177">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ec779-178">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="ec779-178">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ec779-179">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ec779-179">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ec779-180">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="ec779-180">Creating an Azure AD test user</span></span>
<span data-ttu-id="ec779-181">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="ec779-181">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="ec779-183">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="ec779-183">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ec779-184">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="ec779-184">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mixpanel-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ec779-186">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="ec779-186">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mixpanel-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ec779-188">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ec779-188">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mixpanel-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ec779-190">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="ec779-190">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mixpanel-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ec779-192">a.</span><span class="sxs-lookup"><span data-stu-id="ec779-192">a.</span></span> <span data-ttu-id="ec779-193">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ec779-193">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ec779-194">b.</span><span class="sxs-lookup"><span data-stu-id="ec779-194">b.</span></span> <span data-ttu-id="ec779-195">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ec779-195">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ec779-196">c.</span><span class="sxs-lookup"><span data-stu-id="ec779-196">c.</span></span> <span data-ttu-id="ec779-197">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="ec779-197">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ec779-198">d.</span><span class="sxs-lookup"><span data-stu-id="ec779-198">d.</span></span> <span data-ttu-id="ec779-199">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="ec779-199">Click **Create**.</span></span>
 
### <a name="creating-a-mixpanel-test-user"></a><span data-ttu-id="ec779-200">Een testgebruiker Mixpanel maken</span><span class="sxs-lookup"><span data-stu-id="ec779-200">Creating a Mixpanel test user</span></span>

<span data-ttu-id="ec779-201">Het doel van deze sectie is het maken van een gebruiker Britta Simon in Mixpanel genoemd.</span><span class="sxs-lookup"><span data-stu-id="ec779-201">The objective of this section is to create a user called Britta Simon in Mixpanel.</span></span> 

1. <span data-ttu-id="ec779-202">Meld u op met uw bedrijf Mixpanel site als een beheerder.</span><span class="sxs-lookup"><span data-stu-id="ec779-202">Sign on to your Mixpanel company site as an administrator.</span></span>

2. <span data-ttu-id="ec779-203">Aan de onderkant van de pagina, klikt u weinig tandwielpictogram in de linkerhoek openen de **instellingen** venster.</span><span class="sxs-lookup"><span data-stu-id="ec779-203">On the bottom of the page, click the little gear button on the left corner to open the **Settings** window.</span></span>

3. <span data-ttu-id="ec779-204">Klik op de **Team** tabblad.</span><span class="sxs-lookup"><span data-stu-id="ec779-204">Click the **Team** tab.</span></span>

4. <span data-ttu-id="ec779-205">In de **teamlid** textbox Britta van e-mailadres typt in Azure.</span><span class="sxs-lookup"><span data-stu-id="ec779-205">In the **team member** textbox, type Britta's email address in the Azure.</span></span>
   
    ![Mixpanel instellingen](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_11.png) 

5. <span data-ttu-id="ec779-207">Klik op **uitnodigen**.</span><span class="sxs-lookup"><span data-stu-id="ec779-207">Click **Invite**.</span></span> 

> [!Note]
> <span data-ttu-id="ec779-208">De gebruiker ontvangt een e-mailbericht voor het instellen van het profiel.</span><span class="sxs-lookup"><span data-stu-id="ec779-208">The user will get an email to set up the profile.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ec779-209">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="ec779-209">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ec779-210">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Mixpanel.</span><span class="sxs-lookup"><span data-stu-id="ec779-210">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Mixpanel.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="ec779-212">**Britta Simon om aan te wijzen Mixpanel, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="ec779-212">**To assign Britta Simon to Mixpanel, perform the following steps:**</span></span>

1. <span data-ttu-id="ec779-213">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ec779-213">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="ec779-215">Selecteer in de lijst met toepassingen **Mixpanel**.</span><span class="sxs-lookup"><span data-stu-id="ec779-215">In the applications list, select **Mixpanel**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_app.png) 

3. <span data-ttu-id="ec779-217">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="ec779-217">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="ec779-219">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="ec779-219">Click **Add** button.</span></span> <span data-ttu-id="ec779-220">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ec779-220">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="ec779-222">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="ec779-222">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ec779-223">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ec779-223">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ec779-224">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ec779-224">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ec779-225">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ec779-225">Testing single sign-on</span></span>

<span data-ttu-id="ec779-226">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="ec779-226">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ec779-227">Als u op de tegel Mixpanel in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Mixpanel.</span><span class="sxs-lookup"><span data-stu-id="ec779-227">When you click the Mixpanel tile in the Access Panel, you should get automatically signed-on to your Mixpanel application.</span></span>
<span data-ttu-id="ec779-228">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ec779-228">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ec779-229">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="ec779-229">Additional resources</span></span>

* [<span data-ttu-id="ec779-230">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ec779-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ec779-231">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ec779-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_203.png

