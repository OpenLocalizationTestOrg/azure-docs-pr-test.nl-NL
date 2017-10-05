---
title: 'Zelfstudie: Azure Active Directory-integratie met Syncplicity | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Syncplicity.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 896a3211-f368-46d7-95b8-e4768c23be08
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 1321fa71bcd625d6ea754432bfb402d3919e38f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-syncplicity"></a><span data-ttu-id="c6461-103">Zelfstudie: Azure Active Directory-integratie met Syncplicity</span><span class="sxs-lookup"><span data-stu-id="c6461-103">Tutorial: Azure Active Directory integration with Syncplicity</span></span>

<span data-ttu-id="c6461-104">In deze zelfstudie leert u hoe Syncplicity integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c6461-104">In this tutorial, you learn how to integrate Syncplicity with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c6461-105">Syncplicity integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="c6461-105">Integrating Syncplicity with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c6461-106">U kunt beheren in Azure AD die toegang tot Syncplicity heeft</span><span class="sxs-lookup"><span data-stu-id="c6461-106">You can control in Azure AD who has access to Syncplicity</span></span>
- <span data-ttu-id="c6461-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Syncplicity (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="c6461-107">You can enable your users to automatically get signed-on to Syncplicity (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c6461-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="c6461-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c6461-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c6461-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c6461-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="c6461-110">Prerequisites</span></span>

<span data-ttu-id="c6461-111">Voor het configureren van Azure AD-integratie met Syncplicity, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="c6461-111">To configure Azure AD integration with Syncplicity, you need the following items:</span></span>

- <span data-ttu-id="c6461-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="c6461-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c6461-113">Een Syncplicity eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="c6461-113">A Syncplicity single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c6461-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="c6461-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c6461-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="c6461-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c6461-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="c6461-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c6461-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c6461-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c6461-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="c6461-118">Scenario description</span></span>
<span data-ttu-id="c6461-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="c6461-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c6461-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="c6461-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c6461-121">Syncplicity uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="c6461-121">Adding Syncplicity from the gallery</span></span>
2. <span data-ttu-id="c6461-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="c6461-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-syncplicity-from-the-gallery"></a><span data-ttu-id="c6461-123">Syncplicity uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="c6461-123">Adding Syncplicity from the gallery</span></span>
<span data-ttu-id="c6461-124">Voor het configureren van de integratie van Syncplicity in Azure AD, moet u Syncplicity uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="c6461-124">To configure the integration of Syncplicity into Azure AD, you need to add Syncplicity from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c6461-125">**Als u wilt toevoegen Syncplicity uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="c6461-125">**To add Syncplicity from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c6461-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="c6461-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c6461-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c6461-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c6461-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c6461-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="c6461-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c6461-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="c6461-133">Typ in het zoekvak **Syncplicity**.</span><span class="sxs-lookup"><span data-stu-id="c6461-133">In the search box, type **Syncplicity**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_search.png)

5. <span data-ttu-id="c6461-135">Selecteer in het deelvenster resultaten **Syncplicity**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="c6461-135">In the results panel, select **Syncplicity**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c6461-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="c6461-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c6461-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Syncplicity op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="c6461-138">In this section, you configure and test Azure AD single sign-on with Syncplicity based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c6461-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Syncplicity is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c6461-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Syncplicity is to a user in Azure AD.</span></span> <span data-ttu-id="c6461-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Syncplicity tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="c6461-140">In other words, a link relationship between an Azure AD user and the related user in Syncplicity needs to be established.</span></span>

<span data-ttu-id="c6461-141">Wijs in Syncplicity, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="c6461-141">In Syncplicity, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c6461-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Syncplicity, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="c6461-142">To configure and test Azure AD single sign-on with Syncplicity, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c6461-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c6461-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c6461-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c6461-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c6461-145">**[Maken van een testgebruiker Syncplicity](#creating-a-syncplicity-test-user)**  - Syncplicity die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="c6461-145">**[Creating a Syncplicity test user](#creating-a-syncplicity-test-user)** - to have a counterpart of Britta Simon in Syncplicity that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c6461-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="c6461-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c6461-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="c6461-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c6461-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="c6461-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c6461-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Syncplicity configureren.</span><span class="sxs-lookup"><span data-stu-id="c6461-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Syncplicity application.</span></span>

<span data-ttu-id="c6461-150">**Voor het configureren van Azure AD eenmalige aanmelding met Syncplicity, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="c6461-150">**To configure Azure AD single sign-on with Syncplicity, perform the following steps:**</span></span>

