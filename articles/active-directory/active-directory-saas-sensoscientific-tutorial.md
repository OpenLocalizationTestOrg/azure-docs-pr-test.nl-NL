---
title: 'Zelfstudie: Azure Active Directory-integratie met SensoScientific draadloze temperatuur Monitoring System | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en SensoScientific draadloze temperatuur Monitoring System.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ee9a924d-ccde-45b0-ab40-877f82f5dfa2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: jeedes
ms.openlocfilehash: fa6242cf7f9559ca394ffde2e5e734cb935b03dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sensoscientific-wireless-temperature-monitoring-system"></a><span data-ttu-id="02055-103">Zelfstudie: Azure Active Directory-integratie met SensoScientific draadloze temperatuur Monitoring System</span><span class="sxs-lookup"><span data-stu-id="02055-103">Tutorial: Azure Active Directory integration with SensoScientific Wireless Temperature Monitoring System</span></span>

<span data-ttu-id="02055-104">In deze zelfstudie leert u hoe SensoScientific draadloze temperatuur Monitoring System integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="02055-104">In this tutorial, you learn how to integrate SensoScientific Wireless Temperature Monitoring System with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="02055-105">SensoScientific draadloze temperatuur Monitoring System integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="02055-105">Integrating SensoScientific Wireless Temperature Monitoring System with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="02055-106">U kunt beheren in Azure AD die toegang tot SensoScientific draadloze temperatuur Monitoring System heeft</span><span class="sxs-lookup"><span data-stu-id="02055-106">You can control in Azure AD who has access to SensoScientific Wireless Temperature Monitoring System</span></span>
- <span data-ttu-id="02055-107">U kunt uw gebruikers automatisch ophalen aangemeld bij SensoScientific draadloze temperatuur Monitoring System (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="02055-107">You can enable your users to automatically get signed-on to SensoScientific Wireless Temperature Monitoring System (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="02055-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="02055-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="02055-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="02055-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="02055-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="02055-110">Prerequisites</span></span>

<span data-ttu-id="02055-111">Voor het configureren van Azure AD-integratie met SensoScientific draadloze temperatuur Monitoring System, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="02055-111">To configure Azure AD integration with SensoScientific Wireless Temperature Monitoring System, you need the following items:</span></span>

- <span data-ttu-id="02055-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="02055-112">An Azure AD subscription</span></span>
- <span data-ttu-id="02055-113">Een SensoScientific draadloze temperatuur Monitoring System eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="02055-113">A SensoScientific Wireless Temperature Monitoring System single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="02055-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="02055-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="02055-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="02055-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="02055-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="02055-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="02055-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="02055-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="02055-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="02055-118">Scenario description</span></span>
<span data-ttu-id="02055-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="02055-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="02055-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="02055-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="02055-121">SensoScientific draadloze temperatuur Monitoring System uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="02055-121">Adding SensoScientific Wireless Temperature Monitoring System from the gallery</span></span>
2. <span data-ttu-id="02055-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="02055-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sensoscientific-wireless-temperature-monitoring-system-from-the-gallery"></a><span data-ttu-id="02055-123">SensoScientific draadloze temperatuur Monitoring System uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="02055-123">Adding SensoScientific Wireless Temperature Monitoring System from the gallery</span></span>
<span data-ttu-id="02055-124">Voor het configureren van de integratie van SensoScientific draadloze temperatuur-bewakingssysteem in Azure AD, moet u SensoScientific draadloze temperatuur Monitoring System uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="02055-124">To configure the integration of SensoScientific Wireless Temperature Monitoring System into Azure AD, you need to add SensoScientific Wireless Temperature Monitoring System from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="02055-125">**Als u wilt toevoegen SensoScientific draadloze temperatuur Monitoring System uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="02055-125">**To add SensoScientific Wireless Temperature Monitoring System from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="02055-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="02055-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="02055-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="02055-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="02055-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="02055-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="02055-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="02055-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="02055-133">Typ in het zoekvak **SensoScientific draadloze temperatuur Monitoring System**.</span><span class="sxs-lookup"><span data-stu-id="02055-133">In the search box, type **SensoScientific Wireless Temperature Monitoring System**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_search.png)

5. <span data-ttu-id="02055-135">Selecteer in het deelvenster resultaten **SensoScientific draadloze temperatuur Monitoring System**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="02055-135">In the results panel, select **SensoScientific Wireless Temperature Monitoring System**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="02055-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="02055-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="02055-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met SensoScientific draadloze temperatuur Monitoring System op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="02055-138">In this section, you configure and test Azure AD single sign-on with SensoScientific Wireless Temperature Monitoring System based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="02055-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in SensoScientific draadloze temperatuur Monitoring System is aan een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="02055-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SensoScientific Wireless Temperature Monitoring System is to a user in Azure AD.</span></span> <span data-ttu-id="02055-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in SensoScientific draadloze temperatuur Monitoring System tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="02055-140">In other words, a link relationship between an Azure AD user and the related user in SensoScientific Wireless Temperature Monitoring System needs to be established.</span></span>

<span data-ttu-id="02055-141">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in SensoScientific draadloze temperatuur Monitoring System.</span><span class="sxs-lookup"><span data-stu-id="02055-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SensoScientific Wireless Temperature Monitoring System.</span></span>

<span data-ttu-id="02055-142">Om te configureren en testen van Azure AD eenmalige aanmelding met SensoScientific draadloze temperatuur Monitoring System, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="02055-142">To configure and test Azure AD single sign-on with SensoScientific Wireless Temperature Monitoring System, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="02055-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="02055-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="02055-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="02055-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="02055-145">**[Maken van een testgebruiker SensoScientific draadloze temperatuur Monitoring System](#creating-a-sensoscientific-wireless-temperature-monitoring-system-test-user)**  - SensoScientific draadloze temperatuur Monitoring System dat is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="02055-145">**[Creating a SensoScientific Wireless Temperature Monitoring System test user](#creating-a-sensoscientific-wireless-temperature-monitoring-system-test-user)** - to have a counterpart of Britta Simon in SensoScientific Wireless Temperature Monitoring System that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="02055-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="02055-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="02055-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="02055-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="02055-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="02055-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="02055-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw toepassing SensoScientific draadloze temperatuur Monitoring System.</span><span class="sxs-lookup"><span data-stu-id="02055-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SensoScientific Wireless Temperature Monitoring System application.</span></span>

<span data-ttu-id="02055-150">**Voor het configureren van Azure AD eenmalige aanmelding met SensoScientific draadloze temperatuur Monitoring System, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="02055-150">**To configure Azure AD single sign-on with SensoScientific Wireless Temperature Monitoring System, perform the following steps:**</span></span>

1. <span data-ttu-id="02055-151">In de Azure-portal op de **SensoScientific draadloze temperatuur Monitoring System** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="02055-151">In the Azure portal, on the **SensoScientific Wireless Temperature Monitoring System** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="02055-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="02055-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_samlbase.png)

3. <span data-ttu-id="02055-155">Op de **SensoScientific draadloze temperatuur bewaking systeemdomein en URL's** sectie, u hoeft stappen uitvoeren als de app al vooraf geïntegreerde met Azure is:</span><span class="sxs-lookup"><span data-stu-id="02055-155">On the **SensoScientific Wireless Temperature Monitoring System Domain and URLs** section, no need to perform any steps as the app is already pre-integrated with Azure:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_url.png)

4. <span data-ttu-id="02055-157">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="02055-157">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_certificate.png) 

