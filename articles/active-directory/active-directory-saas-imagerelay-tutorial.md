---
title: 'Zelfstudie: Azure Active Directory-integratie met installatiekopie Relay | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en afbeelding Relay.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 65bb5990-07ef-4244-9f41-cd28fc2cb5a2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 0bfbbaee7a74df6508584b7c8846fd07c2dc15c9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-image-relay"></a><span data-ttu-id="89f04-103">Zelfstudie: Azure Active Directory-integratie met installatiekopie Relay</span><span class="sxs-lookup"><span data-stu-id="89f04-103">Tutorial: Azure Active Directory integration with Image Relay</span></span>

<span data-ttu-id="89f04-104">In deze zelfstudie leert u hoe installatiekopie Relay integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="89f04-104">In this tutorial, you learn how to integrate Image Relay with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="89f04-105">Afbeelding Relay integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="89f04-105">Integrating Image Relay with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="89f04-106">U kunt beheren in Azure AD die toegang tot de installatiekopie Relay heeft</span><span class="sxs-lookup"><span data-stu-id="89f04-106">You can control in Azure AD who has access to Image Relay</span></span>
- <span data-ttu-id="89f04-107">U kunt uw gebruikers automatisch ophalen aangemeld bij de Relay-installatiekopie (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="89f04-107">You can enable your users to automatically get signed-on to Image Relay (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="89f04-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="89f04-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="89f04-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="89f04-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="89f04-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="89f04-110">Prerequisites</span></span>

<span data-ttu-id="89f04-111">Voor het configureren van Azure AD-integratie met installatiekopie Relay, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="89f04-111">To configure Azure AD integration with Image Relay, you need the following items:</span></span>

- <span data-ttu-id="89f04-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="89f04-112">An Azure AD subscription</span></span>
- <span data-ttu-id="89f04-113">Een installatiekopie Relay eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="89f04-113">An Image Relay single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="89f04-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="89f04-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="89f04-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="89f04-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="89f04-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="89f04-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="89f04-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="89f04-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="89f04-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="89f04-118">Scenario description</span></span>
<span data-ttu-id="89f04-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="89f04-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="89f04-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="89f04-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="89f04-121">Relay-installatiekopie uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="89f04-121">Adding Image Relay from the gallery</span></span>
2. <span data-ttu-id="89f04-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="89f04-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-image-relay-from-the-gallery"></a><span data-ttu-id="89f04-123">Relay-installatiekopie uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="89f04-123">Adding Image Relay from the gallery</span></span>
<span data-ttu-id="89f04-124">Voor het configureren van de integratie van afbeelding Relay in Azure AD, moet u de installatiekopie Relay uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="89f04-124">To configure the integration of Image Relay into Azure AD, you need to add Image Relay from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="89f04-125">**Als u wilt toevoegen Relay-installatiekopie uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="89f04-125">**To add Image Relay from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="89f04-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="89f04-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="89f04-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="89f04-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="89f04-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="89f04-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="89f04-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="89f04-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="89f04-133">Typ in het zoekvak **installatiekopie Relay**.</span><span class="sxs-lookup"><span data-stu-id="89f04-133">In the search box, type **Image Relay**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_search.png)

5. <span data-ttu-id="89f04-135">Selecteer in het deelvenster resultaten **installatiekopie Relay**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="89f04-135">In the results panel, select **Image Relay**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="89f04-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="89f04-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="89f04-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met installatiekopie Relay op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="89f04-138">In this section, you configure and test Azure AD single sign-on with Image Relay based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="89f04-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in afbeelding Relay in Azure AD voor een gebruiker is.</span><span class="sxs-lookup"><span data-stu-id="89f04-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Image Relay is to a user in Azure AD.</span></span> <span data-ttu-id="89f04-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in de afbeelding Relay tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="89f04-140">In other words, a link relationship between an Azure AD user and the related user in Image Relay needs to be established.</span></span>

<span data-ttu-id="89f04-141">In afbeelding Relay, wijs de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="89f04-141">In Image Relay, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="89f04-142">Om te configureren en testen van Azure AD eenmalige aanmelding met installatiekopie Relay, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="89f04-142">To configure and test Azure AD single sign-on with Image Relay, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="89f04-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="89f04-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="89f04-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="89f04-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="89f04-145">**[Maken van een installatiekopie Relay testgebruiker](#creating-an-image-relay-test-user)**  - installatiekopie Relay die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="89f04-145">**[Creating an Image Relay test user](#creating-an-image-relay-test-user)** - to have a counterpart of Britta Simon in Image Relay that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="89f04-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="89f04-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="89f04-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="89f04-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="89f04-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="89f04-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="89f04-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw installatiekopie Relay-toepassing.</span><span class="sxs-lookup"><span data-stu-id="89f04-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Image Relay application.</span></span>

<span data-ttu-id="89f04-150">**Voor het configureren van Azure AD eenmalige aanmelding met installatiekopie Relay, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="89f04-150">**To configure Azure AD single sign-on with Image Relay, perform the following steps:**</span></span>

1. <span data-ttu-id="89f04-151">In de Azure-portal op de **installatiekopie Relay** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="89f04-151">In the Azure portal, on the **Image Relay** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="89f04-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="89f04-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_samlbase.png)

3. <span data-ttu-id="89f04-155">Op de **installatiekopie Relay domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="89f04-155">On the **Image Relay Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_url.png)

    <span data-ttu-id="89f04-157">a.</span><span class="sxs-lookup"><span data-stu-id="89f04-157">a.</span></span> <span data-ttu-id="89f04-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<companyname>.imagerelay.com/`</span><span class="sxs-lookup"><span data-stu-id="89f04-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.imagerelay.com/`</span></span>

    <span data-ttu-id="89f04-159">b.</span><span class="sxs-lookup"><span data-stu-id="89f04-159">b.</span></span> <span data-ttu-id="89f04-160">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<companyname>.imagerelay.com/sso/metadata`</span><span class="sxs-lookup"><span data-stu-id="89f04-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.imagerelay.com/sso/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="89f04-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="89f04-161">These values are not real.</span></span> <span data-ttu-id="89f04-162">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="89f04-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="89f04-163">Neem contact op met [installatiekopie Relay Client ondersteuningsteam](http://support.imagerelay.com/) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="89f04-163">Contact [Image Relay Client support team](http://support.imagerelay.com/) to get these values.</span></span> 
 


