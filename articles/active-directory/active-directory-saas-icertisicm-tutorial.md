---
title: 'Zelfstudie: Azure Active Directory-integratie met Icertis Contract beheerplatform | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Icertis Contract beheerplatform.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6627e6dd-f559-4cd4-a509-f6d9a4961b49
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 9dd002f71b7a960338071db869f7c8cf88071342
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-icertis-contract-management-platform"></a><span data-ttu-id="c80e2-103">Zelfstudie: Azure Active Directory-integratie met Icertis Contract beheerplatform</span><span class="sxs-lookup"><span data-stu-id="c80e2-103">Tutorial: Azure Active Directory integration with Icertis Contract Management Platform</span></span>

<span data-ttu-id="c80e2-104">In deze zelfstudie leert u hoe Icertis Contract beheerplatform integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c80e2-104">In this tutorial, you learn how to integrate Icertis Contract Management Platform with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c80e2-105">Platform voor het beheer van Contract Icertis integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="c80e2-105">Integrating Icertis Contract Management Platform with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c80e2-106">U kunt beheren in Azure AD die toegang tot Icertis Contract beheerplatform heeft</span><span class="sxs-lookup"><span data-stu-id="c80e2-106">You can control in Azure AD who has access to Icertis Contract Management Platform</span></span>
- <span data-ttu-id="c80e2-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Icertis Contract beheerplatform (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="c80e2-107">You can enable your users to automatically get signed-on to Icertis Contract Management Platform (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c80e2-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="c80e2-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c80e2-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c80e2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c80e2-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="c80e2-110">Prerequisites</span></span>

<span data-ttu-id="c80e2-111">Voor het configureren van Azure AD-integratie met Icertis Contract Management Platform, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="c80e2-111">To configure Azure AD integration with Icertis Contract Management Platform, you need the following items:</span></span>

- <span data-ttu-id="c80e2-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="c80e2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c80e2-113">Een Platform voor het beheer van Contract Icertis eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="c80e2-113">An Icertis Contract Management Platform single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c80e2-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="c80e2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c80e2-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="c80e2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c80e2-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="c80e2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c80e2-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c80e2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c80e2-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="c80e2-118">Scenario description</span></span>
<span data-ttu-id="c80e2-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="c80e2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c80e2-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="c80e2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c80e2-121">Platform voor het beheer van Contract Icertis uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="c80e2-121">Adding Icertis Contract Management Platform from the gallery</span></span>
2. <span data-ttu-id="c80e2-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="c80e2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-icertis-contract-management-platform-from-the-gallery"></a><span data-ttu-id="c80e2-123">Platform voor het beheer van Contract Icertis uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="c80e2-123">Adding Icertis Contract Management Platform from the gallery</span></span>
<span data-ttu-id="c80e2-124">Voor het configureren van de integratie van Icertis Contract beheerplatform in Azure AD, moet u Icertis Contract beheerplatform uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="c80e2-124">To configure the integration of Icertis Contract Management Platform into Azure AD, you need to add Icertis Contract Management Platform from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c80e2-125">**Als u wilt toevoegen Icertis Contract beheerplatform uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="c80e2-125">**To add Icertis Contract Management Platform from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c80e2-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="c80e2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c80e2-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c80e2-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c80e2-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c80e2-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="c80e2-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c80e2-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="c80e2-133">Typ in het zoekvak **Icertis Contract beheerplatform**.</span><span class="sxs-lookup"><span data-stu-id="c80e2-133">In the search box, type **Icertis Contract Management Platform**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_search.png)

5. <span data-ttu-id="c80e2-135">Selecteer in het deelvenster resultaten **Icertis Contract beheerplatform**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="c80e2-135">In the results panel, select **Icertis Contract Management Platform**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c80e2-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="c80e2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c80e2-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Icertis Contract Platform voor het beheer op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="c80e2-138">In this section, you configure and test Azure AD single sign-on with Icertis Contract Management Platform based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c80e2-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Icertis Contract beheerplatform is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c80e2-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Icertis Contract Management Platform is to a user in Azure AD.</span></span> <span data-ttu-id="c80e2-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in het beheerplatform voor Icertis Contract tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="c80e2-140">In other words, a link relationship between an Azure AD user and the related user in Icertis Contract Management Platform needs to be established.</span></span>

