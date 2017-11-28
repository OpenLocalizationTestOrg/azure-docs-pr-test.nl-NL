---
title: 'Zelfstudie: Azure Active Directory-integratie met LearnUpon | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en LearnUpon.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b11c6315-c79d-4f34-9610-bd17070ab7c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: b6ac8acc244e9029be01ede5e0865c280171217d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learnupon"></a><span data-ttu-id="6b0e7-103">Zelfstudie: Azure Active Directory-integratie met LearnUpon</span><span class="sxs-lookup"><span data-stu-id="6b0e7-103">Tutorial: Azure Active Directory integration with LearnUpon</span></span>

<span data-ttu-id="6b0e7-104">In deze zelfstudie leert u hoe LearnUpon integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6b0e7-104">In this tutorial, you learn how to integrate LearnUpon with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6b0e7-105">LearnUpon integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="6b0e7-105">Integrating LearnUpon with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6b0e7-106">U kunt beheren in Azure AD die toegang tot LearnUpon heeft</span><span class="sxs-lookup"><span data-stu-id="6b0e7-106">You can control in Azure AD who has access to LearnUpon</span></span>
- <span data-ttu-id="6b0e7-107">U kunt uw gebruikers automatisch ophalen aangemeld bij LearnUpon (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="6b0e7-107">You can enable your users to automatically get signed-on to LearnUpon (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6b0e7-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="6b0e7-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="6b0e7-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6b0e7-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6b0e7-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="6b0e7-110">Prerequisites</span></span>

<span data-ttu-id="6b0e7-111">Voor het configureren van Azure AD-integratie met LearnUpon, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="6b0e7-111">To configure Azure AD integration with LearnUpon, you need the following items:</span></span>

- <span data-ttu-id="6b0e7-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="6b0e7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6b0e7-113">Een LearnUpon eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="6b0e7-113">A LearnUpon single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6b0e7-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6b0e7-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="6b0e7-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6b0e7-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6b0e7-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6b0e7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6b0e7-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="6b0e7-118">Scenario description</span></span>
<span data-ttu-id="6b0e7-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6b0e7-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="6b0e7-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6b0e7-121">LearnUpon uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="6b0e7-121">Adding LearnUpon from the gallery</span></span>
2. <span data-ttu-id="6b0e7-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="6b0e7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-learnupon-from-the-gallery"></a><span data-ttu-id="6b0e7-123">LearnUpon uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="6b0e7-123">Adding LearnUpon from the gallery</span></span>
<span data-ttu-id="6b0e7-124">Voor het configureren van de integratie van LearnUpon in Azure AD, moet u LearnUpon uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-124">To configure the integration of LearnUpon into Azure AD, you need to add LearnUpon from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6b0e7-125">**Als u wilt toevoegen LearnUpon uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="6b0e7-125">**To add LearnUpon from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6b0e7-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6b0e7-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6b0e7-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="6b0e7-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="6b0e7-133">Typ in het zoekvak **LearnUpon**.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-133">In the search box, type **LearnUpon**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_search.png)

5. <span data-ttu-id="6b0e7-135">Selecteer in het deelvenster resultaten **LearnUpon**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-135">In the results panel, select **LearnUpon**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6b0e7-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="6b0e7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6b0e7-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met LearnUpon op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-138">In this section, you configure and test Azure AD single sign-on with LearnUpon based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6b0e7-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in LearnUpon is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LearnUpon is to a user in Azure AD.</span></span> <span data-ttu-id="6b0e7-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in LearnUpon tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-140">In other words, a link relationship between an Azure AD user and the related user in LearnUpon needs to be established.</span></span>

<span data-ttu-id="6b0e7-141">Wijs in LearnUpon, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-141">In LearnUpon, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="6b0e7-142">Om te configureren en testen van Azure AD eenmalige aanmelding met LearnUpon, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="6b0e7-142">To configure and test Azure AD single sign-on with LearnUpon, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6b0e7-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6b0e7-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6b0e7-145">**[Maken van een testgebruiker LearnUpon](#creating-a-learnupon-test-user)**  - LearnUpon die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-145">**[Creating a LearnUpon test user](#creating-a-learnupon-test-user)** - to have a counterpart of Britta Simon in LearnUpon that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="6b0e7-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6b0e7-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6b0e7-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="6b0e7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6b0e7-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing LearnUpon configureren.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LearnUpon application.</span></span>

<span data-ttu-id="6b0e7-150">**Voor het configureren van Azure AD eenmalige aanmelding met LearnUpon, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="6b0e7-150">**To configure Azure AD single sign-on with LearnUpon, perform the following steps:**</span></span>

1. <span data-ttu-id="6b0e7-151">In de Azure-portal op de **LearnUpon** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-151">In the Azure portal, on the **LearnUpon** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="6b0e7-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_samlbase.png)

3. <span data-ttu-id="6b0e7-155">Op de **LearnUpon domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="6b0e7-155">On the **LearnUpon Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_url.png)

    <span data-ttu-id="6b0e7-157">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://<companyname>.learnupon.com/saml/consumer`</span><span class="sxs-lookup"><span data-stu-id="6b0e7-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.learnupon.com/saml/consumer`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6b0e7-158">Houd er rekening mee dat dit geen de feitelijke waarde is.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-158">Please note that this is not the real value.</span></span> <span data-ttu-id="6b0e7-159">u moet deze waarde bijwerken met de werkelijke antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-159">you have to update this value with the actual Reply URL.</span></span> <span data-ttu-id="6b0e7-160">Deze waarde Contact op te halen [LearnUpon ondersteuningsteam](https://www.learnupon.com/features/support/).</span><span class="sxs-lookup"><span data-stu-id="6b0e7-160">To get this value Contact [LearnUpon support team](https://www.learnupon.com/features/support/).</span></span>



