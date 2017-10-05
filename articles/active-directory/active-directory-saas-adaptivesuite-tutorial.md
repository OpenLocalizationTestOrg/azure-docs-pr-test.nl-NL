---
title: 'Zelfstudie: Azure Active Directory-integratie met adaptieve Suite | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en adaptieve Suite.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 13af9d00-116a-41b8-8ca0-4870b31e224c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 5d7ba2f4c7d814e3aaa1bf804ddc5030380ccb2d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adaptive-suite"></a><span data-ttu-id="31c67-103">Zelfstudie: Azure Active Directory-integratie met adaptieve Suite</span><span class="sxs-lookup"><span data-stu-id="31c67-103">Tutorial: Azure Active Directory integration with Adaptive Suite</span></span>

<span data-ttu-id="31c67-104">In deze zelfstudie leert u hoe adaptieve Suite integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="31c67-104">In this tutorial, you learn how to integrate Adaptive Suite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="31c67-105">Adaptieve Suite integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="31c67-105">Integrating Adaptive Suite with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="31c67-106">U kunt beheren in Azure AD die toegang tot adaptieve Suite heeft</span><span class="sxs-lookup"><span data-stu-id="31c67-106">You can control in Azure AD who has access to Adaptive Suite</span></span>
- <span data-ttu-id="31c67-107">U kunt uw gebruikers automatisch ophalen aangemeld bij adaptieve Suite (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="31c67-107">You can enable your users to automatically get signed-on to Adaptive Suite (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="31c67-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="31c67-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="31c67-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="31c67-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="31c67-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="31c67-110">Prerequisites</span></span>

<span data-ttu-id="31c67-111">Voor het configureren van Azure AD-integratie met adaptieve Suite, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="31c67-111">To configure Azure AD integration with Adaptive Suite, you need the following items:</span></span>

- <span data-ttu-id="31c67-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="31c67-112">An Azure AD subscription</span></span>
- <span data-ttu-id="31c67-113">Een adaptieve Suite eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="31c67-113">An Adaptive Suite single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="31c67-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="31c67-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="31c67-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="31c67-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="31c67-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="31c67-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="31c67-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="31c67-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="31c67-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="31c67-118">Scenario description</span></span>
<span data-ttu-id="31c67-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="31c67-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="31c67-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="31c67-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="31c67-121">Adaptieve Suite uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="31c67-121">Adding Adaptive Suite from the gallery</span></span>
2. <span data-ttu-id="31c67-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="31c67-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adaptive-suite-from-the-gallery"></a><span data-ttu-id="31c67-123">Adaptieve Suite uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="31c67-123">Adding Adaptive Suite from the gallery</span></span>
<span data-ttu-id="31c67-124">Voor het configureren van de integratie van adaptieve Suite in Azure AD, moet u adaptieve Suite uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="31c67-124">To configure the integration of Adaptive Suite into Azure AD, you need to add Adaptive Suite from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="31c67-125">**Als u wilt toevoegen adaptieve Suite uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="31c67-125">**To add Adaptive Suite from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="31c67-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="31c67-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="31c67-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="31c67-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="31c67-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="31c67-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="31c67-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="31c67-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="31c67-133">Typ in het zoekvak **adaptieve Suite**.</span><span class="sxs-lookup"><span data-stu-id="31c67-133">In the search box, type **Adaptive Suite**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_search.png)

5. <span data-ttu-id="31c67-135">Selecteer in het deelvenster resultaten **adaptieve Suite**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="31c67-135">In the results panel, select **Adaptive Suite**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="31c67-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="31c67-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="31c67-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met adaptieve Suite op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="31c67-138">In this section, you configure and test Azure AD single sign-on with Adaptive Suite based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="31c67-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in adaptieve Suite is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="31c67-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Adaptive Suite is to a user in Azure AD.</span></span> <span data-ttu-id="31c67-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in adaptieve Suite tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="31c67-140">In other words, a link relationship between an Azure AD user and the related user in Adaptive Suite needs to be established.</span></span>

<span data-ttu-id="31c67-141">Wijs in adaptieve Suite de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="31c67-141">In Adaptive Suite, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="31c67-142">Om te configureren en testen van Azure AD eenmalige aanmelding met adaptieve Suite, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="31c67-142">To configure and test Azure AD single sign-on with Adaptive Suite, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="31c67-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="31c67-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="31c67-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="31c67-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="31c67-145">**[Maken van een testgebruiker adaptieve Suite](#creating-an-adaptive-suite-test-user)**  - adaptieve Suite die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="31c67-145">**[Creating an Adaptive Suite test user](#creating-an-adaptive-suite-test-user)** - to have a counterpart of Britta Simon in Adaptive Suite that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="31c67-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="31c67-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="31c67-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="31c67-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="31c67-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="31c67-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="31c67-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw toepassing adaptieve Suite.</span><span class="sxs-lookup"><span data-stu-id="31c67-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Adaptive Suite application.</span></span>

<span data-ttu-id="31c67-150">**Voor het configureren van eenmalige aanmelding Azure AD met adaptieve Suite, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="31c67-150">**To configure Azure AD single sign-on with Adaptive Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="31c67-151">In de Azure-portal op de **adaptieve Suite** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="31c67-151">In the Azure portal, on the **Adaptive Suite** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="31c67-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="31c67-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_samlbase.png)

3. <span data-ttu-id="31c67-155">Op de **adaptieve Suite domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="31c67-155">On the **Adaptive Suite Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_url.png)

    <span data-ttu-id="31c67-157">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://login.adaptiveinsights.com:443/samlsso/<unique-id>`</span><span class="sxs-lookup"><span data-stu-id="31c67-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://login.adaptiveinsights.com:443/samlsso/<unique-id>`</span></span>

    >[!NOTE]
    > <span data-ttu-id="31c67-158">U kunt deze waarde niet ophalen uit de adaptieve Suite **SAML SSO instellingen** pagina.</span><span class="sxs-lookup"><span data-stu-id="31c67-158">You can get this value from the Adaptive Suite’s **SAML SSO Settings** page.</span></span>
    >  

