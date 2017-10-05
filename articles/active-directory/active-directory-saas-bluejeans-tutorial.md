---
title: 'Zelfstudie: Azure Active Directory-integratie met BlueJeans | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en BlueJeans.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dfc634fd-1b55-4ba8-94a8-b8288429b6a9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: jeedes
ms.openlocfilehash: 03bf65852b8d3cf14aebf155891a028db86e78d0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bluejeans"></a><span data-ttu-id="85666-103">Zelfstudie: Azure Active Directory-integratie met BlueJeans</span><span class="sxs-lookup"><span data-stu-id="85666-103">Tutorial: Azure Active Directory integration with BlueJeans</span></span>

<span data-ttu-id="85666-104">In deze zelfstudie leert u hoe BlueJeans integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="85666-104">In this tutorial, you learn how to integrate BlueJeans with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="85666-105">BlueJeans integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="85666-105">Integrating BlueJeans with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="85666-106">U kunt beheren in Azure AD die toegang tot BlueJeans heeft</span><span class="sxs-lookup"><span data-stu-id="85666-106">You can control in Azure AD who has access to BlueJeans</span></span>
- <span data-ttu-id="85666-107">U kunt uw gebruikers automatisch ophalen aangemeld bij BlueJeans (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="85666-107">You can enable your users to automatically get signed-on to BlueJeans (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="85666-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="85666-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="85666-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="85666-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="85666-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="85666-110">Prerequisites</span></span>

<span data-ttu-id="85666-111">Voor het configureren van Azure AD-integratie met BlueJeans, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="85666-111">To configure Azure AD integration with BlueJeans, you need the following items:</span></span>

- <span data-ttu-id="85666-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="85666-112">An Azure AD subscription</span></span>
- <span data-ttu-id="85666-113">Een BlueJeans eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="85666-113">A BlueJeans single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="85666-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="85666-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="85666-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="85666-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="85666-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="85666-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="85666-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="85666-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="85666-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="85666-118">Scenario description</span></span>
<span data-ttu-id="85666-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="85666-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="85666-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="85666-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="85666-121">BlueJeans uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="85666-121">Adding BlueJeans from the gallery</span></span>
2. <span data-ttu-id="85666-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="85666-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bluejeans-from-the-gallery"></a><span data-ttu-id="85666-123">BlueJeans uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="85666-123">Adding BlueJeans from the gallery</span></span>
<span data-ttu-id="85666-124">Voor het configureren van de integratie van BlueJeans in Azure AD, moet u BlueJeans uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="85666-124">To configure the integration of BlueJeans into Azure AD, you need to add BlueJeans from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="85666-125">**Als u wilt toevoegen BlueJeans uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="85666-125">**To add BlueJeans from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="85666-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="85666-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="85666-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="85666-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="85666-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="85666-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="85666-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="85666-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="85666-133">Typ in het zoekvak **BlueJeans**.</span><span class="sxs-lookup"><span data-stu-id="85666-133">In the search box, type **BlueJeans**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_search.png)

5. <span data-ttu-id="85666-135">Selecteer in het deelvenster resultaten **BlueJeans**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="85666-135">In the results panel, select **BlueJeans**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="85666-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="85666-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="85666-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met BlueJeans op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="85666-138">In this section, you configure and test Azure AD single sign-on with BlueJeans based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="85666-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in BlueJeans is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="85666-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BlueJeans is to a user in Azure AD.</span></span> <span data-ttu-id="85666-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in BlueJeans tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="85666-140">In other words, a link relationship between an Azure AD user and the related user in BlueJeans needs to be established.</span></span>

<span data-ttu-id="85666-141">Wijs in BlueJeans, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="85666-141">In BlueJeans, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="85666-142">Om te configureren en testen van Azure AD eenmalige aanmelding met BlueJeans, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="85666-142">To configure and test Azure AD single sign-on with BlueJeans, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="85666-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="85666-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="85666-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="85666-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="85666-145">**[Maken van een testgebruiker BlueJeans](#creating-a-bluejeans-test-user)**  - hebben een equivalent van Britta Simon in BlueJeans die is gekoppeld aan de Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="85666-145">**[Creating a BlueJeans test user](#creating-a-bluejeans-test-user)** - to have a counterpart of Britta Simon in BlueJeans that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="85666-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="85666-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="85666-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="85666-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="85666-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="85666-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="85666-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing BlueJeans configureren.</span><span class="sxs-lookup"><span data-stu-id="85666-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BlueJeans application.</span></span>

<span data-ttu-id="85666-150">**Voor het configureren van Azure AD eenmalige aanmelding met BlueJeans, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="85666-150">**To configure Azure AD single sign-on with BlueJeans, perform the following steps:**</span></span>

1. <span data-ttu-id="85666-151">In de Azure-portal op de **BlueJeans** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="85666-151">In the Azure portal, on the **BlueJeans** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="85666-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="85666-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_samlbase.png)

3. <span data-ttu-id="85666-155">Op de **BlueJeans domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="85666-155">On the **BlueJeans Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_url.png)

    <span data-ttu-id="85666-157">a.</span><span class="sxs-lookup"><span data-stu-id="85666-157">a.</span></span> <span data-ttu-id="85666-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<companyname>.BlueJeans.com`</span><span class="sxs-lookup"><span data-stu-id="85666-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.BlueJeans.com`</span></span>

    <span data-ttu-id="85666-159">b.</span><span class="sxs-lookup"><span data-stu-id="85666-159">b.</span></span> <span data-ttu-id="85666-160">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<companyname>.BlueJeans.com`</span><span class="sxs-lookup"><span data-stu-id="85666-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.BlueJeans.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="85666-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="85666-161">These values are not real.</span></span> <span data-ttu-id="85666-162">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="85666-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="85666-163">Neem contact op met [BlueJeans Client ondersteuningsteam](https://support.bluejeans.com/contact) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="85666-163">Contact [BlueJeans Client support team](https://support.bluejeans.com/contact) to get these values.</span></span> 
 