4. <span data-ttu-id="6b0e7-161">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Raw)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-161">On the **SAML Signing Certificate** section, click **Certificate (Raw)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_certificate.png) 

5. <span data-ttu-id="6b0e7-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-learnupon-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6b0e7-165">Op de **LearnUpon configuratie** sectie, klikt u op **configureren LearnUpon** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-165">On the **LearnUpon Configuration** section, click **Configure LearnUpon** to open **Configure sign-on** window.</span></span> <span data-ttu-id="6b0e7-166">Kopieer de **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="6b0e7-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_configure.png) 

7. <span data-ttu-id="6b0e7-168">Open een ander browserexemplaar en meld u aan bij LearnUpon met een administratoraccount.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-168">Open another browser instance and login into LearnUpon with an administrator account.</span></span> 

8. <span data-ttu-id="6b0e7-169">Klik op de **instellingen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-169">Click the **settings** tab.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_06.png)

9. <span data-ttu-id="6b0e7-171">Klik op **eenmalige aanmelding - SAML**, en klik vervolgens op **algemene instellingen** om SAML-instellingen te configureren.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-171">Click **Single Sign On - SAML**, and then click **General Settings** to configure SAML settings.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_07.png) 

10. <span data-ttu-id="6b0e7-173">In de **algemene instellingen** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="6b0e7-173">In the **General Settings** section, perform the following steps:</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_08.png)  
  
    <span data-ttu-id="6b0e7-175">a.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-175">a.</span></span> <span data-ttu-id="6b0e7-176">Selecteer **ingeschakeld**.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-176">Select **Enabled**.</span></span>

    <span data-ttu-id="6b0e7-177">b.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-177">b.</span></span> <span data-ttu-id="6b0e7-178">Selecteer **versie** als **2.0**.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-178">Select **Version** as **2.0**.</span></span>

    <span data-ttu-id="6b0e7-179">c.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-179">c.</span></span> <span data-ttu-id="6b0e7-180">Selecteer **overslaan voorwaarden** als **Nee**.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-180">Select **Skip conditions** as **No**.</span></span>

    <span data-ttu-id="6b0e7-181">d.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-181">d.</span></span> <span data-ttu-id="6b0e7-182">In de **SAML-Token boeken param naam** textbox, de naam van de aanvraag post-parameter voor de URL van de consument SAML hierboven genoemde type met de SAML-verklaring worden geverifieerd en geverifieerd - bijvoorbeeld **SAMLResponse** .</span><span class="sxs-lookup"><span data-stu-id="6b0e7-182">In the **SAML Token Post param name** textbox, type the name of request post parameter to the SAML consumer URL indicated above that contains the SAML Assertion to be verified and authenticated - for example **SAMLResponse**.</span></span>

    <span data-ttu-id="6b0e7-183">e.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-183">e.</span></span> <span data-ttu-id="6b0e7-184">In de **indeling van de id** textbox type de waarde die waar in uw SAML-verklaring (e-mailadres) van de gebruikers-id aangeeft bevindt zich - bijvoorbeeld **urn: oasis: namen: tc: SAML:1.1:nameid-indeling: emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-184">In the **Name Identifier Format** textbox, type the value that indicates where in your SAML Assertion the users identifier (Email address) resides - for example **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>
  
    <span data-ttu-id="6b0e7-185">f.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-185">f.</span></span> <span data-ttu-id="6b0e7-186">In de **Providerlocatie identificeren** textbox, typ de waarde die waar de gebruikers worden verzonden aangeeft als ze op het pictogram van uw geüploade van het scherm van uw Azure-portal aanmelding klikt.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-186">In the **Identify Provider Location** textbox, type the value that indicates where the users are sent to if they click on your uploaded icon from your Azure portal login screen.</span></span>
  
    <span data-ttu-id="6b0e7-187">g.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-187">g.</span></span> <span data-ttu-id="6b0e7-188">In de **afmelden URL** textbox, plak de **Sign-Out URL** die u hebt gekopieerd uit de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-188">In the **Sign out URL** textbox, paste the **Sign-Out URL** which you have copied from the Azure portal.</span></span>
    
    <span data-ttu-id="6b0e7-189">h.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-189">h.</span></span> <span data-ttu-id="6b0e7-190">Klik op **vinger afdrukken bestellen beheren**, en vervolgens de vingerafdruk van het gedownloade certificaat te uploaden.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-190">Click **Manage finger prints**, and then upload the finger print of your downloaded certificate.</span></span>