1. <span data-ttu-id="c6461-151">In de Azure-portal op de **Syncplicity** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="c6461-151">In the Azure portal, on the **Syncplicity** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="c6461-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="c6461-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_samlbase.png)

3. <span data-ttu-id="c6461-155">Op de **Syncplicity domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="c6461-155">On the **Syncplicity Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_url.png)

    <span data-ttu-id="c6461-157">a.</span><span class="sxs-lookup"><span data-stu-id="c6461-157">a.</span></span> <span data-ttu-id="c6461-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<companyname>.syncplicity.com`</span><span class="sxs-lookup"><span data-stu-id="c6461-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.syncplicity.com`</span></span>

    <span data-ttu-id="c6461-159">b.</span><span class="sxs-lookup"><span data-stu-id="c6461-159">b.</span></span> <span data-ttu-id="c6461-160">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<companyname>.syncplicity.com/sp`</span><span class="sxs-lookup"><span data-stu-id="c6461-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.syncplicity.com/sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c6461-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="c6461-161">These values are not real.</span></span> <span data-ttu-id="c6461-162">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="c6461-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c6461-163">Neem contact op met [Syncplicity Client ondersteuningsteam](https://www.syncplicity.com/contact-us) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="c6461-163">Contact [Syncplicity Client support team](https://www.syncplicity.com/contact-us) to get these values.</span></span> 
 

4. <span data-ttu-id="c6461-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="c6461-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_certificate.png) 

  
5. <span data-ttu-id="c6461-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="c6461-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-syncplicity-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c6461-168">Op de **Syncplicity configuratie** sectie, klikt u op **configureren Syncplicity** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="c6461-168">On the **Syncplicity Configuration** section, click **Configure Syncplicity** to open **Configure sign-on** window.</span></span> <span data-ttu-id="c6461-169">Kopieer de **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="c6461-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_configure.png) 

7. <span data-ttu-id="c6461-171">Aanmelden bij uw **Syncplicity** tenant.</span><span class="sxs-lookup"><span data-stu-id="c6461-171">Sign in to your **Syncplicity** tenant.</span></span>

8. <span data-ttu-id="c6461-172">Klik in het menu bovenaan op **admin**, selecteer **instellingen**, en klik vervolgens op **aangepaste domeinen en eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="c6461-172">In the menu on the top, click **admin**, select **settings**, and then click **Custom domain and single sign-on**.</span></span>
   
    <span data-ttu-id="c6461-173">![Syncplicity](./media/active-directory-saas-syncplicity-tutorial/ic769545.png "Syncplicity")</span><span class="sxs-lookup"><span data-stu-id="c6461-173">![Syncplicity](./media/active-directory-saas-syncplicity-tutorial/ic769545.png "Syncplicity")</span></span>

