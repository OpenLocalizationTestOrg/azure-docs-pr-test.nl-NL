---
title: 'Zelfstudie: Azure Active Directory-integratie met Gigya | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Gigya.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2c7d200b-9242-44a5-ac8a-ab3214a78e41
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: b65a33989a045a3e0b57fda522a9bc3b0770c7f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-gigya"></a><span data-ttu-id="785f4-103">Zelfstudie: Azure Active Directory-integratie met Gigya</span><span class="sxs-lookup"><span data-stu-id="785f4-103">Tutorial: Azure Active Directory integration with Gigya</span></span>

<span data-ttu-id="785f4-104">In deze zelfstudie leert u hoe Gigya integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="785f4-104">In this tutorial, you learn how to integrate Gigya with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="785f4-105">Gigya integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="785f4-105">Integrating Gigya with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="785f4-106">U kunt beheren in Azure AD die toegang tot Gigya heeft</span><span class="sxs-lookup"><span data-stu-id="785f4-106">You can control in Azure AD who has access to Gigya</span></span>
- <span data-ttu-id="785f4-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Gigya (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="785f4-107">You can enable your users to automatically get signed-on to Gigya (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="785f4-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="785f4-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="785f4-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="785f4-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="785f4-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="785f4-110">Prerequisites</span></span>

<span data-ttu-id="785f4-111">Voor het configureren van Azure AD-integratie met Gigya, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="785f4-111">To configure Azure AD integration with Gigya, you need the following items:</span></span>

- <span data-ttu-id="785f4-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="785f4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="785f4-113">Een Gigya eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="785f4-113">A Gigya single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="785f4-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="785f4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="785f4-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="785f4-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="785f4-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="785f4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="785f4-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="785f4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="785f4-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="785f4-118">Scenario description</span></span>
<span data-ttu-id="785f4-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="785f4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="785f4-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="785f4-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="785f4-121">Gigya uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="785f4-121">Adding Gigya from the gallery</span></span>
2. <span data-ttu-id="785f4-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="785f4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-gigya-from-the-gallery"></a><span data-ttu-id="785f4-123">Gigya uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="785f4-123">Adding Gigya from the gallery</span></span>
<span data-ttu-id="785f4-124">Voor het configureren van de integratie van Gigya in Azure AD, moet u Gigya uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="785f4-124">To configure the integration of Gigya into Azure AD, you need to add Gigya from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="785f4-125">**Als u wilt toevoegen Gigya uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="785f4-125">**To add Gigya from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="785f4-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="785f4-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="785f4-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="785f4-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="785f4-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="785f4-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="785f4-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="785f4-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="785f4-133">Typ in het zoekvak **Gigya**.</span><span class="sxs-lookup"><span data-stu-id="785f4-133">In the search box, type **Gigya**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_search.png)

5. <span data-ttu-id="785f4-135">Selecteer in het deelvenster resultaten **Gigya**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="785f4-135">In the results panel, select **Gigya**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="785f4-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="785f4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="785f4-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Gigya op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="785f4-138">In this section, you configure and test Azure AD single sign-on with Gigya based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="785f4-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Gigya is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="785f4-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Gigya is to a user in Azure AD.</span></span> <span data-ttu-id="785f4-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Gigya tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="785f4-140">In other words, a link relationship between an Azure AD user and the related user in Gigya needs to be established.</span></span>

<span data-ttu-id="785f4-141">Wijs in Gigya, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="785f4-141">In Gigya, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="785f4-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Gigya, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="785f4-142">To configure and test Azure AD single sign-on with Gigya, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="785f4-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="785f4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="785f4-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="785f4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="785f4-145">**[Maken van een testgebruiker Gigya](#creating-a-gigya-test-user)**  - Gigya die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="785f4-145">**[Creating a Gigya test user](#creating-a-gigya-test-user)** - to have a counterpart of Britta Simon in Gigya that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="785f4-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="785f4-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="785f4-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="785f4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="785f4-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="785f4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="785f4-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Gigya configureren.</span><span class="sxs-lookup"><span data-stu-id="785f4-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Gigya application.</span></span>