11. <span data-ttu-id="6b0e7-191">Klik op **gebruikersinstellingen**, en voer de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="6b0e7-191">Click **User Settings**, and then perform the following steps:</span></span>
   
     ![Eenmalige aanmelding configureren](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_11.png)  
 
    <span data-ttu-id="6b0e7-193">a.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-193">a.</span></span> <span data-ttu-id="6b0e7-194">In de **voornaam id indeling** textbox type de waarde die kan worden weergegeven wanneer u in uw SAML-verklaring de voornaam van de gebruikers zich - voorbeeld bevindt: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-194">In the **First Name Identifier Format** textbox, type the value that tells us where in your SAML Assertion the users firstname resides - for example: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span></span>
  
    <span data-ttu-id="6b0e7-195">b.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-195">b.</span></span> <span data-ttu-id="6b0e7-196">In de **laatste naamnotatie id** textbox type de waarde die kan worden weergegeven wanneer u in uw SAML-verklaring de achternaam van de gebruikers zich - voorbeeld bevindt: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname** .</span><span class="sxs-lookup"><span data-stu-id="6b0e7-196">In the **Last Name Identifier Format** textbox, type the value that tells us where in your SAML Assertion the users lastname resides - for example: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span></span>

> [!TIP]
> <span data-ttu-id="6b0e7-197">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="6b0e7-197">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6b0e7-198">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-198">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6b0e7-199">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6b0e7-199">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6b0e7-200">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="6b0e7-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="6b0e7-201">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-201">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="6b0e7-203">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="6b0e7-203">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6b0e7-204">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-204">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-learnupon-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6b0e7-206">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-206">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-learnupon-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6b0e7-208">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-208">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-learnupon-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6b0e7-210">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="6b0e7-210">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-learnupon-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6b0e7-212">a.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-212">a.</span></span> <span data-ttu-id="6b0e7-213">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-213">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6b0e7-214">b.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-214">b.</span></span> <span data-ttu-id="6b0e7-215">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-215">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6b0e7-216">c.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-216">c.</span></span> <span data-ttu-id="6b0e7-217">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-217">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6b0e7-218">d.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-218">d.</span></span> <span data-ttu-id="6b0e7-219">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-219">Click **Create**.</span></span>
 
