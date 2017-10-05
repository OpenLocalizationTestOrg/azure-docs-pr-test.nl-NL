---
title: 'Zelfstudie: Azure Active Directory-integratie met 123ContactForm | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en 123ContactForm.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5211910a-ab96-4709-959a-524c4d57c43e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 3a99f0841c3e0d973168991f5dbee40e54c1d054
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-123contactform"></a><span data-ttu-id="c8e5e-103">Zelfstudie: Azure Active Directory-integratie met 123ContactForm</span><span class="sxs-lookup"><span data-stu-id="c8e5e-103">Tutorial: Azure Active Directory integration with 123ContactForm</span></span>

<span data-ttu-id="c8e5e-104">In deze zelfstudie leert u hoe 123ContactForm integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c8e5e-104">In this tutorial, you learn how to integrate 123ContactForm with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c8e5e-105">123ContactForm integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="c8e5e-105">Integrating 123ContactForm with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c8e5e-106">U kunt beheren in Azure AD die toegang tot 123ContactForm heeft</span><span class="sxs-lookup"><span data-stu-id="c8e5e-106">You can control in Azure AD who has access to 123ContactForm</span></span>
- <span data-ttu-id="c8e5e-107">U kunt uw gebruikers automatisch ophalen aangemeld bij 123ContactForm inschakelen (Single Sign-On) met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="c8e5e-107">You can enable your users to automatically get signed-on to 123ContactForm (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c8e5e-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="c8e5e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c8e5e-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c8e5e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c8e5e-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="c8e5e-110">Prerequisites</span></span>

<span data-ttu-id="c8e5e-111">Voor het configureren van Azure AD-integratie met 123ContactForm, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="c8e5e-111">To configure Azure AD integration with 123ContactForm, you need the following items:</span></span>

- <span data-ttu-id="c8e5e-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="c8e5e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c8e5e-113">Een 123ContactForm eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="c8e5e-113">A 123ContactForm single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c8e5e-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c8e5e-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="c8e5e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c8e5e-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c8e5e-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c8e5e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c8e5e-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="c8e5e-118">Scenario description</span></span>
<span data-ttu-id="c8e5e-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c8e5e-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="c8e5e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c8e5e-121">123ContactForm uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="c8e5e-121">Adding 123ContactForm from the gallery</span></span>
2. <span data-ttu-id="c8e5e-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="c8e5e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-123contactform-from-the-gallery"></a><span data-ttu-id="c8e5e-123">123ContactForm uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="c8e5e-123">Adding 123ContactForm from the gallery</span></span>
<span data-ttu-id="c8e5e-124">Voor het configureren van de integratie van 123ContactForm in Azure AD, moet u 123ContactForm uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-124">To configure the integration of 123ContactForm into Azure AD, you need to add 123ContactForm from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c8e5e-125">**Als u wilt toevoegen 123ContactForm uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="c8e5e-125">**To add 123ContactForm from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c8e5e-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c8e5e-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c8e5e-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="c8e5e-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="c8e5e-133">Typ in het zoekvak **123ContactForm**.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-133">In the search box, type **123ContactForm**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_search.png)

5. <span data-ttu-id="c8e5e-135">Selecteer in het deelvenster resultaten **123ContactForm**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-135">In the results panel, select **123ContactForm**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c8e5e-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="c8e5e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c8e5e-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met 123ContactForm op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="c8e5e-138">In this section, you configure and test Azure AD single sign-on with 123ContactForm based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c8e5e-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in 123ContactForm is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in 123ContactForm is to a user in Azure AD.</span></span> <span data-ttu-id="c8e5e-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in 123ContactForm tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-140">In other words, a link relationship between an Azure AD user and the related user in 123ContactForm needs to be established.</span></span>

<span data-ttu-id="c8e5e-141">Wijs in 123ContactForm, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-141">In 123ContactForm, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c8e5e-142">Om te configureren en testen van Azure AD eenmalige aanmelding met 123ContactForm, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="c8e5e-142">To configure and test Azure AD single sign-on with 123ContactForm, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c8e5e-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c8e5e-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c8e5e-145">**[Maken van een testgebruiker 123ContactForm](#creating-a-123contactform-test-user)**  - hebben een equivalent van Britta Simon in 123ContactForm die is gekoppeld aan de Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-145">**[Creating a 123ContactForm test user](#creating-a-123contactform-test-user)** - to have a counterpart of Britta Simon in 123ContactForm that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c8e5e-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c8e5e-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c8e5e-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="c8e5e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c8e5e-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing 123ContactForm configureren.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your 123ContactForm application.</span></span>

<span data-ttu-id="c8e5e-150">**Voor het configureren van Azure AD eenmalige aanmelding met 123ContactForm, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="c8e5e-150">**To configure Azure AD single sign-on with 123ContactForm, perform the following steps:**</span></span>

1. <span data-ttu-id="c8e5e-151">In de Azure-portal op de **123ContactForm** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-151">In the Azure portal, on the **123ContactForm** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="c8e5e-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_samlbase.png)

