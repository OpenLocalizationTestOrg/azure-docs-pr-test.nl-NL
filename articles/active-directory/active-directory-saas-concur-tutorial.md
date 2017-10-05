---
title: 'Zelfstudie: Azure Active Directory-integratie met Concur | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Concur.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1eee0a5d-24fa-4986-9aef-3c543cfe3296
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 0b44437b3dcf69dae3587529da7d12e7809b9f55
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-concur"></a><span data-ttu-id="e76a0-103">Zelfstudie: Azure Active Directory-integratie met Concur</span><span class="sxs-lookup"><span data-stu-id="e76a0-103">Tutorial: Azure Active Directory integration with Concur</span></span>

<span data-ttu-id="e76a0-104">In deze zelfstudie leert u hoe Concur integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e76a0-104">In this tutorial, you learn how to integrate Concur with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e76a0-105">Concur integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="e76a0-105">Integrating Concur with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e76a0-106">U kunt beheren in Azure AD die toegang tot Concur heeft</span><span class="sxs-lookup"><span data-stu-id="e76a0-106">You can control in Azure AD who has access to Concur</span></span>
- <span data-ttu-id="e76a0-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Concur (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="e76a0-107">You can enable your users to automatically get signed-on to Concur (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e76a0-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="e76a0-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e76a0-109">Als u meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e76a0-109">If you want to know more information about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e76a0-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="e76a0-110">Prerequisites</span></span>

<span data-ttu-id="e76a0-111">Voor het configureren van Azure AD-integratie met Concur, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="e76a0-111">To configure Azure AD integration with Concur, you need the following items:</span></span>

- <span data-ttu-id="e76a0-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="e76a0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e76a0-113">Een Concur eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="e76a0-113">A Concur single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e76a0-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="e76a0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e76a0-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="e76a0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e76a0-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="e76a0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e76a0-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e76a0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e76a0-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="e76a0-118">Scenario description</span></span>
<span data-ttu-id="e76a0-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="e76a0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e76a0-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="e76a0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e76a0-121">Concur uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="e76a0-121">Adding Concur from the gallery</span></span>
2. <span data-ttu-id="e76a0-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="e76a0-122">Configuring and testing Azure AD single sign-on</span></span>

>[!NOTE]
><span data-ttu-id="e76a0-123">De configuratie van uw abonnement Concur voor federatieve eenmalige aanmelding via SAML is een afzonderlijke taak, die u moet contact opnemen met [Client instemming ondersteuningsteam](https://www.concur.co.in/contact) om uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="e76a0-123">The configuration of your Concur subscription for federated SSO via SAML is a separate task, which you must contact [Concur Client support team](https://www.concur.co.in/contact) to perform.</span></span> 

## <a name="adding-concur-from-the-gallery"></a><span data-ttu-id="e76a0-124">Concur uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="e76a0-124">Adding Concur from the gallery</span></span>
<span data-ttu-id="e76a0-125">Voor het configureren van de integratie van Concur in Azure AD, moet u Concur uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="e76a0-125">To configure the integration of Concur into Azure AD, you need to add Concur from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e76a0-126">**Als u wilt toevoegen Concur uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="e76a0-126">**To add Concur from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e76a0-127">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="e76a0-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e76a0-129">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="e76a0-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e76a0-130">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="e76a0-130">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="e76a0-132">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e76a0-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="e76a0-134">Typ in het zoekvak **Concur**.</span><span class="sxs-lookup"><span data-stu-id="e76a0-134">In the search box, type **Concur**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-concur-tutorial/tutorial_concur_search.png)

5. <span data-ttu-id="e76a0-136">Selecteer in het deelvenster resultaten **Concur**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="e76a0-136">In the results panel, select **Concur**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-concur-tutorial/tutorial_concur_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e76a0-138">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="e76a0-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e76a0-139">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Concur op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="e76a0-139">In this section, you configure and test Azure AD single sign-on with Concur based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e76a0-140">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Concur is aan een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e76a0-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Concur is to a user in Azure AD.</span></span> <span data-ttu-id="e76a0-141">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Concur tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="e76a0-141">In other words, a link relationship between an Azure AD user and the related user in Concur needs to be established.</span></span>