9. <span data-ttu-id="c6461-174">Op de **eenmalige aanmelding (SSO)** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="c6461-174">On the **Single Sign-On (SSO)** dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="c6461-175">![Eenmalige aanmelding \(eenmalige aanmelding\)](./media/active-directory-saas-syncplicity-tutorial/ic769550.png "Single Sign-On \\\(SSO\\\)")</span><span class="sxs-lookup"><span data-stu-id="c6461-175">![Single Sign-On \(SSO\)](./media/active-directory-saas-syncplicity-tutorial/ic769550.png "Single Sign-On \\\(SSO\\\)")</span></span>   

    <span data-ttu-id="c6461-176">a.</span><span class="sxs-lookup"><span data-stu-id="c6461-176">a.</span></span> <span data-ttu-id="c6461-177">In de **aangepaste domeinen** textbox, typ de naam van uw domein.</span><span class="sxs-lookup"><span data-stu-id="c6461-177">In the **Custom Domain** textbox, type the name of your domain.</span></span>
  
    <span data-ttu-id="c6461-178">b.</span><span class="sxs-lookup"><span data-stu-id="c6461-178">b.</span></span> <span data-ttu-id="c6461-179">Selecteer **ingeschakeld** als **Single Sign-On Status**.</span><span class="sxs-lookup"><span data-stu-id="c6461-179">Select **Enabled** as **Single Sign-On Status**.</span></span>

    <span data-ttu-id="c6461-180">c.</span><span class="sxs-lookup"><span data-stu-id="c6461-180">c.</span></span> <span data-ttu-id="c6461-181">In de **entiteit-Id** textbox, plak de waarde van **SAML entiteit-ID** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="c6461-181">In the **Entity Id** textbox, Paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="c6461-182">d.</span><span class="sxs-lookup"><span data-stu-id="c6461-182">d.</span></span> <span data-ttu-id="c6461-183">In de **aanmelden pagina-URL** textbox, plak de **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="c6461-183">In the **Sign-in page URL** textbox, Paste the **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="c6461-184">e.</span><span class="sxs-lookup"><span data-stu-id="c6461-184">e.</span></span> <span data-ttu-id="c6461-185">In de **pagina-URL voor afmelden** textbox, plak de **Sign-Out URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="c6461-185">In the **Logout page URL** textbox, Paste the **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="c6461-186">f.</span><span class="sxs-lookup"><span data-stu-id="c6461-186">f.</span></span> <span data-ttu-id="c6461-187">In **Provider identiteitscertificaat**, klikt u op **bestand kiezen**, en vervolgens het certificaat dat u hebt gedownload vanuit de Azure-portal uploaden.</span><span class="sxs-lookup"><span data-stu-id="c6461-187">In **Identity Provider Certificate**, click **Choose file**, and then upload the certificate which you have downloaded from the Azure portal.</span></span> 

    <span data-ttu-id="c6461-188">g.</span><span class="sxs-lookup"><span data-stu-id="c6461-188">g.</span></span> <span data-ttu-id="c6461-189">Klik op **wijzigingen opslaan**.</span><span class="sxs-lookup"><span data-stu-id="c6461-189">Click **SAVE CHANGES**.</span></span>

> [!TIP]
> <span data-ttu-id="c6461-190">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="c6461-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c6461-191">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="c6461-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c6461-192">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c6461-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c6461-193">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="c6461-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="c6461-194">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="c6461-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="c6461-196">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="c6461-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c6461-197">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="c6461-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c6461-199">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="c6461-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c6461-201">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c6461-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c6461-203">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="c6461-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c6461-205">a.</span><span class="sxs-lookup"><span data-stu-id="c6461-205">a.</span></span> <span data-ttu-id="c6461-206">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c6461-206">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c6461-207">b.</span><span class="sxs-lookup"><span data-stu-id="c6461-207">b.</span></span> <span data-ttu-id="c6461-208">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c6461-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c6461-209">c.</span><span class="sxs-lookup"><span data-stu-id="c6461-209">c.</span></span> <span data-ttu-id="c6461-210">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="c6461-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c6461-211">d.</span><span class="sxs-lookup"><span data-stu-id="c6461-211">d.</span></span> <span data-ttu-id="c6461-212">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="c6461-212">Click **Create**.</span></span>
 
### <a name="creating-a-syncplicity-test-user"></a><span data-ttu-id="c6461-213">Een testgebruiker Syncplicity maken</span><span class="sxs-lookup"><span data-stu-id="c6461-213">Creating a Syncplicity test user</span></span>
<span data-ttu-id="c6461-214">AAD-gebruikers moeten kunnen aanmelden, als ze worden ingericht op Syncplicity toepassing.</span><span class="sxs-lookup"><span data-stu-id="c6461-214">For AAD users to be able to sign in, they must be provisioned to Syncplicity application.</span></span> <span data-ttu-id="c6461-215">Deze sectie beschrijft het maken van gebruikersaccounts van AAD in Syncplicity.</span><span class="sxs-lookup"><span data-stu-id="c6461-215">This section describes how to create AAD user accounts in Syncplicity.</span></span>

<span data-ttu-id="c6461-216">**Voor het inrichten van een gebruikersaccount aan Syncplicity, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="c6461-216">**To provision a user account to Syncplicity, perform the following steps:**</span></span>

1. <span data-ttu-id="c6461-217">Meld u aan bij uw **Syncplicity** tenant (bijvoorbeeld: `https://company.Syncplicity.com`).</span><span class="sxs-lookup"><span data-stu-id="c6461-217">Log in to your **Syncplicity** tenant (for example: `https://company.Syncplicity.com`).</span></span>

2. <span data-ttu-id="c6461-218">Klik op **admin** en selecteer **gebruikersaccounts**.</span><span class="sxs-lookup"><span data-stu-id="c6461-218">Click **admin** and select **user accounts**.</span></span>

