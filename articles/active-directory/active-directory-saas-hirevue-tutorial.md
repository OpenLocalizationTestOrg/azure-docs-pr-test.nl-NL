---
title: 'Zelfstudie: Azure Active Directory-integratie met HireVue | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en HireVue.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: aadfc342-14db-4d74-a83d-f0c76f0cf63c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 682d88d3010f5781948a9adde0e1351471608a5e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hirevue"></a><span data-ttu-id="2bcf8-103">Zelfstudie: Azure Active Directory-integratie met HireVue</span><span class="sxs-lookup"><span data-stu-id="2bcf8-103">Tutorial: Azure Active Directory integration with HireVue</span></span>

<span data-ttu-id="2bcf8-104">In deze zelfstudie leert u hoe HireVue integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2bcf8-104">In this tutorial, you learn how to integrate HireVue with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2bcf8-105">HireVue integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="2bcf8-105">Integrating HireVue with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2bcf8-106">U kunt beheren in Azure AD die toegang tot HireVue heeft</span><span class="sxs-lookup"><span data-stu-id="2bcf8-106">You can control in Azure AD who has access to HireVue</span></span>
- <span data-ttu-id="2bcf8-107">U kunt uw gebruikers automatisch ophalen aangemeld bij HireVue (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="2bcf8-107">You can enable your users to automatically get signed-on to HireVue (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2bcf8-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="2bcf8-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="2bcf8-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2bcf8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2bcf8-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="2bcf8-110">Prerequisites</span></span>

<span data-ttu-id="2bcf8-111">Voor het configureren van Azure AD-integratie met HireVue, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="2bcf8-111">To configure Azure AD integration with HireVue, you need the following items:</span></span>

- <span data-ttu-id="2bcf8-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="2bcf8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2bcf8-113">Een HireVue eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="2bcf8-113">A HireVue single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2bcf8-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="2bcf8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2bcf8-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="2bcf8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2bcf8-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="2bcf8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2bcf8-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2bcf8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2bcf8-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="2bcf8-118">Scenario description</span></span>
<span data-ttu-id="2bcf8-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="2bcf8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2bcf8-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="2bcf8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2bcf8-121">HireVue uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="2bcf8-121">Adding HireVue from the gallery</span></span>
2. <span data-ttu-id="2bcf8-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="2bcf8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hirevue-from-the-gallery"></a><span data-ttu-id="2bcf8-123">HireVue uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="2bcf8-123">Adding HireVue from the gallery</span></span>
<span data-ttu-id="2bcf8-124">Voor het configureren van de integratie van HireVue in Azure AD, moet u HireVue uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="2bcf8-124">To configure the integration of HireVue into Azure AD, you need to add HireVue from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2bcf8-125">**Als u wilt toevoegen HireVue uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="2bcf8-125">**To add HireVue from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2bcf8-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="2bcf8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2bcf8-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="2bcf8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2bcf8-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="2bcf8-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="2bcf8-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2bcf8-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="2bcf8-133">Typ in het zoekvak **HireVue**.</span><span class="sxs-lookup"><span data-stu-id="2bcf8-133">In the search box, type **HireVue**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_search.png)

5. <span data-ttu-id="2bcf8-135">Selecteer in het deelvenster resultaten **HireVue**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="2bcf8-135">In the results panel, select **HireVue**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2bcf8-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="2bcf8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2bcf8-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met HireVue op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="2bcf8-138">In this section, you configure and test Azure AD single sign-on with HireVue based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2bcf8-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in HireVue is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2bcf8-139">For single sign-on to work, Azure AD needs to know what the counterpart user in HireVue is to a user in Azure AD.</span></span> <span data-ttu-id="2bcf8-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in HireVue tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="2bcf8-140">In other words, a link relationship between an Azure AD user and the related user in HireVue needs to be established.</span></span>

<span data-ttu-id="2bcf8-141">Wijs in HireVue, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="2bcf8-141">In HireVue, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="2bcf8-142">Om te configureren en testen van Azure AD eenmalige aanmelding met HireVue, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="2bcf8-142">To configure and test Azure AD single sign-on with HireVue, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2bcf8-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2bcf8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2bcf8-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2bcf8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2bcf8-145">**[Maken van een testgebruiker HireVue](#creating-a-hirevue-test-user)**  - HireVue die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="2bcf8-145">**[Creating a HireVue test user](#creating-a-hirevue-test-user)** - to have a counterpart of Britta Simon in HireVue that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="2bcf8-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="2bcf8-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2bcf8-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="2bcf8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2bcf8-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="2bcf8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2bcf8-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing HireVue configureren.</span><span class="sxs-lookup"><span data-stu-id="2bcf8-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your HireVue application.</span></span>

<span data-ttu-id="2bcf8-150">**Voor het configureren van Azure AD eenmalige aanmelding met HireVue, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="2bcf8-150">**To configure Azure AD single sign-on with HireVue, perform the following steps:**</span></span>

1. <span data-ttu-id="2bcf8-151">In de Azure-portal op de **HireVue** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="2bcf8-151">In the Azure portal, on the **HireVue** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="2bcf8-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="2bcf8-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_samlbase.png)

3. <span data-ttu-id="2bcf8-155">Op de **HireVue domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="2bcf8-155">On the **HireVue Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_url.png)

    <span data-ttu-id="2bcf8-157">a.</span><span class="sxs-lookup"><span data-stu-id="2bcf8-157">a.</span></span> <span data-ttu-id="2bcf8-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="2bcf8-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>

    | <span data-ttu-id="2bcf8-159">Omgeving</span><span class="sxs-lookup"><span data-stu-id="2bcf8-159">Environment</span></span> | <span data-ttu-id="2bcf8-160">URL</span><span class="sxs-lookup"><span data-stu-id="2bcf8-160">URL</span></span> |
    |-------------|---|
    | <span data-ttu-id="2bcf8-161">Productie</span><span class="sxs-lookup"><span data-stu-id="2bcf8-161">Production</span></span> | `https://<companyname>.hirevue.com` |
    | <span data-ttu-id="2bcf8-162">Fasering</span><span class="sxs-lookup"><span data-stu-id="2bcf8-162">Staging</span></span>    | `https://<companyname>.stghv.com` |
    
    <span data-ttu-id="2bcf8-163">b.</span><span class="sxs-lookup"><span data-stu-id="2bcf8-163">b.</span></span> <span data-ttu-id="2bcf8-164">In de **id** textbox, typ een URL als:</span><span class="sxs-lookup"><span data-stu-id="2bcf8-164">In the **Identifier** textbox, type a URL as:</span></span>
    
    | <span data-ttu-id="2bcf8-165">Omgeving</span><span class="sxs-lookup"><span data-stu-id="2bcf8-165">Environment</span></span> | <span data-ttu-id="2bcf8-166">URN</span><span class="sxs-lookup"><span data-stu-id="2bcf8-166">URN</span></span> |
    |-------------|-----|
    | <span data-ttu-id="2bcf8-167">Productie</span><span class="sxs-lookup"><span data-stu-id="2bcf8-167">Production</span></span> |`urn:federation:hirevue.com:saml:sp:prod` |
    | <span data-ttu-id="2bcf8-168">Fasering</span><span class="sxs-lookup"><span data-stu-id="2bcf8-168">Staging</span></span>    | `urn:federation:hirevue.com:saml:sp:staging`|
    
    > [!NOTE] 
    > <span data-ttu-id="2bcf8-169">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="2bcf8-169">These values are not real.</span></span> <span data-ttu-id="2bcf8-170">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="2bcf8-170">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="2bcf8-171">Neem contact op met [HireVue Client ondersteuningsteam](mailto:samlsupport@hirevue.com) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="2bcf8-171">Contact [HireVue Client support team](mailto:samlsupport@hirevue.com) to get these values.</span></span> 
 