5. <span data-ttu-id="02055-159">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="02055-159">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="02055-161">Op de **SensoScientific draadloze temperatuur bewaking systeemconfiguratie** sectie, klikt u op **configureren SensoScientific draadloze temperatuur Monitoring System** openen **configureren eenmalige aanmelding** venster.</span><span class="sxs-lookup"><span data-stu-id="02055-161">On the **SensoScientific Wireless Temperature Monitoring System Configuration** section, click **Configure SensoScientific Wireless Temperature Monitoring System** to open **Configure sign-on** window.</span></span> <span data-ttu-id="02055-162">Kopiëren de **Sign-Out-URL, de entiteit-ID SAML** en **SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="02055-162">Copy the **Sign-Out URL, SAML Entity ID** and **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_configure.png) 

7. <span data-ttu-id="02055-164">Meld u aan op uw toepassing SensoScientific draadloze temperatuur Monitoring System als beheerder.</span><span class="sxs-lookup"><span data-stu-id="02055-164">Sign on to your SensoScientific Wireless Temperature Monitoring System application as an administrator.</span></span>

8. <span data-ttu-id="02055-165">Klik in het navigatiemenu aan de bovenkant op **configuratie** en Ga naar **configureren** onder **eenmalige aanmelding** om de eenmalige aanmelding op instellingen te openen.</span><span class="sxs-lookup"><span data-stu-id="02055-165">In the navigation menu on the top, click **Configuration** and goto **Configure** under **Single Sign On** to open the Single Sign On Settings.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_admin.png) 

