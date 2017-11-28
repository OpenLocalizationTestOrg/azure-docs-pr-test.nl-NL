---
title: 'Zelfstudie: Azure Active Directory-integratie met Canvas Lms | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Canvas LMS.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bfed291c-a33e-410d-b919-5b965a631d45
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: jeedes
ms.openlocfilehash: 2212b7a81b66d1afd1aa78d1487b07b6d7b84129
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-canvas-lms"></a><span data-ttu-id="974eb-103">Zelfstudie: Azure Active Directory-integratie met Canvas LMS</span><span class="sxs-lookup"><span data-stu-id="974eb-103">Tutorial: Azure Active Directory integration with Canvas LMS</span></span>

<span data-ttu-id="974eb-104">In deze zelfstudie leert u het Canvas integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="974eb-104">In this tutorial, you learn how to integrate Canvas with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="974eb-105">Canvas integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="974eb-105">Integrating Canvas with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="974eb-106">U kunt beheren in Azure AD die toegang tot het Canvas heeft</span><span class="sxs-lookup"><span data-stu-id="974eb-106">You can control in Azure AD who has access to Canvas</span></span>
- <span data-ttu-id="974eb-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Canvas (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="974eb-107">You can enable your users to automatically get signed-on to Canvas (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="974eb-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="974eb-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="974eb-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="974eb-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="974eb-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="974eb-110">Prerequisites</span></span>

<span data-ttu-id="974eb-111">Voor het configureren van Azure AD-integratie met Canvas, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="974eb-111">To configure Azure AD integration with Canvas, you need the following items:</span></span>

- <span data-ttu-id="974eb-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="974eb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="974eb-113">Een Canvas eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="974eb-113">A Canvas single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="974eb-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="974eb-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="974eb-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="974eb-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="974eb-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="974eb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="974eb-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="974eb-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="974eb-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="974eb-118">Scenario description</span></span>
<span data-ttu-id="974eb-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="974eb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="974eb-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="974eb-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="974eb-121">Canvas uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="974eb-121">Adding Canvas from the gallery</span></span>
2. <span data-ttu-id="974eb-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="974eb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-canvas-from-the-gallery"></a><span data-ttu-id="974eb-123">Canvas uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="974eb-123">Adding Canvas from the gallery</span></span>
<span data-ttu-id="974eb-124">Voor het configureren van de integratie van Canvas in Azure AD, moet u Canvas uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="974eb-124">To configure the integration of Canvas into Azure AD, you need to add Canvas from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="974eb-125">**Als u wilt toevoegen Canvas uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="974eb-125">**To add Canvas from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="974eb-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="974eb-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="974eb-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="974eb-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="974eb-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="974eb-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="974eb-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="974eb-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="974eb-133">Typ in het zoekvak **Canvas**.</span><span class="sxs-lookup"><span data-stu-id="974eb-133">In the search box, type **Canvas**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_search.png)

5. <span data-ttu-id="974eb-135">Selecteer in het deelvenster resultaten **Canvas**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="974eb-135">In the results panel, select **Canvas**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="974eb-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="974eb-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="974eb-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Canvas op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="974eb-138">In this section, you configure and test Azure AD single sign-on with Canvas based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="974eb-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Canvas is aan een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="974eb-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Canvas is to a user in Azure AD.</span></span> <span data-ttu-id="974eb-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in het Canvas tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="974eb-140">In other words, a link relationship between an Azure AD user and the related user in Canvas needs to be established.</span></span>

<span data-ttu-id="974eb-141">Wijs in het Canvas de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="974eb-141">In Canvas, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="974eb-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Canvas, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="974eb-142">To configure and test Azure AD single sign-on with Canvas, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="974eb-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="974eb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="974eb-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="974eb-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="974eb-145">**[Maken van een testgebruiker Canvas](#creating-a-canvas-test-user)**  - Canvas die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="974eb-145">**[Creating a Canvas test user](#creating-a-canvas-test-user)** - to have a counterpart of Britta Simon in Canvas that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="974eb-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="974eb-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="974eb-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="974eb-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="974eb-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="974eb-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="974eb-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw toepassing Canvas.</span><span class="sxs-lookup"><span data-stu-id="974eb-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Canvas application.</span></span>

<span data-ttu-id="974eb-150">**Voor het configureren van Azure AD eenmalige aanmelding met Canvas, kunt u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="974eb-150">**To configure Azure AD single sign-on with Canvas, perform the following steps:**</span></span>

1. <span data-ttu-id="974eb-151">In de Azure-portal op de **Canvas** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="974eb-151">In the Azure portal, on the **Canvas** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="974eb-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="974eb-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_samlbase.png)