4. <span data-ttu-id="85666-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="85666-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_certificate.png) 

5. <span data-ttu-id="85666-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="85666-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bluejeans-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="85666-168">Op de **BlueJeans configuratie** sectie, klikt u op **configureren BlueJeans** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="85666-168">On the **BlueJeans Configuration** section, click **Configure BlueJeans** to open **Configure sign-on** window.</span></span> <span data-ttu-id="85666-169">Kopieer de **Sign-Out-URL, de URL van wijzigen wachtwoord en de SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="85666-169">Copy the **Sign-Out URL, Change Password URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_configure.png) 

7. <span data-ttu-id="85666-171">In een ander browservenster geopend, moet u zich aanmelden bij uw **BlueJeans** bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="85666-171">In a different web browser window, log in to your **BlueJeans** company site as an administrator.</span></span>

8. <span data-ttu-id="85666-172">Ga naar **ADMIN \> groepsinstellingen \> beveiliging**.</span><span class="sxs-lookup"><span data-stu-id="85666-172">Go to **ADMIN \> Group Settings \> Security**.</span></span>
   
   <span data-ttu-id="85666-173">![Beheerder](./media/active-directory-saas-bluejeans-tutorial/IC785868.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="85666-173">![Admin](./media/active-directory-saas-bluejeans-tutorial/IC785868.png "Admin")</span></span>

9. <span data-ttu-id="85666-174">In de **beveiliging** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="85666-174">In the **Security** section, perform the following steps:</span></span>
   
   <span data-ttu-id="85666-175">![SAML voor eenmalige aanmelding](./media/active-directory-saas-bluejeans-tutorial/IC785869.png "SAML voor eenmalige aanmelding")</span><span class="sxs-lookup"><span data-stu-id="85666-175">![SAML Single Sign On](./media/active-directory-saas-bluejeans-tutorial/IC785869.png "SAML Single Sign On")</span></span>   
   
   <span data-ttu-id="85666-176">a.</span><span class="sxs-lookup"><span data-stu-id="85666-176">a.</span></span> <span data-ttu-id="85666-177">Selecteer **SAML voor eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="85666-177">Select **SAML Single Sign On**.</span></span>
  
   <span data-ttu-id="85666-178">b.</span><span class="sxs-lookup"><span data-stu-id="85666-178">b.</span></span> <span data-ttu-id="85666-179">Selecteer **automatische inrichting inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="85666-179">Select **Enable automatic provisioning**.</span></span>

10. <span data-ttu-id="85666-180">Gaan met de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="85666-180">Move on with the following steps:</span></span>

    <span data-ttu-id="85666-181">![Pad van het certificaat](./media/active-directory-saas-bluejeans-tutorial/IC785870.png "pad van het certificaat")</span><span class="sxs-lookup"><span data-stu-id="85666-181">![Certificate Path](./media/active-directory-saas-bluejeans-tutorial/IC785870.png "Certificate Path")</span></span>
    
    <span data-ttu-id="85666-182">a.</span><span class="sxs-lookup"><span data-stu-id="85666-182">a.</span></span> <span data-ttu-id="85666-183">Klik op **bestand kiezen**, en vervolgens het gedownloade certificaat te uploaden.</span><span class="sxs-lookup"><span data-stu-id="85666-183">Click **Choose File**, and then upload the downloaded certificate.</span></span>
   
    <span data-ttu-id="85666-184">b.</span><span class="sxs-lookup"><span data-stu-id="85666-184">b.</span></span> <span data-ttu-id="85666-185">Plakken **SAML Single Sign-On Service-URL** in de **aanmeldings-URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="85666-185">Paste **SAML Single Sign-On Service URL** into the **Login URL** textbox.</span></span>
   
    <span data-ttu-id="85666-186">c.</span><span class="sxs-lookup"><span data-stu-id="85666-186">c.</span></span> <span data-ttu-id="85666-187">Plakken **URL van wijzigen wachtwoord** in de **URL voor wachtwoord wijzigen** textbox.</span><span class="sxs-lookup"><span data-stu-id="85666-187">Paste **Change Password URL** into the **Password Change URL** textbox.</span></span>
   
    <span data-ttu-id="85666-188">d.</span><span class="sxs-lookup"><span data-stu-id="85666-188">d.</span></span> <span data-ttu-id="85666-189">Plakken **Sign-Out URL** in de **afmelding URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="85666-189">Paste **Sign-Out URL** into the **Logout URL** textbox.</span></span>

11. <span data-ttu-id="85666-190">Gaan met de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="85666-190">Move on with the following steps:</span></span>
    
    <span data-ttu-id="85666-191">![Wijzigingen opslaan](./media/active-directory-saas-bluejeans-tutorial/IC785874.png "wijzigingen opslaan")</span><span class="sxs-lookup"><span data-stu-id="85666-191">![Save Changes](./media/active-directory-saas-bluejeans-tutorial/IC785874.png "Save Changes")</span></span>
    
    <span data-ttu-id="85666-192">a.</span><span class="sxs-lookup"><span data-stu-id="85666-192">a.</span></span> <span data-ttu-id="85666-193">In de **gebruikers-id** textbox type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="85666-193">In the **User id** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
   
    <span data-ttu-id="85666-194">b.</span><span class="sxs-lookup"><span data-stu-id="85666-194">b.</span></span> <span data-ttu-id="85666-195">In de **e** textbox type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="85666-195">In the **Email** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
   
    <span data-ttu-id="85666-196">c.</span><span class="sxs-lookup"><span data-stu-id="85666-196">c.</span></span> <span data-ttu-id="85666-197">Klik op **wijzigingen opslaan**.</span><span class="sxs-lookup"><span data-stu-id="85666-197">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="85666-198">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="85666-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="85666-199">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="85666-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="85666-200">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="85666-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="85666-201">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="85666-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="85666-202">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="85666-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="85666-204">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="85666-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="85666-205">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="85666-205">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="85666-207">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="85666-207">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="85666-209">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="85666-209">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="85666-211">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="85666-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="85666-213">a.</span><span class="sxs-lookup"><span data-stu-id="85666-213">a.</span></span> <span data-ttu-id="85666-214">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="85666-214">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="85666-215">b.</span><span class="sxs-lookup"><span data-stu-id="85666-215">b.</span></span> <span data-ttu-id="85666-216">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="85666-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="85666-217">c.</span><span class="sxs-lookup"><span data-stu-id="85666-217">c.</span></span> <span data-ttu-id="85666-218">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="85666-218">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="85666-219">d.</span><span class="sxs-lookup"><span data-stu-id="85666-219">d.</span></span> <span data-ttu-id="85666-220">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="85666-220">Click **Create**.</span></span>
 
### <a name="creating-a-bluejeans-test-user"></a><span data-ttu-id="85666-221">Een testgebruiker BlueJeans maken</span><span class="sxs-lookup"><span data-stu-id="85666-221">Creating a BlueJeans test user</span></span>

<span data-ttu-id="85666-222">Om Azure AD-gebruikers zich aanmelden bij BlueJeans, moeten ze worden ingericht in BlueJeans.</span><span class="sxs-lookup"><span data-stu-id="85666-222">To enable Azure AD users to log in to BlueJeans, they must be provisioned into BlueJeans.</span></span>  

<span data-ttu-id="85666-223">In geval van een BlueJeans is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="85666-223">In case of BlueJeans, provisioning is a manual task.</span></span>

<span data-ttu-id="85666-224">**Voor het inrichten van een gebruikersaccount, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="85666-224">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="85666-225">Meld u aan bij uw **BlueJeans** bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="85666-225">Log in to your **BlueJeans** company site as an administrator.</span></span>

2. <span data-ttu-id="85666-226">Ga naar **ADMIN \> gebruikers beheren \> gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="85666-226">Go to **ADMIN \> Manage Users \> Add User**.</span></span>
   
   <span data-ttu-id="85666-227">![Beheerder](./media/active-directory-saas-bluejeans-tutorial/IC785877.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="85666-227">![Admin](./media/active-directory-saas-bluejeans-tutorial/IC785877.png "Admin")</span></span>
   
   >[!IMPORTANT]
   ><span data-ttu-id="85666-228">De **gebruiker toevoegen** tabblad is alleen beschikbaar als in de **tabblad Beveiliging**, **automatische inrichting inschakelen** is uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="85666-228">The **Add User** tab is only available if, in the **Security tab**, **Enable automatic provisioning** is unchecked.</span></span> 
   
3. <span data-ttu-id="85666-229">In de **gebruiker toevoegen** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="85666-229">In the **Add User** section, perform the following steps:</span></span>

    <span data-ttu-id="85666-230">![Gebruiker toevoegen](./media/active-directory-saas-bluejeans-tutorial/IC785886.png "gebruiker toevoegen")</span><span class="sxs-lookup"><span data-stu-id="85666-230">![Add User](./media/active-directory-saas-bluejeans-tutorial/IC785886.png "Add User")</span></span>
    
    <span data-ttu-id="85666-231">a.</span><span class="sxs-lookup"><span data-stu-id="85666-231">a.</span></span> <span data-ttu-id="85666-232">Typ een **BlueJeans gebruikersnaam**, een **e-mailadres**, een **BlueJeans vergadering ID**, een **beheerder wachtwoordcode**, een **volledige naam**, wordt de **bedrijf** van een geldige AAD-account dat u inrichten in de bijbehorende tekstvakken wilt.</span><span class="sxs-lookup"><span data-stu-id="85666-232">Type a **BlueJeans Username**, an **Email address**, a **BlueJeans Meeting ID**, a **Moderator Passcode**, a **Full Name**, the **Company** of a valid AAD account you want to provision into the related textboxes.</span></span>
    
    <span data-ttu-id="85666-233">b.</span><span class="sxs-lookup"><span data-stu-id="85666-233">b.</span></span> <span data-ttu-id="85666-234">Klik op **gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="85666-234">Click **Add User**.</span></span>

>[!NOTE]
><span data-ttu-id="85666-235">U kunt andere BlueJeans gebruiker account hulpmiddelen voor het maken of API's die is geleverd door BlueJeans aan inrichten AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="85666-235">You can use any other BlueJeans user account creation tools or APIs provided by BlueJeans to provision AAD user accounts.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="85666-236">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="85666-236">Assigning the Azure AD test user</span></span>

<span data-ttu-id="85666-237">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan BlueJeans.</span><span class="sxs-lookup"><span data-stu-id="85666-237">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BlueJeans.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="85666-239">**Britta Simon om aan te wijzen BlueJeans, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="85666-239">**To assign Britta Simon to BlueJeans, perform the following steps:**</span></span>

1. <span data-ttu-id="85666-240">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="85666-240">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="85666-242">Selecteer in de lijst met toepassingen **BlueJeans**.</span><span class="sxs-lookup"><span data-stu-id="85666-242">In the applications list, select **BlueJeans**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_app.png) 

3. <span data-ttu-id="85666-244">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="85666-244">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="85666-246">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="85666-246">Click **Add** button.</span></span> <span data-ttu-id="85666-247">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="85666-247">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="85666-249">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="85666-249">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="85666-250">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="85666-250">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="85666-251">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="85666-251">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="85666-252">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="85666-252">Testing single sign-on</span></span>

<span data-ttu-id="85666-253">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="85666-253">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="85666-254">Als u op de tegel BlueJeans in het deelvenster toegang, krijgt u de aanmeldingspagina van BlueJeans toepassing.</span><span class="sxs-lookup"><span data-stu-id="85666-254">When you click the BlueJeans tile in the Access Panel, you should get login page of BlueJeans application.</span></span>
<span data-ttu-id="85666-255">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="85666-255">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="85666-256">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="85666-256">Additional resources</span></span>

* [<span data-ttu-id="85666-257">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="85666-257">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="85666-258">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="85666-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_203.png

