---
title: 'Zelfstudie: Azure Active Directory-integratie met BambooHR | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en BambooHR.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f826b5d2-9c64-47df-bbbf-0adf9eb0fa71
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: jeedes
ms.openlocfilehash: 06bf91b0e598fd3d8e644378efdb753611ee1ebc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bamboohr"></a><span data-ttu-id="bf7bf-103">Zelfstudie: Azure Active Directory-integratie met BambooHR</span><span class="sxs-lookup"><span data-stu-id="bf7bf-103">Tutorial: Azure Active Directory integration with BambooHR</span></span>

<span data-ttu-id="bf7bf-104">In deze zelfstudie leert u hoe BambooHR integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bf7bf-104">In this tutorial, you learn how to integrate BambooHR with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bf7bf-105">BambooHR integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="bf7bf-105">Integrating BambooHR with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="bf7bf-106">U kunt beheren in Azure AD die toegang tot BambooHR heeft</span><span class="sxs-lookup"><span data-stu-id="bf7bf-106">You can control in Azure AD who has access to BambooHR</span></span>
- <span data-ttu-id="bf7bf-107">U kunt uw gebruikers automatisch ophalen aangemeld bij BambooHR (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="bf7bf-107">You can enable your users to automatically get signed-on to BambooHR (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bf7bf-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="bf7bf-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="bf7bf-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bf7bf-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bf7bf-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="bf7bf-110">Prerequisites</span></span>

<span data-ttu-id="bf7bf-111">Voor het configureren van Azure AD-integratie met BambooHR, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="bf7bf-111">To configure Azure AD integration with BambooHR, you need the following items:</span></span>

- <span data-ttu-id="bf7bf-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="bf7bf-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bf7bf-113">Een BambooHR eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="bf7bf-113">A BambooHR single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bf7bf-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bf7bf-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="bf7bf-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bf7bf-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bf7bf-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bf7bf-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bf7bf-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="bf7bf-118">Scenario description</span></span>
<span data-ttu-id="bf7bf-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bf7bf-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="bf7bf-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bf7bf-121">BambooHR uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="bf7bf-121">Adding BambooHR from the gallery</span></span>
2. <span data-ttu-id="bf7bf-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="bf7bf-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bamboohr-from-the-gallery"></a><span data-ttu-id="bf7bf-123">BambooHR uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="bf7bf-123">Adding BambooHR from the gallery</span></span>
<span data-ttu-id="bf7bf-124">Voor het configureren van de integratie van BambooHR in Azure AD, moet u BambooHR uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-124">To configure the integration of BambooHR into Azure AD, you need to add BambooHR from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="bf7bf-125">**Als u wilt toevoegen BambooHR uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="bf7bf-125">**To add BambooHR from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="bf7bf-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="bf7bf-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="bf7bf-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="bf7bf-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="bf7bf-133">Typ in het zoekvak **BambooHR**.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-133">In the search box, type **BambooHR**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_search.png)

5. <span data-ttu-id="bf7bf-135">Selecteer in het deelvenster resultaten **BambooHR**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-135">In the results panel, select **BambooHR**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bf7bf-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="bf7bf-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bf7bf-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met BambooHR op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="bf7bf-138">In this section, you configure and test Azure AD single sign-on with BambooHR based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="bf7bf-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in BambooHR is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BambooHR is to a user in Azure AD.</span></span> <span data-ttu-id="bf7bf-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in BambooHR tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-140">In other words, a link relationship between an Azure AD user and the related user in BambooHR needs to be established.</span></span>

<span data-ttu-id="bf7bf-141">Wijs in BambooHR, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-141">In BambooHR, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="bf7bf-142">Om te configureren en testen van Azure AD eenmalige aanmelding met BambooHR, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="bf7bf-142">To configure and test Azure AD single sign-on with BambooHR, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="bf7bf-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="bf7bf-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bf7bf-145">**[Maken van een testgebruiker BambooHR](#creating-a-bamboohr-test-user)**  - BambooHR die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-145">**[Creating a BambooHR test user](#creating-a-bamboohr-test-user)** - to have a counterpart of Britta Simon in BambooHR that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="bf7bf-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bf7bf-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bf7bf-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="bf7bf-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bf7bf-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing BambooHR configureren.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BambooHR application.</span></span>

<span data-ttu-id="bf7bf-150">**Voor het configureren van Azure AD eenmalige aanmelding met BambooHR, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="bf7bf-150">**To configure Azure AD single sign-on with BambooHR, perform the following steps:**</span></span>

1. <span data-ttu-id="bf7bf-151">In de Azure-portal op de **BambooHR** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-151">In the Azure portal, on the **BambooHR** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="bf7bf-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_samlbase.png)

3. <span data-ttu-id="bf7bf-155">Op de **BambooHR domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="bf7bf-155">On the **BambooHR Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_url.png)

    <span data-ttu-id="bf7bf-157">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<company>.bamboohr.com`</span><span class="sxs-lookup"><span data-stu-id="bf7bf-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company>.bamboohr.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="bf7bf-158">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-158">This value is not real.</span></span> <span data-ttu-id="bf7bf-159">Deze waarde bijwerken met de werkelijke URL voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="bf7bf-160">Neem contact op met [BambooHR Client ondersteuningsteam](https://www.bamboohr.com/contact.php) deze waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-160">Contact [BambooHR Client support team](https://www.bamboohr.com/contact.php) to get this value.</span></span> 
 
4. <span data-ttu-id="bf7bf-161">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_certificate.png) 

5. <span data-ttu-id="bf7bf-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="bf7bf-165">Op de **BambooHR configuratie** sectie, klikt u op **configureren BambooHR** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-165">On the **BambooHR Configuration** section, click **Configure BambooHR** to open **Configure sign-on** window.</span></span> <span data-ttu-id="bf7bf-166">Kopieer de **SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="bf7bf-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_configure.png) 

6. <span data-ttu-id="bf7bf-168">In een ander browservenster, meld u bij uw bedrijf BambooHR site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-168">In a different web browser window, log into your BambooHR company site as an administrator.</span></span>

7. <span data-ttu-id="bf7bf-169">Op de startpagina, de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="bf7bf-169">On the homepage, perform the following steps:</span></span>
   
    <span data-ttu-id="bf7bf-170">![Eenmalige aanmelding](./media/active-directory-saas-bamboo-hr-tutorial/ic796691.png "eenmalige aanmelding")</span><span class="sxs-lookup"><span data-stu-id="bf7bf-170">![Single Sign-On](./media/active-directory-saas-bamboo-hr-tutorial/ic796691.png "Single Sign-On")</span></span>   

    <span data-ttu-id="bf7bf-171">a.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-171">a.</span></span> <span data-ttu-id="bf7bf-172">Klik op **Apps**.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-172">Click **Apps**.</span></span>
   
    <span data-ttu-id="bf7bf-173">b.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-173">b.</span></span> <span data-ttu-id="bf7bf-174">Klik in het menu apps aan de linkerkant op **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-174">In the apps menu on the left, click **Single Sign-On**.</span></span>
   
    <span data-ttu-id="bf7bf-175">c.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-175">c.</span></span> <span data-ttu-id="bf7bf-176">Klik op **SAML Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-176">Click **SAML Single Sign-On**.</span></span>

8. <span data-ttu-id="bf7bf-177">In de **SAML Single Sign-On** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="bf7bf-177">In the **SAML Single Sign-On** section, perform the following steps:</span></span>
   
    <span data-ttu-id="bf7bf-178">![Eenmalige aanmelding SAML](./media/active-directory-saas-bamboo-hr-tutorial/ic796692.png "SAML eenmalige aanmelding")</span><span class="sxs-lookup"><span data-stu-id="bf7bf-178">![SAML Single Sign-On](./media/active-directory-saas-bamboo-hr-tutorial/ic796692.png "SAML Single Sign-On")</span></span>
   
    <span data-ttu-id="bf7bf-179">a.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-179">a.</span></span> <span data-ttu-id="bf7bf-180">Plak de **SAML Single Sign-On Service-URL** waarde in de **aanmeldings-Url voor eenmalige aanmelding** textbox.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-180">Paste the **SAML Single Sign-On Service URL** value into the **SSO Login Url** textbox.</span></span>
      
    <span data-ttu-id="bf7bf-181">b.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-181">b.</span></span> <span data-ttu-id="bf7bf-182">Openen van Base64-gecodeerde certificaat gedownload vanuit Azure-portal in Kladblok, Kopieer de inhoud ervan naar het Klembord en plakt u deze naar de **X.509-certificaat** tekstvak</span><span class="sxs-lookup"><span data-stu-id="bf7bf-182">Open base-64 encoded certificate downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox</span></span>
   
    <span data-ttu-id="bf7bf-183">c.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-183">c.</span></span> <span data-ttu-id="bf7bf-184">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-184">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="bf7bf-185">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="bf7bf-185">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="bf7bf-186">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-186">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="bf7bf-187">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bf7bf-187">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bf7bf-188">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="bf7bf-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="bf7bf-189">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="bf7bf-191">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="bf7bf-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="bf7bf-192">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-192">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bamboo-hr-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bf7bf-194">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-194">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bamboo-hr-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bf7bf-196">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-196">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bamboo-hr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bf7bf-198">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="bf7bf-198">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bamboo-hr-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bf7bf-200">a.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-200">a.</span></span> <span data-ttu-id="bf7bf-201">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-201">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bf7bf-202">b.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-202">b.</span></span> <span data-ttu-id="bf7bf-203">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-203">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bf7bf-204">c.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-204">c.</span></span> <span data-ttu-id="bf7bf-205">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-205">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="bf7bf-206">d.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-206">d.</span></span> <span data-ttu-id="bf7bf-207">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-207">Click **Create**.</span></span>
 
### <a name="creating-a-bamboohr-test-user"></a><span data-ttu-id="bf7bf-208">Een testgebruiker BambooHR maken</span><span class="sxs-lookup"><span data-stu-id="bf7bf-208">Creating a BambooHR test user</span></span>

<span data-ttu-id="bf7bf-209">Om Azure AD-gebruikers zich aanmelden bij BambooHR, moeten ze worden ingericht in BambooHR.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-209">To enable Azure AD users to log in to BambooHR, they must be provisioned into BambooHR.</span></span>  

<span data-ttu-id="bf7bf-210">In het geval van BambooHR is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-210">In the case of BambooHR, provisioning is a manual task.</span></span>

<span data-ttu-id="bf7bf-211">**Voor het inrichten van een gebruikersaccount, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="bf7bf-211">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="bf7bf-212">Meld u aan bij uw **BambooHR** site als administrator.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-212">Log in to your **BambooHR** site as administrator.</span></span>

2. <span data-ttu-id="bf7bf-213">Klik in de werkbalk bovenaan op **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-213">In the toolbar on the top, click **Settings**.</span></span>
   
    <span data-ttu-id="bf7bf-214">![Instelling](./media/active-directory-saas-bamboo-hr-tutorial/ic796694.png "instelling")</span><span class="sxs-lookup"><span data-stu-id="bf7bf-214">![Setting](./media/active-directory-saas-bamboo-hr-tutorial/ic796694.png "Setting")</span></span>

3. <span data-ttu-id="bf7bf-215">Klik op **overzicht**.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-215">Click **Overview**.</span></span>

4. <span data-ttu-id="bf7bf-216">Ga in het navigatiedeelvenster links naar **beveiliging \> gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-216">In the left navigation pane, go to **Security \> Users**.</span></span>

5. <span data-ttu-id="bf7bf-217">Typ de gebruikersnaam, wachtwoord en e-mailadres van een geldige AAD-account dat u inrichten in de bijbehorende tekstvakken wilt.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-217">Type the user name, password, and email address of a valid AAD account you want to provision into the related textboxes.</span></span>

6. <span data-ttu-id="bf7bf-218">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-218">Click **Save**.</span></span>
        
>[!NOTE]
><span data-ttu-id="bf7bf-219">U kunt andere BambooHR gebruiker account hulpmiddelen voor het maken of API's die is geleverd door BambooHR aan inrichten AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-219">You can use any other BambooHR user account creation tools or APIs provided by BambooHR to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="bf7bf-220">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="bf7bf-220">Assigning the Azure AD test user</span></span>

<span data-ttu-id="bf7bf-221">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan BambooHR.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BambooHR.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="bf7bf-223">**Britta Simon om aan te wijzen BambooHR, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="bf7bf-223">**To assign Britta Simon to BambooHR, perform the following steps:**</span></span>

1. <span data-ttu-id="bf7bf-224">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="bf7bf-226">Selecteer in de lijst met toepassingen **BambooHR**.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-226">In the applications list, select **BambooHR**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_app.png) 

3. <span data-ttu-id="bf7bf-228">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-228">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="bf7bf-230">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-230">Click **Add** button.</span></span> <span data-ttu-id="bf7bf-231">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="bf7bf-233">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="bf7bf-234">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bf7bf-235">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bf7bf-236">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="bf7bf-236">Testing single sign-on</span></span>

<span data-ttu-id="bf7bf-237">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="bf7bf-238">Als u op de tegel BambooHR in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing BambooHR.</span><span class="sxs-lookup"><span data-stu-id="bf7bf-238">When you click the BambooHR tile in the Access Panel, you should get automatically signed-on to your BambooHR application.</span></span>
<span data-ttu-id="bf7bf-239">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bf7bf-239">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="bf7bf-240">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="bf7bf-240">Additional resources</span></span>

* [<span data-ttu-id="bf7bf-241">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bf7bf-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bf7bf-242">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bf7bf-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_203.png

