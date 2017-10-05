---
title: 'Zelfstudie: Azure Active Directory-integratie met Picturepark | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Picturepark.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 31c21cd4-9c00-4cad-9538-a13996dc872f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: jeedes
ms.openlocfilehash: 1c009aa1fdd3140a4466cf762b6c9687e74ce4c7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-picturepark"></a><span data-ttu-id="e90b1-103">Zelfstudie: Azure Active Directory-integratie met Picturepark</span><span class="sxs-lookup"><span data-stu-id="e90b1-103">Tutorial: Azure Active Directory integration with Picturepark</span></span>

<span data-ttu-id="e90b1-104">In deze zelfstudie leert u hoe Picturepark integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e90b1-104">In this tutorial, you learn how to integrate Picturepark with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e90b1-105">Picturepark integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="e90b1-105">Integrating Picturepark with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e90b1-106">U kunt beheren in Azure AD die toegang tot Picturepark heeft</span><span class="sxs-lookup"><span data-stu-id="e90b1-106">You can control in Azure AD who has access to Picturepark</span></span>
- <span data-ttu-id="e90b1-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Picturepark (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="e90b1-107">You can enable your users to automatically get signed-on to Picturepark (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e90b1-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="e90b1-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e90b1-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e90b1-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e90b1-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="e90b1-110">Prerequisites</span></span>

<span data-ttu-id="e90b1-111">Voor het configureren van Azure AD-integratie met Picturepark, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="e90b1-111">To configure Azure AD integration with Picturepark, you need the following items:</span></span>

- <span data-ttu-id="e90b1-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="e90b1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e90b1-113">Een Picturepark eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="e90b1-113">A Picturepark single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e90b1-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="e90b1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e90b1-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="e90b1-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e90b1-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="e90b1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e90b1-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e90b1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e90b1-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="e90b1-118">Scenario description</span></span>
<span data-ttu-id="e90b1-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="e90b1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e90b1-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="e90b1-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e90b1-121">Picturepark uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="e90b1-121">Adding Picturepark from the gallery</span></span>
2. <span data-ttu-id="e90b1-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="e90b1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-picturepark-from-the-gallery"></a><span data-ttu-id="e90b1-123">Picturepark uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="e90b1-123">Adding Picturepark from the gallery</span></span>
<span data-ttu-id="e90b1-124">Voor het configureren van de integratie van Picturepark in Azure AD, moet u Picturepark uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="e90b1-124">To configure the integration of Picturepark into Azure AD, you need to add Picturepark from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e90b1-125">**Als u wilt toevoegen Picturepark uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="e90b1-125">**To add Picturepark from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e90b1-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="e90b1-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e90b1-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="e90b1-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e90b1-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="e90b1-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="e90b1-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e90b1-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="e90b1-133">Typ in het zoekvak **Picturepark**.</span><span class="sxs-lookup"><span data-stu-id="e90b1-133">In the search box, type **Picturepark**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_search.png)

5. <span data-ttu-id="e90b1-135">Selecteer in het deelvenster resultaten **Picturepark**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="e90b1-135">In the results panel, select **Picturepark**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e90b1-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="e90b1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e90b1-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Picturepark op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="e90b1-138">In this section, you configure and test Azure AD single sign-on with Picturepark based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e90b1-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Picturepark is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e90b1-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Picturepark is to a user in Azure AD.</span></span> <span data-ttu-id="e90b1-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Picturepark tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="e90b1-140">In other words, a link relationship between an Azure AD user and the related user in Picturepark needs to be established.</span></span>

<span data-ttu-id="e90b1-141">Wijs in Picturepark, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="e90b1-141">In Picturepark, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e90b1-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Picturepark, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="e90b1-142">To configure and test Azure AD single sign-on with Picturepark, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e90b1-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e90b1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e90b1-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e90b1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e90b1-145">**[Maken van een testgebruiker Picturepark](#creating-a-picturepark-test-user)**  - Picturepark die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="e90b1-145">**[Creating a Picturepark test user](#creating-a-picturepark-test-user)** - to have a counterpart of Britta Simon in Picturepark that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e90b1-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="e90b1-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e90b1-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="e90b1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e90b1-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="e90b1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e90b1-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Picturepark configureren.</span><span class="sxs-lookup"><span data-stu-id="e90b1-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Picturepark application.</span></span>

