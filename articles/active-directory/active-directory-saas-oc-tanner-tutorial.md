---
title: 'Zelfstudie: Azure Active Directory-integratie met O.C. Tan - AppreciateHub | Microsoft Docs'
description: Meer informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en O.C. Tan - AppreciateHub.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dee8fbca-0b60-4a21-8917-1fb6919de5a0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: jeedes
ms.openlocfilehash: 9af12372b30d9ee1575e46be3b4144fc3b73ec69
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-oc-tanner---appreciatehub"></a><span data-ttu-id="f98ca-105">Zelfstudie: Azure Active Directory-integratie met O.C.</span><span class="sxs-lookup"><span data-stu-id="f98ca-105">Tutorial: Azure Active Directory integration with O.C.</span></span> <span data-ttu-id="f98ca-106">Tan - AppreciateHub</span><span class="sxs-lookup"><span data-stu-id="f98ca-106">Tanner - AppreciateHub</span></span>

<span data-ttu-id="f98ca-107">In deze zelfstudie leert u hoe O.C. integreren</span><span class="sxs-lookup"><span data-stu-id="f98ca-107">In this tutorial, you learn how to integrate O.C.</span></span> <span data-ttu-id="f98ca-108">Tan - AppreciateHub met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f98ca-108">Tanner - AppreciateHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f98ca-109">Integratie van O.C.</span><span class="sxs-lookup"><span data-stu-id="f98ca-109">Integrating O.C.</span></span> <span data-ttu-id="f98ca-110">Tan - AppreciateHub met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="f98ca-110">Tanner - AppreciateHub with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f98ca-111">U kunt beheren in Azure AD die toegang tot O.C. heeft</span><span class="sxs-lookup"><span data-stu-id="f98ca-111">You can control in Azure AD who has access to O.C.</span></span> <span data-ttu-id="f98ca-112">Tan - AppreciateHub</span><span class="sxs-lookup"><span data-stu-id="f98ca-112">Tanner - AppreciateHub</span></span>
- <span data-ttu-id="f98ca-113">U kunt uw gebruikers automatisch ophalen aangemeld bij O.C. inschakelen</span><span class="sxs-lookup"><span data-stu-id="f98ca-113">You can enable your users to automatically get signed-on to O.C.</span></span> <span data-ttu-id="f98ca-114">Tan - AppreciateHub (Single Sign-On) met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="f98ca-114">Tanner - AppreciateHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f98ca-115">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="f98ca-115">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f98ca-116">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f98ca-116">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f98ca-117">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f98ca-117">Prerequisites</span></span>

<span data-ttu-id="f98ca-118">Azure AD-integratie met O.C. configureren</span><span class="sxs-lookup"><span data-stu-id="f98ca-118">To configure Azure AD integration with O.C.</span></span> <span data-ttu-id="f98ca-119">Tan - AppreciateHub, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="f98ca-119">Tanner - AppreciateHub, you need the following items:</span></span>

- <span data-ttu-id="f98ca-120">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="f98ca-120">An Azure AD subscription</span></span>
- <span data-ttu-id="f98ca-121">EEN O.C.</span><span class="sxs-lookup"><span data-stu-id="f98ca-121">A O.C.</span></span> <span data-ttu-id="f98ca-122">Tan - AppreciateHub eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="f98ca-122">Tanner - AppreciateHub single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f98ca-123">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="f98ca-123">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f98ca-124">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="f98ca-124">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f98ca-125">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="f98ca-125">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f98ca-126">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f98ca-126">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f98ca-127">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="f98ca-127">Scenario description</span></span>
<span data-ttu-id="f98ca-128">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="f98ca-128">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f98ca-129">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="f98ca-129">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f98ca-130">O.C. toevoegen</span><span class="sxs-lookup"><span data-stu-id="f98ca-130">Adding O.C.</span></span> <span data-ttu-id="f98ca-131">Tan - AppreciateHub uit de galerie</span><span class="sxs-lookup"><span data-stu-id="f98ca-131">Tanner - AppreciateHub from the gallery</span></span>
2. <span data-ttu-id="f98ca-132">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f98ca-132">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-oc-tanner---appreciatehub-from-the-gallery"></a><span data-ttu-id="f98ca-133">O.C. toevoegen</span><span class="sxs-lookup"><span data-stu-id="f98ca-133">Adding O.C.</span></span> <span data-ttu-id="f98ca-134">Tan - AppreciateHub uit de galerie</span><span class="sxs-lookup"><span data-stu-id="f98ca-134">Tanner - AppreciateHub from the gallery</span></span>
<span data-ttu-id="f98ca-135">De integratie van O.C. configureren</span><span class="sxs-lookup"><span data-stu-id="f98ca-135">To configure the integration of O.C.</span></span> <span data-ttu-id="f98ca-136">Tan - AppreciateHub met Azure AD, moet u O.C. toevoegen</span><span class="sxs-lookup"><span data-stu-id="f98ca-136">Tanner - AppreciateHub into Azure AD, you need to add O.C.</span></span> <span data-ttu-id="f98ca-137">Tan - AppreciateHub uit de galerie aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="f98ca-137">Tanner - AppreciateHub from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f98ca-138">**O.C. toevoegen Tan - AppreciateHub uit de galerie, de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="f98ca-138">**To add O.C. Tanner - AppreciateHub from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f98ca-139">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="f98ca-139">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f98ca-141">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f98ca-141">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f98ca-142">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f98ca-142">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="f98ca-144">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f98ca-144">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="f98ca-146">Typ in het zoekvak **O.C. Tan - AppreciateHub**.</span><span class="sxs-lookup"><span data-stu-id="f98ca-146">In the search box, type **O.C. Tanner - AppreciateHub**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_search.png)

