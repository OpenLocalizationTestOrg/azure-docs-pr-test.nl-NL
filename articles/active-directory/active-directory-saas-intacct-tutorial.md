---
title: 'Zelfstudie: Azure Active Directory-integratie met Intacct | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Intacct.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 92518e02-a62c-4b1b-a8e9-2803eb2b49ac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: c203b192b9da0d280cbd7f6c123219242ee4a3d1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-intacct"></a><span data-ttu-id="ac50e-103">Zelfstudie: Azure Active Directory-integratie met Intacct</span><span class="sxs-lookup"><span data-stu-id="ac50e-103">Tutorial: Azure Active Directory integration with Intacct</span></span>

<span data-ttu-id="ac50e-104">In deze zelfstudie leert u hoe Intacct integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ac50e-104">In this tutorial, you learn how to integrate Intacct with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ac50e-105">Intacct integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="ac50e-105">Integrating Intacct with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ac50e-106">U kunt beheren in Azure AD die toegang tot Intacct heeft</span><span class="sxs-lookup"><span data-stu-id="ac50e-106">You can control in Azure AD who has access to Intacct</span></span>
- <span data-ttu-id="ac50e-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Intacct (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="ac50e-107">You can enable your users to automatically get signed-on to Intacct (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ac50e-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="ac50e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ac50e-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ac50e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ac50e-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ac50e-110">Prerequisites</span></span>

<span data-ttu-id="ac50e-111">Voor het configureren van Azure AD-integratie met Intacct, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="ac50e-111">To configure Azure AD integration with Intacct, you need the following items:</span></span>

- <span data-ttu-id="ac50e-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="ac50e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ac50e-113">Een Intacct eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="ac50e-113">An Intacct single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ac50e-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="ac50e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ac50e-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="ac50e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ac50e-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="ac50e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ac50e-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ac50e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ac50e-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="ac50e-118">Scenario description</span></span>
<span data-ttu-id="ac50e-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="ac50e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ac50e-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="ac50e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ac50e-121">Intacct uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="ac50e-121">Adding Intacct from the gallery</span></span>
2. <span data-ttu-id="ac50e-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ac50e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-intacct-from-the-gallery"></a><span data-ttu-id="ac50e-123">Intacct uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="ac50e-123">Adding Intacct from the gallery</span></span>
<span data-ttu-id="ac50e-124">Voor het configureren van de integratie van Intacct in Azure AD, moet u Intacct uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="ac50e-124">To configure the integration of Intacct into Azure AD, you need to add Intacct from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ac50e-125">**Als u wilt toevoegen Intacct uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="ac50e-125">**To add Intacct from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ac50e-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="ac50e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ac50e-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ac50e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ac50e-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ac50e-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="ac50e-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ac50e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="ac50e-133">Typ in het zoekvak **Intacct**.</span><span class="sxs-lookup"><span data-stu-id="ac50e-133">In the search box, type **Intacct**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_search.png)

5. <span data-ttu-id="ac50e-135">Selecteer in het deelvenster resultaten **Intacct**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="ac50e-135">In the results panel, select **Intacct**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ac50e-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ac50e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ac50e-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Intacct op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="ac50e-138">In this section, you configure and test Azure AD single sign-on with Intacct based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ac50e-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Intacct is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ac50e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Intacct is to a user in Azure AD.</span></span> <span data-ttu-id="ac50e-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Intacct tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="ac50e-140">In other words, a link relationship between an Azure AD user and the related user in Intacct needs to be established.</span></span>

<span data-ttu-id="ac50e-141">Wijs in Intacct, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="ac50e-141">In Intacct, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ac50e-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Intacct, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="ac50e-142">To configure and test Azure AD single sign-on with Intacct, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ac50e-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ac50e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ac50e-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ac50e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ac50e-145">**[Maken van een testgebruiker Intacct](#creating-an-intacct-test-user)**  - Intacct die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="ac50e-145">**[Creating an Intacct test user](#creating-an-intacct-test-user)** - to have a counterpart of Britta Simon in Intacct that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ac50e-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="ac50e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ac50e-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="ac50e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ac50e-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="ac50e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ac50e-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Intacct configureren.</span><span class="sxs-lookup"><span data-stu-id="ac50e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Intacct application.</span></span>

<span data-ttu-id="ac50e-150">**Voor het configureren van Azure AD eenmalige aanmelding met Intacct, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="ac50e-150">**To configure Azure AD single sign-on with Intacct, perform the following steps:**</span></span>