<span data-ttu-id="785f4-150">**Voor het configureren van Azure AD eenmalige aanmelding met Gigya, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="785f4-150">**To configure Azure AD single sign-on with Gigya, perform the following steps:**</span></span>

1. <span data-ttu-id="785f4-151">In de Azure-portal op de **Gigya** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="785f4-151">In the Azure portal, on the **Gigya** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="785f4-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="785f4-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_samlbase.png)

3. <span data-ttu-id="785f4-155">Op de **Gigya domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="785f4-155">On the **Gigya Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_url.png)

    <span data-ttu-id="785f4-157">a.</span><span class="sxs-lookup"><span data-stu-id="785f4-157">a.</span></span> <span data-ttu-id="785f4-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`http://<companyname>.gigya.com`</span><span class="sxs-lookup"><span data-stu-id="785f4-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `http://<companyname>.gigya.com`</span></span>

    <span data-ttu-id="785f4-159">b.</span><span class="sxs-lookup"><span data-stu-id="785f4-159">b.</span></span> <span data-ttu-id="785f4-160">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://fidm.gigya.com/saml/v2.0/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="785f4-160">In the **Identifier** textbox, type a URL using the following pattern: `https://fidm.gigya.com/saml/v2.0/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="785f4-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="785f4-161">These values are not real.</span></span> <span data-ttu-id="785f4-162">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="785f4-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="785f4-163">Neem contact op met [Gigya Client ondersteuningsteam](https://www.gigya.com/support-policy/) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="785f4-163">Contact [Gigya Client support team](https://www.gigya.com/support-policy/) to get these values.</span></span> 
 
4. <span data-ttu-id="785f4-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="785f4-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_certificate.png) 

5. <span data-ttu-id="785f4-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="785f4-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-gigya-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="785f4-168">Op de **Gigya configuratie** sectie, klikt u op **configureren Gigya** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="785f4-168">On the **Gigya Configuration** section, click **Configure Gigya** to open **Configure sign-on** window.</span></span> <span data-ttu-id="785f4-169">Kopieer de **SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="785f4-169">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_configure.png) 

7. <span data-ttu-id="785f4-171">In een ander browservenster, meld u bij uw bedrijf Gigya site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="785f4-171">In a different web browser window, log into your Gigya company site as an administrator.</span></span>

8. <span data-ttu-id="785f4-172">Ga naar **instellingen \> SAML aanmelding**, en klik vervolgens op de **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="785f4-172">Go to **Settings \> SAML Login**, and then click the **Add** button.</span></span>
   
    <span data-ttu-id="785f4-173">![SAML-aanmelding](./media/active-directory-saas-gigya-tutorial/ic789532.png "SAML-aanmelding")</span><span class="sxs-lookup"><span data-stu-id="785f4-173">![SAML Login](./media/active-directory-saas-gigya-tutorial/ic789532.png "SAML Login")</span></span>

