---
title: 'Zelfstudie: Azure Active Directory-integratie met menselijkheid | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en menselijkheid.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6aa771e9-31c6-48d1-8dde-024bebc06943
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 327cc1e3d0836e79376e0a3cd5a4422a967f5943
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-humanity"></a><span data-ttu-id="c124e-103">Zelfstudie: Azure Active Directory-integratie met menselijkheid</span><span class="sxs-lookup"><span data-stu-id="c124e-103">Tutorial: Azure Active Directory integration with Humanity</span></span>

<span data-ttu-id="c124e-104">In deze zelfstudie leert u hoe menselijkheid integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c124e-104">In this tutorial, you learn how to integrate Humanity with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c124e-105">Menselijkheid integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="c124e-105">Integrating Humanity with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c124e-106">U kunt beheren in Azure AD die toegang tot menselijkheid heeft</span><span class="sxs-lookup"><span data-stu-id="c124e-106">You can control in Azure AD who has access to Humanity</span></span>
- <span data-ttu-id="c124e-107">U kunt uw gebruikers automatisch ophalen aangemeld bij menselijkheid (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="c124e-107">You can enable your users to automatically get signed-on to Humanity (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c124e-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="c124e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c124e-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c124e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c124e-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="c124e-110">Prerequisites</span></span>

<span data-ttu-id="c124e-111">Voor het configureren van Azure AD-integratie met menselijkheid, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="c124e-111">To configure Azure AD integration with Humanity, you need the following items:</span></span>

- <span data-ttu-id="c124e-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="c124e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c124e-113">Een menselijkheid eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="c124e-113">A Humanity single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c124e-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="c124e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c124e-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="c124e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c124e-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="c124e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c124e-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c124e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c124e-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="c124e-118">Scenario description</span></span>
<span data-ttu-id="c124e-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="c124e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c124e-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="c124e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c124e-121">Menselijkheid uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="c124e-121">Adding Humanity from the gallery</span></span>
2. <span data-ttu-id="c124e-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="c124e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-humanity-from-the-gallery"></a><span data-ttu-id="c124e-123">Menselijkheid uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="c124e-123">Adding Humanity from the gallery</span></span>
<span data-ttu-id="c124e-124">Voor het configureren van de integratie van menselijkheid met Azure AD, moet u menselijkheid uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="c124e-124">To configure the integration of Humanity into Azure AD, you need to add Humanity from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c124e-125">**Als u wilt toevoegen menselijkheid uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="c124e-125">**To add Humanity from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c124e-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="c124e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c124e-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c124e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c124e-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c124e-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="c124e-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c124e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="c124e-133">Typ in het zoekvak **menselijkheid**.</span><span class="sxs-lookup"><span data-stu-id="c124e-133">In the search box, type **Humanity**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_search.png)

5. <span data-ttu-id="c124e-135">Selecteer in het deelvenster resultaten **menselijkheid**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="c124e-135">In the results panel, select **Humanity**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c124e-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="c124e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c124e-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met menselijkheid op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="c124e-138">In this section, you configure and test Azure AD single sign-on with Humanity based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c124e-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in menselijkheid is aan een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c124e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Humanity is to a user in Azure AD.</span></span> <span data-ttu-id="c124e-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in menselijkheid tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="c124e-140">In other words, a link relationship between an Azure AD user and the related user in Humanity needs to be established.</span></span>

<span data-ttu-id="c124e-141">Wijs in menselijkheid, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="c124e-141">In Humanity, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c124e-142">Om te configureren en testen eenmalige aanmelding Azure AD met menselijkheid, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="c124e-142">To configure and test Azure AD single sign-on with Humanity, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c124e-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c124e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c124e-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c124e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c124e-145">**[Maken van een testgebruiker menselijkheid](#creating-a-humanity-test-user)**  - menselijkheid die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="c124e-145">**[Creating a Humanity test user](#creating-a-humanity-test-user)** - to have a counterpart of Britta Simon in Humanity that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c124e-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="c124e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c124e-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="c124e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c124e-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="c124e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c124e-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing menselijkheid configureren.</span><span class="sxs-lookup"><span data-stu-id="c124e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Humanity application.</span></span>

<span data-ttu-id="c124e-150">**Voor het configureren van Azure AD eenmalige aanmelding met menselijkheid, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="c124e-150">**To configure Azure AD single sign-on with Humanity, perform the following steps:**</span></span>

1. <span data-ttu-id="c124e-151">In de Azure-portal op de **menselijkheid** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="c124e-151">In the Azure portal, on the **Humanity** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="c124e-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="c124e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_samlbase.png)

3. <span data-ttu-id="c124e-155">Op de **menselijkheid domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="c124e-155">On the **Humanity Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_url.png)

    <span data-ttu-id="c124e-157">a.</span><span class="sxs-lookup"><span data-stu-id="c124e-157">a.</span></span> <span data-ttu-id="c124e-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://company.humanity.com/includes/saml/`</span><span class="sxs-lookup"><span data-stu-id="c124e-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://company.humanity.com/includes/saml/`</span></span>

    <span data-ttu-id="c124e-159">b.</span><span class="sxs-lookup"><span data-stu-id="c124e-159">b.</span></span> <span data-ttu-id="c124e-160">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://company.humanity.com/app/`</span><span class="sxs-lookup"><span data-stu-id="c124e-160">In the **Identifier** textbox, type a URL using the following pattern: `https://company.humanity.com/app/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c124e-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="c124e-161">These values are not real.</span></span> <span data-ttu-id="c124e-162">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="c124e-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c124e-163">Neem contact op met [menselijkheid Client ondersteuningsteam](https://www.humanity.com/support/) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="c124e-163">Contact [Humanity Client support team](https://www.humanity.com/support/) to get these values.</span></span> 
 
4. <span data-ttu-id="c124e-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="c124e-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_certificate.png) 