4. <span data-ttu-id="89f04-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="89f04-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_certificate.png) 

5. <span data-ttu-id="89f04-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="89f04-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-imagerelay-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="89f04-168">Op de **Image Relay-configuratie** sectie, klikt u op **installatiekopie Relay configureren** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="89f04-168">On the **Image Relay Configuration** section, click **Configure Image Relay** to open **Configure sign-on** window.</span></span> <span data-ttu-id="89f04-169">Kopieer de **Sign-Out Service-URL en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="89f04-169">Copy the **Sign-Out Service URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_configure.png) 

7. <span data-ttu-id="89f04-171">In een ander browservenster aanmelden bij uw bedrijf installatiekopie Relay site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="89f04-171">In another browser window, sign in to your Image Relay company site as an administrator.</span></span>

8. <span data-ttu-id="89f04-172">Klik in de werkbalk bovenaan op de **gebruikers en machtigingen** werkbelasting.</span><span class="sxs-lookup"><span data-stu-id="89f04-172">In the toolbar on the top, click the **Users & Permissions** workload.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_06.png) 

9. <span data-ttu-id="89f04-174">Klik op **maken van nieuwe machtiging**.</span><span class="sxs-lookup"><span data-stu-id="89f04-174">Click **Create New Permission**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_08.png)

10. <span data-ttu-id="89f04-176">In de **eenmalige aanmelding op instellingen** werkbelasting, selecteer de **deze groep kan alleen aanmelden via eenmalige aanmelding** selectievakje en klik vervolgens op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="89f04-176">In the **Single Sign On Settings** workload, select the **This Group can only sign-in via Single Sign On** check box, and then click **Save**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_09.png) 

11. <span data-ttu-id="89f04-178">Ga naar **Accountinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="89f04-178">Go to **Account Settings**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_10.png) 

12. <span data-ttu-id="89f04-180">Ga naar de **eenmalige aanmelding op instellingen** werkbelasting.</span><span class="sxs-lookup"><span data-stu-id="89f04-180">Go to the **Single Sign On Settings** workload.</span></span>
    
     ![Eenmalige aanmelding configureren](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_11.png)

