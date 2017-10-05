---
title: 'Zelfstudie: Azure Active Directory-integratie met Workfront | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Workfront.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: aab8bd2f-f9dd-42da-a18e-d707865687d7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: f7ba8d4895474de0da0e04da5f31959963ae65ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workfront"></a><span data-ttu-id="6ee67-103">Zelfstudie: Azure Active Directory-integratie met Workfront</span><span class="sxs-lookup"><span data-stu-id="6ee67-103">Tutorial: Azure Active Directory integration with Workfront</span></span>

<span data-ttu-id="6ee67-104">In deze zelfstudie leert u hoe Workfront integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6ee67-104">In this tutorial, you learn how to integrate Workfront with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6ee67-105">Workfront integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="6ee67-105">Integrating Workfront with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6ee67-106">U kunt beheren in Azure AD die toegang tot Workfront heeft</span><span class="sxs-lookup"><span data-stu-id="6ee67-106">You can control in Azure AD who has access to Workfront</span></span>
- <span data-ttu-id="6ee67-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Workfront (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="6ee67-107">You can enable your users to automatically get signed-on to Workfront (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6ee67-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="6ee67-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="6ee67-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6ee67-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6ee67-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="6ee67-110">Prerequisites</span></span>

<span data-ttu-id="6ee67-111">Voor het configureren van Azure AD-integratie met Workfront, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="6ee67-111">To configure Azure AD integration with Workfront, you need the following items:</span></span>

- <span data-ttu-id="6ee67-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="6ee67-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6ee67-113">Een Workfront eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="6ee67-113">A Workfront single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6ee67-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="6ee67-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6ee67-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="6ee67-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6ee67-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="6ee67-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6ee67-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6ee67-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6ee67-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="6ee67-118">Scenario description</span></span>
<span data-ttu-id="6ee67-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="6ee67-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6ee67-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="6ee67-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6ee67-121">Workfront uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="6ee67-121">Adding Workfront from the gallery</span></span>
2. <span data-ttu-id="6ee67-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="6ee67-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workfront-from-the-gallery"></a><span data-ttu-id="6ee67-123">Workfront uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="6ee67-123">Adding Workfront from the gallery</span></span>
<span data-ttu-id="6ee67-124">Voor het configureren van de integratie van Workfront in Azure AD, moet u Workfront uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="6ee67-124">To configure the integration of Workfront into Azure AD, you need to add Workfront from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6ee67-125">**Als u wilt toevoegen Workfront uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="6ee67-125">**To add Workfront from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6ee67-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="6ee67-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6ee67-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="6ee67-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6ee67-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="6ee67-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="6ee67-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6ee67-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="6ee67-133">Typ in het zoekvak **Workfront**.</span><span class="sxs-lookup"><span data-stu-id="6ee67-133">In the search box, type **Workfront**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_search.png)

5. <span data-ttu-id="6ee67-135">Selecteer in het deelvenster resultaten **Workfront**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="6ee67-135">In the results panel, select **Workfront**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6ee67-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="6ee67-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6ee67-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Workfront op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="6ee67-138">In this section, you configure and test Azure AD single sign-on with Workfront based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="6ee67-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Workfront is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6ee67-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Workfront is to a user in Azure AD.</span></span> <span data-ttu-id="6ee67-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Workfront tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="6ee67-140">In other words, a link relationship between an Azure AD user and the related user in Workfront needs to be established.</span></span>

<span data-ttu-id="6ee67-141">Wijs in Workfront, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="6ee67-141">In Workfront, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="6ee67-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Workfront, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="6ee67-142">To configure and test Azure AD single sign-on with Workfront, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6ee67-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6ee67-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6ee67-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6ee67-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6ee67-145">**[Maken van een testgebruiker Workfront](#creating-a-workfront-test-user)**  - Workfront die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="6ee67-145">**[Creating a Workfront test user](#creating-a-workfront-test-user)** - to have a counterpart of Britta Simon in Workfront that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="6ee67-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="6ee67-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6ee67-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="6ee67-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6ee67-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="6ee67-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6ee67-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Workfront configureren.</span><span class="sxs-lookup"><span data-stu-id="6ee67-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Workfront application.</span></span>

<span data-ttu-id="6ee67-150">**Voor het configureren van Azure AD eenmalige aanmelding met Workfront, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="6ee67-150">**To configure Azure AD single sign-on with Workfront, perform the following steps:**</span></span>

1. <span data-ttu-id="6ee67-151">In de Azure-portal op de **Workfront** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="6ee67-151">In the Azure portal, on the **Workfront** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="6ee67-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="6ee67-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_samlbase.png)