9. <span data-ttu-id="785f4-174">In de **SAML aanmelding** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="785f4-174">In the **SAML Login** section, perform the following steps:</span></span>
   
    <span data-ttu-id="785f4-175">![De SAML-configuratie](./media/active-directory-saas-gigya-tutorial/ic789533.png "SAML-configuratie")</span><span class="sxs-lookup"><span data-stu-id="785f4-175">![SAML Configuration](./media/active-directory-saas-gigya-tutorial/ic789533.png "SAML Configuration")</span></span>
   
    <span data-ttu-id="785f4-176">a.</span><span class="sxs-lookup"><span data-stu-id="785f4-176">a.</span></span> <span data-ttu-id="785f4-177">In de **naam** textbox, typ een naam voor uw configuratie.</span><span class="sxs-lookup"><span data-stu-id="785f4-177">In the **Name** textbox, type a name for your configuration.</span></span>
   
    <span data-ttu-id="785f4-178">b.</span><span class="sxs-lookup"><span data-stu-id="785f4-178">b.</span></span> <span data-ttu-id="785f4-179">In **verlener** textbox, plak de waarde van **SAML entiteit-ID** die u hebt gekopieerd vanuit Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="785f4-179">In **Issuer** textbox, paste the value of **SAML Entity ID** which you have copied from Azure Portal.</span></span> 
   
    <span data-ttu-id="785f4-180">c.</span><span class="sxs-lookup"><span data-stu-id="785f4-180">c.</span></span> <span data-ttu-id="785f4-181">In **Single Sign-On Service-URL** textbox, plak de waarde van **Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="785f4-181">In **Single Sign-On Service URL** textbox, paste the value of **Single Sign-On Service URL** which you have copied from Azure Portal.</span></span>
   
    <span data-ttu-id="785f4-182">d.</span><span class="sxs-lookup"><span data-stu-id="785f4-182">d.</span></span> <span data-ttu-id="785f4-183">In **indeling naam-ID** textbox, plak de waarde van **indeling van de id** die u hebt gekopieerd vanuit Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="785f4-183">In **Name ID Format** textbox, paste the value of **Name Identifier Format** which you have copied from Azure Portal.</span></span>
   
    <span data-ttu-id="785f4-184">e.</span><span class="sxs-lookup"><span data-stu-id="785f4-184">e.</span></span> <span data-ttu-id="785f4-185">De base-64 gecodeerde certificaat openen in Kladblok van Azure portal hebt gedownload, Kopieer de inhoud ervan naar het Klembord en plakt u deze naar de **X.509-certificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="785f4-185">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox.</span></span>
   
    <span data-ttu-id="785f4-186">f.</span><span class="sxs-lookup"><span data-stu-id="785f4-186">f.</span></span> <span data-ttu-id="785f4-187">Klik op **instellingen opslaan**.</span><span class="sxs-lookup"><span data-stu-id="785f4-187">Click **Save Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="785f4-188">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="785f4-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="785f4-189">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="785f4-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="785f4-190">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="785f4-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="785f4-191">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="785f4-191">Creating an Azure AD test user</span></span>

<span data-ttu-id="785f4-192">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="785f4-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="785f4-194">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="785f4-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="785f4-195">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="785f4-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-gigya-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="785f4-197">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="785f4-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-gigya-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="785f4-199">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="785f4-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-gigya-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="785f4-201">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="785f4-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-gigya-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="785f4-203">a.</span><span class="sxs-lookup"><span data-stu-id="785f4-203">a.</span></span> <span data-ttu-id="785f4-204">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="785f4-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="785f4-205">b.</span><span class="sxs-lookup"><span data-stu-id="785f4-205">b.</span></span> <span data-ttu-id="785f4-206">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="785f4-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="785f4-207">c.</span><span class="sxs-lookup"><span data-stu-id="785f4-207">c.</span></span> <span data-ttu-id="785f4-208">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="785f4-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="785f4-209">d.</span><span class="sxs-lookup"><span data-stu-id="785f4-209">d.</span></span> <span data-ttu-id="785f4-210">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="785f4-210">Click **Create**.</span></span>
 
### <a name="creating-a-gigya-test-user"></a><span data-ttu-id="785f4-211">Een testgebruiker Gigya maken</span><span class="sxs-lookup"><span data-stu-id="785f4-211">Creating a Gigya test user</span></span>

<span data-ttu-id="785f4-212">Om in te schakelen gebruikers van Azure AD aan te melden bij Gigya, moeten ze worden ingericht in Gigya.</span><span class="sxs-lookup"><span data-stu-id="785f4-212">In order to enable Azure AD users to log into Gigya, they must be provisioned into Gigya.</span></span>  
<span data-ttu-id="785f4-213">In het geval van Gigya is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="785f4-213">In the case of Gigya, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-accounts-perform-the-following-steps"></a><span data-ttu-id="785f4-214">Voor het inrichten van een gebruikersaccount, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="785f4-214">To provision a user accounts, perform the following steps:</span></span>

1. <span data-ttu-id="785f4-215">Meld u aan bij uw **Gigya** bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="785f4-215">Log in to your **Gigya** company site as an administrator.</span></span>

