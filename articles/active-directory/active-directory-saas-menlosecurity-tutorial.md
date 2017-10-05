---
title: 'Zelfstudie: Azure Active Directory-integratie met Menlo beveiliging | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Menlo beveiliging.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9e63fe6b-0ad0-405d-9e41-6a1a40a41df8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: jeedes
ms.openlocfilehash: 75366abafa551d21630b0edddb65db23b9ea9d42
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-menlo-security"></a><span data-ttu-id="86058-103">Zelfstudie: Azure Active Directory-integratie met Menlo beveiliging</span><span class="sxs-lookup"><span data-stu-id="86058-103">Tutorial: Azure Active Directory integration with Menlo Security</span></span>

<span data-ttu-id="86058-104">In deze zelfstudie leert u hoe Menlo beveiliging integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="86058-104">In this tutorial, you learn how to integrate Menlo Security with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="86058-105">Menlo beveiliging integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="86058-105">Integrating Menlo Security with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="86058-106">U kunt beheren in Azure AD die toegang tot Menlo beveiliging heeft</span><span class="sxs-lookup"><span data-stu-id="86058-106">You can control in Azure AD who has access to Menlo Security</span></span>
- <span data-ttu-id="86058-107">U kunt uw gebruikers automatisch ophalen aangemeld bij de beveiliging Menlo (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="86058-107">You can enable your users to automatically get signed-on to Menlo Security (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="86058-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="86058-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="86058-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, zien.</span><span class="sxs-lookup"><span data-stu-id="86058-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="86058-110">[Wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="86058-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="86058-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="86058-111">Prerequisites</span></span>

<span data-ttu-id="86058-112">Voor het configureren van Azure AD-integratie met Menlo beveiliging, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="86058-112">To configure Azure AD integration with Menlo Security, you need the following items:</span></span>

- <span data-ttu-id="86058-113">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="86058-113">An Azure AD subscription</span></span>
- <span data-ttu-id="86058-114">Een Menlo beveiliging eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="86058-114">A Menlo Security single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="86058-115">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="86058-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="86058-116">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="86058-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="86058-117">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="86058-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="86058-118">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="86058-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="86058-119">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="86058-119">Scenario description</span></span>
<span data-ttu-id="86058-120">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="86058-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="86058-121">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="86058-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="86058-122">Menlo beveiliging toe te voegen uit de galerie</span><span class="sxs-lookup"><span data-stu-id="86058-122">Adding Menlo Security from the gallery</span></span>
2. <span data-ttu-id="86058-123">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="86058-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-menlo-security-from-the-gallery"></a><span data-ttu-id="86058-124">Menlo beveiliging toe te voegen uit de galerie</span><span class="sxs-lookup"><span data-stu-id="86058-124">Adding Menlo Security from the gallery</span></span>
<span data-ttu-id="86058-125">Voor het configureren van de integratie van Menlo beveiliging met Azure AD, moet u Menlo beveiliging uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="86058-125">To configure the integration of Menlo Security into Azure AD, you need to add Menlo Security from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="86058-126">**Als u wilt toevoegen Menlo beveiliging uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="86058-126">**To add Menlo Security from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="86058-127">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="86058-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="86058-129">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="86058-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="86058-130">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="86058-130">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="86058-132">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="86058-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="86058-134">Typ in het zoekvak **Menlo beveiliging**.</span><span class="sxs-lookup"><span data-stu-id="86058-134">In the search box, type **Menlo Security**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_search.png)

5. <span data-ttu-id="86058-136">Selecteer in het deelvenster resultaten **Menlo beveiliging**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="86058-136">In the results panel, select **Menlo Security**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="86058-138">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="86058-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="86058-139">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Menlo beveiliging op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="86058-139">In this section, you configure and test Azure AD single sign-on with Menlo Security based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="86058-140">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Menlo beveiliging in Azure AD voor een gebruiker is.</span><span class="sxs-lookup"><span data-stu-id="86058-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Menlo Security is to a user in Azure AD.</span></span> <span data-ttu-id="86058-141">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Menlo beveiliging worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="86058-141">In other words, a link relationship between an Azure AD user and the related user in Menlo Security needs to be established.</span></span>

<span data-ttu-id="86058-142">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in Menlo beveiliging.</span><span class="sxs-lookup"><span data-stu-id="86058-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Menlo Security.</span></span>

<span data-ttu-id="86058-143">Om te configureren en testen van Azure AD eenmalige aanmelding met Menlo beveiliging, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="86058-143">To configure and test Azure AD single sign-on with Menlo Security, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="86058-144">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="86058-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="86058-145">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="86058-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="86058-146">**[Maken van een testgebruiker Menlo beveiliging](#creating-a-menlo-security-test-user)**  - Menlo beveiliging die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="86058-146">**[Creating a Menlo Security test user](#creating-a-menlo-security-test-user)** - to have a counterpart of Britta Simon in Menlo Security that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="86058-147">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="86058-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="86058-148">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="86058-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="86058-149">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="86058-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="86058-150">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Menlo beveiliging configureren.</span><span class="sxs-lookup"><span data-stu-id="86058-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Menlo Security application.</span></span>

<span data-ttu-id="86058-151">**Voor het configureren van Azure AD eenmalige aanmelding met Menlo beveiliging, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="86058-151">**To configure Azure AD single sign-on with Menlo Security, perform the following steps:**</span></span>

1. <span data-ttu-id="86058-152">In de Azure-portal op de **Menlo beveiliging** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="86058-152">In the Azure portal, on the **Menlo Security** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="86058-154">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="86058-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_samlbase.png)

3. <span data-ttu-id="86058-156">Op de **Menlo beveiligingsdomein en URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="86058-156">On the **Menlo Security Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_url.png)

    <span data-ttu-id="86058-158">a.</span><span class="sxs-lookup"><span data-stu-id="86058-158">a.</span></span> <span data-ttu-id="86058-159">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<subdomain>.menlosecurity.com/account/login`</span><span class="sxs-lookup"><span data-stu-id="86058-159">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.menlosecurity.com/account/login`</span></span>

    <span data-ttu-id="86058-160">b.</span><span class="sxs-lookup"><span data-stu-id="86058-160">b.</span></span> <span data-ttu-id="86058-161">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<subdomain>.menlosecurity.com/safeview-auth-server/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="86058-161">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.menlosecurity.com/safeview-auth-server/saml/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="86058-162">Deze waarden zijn niet de werkelijke.</span><span class="sxs-lookup"><span data-stu-id="86058-162">These values are not the real.</span></span> <span data-ttu-id="86058-163">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="86058-163">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="86058-164">Neem contact op met [Beveiligingsclient Menlo ondersteuningsteam](https://www.menlosecurity.com/menlo-contact) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="86058-164">Contact [Menlo Security Client support team](https://www.menlosecurity.com/menlo-contact) to get these values.</span></span> 
 
4. <span data-ttu-id="86058-165">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="86058-165">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the Certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_certificate.png) 

5. <span data-ttu-id="86058-167">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="86058-167">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="86058-169">Op de **Menlo Beveiligingsconfiguratie** sectie, klikt u op **Menlo beveiliging configureren** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="86058-169">On the **Menlo Security Configuration** section, click **Configure Menlo Security** to open **Configure sign-on** window.</span></span> <span data-ttu-id="86058-170">Kopieer de **SAML entiteit-ID**, en **SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="86058-170">Copy the **SAML Entity ID**, and **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_configure.png) 

7. <span data-ttu-id="86058-172">Eenmalige aanmelding configureren op **Menlo beveiliging** side, meld u aan bij de **Menlo beveiliging** website als beheerder.</span><span class="sxs-lookup"><span data-stu-id="86058-172">To configure single sign-on on **Menlo Security** side, login to the **Menlo Security** website as an administrator.</span></span>

8. <span data-ttu-id="86058-173">Onder **instellingen** gaat u naar **verificatie** en de volgende acties uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="86058-173">Under **Settings** go to **Authentication** and perform following actions:</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-menlosecurity-tutorial/menlo_user_setup.png)

    <span data-ttu-id="86058-175">a.</span><span class="sxs-lookup"><span data-stu-id="86058-175">a.</span></span> <span data-ttu-id="86058-176">Vink het selectievakje **gebruikersverificatie inschakelen via SAML**.</span><span class="sxs-lookup"><span data-stu-id="86058-176">Tick the checkbox **Enable user authentication using SAML**.</span></span>

    <span data-ttu-id="86058-177">b.</span><span class="sxs-lookup"><span data-stu-id="86058-177">b.</span></span> <span data-ttu-id="86058-178">Selecteer **toestaan van externe toegang** naar **Ja**.</span><span class="sxs-lookup"><span data-stu-id="86058-178">Select **Allow External Access** to **Yes**.</span></span>

    <span data-ttu-id="86058-179">c.</span><span class="sxs-lookup"><span data-stu-id="86058-179">c.</span></span> <span data-ttu-id="86058-180">Onder **SAML Provider**, selecteer **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="86058-180">Under **SAML Provider**, select **Azure Active Directory**.</span></span>

    <span data-ttu-id="86058-181">d.</span><span class="sxs-lookup"><span data-stu-id="86058-181">d.</span></span> <span data-ttu-id="86058-182">**SAML 2.0 eindpunt** : plak de **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="86058-182">**SAML 2.0 Endpoint** : Paste the **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="86058-183">e.</span><span class="sxs-lookup"><span data-stu-id="86058-183">e.</span></span> <span data-ttu-id="86058-184">**Service-id (verlener genoemd)** : plak de **SAML entiteit-ID** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="86058-184">**Service Identifier (Issuer)** : Paste the **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="86058-185">f.</span><span class="sxs-lookup"><span data-stu-id="86058-185">f.</span></span> <span data-ttu-id="86058-186">**X.509-certificaat** : Open de **certificaat (Base64)** gedownload vanuit de Azure-Portal in Kladblok en plak deze in dit vak.</span><span class="sxs-lookup"><span data-stu-id="86058-186">**X.509 Certificate** : Open the **Certificate (Base64)** downloaded from the Azure Portal in notepad and paste it in this box.</span></span>

    <span data-ttu-id="86058-187">g.</span><span class="sxs-lookup"><span data-stu-id="86058-187">g.</span></span> <span data-ttu-id="86058-188">Klik op **opslaan** de instellingen op te slaan.</span><span class="sxs-lookup"><span data-stu-id="86058-188">Click **Save** to save the settings.</span></span>

> [!TIP]
> <span data-ttu-id="86058-189">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="86058-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="86058-190">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="86058-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="86058-191">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="86058-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="86058-192">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="86058-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="86058-193">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="86058-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="86058-195">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="86058-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="86058-196">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="86058-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="86058-198">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="86058-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="86058-200">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="86058-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="86058-202">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="86058-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="86058-204">a.</span><span class="sxs-lookup"><span data-stu-id="86058-204">a.</span></span> <span data-ttu-id="86058-205">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="86058-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="86058-206">b.</span><span class="sxs-lookup"><span data-stu-id="86058-206">b.</span></span> <span data-ttu-id="86058-207">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="86058-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="86058-208">c.</span><span class="sxs-lookup"><span data-stu-id="86058-208">c.</span></span> <span data-ttu-id="86058-209">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="86058-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="86058-210">d.</span><span class="sxs-lookup"><span data-stu-id="86058-210">d.</span></span> <span data-ttu-id="86058-211">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="86058-211">Click **Create**.</span></span>
 
### <a name="creating-a-menlo-security-test-user"></a><span data-ttu-id="86058-212">Maken van een testgebruiker Menlo beveiliging</span><span class="sxs-lookup"><span data-stu-id="86058-212">Creating a Menlo Security test user</span></span>
 
<span data-ttu-id="86058-213">In deze sectie maakt u Britta Simon aangeroepen in Menlo beveiliging van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="86058-213">In this section, you create a user called Britta Simon in Menlo Security.</span></span> <span data-ttu-id="86058-214">Werken met [Beveiligingsclient Menlo ondersteuningsteam](https://www.menlosecurity.com/menlo-contact) om toe te voegen de gebruikers van het platform Menlo beveiliging.</span><span class="sxs-lookup"><span data-stu-id="86058-214">Work with [Menlo Security Client support team](https://www.menlosecurity.com/menlo-contact) to add the users in the Menlo Security platform.</span></span> <span data-ttu-id="86058-215">Gebruikers moeten worden gemaakt en worden geactiveerd voordat u eenmalige aanmelding gebruiken.</span><span class="sxs-lookup"><span data-stu-id="86058-215">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="86058-216">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="86058-216">Assigning the Azure AD test user</span></span>

<span data-ttu-id="86058-217">In deze sectie maakt inschakelen u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Menlo beveiliging.</span><span class="sxs-lookup"><span data-stu-id="86058-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Menlo Security.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="86058-219">**Als u wilt toewijzen Britta Simon Menlo beveiliging, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="86058-219">**To assign Britta Simon to Menlo Security, perform the following steps:**</span></span>

1. <span data-ttu-id="86058-220">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="86058-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="86058-222">Selecteer in de lijst met toepassingen **Menlo beveiliging**.</span><span class="sxs-lookup"><span data-stu-id="86058-222">In the applications list, select **Menlo Security**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_app.png) 

3. <span data-ttu-id="86058-224">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="86058-224">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="86058-226">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="86058-226">Click **Add** button.</span></span> <span data-ttu-id="86058-227">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="86058-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="86058-229">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="86058-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="86058-230">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="86058-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="86058-231">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="86058-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="86058-232">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="86058-232">Testing single sign-on</span></span>

<span data-ttu-id="86058-233">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie testen.</span><span class="sxs-lookup"><span data-stu-id="86058-233">In this section, you test your Azure AD single sign-on configuration.</span></span>

<span data-ttu-id="86058-234">Open een browservenster in de modus 'InPrivate' of 'Incognito' voor het activeren van een nieuwe verificatie.</span><span class="sxs-lookup"><span data-stu-id="86058-234">Open a browser window in an "InPrivate" or "Incognito" mode to trigger a new authentication.</span></span>  <span data-ttu-id="86058-235">Gebruik Ctrl + Shift + P in Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="86058-235">In Internet Explorer, use Ctrl+Shift+P.</span></span>  <span data-ttu-id="86058-236">Gebruik Ctrl + Shift + N in Chrome.</span><span class="sxs-lookup"><span data-stu-id="86058-236">In Chrome, use Ctrl+Shift+N.</span></span>  <span data-ttu-id="86058-237">Blader naar een beveiligde bron in het persoonlijke Browse venster en uitvoeren van een Azure AD-aanmelding.</span><span class="sxs-lookup"><span data-stu-id="86058-237">In the private browsing window, browse to a protected resource and perform an Azure AD login.</span></span>  <span data-ttu-id="86058-238">Bij geslaagde aanmelding gaat u naar de gewenste site in een sessie isolatie.</span><span class="sxs-lookup"><span data-stu-id="86058-238">Upon successful login, you will be taken to the requested site in an isolation session.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="86058-239">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="86058-239">Additional resources</span></span>

* [<span data-ttu-id="86058-240">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="86058-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="86058-241">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="86058-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_203.png