3. <span data-ttu-id="974eb-155">Op de **Canvas domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="974eb-155">On the **Canvas Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_url.png)

    <span data-ttu-id="974eb-157">a.</span><span class="sxs-lookup"><span data-stu-id="974eb-157">a.</span></span> <span data-ttu-id="974eb-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<tenant-name>.instructure.com`</span><span class="sxs-lookup"><span data-stu-id="974eb-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.instructure.com`</span></span>

    <span data-ttu-id="974eb-159">b.</span><span class="sxs-lookup"><span data-stu-id="974eb-159">b.</span></span> <span data-ttu-id="974eb-160">In de **id** textbox, typ de waarde met het volgende patroon volgen:`https://<tenant-name>.instructure.com/saml2`</span><span class="sxs-lookup"><span data-stu-id="974eb-160">In the **Identifier** textbox, type the value using the following pattern: `https://<tenant-name>.instructure.com/saml2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="974eb-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="974eb-161">These values are not real.</span></span> <span data-ttu-id="974eb-162">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="974eb-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="974eb-163">Neem contact op met [Canvas Client ondersteuningsteam](https://community.canvaslms.com/community/help) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="974eb-163">Contact [Canvas Client support team](https://community.canvaslms.com/community/help) to get these values.</span></span> 
 
4. <span data-ttu-id="974eb-164">Op de **SAML-certificaat voor ondertekening van** sectie, Kopieer de **VINGERAFDRUK** waarde van het certificaat.</span><span class="sxs-lookup"><span data-stu-id="974eb-164">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_certificate.png) 

5. <span data-ttu-id="974eb-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="974eb-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="974eb-168">Op de **configuratie tekenpapier** sectie, klikt u op **Canvas configureren** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="974eb-168">On the **Canvas Configuration** section, click **Configure Canvas** to open **Configure sign-on** window.</span></span> <span data-ttu-id="974eb-169">Kopieer de **URL van wijzigen wachtwoord, Sign-Out URL SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="974eb-169">Copy the **Change Password URL, Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_configure.png) 
 
7. <span data-ttu-id="974eb-171">In een ander browservenster, meld u aan bij uw bedrijf Canvas site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="974eb-171">In a different web browser window, log in to your Canvas company site as an administrator.</span></span>