<span data-ttu-id="e90b1-150">**Voor het configureren van Azure AD eenmalige aanmelding met Picturepark, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="e90b1-150">**To configure Azure AD single sign-on with Picturepark, perform the following steps:**</span></span>

1. <span data-ttu-id="e90b1-151">In de Azure-portal op de **Picturepark** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="e90b1-151">In the Azure portal, on the **Picturepark** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="e90b1-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="e90b1-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_samlbase.png)

3. <span data-ttu-id="e90b1-155">Op de **Picturepark domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="e90b1-155">On the **Picturepark Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_url.png)

    <span data-ttu-id="e90b1-157">a.</span><span class="sxs-lookup"><span data-stu-id="e90b1-157">a.</span></span> <span data-ttu-id="e90b1-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<companyname>.picturepark.com`</span><span class="sxs-lookup"><span data-stu-id="e90b1-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.picturepark.com`</span></span>

    <span data-ttu-id="e90b1-159">b.</span><span class="sxs-lookup"><span data-stu-id="e90b1-159">b.</span></span> <span data-ttu-id="e90b1-160">In de **id** textbox, typ een URL met het volgende patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="e90b1-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span> 
    
    |  |
    |--|
    | `https://<companyname>.current-picturepark.com`|
    | `https://<companyname>.picturepark.com`|
    | `https://<companyname>.next-picturepark.com`|
    | |

    > [!NOTE] 
    > <span data-ttu-id="e90b1-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="e90b1-161">These values are not real.</span></span> <span data-ttu-id="e90b1-162">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="e90b1-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="e90b1-163">Neem contact op met [Picturepark Client ondersteuningsteam](https://picturepark.com/about/contact/) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="e90b1-163">Contact [Picturepark Client support team](https://picturepark.com/about/contact/) to get these values.</span></span> 
 
4. <span data-ttu-id="e90b1-164">Op de **SAML-certificaat voor ondertekening van** sectie, Kopieer de **VINGERAFDRUK** waarde van het certificaat.</span><span class="sxs-lookup"><span data-stu-id="e90b1-164">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_certificate.png) 

5. <span data-ttu-id="e90b1-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="e90b1-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-picturepark-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e90b1-168">Op de **Picturepark configuratie** sectie, klikt u op **configureren Picturepark** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="e90b1-168">On the **Picturepark Configuration** section, click **Configure Picturepark** to open **Configure sign-on** window.</span></span> <span data-ttu-id="e90b1-169">Kopieer de **SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="e90b1-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_configure.png) 

7. <span data-ttu-id="e90b1-171">In een ander browservenster, meld u bij uw bedrijf Picturepark site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="e90b1-171">In a different web browser window, log into your Picturepark company site as an administrator.</span></span>

8. <span data-ttu-id="e90b1-172">Klik in de werkbalk bovenaan op **Systeembeheer**, en klik vervolgens op **beheerconsole**.</span><span class="sxs-lookup"><span data-stu-id="e90b1-172">In the toolbar on the top, click **Administrative tools**, and then click **Management Console**.</span></span>
   
    <span data-ttu-id="e90b1-173">![Beheerconsole](./media/active-directory-saas-picturepark-tutorial/ic795062.png "-beheerconsole")</span><span class="sxs-lookup"><span data-stu-id="e90b1-173">![Management Console](./media/active-directory-saas-picturepark-tutorial/ic795062.png "Management Console")</span></span>

9. <span data-ttu-id="e90b1-174">Klik op **verificatie**, en klik vervolgens op **identiteitsproviders**.</span><span class="sxs-lookup"><span data-stu-id="e90b1-174">Click **Authentication**, and then click **Identity providers**.</span></span>
   
    <span data-ttu-id="e90b1-175">![Verificatie](./media/active-directory-saas-picturepark-tutorial/ic795063.png "verificatie")</span><span class="sxs-lookup"><span data-stu-id="e90b1-175">![Authentication](./media/active-directory-saas-picturepark-tutorial/ic795063.png "Authentication")</span></span>

