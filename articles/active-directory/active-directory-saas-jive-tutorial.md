---
title: 'Zelfstudie: Azure Active Directory-integratie met Jive | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Jive.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9fc5659a-c116-4a1b-a601-333325a26b46
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 6d2d4b777d7afd74598d2eba4a7e3571a8a18d6f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jive"></a><span data-ttu-id="3d4af-103">Zelfstudie: Azure Active Directory-integratie met Jive</span><span class="sxs-lookup"><span data-stu-id="3d4af-103">Tutorial: Azure Active Directory integration with Jive</span></span>

<span data-ttu-id="3d4af-104">In deze zelfstudie leert u hoe Jive integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3d4af-104">In this tutorial, you learn how to integrate Jive with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3d4af-105">Jive integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="3d4af-105">Integrating Jive with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3d4af-106">U kunt beheren in Azure AD die toegang tot Jive heeft</span><span class="sxs-lookup"><span data-stu-id="3d4af-106">You can control in Azure AD who has access to Jive</span></span>
- <span data-ttu-id="3d4af-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Jive (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="3d4af-107">You can enable your users to automatically get signed-on to Jive (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3d4af-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="3d4af-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3d4af-109">Als u meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3d4af-109">If you want to know more information about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3d4af-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="3d4af-110">Prerequisites</span></span>

<span data-ttu-id="3d4af-111">Voor het configureren van Azure AD-integratie met Jive, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="3d4af-111">To configure Azure AD integration with Jive, you need the following items:</span></span>

- <span data-ttu-id="3d4af-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="3d4af-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3d4af-113">Een Jive eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="3d4af-113">A Jive single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3d4af-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="3d4af-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3d4af-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="3d4af-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3d4af-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="3d4af-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3d4af-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3d4af-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3d4af-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="3d4af-118">Scenario description</span></span>
<span data-ttu-id="3d4af-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="3d4af-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3d4af-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="3d4af-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3d4af-121">Jive uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="3d4af-121">Adding Jive from the gallery</span></span>
2. <span data-ttu-id="3d4af-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="3d4af-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jive-from-the-gallery"></a><span data-ttu-id="3d4af-123">Jive uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="3d4af-123">Adding Jive from the gallery</span></span>
<span data-ttu-id="3d4af-124">Voor het configureren van de integratie van Jive met Azure AD, moet u Jive uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="3d4af-124">To configure the integration of Jive into Azure AD, you need to add Jive from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3d4af-125">**Als u wilt toevoegen Jive uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="3d4af-125">**To add Jive from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3d4af-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="3d4af-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3d4af-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="3d4af-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3d4af-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="3d4af-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="3d4af-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3d4af-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="3d4af-133">Typ in het zoekvak **Jive**.</span><span class="sxs-lookup"><span data-stu-id="3d4af-133">In the search box, type **Jive**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jive-tutorial/tutorial_jive_search.png)

5. <span data-ttu-id="3d4af-135">Selecteer in het deelvenster resultaten **Jive**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="3d4af-135">In the results panel, select **Jive**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jive-tutorial/tutorial_jive_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3d4af-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="3d4af-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3d4af-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Jive op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="3d4af-138">In this section, you configure and test Azure AD single sign-on with Jive based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3d4af-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Jive is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3d4af-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Jive is to a user in Azure AD.</span></span> <span data-ttu-id="3d4af-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Jive tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="3d4af-140">In other words, a link relationship between an Azure AD user and the related user in Jive needs to be established.</span></span>

<span data-ttu-id="3d4af-141">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in Jive.</span><span class="sxs-lookup"><span data-stu-id="3d4af-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Jive.</span></span>

<span data-ttu-id="3d4af-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Jive, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="3d4af-142">To configure and test Azure AD single sign-on with Jive, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3d4af-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3d4af-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3d4af-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3d4af-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3d4af-145">**[Maken van een testgebruiker Jive](#creating-a-jive-test-user)**  - Jive die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="3d4af-145">**[Creating a Jive test user](#creating-a-jive-test-user)** - to have a counterpart of Britta Simon in Jive that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3d4af-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="3d4af-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3d4af-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="3d4af-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3d4af-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="3d4af-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3d4af-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Jive configureren.</span><span class="sxs-lookup"><span data-stu-id="3d4af-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Jive application.</span></span>

<span data-ttu-id="3d4af-150">**Voor het configureren van Azure AD eenmalige aanmelding met Jive, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="3d4af-150">**To configure Azure AD single sign-on with Jive, perform the following steps:**</span></span>

1. <span data-ttu-id="3d4af-151">In de Azure-portal op de **Jive** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="3d4af-151">In the Azure portal, on the **Jive** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="3d4af-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="3d4af-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jive-tutorial/tutorial_jive_samlbase.png)