13. <span data-ttu-id="89f04-182">Op de **SAML instellingen** dialoogvenster de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="89f04-182">On the **SAML Settings** dialog, perform the following steps:</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_12.png)
    
    <span data-ttu-id="89f04-184">a.</span><span class="sxs-lookup"><span data-stu-id="89f04-184">a.</span></span> <span data-ttu-id="89f04-185">In **aanmeldings-URL** textbox, plak de waarde van **Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="89f04-185">In **Login URL** textbox, paste the value of **Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="89f04-186">b.</span><span class="sxs-lookup"><span data-stu-id="89f04-186">b.</span></span> <span data-ttu-id="89f04-187">In **afmelding URL** textbox, plak de waarde van **Service-URL met eenmalige Sign-Out** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="89f04-187">In **Logout URL**  textbox, paste the value of **Single Sign-Out Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="89f04-188">c.</span><span class="sxs-lookup"><span data-stu-id="89f04-188">c.</span></span> <span data-ttu-id="89f04-189">Als **indeling naam-Id**, selecteer **urn: oasis: namen: tc: SAML:1.1:nameid-indeling: emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="89f04-189">As **Name Id Format**, select **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="89f04-190">d.</span><span class="sxs-lookup"><span data-stu-id="89f04-190">d.</span></span> <span data-ttu-id="89f04-191">Als **Binding opties voor het aanvragen van de serviceprovider (installatiekopie-Relay)**, selecteer **POST Binding**.</span><span class="sxs-lookup"><span data-stu-id="89f04-191">As **Binding Options for Requests from the Service Provider (Image Relay)**, select **POST Binding**.</span></span>

    <span data-ttu-id="89f04-192">e.</span><span class="sxs-lookup"><span data-stu-id="89f04-192">e.</span></span> <span data-ttu-id="89f04-193">Onder **x.509-certificaat**, klikt u op **certificaat bijwerken**.</span><span class="sxs-lookup"><span data-stu-id="89f04-193">Under **x.509 Certificate**, click **Update Certificate**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_17.png)

    <span data-ttu-id="89f04-195">f.</span><span class="sxs-lookup"><span data-stu-id="89f04-195">f.</span></span> <span data-ttu-id="89f04-196">Het gedownloade certificaat openen in Kladblok, Kopieer de inhoud en plak deze in het tekstvak voor de x.509-certificaat.</span><span class="sxs-lookup"><span data-stu-id="89f04-196">Open the downloaded certificate in notepad, copy the content, and then paste it into the x.509 Certificate textbox.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_18.png)

    <span data-ttu-id="89f04-198">g.</span><span class="sxs-lookup"><span data-stu-id="89f04-198">g.</span></span> <span data-ttu-id="89f04-199">In **compileerprogramma gebruikersaanvragen** sectie, selecteer de **compileerprogramma gebruikersaanvragen inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="89f04-199">In **Just-In-Time User Provisioning** section, select the **Enable Just-In-Time User Provisioning**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_19.png)

    <span data-ttu-id="89f04-201">h.</span><span class="sxs-lookup"><span data-stu-id="89f04-201">h.</span></span> <span data-ttu-id="89f04-202">Selecteer de machtigingsgroep (bijvoorbeeld **SSO Basic**) die is toegestaan aanmelden alleen via eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="89f04-202">Select the permission group (for example, **SSO Basic**) which is allowed to sign in only through single sign-on.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_20.png)

    <span data-ttu-id="89f04-204">ik.</span><span class="sxs-lookup"><span data-stu-id="89f04-204">i.</span></span> <span data-ttu-id="89f04-205">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="89f04-205">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="89f04-206">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="89f04-206">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="89f04-207">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="89f04-207">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="89f04-208">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="89f04-208">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="89f04-209">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="89f04-209">Creating an Azure AD test user</span></span>
<span data-ttu-id="89f04-210">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="89f04-210">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="89f04-212">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="89f04-212">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="89f04-213">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="89f04-213">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="89f04-215">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="89f04-215">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="89f04-217">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="89f04-217">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="89f04-219">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="89f04-219">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="89f04-221">a.</span><span class="sxs-lookup"><span data-stu-id="89f04-221">a.</span></span> <span data-ttu-id="89f04-222">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="89f04-222">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="89f04-223">b.</span><span class="sxs-lookup"><span data-stu-id="89f04-223">b.</span></span> <span data-ttu-id="89f04-224">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="89f04-224">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="89f04-225">c.</span><span class="sxs-lookup"><span data-stu-id="89f04-225">c.</span></span> <span data-ttu-id="89f04-226">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="89f04-226">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="89f04-227">d.</span><span class="sxs-lookup"><span data-stu-id="89f04-227">d.</span></span> <span data-ttu-id="89f04-228">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="89f04-228">Click **Create**.</span></span>
 
