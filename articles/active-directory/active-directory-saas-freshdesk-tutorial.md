---
title: 'Zelfstudie: Azure Active Directory-integratie met FreshDesk | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en FreshDesk.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2a3e5aa-7b5a-4fe4-9285-45dbe6e8efcc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: f4b47e345a40b64f69ad8a4618564662b4a6c879
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-freshdesk"></a><span data-ttu-id="2c9be-103">Zelfstudie: Azure Active Directory-integratie met FreshDesk</span><span class="sxs-lookup"><span data-stu-id="2c9be-103">Tutorial: Azure Active Directory integration with FreshDesk</span></span>

<span data-ttu-id="2c9be-104">In deze zelfstudie leert u hoe FreshDesk integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2c9be-104">In this tutorial, you learn how to integrate FreshDesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2c9be-105">FreshDesk integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="2c9be-105">Integrating FreshDesk with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2c9be-106">U kunt beheren in Azure AD die toegang tot FreshDesk heeft</span><span class="sxs-lookup"><span data-stu-id="2c9be-106">You can control in Azure AD who has access to FreshDesk</span></span>
- <span data-ttu-id="2c9be-107">U kunt uw gebruikers automatisch ophalen aangemeld bij FreshDesk (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="2c9be-107">You can enable your users to automatically get signed-on to FreshDesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2c9be-108">U kunt uw accounts op één centrale locatie - en de Azure Management portal beheren</span><span class="sxs-lookup"><span data-stu-id="2c9be-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="2c9be-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2c9be-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2c9be-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="2c9be-110">Prerequisites</span></span>

<span data-ttu-id="2c9be-111">Voor het configureren van Azure AD-integratie met FreshDesk, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="2c9be-111">To configure Azure AD integration with FreshDesk, you need the following items:</span></span>

- <span data-ttu-id="2c9be-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="2c9be-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2c9be-113">Een FreshDesk eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="2c9be-113">A FreshDesk single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2c9be-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="2c9be-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2c9be-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="2c9be-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2c9be-116">U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="2c9be-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="2c9be-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2c9be-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2c9be-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="2c9be-118">Scenario description</span></span>
<span data-ttu-id="2c9be-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="2c9be-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2c9be-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="2c9be-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2c9be-121">FreshDesk uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="2c9be-121">Adding FreshDesk from the gallery</span></span>
2. <span data-ttu-id="2c9be-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="2c9be-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-freshdesk-from-the-gallery"></a><span data-ttu-id="2c9be-123">FreshDesk uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="2c9be-123">Adding FreshDesk from the gallery</span></span>
<span data-ttu-id="2c9be-124">Voor het configureren van de integratie van FreshDesk in Azure AD, moet u FreshDesk uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="2c9be-124">To configure the integration of FreshDesk into Azure AD, you need to add FreshDesk from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2c9be-125">**Als u wilt toevoegen FreshDesk uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="2c9be-125">**To add FreshDesk from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2c9be-126">In de  **[Azure Management Portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="2c9be-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2c9be-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="2c9be-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2c9be-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="2c9be-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="2c9be-131">Klik op **toevoegen** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2c9be-131">Click **Add** button on the top of the dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="2c9be-133">Typ in het zoekvak **FreshDesk**.</span><span class="sxs-lookup"><span data-stu-id="2c9be-133">In the search box, type **FreshDesk**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_search.png)

5. <span data-ttu-id="2c9be-135">Selecteer in het deelvenster resultaten **FreshDesk**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="2c9be-135">In the results panel, select **FreshDesk**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2c9be-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="2c9be-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2c9be-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met FreshDesk op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="2c9be-138">In this section, you configure and test Azure AD single sign-on with FreshDesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2c9be-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in FreshDesk is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2c9be-139">For single sign-on to work, Azure AD needs to know what the counterpart user in FreshDesk is to a user in Azure AD.</span></span> <span data-ttu-id="2c9be-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in FreshDesk tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="2c9be-140">In other words, a link relationship between an Azure AD user and the related user in FreshDesk needs to be established.</span></span>

<span data-ttu-id="2c9be-141">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in FreshDesk.</span><span class="sxs-lookup"><span data-stu-id="2c9be-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in FreshDesk.</span></span>

<span data-ttu-id="2c9be-142">Om te configureren en testen van Azure AD eenmalige aanmelding met FreshDesk, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="2c9be-142">To configure and test Azure AD single sign-on with FreshDesk, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2c9be-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2c9be-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2c9be-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2c9be-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2c9be-145">**[Maken van een testgebruiker FreshDesk](#creating-a-freshdesk-test-user)**  - FreshDesk die is gekoppeld aan de Azure AD-representatie van haar van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="2c9be-145">**[Creating a FreshDesk test user](#creating-a-freshdesk-test-user)** - to have a counterpart of Britta Simon in FreshDesk that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="2c9be-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="2c9be-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2c9be-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="2c9be-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2c9be-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="2c9be-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2c9be-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure-beheerportal en eenmalige aanmelding in uw toepassing FreshDesk configureren.</span><span class="sxs-lookup"><span data-stu-id="2c9be-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your FreshDesk application.</span></span>

<span data-ttu-id="2c9be-150">**Voor het configureren van Azure AD eenmalige aanmelding met FreshDesk, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="2c9be-150">**To configure Azure AD single sign-on with FreshDesk, perform the following steps:**</span></span>

1. <span data-ttu-id="2c9be-151">In de Azure-beheerportal op de **FreshDesk** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="2c9be-151">In the Azure Management portal, on the **FreshDesk** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="2c9be-153">Op de **eenmalige aanmelding** dialoogvenster als **modus** Selecteer **op basis van SAML aanmelding** eenmalige aanmelding inschakelen op.</span><span class="sxs-lookup"><span data-stu-id="2c9be-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_samlbase.png)

3. <span data-ttu-id="2c9be-155">Op de **FreshDesk domein en de URL's** sectie, voer de **aanmeldings-URL** als: `https://<tenant-name>.freshdesk.com` of een andere waarde Freshdesk is voorgesteld.</span><span class="sxs-lookup"><span data-stu-id="2c9be-155">On the **FreshDesk Domain and URLs** section, please enter the **Sign-on URL** as: `https://<tenant-name>.freshdesk.com` or any other value Freshdesk has suggested.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_url.png)

    > [!NOTE] 
    > <span data-ttu-id="2c9be-157">Houd er rekening mee dat dit geen de feitelijke waarde is.</span><span class="sxs-lookup"><span data-stu-id="2c9be-157">Please note that this is not the real value.</span></span> <span data-ttu-id="2c9be-158">U moet de waarde wordt bijgewerkt met de werkelijke URL voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="2c9be-158">You have to update the value with the actual Sign-on URL.</span></span> <span data-ttu-id="2c9be-159">Neem contact op met [FreshDesk Client ondersteuningsteam](https://freshdesk.com/helpdesk-software?utm_source=Google-AdWords&utm_medium=Search-IND-Brand&utm_campaign=Search-IND-Brand&utm_term=freshdesk&device=c&gclid=COSH2_LH7NICFVUDvAodBPgBZg) deze waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="2c9be-159">Contact [FreshDesk Client support team](https://freshdesk.com/helpdesk-software?utm_source=Google-AdWords&utm_medium=Search-IND-Brand&utm_campaign=Search-IND-Brand&utm_term=freshdesk&device=c&gclid=COSH2_LH7NICFVUDvAodBPgBZg) to get this value.</span></span>  

4. <span data-ttu-id="2c9be-160">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat** en sla het certificaat op uw computer.</span><span class="sxs-lookup"><span data-stu-id="2c9be-160">On the **SAML Signing Certificate** section, click **Certificate** and then save the certificate on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_certificate.png) 

5. <span data-ttu-id="2c9be-162">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="2c9be-162">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-freshdesk-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2c9be-164">Op de **FreshDesk configuratie** sectie, klikt u op **FreshDesk configureren** om configureren aanmelding venster te openen.</span><span class="sxs-lookup"><span data-stu-id="2c9be-164">On the **FreshDesk Configuration** section, click **Configure FreshDesk** to open Configure sign-on window.</span></span> <span data-ttu-id="2c9be-165">Kopieer de SAML Single Sign-On Service-URL en Sign-Out URL uit de **Naslaggids** sectie.</span><span class="sxs-lookup"><span data-stu-id="2c9be-165">Copy the SAML Single Sign-On Service URL and Sign-Out URL from the **Quick Reference** section.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_configure.png)

7. <span data-ttu-id="2c9be-167">In een ander browservenster, meld u bij uw bedrijf Freshdesk site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="2c9be-167">In a different web browser window, log into your Freshdesk company site as an administrator.</span></span>

8. <span data-ttu-id="2c9be-168">Klik in het menu bovenaan op **Admin**.</span><span class="sxs-lookup"><span data-stu-id="2c9be-168">In the menu on the top, click **Admin**.</span></span>
   
   <span data-ttu-id="2c9be-169">![Beheerder](./media/active-directory-saas-freshdesk-tutorial/IC776768.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="2c9be-169">![Admin](./media/active-directory-saas-freshdesk-tutorial/IC776768.png "Admin")</span></span>

9. <span data-ttu-id="2c9be-170">In de **algemene instellingen** tabblad **beveiliging**.</span><span class="sxs-lookup"><span data-stu-id="2c9be-170">In the **General Settings** tab, click **Security**.</span></span>
   
   <span data-ttu-id="2c9be-171">![Beveiliging](./media/active-directory-saas-freshdesk-tutorial/IC776769.png "beveiliging")</span><span class="sxs-lookup"><span data-stu-id="2c9be-171">![Security](./media/active-directory-saas-freshdesk-tutorial/IC776769.png "Security")</span></span>

10. <span data-ttu-id="2c9be-172">In de **beveiliging** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="2c9be-172">In the **Security** section, perform the following steps:</span></span>
   
    <span data-ttu-id="2c9be-173">![Eenmalige aanmelding](./media/active-directory-saas-freshdesk-tutorial/IC776770.png "eenmalige aanmelding")</span><span class="sxs-lookup"><span data-stu-id="2c9be-173">![Single Sign On](./media/active-directory-saas-freshdesk-tutorial/IC776770.png "Single Sign On")</span></span>
   
    <span data-ttu-id="2c9be-174">a.</span><span class="sxs-lookup"><span data-stu-id="2c9be-174">a.</span></span> <span data-ttu-id="2c9be-175">Voor **eenmalige aanmelding op (SSO)**, selecteer **op**.</span><span class="sxs-lookup"><span data-stu-id="2c9be-175">For **Single Sign On (SSO)**, select **On**.</span></span>

    <span data-ttu-id="2c9be-176">b.</span><span class="sxs-lookup"><span data-stu-id="2c9be-176">b.</span></span> <span data-ttu-id="2c9be-177">Selecteer **SAML SSO**.</span><span class="sxs-lookup"><span data-stu-id="2c9be-177">Select **SAML SSO**.</span></span>

    <span data-ttu-id="2c9be-178">c.</span><span class="sxs-lookup"><span data-stu-id="2c9be-178">c.</span></span> <span data-ttu-id="2c9be-179">Type de **SAML Single Sign-On Service-URL** u hebt gekopieerd uit de Azure-portal in de **aanmeldings-URL van SAML** textbox.</span><span class="sxs-lookup"><span data-stu-id="2c9be-179">Type the **SAML Single Sign-On Service URL** you copied from Azure portal into the **SAML Login URL** textbox.</span></span>

    <span data-ttu-id="2c9be-180">d.</span><span class="sxs-lookup"><span data-stu-id="2c9be-180">d.</span></span> <span data-ttu-id="2c9be-181">Type de **Sign-Out URL** u hebt gekopieerd uit de Azure-portal in de **afmelding URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="2c9be-181">Type the **Sign-Out URL**  you copied from Azure portal into the **Logout URL** textbox.</span></span>

    <span data-ttu-id="2c9be-182">e.</span><span class="sxs-lookup"><span data-stu-id="2c9be-182">e.</span></span> <span data-ttu-id="2c9be-183">Kopieer de **vingerafdruk** waarde uit het gedownloade certificaat vanuit Azure-portal en plak deze in de **beveiliging certificaat vingerafdruk** textbox.</span><span class="sxs-lookup"><span data-stu-id="2c9be-183">Copy the **Thumbprint** value from the downloaded certificate from Azure portal and paste it into the **Security Certificate Fingerprint** textbox.</span></span>  
 
    >[!TIP]
    ><span data-ttu-id="2c9be-184">Zie voor meer informatie [hoe op te halen van een certificaat vingerafdrukwaarde](http://youtu.be/YKQF266SAxI).</span><span class="sxs-lookup"><span data-stu-id="2c9be-184">For more details, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span></span> 
    
    <span data-ttu-id="2c9be-185">f.</span><span class="sxs-lookup"><span data-stu-id="2c9be-185">f.</span></span> <span data-ttu-id="2c9be-186">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="2c9be-186">Click **Save**.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2c9be-187">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="2c9be-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="2c9be-188">Het doel van deze sectie is het een testgebruiker maken in Azure Management portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="2c9be-188">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="2c9be-190">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="2c9be-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2c9be-191">In de **Azure Management portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="2c9be-191">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2c9be-193">Ga naar **gebruikers en groepen** en klik op **alle gebruikers** om de lijst met gebruikers weer te geven.</span><span class="sxs-lookup"><span data-stu-id="2c9be-193">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2c9be-195">Klik aan de bovenkant van het dialoogvenster **toevoegen** openen de **gebruiker** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2c9be-195">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2c9be-197">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="2c9be-197">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2c9be-199">a.</span><span class="sxs-lookup"><span data-stu-id="2c9be-199">a.</span></span> <span data-ttu-id="2c9be-200">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2c9be-200">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2c9be-201">b.</span><span class="sxs-lookup"><span data-stu-id="2c9be-201">b.</span></span> <span data-ttu-id="2c9be-202">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2c9be-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2c9be-203">c.</span><span class="sxs-lookup"><span data-stu-id="2c9be-203">c.</span></span> <span data-ttu-id="2c9be-204">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="2c9be-204">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="2c9be-205">d.</span><span class="sxs-lookup"><span data-stu-id="2c9be-205">d.</span></span> <span data-ttu-id="2c9be-206">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="2c9be-206">Click **Create**.</span></span>
 
### <a name="creating-a-freshdesk-test-user"></a><span data-ttu-id="2c9be-207">Een testgebruiker FreshDesk maken</span><span class="sxs-lookup"><span data-stu-id="2c9be-207">Creating a FreshDesk test user</span></span>

<span data-ttu-id="2c9be-208">Om in te schakelen gebruikers van Azure AD aan te melden bij FreshDesk, moeten ze worden ingericht in FreshDesk.</span><span class="sxs-lookup"><span data-stu-id="2c9be-208">In order to enable Azure AD users to log into FreshDesk, they must be provisioned into FreshDesk.</span></span>  
<span data-ttu-id="2c9be-209">In het geval van FreshDesk is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="2c9be-209">In the case of FreshDesk, provisioning is a manual task.</span></span>

<span data-ttu-id="2c9be-210">**Voor het inrichten van een gebruikersaccount, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="2c9be-210">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="2c9be-211">Meld u aan bij uw **Freshdesk** tenant.</span><span class="sxs-lookup"><span data-stu-id="2c9be-211">Log in to your **Freshdesk** tenant.</span></span>
2. <span data-ttu-id="2c9be-212">Klik in het menu bovenaan op **Admin**.</span><span class="sxs-lookup"><span data-stu-id="2c9be-212">In the menu on the top, click **Admin**.</span></span>
   
   <span data-ttu-id="2c9be-213">![Beheerder](./media/active-directory-saas-freshdesk-tutorial/IC776772.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="2c9be-213">![Admin](./media/active-directory-saas-freshdesk-tutorial/IC776772.png "Admin")</span></span>

3. <span data-ttu-id="2c9be-214">In de **algemene instellingen** tabblad **Agents**.</span><span class="sxs-lookup"><span data-stu-id="2c9be-214">In the **General Settings** tab, click **Agents**.</span></span>
   
   <span data-ttu-id="2c9be-215">![Agents](./media/active-directory-saas-freshdesk-tutorial/IC776773.png "Agents")</span><span class="sxs-lookup"><span data-stu-id="2c9be-215">![Agents](./media/active-directory-saas-freshdesk-tutorial/IC776773.png "Agents")</span></span>

4. <span data-ttu-id="2c9be-216">Klik op **nieuwe Agent**.</span><span class="sxs-lookup"><span data-stu-id="2c9be-216">Click **New Agent**.</span></span>
   
    <span data-ttu-id="2c9be-217">![De nieuwe Agent](./media/active-directory-saas-freshdesk-tutorial/IC776774.png "nieuwe-Agent")</span><span class="sxs-lookup"><span data-stu-id="2c9be-217">![New Agent](./media/active-directory-saas-freshdesk-tutorial/IC776774.png "New Agent")</span></span>

5. <span data-ttu-id="2c9be-218">Voer de volgende stappen uit in het dialoogvenster gegevens van agents:</span><span class="sxs-lookup"><span data-stu-id="2c9be-218">On the Agent Information dialog, perform the following steps:</span></span>
   
   <span data-ttu-id="2c9be-219">![Agentgegevens](./media/active-directory-saas-freshdesk-tutorial/IC776775.png "agentgegevens")</span><span class="sxs-lookup"><span data-stu-id="2c9be-219">![Agent Information](./media/active-directory-saas-freshdesk-tutorial/IC776775.png "Agent Information")</span></span>
   
   <span data-ttu-id="2c9be-220">a.</span><span class="sxs-lookup"><span data-stu-id="2c9be-220">a.</span></span> <span data-ttu-id="2c9be-221">In de **volledige naam** textbox, typ de naam van de Azure AD-account dat u inrichten wilt.</span><span class="sxs-lookup"><span data-stu-id="2c9be-221">In the **Full Name** textbox, type the name of the Azure AD account you want to provision.</span></span>

   <span data-ttu-id="2c9be-222">b.</span><span class="sxs-lookup"><span data-stu-id="2c9be-222">b.</span></span> <span data-ttu-id="2c9be-223">In de **e** textbox type de Azure AD-e-mailadres van de Azure AD-account dat u inrichten wilt.</span><span class="sxs-lookup"><span data-stu-id="2c9be-223">In the **Email** textbox, type the Azure AD email address of the Azure AD account you want to provision.</span></span>

   <span data-ttu-id="2c9be-224">c.</span><span class="sxs-lookup"><span data-stu-id="2c9be-224">c.</span></span> <span data-ttu-id="2c9be-225">In de **titel** textbox, typ de titel van de Azure AD-account dat u inrichten wilt.</span><span class="sxs-lookup"><span data-stu-id="2c9be-225">In the **Title** textbox, type the title of the Azure AD account you want to provision.</span></span>

   <span data-ttu-id="2c9be-226">d.</span><span class="sxs-lookup"><span data-stu-id="2c9be-226">d.</span></span> <span data-ttu-id="2c9be-227">Selecteer **Agents rol**, en klik vervolgens op **toewijzen**.</span><span class="sxs-lookup"><span data-stu-id="2c9be-227">Select **Agents role**, and then click **Assign**.</span></span>
       
   <span data-ttu-id="2c9be-228">e.</span><span class="sxs-lookup"><span data-stu-id="2c9be-228">e.</span></span> <span data-ttu-id="2c9be-229">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="2c9be-229">Click **Save**.</span></span>     
   
    >[!NOTE]
    ><span data-ttu-id="2c9be-230">De accounthouder Azure AD ontvangt een e-mailbericht een koppeling om te bevestigen van het account bevat voordat deze wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="2c9be-230">The Azure AD account holder will get an email that includes a link to confirm the account before it is activated.</span></span> 
    > 
    
    >[!NOTE]
    ><span data-ttu-id="2c9be-231">U kunt andere Freshdesk gebruiker account hulpmiddelen voor het maken of API's die is geleverd door Freshdesk aan inrichten AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="2c9be-231">You can use any other Freshdesk user account creation tools or APIs provided by Freshdesk to provision AAD user accounts.</span></span> <span data-ttu-id="2c9be-232">naar FreshDesk.</span><span class="sxs-lookup"><span data-stu-id="2c9be-232">to FreshDesk.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="2c9be-233">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="2c9be-233">Assigning the Azure AD test user</span></span>

<span data-ttu-id="2c9be-234">In deze sectie maakt inschakelen u Britta Simon Azure eenmalige aanmelding gebruiken door haar toegang te verlenen aan vak.</span><span class="sxs-lookup"><span data-stu-id="2c9be-234">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Box.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="2c9be-236">**Britta Simon om aan te wijzen FreshDesk, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="2c9be-236">**To assign Britta Simon to FreshDesk, perform the following steps:**</span></span>

1. <span data-ttu-id="2c9be-237">In de Azure-beheerportal, opent u de weergave toepassingen en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="2c9be-237">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="2c9be-239">Selecteer in de lijst met toepassingen **FreshDesk**.</span><span class="sxs-lookup"><span data-stu-id="2c9be-239">In the applications list, select **FreshDesk**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_app.png) 

3. <span data-ttu-id="2c9be-241">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="2c9be-241">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="2c9be-243">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="2c9be-243">Click **Add** button.</span></span> <span data-ttu-id="2c9be-244">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2c9be-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="2c9be-246">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="2c9be-246">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="2c9be-247">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2c9be-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2c9be-248">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2c9be-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2c9be-249">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="2c9be-249">Testing single sign-on</span></span>

<span data-ttu-id="2c9be-250">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="2c9be-250">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="2c9be-251">Als u op de tegel FreshDesk in het deelvenster toegang, krijgt u de aanmeldingspagina te verkrijgen aangemeld bij uw toepassing FreshDesk.</span><span class="sxs-lookup"><span data-stu-id="2c9be-251">When you click the FreshDesk tile in the Access Panel, you should get login page to get signed-on to your FreshDesk application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2c9be-252">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="2c9be-252">Additional resources</span></span>

* [<span data-ttu-id="2c9be-253">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2c9be-253">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2c9be-254">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2c9be-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_203.png