1. <span data-ttu-id="ac50e-151">In de Azure-portal op de **Intacct** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="ac50e-151">In the Azure portal, on the **Intacct** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="ac50e-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="ac50e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_samlbase.png)

3. <span data-ttu-id="ac50e-155">Op de **Intacct domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="ac50e-155">On the **Intacct Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_url.png)

    <span data-ttu-id="ac50e-157">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="ac50e-157">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.intacct.com/ia/acct/sso_response.phtml`|
    | `https://www.intacct.com/ia/acct/sso_response.phtml` |

    > [!NOTE] 
    > <span data-ttu-id="ac50e-158">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="ac50e-158">This value is not real.</span></span> <span data-ttu-id="ac50e-159">Deze waarde bijwerken met de werkelijke antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="ac50e-159">Update this value with the actual Reply URL.</span></span> <span data-ttu-id="ac50e-160">Neem contact op met [Intacct ondersteuningsteam](https://us.intacct.com/support) deze waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="ac50e-160">Contact [Intacct support team](https://us.intacct.com/support) to get this value.</span></span>

4. <span data-ttu-id="ac50e-161">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="ac50e-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_certificate.png) 

5. <span data-ttu-id="ac50e-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="ac50e-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-intacct-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ac50e-165">Op de **Intacct configuratie** sectie, klikt u op **configureren Intacct** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="ac50e-165">On the **Intacct Configuration** section, click **Configure Intacct** to open **Configure sign-on** window.</span></span> <span data-ttu-id="ac50e-166">Kopieer de **SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="ac50e-166">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_configure.png) 

7. <span data-ttu-id="ac50e-168">In een ander browservenster aanmelden bij uw bedrijf Intacct site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="ac50e-168">In a different web browser window, sign in to your Intacct company site as an administrator.</span></span>

8. <span data-ttu-id="ac50e-169">Klik op de **bedrijf** tabblad en klik vervolgens op **bedrijfsgegevens**.</span><span class="sxs-lookup"><span data-stu-id="ac50e-169">Click the **Company** tab, and then click **Company Info**.</span></span>

    <span data-ttu-id="ac50e-170">![Bedrijf](./media/active-directory-saas-intacct-tutorial/ic790037.png "bedrijf")</span><span class="sxs-lookup"><span data-stu-id="ac50e-170">![Company](./media/active-directory-saas-intacct-tutorial/ic790037.png "Company")</span></span>

9. <span data-ttu-id="ac50e-171">Klik op de **beveiliging** tabblad en klik vervolgens op **bewerken**.</span><span class="sxs-lookup"><span data-stu-id="ac50e-171">Click the **Security** tab, and then click **Edit**.</span></span>

    <span data-ttu-id="ac50e-172">![Beveiliging](./media/active-directory-saas-intacct-tutorial/ic790038.png "beveiliging")</span><span class="sxs-lookup"><span data-stu-id="ac50e-172">![Security](./media/active-directory-saas-intacct-tutorial/ic790038.png "Security")</span></span>

10. <span data-ttu-id="ac50e-173">In de **eenmalige aanmelding (SSO)** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="ac50e-173">In the **Single sign on (SSO)** section, perform the following steps:</span></span>

    <span data-ttu-id="ac50e-174">![Eenmalige aanmelding](./media/active-directory-saas-intacct-tutorial/ic790039.png "eenmalige aanmelding")</span><span class="sxs-lookup"><span data-stu-id="ac50e-174">![Single sign on](./media/active-directory-saas-intacct-tutorial/ic790039.png "single sign on")</span></span>

    <span data-ttu-id="ac50e-175">a.</span><span class="sxs-lookup"><span data-stu-id="ac50e-175">a.</span></span> <span data-ttu-id="ac50e-176">Selecteer **eenmalige aanmelding inschakelen op**.</span><span class="sxs-lookup"><span data-stu-id="ac50e-176">Select **Enable single sign on**.</span></span>

    <span data-ttu-id="ac50e-177">b.</span><span class="sxs-lookup"><span data-stu-id="ac50e-177">b.</span></span> <span data-ttu-id="ac50e-178">Als **identiteit providertype**, selecteer **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="ac50e-178">As **Identity provider type**, select **SAML 2.0**.</span></span>

    <span data-ttu-id="ac50e-179">c.</span><span class="sxs-lookup"><span data-stu-id="ac50e-179">c.</span></span> <span data-ttu-id="ac50e-180">In **URL-verlener** textbox, plak de waarde van **SAML entiteit-ID** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="ac50e-180">In **Issuer URL** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="ac50e-181">d.</span><span class="sxs-lookup"><span data-stu-id="ac50e-181">d.</span></span> <span data-ttu-id="ac50e-182">In **aanmeldings-URL** textbox, plak de waarde van **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="ac50e-182">In **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="ac50e-183">e.</span><span class="sxs-lookup"><span data-stu-id="ac50e-183">e.</span></span> <span data-ttu-id="ac50e-184">Open uw **base 64-** gecodeerde certificaat in Kladblok, Kopieer de inhoud ervan naar het Klembord en plakt u deze naar de **certificaat** vak.</span><span class="sxs-lookup"><span data-stu-id="ac50e-184">Open your **base-64** encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Certificate** box.</span></span>
   
    <span data-ttu-id="ac50e-185">f.</span><span class="sxs-lookup"><span data-stu-id="ac50e-185">f.</span></span> <span data-ttu-id="ac50e-186">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="ac50e-186">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="ac50e-187">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="ac50e-187">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ac50e-188">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="ac50e-188">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ac50e-189">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ac50e-189">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ac50e-190">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="ac50e-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="ac50e-191">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="ac50e-191">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="ac50e-193">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="ac50e-193">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ac50e-194">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="ac50e-194">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-intacct-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ac50e-196">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="ac50e-196">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-intacct-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ac50e-198">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ac50e-198">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-intacct-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ac50e-200">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="ac50e-200">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-intacct-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ac50e-202">a.</span><span class="sxs-lookup"><span data-stu-id="ac50e-202">a.</span></span> <span data-ttu-id="ac50e-203">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ac50e-203">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ac50e-204">b.</span><span class="sxs-lookup"><span data-stu-id="ac50e-204">b.</span></span> <span data-ttu-id="ac50e-205">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ac50e-205">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ac50e-206">c.</span><span class="sxs-lookup"><span data-stu-id="ac50e-206">c.</span></span> <span data-ttu-id="ac50e-207">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="ac50e-207">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ac50e-208">d.</span><span class="sxs-lookup"><span data-stu-id="ac50e-208">d.</span></span> <span data-ttu-id="ac50e-209">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="ac50e-209">Click **Create**.</span></span>
 
### <a name="creating-an-intacct-test-user"></a><span data-ttu-id="ac50e-210">Een testgebruiker Intacct maken</span><span class="sxs-lookup"><span data-stu-id="ac50e-210">Creating an Intacct test user</span></span>

<span data-ttu-id="ac50e-211">Als u Azure AD-gebruikers instelt, zodat deze zich voor Intacct aanmelden kunnen, moeten ze worden ingericht in Intacct.</span><span class="sxs-lookup"><span data-stu-id="ac50e-211">To set up Azure AD users so they can sign in to Intacct, they must be provisioned into Intacct.</span></span> <span data-ttu-id="ac50e-212">Voor Intacct is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="ac50e-212">For Intacct, provisioning is a manual task.</span></span>

<span data-ttu-id="ac50e-213">**Voor het inrichten van gebruikersaccounts, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="ac50e-213">**To provision user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="ac50e-214">Aanmelden bij uw **Intacct** tenant.</span><span class="sxs-lookup"><span data-stu-id="ac50e-214">Sign in to your **Intacct** tenant.</span></span>

2. <span data-ttu-id="ac50e-215">Klik op de **bedrijf** tabblad en klik vervolgens op **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="ac50e-215">Click the **Company** tab, and then click **Users**.</span></span>

    <span data-ttu-id="ac50e-216">![Gebruikers](./media/active-directory-saas-intacct-tutorial/ic790041.png "gebruikers")</span><span class="sxs-lookup"><span data-stu-id="ac50e-216">![Users](./media/active-directory-saas-intacct-tutorial/ic790041.png "Users")</span></span>
3. <span data-ttu-id="ac50e-217">Klik op de **toevoegen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="ac50e-217">Click the **Add** tab.</span></span>

    <span data-ttu-id="ac50e-218">![Voeg](./media/active-directory-saas-intacct-tutorial/ic790042.png "toevoegen")</span><span class="sxs-lookup"><span data-stu-id="ac50e-218">![Add](./media/active-directory-saas-intacct-tutorial/ic790042.png "Add")</span></span>
4. <span data-ttu-id="ac50e-219">In de **gebruikersgegevens** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="ac50e-219">In the **User Information** section, perform the following steps:</span></span>

    <span data-ttu-id="ac50e-220">![Gebruikersgegevens](./media/active-directory-saas-intacct-tutorial/ic790043.png "gebruikersgegevens")</span><span class="sxs-lookup"><span data-stu-id="ac50e-220">![User Information](./media/active-directory-saas-intacct-tutorial/ic790043.png "User Information")</span></span>

    <span data-ttu-id="ac50e-221">a.</span><span class="sxs-lookup"><span data-stu-id="ac50e-221">a.</span></span> <span data-ttu-id="ac50e-222">Voer de **gebruikers-ID**, wordt de **achternaam**, **voornaam**, wordt de **e-mailadres**, wordt de **titel**, en de **Phone** van een Azure AD-account dat u wilt inrichten in de **gebruikersgegevens** sectie.</span><span class="sxs-lookup"><span data-stu-id="ac50e-222">Enter the **User ID**, the **Last name**, **First name**, the **Email address**, the **Title**, and the **Phone** of an Azure AD account that you want to provision into the **User Information** section.</span></span>

    <span data-ttu-id="ac50e-223">b.</span><span class="sxs-lookup"><span data-stu-id="ac50e-223">b.</span></span> <span data-ttu-id="ac50e-224">Selecteer de **beheerdersbevoegdheden** van een Azure AD-account dat u inrichten wilt.</span><span class="sxs-lookup"><span data-stu-id="ac50e-224">Select the **Admin privileges** of an Azure AD account that you want to provision.</span></span>
   
    <span data-ttu-id="ac50e-225">c.</span><span class="sxs-lookup"><span data-stu-id="ac50e-225">c.</span></span> <span data-ttu-id="ac50e-226">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="ac50e-226">Click **Save**.</span></span> <span data-ttu-id="ac50e-227">De accounthouder Azure AD ontvangt een e-mailbericht en volgt een koppeling om hun account te bevestigen voordat deze geactiveerd wordt.</span><span class="sxs-lookup"><span data-stu-id="ac50e-227">The Azure AD account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

>[!NOTE]
><span data-ttu-id="ac50e-228">U kunt andere hulpprogramma's voor Intacct gebruiker-account maken of API's die worden geleverd door Intacct gebruiken voor het inrichten van Azure AD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="ac50e-228">To provision Azure AD user accounts, you can use other Intacct user account creation tools or APIs that are provided by Intacct.</span></span>
        
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ac50e-229">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="ac50e-229">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ac50e-230">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Intacct.</span><span class="sxs-lookup"><span data-stu-id="ac50e-230">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Intacct.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="ac50e-232">**Britta Simon om aan te wijzen Intacct, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="ac50e-232">**To assign Britta Simon to Intacct, perform the following steps:**</span></span>

1. <span data-ttu-id="ac50e-233">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ac50e-233">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="ac50e-235">Selecteer in de lijst met toepassingen **Intacct**.</span><span class="sxs-lookup"><span data-stu-id="ac50e-235">In the applications list, select **Intacct**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_app.png) 

3. <span data-ttu-id="ac50e-237">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="ac50e-237">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="ac50e-239">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="ac50e-239">Click **Add** button.</span></span> <span data-ttu-id="ac50e-240">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ac50e-240">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="ac50e-242">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="ac50e-242">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ac50e-243">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ac50e-243">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ac50e-244">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ac50e-244">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ac50e-245">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ac50e-245">Testing single sign-on</span></span>

<span data-ttu-id="ac50e-246">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie testen met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="ac50e-246">In this section, you test your Azure AD single sign-on configuration by using the Access Panel.</span></span>

<span data-ttu-id="ac50e-247">Als u op de tegel Intacct in het deelvenster toegang, moet u worden automatisch aangemeld bij uw toepassing Intacct.</span><span class="sxs-lookup"><span data-stu-id="ac50e-247">When you click the Intacct tile in the Access Panel, you should be automatically signed in to your Intacct application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ac50e-248">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="ac50e-248">Additional resources</span></span>

* [<span data-ttu-id="ac50e-249">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ac50e-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ac50e-250">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ac50e-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_203.png