### <a name="creating-an-image-relay-test-user"></a><span data-ttu-id="89f04-229">Maken van een installatiekopie Relay testgebruiker</span><span class="sxs-lookup"><span data-stu-id="89f04-229">Creating an Image Relay test user</span></span>

<span data-ttu-id="89f04-230">Het doel van deze sectie is het maken van een gebruiker Britta Simon aangeroepen in afbeelding Relay.</span><span class="sxs-lookup"><span data-stu-id="89f04-230">The objective of this section is to create a user called Britta Simon in Image Relay.</span></span>

<span data-ttu-id="89f04-231">**Voor het maken van een gebruiker Britta Simon aangeroepen in afbeelding Relay, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="89f04-231">**To create a user called Britta Simon in Image Relay, perform the following steps:**</span></span>

1. <span data-ttu-id="89f04-232">Aanmelding bij uw bedrijf installatiekopie Relay site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="89f04-232">Sign-on to your Image Relay company site as an administrator.</span></span>

2. <span data-ttu-id="89f04-233">Ga naar **gebruikers en machtigingen** en selecteer **SSO-gebruiker maken**.</span><span class="sxs-lookup"><span data-stu-id="89f04-233">Go to **Users & Permissions**     and select **Create SSO User**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_21.png) 

3. <span data-ttu-id="89f04-235">Voer de **e**, **voornaam**, **achternaam**, en **bedrijf** van de gebruiker die u wilt inrichten en de machtigingsgroep (voor selecteren bijvoorbeeld eenmalige aanmelding Basic) die is de groep die alleen via eenmalige aanmelding kunt aanmelden.</span><span class="sxs-lookup"><span data-stu-id="89f04-235">Enter the **Email**, **First Name**, **Last Name**, and **Company** of the user you want to provision and select the permission group (for example, SSO Basic) which is the group that can sign in only through single sign-on.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_22.png) 

4. <span data-ttu-id="89f04-237">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="89f04-237">Click **Create**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="89f04-238">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="89f04-238">Assigning the Azure AD test user</span></span>

<span data-ttu-id="89f04-239">In deze sectie maakt inschakelen u Britta Simon Azure eenmalige aanmelding gebruiken door het verlenen van toegang aan de installatiekopie Relay.</span><span class="sxs-lookup"><span data-stu-id="89f04-239">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Image Relay.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="89f04-241">**Britta Simon om aan te wijzen installatiekopie Relay, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="89f04-241">**To assign Britta Simon to Image Relay, perform the following steps:**</span></span>

1. <span data-ttu-id="89f04-242">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="89f04-242">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="89f04-244">Selecteer in de lijst met toepassingen **installatiekopie Relay**.</span><span class="sxs-lookup"><span data-stu-id="89f04-244">In the applications list, select **Image Relay**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_app.png) 

3. <span data-ttu-id="89f04-246">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="89f04-246">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="89f04-248">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="89f04-248">Click **Add** button.</span></span> <span data-ttu-id="89f04-249">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="89f04-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="89f04-251">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="89f04-251">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="89f04-252">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="89f04-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="89f04-253">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="89f04-253">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="89f04-254">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="89f04-254">Testing single sign-on</span></span>

<span data-ttu-id="89f04-255">Het doel van deze sectie is het testen van uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="89f04-255">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>    

<span data-ttu-id="89f04-256">Als u op de installatiekopie Relay-tegel in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw installatiekopie Relay-toepassing.</span><span class="sxs-lookup"><span data-stu-id="89f04-256">When you click the Image Relay tile in the Access Panel, you should get automatically signed-on to your Image Relay application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="89f04-257">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="89f04-257">Additional resources</span></span>

* [<span data-ttu-id="89f04-258">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="89f04-258">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="89f04-259">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="89f04-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_04.png


[100]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_203.png