5. <span data-ttu-id="f98ca-148">Selecteer in het deelvenster resultaten **O.C. Tan - AppreciateHub**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="f98ca-148">In the results panel, select **O.C. Tanner - AppreciateHub**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f98ca-150">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f98ca-150">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f98ca-151">In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met O.C.</span><span class="sxs-lookup"><span data-stu-id="f98ca-151">In this section, you configure and test Azure AD single sign-on with O.C.</span></span> <span data-ttu-id="f98ca-152">Tan - AppreciateHub op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="f98ca-152">Tanner - AppreciateHub based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f98ca-153">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de equivalente gebruiker in O.C.</span><span class="sxs-lookup"><span data-stu-id="f98ca-153">For single sign-on to work, Azure AD needs to know what the counterpart user in O.C.</span></span> <span data-ttu-id="f98ca-154">Tan - AppreciateHub is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f98ca-154">Tanner - AppreciateHub is to a user in Azure AD.</span></span> <span data-ttu-id="f98ca-155">Met andere woorden, een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in O.C.</span><span class="sxs-lookup"><span data-stu-id="f98ca-155">In other words, a link relationship between an Azure AD user and the related user in O.C.</span></span> <span data-ttu-id="f98ca-156">Tan - AppreciateHub moet tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="f98ca-156">Tanner - AppreciateHub needs to be established.</span></span>

<span data-ttu-id="f98ca-157">In O.C.</span><span class="sxs-lookup"><span data-stu-id="f98ca-157">In O.C.</span></span> <span data-ttu-id="f98ca-158">Tan - AppreciateHub, wijs de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="f98ca-158">Tanner - AppreciateHub, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f98ca-159">Configureren en testen Azure AD eenmalige aanmelding met O.C.</span><span class="sxs-lookup"><span data-stu-id="f98ca-159">To configure and test Azure AD single sign-on with O.C.</span></span> <span data-ttu-id="f98ca-160">Tan - AppreciateHub, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="f98ca-160">Tanner - AppreciateHub, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f98ca-161">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f98ca-161">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f98ca-162">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f98ca-162">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f98ca-163">**[Maken van een O.C. Tan - testgebruiker AppreciateHub](#creating-a-oc-tanner---appreciatehub-test-user)**  - met een exemplaar van Britta Simon O.C.</span><span class="sxs-lookup"><span data-stu-id="f98ca-163">**[Creating a O.C. Tanner - AppreciateHub test user](#creating-a-oc-tanner---appreciatehub-test-user)** - to have a counterpart of Britta Simon in O.C.</span></span> <span data-ttu-id="f98ca-164">Tan - AppreciateHub die is gekoppeld aan de Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="f98ca-164">Tanner - AppreciateHub that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f98ca-165">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="f98ca-165">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f98ca-166">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="f98ca-166">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f98ca-167">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="f98ca-167">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f98ca-168">In deze sectie kunt u Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw O.C. configureren</span><span class="sxs-lookup"><span data-stu-id="f98ca-168">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your O.C.</span></span> <span data-ttu-id="f98ca-169">Tan - AppreciateHub toepassing.</span><span class="sxs-lookup"><span data-stu-id="f98ca-169">Tanner - AppreciateHub application.</span></span>

<span data-ttu-id="f98ca-170">**Eenmalige aanmelding Azure AD configureren met O.C. Tan - AppreciateHub, voer de volgende stappen uit:**</span><span class="sxs-lookup"><span data-stu-id="f98ca-170">**To configure Azure AD single sign-on with O.C. Tanner - AppreciateHub, perform the following steps:**</span></span>

1. <span data-ttu-id="f98ca-171">In de Azure-portal op de **O.C. Tan - AppreciateHub** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="f98ca-171">In the Azure portal, on the **O.C. Tanner - AppreciateHub** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="f98ca-173">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="f98ca-173">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_samlbase.png)