10. <span data-ttu-id="e90b1-176">In de **identiteit providerconfiguratie** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="e90b1-176">In the **Identity provider configuration** section, perform the following steps:</span></span>
   
    <span data-ttu-id="e90b1-177">![Configuratie van de provider identiteit](./media/active-directory-saas-picturepark-tutorial/ic795064.png "providerconfiguratie identiteit")</span><span class="sxs-lookup"><span data-stu-id="e90b1-177">![Identity provider configuration](./media/active-directory-saas-picturepark-tutorial/ic795064.png "Identity provider configuration")</span></span>
   
    <span data-ttu-id="e90b1-178">a.</span><span class="sxs-lookup"><span data-stu-id="e90b1-178">a.</span></span> <span data-ttu-id="e90b1-179">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="e90b1-179">Click **Add**.</span></span>
  
    <span data-ttu-id="e90b1-180">b.</span><span class="sxs-lookup"><span data-stu-id="e90b1-180">b.</span></span> <span data-ttu-id="e90b1-181">Typ een naam voor uw configuratie.</span><span class="sxs-lookup"><span data-stu-id="e90b1-181">Type a name for your configuration.</span></span>
   
    <span data-ttu-id="e90b1-182">c.</span><span class="sxs-lookup"><span data-stu-id="e90b1-182">c.</span></span> <span data-ttu-id="e90b1-183">Selecteer **ingesteld als standaard**.</span><span class="sxs-lookup"><span data-stu-id="e90b1-183">Select **Set as default**.</span></span>
   
    <span data-ttu-id="e90b1-184">d.</span><span class="sxs-lookup"><span data-stu-id="e90b1-184">d.</span></span> <span data-ttu-id="e90b1-185">In **verlener URI** textbox, plak de waarde van **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="e90b1-185">In **Issuer URI** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="e90b1-186">e.</span><span class="sxs-lookup"><span data-stu-id="e90b1-186">e.</span></span> <span data-ttu-id="e90b1-187">In **vertrouwde verlener miniatuur afdrukken** textbox, plak de waarde van **vingerafdruk** die u hebt gekopieerd uit **certificaat voor ondertekening van SAML** sectie.</span><span class="sxs-lookup"><span data-stu-id="e90b1-187">In **Trusted Issuer Thumb Print** textbox, paste the value of **Thumbprint** which you have copied from **SAML Signing Certificate** section.</span></span> 

11. <span data-ttu-id="e90b1-188">Klik op **JoinDefaultUsersGroup**.</span><span class="sxs-lookup"><span data-stu-id="e90b1-188">Click **JoinDefaultUsersGroup**.</span></span>

12. <span data-ttu-id="e90b1-189">Om in te stellen de **Emailaddress** kenmerk in de **Claim** textbox type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` en klik op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="e90b1-189">To set the **Emailaddress** attribute in the **Claim** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` and click **Save**.</span></span>

      <span data-ttu-id="e90b1-190">![Configuratie](./media/active-directory-saas-picturepark-tutorial/ic795065.png "configuratie")</span><span class="sxs-lookup"><span data-stu-id="e90b1-190">![Configuration](./media/active-directory-saas-picturepark-tutorial/ic795065.png "Configuration")</span></span>

> [!TIP]
> <span data-ttu-id="e90b1-191">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="e90b1-191">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e90b1-192">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="e90b1-192">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e90b1-193">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e90b1-193">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e90b1-194">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="e90b1-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="e90b1-195">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="e90b1-195">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="e90b1-197">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="e90b1-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e90b1-198">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="e90b1-198">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-picturepark-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e90b1-200">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="e90b1-200">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-picturepark-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e90b1-202">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e90b1-202">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-picturepark-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e90b1-204">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="e90b1-204">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-picturepark-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e90b1-206">a.</span><span class="sxs-lookup"><span data-stu-id="e90b1-206">a.</span></span> <span data-ttu-id="e90b1-207">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e90b1-207">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e90b1-208">b.</span><span class="sxs-lookup"><span data-stu-id="e90b1-208">b.</span></span> <span data-ttu-id="e90b1-209">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e90b1-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e90b1-210">c.</span><span class="sxs-lookup"><span data-stu-id="e90b1-210">c.</span></span> <span data-ttu-id="e90b1-211">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="e90b1-211">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e90b1-212">d.</span><span class="sxs-lookup"><span data-stu-id="e90b1-212">d.</span></span> <span data-ttu-id="e90b1-213">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="e90b1-213">Click **Create**.</span></span>
 
