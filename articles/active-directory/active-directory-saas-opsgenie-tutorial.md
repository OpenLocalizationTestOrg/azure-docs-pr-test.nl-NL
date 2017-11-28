---
title: 'Zelfstudie: Azure Active Directory-integratie met OpsGenie | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en OpsGenie.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 41b59b22-a61d-4fe6-ab0d-6c3991d1375f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: ce63726d2406d2f1415d29786f0ef92ca95b9b90
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-opsgenie"></a><span data-ttu-id="6b520-103">Zelfstudie: Azure Active Directory-integratie met OpsGenie</span><span class="sxs-lookup"><span data-stu-id="6b520-103">Tutorial: Azure Active Directory integration with OpsGenie</span></span>

<span data-ttu-id="6b520-104">In deze zelfstudie leert u hoe OpsGenie integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6b520-104">In this tutorial, you learn how to integrate OpsGenie with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6b520-105">OpsGenie integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="6b520-105">Integrating OpsGenie with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6b520-106">U kunt beheren in Azure AD die toegang tot OpsGenie heeft</span><span class="sxs-lookup"><span data-stu-id="6b520-106">You can control in Azure AD who has access to OpsGenie</span></span>
- <span data-ttu-id="6b520-107">U kunt uw gebruikers automatisch ophalen aangemeld bij OpsGenie (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="6b520-107">You can enable your users to automatically get signed-on to OpsGenie (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6b520-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="6b520-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="6b520-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6b520-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6b520-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="6b520-110">Prerequisites</span></span>

<span data-ttu-id="6b520-111">Voor het configureren van Azure AD-integratie met OpsGenie, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="6b520-111">To configure Azure AD integration with OpsGenie, you need the following items:</span></span>

- <span data-ttu-id="6b520-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="6b520-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6b520-113">Een OpsGenie eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="6b520-113">A OpsGenie single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6b520-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="6b520-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6b520-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="6b520-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6b520-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="6b520-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6b520-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6b520-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6b520-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="6b520-118">Scenario description</span></span>
<span data-ttu-id="6b520-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="6b520-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6b520-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="6b520-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6b520-121">OpsGenie uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="6b520-121">Adding OpsGenie from the gallery</span></span>
2. <span data-ttu-id="6b520-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="6b520-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-opsgenie-from-the-gallery"></a><span data-ttu-id="6b520-123">OpsGenie uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="6b520-123">Adding OpsGenie from the gallery</span></span>
<span data-ttu-id="6b520-124">Voor het configureren van de integratie van OpsGenie in Azure AD, moet u OpsGenie uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="6b520-124">To configure the integration of OpsGenie into Azure AD, you need to add OpsGenie from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6b520-125">**Als u wilt toevoegen OpsGenie uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="6b520-125">**To add OpsGenie from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6b520-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="6b520-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6b520-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="6b520-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6b520-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="6b520-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="6b520-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6b520-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="6b520-133">Typ in het zoekvak **OpsGenie**.</span><span class="sxs-lookup"><span data-stu-id="6b520-133">In the search box, type **OpsGenie**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_search.png)

5. <span data-ttu-id="6b520-135">Selecteer in het deelvenster resultaten **OpsGenie**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="6b520-135">In the results panel, select **OpsGenie**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6b520-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="6b520-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6b520-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met OpsGenie op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="6b520-138">In this section, you configure and test Azure AD single sign-on with OpsGenie based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6b520-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in OpsGenie is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6b520-139">For single sign-on to work, Azure AD needs to know what the counterpart user in OpsGenie is to a user in Azure AD.</span></span> <span data-ttu-id="6b520-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in OpsGenie tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="6b520-140">In other words, a link relationship between an Azure AD user and the related user in OpsGenie needs to be established.</span></span>

<span data-ttu-id="6b520-141">Wijs in OpsGenie, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="6b520-141">In OpsGenie, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="6b520-142">Om te configureren en testen van Azure AD eenmalige aanmelding met OpsGenie, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="6b520-142">To configure and test Azure AD single sign-on with OpsGenie, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6b520-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6b520-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6b520-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6b520-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6b520-145">**[Maken van een testgebruiker OpsGenie](#creating-a-opsgenie-test-user)**  - OpsGenie die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="6b520-145">**[Creating a OpsGenie test user](#creating-a-opsgenie-test-user)** - to have a counterpart of Britta Simon in OpsGenie that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="6b520-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="6b520-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6b520-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="6b520-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6b520-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="6b520-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6b520-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing OpsGenie configureren.</span><span class="sxs-lookup"><span data-stu-id="6b520-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your OpsGenie application.</span></span>

<span data-ttu-id="6b520-150">**Voor het configureren van Azure AD eenmalige aanmelding met OpsGenie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="6b520-150">**To configure Azure AD single sign-on with OpsGenie, perform the following steps:**</span></span>

1. <span data-ttu-id="6b520-151">In de Azure-portal op de **OpsGenie** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="6b520-151">In the Azure portal, on the **OpsGenie** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="6b520-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="6b520-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_samlbase.png)

3. <span data-ttu-id="6b520-155">Op de **OpsGenie domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="6b520-155">On the **OpsGenie Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_url.png)

    <span data-ttu-id="6b520-157">In de **aanmeldings-URL** textbox, typ de URL:`https://app.opsgenie.com/auth/login`</span><span class="sxs-lookup"><span data-stu-id="6b520-157">In the **Sign-on URL** textbox, type the URL: `https://app.opsgenie.com/auth/login`</span></span>