3. <span data-ttu-id="6ee67-155">Op de **Workfront domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="6ee67-155">On the **Workfront Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_url.png)

    <span data-ttu-id="6ee67-157">a.</span><span class="sxs-lookup"><span data-stu-id="6ee67-157">a.</span></span> <span data-ttu-id="6ee67-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<companyname>.attask-ondemand.com`</span><span class="sxs-lookup"><span data-stu-id="6ee67-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.attask-ondemand.com`</span></span>

    <span data-ttu-id="6ee67-159">b.</span><span class="sxs-lookup"><span data-stu-id="6ee67-159">b.</span></span> <span data-ttu-id="6ee67-160">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<companyname>.attasksandbox.com/SAML2`</span><span class="sxs-lookup"><span data-stu-id="6ee67-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.attasksandbox.com/SAML2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6ee67-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="6ee67-161">These values are not real.</span></span> <span data-ttu-id="6ee67-162">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="6ee67-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="6ee67-163">Neem contact op met [Workfront Client ondersteuningsteam](https://www.workfront.com/contact-us/) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="6ee67-163">Contact [Workfront Client support team](https://www.workfront.com/contact-us/) to get these values.</span></span> 
 
4. <span data-ttu-id="6ee67-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="6ee67-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the Certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_certificate.png) 

5. <span data-ttu-id="6ee67-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="6ee67-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-workfront-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6ee67-168">Op de **Workfront configuratie** sectie, klikt u op **configureren Workfront** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="6ee67-168">On the **Workfront Configuration** section, click **Configure Workfront** to open **Configure sign-on** window.</span></span> <span data-ttu-id="6ee67-169">Kopieer de **Sign-Out URL's, en SAML Single Sign-On Service** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="6ee67-169">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_configure.png) 

7. <span data-ttu-id="6ee67-171">Aanmelding bij uw bedrijf Workfront site als administrator.</span><span class="sxs-lookup"><span data-stu-id="6ee67-171">Sign-on to your Workfront company site as administrator.</span></span>

8. <span data-ttu-id="6ee67-172">Ga naar **eenmalige van configuratie**.</span><span class="sxs-lookup"><span data-stu-id="6ee67-172">Go to **Single Sign On Configuration**.</span></span>

9. <span data-ttu-id="6ee67-173">Op de **Single Sign-On** dialoogvenster de volgende stappen uitvoeren</span><span class="sxs-lookup"><span data-stu-id="6ee67-173">On the **Single Sign-On** dialog, perform the following steps</span></span>
    
    ![Eenmalige aanmelding configureren][23]
   
    <span data-ttu-id="6ee67-175">a.</span><span class="sxs-lookup"><span data-stu-id="6ee67-175">a.</span></span> <span data-ttu-id="6ee67-176">Als **Type**, selecteer **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="6ee67-176">As **Type**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="6ee67-177">b.</span><span class="sxs-lookup"><span data-stu-id="6ee67-177">b.</span></span> <span data-ttu-id="6ee67-178">Selecteer **Service Provider-ID**.</span><span class="sxs-lookup"><span data-stu-id="6ee67-178">Select **Service Provider ID**.</span></span>
   
    <span data-ttu-id="6ee67-179">c.</span><span class="sxs-lookup"><span data-stu-id="6ee67-179">c.</span></span> <span data-ttu-id="6ee67-180">Plak de **SAML Single Sign-On Service-URL** in de **Portal de aanmeldings-URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="6ee67-180">Paste the **SAML Single Sign-On Service URL** into the **Login Portal URL** textbox.</span></span>
   
    <span data-ttu-id="6ee67-181">d.</span><span class="sxs-lookup"><span data-stu-id="6ee67-181">d.</span></span> <span data-ttu-id="6ee67-182">Plakken **Service-URL met eenmalige Sign-Out** in de **Sign-Out URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="6ee67-182">Paste **Single Sign-Out Service URL** into the **Sign-Out URL** textbox.</span></span>
   
    <span data-ttu-id="6ee67-183">e.</span><span class="sxs-lookup"><span data-stu-id="6ee67-183">e.</span></span> <span data-ttu-id="6ee67-184">Plakken **URL van wijzigen wachtwoord** in de **URL van wijzigen wachtwoord** textbox.</span><span class="sxs-lookup"><span data-stu-id="6ee67-184">Paste **Change Password URL** into the **Change Password URL** textbox.</span></span>
   
    <span data-ttu-id="6ee67-185">f.</span><span class="sxs-lookup"><span data-stu-id="6ee67-185">f.</span></span> <span data-ttu-id="6ee67-186">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="6ee67-186">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="6ee67-187">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="6ee67-187">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6ee67-188">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="6ee67-188">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6ee67-189">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6ee67-189">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6ee67-190">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="6ee67-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="6ee67-191">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="6ee67-191">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="6ee67-193">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="6ee67-193">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6ee67-194">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="6ee67-194">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-workfront-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6ee67-196">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="6ee67-196">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-workfront-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6ee67-198">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6ee67-198">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-workfront-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6ee67-200">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="6ee67-200">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-workfront-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6ee67-202">a.</span><span class="sxs-lookup"><span data-stu-id="6ee67-202">a.</span></span> <span data-ttu-id="6ee67-203">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6ee67-203">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6ee67-204">b.</span><span class="sxs-lookup"><span data-stu-id="6ee67-204">b.</span></span> <span data-ttu-id="6ee67-205">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6ee67-205">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6ee67-206">c.</span><span class="sxs-lookup"><span data-stu-id="6ee67-206">c.</span></span> <span data-ttu-id="6ee67-207">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="6ee67-207">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6ee67-208">d.</span><span class="sxs-lookup"><span data-stu-id="6ee67-208">d.</span></span> <span data-ttu-id="6ee67-209">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="6ee67-209">Click **Create**.</span></span>
 