### <a name="creating-a-picturepark-test-user"></a><span data-ttu-id="e90b1-214">Een testgebruiker Picturepark maken</span><span class="sxs-lookup"><span data-stu-id="e90b1-214">Creating a Picturepark test user</span></span>

<span data-ttu-id="e90b1-215">Om in te schakelen gebruikers van Azure AD aan te melden bij Picturepark, moeten ze worden ingericht in Picturepark.</span><span class="sxs-lookup"><span data-stu-id="e90b1-215">In order to enable Azure AD users to log into Picturepark, they must be provisioned into Picturepark.</span></span> <span data-ttu-id="e90b1-216">In het geval van Picturepark is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="e90b1-216">In the case of Picturepark, provisioning is a manual task.</span></span>

<span data-ttu-id="e90b1-217">**Voor het inrichten van een gebruikersaccount, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="e90b1-217">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="e90b1-218">Meld u aan bij uw **Picturepark** tenant.</span><span class="sxs-lookup"><span data-stu-id="e90b1-218">Log in to your **Picturepark** tenant.</span></span>

2. <span data-ttu-id="e90b1-219">Klik in de werkbalk bovenaan op **Systeembeheer**, en klik vervolgens op **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="e90b1-219">In the toolbar on the top, click **Administrative tools**, and then click **Users**.</span></span>
   
    <span data-ttu-id="e90b1-220">![Gebruikers](./media/active-directory-saas-picturepark-tutorial/ic795067.png "gebruikers")</span><span class="sxs-lookup"><span data-stu-id="e90b1-220">![Users](./media/active-directory-saas-picturepark-tutorial/ic795067.png "Users")</span></span>

3. <span data-ttu-id="e90b1-221">In de **overzicht van gebruikers** tabblad **nieuw**.</span><span class="sxs-lookup"><span data-stu-id="e90b1-221">In the **Users overview** tab, click **New**.</span></span>
   
    <span data-ttu-id="e90b1-222">![Gebruikersbeheer](./media/active-directory-saas-picturepark-tutorial/ic795068.png "Gebruikersbeheer")</span><span class="sxs-lookup"><span data-stu-id="e90b1-222">![User management](./media/active-directory-saas-picturepark-tutorial/ic795068.png "User management")</span></span>