8. <span data-ttu-id="974eb-172">Ga naar **cursussen \> beheerde Accounts \> Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="974eb-172">Go to **Courses \> Managed Accounts \> Microsoft**.</span></span>
   
    <span data-ttu-id="974eb-173">![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span><span class="sxs-lookup"><span data-stu-id="974eb-173">![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span></span>

9. <span data-ttu-id="974eb-174">Selecteer in het navigatievenster aan de linkerkant **verificatie**, en klik vervolgens op **nieuwe SAML-configuratie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="974eb-174">In the navigation pane on the left, select **Authentication**, and then click **Add New SAML Config**.</span></span>
   
    <span data-ttu-id="974eb-175">![Verificatie](./media/active-directory-saas-canvas-lms-tutorial/IC775991.png "verificatie")</span><span class="sxs-lookup"><span data-stu-id="974eb-175">![Authentication](./media/active-directory-saas-canvas-lms-tutorial/IC775991.png "Authentication")</span></span>

10. <span data-ttu-id="974eb-176">Voer de volgende stappen uit op de pagina huidige integratie:</span><span class="sxs-lookup"><span data-stu-id="974eb-176">On the Current Integration page, perform the following steps:</span></span>
   
    <span data-ttu-id="974eb-177">![Huidige integratie](./media/active-directory-saas-canvas-lms-tutorial/IC775992.png "huidige integratie")</span><span class="sxs-lookup"><span data-stu-id="974eb-177">![Current Integration](./media/active-directory-saas-canvas-lms-tutorial/IC775992.png "Current Integration")</span></span>

    <span data-ttu-id="974eb-178">a.</span><span class="sxs-lookup"><span data-stu-id="974eb-178">a.</span></span> <span data-ttu-id="974eb-179">In **IdP entiteit-ID** textbox, plak de waarde van **SAML entiteit-ID** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="974eb-179">In **IdP Entity ID** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="974eb-180">b.</span><span class="sxs-lookup"><span data-stu-id="974eb-180">b.</span></span> <span data-ttu-id="974eb-181">In **logboek URL** textbox, plak de waarde van **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="974eb-181">In **Log On URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal .</span></span>

    <span data-ttu-id="974eb-182">c.</span><span class="sxs-lookup"><span data-stu-id="974eb-182">c.</span></span> <span data-ttu-id="974eb-183">In **afmeldings-URL** textbox, plak de waarde van **Sign-Out URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="974eb-183">In **Log Out URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="974eb-184">d.</span><span class="sxs-lookup"><span data-stu-id="974eb-184">d.</span></span> <span data-ttu-id="974eb-185">In **koppeling van wijzigen wachtwoord** textbox, plak de waarde van **URL van wijzigen wachtwoord** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="974eb-185">In **Change Password Link** textbox, paste the value of **Change Password URL** which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="974eb-186">e.</span><span class="sxs-lookup"><span data-stu-id="974eb-186">e.</span></span> <span data-ttu-id="974eb-187">In **vingerafdruk van certificaat** textbox, plak de **vingerafdruk** waarde van het certificaat dat u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="974eb-187">In **Certificate Fingerprint** textbox, paste the **Thumbprint** value of certificate which you have copied from Azure portal.</span></span>      
        
    <span data-ttu-id="974eb-188">f.</span><span class="sxs-lookup"><span data-stu-id="974eb-188">f.</span></span> <span data-ttu-id="974eb-189">Van de **aanmelding kenmerk** selecteert **NameID**.</span><span class="sxs-lookup"><span data-stu-id="974eb-189">From the **Login Attribute** list, select **NameID**.</span></span>

    <span data-ttu-id="974eb-190">g.</span><span class="sxs-lookup"><span data-stu-id="974eb-190">g.</span></span> <span data-ttu-id="974eb-191">Van de **id indeling** selecteert **emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="974eb-191">From the **Identifier Format** list, select **emailAddress**.</span></span>

    <span data-ttu-id="974eb-192">h.</span><span class="sxs-lookup"><span data-stu-id="974eb-192">h.</span></span> <span data-ttu-id="974eb-193">Klik op **verificatie-instellingen opslaan**.</span><span class="sxs-lookup"><span data-stu-id="974eb-193">Click **Save Authentication Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="974eb-194">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="974eb-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="974eb-195">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="974eb-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="974eb-196">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="974eb-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="974eb-197">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="974eb-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="974eb-198">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="974eb-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="974eb-200">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="974eb-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="974eb-201">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="974eb-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="974eb-203">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="974eb-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="974eb-205">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="974eb-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="974eb-207">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="974eb-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="974eb-209">a.</span><span class="sxs-lookup"><span data-stu-id="974eb-209">a.</span></span> <span data-ttu-id="974eb-210">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="974eb-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="974eb-211">b.</span><span class="sxs-lookup"><span data-stu-id="974eb-211">b.</span></span> <span data-ttu-id="974eb-212">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="974eb-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="974eb-213">c.</span><span class="sxs-lookup"><span data-stu-id="974eb-213">c.</span></span> <span data-ttu-id="974eb-214">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="974eb-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="974eb-215">d.</span><span class="sxs-lookup"><span data-stu-id="974eb-215">d.</span></span> <span data-ttu-id="974eb-216">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="974eb-216">Click **Create**.</span></span>
 
### <a name="creating-a-canvas-test-user"></a><span data-ttu-id="974eb-217">Maken van een testgebruiker Canvas</span><span class="sxs-lookup"><span data-stu-id="974eb-217">Creating a Canvas test user</span></span>

<span data-ttu-id="974eb-218">Om Azure AD-gebruikers zich aanmelden bij Canvas, moeten ze worden ingericht in Canvas.</span><span class="sxs-lookup"><span data-stu-id="974eb-218">To enable Azure AD users to log in to Canvas, they must be provisioned into Canvas.</span></span>

<span data-ttu-id="974eb-219">In geval van een Canvas is gebruikersaanvragen een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="974eb-219">In case of Canvas, user provisioning is a manual task.</span></span>

<span data-ttu-id="974eb-220">**Voor het inrichten van een gebruikersaccount, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="974eb-220">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="974eb-221">Meld u aan bij uw **Canvas** tenant.</span><span class="sxs-lookup"><span data-stu-id="974eb-221">Log in to your **Canvas** tenant.</span></span>

2. <span data-ttu-id="974eb-222">Ga naar **cursussen \> beheerde Accounts \> Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="974eb-222">Go to **Courses \> Managed Accounts \> Microsoft**.</span></span>
   
   <span data-ttu-id="974eb-223">![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span><span class="sxs-lookup"><span data-stu-id="974eb-223">![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span></span>

3. <span data-ttu-id="974eb-224">Klik op **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="974eb-224">Click **Users**.</span></span>
   
   <span data-ttu-id="974eb-225">![Gebruikers](./media/active-directory-saas-canvas-lms-tutorial/IC775995.png "gebruikers")</span><span class="sxs-lookup"><span data-stu-id="974eb-225">![Users](./media/active-directory-saas-canvas-lms-tutorial/IC775995.png "Users")</span></span>

4. <span data-ttu-id="974eb-226">Klik op **nieuwe gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="974eb-226">Click **Add New User**.</span></span>
   
   <span data-ttu-id="974eb-227">![Gebruikers](./media/active-directory-saas-canvas-lms-tutorial/IC775996.png "gebruikers")</span><span class="sxs-lookup"><span data-stu-id="974eb-227">![Users](./media/active-directory-saas-canvas-lms-tutorial/IC775996.png "Users")</span></span>

5. <span data-ttu-id="974eb-228">Voer de volgende stappen uit op de pagina dialoogvenster Nieuwe gebruiker toevoegen:</span><span class="sxs-lookup"><span data-stu-id="974eb-228">On the Add a New User dialog page, perform the following steps:</span></span>
   
   <span data-ttu-id="974eb-229">![Gebruiker toevoegen](./media/active-directory-saas-canvas-lms-tutorial/IC775997.png "gebruiker toevoegen")</span><span class="sxs-lookup"><span data-stu-id="974eb-229">![Add User](./media/active-directory-saas-canvas-lms-tutorial/IC775997.png "Add User")</span></span>
   
   <span data-ttu-id="974eb-230">a.</span><span class="sxs-lookup"><span data-stu-id="974eb-230">a.</span></span> <span data-ttu-id="974eb-231">In de **volledige naam** textbox, voer de naam van gebruiker zoals **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="974eb-231">In the **Full Name** textbox, enter the name of user like **BrittaSimon**.</span></span>

   <span data-ttu-id="974eb-232">b.</span><span class="sxs-lookup"><span data-stu-id="974eb-232">b.</span></span> <span data-ttu-id="974eb-233">In de **e** textbox, voer het e-mailadres van de gebruiker zoals  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="974eb-233">In the **Email** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>

   <span data-ttu-id="974eb-234">c.</span><span class="sxs-lookup"><span data-stu-id="974eb-234">c.</span></span> <span data-ttu-id="974eb-235">In de **aanmelding** textbox, voer de gebruiker Azure AD e-mailadres zoals  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="974eb-235">In the **Login** textbox, enter the user’s Azure AD email address like **brittasimon@contoso.com**.</span></span>

   <span data-ttu-id="974eb-236">d.</span><span class="sxs-lookup"><span data-stu-id="974eb-236">d.</span></span> <span data-ttu-id="974eb-237">Selecteer **de gebruiker over het maken van dit account een E-mail**.</span><span class="sxs-lookup"><span data-stu-id="974eb-237">Select **Email the user about this account creation**.</span></span>

   <span data-ttu-id="974eb-238">e.</span><span class="sxs-lookup"><span data-stu-id="974eb-238">e.</span></span> <span data-ttu-id="974eb-239">Klik op **gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="974eb-239">Click **Add User**.</span></span>

>[!NOTE]
><span data-ttu-id="974eb-240">U kunt andere Canvas gebruiker account hulpmiddelen voor het maken of API's die is geleverd door Canvas aan inrichten AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="974eb-240">You can use any other Canvas user account creation tools or APIs provided by Canvas to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="974eb-241">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="974eb-241">Assigning the Azure AD test user</span></span>

<span data-ttu-id="974eb-242">In deze sectie maakt inschakelen u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Canvas.</span><span class="sxs-lookup"><span data-stu-id="974eb-242">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Canvas.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="974eb-244">**Britta Simon om aan te wijzen papier, kunt u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="974eb-244">**To assign Britta Simon to Canvas, perform the following steps:**</span></span>

1. <span data-ttu-id="974eb-245">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="974eb-245">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="974eb-247">Selecteer in de lijst met toepassingen **Canvas**.</span><span class="sxs-lookup"><span data-stu-id="974eb-247">In the applications list, select **Canvas**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_app.png) 

3. <span data-ttu-id="974eb-249">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="974eb-249">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="974eb-251">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="974eb-251">Click **Add** button.</span></span> <span data-ttu-id="974eb-252">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="974eb-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="974eb-254">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="974eb-254">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="974eb-255">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="974eb-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="974eb-256">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="974eb-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="974eb-257">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="974eb-257">Testing single sign-on</span></span>

<span data-ttu-id="974eb-258">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="974eb-258">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="974eb-259">Als u op de tegel Canvas in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Canvas.</span><span class="sxs-lookup"><span data-stu-id="974eb-259">When you click the Canvas tile in the Access Panel, you should get automatically signed-on to your Canvas application.</span></span>
<span data-ttu-id="974eb-260">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="974eb-260">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="974eb-261">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="974eb-261">Additional resources</span></span>

* [<span data-ttu-id="974eb-262">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="974eb-262">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="974eb-263">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="974eb-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_203.png