<span data-ttu-id="c80e2-141">Wijs in het beheerplatform Icertis Contract, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="c80e2-141">In Icertis Contract Management Platform, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c80e2-142">Als u wilt configureren en testen Azure AD eenmalige aanmelding met Icertis Contract Management Platform, moet u voltooien van de volgende elementen:</span><span class="sxs-lookup"><span data-stu-id="c80e2-142">To configure and test Azure AD single sign-on with Icertis Contract Management Platform, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c80e2-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c80e2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c80e2-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c80e2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c80e2-145">**[Maken van een testgebruiker Icertis Contract beheerplatform](#creating-an-icertis-contract-management-platform-test-user)**  - Icertis Contract beheerplatform die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="c80e2-145">**[Creating an Icertis Contract Management Platform test user](#creating-an-icertis-contract-management-platform-test-user)** - to have a counterpart of Britta Simon in Icertis Contract Management Platform that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c80e2-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="c80e2-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c80e2-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="c80e2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c80e2-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="c80e2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c80e2-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw toepassing Icertis Contract beheerplatform.</span><span class="sxs-lookup"><span data-stu-id="c80e2-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Icertis Contract Management Platform application.</span></span>

<span data-ttu-id="c80e2-150">**Voor het configureren van Azure AD eenmalige aanmelding met Icertis Contract Management Platform, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="c80e2-150">**To configure Azure AD single sign-on with Icertis Contract Management Platform, perform the following steps:**</span></span>

1. <span data-ttu-id="c80e2-151">In de Azure-portal op de **Icertis Contract beheerplatform** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="c80e2-151">In the Azure portal, on the **Icertis Contract Management Platform** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="c80e2-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="c80e2-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_samlbase.png)

3. <span data-ttu-id="c80e2-155">Op de **Icertis Contract beheerdomein Platform en URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="c80e2-155">On the **Icertis Contract Management Platform Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_url.png)

    <span data-ttu-id="c80e2-157">a.</span><span class="sxs-lookup"><span data-stu-id="c80e2-157">a.</span></span> <span data-ttu-id="c80e2-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<company name>.icertis.com`</span><span class="sxs-lookup"><span data-stu-id="c80e2-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.icertis.com`</span></span>

    <span data-ttu-id="c80e2-159">b.</span><span class="sxs-lookup"><span data-stu-id="c80e2-159">b.</span></span> <span data-ttu-id="c80e2-160">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<company name>.icertis.com`</span><span class="sxs-lookup"><span data-stu-id="c80e2-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.icertis.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c80e2-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="c80e2-161">These values are not real.</span></span> <span data-ttu-id="c80e2-162">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="c80e2-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c80e2-163">Neem contact op met [Icertis Contract Beheerclient Platform ondersteuningsteam](https://www.icertis.com/company/contact/) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="c80e2-163">Contact [Icertis Contract Management Platform Client support team](https://www.icertis.com/company/contact/) to get these values.</span></span> 

4. <span data-ttu-id="c80e2-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="c80e2-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_certificate.png) 

5. <span data-ttu-id="c80e2-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="c80e2-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-icertisicm-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c80e2-168">Op de **Icertis Contract Management platformconfiguratie** sectie, klikt u op **Icertis Contract beheerplatform configureren** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="c80e2-168">On the **Icertis Contract Management Platform Configuration** section, click **Configure Icertis Contract Management Platform** to open **Configure sign-on** window.</span></span> <span data-ttu-id="c80e2-169">Kopieer de **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="c80e2-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_configure.png) 

