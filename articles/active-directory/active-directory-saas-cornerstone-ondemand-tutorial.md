---
title: 'Zelfstudie: Azure Active Directory-integratie met basis OnDemand | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en basis OnDemand.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f57c5fef-49b0-4591-91ef-fc0de6d654ab
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 8bb32588579a0d40b9ae7e0f823c6daab21c856e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cornerstone-ondemand"></a><span data-ttu-id="59b8f-103">Zelfstudie: Azure Active Directory-integratie met basis OnDemand</span><span class="sxs-lookup"><span data-stu-id="59b8f-103">Tutorial: Azure Active Directory integration with Cornerstone OnDemand</span></span>

<span data-ttu-id="59b8f-104">In deze zelfstudie leert u hoe basis OnDemand integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="59b8f-104">In this tutorial, you learn how to integrate Cornerstone OnDemand with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="59b8f-105">Basis OnDemand integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="59b8f-105">Integrating Cornerstone OnDemand with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="59b8f-106">U kunt beheren in Azure AD die toegang tot basis OnDemand heeft</span><span class="sxs-lookup"><span data-stu-id="59b8f-106">You can control in Azure AD who has access to Cornerstone OnDemand</span></span>
- <span data-ttu-id="59b8f-107">U kunt uw gebruikers automatisch ophalen aangemeld bij basis OnDemand (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="59b8f-107">You can enable your users to automatically get signed-on to Cornerstone OnDemand (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="59b8f-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="59b8f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="59b8f-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="59b8f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="59b8f-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="59b8f-110">Prerequisites</span></span>

<span data-ttu-id="59b8f-111">Voor het configureren van Azure AD-integratie met basis OnDemand, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="59b8f-111">To configure Azure AD integration with Cornerstone OnDemand, you need the following items:</span></span>

- <span data-ttu-id="59b8f-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="59b8f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="59b8f-113">Een basis OnDemand eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="59b8f-113">A Cornerstone OnDemand single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="59b8f-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="59b8f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="59b8f-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="59b8f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="59b8f-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="59b8f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="59b8f-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="59b8f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="59b8f-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="59b8f-118">Scenario description</span></span>
<span data-ttu-id="59b8f-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="59b8f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="59b8f-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="59b8f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="59b8f-121">Basis OnDemand uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="59b8f-121">Adding Cornerstone OnDemand from the gallery</span></span>
2. <span data-ttu-id="59b8f-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="59b8f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cornerstone-ondemand-from-the-gallery"></a><span data-ttu-id="59b8f-123">Basis OnDemand uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="59b8f-123">Adding Cornerstone OnDemand from the gallery</span></span>
<span data-ttu-id="59b8f-124">Voor het configureren van de integratie van basis OnDemand in Azure AD, moet u basis OnDemand uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="59b8f-124">To configure the integration of Cornerstone OnDemand into Azure AD, you need to add Cornerstone OnDemand from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="59b8f-125">**Als u wilt toevoegen basis OnDemand uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="59b8f-125">**To add Cornerstone OnDemand from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="59b8f-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="59b8f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="59b8f-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="59b8f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="59b8f-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="59b8f-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="59b8f-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="59b8f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="59b8f-133">Typ in het zoekvak **basis OnDemand**.</span><span class="sxs-lookup"><span data-stu-id="59b8f-133">In the search box, type **Cornerstone OnDemand**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_search.png)

5. <span data-ttu-id="59b8f-135">Selecteer in het deelvenster resultaten **basis OnDemand**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="59b8f-135">In the results panel, select **Cornerstone OnDemand**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="59b8f-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="59b8f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="59b8f-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met basis OnDemand op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="59b8f-138">In this section, you configure and test Azure AD single sign-on with Cornerstone OnDemand based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="59b8f-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in basis OnDemand is aan een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="59b8f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Cornerstone OnDemand is to a user in Azure AD.</span></span> <span data-ttu-id="59b8f-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in basis OnDemand tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="59b8f-140">In other words, a link relationship between an Azure AD user and the related user in Cornerstone OnDemand needs to be established.</span></span>

<span data-ttu-id="59b8f-141">Wijs in basis OnDemand, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="59b8f-141">In Cornerstone OnDemand, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="59b8f-142">Om te configureren en testen van Azure AD eenmalige aanmelding met basis OnDemand, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="59b8f-142">To configure and test Azure AD single sign-on with Cornerstone OnDemand, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="59b8f-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="59b8f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="59b8f-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="59b8f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="59b8f-145">**[Maken van een basis OnDemand testgebruiker](#creating-a-cornerstone-ondemand-test-user)**  - basis OnDemand die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="59b8f-145">**[Creating a Cornerstone OnDemand test user](#creating-a-cornerstone-ondemand-test-user)** - to have a counterpart of Britta Simon in Cornerstone OnDemand that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="59b8f-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="59b8f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="59b8f-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="59b8f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="59b8f-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="59b8f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="59b8f-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing basis OnDemand configureren.</span><span class="sxs-lookup"><span data-stu-id="59b8f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Cornerstone OnDemand application.</span></span>

<span data-ttu-id="59b8f-150">**Voor het configureren van Azure AD eenmalige aanmelding met basis OnDemand, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="59b8f-150">**To configure Azure AD single sign-on with Cornerstone OnDemand, perform the following steps:**</span></span>

1. <span data-ttu-id="59b8f-151">In de Azure-portal op de **basis OnDemand** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="59b8f-151">In the Azure portal, on the **Cornerstone OnDemand** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="59b8f-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="59b8f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_samlbase.png)

3. <span data-ttu-id="59b8f-155">Op de **basis OnDemand domein en de URL's** sectie, voert u de volgende stap:</span><span class="sxs-lookup"><span data-stu-id="59b8f-155">On the **Cornerstone OnDemand Domain and URLs** section, perform the following step:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_url.png)

    <span data-ttu-id="59b8f-157">a.</span><span class="sxs-lookup"><span data-stu-id="59b8f-157">a.</span></span> <span data-ttu-id="59b8f-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<company>.csod.com`</span><span class="sxs-lookup"><span data-stu-id="59b8f-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company>.csod.com`</span></span>

    <span data-ttu-id="59b8f-159">b.</span><span class="sxs-lookup"><span data-stu-id="59b8f-159">b.</span></span> <span data-ttu-id="59b8f-160">In **id** textbox, typ een URL met het volgende patroon volgen:`https://<company>.csod.com`</span><span class="sxs-lookup"><span data-stu-id="59b8f-160">In **Identifier** textbox, type a URL using the following pattern: `https://<company>.csod.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="59b8f-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="59b8f-161">These values are not real.</span></span> <span data-ttu-id="59b8f-162">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="59b8f-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="59b8f-163">Neem contact op met [basis OnDemand Client ondersteuningsteam](mailTo:moreinfo@csod.com) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="59b8f-163">Contact [Cornerstone OnDemand Client support team](mailTo:moreinfo@csod.com) to get these values.</span></span> 
 
4. <span data-ttu-id="59b8f-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="59b8f-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_certificate.png) 