3. <span data-ttu-id="f98ca-175">Op de **O.C. Tan - URL's en AppreciateHub domein** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="f98ca-175">On the **O.C. Tanner - AppreciateHub Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_url.png)

    <span data-ttu-id="f98ca-177">a.</span><span class="sxs-lookup"><span data-stu-id="f98ca-177">a.</span></span> <span data-ttu-id="f98ca-178">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://<companyname>.appreciatehub.com/fed/sp/authnResponse20`</span><span class="sxs-lookup"><span data-stu-id="f98ca-178">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.appreciatehub.com/fed/sp/authnResponse20`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f98ca-179">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="f98ca-179">This value is not real.</span></span> <span data-ttu-id="f98ca-180">Deze waarde bijwerken met de werkelijke antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="f98ca-180">Update this value with the actual Reply URL.</span></span> <span data-ttu-id="f98ca-181">Neem contact op met [O.C. Tan - ondersteuningsteam AppreciateHub](mailto:sso@octanner.com) deze waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="f98ca-181">Contact [O.C. Tanner - AppreciateHub support team](mailto:sso@octanner.com) to get this value.</span></span>

    <span data-ttu-id="f98ca-182">b.</span><span class="sxs-lookup"><span data-stu-id="f98ca-182">b.</span></span> <span data-ttu-id="f98ca-183">Open het bestand met metagegevens met de volgende koppeling: [https://fed.appreciatehub.com/fed/sp/metadata](https://fed.appreciatehub.com/fed/sp/metadata).</span><span class="sxs-lookup"><span data-stu-id="f98ca-183">Open the metadata file using the following link: [https://fed.appreciatehub.com/fed/sp/metadata](https://fed.appreciatehub.com/fed/sp/metadata).</span></span>
   
    <span data-ttu-id="f98ca-184">c.</span><span class="sxs-lookup"><span data-stu-id="f98ca-184">c.</span></span> <span data-ttu-id="f98ca-185">Zoek de **md:AssertionConsumerService** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="f98ca-185">Locate the **md:AssertionConsumerService** node.</span></span> 
   
    <span data-ttu-id="f98ca-186">d.</span><span class="sxs-lookup"><span data-stu-id="f98ca-186">d.</span></span> <span data-ttu-id="f98ca-187">Kopieer de waarde van de **locatie** kenmerk.</span><span class="sxs-lookup"><span data-stu-id="f98ca-187">Copy the value of the **Location** attribute.</span></span> 
   
    ![App-instellingen configureren][12]
   
    <span data-ttu-id="f98ca-189">e.</span><span class="sxs-lookup"><span data-stu-id="f98ca-189">e.</span></span> <span data-ttu-id="f98ca-190">In de **aanmelding op URL** textbox voorbij de waarde die u in de vorige stap hebt verkregen.</span><span class="sxs-lookup"><span data-stu-id="f98ca-190">In the **Sign On URL** textbox, past the value you have obtained in the previous step.</span></span>

4. <span data-ttu-id="f98ca-191">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="f98ca-191">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_certificate.png) 

5. <span data-ttu-id="f98ca-193">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="f98ca-193">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f98ca-195">Eenmalige aanmelding configureren op **O.C. Tan - AppreciateHub** zijde, moet u de gedownloade verzenden **Metadata XML** naar [O.C. Tan - ondersteuningsteam AppreciateHub](mailto:sso@octanner.com).</span><span class="sxs-lookup"><span data-stu-id="f98ca-195">To configure single sign-on on **O.C. Tanner - AppreciateHub** side, you need to send the downloaded **Metadata XML** to [O.C. Tanner - AppreciateHub support team](mailto:sso@octanner.com).</span></span>

> [!TIP]
> <span data-ttu-id="f98ca-196">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="f98ca-196">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f98ca-197">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="f98ca-197">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f98ca-198">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f98ca-198">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f98ca-199">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="f98ca-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="f98ca-200">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="f98ca-200">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="f98ca-202">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="f98ca-202">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f98ca-203">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="f98ca-203">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f98ca-205">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="f98ca-205">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f98ca-207">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f98ca-207">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f98ca-209">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="f98ca-209">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f98ca-211">a.</span><span class="sxs-lookup"><span data-stu-id="f98ca-211">a.</span></span> <span data-ttu-id="f98ca-212">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f98ca-212">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f98ca-213">b.</span><span class="sxs-lookup"><span data-stu-id="f98ca-213">b.</span></span> <span data-ttu-id="f98ca-214">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f98ca-214">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f98ca-215">c.</span><span class="sxs-lookup"><span data-stu-id="f98ca-215">c.</span></span> <span data-ttu-id="f98ca-216">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="f98ca-216">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f98ca-217">d.</span><span class="sxs-lookup"><span data-stu-id="f98ca-217">d.</span></span> <span data-ttu-id="f98ca-218">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="f98ca-218">Click **Create**.</span></span>
 