3. <span data-ttu-id="c6461-219">Klik op **toevoegen van een gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="c6461-219">Click **ADD A USER**.</span></span>
   
    <span data-ttu-id="c6461-220">![Gebruikers beheren](./media/active-directory-saas-syncplicity-tutorial/ic769764.png "gebruikers beheren")</span><span class="sxs-lookup"><span data-stu-id="c6461-220">![Manage Users](./media/active-directory-saas-syncplicity-tutorial/ic769764.png "Manage Users")</span></span>

4. <span data-ttu-id="c6461-221">Type de **e adressen** van een AAD-account dat u inrichten wilt, selecteer **gebruiker** als **rol**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="c6461-221">Type the **Email addressess** of an AAD account you want to provision, select **User** as **Role**, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="c6461-222">![Accountgegevens](./media/active-directory-saas-syncplicity-tutorial/ic769765.png "accountgegevens")</span><span class="sxs-lookup"><span data-stu-id="c6461-222">![Account Information](./media/active-directory-saas-syncplicity-tutorial/ic769765.png "Account Information")</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="c6461-223">De accounthouder AAD Hiermee haalt u een e-mailbericht een koppeling om te bevestigen en activeren van het account waaronder.</span><span class="sxs-lookup"><span data-stu-id="c6461-223">The AAD account holder  gets an email including a link to confirm and activate the account.</span></span> 
    > 

5. <span data-ttu-id="c6461-224">Selecteer een groep in uw bedrijf dat de nieuwe gebruiker moet lid van en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="c6461-224">Select a group in your company that your new user should become a member of, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="c6461-225">![Groepslidmaatschap](./media/active-directory-saas-syncplicity-tutorial/ic769772.png "groepslidmaatschap")</span><span class="sxs-lookup"><span data-stu-id="c6461-225">![Group Membership](./media/active-directory-saas-syncplicity-tutorial/ic769772.png "Group Membership")</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="c6461-226">Als er geen groepen die zijn vermeld zijn, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="c6461-226">If there are no groups listed, click **NEXT**.</span></span> 
    > 

6. <span data-ttu-id="c6461-227">Selecteer de mappen die u wilt plaatsen, onder het beheer van Syncplicity op de computer van de gebruiker en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="c6461-227">Select the folders you would like to place under Syncplicity’s control on the user’s computer, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="c6461-228">![Syncplicity mappen](./media/active-directory-saas-syncplicity-tutorial/ic769773.png "Syncplicity mappen")</span><span class="sxs-lookup"><span data-stu-id="c6461-228">![Syncplicity Folders](./media/active-directory-saas-syncplicity-tutorial/ic769773.png "Syncplicity Folders")</span></span>

>[!NOTE]
><span data-ttu-id="c6461-229">U kunt andere Syncplicity gebruiker account hulpmiddelen voor het maken of API's die is geleverd door Syncplicity aan inrichten AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="c6461-229">You can use any other Syncplicity user account creation tools or APIs provided by Syncplicity to provision AAD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c6461-230">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="c6461-230">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c6461-231">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Syncplicity.</span><span class="sxs-lookup"><span data-stu-id="c6461-231">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Syncplicity.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="c6461-233">**Britta Simon om aan te wijzen Syncplicity, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="c6461-233">**To assign Britta Simon to Syncplicity, perform the following steps:**</span></span>

1. <span data-ttu-id="c6461-234">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c6461-234">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="c6461-236">Selecteer in de lijst met toepassingen **Syncplicity**.</span><span class="sxs-lookup"><span data-stu-id="c6461-236">In the applications list, select **Syncplicity**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_app.png) 

3. <span data-ttu-id="c6461-238">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="c6461-238">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="c6461-240">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="c6461-240">Click **Add** button.</span></span> <span data-ttu-id="c6461-241">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c6461-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="c6461-243">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="c6461-243">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c6461-244">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c6461-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c6461-245">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c6461-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c6461-246">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="c6461-246">Testing single sign-on</span></span>

<span data-ttu-id="c6461-247">Het doel van deze sectie is het testen van uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="c6461-247">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c6461-248">Als u op de tegel Syncplicity in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Syncplicity.</span><span class="sxs-lookup"><span data-stu-id="c6461-248">When you click the Syncplicity tile in the Access Panel, you should get automatically signed-on to your Syncplicity application.</span></span>
## <a name="additional-resources"></a><span data-ttu-id="c6461-249">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="c6461-249">Additional resources</span></span>

* [<span data-ttu-id="c6461-250">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c6461-250">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c6461-251">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c6461-251">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_203.png