5. <span data-ttu-id="59b8f-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="59b8f-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="59b8f-168">Op de **basis OnDemand configuratie** sectie, klikt u op **configureren basis OnDemand** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="59b8f-168">On the **Cornerstone OnDemand Configuration** section, click **Configure Cornerstone OnDemand** to open **Configure sign-on** window.</span></span> <span data-ttu-id="59b8f-169">Kopieer de **Sign-Out URL's en SAML Single Sign-On Service** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="59b8f-169">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_configure.png) 

7. <span data-ttu-id="59b8f-171">Eenmalige aanmelding configureren op **basis OnDemand** zijde, moet u de gedownloade verzenden **certificaat**, **Sign-Out URL** en **SAML Single Sign-On Service-URL** naar [ondersteuningsteam voor OnDemand basis](mailTo:moreinfo@csod.com).</span><span class="sxs-lookup"><span data-stu-id="59b8f-171">To configure single sign-on on **Cornerstone OnDemand** side, you need to send the downloaded **Certificate**, **Sign-Out URL** and **SAML Single Sign-On Service URL**  to [Cornerstone OnDemand support team](mailTo:moreinfo@csod.com).</span></span> <span data-ttu-id="59b8f-172">Ze deze instelling zodat de SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="59b8f-172">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="59b8f-173">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="59b8f-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="59b8f-174">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="59b8f-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="59b8f-175">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="59b8f-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="59b8f-176">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="59b8f-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="59b8f-177">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="59b8f-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="59b8f-179">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="59b8f-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="59b8f-180">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="59b8f-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cornerstone-ondemand-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="59b8f-182">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="59b8f-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cornerstone-ondemand-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="59b8f-184">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="59b8f-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cornerstone-ondemand-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="59b8f-186">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="59b8f-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cornerstone-ondemand-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="59b8f-188">a.</span><span class="sxs-lookup"><span data-stu-id="59b8f-188">a.</span></span> <span data-ttu-id="59b8f-189">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="59b8f-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="59b8f-190">b.</span><span class="sxs-lookup"><span data-stu-id="59b8f-190">b.</span></span> <span data-ttu-id="59b8f-191">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="59b8f-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="59b8f-192">c.</span><span class="sxs-lookup"><span data-stu-id="59b8f-192">c.</span></span> <span data-ttu-id="59b8f-193">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="59b8f-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="59b8f-194">d.</span><span class="sxs-lookup"><span data-stu-id="59b8f-194">d.</span></span> <span data-ttu-id="59b8f-195">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="59b8f-195">Click **Create**.</span></span>
 
