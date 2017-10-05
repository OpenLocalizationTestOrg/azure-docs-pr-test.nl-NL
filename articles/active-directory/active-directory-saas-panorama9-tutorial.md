---
title: 'Zelfstudie: Azure Active Directory-integratie met Panorama9 | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Panorama9.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5e28d7fa-03be-49f3-96c8-b567f1257d44
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 934c0743464fd32398071aa3d07f7af76fdf7e3b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-panorama9"></a><span data-ttu-id="b8525-103">Zelfstudie: Azure Active Directory-integratie met Panorama9</span><span class="sxs-lookup"><span data-stu-id="b8525-103">Tutorial: Azure Active Directory integration with Panorama9</span></span>

<span data-ttu-id="b8525-104">In deze zelfstudie leert u hoe Panorama9 integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b8525-104">In this tutorial, you learn how to integrate Panorama9 with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b8525-105">Panorama9 integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="b8525-105">Integrating Panorama9 with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b8525-106">U kunt beheren in Azure AD die toegang tot Panorama9 heeft</span><span class="sxs-lookup"><span data-stu-id="b8525-106">You can control in Azure AD who has access to Panorama9</span></span>
- <span data-ttu-id="b8525-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Panorama9 inschakelen (Single Sign-On) met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="b8525-107">You can enable your users to automatically get signed-on to Panorama9 (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b8525-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="b8525-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b8525-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b8525-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b8525-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="b8525-110">Prerequisites</span></span>

<span data-ttu-id="b8525-111">Voor het configureren van Azure AD-integratie met Panorama9, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="b8525-111">To configure Azure AD integration with Panorama9, you need the following items:</span></span>

- <span data-ttu-id="b8525-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="b8525-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b8525-113">Een Panorama9 eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="b8525-113">A Panorama9 single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b8525-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="b8525-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b8525-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="b8525-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b8525-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="b8525-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b8525-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b8525-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b8525-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="b8525-118">Scenario description</span></span>
<span data-ttu-id="b8525-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="b8525-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b8525-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="b8525-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b8525-121">Panorama9 uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="b8525-121">Adding Panorama9 from the gallery</span></span>
2. <span data-ttu-id="b8525-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b8525-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-panorama9-from-the-gallery"></a><span data-ttu-id="b8525-123">Panorama9 uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="b8525-123">Adding Panorama9 from the gallery</span></span>
<span data-ttu-id="b8525-124">Voor het configureren van de integratie van Panorama9 in Azure AD, moet u Panorama9 uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="b8525-124">To configure the integration of Panorama9 into Azure AD, you need to add Panorama9 from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b8525-125">**Als u wilt toevoegen Panorama9 uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b8525-125">**To add Panorama9 from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b8525-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="b8525-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b8525-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b8525-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b8525-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b8525-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="b8525-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b8525-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="b8525-133">Typ in het zoekvak **Panorama9**.</span><span class="sxs-lookup"><span data-stu-id="b8525-133">In the search box, type **Panorama9**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_search.png)

5. <span data-ttu-id="b8525-135">Selecteer in het deelvenster resultaten **Panorama9**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="b8525-135">In the results panel, select **Panorama9**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b8525-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b8525-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="b8525-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Panorama9 op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="b8525-138">In this section, you configure and test Azure AD single sign-on with Panorama9 based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b8525-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Panorama9 is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b8525-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Panorama9 is to a user in Azure AD.</span></span> <span data-ttu-id="b8525-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Panorama9 tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="b8525-140">In other words, a link relationship between an Azure AD user and the related user in Panorama9 needs to be established.</span></span>

<span data-ttu-id="b8525-141">Wijs in Panorama9, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="b8525-141">In Panorama9, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b8525-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Panorama9, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="b8525-142">To configure and test Azure AD single sign-on with Panorama9, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b8525-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b8525-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b8525-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b8525-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b8525-145">**[Maken van een testgebruiker Panorama9](#creating-a-panorama9-test-user)**  - Panorama9 die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="b8525-145">**[Creating a Panorama9 test user](#creating-a-panorama9-test-user)** - to have a counterpart of Britta Simon in Panorama9 that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b8525-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="b8525-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b8525-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="b8525-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b8525-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="b8525-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b8525-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Panorama9 configureren.</span><span class="sxs-lookup"><span data-stu-id="b8525-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Panorama9 application.</span></span>

<span data-ttu-id="b8525-150">**Voor het configureren van Azure AD eenmalige aanmelding met Panorama9, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b8525-150">**To configure Azure AD single sign-on with Panorama9, perform the following steps:**</span></span>

1. <span data-ttu-id="b8525-151">In de Azure-portal op de **Panorama9** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="b8525-151">In the Azure portal, on the **Panorama9** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="b8525-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="b8525-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_samlbase.png)