### <a name="creating-a-oc-tanner---appreciatehub-test-user"></a><span data-ttu-id="f98ca-219">Maken van een O.C.</span><span class="sxs-lookup"><span data-stu-id="f98ca-219">Creating a O.C.</span></span> <span data-ttu-id="f98ca-220">Tan - AppreciateHub testgebruiker</span><span class="sxs-lookup"><span data-stu-id="f98ca-220">Tanner - AppreciateHub test user</span></span>

<span data-ttu-id="f98ca-221">Het doel van deze sectie is het maken van een gebruiker Britta Simon aangeroepen in O.C.</span><span class="sxs-lookup"><span data-stu-id="f98ca-221">The objective of this section is to create a user called Britta Simon in O.C.</span></span> <span data-ttu-id="f98ca-222">Tan - AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="f98ca-222">Tanner - AppreciateHub.</span></span>

<span data-ttu-id="f98ca-223">**Een gebruiker Britta Simon aangeroepen in O.C. maken Tan - AppreciateHub, voer de volgende stappen uit:**</span><span class="sxs-lookup"><span data-stu-id="f98ca-223">**To create a user called Britta Simon in O.C. Tanner - AppreciateHub, perform the following steps:**</span></span>

<span data-ttu-id="f98ca-224">Vraag uw [O.C. Tan - ondersteuningsteam AppreciateHub](mailto:sso@octanner.com) voor het maken van een gebruiker die als nameID kenmerk dezelfde waarde als de gebruikersnaam van Britta Simon in Azure AD heeft.</span><span class="sxs-lookup"><span data-stu-id="f98ca-224">Ask your [O.C. Tanner - AppreciateHub support team](mailto:sso@octanner.com) to create a user that has as nameID attribute the same value as the user name of Britta Simon in Azure AD.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f98ca-225">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="f98ca-225">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f98ca-226">In deze sectie maakt inschakelen u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan O.C.</span><span class="sxs-lookup"><span data-stu-id="f98ca-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to O.C.</span></span> <span data-ttu-id="f98ca-227">Tan - AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="f98ca-227">Tanner - AppreciateHub.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="f98ca-229">**Britta Simon toewijzen aan O.C. Tan - AppreciateHub, voer de volgende stappen uit:**</span><span class="sxs-lookup"><span data-stu-id="f98ca-229">**To assign Britta Simon to O.C. Tanner - AppreciateHub, perform the following steps:**</span></span>

1. <span data-ttu-id="f98ca-230">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f98ca-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="f98ca-232">Selecteer in de lijst met toepassingen **O.C. Tan - AppreciateHub**.</span><span class="sxs-lookup"><span data-stu-id="f98ca-232">In the applications list, select **O.C. Tanner - AppreciateHub**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_app.png) 

3. <span data-ttu-id="f98ca-234">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="f98ca-234">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="f98ca-236">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="f98ca-236">Click **Add** button.</span></span> <span data-ttu-id="f98ca-237">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f98ca-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="f98ca-239">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="f98ca-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f98ca-240">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f98ca-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f98ca-241">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f98ca-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f98ca-242">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f98ca-242">Testing single sign-on</span></span>

<span data-ttu-id="f98ca-243">Het doel van deze sectie is het testen van uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="f98ca-243">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="f98ca-244">Wanneer u klikt op de O.C.</span><span class="sxs-lookup"><span data-stu-id="f98ca-244">When you click the O.C.</span></span> <span data-ttu-id="f98ca-245">Tan - tegel in het deelvenster toegang AppreciateHub u moet ophalen automatisch aangemeld bij uw O.C.</span><span class="sxs-lookup"><span data-stu-id="f98ca-245">Tanner - AppreciateHub tile in the Access Panel, you should get automatically signed-on to your O.C.</span></span> <span data-ttu-id="f98ca-246">Tan - AppreciateHub toepassing.</span><span class="sxs-lookup"><span data-stu-id="f98ca-246">Tanner - AppreciateHub application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f98ca-247">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="f98ca-247">Additional resources</span></span>

* [<span data-ttu-id="f98ca-248">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f98ca-248">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f98ca-249">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f98ca-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_04.png

[12]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_octanner_08.png

[100]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_203.png

