---
title: 'Zelfstudie: Azure Active Directory-integratie met Convercent | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Convercent.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f9c9d290-0e13-490b-b559-0be772d6a690
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: jeedes
ms.openlocfilehash: 7af33cae7448a212734d327570b5082d0278fa0d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-convercent"></a><span data-ttu-id="7835c-103">Zelfstudie: Azure Active Directory-integratie met Convercent</span><span class="sxs-lookup"><span data-stu-id="7835c-103">Tutorial: Azure Active Directory integration with Convercent</span></span>

<span data-ttu-id="7835c-104">In deze zelfstudie leert u hoe Convercent integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7835c-104">In this tutorial, you learn how to integrate Convercent with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7835c-105">Convercent integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="7835c-105">Integrating Convercent with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7835c-106">U kunt beheren in Azure AD die toegang tot Convercent heeft</span><span class="sxs-lookup"><span data-stu-id="7835c-106">You can control in Azure AD who has access to Convercent</span></span>
- <span data-ttu-id="7835c-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Convercent (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="7835c-107">You can enable your users to automatically get signed-on to Convercent (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7835c-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="7835c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7835c-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7835c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7835c-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="7835c-110">Prerequisites</span></span>

<span data-ttu-id="7835c-111">Voor het configureren van Azure AD-integratie met Convercent, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="7835c-111">To configure Azure AD integration with Convercent, you need the following items:</span></span>

- <span data-ttu-id="7835c-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="7835c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7835c-113">Een Convercent eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="7835c-113">A Convercent single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7835c-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="7835c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7835c-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="7835c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7835c-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="7835c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7835c-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7835c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7835c-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="7835c-118">Scenario description</span></span>
<span data-ttu-id="7835c-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="7835c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7835c-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="7835c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7835c-121">Convercent uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="7835c-121">Adding Convercent from the gallery</span></span>
2. <span data-ttu-id="7835c-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="7835c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-convercent-from-the-gallery"></a><span data-ttu-id="7835c-123">Convercent uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="7835c-123">Adding Convercent from the gallery</span></span>
<span data-ttu-id="7835c-124">Voor het configureren van de integratie van Convercent in Azure AD, moet u Convercent uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="7835c-124">To configure the integration of Convercent into Azure AD, you need to add Convercent from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7835c-125">**Als u wilt toevoegen Convercent uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="7835c-125">**To add Convercent from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7835c-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="7835c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7835c-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="7835c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7835c-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="7835c-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="7835c-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7835c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="7835c-133">Typ in het zoekvak **Convercent**.</span><span class="sxs-lookup"><span data-stu-id="7835c-133">In the search box, type **Convercent**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_search.png)

5. <span data-ttu-id="7835c-135">Selecteer in het deelvenster resultaten **Convercent**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="7835c-135">In the results panel, select **Convercent**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7835c-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="7835c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7835c-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Convercent op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="7835c-138">In this section, you configure and test Azure AD single sign-on with Convercent based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7835c-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Convercent is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7835c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Convercent is to a user in Azure AD.</span></span> <span data-ttu-id="7835c-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Convercent tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="7835c-140">In other words, a link relationship between an Azure AD user and the related user in Convercent needs to be established.</span></span>

<span data-ttu-id="7835c-141">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in Convercent.</span><span class="sxs-lookup"><span data-stu-id="7835c-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Convercent.</span></span>

<span data-ttu-id="7835c-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Convercent, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="7835c-142">To configure and test Azure AD single sign-on with Convercent, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7835c-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7835c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7835c-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7835c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7835c-145">**[Maken van een testgebruiker Convercent](#creating-a-convercent-test-user)**  - Convercent die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="7835c-145">**[Creating a Convercent test user](#creating-a-convercent-test-user)** - to have a counterpart of Britta Simon in Convercent that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7835c-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="7835c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7835c-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="7835c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7835c-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="7835c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7835c-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Convercent configureren.</span><span class="sxs-lookup"><span data-stu-id="7835c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Convercent application.</span></span>

<span data-ttu-id="7835c-150">**Voor het configureren van Azure AD eenmalige aanmelding met Convercent, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="7835c-150">**To configure Azure AD single sign-on with Convercent, perform the following steps:**</span></span>

1. <span data-ttu-id="7835c-151">In de Azure-portal op de **Convercent** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="7835c-151">In the Azure portal, on the **Convercent** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="7835c-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="7835c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_samlbase.png)

3. <span data-ttu-id="7835c-155">Op de **Convercent domein en de URL's** sectie als u wilt configureren van de toepassing in **IDP geïnitieerd modus**, voer de volgende stap:</span><span class="sxs-lookup"><span data-stu-id="7835c-155">On the **Convercent Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**, perform the following step:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_url.png)

    <span data-ttu-id="7835c-157">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<instancename>.convercent.com/`</span><span class="sxs-lookup"><span data-stu-id="7835c-157">In the **Identifier** textbox, type a URL using the following pattern: `https://<instancename>.convercent.com/`</span></span>
 