4. <span data-ttu-id="6b520-158">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="6b520-158">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_certificate.png) 

5. <span data-ttu-id="6b520-160">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="6b520-160">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-opsgenie-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6b520-162">Op de **OpsGenie configuratie** sectie, klikt u op **configureren OpsGenie** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="6b520-162">On the **OpsGenie Configuration** section, click **Configure OpsGenie** to open **Configure sign-on** window.</span></span> <span data-ttu-id="6b520-163">Kopieer de **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="6b520-163">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_configure.png) 

7. <span data-ttu-id="6b520-165">Open een ander browserexemplaar, en vervolgens aanmelden op OpsGenie als beheerder.</span><span class="sxs-lookup"><span data-stu-id="6b520-165">Open another browser instance, and then log-in to OpsGenie as an administrator.</span></span>

8. <span data-ttu-id="6b520-166">Klik op **instellingen**, en klik vervolgens op de **eenmalige aanmelding** tabblad.</span><span class="sxs-lookup"><span data-stu-id="6b520-166">Click **Settings**, and then click the **Single Sign On** tab.</span></span>
   
    ![OpsGenie voor eenmalige aanmelding](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_06.png)

9. <span data-ttu-id="6b520-168">Als u eenmalige aanmelding, schakelt **ingeschakeld**.</span><span class="sxs-lookup"><span data-stu-id="6b520-168">To enable SSO, select **Enabled**.</span></span>
   
    ![OpsGenie instellingen](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_07.png) 

10. <span data-ttu-id="6b520-170">In de **Provider** sectie, klikt u op de **Azure Active Directory** tabblad.</span><span class="sxs-lookup"><span data-stu-id="6b520-170">In the **Provider** section, click the **Azure Active Directory** tab.</span></span>
   
    ![OpsGenie instellingen](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_08.png) 

11. <span data-ttu-id="6b520-172">Voer de volgende stappen uit op de pagina van het dialoogvenster Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="6b520-172">On the Azure Active Directory dialog page, perform the following steps:</span></span>
   
    ![OpsGenie instellingen](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_09.png)
    
    <span data-ttu-id="6b520-174">a.</span><span class="sxs-lookup"><span data-stu-id="6b520-174">a.</span></span> <span data-ttu-id="6b520-175">Plakken **aanmelding op Service-URL met eenmalige**, die u hebt gekopieerd vanuit de Azure-portal in de **SAML 2.0 eindpunt** textbox.</span><span class="sxs-lookup"><span data-stu-id="6b520-175">Paste **Single Sign On Service URL**, which you have copied from the Azure portal into the **SAML 2.0 Endpoint** textbox.</span></span>
    
    <span data-ttu-id="6b520-176">b.</span><span class="sxs-lookup"><span data-stu-id="6b520-176">b.</span></span> <span data-ttu-id="6b520-177">Open uw gedownloade base-64 gecodeerde certificaat in Kladblok, Kopieer de inhoud ervan naar het Klembord en plakt u deze in de **X.500 certificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="6b520-177">Open your downloaded base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it into the **X.500 Certificate** textbox.</span></span>
    
    <span data-ttu-id="6b520-178">c.</span><span class="sxs-lookup"><span data-stu-id="6b520-178">c.</span></span> <span data-ttu-id="6b520-179">Klik op **wijzigingen opslaan**.</span><span class="sxs-lookup"><span data-stu-id="6b520-179">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="6b520-180">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="6b520-180">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6b520-181">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="6b520-181">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6b520-182">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6b520-182">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6b520-183">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="6b520-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="6b520-184">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="6b520-184">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="6b520-186">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="6b520-186">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6b520-187">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="6b520-187">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6b520-189">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="6b520-189">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6b520-191">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6b520-191">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6b520-193">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="6b520-193">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6b520-195">a.</span><span class="sxs-lookup"><span data-stu-id="6b520-195">a.</span></span> <span data-ttu-id="6b520-196">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6b520-196">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6b520-197">b.</span><span class="sxs-lookup"><span data-stu-id="6b520-197">b.</span></span> <span data-ttu-id="6b520-198">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6b520-198">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6b520-199">c.</span><span class="sxs-lookup"><span data-stu-id="6b520-199">c.</span></span> <span data-ttu-id="6b520-200">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="6b520-200">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6b520-201">d.</span><span class="sxs-lookup"><span data-stu-id="6b520-201">d.</span></span> <span data-ttu-id="6b520-202">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="6b520-202">Click **Create**.</span></span>
 