9. <span data-ttu-id="02055-167">In **eenmalige aanmelding op instellingen** formulier de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="02055-167">In **Single Sign On Settings** form perform the following steps:</span></span>
 
    <span data-ttu-id="02055-168">a.</span><span class="sxs-lookup"><span data-stu-id="02055-168">a.</span></span> <span data-ttu-id="02055-169">Selecteer **certificaatverlener** als Azure AD.</span><span class="sxs-lookup"><span data-stu-id="02055-169">Select **Issuer Name** as Azure AD.</span></span>
    
    <span data-ttu-id="02055-170">b.</span><span class="sxs-lookup"><span data-stu-id="02055-170">b.</span></span> <span data-ttu-id="02055-171">Plak de **SAML entiteit-ID** die u hebt gekopieerd vanuit Azure-portal in URL-verlener tekstvak.</span><span class="sxs-lookup"><span data-stu-id="02055-171">Paste the **SAML Entity ID** which you have copied from Azure portal into Issuer URL textbox.</span></span>
    
    <span data-ttu-id="02055-172">c.</span><span class="sxs-lookup"><span data-stu-id="02055-172">c.</span></span> <span data-ttu-id="02055-173">Plak de **SAML Single Sign-On Service-URL** die u in één Service-URL aanmelding tekstvak vanuit Azure-portal hebt gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="02055-173">Paste the **SAML Single Sign-On Service URL** which you have copied from Azure portal into Single Sign-On Service URL textbox.</span></span>

    <span data-ttu-id="02055-174">d.</span><span class="sxs-lookup"><span data-stu-id="02055-174">d.</span></span> <span data-ttu-id="02055-175">Plak de **Sign-Out URL** die u in het tekstvak voor de Service-URL met eenmalige Sign-Out vanuit Azure-portal hebt gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="02055-175">Paste the **Sign-Out URL** which you have copied from Azure portal into Single Sign-Out Service URL textbox.</span></span>

    <span data-ttu-id="02055-176">e.</span><span class="sxs-lookup"><span data-stu-id="02055-176">e.</span></span> <span data-ttu-id="02055-177">Blader in het certificaat dat u hebt gedownload vanuit Azure-portal en hier uploaden.</span><span class="sxs-lookup"><span data-stu-id="02055-177">Browse the certificate which you have downloaded from Azure portal and upload here.</span></span>
    
    <span data-ttu-id="02055-178">f.</span><span class="sxs-lookup"><span data-stu-id="02055-178">f.</span></span> <span data-ttu-id="02055-179">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="02055-179">Click **Save**.</span></span>
  