<span data-ttu-id="e76a0-142">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in Concur.</span><span class="sxs-lookup"><span data-stu-id="e76a0-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Concur.</span></span>

<span data-ttu-id="e76a0-143">Om te configureren en testen van Azure AD eenmalige aanmelding met Concur, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="e76a0-143">To configure and test Azure AD single sign-on with Concur, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e76a0-144">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e76a0-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e76a0-145">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e76a0-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e76a0-146">**[Maken van een testgebruiker Concur](#creating-a-concur-test-user)**  - Concur die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="e76a0-146">**[Creating a Concur test user](#creating-a-concur-test-user)** - to have a counterpart of Britta Simon in Concur that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e76a0-147">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="e76a0-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e76a0-148">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="e76a0-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e76a0-149">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="e76a0-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e76a0-150">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Concur configureren.</span><span class="sxs-lookup"><span data-stu-id="e76a0-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Concur application.</span></span>

<span data-ttu-id="e76a0-151">**Voor het configureren van Azure AD eenmalige aanmelding met Concur, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="e76a0-151">**To configure Azure AD single sign-on with Concur, perform the following steps:**</span></span>

1. <span data-ttu-id="e76a0-152">In de Azure-portal op de **Concur** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="e76a0-152">In the Azure portal, on the **Concur** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="e76a0-154">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="e76a0-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-concur-tutorial/tutorial_concur_samlbase.png)

3. <span data-ttu-id="e76a0-156">Op de **instemming domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="e76a0-156">On the **Concur Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-concur-tutorial/tutorial_concur_url.png)

    <span data-ttu-id="e76a0-158">a.</span><span class="sxs-lookup"><span data-stu-id="e76a0-158">a.</span></span> <span data-ttu-id="e76a0-159">In de **aanmelden URL** textbox, typ de waarde met het volgende patroon volgen:`https://www.concursolutions.com/UI/SSO/<OrganizationId>`</span><span class="sxs-lookup"><span data-stu-id="e76a0-159">In the **Sign on URL** textbox, type the value using the following pattern: `https://www.concursolutions.com/UI/SSO/<OrganizationId>`</span></span>

    <span data-ttu-id="e76a0-160">b.</span><span class="sxs-lookup"><span data-stu-id="e76a0-160">b.</span></span> <span data-ttu-id="e76a0-161">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<customer-domain>.concursolutions.com`</span><span class="sxs-lookup"><span data-stu-id="e76a0-161">In the **Identifier** textbox, type a URL using the following pattern: `https://<customer-domain>.concursolutions.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e76a0-162">Deze waarden zijn niet de werkelijke.</span><span class="sxs-lookup"><span data-stu-id="e76a0-162">These values are not the real.</span></span> <span data-ttu-id="e76a0-163">Deze waarden bijwerken met de werkelijke aanmelding URL en de id.</span><span class="sxs-lookup"><span data-stu-id="e76a0-163">Update these values with the actual Sign on URL and Identifier.</span></span> <span data-ttu-id="e76a0-164">Neem contact op met [Client instemming ondersteuningsteam](https://www.concur.co.in/contact) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="e76a0-164">Contact [Concur Client support team](https://www.concur.co.in/contact) to get these values.</span></span> 

4. <span data-ttu-id="e76a0-165">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het XML-bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="e76a0-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-concur-tutorial/tutorial_concur_certificate.png) 

5. <span data-ttu-id="e76a0-167">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="e76a0-167">Click **Save** button.</span></span>

    <span data-ttu-id="e76a0-168">![Eenmalige aanmelding configureren](./media/active-directory-saas-concur-tutorial/tutorial_general_400.png)
<CS></span><span class="sxs-lookup"><span data-stu-id="e76a0-168">![Configure Single Sign-On](./media/active-directory-saas-concur-tutorial/tutorial_general_400.png)
<CS></span></span>