### <a name="creating-a-learnupon-test-user"></a><span data-ttu-id="6b0e7-220">Een testgebruiker LearnUpon maken</span><span class="sxs-lookup"><span data-stu-id="6b0e7-220">Creating a LearnUpon test user</span></span>

<span data-ttu-id="6b0e7-221">Het doel van deze sectie is het maken van een gebruiker Britta Simon in LearnUpon genoemd.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-221">The objective of this section is to create a user called Britta Simon in LearnUpon.</span></span> <span data-ttu-id="6b0e7-222">LearnUpon ondersteunt just-in-time-inrichting, dit is standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-222">LearnUpon supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="6b0e7-223">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-223">There is no action item for you in this section.</span></span> <span data-ttu-id="6b0e7-224">Een nieuwe gebruiker wordt gemaakt tijdens een poging tot toegang tot LearnUpon als deze nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-224">A new user will be created during an attempt to access LearnUpon if it doesn't exist yet.</span></span> <span data-ttu-id="6b0e7-225">[Configureren van Azure AD voor eenmalige aanmelding](#configuring-azure-ad-single-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="6b0e7-225">[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on).</span></span>

>[!NOTE]
><span data-ttu-id="6b0e7-226">Als u een gebruiker handmatig maken wilt, moet u contact op met [LearnUpon ondersteuningsteam](https://www.learnupon.com/features/support/).</span><span class="sxs-lookup"><span data-stu-id="6b0e7-226">If you need to create an user manually, you need to contact [LearnUpon support team](https://www.learnupon.com/features/support/).</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="6b0e7-227">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="6b0e7-227">Assigning the Azure AD test user</span></span>

<span data-ttu-id="6b0e7-228">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan LearnUpon.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-228">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LearnUpon.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="6b0e7-230">**Britta Simon om aan te wijzen LearnUpon, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="6b0e7-230">**To assign Britta Simon to LearnUpon, perform the following steps:**</span></span>

1. <span data-ttu-id="6b0e7-231">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-231">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="6b0e7-233">Selecteer in de lijst met toepassingen **LearnUpon**.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-233">In the applications list, select **LearnUpon**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_app.png) 

3. <span data-ttu-id="6b0e7-235">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-235">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="6b0e7-237">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-237">Click **Add** button.</span></span> <span data-ttu-id="6b0e7-238">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="6b0e7-240">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-240">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6b0e7-241">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6b0e7-242">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6b0e7-243">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="6b0e7-243">Testing single sign-on</span></span>

<span data-ttu-id="6b0e7-244">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-244">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="6b0e7-245">Als u op de tegel LearnUpon in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing LearnUpon.</span><span class="sxs-lookup"><span data-stu-id="6b0e7-245">When you click the LearnUpon tile in the Access Panel, you should get automatically signed-on to your LearnUpon application.</span></span>
<span data-ttu-id="6b0e7-246">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6b0e7-246">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6b0e7-247">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="6b0e7-247">Additional resources</span></span>

* [<span data-ttu-id="6b0e7-248">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6b0e7-248">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6b0e7-249">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6b0e7-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_203.png