### <a name="creating-a-cornerstone-ondemand-test-user"></a><span data-ttu-id="59b8f-196">Maken van een basis OnDemand testgebruiker</span><span class="sxs-lookup"><span data-stu-id="59b8f-196">Creating a Cornerstone OnDemand test user</span></span>

<span data-ttu-id="59b8f-197">Om in te schakelen gebruikers van Azure AD aan te melden bij basis OnDemand, moeten ze worden ingericht in basis OnDemand.</span><span class="sxs-lookup"><span data-stu-id="59b8f-197">In order to enable Azure AD users to log into Cornerstone OnDemand, they must be provisioned into Cornerstone OnDemand.</span></span> <span data-ttu-id="59b8f-198">In het geval van een basis-OnDemand is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="59b8f-198">In the case of Cornerstone OnDemand, provisioning is a manual task.</span></span>

<span data-ttu-id="59b8f-199">Als u wilt configureren voor gebruikers inrichten, verzendt de gegevens (bijvoorbeeld: naam, e) over de Azure AD-gebruiker u wilt inrichten op de [ondersteuningsteam voor OnDemand basis](mailTo:moreinfo@csod.com).</span><span class="sxs-lookup"><span data-stu-id="59b8f-199">To configure user provisioning, send the information (e.g.: Name, Email) about the Azure AD user you want to provision to the [Cornerstone OnDemand support team](mailTo:moreinfo@csod.com).</span></span>

>[!NOTE]
><span data-ttu-id="59b8f-200">U kunt een andere basis OnDemand gebruiker account hulpmiddelen voor het maken of API's die is geleverd door basis OnDemand aan inrichten AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="59b8f-200">You can use any other Cornerstone OnDemand user account creation tools or APIs provided by Cornerstone OnDemand to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="59b8f-201">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="59b8f-201">Assigning the Azure AD test user</span></span>

<span data-ttu-id="59b8f-202">In deze sectie maakt inschakelen u Britta Simon Azure eenmalige aanmelding gebruiken door het verlenen van toegang aan de basis OnDemand.</span><span class="sxs-lookup"><span data-stu-id="59b8f-202">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Cornerstone OnDemand.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="59b8f-204">**Britta Simon om aan te wijzen basis OnDemand, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="59b8f-204">**To assign Britta Simon to Cornerstone OnDemand, perform the following steps:**</span></span>

1. <span data-ttu-id="59b8f-205">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="59b8f-205">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="59b8f-207">Selecteer in de lijst met toepassingen **basis OnDemand**.</span><span class="sxs-lookup"><span data-stu-id="59b8f-207">In the applications list, select **Cornerstone OnDemand**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_app.png) 

3. <span data-ttu-id="59b8f-209">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="59b8f-209">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="59b8f-211">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="59b8f-211">Click **Add** button.</span></span> <span data-ttu-id="59b8f-212">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="59b8f-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="59b8f-214">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="59b8f-214">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="59b8f-215">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="59b8f-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="59b8f-216">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="59b8f-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="59b8f-217">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="59b8f-217">Testing single sign-on</span></span>

<span data-ttu-id="59b8f-218">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="59b8f-218">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="59b8f-219">Als u op de basis OnDemand-tegel in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw basis OnDemand-toepassing.</span><span class="sxs-lookup"><span data-stu-id="59b8f-219">When you click the Cornerstone OnDemand tile in the Access Panel, you should get automatically signed-on to your Cornerstone OnDemand application.</span></span>
<span data-ttu-id="59b8f-220">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="59b8f-220">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="59b8f-221">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="59b8f-221">Additional resources</span></span>

* [<span data-ttu-id="59b8f-222">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="59b8f-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="59b8f-223">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="59b8f-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_203.png