3. <span data-ttu-id="c8e5e-155">Op de **123ContactForm domein en de URL's** sectie als u wilt configureren van de toepassing in **IDP geïnitieerd modus**, voer de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="c8e5e-155">On the **123ContactForm Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-123contactform-tutorial/url1.png)

    <span data-ttu-id="c8e5e-157">a.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-157">a.</span></span> <span data-ttu-id="c8e5e-158">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://www.123contactform.com/saml/azure_ad/<tenant_id>/metadata`</span><span class="sxs-lookup"><span data-stu-id="c8e5e-158">In the **Identifier** textbox, type a URL using the following pattern: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/metadata`</span></span>

    <span data-ttu-id="c8e5e-159">b.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-159">b.</span></span> <span data-ttu-id="c8e5e-160">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://www.123contactform.com/saml/azure_ad/<tenant_id>/acs`</span><span class="sxs-lookup"><span data-stu-id="c8e5e-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/acs`</span></span>

4. <span data-ttu-id="c8e5e-161">Als u wilt configureren van de toepassing in **SP geïnitieerd modus**, voer de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="c8e5e-161">If you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-123contactform-tutorial/url2.png)

    <span data-ttu-id="c8e5e-163">a.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-163">a.</span></span> <span data-ttu-id="c8e5e-164">Klik op de **weergeven geavanceerde instellingen voor URL** optie</span><span class="sxs-lookup"><span data-stu-id="c8e5e-164">Click the **Show advanced URL settings** option</span></span>

    <span data-ttu-id="c8e5e-165">b.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-165">b.</span></span> <span data-ttu-id="c8e5e-166">In de **aanmelding op URL** textbox, typ een URL als:`https://www.123contactform.com/saml/azure_ad/<tenant_id>/sso`</span><span class="sxs-lookup"><span data-stu-id="c8e5e-166">In the **Sign On URL** textbox, type a URL as: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/sso`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c8e5e-167">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-167">These values are not real.</span></span> <span data-ttu-id="c8e5e-168">U moet deze waarde van de werkelijke URL's en -id die verderop in de zelfstudie wordt uitgelegd bijwerken.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-168">You'll need to update these value from actual URLs and Identifier which is explained later in the tutorial.</span></span>
    
5. <span data-ttu-id="c8e5e-169">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-169">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_certificate.png) 

6. <span data-ttu-id="c8e5e-171">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-171">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-123contactform-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="c8e5e-173">Eenmalige aanmelding configureren op **123ContactForm** aan clientzijde, gaat u naar [https://www.123contactform.com/form-2709121/](https://www.123contactform.com/form-2709121/) en voer de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="c8e5e-173">To configure single sign-on on **123ContactForm** side, go to [https://www.123contactform.com/form-2709121/](https://www.123contactform.com/form-2709121/) and perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-123contactform-tutorial/submit.png) 

    <span data-ttu-id="c8e5e-175">a.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-175">a.</span></span> <span data-ttu-id="c8e5e-176">In de **e** textbox, typ de e-mailadres van de gebruiker eenledige</span><span class="sxs-lookup"><span data-stu-id="c8e5e-176">In the **Email** textbox, type the email of the user i.e</span></span> <span data-ttu-id="c8e5e-177">**BrittaSimon@Contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-177">**BrittaSimon@Contoso.com**.</span></span>

    <span data-ttu-id="c8e5e-178">b.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-178">b.</span></span> <span data-ttu-id="c8e5e-179">Klik op **uploaden** en blader naar het Metadata XML-bestand dat u hebt gedownload vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-179">Click **Upload** and browse the Metadata XML file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="c8e5e-180">c.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-180">c.</span></span> <span data-ttu-id="c8e5e-181">Klik op **indienen formulier**.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-181">Click **SUBMIT FORM**.</span></span>