> [!TIP]
> <span data-ttu-id="02055-180">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="02055-180">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="02055-181">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="02055-181">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="02055-182">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD](https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="02055-182">You can read more about the embedded documentation feature here: [Azure AD embedded documentation](https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="02055-183">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="02055-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="02055-184">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="02055-184">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="02055-186">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="02055-186">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="02055-187">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="02055-187">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="02055-189">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="02055-189">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="02055-191">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="02055-191">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="02055-193">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="02055-193">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="02055-195">a.</span><span class="sxs-lookup"><span data-stu-id="02055-195">a.</span></span> <span data-ttu-id="02055-196">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="02055-196">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="02055-197">b.</span><span class="sxs-lookup"><span data-stu-id="02055-197">b.</span></span> <span data-ttu-id="02055-198">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="02055-198">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="02055-199">c.</span><span class="sxs-lookup"><span data-stu-id="02055-199">c.</span></span> <span data-ttu-id="02055-200">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="02055-200">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="02055-201">d.</span><span class="sxs-lookup"><span data-stu-id="02055-201">d.</span></span> <span data-ttu-id="02055-202">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="02055-202">Click **Create**.</span></span>
 
### <a name="creating-a-sensoscientific-wireless-temperature-monitoring-system-test-user"></a><span data-ttu-id="02055-203">Maken van een testgebruiker SensoScientific draadloze temperatuur Monitoring System</span><span class="sxs-lookup"><span data-stu-id="02055-203">Creating a SensoScientific Wireless Temperature Monitoring System test user</span></span>

<span data-ttu-id="02055-204">Om Azure AD-gebruikers zich aanmelden bij SensoScientific draadloze temperatuur Monitoring System, moeten ze worden ingericht in SensoScientific draadloze temperatuur Monitoring System.</span><span class="sxs-lookup"><span data-stu-id="02055-204">To enable Azure AD users to log in to SensoScientific Wireless Temperature Monitoring System, they must be provisioned into SensoScientific Wireless Temperature Monitoring System.</span></span> <span data-ttu-id="02055-205">Werken met [SensoScientific draadloze temperatuur Monitoring System ondersteuningsteam](https://www.sensoscientific.com/contact-us/) om toe te voegen de gebruikers van het platform SensoScientific draadloze temperatuur Monitoring System.</span><span class="sxs-lookup"><span data-stu-id="02055-205">Work with [SensoScientific Wireless Temperature Monitoring System support team](https://www.sensoscientific.com/contact-us/) to add the users in the SensoScientific Wireless Temperature Monitoring System platform.</span></span> <span data-ttu-id="02055-206">Gebruikers moeten worden gemaakt en worden geactiveerd voordat u eenmalige aanmelding gebruiken.</span><span class="sxs-lookup"><span data-stu-id="02055-206">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="02055-207">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="02055-207">Assigning the Azure AD test user</span></span>

<span data-ttu-id="02055-208">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan SensoScientific draadloze temperatuur Monitoring System.</span><span class="sxs-lookup"><span data-stu-id="02055-208">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SensoScientific Wireless Temperature Monitoring System.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="02055-210">**Britta Simon om aan te wijzen SensoScientific draadloze temperatuur Monitoring System, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="02055-210">**To assign Britta Simon to SensoScientific Wireless Temperature Monitoring System, perform the following steps:**</span></span>

1. <span data-ttu-id="02055-211">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="02055-211">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="02055-213">Selecteer in de lijst met toepassingen **SensoScientific draadloze temperatuur Monitoring System**.</span><span class="sxs-lookup"><span data-stu-id="02055-213">In the applications list, select **SensoScientific Wireless Temperature Monitoring System**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_app.png) 

3. <span data-ttu-id="02055-215">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="02055-215">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="02055-217">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="02055-217">Click **Add** button.</span></span> <span data-ttu-id="02055-218">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="02055-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="02055-220">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="02055-220">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="02055-221">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="02055-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="02055-222">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="02055-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="02055-223">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="02055-223">Testing single sign-on</span></span>

<span data-ttu-id="02055-224">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="02055-224">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span> <span data-ttu-id="02055-225">Klik op de tegel SensoScientific draadloze temperatuur Monitoring System in het deelvenster toegang, u zal worden automatisch aangemeld bij uw toepassing SensoScientific draadloze temperatuur Monitoring System.</span><span class="sxs-lookup"><span data-stu-id="02055-225">Click the SensoScientific Wireless Temperature Monitoring System tile in the Access Panel, you will be automatically signed-on to your SensoScientific Wireless Temperature Monitoring System application.</span></span> <span data-ttu-id="02055-226">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="02055-226">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="02055-227">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="02055-227">Additional resources</span></span>

* [<span data-ttu-id="02055-228">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="02055-228">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="02055-229">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="02055-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_203.png