4. <span data-ttu-id="e90b1-223">Op de **gebruiker maken** dialoogvenster de volgende stappen uit een geldige Azure Active Directory-gebruiker u wilt inrichten:</span><span class="sxs-lookup"><span data-stu-id="e90b1-223">On the **Create User** dialog, perform the following steps of a valid Azure Active Directory User you want to provision:</span></span>
   
    <span data-ttu-id="e90b1-224">![Gebruiker maken](./media/active-directory-saas-picturepark-tutorial/ic795069.png "gebruiker maken")</span><span class="sxs-lookup"><span data-stu-id="e90b1-224">![Create User](./media/active-directory-saas-picturepark-tutorial/ic795069.png "Create User")</span></span>
   
    <span data-ttu-id="e90b1-225">a.</span><span class="sxs-lookup"><span data-stu-id="e90b1-225">a.</span></span> <span data-ttu-id="e90b1-226">In de **e-mailadres** textbox type de **e-mailadres** van de gebruiker  **BrittaSimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="e90b1-226">In the **Email Address** textbox, type the **email address** of the user **BrittaSimon@contoso.com**.</span></span>  
   
    <span data-ttu-id="e90b1-227">b.</span><span class="sxs-lookup"><span data-stu-id="e90b1-227">b.</span></span> <span data-ttu-id="e90b1-228">In de **wachtwoord** en **wachtwoord bevestigen** tekstvakken, typ de **wachtwoord** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e90b1-228">In the **Password** and **Confirm Password** textboxes, type the **password** of BrittaSimon.</span></span> 
   
    <span data-ttu-id="e90b1-229">c.</span><span class="sxs-lookup"><span data-stu-id="e90b1-229">c.</span></span> <span data-ttu-id="e90b1-230">In de **voornaam** textbox type de **voornaam** van de gebruiker **Britta**.</span><span class="sxs-lookup"><span data-stu-id="e90b1-230">In the **First Name** textbox, type the **First Name** of the user **Britta**.</span></span> 
   
    <span data-ttu-id="e90b1-231">d.</span><span class="sxs-lookup"><span data-stu-id="e90b1-231">d.</span></span> <span data-ttu-id="e90b1-232">In de **achternaam** textbox type de **achternaam** van de gebruiker **Simon**.</span><span class="sxs-lookup"><span data-stu-id="e90b1-232">In the **Last Name** textbox, type the **Last Name** of the user **Simon**.</span></span>
   
    <span data-ttu-id="e90b1-233">e.</span><span class="sxs-lookup"><span data-stu-id="e90b1-233">e.</span></span> <span data-ttu-id="e90b1-234">In de **bedrijf** textbox type de **bedrijfsnaam** van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="e90b1-234">In the **Company** textbox, type the **Company name** of the user.</span></span> 
   
    <span data-ttu-id="e90b1-235">f.</span><span class="sxs-lookup"><span data-stu-id="e90b1-235">f.</span></span> <span data-ttu-id="e90b1-236">In de **land** textbox, selecteer de **land** van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="e90b1-236">In the **Country** textbox, select the **Country** of the user.</span></span>
  
    <span data-ttu-id="e90b1-237">g.</span><span class="sxs-lookup"><span data-stu-id="e90b1-237">g.</span></span> <span data-ttu-id="e90b1-238">In de **ZIP** textbox type de **postcode** van de plaats.</span><span class="sxs-lookup"><span data-stu-id="e90b1-238">In the **ZIP** textbox, type the **ZIP code** of the city.</span></span>
   
    <span data-ttu-id="e90b1-239">h.</span><span class="sxs-lookup"><span data-stu-id="e90b1-239">h.</span></span> <span data-ttu-id="e90b1-240">In de **stad** textbox type de **plaatsnaam** van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="e90b1-240">In the **City** textbox, type the **City name** of the user.</span></span>

    <span data-ttu-id="e90b1-241">ik.</span><span class="sxs-lookup"><span data-stu-id="e90b1-241">i.</span></span> <span data-ttu-id="e90b1-242">Selecteer een **taal**.</span><span class="sxs-lookup"><span data-stu-id="e90b1-242">Select a **Language**.</span></span>
   
    <span data-ttu-id="e90b1-243">j.</span><span class="sxs-lookup"><span data-stu-id="e90b1-243">j.</span></span> <span data-ttu-id="e90b1-244">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="e90b1-244">Click **Create**.</span></span>

>[!NOTE]
><span data-ttu-id="e90b1-245">U kunt andere Picturepark gebruiker account hulpmiddelen voor het maken of API's die is geleverd door Picturepark voor het inrichten van Azure AD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="e90b1-245">You can use any other Picturepark user account creation tools or APIs provided by Picturepark to provision Azure AD user accounts.</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e90b1-246">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="e90b1-246">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e90b1-247">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Picturepark.</span><span class="sxs-lookup"><span data-stu-id="e90b1-247">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Picturepark.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="e90b1-249">**Britta Simon om aan te wijzen Picturepark, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="e90b1-249">**To assign Britta Simon to Picturepark, perform the following steps:**</span></span>

1. <span data-ttu-id="e90b1-250">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="e90b1-250">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="e90b1-252">Selecteer in de lijst met toepassingen **Picturepark**.</span><span class="sxs-lookup"><span data-stu-id="e90b1-252">In the applications list, select **Picturepark**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_app.png) 

3. <span data-ttu-id="e90b1-254">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="e90b1-254">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="e90b1-256">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="e90b1-256">Click **Add** button.</span></span> <span data-ttu-id="e90b1-257">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e90b1-257">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="e90b1-259">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="e90b1-259">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e90b1-260">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e90b1-260">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e90b1-261">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e90b1-261">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e90b1-262">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="e90b1-262">Testing single sign-on</span></span>

<span data-ttu-id="e90b1-263">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="e90b1-263">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e90b1-264">Als u op de tegel Picturepark in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Picturepark.</span><span class="sxs-lookup"><span data-stu-id="e90b1-264">When you click the Picturepark tile in the Access Panel, you should get automatically signed-on to your Picturepark application.</span></span> <span data-ttu-id="e90b1-265">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e90b1-265">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e90b1-266">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="e90b1-266">Additional resources</span></span>

* [<span data-ttu-id="e90b1-267">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e90b1-267">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e90b1-268">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e90b1-268">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_203.png