3. <span data-ttu-id="3d4af-155">Op de **Jive domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="3d4af-155">On the **Jive Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jive-tutorial/tutorial_jive_url.png)

    <span data-ttu-id="3d4af-157">a.</span><span class="sxs-lookup"><span data-stu-id="3d4af-157">a.</span></span> <span data-ttu-id="3d4af-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<instance name>.jivecustom.com`</span><span class="sxs-lookup"><span data-stu-id="3d4af-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<instance name>.jivecustom.com`</span></span>

    <span data-ttu-id="3d4af-159">b.</span><span class="sxs-lookup"><span data-stu-id="3d4af-159">b.</span></span> <span data-ttu-id="3d4af-160">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<instance name>.jiveon.com`</span><span class="sxs-lookup"><span data-stu-id="3d4af-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<instance name>.jiveon.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3d4af-161">Deze waarden zijn niet de werkelijke.</span><span class="sxs-lookup"><span data-stu-id="3d4af-161">These values are not the real.</span></span> <span data-ttu-id="3d4af-162">Deze waarden bijwerken met de werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="3d4af-162">Update these values with the actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="3d4af-163">Neem contact op met [Jive Client ondersteuningsteam](https://www.jivesoftware.com/services-support/) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="3d4af-163">Contact [Jive Client support team](https://www.jivesoftware.com/services-support/) to get these values.</span></span> 
 
4. <span data-ttu-id="3d4af-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het XML-bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="3d4af-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jive-tutorial/tutorial_jive_certificate.png) 

5. <span data-ttu-id="3d4af-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="3d4af-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jive-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3d4af-168">Eenmalige aanmelding configureren op **Jive** kant aanmelding bij uw tenant Jive als beheerder.</span><span class="sxs-lookup"><span data-stu-id="3d4af-168">To configure single sign-on on **Jive** side, sign-on to your Jive tenant as an administrator.</span></span>

7. <span data-ttu-id="3d4af-169">Klik in het menu bovenaan op '**Saml**. "</span><span class="sxs-lookup"><span data-stu-id="3d4af-169">In the menu on the top, Click "**Saml**."</span></span>

    ![App-zijde eenmalige aanmelding configureren](./media/active-directory-saas-jive-tutorial/tutorial_jive_002.png)

    <span data-ttu-id="3d4af-171">a.</span><span class="sxs-lookup"><span data-stu-id="3d4af-171">a.</span></span> <span data-ttu-id="3d4af-172">Selecteer **ingeschakeld** onder de **algemene** tabblad.</span><span class="sxs-lookup"><span data-stu-id="3d4af-172">Select **Enabled** under the **General** tab.</span></span>   
    <span data-ttu-id="3d4af-173">b.</span><span class="sxs-lookup"><span data-stu-id="3d4af-173">b.</span></span> <span data-ttu-id="3d4af-174">Klik op de '**alle saml-instellingen opslaan**' knop.</span><span class="sxs-lookup"><span data-stu-id="3d4af-174">Click the "**Save all saml settings**" button.</span></span>

8. <span data-ttu-id="3d4af-175">Navigeer naar de '**Idp metagegevens**' tabblad.</span><span class="sxs-lookup"><span data-stu-id="3d4af-175">Navigate to the "**Idp Metadata**" tab.</span></span>
   
    ![App-zijde eenmalige aanmelding configureren](./media/active-directory-saas-jive-tutorial/tutorial_jive_003.png)
   
    <span data-ttu-id="3d4af-177">a.</span><span class="sxs-lookup"><span data-stu-id="3d4af-177">a.</span></span> <span data-ttu-id="3d4af-178">Kopieer de inhoud van het gedownloade metagegevens-XML-bestand en plakt u deze in de **Identity-Provider (IDP) metagegevens** textbox.</span><span class="sxs-lookup"><span data-stu-id="3d4af-178">Copy the content of the downloaded metadata XML file, and then paste it into the **Identity Provider (IDP) Metadata** textbox.</span></span>
    
    <span data-ttu-id="3d4af-179">b.</span><span class="sxs-lookup"><span data-stu-id="3d4af-179">b.</span></span> <span data-ttu-id="3d4af-180">Klik op de '**alle saml-instellingen opslaan**' knop.</span><span class="sxs-lookup"><span data-stu-id="3d4af-180">Click the "**Save all saml settings**" button.</span></span> 