4. <span data-ttu-id="7835c-158">Als u wilt configureren van de toepassing in **SP geïnitieerd modus**op de **Convercent domein en de URL's** sectie de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="7835c-158">If you wish to configure the application in **SP initiated mode**, on the **Convercent Domain and URLs** section perform the following steps:</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_url1.png)

     <span data-ttu-id="7835c-160">a.</span><span class="sxs-lookup"><span data-stu-id="7835c-160">a.</span></span> <span data-ttu-id="7835c-161">Klik op **'Weergeven geavanceerde instellingen voor de URL'.**</span><span class="sxs-lookup"><span data-stu-id="7835c-161">Click **"Show advanced URL settings."**</span></span> 

     <span data-ttu-id="7835c-162">b.</span><span class="sxs-lookup"><span data-stu-id="7835c-162">b.</span></span> <span data-ttu-id="7835c-163">In de **aanmelding op URL** textbox, typ de waarde met het volgende patroon volgen:`https://<instancename>.convercent.com/`</span><span class="sxs-lookup"><span data-stu-id="7835c-163">In the **Sign On URL** textbox, type the value using the following pattern: `https://<instancename>.convercent.com/`</span></span>

     <span data-ttu-id="7835c-164">c.</span><span class="sxs-lookup"><span data-stu-id="7835c-164">c.</span></span> <span data-ttu-id="7835c-165">In de **Relay status** textbox, typ de waarde met het volgende patroon volgen:`https://<instancename>.convercent.com/`</span><span class="sxs-lookup"><span data-stu-id="7835c-165">In the **Relay State** textbox, type the value using the following pattern: `https://<instancename>.convercent.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7835c-166">Deze waarden zijn niet de werkelijke waarden.</span><span class="sxs-lookup"><span data-stu-id="7835c-166">These values are not the real values.</span></span> <span data-ttu-id="7835c-167">Deze waarden bijwerken met de werkelijke id, meld u op URL en de Relay-status.</span><span class="sxs-lookup"><span data-stu-id="7835c-167">Update these values with the actual Identifier, Sign On URL and Relay State.</span></span> <span data-ttu-id="7835c-168">Neem contact op met [Convercent Client ondersteuningsteam](http://support.convercent.com) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="7835c-168">Contact [Convercent Client support team](http://support.convercent.com) to get these values.</span></span>

5. <span data-ttu-id="7835c-169">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het XML-bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="7835c-169">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_certificate.png) 

6. <span data-ttu-id="7835c-171">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="7835c-171">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-convercent-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="7835c-173">Als u eenmalige aanmelding die zijn geconfigureerd voor uw toepassing, neem contact op met [Convercent ondersteuningsteam](mailto:support@convercent.com) en geeft u de gedownloade **Metadata XML**.</span><span class="sxs-lookup"><span data-stu-id="7835c-173">To get SSO configured for your application, contact [Convercent support team](mailto:support@convercent.com) and provide them with the downloaded **Metadata XML**.</span></span>

> [!TIP]
> <span data-ttu-id="7835c-174">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="7835c-174">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7835c-175">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="7835c-175">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7835c-176">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7835c-176">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7835c-177">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="7835c-177">Creating an Azure AD test user</span></span>
<span data-ttu-id="7835c-178">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="7835c-178">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="7835c-180">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="7835c-180">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7835c-181">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="7835c-181">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-convercent-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7835c-183">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="7835c-183">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-convercent-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7835c-185">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7835c-185">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-convercent-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7835c-187">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="7835c-187">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-convercent-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7835c-189">a.</span><span class="sxs-lookup"><span data-stu-id="7835c-189">a.</span></span> <span data-ttu-id="7835c-190">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7835c-190">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7835c-191">b.</span><span class="sxs-lookup"><span data-stu-id="7835c-191">b.</span></span> <span data-ttu-id="7835c-192">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7835c-192">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7835c-193">c.</span><span class="sxs-lookup"><span data-stu-id="7835c-193">c.</span></span> <span data-ttu-id="7835c-194">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="7835c-194">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7835c-195">d.</span><span class="sxs-lookup"><span data-stu-id="7835c-195">d.</span></span> <span data-ttu-id="7835c-196">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="7835c-196">Click **Create**.</span></span>
 
### <a name="creating-a-convercent-test-user"></a><span data-ttu-id="7835c-197">Een testgebruiker Convercent maken</span><span class="sxs-lookup"><span data-stu-id="7835c-197">Creating a Convercent test user</span></span>

<span data-ttu-id="7835c-198">Werken met [Convercent ondersteuningsteam](mailto:support@convercent.com) de gebruikers van het platform Convercent toevoegen.</span><span class="sxs-lookup"><span data-stu-id="7835c-198">Work with [Convercent support team](mailto:support@convercent.com) to add the users in the Convercent platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7835c-199">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="7835c-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7835c-200">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Convercent.</span><span class="sxs-lookup"><span data-stu-id="7835c-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Convercent.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="7835c-202">**Britta Simon om aan te wijzen Convercent, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="7835c-202">**To assign Britta Simon to Convercent, perform the following steps:**</span></span>

1. <span data-ttu-id="7835c-203">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="7835c-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="7835c-205">Selecteer in de lijst met toepassingen **Convercent**.</span><span class="sxs-lookup"><span data-stu-id="7835c-205">In the applications list, select **Convercent**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_app.png) 

3. <span data-ttu-id="7835c-207">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="7835c-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="7835c-209">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="7835c-209">Click **Add** button.</span></span> <span data-ttu-id="7835c-210">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7835c-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="7835c-212">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="7835c-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7835c-213">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7835c-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7835c-214">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7835c-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7835c-215">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="7835c-215">Testing single sign-on</span></span>

<span data-ttu-id="7835c-216">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="7835c-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="7835c-217">Als u op de tegel Convercent in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Convercent.</span><span class="sxs-lookup"><span data-stu-id="7835c-217">When you click the Convercent tile in the Access Panel, you should get automatically signed-on to your Convercent application.</span></span>
<span data-ttu-id="7835c-218">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7835c-218">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7835c-219">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="7835c-219">Additional resources</span></span>

* [<span data-ttu-id="7835c-220">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7835c-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7835c-221">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7835c-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_203.png