### <a name="creating-a-workfront-test-user"></a><span data-ttu-id="6ee67-210">Een testgebruiker Workfront maken</span><span class="sxs-lookup"><span data-stu-id="6ee67-210">Creating a Workfront test user</span></span>

<span data-ttu-id="6ee67-211">Het doel van deze sectie is het maken van een gebruiker Britta Simon in Workfront genoemd.</span><span class="sxs-lookup"><span data-stu-id="6ee67-211">The objective of this section is to create a user called Britta Simon in Workfront.</span></span>

<span data-ttu-id="6ee67-212">**Als u wilt een gebruiker Britta Simon aangeroepen in Workfront maakt, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="6ee67-212">**To create a user called Britta Simon in Workfront, perform the following steps:**</span></span>

1. <span data-ttu-id="6ee67-213">Meld u op met uw bedrijf Workfront site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="6ee67-213">Sign on to your Workfront company site as administrator.</span></span>
2. <span data-ttu-id="6ee67-214">Klik in het menu bovenaan op **mensen**.</span><span class="sxs-lookup"><span data-stu-id="6ee67-214">In the menu on the top, click **People**.</span></span>
3. <span data-ttu-id="6ee67-215">Klik op **nieuwe persoon**.</span><span class="sxs-lookup"><span data-stu-id="6ee67-215">Click **New Person**.</span></span> 
4. <span data-ttu-id="6ee67-216">In het dialoogvenster nieuwe persoon, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="6ee67-216">On the New Person dialog, perform the following steps:</span></span>
   
    ![Een testgebruiker Workfront maken][21] 
   
    <span data-ttu-id="6ee67-218">a.</span><span class="sxs-lookup"><span data-stu-id="6ee67-218">a.</span></span> <span data-ttu-id="6ee67-219">In de **voornaam** textbox, typt u "Britta."</span><span class="sxs-lookup"><span data-stu-id="6ee67-219">In the **First Name** textbox, type "Britta."</span></span>
   
    <span data-ttu-id="6ee67-220">b.</span><span class="sxs-lookup"><span data-stu-id="6ee67-220">b.</span></span> <span data-ttu-id="6ee67-221">In de **achternaam** textbox, typt u "Simon."</span><span class="sxs-lookup"><span data-stu-id="6ee67-221">In the **Last Name** textbox, type "Simon."</span></span>
   
    <span data-ttu-id="6ee67-222">c.</span><span class="sxs-lookup"><span data-stu-id="6ee67-222">c.</span></span> <span data-ttu-id="6ee67-223">In de **e-mailadres** textbox Britta Simon van e-mailadres typt in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6ee67-223">In the **Email Address** textbox, type Britta Simon's email address in Azure Active Directory.</span></span>
   
    <span data-ttu-id="6ee67-224">d.</span><span class="sxs-lookup"><span data-stu-id="6ee67-224">d.</span></span> <span data-ttu-id="6ee67-225">Klik op **persoon toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="6ee67-225">Click **Add Person**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="6ee67-226">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="6ee67-226">Assigning the Azure AD test user</span></span>

<span data-ttu-id="6ee67-227">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Workfront.</span><span class="sxs-lookup"><span data-stu-id="6ee67-227">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Workfront.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="6ee67-229">**Britta Simon om aan te wijzen Workfront, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="6ee67-229">**To assign Britta Simon to Workfront, perform the following steps:**</span></span>

1. <span data-ttu-id="6ee67-230">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="6ee67-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="6ee67-232">Selecteer in de lijst met toepassingen **Workfront**.</span><span class="sxs-lookup"><span data-stu-id="6ee67-232">In the applications list, select **Workfront**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_app.png) 

3. <span data-ttu-id="6ee67-234">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="6ee67-234">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="6ee67-236">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="6ee67-236">Click **Add** button.</span></span> <span data-ttu-id="6ee67-237">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6ee67-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="6ee67-239">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="6ee67-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6ee67-240">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6ee67-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6ee67-241">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6ee67-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6ee67-242">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="6ee67-242">Testing single sign-on</span></span>

<span data-ttu-id="6ee67-243">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="6ee67-243">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="6ee67-244">Als u op de tegel Workfront in het deelvenster toegang, krijgt u de aanmeldingspagina van Workfront toepassing.</span><span class="sxs-lookup"><span data-stu-id="6ee67-244">When you click the Workfront tile in the Access Panel, you should get login page of Workfront application.</span></span>
<span data-ttu-id="6ee67-245">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6ee67-245">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="6ee67-246">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="6ee67-246">Additional resources</span></span>

* [<span data-ttu-id="6ee67-247">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6ee67-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6ee67-248">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6ee67-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_04.png
[21]:./media/active-directory-saas-workfront-tutorial/tutorial_attask_08.png
[23]:./media/active-directory-saas-workfront-tutorial/tutorial_attask_06.png
[100]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_203.png