6. <span data-ttu-id="e76a0-169">Eenmalige aanmelding configureren op **Concur** zijde, moet u de gedownloade verzenden **Metadata XML** Concur ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="e76a0-169">To configure single sign-on on **Concur** side, you need to send the downloaded **Metadata XML** to Concur support.</span></span> <span data-ttu-id="e76a0-170">Ze deze instelling zodat de SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="e76a0-170">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

  >[!NOTE]
  ><span data-ttu-id="e76a0-171">De configuratie van uw abonnement Concur voor federatieve eenmalige aanmelding via SAML is een afzonderlijke taak, die u moet contact opnemen met [Client instemming ondersteuningsteam](https://www.concur.co.in/contact) om uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="e76a0-171">The configuration of your Concur subscription for federated SSO via SAML is a separate task, which you must contact [Concur Client support team](https://www.concur.co.in/contact) to perform.</span></span> 
  
<CE>

> [!TIP]
> <span data-ttu-id="e76a0-172">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="e76a0-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e76a0-173">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="e76a0-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e76a0-174">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e76a0-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e76a0-175">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="e76a0-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="e76a0-176">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="e76a0-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="e76a0-178">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="e76a0-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e76a0-179">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="e76a0-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-concur-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e76a0-181">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="e76a0-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-concur-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e76a0-183">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e76a0-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-concur-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e76a0-185">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="e76a0-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-concur-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e76a0-187">a.</span><span class="sxs-lookup"><span data-stu-id="e76a0-187">a.</span></span> <span data-ttu-id="e76a0-188">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e76a0-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e76a0-189">b.</span><span class="sxs-lookup"><span data-stu-id="e76a0-189">b.</span></span> <span data-ttu-id="e76a0-190">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e76a0-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e76a0-191">c.</span><span class="sxs-lookup"><span data-stu-id="e76a0-191">c.</span></span> <span data-ttu-id="e76a0-192">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="e76a0-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e76a0-193">d.</span><span class="sxs-lookup"><span data-stu-id="e76a0-193">d.</span></span> <span data-ttu-id="e76a0-194">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="e76a0-194">Click **Create**.</span></span>
 
### <a name="creating-a-concur-test-user"></a><span data-ttu-id="e76a0-195">Een testgebruiker Concur maken</span><span class="sxs-lookup"><span data-stu-id="e76a0-195">Creating a Concur test user</span></span>

<span data-ttu-id="e76a0-196">Toepassing ondersteunt de Just in time gebruikers inrichten en na verificatie gebruikers automatisch in de toepassing gemaakt worden.</span><span class="sxs-lookup"><span data-stu-id="e76a0-196">Application supports the Just in time user provisioning and after authentication users are created in the application automatically.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e76a0-197">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="e76a0-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e76a0-198">In deze sectie maakt inschakelen u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Concur.</span><span class="sxs-lookup"><span data-stu-id="e76a0-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Concur.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="e76a0-200">**Britta Simon om aan te wijzen Concur, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="e76a0-200">**To assign Britta Simon to Concur, perform the following steps:**</span></span>

1. <span data-ttu-id="e76a0-201">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="e76a0-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="e76a0-203">Selecteer in de lijst met toepassingen **Concur**.</span><span class="sxs-lookup"><span data-stu-id="e76a0-203">In the applications list, select **Concur**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-concur-tutorial/tutorial_concur_app.png) 

3. <span data-ttu-id="e76a0-205">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="e76a0-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="e76a0-207">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="e76a0-207">Click **Add** button.</span></span> <span data-ttu-id="e76a0-208">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e76a0-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="e76a0-210">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="e76a0-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e76a0-211">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e76a0-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e76a0-212">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e76a0-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e76a0-213">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="e76a0-213">Testing single sign-on</span></span>

<span data-ttu-id="e76a0-214">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="e76a0-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e76a0-215">Als u op de tegel Concur in het deelvenster toegang, krijgt u de aanmeldingspagina van Concur toepassing.</span><span class="sxs-lookup"><span data-stu-id="e76a0-215">When you click the Concur tile in the Access Panel, you should get login page of Concur application.</span></span>
<span data-ttu-id="e76a0-216">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e76a0-216">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="e76a0-217">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="e76a0-217">Additional resources</span></span>

* [<span data-ttu-id="e76a0-218">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e76a0-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e76a0-219">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e76a0-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="e76a0-220">Gebruikers inrichten configureren</span><span class="sxs-lookup"><span data-stu-id="e76a0-220">Configure User Provisioning</span></span>](active-directory-saas-concur-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-concur-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-concur-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-concur-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-concur-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-concur-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-concur-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-concur-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-concur-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-concur-tutorial/tutorial_general_203.png