8. <span data-ttu-id="c8e5e-182">Op de **instellingen App van Microsoft Azure AD eenmalige aanmelding -** de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="c8e5e-182">On the **Microsoft Azure AD - Single sign-on - Configure App Settings** perform the following steps:</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-123contactform-tutorial/url3.png)

    <span data-ttu-id="c8e5e-184">a.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-184">a.</span></span> <span data-ttu-id="c8e5e-185">Als u wilt configureren van de toepassing in **IDP geïnitieerd modus**, Kopieer de **id** waarde voor uw exemplaar en plak deze in **id** textbox in  **123ContactForm domein en de URL's** sectie op Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-185">If you wish to configure the application in **IDP initiated mode**, copy the **IDENTIFIER** value for your instance and paste it in **Identifier** textbox in **123ContactForm Domain and URLs** section on Azure portal.</span></span>
    
    <span data-ttu-id="c8e5e-186">b.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-186">b.</span></span> <span data-ttu-id="c8e5e-187">Als u wilt configureren van de toepassing in **IDP geïnitieerd modus**, Kopieer de **antwoord-URL** waarde voor uw exemplaar en plak deze in **antwoord-URL** textbox in  **123ContactForm domein en de URL's** sectie op Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-187">If you wish to configure the application in **IDP initiated mode**, copy the **REPLY URL** value for your instance and paste it in **Reply URL** textbox in **123ContactForm Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="c8e5e-188">c.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-188">c.</span></span> <span data-ttu-id="c8e5e-189">Als u wilt configureren van de toepassing in **SP geïnitieerd modus**, exemplaar de **SIGN-ON-URL** waarde voor uw exemplaar en plak deze in **aanmelding op URL** textbox in  **123ContactForm domein en de URL's** sectie op Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-189">If you wish to configure the application in **SP initiated mode**, copy the **SIGN ON URL** value for your instance and paste it in **Sign On URL** textbox in **123ContactForm Domain and URLs** section on Azure portal.</span></span>

> [!TIP]
> <span data-ttu-id="c8e5e-190">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="c8e5e-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c8e5e-191">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c8e5e-192">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c8e5e-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c8e5e-193">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="c8e5e-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="c8e5e-194">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="c8e5e-196">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="c8e5e-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c8e5e-197">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-123contactform-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c8e5e-199">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-123contactform-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c8e5e-201">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-123contactform-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c8e5e-203">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="c8e5e-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-123contactform-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c8e5e-205">a.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-205">a.</span></span> <span data-ttu-id="c8e5e-206">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-206">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c8e5e-207">b.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-207">b.</span></span> <span data-ttu-id="c8e5e-208">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c8e5e-209">c.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-209">c.</span></span> <span data-ttu-id="c8e5e-210">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c8e5e-211">d.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-211">d.</span></span> <span data-ttu-id="c8e5e-212">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-212">Click **Create**.</span></span>
 
### <a name="creating-a-123contactform-test-user"></a><span data-ttu-id="c8e5e-213">Een testgebruiker 123ContactForm maken</span><span class="sxs-lookup"><span data-stu-id="c8e5e-213">Creating a 123ContactForm test user</span></span>

<span data-ttu-id="c8e5e-214">Toepassing ondersteunt Just in tijd gebruikers inrichten en na verificatie gebruikers wordt in de toepassing automatisch gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-214">Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c8e5e-215">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="c8e5e-215">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c8e5e-216">In deze sectie schakelt u Britta Simon Azure eenmalige aanmelding gebruiken door het verlenen van toegang tot 123ContactForm.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to 123ContactForm.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="c8e5e-218">**Britta Simon om aan te wijzen 123ContactForm, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="c8e5e-218">**To assign Britta Simon to 123ContactForm, perform the following steps:**</span></span>

1. <span data-ttu-id="c8e5e-219">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="c8e5e-221">Selecteer in de lijst met toepassingen **123ContactForm**.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-221">In the applications list, select **123ContactForm**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_app.png) 

3. <span data-ttu-id="c8e5e-223">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-223">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="c8e5e-225">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-225">Click **Add** button.</span></span> <span data-ttu-id="c8e5e-226">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="c8e5e-228">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c8e5e-229">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c8e5e-230">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c8e5e-231">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="c8e5e-231">Testing single sign-on</span></span>

<span data-ttu-id="c8e5e-232">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-232">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c8e5e-233">Als u op de tegel 123ContactForm in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing 123ContactForm.</span><span class="sxs-lookup"><span data-stu-id="c8e5e-233">When you click the 123ContactForm tile in the Access Panel, you should get automatically signed-on to your 123ContactForm application.</span></span>
<span data-ttu-id="c8e5e-234">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c8e5e-234">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c8e5e-235">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="c8e5e-235">Additional resources</span></span>

* [<span data-ttu-id="c8e5e-236">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c8e5e-236">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c8e5e-237">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c8e5e-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_203.png