5. <span data-ttu-id="c124e-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="c124e-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c124e-168">Op de **menselijkheid configuratie** sectie, klikt u op **menselijkheid configureren** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="c124e-168">On the **Humanity Configuration** section, click **Configure Humanity** to open **Configure sign-on** window.</span></span> <span data-ttu-id="c124e-169">Kopieer de **SAML Single Sign-On Service-URL en Sign-Out URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="c124e-169">Copy the **SAML Single Sign-On Service URL, and Sign-Out URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_configure.png) 

7. <span data-ttu-id="c124e-171">In een ander browservenster geopend, moet u zich aanmelden bij uw **menselijkheid** bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="c124e-171">In a different web browser window, log in to your **Humanity** company site as an administrator.</span></span>

8. <span data-ttu-id="c124e-172">Klik in het menu bovenaan op **Admin**.</span><span class="sxs-lookup"><span data-stu-id="c124e-172">In the menu on the top, click **Admin**.</span></span>
   
    <span data-ttu-id="c124e-173">![Beheerder](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="c124e-173">![Admin](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Admin")</span></span>

9. <span data-ttu-id="c124e-174">Onder **integratie**, klikt u op **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="c124e-174">Under **Integration**, click **Single Sign-On**.</span></span>
   
    <span data-ttu-id="c124e-175">![Eenmalige aanmelding](./media/active-directory-saas-shiftplanning-tutorial/iC786620.png "eenmalige aanmelding")</span><span class="sxs-lookup"><span data-stu-id="c124e-175">![Single Sign-On](./media/active-directory-saas-shiftplanning-tutorial/iC786620.png "Single Sign-On")</span></span>

10. <span data-ttu-id="c124e-176">In de **Single Sign-On** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="c124e-176">In the **Single Sign-On** section, perform the following steps:</span></span>
   
    <span data-ttu-id="c124e-177">![Eenmalige aanmelding](./media/active-directory-saas-shiftplanning-tutorial/iC786905.png "eenmalige aanmelding")</span><span class="sxs-lookup"><span data-stu-id="c124e-177">![Single Sign-On](./media/active-directory-saas-shiftplanning-tutorial/iC786905.png "Single Sign-On")</span></span>
   
    <span data-ttu-id="c124e-178">a.</span><span class="sxs-lookup"><span data-stu-id="c124e-178">a.</span></span> <span data-ttu-id="c124e-179">Selecteer **SAML ingeschakeld**.</span><span class="sxs-lookup"><span data-stu-id="c124e-179">Select **SAML Enabled**.</span></span>

    <span data-ttu-id="c124e-180">b.</span><span class="sxs-lookup"><span data-stu-id="c124e-180">b.</span></span> <span data-ttu-id="c124e-181">Selecteer **wachtwoord aanmelding toestaan**.</span><span class="sxs-lookup"><span data-stu-id="c124e-181">Select **Allow Password Login**.</span></span>

    <span data-ttu-id="c124e-182">c.</span><span class="sxs-lookup"><span data-stu-id="c124e-182">c.</span></span> <span data-ttu-id="c124e-183">Plak de **SAML Single Sign-On Service-URL** waarde in de **URL-verlener SAML** textbox.</span><span class="sxs-lookup"><span data-stu-id="c124e-183">Paste the **SAML Single Sign-On Service URL** value into the **SAML Issuer URL** textbox.</span></span>

    <span data-ttu-id="c124e-184">d.</span><span class="sxs-lookup"><span data-stu-id="c124e-184">d.</span></span> <span data-ttu-id="c124e-185">Plak de **Sign-Out URL** waarde in de **externe URL voor afmelden** textbox.</span><span class="sxs-lookup"><span data-stu-id="c124e-185">Paste the **Sign-Out URL** value into the **Remote Logout URL** textbox.</span></span>
   
    <span data-ttu-id="c124e-186">e.</span><span class="sxs-lookup"><span data-stu-id="c124e-186">e.</span></span> <span data-ttu-id="c124e-187">Open uw base-64 gecodeerde certificaat in Kladblok, Kopieer de inhoud ervan naar het Klembord en plakt u deze naar de **X.509-certificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="c124e-187">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox.</span></span>

11. <span data-ttu-id="c124e-188">Klik op **instellingen opslaan**.</span><span class="sxs-lookup"><span data-stu-id="c124e-188">Click **Save Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="c124e-189">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="c124e-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c124e-190">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="c124e-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c124e-191">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c124e-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c124e-192">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="c124e-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="c124e-193">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="c124e-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="c124e-195">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="c124e-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c124e-196">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="c124e-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c124e-198">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="c124e-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c124e-200">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c124e-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c124e-202">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="c124e-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c124e-204">a.</span><span class="sxs-lookup"><span data-stu-id="c124e-204">a.</span></span> <span data-ttu-id="c124e-205">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c124e-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c124e-206">b.</span><span class="sxs-lookup"><span data-stu-id="c124e-206">b.</span></span> <span data-ttu-id="c124e-207">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c124e-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c124e-208">c.</span><span class="sxs-lookup"><span data-stu-id="c124e-208">c.</span></span> <span data-ttu-id="c124e-209">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="c124e-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c124e-210">d.</span><span class="sxs-lookup"><span data-stu-id="c124e-210">d.</span></span> <span data-ttu-id="c124e-211">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="c124e-211">Click **Create**.</span></span>
 
### <a name="creating-a-humanity-test-user"></a><span data-ttu-id="c124e-212">Een testgebruiker menselijkheid maken</span><span class="sxs-lookup"><span data-stu-id="c124e-212">Creating a Humanity test user</span></span>

<span data-ttu-id="c124e-213">Om Azure AD-gebruikers zich aanmelden bij menselijkheid inschakelt, moeten ze worden ingericht in menselijkheid.</span><span class="sxs-lookup"><span data-stu-id="c124e-213">In order to enable Azure AD users to log in to Humanity, they must be provisioned into Humanity.</span></span> <span data-ttu-id="c124e-214">In het geval van menselijkheid is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="c124e-214">In the case of Humanity, provisioning is a manual task.</span></span>

<span data-ttu-id="c124e-215">**Voor het inrichten van een gebruikersaccount, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="c124e-215">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="c124e-216">Meld u aan bij uw **menselijkheid** bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="c124e-216">Log in to your **Humanity** company site as an administrator.</span></span>

2. <span data-ttu-id="c124e-217">Klik op **Admin**.</span><span class="sxs-lookup"><span data-stu-id="c124e-217">Click **Admin**.</span></span>
   
    <span data-ttu-id="c124e-218">![Beheerder](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="c124e-218">![Admin](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Admin")</span></span>

3. <span data-ttu-id="c124e-219">Klik op **personeel**.</span><span class="sxs-lookup"><span data-stu-id="c124e-219">Click **Staff**.</span></span>
   
    <span data-ttu-id="c124e-220">![Personeel](./media/active-directory-saas-shiftplanning-tutorial/ic786623.png "personeel")</span><span class="sxs-lookup"><span data-stu-id="c124e-220">![Staff](./media/active-directory-saas-shiftplanning-tutorial/ic786623.png "Staff")</span></span>

4. <span data-ttu-id="c124e-221">Onder **acties**, klikt u op **werknemers toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="c124e-221">Under **Actions**, click **Add Employees**.</span></span>
   
    <span data-ttu-id="c124e-222">![Werknemers toevoegen](./media/active-directory-saas-shiftplanning-tutorial/iC786624.png "werknemers toevoegen")</span><span class="sxs-lookup"><span data-stu-id="c124e-222">![Add Employees](./media/active-directory-saas-shiftplanning-tutorial/iC786624.png "Add Employees")</span></span>

5. <span data-ttu-id="c124e-223">In de **werknemers toevoegen** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="c124e-223">In the **Add Employees** section, perform the following steps:</span></span>
   
    <span data-ttu-id="c124e-224">![Opslaan van werknemers](./media/active-directory-saas-shiftplanning-tutorial/iC786625.png "werknemers opslaan")</span><span class="sxs-lookup"><span data-stu-id="c124e-224">![Save Employees](./media/active-directory-saas-shiftplanning-tutorial/iC786625.png "Save Employees")</span></span>
   
    <span data-ttu-id="c124e-225">a.</span><span class="sxs-lookup"><span data-stu-id="c124e-225">a.</span></span> <span data-ttu-id="c124e-226">Typ de **voornaam**, **achternaam**, en **e** van een geldige AAD-account dat u inrichten in de bijbehorende tekstvakken wilt.</span><span class="sxs-lookup"><span data-stu-id="c124e-226">Type the **First Name**, **Last Name**, and **Email** of a valid AAD account you want to provision into the related textboxes.</span></span>

    <span data-ttu-id="c124e-227">b.</span><span class="sxs-lookup"><span data-stu-id="c124e-227">b.</span></span> <span data-ttu-id="c124e-228">Klik op **opslaan werknemers**.</span><span class="sxs-lookup"><span data-stu-id="c124e-228">Click **Save Employees**.</span></span>

>[!NOTE]
><span data-ttu-id="c124e-229">U kunt andere menselijkheid gebruiker account hulpmiddelen voor het maken of API's die is geleverd door menselijkheid aan inrichten AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="c124e-229">You can use any other Humanity user account creation tools or APIs provided by Humanity to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c124e-230">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="c124e-230">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c124e-231">In deze sectie maakt inschakelen u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan menselijkheid.</span><span class="sxs-lookup"><span data-stu-id="c124e-231">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Humanity.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="c124e-233">**Britta Simon om aan te wijzen menselijkheid, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="c124e-233">**To assign Britta Simon to Humanity, perform the following steps:**</span></span>

1. <span data-ttu-id="c124e-234">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c124e-234">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="c124e-236">Selecteer in de lijst met toepassingen **menselijkheid**.</span><span class="sxs-lookup"><span data-stu-id="c124e-236">In the applications list, select **Humanity**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_app.png) 

3. <span data-ttu-id="c124e-238">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="c124e-238">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="c124e-240">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="c124e-240">Click **Add** button.</span></span> <span data-ttu-id="c124e-241">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c124e-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="c124e-243">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="c124e-243">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c124e-244">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c124e-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c124e-245">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c124e-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c124e-246">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="c124e-246">Testing single sign-on</span></span>

<span data-ttu-id="c124e-247">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="c124e-247">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c124e-248">Als u op de tegel menselijkheid in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing menselijkheid.</span><span class="sxs-lookup"><span data-stu-id="c124e-248">When you click the Humanity tile in the Access Panel, you should get automatically signed-on to your Humanity application.</span></span>
<span data-ttu-id="c124e-249">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c124e-249">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c124e-250">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="c124e-250">Additional resources</span></span>

* [<span data-ttu-id="c124e-251">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c124e-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c124e-252">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c124e-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_203.png