4. <span data-ttu-id="2bcf8-172">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="2bcf8-172">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_certificate.png) 

5. <span data-ttu-id="2bcf8-174">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="2bcf8-174">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hirevue-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2bcf8-176">Op de **HireVue configuratie** sectie, klikt u op **configureren HireVue** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="2bcf8-176">On the **HireVue Configuration** section, click **Configure HireVue** to open **Configure sign-on** window.</span></span> <span data-ttu-id="2bcf8-177">Kopieer de **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="2bcf8-177">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_configure.png) 

7. <span data-ttu-id="2bcf8-179">Eenmalige aanmelding configureren op **HireVue** zijde, moet u de gedownloade verzenden **Certificate(Base64)** en **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** naar [HireVue ondersteuningsteam](mailto:samlsupport@hirevue.com).</span><span class="sxs-lookup"><span data-stu-id="2bcf8-179">To configure single sign-on on **HireVue** side, you need to send the downloaded **Certificate(Base64)** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [HireVue support team](mailto:samlsupport@hirevue.com).</span></span> <span data-ttu-id="2bcf8-180">Ze deze instelling zodat de SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="2bcf8-180">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="2bcf8-181">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="2bcf8-181">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="2bcf8-182">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="2bcf8-182">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="2bcf8-183">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2bcf8-183">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2bcf8-184">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="2bcf8-184">Creating an Azure AD test user</span></span>
<span data-ttu-id="2bcf8-185">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="2bcf8-185">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="2bcf8-187">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="2bcf8-187">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2bcf8-188">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="2bcf8-188">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hirevue-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2bcf8-190">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="2bcf8-190">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hirevue-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2bcf8-192">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2bcf8-192">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hirevue-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2bcf8-194">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="2bcf8-194">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hirevue-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2bcf8-196">a.</span><span class="sxs-lookup"><span data-stu-id="2bcf8-196">a.</span></span> <span data-ttu-id="2bcf8-197">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2bcf8-197">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2bcf8-198">b.</span><span class="sxs-lookup"><span data-stu-id="2bcf8-198">b.</span></span> <span data-ttu-id="2bcf8-199">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2bcf8-199">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2bcf8-200">c.</span><span class="sxs-lookup"><span data-stu-id="2bcf8-200">c.</span></span> <span data-ttu-id="2bcf8-201">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="2bcf8-201">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="2bcf8-202">d.</span><span class="sxs-lookup"><span data-stu-id="2bcf8-202">d.</span></span> <span data-ttu-id="2bcf8-203">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="2bcf8-203">Click **Create**.</span></span>
 