9. <span data-ttu-id="3d4af-181">Ga naar de '**kenmerk Gebruikerskoppeling**' tabblad.</span><span class="sxs-lookup"><span data-stu-id="3d4af-181">Go to the "**User Attribute Mapping**" tab.</span></span>
   
    ![App-zijde eenmalige aanmelding configureren](./media/active-directory-saas-jive-tutorial/tutorial_jive_004.png)
   
    <span data-ttu-id="3d4af-183">a.</span><span class="sxs-lookup"><span data-stu-id="3d4af-183">a.</span></span> <span data-ttu-id="3d4af-184">In de **e** textbox kopieert en plakt u de naam van het kenmerk van **mail** waarde.</span><span class="sxs-lookup"><span data-stu-id="3d4af-184">In the **Email** textbox, copy and paste the attribute name of **mail** value.</span></span>
   
    <span data-ttu-id="3d4af-185">b.</span><span class="sxs-lookup"><span data-stu-id="3d4af-185">b.</span></span> <span data-ttu-id="3d4af-186">In de **voornaam** textbox kopieert en plakt u de naam van het kenmerk van **givenname** waarde.</span><span class="sxs-lookup"><span data-stu-id="3d4af-186">In the **First Name** textbox, copy and paste the attribute name of **givenname** value.</span></span>
   
    <span data-ttu-id="3d4af-187">c.</span><span class="sxs-lookup"><span data-stu-id="3d4af-187">c.</span></span> <span data-ttu-id="3d4af-188">In de **achternaam** textbox kopieert en plakt u de naam van het kenmerk van **achternaam** waarde.</span><span class="sxs-lookup"><span data-stu-id="3d4af-188">In the **Last Name** textbox, copy and paste the attribute name of **surname** value.</span></span>

> [!TIP]
> <span data-ttu-id="3d4af-189">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="3d4af-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3d4af-190">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="3d4af-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3d4af-191">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3d4af-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3d4af-192">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="3d4af-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="3d4af-193">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="3d4af-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="3d4af-195">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="3d4af-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3d4af-196">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="3d4af-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jive-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3d4af-198">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="3d4af-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jive-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3d4af-200">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3d4af-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jive-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3d4af-202">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="3d4af-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jive-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3d4af-204">a.</span><span class="sxs-lookup"><span data-stu-id="3d4af-204">a.</span></span> <span data-ttu-id="3d4af-205">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3d4af-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3d4af-206">b.</span><span class="sxs-lookup"><span data-stu-id="3d4af-206">b.</span></span> <span data-ttu-id="3d4af-207">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3d4af-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3d4af-208">c.</span><span class="sxs-lookup"><span data-stu-id="3d4af-208">c.</span></span> <span data-ttu-id="3d4af-209">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="3d4af-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3d4af-210">d.</span><span class="sxs-lookup"><span data-stu-id="3d4af-210">d.</span></span> <span data-ttu-id="3d4af-211">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="3d4af-211">Click **Create**.</span></span>
 
### <a name="creating-a-jive-test-user"></a><span data-ttu-id="3d4af-212">Een testgebruiker Jive maken</span><span class="sxs-lookup"><span data-stu-id="3d4af-212">Creating a Jive test user</span></span>

<span data-ttu-id="3d4af-213">Werken met [Jive Client ondersteuningsteam](https://www.jivesoftware.com/services-support/) de gebruikers van het platform Jive toevoegen.</span><span class="sxs-lookup"><span data-stu-id="3d4af-213">Work with [Jive Client support team](https://www.jivesoftware.com/services-support/) to add the users in the Jive platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3d4af-214">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="3d4af-214">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3d4af-215">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Jive.</span><span class="sxs-lookup"><span data-stu-id="3d4af-215">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Jive.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="3d4af-217">**Britta Simon om aan te wijzen Jive, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="3d4af-217">**To assign Britta Simon to Jive, perform the following steps:**</span></span>

1. <span data-ttu-id="3d4af-218">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="3d4af-218">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="3d4af-220">Selecteer in de lijst met toepassingen **Jive**.</span><span class="sxs-lookup"><span data-stu-id="3d4af-220">In the applications list, select **Jive**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jive-tutorial/tutorial_jive_app.png) 

3. <span data-ttu-id="3d4af-222">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="3d4af-222">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="3d4af-224">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="3d4af-224">Click **Add** button.</span></span> <span data-ttu-id="3d4af-225">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3d4af-225">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="3d4af-227">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="3d4af-227">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3d4af-228">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3d4af-228">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3d4af-229">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3d4af-229">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3d4af-230">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="3d4af-230">Testing single sign-on</span></span>

<span data-ttu-id="3d4af-231">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="3d4af-231">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3d4af-232">Als u op de tegel Jive in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Jive.</span><span class="sxs-lookup"><span data-stu-id="3d4af-232">When you click the Jive tile in the Access Panel, you should get automatically signed-on to your Jive application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3d4af-233">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="3d4af-233">Additional resources</span></span>

* [<span data-ttu-id="3d4af-234">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3d4af-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3d4af-235">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3d4af-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="3d4af-236">Gebruikers inrichten configureren</span><span class="sxs-lookup"><span data-stu-id="3d4af-236">Configure User Provisioning</span></span>](active-directory-saas-jive-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-jive-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jive-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jive-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jive-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jive-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jive-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jive-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jive-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jive-tutorial/tutorial_general_203.png