### <a name="creating-a-opsgenie-test-user"></a><span data-ttu-id="6b520-203">Een testgebruiker OpsGenie maken</span><span class="sxs-lookup"><span data-stu-id="6b520-203">Creating a OpsGenie test user</span></span>

<span data-ttu-id="6b520-204">Het doel van deze sectie is het maken van een gebruiker Britta Simon in OpsGenie genoemd.</span><span class="sxs-lookup"><span data-stu-id="6b520-204">The objective of this section is to create a user called Britta Simon in OpsGenie.</span></span> 

1. <span data-ttu-id="6b520-205">Meld u aan bij uw tenant OpsGenie als een beheerder in een browservenster.</span><span class="sxs-lookup"><span data-stu-id="6b520-205">In a web browser window, log into your OpsGenie tenant as an administrator.</span></span>

2. <span data-ttu-id="6b520-206">Navigeer naar de lijst gebruikers door te klikken op **gebruiker** in het linkerdeelvenster.</span><span class="sxs-lookup"><span data-stu-id="6b520-206">Navigate to Users list by clicking **User** in left panel.</span></span>
   
   ![OpsGenie instellingen](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_10.png) 

3. <span data-ttu-id="6b520-208">Klik op **gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="6b520-208">Click **Add User**.</span></span>

4. <span data-ttu-id="6b520-209">Op de **gebruiker toevoegen** dialoogvenster de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="6b520-209">On the **Add User** dialog, perform the following steps:</span></span>
   
   ![OpsGenie instellingen](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_11.png)
   
   <span data-ttu-id="6b520-211">a.</span><span class="sxs-lookup"><span data-stu-id="6b520-211">a.</span></span> <span data-ttu-id="6b520-212">In de **e** textbox, typ het e-mailadres van BrittaSimon behandeld in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6b520-212">In the **Email** textbox, type the email address of BrittaSimon addressed in Azure Active Directory.</span></span>
   
   <span data-ttu-id="6b520-213">b.</span><span class="sxs-lookup"><span data-stu-id="6b520-213">b.</span></span> <span data-ttu-id="6b520-214">In de **volledige naam** textbox type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="6b520-214">In the **Full Name** textbox, type **Britta Simon**.</span></span>
   
   <span data-ttu-id="6b520-215">c.</span><span class="sxs-lookup"><span data-stu-id="6b520-215">c.</span></span> <span data-ttu-id="6b520-216">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="6b520-216">Click **Save**.</span></span> 

>[!NOTE]
><span data-ttu-id="6b520-217">Britta Hiermee haalt u een e-mailbericht met instructies voor het instellen van haar profiel.</span><span class="sxs-lookup"><span data-stu-id="6b520-217">Britta gets an email with instructions for setting up her profile.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="6b520-218">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="6b520-218">Assigning the Azure AD test user</span></span>

<span data-ttu-id="6b520-219">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan OpsGenie.</span><span class="sxs-lookup"><span data-stu-id="6b520-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to OpsGenie.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="6b520-221">**Britta Simon om aan te wijzen OpsGenie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="6b520-221">**To assign Britta Simon to OpsGenie, perform the following steps:**</span></span>

1. <span data-ttu-id="6b520-222">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="6b520-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="6b520-224">Selecteer in de lijst met toepassingen **OpsGenie**.</span><span class="sxs-lookup"><span data-stu-id="6b520-224">In the applications list, select **OpsGenie**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_app.png) 

3. <span data-ttu-id="6b520-226">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="6b520-226">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="6b520-228">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="6b520-228">Click **Add** button.</span></span> <span data-ttu-id="6b520-229">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6b520-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="6b520-231">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="6b520-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6b520-232">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6b520-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6b520-233">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6b520-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6b520-234">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="6b520-234">Testing single sign-on</span></span>

<span data-ttu-id="6b520-235">Het doel van deze sectie is het testen van uw Azure AD SSO-configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="6b520-235">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="6b520-236">Als u op de tegel OpsGenie in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing OpsGenie.</span><span class="sxs-lookup"><span data-stu-id="6b520-236">When you click the OpsGenie tile in the Access Panel, you should get automatically signed-on to your OpsGenie application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6b520-237">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="6b520-237">Additional resources</span></span>

* [<span data-ttu-id="6b520-238">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6b520-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6b520-239">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6b520-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_203.png