### <a name="creating-a-hirevue-test-user"></a><span data-ttu-id="2bcf8-204">Een testgebruiker HireVue maken</span><span class="sxs-lookup"><span data-stu-id="2bcf8-204">Creating a HireVue test user</span></span>

<span data-ttu-id="2bcf8-205">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in HireVue maken.</span><span class="sxs-lookup"><span data-stu-id="2bcf8-205">In this section, you create a user called Britta Simon in HireVue.</span></span> <span data-ttu-id="2bcf8-206">Neem contact op met [HireVue ondersteuningsteam](mailto:samlsupport@hirevue.com) de gebruikers van het platform HireVue toevoegen.</span><span class="sxs-lookup"><span data-stu-id="2bcf8-206">Please work with [HireVue support team](mailto:samlsupport@hirevue.com) to add the users in the HireVue platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="2bcf8-207">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="2bcf8-207">Assigning the Azure AD test user</span></span>

<span data-ttu-id="2bcf8-208">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan HireVue.</span><span class="sxs-lookup"><span data-stu-id="2bcf8-208">In this section, you enable Britta Simon to use Azure single sign-on by granting access to HireVue.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="2bcf8-210">**Britta Simon om aan te wijzen HireVue, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="2bcf8-210">**To assign Britta Simon to HireVue, perform the following steps:**</span></span>

1. <span data-ttu-id="2bcf8-211">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="2bcf8-211">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="2bcf8-213">Selecteer in de lijst met toepassingen **HireVue**.</span><span class="sxs-lookup"><span data-stu-id="2bcf8-213">In the applications list, select **HireVue**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_app.png) 

3. <span data-ttu-id="2bcf8-215">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="2bcf8-215">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="2bcf8-217">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="2bcf8-217">Click **Add** button.</span></span> <span data-ttu-id="2bcf8-218">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2bcf8-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="2bcf8-220">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="2bcf8-220">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="2bcf8-221">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2bcf8-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2bcf8-222">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2bcf8-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2bcf8-223">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="2bcf8-223">Testing single sign-on</span></span>

<span data-ttu-id="2bcf8-224">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="2bcf8-224">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="2bcf8-225">Als u op de tegel HireVue in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing HireVue.</span><span class="sxs-lookup"><span data-stu-id="2bcf8-225">When you click the HireVue tile in the Access Panel, you should get automatically signed-on to your HireVue application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2bcf8-226">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="2bcf8-226">Additional resources</span></span>

* [<span data-ttu-id="2bcf8-227">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2bcf8-227">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2bcf8-228">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2bcf8-228">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_203.png