3. <span data-ttu-id="b8525-155">Op de **Panorama9 domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="b8525-155">On the **Panorama9 Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_url.png)

    <span data-ttu-id="b8525-157">a.</span><span class="sxs-lookup"><span data-stu-id="b8525-157">a.</span></span> <span data-ttu-id="b8525-158">In de **aanmeldings-URL** textbox, typ een URL als:`https://dashboard.panorama9.com/saml/access/3262`</span><span class="sxs-lookup"><span data-stu-id="b8525-158">In the **Sign-on URL** textbox, type a URL as: `https://dashboard.panorama9.com/saml/access/3262`</span></span>

    <span data-ttu-id="b8525-159">b.</span><span class="sxs-lookup"><span data-stu-id="b8525-159">b.</span></span> <span data-ttu-id="b8525-160">In de **id** textbox, typ een URL met het volgende patroon volgen:`http://www.panorama9.com/saml20/<tenant-name>`</span><span class="sxs-lookup"><span data-stu-id="b8525-160">In the **Identifier** textbox, type a URL using the following pattern: `http://www.panorama9.com/saml20/<tenant-name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b8525-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="b8525-161">These values are not real.</span></span> <span data-ttu-id="b8525-162">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="b8525-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="b8525-163">Neem contact op met [Panorama9 Client ondersteuningsteam](https://support.panorama9.com) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="b8525-163">Contact [Panorama9 Client support team](https://support.panorama9.com) to get these values.</span></span> 
 
4. <span data-ttu-id="b8525-164">Op de **SAML-certificaat voor ondertekening van** sectie, Kopieer de **VINGERAFDRUK** waarde van het certificaat.</span><span class="sxs-lookup"><span data-stu-id="b8525-164">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_certificate.png) 

5. <span data-ttu-id="b8525-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="b8525-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-panorama9-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b8525-168">Op de **Panorama9 configuratie** sectie, klikt u op **configureren Panorama9** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="b8525-168">On the **Panorama9 Configuration** section, click **Configure Panorama9** to open **Configure sign-on** window.</span></span> <span data-ttu-id="b8525-169">Kopieer de **SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="b8525-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_configure.png) 

5. <span data-ttu-id="b8525-171">In een ander browservenster, meld u bij uw bedrijf Panorama9 site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="b8525-171">In a different web browser window, log into your Panorama9 company site as an administrator.</span></span>

6. <span data-ttu-id="b8525-172">Klik in de werkbalk bovenaan op **beheren**, en klik vervolgens op **extensies**.</span><span class="sxs-lookup"><span data-stu-id="b8525-172">In the toolbar on the top, click **Manage**, and then click **Extensions**.</span></span>
   
   <span data-ttu-id="b8525-173">![Extensies](./media/active-directory-saas-panorama9-tutorial/ic790023.png "extensies")</span><span class="sxs-lookup"><span data-stu-id="b8525-173">![Extensions](./media/active-directory-saas-panorama9-tutorial/ic790023.png "Extensions")</span></span>
7. <span data-ttu-id="b8525-174">Op de **extensies** dialoogvenster, klikt u op **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="b8525-174">On the **Extensions** dialog, click **Single Sign-On**.</span></span>
   
   <span data-ttu-id="b8525-175">![Eenmalige aanmelding](./media/active-directory-saas-panorama9-tutorial/ic790024.png "eenmalige aanmelding")</span><span class="sxs-lookup"><span data-stu-id="b8525-175">![Single Sign-On](./media/active-directory-saas-panorama9-tutorial/ic790024.png "Single Sign-On")</span></span>
8. <span data-ttu-id="b8525-176">In de **instellingen** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="b8525-176">In the **Settings** section, perform the following steps:</span></span>
   
   <span data-ttu-id="b8525-177">![Instellingen](./media/active-directory-saas-panorama9-tutorial/ic790025.png "instellingen")</span><span class="sxs-lookup"><span data-stu-id="b8525-177">![Settings](./media/active-directory-saas-panorama9-tutorial/ic790025.png "Settings")</span></span>
   
    <span data-ttu-id="b8525-178">a.</span><span class="sxs-lookup"><span data-stu-id="b8525-178">a.</span></span> <span data-ttu-id="b8525-179">In **identiteit provider URL** textbox, plak de waarde van **Single Sign-On Service-URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="b8525-179">In **Identity provider URL** textbox, paste the value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="b8525-180">b.</span><span class="sxs-lookup"><span data-stu-id="b8525-180">b.</span></span> <span data-ttu-id="b8525-181">In **vingerafdruk van certificaat** textbox, plak de **vingerafdruk** waarde van het certificaat dat u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="b8525-181">In **Certificate fingerprint** textbox, paste the **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span>    
         
9. <span data-ttu-id="b8525-182">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="b8525-182">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="b8525-183">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="b8525-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b8525-184">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="b8525-184">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b8525-185">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b8525-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b8525-186">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="b8525-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="b8525-187">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="b8525-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="b8525-189">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b8525-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b8525-190">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="b8525-190">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-panorama9-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b8525-192">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="b8525-192">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-panorama9-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b8525-194">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b8525-194">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-panorama9-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b8525-196">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="b8525-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-panorama9-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b8525-198">a.</span><span class="sxs-lookup"><span data-stu-id="b8525-198">a.</span></span> <span data-ttu-id="b8525-199">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b8525-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b8525-200">b.</span><span class="sxs-lookup"><span data-stu-id="b8525-200">b.</span></span> <span data-ttu-id="b8525-201">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b8525-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b8525-202">c.</span><span class="sxs-lookup"><span data-stu-id="b8525-202">c.</span></span> <span data-ttu-id="b8525-203">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="b8525-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b8525-204">d.</span><span class="sxs-lookup"><span data-stu-id="b8525-204">d.</span></span> <span data-ttu-id="b8525-205">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="b8525-205">Click **Create**.</span></span>
 
### <a name="creating-a-panorama9-test-user"></a><span data-ttu-id="b8525-206">Een testgebruiker Panorama9 maken</span><span class="sxs-lookup"><span data-stu-id="b8525-206">Creating a Panorama9 test user</span></span>

<span data-ttu-id="b8525-207">Om in te schakelen gebruikers van Azure AD aan te melden bij Panorama9, moeten ze worden ingericht in Panorama9.</span><span class="sxs-lookup"><span data-stu-id="b8525-207">In order to enable Azure AD users to log into Panorama9, they must be provisioned into Panorama9.</span></span>  

<span data-ttu-id="b8525-208">In het geval van Panorama9 is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="b8525-208">In the case of Panorama9, provisioning is a manual task.</span></span>

<span data-ttu-id="b8525-209">**Als u wilt configureren voor gebruikers inrichten, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b8525-209">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="b8525-210">Meld u aan bij uw **Panorama9** bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="b8525-210">Log in to your **Panorama9** company site as an administrator.</span></span>

2. <span data-ttu-id="b8525-211">Klik in het menu bovenaan op **beheren**, en klik vervolgens op **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="b8525-211">In the menu on the top, click **Manage**, and then click **Users**.</span></span>
   
  <span data-ttu-id="b8525-212">![Gebruikers](./media/active-directory-saas-panorama9-tutorial/ic790027.png "gebruikers")</span><span class="sxs-lookup"><span data-stu-id="b8525-212">![Users](./media/active-directory-saas-panorama9-tutorial/ic790027.png "Users")</span></span>

3. <span data-ttu-id="b8525-213">Klik in de sectie gebruikers  **+**  nieuwe gebruiker toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="b8525-213">In the Users section, Click **+** to add new user.</span></span>

 <span data-ttu-id="b8525-214">![Gebruikers](./media/active-directory-saas-panorama9-tutorial/ic790028.png "gebruikers")</span><span class="sxs-lookup"><span data-stu-id="b8525-214">![Users](./media/active-directory-saas-panorama9-tutorial/ic790028.png "Users")</span></span>

4. <span data-ttu-id="b8525-215">Ga naar de gebruiker gegevenssectie, typt u het e-mailadres van een geldige Azure Active Directory-gebruiker die u inrichten wilt in de **e** textbox.</span><span class="sxs-lookup"><span data-stu-id="b8525-215">Go to the User data section, type the email address of a valid Azure Active Directory user you want to provision into the **Email** textbox.</span></span>

5. <span data-ttu-id="b8525-216">Ga naar de sectie gebruikers, klikt u op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="b8525-216">Come to the Users section, Click **Save**.</span></span>
   
> [!NOTE]
    > <span data-ttu-id="b8525-217">De houder van Azure Active Directory-account ontvangt een e-mailbericht en volgt een koppeling om hun account te bevestigen voordat deze geactiveerd wordt.</span><span class="sxs-lookup"><span data-stu-id="b8525-217">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b8525-218">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="b8525-218">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b8525-219">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Panorama9.</span><span class="sxs-lookup"><span data-stu-id="b8525-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Panorama9.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="b8525-221">**Britta Simon om aan te wijzen Panorama9, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b8525-221">**To assign Britta Simon to Panorama9, perform the following steps:**</span></span>

1. <span data-ttu-id="b8525-222">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b8525-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="b8525-224">Selecteer in de lijst met toepassingen **Panorama9**.</span><span class="sxs-lookup"><span data-stu-id="b8525-224">In the applications list, select **Panorama9**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_app.png) 

3. <span data-ttu-id="b8525-226">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="b8525-226">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="b8525-228">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="b8525-228">Click **Add** button.</span></span> <span data-ttu-id="b8525-229">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b8525-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="b8525-231">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="b8525-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b8525-232">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b8525-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b8525-233">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b8525-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b8525-234">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b8525-234">Testing single sign-on</span></span>

<span data-ttu-id="b8525-235">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="b8525-235">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b8525-236">Als u op de tegel Panorama9 in het deelvenster toegang, u moet ophalen automatisch aangemeld bij Panorama9 toepassing.</span><span class="sxs-lookup"><span data-stu-id="b8525-236">When you click the Panorama9 tile in the Access Panel, you should get automatically signed-on to Panorama9 application.</span></span>
<span data-ttu-id="b8525-237">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b8525-237">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b8525-238">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="b8525-238">Additional resources</span></span>

* [<span data-ttu-id="b8525-239">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b8525-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b8525-240">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b8525-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_203.png