7. <span data-ttu-id="c80e2-171">Eenmalige aanmelding configureren op **Icertis Contract beheerplatform** zijde, moet u de gedownloade verzenden **Metadata XML** en **Sign-Out-URL, SAML entiteit-ID en eenmalige aanmelding SAML Service-URL** naar [Icertis Contract beheerplatform ondersteuningsteam](https://www.icertis.com/company/contact/).</span><span class="sxs-lookup"><span data-stu-id="c80e2-171">To configure single sign-on on **Icertis Contract Management Platform** side, you need to send the downloaded **Metadata XML** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Icertis Contract Management Platform support team](https://www.icertis.com/company/contact/).</span></span>

> [!TIP]
> <span data-ttu-id="c80e2-172">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="c80e2-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c80e2-173">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="c80e2-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c80e2-174">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c80e2-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c80e2-175">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="c80e2-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="c80e2-176">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="c80e2-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="c80e2-178">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="c80e2-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c80e2-179">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="c80e2-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-icertisicm-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c80e2-181">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="c80e2-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-icertisicm-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c80e2-183">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c80e2-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-icertisicm-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c80e2-185">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="c80e2-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-icertisicm-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c80e2-187">a.</span><span class="sxs-lookup"><span data-stu-id="c80e2-187">a.</span></span> <span data-ttu-id="c80e2-188">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c80e2-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c80e2-189">b.</span><span class="sxs-lookup"><span data-stu-id="c80e2-189">b.</span></span> <span data-ttu-id="c80e2-190">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c80e2-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c80e2-191">c.</span><span class="sxs-lookup"><span data-stu-id="c80e2-191">c.</span></span> <span data-ttu-id="c80e2-192">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="c80e2-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c80e2-193">d.</span><span class="sxs-lookup"><span data-stu-id="c80e2-193">d.</span></span> <span data-ttu-id="c80e2-194">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="c80e2-194">Click **Create**.</span></span>
 
### <a name="creating-an-icertis-contract-management-platform-test-user"></a><span data-ttu-id="c80e2-195">Maken van een Platform voor het beheer van Contract Icertis testgebruiker</span><span class="sxs-lookup"><span data-stu-id="c80e2-195">Creating an Icertis Contract Management Platform test user</span></span>

<span data-ttu-id="c80e2-196">In deze sectie maakt maakt u een gebruiker die Britta Simon aangeroepen in Icertis Contract beheerplatform.</span><span class="sxs-lookup"><span data-stu-id="c80e2-196">In this section, you create a user called Britta Simon in Icertis Contract Management Platform.</span></span> <span data-ttu-id="c80e2-197">Neem contact op met [Icertis Contract beheerplatform ondersteuningsteam](https://www.icertis.com/company/contact/) toevoegen van de gebruikers in het beheerplatform voor Icertis Contract.</span><span class="sxs-lookup"><span data-stu-id="c80e2-197">Please work with [Icertis Contract Management Platform support team](https://www.icertis.com/company/contact/) to add the users in the Icertis Contract Management Platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c80e2-198">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="c80e2-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c80e2-199">In deze sectie maakt inschakelen u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Icertis Contract beheerplatform.</span><span class="sxs-lookup"><span data-stu-id="c80e2-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Icertis Contract Management Platform.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="c80e2-201">**Britta Simon om aan te wijzen Icertis Contract beheerplatform, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="c80e2-201">**To assign Britta Simon to Icertis Contract Management Platform, perform the following steps:**</span></span>

1. <span data-ttu-id="c80e2-202">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c80e2-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="c80e2-204">Selecteer in de lijst met toepassingen **Icertis Contract beheerplatform**.</span><span class="sxs-lookup"><span data-stu-id="c80e2-204">In the applications list, select **Icertis Contract Management Platform**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_app.png) 

3. <span data-ttu-id="c80e2-206">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="c80e2-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="c80e2-208">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="c80e2-208">Click **Add** button.</span></span> <span data-ttu-id="c80e2-209">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c80e2-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="c80e2-211">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="c80e2-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c80e2-212">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c80e2-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c80e2-213">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c80e2-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c80e2-214">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="c80e2-214">Testing single sign-on</span></span>

<span data-ttu-id="c80e2-215">Het doel van deze sectie is het testen van uw Azure AD SSO-configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="c80e2-215">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="c80e2-216">Als u op de tegel Icertis Contract beheerplatform in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Icertis Contract beheerplatform.</span><span class="sxs-lookup"><span data-stu-id="c80e2-216">When you click the Icertis Contract Management Platform tile in the Access Panel, you should get automatically signed-on to your Icertis Contract Management Platform application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c80e2-217">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="c80e2-217">Additional resources</span></span>

* [<span data-ttu-id="c80e2-218">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c80e2-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c80e2-219">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c80e2-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_203.png