4. <span data-ttu-id="31c67-159">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="31c67-159">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_certificate.png) 

5. <span data-ttu-id="31c67-161">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="31c67-161">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="31c67-163">Op de **geavanceerde configuratie van de Suite** sectie, klikt u op **adaptieve Suite configureren** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="31c67-163">On the **Adaptive Suite Configuration** section, click **Configure Adaptive Suite** to open **Configure sign-on** window.</span></span> <span data-ttu-id="31c67-164">Kopieer de **SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="31c67-164">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_configure.png) 

7. <span data-ttu-id="31c67-166">In een ander browservenster, meld u aan bij uw bedrijf adaptieve Suite site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="31c67-166">In a different web browser window, log in to your Adaptive Suite company site as an administrator.</span></span>

8. <span data-ttu-id="31c67-167">Ga naar **Admin**.</span><span class="sxs-lookup"><span data-stu-id="31c67-167">Go to **Admin**.</span></span>
   
    <span data-ttu-id="31c67-168">![Beheerder](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="31c67-168">![Admin](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Admin")</span></span>

9. <span data-ttu-id="31c67-169">In de **gebruikers en rollen** sectie, klikt u op **SAML SSO-instellingen beheren**.</span><span class="sxs-lookup"><span data-stu-id="31c67-169">In the **Users and Roles** section, click **Manage SAML SSO Settings**.</span></span>
   
    <span data-ttu-id="31c67-170">![SAML SSO-instellingen beheren](./media/active-directory-saas-adaptivesuite-tutorial/IC805645.png "SAML SSO-instellingen beheren")</span><span class="sxs-lookup"><span data-stu-id="31c67-170">![Manage SAML SSO Settings](./media/active-directory-saas-adaptivesuite-tutorial/IC805645.png "Manage SAML SSO Settings")</span></span>

10. <span data-ttu-id="31c67-171">Op de **SAML SSO instellingen** pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="31c67-171">On the **SAML SSO Settings** page, perform the following steps:</span></span>
   
    <span data-ttu-id="31c67-172">![Instellingen voor eenmalige aanmelding SAML](./media/active-directory-saas-adaptivesuite-tutorial/IC805646.png "SAML SSO-instellingen")</span><span class="sxs-lookup"><span data-stu-id="31c67-172">![SAML SSO Settings](./media/active-directory-saas-adaptivesuite-tutorial/IC805646.png "SAML SSO Settings")</span></span>

    <span data-ttu-id="31c67-173">a.</span><span class="sxs-lookup"><span data-stu-id="31c67-173">a.</span></span> <span data-ttu-id="31c67-174">In de **identiteit providernaam** textbox, typ een naam voor uw configuratie.</span><span class="sxs-lookup"><span data-stu-id="31c67-174">In the **Identity provider name** textbox, type a name for your configuration.</span></span>
    
    <span data-ttu-id="31c67-175">b.</span><span class="sxs-lookup"><span data-stu-id="31c67-175">b.</span></span> <span data-ttu-id="31c67-176">Plak de **SAML entiteit-ID** waarde opgehaald uit Azure-portal in de **identiteitsprovider entiteit-ID** textbox.</span><span class="sxs-lookup"><span data-stu-id="31c67-176">Paste the **SAML Entity ID** value copied from Azure portal into the **Identity provider Entity ID** textbox.</span></span>
  
    <span data-ttu-id="31c67-177">c.</span><span class="sxs-lookup"><span data-stu-id="31c67-177">c.</span></span> <span data-ttu-id="31c67-178">Plak de **SAML Single Sign-On Service-URL** waarde opgehaald uit Azure-portal in de **identiteitsprovider SSO-URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="31c67-178">Paste the **SAML Single Sign-On Service URL** value copied from Azure portal into the **Identity provider SSO URL** textbox.</span></span>
  
    <span data-ttu-id="31c67-179">d.</span><span class="sxs-lookup"><span data-stu-id="31c67-179">d.</span></span> <span data-ttu-id="31c67-180">Plak de **SAML Single Sign-On Service-URL** waarde opgehaald uit Azure-portal in de **aangepaste afmelding URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="31c67-180">Paste the **SAML Single Sign-On Service URL** value copied from Azure portal into the **Custom logout URL** textbox.</span></span>
  
    <span data-ttu-id="31c67-181">e.</span><span class="sxs-lookup"><span data-stu-id="31c67-181">e.</span></span> <span data-ttu-id="31c67-182">Als u wilt uw gedownloade certificaat uploaden, klikt u op **bestand kiezen**.</span><span class="sxs-lookup"><span data-stu-id="31c67-182">To upload your downloaded certificate, click **Choose file**.</span></span>
  
    <span data-ttu-id="31c67-183">f.</span><span class="sxs-lookup"><span data-stu-id="31c67-183">f.</span></span> <span data-ttu-id="31c67-184">Selecteer het volgende voor:</span><span class="sxs-lookup"><span data-stu-id="31c67-184">Select the following, for:</span></span>
    * <span data-ttu-id="31c67-185">**Gebruikers-id van SAML**, selecteer **adaptieve Insights gebruiker gebruikersnaam**.</span><span class="sxs-lookup"><span data-stu-id="31c67-185">**SAML user id**, select **User’s Adaptive Insights user name**.</span></span>
    * <span data-ttu-id="31c67-186">**Locatie van het SAML-id**, selecteer **gebruikers-id in NameID van onderwerp**.</span><span class="sxs-lookup"><span data-stu-id="31c67-186">**SAML user id location**, select **User id in NameID of Subject**.</span></span>
    * <span data-ttu-id="31c67-187">**SAML NameID indeling**, selecteer **e-mailadres**.</span><span class="sxs-lookup"><span data-stu-id="31c67-187">**SAML NameID format**, select **Email address**.</span></span>
    * <span data-ttu-id="31c67-188">**SAML inschakelen**, selecteer **toestaan SAML SSO en direct adaptieve Insights aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="31c67-188">**Enable SAML**, select **Allow SAML SSO and direct Adaptive Insights login**.</span></span>
    
    <span data-ttu-id="31c67-189">g.</span><span class="sxs-lookup"><span data-stu-id="31c67-189">g.</span></span> <span data-ttu-id="31c67-190">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="31c67-190">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="31c67-191">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="31c67-191">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="31c67-192">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="31c67-192">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="31c67-193">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="31c67-193">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="31c67-194">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="31c67-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="31c67-195">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="31c67-195">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="31c67-197">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="31c67-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="31c67-198">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="31c67-198">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="31c67-200">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="31c67-200">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="31c67-202">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="31c67-202">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="31c67-204">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="31c67-204">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="31c67-206">a.</span><span class="sxs-lookup"><span data-stu-id="31c67-206">a.</span></span> <span data-ttu-id="31c67-207">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="31c67-207">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="31c67-208">b.</span><span class="sxs-lookup"><span data-stu-id="31c67-208">b.</span></span> <span data-ttu-id="31c67-209">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="31c67-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="31c67-210">c.</span><span class="sxs-lookup"><span data-stu-id="31c67-210">c.</span></span> <span data-ttu-id="31c67-211">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="31c67-211">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="31c67-212">d.</span><span class="sxs-lookup"><span data-stu-id="31c67-212">d.</span></span> <span data-ttu-id="31c67-213">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="31c67-213">Click **Create**.</span></span>
 
### <a name="creating-an-adaptive-suite-test-user"></a><span data-ttu-id="31c67-214">Maken van een testgebruiker adaptieve Suite</span><span class="sxs-lookup"><span data-stu-id="31c67-214">Creating an Adaptive Suite test user</span></span>

<span data-ttu-id="31c67-215">Om Azure AD-gebruikers zich aanmelden bij adaptieve Suite, moeten ze worden ingericht in adaptieve Suite.</span><span class="sxs-lookup"><span data-stu-id="31c67-215">To enable Azure AD users to log in to Adaptive Suite, they must be provisioned into Adaptive Suite.</span></span>  

* <span data-ttu-id="31c67-216">In het geval van adaptieve Suite is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="31c67-216">In the case of Adaptive Suite, provisioning is a manual task.</span></span>

<span data-ttu-id="31c67-217">**Als u wilt configureren voor gebruikers inrichten, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="31c67-217">**To configure user provisioning, perform the following steps:**</span></span> 

1. <span data-ttu-id="31c67-218">Meld u aan bij uw **adaptieve Suite** bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="31c67-218">Log in to your **Adaptive Suite** company site as an administrator.</span></span>
2. <span data-ttu-id="31c67-219">Ga naar **Admin**.</span><span class="sxs-lookup"><span data-stu-id="31c67-219">Go to **Admin**.</span></span>
   
   <span data-ttu-id="31c67-220">![Beheerder](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="31c67-220">![Admin](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Admin")</span></span>
3. <span data-ttu-id="31c67-221">In de **gebruikers en rollen** sectie, klikt u op **gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="31c67-221">In the **Users and Roles** section, click **Add User**.</span></span>
   
   <span data-ttu-id="31c67-222">![Gebruiker toevoegen](./media/active-directory-saas-adaptivesuite-tutorial/IC805648.png "gebruiker toevoegen")</span><span class="sxs-lookup"><span data-stu-id="31c67-222">![Add User](./media/active-directory-saas-adaptivesuite-tutorial/IC805648.png "Add User")</span></span>
4. <span data-ttu-id="31c67-223">In de **nieuwe gebruiker** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="31c67-223">In the **New User** section, perform the following steps:</span></span>
   
   <span data-ttu-id="31c67-224">![Indienen](./media/active-directory-saas-adaptivesuite-tutorial/IC805649.png "verzenden")</span><span class="sxs-lookup"><span data-stu-id="31c67-224">![Submit](./media/active-directory-saas-adaptivesuite-tutorial/IC805649.png "Submit")</span></span>   

   <span data-ttu-id="31c67-225">a.</span><span class="sxs-lookup"><span data-stu-id="31c67-225">a.</span></span> <span data-ttu-id="31c67-226">Typ de **naam**, **aanmelding**, **e**, **wachtwoord** van een geldige Azure Active Directory-gebruiker die u inrichten in de bijbehorende tekstvakken wilt.</span><span class="sxs-lookup"><span data-stu-id="31c67-226">Type the **Name**, **Login**, **Email**, **Password** of a valid Azure Active Directory user you want to provision into the related textboxes.</span></span>
  
   <span data-ttu-id="31c67-227">b.</span><span class="sxs-lookup"><span data-stu-id="31c67-227">b.</span></span> <span data-ttu-id="31c67-228">Selecteer een **rol**.</span><span class="sxs-lookup"><span data-stu-id="31c67-228">Select a **Role**.</span></span>
  
   <span data-ttu-id="31c67-229">c.</span><span class="sxs-lookup"><span data-stu-id="31c67-229">c.</span></span> <span data-ttu-id="31c67-230">Klik op **indienen**.</span><span class="sxs-lookup"><span data-stu-id="31c67-230">Click **Submit**.</span></span>

>[!NOTE]
><span data-ttu-id="31c67-231">U kunt andere adaptieve Suite gebruiker account hulpmiddelen voor het maken of API's geleverd door adaptieve Suite aan inrichten AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="31c67-231">You can use any other Adaptive Suite user account creation tools or APIs provided by Adaptive Suite to provision AAD user accounts.</span></span>
>  

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="31c67-232">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="31c67-232">Assigning the Azure AD test user</span></span>

<span data-ttu-id="31c67-233">In deze sectie maakt inschakelen u Britta Simon toegang verlenen aan adaptieve Suite gebruikt Azure eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="31c67-233">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Adaptive Suite.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="31c67-235">**Als u wilt toewijzen Britta Simon adaptieve Suite, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="31c67-235">**To assign Britta Simon to Adaptive Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="31c67-236">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="31c67-236">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="31c67-238">Selecteer in de lijst met toepassingen **adaptieve Suite**.</span><span class="sxs-lookup"><span data-stu-id="31c67-238">In the applications list, select **Adaptive Suite**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_app.png) 

3. <span data-ttu-id="31c67-240">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="31c67-240">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="31c67-242">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="31c67-242">Click **Add** button.</span></span> <span data-ttu-id="31c67-243">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="31c67-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="31c67-245">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="31c67-245">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="31c67-246">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="31c67-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="31c67-247">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="31c67-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="31c67-248">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="31c67-248">Testing single sign-on</span></span>

<span data-ttu-id="31c67-249">Het doel van deze sectie is het testen van uw Microsoft Azure AD Single Sign-On configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="31c67-249">The objective of this section is to test your Microsoft Azure AD Single Sign-On configuration using the Access Panel.</span></span>

<span data-ttu-id="31c67-250">Als u op de tegel adaptieve Suite in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing adaptieve Suite.</span><span class="sxs-lookup"><span data-stu-id="31c67-250">When you click the Adaptive Suite tile in the Access Panel, you should get automatically signed-on to your Adaptive Suite application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="31c67-251">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="31c67-251">Additional resources</span></span>

* [<span data-ttu-id="31c67-252">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="31c67-252">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="31c67-253">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="31c67-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_203.png