2. <span data-ttu-id="785f4-216">Ga naar **Admin \> gebruikers beheren**, en klik vervolgens op **gebruikers uitnodigen**.</span><span class="sxs-lookup"><span data-stu-id="785f4-216">Go to **Admin \> Manage Users**, and then click **Invite Users**.</span></span>
   
    <span data-ttu-id="785f4-217">![Gebruikers beheren](./media/active-directory-saas-gigya-tutorial/ic789535.png "gebruikers beheren")</span><span class="sxs-lookup"><span data-stu-id="785f4-217">![Manage Users](./media/active-directory-saas-gigya-tutorial/ic789535.png "Manage Users")</span></span>

3. <span data-ttu-id="785f4-218">Voer de volgende stappen uit in het dialoogvenster gebruikers uitnodigen:</span><span class="sxs-lookup"><span data-stu-id="785f4-218">On the Invite Users dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="785f4-219">![Gebruikers uitnodigen](./media/active-directory-saas-gigya-tutorial/ic789536.png "gebruikers uitnodigen")</span><span class="sxs-lookup"><span data-stu-id="785f4-219">![Invite Users](./media/active-directory-saas-gigya-tutorial/ic789536.png "Invite Users")</span></span>
   
    <span data-ttu-id="785f4-220">a.</span><span class="sxs-lookup"><span data-stu-id="785f4-220">a.</span></span> <span data-ttu-id="785f4-221">In de **e** textbox, typ de e-mailalias op van een geldige Azure Active Directory-account dat u inrichten wilt.</span><span class="sxs-lookup"><span data-stu-id="785f4-221">In the **Email** textbox, type the email alias of a valid Azure Active Directory account you want to provision.</span></span>
    
    <span data-ttu-id="785f4-222">b.</span><span class="sxs-lookup"><span data-stu-id="785f4-222">b.</span></span> <span data-ttu-id="785f4-223">Klik op **gebruiker uitnodigen**.</span><span class="sxs-lookup"><span data-stu-id="785f4-223">Click **Invite User**.</span></span>
      
    > [!NOTE]
    > <span data-ttu-id="785f4-224">De houder van Azure Active Directory-account ontvangt een e-mailbericht een koppeling om te bevestigen van het account bevat voordat deze geactiveerd wordt.</span><span class="sxs-lookup"><span data-stu-id="785f4-224">The Azure Active Directory account holder will receive an email that includes a link to confirm the account before it becomes active.</span></span>
    > 
    

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="785f4-225">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="785f4-225">Assigning the Azure AD test user</span></span>

<span data-ttu-id="785f4-226">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Gigya.</span><span class="sxs-lookup"><span data-stu-id="785f4-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Gigya.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="785f4-228">**Britta Simon om aan te wijzen Gigya, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="785f4-228">**To assign Britta Simon to Gigya, perform the following steps:**</span></span>

1. <span data-ttu-id="785f4-229">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="785f4-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="785f4-231">Selecteer in de lijst met toepassingen **Gigya**.</span><span class="sxs-lookup"><span data-stu-id="785f4-231">In the applications list, select **Gigya**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_app.png) 

3. <span data-ttu-id="785f4-233">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="785f4-233">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="785f4-235">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="785f4-235">Click **Add** button.</span></span> <span data-ttu-id="785f4-236">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="785f4-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="785f4-238">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="785f4-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="785f4-239">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="785f4-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="785f4-240">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="785f4-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="785f4-241">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="785f4-241">Testing single sign-on</span></span>

<span data-ttu-id="785f4-242">Het doel van deze sectie is het testen van uw Azure AD SSO-configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="785f4-242">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="785f4-243">Als u op de tegel Gigya in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Gigya.</span><span class="sxs-lookup"><span data-stu-id="785f4-243">When you click the Gigya tile in the Access Panel, you should get automatically signed-on to your Gigya application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="785f4-244">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="785f4-244">Additional resources</span></span>

* [<span data-ttu-id="785f4-245">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="785f4-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="785f4-246">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="785f4-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_203.png

